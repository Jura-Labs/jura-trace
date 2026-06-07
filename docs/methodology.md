# Jura Trace — C2PA Implementation and Forensic Methodology

*A two-page technical overview for journalists, funders, partners, and conformance assessors evaluating Jura Trace v1.0.*

*Last updated 2026-06-04 for v1.0 (target Monday 22 June 2026).*

## Summary

Jura Trace verifies and signs digital images using a local-first architecture that combines two layers: a C2PA Content Credentials implementation and a thirteen-detector forensic pipeline. Everything runs on the user's device. Source code is published under AGPL-3.0-or-later, which means every figure cited here is reproducible by reading the code at the references given.

Jura Trace is a Validator-Conformant C2PA application (recordId `019d8d83-ed1c-787c-920c-8fad67b55cbe`, spec version 2.2, conformant from 2026-05-06, publicly listed on the [C2PA Conforming Products List](https://spec.c2pa.org/conformance-explorer/) from 2026-05-31). It is the first AGPL-licensed Validator-Conformant desktop application on the CPL, the first UK validator, and the tenth globally.

## 1. C2PA implementation

### 1.1 Dual signing modes

Jura Trace signs content in two distinct, user-selectable modes that occupy different points on the trust-versus-control axis.

**Sovereign mode** generates a per-installation local Certificate Authority on first launch. Every asset the user signs in Sovereign mode is signed by a certificate this CA issued. This certificate is not on any public trust list. Verifiers see a "self-signed" or "unknown issuer" disclosure but the cryptographic chain is intact. Sovereign mode is the offline-first default: it makes no network calls, depends on no external infrastructure, and works on an air-gapped machine. The journalistic and human-rights documentation use cases that drove this design need verifiable provenance even when the operator does not want, or cannot achieve, listing on an industry trust list.

**Conformant mode** signs with a trust-listed certificate issued by a public CA. Verifiers on Adobe, Microsoft, Google, Truepic, and other trust-list participants will resolve the chain to a recognised issuer. Conformant mode is intended for organisations whose work is consumed by news desks, picture agencies, and content platforms that already participate in the C2PA ecosystem. It is feature-flagged off in v1.0.0 pending publisher onboarding and reactivated in v1.0.2 (October 2026).

The mode choice is exposed through a clear pre-seal disclosure that lists what gets embedded in the manifest, the TSA URL, the certificate SHA-256 fingerprint, the claim-generator string, and the chosen action (created or published). This addresses the C2PA UX Recommendations v1.4 requirement that signers understand what they are attesting.

### 1.2 Manifest spec compliance

Jura Trace produces C2PA manifests that pass the c2patool selfqa test for JPEG, PNG, TIFF, and WebP. Several spec corners require explicit attention:

- **Training and mining policy** is declared via `c2pa.training-mining` per spec §18.18, including a CC0-aware default for cultural-heritage public-domain assets. The earlier non-conformant `c2pa.rights` assertion has been removed.
- **Claim generator information** appears as a `claim_generator_info` array, with `softwareAgent` declared as a `ClaimGeneratorInfoMap` and `digitalSourceType` placed inside the action (not at manifest root).
- **Ingredient handling on re-sign** preserves `parentOf` so the provenance chain is not broken when a downstream operator re-signs an already-signed asset.
- **Action selection** offers `c2pa.created` (new work) versus `c2pa.published` (existing work being released) with UI radio controls and contextual hints for institutional edge cases.

### 1.3 Trust-list awareness and revocation

Verification consults the bundled Adobe / Microsoft / Google / Truepic trust list and reports the trust state honestly: trusted, untrusted, or self-signed, with the certificate's claimed identity rendered for the user. By default Jura Trace is fully offline; an optional **Enhanced mode** enables OCSP/CRL revocation checks and remote manifest fetching, which closes the §15.9 audit gap for organisations that need full conformance over correctness-only operation.

### 1.4 Progressive disclosure (L1 to L4)

The verify panel implements the four-level progressive disclosure model from the C2PA UX Recommendations v1.4: L1 seal pin, L2 provenance summary, L3 full manifest detail with action labels, L4 raw JUMBF box inspection. Manifest-chain display includes the >4-manifest collapse rule for assets with long histories.

## 2. Forensic methodology

### 2.1 The thirteen-detector pipeline

When trust is not provable by C2PA alone (no manifest, broken chain, or external user demand), Jura Trace falls back to a forensic pipeline of thirteen detectors. Ten run automatically; three are on-demand investigation tools that inform investigator judgement but do not contribute to the numeric trust score.

**Automatic (ten):** EXIF anomaly (including XMP AI-provenance detection and injection-detection sub-checks), C2PA, Error Level Analysis, noise analysis, copy-move detection, GBM deepfake classifier, UnivFD deepfake classifier (CLIP ViT-B/32-based), JPEG Ghost at 0.5× weight, segmented ELA, colour temperature, CLIP zero-shot AI detection.

**On-demand (three):** no-reference perceptual quality, shadow consistency, splice boundary.

Chromatic aberration was removed entirely (forensic audit graded it 1/5). The earlier diffusion-artefact detector was superseded by UnivFD v10onnx and removed.

### 2.2 Trust-score algorithm

The trust score is a five-component composite, anchored in code at `src-tauri/src/lib.rs::compute_trust`:

1. **Forensic primary**: 80% weight from the ten automatic detectors, calibrated against the training corpus.
2. **EXIF corroborating**: 20% weight, capped, drawn from EXIF anomaly + MakerNote authenticity + injection-detection sub-checks.
3. **C2PA adjustment**: positive contribution for trusted manifests, negative for broken chains, neutral for absent.
4. **Composite cap**: 0.55 ceiling on the EXIF+C2PA contribution to prevent metadata alone (which is forgeable) from carrying the verdict.
5. **Deepfake verdict ceiling**: a `deepfake_likely` verdict caps trust at 0.30 regardless of other signals.

The 20/80 split (reduced from 40/60 after a security audit) reflects the operational reality that metadata is the most forgeable layer in the stack. This is documented across the in-app methodology page, the Berkeley Protocol disclosure, the glossary, and the PDF trust report, with `src-tauri/src/lib.rs::compute_trust` cited as the AGPL-3.0 reproducibility anchor.

### 2.3 Model performance

Two production models drive the deepfake verdict:

- **GBM deepfake classifier v4**: 84-feature gradient-boosted-model trained on 10,709 images (5,724 authentic, 4,985 AI). AUC-ROC 0.9868, authentic false-positive rate 4.54%, AI recall 92.52%, decision threshold 0.49. SHA-256 `512def7ec62cbeb023c5343859a15606a02742d48b1fca31df11667c0b9ba14a`.
- **UnivFD probe v10onnx** (CLIP ViT-B/32 embeddings + logistic regression, ONNX-runtime-aligned training): 50,710 training samples spanning original JPEG + platform-forwarded re-saves (Q=75/85/2× to defend against platform compression) + multi-format augmentation (PNG, TIFF, WebP, HEIC). AUC-ROC 0.9929, false-positive rate 3.87%, recall 95.77%. Decision boundary: synthetic ≥ 0.60, authentic ≤ 0.35. SHA-256 `0534a9e80e352a5bd8af5fc447d03e37be2e1aa68a05d81f05736d6ef8956a86`. The "onnx" suffix denotes that the probe was retrained against the production sidecar's PIL + ONNX runtime feature path (rather than the open_clip + PyTorch path used during research) to eliminate a 0.996 mean-cosine-similarity divergence between training and deployment embeddings.

Composite false-positive rate across the ensemble after MakerNote authenticity bonus and known-vendor recognition: 3.87% on the held-out validation set. Full per-generator recall, per-format AUC, and the v9 → v10onnx migration record lives at `docs/calibration/univfd-v10onnx-divergence-fix.md` in the source tree.

### 2.4 Composite signal amplification and known limitations

When multiple detectors flag the same asset, the composite score elevates nonlinearly (specified per the algorithm in `compute_trust`). This is intended to surface the case where individual detector signals are weak but coherent across modalities.

Known limitations are documented openly: Jura Trace is not a deepfake-detector-of-record; the training corpus is JPEG-heavy and weaker on rare formats; flux_dev (88.9% recall) and sdxl_turbo (91.1% recall) are the weakest generator families; audio and video deepfake analysis are deferred to v1.0.1 (target Monday 4 August 2026, aligned with EU AI Act Article 50 binding).

## 3. Reproducibility and transparency

Every quantitative claim in this document is reproducible by reading the AGPL-3.0-licensed source at `codeberg.org/jura-labs/jura-trace` (public from 2026-06-22) or the mirror at `github.com/Jura-Labs/jura-archive`. This is the Berkeley Protocol §6 reproducibility commitment.

Specific anchors:

| Claim | Source anchor |
|---|---|
| Trust-score algorithm | `src-tauri/src/lib.rs::compute_trust` |
| GBM classifier model card | `docs/calibration/gbm-classifier-v4-model-card.md` |
| UnivFD probe model card | `docs/calibration/univfd-v10onnx-divergence-fix.md` |
| C2PA manifest schema | `src-tauri/src/c2pa.rs` |
| Trust-list embedding | `src-tauri/src/c2pa.rs::TRUSTED_ISSUERS` |
| Detector lineup persistence | `src-tauri/src/db.rs` schema v6 |

## 4. References

- C2PA specification 2.2: <https://spec.c2pa.org>
- C2PA Conforming Products List: <https://spec.c2pa.org/conformance-explorer/>
- C2PA UX Recommendations v1.4: <https://spec.c2pa.org/specifications/specifications/>
- Berkeley Protocol on Digital Open Source Investigations: <https://www.ohchr.org/en/publications/policy-and-methodological-publications/berkeley-protocol-digital-open-source>
- Content Authenticity Initiative (member from 2026-05-28): <https://contentauthenticity.org>

## 5. Contact

- **Press, partnership, commercial, licensing enquiries:** `hello@juralabs.org`
- **Security disclosure:** `security@juralabs.org`
- **General website:** <https://juralabs.org>

---

*Jura Labs is a UK Community Interest Company (Companies House 17117467), an asset-locked non-profit. Surplus from any commercial licensing is reinvested in mission delivery.*

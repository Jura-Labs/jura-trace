# Jura Trace — Downloads

Official downloads for **Jura Trace**, a local-first forensic media verification tool published by Jura Labs Community Interest Company (UK, Companies House 17117467).

[![Latest release](https://img.shields.io/github/v/release/Jura-Labs/jura-trace?include_prereleases&label=latest)](https://github.com/Jura-Labs/jura-trace/releases/latest)
[![Licence: AGPL-3.0-or-later](https://img.shields.io/badge/licence-AGPL--3.0--or--later-5A85B5)](LICENSE)
[![Website](https://img.shields.io/badge/website-juralabs.org-5A85B5)](https://juralabs.org)

> 📥 **The canonical download surface for current installers is [juralabs.org](https://juralabs.org).** The Releases page on this repository remains available as a stable mirror.

---


## What is Jura Trace?

Jura Trace examines images and documents and reports what it finds. Honestly, and without certainty where none exists. Everything runs on your device.

- **13 forensic detectors** in v1.0, covering Error Level Analysis, noise, copy-move, deepfake (GBM v4 plus UnivFD v10onnx ensemble), JPEG ghost, segmented ELA, colour temperature, CLIP zero-shot AI detection, perceptual fingerprinting, and EXIF anomaly with XMP AI-provenance detection. Three detectors (NPR, shadow consistency, splice boundary) are available on demand as investigation tools.
- **C2PA Validator-Conformant** since 6 May 2026, publicly listed on the [C2PA Conforming Products List](https://spec.c2pa.org/conformance-explorer/) from 31 May 2026. Record identifier `019d8d83-ed1c-787c-920c-8fad67b55cbe`, spec version 2.2, image formats JPEG / PNG / TIFF / WebP. First AGPL-licensed Validator-Conformant desktop application on the public CPL; first UK validator. Full L1 to L4 progressive disclosure aligned with the C2PA UX Recommendations v1.4. Trust-list aware (Adobe, Microsoft, Google, Truepic and others).
- **Local-first.** No cloud, no accounts, no telemetry. An optional Enhanced mode permits OCSP/CRL revocation checks and remote manifest fetching for full C2PA conformance.
- **Cross-platform.** macOS (Apple Silicon) and Windows (x64) are shipping. Linux is paused for v1.0.

## Download

The canonical download surface is **[juralabs.org](https://juralabs.org)**. For specific historical builds you can also browse the [Releases](https://github.com/Jura-Labs/jura-trace/releases) page on this repository.

| Platform | Installer | Signing |
|---|---|---|
| **macOS** (Apple Silicon) | `Jura.Trace_0.9.0_aarch64.dmg` | Apple Developer ID, Jura Labs CIC (notarised) |
| **Windows** (x64) | `Jura.Trace_0.9.0_x64_en-US.msi` (recommended) <br> `Jura.Trace_0.9.0_x64-setup.exe` (NSIS) | Azure Trusted Signing |
| Linux | paused for v1.0 | — |

Step-by-step install and first-verification walkthrough: **[GETTING_STARTED.md](GETTING_STARTED.md)**.

## v1.0 public release: Monday 22 June 2026

Jura Trace v1.0 is in launch preparation. The public release lands on **Monday 22 June 2026**, with v0.9.0-rc builds available now for testing.

## For journalists, funders, and partners

If you are evaluating Jura Trace for editorial coverage, a funding decision, or a partnership conversation, the following resources are the right starting points.

**Read the methodology before you write.** A two-page technical overview of the C2PA implementation (dual signing modes, trust-list awareness, manifest spec compliance) and the forensic methodology (thirteen detectors, trust-score algorithm, model performance, known limitations) is published at **[docs/methodology.md](docs/methodology.md)**. Every quantitative claim is anchored to a specific file in the source tree, reproducible under the AGPL.

**Verifiable conformance status.** Validator-Conformant on the public [C2PA Conforming Products List](https://spec.c2pa.org/conformance-explorer/) since 2026-05-31. Record identifier `019d8d83-ed1c-787c-920c-8fad67b55cbe`, spec version 2.2, JPEG / PNG / TIFF / WebP. First AGPL-licensed Validator-Conformant desktop application, first UK validator, tenth globally. Content Authenticity Initiative member from 2026-05-28.

**Press contact.** Email `hello@juralabs.org`. Direct contact with the founder Paul Griffiths is available for technical or editorial briefings on request. Press kit (logos, screenshots, founder headshot, embedded preview video) is published at juralabs.org/press from 15 June 2026.

**Wider documentation.** A public wiki mirror of the in-app help is published at [codeberg.org/jura-labs/jura-trace/wiki](https://codeberg.org/jura-labs/jura-trace/wiki) from 2026-06-22 (coincident with the v1.0 public release). It includes the full Methodology page, Format Support matrix, and Glossary.

**Try it.** Installers in the [Releases](https://github.com/Jura-Labs/jura-trace/releases) tab on this repository are signed (Apple Developer ID for macOS, Azure Trusted Signing for Windows) and run without further setup. Verification works fully offline.

## Licence

**AGPL-3.0-or-later.** Free and open-source for anyone, including commercial use that complies with the AGPL's network-use clause and copyleft terms. See [`LICENSE`](LICENSE) for the full text.

The project switched to AGPL-3.0-or-later on 2026-05-06. Earlier releases were published under PolyForm Noncommercial 1.0.0; rc.21 onwards are AGPL-3.0-or-later.

A commercial licence is available for use cases that cannot operate under the AGPL (for example, integration into closed-source products, internal modified deployments, or cases requiring contractual indemnification). Contact `licensing@juralabs.org`.

## Source code

Source code for Jura Trace will be published on Codeberg at **[codeberg.org/jura-labs/jura-trace](https://codeberg.org/jura-labs/jura-trace)** from **Monday 22 June 2026**, coincident with the v1.0 public release.

Before that date the source remains in a private development repository; the signed installers in this repository are the only public artefacts. After 22 June the public source mirror on Codeberg is the authoritative read-only home for the AGPL source tree. This GitHub repository is retained for installer distribution and the auto-updater endpoint.

GitHub auto-generates `Source code (zip/tar.gz)` archives for every release. **Those archives are empty placeholders.** They do not contain the Jura Trace source. Use the platform installers for the application itself, and (from 22 June 2026) the Codeberg mirror for the source.

## On the use of Generative AI in this codebase

Jura Trace is developed by a sole maintainer (Paul Griffiths),  Anthropic Claude has been used as a coding and documentation assistant, structured around the guidelines below: 

**Architecture and design decisions are human-led.** Architectural choices (the four-layer Tauri / Rust / Python sidecar / SvelteKit structure, the Sovereign vs Conformant signing-mode split, the trust-score weighting, the local-first guarantee, the detector lineup, the licence and CIC framing) are made by the developer. 

**Tests are managed by the maintaner.** The Rust library tests, Rust API integration tests, Python sidecar tests, Playwright end-to-end tests, and Vitest component tests are authored and reviewed by the developer. AI is not used for test sign-off, coverage decisions, or detector threshold setting.

**Sources are human-verified.** Calibration figures, per-generator recall tables, vendor specification references, trust-list certificate fingerprints, conformance-programme record identifiers, and academic citations are checked against primary sources by the maintainer. 

**Code generation is AI-assisted, human-reviewed.** Boilerplate, error-handling patterns, accessibility fixes, and refactoring are sometimes drafted with AI assistance and then reviewed, edited, and integrated by the maintainer. Generated code is treated as a draft. Nothing reaches `main` without human review.

**Documentation is AI-assisted, human-edited.** README sections, in-source comments, user-facing guides, and changelog entries frequently begin as AI drafts and are edited for accuracy by the maintainer.

**Security-sensitive code** (signing, key handling, network boundaries, file-system access, IPC permissions, certificate handling, trust evaluation) receives explicit human review regardless of how it was drafted.

**Forensic verdicts** (the runtime detection output users see) are produced by the deployed detectors; the final conclusion, scoring, forensic detectors are not aided by AI. 


## About

- **Developer:** [Jura Labs Community Interest Company](https://juralabs.org) (UK, Companies House 17117467).
- **Licence:** [AGPL-3.0-or-later](LICENSE).
- **Source code:** publishing 2026-06-22 on [Codeberg](https://codeberg.org/jura-labs/jura-trace).
- **Security:** see [SECURITY.md](SECURITY.md) for vulnerability disclosure.
- **Commercial licensing:** `hello@juralabs.org`.

Copyright © 2025-2026 Paul Griffiths, published by Jura Labs CIC under perpetual royalty-free licence.

# Jura Trace — Downloads

Official downloads for **Jura Trace**, a local-first forensic media verification tool published by Jura Labs Community Interest Company (UK, Companies House 17117467).

[![Latest release](https://img.shields.io/github/v/release/Jura-Labs/jura-trace?include_prereleases&label=latest)](https://github.com/Jura-Labs/jura-trace/releases/latest)
[![Licence: AGPL-3.0-or-later](https://img.shields.io/badge/licence-AGPL--3.0--or--later-5A85B5)](LICENSE)
[![C2PA Validator-Conformant](https://img.shields.io/badge/C2PA-Validator--Conformant-5A85B5)](https://spec.c2pa.org/conformance-explorer/)
[![CAI Member](https://img.shields.io/badge/CAI-Member-5B8A5F)](https://contentauthenticity.org)
[![Website](https://img.shields.io/badge/website-juralabs.org-5A85B5)](https://juralabs.org)

> 📥 **The canonical download surface for current installers is [juralabs.org](https://juralabs.org).** The Releases page on this repository remains available as a stable mirror.

**Documentation**: read the [Methodology overview](docs/methodology.md) (two-page C2PA + forensic algorithm) before evaluating, citing, or writing about Jura Trace. Public wiki: [github.com/Jura-Labs/jura-trace/wiki](https://github.com/Jura-Labs/jura-trace/wiki).

---


## What is Jura Trace?

Jura Trace examines images and reports what it finds. Honestly, and without certainty where none exists. Everything runs on your device.

- **12 forensic detectors**, covering Error Level Analysis, noise, copy-move, deepfake (GBM v4 plus UnivFD v10onnx ensemble), JPEG ghost, segmented ELA, colour temperature, CLIP zero-shot AI detection, and EXIF anomaly with XMP AI-provenance detection. Nine run automatically; three (NPR, shadow consistency, splice boundary) are on-demand investigation tools. C2PA provenance reading is counted separately, as reading a manifest is not forensics.
- **C2PA Validator-Conformant** since 6 May 2026, publicly listed on the [C2PA Conforming Products List](https://spec.c2pa.org/conformance-explorer/) from 31 May 2026. Record identifier `019d8d83-ed1c-787c-920c-8fad67b55cbe`, spec version 2.2, image formats JPEG / PNG / TIFF / WebP. The first UK validator on that list, and the only Community Interest Company on it. Full L1 to L4 progressive disclosure aligned with the C2PA UX Recommendations v1.4. Trust-list aware (Adobe, Microsoft, Google, Truepic and others).
- **Local-first.** No cloud, no accounts, no telemetry. An optional Enhanced mode fetches remote manifests. Revocation checking is not implemented: the mode is a hook for it, and c2pa-rs 0.90 does not yet expose OCSP or CRL at the API level.
- **Cross-platform.** macOS (Apple Silicon), Windows (x64) and Linux (x86_64) are shipping.

## Download

The canonical download surface is **[juralabs.org](https://juralabs.org)**. For specific historical builds you can also browse the [Releases](https://github.com/Jura-Labs/jura-trace/releases) page on this repository.

| Platform | Installer | Signing |
|---|---|---|
| **macOS** (Apple Silicon) | `JuraTrace-<version>-macOS-AppleSilicon.dmg` | Apple Developer ID, Jura Labs CIC (notarised) |
| **Windows** (x64) | `JuraTrace-<version>-Windows-x64.msi` (recommended) <br> `JuraTrace-<version>-Windows-x64-setup.exe` (NSIS) | Azure Trusted Signing |
| **Linux** (x86_64) | `JuraTrace-<version>-Linux-x86_64.AppImage` <br> `JuraTrace-<version>-Linux-x86_64.deb` | Self-signed, AGPL source build |

Filenames carry the version of the release you are looking at, so take them
from the release page rather than typing them.

Step-by-step install and first-verification walkthrough: **[GETTING_STARTED.md](GETTING_STARTED.md)**.

## Releases

v1.1.0 was published on 10 September 2026 and is the current public release.
It repairs the automatic update path, which had never worked in v1.0.0. The
[Releases](https://github.com/Jura-Labs/jura-trace/releases) page on this
repository is the record of what has shipped.

## For journalists, funders, and partners

If you are evaluating Jura Trace for editorial coverage, a funding decision, or a partnership conversation, the following resources are the right starting points.

**Read the methodology before you write.** A two-page technical overview of the C2PA implementation (dual signing modes, trust-list awareness, manifest spec compliance) and the forensic methodology (twelve detectors, trust-score algorithm, model performance, known limitations) is published at **[docs/methodology.md](docs/methodology.md)**. Every quantitative claim is anchored to a specific file in the source tree, reproducible under the AGPL.

**Verifiable conformance status.** Validator-Conformant on the public [C2PA Conforming Products List](https://spec.c2pa.org/conformance-explorer/) since 2026-05-31. Record identifier `019d8d83-ed1c-787c-920c-8fad67b55cbe`, spec version 2.2, JPEG / PNG / TIFF / WebP. The first UK validator on that list, the only Community Interest Company on it, and the tenth validator worldwide by conformance date. Content Authenticity Initiative member from 2026-05-28.

**Press contact.** Email `hello@juralabs.org`. Direct contact with the founder Paul Griffiths is available for technical or editorial briefings on request. Press kit (logos, screenshots, founder headshot, embedded preview video) is published at juralabs.org/press from 15 June 2026.

**Wider documentation.** A public wiki mirror of the in-app help is live now at [github.com/Jura-Labs/jura-trace/wiki](https://github.com/Jura-Labs/jura-trace/wiki). From 2026-06-22 the same content is also published on Codeberg (`codeberg.org/jura-labs/jura-trace/wiki`, going live with the v1.0 public source release). Includes the full Methodology page, Format Support matrix, and Glossary.

**Try it.** Installers in the [Releases](https://github.com/Jura-Labs/jura-trace/releases) tab on this repository are signed (Apple Developer ID for macOS, Azure Trusted Signing for Windows) and run without further setup. Verification works fully offline.

## Licence

**AGPL-3.0-or-later.** Free and open-source for anyone, including commercial use that complies with the AGPL's network-use clause and copyleft terms. See [`LICENSE`](LICENSE) for the full text.

The project switched to AGPL-3.0-or-later on 2026-05-06. Earlier releases were published under PolyForm Noncommercial 1.0.0; rc.21 onwards are AGPL-3.0-or-later.

A commercial licence is available for use cases that cannot operate under the AGPL (for example, integration into closed-source products, internal modified deployments, or cases requiring contractual indemnification). Contact `licensing@juralabs.org`.

## Source code

The source is published at **[github.com/Jura-Labs/jura-trace-dev](https://github.com/Jura-Labs/jura-trace-dev)**, under AGPL-3.0-or-later, with development, issues and pull requests in the open there since 8 September 2026. That is the repository to read, build, cite or contribute to.

This repository holds the signed installers and the auto-updater endpoint only. GitHub auto-generates `Source code (zip/tar.gz)` archives for every release here; **those archives are empty placeholders** and do not contain the Jura Trace source.

The earlier public snapshot at codeberg.org/jura-labs/jura-trace is frozen at v1.0.0 (21 June 2026) and now points here. Jura Trace was first published on Codeberg because we support what Codeberg stands for; in July 2026 its members voted to discourage single-maintainer, AI-assisted projects with heavy build needs, which describes this one honestly, and Codeberg offers no macOS or Windows build runners.

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
- **Source code:** [github.com/Jura-Labs/jura-trace-dev](https://github.com/Jura-Labs/jura-trace-dev).
- **Security:** see [SECURITY.md](SECURITY.md) for vulnerability disclosure.
- **Commercial licensing:** `hello@juralabs.org`.

Copyright © 2025-2026 Paul Griffiths, published by Jura Labs CIC under perpetual royalty-free licence.

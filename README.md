# Jura Trace — Downloads

Official installer downloads for **Jura Trace**, a forensic media verification tool.

[![Latest release](https://img.shields.io/github/v/release/Jura-Labs/jura-trace?include_prereleases&label=latest)](https://github.com/Jura-Labs/jura-trace/releases/latest)
[![Licence: PolyForm NC 1.0.0](https://img.shields.io/badge/licence-PolyForm--NC--1.0.0-informational)](LICENSE)
[![Website](https://img.shields.io/badge/website-juralabs.org-5A85B5)](https://juralabs.org)

> 🚀 **First-time pilot tester?** Read the **[Getting Started guide](GETTING_STARTED.md)** — install + your first Content Credentials verification in 10 minutes.

**Download the latest version from the [Releases](https://github.com/Jura-Labs/jura-trace/releases) page.**

---

## What is Jura Trace?

Jura Trace examines images, videos and documents and tells you what it finds — honestly, and without certainty where none exists. It runs entirely on your device.

- **12 forensic detectors** — including ELA, noise, copy-move, deepfake (GBM + UnivFD ensemble), JPEG ghost, segmented ELA, colour temperature, CLIP, watermark, video deepfake, and EXIF anomaly with XMP AI-provenance.
- **C2PA Content Credentials** — full L1–L4 progressive disclosure aligned with the C2PA UX Recommendations v1.4. Trust-list-aware (Adobe, Microsoft, Google, Truepic, etc.).
- **Local-first** — no cloud, no accounts, no telemetry. Optional Enhanced mode allows OCSP/CRL revocation checks and remote manifest fetching for full C2PA conformance.
- **Cross-platform** — macOS (Apple Silicon), Windows (x64). Linux AppImage paused for v1.0.

## Install

| Platform | Installer | Signed |
|---|---|---|
| **macOS** (Apple Silicon) | `Jura.Trace_0.9.0_aarch64.dmg` | Apple Developer ID — Jura Labs CIC (notarised) |
| **Windows** (x64) | `Jura.Trace_0.9.0_x64_en-US.msi` (recommended) <br> `Jura.Trace_0.9.0_x64-setup.exe` (NSIS) | Azure Trusted Signing |
| Linux | (paused — re-enabling for v1.0) | — |

Step-by-step install + first-test walkthrough: **[GETTING_STARTED.md](GETTING_STARTED.md)**.

## About

- **Developer:** [Jura Labs Community Interest Company](https://juralabs.org) (UK CIC, Companies House 17117467)
- **Licence:** [PolyForm Noncommercial 1.0.0](LICENSE) — free for non-commercial, education, research, and cultural use
- **Source code:** maintained in a separate private repository; this public repo distributes signed installers only
- **Security:** see [SECURITY.md](SECURITY.md) for how to report vulnerabilities

## Note on the "Source code" archives

GitHub auto-generates `Source code (zip/tar.gz)` archives for every release. **Those archives are empty placeholders** — they do not contain the Jura Trace source. Download the platform installers (`.dmg`, `.msi`, `.exe`) instead.

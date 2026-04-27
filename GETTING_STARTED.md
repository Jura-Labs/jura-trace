# Getting Started with Jura Trace

> *A 10-minute walkthrough for first-time pilot testers — install, run your first verification, and see Content Credentials in action.*

This guide is for **release candidate v0.9.0-rc.24**. Jura Trace is pre-1.0 software in active testing — your feedback shapes the v1.0 release.

---

## Contents

1. [Before you begin](#1-before-you-begin)
2. [Install on macOS](#2-install-on-macos)
3. [Install on Windows](#3-install-on-windows)
4. [First launch](#4-first-launch)
5. [Try Content Credentials verification](#5-try-content-credentials-verification)
6. [Try forensic analysis on an unsigned image](#6-try-forensic-analysis-on-an-unsigned-image)
7. [Where things live](#7-where-things-live)
8. [Common questions](#8-common-questions)
9. [Sending feedback](#9-sending-feedback)

---

## 1. Before you begin

**System requirements**

| | macOS | Windows |
|---|---|---|
| Version | macOS 12 (Monterey) or later | Windows 10 or later (x64) |
| Architecture | Apple Silicon (M-series) | x64 |
| Disk space | 800 MB | 800 MB |
| Network | Optional (used for Content Credentials trust checks) | Optional |

**What gets installed**

- The Jura Trace desktop application
- A small Python analysis service that runs locally on your computer (port 8200)
- A local REST API on port 8300 (used by the desktop app itself)
- A local SQLite database storing your verification history

**What does NOT happen**

- No images, video or audio leave your computer
- No accounts, no telemetry, no analytics
- No background processes when the app is closed

---

## 2. Install on macOS

### Download

Open **[the latest release page](https://github.com/Jura-Labs/jura-trace/releases/latest)** and download:

```
Jura.Trace_0.9.0_aarch64.dmg     (Apple Silicon)
```

> **Intel Mac?** Apple Silicon only in this build. Intel support returns at v1.0 via a universal binary.

### Install

1. **Double-click** the downloaded `.dmg` file. A window opens showing the **Jura Trace** app icon and an **Applications** folder.
2. **Drag** the Jura Trace icon onto the Applications folder.
3. **Eject** the DMG (right-click the disk icon on your desktop → Eject).
4. Open **Applications** in Finder, find **Jura Trace**, and **double-click** to launch.

### First-launch security prompt

This build is signed with our Apple Developer ID and notarised by Apple. You should **not** see the "unidentified developer" warning. If you do, right-click the app and choose **Open** — macOS will remember your choice for future launches.

---

## 3. Install on Windows

### Download

Open **[the latest release page](https://github.com/Jura-Labs/jura-trace/releases/latest)** and download **one** of:

```
Jura.Trace_0.9.0_x64_en-US.msi          (recommended for most users)
Jura.Trace_0.9.0_x64-setup.exe          (NSIS installer — better for re-installs)
```

> **Which one?** The `.msi` is the standard Windows installer — best for first installs and IT-managed deployments. The `.exe` (NSIS) handles re-installs more gracefully if you have an older version already installed.

### Install

1. **Double-click** the downloaded installer.
2. Windows will show a **SmartScreen** warning ("Windows protected your PC"). Click **More info** → **Run anyway**. This warning will disappear in a future build once Microsoft's reputation system has seen enough downloads of our signed binary.
3. Follow the installer prompts (default options are fine).
4. Launch **Jura Trace** from the Start menu.

### Optional: install FFmpeg for video / audio analysis

Image verification works out of the box. Video and audio require FFmpeg:

- **With winget** (Windows 10 1709+): open PowerShell and run:
  ```
  winget install Gyan.FFmpeg
  ```
- **Without winget** (Windows Server, locked-down enterprise SKUs): the in-app **Settings → Setup Wizard** has a step-by-step guide for downloading the static binary from gyan.dev.

---

## 4. First launch

When Jura Trace starts for the first time:

- A small one-time setup runs (~5 seconds) — initialising the local database and starting the analysis service
- The app opens to the **Dashboard** screen
- The top of the screen shows your activity counters (all zeroes on first run) and a **"Welcome to Jura Trace"** card with a button to start verifying

You don't need to log in or create an account. There isn't one.

**Quick orientation**

| Top-nav tab | What it does |
|---|---|
| **Dashboard** | Activity overview, sidecar service status |
| **Verify** | Drag in an image, video or document → see what Jura Trace finds |
| **Settings** | Network mode, optional AI add-ons, data location |
| **Help** | In-app documentation, methodology, FAQ |

---

## 5. Try Content Credentials verification

This is the most exciting workflow to try first. **Content Credentials** are a cryptographic provenance standard ([C2PA](https://c2pa.org)) that lets cameras and editing tools embed a tamper-evident record of how an image was created. Jura Trace verifies these credentials and shows you the full chain in plain English.

### Step A — Get a test image with valid Content Credentials

Pick **any** of these sources:

#### Easiest — Adobe's gallery

1. Open <https://contentcredentials.org/verify> in your browser
2. The page has a **gallery** of example images — Adobe Firefly creations, Pixel camera captures, Truepic-signed news photos
3. Right-click any thumbnail → **Save image as…** to download it
4. (Optional) Notice the same page shows the credentials inline — you can compare what Jura Trace finds against the official Content Credentials viewer

#### If you have a Pixel phone (8, 8a, 9, 9a, 9 Pro)

Recent Pixel cameras embed C2PA Content Credentials in every photo by default — including Magic Editor and Zoom Enhance edits. Just **AirDrop or transfer one of your own Pixel photos** to your computer.

#### If you use Adobe Photoshop, Lightroom, or Firefly

Any export from these tools (with Content Credentials enabled in preferences) will have valid credentials. Export a recent edit and use that.

#### Or use a sample we know works

Adobe maintains a permanent C2PA test image at:

```
https://opensource.contentauthenticity.org/docs/manifest/examples/CAICAI.jpg
```

Right-click → Save as. Download it to your Desktop.

### Step B — Verify it in Jura Trace

1. Open **Jura Trace**
2. Click the **Verify** tab in the top nav
3. **Drag the downloaded image** onto the upload area in the centre of the page (or click to browse)
4. Wait ~5–15 seconds while the analysis runs

### Step C — Read the results

You'll see a layered, progressive disclosure of what was found:

#### **L1 — The seal (top of the page)**

A small badge with the Content Credentials `cr` icon if credentials are present. Colour indicates trust level: green (verified), amber (mixed), red (failed/missing).

#### **L2 — Provenance summary**

A plain-English single line. Examples:
- *"Created by Pixel Camera on 5 August 2025 — verified."*
- *"Edited in Adobe Photoshop, originally from Adobe Firefly — verified."*
- *"AI-generated by Adobe Firefly — verified."*

#### **L3 — Full detail panel**

Click **"Show full details"** to open a panel showing:
- The full **manifest chain** — every step the image went through (Capture → Edit → Export, etc.)
- For each step: who signed it, what action was performed, when it happened
- Validation status of the cryptographic signatures
- Any warnings (e.g. expired certificates, untrusted signers)
- The 12 automatic forensic detectors' results, displayed alongside the C2PA chain

#### **L4 — Raw data (for the technically curious)**

A "Show raw validation codes" toggle reveals the exact c2pa-rs validation outcomes — useful for cross-checking against the C2PA spec.

### What to look for

- **Green dots** in the manifest chain timeline = each step's signature validated
- The **Active manifest** is the most recent edit; the **Origin manifest** is the original capture
- **AI-generated** content (e.g. Firefly exports) caps the trust score at 25% — by design, because the producer self-declared AI generation
- **Composite-AI** content (e.g. Pixel Zoom Enhance — real photos with AI-edited regions) caps trust at 55% — a real photograph with declared AI components

### Things you should try

- Verify a Pixel photo (or one from the contentcredentials.org gallery) — should show the full chain with green ticks
- Verify a Firefly export — should show "AI-generated" prominently and cap trust at 25%
- Verify a Pixel Zoom Enhance image — should show two manifests in the chain (Capture → Zoom Enhance edit) with both validated
- Edit one of those images in Photoshop without Content Credentials enabled, save, and verify the result — Jura Trace should report the credentials as broken or missing

---

## 6. Try forensic analysis on an unsigned image

Most images on the web don't have Content Credentials — they're just JPEGs. Jura Trace also runs **12 automatic forensic detectors** that look for signs of manipulation independently of any cryptographic provenance.

### Try this

1. Find any **AI-generated image without Content Credentials** — e.g. a Stable Diffusion or Midjourney output, or any image you can find on Reddit's r/midjourney
2. Drag it into the **Verify** tab
3. Open the **"Is this AI-generated?"** card

You should see signals from:
- **Deepfake classifier** (GBM ensemble + UnivFD CLIP probe)
- **CLIP zero-shot AI/authentic detector** (if enabled)
- **EXIF anomaly** detector (looks for AI-pipeline traces in metadata)
- **JPEG ghost** (looks for re-compression artefacts that suggest editing)
- And more

Each detector has a confidence and a one-line explanation. The trust score combines them with a documented formula (see **Help → Methodology** in-app for the full breakdown).

### What's normal

- A real photo with no C2PA: usually scores 75-95% trust ("Good") — most detectors return null/low
- An AI-generated image: usually scores 5-30% trust ("Low") — multiple detectors flag concerns
- A real photo with no metadata at all (e.g. a screenshot of a screenshot): may score "Mixed" — detectors can't disprove AI without metadata to anchor against

This is the **honest output** Jura Trace's brand promise commits to: certainty when warranted, uncertainty when warranted, and full disclosure of how each verdict was reached.

---

## 7. Where things live

**macOS**

| | Path |
|---|---|
| App | `/Applications/Jura Trace.app` |
| User data | `~/Library/Application Support/org.juralabs.trace/` |
| Verification database | `~/Library/Application Support/org.juralabs.trace/jura.db` |
| Logs | `~/Library/Logs/jura-trace/` |
| Sidecar service log | `~/Library/Logs/jura-trace/sidecar.log` |

**Windows**

| | Path |
|---|---|
| App | `C:\Program Files\Jura Trace\` |
| User data | `%APPDATA%\org.juralabs.trace\` |
| Verification database | `%APPDATA%\org.juralabs.trace\jura.db` |
| Logs | `%APPDATA%\jura-trace\logs\` |

---

## 8. Common questions

### Why does my computer fan run during a verification?

The forensic detectors do real CPU work, especially the deepfake classifier and CLIP probe. A typical image takes 5–15 seconds and the fan calms down once analysis is complete.

### What is "Network mode"?

In **Settings → Network Access** you'll see two options:
- **Enhanced (default)** — allows outbound HTTPS to certificate-authority OCSP/CRL endpoints (for full Content Credentials trust validation), the open-meteo weather API (for verify-context), and any remote manifest URLs embedded in the credentials of files you choose to verify.
- **Standard (offline)** — fully offline. Some Content Credentials checks become "informational" (we can't reach the CA to confirm a certificate hasn't been revoked).

For pilot testing we recommend keeping **Enhanced** on. If you switch to Standard you'll see the difference clearly: many real-world Pixel and Adobe-signed images report "trust uncertain" because we can't reach Apple/Google/Adobe's CAs.

### What about Ollama / LLaVA / Qwen?

Optional. Jura Trace works fully without them. They power two add-on features:
- LLaVA (vision LLM) — generates plain-English image descriptions in the verify L3 panel
- Qwen2.5 (text LLM) — powers the experimental claim verification feature

If Ollama is installed and running on its default port (11434), Jura Trace detects it automatically. See **Help → Settings → Ollama AI Features** in-app.

### Why are some pages missing from the nav?

The **Monitor** tab is hidden in this build to keep pilot testing focused on Verify (the workflow under formal C2PA Validator review). The route still works if you visit `/monitor` directly. **Protect** (Content Credentials *signing*) is similarly hidden — it's a separate workstream not yet ready for pilot review.

### My Pixel image shows "Concern" even though it's a real photo!

This is **expected** for **Pixel Zoom Enhance** photos. They use AI to add detail — Pixel itself declares this in the Content Credentials as `compositeWithTrainedAlgorithmicMedia`. Jura Trace honours that declaration and caps trust at 55% (yellow / "Mixed signals"). If you take a normal Pixel photo (no Zoom Enhance, no Magic Editor), trust should land in the green.

### Is anything sent to a server?

In **Standard (offline)** mode: nothing. In **Enhanced** mode: only outbound HTTPS to:
- Certificate authorities (revocation checks, only when verifying a signed file)
- open-meteo.com (only if you click the optional weather-context button)
- Any HTTPS URL explicitly embedded in the Content Credentials of a file you choose to verify

The image itself **never** leaves your device.

---

## 9. Sending feedback

### Bugs

Open an issue using the bug-report template:

<https://github.com/Jura-Labs/jura-trace/issues/new/choose>

Please include:
- The Jura Trace version (visible in **Help → About** in-app, also in the footer)
- Your OS and version (e.g. macOS 15.4, Windows 11 23H2)
- Steps to reproduce
- A screenshot if relevant
- Sidecar log if a verification failed (path in [§7 Where things live](#7-where-things-live))

### Security issues

**Please don't file these as public issues.** See [SECURITY.md](https://github.com/Jura-Labs/jura-trace/blob/main/SECURITY.md) for the responsible disclosure process.

### Pilot programme questions

Email **pilots@juralabs.org** (or **hello@juralabs.org** if pilots@ isn't yet provisioned).

### General

- Website: <https://juralabs.org>
- Brand: <https://github.com/Jura-Labs/jura-trace/blob/main/README.md>

---

*Thank you for piloting Jura Trace. The honest output you'll see is the result of months of calibration work — every detector has a documented false-positive rate, every claim has evidence behind it, and the trust score formula is published in-app.*

*— Jura Labs CIC, 27 April 2026*

# Security Policy

## Reporting a Vulnerability

We take the security of Jura Trace seriously. If you believe you have found a security vulnerability in Jura Trace, the Python ML sidecar, or any related component, please report it to us responsibly.

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, report them by email to:

**hello@juralabs.org** with `[SECURITY]` in the subject line)

You should receive an acknowledgement within **5 working days**. If, for any reason, you do not, please follow up to ensure we received your original message.

Please include the following in your report:

- The type of issue (e.g. buffer overflow, IPC injection, signature bypass, supply-chain concern)
- Full paths of source file(s) related to the issue, if you have them
- The location of the affected source code (tag/branch/commit or direct URL)
- Any special configuration required to reproduce the issue
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit it

This information will help us triage your report more quickly.

## Disclosure Policy

We follow a **coordinated disclosure** process:

1. We confirm the vulnerability and determine its scope.
2. We develop and test a fix.
3. We release the fix in a new version and credit the reporter (with their permission) in the release notes.
4. We publicly disclose the vulnerability, typically within **90 days** of the initial report or once a fix is broadly available — whichever comes first.

## Supported Versions

Jura Trace is in a release-candidate phase. The currently supported version is the **latest published release** in this repository. Older release candidates are not patched.

| Version            | Supported          |
| ------------------ | ------------------ |
| Latest release     | :white_check_mark: |
| Older release candidates | :x:           |

## Scope

In scope:
- The Tauri desktop application (Rust core, SvelteKit frontend, IPC surface, REST API on port 8300)
- The Python ML sidecar on port 8200
- C2PA signing and verification logic
- Auto-updater pipeline
- Build and signing infrastructure (release artefacts, code-signing certificates)

Out of scope:
- Self-hosted modifications
- Issues caused by third-party software the user has installed (Ollama, custom models, etc.)
- Vulnerabilities in upstream dependencies that have already been disclosed and have a public CVE — please report those upstream

## Safe Harbour

We will not pursue legal action against researchers who:

- Make a good-faith effort to comply with this policy
- Avoid privacy violations, destruction of data, and interruption or degradation of services
- Do not exploit a security issue beyond what is necessary to confirm it
- Give us reasonable time to address the issue before public disclosure

Thank you for helping keep Jura Trace and its users safe.

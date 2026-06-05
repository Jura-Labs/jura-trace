# Contributing to Jura Trace

Thank you for your interest in contributing to Jura Trace, a local-first
desktop application for forensic media verification, published as
public-interest infrastructure by Jura Labs Community Interest Company.

This repository (`Jura-Labs/jura-trace` on GitHub) is the public
release-distribution surface. From Monday 22 June 2026 the canonical source
code repository will be `codeberg.org/jura-labs/jura-trace`. This GitHub
repository will continue to host signed installer binaries, the README, the
methodology documentation, and the auto-updater endpoint.

## What this repository accepts

| Contribution type | Where to file |
|---|---|
| Bug reports on installer binaries (signing, install failure, platform-specific behaviour) | Issues on this repository |
| Documentation PRs (README, `docs/`, methodology, glossary, install guides) | Pull requests on this repository |
| Translation contributions | Pull requests on this repository |
| Source code changes (Rust, Python, SvelteKit) | From 2026-06-22, pull requests on `codeberg.org/jura-labs/jura-trace` |
| Security vulnerabilities | Email `security@juralabs.org`, do NOT open a public issue. See `SECURITY.md`. |

## Filing a bug report

Use the issue template at `.github/ISSUE_TEMPLATE/bug_report.yml`. Please
include:

1. Jura Trace version (visible in the About menu or in the installer filename)
2. Platform and version (macOS 15.x, Windows 11, Linux distribution and version)
3. Steps to reproduce
4. What you expected to see versus what actually happened
5. Any error messages, trace IDs, or screenshots

For verification-pipeline questions (trust score, detector output, false
positives), please include the image file or a description of the image
characteristics, with attention to source-protection if the image is
sensitive (see `SECURITY.md` for guidance on sensitive-material reporting).

## Submitting a documentation pull request

1. Fork the repository
2. Make your change in a feature branch with a descriptive name
3. Open a pull request using the template at `.github/PULL_REQUEST_TEMPLATE.md`
4. Complete the **AI-Disclosure** field (required, see below)
5. A maintainer will respond within 5 working days

## AI tool use disclosure

Jura Labs publishes its full Generative AI Use Policy at
`GENAI_USE_POLICY.md`. The policy is aligned with the NLnet NGI Zero
Generative AI policy v1.1 (26 January 2026).

Every pull request must complete the AI-Disclosure field in the PR template.
Disclose:

- Whether AI assistance was used in drafting any part of the change
- Which tools (Claude, GitHub Copilot, ChatGPT, others)
- Which parts of the diff the AI helped draft
- What you personally read, ran, and verified before submitting

Honest disclosure is welcome. Concealment of AI assistance is grounds for
closing the pull request without merge.

## Code of Conduct

This project follows the Contributor Covenant 2.1 (see `CODE_OF_CONDUCT.md`).
Conduct concerns should be sent to `hello@juralabs.org`.

## Style

For documentation contributions:

- British spelling for user-facing text (organisation, colour, catalogue)
- American spelling acceptable in code identifiers for framework consistency
- Plain English, avoid corporate-speak
- No emojis in body text (acceptable in commit messages where conventional)
- Match the existing tone and structure of the file you are editing

## Licensing of contributions

Jura Trace is dual-licensed: AGPL-3.0-or-later for the open-source
community, with a parallel commercial-licence path for use cases that cannot
operate under copyleft terms (see `COMMERCIAL.md`).

By submitting a contribution to this repository, you confirm that:

1. You wrote the contribution yourself, or you have permission from the
   original author to submit it.
2. You grant the copyright holder (Paul Griffiths) a perpetual, worldwide,
   non-exclusive, royalty-free, irrevocable licence to use, reproduce,
   modify, prepare derivative works of, publicly display, publicly perform,
   sublicense, and distribute your contribution and any derivative works.
3. You retain copyright in your contribution; the licence above is a grant,
   not an assignment.
4. The grant includes the right to relicense your contribution under any
   future open-source licence and the right to license it commercially as
   part of the dual-licensing model.

The full contributor licence agreement is documented in the canonical source
repository at `codeberg.org/jura-labs/jura-trace` from 22 June 2026.

## Contact

| Purpose | Email |
|---|---|
| General, partnership, commercial, licensing | `hello@juralabs.org` |
| Security disclosure | `security@juralabs.org` |
| Press and media | `press@juralabs.org` (from 2026-06-15) |

## Acknowledgements

Jura Trace exists because journalists, fact-checkers, human-rights
investigators, archivists, and curious citizens need tools to make sense of
synthetic media. Every honest contribution helps. Thank you.

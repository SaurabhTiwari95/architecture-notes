# Release checklist

The same checklist every one of my projects meets before publishing. This repo is design notes plus
one check script, so items that only apply to running services are marked **N/A** with the reason.

Last checked: 2026-11-09

## A. Installation and usage

- [x] What it is, with a diagram
- [x] Prerequisites with versions and links
- [x] Install steps for Windows and macOS/Linux
- [x] Usage with expected output (reading the notes; running the check)
- [x] One command to run the tests
- [x] Configuration table for every environment variable
- [x] Troubleshooting
- [x] Design decisions, trade-offs, what's next
- [x] AI-assisted line
- [x] Relative links checked (0 broken); external links checked in CI by lychee

## B. No private data

- [x] Sample and illustrative content only; cost figures are made up and labelled
- [x] No employer, product or people names; no real hosts, IPs, account ids, ARNs, buckets or keys
- [x] No work code, names, counts or costs
- [x] Only personal detail: author name in `LICENSE`
- [x] Pre-publish check passes locally (0 hits) and runs in CI; gitleaks runs in CI over full history
- [ ] gitleaks run locally: not installed on the build machine; CI covers it on the first push

## C. Secure by default

- [x] No secrets used; `.env`, keys and the block-list are git-ignored
- [x] CI token permissions limited to `contents: read`
- [x] Dev dependencies pinned; Dependabot for pip and GitHub Actions
- [x] `SECURITY.md`
- [ ] GitHub Actions pinned to full commit SHAs: pinned to major versions for now; Dependabot keeps them current
- [ ] Repo settings (do on GitHub after the first push): secret scanning + push protection, private vulnerability reporting, branch protection on `main` requiring CI
- N/A Input validation, parameterised SQL, rate limits, auth, error handling, Docker non-root, CodeQL: no service or app code here (CodeQL added in the code projects)

## D. Scalable

- [x] "How it scales" section (content growth, ADR numbering, check speed)
- N/A Stateless app, pooling, migrations, pagination, background jobs, health endpoints: no service

## E. Optimised

- [x] Check script reads each file once and skips files over 2 MB; whole repo scans in under a second
- N/A Async I/O, caching, Docker images, LLM cost controls, load test: no service

## F. Repo basics

- [x] Tests: 21 passing, coverage 99% (gate at 80%)
- [x] Lint: ruff check and ruff format clean
- [x] Markdown: core markdownlint rules checked locally (0 issues); full markdownlint runs in CI
- [x] `.gitignore`, `LICENSE` (MIT), `CHANGELOG.md`

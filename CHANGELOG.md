# Changelog

All notable changes to this repository are documented in this file. The format is based on [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).

This repository has no version numbers: a merge to `main` is the release and callers pin a commit SHA, so every section is headed by its merge date and `[Unreleased]` stays empty, because each pull request writes its entry straight under the date it is merged.

## [Unreleased]

## [2026-10-31]

### Added

- **Example workflows for a pipeline that runs every check once.** `examples/ci.yml` runs the caller's own `check` and then `e2e.yml` only when `check` is green and code changed; `examples/deploy-test.yml` and `examples/deploy-prod.yml` deploy, run a smoke check, and for production create the tag and the release after it. The README describes the setup in the new section "Recommended pipeline". (#3)
- **`templates/smoke.sh` checks a deployed site with a few requests.** `expect <path> <status> [text]` retries on network errors and 5xx answers, and exits 1 when a status or a text does not match. (#3)

### Changed

- **`examples/private-caller.yml` is now the private Security caller only.** It runs on every pull request, every Monday at 03:15 UTC and by hand, and no longer again on a push to `main`. The reusable workflows did not change, so a pin to `b28b032feca5d88400eba1f2b8f8a427661dbcfe` stays current. (#3)

## [2026-10-26]

### Added

- **Reusable workflows `security.yml`, `e2e.yml` and `zap-baseline.yml`, first at commit `e370deec955af4b0bf2e74b930a8e6f365915ec0`.** `security.yml` runs gitleaks, OSV-Scanner, Semgrep, actionlint and zizmor, plus CodeQL and OpenSSF Scorecard for a public caller; `e2e.yml` runs Playwright and uploads the report; `zap-baseline.yml` scans a URL the caller passes. The repository also got `templates/dependabot.yml`, a public and a private caller example, and its own CI (actionlint and zizmor). (#1)

### Changed

- **The repository is `jrhimself/platform`, the shared repository for every `jrhimself` repository.** The README and caller examples use the new name, and from commit `b28b032feca5d88400eba1f2b8f8a427661dbcfe` the zizmor policy in `security.yml` lets `jrhimself/platform/*` be pinned by tag instead of the old name `jrhimself/ci-templates/*`. Workflow paths and inputs are unchanged. (#2)

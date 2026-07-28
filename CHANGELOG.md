# Changelog

Format based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.2-private-review] - 2026-07-28

### Added
- Customer verify path: `make prove`, `compliance/verify.json`, `scripts/score-results.py`.

### Changed
- README and this changelog list current OpenSCAP verify scores (≥90% floor).
- All CIS/STIG profiles apply SSG remediation via `stigforge_profile` task includes.
- Matrix cell `ubuntu24_cis` marked **green** with passing docker verify evidence.

### Fixed
- CIS/STIG roles no longer point at empty `rules.yml` scaffold (remediation runs in verify).

### Verified (OpenSCAP)

- **`cis-l1`** — score **95.0%** (floor 90.0%) · gate **PASS** · evidence `20260728T093616Z`
  - Remaining counted failures: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_passwords_pam_faillock_deny, accounts_passwords_pam_faillock_enabled`
  - _(+1 more — see `score.json`)_
- **`cis-l2`** — score **94.05%** (floor 90.0%) · gate **PASS** · evidence `20260728T093804Z`
  - Remaining counted failures: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_minimum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_passwords_pam_faillock_deny`
  - _(+3 more — see `score.json`)_

### Provenance

- Factory pipeline: https://github.com/stigready/stigforge/actions/runs/30348467615
- Factory commit: `49f1c019fbf7ba7f8edc345d79321ed45f9534de`

## [0.2.1-private-review] - 2026-07-28

### Changed
- Galaxy-style layout: Ansible role at repository root; evidence under `compliance/`.
- Private review tag `v0.2.1-private-review` (supersedes nested `roles/<role>/` export).

## [0.2.0-private-review] - 2026-07-26

### Added
- First private StigForge export to `stigready/*` (factory review; nested role path).

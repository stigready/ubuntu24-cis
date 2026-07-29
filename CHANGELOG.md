# Changelog

Format based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.4-private-review] - 2026-07-29

### Changed
- StigForge export refresh for `ubuntu24_cis` at `0.2.4-private-review`.

### Verified (OpenSCAP)

- **`cis-l1`** — score **97.78%** (floor 90.0%) · gate **PASS** · evidence `20260729T100314Z`
  - Remaining counted failures: `accounts_password_pam_pwhistory_remember, accounts_passwords_pam_faillock_deny, accounts_passwords_pam_faillock_enabled, accounts_passwords_pam_faillock_unlock_time`
- **`cis-l2`** — score **97.3%** (floor 90.0%) · gate **PASS** · evidence `20260729T100631Z`
  - Remaining counted failures: `accounts_password_pam_pwhistory_remember, accounts_passwords_pam_faillock_deny, accounts_passwords_pam_faillock_enabled, accounts_passwords_pam_faillock_root_unlock_time, accounts_passwords_pam_faillock_unlock_time`

### Provenance

- Factory pipeline: https://github.com/stigready/stigforge/actions/runs/30440754045
- Factory commit: `c481b47d629f5bc2357a86a933aa6f94f5245fce`

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

- **`cis-l1`** — score **88.17%** (floor 90.0%) · gate **FAIL** · evidence `20260726T135932Z`
  - Remaining counted failures: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_password_pam_pwquality_enabled, accounts_passwords_pam_faillock_deny`
  - _(+12 more — see `score.json`)_
- **`cis-l2`** — score **87.36%** (floor 90.0%) · gate **FAIL** · evidence `20260726T135941Z`
  - Remaining counted failures: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_minimum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_password_pam_pwquality_enabled`
  - _(+14 more — see `score.json`)_

### Provenance

- Factory pipeline: https://github.com/stigready/stigforge/actions/runs/30353408831
- Factory commit: `5601d6c388051bf9f7636b086d93888a709b8b31`

## [0.2.1-private-review] - 2026-07-28

### Changed
- Galaxy-style layout: Ansible role at repository root; evidence under `compliance/`.
- Private review tag `v0.2.1-private-review` (supersedes nested `roles/<role>/` export).

## [0.2.0-private-review] - 2026-07-26

### Added
- First private StigForge export to `stigready/*` (factory review; nested role path).

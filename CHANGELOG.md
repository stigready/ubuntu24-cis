# Changelog

Format based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.2-private-review] - export review

### Added
- Initial StigForge export of matrix role `ubuntu24_cis`.
- OpenSCAP verify evidence bundles per profile under `compliance/releases/`.

### Verified (CI)

- **`cis-l1`** — score **95.0%** (floor 90.0%) · gate **PASS** · evidence `20260728T093616Z`
  - OpenSCAP failures still counted: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_passwords_pam_faillock_deny, accounts_passwords_pam_faillock_enabled`
- **`cis-l2`** — score **94.05%** (floor 90.0%) · gate **PASS** · evidence `20260728T093804Z`
  - OpenSCAP failures still counted: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_minimum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_passwords_pam_faillock_deny`

### Provenance

- Factory pipeline: https://github.com/stigready/stigforge/actions/runs/30348467615
- Factory commit: `49f1c019fbf7ba7f8edc345d79321ed45f9534de`


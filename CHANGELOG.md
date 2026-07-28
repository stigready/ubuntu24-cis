# Changelog

Format based on [Keep a Changelog](https://keepachangelog.com/).

## [0.2.1-private-review] - export review

### Added
- Initial StigForge export of matrix role `ubuntu24_cis`.
- OpenSCAP verify evidence bundles per profile under `compliance/releases/`.

### Verified (CI)

- **`cis-l1`** — score **88.17%** (floor 90.0%) · gate **FAIL** · evidence `20260726T135932Z`
  - OpenSCAP failures still counted: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_password_pam_pwquality_enabled, accounts_passwords_pam_faillock_deny`
- **`cis-l2`** — score **87.36%** (floor 90.0%) · gate **FAIL** · evidence `20260726T135941Z`
  - OpenSCAP failures still counted: `account_disable_post_pw_expiration, accounts_maximum_age_login_defs, accounts_minimum_age_login_defs, accounts_password_pam_pwhistory_enabled, accounts_password_pam_pwhistory_enforce_root, accounts_password_pam_pwhistory_remember, accounts_password_pam_pwhistory_use_authtok, accounts_password_pam_pwquality_enabled`

### Provenance

- Factory pipeline: https://github.com/stigready/stigforge/actions/runs/30277229616
- Factory commit: `f0323b6e2f0f36a0418447b9859a0576278541b8`


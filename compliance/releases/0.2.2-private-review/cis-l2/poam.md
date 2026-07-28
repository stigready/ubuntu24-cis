# POA&M — ubuntu24_cis / cis-l2

StigForge docker verify (OpenSCAP). Policy-exempt rules are excluded from the score denominator.
Failure buckets follow stigready `poam-from-arf.py` classification (N/A / risk-accepted / gap).

**Score:** 87.36% (floor 90.0%) — below floor

## OpenSCAP failures — classified (22)

### Gap - deterministic config (fixable in role) (5)

- `accounts_password_pam_pwhistory_enforce_root`
- `accounts_passwords_pam_faillock_deny`
- `accounts_passwords_pam_faillock_enabled`
- `accounts_passwords_pam_faillock_root_unlock_time`
- `accounts_passwords_pam_faillock_unlock_time`

### Gap - role vs SSG (scheduled remediation) (17)

- `account_disable_post_pw_expiration`
- `accounts_maximum_age_login_defs`
- `accounts_minimum_age_login_defs`
- `accounts_password_pam_pwhistory_enabled`
- `accounts_password_pam_pwhistory_remember`
- `accounts_password_pam_pwhistory_use_authtok`
- `accounts_password_pam_pwquality_enabled`
- `accounts_umask_etc_bashrc`
- `accounts_umask_etc_login_defs`
- `accounts_umask_etc_profile`
- `disable_users_coredumps`
- `ensure_pam_wheel_group_empty`
- `file_permission_user_init_files`
- `file_permissions_ungroupowned`
- `package_pam_pwquality_installed`
- `permissions_local_var_log`
- `use_pam_wheel_group_for_su`

## Policy exempt — not scored (32)

- `accounts_password_pam_enforce_root`
- `auditd_audispd_configure_remote_server`
- `auditd_offload_logs`
- `configure_opensc_card_drivers`
- `dconf_gnome_screensaver_idle_delay`
- `dconf_gnome_session_idle_user_locks`
- `ensure_root_password_configured`
- `force_opensc_card_drivers`
- `grub2_admin_username`
- `grub2_password`
- `grub2_set_password`
- `grub2_uefi_password`
- `grub2_unique_name`
- `install_smartcard_packages`
- `installed_OS_is_vendor_supported`
- `package_opensc_installed`
- `package_pcsc-lite_installed`
- `package_subscription-manager_installed`
- `rsyslog_encrypt_offload_defaultnetstreamdriver`
- `rsyslog_remote_access_monitoring`
- `rsyslog_remote_loghost`
- `service_pcscd_enabled`
- `smartcard_configure_ca`
- `smartcard_configure_cert_checking`
- `smartcard_configure_crl`
- `smartcard_pam_enabled`
- `sssd_certificate_verification`
- `sssd_enable_certmap`
- `sssd_enable_smartcards`
- `sudo_remove_nopasswd`
- `sudo_require_authentication`
- `sudo_require_reauthentication`


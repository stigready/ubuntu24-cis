# ubuntu24_cis — Ansible role (ubuntu24-cis)

**Ansible hardening role** for **Ubuntu 24.04 LTS**, generated from the CIS Ubuntu Linux 24.04 LTS Benchmark profiles in ComplianceAsCode SSG 0.1.82. Suitable for playbooks, Packer/Ansible provisioners, and golden-image pipelines. Search keywords: `ansible`, `ansible-role`, `cis`, `cis-benchmark`, `cis-hardening`, `compliance`, `devsecops`, `hardening`, `infrastructure`, `noble`, `openscap`, `security`, `stigforge`, `ubuntu`.

StigForge-exported Ansible role **`ubuntu24_cis`** · release **`0.3.51`**.
Matrix cell status: **`green`**.

## Before you run this role

Each default below changes how a running host behaves. Read them before you apply the role to a host you depend on.

### A default-deny nftables firewall replaces ufw

_Profiles: cis-l1, cis-l2 (cis-ws-l1 and cis-ws-l2 remove ufw but do not write this firewall). Requirement: ComplianceAsCode rules `nftables_ensure_default_deny_policy` ("Ensure nftables Default Deny Firewall Policy") and `package_ufw_removed` ("Remove ufw Package"), selected in SSG's CIS Ubuntu 24.04 Level 1 and Level 2 profiles._

**What the role does.** Removes the ufw package, writes /etc/nftables.rules and loads it during the play; nftables.service loads it again at every boot. The input, forward and output chains drop by default. Inbound, only loopback, replies to connections the host opened, TCP port 22 (SSH), and the DHCPv4, DHCPv6 and IPv6 neighbour-discovery traffic an EC2 instance needs to keep its address are allowed. Outbound, only loopback, replies, DNS (port 53), NTP (UDP 123), HTTP and HTTPS (80, 443), DHCP and neighbour discovery are allowed.

**Who is affected.** A host where SSH listens on a port other than 22 loses SSH access when the ruleset loads. So does any service that is not in the list above: application listeners, outbound mail, LDAP or Kerberos, monitoring and backup agents, container networking. A host outside EC2 may also need other DHCP or management traffic.

**How to change it.** Before the first run, set `ubuntu24cis_nftables_ensure_default_deny_policy: false` so the firewall is neither written nor loaded (nftables then keeps an accept-all ruleset), and set `ubuntu24cis_package_ufw_removed: false` to keep ufw. To keep the firewall and allow more traffic, add rules to /etc/nftables.rules and run `nft -f /etc/nftables.conf`. Each run of the role rewrites /etc/nftables.rules, so add them again after every run. If the role has already run, setting the variable to false does not remove the firewall: also replace /etc/nftables.rules with an accept-all table (or delete it and run the role again, which then writes an accept-all table) and run `nft -f /etc/nftables.conf`, or the default-deny ruleset loads again at the next boot. Run `apt install ufw` if you want ufw back.

**Effect on compliance.** With either variable set to false, the role no longer remediates that CIS rule, and an OpenSCAP scan reports it as failing.

### auditd halts the host when the audit log disk fills

_Profiles: cis-l2. Requirement: ComplianceAsCode rules `auditd_data_disk_full_action` ("Configure auditd Disk Full Action when Disk Space Is Full") and `auditd_data_retention_admin_space_left_action` ("Configure auditd admin_space_left Action on Low Disk Space"), selected in SSG's CIS Ubuntu 24.04 Level 2 profiles._

**What the role does.** Sets `disk_full_action = halt` and `admin_space_left_action = halt` in /etc/audit/auditd.conf. When the audit log disk is full, or its free space falls below the admin_space_left threshold, auditd shuts the host down so that no audit record is lost. `disk_error_action` is set to syslog.

**Who is affected.** Any host whose /var/log/audit can fill, for example a small or shared partition with no log shipping. The host shuts down, and its workloads with it. On EC2 the instance stops if its shutdown behaviour is stop (the default), and you can start it again. If its shutdown behaviour is terminate, or it is a Spot or Auto Scaling instance, it is terminated or replaced, and a root volume set to delete on termination is lost.

**How to change it.** Set `var_auditd_disk_full_action` and `var_auditd_admin_space_left_action` to the auditd action you want, for example `syslog`. The role writes the value you set. Where you can, size and monitor the audit log partition instead.

**Effect on compliance.** The OpenSCAP check in SSG's CIS Level 2 profile passes `halt` or `single` for disk_full_action, and only `halt` for admin_space_left_action. With any other value, including `syslog`, a scan reports the rule as failing. `single` is not a cloud-safe alternative: single-user mode leaves an instance with no console unreachable.

### The role removes the web server packages apache2 and nginx

_Requirement: ComplianceAsCode rules `package_httpd_removed` and `package_nginx_removed`, selected by the CIS profile for this product._

**What the role does.** Removes the apache2 and nginx packages if they are installed. Their configuration is removed or orphaned with them, depending on the package.

**Who is affected.** A host that serves web traffic, or runs an application that embeds either server as a package dependency. The services stop at the first run and do not come back at reboot.

**How to change it.** Before the first run, set `ubuntu24cis_package_httpd_removed: false` to keep apache2 (the variable is named after the ComplianceAsCode rule `package_httpd_removed`, which removes apache2 on Ubuntu), or `ubuntu24cis_package_nginx_removed: false` to keep nginx. The role then leaves that package alone. It does not report on the rule; only an OpenSCAP scan does (see Effect on compliance). If the role has already run, reinstall the package with the system package manager.

**Effect on compliance.** With a variable set to false, the role no longer remediates that CIS rule, and an OpenSCAP scan reports it as failing.

### The role removes rsync

_Requirement: ComplianceAsCode rule `package_rsync_removed`, selected by the CIS profile for this product._

**What the role does.** Removes the rsync package if it is installed.

**Who is affected.** Any host that uses rsync for backups, deployments, mirroring or file synchronisation, and any script that calls it. Other packages that depend on rsync are removed with it by the package manager's dependency handling.

**How to change it.** Before the first run, set `ubuntu24cis_package_rsync_removed: false` to keep rsync. The role then leaves it alone. It does not report on the rule; only an OpenSCAP scan does (see Effect on compliance). If the role has already run, reinstall the package with the system package manager.

**Effect on compliance.** With the variable set to false, the role no longer remediates that CIS rule, and an OpenSCAP scan reports it as failing.

### The role removes the GNOME display manager (gdm3)

_Profiles: cis-l2. Requirement: ComplianceAsCode rule `package_gdm_removed`, selected by the CIS Level 2 profile for this product._

**What the role does.** Removes the gdm3 package if it is installed. Only the cis-l2 profile does this; the default profile (cis-l1) and the workstation profiles leave gdm3 installed.

**Who is affected.** A host used as a graphical desktop or a remote desktop session host. After the removal there is no graphical login on the console.

**How to change it.** Before the first run with `stigforge_profile: cis-l2`, set `ubuntu24cis_package_gdm_removed: false` to keep gdm3. The role then leaves it alone. It does not report on the rule; only an OpenSCAP scan does (see Effect on compliance). If the role has already run, reinstall the package with the system package manager.

**Effect on compliance.** With the variable set to false, the role no longer remediates that CIS rule, and an OpenSCAP scan reports it as failing.

## Prefer a ready-made image?

StigReady Applied AMIs for AWS are built with a pinned release of this role, scored with OpenSCAP in the
build, and come with a per-version evidence bundle on request. See [https://stigready.com/applied/](https://stigready.com/applied/).

## Install

This repository root **is** the Ansible role (Galaxy-style layout). Release metadata and the
scoring helper live under `compliance/` and are not loaded when the role runs.

From **GitHub** (public):

```yaml
# requirements.yml
roles:
  - src: https://github.com/stigready/ubuntu24-cis
    scm: git
    version: v0.3.51   # or an immutable commit SHA
    name: ubuntu24_cis
```

```bash
ansible-galaxy role install -r requirements.yml -p ./roles
ansible-playbook -i inventory site.yml   # role: ubuntu24_cis
```

## Verification status (this release)

This release carries no per-role OpenSCAP score, and no OpenSCAP results ship with it. A container
cannot evaluate most hardening rules, so the role is not scored here. To score a host you hardened
with it, see *Score it yourself*. `compliance/releases/0.3.51/manifest.json` records this.

## Exceptions (excluded from the score gate)

These rules are excluded from the OpenSCAP score gate. Most depend on the network or organization the AMI is deployed into, so the role leaves them to the AMI owner; where the role does enforce a control and only the scanner cannot confirm it, the table says so. Each is tracked in the StigForge policy for this role and listed in the image's POA&M. The shared cloud policy strips a further documented set (for example the bootloader password and smartcard rules).

| Rule | Requirement | What this role does | What the AMI owner does |
|---|---|---|---|
| `kernel_module_overlayfs_disabled` | CIS Level 2: Ensure overlayfs kernel module is not available | Does not block the overlay module: no `install overlay /bin/false` and no blacklist line. The generated SSG tasks that wrote /etc/modprobe.d/overlay.conf are stripped. | Where no container runtime is used, add `install overlayfs /bin/false` to /etc/modprobe.d/overlayfs.conf, as the CIS control states. |

## Reports & review

- **[reports/index.html](reports/index.html)** — HTML report index
- **[CHANGELOG.md](CHANGELOG.md)** — release notes

## Score it yourself

This repository ships no OpenSCAP results (see *Verification status*). To score a host you
hardened with this role, run `oscap xccdf eval` on it and score the `results.xml` with this role's
exception list: see **[compliance/README.md](compliance/README.md)**.

## Notices

StigForge and StigReady are independent. They are not affiliated with, endorsed by or certified by the Center for Internet Security, Inc. (CIS), the Defense Information Systems Agency (DISA), the U.S. Department of Defense, NIST, Canonical or the ComplianceAsCode project. "CIS" and "CIS Benchmarks" are trademarks of the Center for Internet Security, Inc. DISA STIGs are DISA publications. Ubuntu is a trademark of Canonical Ltd. Linux is the registered trademark of Linus Torvalds in the U.S. and other countries. All trademarks are the property of their respective owners. This role applies ComplianceAsCode (SSG 0.1.82) remediation from SSG's CIS Ubuntu Linux 24.04 LTS Benchmark profiles. An OpenSCAP score is a measurement, not a certification.

## License

Copyright (c) 2026 StigReady.

- **[LICENSE](LICENSE)** (MIT) — StigForge export packaging
- **[NOTICE](NOTICE)** — ComplianceAsCode / BSD-3-Clause task body attribution

## Catalog

- [https://stigready.com/#stigforge](https://stigready.com/#stigforge)


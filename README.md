# ubuntu24_cis — Ansible role (ubuntu24-cis)

**Ansible hardening role** for **Ubuntu 24.04 LTS** (CIS Benchmark). Suitable for playbooks, Packer/Ansible provisioners, and golden-image pipelines. Search keywords: `ansible`, `ansible-role`, `cis`, `cis-benchmark`, `cis-hardening`, `compliance`, `devsecops`, `hardening`, `infrastructure`, `noble`, `openscap`, `security`, `stigforge`, `ubuntu`.

StigForge-exported Ansible role **`ubuntu24_cis`** · release **`0.3.33`**.
Matrix cell status: **`green`**.

## Install (Ansible Galaxy)

This repository root **is** the Ansible role (Galaxy-style layout). OpenSCAP evidence
lives under `compliance/` and is not loaded when the role runs.

From **Ansible Galaxy** (after import; namespace `stigready`):

```bash
ansible-galaxy role install stigready.ubuntu24_cis,0.3.33
```

From **GitHub** (public):

```yaml
# requirements.yml
roles:
  - src: https://github.com/stigready/ubuntu24-cis
    scm: git
    version: v0.3.33   # or an immutable commit SHA
    name: ubuntu24_cis
```

```bash
ansible-galaxy role install -r requirements.yml -p ./roles
ansible-playbook -i inventory site.yml   # role: ubuntu24_cis
```

## Verification status (this release)

Evidence was produced by **docker verify + OpenSCAP** on the factory CI run cited below.

| Profile | Score | Floor | Gate | Ansible | Evidence tested (UTC) |
|---|---:|---:|---|---|---|

## Exceptions (excluded from the score gate)

These rules are excluded from the OpenSCAP score gate. Most depend on the network or organisation the AMI is deployed into, so the role leaves them to the AMI owner; where the role does enforce a control and only the scanner cannot confirm it, the table says so. Each is tracked in `policy/products/` of [stigforge](https://github.com/stigready/stigforge) and listed in the image's POA&M. The shared cloud policy (`policy/cloud-ami.yml`) strips a further documented set (for example the bootloader password and smartcard rules).

| Rule | Requirement | What this role does | What the AMI owner does |
|---|---|---|---|
| `kernel_module_overlayfs_disabled` | CIS Level 2: Ensure overlayfs kernel module is not available | Does not block the overlay module: no `install overlay /bin/false` and no blacklist line. The generated SSG tasks that wrote /etc/modprobe.d/overlay.conf are stripped. | Where no container runtime is used, add `install overlayfs /bin/false` to /etc/modprobe.d/overlayfs.conf, as the CIS control states. |

Full artifacts per profile: `compliance/releases/0.3.33/<profile>/` (`score.json`, `results.xml`, `arf.xml`, `evidence.json`, `evidence-report.html`, `poam.md`).

## Reports & review

- **[REVIEW.md](REVIEW.md)** — linked evidence index for product owner review
- **[reports/index.html](reports/index.html)** — HTML report index
- **[CHANGELOG.md](CHANGELOG.md)** — release notes and verify summary

## Verify the score (customer)

Re-run OpenSCAP in Docker and compare to this release's evidence:

```bash
make prove RELEASE=0.3.33
```

Or score your own `results.xml`: see **[compliance/README.md](compliance/README.md)**.

## License

- **[LICENSE](LICENSE)** (MIT) — StigForge export packaging
- **[NOTICE](NOTICE)** — ComplianceAsCode / BSD-3-Clause task body attribution

## Factory

- Monorepo: [stigready/stigforge](https://github.com/stigready/stigforge) @ `6ac0366c316c968cd1edd620100e9fe2d9c923e2`
- CI run: https://github.com/stigready/stigforge/actions/runs/38901987134
- Catalog: [https://stigready.com/#stigforge](https://stigready.com/#stigforge)


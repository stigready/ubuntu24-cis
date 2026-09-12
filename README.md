# ubuntu24_cis — Ansible role (ubuntu24-cis)

**Ansible hardening role** for **Ubuntu 24.04 LTS** (CIS Benchmark). Suitable for playbooks, Packer/Ansible provisioners, and golden-image pipelines. Search keywords: `ansible`, `ansible-role`, `cis`, `cis-benchmark`, `cis-hardening`, `compliance`, `devsecops`, `hardening`, `infrastructure`, `noble`, `openscap`, `security`, `stigforge`, `ubuntu`.

StigForge-exported Ansible role **`ubuntu24_cis`** · release **`0.3.0`**.
Matrix cell status: **`green`**.

## Install (Ansible Galaxy)

This repository root **is** the Ansible role (Galaxy-style layout). OpenSCAP evidence
lives under `compliance/` and is not loaded when the role runs.

From **Ansible Galaxy** (after import; namespace `stigready`):

```bash
ansible-galaxy role install stigready.ubuntu24_cis,0.3.0
```

From **GitHub** (public):

```yaml
# requirements.yml
roles:
  - src: https://github.com/stigready/ubuntu24-cis
    scm: git
    version: v0.3.0   # or an immutable commit SHA
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
| `cis-l1` | **99.28%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260912T134404Z |
| `cis-l2` | **99.29%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260912T134628Z |
| `cis-ws-l1` | **99.26%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260912T134801Z |
| `cis-ws-l2` | **99.28%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260912T135023Z |

Full artifacts per profile: `compliance/releases/0.3.0/<profile>/` (`score.json`, `results.xml`, `arf.xml`, `evidence.json`, `evidence-report.html`, `poam.md`).

## Reports & review

- **[REVIEW.md](REVIEW.md)** — linked evidence index for product owner review
- **[reports/index.html](reports/index.html)** — HTML report index
- **[CHANGELOG.md](CHANGELOG.md)** — release notes and verify summary

## Verify the score (customer)

Re-run OpenSCAP in Docker and compare to this release's evidence:

```bash
make prove RELEASE=0.3.0
```

Or score your own `results.xml`: see **[compliance/README.md](compliance/README.md)**.

## License

- **[LICENSE](LICENSE)** (MIT) — StigForge export packaging
- **[NOTICE](NOTICE)** — ComplianceAsCode / BSD-3-Clause task body attribution

## Factory

- Monorepo: [stigready/stigforge](https://github.com/stigready/stigforge) @ `562a1f7c1a8e19235ee26e972174d1be6c88998c`
- CI run: https://github.com/stigready/stigforge/actions/runs/34693316989
- Catalog: [https://stigready.com/#stigforge](https://stigready.com/#stigforge)


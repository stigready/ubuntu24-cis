# stigready/ubuntu24-cis

StigForge-exported Ansible role **`ubuntu24_cis`** · release **`0.2.1-private-review`**.
Matrix cell status: **`green`**.

## Install (Ansible Galaxy)

This repository root **is** the Ansible role (Galaxy-style layout). OpenSCAP evidence
lives under `compliance/` and is not loaded when the role runs.

```yaml
# requirements.yml
roles:
  - src: https://github.com/stigready/ubuntu24-cis
    scm: git
    version: v0.2.1-private-review   # or an immutable commit SHA
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
| `cis-l1` | **88.17%** ✗ | 90.0% | FAIL ✗ | rc 2 | 20260726T135932Z |
| `cis-l2` | **87.36%** ✗ | 90.0% | FAIL ✗ | rc 2 | 20260726T135941Z |

Full artifacts per profile: `compliance/releases/0.2.1-private-review/<profile>/` (`score.json`, `results.xml`, `report.html`, `evidence.json`, `evidence-report.html`, `poam.md`).

## Reports & review

- **[REVIEW.md](REVIEW.md)** — linked evidence index for product owner review
- **[reports/index.html](reports/index.html)** — HTML report index
- **[CHANGELOG.md](CHANGELOG.md)** — release notes and verify summary

## License

- **[LICENSE](LICENSE)** (MIT) — StigForge export packaging
- **[NOTICE](NOTICE)** — ComplianceAsCode / BSD-3-Clause task body attribution

## Factory

- Monorepo: [stigready/stigforge](https://github.com/stigready/stigforge) @ `ccc5f55bd24b1c9cb1b8ca95a70b55443e0064b5`
- CI run: https://github.com/stigready/stigforge/actions/runs/30277229616
- Catalog: [https://stigready.com/#stigforge](https://stigready.com/#stigforge)


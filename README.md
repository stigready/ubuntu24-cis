# stigready/ubuntu24-cis

StigForge-exported Ansible role **`ubuntu24_cis`** · release **`0.2.2-private-review`**.
Matrix cell status: **`green`**.

## Install (Ansible Galaxy)

This repository root **is** the Ansible role (Galaxy-style layout). OpenSCAP evidence
lives under `compliance/` and is not loaded when the role runs.

From **Ansible Galaxy** (after import; namespace `stigready`):

```bash
ansible-galaxy role install stigready.ubuntu24_cis,0.2.2-private-review
```

From **GitHub** (private or public):

```yaml
# requirements.yml
roles:
  - src: https://github.com/stigready/ubuntu24-cis
    scm: git
    version: v0.2.2-private-review   # or an immutable commit SHA
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
| `cis-l1` | **95.0%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260728T093616Z |
| `cis-l2` | **94.05%** ✓ | 90.0% | PASS ✓ | rc 0 | 20260728T093804Z |

Full artifacts per profile: `compliance/releases/0.2.2-private-review/<profile>/` (`score.json`, `results.xml`, `report.html`, `evidence.json`, `evidence-report.html`, `poam.md`).

## Reports & review

- **[REVIEW.md](REVIEW.md)** — linked evidence index for product owner review
- **[reports/index.html](reports/index.html)** — HTML report index
- **[CHANGELOG.md](CHANGELOG.md)** — release notes and verify summary

## Verify the score (customer)

Re-run OpenSCAP in Docker and compare to this release's evidence:

```bash
make prove RELEASE=0.2.2-private-review
```

Or score your own `results.xml`: see **[compliance/README.md](compliance/README.md)**.

## License

- **[LICENSE](LICENSE)** (MIT) — StigForge export packaging
- **[NOTICE](NOTICE)** — ComplianceAsCode / BSD-3-Clause task body attribution

## Factory

- Monorepo: [stigready/stigforge](https://github.com/stigready/stigforge) @ `49f1c019fbf7ba7f8edc345d79321ed45f9534de`
- CI run: https://github.com/stigready/stigforge/actions/runs/30348467615
- Catalog: [https://stigready.com/#stigforge](https://stigready.com/#stigforge)


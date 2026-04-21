# Curriculum: Biomedical Materials Informatics

> Learning roadmap for deep learning applied to biomedical biomaterials informatics. Home of the [`deepbiomat`](https://github.com/deepbiomat) project repos.

**Status:** `v0.1.0` (scaffold complete; see [`CHANGELOG.md`](./CHANGELOG.md))
**GitHub org:** [`deepbiomat`](https://github.com/deepbiomat) (locked 2026-04-21)
**License:** `CC-BY-4.0` (locked 2026-04-21 — open educational content; attribution-only).

---

## North Star

Be able to independently produce reproducible, citable work at the intersection of biomaterials and machine learning — at a level where an upstream PR to `pymatgen`, `matminer`, or `DeepChem` would be reviewed on technical merit, not gatekept by lack of credentials.

## Non-Goals

- This is **not** a software project. It produces understanding, not a binary.
- This is **not** a credential substitute. It is a credential **generator** — by feeding the four project repos (P1–P4) that serve as the public track record.
- This is **not** a survey of the field. It is a directed path with explicit prerequisites and stopping criteria.

## The Four Layers

| Layer | Domain | Primary anchor |
|---|---|---|
| **L1** Foundations | Linear algebra, probability, ODEs, biochem, continuum/solid mechanics | MIT OCW (BE/2.797, 3.024) |
| **L2** Biomaterials canonical | Materials in medicine: polymers, ceramics, metals, composites, host response | Ratner et al., *Biomaterials Science* (Academic Press) |
| **L3** Computational + ML for materials/molecules | Featurization, GNNs, regression on materials properties; uncertainty quantification (calibration, conformal, Bayesian) | White, *Deep Learning for Molecules and Materials* (dmol.pub); Materials Project Workshop |
| **L4** Bridge to medicine | Linking material properties to clinical/biological outcomes; multi-omics integration framing (genomics / proteomics / metabolomics × materials descriptors) | PyHealth, MONAI, MIMIC-IV; nanoHUB |

Layers may run in parallel, but project repos (P1–P4) only open once their prerequisite layers are at the required maturity. See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the dependency rules.

## Versioning Philosophy

This repo is SemVer'd against **epistemic milestones**, not software releases:

- `v0.x.0` — layer *x* foundations covered (one bump per layer)
- `v0.x.y` — sub-progress within a layer (notes, summaries, exercises completed)
- `v1.0.0` — all four layers at "can produce work" maturity, validated by at least one merged upstream PR or accepted preprint from the project repos

Versions never go backward. If understanding is revised, the new version supersedes — old commits remain in history.

## How to Use

1. Read [`ARCHITECTURE.md`](./ARCHITECTURE.md) to understand layer progression and evaluation criteria.
2. Read [`TODO.md`](./TODO.md) to see atomic tasks and current cursor.
3. Notes live in `notes/L{1..4}/` (created at each layer's v0.x.0).
4. Project repos consume this curriculum's outputs as inputs — see the dependency diagram below.

## Relationship to Project Repos

All project repos live under the [`deepbiomat`](https://github.com/deepbiomat) GitHub org.

```
curriculum (this repo — deepbiomat/curriculum)
    │
    ├─→ P1: deepbiomat/deepbiomat-repro       (needs L1, L3 ≥ v0.3)
    ├─→ P2: deepbiomat/deepbiomat-features    (needs L2, L3 ≥ v0.4)
    ├─→ P3: deepbiomat/deepbiomat-bench       (needs P1 + P2 + L3 complete)
    └─→ P4: deepbiomat/deepbiomat-rs          (needs P1–P3 + Rust fluency, separate track)
```

## Resources (Verified)

- Andrew White, *Deep Learning for Molecules and Materials*, Living J. Comp. Mol. Sci. 3(1):1499 (2022). Free at https://dmol.pub
- `pymatgen` — https://pymatgen.org
- `matminer` — https://hackingmaterials.lbl.gov/matminer/
- `DeepChem` — https://deepchem.io
- Materials Project Workshop — https://workshop.materialsproject.org
- Ratner, Hoffman, Schoen, Lemons (eds.), *Biomaterials Science: An Introduction to Materials in Medicine*, Academic Press (current edition)
- MIT OpenCourseWare — https://ocw.mit.edu

Additional resources are vetted and added in [`TODO.md`](./TODO.md) under the relevant layer.

## Conventions

- Notes in Markdown, source-of-truth for understanding.
- Citations follow APA 7 in notes; BibTeX entries in `references.bib` (created at v0.1.0).
- Commits follow Conventional Commits (`docs:`, `notes:`, `chore:`).
- One PR per atomic task in `TODO.md`.

---

## License

© 2026 Deepbiomat. This work is licensed under a [Creative Commons Attribution 4.0 International License](LICENSE).


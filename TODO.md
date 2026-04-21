# TODO: Curriculum

> Atomic tasks in tasks/subtasks form. Bind each to a SemVer milestone. Check off only with linked commit/PR.

**Cursor:** `v0.0.5` (pre-scaffold, no work started; curriculum retitled — see [`CHANGELOG.md`](./CHANGELOG.md))

---

## v0.1.0 — Scaffold

- [ ] **0.1** Add LICENSE *(locked in v0.0.2: `CC-BY-4.0`)*
  - [ ] 0.1.1 Add `LICENSE` file with the canonical CC-BY-4.0 legal code (from creativecommons.org)
  - [ ] 0.1.2 Add license note + copyright line in `README.md` footer
- [ ] **0.2** Create file structure per `ARCHITECTURE.md` §1
  - [ ] 0.2.1 Create `notes/L{1..4}/` dirs with empty `README.md` placeholders
  - [ ] 0.2.2 Create `exercises/L{1..4}/` dirs
  - [ ] 0.2.3 Create `reviews/` dir
  - [ ] 0.2.4 Create empty `references.bib`
  - [ ] 0.2.5 Create `CHANGELOG.md` per Keep a Changelog
- [ ] **0.3** Repo hygiene
  - [ ] 0.3.1 `.gitignore` (Python, OS, editor)
  - [ ] 0.3.2 `.editorconfig`
  - [ ] 0.3.3 Conventional Commits config
  - [ ] 0.3.4 Optional: pre-commit with `markdownlint` + link-check
- [ ] **0.4** Tag `v0.1.0`

## v0.2.0 — L1 Foundations Complete

- [ ] **1.1** Linear algebra
  - [ ] 1.1.1 Vector spaces, bases, change of basis (notes)
  - [ ] 1.1.2 Eigendecomposition + SVD (notes + exercise)
  - [ ] 1.1.3 Matrix calculus (notes + 5 derived gradients exercise)
- [ ] **1.2** Probability
  - [ ] 1.2.1 Conditional probability + Bayes (notes)
  - [ ] 1.2.2 MLE vs MAP (notes + worked example)
  - [ ] 1.2.3 Common distributions (notes + sampling exercise)
- [ ] **1.3** ODEs/PDEs
  - [ ] 1.3.1 Linear ODEs, separation of variables (notes)
  - [ ] 1.3.2 Heat/diffusion equation intuition (notes)
- [ ] **1.4** Biochemistry
  - [ ] 1.4.1 Central dogma + protein structure (notes)
  - [ ] 1.4.2 Enzymes + binding kinetics (notes)
- [ ] **1.5** Continuum / solid mechanics
  - [ ] 1.5.1 Stress/strain tensors (notes)
  - [ ] 1.5.2 Linear elasticity, Hooke's law in tensor form (notes)
  - [ ] 1.5.3 Sketch + explain stress-strain curves: polymer vs ceramic vs metal (exercise)
- [ ] **1.6** L1 exit gate
  - [ ] 1.6.1 Self-written 5-question test answered without notes
  - [ ] 1.6.2 `notes/L1-foundations/teachback.md`
  - [ ] 1.6.3 `notes/L1-foundations/things-i-got-wrong.md` (non-empty)
  - [ ] 1.6.4 `reviews/YYYY-MM-DD-L1-exit.md`
- [ ] **1.7** Tag `v0.2.0`

## v0.3.0 — L2 Biomaterials Canonical Complete

- [ ] **2.1** Class taxonomy
  - [ ] 2.1.1 Synthetic polymers (PLA, PGA, PCL, PEG, PEEK) — notes
  - [ ] 2.1.2 Bioceramics (HA, TCP, bioactive glass) — notes
  - [ ] 2.1.3 Metallic implants (Ti alloys, CoCr, Mg) — notes
  - [ ] 2.1.4 Composites + hydrogels — notes
- [ ] **2.2** Surface + interface
  - [ ] 2.2.1 Surface modification techniques (notes)
  - [ ] 2.2.2 Protein adsorption (Vroman effect) — notes
- [ ] **2.3** Biological response
  - [ ] 2.3.1 Foreign body response cascade (notes)
  - [ ] 2.3.2 ISO 10993 framework overview (notes)
- [ ] **2.4** Degradation + drug delivery
  - [ ] 2.4.1 Hydrolytic vs enzymatic degradation (notes)
  - [ ] 2.4.2 Higuchi + zero-order release models (notes + exercise)
- [ ] **2.5** Tissue engineering scaffolds
  - [ ] 2.5.1 Porosity, mechanical match, vascularization (notes)
- [ ] **2.6** L2 exit gate (test, teach-back, failures, review)
- [ ] **2.7** Tag `v0.3.0`

## v0.4.0 — L3 Computational + ML Complete

- [ ] **3.1** Classical ML refresher
  - [ ] 3.1.1 Train/val/test, leakage, CV (notes)
  - [ ] 3.1.2 Linear/logistic regression, RF, GBM (notes + scikit-learn notebook)
- [ ] **3.2** Materials featurization (matminer)
  - [ ] 3.2.1 Composition featurizers (notes + notebook)
  - [ ] 3.2.2 Structure featurizers (notes + notebook)
  - [ ] 3.2.3 DOS/band-structure featurizers (notes)
- [ ] **3.3** Deep learning core (dmol.pub Sections A–C)
  - [ ] 3.3.1 Math review chapter (notes + exercises)
  - [ ] 3.3.2 ML chapter (notes)
  - [ ] 3.3.3 DL principles + standard architectures (notes)
  - [ ] 3.3.4 Graph neural networks chapter (notes + reimplementation exercise)
- [ ] **3.4** Materials applications (dmol.pub Section D)
  - [ ] 3.4.1 Walk through worked examples (notebooks)
- [ ] **3.5** Materials Project Workshop
  - [ ] 3.5.1 Complete the matminer ML lesson
  - [ ] 3.5.2 Complete the pymatgen lessons
- [ ] **3.6** Capstone exercise
  - [ ] 3.6.1 Train a baseline GNN on a Matbench task (any) — beat random forest
- [ ] **3.7** Uncertainty quantification *(added in v0.0.1)*
  - [ ] 3.7.1 Calibration: reliability diagrams, ECE, temperature scaling (notes + notebook)
  - [ ] 3.7.2 Conformal prediction: split-conformal for regression and classification (notes + notebook)
  - [ ] 3.7.3 Bayesian DL primer: MC dropout, deep ensembles (notes + notebook)
  - [ ] 3.7.4 Apply UQ method to the v0.4.0 capstone GNN; verify calibration empirically
- [ ] **3.8** L3 exit gate *(was 3.7 in v0.0.0)*
- [ ] **3.9** Tag `v0.4.0` — **P1 + P2 may now begin** *(was 3.8 in v0.0.0)*

## v0.5.0 — L4 Bridge to Medicine Complete

- [ ] **4.1** Clinical data sources
  - [ ] 4.1.1 MIMIC-IV access + schema overview (notes)
  - [ ] 4.1.2 Medical device registries landscape (notes)
- [ ] **4.2** Imaging pipelines
  - [ ] 4.2.1 MONAI tutorial walkthrough (notebook)
- [ ] **4.3** Outcome modeling
  - [ ] 4.3.1 PyHealth task taxonomy (notes)
  - [ ] 4.3.2 Endpoint definition: hard vs surrogate (notes)
- [ ] **4.4** Regulatory framing
  - [ ] 4.4.1 FDA 510(k) basics (notes)
  - [ ] 4.4.2 ISO 10993 deep dive (notes)
- [ ] **4.5** Multi-omics integration framing *(added in v0.0.1)*
  - [ ] 4.5.1 Vocabulary: genomics, transcriptomics, proteomics, metabolomics (notes)
  - [ ] 4.5.2 How omics data is shaped (high-dim, sparse, batch effects) — notes
  - [ ] 4.5.3 Joint modeling pattern: omics + materials descriptors as concatenated/fused inputs (notes + sketch)
  - [ ] 4.5.4 Map: which clinical-outcome problems are improved by adding which omics modality (essay)
- [ ] **4.6** Synthesis *(was 4.5 in v0.0.0)*
  - [ ] 4.6.1 Frame one biomaterial problem with a clinical loss function (essay)
- [ ] **4.7** L4 exit gate *(was 4.6 in v0.0.0)*
- [ ] **4.8** Tag `v0.5.0` *(was 4.7 in v0.0.0)*

## v1.0.0 — Curriculum Mature

- [ ] **5.1** All four layers at exit gate
- [ ] **5.2** At least one merged upstream PR (pymatgen / matminer / DeepChem) from project work
- [ ] **5.3** At least one preprint posted (arXiv or Zenodo) from P3
- [ ] **5.4** Final review document `reviews/YYYY-MM-DD-v1.0-curriculum-mature.md`
- [ ] **5.5** Tag `v1.0.0`

---

## Backlog (Unscheduled)

- [ ] Add Bayesian/active learning subsection if needed for P3
- [ ] Add equivariant neural networks (e.g., e3nn) if needed for P4
- [ ] Add basic FEM if a project requires structural simulation

## Open Questions

(Maintained as `notes/L{n}/open-questions.md` per layer; ledger here when cross-cutting)

- _none yet_

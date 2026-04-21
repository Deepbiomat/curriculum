# Architecture: Curriculum

> Structural design of the learning system. Not software architecture — *learning* architecture.

## 1. Top-Level Structure

```
curriculum/
├── README.md
├── ARCHITECTURE.md          ← this file
├── TODO.md
├── LICENSE                  ← CC-BY-4.0
├── CHANGELOG.md             ← Keep a Changelog format
├── references.bib           ← BibTeX, single source of citation truth
├── notes/
│   ├── L1-foundations/
│   ├── L2-biomaterials/
│   ├── L3-computational/
│   └── L4-bridge-medicine/
├── exercises/
│   ├── L1/                  ← worked problems, derivations
│   ├── L2/                  ← case studies, material selection problems
│   ├── L3/                  ← Jupyter notebooks (uv-managed)
│   └── L4/                  ← clinical-outcome linkage exercises
└── reviews/
    └── YYYY-MM-DD-*.md      ← periodic self-review snapshots
```

## 2. The Four Layers

### L1 — Foundations
**Purpose:** mathematical and physical machinery required to read everything downstream.
**Coverage:** linear algebra (through SVD), probability (through Bayes + MLE/MAP), ODEs/PDEs (basic), biochem (central dogma + protein structure), continuum mechanics (stress/strain tensors, basic FEM intuition).
**Exit criterion:** can derive backprop from scratch, can read a paper using tensor notation without re-learning notation, can sketch a stress-strain curve for a polymer vs. a ceramic and explain the difference mechanistically.

### L2 — Biomaterials Canonical
**Purpose:** vocabulary, taxonomy, and engineering tradeoffs of materials used in medicine.
**Coverage:** synthetic polymers, bioceramics, metallic implants, composites, surface modification, host response (FBR), degradation, drug delivery carriers, tissue engineering scaffolds.
**Exit criterion:** can read a biomaterials paper and identify the material class, the failure modes the authors are mitigating, and the standard characterization techniques used.

### L3 — Computational + ML for Materials/Molecules
**Purpose:** the actual technical core of the bridge.
**Coverage:** classical ML (scikit-learn baselines), featurization (compositional, structural, electronic via `matminer`), graph neural nets (CGCNN, MEGNet, equivariant nets), generative models for molecules (basic), Bayesian/active learning for design, uncertainty quantification (model calibration, conformal prediction, Bayesian deep learning).
**Exit criterion:** can independently train a GNN on a `Matbench` task and beat the random-forest baseline; can write a `matminer`-compatible featurizer; can produce calibrated uncertainty estimates for predictions and verify calibration empirically.

### L4 — Bridge to Medicine
**Purpose:** the differentiating layer — linking material properties to clinical/biological outcomes.
**Coverage:** clinical data sources (MIMIC-IV, registries), medical imaging pipelines (MONAI), outcome modeling (PyHealth tasks), regulatory framing (FDA 510(k) basics, ISO 10993), multi-omics integration framing (genomics, proteomics, metabolomics as joint inputs alongside materials descriptors).
**Exit criterion:** can frame a biomaterial design problem with a clinical endpoint as the loss function.

## 3. Progression Rules

1. **Strict prerequisite:** L1 must reach `v0.1.x` before L3 can start.
2. **Parallel allowed:** L2 and L3 may proceed concurrently after L1 ≥ `v0.1.x`.
3. **L4 is gated:** L4 cannot start until L2 ≥ `v0.x.0` (taxonomy) and L3 ≥ `v0.x.0` (modeling baseline).
4. **No skipping:** if a downstream concept is encountered without its prerequisite, halt and patch the gap.
5. **No abandoning:** a layer cannot be marked complete with open questions in its `notes/L{n}/open-questions.md`.

## 4. Evaluation Criteria

Each layer's exit is gated by a self-review document in `reviews/`:

- **Written test (open-book):** 5 questions you write yourself before starting the layer, answered without notes after.
- **Teach-back:** a `notes/L{n}/teachback.md` explaining the layer to an imagined reader at the level just below yours.
- **Artifact:** at least one exercise notebook or worked problem set.
- **Failure log:** `notes/L{n}/things-i-got-wrong.md` — non-empty by design.

A layer with no failure log is suspect and triggers re-review.

## 5. Feedback Loop with Project Repos

```
                    ┌──────────────────────────┐
                    │      curriculum repo     │
                    │                          │
   exit criteria ───┤  L1 → L2 → L3 → L4       │
                    └────────┬─────────────────┘
                             │ unlocks
                             ▼
        ┌────────────────────────────────────────┐
        │ P1 → P2 → P3 → P4  (project repos)     │
        └────────┬───────────────────────────────┘
                 │
   gaps observed │ feeds back as
   during build  ▼ TODO entries
                    ┌──────────────────────────┐
                    │  curriculum/TODO.md      │
                    └──────────────────────────┘
```

Building the projects is the highest-fidelity test of the curriculum. Anything that blocks a project becomes a curriculum task.

## 6. Knowledge Artifacts Produced

- **Notes** — Markdown, hand-written synthesis, never copy-paste.
- **References** — `references.bib`, every cited work with DOI.
- **Exercises** — runnable where possible (`exercises/L3/` uses `uv` for env mgmt).
- **Teach-backs** — exit-gate documents per layer.
- **Open questions** — `open-questions.md` per layer; ledger of known unknowns.

## 7. Toolchain

- **Markdown editor:** any (no lock-in).
- **Notebook env (L3, L4):** Python via `uv`, latest stable interpreter.
- **Diagram source:** Mermaid (rendered by GitHub) or plain ASCII.
- **CI (optional):** GitHub Actions running `markdownlint` and link-check on PR.

## 8. Anti-Patterns to Refuse

- **Tutorial completionism** — finishing a course is not understanding.
- **Bookmark hoarding** — every added resource must be tied to a TODO task.
- **Layer ping-pong** — switching layers without exit-criteria progress is procrastination.
- **Note bloat** — notes over ~500 lines per topic must be split or summarized.
- **Synonym worship** — copying terminology without re-deriving the concept.

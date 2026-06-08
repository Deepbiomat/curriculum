# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

This is **not a software project** — it produces educational understanding in biomedical materials informatics. The curriculum is structured as four progressive layers (L1–L4) that build from mathematical foundations through computational ML to clinical-outcome linkage.

**North Star:** Develop independent capability to produce reproducible, citable work at the intersection of biomaterials and machine learning — at a level where an upstream PR to `pymatgen`, `matminer`, or `DeepChem` would be reviewed on technical merit.

---

## Structure & Conventions

### File Organization

```
curriculum/
├── notes/L{1..4}/          # Layer-specific notes (Markdown, hand-written)
├── exercises/L{1..4}/      # Worked problems, notebooks, case studies
├── reviews/                # Layer exit-gate self-review snapshots
├── references.bib          # Single source of truth for citations (BibTeX)
├── TODO.md                 # Atomic tasks bound to SemVer milestones
└── CHANGELOG.md            # Keep a Changelog format
```

### Commit Convention

@.claude/rules/commit-convention.md

**Key point:** No `Co-Authored-By:` trailers — commit attribution stays with the human author.

### Language Requirement

@.claude/rules/language-requirement.md

All Plans.md content and harness output must be in English only.

### Citation Management

- **Single source of truth:** `references.bib`
- **Format:** BibTeX with DOI for every entry
- **In notes:** Use APA 7 style; cite with `[Author, Year]` (GitHub markdown)
- **When to update:** Every cited work must have a BibTeX entry before the commit

### Note Structure (Per Layer)

- `notes/L{n}/README.md` — index and topics covered
- `notes/L{n}/*.md` — one file per major concept
- `notes/L{n}/open-questions.md` — ledger of known unknowns (required, non-empty)
- `notes/L{n}/teachback.md` — exit-gate artifact explaining layer to reader one level below
- `notes/L{n}/things-i-got-wrong.md` — failure log (required at exit, non-empty)

### Exercise Structure (Per Layer)

- `exercises/L1/` — worked derivations, PDF/Markdown
- `exercises/L2/` — case studies, material selection problems
- `exercises/L3/` — Jupyter notebooks with Python environments (via `uv`)
- `exercises/L4/` — clinical-outcome linkage exercises

L3/L4 exercises are runnable:
```bash
cd exercises/L3
uv sync                  # Install dependencies
uv run jupyter notebook  # or: uv run python script.py
```

---

## Layer Progression Rules

@.claude/rules/layer-progression.md

**Critical:** These rules gate project repo unlocks — violations delay all downstream work.

---

## Working with Notes

### Guidelines

- **Hand-written synthesis:** Never copy-paste from sources; re-derive or summarize in your own words.
- **No bloat:** One topic per file; if >500 lines, split into subtopics.
- **Re-derivation over synonyms:** Terminology is copied content until you've re-derived the concept.
- **Interdependency:** Link concepts explicitly (use Markdown links to related notes).

### Before Starting a Topic

1. Add an empty subtask to `TODO.md` under the appropriate layer milestone.
2. If the topic requires reading a paper, add a BibTeX entry to `references.bib` first (include DOI).
3. Draft an outline: what does the reader need to understand *before* this topic?

### When Committing Notes

- Title: `notes(l{n}): concise topic name`
- Link the atomic TODO task in the PR description
- Include 1–2 sentences on what was added and why

---

## Working with Exercises

### Python Environments (L3 + L4)

All Python work uses `uv` for deterministic, reproducible environments.

**See @.claude/rules/workflows.md for examples.**

Do **not** commit `.venv/`, `__pycache__/`, or `*.ipynb_checkpoints/` (covered by `.gitignore`).

### Exercise Validation

An exercise is "done" when:
1. The code runs without errors in a fresh environment (`uv sync && uv run ...`)
2. All derivations or worked steps are shown (not just the answer)
3. At least one non-trivial case is worked through

---

## Layer Exit Gates (Self-Review)

Each layer's completion is validated by these **non-negotiable** artifacts:

1. **Written test (open-book answer key):** 5 questions you write *before* starting the layer, answered *without* notes after. Place in `reviews/YYYY-MM-DD-L{n}-exit.md`.
2. **Teach-back:** `notes/L{n}/teachback.md` — explain the layer to someone at the level just below yours.
3. **Artifact:** At least one exercise notebook or worked problem set.
4. **Failure log:** `notes/L{n}/things-i-got-wrong.md` — **must be non-empty** (a layer with no mistakes is suspect).

Only when all four are present and non-trivial can the layer be marked complete in `TODO.md`.

---

## SemVer Milestones

Versions are bound to **epistemic milestones**, not software releases:

- `v0.1.0` — Scaffold complete (structure, LICENSE, CI hygiene)
- `v0.2.0` — L1 complete (linear algebra, probability, ODEs, biochem, mechanics)
- `v0.3.0` — L2 complete (biomaterials taxonomy and engineering)
- `v0.4.0` — L3 complete (computational + ML) — **P1 + P2 unlock**
- `v0.5.0` — L4 complete (clinical-outcome linkage) — **P3 + P4 unlock**
- `v1.0.0` — All layers mature, validated by upstream contributions

Versions **never go backward**. If understanding is revised, the new version supersedes; old commits remain in history.

---

## Anti-Patterns to Refuse

@.claude/rules/anti-patterns.md

---

## Common Workflows

@.claude/rules/workflows.md

---

## References & Resources

- **ARCHITECTURE.md** — learning structure and progression rules (read first)
- **TODO.md** — atomic tasks and current cursor (check before starting work)
- **references.bib** — keep it organized; every citation needs a DOI
- **Keep a Changelog** — https://keepachangelog.com/ (format for CHANGELOG.md)
- **Conventional Commits** — https://www.conventionalcommits.org/ (commit schema)

---

## Project Dependencies (Information Only)

The four layers feed into four project repos, all under the [`deepbiomat`](https://github.com/deepbiomat) GitHub org:

- **P1** (`deepbiomat-repro`) — needs L1, L3 ≥ v0.3
- **P2** (`deepbiomat-features`) — needs L2, L3 ≥ v0.4
- **P3** (`deepbiomat-bench`) — needs P1 + P2 + L3 complete
- **P4** (`deepbiomat-rs`) — needs P1–P3 + Rust fluency (separate track)

Building these projects is the highest-fidelity test of the curriculum. Gaps observed during project work feed back as TODO entries.

# Deepbiomat Curriculum Plans.md

Created: 2026-06-08

---

## Phase 1: L1 Linear Algebra & Probability (Complete)

| Task | Content | DoD | Depends | Status |
|------|---------|-----|---------|--------|
| 1.1.1 | Vector spaces, bases, change of basis (notes) | notes/L1-foundations/linear-algebra.md exists | - | cc:done |
| 1.1.2 | Linear transformations, rank, nullity, four fundamental subspaces (notes) | notes/L1-foundations/linear-algebra.md covers linear transformations, rank, nullity, four subspaces with examples | 1.1.1 | cc:done |
| 1.1.3 | Orthogonality: projections, Gram-Schmidt, QR decomposition (notes) | notes/L1-foundations/linear-algebra.md explains orthogonality, derives Gram-Schmidt, explains QR decomposition | 1.1.2 | cc:done |
| 1.1.4 | Eigendecomposition + SVD (notes + exercise) | exercises/L1/eigendecomposition.md works without errors | 1.1.3 | cc:done |
| 1.1.5 | Matrix calculus (notes + 5 derived gradients exercise) | 5 gradients correctly derived in exercise | 1.1.4 | cc:done |
| 1.1.6 | Tensor notation: index notation, Einstein summation (notes) | notes/L1-foundations/tensor-notation.md complete | 1.1.5 | cc:done |
| 1.1.7 | Derive backpropagation from scratch (exercise) | exercises/L1/backprop-derivation.md runs, derivation complete | 1.1.6 | cc:done |
| 1.2.1 | Conditional probability + Bayes (notes) | notes/L1-foundations/probability.md covers both | - | cc:done |
| 1.2.2 | MLE vs MAP (notes + worked example) | notes/L1-foundations/probability.md includes worked example demonstrating MLE vs MAP | 1.2.1 | cc:done |
| 1.2.3 | Common distributions (notes + sampling exercise) | exercises/L1/sampling.md runs, distributions sampled | 1.2.2 | cc:done |

## Phase 2: L1 ODEs & Biochemistry

| Task | Content | DoD | Depends | Status |
|------|---------|-----|---------|--------|
| 1.3.1 | Linear ODEs, separation of variables (notes) [tdd:skip:notes-only] | notes/L1-foundations/odes.md exists, separation of variables explained with examples | Phase 1 | cc:done [90142fc] |
| 1.3.2 | Heat/diffusion equation intuition (notes) [tdd:skip:notes-only] | notes/L1-foundations/pdes.md explains heat equation, intuition clear | 1.3.1 | cc:todo |
| 1.4.1 | Central dogma + protein structure (notes) [tdd:skip:notes-only] | notes/L1-foundations/biochem.md covers central dogma and protein tertiary structure | Phase 1 | cc:todo |
| 1.4.2 | Enzymes + binding kinetics (notes) [tdd:skip:notes-only] | notes content explains enzyme kinetics and Michaelis-Menten | 1.4.1 | cc:todo |

## Phase 3: L1 Continuum & Solid Mechanics

| Task | Content | DoD | Depends | Status |
|------|---------|-----|---------|--------|
| 1.5.1 | Stress/strain tensors (notes) [tdd:skip:notes-only] | notes/L1-foundations/mechanics.md defines stress and strain tensors with index notation | Phase 2 | cc:todo |
| 1.5.2 | Linear elasticity, Hooke's law in tensor form (notes) [tdd:skip:notes-only] | Hooke's law written in tensor notation, linear elasticity explained | 1.5.1 | cc:todo |
| 1.5.3 | Sketch + explain stress-strain curves (exercise) | exercises/L1/stress-strain.md compares polymer vs ceramic vs metal with explanations | 1.5.2 | cc:todo |

## Phase 4: L1 Exit Gate

| Task | Content | DoD | Depends | Status |
|------|---------|-----|---------|--------|
| 1.6.1 | Self-written 5-question test answered without notes [tdd:skip:notes-only] | reviews/YYYY-MM-DD-L1-exit.md contains 5 questions and answers | Phase 3 | cc:todo |
| 1.6.2 | Teach-back document [tdd:skip:notes-only] | notes/L1-foundations/teachback.md explains L1 to reader one level below | 1.6.1 | cc:todo |
| 1.6.3 | Failure log (non-empty) [tdd:skip:notes-only] | notes/L1-foundations/things-i-got-wrong.md exists with at least 3 real failures | 1.6.1 | cc:todo |
| 1.6.4 | Exit review document [tdd:skip:notes-only] | reviews/YYYY-MM-DD-L1-exit.md completed with all 4 artifacts | 1.6.2, 1.6.3 | cc:todo |
| 1.7 | Tag v0.2.0 | git tag v0.2.0 created and pushed | 1.6.4 | cc:todo |

# Exercise 1.2: SVD Verification

Covers notes 04 (eigendecomposition and SVD).

---

## Problem 1 — Eigendecomposition

Given $A = \begin{bmatrix} 4 & 1 \\ 2 & 3 \end{bmatrix}$:

**Tasks:**
1. Find eigenvalues via characteristic polynomial
2. Find eigenvectors for each eigenvalue
3. Construct $P$ and $D$ such that $A = PDP^{-1}$
4. Verify by computing $PDP^{-1}$ explicitly
5. Compute $A^3$ using the decomposition

---

## Problem 2 — Symmetric Matrix Eigendecomposition

Given $A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$:

**Tasks:**
1. Find eigenvalues and eigenvectors
2. Verify eigenvectors are orthogonal
3. Construct orthogonal $Q$ and verify $A = QDQ^T$
4. Explain why orthogonality is guaranteed

---

## Problem 3 — Full SVD Computation

Given $A = \begin{bmatrix} 1 & 1 \\ 0 & 1 \\ 1 & 0 \end{bmatrix}$:

**Tasks:**
1. Compute $A^TA$ and find its eigenvalues/eigenvectors → $V$, $\sigma_i$
2. Compute $AA^T$ and find its eigenvalues/eigenvectors → $U$
3. Construct $\Sigma$
4. Verify $A = U\Sigma V^T$
5. Compute the best rank-1 approximation $A_1$
6. Compute $\|A - A_1\|_F$ and verify it equals $\sigma_2$

---

## Problem 4 — SVD and the Four Subspaces

Using the SVD from Problem 3:

**Tasks:**
1. Identify an orthonormal basis for each of the four fundamental subspaces from the SVD factors
2. Verify the dimension of each subspace matches the rank
3. Verify orthogonality between paired subspaces

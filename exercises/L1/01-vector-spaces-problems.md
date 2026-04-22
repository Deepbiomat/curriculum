# Exercise 1.1: Vector Spaces, Transformations, Orthogonality

Covers notes 01–03 (vector spaces, linear transformations, orthogonality).

---

## Problem 1 — Linear Independence

Determine whether the following vectors are linearly independent in $\mathbb{R}^3$:

$$\mathbf{v}_1 = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}, \quad \mathbf{v}_2 = \begin{bmatrix} 4 \\ 5 \\ 6 \end{bmatrix}, \quad \mathbf{v}_3 = \begin{bmatrix} 7 \\ 8 \\ 9 \end{bmatrix}$$

**Tasks:**
1. Form the matrix $A = [\mathbf{v}_1 | \mathbf{v}_2 | \mathbf{v}_3]$ and row-reduce
2. Determine rank and nullity
3. If dependent, find the dependency relation

---

## Problem 2 — Change of Basis

Let $\mathcal{B} = \left\{\begin{bmatrix} 1 \\ 1 \end{bmatrix}, \begin{bmatrix} 1 \\ -1 \end{bmatrix}\right\}$ and $\mathcal{S}$ be the standard basis.

**Tasks:**
1. Find $P_{\mathcal{S} \leftarrow \mathcal{B}}$
2. Find $P_{\mathcal{B} \leftarrow \mathcal{S}}$
3. Given $[\mathbf{v}]_{\mathcal{B}} = \begin{bmatrix} 3 \\ 2 \end{bmatrix}$, find $[\mathbf{v}]_{\mathcal{S}}$
4. Verify $P_{\mathcal{S} \leftarrow \mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{S}} = I$

---

## Problem 3 — Four Fundamental Subspaces

Given $A = \begin{bmatrix} 1 & 3 & 5 \\ 2 & 6 & 10 \\ 1 & 3 & 7 \end{bmatrix}$:

**Tasks:**
1. Find rank via row reduction
2. Find basis for column space
3. Find basis for null space
4. Find basis for row space
5. Find basis for left null space
6. Verify: $\text{rank} + \text{nullity} = n$
7. Verify orthogonality: pick one vector from row space and one from null space, confirm their dot product is 0

---

## Problem 4 — Orthogonal Projection

Let $W = \text{span}\left\{\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}, \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}\right\}$ and $\mathbf{b} = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$.

**Tasks:**
1. Apply Gram-Schmidt to obtain an orthonormal basis for $W$
2. Compute $\text{proj}_W(\mathbf{b})$ using the orthonormal basis
3. Compute the residual $\mathbf{r} = \mathbf{b} - \text{proj}_W(\mathbf{b})$
4. Verify $\mathbf{r} \perp W$

---

## Problem 5 — QR Decomposition

Compute the QR decomposition of:

$$A = \begin{bmatrix} 1 & 1 \\ 1 & 0 \\ 0 & 1 \end{bmatrix}$$

**Tasks:**
1. Apply Gram-Schmidt to columns of $A$
2. Construct $Q$ and $R$
3. Verify $A = QR$
4. Use QR to solve the least squares problem $A\mathbf{x} \approx \mathbf{b}$ where $\mathbf{b} = \begin{bmatrix} 2 \\ 1 \\ 1 \end{bmatrix}$

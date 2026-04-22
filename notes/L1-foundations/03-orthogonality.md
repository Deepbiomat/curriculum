# 1.1.3 Orthogonality: Projections, Gram-Schmidt, QR Decomposition

## Inner Products and Orthogonality

The standard **inner product** on $\mathbb{R}^n$:

$$\langle \mathbf{u}, \mathbf{v} \rangle = \mathbf{u}^T\mathbf{v} = \sum_{i=1}^{n} u_i v_i$$

Two vectors are **orthogonal** if $\langle \mathbf{u}, \mathbf{v} \rangle = 0$, written $\mathbf{u} \perp \mathbf{v}$.

### Norms

$$\|\mathbf{v}\| = \sqrt{\langle \mathbf{v}, \mathbf{v} \rangle} = \sqrt{\mathbf{v}^T\mathbf{v}}$$

**Cauchy-Schwarz inequality:** $|\langle \mathbf{u}, \mathbf{v} \rangle| \leq \|\mathbf{u}\| \|\mathbf{v}\|$

### Orthonormal Sets

A set $\{\mathbf{q}_1, \ldots, \mathbf{q}_k\}$ is **orthonormal** if:
$$\langle \mathbf{q}_i, \mathbf{q}_j \rangle = \delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases}$$

An **orthogonal matrix** $Q$ has orthonormal columns: $Q^TQ = I$.

Properties of orthogonal matrices:
- $Q^{-1} = Q^T$ (inversion is free)
- $\|Q\mathbf{x}\| = \|\mathbf{x}\|$ (preserves lengths)
- $\langle Q\mathbf{u}, Q\mathbf{v} \rangle = \langle \mathbf{u}, \mathbf{v} \rangle$ (preserves angles)
- $\det(Q) = \pm 1$

## Orthogonal Projection

### Projection onto a Vector

The projection of $\mathbf{v}$ onto $\mathbf{u}$:

$$\text{proj}_{\mathbf{u}}(\mathbf{v}) = \frac{\langle \mathbf{v}, \mathbf{u} \rangle}{\langle \mathbf{u}, \mathbf{u} \rangle}\mathbf{u} = \frac{\mathbf{u}\mathbf{u}^T}{\mathbf{u}^T\mathbf{u}}\mathbf{v}$$

The **projection matrix** is $P = \frac{\mathbf{u}\mathbf{u}^T}{\mathbf{u}^T\mathbf{u}}$.

Properties of projection matrices:
- $P^2 = P$ (idempotent — projecting twice does nothing)
- $P^T = P$ (symmetric)

### Projection onto a Subspace

For subspace $W$ with orthonormal basis $Q = [\mathbf{q}_1 | \cdots | \mathbf{q}_k]$:

$$\text{proj}_W(\mathbf{v}) = QQ^T\mathbf{v} = \sum_{i=1}^{k} \langle \mathbf{v}, \mathbf{q}_i \rangle \mathbf{q}_i$$

For general (non-orthonormal) basis $A$:

$$\text{proj}_W(\mathbf{v}) = A(A^TA)^{-1}A^T\mathbf{v}$$

### Least Squares Connection

The least squares solution to $A\mathbf{x} = \mathbf{b}$ (overdetermined system) minimizes $\|\mathbf{b} - A\mathbf{x}\|$:

$$\hat{\mathbf{x}} = (A^TA)^{-1}A^T\mathbf{b}$$

This is exactly the projection of $\mathbf{b}$ onto $\text{col}(A)$.

**Residual:** $\mathbf{r} = \mathbf{b} - A\hat{\mathbf{x}} \perp \text{col}(A)$

## Gram-Schmidt Process

Converts any basis $\{\mathbf{v}_1, \ldots, \mathbf{v}_n\}$ to an orthonormal basis $\{\mathbf{q}_1, \ldots, \mathbf{q}_n\}$:

**Algorithm:**
1. $\mathbf{u}_1 = \mathbf{v}_1$, $\quad \mathbf{q}_1 = \mathbf{u}_1 / \|\mathbf{u}_1\|$
2. For $k = 2, \ldots, n$:
   - Subtract projections onto all previous vectors:
     $$\mathbf{u}_k = \mathbf{v}_k - \sum_{j=1}^{k-1} \langle \mathbf{v}_k, \mathbf{q}_j \rangle \mathbf{q}_j$$
   - Normalize: $\mathbf{q}_k = \mathbf{u}_k / \|\mathbf{u}_k\|$

### Worked Example

Orthonormalize $\{\mathbf{v}_1 = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix}, \mathbf{v}_2 = \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}, \mathbf{v}_3 = \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}\}$:

**Step 1:** $\mathbf{q}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix}$

**Step 2:** $\mathbf{u}_2 = \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix} - \frac{1}{2}\begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} = \begin{bmatrix} 1/2 \\ -1/2 \\ 1 \end{bmatrix}$, $\quad \mathbf{q}_2 = \frac{1}{\sqrt{3/2}}\begin{bmatrix} 1/2 \\ -1/2 \\ 1 \end{bmatrix} = \frac{1}{\sqrt{6}}\begin{bmatrix} 1 \\ -1 \\ 2 \end{bmatrix}$

**Step 3:** $\mathbf{u}_3 = \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix} - \frac{1}{\sqrt{2}} \cdot \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} - \frac{1}{\sqrt{6}} \cdot \frac{1}{\sqrt{6}}\begin{bmatrix} 1 \\ -1 \\ 2 \end{bmatrix}$

$= \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix} - \frac{1}{2}\begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} - \frac{1}{6}\begin{bmatrix} 1 \\ -1 \\ 2 \end{bmatrix} = \begin{bmatrix} -2/3 \\ 2/3 \\ 2/3 \end{bmatrix}$

$\mathbf{q}_3 = \frac{1}{\sqrt{4/3}} \begin{bmatrix} -2/3 \\ 2/3 \\ 2/3 \end{bmatrix} = \frac{1}{\sqrt{3}}\begin{bmatrix} -1 \\ 1 \\ 1 \end{bmatrix}$

**Verify:** $\mathbf{q}_i^T\mathbf{q}_j = \delta_{ij}$ ✓

### Numerical Instability

Classical Gram-Schmidt can lose orthogonality due to floating-point errors. **Modified Gram-Schmidt** re-orthogonalizes at each step and is preferred in practice. Householder reflections are even more stable.

## QR Decomposition

Any $A \in \mathbb{R}^{m \times n}$ ($m \geq n$, full column rank) can be factored as:

$$A = QR$$

where:
- $Q \in \mathbb{R}^{m \times n}$: orthonormal columns
- $R \in \mathbb{R}^{n \times n}$: upper triangular with positive diagonal

### Construction via Gram-Schmidt

Gram-Schmidt on columns of $A$ gives $Q$. The entries of $R$ are:
$$R_{ij} = \begin{cases} \langle \mathbf{a}_j, \mathbf{q}_i \rangle & i < j \\ \|\mathbf{u}_i\| & i = j \\ 0 & i > j \end{cases}$$

### Applications

| Application | How QR is used |
|-------------|---------------|
| Solving least squares | $A\mathbf{x} = \mathbf{b} \Rightarrow R\mathbf{x} = Q^T\mathbf{b}$ (back-substitution) |
| QR algorithm for eigenvalues | Iterative QR factorization converges to Schur form |
| Numerical stability | QR is more stable than normal equations $(A^TA)^{-1}A^T\mathbf{b}$ |

### Least Squares via QR

Given $A = QR$:
$$\hat{\mathbf{x}} = R^{-1}Q^T\mathbf{b}$$

This avoids forming $A^TA$ (which squares the condition number) and is the preferred method in practice.

## Key Insights

1. **Orthogonality** makes computation clean — projections become dot products
2. **Least squares** is projection — the residual is orthogonal to the column space
3. **QR** is numerically superior to normal equations for least squares
4. **Gram-Schmidt** is the bridge from any basis to an orthonormal one
5. **Orthogonal matrices** preserve geometry — rotations and reflections

## Exit Check

- [ ] Can project a vector onto a subspace given a basis
- [ ] Can execute Gram-Schmidt on a set of 3 vectors by hand
- [ ] Can construct QR decomposition from Gram-Schmidt output
- [ ] Can solve least squares via QR and explain why it beats normal equations

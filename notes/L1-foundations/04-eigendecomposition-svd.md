# 1.1.2 Eigendecomposition and Singular Value Decomposition (SVD)

## Eigenvalues and Eigenvectors

For a square matrix $A \in \mathbb{R}^{n \times n}$, a non-zero vector $\mathbf{v}$ is an **eigenvector** with **eigenvalue** $\lambda$ if:

$$A\mathbf{v} = \lambda\mathbf{v}$$

This means $A$ acts on $\mathbf{v}$ by only scaling it — no rotation or change of direction.

### Finding Eigenvalues

$$\det(A - \lambda I) = 0$$

This is the **characteristic polynomial**. Roots are eigenvalues (counting multiplicities).

### Finding Eigenvectors

For each eigenvalue $\lambda_i$, solve:
$$(A - \lambda_i I)\mathbf{v} = \mathbf{0}$$

The solution space is the **eigenspace** $E_{\lambda_i}$.

## Eigendecomposition

For a diagonalizable matrix $A$:

$$A = PDP^{-1}$$

Where:
- $P = [\mathbf{v}_1 | \mathbf{v}_2 | \cdots | \mathbf{v}_n]$ (eigenvectors as columns)
- $D = \text{diag}(\lambda_1, \lambda_2, \ldots, \lambda_n)$ (eigenvalues on diagonal)

### When is a Matrix Diagonalizable?

A matrix is diagonalizable if and only if:
- It has $n$ linearly independent eigenvectors (full set)
- The sum of geometric multiplicities equals $n$

**Sufficient conditions:**
- $n$ distinct eigenvalues
- Real symmetric matrices ($A = A^T$)
- Normal matrices ($A^*A = AA^*$)

### Properties of Symmetric Matrices

For $A = A^T$:
1. All eigenvalues are **real**
2. Eigenvectors for distinct eigenvalues are **orthogonal**
3. Diagonalization: $A = QDQ^T$ where $Q$ is orthogonal ($Q^TQ = I$)

## Singular Value Decomposition (SVD)

For **any** matrix $A \in \mathbb{R}^{m \times n}$:

$$A = U\Sigma V^T$$

Where:
- $U \in \mathbb{R}^{m \times m}$: orthogonal matrix (left singular vectors)
- $\Sigma \in \mathbb{R}^{m \times n}$: diagonal matrix with $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_r \geq 0$ (singular values)
- $V \in \mathbb{R}^{n \times n}$: orthogonal matrix (right singular vectors)

### Computing SVD

1. $A^TA = V\Sigma^T\Sigma V^T$ — eigenvalue decomposition gives $V$ and $\sigma_i^2$
2. $AA^T = U\Sigma\Sigma^T U^T$ — eigenvalue decomposition gives $U$ and $\sigma_i^2$
3. $\sigma_i = \sqrt{\lambda_i(A^TA)}$

### Rank-$k$ Approximation (Eckart-Young)

Best rank-$k$ approximation in Frobenius norm:

$$A_k = \sum_{i=1}^{k} \sigma_i \mathbf{u}_i \mathbf{v}_i^T = U_k \Sigma_k V_k^T$$

Error: $\|A - A_k\|_F^2 = \sum_{i=k+1}^{r} \sigma_i^2$

## Applications

| Application | How SVD/Eigen is Used |
|-------------|----------------------|
| PCA | Eigenvalues of covariance matrix |
| Image compression | Low-rank SVD approximation |
| Recommender systems | Matrix factorization (Netflix prize) |
| Pseudoinverse | $A^+ = V\Sigma^+ U^T$ |
| Spectral clustering | Eigenvectors of graph Laplacian |

## Exercise: Verify SVD Properties

Given $A = \begin{bmatrix} 3 & 0 \\ 0 & 1 \\ 0 & 0 \end{bmatrix}$:

1. Compute $A^TA$ and $AA^T$
2. Find eigenvalues and eigenvectors
3. Construct $U$, $\Sigma$, $V$
4. Verify $A = U\Sigma V^T$
5. Find best rank-1 approximation

**Solution:**

1. **Compute $A^TA$ and $AA^T$:**
   $$A^TA = \begin{bmatrix} 9 & 0 \\ 0 & 1 \end{bmatrix}, \quad AA^T = \begin{bmatrix} 9 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 0 \end{bmatrix}$$

2. **Find eigenvalues and eigenvectors:**
   - $A^TA$: eigenvalues $\lambda_1 = 9, \lambda_2 = 1$
   - Eigenvectors: $\mathbf{v}_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}, \mathbf{v}_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$
   - $AA^T$: eigenvalues $\lambda_1 = 9, \lambda_2 = 1, \lambda_3 = 0$
   - Eigenvectors: $\mathbf{u}_1 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, \mathbf{u}_2 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \mathbf{u}_3 = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$

3. **Construct $U$, $\Sigma$, $V$:**
   $$U = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}, \quad \Sigma = \begin{bmatrix} 3 & 0 \\ 0 & 1 \\ 0 & 0 \end{bmatrix}, \quad V = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

4. **Verify $A = U\Sigma V^T$:**
   $$U\Sigma V^T = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 3 & 0 \\ 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} 3 & 0 \\ 0 & 1 \\ 0 & 0 \end{bmatrix} = A ✓$$

5. **Best rank-1 approximation:**
   $$A_1 = \sigma_1 \mathbf{u}_1 \mathbf{v}_1^T = 3 \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \begin{bmatrix} 1 & 0 \end{bmatrix} = \begin{bmatrix} 3 & 0 \\ 0 & 0 \\ 0 & 0 \end{bmatrix}$$
   
   Error: $\|A - A_1\|_F^2 = \sigma_2^2 = 1$

## Key Insights

1. **Eigendecomposition** reveals the "natural axes" of a linear transformation
2. **SVD** exists for all matrices — generalizes eigendecomposition
3. **Singular values** measure "energy" or importance in each direction
4. **Truncated SVD** provides optimal low-rank approximation
5. **Condition number** $\kappa(A) = \sigma_{\max}/\sigma_{\min}$ measures numerical stability

## Exit Check

- [ ] Can find eigenvalues/vectors of 2×2 and 3×3 matrices
- [ ] Can determine if a matrix is diagonalizable
- [ ] Can compute SVD of small matrices by hand
- [ ] Understand relationship between eigenvalues of $A$ and singular values of $A$
- [ ] Can explain why SVD gives optimal low-rank approximation

# 1.1.2 Linear Transformations, Rank, Nullity, Four Fundamental Subspaces

## Linear Transformations

A function $T: V \to W$ between vector spaces is a **linear transformation** if:

$$T(\alpha\mathbf{u} + \beta\mathbf{v}) = \alpha T(\mathbf{u}) + \beta T(\mathbf{v})$$

for all $\mathbf{u}, \mathbf{v} \in V$ and scalars $\alpha, \beta$.

### Matrix Representation

Every linear transformation $T: \mathbb{R}^n \to \mathbb{R}^m$ can be represented as:

$$T(\mathbf{x}) = A\mathbf{x}$$

where $A \in \mathbb{R}^{m \times n}$. The $j$-th column of $A$ is $T(\mathbf{e}_j)$.

### Key Examples

| Transformation | Matrix | Effect |
|---------------|--------|--------|
| Rotation by $\theta$ in $\mathbb{R}^2$ | $\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$ | Rotates vectors |
| Projection onto $x$-axis | $\begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}$ | Drops $y$-component |
| Scaling by $k$ | $kI$ | Uniform scaling |
| Reflection through $x$-axis | $\begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix}$ | Flips $y$-component |

## Kernel and Image

For $T: V \to W$:

- **Kernel** (null space): $\ker(T) = \{\mathbf{v} \in V : T(\mathbf{v}) = \mathbf{0}\}$
- **Image** (range, column space): $\text{im}(T) = \{T(\mathbf{v}) : \mathbf{v} \in V\}$

Both are subspaces ($\ker(T) \subseteq V$, $\text{im}(T) \subseteq W$).

## Rank and Nullity

- **Rank**: $\text{rank}(A) = \dim(\text{im}(T)) = \dim(\text{col}(A))$
- **Nullity**: $\text{nullity}(A) = \dim(\ker(T)) = \dim(\text{null}(A))$

### Rank-Nullity Theorem

$$\text{rank}(A) + \text{nullity}(A) = n$$

where $n$ is the number of columns (dimension of the domain).

**Interpretation:** every dimension of the domain either maps to something non-zero (rank) or collapses to zero (nullity). Nothing is lost or created.

## The Four Fundamental Subspaces

For $A \in \mathbb{R}^{m \times n}$:

| Subspace | Notation | Lives in | Dimension |
|----------|----------|----------|-----------|
| Column space | $\text{col}(A) = \text{im}(A)$ | $\mathbb{R}^m$ | $r$ |
| Null space | $\text{null}(A) = \ker(A)$ | $\mathbb{R}^n$ | $n - r$ |
| Row space | $\text{row}(A) = \text{col}(A^T)$ | $\mathbb{R}^n$ | $r$ |
| Left null space | $\text{null}(A^T)$ | $\mathbb{R}^m$ | $m - r$ |

where $r = \text{rank}(A)$.

### Orthogonality Relations

The four subspaces come in two orthogonal pairs:

$$\text{row}(A) \perp \text{null}(A) \quad \text{in } \mathbb{R}^n$$
$$\text{col}(A) \perp \text{null}(A^T) \quad \text{in } \mathbb{R}^m$$

Together they decompose the domain and codomain:
$$\mathbb{R}^n = \text{row}(A) \oplus \text{null}(A)$$
$$\mathbb{R}^m = \text{col}(A) \oplus \text{null}(A^T)$$

### Geometric Picture

```
Domain (R^n)                    Codomain (R^m)
┌──────────────────┐            ┌──────────────────┐
│                  │            │                  │
│  row(A)    ──────┼── A ──────▶│  col(A)          │
│  dim = r         │            │  dim = r         │
│                  │            │                  │
│──────────────────│            │──────────────────│
│                  │            │                  │
│  null(A)   ──────┼── A ──────▶│  {0}             │
│  dim = n-r       │            │                  │
│                  │            │  null(A^T)       │
│                  │            │  dim = m-r       │
└──────────────────┘            └──────────────────┘
```

$A$ maps the row space bijectively to the column space, and crushes the null space to zero.

### Connection to SVD

The SVD $A = U\Sigma V^T$ makes the four subspaces explicit:
- Columns of $V$ corresponding to non-zero $\sigma_i$ → orthonormal basis for row space
- Remaining columns of $V$ → orthonormal basis for null space
- Columns of $U$ corresponding to non-zero $\sigma_i$ → orthonormal basis for column space
- Remaining columns of $U$ → orthonormal basis for left null space

## Worked Example

Given $A = \begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \end{bmatrix}$:

1. **Rank:** Row 2 = 2 × Row 1, so $\text{rank}(A) = 1$
2. **Nullity:** $n - r = 3 - 1 = 2$
3. **Column space:** $\text{span}\left(\begin{bmatrix} 1 \\ 2 \end{bmatrix}\right)$
4. **Null space:** Solve $A\mathbf{x} = \mathbf{0}$: $x_1 + 2x_2 + 3x_3 = 0$
   - Basis: $\left\{\begin{bmatrix} -2 \\ 1 \\ 0 \end{bmatrix}, \begin{bmatrix} -3 \\ 0 \\ 1 \end{bmatrix}\right\}$ (2-dimensional, checks out)
5. **Row space:** $\text{span}\left(\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}\right)$
6. **Left null space:** Solve $A^T\mathbf{y} = \mathbf{0}$: basis $\left\{\begin{bmatrix} -2 \\ 1 \end{bmatrix}\right\}$

**Verify dimensions:** $r + (n-r) = 1 + 2 = 3 = n$ ✓, $r + (m-r) = 1 + 1 = 2 = m$ ✓

## Key Insights

1. **Rank** is the single number that governs all four subspace dimensions
2. **Systems $A\mathbf{x} = \mathbf{b}$** are solvable iff $\mathbf{b} \in \text{col}(A)$
3. **Uniqueness** of solution iff $\text{null}(A) = \{\mathbf{0}\}$ (rank = $n$)
4. The four subspaces give the **complete geometry** of what a matrix does

## Exit Check

- [ ] Can compute rank via row reduction
- [ ] Can find bases for all four fundamental subspaces
- [ ] Can verify orthogonality relations and dimension counts
- [ ] Can explain what rank deficiency means geometrically

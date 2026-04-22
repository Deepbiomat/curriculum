# 1.1.6 Tensor Notation: Index Notation, Einstein Summation

## Why Tensor Notation

Tensor notation is the standard language in physics and materials science papers. Without fluency, you cannot read:
- Continuum mechanics (stress/strain tensors)
- General relativity or differential geometry
- Crystal symmetry and anisotropic material properties
- Many ML papers on equivariant neural networks

## Scalars, Vectors, Matrices as Tensors

A **tensor** of order (rank) $k$ on $\mathbb{R}^n$ has $n^k$ components indexed by $k$ indices.

| Order | Object | Components | Example |
|-------|--------|------------|---------|
| 0 | Scalar | $\phi$ | Temperature $T$ |
| 1 | Vector | $v_i$ | Displacement $u_i$ |
| 2 | Matrix | $A_{ij}$ | Stress $\sigma_{ij}$ |
| 3 | 3-tensor | $C_{ijk}$ | Piezoelectric tensor |
| 4 | 4-tensor | $C_{ijkl}$ | Elastic stiffness tensor |

## Index Notation

### Free and Dummy Indices

- **Free index:** appears exactly once per term; determines the tensor order of the expression
- **Dummy index:** appears exactly twice in a term; implies summation

Example: $c_i = A_{ij}b_j$

- $i$ is free (the result is a vector indexed by $i$)
- $j$ is dummy (summed over): $c_i = \sum_{j=1}^{n} A_{ij}b_j$

### Rules

1. Free indices must match on both sides of an equation
2. Dummy indices appear exactly twice per term
3. No index appears more than twice in a single term
4. Dummy index letter can be renamed without changing meaning ($A_{ij}b_j = A_{ik}b_k$)

## Einstein Summation Convention

**Rule:** repeated indices in a single term are implicitly summed over.

### Common Operations in Index Notation

| Operation | Standard | Index notation |
|-----------|----------|---------------|
| Dot product | $\mathbf{a}^T\mathbf{b}$ | $a_i b_i$ |
| Matrix-vector | $A\mathbf{x}$ | $A_{ij}x_j$ |
| Matrix multiply | $AB$ | $A_{ik}B_{kj}$ |
| Trace | $\text{tr}(A)$ | $A_{ii}$ |
| Outer product | $\mathbf{a}\mathbf{b}^T$ | $a_i b_j$ |
| Frobenius norm² | $\|A\|_F^2$ | $A_{ij}A_{ij}$ |
| Quadratic form | $\mathbf{x}^TA\mathbf{x}$ | $x_i A_{ij} x_j$ |

### The Kronecker Delta

$$\delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases}$$

Acts as the identity: $\delta_{ij}v_j = v_i$

### The Levi-Civita Symbol (Permutation Tensor)

$$\epsilon_{ijk} = \begin{cases} +1 & (i,j,k) \text{ is an even permutation of } (1,2,3) \\ -1 & (i,j,k) \text{ is an odd permutation of } (1,2,3) \\ 0 & \text{any repeated index} \end{cases}$$

Used for cross products: $(\mathbf{a} \times \mathbf{b})_i = \epsilon_{ijk}a_j b_k$

Key identity: $\epsilon_{ijk}\epsilon_{imn} = \delta_{jm}\delta_{kn} - \delta_{jn}\delta_{km}$

## Reading Tensor Expressions in Papers

### Example 1: Hooke's Law (Linear Elasticity)

$$\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$$

- $\sigma_{ij}$: stress tensor (order 2, symmetric)
- $\varepsilon_{kl}$: strain tensor (order 2, symmetric)
- $C_{ijkl}$: elastic stiffness tensor (order 4, up to 21 independent components)
- $k, l$ are dummy indices: this is a double sum $\sigma_{ij} = \sum_k \sum_l C_{ijkl}\varepsilon_{kl}$

### Example 2: Navier-Stokes (Incompressible)

$$\rho\left(\frac{\partial v_i}{\partial t} + v_j \frac{\partial v_i}{\partial x_j}\right) = -\frac{\partial p}{\partial x_i} + \mu \frac{\partial^2 v_i}{\partial x_j \partial x_j}$$

- $v_j \frac{\partial v_i}{\partial x_j}$: convective term ($j$ summed)
- $\frac{\partial^2 v_i}{\partial x_j \partial x_j}$: Laplacian ($j$ summed)
- $i$ is free: one equation per spatial dimension

### Example 3: Equivariant Neural Networks

In papers on E(3)-equivariant GNNs:

$$\mathbf{m}_{ij}^{(l)} = \sum_{l_1, l_2} W_{l_1 l_2}^{(l)} \left(\mathbf{x}_i^{(l_1)} \otimes \mathbf{x}_j^{(l_2)}\right)^{(l)}$$

Here indices $l, l_1, l_2$ label irreducible representations (angular momentum channels), and $\otimes$ is a tensor product decomposed via Clebsch-Gordan coefficients. Fluency in index notation is required to parse such expressions.

## NumPy `einsum` Connection

NumPy's `einsum` directly implements Einstein summation:

```python
import numpy as np

A = np.random.randn(3, 4)
B = np.random.randn(4, 5)
x = np.random.randn(4)

# Matrix multiply: C_ij = A_ik B_kj
C = np.einsum('ik,kj->ij', A, B)

# Matrix-vector: y_i = A_ij x_j
y = np.einsum('ij,j->i', A, x)

# Trace: t = A_ii
t = np.einsum('ii', A[:3,:3])

# Frobenius norm squared: f = A_ij A_ij
f = np.einsum('ij,ij', A, A)

# Batch matrix multiply: C_bij = A_bik B_bkj
A_batch = np.random.randn(2, 3, 4)
B_batch = np.random.randn(2, 4, 5)
C_batch = np.einsum('bik,bkj->bij', A_batch, B_batch)
```

## Key Insights

1. **Index notation** is not harder — it's more explicit than matrix notation
2. **Einstein summation** is just a notational shortcut for repeated-index sums
3. **Free indices** tell you the shape of the result
4. **Kronecker delta** and **Levi-Civita symbol** are the fundamental building blocks
5. **`np.einsum`** is the computational realization of Einstein summation
6. Materials science papers use order-4 tensors routinely ($C_{ijkl}$)

## Exit Check

- [ ] Can convert between matrix notation and index notation
- [ ] Can identify free vs dummy indices and determine tensor order of result
- [ ] Can expand an Einstein summation expression into explicit sums
- [ ] Can read Hooke's law in tensor form and explain each index
- [ ] Can write `np.einsum` calls matching tensor expressions

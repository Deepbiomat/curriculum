# Exercise 1.4: Einstein Summation / `np.einsum` Practice

Covers notes 06 (tensor notation). Translate between math and code.

---

## Part A — Index Notation to `einsum`

Write the `np.einsum` call for each expression. Verify against the standard NumPy operation.

```python
import numpy as np

A = np.random.randn(3, 4)
B = np.random.randn(4, 5)
C = np.random.randn(3, 4)
x = np.random.randn(4)
y = np.random.randn(3)
```

| # | Expression | Index notation | `einsum` string | Verify against |
|---|-----------|---------------|----------------|----------------|
| 1 | $\mathbf{x}^T\mathbf{x}$ | $x_i x_i$ | `'i,i->'` | `x @ x` |
| 2 | $A\mathbf{x}$ | $A_{ij}x_j$ | ? | `A @ x` |
| 3 | $AB$ | $A_{ik}B_{kj}$ | ? | `A @ B` |
| 4 | $\text{tr}(A^TC)$ | $A_{ij}C_{ij}$ | ? | `np.trace(A.T @ C)` |
| 5 | $\mathbf{y}^TA\mathbf{x}$ | $y_i A_{ij} x_j$ | ? | `y @ A @ x` |
| 6 | $A \odot C$ (element-wise) | $A_{ij}C_{ij} \to$ scalar | ? | `np.sum(A * C)` |
| 7 | Outer product $\mathbf{x}\mathbf{y}^T$ | $x_i y_j$ | ? | `np.outer(x[:3], y)` |

---

## Part B — `einsum` to Math

Translate each `einsum` call into standard mathematical notation:

1. `np.einsum('ii->i', M)` where $M \in \mathbb{R}^{n \times n}$
2. `np.einsum('ijk,kl->ijl', T, A)` where $T \in \mathbb{R}^{a \times b \times c}$, $A \in \mathbb{R}^{c \times d}$
3. `np.einsum('bi,bj->bij', X, Y)` where $X, Y \in \mathbb{R}^{B \times n}$

---

## Part C — Hooke's Law in Code

Implement generalized Hooke's law $\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$ using `einsum`:

```python
# Isotropic material: C_ijkl = lambda * delta_ij * delta_kl + mu * (delta_ik * delta_jl + delta_il * delta_jk)
lam = 1.0  # first Lamé parameter
mu = 0.5   # shear modulus

delta = np.eye(3)

# Task 1: Construct C_ijkl
C = lam * np.einsum('ij,kl->ijkl', delta, delta) + \
    mu * (np.einsum('ik,jl->ijkl', delta, delta) + np.einsum('il,jk->ijkl', delta, delta))

# Task 2: Given a strain tensor, compute the stress tensor
epsilon = np.array([[0.01, 0.005, 0.0],
                    [0.005, 0.02, 0.0],
                    [0.0, 0.0, -0.01]])

# sigma_ij = C_ijkl * epsilon_kl
sigma = np.einsum('ijkl,kl->ij', C, epsilon)

# Task 3: Verify sigma is symmetric
# Task 4: Compute the trace of sigma and relate to tr(epsilon)
```

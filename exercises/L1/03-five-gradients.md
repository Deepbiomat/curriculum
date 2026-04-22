# Exercise 1.3: Five Gradient Derivations

Covers notes 05 (matrix calculus). Derive each gradient from first principles — no lookup.

---

## Gradient 1 — Linear Function

**Given:** $f(\mathbf{x}) = \mathbf{w}^T\mathbf{x} + b$

**Derive:** $\nabla_{\mathbf{x}} f$

**Hint:** Expand using $f = \sum_j w_j x_j + b$ and differentiate component-wise.

---

## Gradient 2 — Quadratic Form

**Given:** $f(\mathbf{x}) = \mathbf{x}^T\mathbf{A}\mathbf{x}$ where $\mathbf{A}$ is symmetric

**Derive:** $\nabla_{\mathbf{x}} f$

**Hint:** Write $f = \sum_{i,j} A_{ij}x_i x_j$ and differentiate w.r.t. $x_k$.

---

## Gradient 3 — Least Squares

**Given:** $f(\mathbf{w}) = \frac{1}{2}\|\mathbf{Xw} - \mathbf{y}\|^2$

**Derive:** $\nabla_{\mathbf{w}} f$

**Tasks:**
1. Expand the squared norm
2. Differentiate
3. Set $\nabla f = 0$ and derive the normal equation $\hat{\mathbf{w}} = (X^TX)^{-1}X^T\mathbf{y}$

---

## Gradient 4 — Logistic Loss

**Given:** $\sigma(z) = \frac{1}{1+e^{-z}}$, $f(\mathbf{w}) = -y\log(\sigma(\mathbf{w}^T\mathbf{x})) - (1-y)\log(1-\sigma(\mathbf{w}^T\mathbf{x}))$

**Derive:** $\nabla_{\mathbf{w}} f$

**Tasks:**
1. First show $\sigma'(z) = \sigma(z)(1-\sigma(z))$
2. Apply chain rule through the loss
3. Simplify to $(\hat{y} - y)\mathbf{x}$

---

## Gradient 5 — Matrix Trace

**Given:** $f(\mathbf{X}) = \text{tr}(\mathbf{AXB})$

**Derive:** $\frac{\partial f}{\partial \mathbf{X}}$

**Hint:** Write in index notation: $f = \sum_{i,j,k} A_{ij}X_{jk}B_{ki}$ and differentiate w.r.t. $X_{mn}$.

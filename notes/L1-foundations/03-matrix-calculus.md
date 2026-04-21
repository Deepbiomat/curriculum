# 1.1.3 Matrix Calculus

## The Gradient

For $f: \mathbb{R}^n \to \mathbb{R}$, the **gradient** is:

$$\nabla f(\mathbf{x}) = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{bmatrix} \in \mathbb{R}^n$$

Points in direction of steepest ascent.

## Common Gradient Identities

| Function | Gradient |
|----------|----------|
| $f(\mathbf{x}) = \mathbf{a}^T\mathbf{x}$ | $\nabla f = \mathbf{a}$ |
| $f(\mathbf{x}) = \mathbf{x}^T\mathbf{A}\mathbf{x}$ | $\nabla f = (\mathbf{A} + \mathbf{A}^T)\mathbf{x}$ |
| $f(\mathbf{x}) = \|\mathbf{Ax} - \mathbf{b}\|^2$ | $\nabla f = 2\mathbf{A}^T(\mathbf{Ax} - \mathbf{b})$ |
| $f(\mathbf{x}) = \mathbf{x}^T\mathbf{x}$ | $\nabla f = 2\mathbf{x}$ |

## The Hessian

Second derivative matrix:

$$H_f(\mathbf{x}) = \begin{bmatrix} \frac{\partial^2 f}{\partial x_i \partial x_j} \end{bmatrix} \in \mathbb{R}^{n \times n}$$

- Symmetric when $f$ is twice continuously differentiable
- Positive definite $\Rightarrow$ local minimum
- Negative definite $\Rightarrow$ local maximum
- Indefinite $\Rightarrow$ saddle point

## Derivatives with Respect to Matrices

For $f: \mathbb{R}^{m \times n} \to \mathbb{R}$:

$$\frac{\partial f}{\partial \mathbf{X}} = \begin{bmatrix} \frac{\partial f}{\partial X_{ij}} \end{bmatrix}$$

### Key Matrix Derivatives

| Function | Derivative |
|----------|------------|
| $f(\mathbf{X}) = \text{tr}(\mathbf{X})$ | $\frac{\partial f}{\partial \mathbf{X}} = \mathbf{I}$ |
| $f(\mathbf{X}) = \text{tr}(\mathbf{AX})$ | $\frac{\partial f}{\partial \mathbf{X}} = \mathbf{A}^T$ |
| $f(\mathbf{X}) = \text{tr}(\mathbf{X}^T\mathbf{X})$ | $\frac{\partial f}{\partial \mathbf{X}} = 2\mathbf{X}$ |
| $f(\mathbf{X}) = \det(\mathbf{X})$ | $\frac{\partial f}{\partial \mathbf{X}} = \det(\mathbf{X})(\mathbf{X}^{-1})^T$ |
| $f(\mathbf{X}) = \mathbf{a}^T\mathbf{X}\mathbf{b}$ | $\frac{\partial f}{\partial \mathbf{X}} = \mathbf{ab}^T$ |

## Chain Rule for Vectors

For $\mathbf{z} = \mathbf{g}(\mathbf{x})$ and $f = h(\mathbf{z})$:

$$\frac{\partial f}{\partial \mathbf{x}} = \left(\frac{\partial \mathbf{z}}{\partial \mathbf{x}}\right)^T \frac{\partial f}{\partial \mathbf{z}}$$

The Jacobian matrix $\frac{\partial \mathbf{z}}{\partial \mathbf{x}}$ has entries $\frac{\partial z_i}{\partial x_j}$.

## Exercise: Derive 5 Gradients

### 1. Linear Function
**Given:** $f(\mathbf{x}) = \mathbf{w}^T\mathbf{x} + b$

**Derive:** $\nabla_{\mathbf{x}} f = \mathbf{w}$

**Solution:**
$$\frac{\partial f}{\partial x_i} = \frac{\partial}{\partial x_i}\sum_j w_j x_j = w_i$$
Therefore: $\nabla_{\mathbf{x}} f = \mathbf{w}$

---

### 2. Quadratic Form
**Given:** $f(\mathbf{x}) = \mathbf{x}^T\mathbf{A}\mathbf{x}$ where $\mathbf{A}$ is symmetric

**Derive:** $\nabla_{\mathbf{x}} f = 2\mathbf{Ax}$

**Solution:**
$$f = \sum_{i,j} A_{ij}x_i x_j$$
$$\frac{\partial f}{\partial x_k} = \sum_j A_{kj}x_j + \sum_i A_{ik}x_i = 2\sum_j A_{kj}x_j$$
Therefore: $\nabla_{\mathbf{x}} f = 2\mathbf{Ax}$

---

### 3. Squared Error
**Given:** $f(\mathbf{w}) = \frac{1}{2}\|\mathbf{Xw} - \mathbf{y}\|^2$

**Derive:** $\nabla_{\mathbf{w}} f = \mathbf{X}^T(\mathbf{Xw} - \mathbf{y})$

**Solution:**
$$f = \frac{1}{2}(\mathbf{Xw} - \mathbf{y})^T(\mathbf{Xw} - \mathbf{y})$$
$$\nabla_{\mathbf{w}} f = \frac{1}{2} \cdot 2\mathbf{X}^T(\mathbf{Xw} - \mathbf{y}) = \mathbf{X}^T(\mathbf{Xw} - \mathbf{y})$$

**Note:** This is the **normal equation** for least squares.

---

### 4. Logistic Loss (Sigmoid)
**Given:** $\sigma(z) = \frac{1}{1+e^{-z}}$, $f(\mathbf{w}) = -y\log(\sigma(\mathbf{w}^T\mathbf{x})) - (1-y)\log(1-\sigma(\mathbf{w}^T\mathbf{x}))$

**Derive:** $\nabla_{\mathbf{w}} f = (\sigma(\mathbf{w}^T\mathbf{x}) - y)\mathbf{x}$

**Solution:**
First, note: $\frac{d\sigma}{dz} = \sigma(1-\sigma)$

Let $\hat{y} = \sigma(\mathbf{w}^T\mathbf{x})$
$$\frac{\partial f}{\partial \mathbf{w}} = -y\frac{1}{\hat{y}}\hat{y}(1-\hat{y})\mathbf{x} - (1-y)\frac{1}{1-\hat{y}}(-\hat{y}(1-\hat{y}))\mathbf{x}$$
$$= -y(1-\hat{y})\mathbf{x} + (1-y)\hat{y}\mathbf{x} = (\hat{y} - y)\mathbf{x}$$

---

### 5. Matrix Trace
**Given:** $f(\mathbf{X}) = \text{tr}(\mathbf{AXB})$

**Derive:** $\frac{\partial f}{\partial \mathbf{X}} = \mathbf{A}^T\mathbf{B}^T$

**Solution:**
$$f = \sum_i (\mathbf{AXB})_{ii} = \sum_{i,j,k} A_{ij}X_{jk}B_{ki}$$
$$\frac{\partial f}{\partial X_{mn}} = \sum_i A_{im}B_{ni} = (\mathbf{B}^T\mathbf{A}^T)_{nm} = (\mathbf{A}^T\mathbf{B}^T)_{mn}$$
Therefore: $\frac{\partial f}{\partial \mathbf{X}} = \mathbf{A}^T\mathbf{B}^T$

## Key Insights

1. **Gradient points uphill** — for minimization, go opposite direction
2. **Hessian curvature** determines convergence rate of optimization
3. **Chain rule** is the foundation of backpropagation
4. **Matrix derivatives** follow layout conventions (numerator vs denominator)
5. **Trace trick**: $\mathbf{a}^T\mathbf{X}\mathbf{b} = \text{tr}(\mathbf{a}^T\mathbf{X}\mathbf{b}) = \text{tr}(\mathbf{X}\mathbf{b}\mathbf{a}^T)$

## Applications to ML

| Context | Matrix Calculus Application |
|---------|---------------------------|
| Linear regression | Normal equations from $\nabla f = 0$ |
| Gradient descent | $\mathbf{x}_{t+1} = \mathbf{x}_t - \eta \nabla f(\mathbf{x}_t)$ |
| Newton's method | $\mathbf{x}_{t+1} = \mathbf{x}_t - H_f^{-1}\nabla f$ |
| Backpropagation | Chain rule through computation graph |

## Exit Check

- [ ] Can derive gradients of common ML loss functions
- [ ] Can apply chain rule for vector-valued functions
- [ ] Can compute matrix derivatives using trace identities
- [ ] Understand relationship between gradient and Hessian
- [ ] Can set up and solve $\nabla f = 0$ for optimization problems

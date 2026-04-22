# Exercise 1.5: Backpropagation from Scratch

Covers notes 07 (backpropagation derivation). Two parts: pen-and-paper derivation, then NumPy implementation.

---

## Part A — Derivation (Pen and Paper)

Consider a 2-layer MLP with sigmoid activations and binary cross-entropy loss.

**Architecture:**
- Input: $\mathbf{x} \in \mathbb{R}^2$
- Hidden: $h = 3$ neurons, sigmoid activation
- Output: 1 neuron, sigmoid activation

**Tasks:**

1. Write the complete forward pass equations
2. Derive $\delta^{(2)} = \frac{\partial \mathcal{L}}{\partial z^{(2)}}$
3. Derive $\frac{\partial \mathcal{L}}{\partial \mathbf{w}^{(2)}}$ and $\frac{\partial \mathcal{L}}{\partial b^{(2)}}$
4. Derive $\boldsymbol{\delta}^{(1)} = \frac{\partial \mathcal{L}}{\partial \mathbf{z}^{(1)}}$
5. Derive $\frac{\partial \mathcal{L}}{\partial W^{(1)}}$ and $\frac{\partial \mathcal{L}}{\partial \mathbf{b}^{(1)}}$
6. State all gradient shapes and verify they match the parameter shapes

---

## Part B — NumPy Implementation

Implement forward pass, backward pass, and gradient checking.

```python
import numpy as np

np.random.seed(42)

# --- Sigmoid and its derivative ---
def sigmoid(z):
    return 1.0 / (1.0 + np.exp(-z))

def sigmoid_prime(z):
    s = sigmoid(z)
    return s * (1.0 - s)

# --- Binary cross-entropy loss ---
def bce_loss(y_hat, y):
    eps = 1e-8
    return -(y * np.log(y_hat + eps) + (1 - y) * np.log(1 - y_hat + eps))

# --- Network parameters ---
d_in, d_hidden, d_out = 2, 3, 1

W1 = np.random.randn(d_hidden, d_in) * 0.5
b1 = np.zeros(d_hidden)
W2 = np.random.randn(d_out, d_hidden) * 0.5
b2 = np.zeros(d_out)

# --- Sample data ---
x = np.array([0.5, -0.3])
y = 1.0

# === Task 1: Forward pass ===
# TODO: Compute z1, a1, z2, y_hat, loss

# === Task 2: Backward pass ===
# TODO: Compute delta2, dW2, db2, delta1, dW1, db1

# === Task 3: Gradient check ===
def numerical_gradient(param, param_name, epsilon=1e-5):
    """Compute numerical gradient via central differences."""
    grad = np.zeros_like(param)
    it = np.nditer(param, flags=['multi_index'])
    while not it.finished:
        idx = it.multi_index
        old_val = param[idx]

        param[idx] = old_val + epsilon
        # TODO: recompute forward pass and loss_plus

        param[idx] = old_val - epsilon
        # TODO: recompute forward pass and loss_minus

        grad[idx] = (loss_plus - loss_minus) / (2 * epsilon)
        param[idx] = old_val
        it.iternext()
    return grad

# TODO: Compare analytic vs numerical gradients for W1, b1, W2, b2
# Relative error should be < 1e-5

# === Task 4: Training loop (bonus) ===
# Train on XOR dataset: [(0,0)->0, (0,1)->1, (1,0)->1, (1,1)->0]
# Use the gradients derived above with learning rate eta = 0.5
# Plot loss over 1000 iterations
```

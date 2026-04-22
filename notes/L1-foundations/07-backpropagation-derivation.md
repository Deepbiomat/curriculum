# 1.1.7 Derive Backpropagation from Scratch

## Setup: A Simple MLP

Consider a 2-layer MLP for binary classification:

**Forward pass:**
$$\mathbf{z}^{(1)} = W^{(1)}\mathbf{x} + \mathbf{b}^{(1)}$$
$$\mathbf{a}^{(1)} = \sigma(\mathbf{z}^{(1)})$$
$$z^{(2)} = \mathbf{w}^{(2)T}\mathbf{a}^{(1)} + b^{(2)}$$
$$\hat{y} = \sigma(z^{(2)})$$

where $\sigma(z) = \frac{1}{1+e^{-z}}$ is the sigmoid function.

**Loss (binary cross-entropy):**
$$\mathcal{L} = -[y\log\hat{y} + (1-y)\log(1-\hat{y})]$$

**Dimensions:**
- $\mathbf{x} \in \mathbb{R}^{d}$ (input)
- $W^{(1)} \in \mathbb{R}^{h \times d}$, $\mathbf{b}^{(1)} \in \mathbb{R}^{h}$ (hidden layer)
- $\mathbf{w}^{(2)} \in \mathbb{R}^{h}$, $b^{(2)} \in \mathbb{R}$ (output layer)

## Prerequisite: Sigmoid Derivative

$$\frac{d\sigma}{dz} = \sigma(z)(1 - \sigma(z))$$

**Proof:**
$$\frac{d}{dz}\left(\frac{1}{1+e^{-z}}\right) = \frac{e^{-z}}{(1+e^{-z})^2} = \frac{1}{1+e^{-z}} \cdot \frac{e^{-z}}{1+e^{-z}} = \sigma(z)(1-\sigma(z))$$

## Step 1: Derivative of Loss w.r.t. Output

$$\frac{\partial \mathcal{L}}{\partial \hat{y}} = -\frac{y}{\hat{y}} + \frac{1-y}{1-\hat{y}} = \frac{\hat{y} - y}{\hat{y}(1-\hat{y})}$$

## Step 2: Derivative of Loss w.r.t. $z^{(2)}$

By chain rule:
$$\delta^{(2)} \equiv \frac{\partial \mathcal{L}}{\partial z^{(2)}} = \frac{\partial \mathcal{L}}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z^{(2)}} = \frac{\hat{y} - y}{\hat{y}(1-\hat{y})} \cdot \hat{y}(1-\hat{y}) = \hat{y} - y$$

This clean result is why sigmoid + cross-entropy pair so well.

## Step 3: Gradients of Output Layer Parameters

$$\frac{\partial \mathcal{L}}{\partial \mathbf{w}^{(2)}} = \frac{\partial \mathcal{L}}{\partial z^{(2)}} \cdot \frac{\partial z^{(2)}}{\partial \mathbf{w}^{(2)}} = \delta^{(2)} \mathbf{a}^{(1)}$$

$$\frac{\partial \mathcal{L}}{\partial b^{(2)}} = \delta^{(2)}$$

## Step 4: Propagate Error to Hidden Layer

$$\frac{\partial \mathcal{L}}{\partial \mathbf{a}^{(1)}} = \frac{\partial \mathcal{L}}{\partial z^{(2)}} \cdot \frac{\partial z^{(2)}}{\partial \mathbf{a}^{(1)}} = \delta^{(2)} \mathbf{w}^{(2)}$$

## Step 5: Derivative w.r.t. $\mathbf{z}^{(1)}$

$$\boldsymbol{\delta}^{(1)} \equiv \frac{\partial \mathcal{L}}{\partial \mathbf{z}^{(1)}} = \frac{\partial \mathcal{L}}{\partial \mathbf{a}^{(1)}} \odot \sigma'(\mathbf{z}^{(1)}) = \delta^{(2)} \mathbf{w}^{(2)} \odot \mathbf{a}^{(1)} \odot (1 - \mathbf{a}^{(1)})$$

where $\odot$ denotes element-wise multiplication.

## Step 6: Gradients of Hidden Layer Parameters

$$\frac{\partial \mathcal{L}}{\partial W^{(1)}} = \boldsymbol{\delta}^{(1)} \mathbf{x}^T \in \mathbb{R}^{h \times d}$$

$$\frac{\partial \mathcal{L}}{\partial \mathbf{b}^{(1)}} = \boldsymbol{\delta}^{(1)} \in \mathbb{R}^{h}$$

## Summary: The Backpropagation Algorithm

### General Pattern for Layer $l$

For a network with $L$ layers:

**Forward (for each layer $l = 1, \ldots, L$):**
$$\mathbf{z}^{(l)} = W^{(l)}\mathbf{a}^{(l-1)} + \mathbf{b}^{(l)}$$
$$\mathbf{a}^{(l)} = g^{(l)}(\mathbf{z}^{(l)})$$

where $\mathbf{a}^{(0)} = \mathbf{x}$ (input).

**Backward (for each layer $l = L, L-1, \ldots, 1$):**
$$\boldsymbol{\delta}^{(l)} = \begin{cases} \nabla_{\mathbf{a}^{(L)}} \mathcal{L} \odot g'^{(L)}(\mathbf{z}^{(L)}) & l = L \\ (W^{(l+1)T}\boldsymbol{\delta}^{(l+1)}) \odot g'^{(l)}(\mathbf{z}^{(l)}) & l < L \end{cases}$$

**Parameter gradients:**
$$\frac{\partial \mathcal{L}}{\partial W^{(l)}} = \boldsymbol{\delta}^{(l)} \mathbf{a}^{(l-1)T}$$
$$\frac{\partial \mathcal{L}}{\partial \mathbf{b}^{(l)}} = \boldsymbol{\delta}^{(l)}$$

### Computation Graph View

```
x ──→ [z¹ = W¹x + b¹] ──→ [a¹ = σ(z¹)] ──→ [z² = w²ᵀa¹ + b²] ──→ [ŷ = σ(z²)] ──→ L
         │                      │                    │                     │
   ∂L/∂W¹ = δ¹xᵀ         ∂L/∂a¹ = δ²w²       ∂L/∂w² = δ²a¹        δ² = ŷ - y
   ∂L/∂b¹ = δ¹            δ¹ = δ²w² ⊙ σ'(z¹)  ∂L/∂b² = δ²
```

## Numerical Verification

For any derived gradient, verify with finite differences:

$$\frac{\partial \mathcal{L}}{\partial \theta_i} \approx \frac{\mathcal{L}(\theta_i + \epsilon) - \mathcal{L}(\theta_i - \epsilon)}{2\epsilon}$$

with $\epsilon \approx 10^{-5}$. Relative error should be $< 10^{-5}$:

$$\text{rel. error} = \frac{|g_{\text{analytic}} - g_{\text{numeric}}|}{|g_{\text{analytic}}| + |g_{\text{numeric}}| + \epsilon}$$

## Why Backprop is Efficient

**Naive approach:** compute $\frac{\partial \mathcal{L}}{\partial \theta_i}$ independently for each parameter → $O(P)$ forward passes, where $P$ = total parameters.

**Backprop:** one forward + one backward pass → $O(1)$ passes, cost proportional to one forward pass.

This is the **reverse-mode automatic differentiation** — efficient when output dimension (loss = scalar) ≪ input dimension (many parameters).

## Key Insights

1. Backprop is just the **chain rule** applied systematically through a computation graph
2. Each layer's gradient depends on the **downstream error signal** $\boldsymbol{\delta}^{(l+1)}$
3. The gradient w.r.t. weights at layer $l$ is always **error × input**: $\boldsymbol{\delta}^{(l)}\mathbf{a}^{(l-1)T}$
4. **Vanishing gradients** occur when $\sigma'(z) \approx 0$ at many layers (motivates ReLU)
5. Backprop computes **all** parameter gradients in a single backward pass

## Exit Check

- [ ] Can derive backprop for a 2-layer MLP with sigmoid activation
- [ ] Can write the general backward recurrence for $\boldsymbol{\delta}^{(l)}$
- [ ] Can explain why backprop is $O(1)$ forward passes, not $O(P)$
- [ ] Can verify gradients numerically with finite differences
- [ ] Understand the connection: backprop = reverse-mode autodiff

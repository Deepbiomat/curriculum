# 1.2.2 MLE vs MAP

## Why this note exists

In L3 and beyond, many training objectives are negative log-likelihoods.
Understanding MLE and MAP explains why those losses look the way they do,
and how priors induce regularization.

This note is intentionally practical: definitions, derivations, one complete worked example, and decision heuristics.

---

## 1. Setup and notation

Let dataset be

$\mathcal{D}=\{(x_i,y_i)\}_{i=1}^n$.

Let model parameters be $\theta$.

A probabilistic model specifies $p(y\mid x,\theta)$.

### 1.1 Likelihood

Given observed data, likelihood is

$L(\theta;\mathcal{D})=p(\mathcal{D}\mid\theta)$.

As a function of $\theta$, data are fixed.

With i.i.d. assumptions,

$p(\mathcal{D}\mid\theta)=\prod_{i=1}^n p(y_i\mid x_i,\theta)$.

### 1.2 Log-likelihood

Because products are inconvenient,

$\ell(\theta)=\log p(\mathcal{D}\mid\theta)=\sum_{i=1}^n \log p(y_i\mid x_i,\theta)$.

Maximizing $\ell$ is equivalent to maximizing $L$ (log is monotone).

---

## 2. Maximum Likelihood Estimation (MLE)

Definition:

$\hat\theta_{\text{MLE}}=\arg\max_\theta p(\mathcal{D}\mid\theta)=\arg\max_\theta \ell(\theta)$.

Interpretation: choose parameter values that make observed data most probable under the model family.

### 2.1 MLE and loss functions

Equivalent minimization form:

$\hat\theta_{\text{MLE}}=\arg\min_\theta\left[-\sum_{i=1}^n\log p(y_i\mid x_i,\theta)\right]$.

So minimizing negative log-likelihood is MLE.

This is the direct bridge to common ML losses:

- Gaussian noise assumption leads to MSE,
- Bernoulli likelihood leads to binary cross-entropy,
- Categorical likelihood leads to multiclass cross-entropy.

---

## 3. Maximum A Posteriori (MAP)

Bayesian setup introduces prior $p(\theta)$.
Posterior:

$p(\theta\mid\mathcal{D})\propto p(\mathcal{D}\mid\theta)p(\theta)$.

Definition:

$\hat\theta_{\text{MAP}}=\arg\max_\theta p(\theta\mid\mathcal{D})
=\arg\max_\theta p(\mathcal{D}\mid\theta)p(\theta)$.

Take logs:

$\hat\theta_{\text{MAP}}=\arg\max_\theta\big(\log p(\mathcal{D}\mid\theta)+\log p(\theta)\big)$.

Equivalent minimization:

$\hat\theta_{\text{MAP}}=\arg\min_\theta\Big(-\log p(\mathcal{D}\mid\theta)-\log p(\theta)\Big)$.

Interpretation: likelihood term fits data, prior term regularizes toward plausible parameter values.

---

## 4. Relationship between MLE and MAP

If prior is uniform/constant over feasible region, $\log p(\theta)$ is constant,
so MAP reduces to MLE.

If prior is informative, MAP deviates from MLE, especially with small datasets.

As sample size grows and likelihood concentrates, prior effect often diminishes.

---

## 5. Worked example: linear regression with Gaussian noise

We build a tiny example from first principles and compute both estimators.

### 5.1 Model

Assume scalar input/output and model

$y_i = wx_i + b + \varepsilon_i$, with $\varepsilon_i\sim\mathcal{N}(0,\sigma^2)$ i.i.d.

Parameter vector:

$\theta = [w,b]^\top$.

Given $x_i$, conditional density:

$p(y_i\mid x_i,\theta)=\dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\dfrac{(y_i-wx_i-b)^2}{2\sigma^2}\right)$.

For all points, log-likelihood:

$\ell(\theta)= -\dfrac{n}{2}\log(2\pi\sigma^2)-\dfrac{1}{2\sigma^2}\sum_{i=1}^n(y_i-wx_i-b)^2$.

First term is constant in $(w,b)$.
So MLE is

$\arg\min_{w,b}\sum_{i=1}^n(y_i-wx_i-b)^2$,

which is ordinary least squares.

### 5.2 Data

Use 6 points:

$(x,y)=\{(0,1.2),(1,2.0),(2,2.9),(3,3.7),(4,5.1),(5,6.2)\}$.

Let design matrix

$X = \begin{bmatrix}
0 & 1 \\
1 & 1 \\
2 & 1 \\
3 & 1 \\
4 & 1 \\
5 & 1
\end{bmatrix}$,

response

$\mathbf{y}=\begin{bmatrix}1.2\\2.0\\2.9\\3.7\\5.1\\6.2\end{bmatrix}$.

OLS/MLE solution:

$\hat\theta_{\text{MLE}}=(X^\top X)^{-1}X^\top\mathbf{y}$.

Compute pieces:

$X^\top X=\begin{bmatrix}55&15\\15&6\end{bmatrix}$,

$X^\top\mathbf{y}=\begin{bmatrix}70.6\\21.1\end{bmatrix}$.

Inverse:

$(X^\top X)^{-1}=\dfrac{1}{105}\begin{bmatrix}6&-15\\-15&55\end{bmatrix}$.

Multiply:

$\hat\theta_{\text{MLE}}=\dfrac{1}{105}\begin{bmatrix}6&-15\\-15&55\end{bmatrix}
\begin{bmatrix}70.6\\21.1\end{bmatrix}
=\dfrac{1}{105}\begin{bmatrix}106.1\\101.5\end{bmatrix}
\approx
\begin{bmatrix}1.0105\\0.9667\end{bmatrix}$.

So

$\hat w_{\text{MLE}}\approx1.0105,\quad \hat b_{\text{MLE}}\approx0.9667$.

### 5.3 MAP with Gaussian prior

Put zero-mean isotropic Gaussian prior on parameters:

$p(\theta)=\mathcal{N}(\mathbf{0},\tau^2 I)$.

Then

$-\log p(\theta)=\text{const}+\dfrac{1}{2\tau^2}\|\theta\|_2^2$.

MAP minimization becomes

$\arg\min_\theta \left(\dfrac{1}{2\sigma^2}\|\mathbf{y}-X\theta\|_2^2 + \dfrac{1}{2\tau^2}\|\theta\|_2^2\right)$.

Multiply by $2\sigma^2$:

$\arg\min_\theta \left(\|\mathbf{y}-X\theta\|_2^2 + \lambda\|\theta\|_2^2\right),
\quad \lambda=\sigma^2/\tau^2$.

This is ridge regression objective.

Closed form:

$\hat\theta_{\text{MAP}}=(X^\top X + \lambda I)^{-1}X^\top\mathbf{y}$.

Choose illustrative $\lambda=1$.
Then

$X^\top X + I = \begin{bmatrix}56&15\\15&7\end{bmatrix}$.

Inverse:

$(X^\top X + I)^{-1}=\dfrac{1}{167}\begin{bmatrix}7&-15\\-15&56\end{bmatrix}$.

Multiply:

$\hat\theta_{\text{MAP}}=\dfrac{1}{167}\begin{bmatrix}7&-15\\-15&56\end{bmatrix}
\begin{bmatrix}70.6\\21.1\end{bmatrix}
=\dfrac{1}{167}\begin{bmatrix}176.7\\120.1\end{bmatrix}
\approx
\begin{bmatrix}1.0581\\0.7192\end{bmatrix}$.

So

$\hat w_{\text{MAP}}\approx1.0581,\quad \hat b_{\text{MAP}}\approx0.7192$.

### 5.4 Numerical comparison

- MLE: $(w,b) \approx (1.0105, 0.9667)$
- MAP (with $\lambda=1$): $(w,b) \approx (1.0581, 0.7192)$

MAP moved parameters toward prior-preferred region (here, toward zero vector), trading slight fit quality for regularization.

### 5.5 Materials context interpretation

Suppose $x$ is porosity fraction and $y$ is measured elastic modulus proxy.
With only a few experiments, MLE may overfit noise.
MAP lets us encode prior belief that extreme slopes/intercepts are unlikely given known biomechanics.

This is useful in early-stage biomaterial studies where sample counts are small and measurements noisy.

---

## 6. Decision heuristic: when to use MLE vs MAP

Use MLE when:

1. you have abundant data,
2. priors are unavailable or untrusted,
3. baseline frequentist estimate is sufficient.

Use MAP when:

1. data are scarce,
2. domain prior knowledge exists,
3. regularization is needed for stability,
4. you need an interpretable prior-to-posterior update.

Practical note: in deep learning, L2 weight decay corresponds to a Gaussian-prior-style MAP objective under suitable assumptions.

---

## 7. Geometric viewpoint

- MLE minimizes data misfit surface.
- MAP minimizes data misfit plus prior penalty.

The prior adds curvature and can improve conditioning.
In linear models, this often stabilizes inversion when $X^\top X$ is ill-conditioned.

---

## 8. Bias-variance intuition

- MLE: usually lower bias, potentially higher variance.
- MAP: introduces bias via prior, often lowers variance.

With tiny datasets, variance reduction can improve generalization error.

---

## 9. Common pitfalls

1. Treating MAP as "always better".
   It depends on prior quality.

2. Forgetting prior choice is part of model design.
   Poor priors can systematically mislead.

3. Confusing posterior mode (MAP) with posterior mean.
   They are generally different.

4. Ignoring scaling of features in ridge/MAP interpretations.
   Prior effect changes with parameter scale.

---

## 10. Bridge to L3 losses

Negative log-likelihood minimization in neural nets is MLE under a probabilistic output model.
Adding explicit prior-like penalties gives MAP-style training objectives.

So MLE/MAP is not separate from ML engineering; it is the probabilistic meaning behind standard losses and regularization.

---

## 11. Quick self-check

1. Derive MLE for Gaussian-mean estimation with known variance.
2. Show algebraically that Gaussian prior on parameters yields L2 penalty.
3. Explain why MAP and MLE converge as $n$ grows (under regularity assumptions).
4. In a small biomaterials dataset, what prior could be justified physically?

---

## 12. References

- Bishop, 2006, regression and Bayesian linear models.
- Murphy, 2022, MLE/MAP and probabilistic learning.

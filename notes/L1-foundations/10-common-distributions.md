# 1.2.3 Common Distributions

## Purpose of this note

This note is a compact reference for distributions you will repeatedly encounter in:

- classification and regression losses,
- Bayesian priors/posteriors,
- uncertainty quantification,
- modeling experimental noise in biomaterials workflows.

A companion sampling exercise lives at
`exercises/L1/1.2.3-distribution-sampling.ipynb`.

---

## 1. Quick taxonomy

Discrete distributions (countable outcomes):

- Bernoulli,
- Binomial,
- Categorical.

Continuous distributions:

- Gaussian (univariate, multivariate),
- Gamma,
- Beta.

---

## 2. Bernoulli distribution

### 2.1 Definition

$X\sim\text{Bernoulli}(p)$ with support $\{0,1\}$ and parameter $p\in[0,1]$.

PMF:

$P(X=x)=p^x(1-p)^{1-x},\quad x\in\{0,1\}$.

### 2.2 Moments

$\mathbb{E}[X]=p$,

$\mathrm{Var}(X)=p(1-p)$.

### 2.3 Use cases

- binary failure/success events,
- implant pass/fail indicator,
- adverse event present/absent.

---

## 3. Binomial distribution

### 3.1 Definition

$X\sim\text{Binomial}(n,p)$ counts successes in $n$ i.i.d. Bernoulli trials.

Support: $\{0,1,\dots,n\}$.

PMF:

$P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}$.

### 3.2 Moments

$\mathbb{E}[X]=np$,

$\mathrm{Var}(X)=np(1-p)$.

### 3.3 Use cases

- number of defective samples in batch,
- number of successful cell attachments out of fixed assays,
- number of positive outcomes in fixed cohort size.

---

## 4. Categorical distribution

### 4.1 Definition

$X\sim\text{Categorical}(\pi_1,\dots,\pi_K)$ where $\pi_k\ge0$ and $\sum_k\pi_k=1$.

Support: class labels $\{1,\dots,K\}$.

PMF:

$P(X=k)=\pi_k$.

### 4.2 Moments (indicator form)

Let one-hot indicator vector $\mathbf{z}\in\{0,1\}^K$, $\sum z_k=1$.
Then

$\mathbb{E}[z_k]=\pi_k$,

$\mathrm{Cov}(z_i,z_j)=\begin{cases}
\pi_i(1-\pi_i), & i=j \\
-\pi_i\pi_j, & i\ne j
\end{cases}$.

### 4.3 Use cases

- material class labels,
- tissue response categories,
- multi-class diagnostic predictions.

---

## 5. Gaussian (Normal) distribution: univariate

### 5.1 Definition

$X\sim\mathcal{N}(\mu,\sigma^2)$, support $x\in\mathbb{R}$.

PDF:

$f(x)=\dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\dfrac{(x-\mu)^2}{2\sigma^2}\right)$.

### 5.2 Moments

$\mathbb{E}[X]=\mu$,

$\mathrm{Var}(X)=\sigma^2$.

### 5.3 Use cases

- additive measurement noise,
- residual assumptions in linear regression,
- approximate latent variable distributions.

---

## 6. Gaussian distribution: multivariate

### 6.1 Definition

$\mathbf{X}\sim\mathcal{N}(\boldsymbol\mu,\Sigma)$ in $\mathbb{R}^d$.

PDF:

$f(\mathbf{x})=\dfrac{1}{\sqrt{(2\pi)^d|\Sigma|}}
\exp\left(-\dfrac{1}{2}(\mathbf{x}-\boldsymbol\mu)^\top\Sigma^{-1}(\mathbf{x}-\boldsymbol\mu)\right)$.

### 6.2 Moments

$\mathbb{E}[\mathbf{X}] = \boldsymbol\mu$,

$\mathrm{Cov}(\mathbf{X}) = \Sigma$.

### 6.3 Use cases

- joint modeling of correlated descriptors,
- Gaussian priors over parameter vectors,
- Kalman-like state uncertainty.

---

## 7. Gamma distribution

### 7.1 Definition

Use shape-rate parameterization:

$X\sim\text{Gamma}(\alpha,\beta)$ with support $x>0$,
$\alpha>0,\beta>0$.

PDF:

$f(x)=\dfrac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}$.

### 7.2 Moments

$\mathbb{E}[X]=\dfrac{\alpha}{\beta}$,

$\mathrm{Var}(X)=\dfrac{\alpha}{\beta^2}$.

### 7.3 Use cases

- positive-valued waiting times,
- priors for rates/precisions,
- skewed positive experimental variables.

---

## 8. Beta distribution

### 8.1 Definition

$X\sim\text{Beta}(\alpha,\beta)$ with support $x\in(0,1)$, $\alpha,\beta>0$.

PDF:

$f(x)=\dfrac{1}{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1}$,

where

$B(\alpha,\beta)=\dfrac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$.

### 8.2 Moments

$\mathbb{E}[X]=\dfrac{\alpha}{\alpha+\beta}$,

$\mathrm{Var}(X)=\dfrac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$.

### 8.3 Use cases

- priors over probabilities,
- uncertainty on defect rate,
- posterior over Bernoulli success probability.

---

## 9. Conjugacy table (high-value pairs)

1. Bernoulli likelihood + Beta prior -> Beta posterior.
2. Binomial likelihood + Beta prior -> Beta posterior.
3. Categorical likelihood + Dirichlet prior -> Dirichlet posterior (optional extension).
4. Poisson likelihood + Gamma prior -> Gamma posterior.
5. Gaussian mean likelihood (known variance) + Gaussian prior -> Gaussian posterior.

Conjugacy means posterior is in same distribution family as prior, enabling closed-form updates.

---

## 10. Distribution-to-loss connections

- Bernoulli likelihood -> binary cross-entropy loss.
- Categorical likelihood -> multiclass cross-entropy.
- Gaussian likelihood with fixed variance -> MSE (up to constants).
- Laplace likelihood -> MAE (for reference; not covered in detail here).

This helps interpret objective functions as probabilistic assumptions.

---

## 11. Practical selection heuristics

1. Outcome binary?
   Use Bernoulli/Binomial model family.

2. Outcome multi-class?
   Use Categorical (or multinomial for counts).

3. Outcome continuous with roughly symmetric residuals?
   Start with Gaussian.

4. Positive and skewed quantity?
   Consider Gamma.

5. Unknown probability parameter?
   Beta prior is often natural.

---

## 12. Domain mini-examples

- Bernoulli: did a scaffold sample fail under threshold load (yes/no)?
- Binomial: how many of 30 cultured samples show viable adhesion?
- Categorical: classify inflammation response into mild/moderate/severe.
- Gaussian: measurement noise on elastic modulus.
- Gamma: time to degradation event (positive, right-skewed).
- Beta: posterior uncertainty of complication probability.

---

## 13. Common pitfalls

1. Ignoring support constraints (e.g., Gamma for negative values).
2. Mixing parameterizations silently (shape-rate vs shape-scale).
3. Treating distribution choice as cosmetic when it determines implied loss.

---

## 14. Bridge to exercise

Now run sampling and empirical moment checks in:

`exercises/L1/1.2.3-distribution-sampling.ipynb`

Goal: verify visually and numerically that sampled data matches each distribution's theoretical behavior.

---

## 15. References

- Murphy, 2022, introductory probabilistic modeling chapters.
- Bishop, 2006, canonical distribution review sections.

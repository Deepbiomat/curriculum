# 1.2.1 Conditional Probability and Bayes' Theorem

## Why this topic exists in L1

Probability is the language for uncertainty. In this curriculum, uncertainty appears everywhere:

- lab measurement error,
- biological variability,
- model uncertainty,
- decision-making under incomplete information.

This note builds the minimum probability toolkit needed for L3 topics like negative log-likelihood losses, calibration, and Bayesian reasoning.

---

## 1. Kolmogorov Axioms (minimal foundation)

Let the sample space be $\Omega$ and let events be measurable subsets of $\Omega$.
A probability measure $P$ satisfies:

1. Non-negativity:
   $P(A) \ge 0$ for every event $A$.
2. Normalization:
   $P(\Omega) = 1$.
3. Countable additivity:
   if $A_1, A_2, \dots$ are pairwise disjoint,
   $P\left(\bigcup_i A_i\right) = \sum_i P(A_i)$.

From these three axioms, useful rules follow.

### 1.1 Immediate consequences

- Empty event has zero probability:
  $P(\varnothing) = 0$.
- Complement rule:
  $P(A^c) = 1 - P(A)$.
- Monotonicity:
  if $A \subseteq B$, then $P(A) \le P(B)$.
- Inclusion-exclusion for two events:
  $P(A \cup B) = P(A) + P(B) - P(A \cap B)$.

### 1.2 Derivation: complement rule

Because $A$ and $A^c$ are disjoint and $A \cup A^c = \Omega$,

$P(\Omega) = P(A \cup A^c) = P(A) + P(A^c)$,

so

$P(A^c) = 1 - P(A)$.

---

## 2. Conditional Probability

For events $A$ and $B$ with $P(B) > 0$, define

$P(A \mid B) = \dfrac{P(A \cap B)}{P(B)}$.

Interpretation: after learning that $B$ occurred, what fraction of the probability mass inside $B$ lies in $A$?

### 2.1 Rearrangement (product rule)

From the definition,

$P(A \cap B) = P(A \mid B)P(B)$.

Similarly,

$P(A \cap B) = P(B \mid A)P(A)$.

These two equalities are the algebraic bridge to Bayes' theorem.

### 2.2 Independence as a special case

$A$ and $B$ are independent if

$P(A \cap B) = P(A)P(B)$.

Equivalent statement (if $P(B)>0$):

$P(A \mid B) = P(A)$.

So independence means conditioning on one event does not change the probability of the other.

---

## 3. Bayes' Theorem

From

$P(A \cap B)=P(A\mid B)P(B)=P(B\mid A)P(A)$,

assuming $P(B)>0$:

$P(A\mid B)=\dfrac{P(B\mid A)P(A)}{P(B)}$.

This is Bayes' theorem.

### 3.1 Terminology

- $P(A)$: prior probability.
- $P(B\mid A)$: likelihood.
- $P(A\mid B)$: posterior probability.
- $P(B)$: evidence (normalizer).

### 3.2 Law of total probability (for denominator)

If $\{H_k\}$ is a partition of $\Omega$,

$P(B)=\sum_k P(B\mid H_k)P(H_k)$.

Then

$P(H_j\mid B)=\dfrac{P(B\mid H_j)P(H_j)}{\sum_k P(B\mid H_k)P(H_k)}$.

This form is what we use in diagnosis and model comparison.

---

## 4. Interpretation 1: Inverse Probability

Often we can estimate $P(B\mid A)$ from physics/biology or instrument behavior.
But what we need for decisions is $P(A\mid B)$.

Bayes' theorem performs this inversion.

Example shape:

- easy: probability test is positive given disease,
- needed: probability disease is present given test is positive.

These are not equal unless under very special conditions.

---

## 5. Interpretation 2: Belief Updating

Bayesian update in words:

posterior = prior adjusted by how compatible observations are with the hypothesis.

If observation $B$ is much more likely under $A$ than under alternatives,
posterior for $A$ increases.

If $B$ is common under many alternatives,
posterior change is small because evidence is weakly discriminative.

---

## 6. Odds form of Bayes (useful in practice)

For hypothesis $H$ vs $\neg H$, define odds:

$\text{Odds}(H)=\dfrac{P(H)}{P(\neg H)}$.

Then Bayes can be written as

$\text{Posterior odds} = \text{Prior odds} \times \text{Likelihood ratio}$,

where likelihood ratio is

$\dfrac{P(B\mid H)}{P(B\mid \neg H)}$.

This form is common in medical diagnostics and risk stratification.

---

## 7. Worked Example A: Medical Diagnostic Test

Suppose:

- prevalence of disease: $P(D)=0.01$,
- sensitivity: $P(+\mid D)=0.95$,
- specificity: $P(-\mid \neg D)=0.90$.

Then false positive rate is

$P(+\mid \neg D)=0.10$.

We want $P(D\mid +)$.

By Bayes:

$P(D\mid +)=\dfrac{P(+\mid D)P(D)}{P(+)}$.

Compute denominator by total probability:

$P(+)=P(+\mid D)P(D)+P(+\mid \neg D)P(\neg D)$

$=0.95\cdot0.01 + 0.10\cdot0.99$

$=0.0095+0.099=0.1085$.

Now posterior:

$P(D\mid +)=\dfrac{0.0095}{0.1085}\approx0.0876$.

So a positive result means only about 8.76% posterior probability of disease in this low-prevalence setting.

Key lesson: base rates matter.

---

## 8. Worked Example B: Biomaterials Screening Context

A toy scenario for implant coating quality screening.

Let

- $Q$: coating truly meets target adhesion threshold,
- $T$: lab assay reports "pass".

Suppose process historically yields

$P(Q)=0.80$.

Assay performance:

- true pass rate for good coating: $P(T\mid Q)=0.92$,
- false pass rate for bad coating: $P(T\mid \neg Q)=0.15$.

Question: if assay says pass, what is probability coating is truly good?

Bayes:

$P(Q\mid T)=\dfrac{P(T\mid Q)P(Q)}{P(T\mid Q)P(Q)+P(T\mid\neg Q)P(\neg Q)}$.

Substitute:

$P(Q\mid T)=\dfrac{0.92\cdot0.80}{0.92\cdot0.80 + 0.15\cdot0.20}$

$=\dfrac{0.736}{0.736+0.03}=\dfrac{0.736}{0.766}\approx0.9608$.

Interpretation: "pass" implies about 96.1% probability of true quality under these process priors.

Why this matters: posterior probability is what should drive release decisions, not raw assay pass/fail labels.

---

## 9. Multiple-hypothesis Bayes (short form)

If several classes $C_1,\dots,C_K$ are possible and mutually exclusive,

$P(C_k\mid x)=\dfrac{P(x\mid C_k)P(C_k)}{\sum_{j=1}^K P(x\mid C_j)P(C_j)}$.

This appears later in:

- Naive Bayes classifiers,
- probabilistic soft labels,
- model-based diagnosis with competing causes.

---

## 10. Frequent mistakes and corrections

1. Confusing $P(A\mid B)$ with $P(B\mid A)$.
   Correction: write both explicitly before calculating.

2. Forgetting denominator $P(B)$.
   Correction: compute with total probability.

3. Ignoring base rates.
   Correction: inspect prior odds before update.

4. Treating independence as default.
   Correction: independence is a strong assumption; justify it.

5. Using conditional probability when $P(B)=0$.
   Correction: conditioning requires positive-probability condition event in this elementary setup.

---

## 11. Micro-derivation: Bayes from product rule only

Start with product rule both ways:

$P(A\cap B)=P(A\mid B)P(B)$ and $P(A\cap B)=P(B\mid A)P(A)$.

Set equal:

$P(A\mid B)P(B)=P(B\mid A)P(A)$.

Divide by $P(B)$ (assuming positive):

$P(A\mid B)=\dfrac{P(B\mid A)P(A)}{P(B)}$.

Done.

---

## 12. Bridge to 1.2.2 (MLE vs MAP)

MAP estimation is Bayes' theorem applied to parameters:

$P(\theta\mid \mathcal{D}) \propto P(\mathcal{D}\mid\theta)P(\theta)$.

- MLE picks $\theta$ maximizing likelihood $P(\mathcal{D}\mid\theta)$.
- MAP picks $\theta$ maximizing posterior $P(\theta\mid\mathcal{D})$.

So this note is the conceptual prerequisite for the next one.

---

## 13. Quick self-check questions

1. Why can a high-sensitivity test still produce many false alarms in low-prevalence populations?
2. In a two-hypothesis case, what term in Bayes controls evidence strength from data alone?
3. If prior odds are 1:9 and likelihood ratio is 20, what are posterior odds?
4. What assumption is needed to write $P(A\mid B)=P(A)$?

---

## 14. Suggested references

- Murphy, 2022, chapters on probability and Bayesian inference.
- Bishop, 2006, probabilistic modeling preliminaries.
- Jaynes, 2003, interpretation of probability as logic under uncertainty.

(Full entries in `references.bib`.)

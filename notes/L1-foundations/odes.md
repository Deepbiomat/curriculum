# 1.3.1 Linear ODEs and Separation of Variables

**Learning objective:** Solve first-order linear ordinary differential equations (ODEs) using separation of variables. Understand initial conditions and general solutions.

---

## Definition and Linearity

An **ordinary differential equation (ODE)** is an equation involving a function $y(t)$ and its derivatives:

$$F(t, y, y', y'', \ldots, y^{(n)}) = 0$$

**Linear ODE** of order $n$:
$$a_n(t) y^{(n)} + a_{n-1}(t) y^{(n-1)} + \cdots + a_1(t) y' + a_0(t) y = f(t)$$

- If $f(t) = 0$: **homogeneous**
- If $f(t) \neq 0$: **non-homogeneous**
- If all $a_i$ are constants: **constant-coefficient**

**First-order form** (focus here):
$$\frac{dy}{dt} + p(t) y = g(t)$$

---

## Separation of Variables (First-Order)

### Homogeneous Case: $\frac{dy}{dt} = f(t)$

**Method:** Integrate both sides.

$$dy = f(t) \, dt$$
$$\int dy = \int f(t) \, dt$$
$$y(t) = F(t) + C$$

where $F(t) = \int f(t) \, dt$ and $C$ is an arbitrary constant.

**Example:** $\frac{dy}{dt} = -ky$ (exponential decay)

$$\frac{dy}{y} = -k \, dt$$
$$\ln|y| = -kt + C_1$$
$$y(t) = A e^{-kt}$$

where $A = e^{C_1}$.

### Separable Case: $\frac{dy}{dt} = f(t) g(y)$

**Method:** Separate $y$ and $t$ to opposite sides.

$$\frac{dy}{g(y)} = f(t) \, dt$$

Integrate both sides:
$$\int \frac{dy}{g(y)} = \int f(t) \, dt$$

**Example:** Logistic growth: $\frac{dP}{dt} = rP(1 - P/K)$

Separate:
$$\frac{dP}{P(1 - P/K)} = r \, dt$$

Use partial fractions:
$$\frac{1}{P(1 - P/K)} = \frac{1}{P} + \frac{1/K}{1 - P/K}$$

Integrate:
$$\ln P - \ln(1 - P/K) = rt + C$$
$$\ln \frac{P}{1 - P/K} = rt + C$$

Solve for $P(t)$:
$$P(t) = \frac{K e^{rt + C}}{1 + e^{rt + C}} = \frac{K}{1 + A e^{-rt}}$$

where $A = e^{-C}$.

---

## Linear First-Order ODEs: Integrating Factor Method

For $\frac{dy}{dt} + p(t) y = g(t)$:

**Step 1:** Compute integrating factor
$$\mu(t) = e^{\int p(t) \, dt}$$

**Step 2:** Multiply both sides by $\mu(t)$:
$$\mu(t) \frac{dy}{dt} + \mu(t) p(t) y = \mu(t) g(t)$$

Left side is the derivative of $\mu(t) y$:
$$\frac{d}{dt}[\mu(t) y] = \mu(t) g(t)$$

**Step 3:** Integrate:
$$\mu(t) y = \int \mu(t) g(t) \, dt + C$$

**Example:** $\frac{dy}{dt} + 2y = e^{-t}$

Integrating factor: $\mu(t) = e^{\int 2 \, dt} = e^{2t}$

Multiply both sides:
$$e^{2t} \frac{dy}{dt} + 2 e^{2t} y = e^{t}$$

$$\frac{d}{dt}[e^{2t} y] = e^{t}$$

Integrate:
$$e^{2t} y = e^{t} + C$$

$$y(t) = e^{-t} + C e^{-2t}$$

---

## Initial Conditions and Unique Solutions

An **initial value problem (IVP)** specifies:
- ODE: $\frac{dy}{dt} + p(t) y = g(t)$
- Initial condition: $y(t_0) = y_0$

The general solution contains an arbitrary constant $C$. The initial condition **fixes** $C$ uniquely.

**Example:** $\frac{dy}{dt} = -2y$ with $y(0) = 3$

General solution: $y(t) = A e^{-2t}$

Apply initial condition: $y(0) = 3 \Rightarrow A = 3$

**Particular solution:** $y(t) = 3 e^{-2t}$

---

## Qualitative Behavior (Without Solving)

For autonomous ODEs $\frac{dy}{dt} = f(y)$:

- **Equilibrium:** $\frac{dy}{dt} = 0 \Rightarrow f(y^*) = 0$
- **Stability:** If $f'(y^*) < 0$, equilibrium is **stable** (nearby solutions converge)
- **Stability:** If $f'(y^*) > 0$, equilibrium is **unstable** (solutions diverge)

**Example:** $\frac{dy}{dt} = y(1 - y)$ (logistic)

Equilibria: $y^* = 0$ (unstable, $f'(0) = 1 > 0$) and $y^* = 1$ (stable, $f'(1) = -1 < 0$)

Any solution with $0 < y(0) < 1$ will approach $y = 1$ as $t \to \infty$.

---

## Connection to Materials & Biology

**Drug concentration in tissue:** Assume linear clearance (first-order kinetics)
$$\frac{dC}{dt} = -k C$$
Solution: $C(t) = C_0 e^{-kt}$ (half-life = $\frac{\ln 2}{k}$)

**Polymer degradation:** For hydrolytic breakdown at constant rate
$$\frac{dM}{dt} = -\alpha$$
Solution: $M(t) = M_0 - \alpha t$ (linear, not exponential)

**Biomaterial diffusion (Fick's law, 1D, constant $D$):**
$$\frac{\partial c}{\partial t} = D \frac{\partial^2 c}{\partial x^2}$$
This is a **PDE**, but its solutions often involve separation of variables (see 1.3.2).

---

## Summary

| Method | Form | Solution |
|--------|------|----------|
| Direct integration | $y' = f(t)$ | $y = \int f(t) \, dt + C$ |
| Separation of variables | $y' = f(t)g(y)$ | $\int \frac{dy}{g(y)} = \int f(t) \, dt + C$ |
| Integrating factor | $y' + py = g(t)$ | $\mu = e^{\int p \, dt}$; solve $(\mu y)' = \mu g$ |
| Equilibrium analysis | $y' = f(y)$ | Stability: sign of $f'(y^*)$ |

**Key insight:** Linear ODEs are solvable in closed form. PDEs and nonlinear ODEs often require numerical methods or approximations (studied in L3).

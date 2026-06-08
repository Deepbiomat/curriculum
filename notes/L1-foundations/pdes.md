# 1.3.2 Heat/Diffusion Equation and PDE Intuition

**Learning objective:** Understand why partial differential equations (PDEs) are necessary for spatial systems. Develop intuition for the heat/diffusion equation as the canonical physical model. Connect separation of variables from ODEs to PDEs.

---

## From ODEs to PDEs: Why Space Matters

### Single-Point Systems (ODE)

An ODE describes a system with **one degree of freedom**:
$$\frac{dC}{dt} = -kC$$

Example: Drug concentration in blood (well-mixed, uniform). $C(t)$ is the *only* unknown—where it is doesn't matter.

**Assumption:** The system is homogeneous (same C everywhere).

### Extended Systems (PDE)

Reality: Concentration varies in **space and time**. A polymer matrix is not well-mixed. Solute concentration depends on position **and** time:

$$C(x,t) = \text{concentration at position } x \text{ at time } t$$

Now we need a **partial differential equation** (PDE), not an ODE.

---

## Fick's Law: The Physical Principle

Diffusion is driven by a **concentration gradient** (steepness of the C(x) curve):

$$J = -D \frac{\partial C}{\partial x}$$

where:
- $J$ = flux (how much solute crosses a plane per unit area per unit time)
- $D$ = diffusion coefficient (how fast molecules move)
- $\frac{\partial C}{\partial x}$ = concentration gradient (steepness)

**Intuition:** Molecules move from high to low concentration. A steeper gradient means faster flux.

---

## The Heat/Diffusion Equation (1D)

### Derivation: Conservation of Mass

Consider a thin slab from $x$ to $x + dx$. Mass in = mass out + accumulation:

$$\text{Flux in} - \text{Flux out} = \text{Rate of accumulation}$$

$$J(x) - J(x+dx) = \frac{\partial C}{\partial t} \cdot dx$$

Substitute Fick's law:
$$-D\frac{\partial C}{\partial x}\bigg|_x - \left(-D\frac{\partial C}{\partial x}\bigg|_{x+dx}\right) = \frac{\partial C}{\partial t} \cdot dx$$

Taylor expand: $\frac{\partial C}{\partial x}\bigg|_{x+dx} \approx \frac{\partial C}{\partial x}\bigg|_x + \frac{\partial^2 C}{\partial x^2} dx$

$$D \frac{\partial^2 C}{\partial x^2} dx = \frac{\partial C}{\partial t} dx$$

### The Heat/Diffusion Equation

$$\frac{\partial C}{\partial t} = D \frac{\partial^2 C}{\partial x^2}$$

This is a **parabolic PDE**—the canonical model for diffusion and heat conduction.

---

## Solving the Heat Equation: Separation of Variables (PDE Method)

### Ansatz (Educated Guess)

Assume the solution has a **product form**:
$$C(x,t) = X(x) \cdot T(t)$$

(This mirrors the ODE method where we separated y and t.)

### Substitute into the PDE

$$X(x) \frac{dT}{dt} = D T(t) \frac{d^2X}{dx^2}$$

Divide both sides by $X(x) T(t)$:
$$\frac{1}{T}\frac{dT}{dt} = D \frac{1}{X}\frac{d^2X}{dx^2}$$

**Key insight:** Left side depends only on $t$, right side only on $x$. For this equation to hold for *all* $x$ and $t$, both sides must equal the same constant:

$$\frac{1}{T}\frac{dT}{dt} = D \frac{1}{X}\frac{d^2X}{dx^2} = -\lambda$$

where $\lambda > 0$ is a separation constant (negative sign chosen for stability).

### Two ODEs

**Time equation:**
$$\frac{dT}{dt} = -\lambda T \Rightarrow T(t) = A e^{-\lambda t}$$

**Space equation:**
$$\frac{d^2X}{dx^2} = -\frac{\lambda}{D} X$$

Define $k^2 = \lambda/D$:
$$\frac{d^2X}{dx^2} + k^2 X = 0 \Rightarrow X(x) = B\sin(kx) + C\cos(kx)$$

### General Solution

The general solution is a **superposition** (infinite sum) of modes:

$$C(x,t) = \sum_{n=1}^{\infty} A_n \sin\left(\frac{n\pi x}{L}\right) e^{-D(n\pi/L)^2 t}$$

(assuming the slab has length $L$ and zero-concentration boundary conditions at the edges).

---

## Boundary and Initial Conditions

### Why They Matter

The PDE alone is not enough to find $C(x,t)$. We need:

**Boundary conditions (BC):** Constraints at the edges ($x=0$ and $x=L$)
- Dirichlet: $C(0,t) = C_0$ (fixed concentration at edge)
- Neumann: $\frac{\partial C}{\partial x}|_{x=0} = 0$ (no flux out—sealed edge)
- Robin: $-D \frac{\partial C}{\partial x}|_{x=0} = h(C - C_{\text{outside}})$ (flux proportional to difference)

**Initial condition (IC):** Concentration profile at $t=0$
- $C(x,0) = f(x)$ (prescribed starting distribution)

### Physical Example: Dye Diffusion

- **Domain:** Polymer slab from $x=0$ to $x=L$
- **IC:** All dye at the surface: $C(x,0) = C_0$ for $x$ near 0, else 0
- **BC:** Edges sealed (no-flux): $\frac{\partial C}{\partial x}|_{x=0} = \frac{\partial C}{\partial x}|_{x=L} = 0$
- **PDE:** $\frac{\partial C}{\partial t} = D \frac{\partial^2 C}{\partial x^2}$

**What happens?** Dye spreads inward over time. The shape flattens exponentially (the temperature of a cooling rod, the concentration of a spreading drug).

---

## Qualitative Behavior Without Solving

### Diffusive Smoothing

The heat equation **always smooths** spatial variations over time:
- Sharp peaks diffuse out
- Steep gradients decrease
- Eventually, the system equilibrates to a uniform value (if no source)

### Speed: Diffusion Length

A useful scale for diffusion distance in time $t$:
$$l_D = \sqrt{Dt}$$

Solute diffuses roughly distance $l_D$ in time $t$. For example:
- In water: $D \approx 10^{-5}$ cm²/s → in 1 second, diffusion distance ~ 0.3 mm
- In polymer: $D \approx 10^{-9}$ cm²/s → in 1 second, diffusion distance ~ 3 μm

This $l_D$ scaling is key to understanding transport in materials.

---

## Connection to Biomaterials and Beyond

### Drug Delivery from a Polymer

A polymer sphere loaded with drug. Drug diffuses out according to Fick's law:
$$\frac{\partial C}{\partial t} = D_{\text{polymer}} \nabla^2 C$$

(In spherical symmetry: $\nabla^2 C = \frac{1}{r^2}\frac{d}{dr}\left(r^2 \frac{dC}{dr}\right)$)

Boundary condition: $C(R, t) = C_{\text{sink}}$ (body removes drug at the surface).

Solution: Drug release rate $\propto \sqrt{t}$ (Higuchi model, used in pharmaceutical design).

### Tissue Engineering Scaffold

A porous scaffold must allow nutrients to diffuse inward. The maximum pore depth is limited by diffusion length:

$$\text{Max depth} \sim \sqrt{D_{\text{nutrient}} \cdot t_{\text{viable}}}$$

Cells die if nutrients can't reach them in time $t_{\text{viable}}$. Engineering controls pore size to match this.

### Continuum Mechanics (Foreshadow: L1.5)

Stress and strain in materials also satisfy PDEs (but hyperbolic, not parabolic). Separation of variables works there too—we'll see wave equations with similar structure.

---

## Summary

| Concept | Meaning |
|---------|---------|
| PDE | Equation involving spatial and temporal derivatives |
| Fick's Law | $J = -D \nabla C$ (flux driven by gradient) |
| Heat/Diffusion | $\frac{\partial C}{\partial t} = D \nabla^2 C$ |
| Separation of Variables | Assume $C(x,t) = X(x)T(t)$, split into two ODEs |
| Boundary Conditions | Constraints at $x=0, x=L$ (Dirichlet, Neumann, Robin) |
| Initial Condition | Starting profile $C(x,0)$ |
| Diffusion Length | $l_D = \sqrt{Dt}$ — characteristic distance in time $t$ |

**Key intuition:** The heat equation describes how concentration smooths and spreads. Separation of variables breaks the PDE into spatial modes (standing waves) that decay exponentially in time. This is the foundational model for all transport processes in materials.

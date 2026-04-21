# 1.1.1 Vector Spaces, Bases, and Change of Basis

## Vector Spaces

A **vector space** $V$ over a field $\mathbb{F}$ (typically $\mathbb{R}$ or $\mathbb{C}$) is a set with two operations:
- **Vector addition**: $V \times V \to V$
- **Scalar multiplication**: $\mathbb{F} \times V \to V$

Satisfying eight axioms: associativity, commutativity, identity, inverses for addition; and compatibility, identity, distributivity for scalar multiplication.

### Key Examples

| Space | Description | Dimension |
|-------|-------------|-----------|
| $\mathbb{R}^n$ | Coordinate vectors | $n$ |
| $\mathbb{P}_n$ | Polynomials of degree $\leq n$ | $n+1$ |
| $M_{m \times n}$ | $m \times n$ matrices | $mn$ |
| $C[a,b]$ | Continuous functions on $[a,b]$ | Infinite |

## Subspaces

A **subspace** $W \subseteq V$ is a non-empty subset closed under:
1. Addition: $\mathbf{u}, \mathbf{v} \in W \Rightarrow \mathbf{u} + \mathbf{v} \in W$
2. Scalar multiplication: $\mathbf{u} \in W, c \in \mathbb{F} \Rightarrow c\mathbf{u} \in W$

## Linear Independence

Vectors $\{\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_n\}$ are **linearly independent** if:

$$c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \cdots + c_n\mathbf{v}_n = \mathbf{0} \Rightarrow c_1 = c_2 = \cdots = c_n = 0$$

Otherwise, they are **linearly dependent**.

## Basis

A **basis** for $V$ is a set of vectors $\{\mathbf{b}_1, \mathbf{b}_2, \ldots, \mathbf{b}_n\}$ that is:
1. **Linearly independent**
2. **Spans** $V$ (every $\mathbf{v} \in V$ can be written as a linear combination)

The **dimension** of $V$ is the number of vectors in any basis.

### Standard Bases

- $\mathbb{R}^n$: $\{\mathbf{e}_1, \ldots, \mathbf{e}_n\}$ where $\mathbf{e}_i$ has 1 in position $i$
- $\mathbb{P}_n$: $\{1, x, x^2, \ldots, x^n\}$
- $M_{2 \times 2}$: $\{E_{11}, E_{12}, E_{21}, E_{22}\}$ (matrix units)

## Change of Basis

Given two bases $\mathcal{B} = \{\mathbf{b}_1, \ldots, \mathbf{b}_n\}$ and $\mathcal{C} = \{\mathbf{c}_1, \ldots, \mathbf{c}_n\}$ for $V$:

### Coordinate Vectors

For $\mathbf{v} \in V$:
- $[\mathbf{v}]_{\mathcal{B}}$: coordinates in basis $\mathcal{B}$
- $[\mathbf{v}]_{\mathcal{C}}$: coordinates in basis $\mathcal{C}$

### Change of Basis Matrix

The **change of basis matrix** from $\mathcal{B}$ to $\mathcal{C}$ is:

$$P_{\mathcal{C} \leftarrow \mathcal{B}} = \begin{bmatrix} [\mathbf{b}_1]_{\mathcal{C}} & [\mathbf{b}_2]_{\mathcal{C}} & \cdots & [\mathbf{b}_n]_{\mathcal{C}} \end{bmatrix}$$

Transformation:
$$[\mathbf{v}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}$$

Properties:
- $P_{\mathcal{B} \leftarrow \mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}}^{-1}$
- $P_{\mathcal{D} \leftarrow \mathcal{B}} = P_{\mathcal{D} \leftarrow \mathcal{C}} \cdot P_{\mathcal{C} \leftarrow \mathcal{B}}$ (composition)

## Key Insights

1. **Basis choice affects coordinates, not the vector itself**
2. **Orthonormal bases** simplify projections and inner products
3. **Gram-Schmidt** converts any basis to an orthonormal basis
4. Change of basis is equivalent to: viewing the same object through different coordinate systems

## Exit Check

- [ ] Can prove linear independence of a given set
- [ ] Can find basis for a subspace
- [ ] Can construct change of basis matrix given two bases
- [ ] Can verify $P_{\mathcal{C} \leftarrow \mathcal{B}} \cdot P_{\mathcal{B} \leftarrow \mathcal{C}} = I$

# System Theory: General Concepts (DT & CT)

## Jordan Form
### Definition and Structure

> [!danger] Definition: Jordan Form
> A matrix $J \in \mathbb{C}^{n \times n}$ is said to be in Jordan Form if, possibly after row-column permutations, it can be written as:
> $$
> J = \begin{bmatrix}
> J_1 & & \boldsymbol{\oslash} \\
> & \ddots & \\
> \boldsymbol{\oslash} & & J_r
> \end{bmatrix}
> $$
> Where $J_i$ is the **Jordan Block** associated with eigenvalue $\lambda_i$.
> Note: $\lambda_i \neq \lambda_j$ if $i \neq j$.

Inside each Jordan block $J_i$, we have sub-blocks called **Jordan Miniblocks**:
$$
J_i = \begin{bmatrix}
J_{i1} & & \boldsymbol{\oslash} \\
& \ddots & \\
\boldsymbol{\oslash} & & J_{is_i}
\end{bmatrix} \in \mathbb{C}^{n_i \times n_i}
$$
The generic $k$-th Jordan Miniblock associated with $\lambda_i$ is denoted $J_{ik}$:
$$
J_{ik} = \begin{bmatrix}
\lambda_i & 1 & & \boldsymbol{\oslash} \\
& \lambda_i & \ddots & \\
& & \ddots & 1 \\
\boldsymbol{\oslash} & & & \lambda_i
\end{bmatrix}
$$
Usually, the sizes are ordered: $n_{i1} \ge n_{i2} \ge \dots \ge n_{is_i}$.

#### Multiplicities
* **Algebraic Multiplicity ($n_i$):** The size of the Jordan Block $J_i$. It is the sum of the sizes of the miniblocks: $n_i = \sum_k \dim(J_{ik})$.
* **Geometric Multiplicity ($s_i$):** The number of Jordan Miniblocks associated with $\lambda_i$.

> [!success] Formula: Geometric Multiplicity
> The geometric multiplicity corresponds to the dimension of the kernel of $(J - \lambda I)$:
> $$s_i = \dim(\ker(\lambda_i I_n - J)) = n - \text{rank}(\lambda_i I_n - J)$$

---

### Minimal Polynomial

> [!danger] Definition: Annihilating Polynomial
> Given a matrix $F \in \mathbb{R}^{n \times n}$, a polynomial $p(s) \in \mathbb{R}[s]$ is said to be an **Annihilating Polynomial** of $F$ if:
> $$p(F) = p_d F^d + \dots + p_1 F + p_0 I = \boldsymbol{0}_{n \times n}$$

If we consider the set $\mathcal{P}_F$ of all annihilating polynomials of $F$, there exists a monic polynomial of minimal degree in $\mathcal{P}_F$, denoted $\Psi_F(s)$, such that any $p(s) \in \mathcal{P}_F$ is a multiple of $\Psi_F(s)$.
$\Psi_F(s)$ is called the **Minimal Polynomial** of the matrix $F$.

> [!success] Formula: Minimal Polynomial in Jordan Form
> It is possible to prove that if $J$ is in Jordan form:
> $$\Psi_J(s) = (s - \lambda_1)^{n_{11}} (s - \lambda_2)^{n_{21}} \dots (s - \lambda_r)^{n_{r1}}$$
> Where $n_{i1}$ is the dimension of the **largest** miniblock associated with $\lambda_i$.

---

### Examples

> [!example] Example 1: Identifying Multiplicities
> Consider the matrix $J$:
> $$
> J = \begin{bmatrix}
> \boxed{\begin{smallmatrix} 2 & 1 \\ 0 & 2 \end{smallmatrix}} & \boldsymbol{0} & \boldsymbol{0} \\
> \boldsymbol{0} & \boxed{\begin{smallmatrix} 2 & 1 \\ 0 & 2 \end{smallmatrix}} & \boldsymbol{0} \\
> \boldsymbol{0} & \boldsymbol{0} & \boxed{3}
> \end{bmatrix}
> $$
> **Eigenvalues:** $\lambda_1 = 2$, $\lambda_2 = 3$.
> **Analysis for $\lambda_1=2$:**
> * Algebraic Multiplicity $n_1 = 2+2 = 4$.
> * Geometric Multiplicity $s_1 = 2$ (because there are 2 miniblocks).
>
> **Calculation of Geometric Multiplicity:**
> We know $\dim(\ker(\lambda I - J)) = n - \text{rank}(\lambda I - J)$.
> Let's check for $\lambda_1=2$:
> $$J - 2I = \begin{bmatrix} 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 \end{bmatrix}$$
> The rank is 3 (non-zero rows).
> $\dim(\ker(J-2I)) = 5 - 3 = 2$. This matches the number of miniblocks.

> [!example] Example 2: Structure of J
> $$
> J = \begin{bmatrix}
> 1 & 1 & 0 & 0 & 0 & 0 \\
> 0 & 1 & 0 & 0 & 0 & 0 \\
> 0 & 0 & 2 & 1 & 0 & 0 \\
> 0 & 0 & 0 & 2 & 0 & 0 \\
> 0 & 0 & 0 & 0 & 2 & 1 \\
> 0 & 0 & 0 & 0 & 0 & 2 \\
> 0 & 0 & 0 & 0 & 0 & 0 & 1
> \end{bmatrix} \quad \text{(Note: simplified representation from image)}
> $$
> **Eigenvalues:**
> * $\lambda_1 = 1$: $n_1 = 3$ (Alg), $s_1 = 2$ (Geom - number of miniblocks).
> * $\lambda_2 = 2$: $n_2 = 3$ (Alg), $s_2 = 1$ (Geom).
> * $\lambda_3 = 0$: $n_3 = 1$ (Alg), $s_3 = 1$ (Geom).

> [!example] Example 3: Minimal Polynomial Calculation
> Given:
> * $\lambda_1 = 2, n_1 = 4, s_1 = 2$.
> * $\lambda_2 = 1, n_2 = 4, s_2 = 3$.
> * $\lambda_3 = 0, n_3 = 3, s_3 = 2$.
>
> Looking at the largest blocks in the image:
> * For $\lambda=2$: Largest block has size 3.
> * For $\lambda=1$: Largest block has size 2.
> * For $\lambda=0$: Largest block has size 2.
>
> $$\Psi_J(s) = (s-2)^3 (s-1)^2 (s-0)^2$$

> [!example] Example 4: Reconstructing J
> **Given Information:**
> * $\lambda_1 = 2, n_1 = 3, s_1 = 2$
> * $\lambda_2 = 3, n_2 = 2, s_2 = 2$
> * $\lambda_3 = 1, n_3 = 4, s_3 = 2$
> * Additional Info: $\Psi_J(s) = (s-2)^2 (s-3) (s-1)^2$
>
> **Deduction:**
> 1.  **$\lambda=2$:** Largest block is size 2 (from $\Psi$). Total size 3. $s=2$ implies 2 blocks. Combination must be: **[2, 1]**.
> 2.  **$\lambda=3$:** Largest block size 1. Total size 2. $s=2$ implies 2 blocks. Combination must be: **[1, 1]**.
> 3.  **$\lambda=1$:** Largest block size 2. Total size 4. $s=2$ implies 2 blocks. Combination must be: **[2, 2]**.

---

## Powers of a Matrix in Jordan Form

To compute $J^t$, since $J$ is block diagonal, we only need to compute the power of the generic Jordan Miniblock $J_\lambda \in \mathbb{C}^{\nu \times \nu}$.
This is crucial for computing the matrix exponential in [Continuous Time](CT.md#matrix-exponential--time-response) and matrix powers in [Discrete Time](DT.md#time-response-evolution).

We can write:
$$J_\lambda = \lambda I_\nu + J_0$$
Where $J_0$ is a nilpotent matrix (zeros on diagonal, 1s on superdiagonal).

> [!success] Formula: Power of a Miniblock
> Using Newton's Binomial formula for scalars $(a+b)^t = \sum_{i=0}^t \binom{t}{i} a^{t-i} b^i$:
>
> $$J_\lambda^t = (\lambda I + J_0)^t = \sum_{i=0}^{t} \binom{t}{i} (\lambda)^{t-i} (J_0)^i$$
>
> Since $J_0^\nu = 0$, the sum is finite. The result behaves like a scalar expansion:
> $$
> J_\lambda^t = \begin{bmatrix}
> \lambda^t & \binom{t}{1}\lambda^{t-1} & \binom{t}{2}\lambda^{t-2} & \dots \\
> 0 & \lambda^t & \binom{t}{1}\lambda^{t-1} & \dots \\
> 0 & 0 & \lambda^t & \dots \\
> \vdots & \vdots & \vdots & \ddots
> \end{bmatrix}
> $$
> Note: If $\lambda=0$, then $J_0^t$ is simply a matrix shifting the diagonal of 1s to the right as $t$ increases, eventually becoming 0 for $t \ge \nu$.

---
## General Stability Definitions

> [!danger] Definition: Equilibrium Point (General Concept)
> A state $x_e$ is an equilibrium point if, starting at $x_e$, the system state remains at $x_e$ for all future time.
> * **DT:** $x(t+1) = x(t) = x_e$ (See [DT Stability](DT.md#stability--equilibrium-points))
> * **CT:** $\dot{x}(t) = 0 \implies x(t) = \text{const}$ (See [CT Stability](CT.md#stability-criteria-ct))

> [!danger] Definition: Stability Types
> The definitions of stability for an equilibrium point $x_e$ are formally the same in both cases:
>
> 1.  **Stable (Lyapunov):** The state stays close to $x_e$ if it starts close to $x_e$.
> 2.  **Attractive:** The state converges to $x_e$ as $t \to \infty$ if it starts close enough.
> 3.  **Asymptotically Stable:** If it is both Stable and Attractive.

> [!info] Linearization Logic
> For both DT and CT Non-Linear systems, we approximate the dynamics around an equilibrium pair $(x_e, \bar{u})$ using **Taylor Expansion** (truncating higher-order terms).
>
> We define deviations:
> * $\delta x(t) = x(t) - x_e$
> * $\delta u(t) = u(t) - \bar{u}$
> * $\delta y(t) = y(t) - y_e$

---
## Reachability vs. Controllability

> [!danger] Definition: Reachability
> Given some time $T > 0$ finite, and some state $x_f \in \mathbb{X}$, can I find an input signal $u(t), t \in [0, T]$ that drives the state of the system from $x(0)=0$ to $x(T)=x_f$?
> 
> [!danger] Definition: Zero Controllability (or Controllability to Zero)
> Given some time $T > 0$ and some state $x_0 \in \mathbb{X}$, can I find an input signal $u(t), t \in [0, T]$ that drives the state of the system from $x(0)=x_0$ to $x(T)=0$?
> 

---
### Cayley-Hamilton Theorem

> [!warning] Theorem: Cayley-Hamilton
> Given $F \in \mathbb{D}^{n \times n}$, let $\Delta_F(z) = z^n + a_{n-1}z^{n-1} + \dots + a_0$ be its characteristic polynomial (i.e., $\det(zI_n - F)$).
> Then $\Delta_F(z)$ is an **annihilating polynomial** of $F$, i.e.:
> $$\Delta_F(F) = F^n + a_{n-1}F^{n-1} + \dots + a_1 F + a_0 I_n = \boldsymbol{0}_{n \times n}$$
> This implies:
> $$F^n = - \sum_{i=0}^{n-1} a_i F^i$$
> *Consequence:* Any power $F^k$ with $k \ge n$ can be written as a linear combination of $\{I, F, \dots, F^{n-1}\}$.

### Change of Basis & Algebraic Equivalence

We assume to change the basis of the state space $\mathbb{X}$.
Old Basis: $B_x = \{v_1, \dots, v_n\}$
New Basis: $\bar{B}_x = \{\bar{v}_1, \dots, \bar{v}_n\}$

We relate the vectors via a non-singular transformation matrix $T \in \mathbb{C}^{n \times n}$:
$$[\bar{v}_1 | \dots | \bar{v}_n] = [v_1 | \dots | v_n] T$$
Consequently, if $x(t)$ are coords in $B_x$ and $\tilde{x}(t)$ are coords in $\bar{B}_x$:
$$x(t) = T \tilde{x}(t) \iff \tilde{x}(t) = T^{-1}x(t)$$

> [!success] Formula: Algebraically Equivalent System
> Applying the transformation to the State-Space Model $\Sigma = (F, G, H, D)$:
> $$
> \begin{cases}
> \tilde{x}(t+1) = T^{-1}FT \tilde{x}(t) + T^{-1}G u(t) \\
> y(t) = HT \tilde{x}(t) + D u(t)
> \end{cases}
> $$
> The new system $\tilde{\Sigma} = (\tilde{F}, \tilde{G}, \tilde{H}, \tilde{D})$ is defined as:
> * $\tilde{F} = T^{-1}FT$
> * $\tilde{G} = T^{-1}G$
> * $\tilde{H} = HT$
> * $\tilde{D} = D$

> [!danger] Definition: Algebraic Equivalence
> Two systems $\Sigma$ and $\tilde{\Sigma}$ of the same dimension are **Algebraically Equivalent** if they represent the same system with two different bases in $\mathbb{X}$, meaning there exists a non-singular matrix $T$ satisfying the relations above.

---
## Inner Product and Orthogonality

> [!danger] Definition: Inner Product
> Given a vector space $V$ over $\mathbb{R}$, an **inner product** is a function $\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}$ that satisfies 3 properties:
> 1.  **Symmetry:** $\forall v_1, v_2 \in V, \quad \langle v_1, v_2 \rangle = \langle v_2, v_1 \rangle$.
> 2.  **Bilinearity:** $\forall v_1, v_2, v \in V, \forall \alpha_1, \alpha_2 \in \mathbb{R}$:
>     $\langle \alpha_1 v_1 + \alpha_2 v_2, v \rangle = \alpha_1 \langle v_1, v \rangle + \alpha_2 \langle v_2, v \rangle$.
> 3.  **Positive Definiteness:** $\forall v \in V, \langle v, v \rangle \ge 0$ and $\langle v, v \rangle = 0 \iff v = 0$.

> [!danger] Definition: Orthogonality
> Two vectors $v_1, v_2 \in V$ are said to be **orthogonal** ($v_1 \perp v_2$) if $\langle v_1, v_2 \rangle = 0$.

> [!danger] Definition: Orthogonal Complement
> Let $U$ be a subspace of $V$. The orthogonal complement is:
> $$U^\perp \triangleq \{ v \in V : \langle v, u \rangle = 0, \forall u \in U \}$$

> [!info] Properties
> a) $(U^\perp)^\perp \supseteq U$ (Equality holds in finite dimensional spaces).
> b) $U \cap U^\perp = \{0\}$.
> c) If $V$ is finite dimensional: $V = U \oplus U^\perp$ (Direct Sum).

# Linear Algebra Tools

## Adjoint Transformations

> [!danger] Definition: Adjoint Transformation
> Let $V$ and $W$ be two vector spaces over $\mathbb{R}$. Assume we have defined two inner products: $\langle \cdot, \cdot \rangle_V$ in $V$ and $\langle \cdot, \cdot \rangle_W$ in $W$.
>
> Let $\mathcal{A}: V \to W$ be a linear transformation.
> A linear transformation $\mathcal{A}^*: W \to V$ is said to be the **Adjoint** of $\mathcal{A}$ if:
> $$\langle \mathcal{A}(v), w \rangle_W = \langle v, \mathcal{A}^*(w) \rangle_V \quad \forall v \in V, \forall w \in W$$
>
> **Remark:** $\mathcal{A}^*$ doesn't necessarily exist, but if it exists, it is **unique**.

### Case 1: Finite Dimensional Spaces
Assume $V = \mathbb{R}^k$ and $W = \mathbb{R}^p$.
Assume standard inner products (dot product):
* $\langle v_1, v_2 \rangle_V \triangleq v_1^\top v_2$
* $\langle w_1, w_2 \rangle_W \triangleq w_1^\top w_2$

If $\mathcal{A}: V \to W$ is a linear transformation represented by a matrix $A \in \mathbb{R}^{p \times k}$ (where $\mathcal{A}(v) = Av$), we want to show how $\mathcal{A}^*$ is represented.

> [!success] Formula: Adjoint Matrix
> $\mathcal{A}^*$ is represented by the transpose matrix $A^\top$.
> $$\mathcal{A}^*: W \to V$$
> $$w \mapsto A^\top w$$

**Proof:**
For every $v \in V, w \in W$:
$$
\begin{aligned}
\langle \mathcal{A}v, w \rangle_W &= (Av)^\top w \\
&= v^\top A^\top w \\
&= v^\top [A^\top w] \\
&= \langle v, \mathcal{A}^*(w) \rangle_V
\end{aligned}
$$
Thus, $\mathcal{A}^*(w) = A^\top w$.

---

### Case 2: Function Spaces (Infinite Dimensional)
This case is fundamental for [Continuous Time systems analysis](CT.md#reachability-operator-and-gramian).

* **Space V:** Let $V = \mathcal{U}_{[0,t]}$ be the set of piece-wise continuous functions defined on $[0,t]$ taking values in $\mathbb{U} = \mathbb{R}^m$.
    * Inner Product: $\langle u_1(\cdot), u_2(\cdot) \rangle_{\mathcal{U}_{[0,t]}} = \int_{0}^{t} u_1^\top(\tau) u_2(\tau) d\tau$
* **Space W:** Let $W = X = \mathbb{R}^n$.
    * Inner Product: $\langle x_1, x_2 \rangle_X \triangleq x_1^\top x_2$

Consider the Linear Transformation $\mathcal{A}: \mathcal{U}_{[0,t]} \to X$:
$$\mathcal{A}(u(\cdot)) = \int_{0}^{t} M(\tau)u(\tau) d\tau$$
Where $M(\tau) \in \mathbb{R}^{n \times m}$ is a matrix-valued function.

**Goal:** Identify the adjoint $\mathcal{A}^*: X \to \mathcal{U}_{[0,t]}$.
The adjoint must satisfy: $\langle \mathcal{A}(u(\cdot)), x \rangle_X = \langle u(\cdot), \mathcal{A}^*(x) \rangle_{\mathcal{U}_{[0,t]}}$.

**Derivation:**
$$
\begin{aligned}
\langle \mathcal{A}(u(\cdot)), x \rangle_X &= \left[ \int_{0}^{t} M(\tau) u(\tau) d\tau \right]^\top x \\
&= \int_{0}^{t} u^\top(\tau) M^\top(\tau) x \, d\tau \\
&= \int_{0}^{t} u^\top(\tau) [M^\top(\tau) x] \, d\tau \\
&= \langle u(\cdot), \mathcal{A}^*(x)(\cdot) \rangle_{\mathcal{U}_{[0,t]}}
\end{aligned}
$$

> [!success] Formula: Adjoint in Function Space
> The adjoint $\mathcal{A}^*$ maps a vector $x \in \mathbb{R}^n$ to a function of time:
> $$[\mathcal{A}^* x](\tau) = M^\top(\tau) x, \quad \tau \in [0, t]$$

---

## Main Properties of Adjoint Transformations

> [!warning] Theorem: Properties
> Given a linear transformation $\mathcal{A}$ and its adjoint $\mathcal{A}^*$:
>
> 1.  **Kernel Property:**
>     $$\ker \mathcal{A} = (\text{Im} \mathcal{A}^*)^\perp$$
>
> 2.  **Kernel Composition:**
>     $$\ker \mathcal{A} = \ker [\mathcal{A}^* \mathcal{A}] = \ker [\mathcal{A}^* (\mathcal{A})]$$
>     *Visualization: * $$V\xrightarrow{\mathcal{A}} W \xrightarrow{\mathcal{A}^*}V $$ 
>
> 3.  **Image Inclusion 1:**
>     $$\text{Im} \mathcal{A} \subseteq (\ker \mathcal{A}^*)^\perp$$
>
> 4.  **Image Inclusion 2:**
>     $$\text{Im} \mathcal{A} \supseteq \text{Im}(\mathcal{A} \mathcal{A}^*)$$
>
> **Note:** If $\text{Im} \mathcal{A}$ is finite dimensional, then (3) and (4) become **equalities**.

---
# General Reachability & Decomposition

## Standard Reachability Form (Kalman Decomposition)

A form to which we can reduce every non-reachable system (CT or DT) by a change of basis in $\mathbb{X}$.
The main result relies on the fact that the reachable subspace $X^R = \text{Im}(\mathcal{R})$ is $F$-invariant and includes $\text{Im}(G)$.

### Construction of the Transformation Matrix $T$
Consider a system $\Sigma = (F,G,H,D)$ that is **NOT Reachable**.
Let $\rho = \dim(X^R) = \text{rank}(\mathcal{R}) < n$.

We want to construct a non-singular matrix $T = [v_1 | \dots | v_\rho | w_{\rho+1} | \dots | w_n] \in \mathbb{R}^{n \times n}$ such that:
1.  **Reachable Part:** The first $\rho$ columns $\{v_1, \dots, v_\rho\}$ form a basis for the reachable subspace $X^R = \text{Im}(\mathcal{R})$.
2.  **Completion:** The remaining $n-\rho$ columns $\{w_{\rho+1}, \dots, w_n\}$ complete the basis for $\mathbb{R}^n$.

### Structure of the Decomposed Matrices
Using the change of basis $\bar{x} = T^{-1}x$, the new system matrices $\bar{F} = T^{-1}FT$ and $\bar{G} = T^{-1}G$ have a specific block structure:

> [!success] Formula: Standard Reachability Form
> $$
> \bar{F} = \begin{bmatrix}
> F_{11} & F_{12} \\
> \boldsymbol{0} & F_{22}
> \end{bmatrix}
> \quad
> \bar{G} = \begin{bmatrix}
> G_1 \\
> \boldsymbol{0}
> \end{bmatrix}
> \quad
> \bar{H} = \begin{bmatrix} H_1 & H_2 \end{bmatrix}
> $$
> **Dimensions:**
> * $F_{11} \in \mathbb{R}^{\rho \times \rho}$ (Reachable dynamics)
> * $F_{22} \in \mathbb{R}^{(n-\rho) \times (n-\rho)}$ (Unreachable dynamics)
> * $G_1 \in \mathbb{R}^{\rho \times m}$

![[image 16.png]]
![[image-1 7.png]]






# Continuous Time (CT) Systems

## State-Space Models

> [!danger] Definition: Continuous Time State-Space Model
> A continuous time state-space model is described by the following differential equations:
> $$
> \Sigma: \begin{cases}
> \dot{x}(t) = Fx(t) + Gu(t) & \text{(State Equation)} \\
> y(t) = Hx(t) + Du(t) & \text{(Output Equation)}
> \end{cases}
> \quad t \in \mathbb{R}
> $$
> Where:
> * $x(t) \in \mathbb{X} \triangleq \mathbb{R}^n$ (State Space)
> * $u(t) \in \mathbb{U} \triangleq \mathbb{R}^m$ (Input Alphabet)
> * $y(t) \in \mathbb{Y} \triangleq \mathbb{R}^p$ (Output Alphabet)

![[image-1 6.png]]

The system is denoted as $\Sigma = (F, G, H, D)$. It is Linear, Time-Invariant and Proper.
* If $D=0$, the system is **strictly proper**, denoted $\Sigma = (F, G, H)$.

> [!info] Block Diagram
> Unlike the [Discrete Time case](DT.md#block-diagram) (which uses a Delay $z^{-1}$), the Continuous Time model uses an **Integrator** ($\int$) to relate $\dot{x}(t)$ to $x(t)$.

## Matrix Exponential & Time Response

To solve the differential equation given initial conditions $x(0) = x_0$ and input $u(t)$, we need the concept of the Matrix Exponential.

> [!danger] Definition: Exponential of a Matrix
> Given a matrix $F \in \mathbb{C}^{n \times n}$, we define the exponential of $F$ as:
> $$e^{Ft} = \exp(Ft) \triangleq \sum_{k=0}^{+\infty} \frac{F^k t^k}{k!}$$
> The series always converges $\forall t \in \mathbb{R}$.

> [!info] Properties of $e^{Ft}$
> 1.  $e^{Ft} \big|_{t=0} = I_n$
> 2.  $\frac{d}{dt} [e^{Ft}] = F e^{Ft} = e^{Ft} F$
> 3.  $e^{Ft}$ is invertible: $[e^{Ft}]^{-1} = e^{-Ft}$
> 4.  If $v$ is an eigenvector of $F$ ($Fv = \lambda v$), then:
>     $$\underbrace{e^{Ft}}_{\text{Matrix}} v = \underbrace{e^{\lambda t}}_{\text{Scalar}} v$$

> [!success] Formula: Lagrange Formula (CT Solution)
> Using the matrix exponential, we can solve the state equation:
>
> **State Evolution:**
> $$x(t) = \underbrace{e^{Ft}x_0}_{\text{Free/Unforced } x_{\ell}(t)} + \underbrace{\int_{0}^{t} e^{F(t-\tau)} G u(\tau) d\tau}_{\text{Forced } x_f(t)}$$
>
> **Output Evolution:**
> $$y(t) = \underbrace{H e^{Ft}x_0}_{\text{Free } y_{\ell}(t)} + \underbrace{\left[ \int_{0}^{t} H e^{F(t-\tau)} G u(\tau) d\tau + D u(t) \right]}_{\text{Forced } y_f(t)}$$

### Impulse Response (CT)
We define the impulse response of the CT state-space model.

> [!danger] Definition: CT Impulse Response
> $$W(t) \triangleq D\delta(t) + H e^{Ft} G \delta_{-1}(t)$$
> Where:
> * $\delta(t)$ is the Dirac Impulse.
> * $\delta_{-1}(t)$ is the Continuous Time Step Function (Heaviside).

The forced output is the convolution:
$$y_f(t) = [W * u](t) = \int_{0}^{t} W(\tau) u(t-\tau) d\tau$$

---

## Analysis via Laplace Transform

By applying the Laplace Transform $\mathcal{L}[\cdot]$ to the state equations (assuming $x(0)=0$ for the transfer function):

$$
\begin{aligned}
sX(s) &= FX(s) + GU(s) \implies (sI_n - F)X(s) = GU(s) \\
X(s) &= (sI_n - F)^{-1}GU(s)
\end{aligned}
$$

> [!success] Formula: Transfer Matrix (CT)
> The transfer matrix of the system $\Sigma = (F, G, H, D)$ is:
> $$W(s) \triangleq H(sI_n - F)^{-1}G + D \in \mathbb{R}(s)^{p \times m}$$
> $W(s)$ is a proper rational matrix (strictly proper if $D=0$).

> [!info] Poles and Eigenvalues
> The poles of $W(s)$ are a subset of the eigenvalues of $F$ (the spectrum $\sigma(F)$).
> $$\{\text{Poles of } W(s)\} = \bigcup_{i,j} \{\text{Poles of } W_{ij}(s)\} \subseteq \{\text{Zeros of } \Delta_F(s)\} = \sigma(F)$$

---

## Modes and Jordan Form (CT)

Since every matrix $F$ is similar to a matrix in [Jordan Form](DT%20&%20CT.md#jordan-form) $J$ ($F = TJT^{-1}$), we have:
$$e^{Ft} = T e^{Jt} T^{-1}$$
The elementary modes of $e^{Ft}$ coincide with the elementary modes of $e^{Jt}$.

### Exponential of a Jordan Block
If $J$ is in Jordan form, it is block diagonal. $e^{Jt}$ is also block diagonal.
For a specific Miniblock $J_\lambda$ of size $\nu \times \nu$ associated with eigenvalue $\lambda$:

> [!success] Formula: Exponential of a Miniblock
> $$
> e^{J_\lambda t} = \begin{bmatrix}
> e^{\lambda t} & t e^{\lambda t} & \frac{t^2}{2!} e^{\lambda t} & \dots & \frac{t^{\nu-1}}{(\nu-1)!}e^{\lambda t} \\
> 0 & e^{\lambda t} & t e^{\lambda t} & \dots & \vdots \\
> \vdots & & \ddots & \ddots & \vdots \\
> 0 & \dots & \dots & 0 & e^{\lambda t}
> \end{bmatrix}
> $$
> The terms $e^{\lambda t}, t e^{\lambda t}, \dots$ are the **Elementary Modes** associated with $J_\lambda$.

> [!example] Example: Identification of Modes

Given a Matrix $J$:
 $$
J = \begin{bmatrix}
\boxed{\begin{smallmatrix} 1 \end{smallmatrix}} & 0 & 0 \\
0 & \boxed{\begin{smallmatrix} 1 & 1 \\ 0 & 1 \end{smallmatrix}} & 0 \\
0 & 0 & \boxed{\begin{smallmatrix} 2 & 1 & 0 \\ 0 & 2 & 1 \\ 0 & 0 & 2 \end{smallmatrix}}
\end{bmatrix}
\quad \text{(simplified structure for example)}
$$
* **$\lambda_1 = 1$:**
    * One block of size 1 $\to$ Mode: $e^{t}$
     * One block of size 2 $\to$ Modes: $e^{t}, t e^{t}$
 * **$\lambda_2 = 2$:**
     * One block of size 3 $\to$ Modes: $e^{2t}, t e^{2t}, \frac{t^2}{2!}e^{2t}$

---
## Non-Linear Linearization (CT)

Given a NL CT system:
$$
\begin{cases}
\dot{x}(t) = f(x(t), u(t)) \\
y(t) = h(x(t), u(t))
\end{cases}
$$
With equilibrium defined by $0 = f(x_e, \bar{u})$.

> [!success] Formula: CT Linearized Model
> The linearized dynamics of the displacement $\dot{\delta x}(t)$ are:
> $$
> \begin{cases}
> \dot{\delta x}(t) = F \delta x(t) + G \delta u(t) \\
> \delta y(t) = H \delta x(t) + D \delta u(t)
> \end{cases}
> $$
> Where the Jacobians are defined exactly as in the [DT case](DT.md#non-linear-linearization-dt) (partial derivatives evaluated at $x_e, \bar{u}$).

## Stability Criteria (CT)

See also [General Stability Definitions](DT%20&%20CT.md#general-stability-definitions).

> [!warning] Theorem: Stability via Eigenvalues (CT)
> For a Linear (or Linearized) CT system with matrix $F$:
>
> 1.  **Asymptotically Stable:** $\iff \forall \lambda \in \sigma(F), \quad \text{Re}(\lambda) < 0$
>     *(All eigenvalues strictly in the left half complex plane).*
> 2.  **Stable (Lyapunov):** $\iff \forall \lambda \in \sigma(F), \text{Re}(\lambda) \le 0$
>     *AND* for any $\lambda$ with $\text{Re}(\lambda)=0$ (imaginary axis), the Jordan miniblocks have size 1.
> 3.  **Unstable:** $\iff \exists \lambda \in \sigma(F), \text{Re}(\lambda) > 0$.

> [!info] Modes Comparison
> * **CT Converging Mode:** $e^{\lambda t} \to 0 \iff \text{Re}(\lambda) < 0$
> * **CT Bounded Mode:** $e^{\lambda t}$ bounded $\iff \text{Re}(\lambda) = 0$ (Pure oscillation/constant).

### Linearization Method for Autonomous Systems

The following proposition formalizes how to use the linearized model to determine the stability of the original non-linear system.

> [!warning] Proposition: Linearization Method
> Consider a Non-Linear (NL) Continuous Time (CT) Autonomous State-Space Model:
> $$\dot{x}(t) = f(x(t)) \quad t \in \mathbb{R}_+, \quad \dim x = n$$
>
> **Assumptions:**
> 1.  $x_e$ is an equilibrium point of the system (A).
> 2.  $f(\cdot)$ is continuous with its derivatives ($C^1$ regular).
>
> **Consider the Linearized Model:**
> $$\frac{d}{dt}[\delta x(t)] = F \delta x(t) \quad \text{where} \quad F \triangleq \left. \frac{\partial f}{\partial x} \right|_{x=x_e}$$
>
> **Stability Conclusions based on Eigenvalues $\sigma(F)$:**
> >
> * **(a) Asymptotic Stability:**
>     If $\forall \lambda \in \sigma(F), \text{Re}(\lambda) < 0$, then $x_e$ is an **Asymptotically Stable** equilibrium point of (A).
>     *(All eigenvalues are strictly in the left half-plane).*
>
> * **(b) Instability:**
>     If $\exists \lambda \in \sigma(F)$ such that $\text{Re}(\lambda) > 0$, then $x_e$ is an **Unstable** equilibrium point of (A).
>     *(At least one eigenvalue is in the right half-plane).*
>
> * **(c) Inconclusive (Critical Case):**
>     If $\nexists \lambda \in \sigma(F)$ with $\text{Re}(\lambda) > 0$ BUT $\exists \lambda \in \sigma(F)$ with $\text{Re}(\lambda) = 0$, then this method gives **NO ANSWER**.
>     *(Eigenvalues on the imaginary axis, none on the right. Stability depends on higher-order non-linear terms).*

# Continuous Time (CT) Reachability Analysis

## Reachability Operator and Gramian

> [!danger] Definition: Reachable State at time $t$
> Given a time $t > 0$, a state $x_f \in \mathbb{X} = \mathbb{R}^n$ is reachable at time $t$ if there exists an input function $u(\cdot) \in \mathcal{U}_{[0,t]}$ that drags the state of the system from $x(0)=0$ to $x(t)=x_f$.
>
> *Notation:* $\mathcal{U}_{[0,t]}$ is the set of piece-wise continuous functions defined on $[0,t]$ taking values in $\mathbb{U} = \mathbb{R}^m$.

From the Lagrange formula (assuming $x(0)=0$):
$$x(t) = x_f(t) = \int_{0}^{t} e^{F(t-\tau)} G u(\tau) d\tau$$

We deduce that $x_f$ is reachable at time $t \iff \exists u(\cdot) \in \mathcal{U}_{[0,t]}$ such that $x_f = \mathcal{R}_t(u(\cdot))$.
We define the **Reachability Operator** $\mathcal{R}_t$:
$$
\begin{aligned}
\mathcal{R}_t : \mathcal{U}_{[0,t]} &\longrightarrow X = \mathbb{R}^n \\
u(\tau) &\longmapsto \int_{0}^{t} e^{F(t-\tau)} G u(\tau) d\tau
\end{aligned}
$$
$\mathcal{R}_t$ is a Linear Transformation. Its image $\text{Im}(\mathcal{R}_t)$ is the set of reachable states at time $t$, denoted $X_t^R$.

### The Reachability Gramian ($W_t$)

To analyze $\mathcal{R}_t$, we introduce inner products and the [Adjoint Operator](DT%20&%20CT.md#adjoint-transformations).
1.  **Inner Product on $\mathcal{U}_{[0,t]}$:** $\langle u_1, u_2 \rangle_{\mathcal{U}} \triangleq \int_{0}^{t} u_1^\top(\tau) u_2(\tau) d\tau$
2.  **Inner Product on $X$:** $\langle x_1, x_2 \rangle_X \triangleq x_1^\top x_2$

The Adjoint Transformation $\mathcal{R}_t^*: X \to \mathcal{U}_{[0,t]}$ is defined as:
$$[\mathcal{R}_t^* x](\tau) = G^\top e^{F^\top(t-\tau)} x, \quad \tau \in [0,t]$$

Exploiting the property that $\text{Im}(\mathcal{R}_t)$ is finite dimensional, we claim $\text{Im}(\mathcal{R}_t) = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*)$.
We compute the composition $\mathcal{R}_t \mathcal{R}_t^*$:
$$\mathcal{R}_t \mathcal{R}_t^* x = \int_{0}^{t} e^{F(t-\tau)} G G^\top e^{F^\top(t-\tau)} x \, d\tau = \left[ \int_{0}^{t} e^{F(t-\tau)} G G^\top e^{F^\top(t-\tau)} d\tau \right] x$$

> [!success] Definition: Reachability Gramian
> The matrix resulting from the composition is called the **Reachability Gramian** at time $t$:
> $$W_t \triangleq \int_{0}^{t} e^{F(t-\tau)} G G^\top e^{F^\top(t-\tau)} d\tau \in \mathbb{R}^{n \times n}$$
>
> **Property:** $X_t^R = \text{Im}(\mathcal{R}_t) = \text{Im}(W_t)$.

---

## Equivalence with Algebraic Reachability

> [!warning] Proposition: Fundamental Reachability Theorem
> For every $t > 0$, the reachable subspace coincides with the image of the standard Reachability Matrix $\mathcal{R}$:
> $$X_t^R = \text{Im}(\mathcal{R}_t) = \text{Im}(W_t) = \text{Im}(\mathcal{R})$$
> Where $\mathcal{R} = [G | FG | \dots | F^{n-1}G]$.

**Proof:**
We want to prove $\text{Im}(\mathcal{R}_t) = \text{Im}(\mathcal{R})$. Equivalently, we prove their orthogonal complements are equal: $(\text{Im}(\mathcal{R}_t))^\perp = (\text{Im}(\mathcal{R}))^\perp$.
Using the [Kernel-Image property](DT%20&%20CT.md#main-properties-of-adjoint-transformations) ($\ker \mathcal{A}^* = (\text{Im} \mathcal{A})^\perp$), this is equivalent to proving:
$$\ker \mathcal{R}_t^* = \ker \mathcal{R}^\top$$

$$
\begin{aligned}
x \in \ker \mathcal{R}_t^* &\iff \mathcal{R}_t^* x = 0_{\mathcal{U}_{[0,t]}} \\
&\iff G^\top e^{F^\top(t-\tau)} x = 0 \quad \forall \tau \in [0,t] \\
&\iff G^\top \sum_{k=0}^{\infty} (F^\top)^k \frac{(t-\tau)^k}{k!} x = 0 \quad \forall \tau \in [0,t]
\end{aligned}
$$
By the Principle of Identity of Power Series, the coefficients must be zero:
$$\iff G^\top (F^\top)^k x = 0 \quad \forall k \in \mathbb{Z}_+$$
By Cayley-Hamilton, we only need to check up to $n-1$:
$$\iff G^\top (F^\top)^k x = 0 \quad k=0, 1, \dots, n-1$$
$$\iff \begin{bmatrix} G^\top \\ G^\top F \\ \vdots \\ G^\top F^{n-1} \end{bmatrix} x = 0 \iff \mathcal{R}^\top x = 0 \iff x \in \ker \mathcal{R}^\top \quad \blacksquare$$

### Consequences

> [!success] CT Reachability Condition
> The Continuous Time system is **Reachable** ($X^R = \mathbb{R}^n$) if and only if:
> $$\text{rank}(\mathcal{R}) = n$$
> *(Exactly the same condition as in [Discrete Time](DT.md#the-reachable-subspace-xr))*.

> [!danger] Controllability to Zero (CT)
> A state $x_0$ is Controllable to Zero at $t>0$ if $\exists u(\cdot)$ such that $x(t) = e^{Ft}x_0 + \mathcal{R}_t u(\cdot) = 0$.
> $$e^{Ft}x_0 = -\mathcal{R}_t u(\cdot) \iff e^{Ft}x_0 \in \text{Im}(\mathcal{R}_t)$$
>
> The set of controllable states to zero $X_t^C$ is:
> $$X_t^C = \{ x \in X : e^{Ft} x \in \text{Im}(\mathcal{R}_t) = \text{Im}(\mathcal{R}) \}$$

# Continuous Time (CT) Point-to-Point Control

## Problem Formulation

> [!example] Goal: CT State Steering
> Given a CT system $\Sigma: \dot{x} = Fx + Gu$, a time $t > 0$, and states $x_0, x_f$.
> Determine an input $u(\cdot) \in \mathcal{U}_{[0,t]}$ that steers the state from $x(0)=x_0$ to $x(t)=x_f$.

The state evolution is given by:
$$x(t) = e^{Ft}x_0 + \mathcal{R}_t u(\cdot)$$
The problem is solvable iff:
$$x_f - e^{Ft}x_0 \in \text{Im}(\mathcal{R}_t) = \text{Im}(\mathcal{R})$$

We solve the integral equation by exploiting the Reachability Gramian $W_t$.
We solve the auxiliary equation for $v_t$:
$$x_f - e^{Ft}x_0 = \mathcal{R}_t \mathcal{R}_t^* v_t = W_t v_t$$

If $v_t$ solves the equation above, then the input:
$$u^*(\cdot) = \mathcal{R}_t^* v_t$$
is the solution to the control problem.

> [!success] Formula: Optimal Input
> $$u^*(\tau) = G^\top e^{F^\top(t-\tau)} v_t \quad \tau \in [0, t]$$
> This solution $u^*(\cdot)$ is **unique** and has the **Minimum Norm** ($\int \|u\|^2$) among all valid inputs.

**Proof of Minimality:**
$$ \|u(\cdot)\|^2 = \|u^*(\cdot) + \tilde{u}(\cdot)\|^2 = \|u^*(\cdot)\|^2 + \|\tilde{u}(\cdot)\|^2$$
Where $\tilde{u} \in \ker \mathcal{R}_t$ and $u^* \in \text{Im} \mathcal{R}_t^* = (\ker \mathcal{R}_t)^\perp$.

## Solved Examples: Decomposition

> [!example] Exercise: Kalman Decomposition
> **Given System (CT):**
> $$F = \begin{bmatrix} 0 & 1 & 1 \\ 2 & 1 & 0 \\ 1 & 1 & 2 \end{bmatrix}, \quad g = \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix}$$
> **Goal:** Prove the system is not reachable and derive the Standard Reachability Form.

**Solution:**

**1. Reachability Analysis**
Calculate the Reachability Matrix $\mathcal{R} = [g \mid Fg \mid F^2g]$.
* $g = \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix}$
* $Fg = \begin{bmatrix} 0 & 1 & 1 \\ 2 & 1 & 0 \\ 1 & 1 & 2 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix} = g$
Since $Fg = g$, $g$ is an eigenvector (associated with eigenvalue 1).
$\mathcal{R} = [g \mid g \mid g]$.
**Rank is 1** ($\rho = 1$). Since $1 < 3$, the system is **Not Reachable**.

**2. Basis Construction**
* Reachable Basis: $v_1 = g = \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix}$.
* Completion: Need 2 more independent vectors.
  Choose $w_2 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$, $w_3 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}$.
  $$T = \begin{bmatrix} 0 & 1 & 0 \\ 1 & 0 & 1 \\ -1 & 0 & 0 \end{bmatrix}$$

**3. Transformation**
Calculate $T^{-1}$.
$$T^{-1} = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix}$$

Calculate $\bar{F} = T^{-1}FT$:
$$
\bar{F} = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 & 1 & 1 \\ 2 & 1 & 0 \\ 1 & 1 & 2 \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 1 & 0 & 1 \\ -1 & 0 & 0 \end{bmatrix} = \begin{bmatrix} 1 & -1 & -1 \\ 0 & 0 & 1 \\ 0 & 3 & 2 \end{bmatrix}
$$
Identify blocks:
* $F_{11} = [1]$ (Reachable part, eigenvalue 1 matches our finding).
* $F_{22} = \begin{bmatrix} 0 & 1 \\ 3 & 2 \end{bmatrix}$ (Unreachable part).

Calculate $\bar{g} = T^{-1}g$:
$$
\bar{g} = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}
$$
Matches the form $\begin{bmatrix} G_1 \\ 0 \end{bmatrix}$.


# Systems Theory Summary (Cheat Sheet)

## 1. State Space Models (SSM)
### Discrete Time (DT)
> [!success] State Space Equations
> $$
> \begin{cases}
> x(t+1) = Fx(t) + Gu(t) & \leftarrow \text{State Equation (First order diff. equa.)} \\
> y(t) = Hx(t) + Du(t) & \leftarrow \text{Output Equation (Static Equation)}
> \end{cases}
> $$

*   **Solution**: $x(k) = F^{k-k_0}x(k_0) + \sum_{j=k_0}^{k-1} F^{k-1-j}G u(j)$
*   **Impulse Response**: $w(k) = \begin{cases} D & k=0 \\ H F^{k-1} G & k > 0 \end{cases}$
*   **Transfer Function**: $W(z) = H(zI - F)^{-1}G + D$

> [!success] Characteristic Polynomial
> The characteristic polynomial of $F$ is:
> $$\Delta_F(z) \triangleq \det(zI_n - F) = z^n + a_{n-1}z^{n-1} + \dots + a_1 z + a_0 \in \mathbb{R}[z]$$
>
> * **Monic:** Since the coeff. of $z^n = 1$.
> * $\deg \Delta_F(z) = n$.
> * Set of polynomials in the unknown $z$ with real coeff.

> [!success] Impulse Response
> If $n=1, x(0)=0$ and $u(t)=\delta(t)$:
> $$
> y(t) = \begin{cases}
> D & t=0 \\
> H F^{t-1} G & t \in \mathbb{Z}, t \ge 1
> \end{cases}
> $$

### Powers of a Square Matrix and Jordan Form

> [!danger] Definition
> A matrix $J \in \mathbb{C}^{n \times n}$ is said to be in **Jordan Form** if, possibly after row-column-permutations, it can be written as follows:
>
> $$J = \begin{bmatrix} J_1 & & \huge\mathbb{O} \\ & J_2 & \\ \huge\mathbb{O} & & J_r \end{bmatrix}$$
>
> Where $J_i \in \mathbb{C}^{n_i \times n_i}$ is a **Jordan Block** associated with $\lambda_i \in \mathbb{C}$ ($\lambda_i \neq \lambda_j$ if $i \neq j$).
> Note: $u$ is Algebraic Multiplicity of $\lambda_i$.
>
> $$n_1 + n_2 + \dots + n_r = n$$

> [!warning] Theorem
> We know: $\dim[\ker(\lambda_i I_n - J)] = n - \text{rank}(\lambda_i I_n - J)$

### Generic Power of a Matrix in Jordan Form
Since $J$ is Block Diagonal:
$$J^t = \begin{bmatrix} J_1^t & & \\ & J_2^t & \\ & & J_r^t \end{bmatrix}$$

In turn, each $J_i$ is Block Diagonal.
$$J_r^t = \begin{bmatrix} J_{i1}^t & & \\ & J_{i2}^t & \\ & & J_{is_i}^t \end{bmatrix}$$
I can represent $J_\lambda^t$ in compact form using discrete impulses:
$$J_\lambda^t = \begin{bmatrix} \delta(t) & \delta(t-1) & \dots & \delta(t-\nu+1) \\ & \ddots & \ddots & \vdots \\ & & \ddots & \delta(t-1) \\ & & & \delta(t) \end{bmatrix}$$
For $\lambda \neq 0$:
$$
J_\lambda^t = \begin{bmatrix}
\lambda^t & \binom{t}{1}\lambda^{t-1} & \binom{t}{2}\lambda^{t-2} & \dots & \binom{t}{\nu-1}\lambda^{t-\nu+1} \\
& \lambda^t & \binom{t}{1}\lambda^{t-1} & \dots & \\
& & \ddots & \ddots & \\
& 0 & & \binom{t}{1}\lambda^{t-1} & \\
& & & & \lambda^t
\end{bmatrix}
$$

> [!warning] Proposition
> For any $F \in \mathbb{C}^{n \times n}$ (in particular $F \in \mathbb{R}^{n \times n}$), exists $T \in \mathbb{C}^{n \times n}$ non-singular such that:
> $$T^{-1}FT = J \quad (\text{Jordan Form})$$
> $$F^t = T J^t T^{-1} \Rightarrow F^t = (T J T^{-1}) (T J T^{-1}) \dots (T J T^{-1}) = T J^t T^{-1}$$
> $$J^t = T^{-1} F^t T$$
>
> This implies that the entry $F^t$ are **Linear Combination** of the elementary modes of $J$.
>
> $\Rightarrow$ All the elementary modes associated with $J$ appear in $F^t$ and no other. We call them (also) elementary modes of $F$.
>
> **Note:** $\psi_F(s) = \psi_J(s)$ because they are **Similar**.

## Zeta Transform
It's used to study **Discrete-Time** State Space Models.

Let $v(t), t \in \mathbb{Z}_+$ be a possibly vector value or matrix value discrete time sequence. We define its **Zeta-Transform** (or Z-Transform) (if it exists) as the complex value (vector/matrix valued) function of the complex variable $z \in \mathbb{C}$ defined as:
> [!success] Z-Transform Definition
> $$V(z) = \mathcal{Z}[v(t)] \triangleq \sum_{t=0}^{+\infty} v(t) z^{-t} = v(0) + v(1)z^{-1} + v(2)z^{-2} + \dots$$

**Properties of Z-Transform we need:**

1.  **Linearity:** if $V_i(z) = \mathcal{Z}[v_i(t)]$ ($i=1,2$ and $\alpha_1, \alpha_2 \in \mathbb{C}$)
    Then $\mathcal{Z}[\alpha_1 v_1(t) + \alpha_2 v_2(t)] = \alpha_1 V_1(z) + \alpha_2 V_2(z)$
2.  **One Step Advanced:** if we have $V(z) = \mathcal{Z}[v(t)]$
    Then $\mathcal{Z}[v(t+1)] = z V(z) - z v(0)$
> [!success] Output Z-Transform
> $$Y(z) = H(zI_n - F)^{-1} z x_0 + [H(zI_n - F)^{-1}G + D] U(z)$$

### Analysis of DT SSM via Z-Transform
We define **Transfer Matrix** of the State-Space Model $\Sigma(F, G, H, D)$:

> [!danger] Definition
> $$W(z) \triangleq H(zI_n - F)^{-1} G + D$$

**Define:** $\forall i \in \{1, \dots, p\}, \forall j \in \{1, \dots, m\}$

> [!success] Element Formula
> $$[W(z)]_{ij} = W_{ij}(z) = \frac{e_i^\top H \text{adj}(zI_n - F) G e_j}{\Delta_F(z)} + d_{ij}$$
>
> * The numerator $e_i^\top H \text{adj}(zI_n - F) G e_j$ is a **Polynomial of degree $\le n-1$**.
> * The fraction term is a **Polynomial of degree $n$ (Strictly proper function)**.

We say $\lambda \in \mathbb{C}$ is a **Pole of $W(z)$** if it is a pole of some of its entries:
Therefore:
> [!success] Poles Definition
> $$\{\text{Poles of } W(z)\} \triangleq \bigcup_{\substack{i \in 1 \dots p \\ j \in 1 \dots m}} \{\text{Poles of } W_{ij}(z)\} \subseteq \{\text{Zeros of } \Delta_F(z)\} = \sigma(F)$$
>
> *$(\sigma(F)$ is the **Spectrum of F**, i.e., the set of eigenvalues).

---
### Continuous Time (CT)
> [!success] State Space Equations
> $$
> \begin{cases}
> \dot{x}(t) = F x(t) + G u(t) \\
> y(t) = H x(t) + D u(t)
> \end{cases}
> $$

*   **Solution**: $x(t) = e^{F(t-t_0)}x(t_0) + \int_{t_0}^t e^{F(t-\tau)}G u(\tau) d\tau$
*   **Impulse Response**: $w(t) = H e^{Ft} G + D \delta(t)$
*   **Transfer Function**: $W(s) = H(sI - F)^{-1}G + D$

We introduce the concept of **Exponential of a Matrix**.

> [!danger] Definition
> Given a matrix $F \in \mathbb{C}^{n \times n}$ we define the **Exponential of F** as:
> $$e^{Ft} = \exp(Ft) \triangleq \sum_{k=0}^{+\infty} F^k \frac{t^k}{k!}$$

#### Some Properties of the Exponential Matrix

1.  $$e^{Ft} \Big|_{t=0} = I_n + Ft + F^2 \frac{t^2}{2!} + F^3 \frac{t^3}{3!} + \dots \Big|_{t=0} = I_n$$

2.  $$\frac{d}{dt} [e^{Ft}] = \frac{d}{dt} \left[ I_n + Ft + F^2 \frac{t^2}{2!} + \dots \right] = F + F^2 t + F^3 \frac{t^2}{2!} + \dots = F e^{Ft} \ (= e^{Ft}F)$$

3.  $$e^{Ft} \text{ is an INVERTIBLE MATRIX } \forall t \in \mathbb{R} \text{ and } [e^{Ft}]^{-1} = e^{(-F)t} = e^{-Ft}$$

4.  If $v \neq 0$ is an **Eigenvector** of $F$ corresponding to the eigenvalue $\lambda \in \mathbb{C}$ (i.e. $Fv = \lambda v$)
    Then $\forall t \in \mathbb{R}$:
    $$\underbrace{e^{Ft}}_{\text{Matrix}} v = \underbrace{e^{\lambda t}}_{\text{Scalar}} v$$
> [!success] State and Output Evolution (CT)
> **State:**
> $$x(t) = \underbrace{e^{Ft} x_0}_{\triangleq x_{\ell}(t)} + \underbrace{\int_0^t e^{F(t-\tau)} G u(\tau) d\tau}_{\triangleq x_f(t)}$$
> * $x_{\ell}(t)$: Free/Unforced State Component
> * $x_f(t)$: Forced State Component
>
> **Output:**
> $$y(t) = \underbrace{H e^{Ft} x_0}_{\triangleq y_{\ell}(t)} + \underbrace{\left[ \int_0^t H e^{F(t-\tau)} G u(\tau) d\tau + D u(t) \right]}_{\triangleq y_f(t)}$$
> * $y_f(t)$: Forced Output Component

We define **Impulse Response** of the CT State-Space Model:

> [!success] Impulse Response Formula
> $$W(t) \triangleq D \delta(t) + H e^{Ft} G \delta_{-1}(t)$$
>
> * $\delta(t)$: Dirac Impulse
> * $\delta_{-1}(t)$: Continuous Time Step Function

### Exponential of a Matrix in Jordan Form
if we look to the definition of the exponential we deduce that:
$$e^{Jt} = \begin{bmatrix} e^{J_1 t} & & \\ & e^{J_2 t} & \\ & & \ddots \end{bmatrix}, \quad e^{J_i t} = \begin{bmatrix} e^{J_{i1} t} & & \\ & e^{J_{i2} t} & \\ & & \ddots \end{bmatrix}$$

> [!success] Exponential of a Miniblock
> $$e^{J_\lambda t} = \begin{bmatrix}
> e^{\lambda t} & t e^{\lambda t} & \frac{t^2}{2!}e^{\lambda t} & \dots & \frac{t^{\nu-1}}{(\nu-1)!}e^{\lambda t} \\
> & e^{\lambda t} & t e^{\lambda t} & \frac{t^2}{2!}e^{\lambda t} & \vdots \\
> & & e^{\lambda t} & \ddots & \\
> & & & \ddots & t e^{\lambda t} \\
> & & & & e^{\lambda t}
> \end{bmatrix}$$
>
> The terms $e^{\lambda t}, t e^{\lambda t}, \dots, \frac{t^{\nu-1}}{(\nu-1)!}e^{\lambda t}$ are the $\nu$ **Elementary Modes** associated with a Miniblock $J_\lambda$.

### Analysis of Continuous Time State-Space Models via Laplace Transform

> [!success] State Expression (Laplace)
> $$X(s) = \underbrace{(sI_n - F)^{-1}x_0}_{\equiv X_{\ell}(s) \triangleq \mathcal{L}[x_{\ell}(t)]} + \underbrace{(sI_n - F)^{-1}GU(s)}_{\equiv X_f(s) \triangleq \mathcal{L}[x_f(t)]}$$

> [!success] Output Expression (Laplace)
> $$Y(s) = \underbrace{H(sI_n - F)^{-1}x_0}_{\equiv Y_{\ell}(s) \triangleq \mathcal{L}[y_{\ell}(t)]} + \underbrace{[H(sI_n - F)^{-1}G + D]U(s)}_{\equiv Y_f(s) \triangleq \mathcal{L}[y_f(t)]}$$

We define the **Transfer Matrix** of the CT System $\Sigma = (F, G, H, D)$:

> [!danger] Definition
> $$W(s) \triangleq H(sI_n - F)^{-1}G + D \quad \in \mathbb{R}(s)^{p \times m}$$
> *(Proper Rational Matrix)*

$W(s)$ is strictly proper $\Leftrightarrow D=0$ (i.e. $\Sigma$ is strictly proper).

We have:
$$\{\text{Poles of } W(s)\} = \bigcup_{ij} \{\text{Poles of } W_{ij}(s)\} \subseteq \sigma(F) \quad \left(\substack{\text{Set of the} \\ \text{Eigenvalues} \\ \text{of } F} \right)$$
---
## Non Linear Discrete Time State-Space Models

A non linear DT time invariant state space model is described as follows:

$$
\begin{cases}
x(t+1) = f(x(t), u(t)) & \leftarrow \text{State Equation} \\
y(t) = h(x(t), u(t)) & \leftarrow \text{Output Equation}
\end{cases} \quad t \in \mathbb{Z}
$$

> [!danger] Definition
> A state $x_e \in \mathbb{R}^n$ is said to be an **Equilibrium Point** of the system corresponding to the constant input $u(t) = \bar{u}$ if:
>
> $$
> \left.
> \begin{aligned}
> x(0) &= x_e \\
> u(t) &= \bar{u} \quad \forall t \in \mathbb{Z}_+
> \end{aligned}
> \right\} \implies x(t) = x_e \quad \forall t \in \mathbb{Z}_+
> $$

> [!success] Characterization
> It is immediate to see that:
> $x_e$ is an equilibrium point corresponding to $u(t) = \bar{u} \iff f(x_e, \bar{u}) = x_e$

> [!danger] Definition
> We say that $x_e$ is an **Equilibrium Point** of the autonomous state space models if:
>
> $$x(0) = x_e \implies x(t) = x_e \quad \forall t \in \mathbb{Z}_+$$
>
> $x_e$ is an equilibrium point $\Leftrightarrow x_e = f(x_e)$ (i.e. $x_e$ is a fixed point of the map $f(\cdot)$)

> [!danger] Definition: Types of Equilibrium Point
> Let $x_e \in \mathbb{R}^n$ be an equilibrium point of system (A), then:
>
> * $x_e$ is a **Stable Equilibrium Point** if $\forall \epsilon > 0 \ \exists \delta > 0$ such that:
>     If $\|x(0) - x_e\| < \delta$ then $\|x(t) - x_e\| < \epsilon \quad \forall t \in \mathbb{Z}_+$
>     *(Note: $\| \cdot \|$ is Norm)*
>
> * $x_e$ is an **Attractive Equilibrium Point** if $\exists \bar{\delta} > 0$ such that:
>     If $\|x(0) - x_e\| < \bar{\delta}$ then $\lim_{t \to +\infty} \|x(t) - x_e\| = 0$
>
> * $x_e$ is **Asymptotically Stable Equilibrium Point** if it is **Both Stable and Attractive**.

***Case 1: $1 \in \sigma(F)$***
If it's the case then the $\text{Ker}(I_n - F)$ (which is a vector subspace) contains infinite number of elements.
In fact $\bar{x} \in \text{Ker}(I_n - F)$ then $\alpha \bar{x} \in \text{Ker}(I_n - F) \quad \forall \alpha \in \mathbb{R}$.
> [!warning] Conclusion Case 1
> If $\lambda=1 \in \sigma(F)$ all the equilibria cannot be attractive, they can be (at best) stable.

***Case 2: $1 \notin \sigma(F)$***
We know is that:
$$x(t) = x_e(t) = F^t x_0$$
$$= (T J^t T^{-1}) x_0$$

**Analysis of $J^t$:**
1.  **All the elementary modes** $\delta(t), \delta(t-1) \dots$ IF $0 \in \sigma(F)$.
2.  $\binom{t}{k} \lambda^{t-k}$ IF $\lambda \in \sigma(F)$.

> [!success] Convergence
> $$\underbrace{p_k(t)}_{\substack{\text{Polynomial} \\ \text{in } t}} \lambda^{t-k}$$
>
> * **Converges when** $|\lambda| < 1 \to 0$.
> * **Convergence uniquely influenced by $\lambda$**.

#### The Elementary Modes
$$
\binom{t}{k} \lambda^{t-k} = \underbrace{\tilde{P}_k(t)}_{\substack{\text{Polynomial in } t \\ \text{of degree } k}} \lambda^t
$$
**Behavior:**
* **Converges to 0** $\iff |\lambda| < 1$.
* **Is bounded** if $|\lambda| < 1$ OR ($|\lambda| = 1$ and $k=0$).
* **Diverges** in all of the other cases.

> [!success] Attraction Condition
> $x_e=0$ is an **Attractive Equilibrium Point** $\iff \forall \lambda \in \sigma(F) \quad |\lambda| < 1$
>
> *($F$ is Schur Stable)*
>
> $\downarrow$
> *Discrete time system is attractive/convergent*

In the linear case if $x_e=0$ is an attractive equilibrium point, then it is also stable.

> [!success] Asymptotic Stability
> $\implies \Sigma$ is **Asymptotically Stable** $\iff \forall \lambda \in \sigma(F) \quad |\lambda| < 1$
>
> *($x_e=0$ is asymptotically stable)*

> [!success] Stability
> $\Sigma$ is **Stable** ($x_e=0$ stable) $\iff \forall \lambda \in \sigma(F)$ either:
>
> * $|\lambda| < 1$
> * $|\lambda| = 1$ AND all Jordan Miniblocks associated with it have **size 1** ($n_{i1}=1$).

#### Autonomous Non Linear Discrete Time State Space Models 

$$
\begin{cases}
x(t+1) = f(x(t)) \\
y(t) = h(x(t))
\end{cases} \quad t \in \mathbb{Z}_+ \quad (A)
$$

**Dimensions:**
$\dim x = n, \quad \dim y = p$
$x_e \in X = \mathbb{R}^n$

When $x(0) = x_e \implies y(t) \equiv y_e = h(x_e) \quad \forall t \in \mathbb{Z}_+$

$$
x_e \begin{cases} \text{Stable} \\ \text{Attractive} \\ \text{Asymptotically Stable} \triangleq \substack{\text{Stable} \\ + \\ \text{Attractive}} \end{cases}
$$

> [!danger] Proposition
> Consider a NL DT Autonomous SSM
> $$x(t+1) = f(x(t)) \quad t \in \mathbb{Z}_+ \quad (A)$$
> With $\dim x = n$ and assume:
> 1. $x_e$ is an equilibrium point of (A).
> 2. $F$ is continuous with its partial derivatives.
>
> Then if we set $\delta x(t) \triangleq x(t) - x_e$, we have the linearized model:
> $$\delta x(t+1) = F \delta x(t) \quad \text{where } F \triangleq \frac{\partial f}{\partial x}\bigg|_{x=x_e}$$
>
> **Then:**
>
> a) If $F$ is **Schur Stable** (i.e., $\forall \lambda \in \sigma(F) \quad |\lambda| < 1$)
>    Then $x_e$ is an **Asymptotically Stable Eq. Point** of (A).
>
> b) If $\exists \lambda \in \sigma(F)$ with $|\lambda| > 1$ then $x_e$ is **Not a Stable Eq. Point** of (A).
>
>    *(Diagrams a, b, c showing eigenvalues relative to the unit circle)*
>
> c) If $\exists \lambda \in \sigma(F)$ with $|\lambda|=1$ and no eigenvalues with $|\lambda|>1$, then we cannot say anything about $x_e$ as an eq. point of (A).

---
## Continuous Time Non Linear Time Invariant SSM

$$
\begin{cases}
\dot{x}(t) = f(x(t), u(t)) & \leftarrow \text{State Eq.} \\
y(t) = h(x(t), u(t)) & \leftarrow \text{Output Eq.}
\end{cases} \quad t \in \mathbb{R}_+
$$

* $x(t) \in X = \mathbb{R}^n$
* $u(t) \in U = \mathbb{R}^m$
* $y(t) \in Y = \mathbb{R}^p$

**Assumption:**
$f(\cdot, \cdot)$ is sufficiently "Regular" to allow $\forall x(0) = x_0 \in X$, $\forall u(t) \ t \in \mathbb{R}_+$ the existence of a solution $x(t) \ t \in \mathbb{R}_+$ to (1).

> [!danger] Definition
> A state $x_e \in X$ is an **Eq. Point** of the system corresponding to $u(t) = \bar{u}$ if
> $$
> \left.
> \begin{aligned}
> x(0) &= x_e \\
> u(t) &= \bar{u} \quad \forall t \ge 0
> \end{aligned}
> \right\} \implies x(t) = x_e \quad \forall t \ge 0
> $$
> (Const solution $\leftrightarrow \dot{x} = 0$)
>
> $x_e$ is an Eq. Point corresponding to $u(t)=\bar{u}$ IFF $0 = f(x_e, \bar{u})$.
> When so $y(t) = y_e \triangleq h(x_e, \bar{u}) \quad \forall t \ge 0$.

### Autonomous Case:

$$
(A) \quad \begin{cases}
\dot{x}(t) = f(x(t)) \\
y(t) = h(x(t))
\end{cases} \quad t \in \mathbb{R}_+
$$

> [!danger] Definition
> A state $x_e \in X$ is **Eq. Point** if: $x(0) = x_e \implies x(t) = x_e \quad \forall t \ge 0$.

The definitions of **Stable**, **Attractive** and **Asymptotically Stable** Eq. Point for (A) are the same as in the DT case.

#### The Linear (Autonomous) Case:
Given:

$$
\dot{x}(t) = F x(t) \quad t \in \mathbb{R}_+
$$
**Easily seen that:**
1.  $x_e$ Eq. Point IFF $0 = F x_e$
2.  $x_e = 0$ is **always** Eq. Point
3.  $\exists x_e \neq 0$ as Eq. Point of the system IFF $\text{Ker}(F) \supsetneq \{0\}$
    $\iff F$ is Singular
    $\iff 0 \in \sigma(F)$ (Eigenvalue of $F$ corresponding to $\lambda=0$)
4.  $x_e = 0$ is an **Attractive Eq. Point** IFF $\forall x_0 \quad x_{\ell}(t) = e^{Ft} x_0 \xrightarrow{t \to +\infty} 0$
    *(Note blue: Same as DT $x(t)=F^t x_0$)*
    $\iff$ All Elementary Modes associated with $e^{Ft}$ ($\equiv$ to $F$) converge to $0$ as $t \to +\infty$
    $\iff \frac{t^k}{k!} e^{\lambda_i t} \xrightarrow[\substack{\text{Goes} \\ \text{to } 0 \\ \text{IFF}}]{} 0 \forall i \ \text{Re}(\lambda_i) < 0 \iff \forall \lambda \in \sigma(F), \text{Re}(\lambda) < 0$
5.  $x_e = 0$ is a **Stable Eq. Point** IFF elementary modes associated with $F$ are **Bounded**.
    $\iff \forall i \ \text{Re}(\lambda_i) \le 0$ AND if $\text{Re}(\lambda) = 0$ then there is only one elementary mode associated with $\lambda_i$.
6.  We say that system is (Asymptotically) Stable if $x_e = 0$ is (Asymptotically) Stable.



---
---
## 2. Stability & Linearization

### Definitions
*   **Stable**: $\lim_{t \to \infty} x_{free}(t) = 0$ (Asymptotic Stability).
*   **Marginally Stable**: $x_{free}(t)$ is bounded.
*   **Unstable**: $x_{free}(t)$ grows unbounded.

### Criteria (Eigenvalues of $F$)

| Type                     | Continuous Time (CT)                                                                             | Discrete Time (DT)                                                          |
| :----------------------- | :----------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| **Asymptotic Stability** | $\text{Re}(\lambda_i) < 0, \forall i$ (Hurwitz)                                                  | $\lambda_i$$< 1, \forall i$ (Schur)                                         |
| **Marginal Stability**   | $\text{Re}(\lambda_i) \le 0$ and those with $\text{Re}=0$ have Jordan blocks of size 1 (simple). | $\lambda_i$$\le 1$ and those with $\lambda=1$ have Jordan blocks of size 1. |
| **Instability**          | $\exists i : \text{Re}(\lambda_i) > 0$ OR $\text{Re}=0$ with block size $>1$.                    | $\exists i :\lambda_i> 1$ OR $\lambda$ $=1$ with block size $>1$.           |

---
### Linearization (Equilibrium Points)
Given $\dot{x} = f(x,u)$, equilibrium $(\bar{x}, \bar{u})$ satisfies $f(\bar{x}, \bar{u}) = 0$.
Linearized system matrices:
$$
F = \frac{\partial f}{\partial x}\bigg|_{(\bar{x}, \bar{u})}, \quad G = \frac{\partial f}{\partial u}\bigg|_{(\bar{x}, \bar{u})}
$$
*   **Theorem**: If linearized system is Asymptotically Stable $\implies$ Non-linear system is Locally Asymptotically Stable.
*   **Theorem**: If linearized system is Unstable $\implies$ Non-linear system is Unstable.
*   **Note**: If linearized system is Marginally Stable, no conclusion can be drawn about the non-linear system.

#### Linearization of CT NC SSM around Eq. Condition
> [!success] Linearized State Equation
> $$\frac{d}{dt}[\delta x(t)] = F \delta x(t) + G \delta u(t)$$
>
> Where:
> $$F \triangleq \frac{\partial f}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \quad \text{and} \quad G \triangleq \frac{\partial f}{\partial u}\bigg|_{\substack{x=x_e \\ u=\bar{u}}}$$

> [!success] Linearized Output Equation
> $$\delta y(t) = H \delta x(t) + D \delta u(t)$$
>
> Where:
> $$H \triangleq \frac{\partial h}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \quad \text{and} \quad D \triangleq \frac{\partial h}{\partial u}\bigg|_{\substack{x=x_e \\ u=\bar{u}}}$$

> [!warning] Proposition: [Linearization Method]
> Consider a NL CT Autonomous SSM
>
> $$\dot{x}(t) = f(x(t)) \quad t \in \mathbb{R}_+ \quad \dim x = n$$
>
> **Assume:**
> 1.  $x_e$ is an **Eq. Point** of system (A).
> 2.  $f(\cdot)$ is continuous with its derivatives.
>
> **Consider Linearized Model:**
>
> $$\frac{d}{dt}[\delta x(t)] = F \delta x(t) \quad \text{where} \quad F \triangleq \frac{\partial f}{\partial x}\bigg|_{x=x_e}$$
>
> (a) If $\forall \lambda \in \sigma(F) \quad \text{Re}(\lambda) < 0$ then $x_e$ is an **Asymptotically Stable** Eq. Point of (A).
>
> (b) If $\exists \lambda \in \sigma(F) \quad \text{Re}(\lambda) > 0$ then $x_e$ is an **Unstable** Eq. Point of (A).
>
> (c) If $\nexists \lambda \in \sigma(F)$ with $\text{Re}(\lambda) > 0$ BUT $\exists \lambda \in \sigma(F)$ with $\text{Re}(\lambda) = 0$ then **this method gives me answer**.
>
> *Diagrams:*
> * **(a):** Eigenvalues in the Left Half Plane (Stable).
> * **(b):** At least one Eigenvalue in the Right Half Plane (Unstable).
> * **(c):** Eigenvalues on the Imaginary Axis (Critical).

| Discrete Time (DT)                                                                                                                                                                                                                                                                                                                                                                                                               | Continuous Time (CT)                                                                                                                                                                                                                                                                                                                                                                                                                             |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Stability & Equilibrium**<br><br>**Equilibrium:** $x_e = f(x_e)$ (Fixed point).<br>Linear case: $x(t+1)=Fx(t) \implies (I-F)x_e = 0$.<br><br>**Stability Criteria (Linear):**<br>1. **Asymptotically Stable:** $\forall \lambda \in \sigma(F), \| \lambda \| < 1$.<br>2. **Stable:** $\forall \lambda, \| \lambda \| \le 1$ AND simple blocks for $\| \lambda \|=1$.<br>3. **Unstable:** $\exists \lambda, \| \lambda \| > 1$. | **Stability & Equilibrium**<br><br>**Equilibrium:** $f(x_e) = 0$ (Null derivative).<br>Linear case: $\dot{x}=Fx \implies Fx_e = 0$.<br><br>**Stability Criteria (Linear):**<br>1. **Asymptotically Stable:** $\forall \lambda \in \sigma(F), \text{Re}(\lambda) < 0$.<br>2. **Stable:** $\forall \lambda, \text{Re}(\lambda) \le 0$ AND simple blocks for $\text{Re}(\lambda)=0$.<br>3. **Unstable:** $\exists \lambda, \text{Re}(\lambda) > 0$. |
| **Non-Linear Linearization**<br><br>Jacobians evaluated at $(x_e, \bar{u})$.<br>Stability of $x_e$ determined by eigenvalues of $F = \frac{\partial f}{\partial x}$.<br>**Critical Case:** If eigenvalues on unit circle ($\lambda=1$), linearization is inconclusive.                                                                                                                                                           | **Non-Linear Linearization**<br><br>Jacobians evaluated at $(x_e, \bar{u})$.<br>Stability of $x_e$ determined by eigenvalues of $F = \frac{\partial f}{\partial x}$.<br>**Critical Case:** If eigenvalues on imaginary axis ($\text{Re}(\lambda)=0$), linearization is inconclusive.                                                                                                                                                             |

---
---
## 3. Matrix Analysis & Functions

### Cayley-Hamilton Theorem
Every square matrix satisfies its own characteristic equation: $\Delta_F(F) = 0$.
*   Useful for computing $F^k$ or $e^{Ft}$ as a polynomial in $F$ of degree $n-1$.

### Jordan Form
$F = T J T^{-1}$, where $J = \text{diag}(J_1, \dots, J_r)$.
*   **Functions**: $f(F) = T f(J) T^{-1}$.
*   For a Jordan block $J_i$ of size $k$:
    $$
    f(J_i) = \begin{bmatrix}
    f(\lambda) & f'(\lambda) & \frac{f''(\lambda)}{2!} & \dots & \frac{f^{(k-1)}(\lambda)}{(k-1)!} \\
    0 & f(\lambda) & f'(\lambda) & \dots & \vdots \\
    \vdots & & \ddots & \ddots & \vdots \\
    0 & \dots & \dots & 0 & f(\lambda)
    \end{bmatrix}
    $$
    *   **CT**: $f(\lambda) = e^{\lambda t}$.
    *   **DT**: $f(\lambda) = \lambda^k$.

---
---
## 4. Reachability & Controllability

### Definitions
*   **Reachability**: Ability to steer state from $0$ to any $x_f$ in finite time.
*   **Controllability**: Ability to steer any state $x_0$ to $0$ in finite time.
*   **CT**: Reachability $\iff$ Controllability.
*   **DT**: Reachability $\implies$ Controllability (converse true only if $F$ is invertible, i.e., no 0 eigenvalues).

### Tests

#### 1. Kalman Rank Condition (General)
The pair $(F,G)$ is Reachable if and only if the Reachability Matrix has full rank $n$:
$$
R = [G \mid FG \mid F^2G \mid \dots \mid F^{n-1}G]
$$
$$
\text{rank}(R) = n
$$

#### 2. PBH Test (Eigenvector Test)
$(F,G)$ is Reachable if and only if:
$$
\text{rank}[sI - F \mid G] = n, \quad \forall s \in \mathbb{C}
$$
*   **Practical Tip**: You only need to check this for $s = \lambda_i$ (eigenvalues of $F$). If rank drops at $\lambda_i$, that mode is unreachable.

#### 3. PBH for Jordan Form (Special Case)
If $F$ is in Jordan Form $J$:
*   $(J, G)$ is Reachable $\iff$ The rows of $G$ corresponding to the **last row of each Jordan block** associated with the same eigenvalue are linearly independent.
*   **Corollary**: For Single Input ($m=1$), Reachable $\iff$ One Jordan block per eigenvalue (Geometric Multiplicity = 1 for all $\lambda$).

### Gramians (Energy & Optimization)
*   **Reachability Gramian** ($W_r(t)$ for CT, $W_k$ for DT):
    $$
    W_r(t) = \int_0^t e^{F\tau} G G^T e^{F^T\tau} d\tau
    $$
*   **Reachability Condition**: $W_r(t)$ is positive definite ($>0$) for any $t>0$.
*   **Minimum Energy Control**: To go from $0$ to $x_f$ in time $t$:
    $$
    u_{opt}(\tau) = G^T e^{F^T(t-\tau)} W_r(t)^{-1} x_f
    $$
    Energy: $\|u\|^2 = x_f^T W_r(t)^{-1} x_f$.

### Standard Decomposition (Kalman)
If $\text{rank}(R) = \rho < n$, there exists a transformation $T$ such that:
$$
\bar{F} = T^{-1}FT = \begin{bmatrix} F_{11} & F_{12} \\ 0 & F_{22} \end{bmatrix}, \quad \bar{G} = T^{-1}G = \begin{bmatrix} G_1 \\ 0 \end{bmatrix}
$$
*   Subsystem $(F_{11}, G_1)$ is **Reachable** (dimension $\rho$).
*   Eigenvalues of $F_{11}$ are the **Reachable Modes** (can be moved).
*   Eigenvalues of $F_{22}$ are the **Unreachable Modes** (cannot be moved).
*   **Stability**: System is stabilizable if all Unreachable Modes ($F_{22}$) are stable.

| Discrete Time (DT)                                                                                                                                                                                                                        | Continuous Time (CT)                                                                                                                                                                                                                                                                                                                             |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reachability**<br><br>**Definition:** Reachable if $\exists u$ driving $x(0)=0$ to $x(k)=x_f$.<br><br>**Condition:**<br>$\text{rank } R_k = n$ (for $k \ge n$).<br>$R_k = [G                                                            | $[FG \| \dots \|F^{k-1}G]$<br><br>**Gramian:**<br>$W_k = R_k R_k^T$.<br>**Reachability**<br><br>**Definition:** Reachable if $\exists u$ driving $x(0)=0$ to $x(t)=x_f$.<br><br>**Condition:**<br>$\text{rank } R = n$.<br>$R = [G\|FG\| \dots \| F^{n-1}G]$.<br><br>**Gramian:**<br>$W_t = \int_0^t e^{F(t-\tau)} G G^T e^{F^T(t-\tau)} d\tau$. |
| **Point-to-Point Control**<br><br>**Problem:** $x_0 \to x_f$ in time $k$.<br>**Solvability:** $x_f - F^k x_0 \in \text{Im } R_k$.<br>**Min Norm Solution:**<br>$\mathcal{U}_k^* = R_k^T (R_k R_k^T)^{-1} (x_f - F^k x_0)$ (if reachable). | **Point-to-Point Control**<br><br>**Problem:** $x_0 \to x_f$ in time $t$.<br>**Solvability:** $x_f - e^{Ft} x_0 \in \text{Im } R$.<br>**Min Norm Solution:**<br>$\mu^*(\cdot) = \mathcal{R}_t^* W_t^{-1} (x_f - e^{Ft} x_0)$ (if reachable).                                                                                                     |
| **Controllability to Zero**<br><br>**Set:** $X_k^C = \{ x : F^k x \in \text{Im } R_k \}$.<br>If $F$ is singular, $X_k^C$ can be larger than $X^R$.                                                                                        | **Controllability to Zero**<br><br>**Set:** $X_t^C = e^{-Ft} X^R = X^R$.<br>In CT, the set of states controllable to zero coincides with the reachable subspace.                                                                                                                                                                                 |

---
---
## 5. State Feedback & Eigenvalue Assignment

### Control Law
$$
u(t) = K x(t) + v(t)
$$
Closed loop system: $\dot{x} = (F+GK)x + Gv$.

### Theorem
We can assign arbitrary eigenvalues to $F+GK$ (via choice of $K$) **IF AND ONLY IF** $(F,G)$ is Reachable.

### PBH Test for Stabilizability
$(F,G)$ is Stabilizable if and only if:
$$
\text{rank}[\lambda I - F \mid G] = n, \quad \forall \lambda \text{ such that } \text{Re}(\lambda) \ge 0 \ (\text{or } |\lambda| \ge 1 \text{ for DT})
$$
(i.e., Unreachable modes must be stable).

### Formula for Single Input (Ackermann-like / Companion Form)
1.  Check Reachability.
2.  Calculate $\Delta_F(s) = s^n + a_{n-1}s^{n-1} + \dots + a_0$.
3.  Define desired polynomial $p(s) = s^n + p_{n-1}s^{n-1} + \dots + p_0$.
4.  If in **Controllable Canonical Form** ($F_c, g_c$):
    $$
    K_c = [a_0 - p_0, \ a_1 - p_1, \ \dots, \ a_{n-1} - p_{n-1}]
    $$
    (Note: Signs might vary based on definition of $F_c$, check if bottom row is $-a_i$).
5.  Transform back: $K = K_c T^{-1}$.

|                           | Discrete Time (DT)                                | Continuous Time (CT)                        |
| :------------------------ | :------------------------------------------------ | ------------------------------------------- |
| **Control Law**           | $u(k) = Kx(k) + v(k)$                             | $u(t) = Kx(t) + v(t)$                       |
| **Closed Loop Dynamics**  | $x(k+1) = (F+GK)x(k) + Gv(k)$                     | $\dot{x}(t) = (F+GK)x(t) + Gv(t)$           |
| **Reachability Property** | Feedback $u=Kx+v$ preserves Reachability          | Feedback $u=Kx+v$ preserves Reachability    |
| **Eigenvalue Allocation** | Possible iff $(F,G)$ is Reachable                 | Possible iff $(F,G)$ is Reachable           |
| **Target Polynomial**     | $p(z) = z^n + p_{n-1}z^{n-1} + \dots + p_0$       | $p(s) = s^n + p_{n-1}s^{n-1} + \dots + p_0$ |
| **Stability Goal**        | Roots of $p(z)$ inside unit circle ($\lambda< 1$) | Roots of $p(s)$ in LHP ($Re(\lambda) < 0$)  |
| **Canonical Form**        | $F_c, G_c$ structure identical to CT              | $F_c, G_c$ structure identical to DT        |

---
---
## 6. Exercise Cheat Sheet

### How to check Reachability?
1.  Compute $R = [G \mid FG \mid \dots]$. Check Rank.
2.  If $F$ is diagonal/Jordan: Check rows of $G$ corresponding to last rows of blocks.
3.  If parameter $k$ is involved: Use PBH test on eigenvalues.

### How to find Minimum Energy Input?
1.  Compute Gramian $W_r(t)$.
2.  Invert $W_r(t)$.
3.  Apply formula $u(\tau) = B^T e^{A^T(t-\tau)} W^{-1} x_f$.

### How to Stabilize / Assign Eigenvalues?
1.  Check if Reachable.
2.  If **Reachable**: All $\lambda$ can be moved.
    *   Write $\det(sI - (F+GK)) = \text{desired poly}$.
    *   Solve system of equations for entries of $K$.
3.  If **Not Reachable**:
    *   Find Unreachable eigenvalues (PBH rank drop).
    *   If Unreachable $\lambda$ are stable $\to$ Stabilizable.
    *   If Unreachable $\lambda$ are unstable $\to$ Not Stabilizable.

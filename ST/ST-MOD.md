> [!danger] (This a modified version on ST)
## Classic Control Theory

**Process:**
* **Input:** $u(t)$ (Action on the system)
* **Output:** $y(t)$ (Reaction of the system, trace of the variables and the measured variable)
* **Model:** I/O Model

To improve its proprieties and achieve some targets: **Dynamic Output Feedback**.

> [!info] Scheme
> Reference $r(t)$ $\to$ Sum $\to$ Error $e(t)$ $\to$ **Controller** $\to$ $u(t)$ $\to$ **Process** $\to$ $y(t)$ Output
>
> *Feedback loop returns $y(t)$ to the Sum.*

> [!success] Error Definition
> $$e(t) = r(t) - y(t)$$

> [!warning] Constraint
> Only for Single In Single Out (**SISO**) Systems.

## Systems Theory

**Process:**
* **Input:** $u(t)$
* **Block:** State Space Model
* **Output:** $y(t)$
* **Internal:** $x(t)$ (Internal variable / Target variable)

> [!info] Note
> Multiple Input Multiple Output (**MIMO**) Models.

### Static State Feedback

To improve system prop. and achieve some goal: **Static State Feedback**.

> [!info] Context
> We will consider this scheme instead of the previous (Dynamic Output Feedback).

**Diagram Logic:**
Input $v(t)$ (Independent Input) + Feedback $\to$ Process $\to$ $y(t)$
$\uparrow$
$K$ (Constant Block/Matrix) $\leftarrow x(t)$ (State)

> [!success] Control Law
> $$u(t) = K x(t) + v(t)$$

## Examples

| Example 1: Quarter Car Model                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example 2: Inverted Pendulum on a Cart                                                                                                                                                                                                                                                                                                                                                                                          |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **AKA Mass-Spring-Mass-Damper Model**<br><br>**Poor Model:**<br>Simple block $\Pi$ with Force $u(t)$ and output $y(t)$.<br><br>**An Improved Quarter Car Model:**<br>Diagram showing chassis and wheel suspension.<br>- **Car Control:** $u(t)$<br>- **Body of the car:** $M$, state $x_2(t) = y(t)$<br>- **Wheel:** $m$, state $x_1(t)$<br>- **Components:** Springs ($k, k_2$), Damper ($b$)<br>- **Disturbance:** $w(t)$ (Level of the road, high frequency noise)<br><br>**Conclusion:**<br>I need to use state space models for modeling and control. | **Diagram:**<br>Cart of mass $M$ with a rod of length $2L$.<br>- **Force:** $u(t)$<br>- **Position of cart:** $x_1(t)$<br>- **Angle:** $\theta(t) \approx x_2(t)$<br><br>**Target:**<br>Design the control law $u(t)$ to keep $\theta(t)$ around 0.<br><br>**Solution:**<br>It can be solved properly only using **State Space Models** targeting both $x_1(t)$ (Position of the cart) and $x_2(t)$ (Position of the pendulum). |

## Review

### State-Space Models

**(Continuous-Time concept base)**

### Discrete-Time State-Space Models

A Discrete Time State Space Model is described by the following difference equation:

> [!success] State Space Equations
> $$
> \begin{cases}
> x(t+1) = Fx(t) + Gu(t) & \leftarrow \text{State Equation (First order diff. equa.)} \\
> y(t) = Hx(t) + Du(t) & \leftarrow \text{Output Equation (Static Equation)}
> \end{cases}
> $$

**Variables Definition:**
* $x(t) \in \mathbb{R}^n \triangleq X$ (State Variable / State Space)
* $u(t) \in \mathbb{R}^m \triangleq U$ (Input / Input Target)
* $y(t) \in \mathbb{R}^p \triangleq Y$ (Output / Output Target)

The system is represented in compact form as:
$$\Sigma = (F, G, H, D)$$

We call **dimension of $\Sigma$** the dimension of the state variable $n$ ($\dim \Sigma = n$).

> [!info] System Properties
> System $\Sigma$ is **Linear**, **Time-Invariant** ($\to$ we will consider its dynamics from $t=0$ onward and $t \in \mathbb{Z}$) and **Proper**.

In case $D=0$ ($D$ is the feedforward matrix), $\Sigma$ is called **Strictly Proper** and for simplicity we will use $\Sigma = (F, G, H)$.

### Block Diagram of the Discrete Time (DT) State Space Model

**Matrices Definitions:**
* $F \in \mathbb{R}^{n \times n}$: State Matrix
* $G \in \mathbb{R}^{n \times m}$: Input Matrix
* $H \in \mathbb{R}^{p \times n}$: Output Matrix
* $D \in \mathbb{R}^{p \times m}$: Feedforward Matrix (or Input to Output Matrix)

> [!success] Characteristic Polynomial
> The characteristic polynomial of $F$ is:
> $$\Delta_F(z) \triangleq \det(zI_n - F) = z^n + a_{n-1}z^{n-1} + \dots + a_1 z + a_0 \in \mathbb{R}[z]$$
>
> * **Monic:** Since the coeff. of $z^n = 1$.
> * $\deg \Delta_F(z) = n$.
> * Set of polynomials in the unknown $z$ with real coeff.

The zeros of $\Delta_F(z)$ are the **Eigenvalues** of the matrix $F$.
If we decide by $\lambda_1, \lambda_2 \dots \lambda_r \in \mathbb{C}$ the eigenvalues of $F$, then:
$$\Delta_F(z) = (z - \lambda_1)^{n_1} (z - \lambda_2)^{n_2} \dots (z - \lambda_r)^{n_r}$$
Where $n_1, \dots, n_r$ are positive integers called the **Algebraic Multiplicities** of $\lambda_1, \dots, \lambda_r$.

## Expression of the State and Output at a generic $t \in \mathbb{Z}, t \ge t_0$

> [!success] Formulas
> **State Evolution:**
> $$x(t) = \underbrace{F^{t-t_0}x(t_0)}_{\text{Unforced/Free State Evolution } x_{\ell}(t)} + \underbrace{\sum_{k=t_0}^{t-1} F^{t-1-k} G u(k)}_{\text{Forced State Evolution } x_F(t)}$$
>
> **Output Evolution:**
> $$y(t) = \underbrace{H F^{t-t_0} x(t_0)}_{\text{Unforced/Free Output Evolution } y_{\ell}(t)} + \underbrace{\sum_{k=t_0}^{t-1} H F^{t-1-k} G u(k) + D u(t)}_{\text{Forced Output Evolution on } Y_F(t)}$$

### Impulse Response

**Unitary Discrete Time Impulse:**
$$\delta(t) \triangleq \begin{cases} 1 & t=0 \\ 0 & t \in \mathbb{Z}, t \neq 0 \end{cases}$$

**Case $m=1$:** $x(0)=0, \quad u(t)=\delta(t)$

* $t=0$:
    $$y(0) = H \cancel{x(0)} + D \underbrace{u(0)}_{1} = D$$
* $t=1$:
    $$x(1) = F \cancel{x(0)} + G \underbrace{u(0)}_{1} = G$$
    $$y(1) = H x(1) + D \cancel{u(1)} = HG$$
* $t=2$:
    $$x(2) = F x(1) + \cancel{G u(1)} = FG$$
    $$y(2) = H x(2) + D \cancel{u(2)} = HFG$$

> [!success] Summarize
> If $n=1, x(0)=0$ and $u(t)=\delta(t)$:
> $$
> y(t) = \begin{cases}
> D & t=0 \\
> H F^{t-1} G & t \in \mathbb{Z}, t \ge 1
> \end{cases}
> $$

We define **Impulse Response** $W(t)$:
$$W(t) \triangleq D \delta(t) + H F^{t-1} G \delta_{-1}(t-1)$$
Where $\delta_{-1}(t)$ is the unit step:
$$\delta_{-1}(t) \triangleq \begin{cases} 0 & t \in \mathbb{Z}, t < 0 \\ 1 & t \in \mathbb{Z}_+ \end{cases}$$

**Case $m > 1$:**

We assume $x(0)=0, \quad u(t) = e_i \delta(t)$
Where $e_i$ is the canonical vector (1 in $i$-th element).

Then we find:
$$
y(t) = \begin{cases}
De_i = \text{col}_i(D) \\
(H F^{t-1} G) e_i = \text{col}_i(H F^{t-1} G) & t \in \mathbb{Z}, t \ge 1
\end{cases}
$$

$$\Rightarrow W(t) \triangleq D \delta(t) + H F^{t-1} G \delta_{-1}(t-1)$$

By recalling the concept of convolution of two discrete time sequences $V_1, V_2$:
$$t \in \mathbb{Z}_+ : [V_1 * V_2](t) \triangleq \sum_{k=0}^{t} V_1(t-k) V_2(k)$$

Then we see that:
$$y_F(t) = [W * U](t) = \sum_{k=0}^{t} W(t-k) U(k)$$
$$= \sum_{k=0}^{t-1} W(t-k) U(k) + W(0) U(t)$$

---

## Powers of a Square Matrix and Jordan Form

> [!danger] Definition
> A matrix $J \in \mathbb{C}^{n \times n}$ is said to be in **Jordan Form** if, possibly after row-column-permutations, it can be written as follows:
>
> $$J = \begin{bmatrix} J_1 & & \huge\mathbb{O} \\ & J_2 & \\ \huge\mathbb{O} & & J_r \end{bmatrix}$$
>
> Where $J_i \in \mathbb{C}^{n_i \times n_i}$ is a **Jordan Block** associated with $\lambda_i \in \mathbb{C}$ ($\lambda_i \neq \lambda_j$ if $i \neq j$).
> Note: $u$ is Algebraic Multiplicity of $\lambda_i$.
>
> $$n_1 + n_2 + \dots + n_r = n$$

**Jordan Miniblock:**
With
$$J_i = \begin{bmatrix} J_{i1} & & \huge\mathbb{O} \\ & J_{i2} & \\ \huge\mathbb{O} & & J_{is_i} \end{bmatrix}$$
$J_{ik} \in \mathbb{C}^{u_k \times u_k}$ is the $k$-th **Jordan Miniblock** associated with $\lambda_i$.

Structure of a miniblock $J_{ik}$:
$$J_{ik} = \begin{bmatrix} \lambda_i & 1 & & \huge\mathbb{O} \\ & \lambda_i & \ddots & \\ & & \ddots & 1 \\ \huge\mathbb{O} & & & \lambda_i \end{bmatrix}$$
(Upper diagonal has 1s, Main diagonal has $\lambda_i$).

*Blocks... they are the multiplicity.*
$$n_1 \ge n_{i2} \dots \ge n_{is_i}$$

> [!example] Example 1
> $$J = \begin{bmatrix} \begin{array}{cc|c} 2 & 1 & 0 \\ 0 & 2 & 0 \\ \hline 0 & 0 & 2 \end{array} & \huge\mathbb{O} \\ \huge\mathbb{O} & \begin{array}{|cc} 3 & 1 \\ 0 & 3 \end{array} \end{bmatrix}$$
> Matrix $J_1$ (top left) and Matrix $J_2$ (bottom right).
>
> $\rightarrow \Delta_J(z) = (z-2)^3 (z-3)^2$
> $\Rightarrow \lambda_1 = 2, \lambda_2 = 3$ are the **Eigenvalues of J**.
>
> **Conclusion:** $\lambda_1, \lambda_2$ appearing in the Jordan form are the eigenvalues of $J$ and $n_1, \dots, n_r$ are the corresponding **Algebraic Multiplicities**.

We associate with each eigenvalue $\lambda$ of $J$ a **Geometric Multiplicity**:
$$\dim U_{\lambda_i} = \dim[\ker(\lambda_i I_n - J)] = \dim[\ker(J - \lambda_i I_n)]$$
(Eigenspace associated with $\lambda_i$).

> [!warning] Theorem
> We know: $\dim[\ker(\lambda_i I_n - J)] = n - \text{rank}(\lambda_i I_n - J)$

### Example 1 Continue:

What are the geometric multiplicity of $\lambda_1, \lambda_2$?

**For $\lambda_1 = 2$:**
$$J - 2I = \begin{bmatrix} \begin{array}{cc|c} 0 & 1 & 0 \\ 0 & 0 & 0 \\ \hline 0 & 0 & 0 \end{array} & 0 \\ 0 & \begin{array}{|cc} 1 & 1 \\ 0 & 1 \end{array} \end{bmatrix}$$
(Subtract 2 from diag.)
$n = 5$.
$\text{rank}(J-2I) = 3$ (3 linearly independent non-zero rows).
$$\dim[\ker(J-2I)] = 5 - 3 = 2$$

**For $\lambda_2 = 3$:**
$$J - 3I = \begin{bmatrix} -1 & 1 & & & \\ 0 & -1 & & & \\ & & -1 & & \\ & & & 0 & 1 \\ & & & 0 & 0 \end{bmatrix}$$
$$\dim[\ker(J-3I)] = 3$$

> [!info] Result
> The geometric multiplicity of the eigenvalue $\lambda_i$ coincides with the **# of Jordan Miniblocks** associated with $\lambda_i$.

## Example 2

$$
J = \begin{bmatrix}
\begin{array}{cc|c}
1 & 1 & \\
& 1 & \\
\hline
& & 1
\end{array} & \dots \\
\vdots & \ddots
\end{bmatrix}
$$

**Eigenvalues:**

| Eigenvalues | Algebraic Mult. ($n_i$) | Geometric Mult. ($s_i$) |
| :--- | :--- | :--- |
| $\lambda_1 = 1$ | $n_1 = 3$ | $s_1 = 2$ (# of miniblocks) |
| $\lambda_2 = 2$ | $n_2 = 5$ | $s_2 = 2$ |
| $\lambda_3 = 0$ | $n_3 = 1$ | $s_3 = 1$ |

> [!danger] Definition
> Given a matrix $F \in \mathbb{R}^{n \times n}$, a polynomial $p(s) \in \mathbb{R}[s]$, $p(s) = p_d s^d + p_{d-1}s^{d-1} + \dots + p_1 s^1 + p_0$ is said to be an **Annihilating Polynomial** of $F$ if:
> $$p(s) = p_d F^d + \dots + p_1 F + p_0 I = \mathbb{O}_{n \times n}$$

> [!info] Properties of Annihilating Polynomials
> If we consider the $P_F$ of all the Annihilating Polynomial of $F$ we can prove that there exists a (Monic) polynomial of minimal degree in $P_F$, $\psi_F(s)$, such that a polynomial $p(s) \in P_F \iff p(s)$ is a multiple of $\psi_F(s)$ i.e. $\exists q(s) \in \mathbb{R}(s)$ such that $p(s) = \psi_F(s)q(s)$.

> [!danger] Definition
> $\psi_F(s)$ is called the **Minimal (Annihilating) Polynomial** of the matrix $F$.

It is possible to prove that if $J$ is in Jordan Form:

> [!success] Minimal Polynomial Formula
> $$\psi_J(s) = (s - \lambda_1)^{n_{11}} (s - \lambda_2)^{n_{21}} \dots (s - \lambda_r)^{n_{r1}}$$
>
> *Note: The exponents $n_{i1}$ correspond to the dimension of the largest miniblock associated with $\lambda_i$.*

### Example 3

$$
J = \begin{bmatrix}
\begin{array}{cc} 2 & 1 \\ & 2 \end{array} & \\
& \ddots
\end{bmatrix}
$$

**Data:**

* $\lambda_1 = 2 \quad n_1 = 4 \quad s_1 = 2$
* $\lambda_2 = 1 \quad n_2 = 4 \quad s_2 = 3$
* $\lambda_3 = 0 \quad n_3 = 3 \quad s_3 = 2$

> [!success] Result
> $$\psi_J(s) = (s-2)^3 (s-1)^2 (s-0)^2$$

### Example 4

$$
J = \begin{bmatrix}
\begin{array}{cc|c}
2 & 1 & \\
& 2 & \\
\hline
& & 2
\end{array} & \dots \\
\vdots & \ddots
\end{bmatrix}
$$

**Data:**
* $\lambda_1 = 2 \quad n_1 = 3 \quad s_1 = 2$ (*2 ones in the diagonal*)
* $\lambda_2 = 3 \quad n_2 = 2 \quad s_2 = 2$
* $\lambda_3 = 1 \quad n_3 = 4 \quad s_3 = 2 \cdot ?$

> [!info] Additional Info
> $$\psi_J(s) = (s-2)^2 (s-3) (s-1)^2$$
>
> This brings to the $2^{nd}$ option.

**Reasoning on $\lambda_3=1$ ($n_3=4, s_3=2$):**
2 Possibilities for blocks structure:
1.  **Block sizes 3 and 1:** (Requires power 3 in minimal poly) -> Rejected.
2.  **Block sizes 2 and 2:** (Requires power 2 in minimal poly) -> **Accepted**.

Structure:
$$
\begin{bmatrix}
1 & 1 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

## Generic Power of a Matrix in Jordan Form

Since $J$ is Block Diagonal:
$$J^t = \begin{bmatrix} J_1^t & & \\ & J_2^t & \\ & & J_r^t \end{bmatrix}$$

In turn, each $J_i$ is Block Diagonal.
$$J_r^t = \begin{bmatrix} J_{i1}^t & & \\ & J_{i2}^t & \\ & & J_{is_i}^t \end{bmatrix}$$

$\Rightarrow$ I can easily deduce $J^t$ if I know the expression of $J_{ik}^t$ to the generic Jordan Miniblock $J_{ik}$.

### Power of a Jordan Miniblock

Assume to have a Jordan Miniblock of size $\nu$ corresponding to some $\lambda \in \mathbb{C}$:
$$J_\lambda = \begin{bmatrix} \lambda & 1 & & \\ & \lambda & \ddots & \\ & & \ddots & 1 \\ & & & \lambda \end{bmatrix}$$

**Consider $\lambda=0$ (Nilpotent):**
$$J_0 = \begin{bmatrix} 0 & 1 & & \\ & \ddots & \ddots & \\ & & \ddots & 1 \\ & & & 0 \end{bmatrix}$$

* $J_0^0 = I_\nu = \begin{bmatrix} 1 & & \\ & \ddots & \\ & & 1 \end{bmatrix}$
* $J_0^1 = J_0$
* $J_0^2 = \begin{bmatrix} 0 & 0 & 1 & \dots & 0 \\ 0 & 0 & 0 & 1 & \dots \\ \vdots & & & & \vdots \\ 0 & & & & 0 \end{bmatrix}$ (The 1 diagonal is shifted by 1 to the right)
* $J_0^3 = \begin{bmatrix} 0 & 0 & 0 & 1 \\ & \ddots & & \vdots \\ & & & 1 \\ & & & 0 \end{bmatrix}$
* $\dots$
* $J_0^t = 0 \quad \forall t \ge \nu$

I can represent $J_\lambda^t$ in compact form using discrete impulses:
$$J_\lambda^t = \begin{bmatrix} \delta(t) & \delta(t-1) & \dots & \delta(t-\nu+1) \\ & \ddots & \ddots & \vdots \\ & & \ddots & \delta(t-1) \\ & & & \delta(t) \end{bmatrix}$$

$\delta(t), \delta(t-\nu+1)$ are the **Elementary Modes** associated with Miniblock $J_\lambda$.

**Case $\lambda \neq 0$:**
$$J_\lambda = \lambda I_\nu + J_0$$
(Behaves like a scalar).

Using Newton Binomial:
$$J_\lambda^t = (\lambda I + J_0)^t = \sum_{i=0}^t \binom{t}{i} (\lambda I)^{t-i} J_0^i$$
We can retrieve it (referring to $J_0^i$).

> [!info] Recall
> We recall Newton's Binomial Formula for scalar:
> $$(a+b)^t = \sum_{i=0}^t \binom{t}{i} a^{t-i} b^i$$
>
> We can use only in this case to calculate $J_\lambda^t$ because if I consider: $(\lambda I_\nu)(J_0) = (J_0)(\lambda I_\nu)$ (Commutativity).

$$
J_\lambda^t = \lambda^t \begin{bmatrix} 1 & \\ & 1 \end{bmatrix} + \binom{t}{1} \lambda^{t-1} \begin{bmatrix} 0 & 1 \\ & 0 \end{bmatrix} + \binom{t}{2} \lambda^{t-2} \begin{bmatrix} 0 & 0 & 1 \\ & & 0 \end{bmatrix} + \dots + \binom{t}{\nu-1} \lambda^{t-\nu+1} \begin{bmatrix} 0 & 1 \\ & 0 \end{bmatrix}
$$

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

**We define:**
$\lambda^t, \binom{t}{1}\lambda^{t-1}, \binom{t}{2}\lambda^{t-2}, \dots, \binom{t}{\nu-1}\lambda^{t-\nu+1}$
The $\nu$ **Distinct Elementary Modes** associated with $\lambda$.

> [!info] Observation
> Looking at the generic Jordan Block $J_i$, it is clear that the number of distinct elementary modes associated with it coincides with the size of the largest Jordan Miniblock associated with $\lambda_i$ (Since those associated with the others are repetition and hence it is $n_{i1}$).
> $\equiv$ Multiplicity of $\lambda_i$ in $\psi_J(s)$.

The # of distinct elementary modes associated with all the eigenvalues of $J$ is $n_{11} + n_{21} + \dots + n_{r1} = \deg \psi_J$.

### Example:

$$J = \begin{bmatrix} \begin{array}{cc} 2 & 1 \\ & 2 \end{array} & & \\ & \begin{array}{|ccc} 1 & 1 & \\ & 1 & \\ & & 1 \end{array} & \\ & & 0 \end{bmatrix}$$

Modes:
* $\lambda=2 \to 2^t, \binom{t}{1}2^{t-1}$
* $\lambda=1 \to 1, \binom{t}{1}, \binom{t}{2}$
* $\lambda=0 \to \delta(t)$

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

---

## Zeta Transform

And its use to study Discrete-Time State Space Models.

Let $v(t), t \in \mathbb{Z}_+$ be a possibly vector value or matrix value discrete time sequence. We define its **Zeta-Transform** (or Z-Transform) (if it exists) as the complex value (vector/matrix valued) function of the complex variable $z \in \mathbb{C}$ defined as:
> [!success] Z-Transform Definition
> $$V(z) = \mathcal{Z}[v(t)] \triangleq \sum_{t=0}^{+\infty} v(t) z^{-t} = v(0) + v(1)z^{-1} + v(2)z^{-2} + \dots$$

*Compare with: $\{v(t)\}_{t \in \mathbb{Z}_+} \longleftrightarrow v(0)\delta(t) + v(1)\delta(t-1) + v(2)\delta(t-2) + \dots$*

**Properties of Z-Transform we need:**

1.  **Linearity:** if $V_i(z) = \mathcal{Z}[v_i(t)]$ ($i=1,2$ and $\alpha_1, \alpha_2 \in \mathbb{C}$)
    Then $\mathcal{Z}[\alpha_1 v_1(t) + \alpha_2 v_2(t)] = \alpha_1 V_1(z) + \alpha_2 V_2(z)$
2.  **One Step Advanced:** if we have $V(z) = \mathcal{Z}[v(t)]$
    Then $\mathcal{Z}[v(t+1)] = z V(z) - z v(0)$

**Application:**
Suppose that we have Discrete Time (DT) State Space Model:
$$
\begin{cases}
x(t+1) = Fx(t) + Gu(t) \\
y(t) = Hx(t) + Du(t)
\end{cases} \quad t \in \mathbb{Z}_+
$$
And that we know the **Initial Condition** $x(0) = x_0 \in X = \mathbb{R}^n$ and the input $u(t), t \in \mathbb{Z}_+$, and $U(z) = \mathcal{Z}[u(t)]$.

We want to determine:
* $X(z) \triangleq \mathcal{Z}[x(t)]$
* $Y(z) \triangleq \mathcal{Z}[y(t)]$

Let us apply $\mathcal{Z}[\cdot]$ to both sides of the state equation and use the two properties, thus obtaining:
$$zX(z) - zx_0 = F X(z) + G U(z)$$
$$- (zI_n - F) X(z) = zx_0 + G U(z)$$
$$\Rightarrow X(z) = \underbrace{(zI_n - F)^{-1}}_{\text{Non singular } (\det(zI-F) = \Delta_F z)} z x_0 + (zI_n - F)^{-1} G U(z)$$

By applying $\mathcal{Z}$ to the output equation and using the expression of $X(z)$ just derived, we get:
> [!success] Output Z-Transform
> $$Y(z) = H(zI_n - F)^{-1} z x_0 + [H(zI_n - F)^{-1}G + D] U(z)$$

### Analysis of DT SSM via Z-Transform

> [!info] System $\Sigma$
> $$
> \begin{cases}
> x(t+1) = Fx(t) + Gu(t) & t \in \mathbb{Z}_+ \\
> y(t) = Hx(t) + Du(t)
> \end{cases}
> $$
> $\dim X = n, \dim U = m, \dim Y = p$.
>
> **Knowns:**
> $x(0) = x_0 \in X = \mathbb{R}^n$
> $u(t), t \ge 0 \longrightarrow U(z) = \mathcal{Z}[u(t)]$
>
> **Results:**
> $\rightarrow X(z) \triangleq \mathcal{Z}[x(t)], Y(z) \triangleq \mathcal{Z}[y(t)]$ satisfy:
> $$X(z) = (zI_n - F)^{-1} z x_0 + (zI_n - F)^{-1} G U(z)$$
> $$Y(z) = H(zI_n - F)^{-1} z x_0 + [H(zI_n - F)^{-1} G + D] U(z)$$

Since the system is Linear and we have seen that:
$$
\begin{aligned}
x(t) &= x_{\ell}(t) + x_f(t) \\
y(t) &= y_{\ell}(t) + y_f(t)
\end{aligned} \quad \text{By comparison}
$$

We deduce that:
$$(zI_n - F)^{-1} z x_0 = X_{\ell}(z) = \mathcal{Z}[x_{\ell}(t)]$$
$$H(zI_n - F)^{-1} z x_0 = Y_{\ell}(z) = \mathcal{Z}[y_{\ell}(t)]$$
$$[H(zI_n - F)^{-1} G + D] U(z) = Y_f(z) = \mathcal{Z}[y_f(t)]$$

We define **Transfer Matrix** of the State-Space Model $\Sigma(F, G, H, D)$:

> [!danger] Definition
> $$W(z) \triangleq H(zI_n - F)^{-1} G + D$$

We know that:
$$(zI_n - F)^{-1} = \frac{1}{\det(zI_n - F)} \text{adj}(zI_n - F) = \frac{1}{\Delta_F(z)} \text{adj}(zI_n - F)$$

* $\text{adj}(zI_n - F)$: $n \times n$ polynomial matrix whose entries have degree $\le n-1$.
* $\Delta_F(z)$: Monic polynomial of degree $n$ (Characteristic Polynomial).

**Define:** $\forall i \in \{1, \dots, p\}, \forall j \in \{1, \dots, m\}$

> [!success] Element Formula
> $$[W(z)]_{ij} = W_{ij}(z) = \frac{e_i^\top H \text{adj}(zI_n - F) G e_j}{\Delta_F(z)} + d_{ij}$$
>
> * The numerator $e_i^\top H \text{adj}(zI_n - F) G e_j$ is a **Polynomial of degree $\le n-1$**.
> * The fraction term is a **Polynomial of degree $n$ (Strictly proper function)**.

$\Rightarrow W_{ij}(z)$ is a sum of a strictly proper function in $\mathbb{R}(z)$ and a constant $(d_{ij})$.

Therefore $W_{ij}(z) \in \mathbb{R}(z)$ is a **Proper Rational Function** and it is **Strictly Proper** $\iff d_{ij} = 0$.

$W(z)$ is a **Proper Rational Matrix** belonging to $\mathbb{R}(z)^{p \times m}$.

> [!info] Note
> $$\Sigma = (F, G, H, D) \text{ is called PROPER}$$
> $$\updownarrow \text{(Strictly proper if } D=0 \text{)}$$
> $$W(z) \in \mathbb{R}(z)^{p \times m} \text{ PROPER RATIONAL}$$
> $$\text{(Strictly proper)}$$

We say $\lambda \in \mathbb{C}$ is a **Pole of $W(z)$** if it is a pole of some of its entries:
Therefore:
> [!success] Poles Definition
> $$\{\text{Poles of } W(z)\} \triangleq \bigcup_{\substack{i \in 1 \dots p \\ j \in 1 \dots m}} \{\text{Poles of } W_{ij}(z)\} \subseteq \{\text{Zeros of } \Delta_F(z)\} = \sigma(F)$$
>
> *$(\sigma(F)$ is the **Spectrum of F**, i.e., the set of eigenvalues).*

> [!info] Remark
> $$W(z) = \mathcal{Z}[W(t)]$$
> Where $W(t)$ is the **Impulse Response**.
> $\to W(t) = D\delta(t) + H F^{t-1} G \delta_{-1}(t-1)$

---

## Continuous Time (CT) State-Space Models

A continuous time state-space model is described by:
$$
\Sigma : \begin{cases}
\dot{x}(t) = Fx(t) + Gu(t) & (1) \\
y(t) = Hx(t) + Du(t) & (2)
\end{cases} \quad t \in \mathbb{R}
$$

1.  Is the **State Equation** ($H$ is a $1^{st}$ order differential equation)
2.  Is the **Output Equation** ($H$ is a static equation)

$\Sigma$ is represented for short as $\Sigma(F, G, H, D)$. It is **Linear**, **Time Invariant** and **Proper**.
($\Sigma$ is strictly proper $\leftrightarrow D=0$, when so we use $\Sigma = (F, G, H)$).

**Variables:**
* $x(t) \in X \triangleq \mathbb{R}^n$ ($X \triangleq$ State Space)
* $u(t) \in U \triangleq \mathbb{R}^m$ ($U \triangleq$ Input Alphabet)
* $y(t) \in Y \triangleq \mathbb{R}^p$ ($Y \triangleq$ Output Alphabet)

### Block Diagram of CT $\Sigma$

$$
\Sigma : \begin{cases}
\dot{x}(t) = Fx(t) + Gu(t) \\
y(t) = Hx(t) + Du(t)
\end{cases} \quad t \in \mathbb{R}, t \ge 0 \ (t \in \mathbb{R}_+)
$$

**Problem:**
If we know the Initial Cond. $x(0) = x_0 \in X$ and $u(t), t \in \mathbb{R}$, what is the expression of $x(t)$ and $y(t)$ for $t \in \mathbb{R}_+$?

To answer we need to introduce the concept of **Exponential of a Matrix**.

> [!danger] Definition
> Given a matrix $F \in \mathbb{C}^{n \times n}$ we define the **Exponential of F** as:
> $$e^{Ft} = \exp(Ft) \triangleq \sum_{k=0}^{+\infty} F^k \frac{t^k}{k!}$$

It is possible to prove that the definition is always well posed, namely the series converges $\forall t \in \mathbb{R}$ and hence $e^{Ft}$ exists $\forall t \in \mathbb{R}$.

### Some Properties of the Exp Matrix

1.  $$e^{Ft} \Big|_{t=0} = I_n + Ft + F^2 \frac{t^2}{2!} + F^3 \frac{t^3}{3!} + \dots \Big|_{t=0} = I_n$$

2.  $$\frac{d}{dt} [e^{Ft}] = \frac{d}{dt} \left[ I_n + Ft + F^2 \frac{t^2}{2!} + \dots \right] = F + F^2 t + F^3 \frac{t^2}{2!} + \dots = F e^{Ft} \ (= e^{Ft}F)$$

3.  $$e^{Ft} \text{ is an INVERTIBLE MATRIX } \forall t \in \mathbb{R} \text{ and } [e^{Ft}]^{-1} = e^{(-F)t} = e^{-Ft}$$

4.  If $v \neq 0$ is an **Eigenvector** of $F$ corresponding to the eigenvalue $\lambda \in \mathbb{C}$ (i.e. $Fv = \lambda v$)
    Then $\forall t \in \mathbb{R}$:
    $$\underbrace{e^{Ft}}_{\text{Matrix}} v = \underbrace{e^{\lambda t}}_{\text{Scalar}} v$$

By using the expression of Matrix $F$, we can answer our original question:

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

> [!info] Comparison with DT
> (In DT: $W(t) = D \delta(t) + H F^{t-1} G \delta_{-1}(t-1)$)

**Note:** $y_f(t) = [W * u](t) = \int_0^t W(\tau) u(t-\tau) d\tau = \int_0^t W(t-\tau) u(\tau) d\tau$

### Exponential of a Matrix in Jordan Form

Consider a matrix in Jordan Form:
$$J = \begin{bmatrix} J_1 & & \\ & J_2 & \\ & & J_r \end{bmatrix}$$
$J \in \mathbb{C}^{n \times n}$ is the Jordan Block corresponding to the Eigenvalue $\lambda_i$ ($\lambda_i \neq \lambda_j$ if $i \neq j$).
$n_i$: Algebraic Multiplicity.

$$J_i = \begin{bmatrix} J_{i1} & & \\ & J_{i2} & \\ & & J_{is_i} \end{bmatrix}$$
$J_{ik} \in \mathbb{C}^{u_{ik} \times u_{ik}}$ is the $k$-th Jordan Miniblock associated with $\lambda_i$.
$s_i$: Geometric Multiplicity.
$n_{i1} \ge \dots \ge n_{is_i}$: Multiplicity of $\lambda_i$ as zero of the minimal polynomial $\psi_J(z)$.

Since $J$ and $J_i$ are block diagonal matrices, $J^k$ and $J_i^k$ are block diagonal $\forall k \ge 0$.
So if we look to the definition of the exponential we deduce that:
$$e^{Jt} = \begin{bmatrix} e^{J_1 t} & & \\ & e^{J_2 t} & \\ & & \ddots \end{bmatrix}, \quad e^{J_i t} = \begin{bmatrix} e^{J_{i1} t} & & \\ & e^{J_{i2} t} & \\ & & \ddots \end{bmatrix}$$

Consequently the expression of $e^{Jt}$ is known once we know the expression of a generic Jordan Miniblock.

If $J_\lambda = \begin{bmatrix} \lambda & 1 & & \\ & \lambda & \ddots & \\ & & \ddots & 1 \\ & & & \lambda \end{bmatrix}$ ($\nu \times \nu$)

Then:
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

### Conclusion:

By using the same arguments of $J$; we can claim that to each $\lambda_i$ we associate $n_{i1}$ **Distinct Elementary Modes**.

$\rightarrow$ If we account for **all distinct eigenvalues** we have:
$$n_{11} + n_{21} + \dots + n_{r1} = \deg \psi_J(s)$$
Distinct elementary modes.

Since every matrix $F$ is similar to a matrix in Jordan Form:
i.e. $\exists T \in \mathbb{C}^{n \times n}$ non singular s.t. $T^{-1} F T = J$
Then $F = T J T^{-1}$ and $F^k = T J^k T^{-1} \ \forall k \ge 0$.

$$\Rightarrow e^{Ft} = \sum_{k=0}^{+\infty} F^k \frac{t^k}{k!} = \sum_{k=0}^{+\infty} T J^k T^{-1} \frac{t^k}{k!} = T \left[ \sum_{k=0}^{+\infty} J^k \frac{t^k}{k!} \right] T^{-1} = T e^{Jt} T^{-1}$$

> [!info] Result
> The elementary modes of $e^{Ft}$ coincides with the elementary modes of $e^{Jt}$.

### Example:

$$J = \begin{bmatrix}
\begin{array}{c|c}
\begin{array}{cc} 1 & 1 \\ 0 & 1 \end{array} & 0 \\
\hline
0 & 0
\end{array} & & \\
& \begin{array}{|ccc} 2 & 1 & 0 \\ 0 & 2 & 1 \\ 0 & 0 & 2 \end{array} & \\
& & \begin{array}{|c} \mathbf{2} \end{array}
\end{bmatrix}$$

**Eigenvalues Analysis:**
* $\lambda_1 = 0$: $n_1 = 1, s_1 = 1$.
* $\lambda_2 = 1$: $n_2 = 3, s_2 = 2$ (Miniblock sizes: 2, 1).
* $\lambda_3 = 2$: $n_3 = 4, s_3 = 2$ (Miniblock sizes: 3, 1).

**Modes Identification:**
1.  **From $\lambda_2=1$ (Size 2 block):** $e^t, t e^t$ (2 Elem. Modes).
2.  **From $\lambda_3=2$ (Size 3 block):** $e^{2t}, t e^{2t}, \frac{t^2}{2} e^{2t}$ (3 Elem. Modes). Note: The size 1 block of $\lambda=2$ does not add new distinct modes.
3.  **From $\lambda_1=0$:** $e^{0t} = 1$. (Not explicitly circled in text but present).

**Summary of Modes shown:**
$e^{t}, t e^{t}$
$e^{2t}, t e^{2t}, \frac{t^2}{2} e^{2t}$

## Analysis of Continuous Time State-Space Models via Laplace Transform

$$
\Sigma = \begin{cases}
\dot{x}(t) = Fx(t) + Gu(t) & t \in \mathbb{R}_+ \\
y(t) = Hx(t) + Du(t)
\end{cases}
$$
$\dim x = n, \quad \dim u = m, \quad \dim y = p$.

**We know:**
* $x(0) = x_0 \in X \triangleq \mathbb{R}^n$
* $u(t), \ t \in \mathbb{R}_+$ and $U(s) \triangleq \mathcal{L}[u(t)]$

If we define $X(s) \triangleq \mathcal{L}[x(t)]$ and $Y(s) \triangleq \mathcal{L}[y(t)]$, we want to determine their expressions in terms of the given information.

By applying the $\mathcal{L}[\cdot]$ to both sides of the state equation, we get:

$$
\underbrace{sX(s) - x_0}_{\substack{\text{Prop. of} \\ \text{Derivative}}} = \underbrace{\mathcal{L}[\dot{x}(t)]}_{\text{Linearity}} = FX(s) + GU(s)
$$

$$
(sI_n - F)X(s) = x_0 + GU(s)
$$

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

> [!info] In the Discrete-Time Case
> $$X_{\ell}(z) = (zI_n - F)^{-1} z x_0$$
> $$Y_{\ell}(z) = H(zI_n - F)^{-1} z x_0$$

# System Analysis: DT vs CT

| Discrete Time (DT)                                                                                                                                                                                                                                                                                                                                                             | Continuous Time (CT)                                                                                                                                                                                                                                                                                                                                                                                                  |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **State-Space Models**<br><br>**Definition: Discrete Time (DT) Model**<br>$$ \begin{cases} x(t+1) = Fx(t) + Gu(t) \\ y(t) = Hx(t) + Du(t) \end{cases} $$<br>Where $x(t) \in \mathbb{R}^n$, $u(t) \in \mathbb{R}^m$, $y(t) \in \mathbb{R}^p$.<br><br>**Block Diagram:** Uses a delay $z^{-1}$.<br><br>**Characteristic Polynomial:**<br>$\Delta_F(z) \triangleq \det(zI_n - F)$ | **State-Space Models**<br><br>**Definition: Continuous Time State-Space Model**<br>$$ \begin{cases} \dot{x}(t) = Fx(t) + Gu(t) \\ y(t) = Hx(t) + Du(t) \end{cases} $$<br>Where $x(t) \in \mathbb{R}^n$, $u(t) \in \mathbb{R}^m$, $y(t) \in \mathbb{R}^p$.<br><br>**Block Diagram:** Uses an integrator $\int$.                                                                                                        |
| **Time Response Evolution**<br><br>**Lagrange Formula:**<br>$$x(t) = F^t x(0) + \sum_{k=0}^{t-1} F^{t-1-k} G u(k)$$<br>$$y(t) = HF^t x(0) + \sum_{k=0}^{t-1} HF^{t-1-k} G u(k) + Du(t)$$<br><br>**Impulse Response:**<br>$$W(t) \triangleq D\delta(t) + HF^{t-1}G \delta_{-1}(t-1)$$                                                                                           | **Matrix Exponential & Time Response**<br><br>**Matrix Exponential:**<br>$$e^{Ft} \triangleq \sum_{k=0}^{+\infty} \frac{F^k t^k}{k!}$$<br><br>**Lagrange Formula:**<br>$$x(t) = e^{Ft}x_0 + \int_{0}^{t} e^{F(t-\tau)} G u(\tau) d\tau$$<br>$$y(t) = H e^{Ft}x_0 + \int_{0}^{t} H e^{F(t-\tau)} G u(\tau) d\tau + D u(t)$$<br><br>**Impulse Response:**<br>$$W(t) \triangleq D\delta(t) + H e^{Ft} G \delta_{-1}(t)$$ |
| **Analysis via Z-Transform**<br><br>**Z-Transform:** $V(z) = \sum_{t=0}^{+\infty} v(t) z^{-t}$<br><br>**Transfer Matrix:**<br>$$W(z) \triangleq H(zI_n - F)^{-1} G + D$$                                                                                                                                                                                                       | **Analysis via Laplace Transform**<br><br>**Laplace Transform:** $\mathcal{L}[\cdot]$ applied to $\dot{x} = Fx + Gu$.<br><br>**Transfer Matrix:**<br>$$W(s) \triangleq H(sI_n - F)^{-1}G + D$$<br>Poles of $W(s)$ are a subset of eigenvalues of $F$.                                                                                                                                                                 |

---

## Non Linear Discrete Time State-Space Models

A non linear DT time invariant state space model is described as follows:

$$
\begin{cases}
x(t+1) = f(x(t), u(t)) & \leftarrow \text{State Equation} \\
y(t) = h(x(t), u(t)) & \leftarrow \text{Output Equation}
\end{cases} \quad t \in \mathbb{Z}
$$
*(Generated Maps)*

We assume $\dim(x)=n, \quad \dim(u)=m, \quad \dim(y)=p$.
* $f: \mathbb{R}^n \times \mathbb{R}^m \longrightarrow \mathbb{R}^n$
* $h: \mathbb{R}^n \times \mathbb{R}^m \longrightarrow \mathbb{R}^p$

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

> [!info] Remark
> If $x_e$ is an equilibrium point corresponding to $u(t) = \bar{u}$, then corresponding to that the **output convolution** is constant since:
> $$y(t) = h(x(t), u(t)) = h(x_e, \bar{u}) \triangleq y_e \quad \forall t \in \mathbb{Z}_+$$

If the non-linear discrete-time state space model is not affected by an input, then it is an **Autonomous System** (not affected by inputs) and takes the following form:

$$
\begin{cases}
x(t+1) = f(x(t)) \\
y(t) = h(x(t))
\end{cases} \quad t \in \mathbb{Z}_+
$$

Where $\dim X = n, \dim Y = p$
$f: \mathbb{R}^n \to \mathbb{R}^n$
$h: \mathbb{R}^n \to \mathbb{R}^p$

> [!danger] Definition
> We say that $x_e$ is an **Equilibrium Point** of the autonomous state space models if:
>
> $$x(0) = x_e \implies x(t) = x_e \quad \forall t \in \mathbb{Z}_+$$
>
> $x_e$ is an equilibrium point $\Leftrightarrow x_e = f(x_e)$ (i.e. $x_e$ is a fixed point of the map $f(\cdot)$)

Clearly, also in this case the output corresponding to an equilibrium point is constant:
$$y(t) = h(x_e) \triangleq y_e \quad \forall t \in \mathbb{Z}_+$$

We'll focus on:
$$
(A) \quad \begin{cases}
x(t+1) = f(x(t)) \\
y(t) = h(x(t))
\end{cases} \quad t \in \mathbb{Z}_+, \dim(x)=n, \dim(y)=p
$$
*(A) Stands for Autonomous*

> [!danger] Definition
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

![[image 17.png]]


Suppose that we have a DT Linear State-Space Model:
$$x(t+1) = Fx(t) + \xcancel{Gu(t)}$$
> [!info] Note
> $u(t)=0$ (**Autonomous Systems**)

By referring to the linear DT autonomous system $x(t+1) = f(x(t)) \quad t \in \mathbb{Z}_+$, $x_e \in X = \mathbb{R}^n$ is an equilibrium point:
$$\iff x_e = F x_e \iff (I_n - F)x_e = 0 \iff x_e \in \underbrace{\text{Ker}(I_n - F)}_{\text{Vector Subspace}} \iff x_e \text{ is eigenvector of } F \text{ corresponding to } \lambda=1$$
*(Note: $F x_e = \lambda v$)*

## Case 1: $1 \in \sigma(F)$

If it's the case then the $\text{Ker}(I_n - F)$ (which is a vector subspace) contains infinite number of elements.
In fact $\bar{x} \in \text{Ker}(I_n - F)$ then $\alpha \bar{x} \in \text{Ker}(I_n - F) \quad \forall \alpha \in \mathbb{R}$.

> [!example] Illustration
> If $x(0) = x_0 = k\bar{x}$ then $x(t) = x_0 \quad \forall t \ge 0 \implies x(t) \xrightarrow{t \to \infty} \bar{x}$
>
> *[Diagrams showing the line of equilibrium points and a specific point $\bar{x}$]*
> * **Note on diagram:** "All equilibrium points".
> * **Note on diagram:** "If stick here cause it's a new equilibrium point".

> [!warning] Conclusion Case 1
> If $\lambda=1 \in \sigma(F)$ all the equilibria cannot be attractive, they can be (at best) stable.

## Case 2: $1 \notin \sigma(F)$

Then the only equilibrium point is the origin $x_e = 0$.

**When is $x_e = 0$ an attractive equilibrium point?**
If and only if $\|x(0)\|$ is sufficiently $\mathbb{O}$ then $x(t) \xrightarrow{t \to \infty} \mathbb{O}$.

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

## The Elementary Modes

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

### Autonomous Non Linear Discrete Time State Space Models 

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

## Linear DT Autom. State Sp. Mod.

> [!success] Model
> $$x(t+1) = F x(t) \quad t \in \mathbb{Z}_+ \quad F \in \mathbb{R}^{n \times n}$$

### Remarks:

1.  $x_e = 0$ is **always** an Eq. Point.
2.  $\exists x_e \neq 0$
    IFF $\text{Ker}(I_n - F) \neq \{0\}$ IFF $\lambda = 1 \in \sigma(F)$ is **Eigenvalue of F**.

> [!success] Remark 3: Attractivity
> Origin is an **Attractive Equilibrium Point** IFF all elementary modes associated with $F$ converge to $0$ asymptotically IFF every eigenvalue of $F$ has $|\lambda| < 1$.
>
> $\implies$ In this case $F$ is **Schur Stable**.

4.  If $x_e = 0$ is an **Attractive Equilibrium Point**, we have that $\text{Ker}(I_n - F) = \emptyset$ and it's also **Stable** and hence **Asymptotically Stable**.

> [!success] Remark 5: Stability
> $x_e = 0$ is **Stable Eq. Point** (Not necessarily implies attractive)
> $\iff$ All elementary modes associated with $F$ are bounded but not necessarily convergent.
> $\iff \forall \lambda \in \sigma(F)$ we have that $|\lambda| < 1$ OR $|\lambda| = 1$ and the multiplicity of $\lambda_i$ in $\psi_F(s)$ is unitary (Max size of $J_{\lambda_i}$ miniblock is one).

### Example: Linearization and Stability Analysis

**Consider the DT NL SSM:**

$$
\begin{cases}
x_1(t+1) = f_1(x_1(t), x_2(t), u(t)) \\
\quad \quad \ \ = x_1(t)[x_2(t)-1] + x_2(t) + u(t) \\
x_2(t+1) = f_2(x_1(t), x_2(t), u(t)) \\
\quad \quad \ \ = x_1(t) x_2^2(t)
\end{cases}
$$

**Tasks:**
1. Determine for every $\bar{u} \in \mathbb{R}$ the Eq. Point $x_e \in \mathbb{R}^2$ corresponding to $u(t) = \bar{u}$.
2. Determine the linearized model for each such Eq. Condition.

**Step 1: Equilibrium Points**

Set $u(t) = \bar{u}$, $x(t) = x(t+1) = x_e = (x_1, x_2)$. Then the Eq. Condition is determined by imposing:

$$
\begin{cases}
x_1 = f_1(x_1, x_2, \bar{u}) = x_1 x_2 - x_1 + x_2 + \bar{u} & (1) \\
x_2 = f_2(x_1, x_2, \bar{u}) = x_1 x_2^2 & (2)
\end{cases}
$$

**Solving (1):**
$$
(1) \iff 0 = x_1 x_2 - 2x_1 + x_2 + \bar{u} \quad \text{(Error in original derivation steps, corrected logic below based on image)}
$$
*From image:*
$$
(1) \iff 0 = x_1 x_2 + \cancel{x_1} - \cancel{x_1} + x_2 + \bar{u} \implies \text{(Wait, looking at image carefully)}
$$
*Re-reading image:* $(1) \iff 0 = x_1 x_2 - x_1 + \cancel{x_1} - \cancel{x_1} \dots$
Let's trace the image exactly:
$(1) \iff 0 = x_1 x_2 - 2x_1 + x_2 + \bar{u}$? No, the image shows:
$x_1 = x_1 x_2 - x_1 + x_2 + \bar{u} \implies 0 = x_1 x_2 - 2x_1 + x_2 + \bar{u}$.
*Wait, looking at the simplification in the image:*
It seems the writer wrote: $0 = x_1(x_2 + \dots)$.
Let's look at Eq (2) first, it's clearer.
$(2) \iff 0 = x_1 x_2^2 - x_2 = (x_1 x_2 - 1) x_2$

**Eq. (2) Solutions:**
* (2A) $x_2 = 0$
* (2B) $x_1 x_2 - 1 = 0 \implies x_1 x_2 = 1$

**For (2A) $x_2=0$:**
Then (1) becomes: $0 = \cancel{x_1(0)} - 2x_1 + 0 + \bar{u} \implies -2x_1 = -\bar{u} \implies x_1 = \bar{u}/2$.
*Correction from Image Text:* The image actually simplifies (1) differently. Let's look at the "Eq (1)" section in the image.
It writes: $\iff 0 = x_1 x_2 + \cancel{x_1} - \cancel{x_1} + \bar{u}$? No.
Let's stick to the handwritten result logic.

*Image logic:*
$(1) \iff 0 = x_1(x_2 + \dots)$
$(2) \iff 0 = x_1 x_2^2 - x_2 = (x_1 x_2 - 1)x_2$

**Case (1A) $x_1 = 0$:** (This seems to come from a different interpretation of eq 1 in the notes, or it's a specific case).
*Actually, looking at the image "Sol (1)":*
2 Solutions: (1A) $x_1=0$. (1B) $x_2 + \bar{u} = 0 \to x_2 = -\bar{u}$.

*Let's check the original equation again in the image:*
$x_1 = x_1(x_2-1) + x_2 + \bar{u} \implies 0 = x_1 x_2 - 2x_1 + x_2 + \bar{u}$.
The notes seem to solve a slightly different system or I am misreading $f_1$.
Let's look at the block "Ex:" at the top.
$x_1(t+1) = x_1(t)[x_2(t)-1] + x_2(t) + u(t)$. Correct.
The derivation below:
$(1) \iff 0 = x_1 x_2 + \dots$
Let's look at the result analysis at the bottom left.
$(2A) \ \bar{u}=0 \implies x_e=(0,0) \land (x_1, 0) \ x_1 \in \mathbb{R}$.
$(2B) \ \bar{u} \neq 0 \implies x_e=(0,0) \land (-1/\bar{u}, -\bar{u})$.

**Analyzing Eq (2) again from image:**
$\iff 0 = x_1 x_2^2 - x_2 \iff (x_1 x_2 - 1) x_2 = 0$.
So $x_2 = 0$ OR $x_1 x_2 = 1$.

**If $x_2 = 0$:**
Substitute into (1): $x_1 = x_1(-1) + 0 + \bar{u} \implies 2x_1 = \bar{u} \implies x_1 = \bar{u}/2$.
*Wait, the image says $x_e=(0,0)$ for $\bar{u}=0$ and $x_1 \in \mathbb{R}$.*
This implies when $x_2=0$ and $\bar{u}=0$, eq (1) is $x_1 = -x_1 \implies 2x_1 = 0 \implies x_1=0$.
The notes seem to have $x_1(t)[x_2(t)]$ in the first line instead of $x_1(t)[x_2(t)-1]$?
Let's check the line "Eq. 1".
It says: $(1) \iff 0 = x_1 x_2 + x_1 - x_1 + \bar{u}$? No.
It says: $(1) \iff 0 = x_1 x_2 + \bar{u}$. (This matches if the term was just $x_1 x_2$).
**Assumption:** The first equation in the notes is likely $x_1(t+1) = x_1(t)x_2(t) + x_2(t) + u(t)$?
Let's check the linearization matrix $F$.
$F_{11} = \frac{\partial f_1}{\partial x_1} = x_2 + \dots$? In the image it is $x_2 + 1 + \bar{u}$? No, looks like $x_2 + 1$.
$F_{12} = \frac{\partial f_1}{\partial x_2} = x_1$?
If $f_1 = x_1 x_2 + x_2$, then $\partial_{x_1} = x_2$, $\partial_{x_2} = x_1 + 1$.
The image has $F = \begin{bmatrix} x_2+1+\bar{u} & x_1 \\ x_2^2 & 2x_1 x_2 \end{bmatrix}$? No.
Let's transcribe exactly what is written, even if the math in the image seems inconsistent.

**Transcription of the derivation in the image:**
$(1) \iff 0 = x_1 x_2 + \cancel{x_1} - \cancel{x_1} + \bar{u} = x_1(x_2 + \bar{u})$ **(Note: This line is confusing in source)**
$(2) \iff 0 = x_1 x_2^2 - x_2 = (x_1 x_2 - 1) x_2$

**Eq (1) Solutions according to image:**
* (1A) $x_1 = 0$
* (1B) $x_2 + \bar{u} = 0 \implies x_2 = -\bar{u}$

**For (1A) $x_1=0$:**
Then (2) becomes $x_2 = 0 \implies x_e = (0,0)$. (True for every $\bar{u}$).

**For (1B) $x_2 = -\bar{u}$:**
Then (2) becomes $0 = -\bar{u}^2 x_1 + \bar{u}$? No, $x_1(-\bar{u})^2 - (-\bar{u}) = 0$.
$x_1 \bar{u}^2 + \bar{u} = 0$.
* If $\bar{u} = 0$: Always true $\forall x_1 \in \mathbb{R}$. (2A)
* If $\bar{u} \neq 0$: Equation becomes $0 = x_1 \bar{u} + 1 \implies x_1 = -1/\bar{u}$. (2B)

**Summary of Equilibria:**
* (2A) $\bar{u} = 0$: $x_e = (0,0) \land (x_1, 0) \ x_1 \in \mathbb{R}$
* (2B) $\bar{u} \neq 0$: $x_e = (0,0) \land (-1/\bar{u}, -\bar{u})$

**Step 2: Linearized Model**

$$
\delta x(t+1) = F \delta x(t) + G \delta u(t)
$$

Where:
$$
F \triangleq \frac{\partial f}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \quad G \triangleq \frac{\partial f}{\partial u}\bigg|_{\substack{x=x_e \\ u=\bar{u}}}
$$

**Jacobian F:**
$$
F = \begin{bmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2}
\end{bmatrix}_{\substack{x=x_e \\ u=\bar{u}}} = \begin{bmatrix}
x_2 + 1 & x_1 \\
x_2^2 & 2x_1 x_2
\end{bmatrix}
$$
*(Note: The entry $F_{11}$ in image looks like $x_2+1+\bar{u}$ or just $x_2+1$. Based on $f_1 = x_1 x_2 + x_2 + u$, $\partial_{x_1} = x_2$. The image is slightly ambiguous here, transcribing $x_2+1$ which fits $f_1 = x_1(x_2+1)$).*

### Case Analysis

* **Case 1: $\bar{u}=0$**
    * $x_e(x_1, 0), x_1 \in \mathbb{R}$
    $$F = \begin{bmatrix} 1 & x_1 \\ 0 & 0 \end{bmatrix}$$

* **Case 2: $\bar{u} \neq 0$**
    * $x_e = (0,0)$
    $$F = \begin{bmatrix} 1+\bar{u} & 0 \\ 0 & 0 \end{bmatrix}$$
    *(Note: Image shows $1+\bar{u}$, implying $f_1$ had a term depending on $u$ or constant)*.

* **Case 3: $\bar{u} \neq 0$**
    * $x_e (-1/\bar{u}, -\bar{u})$
    $$F = \begin{bmatrix} 1 & -1/\bar{u} \\ \bar{u}^2 & 2 \end{bmatrix}$$

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

## Example (Continued/Revisited)

**Consider:**
$$
\begin{cases}
x_1(t+1) = f_1(x_1(t), x_2(t)) = x_1(t)x_2(t) \\
x_2(t+1) = f_2(x_1(t), x_2(t)) = \frac{1}{2}x_2(t) - x_1(t)x_2(t)
\end{cases}
$$

**Determine Eq. and study the Asymp. Stab. via linearity.**

**Equilibria:**
$$
\begin{cases}
x_1 = x_1 x_2 \implies 0 = x_1 x_2 - x_1 = x_1(x_2 - 1) \\
x_2 = \frac{1}{2}x_2 - x_1 x_2 \implies 0 = \frac{1}{2}x_2 + x_1 x_2
\end{cases}
$$

**From Eq. 1:**
* (1A) $x_1 = 0 \implies$ in (2) $x_2 = 0 \implies x_e=(0,0)$.
* (1B) $x_2 = 1 \implies$ in (2) $0 = -\frac{1}{2} + x_1 \implies x_1 = 1/2$?
    *Image Calculation:*
    $(1B) x_2 = 1 \implies$ Then (2) becomes $\dots$ $x_1 = -1/2$.
    $\to x_e = (-1/2, 1)$.

**Jacobian:**
$$
\frac{\partial f}{\partial x} = \begin{bmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2}
\end{bmatrix} = \begin{bmatrix}
x_2 & x_1 \\
-x_2 & \frac{1}{2} - x_1
\end{bmatrix}
$$

**Analysis:**

1.  **For $x_e = (0,0)$:**
    $$F = \begin{bmatrix} 0 & 0 \\ 0 & 1/2 \end{bmatrix}$$
    $\sigma(F) = \{0, 1/2\}$.
    $\implies x_e = (0,0)$ **Asympt. Stable** for the NL System (is Schur Stable).

2.  **For $x_e = (-1/2, 1)$:**
    $$F = \begin{bmatrix} 1 & -1/2 \\ -1 & 1 \end{bmatrix}$$
    If the sum of diag. is more than 1, not Schur Stable.
    $\text{Tr}(F) = f_{11} + f_{22} = 1 + 1 = 2$.
    $\text{Tr}(F) = \lambda_1 + \lambda_2 = 2$.
    $\lambda_1$ and $\lambda_2$ cannot be both modulus $< 1$.

## Continuous Time NL Time Invariant SSM

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
## The Linear (Autonomous) Case:

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

| Discrete Time (DT)                                                                                   | Continuous Time (CT)                                                                                         |
| :--------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------- |
| **Diagram:** Unit Circle on Complex Plane.<br>Eigenvalues inside the circle.<br>**"Attractiveness"** | **Diagram:** Complex Plane.<br>Eigenvalues on the left half plane ($\text{Re} < 0$).<br>**"Attractiveness"** |
![[image-1 8.png]]

> [!info] Note
> If $x_e = 0$ is **Attractive**, it is also **Stable** and hence **Asymptotically Stable**.

5.  $x_e = 0$ is a **Stable Eq. Point** IFF elementary modes associated with $F$ are **Bounded**.

    $\iff \forall i \ \text{Re}(\lambda_i) \le 0$ AND if $\text{Re}(\lambda) = 0$ then there is only one elementary mode associated with $\lambda_i$.

> [!success] Stability Condition
> $\iff \forall \lambda \in \sigma(F)$ either $\text{Re}(\lambda) < 0$ OR $\text{Re}(\lambda) = 0$ AND the size of the largest Jordan Miniblock associated with $\lambda$ is 1.

6.  We say that system is (Asymptotically) Stable if $x_e = 0$ is (Asymptotically) Stable.

## Linearization of CT NC SSM around Eq. Condition

**Consider:**

$$
\begin{cases}
\dot{x}(t) = f(x(t), u(t)) \\
y(t) = h(x(t), u(t))
\end{cases} \quad t \in \mathbb{R}_+ \quad \dim x = n \quad \dim u = m \quad \dim y = p
$$

**Assume:**
1.  Let $x_e$ be an **Eq. Point** of the system corresponding to $u(t) = \bar{u}$
    $\implies 0 = f(x_e, \bar{u})$ and $y(t) = y_e \triangleq h(x_e, \bar{u})$
2.  $f(\cdot, \cdot)$ and $h(\cdot, \cdot)$ are **continuous with their derivatives**.

Set:
$$
\begin{aligned}
\delta x(t) &\triangleq x(t) - x_e \\
\delta u(t) &\triangleq u(t) - \bar{u} \\
\delta y(t) &\triangleq y(t) - y_e
\end{aligned}
$$

**Then:**
$$
\frac{d}{dt}[\delta x(t)] = \frac{d}{dt}[x(t)] = f(x_e + \delta x(t), \bar{u} + \delta u(t))
$$

Using **Taylor Series Expansion**:
$$
= \underbrace{f(x_e, \bar{u})}_{\equiv 0} + \frac{\partial f}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \delta x(t) + \frac{\partial f}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \delta u(t) + \underbrace{o(x(t), u(t))}_{\substack{\text{Infinitesimal of} \\ \text{higher order wrt} \\ \sqrt{\|\delta x(t)\|^2 + \|\delta u(t)\|^2}}}
$$

**Approximate Terms:**

> [!success] Linearized State Equation
> $$\frac{d}{dt}[\delta x(t)] = F \delta x(t) + G \delta u(t)$$
>
> Where:
> $$F \triangleq \frac{\partial f}{\partial x}\bigg|_{\substack{x=x_e \\ u=\bar{u}}} \quad \text{and} \quad G \triangleq \frac{\partial f}{\partial u}\bigg|_{\substack{x=x_e \\ u=\bar{u}}}$$

**Similarly, we can obtain:**

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

![[image-2 4.png]]

# Stability & Linearization: DT vs CT

| Discrete Time (DT)                                                                                                                                                                                                                                                                                                                                                                                                               | Continuous Time (CT)                                                                                                                                                                                                                                                                                                                                                                                                                             |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Stability & Equilibrium**<br><br>**Equilibrium:** $x_e = f(x_e)$ (Fixed point).<br>Linear case: $x(t+1)=Fx(t) \implies (I-F)x_e = 0$.<br><br>**Stability Criteria (Linear):**<br>1. **Asymptotically Stable:** $\forall \lambda \in \sigma(F), \| \lambda \| < 1$.<br>2. **Stable:** $\forall \lambda, \| \lambda \| \le 1$ AND simple blocks for $\| \lambda \|=1$.<br>3. **Unstable:** $\exists \lambda, \| \lambda \| > 1$. | **Stability & Equilibrium**<br><br>**Equilibrium:** $f(x_e) = 0$ (Null derivative).<br>Linear case: $\dot{x}=Fx \implies Fx_e = 0$.<br><br>**Stability Criteria (Linear):**<br>1. **Asymptotically Stable:** $\forall \lambda \in \sigma(F), \text{Re}(\lambda) < 0$.<br>2. **Stable:** $\forall \lambda, \text{Re}(\lambda) \le 0$ AND simple blocks for $\text{Re}(\lambda)=0$.<br>3. **Unstable:** $\exists \lambda, \text{Re}(\lambda) > 0$. |
| **Non-Linear Linearization**<br><br>Jacobians evaluated at $(x_e, \bar{u})$.<br>Stability of $x_e$ determined by eigenvalues of $F = \frac{\partial f}{\partial x}$.<br>**Critical Case:** If eigenvalues on unit circle ($\lambda=1$), linearization is inconclusive.                                                                                                                                                           | **Non-Linear Linearization**<br><br>Jacobians evaluated at $(x_e, \bar{u})$.<br>Stability of $x_e$ determined by eigenvalues of $F = \frac{\partial f}{\partial x}$.<br>**Critical Case:** If eigenvalues on imaginary axis ($\text{Re}(\lambda)=0$), linearization is inconclusive.                                                                                                                                                             |

---

## Reachability & Controllability Problems:

### Reachability:
Given some time $T>0$ finite, and some state $x_f \in X$, can I find an input signal $u(t) \ t \in [0, T]$ that drives the state of the system from $x(0)=0$ to $x(T)=x_f$?

### Zero Controllability or Controllability to Zero
Given some time $T>0$ and some state $x_0 \in X$, can I find an input signal $u(t) \ t \in [0, T]$ that drives the state of the system from $x(t)=x_0$ to $x(T)=x_f$?

**Diagrams:**
* **Reachability:** Graph showing state trajectory $x(t)$ going from origin $0$ to $x_f$ over time $T$.
* **Controllability:** Graph showing state trajectory $x(t)$ going from $x_0$ to the axis (implicitly $0$) over time $T$.

## Reachability of DT SSM

Consider the system $\Sigma$:
$$
\begin{cases}
x(t+1) = Fx(t) + Gu(t) & t \in \mathbb{Z}_+ \\
y(t) = Hx(t) + Du(t)
\end{cases}
$$

$\dim x = n; \ \dim u = m; \ \dim y = p$

> [!danger] Def
> Given $k \in \mathbb{Z}, \ k>0$. A state $x_f \in X = \mathbb{R}^n$ is said to be **Reachable** at time $t=k$ (equivalently in $k$ steps) if
>
> $\exists u(0), u(1), \dots, u(k-1) \in U = \mathbb{R}^m$ that drives the state from $x(0)=0$ to $x(k)=x_f$.
>
> $$x(0)=0 \xrightarrow{u(0), u(1) \dots u(k-1)} x(k)=x_f$$

Since $x(0)=0$ then:
$$
x(k) = x_f(k) = \sum_{i=0}^{k-1} F^{k-1-i} G u(i) = \underbrace{[G | FG | \dots | F^{k-1} G]}_{\substack{\triangleq R_k \\ \text{Reachability Matrix} \\ \text{at time } k \text{(in } k \text{ steps)}}} \underbrace{\begin{bmatrix} u(k-1) \\ u(k-2) \\ \vdots \\ u(0) \end{bmatrix}}_{\substack{\text{From the} \\ \text{newer to} \\ \text{oldest}}}
$$
*(Note above matrix: Matrix Blocks)*

Therefore:

> [!success] Reachability Condition
> $x_f$ is reachable at time $k \iff \exists u(0), \dots, u(k-1) \in \mathbb{R}^m = U$
>
> $$
> x_f = R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix} \iff x_f \in \text{Im}(R_k)
> $$
> *(Note: analogy to linear system $b=Ax$)*

If we define $X_k^R$ the **Set** of states that are reached in $k$ steps:

> [!danger] Definition: Reachability Set
> $$X_k^R \triangleq \left\{ x_f \in X = \mathbb{R}^n : \exists u(0) \dots u(k-1) \text{ s.t. } x(0) \xrightarrow[u(0)\dots u(k-1)]{} x(k)=x_f \right\}$$


THEN:
> [!success] Result
> $$X_k^R = \text{Im} R_k$$
>
> *It's a Vector Space*

THEREFORE $X_k^R$ IS A VECTOR SUBSPACE OF $X=\mathbb{R}^n$.

## In General:

For every $k \in \mathbb{Z}, \ k>0$:

> [!success] Inclusion Property
> $$X_k^R \subseteq X_{k+1}^R$$

**In Fact:**

$$X_k^R = \text{Im} [G | FG | \dots | F^{k-1} G] \subseteq \text{Im} [G | FG | \dots | F^{k-1} G | F^k G] = X_{k+1}^R$$

**If $x_f \in X_k^R$ THEN**

[Graphs illustration: Shift of the input sequence]

* **Graph 1:** Sequence $u_0, u_1 \dots u_{k-1}$ reaches $x_f$.
* **Graph 2:** Sequence shifted by 1 step to right ($u_0=0, \bar{u}_1=u_0 \dots \bar{u}_k=u_{k-1}$).

> [!info] Logic
> **SHIFT BY 1 STEP TO RIGHT** ($=0$ inserted at start).
>
> $$\implies x_f \in X_{k+1}^R$$

Consequently

$$
\underset{\substack{|| \\ \text{Im } G}}{X_1^R} \subseteq \underset{\substack{|| \\ \text{Im}[G|FG]}}{X_2^R} \subseteq \dots \subseteq \underset{\substack{|| \\ \text{Im}[G|FG|\dots|F^{k-1}G]}}{X_k^R} \subseteq X_{k+1}^R = \text{Im}[G|FG|\dots|F^kG]
$$

Since each $X_k^R$ is a vector subspace of $X=\mathbb{R}^n$ and $X_k^R \subsetneq X_{k+1}^R$ implies $\dim X_{k+1}^R \ge \dim X_k^R + 1$ then it is clear that:

> [!success] Stability of Reachability Subspace
> $\exists \bar{k} \in \mathbb{Z}, \bar{k} > 0$ such that:
> $$X_{\bar{k}}^R \equiv X_k^R \quad \forall k \ge \bar{k}$$
>
> $$X_1^R \subseteq X_2^R \subseteq \dots \subseteq X_{\bar{k}}^R = X_{\bar{k}+1}^R = \dots$$


### Reachability of DT Linear Models

**System $\Sigma$:**
$$
x(t+1) = Fx(t) + Gu(t) \quad t \in \mathbb{Z}_+
$$
$\equiv$ **Pair $(F,G)$** where $F \in \mathbb{R}^{n \times n}, G \in \mathbb{R}^{n \times m}$.

$x_f \in X = \mathbb{R}^n$ is reachable in $k$ steps ($k \in \mathbb{Z}$) $\iff x_f \in \text{Im}[\underbrace{G | FG | \dots | F^{k-1}G}_{\triangleq R_k}]$

> [!info] Reachability Matrix in k-steps
> $\triangleq R_k$

$$
X_k^R \triangleq \{ x \in X : x \text{ reachable in } k \text{ steps} \} \equiv \text{Im} R_k
$$
$\implies X_k^R$ is subspace of $\mathbb{R}^n$ (*Cause of $x \in X$*)

$$
\forall k \ge 1 \quad X_k^R \subseteq X_{k+1}^R \implies X_1^R \subseteq X_2^R \subseteq \dots \subseteq X_k^R \subseteq X_{k+1}^R \subseteq \dots \subseteq X = \mathbb{R}^n
$$

Since $X_k^R$ is a vector subspace $\forall k \ge 1$, then: $X_k^R \subsetneq X_{k+1}^R \implies \dim X_{k+1}^R \ge \dim X_k^R + 1$.

So there cannot be an infinite number of proper inclusion in the prev chain.
**Hence:**
> [!success] Result
> $\exists \bar{k} \ge 1 \quad \text{s.t.} \quad X_k^R = X_{\bar{k}}^R \quad \forall k \ge \bar{k}$

**Is it possible that:** $X_1^R \subset X_2^R \subset X_3^R \subset X_4^R \subset X_5^R = X$?
*[Diagram showing dimension increasing step-wise until it flattens]* -> **Not Possible**.

If the chain stops for some $k$ it cannot grow anymore.

> [!warning] Proposition
> (1) If $X_k^R = X_{k+1}^R$ then $X_{k+1}^R = X_{k+2}^R$ ($\implies X_{k+i}^R = X_k^R \quad \forall i \ge 0$)
>
> (2) If $\bar{k} \triangleq \min \{ k \in \mathbb{Z}, k \ge 1 : X_k^R = X_{k+1}^R \}$ then $\bar{k} \le n$

### Proof

(1) It is always true that $X_{k+1}^R \subseteq X_{k+2}^R$, so we need to prove that if $X_k^R = X_{k+1}^R$ then $X_{k+2}^R \subseteq X_{k+1}^R$.

Assume that $x_f \in X_{k+2}^R$. This means that $\exists \mu(t) = u_t, \ t=0, 1, \dots, k+1$ such that:

| Time | 0 | 1 | 2 | ... | k+1 | k+2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **State** | 0 | $x_1$ | $x_2$ | ... | $x_{k+1}$ | $x_f$ |
| **Input** | $\mu_0$ | $\mu_1$ | $\mu_2$ | | $\mu_{k+1}$ | |

Since $x_{k+1} \in X_{k+1}^R = X_k^R$ $\exists \mu(t) = \bar{u} \quad t=0, \dots, k-1$ such that:

| Time | 0 | 1 | 2 | ... | k-1 | k | k+1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **State** | 0 | $\bar{x}_1$ | $\bar{x}_2$ | ... | $\bar{x}_{k-1}$ | $\bar{x}_{k+1}$ | $x_f$ |
| **Input** | $\bar{\mu}_0$ | $\bar{\mu}_1$ | $\bar{\mu}_2$ | | $\bar{\mu}_{k-1}$ | $\mu_{k+1}$ | |

$\implies x_f \in X_{k+1}^R$

*[Diagram showing trajectories]*

(2) **If $G=0$:**
Then $X_k^R = \{0\} \quad \forall k \ge 1$ and hence the result is trivial.

**If $G \neq 0$:**
$$
\underbrace{X_1^R}_{\dim X_1^R \ge 1} \subset \underbrace{X_2^R}_{\dim X_2^R \ge 2} \subset \underbrace{X_3^R}_{\dim X_3^R \ge 3} \subset \dots \subset \underbrace{X_{\bar{\mu}}^R}_{\substack{\uparrow \\ n = \dim X \ge \dim X_{\bar{\mu}}^R \ge \bar{k}}} = X_{\bar{k}+1}^R \subseteq X
$$

**Consequently:**
$$
X_1^R \subset X_2^R \subset \dots \subset \underbrace{X_k^R = X_{k+1}^R = \dots \subseteq X = \mathbb{R}^n}_{X_k^R \equiv X_n^R \text{ is here}}
$$

## We Define

**Reachable Subspace** of the system $\Sigma$ (Equiv. of the pair $(F,G)$) the set of states that can be reachable in finite number of steps and denote it by $X^R$.

Then:
> [!success] Reachable Subspace Formula
> $$X^R = X_{\bar{k}}^R = X_n^R = \text{Im}[G | FG | \dots | F^{n-1}G]$$
>
> $$\triangleq \mathcal{R} \in \mathbb{R}^{n \times nm} \quad \text{REACHABILITY MATRIX}$$

We say that the pair $(F,G)$ (of system $\Sigma$) is **Reachable in $X$** (can be reached in finite time) if:
$$X^R = X$$
### 1st Reachability Criterion

> [!success] Criterion
> $(F,G)$ is Reachable $\iff \text{rank}[G | FG | \dots | F^{n-1}G] = n$
>
> *($R$ is the Reachability Matrix)*

> [!warning] Proposition
> If $\Sigma$ is a single input reachable system then $\bar{k} = n$.

**Proof:**
I already know that $\bar{k} \le n$.
On the other hand, if we consider the reachability matrices associated with the pair $(F,G) = (F,g)$ ($G=g \in \mathbb{R}^n$) then:

$$X_{\bar{k}}^R = \text{Im}[g | Fg | \dots | F^{\bar{k}-1}g]$$

Has at most dimension $\bar{k}$ ($n \times \bar{k}$ matrix).
So $\bar{k}$ cannot be smaller than $n$.

$\implies \bar{k} = n$.

From now on when a pair $(F,G)$ is reachable we'll call $\bar{k}$ its **Reachability Index** and denote it by $r$.

### (3) Cayley-Hamilton's Theorem

> [!danger] Theorem
> Given $F \in \mathbb{D}^{n \times n}$ let $\Delta_F(z) = z^n + a_{n-1}z^{n-1} + \dots + a_0$ be its **Characteristic Polynomial** (i.e. $\det(zI_n - F)$).
>
> Then $\Delta_F(z)$ is an **Annihilating Polynomial** of $F$, i.e.:
>
> $$\Delta_F(F) = F^n + a_{n-1}F^{n-1} + \dots + a_1 F + a_0 I_n = \mathbb{O}_{n \times n}$$
>
> $$\implies F^n = - \sum_{i=0}^{n-1} a_i F^i$$

### Remark:

> [!info] Matrix Properties
> **(1)** Let $A \in \mathbb{R}^{n \times n}$ matrix and $B \in \mathbb{R}^{n \times k}$ matrix.
> Then $A(\text{Im } B) = \text{Im}(AB)$.
>
> **Proof:**
> $$
> \begin{aligned}
> x \in A(\text{Im } B) &\iff x = Ay \ \exists y \in \text{Im } B \\
> &\iff x = A(Bz) \ \exists z \\
> &\iff x = (AB)z \ \exists z \\
> &\iff x \in \text{Im}(AB)
> \end{aligned}
> $$
>
> **(2)** Let $F \in \mathbb{R}^{n \times n}$ and $S$ a vector subspace of $X = \mathbb{R}^n$. Then $S$ is said to be **$F$-invariant** if:
> $$FS \subseteq S \quad (\text{In other words } \forall s \in S, \ Fs \in S)$$

> [!warning] Proposition
> Given a pair $(F,G)$, $F \in \mathbb{R}^{n \times n}$ and $G \in \mathbb{R}^{n \times m}$, let:
>
> $$X^R = \text{Im}[G | FG | \dots | F^{n-1}G]$$
>
> be its Reachable Subspace then:
> $X^R$ is the **Smallest $F$-Invariant Subspace** of $X=\mathbb{R}^n$ including $\text{Im } G$.
>
> *[Diagram: Inner circle $\text{Im } G$, Middle circle $X^R$, Outer circle $S \subseteq X$. Note: $S$ is any other F-invariant subspace of X including $\text{Im } G$.]*
![[image-3 2.png]]
### Proof

Clearly $\text{Im}[G] \subseteq \text{Im}[G | FG] \subseteq \text{Im}[G | FG | \dots | F^{n-1}G] = X^R$.

We want to prove that $X^R$ is $F$-invariant.
$$FX^R = F(\text{Im}[G | FG | \dots | F^{n-1}G])$$

$$
= \underbrace{\text{Im}(F[G | FG | \dots | F^{n-1}G])}_{\text{Remark (1)}} = \text{Im}[FG | F^2 G | \dots | F^n G] \subseteq \text{Im}[G | FG | \dots | F^{n-1}G | F^n G]
$$

$$
\equiv \underbrace{\text{Im}[G | FG | \dots | F^n G]}_{\text{Remark (3)}} \subset X^R
$$

To conclude we need to prove that if $S$ is any vector subspace of $F$ which includes the $\text{Im } G$ and it's $F$-invariant then: $S \supseteq X^R$.

### Proof

$$
\boxed{\text{Im } G \subseteq S}
$$

$$
\boxed{\text{Im}[FG]} = F(\text{Im } G) \subseteq FS \subseteq \boxed{S}
$$
*(Remark (2))*

$$
\boxed{\text{Im}[F^2 G]} = F(\text{Im}[FG]) \subseteq FS \subseteq \boxed{S}
$$
$$\vdots$$
$$
\text{Im}[F^{n-1} G] \subseteq S
$$

$$
\implies \text{Im}[G | FG | \dots | F^{n-1} G] \subseteq S
$$

> [!info] Note
> If 2 vect subspaces $W_1$ and $W_2$ are included in a vect space $V$ then all Linear Comb. of the vectors of $W_1$ and $W_2$ are included in $V$.

## Review of Basis of vect space and algebraically equivalent systems

Consider, **for instance**, a DT SSM:

$$
\Sigma : \begin{cases}
x(t+1) = Fx(t) + Gu(t) \\
y(t) = Hx(t) + Du(t)
\end{cases} \quad t \in \mathbb{Z}_+
$$

* $\dim x = n$
* $\dim u = m$
* $\dim y = p$

In general we always assume that we have fixed in each vect. spaces:
* $X = \mathbb{R}^n \longleftarrow B_X$
* $U = \mathbb{R}^m \longleftarrow B_U$
* $Y = \mathbb{R}^p \longleftarrow B_Y$

**Basis**

So $x(t), u(t), y(t)$ are the coords of the state at time $t$ wrt $B_X$, the input at time $t$ wrt $B_U$ and finally the output at time $t$ wrt $B_Y$.

**What does it means?**

Assuming that $B_X = \{v_1, \dots, v_n\}$ this means that:

$$
(\substack{\text{State at} \\ \text{time } t}) = \sum_{i=1}^n x_i(t) v_i = [v_1 | v_2 | \dots | v_n] \underbrace{\begin{bmatrix} x_1(t) \\ \vdots \\ x_n(t) \end{bmatrix}}_{x(t)}
$$


We assume now that we change the basis of $X$: new base $\bar{B}_x = \{\bar{v}_1, \bar{v}_2 \dots \bar{v}_n\}$.

We want to understand how the system changes if we move to this new base in $X$ to keep $B_u$ and $B_y$ unrelated.

We recall that:
If we consider $B_x$ as basis of $X$ and $\bar{v}_j$ as a vector of $X$, we can find coefficients $t_{ij} \in \mathbb{C}$ such that:

$$
\bar{v}_j = \sum_{i=1}^n v_i t_{ij} = [v_1 \dots v_n] \begin{bmatrix} t_{1j} \\ t_{2j} \\ \vdots \\ t_{nj} \end{bmatrix} \quad t_{ij} \in \mathbb{C}, \ v_i \in B_x
$$

$$
= [\bar{v}_1 | \bar{v}_2 | \dots | \bar{v}_n] = [v_1 | v_2 | \dots | v_n] \underbrace{\begin{bmatrix} t_{11} & \dots & t_{1n} \\ \vdots & \ddots & \vdots \\ t_{n1} & \dots & t_{nn} \end{bmatrix}}_{\triangleq T \in \mathbb{C}^{n \times n}} \quad \forall j
$$

Conversly we can regard $\bar{B}_x$ as the basis and express each $v_j$ as a linear comb. of the vectors $\bar{v}_1 \dots \bar{v}_n \implies$
$$[v_1 | v_2 | \dots | v_n] = [\bar{v}_1 | \bar{v}_2 | \dots | \bar{v}_n] [S] \quad S \in \mathbb{C}^{n \times n}$$

$$
\implies [v_1 | v_2 | \dots | v_n] = [v_1 | \dots | v_n] [T] [S]
$$

By the uniqueness of the representation of a vector with a given basis, this implies that:
$$
\boxed{T} \boxed{S} = \boxed{I_n}
$$
$\implies S = T^{-1}$, "$T$" is **NOT** singular.

If we denote by $\bar{x}(t)$ the vector of coords of the state at time $t$ w.r.t. the new basis $\bar{B}_x$, we want to know the relationship between $\bar{x}(t)$ and $x(t)$.

**From:**
$$[\bar{v}_1 | \dots | \bar{v}_n] [\bar{x}(t)] = \text{state at time } t = [v_1 | \dots | v_n] [x(t)]$$

$$\implies [v_1 | \dots | v_n] [T] [\bar{x}(t)] = [v_1 | \dots | v_n] [x(t)]$$

**We deduce that:**

$$
\boxed{T} \bigg[\bar{x}(t)\bigg] = \bigg[x(t)\bigg] \underset{\substack{\text{can also} \\ \text{be written}}}{\implies} \bar{x}(t) = \boxed{T^{-1}} x(t)
$$
*(The boxes are to visualize better)*

### As a Result:

> [!success] New System Dynamics
> $$
> \begin{cases}
> \bar{x}(t+1) = T^{-1} x(t+1) = T^{-1} F x(t) + T^{-1} G u(t) = (T^{-1}FT) \bar{x}(t) + (T^{-1}G) u(t) \\
> y(t) = (HT) \bar{x}(t) + (D) u(t)
> \end{cases}
> $$

**Summary of Transformation:**

| Old Basis                   | New Basis                                                                                                                |
| :-------------------------- | :----------------------------------------------------------------------------------------------------------------------- |
| $B_x = \{v_1, \dots, v_n\}$ | $\bar{B}_x = \{\bar{v}_1, \dots, \bar{v}_n\}$                                                                            |
| **Transformation:**         | $[\bar{B}_x] = [B_x][T]$                                                                                                 |
| **State:**                  | $x(t) \longrightarrow \bar{x}(t) = T^{-1} x(t)$                                                                          |
| **System:**                 | $\Sigma = (F, G, H, D) \longrightarrow \bar{\Sigma} = (\bar{F}, \bar{G}, \bar{H}, \bar{D}) = (T^{-1}FT, T^{-1}G, HT, D)$ |

### Definition

Given two SSM, $\Sigma = (F, G, H, D)$ and $\bar{\Sigma} = (\bar{F}, \bar{G}, \bar{H}, \bar{D})$ of the same dimension and with the same number of inputs and outputs, we say that $\Sigma$ and $\bar{\Sigma}$ are **Algebraically Equivalent** if they represent the same system w.r.t. two different basis in $X$, which means that $\exists$ an $n \times n$ non singular matrix $T$ such that:

$$
\begin{cases}
\bar{F} = T^{-1} F T \\
\bar{G} = T^{-1} G \\
\bar{H} = H T \\
\bar{D} = D
\end{cases}
$$

### So some properties of algebraic equivalence:

**(1) Two algebraic equivalent systems have the same Transfer Matrix**

$$
\begin{aligned}
\bar{W}(z) &= (zI_n - \bar{F})^{-1} \bar{G} + \bar{D} \\
&= HT [ z \underbrace{T^{-1} I_n T}_{I_n} - T^{-1} F T ]^{-1} T^{-1} G + D \\
&= HT [ T^{-1} (zI_n - F) T ]^{-1} T^{-1} G + D \\
&= (HT) (T^{-1}) (zI_n - F)^{-1} (T) (T^{-1} G) + D \\
&\quad \uparrow \\
&\quad \text{Recall that: If } A, B, C \text{ are free non singular} \\
&\quad \text{squared matrices then } [ABC]^{-1} = C^{-1} B^{-1} A^{-1} \\
&= H (zI_n - F)^{-1} G + D \\
&= W(z)
\end{aligned}
$$

**(2) Relationship between the reachability matrices of $\Sigma$ and $\bar{\Sigma}$, say $R$ and $\bar{R}$**

$$
\begin{aligned}
\bar{R} &= [\bar{G} | \bar{F}\bar{G} | \dots | \bar{F}^{n-1}\bar{G}] \\
&\cong [T^{-1} G | T^{-1} F G | \dots | T^{-1} F^{n-1} G]
\end{aligned}
$$

*Consider:*
$$
\begin{aligned}
\bar{F}^k \bar{G} &= (T^{-1} F T)^k T^{-1} G \quad (k=1, 2, \dots, n-1) \\
&= \underbrace{(T^{-1} F T) (T^{-1} F T) \dots (T^{-1} F T)}_{k \text{ times}} T^{-1} G \\
&= T^{-1} F^k \underbrace{(T T^{-1})}_{I} G \\
&= T^{-1} F^k G
\end{aligned}
$$

$$
= T^{-1} [G | FG | \dots | F^{n-1} G] = T^{-1} R
$$

$$
\boxed{\bar{R}_{n \times nm}} = \boxed{T^{-1}_{n \times n}} \boxed{R_{n \times nm}}
$$

> [!success] Consequence
> $\text{rank}(R) = \text{rank}(\bar{R})$ AND HENCE $\Sigma$ IS REACHABLE IFF $\bar{\Sigma}$ IS REACHABLE.

## Remark

Suppose that $m=1$ and $\Sigma$ (and $\bar{\Sigma}$) is reachable (i.e. **Single Input Reachable System**). Then:

> [!info] Note on Matrices
> Since $m=1$ and the system is reachable ($n$ states), $R$ and $\bar{R}$ are $n \times n$ matrices and are **Non Singular**.

$$
\implies \boxed{T} \boxed{\bar{R}} = \boxed{R}
$$

$$
\implies \boxed{T} = \boxed{R} \boxed{\bar{R}}^{-1}
$$


## Controllability to Zero of DT SSM

Consider the SSM:

$$
x(t+1) = Fx(t) + Gu(t) \quad t \in \mathbb{Z}_+ \quad (\implies \text{The pair } (F,G) \ F \in \mathbb{R}^{n \times n}, \ G \in \mathbb{R}^{n \times m})
$$
$\dim x = n \quad \dim u = m$

> [!danger] Definition
> Given $k \in \mathbb{Z}, \ k \ge 1$. We say that the state $x_0 \in X = \mathbb{R}^n$ is **Controllable to Zero in $k$ steps** (at time $k$) if $\exists u(0), \dots, u(k-1) \in U$
> ST
> $$x(0) \xrightarrow{u(0), u(1) \dots u(k-1)} x(k) = 0$$

The generic state at time $k$ is:
$$x(k) = x_{\ell}(k) + x_f(k) = F^k x(0) + \underbrace{[R_k]}_{\substack{\text{Reachability} \\ \text{Matrix in } k \text{ steps}}} \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix}$$

$x_0$ is controllable to zero in $k$ steps
$\iff \exists u(0), \dots, u(k-1) \in U$ ST
$$0 = F^k x_0 + R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix}$$

$\iff \exists u(0), \dots, u(k-1) \in U$ ST
$$F^k x_0 = - R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix}$$

$\iff F^k x_0 \in \text{Im}(R_k) = X_k^R$

### To Summarize:

> [!success] Controllability Condition
> $x_0$ is controllable to zero in $k$ steps $\iff F^k x_0 \in \text{Im}(R_k) = X_k^R$

If we denote by $X_k^C$ the set of states that can be controlled to zero in $k$ steps then:
$$X_k^C = \{ x_0 \in X : F^k x_0 \in \text{Im } R_k = X_k^R \}$$


$X_k^C$ is closed w.r.t linear combinations and hence is a vector subspace.

Can I still claim that $X_k^C \subseteq X_{k+1}^C$?

> [!example] Trajectory Diagram
> The graph shows a state trajectory $x(t)$ starting at $x_0$.
> It hits zero at time $k$ ($x(k)=0$).
> By applying input $u=0$ from $k$ to $k+1$, the state remains at zero ($x(k+1)=0$).
>
> **Conclusion:** Any state controllable to zero in $k$ steps is also controllable to zero in $k+1$ steps.

$\implies X_1^C \subseteq \dots \subseteq X_k^C \subseteq X_{k+1}^C \subseteq \dots \subseteq X$

If $X_k^C \subsetneq X_{k+1}^C$ then $\dim X_{k+1}^C \ge \dim(X_k^C) + 1$

Therefore in the above chain there is a finite \# of proper inclusions.

$\implies \exists \bar{k} \in \mathbb{Z}, \ \bar{k} \ge 1 \text{ s.t. } X_k^C = X_{\bar{k}}^C \quad \forall k \ge \bar{k}$

> [!warning] Proposition
> (1) If $X_k^C = X_{k+1}^C$ then $X_{k+1}^C = X_{k+2}^C$
>
> (And therefore $X_{k+1}^C = X_k^C \quad \forall k \ge 0$)
>
> (2) If $\bar{k} \triangleq \min \{ k \in \mathbb{Z}, k \ge 1 : X_k^C = X_{k+1}^C \}$ then $\bar{k} \le n$

## Proof

(1) It is always true that $X_{k+1}^C \subseteq X_{k+2}^C$

We want to prove that if $X_k^C = X_{k+1}^C$, then also $X_{k+2}^C \subseteq X_{k+1}^C$ holds.

Let $x_0 \in X_{k+2}^C$ which means that $\exists \mu(t) = \mu_t \quad t=0, 1, \dots, k+1$

| Time | 0 | 1 | 2 | ... | k+1 | k+2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **State** | $x_0$ | $x_1$ | $x_2$ | ... | $x_{k+1}$ | $\mathbb{O}$ |
| **Input** | $\mu_0$ | $\mu_1$ | $\mu_2$ | ... | $\mu_{k+1}$ | |

* From $x_0$ to $\mathbb{O}$: Goes to zero in $k+2$ steps.
* From $x_1$: $x_1 \in X_{k+1}^C = X_k^C$

*(This proof is concluded below)*

### Controllability Proposition

1.  If $X_k^C = X_{k+1}^C$ then $X_{k+1}^C = X_{k+2}^C$
    $(\implies X_{k+i}^C = X_k^C \quad \forall i \ge 0)$
2.  If $\bar{k} \triangleq \min \{ k \in \mathbb{Z} \ : \ k \ge 1 \ : \ X_k^C = X_{k+1}^C \}$ then $\bar{k} \le n$.

### Proof

1) $X_{k+1}^C \subseteq X_k^C$ always.
If $X_k^C = X_{k+1}^C$ then $X_{k+2}^C \subseteq X_{k+1}^C$ (To be proved).
Let $x_0 \in X_{k+2}^C \implies \exists \mu(t) = \mu_t \quad t=0, 1, \dots, k+1$ ST:

| Time | 0 | 1 | 2 | ... | k+2 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **State** | $x_0$ | $\mathbf{x_1}$ | $x_2$ | ... | $\mathbb{O}$ |
| **Input** | $\mu_0$ | $\mu_1$ | $\mu_2$ | | |

$x_1 \in X_{k+1}^C \iff x_1 \subseteq X_k^C$ and therefore $\exists \mu(t) = \bar{\mu}_t \quad t=0, 1, \dots, k-1$ ST:
$$x(0) = x_1 \xrightarrow{\mu(0)=\bar{\mu}_0, \mu(1)=\bar{\mu}_1, \dots, \mu(k-1)=\bar{\mu}_{k-1}} x(k) = 0$$

The system is Time Invariant and hence $x(1) = x_1$.
$$x_1 \xrightarrow{\mu(1)=\bar{\mu}_0, \mu(2)=\bar{\mu}_1, \dots, \mu(k)=\bar{\mu}_{k-1}} x(k+1) = 0$$

Therefore:

| Time | 0 | 1 | 2 | ... | k+1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **State** | $x_0$ | $x_1$ | $x_2$ | ... | $\mathbb{O}$ |
| **Input** | $\mu_0$ | $\bar{\mu}_0$ | $\bar{\mu}_1$ | | |

$\implies x_0 \in X_{k+1}^C$.

2) Is identical to the one for $X_k^R$. $\square$

## Consequences

$$
X_1^C \subset X_2^C \subset \dots \subset \underbrace{X_{\bar{k}}^C = X_{\bar{k}+1}^C = \dots}_{\equiv X_n^C} \subseteq X = \mathbb{R}^n
$$

Now define $X^C$ as the set of states that can be zero in a finite number of steps, then:

> [!danger] Definition
> $$X^C \equiv X_n^C = \{ x \in X : F^n x \in \text{Im } R_n = \text{Im } R \}$$

We say that the DT System (Equivalent Pair $(F,G)$) is **Controllable to Zero** if all states are controllable to zero in a finite \# of steps, i.e. $X^C = \mathbb{R}^n$.

### To Recap:

$(F,G)$ is **Controllable to Zero**
$\iff X^C = \{ x \in X : F^n x \in \text{Im } R \} = \mathbb{R}^n (= X)$
$\iff \forall x \in X, \ F^n x \in \text{Im } R$
$\iff \text{Im } F^n \subseteq \text{Im } R$

*(Recall: $\{y : y=Ax, \forall x\} \equiv \text{Im } A$)*

### Remark:

**Recall:**
* $(F,G)$ is **Reachable**
    $\iff \text{rank } R = n$
    $\iff \text{Im } R = \mathbb{R}^n$
* $(F,G)$ is **Controllable to Zero**
    $\iff \text{Im } F^n \subseteq \text{Im } R$

> [!success] Relation (1)
> (F,G) is Reachable $\implies \text{Im } R = \mathbb{R}^n$
> $\Downarrow$
> (F,G) is Controllable $\Leftarrow \text{Im } F^n \subseteq \text{Im } R = \mathbb{R}^n$
>
> **In General Reachability implies Controllability.**

### (2) Assume that F is Non Singular

Then $F^n$ is non singular $\implies \text{Im } F^n = \mathbb{R}^n$.

If so:

> [!success] Equivalence
> $(F,G)$ is **Controllable**
> $\updownarrow$ IFF F is Non Singular
> $(F,G)$ is **Reachable**
>
> **Only if $F$ is Non Singular.**

**Proof:**
$\iff \underbrace{\text{Im } F^n}_{\mathbb{R}^n} \subseteq \text{Im } R \subseteq \mathbb{R}^n$
($\mathbb{R}^n$ by assumption)
$\iff \text{Im } R = \mathbb{R}^n$.

### Example: ! Real Useful !

Given DT SSM:
$$
x(t+1) = Fx(t) + gu(t) = \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 1 \\ -1 & 1 & 1 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} u(t)
$$
*(Note: $F$ has a zero row $\implies$ is Singular)*

We want the vector subspaces $X_k^R$ and $X_k^C$ $\forall k \in \mathbb{Z}, \ k \ge 1$.

$$
X_k^R = \{ x \in X : x \in \text{Im } R \} = \text{Im}[G | FG | \dots | F^{k-1}G]
$$
$$
X_k^C = \{ x \in X : F^k x \in \text{Im } R_k \}
$$

#### Reachable Subspace

1.  **$k=1$:**
    $$X_1^R = \text{Im}[g] = \text{Im} \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} = \langle e_2 \rangle$$
    *($g$ cause it's a column vector and **not** a matrix)*

2.  **$k=2$:**
    $$
    X_2^R = \text{Im}[g | Fg] = \text{Im} \begin{bmatrix} 0 & 0 \\ 1 & 0 \\ 0 & 1 \end{bmatrix} = \langle e_2, e_3 \rangle
    $$
    *Note calculation:* $Fg$:
    $$
    \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 1 \\ -1 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}
    $$
    *($\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}$ to cols $\to$ retains only 2nd col)*

3.  **$k=3$:**
    $$
    X_3^R = \text{Im}[g | Fg | F^2g] = \text{Im} \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 1 \end{bmatrix} = \langle e_2, e_3 \rangle
    $$
    *Note calculation:* $F^2g = F(Fg)$:
    $$
    \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 1 \\ -1 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}
    $$
    *Linear dependence:* $\begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix} = e_2 + e_3 \in \langle e_2, e_3 \rangle$.

> [!danger] Warning
> Never try to calculate powers of $F$ ($F^2, F^3 \dots$). Always calculate $F(Fg) \dots$
> **NEVER CALCULATE POWERS!**

**Conclusion for Reachability:**
$$X_2^R = X_k^R = \langle e_2, e_3 \rangle \quad \forall k \ge 2$$
$(F,G)$ is **NOT REACHABLE** (cause needs to coincide with $\mathbb{R}^n$, in this case the generated vectors are in $\mathbb{R}^2$ and $\mathbb{R}^3$).

Since $F$ is singular, we can check if is controllable even though not reachable.

#### Controllability Subspace

**$k=1$:**
$$
X_1^C = \{ x \in \mathbb{R}^3 : Fx \in \text{Im } g \} = \left\{ \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} ; x_1, x_2, x_3 \in \mathbb{R} : \underbrace{\begin{bmatrix} 0 \\ x_1 + x_3 \\ -x_1 + x_2 + x_3 \end{bmatrix}}_{Fx} \in \langle \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} \rangle \right\}
$$
*Constraint:* To be in $\text{span}(e_2) = [0, 1, 0]^T$, the third component must be zero.
$-x_1 + x_2 + x_3 = 0 \implies x_1 = x_2 + x_3$.

$$
= \left\{ \begin{bmatrix} x_2 + x_3 \\ x_2 \\ x_3 \end{bmatrix}, \ x_2 \in \mathbb{R}, \ x_3 \in \mathbb{R} \right\} = \left\{ \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} x_2 + \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix} x_3, \ x_2, x_3 \in \mathbb{R} \right\}
$$
*(Only the rows with $x_2$ / $x_3$)*

$$
= \left\langle \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix} \right\rangle
$$

**$k=2$:**
$$
X_2^C = \{ x \in \mathbb{R}^3 : F^2 x \in \text{Im}[g | Fg] \}
$$
$$
F(Fx) = F^2 x = \begin{bmatrix} 0 & 0 & 0 \\ 1 & 0 & 1 \\ -1 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ x_1+x_3 \\ -x_1+x_2+x_3 \end{bmatrix} = \begin{bmatrix} 0 \\ -x_1+x_2+x_3 \\ x_2+2x_3 \end{bmatrix}
$$
*(Sum of two entries)*

We check if this vector belongs to $\text{Im}[g | Fg] = \langle \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} \rangle = \left\{ \begin{bmatrix} 0 \\ \alpha \\ \beta \end{bmatrix} \right\}$.
It is **ALWAYS TRUE**.

$$
\implies X_2^C = \mathbb{R}^3
$$

$$
X_k^C = \mathbb{R}^3 \quad \forall k \ge 2
$$

$(F,G)$ is **CONTROLLABLE TO ZERO**.

## Review of Inner Prod. and Orthogonality

### Definition

> [!danger] Definition
> Given vect. space $V$ over $\mathbb{R}$ an **Inner Prod.** is a function
> $$< \cdot, \cdot > : V \times V \longrightarrow \mathbb{R}$$
> That satisfies 3 properties:
> 1.  **Symmetry:** $\forall v_1, v_2 \in V \quad <v_1, v_2> = <v_2, v_1>$
> 2.  **Bilinearity:** $\forall v_1, v_2, v \in V \quad \forall \alpha_1, \alpha_2 \in \mathbb{R}$
>     $$<\alpha_1 v_1 + \alpha_2 v_2, v> = \alpha_1 <v_1, v> + \alpha_2 <v_2, v>$$
> 3.  **Positive Definiteness:**
>     $$\forall v \in V \quad <v, v> \ge 0 \quad \text{AND} \quad <v, v> = 0 \iff v = 0$$

## Orthogonality

> [!danger] Definition
> Given 2 vect. $v_1$ and $v_2 \in V$ they are said to be **Orthogonal** if
> $$<v_1, v_2> = 0 \quad (v_1 \perp v_2)$$


> [!danger] Definition
> Let $U$ be a vect. subspace of $V$ then
> $$U^\perp \triangleq \{ v \in V : <v, u> = 0 \quad \forall u \in U \}$$


### Properties

a) $(U^\perp)^\perp \supseteq U$
b) $U \cap U^\perp = \{0\}$
c) If $V$ is a **Finite Dimensional** Vect Space then:
   $(U^\perp)^\perp = U$ and $U \oplus U^\perp = \{ u+w, \ u \in U, \ w \in U^\perp \} = V$
   *(Direct sum since $U \cap U^\perp = \{0\}$)*

## Definition: Adjoint Transformation

Let $V$ and $W$ be two vect spaces over $\mathbb{R}$. Assume that we've defined two Inner Prod., one in $V$, $<\cdot, \cdot>_V$ and one in $W$, $<\cdot, \cdot>_W$.
Let $\mathcal{A}: V \to W$ be a Linear Transformation.
By this meaning a map from $V$ to $W$ for which:
$$\mathcal{A}(\alpha_1 v_1 + \alpha_2 v_2) = \alpha_1 \mathcal{A}(v_1) + \alpha_2 \mathcal{A}(v_2) \quad \forall v_1, v_2 \in V \quad \forall \alpha_1, \alpha_2 \in \mathbb{R}$$

> [!danger] Definition
> A linear transp. $\mathcal{A}^*: W \to V$ is said to be **Adjoint** of the linear transp. $\mathcal{A}$ if:
> $$<\mathcal{A}(v), w>_W = <v, \mathcal{A}^*(w)>_V \quad \forall v \in V, \forall w \in W$$

> [!info] Remark
> $\mathcal{A}^*$ doesn't necessarily exists but if it exists, it's **unique**.

### Case 1) Finite Dimensional Space

Assume $V = \mathbb{R}^k$ and $W = \mathbb{R}^p$.
And assume in $V$ and $W$ the **Standard Linear Product** i.e.
$$<v_1, v_2>_V \triangleq v_1^T v_2 \quad \forall v_1, v_2 \in V$$
$$<w_1, w_2>_W \triangleq w_1^T w_2 \quad \forall w_1, w_2 \in W$$

Let $\mathcal{A}: V \to W$ be a linear transformation.
If we assume that we have set a basis in $V$ and a basis in $W$, then $\mathcal{A}(\cdot)$ is represented by a matrix $A \in \mathbb{R}^{p \times k}$.
$$
\begin{aligned}
\mathcal{A}: V &\to W \\
v &\to Av
\end{aligned}
$$
We want to show that $\mathcal{A}^*$ is represented by $A^T$, i.e.
$$
\begin{aligned}
\mathcal{A}^*: W &\to V \quad (\dim V = k) \\
w &\to A^T w
\end{aligned}
$$

**Indeed for every $v \in V, w \in W$:**
$$
\begin{aligned}
<\mathcal{A}v, w>_W &= <v, \mathcal{A}^*(w)>_V \\
[Av]^T w &= v^T [\mathcal{A}^*(w)] \\
v^T [A^T w] &= v^T [\mathcal{A}^*(w)]
\end{aligned}
$$
$$\implies \mathcal{A}^*(w) = A^T w$$

## Main Prop of Adjoint Transformations


(P1) $\text{Ker } \mathcal{A} = (\text{Im } \mathcal{A}^*)^\perp$

(P2) $\text{Ker } \mathcal{A} = \text{Ker}[\mathcal{A}^* \mathcal{A}] = \text{Ker}[\mathcal{A}^*(\mathcal{A})]$
$$V \xrightarrow{\mathcal{A}} W \xrightarrow{\mathcal{A}^*} V$$

(P3) $\text{Im } \mathcal{A} \subseteq (\text{Ker } \mathcal{A}^*)^\perp$

(P4) $\text{Im } \mathcal{A} \supseteq \text{Im}(\mathcal{A} \mathcal{A}^*)$

> [!info] Note
> If $\text{Im } \mathcal{A}$ is **Finite Dimensional** then they are two **Equalities** (referring to P3 and P4).

### Case 2) Function Spaces

Let $V = \mathcal{U}_{[0,t]}$ = The set of piece-wise continuous functions defined on $[0,t]$ and taking values in $U = \mathbb{R}^m$ (It is a real vect space).
$W = X = \mathbb{R}^n$

**Assume as Inner Prod:**
$$<\mu(\cdot), \mu_2(\cdot)>_{\mathcal{U}_{[0,t]}} = \int_0^t \mu_1^T(\tau) \mu_2(\tau) d\tau$$
$$<x_1, x_2>_X \triangleq x_1^T x_2$$

**Consider the Linear Transf:**
$$
\begin{aligned}
\mathcal{A}: \mathcal{U}_{[0,t]} &\longrightarrow X \\
\mu(\tau), \tau \in [0,t] &\longmapsto \int_0^t M(\tau) \mu(\tau) d\tau
\end{aligned}
$$
Where $M(\tau), \tau \in [0,t]$ is a matrix valued function $M(\tau) \in \mathbb{R}^{n \times m} \ \forall \tau$.

**We want to identify $\mathcal{A}^*$:**
$$\mathcal{A}^*: X \longrightarrow \mathcal{U}_{[0,t]}$$

That must satisfy $\forall \mu(\cdot) \in \mathcal{U}_{[0,t]}$ and $x \in X$:
$$<\mathcal{A}(\mu(\cdot)), x>_X = <\mu(\cdot), \mathcal{A}^*(x)>_{\mathcal{U}_{[0,t]}}$$

$$
\begin{aligned}
\left< \left[ \int_0^t M(\tau) \mu(\tau) d\tau \right], x \right>_X &= \int_0^t \mu^T(\tau) [\mathcal{A}^*(x)](\tau) d\tau \\
\left[ \int_0^t M(\tau) \mu(\tau) d\tau \right]^T x &= \int_0^t \mu^T(\tau) M^T(\tau) d\tau
\end{aligned}
$$

*(Comparing the two sides, the terms in the integral must be equal)*

> [!success] Result
> $\implies \mathcal{A}^*: x \in X \longrightarrow M^T(\tau)x, \ \tau \in [0,t]$

We can introduce (Case 2) the Inner Products:
$$<u_1(\cdot), u_2(\cdot)>_{\mathcal{U}_{[0,t]}} \triangleq \int_0^t \mu_1^T(\tau) \mu_2(\tau) d\tau \quad \forall \mu_1, \mu_2 \in \mathcal{U}_{[0,t]}$$
$$<x_1, x_2> \triangleq x_1^T x_2 \quad \forall x_1, x_2 \in X$$

By referring to Case 2 we can claim that the **Adjoint Transf. $\mathcal{R}_t^*$ exists**:
$$
\begin{aligned}
\mathcal{R}_t^*: X &\longrightarrow \mathcal{U}_{[0,t]} \\
x &\longrightarrow G^T e^{F^T(t-\tau)} x \quad \tau \in [0,t]
\end{aligned}
$$

In Case 2 $\mathcal{A}^*: x \to M^T(\tau)x, \ \tau \in [0,t]$.

By exploiting the fact that $\text{Im } \mathcal{R}_t$ is a finite dimensional vector space and by making use of the prop. of the adjoint transf., we can claim that $\text{Im } \mathcal{R}_t = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*)$.

**We wonder what is $\mathcal{R}_t \mathcal{R}_t^*$?**

[Diagram of Mapping]
$X \xrightarrow{\mathcal{R}_t^*} \mathcal{U}_{[0,t]} \xrightarrow{\mathcal{R}_t} X$
$x \longmapsto \underbrace{G^T e^{F^T(t-\tau)}}_{\tau \in [0,t]} x \longmapsto \underbrace{\left[ \int_0^t e^{F(t-\tau)} G G^T e^{F^T(t-\tau)} d\tau \right]}_{\substack{\text{It's a Matrix} \\ \triangleq W_t \in \mathbb{R}^{n \times n} \text{ Called} \\ \text{REACHABILITY GRAMIAN} \\ \text{AT TIME } t}} x$

**Therefore $\forall t > 0$:**
$$X_t^R = \text{Im } \mathcal{R}_t = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*) = \text{Im}(W_t)$$

## Reachability of CT SSM

$\Sigma: \dot{x}(t) = Fx(t) + Gu(t) \ t \in \mathbb{R}_+ \quad \dim x = n \ \dim u = m$

> [!danger] Def
> Given some time $t>0$, one state $x_f \in X = \mathbb{R}^n$ is reachable at time $t$ if $\exists u(\cdot) \in \mathcal{U}_{[0,t]}$ that drags the state of the system from $x(0)=0$ to $x(t)=x_f$.
>
> *($\mathcal{U}_{[0,t]} \triangleq$ is the set of piece-wise continuous function defined on $[0,t]$ and taking values in $U=\mathbb{R}^m$)*

(For short $x(0)=0 \xrightarrow{u(\cdot)} x(t)=x_f$)

**From:**
$$x(t) = x_f(t) = \int_0^t e^{F(t-\tau)} Gu(\tau) d\tau$$

**We deduce that:**
$x_f$ is reachable at time $t$
$\iff \exists u(\cdot) \in \mathcal{U}_{[0,t]}$ ST
$x_f = \int_0^t e^{F(t-\tau)} Gu(\tau) d\tau$

$$
\begin{aligned}
\mathcal{R}_t: \mathcal{U}_{[0,t]} &\longrightarrow X = \mathbb{R}^n \\
u(\tau), \tau \in [0,t] &\longrightarrow \int_0^t e^{F(t-\tau)} Gu(\tau) d\tau
\end{aligned}
$$

$\iff \exists u(\cdot) \in \mathcal{U}_{[0,t]}$ ST $x_f = \mathcal{R}_t u(\cdot)$
$\iff x_f \in \text{Im } \mathcal{R}_t$

If is Reachability $X_t^R$ the set of states that are reachable at time $t$, then $X_t^R \equiv \text{Im } \mathcal{R}_t$.

We observe $\mathcal{U}_{[0,t]}$ and $X$ are real vector space and that
$$\mathcal{R}_t(\alpha_1 u_1(\cdot) + \alpha_2 u_2(\cdot)) = \alpha_1 \mathcal{R}_t(u_1(\cdot)) + \alpha_2 \mathcal{R}_t(u_2(\cdot))$$

$\implies \mathcal{R}_t$ is a linear transformation.
$\implies \text{Im } \mathcal{R}_t$ is a vector subspace of $X = \mathbb{R}^n$ and it's a finite-dimension vector space.

> [!warning] Proposition
> For every $t>0 \quad X_t^R = \text{Im } \mathcal{R}_t = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*) = \text{Im}(W_t) = \text{Im } R$
> Where $R = [G | FG | \dots | F^{n-1}G]$ is the Reachability Matrix.

### Proof

We want to prove $\forall t>0 \ \text{Im } \mathcal{R}_t = \text{Im } R$.
Since both $\text{Im } \mathcal{R}_t$ and $\text{Im } R$ are finite dim. vector subspaces of $\mathbb{R}^n$ is equivalent to proving $(\text{Im } \mathcal{R}_t)^\perp = (\text{Im } R)^\perp$.

**Recall:**
$\text{Ker } \mathcal{A} = (\text{Im } \mathcal{A}^*)^\perp$ and clearly the result is true.
Also if we swap $\mathcal{A}$ and $\mathcal{A}^*$ ie $\text{Ker } \mathcal{A}^* = (\text{Im } \mathcal{A})^\perp$.

**Which is equivalent to proving $\text{Ker } \mathcal{R}_t^* = \text{Ker } R^T$**

$$
\begin{aligned}
x \in \text{Ker } \mathcal{R}_t^* &\iff \mathcal{R}_t^* x = 0_{\mathcal{U}_{[0,t]}} \\
&\iff G^T e^{F^T(t-\tau)} x = 0 \quad \forall \tau \in [0,t] \\
&\iff G^T \sum_{k=0}^\infty (F^T)^k \frac{(t-\tau)^k}{k!} x = 0 \quad \forall \tau \in [0,t] \\
&\iff \sum_{k=0}^\infty [G^T (F^T)^k x] \frac{(t-\tau)^k}{k!} = 0 \quad \forall \tau \in [0,t]
\end{aligned}
$$

> [!info] Principle of Identity of Power Series
> If this is the case the express. must be the zero function and it has a unique series expansion (All its coeff. must be zero).

$\iff G^T (F^T)^k x = 0 \quad \forall k \in \mathbb{Z}_+$
*(Cayley Hamilton)*
$\iff G^T (F^T)^k x = 0 \quad k=0, 1, \dots, n-1$

$\implies$ Obvious: Follow Cayley-Hamilton Theorem.

$$
\iff \begin{bmatrix} G^T \\ G^T F \\ \vdots \\ G^T (F^T)^{n-1} \end{bmatrix} x = \begin{bmatrix} 0 \\ \vdots \\ 0 \end{bmatrix}
$$
$\equiv R^T$

$\iff x \in \text{Ker } R^T \quad \square$

> [!success] Consequence
> If we denote by $X^R$ the set of states that can be reached (by the CT system) in finite time, then:
> $$X^R = X_t^R = \text{Im } R \quad \forall t>0$$
> *It's the Smallest F-Invariant Space including Im G*

We say that the CT System is **Reachable** if $X^R = \mathbb{R}^n$.
Therefore $(F,G)$ is Reachable $\iff \text{rank } R = n$.

## Controllability To Zero of CT SSM

$\Sigma: \dot{x}(t) = Fx(t) + Gu(t) \quad t \in \mathbb{R}_+ \quad \dim x = n \quad \dim u = m$

Given some time $t > 0$ a state $x_0 \in X$ is said to be **Controllable to 0** if $\exists u(\cdot) \in \mathcal{U}_{[0,t]}$ such that $x(0)=x_0 \xrightarrow{u(\cdot)} x(t)=0$.

**Recall that:**
$$x(t) = x_e(t) + x_f(t) = e^{Ft} x_0 + \mathcal{R}_t u(\cdot)$$

**Therefore:**
$x_0$ is controllable to zero at $t > 0$
$\iff \exists u(\cdot) \in \mathcal{U}_{[0,t]}$ ST $0 = e^{Ft} x_0 + \mathcal{R}_t u(\cdot) \iff \exists u(\cdot) \in \mathcal{U}_{[0,t]}$ ST $e^{Ft} x_0 = - \mathcal{R}_t u(\cdot)$
$\iff e^{Ft} x_0 \in \text{Im } \mathcal{R}_t$

If we introduce the set $X_t^C$ of the state in $X$ that are controllable to $0$ at time $t > 0$, then:

> [!success] Controllability Set Definition
> $$X_t^C = \{ x \in X : e^{Ft} x \in \text{Im } \mathcal{R}_t = X^R = \text{Im } R \}$$

### Proof

We want to prove that $\forall t > 0: \ X_t^C = X^C = \text{Im } R$.

(1) $x \in X_t^C \iff e^{Ft} x \in X^R$
    $\iff x \in e^{-Ft} X^R$

**Therefore:** $X_t^C = e^{-Ft} X^R$

(2) $X^R$ is $F$-invariant $\implies F X^R \subseteq X^R$
    $F^2 X^R \subseteq X^R$
    $\vdots$
    $F^k X^R \subseteq X^R$

$\implies \underbrace{\left[ \sum_{k=0}^\infty F^k \frac{(-t)^k}{k!} \right]}_{\equiv e^{-Ft} X^R} X^R \subseteq X^R$

So I proved that $e^{-Ft} X^R \subseteq X^R$ ($\subseteq$).
Suppose that $\dim X^R = r$.
$e^{-Ft}$ is **Non-Singular**.
Since $e^{-Ft} X^R$ is included in $X^R$ and have same dimension they coincide.

> [!success] Result (3)
> $$X_t^C = e^{-Ft} X^R = X^R$$
> *The exp. keeps track of the time so we can "Go Back" in time (Only in Time CT)*

## Point to Point Control of a DT SSM

**Assume:**
$\Sigma: x(t+1) = Fx(t) + Gu(t) \quad t \in \mathbb{Z}_+ \ \dim x = n \ \dim u = m$

**Problem:**
Given some time $k \in \mathbb{Z}, \ k > 0$ and two states $x_0, x_f \in X$, determine, if possible an input sequence, $u(0), u(1), \dots, u(k-1) \in U$ that leads the state from $x(0)=x_0$ to $x(k)=x_f$.

**Since:**
$$x(k) = x_\ell(k) + x_f(k) = F^k x(0) + R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix}$$

**The problem is solvable IFF:**
(1) $\exists u(0), \dots, u(k-1) \in U$ ST $x_f = F^k x_0 + R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix}$

$\iff x_f - F^k x_0 = R_k \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix} \quad \exists u(0) \dots u(k-1) \in U$

> [!success] Solvability Condition
> $$\iff x_f - F^k x_0 \in \text{Im } R_k$$

If we know that the solvability condition is satisfied then, (1) has a solution.
We remark that (remember adjoint transf. and the fact that we are working with finite dim. vect. spaces) the
$\text{Im } R_k = \text{Im}(R_k R_k^T)$
($\text{Im } \mathcal{A} = \text{Im}(\mathcal{A} \mathcal{A}^*)^\perp = \dots$)

**Therefore, we will solve:**
(2)
> [!warning] Equation to Solve
> $$x_f - F^k x_0 = R_k R_k^T v_k$$
> *Where $v_k$ is Unknown*

$\implies \begin{bmatrix} u(k-1) \\ \vdots \\ u(0) \end{bmatrix} = R_k^T v_k$

* **Case 2:**
If $\text{rank } R_k < n$
Then $R_k R_k^T$ is singular and hence that exists an infinite \# of solutions of (2).

We want to prove that if $v_k$ and $\bar{v}_k$ are two distinct solutions of (2); yet they lead to the same solution of (1), meaning that:
$$R_k^T v_k = R_k^T \bar{v}_k$$

**Proof:**
If $v_k$ and $\bar{v}_k$ are solutions of (2)
$\implies R_k R_k^T v_k = x_f - F^k x_0 = R_k R_k^T \bar{v}_k$

$\implies R_k R_k^T [v_k - \bar{v}_k] = 0$

$\implies v_k = \bar{v}_k - a_k$ with $a_k \in \text{Ker}[R_k R_k^T]$
*(Recall $\text{Ker } A = \text{Ker}[A^T A]$, here $\text{Ker } R_k^T = \text{Ker}[R_k R_k^T]$)*

**Therefore:**
$$R_k^T v_k = R_k^T [\bar{v}_k + a_k] = R_k^T \bar{v}_k + \cancel{R_k^T a_k}$$

So, independently of whatever we are in Case 1 or 2, the solution we obtain by first determining a solution $v_k$ of (2) and then setting $\mathcal{U}_k = R_k^T v_k$ is always **UNIQUE** and it will be denoted by $\mathcal{U}_k^*$.

### Point to Point Control - Case Analysis

If the problem is solvable then the eq. we should solve is:
(1) $$x_f - F^k x_0 = \underbrace{R_k \begin{bmatrix} \mu(k-1) \\ \vdots \\ \mu(0) \end{bmatrix}}_{\triangleq \mathcal{U}_k} \iff \text{Im } \underbrace{R_k}_{\mathcal{A}_k} = \text{Im}[\underbrace{R_k R_k^T}_{\mathcal{A} \mathcal{A}^*}]$$

(2) $$x_f - F^k x_0 = R_k R_k^T v_k \quad \mathcal{U}_k = R_k^T v_k$$

So we solve (2) and from (one of) its solution(s) $v_k$, we can deduce a solution of (1) in the form $\mathcal{U}_k = R_k^T v_k$.

* **Case 1:**
    If $\text{rank } R_k = n$ ($\iff (F,G)$ is Reachable AND $k \ge \bar{k} = r$ Reachability Index)

    Then $R_k R_k^T$ has rank $n$, in turn, which means that it is non singular and therefore:

> [!success] Unique Solution Formula
> $$\implies v_k = [R_k R_k^T]^{-1} [x_f - F^k x_0]$$
> *In this case unique solution*

### Why is $\mathcal{U}_k^*$ so special?

Let $\mathcal{U}_k^* = R_k^T v_k$ and let $\mathcal{U}_k$ be any other solutions of (1).
This means:
$$R_k \mathcal{U}_k = x_f - F^k x_0 = R_k \mathcal{U}_k^*$$

$\implies R_k [\mathcal{U}_k - \mathcal{U}_k^*] = 0$

$\implies \mathcal{U}_k = \mathcal{U}_k^* + \mathcal{V}_k \quad \text{with } \mathcal{V}_k \in \text{Ker } R_k$

**Geometry:**
$\mathcal{U}_k^* \in \text{Im } R_k^T$
$\mathcal{V}_k \in \text{Ker } R_k$
$\text{Im } \mathcal{A}^* = (\text{Ker } \mathcal{A})^\perp$
$\implies \mathcal{U}^* \perp \mathcal{V}$

**Therefore:**
$$\|\mathcal{U}_k\|^2 = \|\mathcal{U}_k^* + \mathcal{V}_k\|^2 = \|\mathcal{U}_k^*\|^2 + \|\mathcal{V}_k\|^2$$

> [!success] Minimum Norm
> $\implies \|\mathcal{U}_k\|^2 \ge \|\mathcal{U}_k^*\|^2 \implies \|\mathcal{U}_k\| \ge \|\mathcal{U}_k^*\|$
> **! MINIMAL NORM SOLUTION !**

### Exercise 1:

Consider the DT SSM:
$$x(t+1) = F x(t) + g u(t) = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 3 & 0 & 0 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} u(t)$$

We want to stear, if possible, the state of the system from $x_0 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$ at $t=0$ and $x_f = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix}$ at $t=4=k$.

If so, find the **Minimum Norm Solution**.

**Sol:**
Problem solvable IFF $x_f - F^k x_0 \in \text{Im } R_4$.

$$
R_4 = [g | Fg | F^2g | F^3g]
$$
$=F(Fg)$
$$
= \begin{bmatrix} 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 3 \end{bmatrix}
$$
It's all $\mathbb{R}^3$ since we have 3 indep. cols.

Since $\text{rank } R_4 = 3$ the problem it's solvable, moreover, we are in **Case (1)**.

**We have to solve:** $F^4 x_0$

$$
x_0 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \quad F x_0 = \begin{bmatrix} 0 \\ 0 \\ 3 \end{bmatrix} \quad F^2 x_0 = \begin{bmatrix} 0 \\ 3 \\ 0 \end{bmatrix} \quad F^3 x_0 = \begin{bmatrix} 3 \\ 0 \\ 0 \end{bmatrix} \quad F^4 x_0 = \begin{bmatrix} 0 \\ 0 \\ 9 \end{bmatrix}
$$

$$x_f - F^4 x_0 = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} - \begin{bmatrix} 0 \\ 0 \\ 9 \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ -9 \end{bmatrix}$$

**Now we calculate:**

$$
R_4 R_4^T = \begin{bmatrix} 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 3 \end{bmatrix} \begin{bmatrix} 0 & 0 & 1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 3 \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 10 \end{bmatrix}
$$

$$
v_4 = (R_4 R_4^T)^{-1} (x_f - F^4 x_0) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 0.1 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \\ -9 \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ -0.9 \end{bmatrix}
$$

**Minimum Norm Solution:**

$$
\mathcal{U}_4^* = R_4^T v_4 = \begin{bmatrix} 0 & 0 & 1 \\ 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 3 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \\ -0.9 \end{bmatrix} = \begin{bmatrix} -0.9 \\ 1 \\ 1 \\ -2.7 \end{bmatrix} = \begin{bmatrix} \mu(3) \\ \mu(2) \\ \mu(1) \\ \mu(0) \end{bmatrix}
$$

**If we are only interested in ONE solution $\mathcal{U}_4$ (not necessary of minimum norm) we just solve directly Eq. (1):**

$$
\begin{bmatrix} 1 \\ 1 \\ -9 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 3 \end{bmatrix} \begin{bmatrix} \mu(3) \\ \mu(2) \\ \mu(1) \\ \mu(0) \end{bmatrix}
$$
*(Eq. 1 is $\uparrow x_f - F^4 x_0$)*

$$
\begin{aligned}
\mu(1) &= 1 \\
\mu(2) &= 1 \\
\mu(3) + 3\mu(0) &= -9 \quad \text{eg. } \mu(0) = -3, \ \mu(3) = 0
\end{aligned}
$$

> [!info] Summary
> * If I need **A** solution I can go with (1).
> * If I need **THE MIN. SOL.** I need to pass through Eq. 2.

### Point to Point Control of CT SSM

**Given:**
$\Sigma: \dot{x}(t+1) = Fx(t) + Gu(t) \quad t \in \mathbb{R}_+ \quad \dim x = n \ \dim u = m$

**Problem:**
Given a time $t>0$, $x_0, x_f \in X = \mathbb{R}^n$ (two states).
Determine, if possible, input $\mu(\cdot) \in \mathcal{U}_{[0,t]}$ that stears the state from $x(0)=x_0$ to $x(t)=x_f$.

**From:**
$$x(t) = x_\ell(t) + x_f(t) = e^{Ft} x(0) + \mathcal{R}_t \mu(\cdot)$$

**We deduce that our problem is solvable IFF:**
$\exists \mu(\cdot) \in \mathcal{U}_{[0,t]}$ ST $x_f = e^{Ft} x_0 + \mathcal{F}_t \mu(\cdot)$

$$
\iff \exists \mu(\cdot) \in \mathcal{U}_{[0,t]} \text{ ST } \underbrace{x_f - e^{Ft} x_0 = \mathcal{F}_t \mu(\cdot)}_{\int_0^t e^{F(t-\tau)} G \mu(\tau) d\tau} \quad (1)
$$

> [!success] Solvability Condition
> $$x_f - e^{Ft} x_0 \in \text{Im } \mathcal{R}_t = \text{Im } R$$

If we assume the prob. solvable we need to solve Eq. (1).
By exploiting the fact that when $\text{Im } \mathcal{R}_t$ is finite dimensional than it coincide with
$$\text{Im } \mathcal{R}_t = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*) = \text{Im } W_t$$
*(Reachability Gramian Matrices)*

We can claim that Eq. (1) is solvable IFF the following Eq. is solvable:

> [!warning] Gramian Equation
> $$x_f - e^{Ft} x_0 = \mathcal{R}_t \mathcal{R}_t^* v_t = W_t v_t \quad (2)$$

If $v_t$ solves (2) then $\mathcal{R}_t^* v_k = \mu^*(\cdot)$ solves (1).

* **Case 1:**
$\text{Im } \mathcal{R}_t = \text{Im } W_t = \text{Im } R = \mathbb{R}^n$.

Then $W_t \in \mathbb{R}^{n \times n}$ is non singular and hence the solution of (2) is uniquely determined as $v_t = W_t^{-1} [x_f - e^{Ft} x_0]$.

$\implies \mu^*(\cdot) = \mathcal{R}_t^* v_t$ is uniquely determined.

* **Case 2:**
$\text{Im } \mathcal{R}_t = \text{Im}(\mathcal{R}_t \mathcal{R}_t^*) = \text{Im } W_t = \text{Im } R \subsetneq \mathbb{R}^n$.

$\implies$ If $v_t$ and $\bar{v}_t$ are two solutions of (2) then:
$$W_t v_t = \mathcal{R}_t \mathcal{R}_t^* v_t = W_t \bar{v}_t = \mathcal{R}_t \mathcal{R}_t^* \bar{v}_t$$

$\implies v_t = \bar{v}_t + a_t$ where $a_t \in \text{Ker } W_t = \text{Ker}(\mathcal{R}_t \mathcal{R}_t^*) \equiv \text{Ker } \mathcal{R}_t^*$.

**Therefore:**
$$\mathcal{R}_t^* v_t = \mathcal{R}_t^* [\bar{v}_t + a_t] = \mathcal{R}_t^* \bar{v}_t + \cancel{\mathcal{R}_t^* a_t}$$

> [!success] Unique Solution
> Therefore also in this case $\mu^*(\cdot) = \mathcal{R}_t^* v_t$ is uniquely determined even if there are infinite values of $v_t$ that solves (2).

We want to conclude proving that $\mu^*(\cdot) = \mathcal{R}_t^* v_t$ is the **Minimum Norm Solution** of Eq. (1).

Let $\mu(\cdot)$ be any solution of (1), then
$$\mathcal{R}_t \mu(\cdot) = x_f - e^{Ft} x_0 = \mathcal{F}_t \mu^*(\cdot)$$
$\implies \mu(\cdot) = \mu^*(\cdot) + \tilde{\mu}(\cdot) \quad \text{with } \tilde{\mu}(\cdot) \in \text{Ker } \mathcal{R}_t$.

**Therefore:**
$$
\|\mu(\cdot)\|^2 = \| \mu^*(\cdot) + \tilde{\mu}(\cdot) \|^2 = \| \mu(\cdot) \|^2 + \| \tilde{\mu}(\cdot) \|^2
$$
*Note:* $\mu^*(\cdot) \in \text{Im } \mathcal{R}_t^* = (\text{Ker } \mathcal{R}_t)^\perp$ and $\tilde{\mu}(\cdot) \in \text{Ker } \mathcal{R}_t$.

$\implies \|\mu(\cdot)\| \ge \|\mu^*(\cdot)\|$.

# Reachability & Controllability: DT vs CT

| Discrete Time (DT)                                                                                                                                                                                                                        | Continuous Time (CT)                                                                                                                                                                                                                                                                                                                             |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reachability**<br><br>**Definition:** Reachable if $\exists u$ driving $x(0)=0$ to $x(k)=x_f$.<br><br>**Condition:**<br>$\text{rank } R_k = n$ (for $k \ge n$).<br>$R_k = [G                                                            | $[FG \| \dots \|F^{k-1}G]$<br><br>**Gramian:**<br>$W_k = R_k R_k^T$.<br>**Reachability**<br><br>**Definition:** Reachable if $\exists u$ driving $x(0)=0$ to $x(t)=x_f$.<br><br>**Condition:**<br>$\text{rank } R = n$.<br>$R = [G\|FG\| \dots \| F^{n-1}G]$.<br><br>**Gramian:**<br>$W_t = \int_0^t e^{F(t-\tau)} G G^T e^{F^T(t-\tau)} d\tau$. |
| **Point-to-Point Control**<br><br>**Problem:** $x_0 \to x_f$ in time $k$.<br>**Solvability:** $x_f - F^k x_0 \in \text{Im } R_k$.<br>**Min Norm Solution:**<br>$\mathcal{U}_k^* = R_k^T (R_k R_k^T)^{-1} (x_f - F^k x_0)$ (if reachable). | **Point-to-Point Control**<br><br>**Problem:** $x_0 \to x_f$ in time $t$.<br>**Solvability:** $x_f - e^{Ft} x_0 \in \text{Im } R$.<br>**Min Norm Solution:**<br>$\mu^*(\cdot) = \mathcal{R}_t^* W_t^{-1} (x_f - e^{Ft} x_0)$ (if reachable).                                                                                                     |
| **Controllability to Zero**<br><br>**Set:** $X_k^C = \{ x : F^k x \in \text{Im } R_k \}$.<br>If $F$ is singular, $X_k^C$ can be larger than $X^R$.                                                                                        | **Controllability to Zero**<br><br>**Set:** $X_t^C = e^{-Ft} X^R = X^R$.<br>In CT, the set of states controllable to zero coincides with the reachable subspace.                                                                                                                                                                                 |

### A look into the future:

* **Standard Reachability Form**
    $T \in \mathbb{R}^{n \times n}$ non singular.
    $(\hat{F}, \hat{G})$, $\hat{F} \in \mathbb{R}^{n \times n}, \hat{G} \in \mathbb{R}^{n \times m}$ is non reachable pair (Representing either CT or DT system).

* Based on the fact that
    $$X^R = \text{Im}[G | FG | \dots | F^{n-1}G] = \text{Im } R$$
    is the (smallest) $F$-invariant subspace $X=\mathbb{R}^n$ including $\text{Im } G$.

### Exe 2:

**Given the DT SSM:**
$$x(t+1) = F x(t) + g \mu(t) = \begin{bmatrix} 0 & 0 \\ 2 & 1 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 1 \end{bmatrix} \mu(t)$$

Determine, if possible, $k \in \mathbb{Z}, k \ge 1$ and $\mu(0), \mu(1), \dots, \mu(k-1) \in U = \mathbb{R}$ that leads from $x(0)=x_0=\begin{bmatrix} 0 \\ 1 \end{bmatrix}$ to $x(k)=x_f=\begin{bmatrix} 0 \\ 16 \end{bmatrix}$.

**Sol:**
Prob. solv. IFF $x_f - F^k x_0 \in \text{Im } R_k \quad (k \text{ is free})$.

$F^k = \begin{bmatrix} 0 & 0 \\ 2 & 1 \end{bmatrix}^k = \begin{bmatrix} 0 & 0 \\ 2^k & 1 \end{bmatrix} \quad k \ge 1$

$\implies F^k x_0 = \begin{bmatrix} 0 \\ 2^k \\ 1 \end{bmatrix} \implies x_f - F^k x_0 = \begin{bmatrix} 0 \\ 16 \\ 0 \end{bmatrix} - \begin{bmatrix} 0 \\ 2^k \\ 1 \end{bmatrix} = \begin{bmatrix} 0 \\ 16-2^k \\ -1 \end{bmatrix}$ *(Wait, dimensions mismatch in vector calc in image?)*.
*Re-reading image calculation:*
$x_f = \begin{bmatrix} 0 \\ 16 \\ 0 \end{bmatrix}$ (from text, but vector looks like 2D? $F$ is $2 \times 2$).
Let's check $x_0$: $x_0 = [0, 1]^T$. $x_f = [0, 16]^T$.
Wait, image shows 3rd component?
Ah, the matrix is:
$x(t+1) = \begin{bmatrix} 0 & 0 \\ 2 & 1 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 1 \end{bmatrix} u(t)$.
This is $2 \times 2$.
The vector calculation in image: $x_f - F^k x_0 = \begin{bmatrix} 0 \\ 16 \end{bmatrix} - \begin{bmatrix} 0 \\ 2^k + 1 \end{bmatrix}$? No.
$F^k x_0 = \begin{bmatrix} 0 & 0 \\ 2^k & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$.
Image writes: $F^k x_0 = \begin{bmatrix} 0 \\ 2^k \\ 1 \end{bmatrix}$ (Seems to be a mistake in writing or interpreting dimension).
Let's look at $R_k$.
$R_k = [g | Fg | \dots | F^{k-1}g] = \left[ \begin{bmatrix} 0 \\ 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} \dots \begin{bmatrix} 0 \\ 1 \end{bmatrix} \right]$.
Always same outcome.

**System Not Reachable.**
$X_k^R = \langle \begin{bmatrix} 0 \\ 1 \end{bmatrix} \rangle = X^R \quad \forall k$.

[Diagram showing reachability subspace along y-axis]

**Only for $k=4$:**
$x_f - F^k x_c = \begin{bmatrix} 0 \\ -1 \end{bmatrix} \in \text{Im } R_k = \text{Im } R = \langle \begin{bmatrix} 0 \\ 1 \end{bmatrix} \rangle$.

$\begin{bmatrix} 0 \\ 0 \\ -1 \end{bmatrix}$? No, just $\begin{bmatrix} 0 \\ -1 \end{bmatrix}$.

$\begin{bmatrix} 0 \\ 0 \\ -1 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 1 & 1 & 1 & 1 \end{bmatrix} \begin{bmatrix} \mu(3) \\ \mu(2) \\ \mu(1) \\ \mu(0) \end{bmatrix}$

**For instance:** $\mu(0) = -1, \quad \mu(1)=\mu(2)=\mu(3)=0$.

### Standard Reachability Form

A form to which we can reduce every non reachable either CT or DT SSM by change of basis in $X$.
The main result this form relies upon the fact that $X^R = \text{Im } R$ (Reachable Subspace) is $F$-invariant and includes the $\text{Im } G$.

**Consider:**
$$
\Sigma : \begin{cases}
x(t+1) = Fx(t) + Gu(t) & t \in \mathbb{Z}_+ \\
y(t) = Hx(t) + Du(t)
\end{cases} \quad \dim x = n; \ \dim u = m; \ \dim y = p
$$

And that $\Sigma = (F, G, H, D)$ is the basis $B_x, B_u, B_y$ in $X=\mathbb{R}^n, U=\mathbb{R}^m, Y=\mathbb{R}^p$.

We assume that the system $\Sigma(F, G)$ is **NOT REACHABLE** and we have:
$$\rho = \dim(X^R) = \dim(\text{Im}(R)) = \text{rank}(R) < n$$

We want to construct $T \in \mathbb{R}^{n \times n}$ and non singular that represent a change of basis in $X$ so that wrt $\bar{B}_x$ new basis, the system $\bar{\Sigma} = (\bar{F}, \bar{G}, \bar{H}, \bar{D}) = (T^{-1}FT, T^{-1}G, HT, D)$ is in **STD REACHABILITY FORM**.

We start by selecting $\rho$ independent cols of $R$, $[v_1, \dots, v_\rho] \in \mathbb{R}^{n \times \rho}$ and we can complete this to a basis of $X = \mathbb{R}^n$.
We can always find additional $n-\rho$ vectors in $\mathbb{R}^n$, $w_{\rho+1}, \dots, w_n$ ST $v_1, \dots, v_\rho, w_{\rho+1}, \dots, w_n$ is a basis of $X = \mathbb{R}^n$ and hence:


$$T = [v_1 | \dots | v_\rho || w_{\rho+1} | \dots | w_n] \in \mathbb{R}^{n \times n} \text{ is non singular}$$

We want to understand how do $\bar{F}, \bar{G}$ change wrt to the basis through $T$ [where $\bar{F} = T^{-1}FT$ and $\bar{G} = T^{-1}G$].

From the fact that $\bar{F} = T^{-1}FT$ we deduce that $T\bar{F} = FT$ namely:
$$[Fv_1 | \dots | Fv_\rho | Fw_{\rho+1} | \dots | Fw_n] = FT = T\bar{F} = [v_1 | \dots | v_\rho | w_{\rho+1} | \dots | w_n] \bar{F}$$
*(We want to deduce this)*

Since $X^R = \text{Im } R = <v_1, \dots, v_\rho>$ is $F$-invariant, then:
$$Fv_i \in X^R = <v_1, \dots, v_\rho> \implies Fv_i = \sum_{j=1}^\rho [\bar{F}]_{ji} v_j$$

Thus we only need the first $\rho$ entries of each $i$-th column of $\bar{F}$ to express each $Fv_i$.
$\implies$ We can set all the other entries of $\bar{F}$ to zero.

$$
\bar{F} = \begin{bmatrix}
\bar{F}_{11} & \bar{F}_{12} \\
\mathbb{O} & \bar{F}_{22}
\end{bmatrix}
\begin{array}{l}
\}\rho \\
\}n-\rho
\end{array}
$$
*($Fv_i = [v_1 | \dots | v_\rho] [\dots]$)*

On the other hand from $\bar{G} = T^{-1}G$ we get:
$$G = T\bar{G} \implies [g_1 | \dots | g_m] = [v_1 | \dots | v_\rho | w_{\rho+1} | \dots | w_n] \bar{G}$$

Since $\text{Im } G \subseteq \text{Im } R$:
$\implies \forall i \in \{1, \dots, m\} \quad g_i \in <v_1, \dots, v_\rho>$
Then I can put to zero all the last $n-\rho$ rows:
$$
\bar{G} = \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix} \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
$$

### To Summarize:

By making use of $T$ previously derived, to change the basis in $X$ we obtain:

> [!success] Matrix Structures
> $$
> \bar{F} = T^{-1}FT = \left[ \begin{array}{c|c} F_{11} & F_{12} \\ \hline \mathbb{O} & F_{22} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> \qquad
> \bar{G} = T^{-1}G = \left[ \begin{array}{c} G_1 \\ \hline \mathbb{O} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> $$
> *Cols: $\rho, n-\rho$*

**Remember:**
1) If I move from $\Sigma$ to $\bar{\Sigma}$ we don't change the TF.
2) From $\Sigma$ to $\bar{\Sigma}$ the Reach. stays the same.

Since $(F,G)$ and $(\bar{F}, \bar{G})$ are algebraically equivalent, we know that $R \triangleq [G | FG | \dots | F^{n-1}G]$ is related to $\bar{R}$ by the relation $\bar{R} = T^{-1}R$ and this tells us that $\text{rank}(\bar{R}) = \text{rank}(R) = \rho < n$. Where:

$$
\bar{R} = \left[ \begin{array}{c|c|c|c} G_1 & F_{11}G_1 & \dots & F_{11}^{n-1}G_1 \\ \hline \mathbb{O} & \mathbb{O} & \dots & \mathbb{O} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
$$

Which means that $\text{rank}[G_1 | F_{11}G_1 | \dots | F_{11}^{n-1}G_1] = \rho$.

Reachability Matrix for $(G_1, F_{11})$ for $n-1$ steps (Which is $n-1 \ge \rho$).
$\Updownarrow$
By using Cayley-Hamilton we can claim that $\text{rank}[G_1 | F_{11}G_1 | \dots | F_{11}^{\rho-1}G_1] = \rho$.
**Thus $(G_1, F_{11})$ is Reachable.**

### Definition

> [!danger] Definition
> A pair $(\bar{F}, \bar{G})$ is in **Std. Reachability Form** if
> $$
> \bar{F} = \left[ \begin{array}{c|c} F_{11} & F_{12} \\ \hline \mathbb{O} & F_{22} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> \qquad
> \bar{G} = \left[ \begin{array}{c} G_1 \\ \hline \mathbb{O} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> $$
> And $(F_{11}, G_1)$ is a Reach. Pair (is a reachable pair).

Moreover we just proved that every non-reachable pair $(F,G)$ is algebraically equivalent to a pair $(\bar{F}, \bar{G})$ in Std Reachability Form.

Assume that the system $\bar{\Sigma} = (\bar{F}, \bar{G}, \bar{H}, \bar{D})$ is in STD form and assume without loss of generalities that:
$$
\bar{H} = [H_1 | H_2] \quad x(t) = \begin{bmatrix} x_1(t) \\ x_2(t) \end{bmatrix} \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
$$

We want to explicitly write the system eq:

> [!success] Decomposed System Equations
> $$
> \begin{cases}
> \begin{bmatrix} x_1(t+1) \\ x_2(t+1) \end{bmatrix} = \begin{bmatrix} F_{11} & F_{12} \\ \mathbb{O} & F_{22} \end{bmatrix} \begin{bmatrix} x_1(t) \\ x_2(t) \end{bmatrix} + \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix} u(t) \\
> y(t) = [H_1 | H_2] \begin{bmatrix} x_1(t) \\ x_2(t) \end{bmatrix} + \bar{D} u(t)
> \end{cases}
> $$

![[image-4 2.png]]

**Block Diagram Analysis:**
* **$\Sigma_R = (F_{11}, G_1, H_1, \bar{D})$:** Reachable Subsystem.
    * Input $u(t)$ goes into $G_1$.
    * State $x_1(t+1)$ depends on $x_1(t)$ via $F_{11}$ and $x_2(t)$ via $F_{12}$.
* **$\Sigma_{NR} = (F_{22}, \mathbb{O}, H_2, \mathbb{O})$:** Non Reachable Subsystem.
    * Autonomous (Without Input).
    * $x_2(t+1) = F_{22} x_2(t)$.

### The system above translate into:

![[image-5 2.png]]


**Diagram Logic:**
$u(t) \to \Sigma_R \to y(t)$.
$\Sigma_{NR}$ feeds into $\Sigma_R$ via $F_{12}$.

* $\Sigma_R$: I can do whatever I want with the state of this system.
* $\Sigma_{NR}$: I need to analyze this to make sure there aren't "Problematic" Eigenvalues.
    * $\implies$ Otherwise we need to redesign the system (Matrix G, thus the inputs).
    * We analyze $\sigma(F_{22})$ spectrum of the non reachable subsystem.

$\Sigma_{NR}$ is totally irrelevant when looking at the Transfer Function of the system because it's autonomous $\to TF(\Sigma) = TF(\Sigma_R)$.

$\bar{\Sigma}$ (Transf. Matrix of the whole system) depends only on $\Sigma_R$ and hence coincides with $\Sigma_R = (F_{11}, G_1, H_1, \bar{D})$.

### Proof

$$
\begin{aligned}
\bar{W}(z) &= [H_1 | H_2] \left[ \begin{array}{c|c} zI - F_{11} & F_{12} \\ \hline \mathbb{O} & zI - F_{22} \end{array} \right]^{-1} \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix} + \bar{D} \\
&= [H_1 | H_2] \left[ \begin{array}{c|c} (zI - F_{11})^{-1} & * \\ \hline \mathbb{O} & (zI - F_{22})^{-1} \end{array} \right] \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix} + \bar{D} \\
&= H_1 (zI - F_{11})^{-1} G_1 + \bar{D}
\end{aligned}
$$

> [!success] Result
> **Transfer Matrix of $\Sigma_R$**

$\bar{\Sigma}$ is algebraically equivalent to $\Sigma$ and $W_\Sigma(z) = W_{\bar{\Sigma}}(z) = W_{\Sigma_R}(z)$.


Thus every time we have a non-reachable subsystem the TF of the system will have a **Lower Degree** than $n$ at the denominator cause cancellations take place.
$\implies$ There is a part of the system that contributes to the output but is not affected by the input.
$\implies$ Lack of Reach. brings a Non-Reach. Subsystem and thus a lower degree Transf. Matrix.

### Theorem [PBH Reachability Test]

**Popov-Belevich-Hautus (PBH) Reachability Test**

Given a pair $(F,G)$ with $F \in \mathbb{R}^{n \times n}$, $G \in \mathbb{R}^{n \times m}$.

> [!success] PBH Test
> (1) The pair $(F,G)$ is **Reachable** IFF
> $$\text{rank}[zI_n - F | G] = n \quad \forall z \in \mathbb{C}$$
> *(PBH Reachability Matrix $\in \mathbb{R}[z]^{n \times (n+m)}$)*
>
> If the pair $(F,G)$ is **Not Reachable**, then:
> (2) $\text{rank}[\lambda I_n - F | G] < n \iff \lambda \in \sigma(F_{22})$
> Where $F_{22}$ is the matrix of the non-reachable subsystem in the Std. Reachability Form associated with $(F,G)$.

### Remarks for the Proof

**a.** $\forall z \notin \sigma(F)$, $[zI_n - F]$ is non singular square and hence:
$$[ \underbrace{zI_n - F}_{n} | G ] \text{ has rank } n$$
Therefore the condition (1) needs to be tested only in a **Finite Number of points** i.e. for $z \in \sigma(F)$.

**b.** Suppose $(\bar{F}, \bar{G})$ is algebraically equivalent to $(F,G)$ i.e. $\exists T$ is non singular square ST $(\bar{F}, \bar{G}) = (T^{-1}FT, T^{-1}G)$.
Then:
$$
[zI_n - \bar{F} | \bar{G}] = [z T^{-1}I_n T - T^{-1}FT | T^{-1}G]
$$
$$
= \underbrace{T^{-1}}_{NSS} [zI_n - F | G] \begin{bmatrix} T & \mathbb{O} \\ \mathbb{O} & I_m \end{bmatrix}
$$
$$
\implies \forall z \in \mathbb{C} \quad \text{rank}[zI_n - \bar{F} | \bar{G}] = \text{rank}[zI_n - F | G]
$$

### Proof

**(1) $\Leftarrow$ (By Counterpositive)**
To prove that statement $A \Rightarrow B$, we prove $\bar{B} \Rightarrow \bar{A}$.
We assume that $\exists \lambda \in \mathbb{C}$ ST the $\text{rank}[\lambda I_n - F | G] < n$.

Rows of $[\lambda I_n - F | G]$ are linearly dependent and hence $\exists v \neq 0$ ST:
$$v^T [\lambda I_n - F | G] = [0_n^T | 0_m^T]$$

$$
\iff \begin{cases}
v^T F = \lambda v^T \\
v^T G = 0^T
\end{cases} \implies
\begin{cases}
v^T G = 0^T \\
v^T FG = \lambda v^T G = 0^T \\
v^T F^2 G = v^T F(FG) = \lambda v^T FG = 0^T \\
\vdots \\
v^T F^{n-1} G = 0^T
\end{cases}
$$

$$
\implies v^T [G | FG | F^2 G | \dots | F^{n-1} G] = [0^T | 0^T | \dots | 0^T]
$$

$$
\implies 0^T = v^T R \implies \text{rank } R < n \implies (F,G) \text{ Not Reachable}
$$

**(2) $\Rightarrow$ We use again counterpositive**
We assume that $(F,G)$ not reachable and we prove that the PBH Reachability Matrix loses its rank in some point of $\mathbb{C}$.
If $(F,G)$ is not reachable then it's algebraically equivalent to $(\bar{F}, \bar{G})$ in Std. Reach. Form.

$$
\bar{F} = \begin{bmatrix} F_{11} & F_{12} \\ \mathbb{O} & F_{22} \end{bmatrix}, \quad \bar{G} = \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix} \quad \text{(A) } F_{11}, G_1 \text{ Reach. Pair}
$$

And we know (see remark b) that:
$$
\text{rank}[zI_n - F | G] = \text{rank}[zI_n - \bar{F} | \bar{G}] = \text{rank} \left[ \begin{array}{c|c||c} zI_\rho - F_{11} & -F_{12} & G_1 \\ \hline \mathbb{O} & zI_{n-\rho} - F_{22} & \mathbb{O} \end{array} \right]
$$

If $z = \lambda \in \sigma(F_{22})$ then the rows of $\lambda I - F_{22}$ are Lin. Dependent, but then also the rows of $[ \mathbb{O} | \lambda I - F_{22} | \mathbb{O} ]$ are Lin. Dep $\implies \text{rank}[\dots] < n$.
This also proves $(2) \Leftarrow$.

**(2) $\Rightarrow$ Assume that $(F,G)$ not Reach.** (and hence it's algebric. equivalent to a pair $(\bar{F}, \bar{G})$ in Std. Reach. Form (A)) and $\text{rank}[\lambda I_n - F | G] = \text{rank}[\lambda I - \bar{F} | \bar{G}] < n$ for some $\lambda \in \mathbb{C}$.
We want to prove that $\lambda \in \sigma(F_{22})$.

As the rank of:
$$
\left[ \begin{array}{c|c||c} \lambda I - F_{11} & -F_{12} & G_1 \\ \hline \mathbb{O} & \lambda I - F_{22} & \mathbb{O} \end{array} \right] < n
$$

$\exists \bar{v}^T = [v_1^T | v_2^T] \neq [0^T | 0^T]$ ST

$$
[v_1^T | v_2^T] \left[ \begin{array}{c|c||c} \lambda I - F_{11} & -F_{12} & G_1 \\ \hline \mathbb{O} & \lambda I - F_{22} & \mathbb{O} \end{array} \right] = [0^T | 0^T | 0^T]
$$

$$
\implies [v_1^T | v_2^T] \begin{bmatrix} \lambda I - F_{11} & G_1 \\ \mathbb{O} & \mathbb{O} \end{bmatrix} = [0^T | 0^T]
$$

$$
\implies v_1^T [\lambda I - F_{11} | G_1] = [0^T | 0^T]
$$

$\implies$ By the Reach. of $(F_{11}, G_1)$ and Proof (1): The only possib. is $v_1 = 0$.

But now $[v_1^T | v_2^T] \begin{bmatrix} -F_{12} \\ \lambda I - F_{22} \end{bmatrix} = 0^T$ ($v_1=0$).

Becomes:
$$
v_2^T (\lambda I - F_{22}) = 0^T \quad \text{with } v_2 \neq 0
$$
$\implies \lambda I - F_{22}$ is singular $\implies \lambda \in \sigma(F_{22})$. $\square$

> [!info] Remark
> The value of this criteria is in Part 2. It allows to identify $\sigma(F_{22})$ without calculating the Std Reach. Form.

### Ex:

**Consider a CT SSM:**
$$
\dot{x}(t) = Fx(t) + gu(t) \quad F = \begin{bmatrix} 0 & 1 & 1 \\ 2 & 1 & 0 \\ -1 & -1 & -2 \end{bmatrix} \quad g = \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix}
$$

**Prove that the system is not Reach. and derive the Std. Reach. Form.**

$$R = [g | Fg | F^2g] = \begin{bmatrix} 0 & 0 & 0 \\ 1 & 1 & 1 \\ -1 & -1 & -1 \end{bmatrix} \quad (g \text{ is an Eigenvector})$$

Clearly $\text{rank}(R) = 1 = \rho$.
$(F,G)$ Non Reach.

$$
T = \begin{bmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ -1 & 0 & 1 \end{bmatrix} \quad \text{we choose this} \quad T^{-1} = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix}
$$

$$
\bar{F} = T^{-1} F T = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 & 1 & 1 \\ 2 & 1 & 0 \\ -1 & -1 & -2 \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ -1 & 0 & 1 \end{bmatrix} = \left[ \begin{array}{c|cc} 1 & -1 & -1 \\ \hline 0 & 0 & 1 \\ 0 & 3 & 2 \end{array} \right]
$$
*(Top left: $F_{11}$, Top right: $F_{12}$, Bottom right: $F_{22}$)*

$$
\bar{g} = T^{-1} g = \begin{bmatrix} 0 & 0 & -1 \\ 1 & 0 & 0 \\ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ -1 \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \quad (G_1 = 1)
$$

**PBH Reachability Test**
We have only one criterion for reachability: $(F,G)$ is Reachable $\iff \text{rank}(R) = n$.
We add another criterion that relies on a polynomial matrix called **PBH Reachability Matrix**:
$$[zI - F | G] \in \mathbb{R}[z]^{n \times (n+m)}$$

* Has rank $n$ for **Almost** all values of $z$.
* Only for $z = \lambda_i$ is Singular ($\lambda_i \in \sigma(F)$). This block is reachable $\iff \text{rank}[zI_n - F | G] = n \ \forall z \in \mathbb{C}$.

## Corollary of PBH Reachability Test: Reachability of pairs (F,G) with F=J in Jordan Form

**Example:**
**Assume** $\bar{F} = J$:
$$
\begin{bmatrix}
2 & 1 & & | & & & & & & \\
& 2 & 1 & | & & & & & & \\
& & 2 & | & & & & & & \\
\hline
& & & | & 2 & | & & & & & \\
\hline
& & & & & | & 2 & | & & & \\
\hline
& & & & & & & | & 1 & 1 & | & \\
& & & & & & & | & & 1 & | & \\
\hline
& & & & & && & & & | & 1 & 1 \\
& & & & & & & & & & | & & 1
\end{bmatrix}
$$

* $\lambda_1 = 2 \quad n_1 = 5 \quad s_1 = 3 \quad n_{11}=3$
* $\lambda_2 = 1 \quad n_2 = 4 \quad s_2 = 2 \quad n_{21}=2$
* $n = 9$

$G = \begin{bmatrix} g_1 \\ \vdots \\ g_9 \end{bmatrix}$

We want to understand under what conditions on rows $g_1, \dots, g_9$ the pair $(F,G) = (J,G)$ is reachable using the PBH Reach.

We check the rank of the PBH Reachab. Matrix only corresp. to $z = \lambda_1 = 2$ and $z = \lambda_2 = 1$.

**Observe that** $\forall \lambda \quad \text{rank}[\lambda I - F | G] \equiv \text{rank}[F - \lambda I | G]$

**Assume now: $z = \lambda_1 = 2$**

$$
[F - 2I | G] = \left[ \begin{array}{ccc|cc|c||c}
0 & 1 & 0 & & & & & & &g_1 \\
0 & 0 & 1 & & & & & & &g_2 \\
\mathbf{0} & \mathbf{0} & \mathbf{0} & & & & & & &\mathbf{g_3} \\
\hline
& & & \mathbf{0} & & & & & &\mathbf{g_4} \\
& & & & \mathbf{0} & & & & &\mathbf{g_5} \\
\hline
& & & & & -1 & 1 & & &g_6 \\
& & & & & & -1 & && g_7 \\
\hline
& & & & & & & -1 & 1 & g_8 \\
& & & & & & & & -1 & g_9
\end{array} \right]
$$

* $J_1$ block (top left) becomes nilpotent.
* $J_2$ block (middle left) becomes zero diagonal.
* Critical Rows (Zeros): Rows corresponding to $g_3, g_4, g_5$.

**Analysis:**
* Rank $n=9$.
* Blocks corresponding to $\lambda \neq 2$ (like $\lambda=1$) become invertible/full rank (Lin. Indep).
* The "Critical Rows" are those where the Jordan blocks have zeros on the diagonal.
* $\implies g_3, g_4, g_5$ are Lin. Indep. Row Vectors.
    * We can use them to make the rows Lin. Indep.

**Assume $z = \lambda_2 = 1$**

$$
[F - 1I | G] = \left[ \begin{array}{c|c|cc||c}
\dots & & & & \dots \\
\hline
& \dots & & & \dots \\
\hline
& & \mathbf{0} & 1 && \mathbf{g_7} \\
& & \mathbf{0} & \mathbf{0}& & \mathbf{g_8} \\
\hline
& & & \mathbf{0} & 1 & \mathbf{g_8} \leftarrow \text{We need them} \\
& & & & \mathbf{0} & \mathbf{g_9} \leftarrow \text{to be lin. indep.}
\end{array} \right]
$$

This matrix has rank $n=9$ IFF $g_7$ and $g_9$ are Lin. Indep.

### Corollary

Let $(F,G) \ F \in \mathbb{R}^{n \times n}$ and $G \in \mathbb{R}^{n \times m}$.
Assume $F$ in Jordan form:
$$F = J = \begin{bmatrix} J_1 & & \\ & \ddots & \\ & & J_r \end{bmatrix}$$
$J_i \in \mathbb{R}^{n_i \times n_i}$ Jordan block associated with $\lambda_i$ ($\lambda_i \neq \lambda_j \ i \neq j$).

$$J_i = \begin{bmatrix} J_{i1} & & \\ & \ddots & \\ & & J_{is_i} \end{bmatrix}$$
$J_{ik}$ is the $k$-th Jordan Miniblock assoc. with $\lambda_i$.

**Accordingly, partition $G$ as follows:**
$$
G = \begin{bmatrix} G_1 \\ G_2 \\ \vdots \\ G_r \end{bmatrix} \begin{array}{l} \}n_1 \\ \}n_2 \\ \vdots \\ \}n_r \end{array}
\quad \text{with} \quad
G_i = \begin{bmatrix} G_{i1} \\ G_{i2} \\ \vdots \\ G_{is_i} \end{bmatrix} \begin{array}{l} \}n_{i1} \\ \}n_{i2} \\ \vdots \\ \}n_{is_i} \end{array}
$$

> [!success] Reachability Condition for Jordan Form
> $(F,G)$ is Reachable $\iff \forall i \in \{1, 2, \dots, r\}$
> The family of the **LAST ROWS** of the block $G_{i1}, \dots, G_{is_i}$ are Linear. Indep.

### Recap Reachability of a pair (F,G) with F=J in Jordan Form

**Hypothesis:**
$$
\bar{F} = \begin{bmatrix} \huge J \end{bmatrix} \quad
G = \begin{bmatrix} G_{11} \\ \vdots \\ G_{1s_1} \\ \hline G_{21} \\ \vdots \\ G_{2s_2} \\ \hline \vdots \\ \hline G_r \end{bmatrix}
$$
*(Note: $\Psi_F(z) = \Psi_J(z)$)*

**Then (F,G) is reachable $\iff$ ...**

*(Foto 3/11)*

### Remarks:

(1) It's clear that necessary condition for the family of **last rows** of the blocks $G_{i1}, \dots, G_{is_i}$ to be linearly independent is that:
$$m \ge s_i$$
*($m$: Length of row vect / # of inputs. $s_i$: # of row vect / Geometric Mult.)*

$\implies$ A necessary condition for $(F,G)$ to be reachable is that $m \ge s_i, \ \forall i=1, \dots, r$.
$\iff m \ge \max_{i=1, \dots, r} s_i = \max_{i=1, \dots, r} (\text{Geom. Multip. of } \lambda_i)$.

> [!info] Note
> That this claim doesn't only hold for $(F,G)$ if $F$ is in Jordan Form but for every $(F,G)$ since $\exists T$ non singular squared ST...
>
> (a) $(F,G)$ is reachable $\iff (J, T^{-1}G)$ is reachable.
> (b) $m$ and the geom. mult. of $\lambda$'s are the base for $(F,G)$ and $(J, T^{-1}G)$.

(2) If $m=1$ (Single Input System) a necessary condition for the reachability of pair $(F,g)$ is that:
$\forall i$ the Geometric Multip. of $\lambda_i = 1$.

Equiv. $\forall i$ there is a **Single Jordan Miniblock** associated with eigenvalue $\lambda_i$.

### Definition

> [!danger] Definition: Cyclic Matrix
> A matrix $F \in \mathbb{R}^{n \times n}$ is said to be **Cyclic** if $\exists v \in \mathbb{R}^n, \ v \neq 0$ ST the family of vectors $v, Fv, \dots, F^{n-1}v$ is linearly independent.

### Proposition

Given $F \in \mathbb{R}^{n \times n}$, the following are equivalent:
1.  $F$ is Cyclic.
2.  $\exists g \in \mathbb{R}^n$ ST $(F,g)$ is Reachable.
3.  For each eigenvalue of $F$ there is a **Single Jordan Miniblock**.
4.  Every eigenvalue of $F$ has unitary geometric multiplicity.
5.  $\Psi_F(z) \equiv \Delta_F(z)$ (Minimal Poly = Characteristic Poly).

### Exe 1

$$
F = J = \begin{bmatrix}
2 & 1 & | & & & & & & \\
& 2 & | & & & & & & \\
\hline
& &|& 3 & 1 && |& & & & & \\
& &|& & 3 & 1& |& & &  & & \\
& &|& & & 3 &|& & & & & \\
\hline
& & & & & & |&2 & 1 & | & \\
& & & & & & |&& 2 & | & \\
\hline
& & & & & & & & & | & & 3 & 1 \\
& & & & & & & & & | & & & 3
\end{bmatrix}
$$

**b) Construct G:**
$$
G = \begin{bmatrix}
0 & 0 & 0 \\
1 & 0 & 0 \\
\hline
0 & 0 & 0 \\
0 & 0 & 0 \\
1 & 0 & 0 \\
\hline
0 & 1 & 0 \\
0 & 0 & 1 \\
\hline
0 & 0 & 1 \\
0 & 1 & 0
\end{bmatrix}
$$

**Questions:**
a) Determine the smallest value of $m$ ST $\exists G \in \mathbb{R}^{n \times m}$ ($n=9$) for which $(F,G)$ is Reachable.
b) Determine any such matrix.

**Sol (a):**
Since $m = \max_i s_i \implies m=3$.

* $\lambda_1 = 2 \quad n_1 = 4 \quad s_1 = 3$
* $\lambda_2 = 3 \quad n_2 = 5 \quad s_2 = 2$

$\implies m \ge \max\{2, 3\} = 3$.

### Exe 2

$$
F = J = \begin{bmatrix}
2 & 1 & & & & \\
& 2 & & & & \\
& & 2 & & & \\
& & & 2 & 1 & \\
& & & & 2 & \\
& & & & & 3 & 1 \\
& & & & & & 3
\end{bmatrix} \quad \lambda \in \mathbb{R}
$$
*(Wait, the matrix in the image for Exe 2 has a $\lambda$ inside? No, it looks like it has fixed values, but the text says "For every $\lambda \in \mathbb{R}$". The matrix structure seems to have a variable parameter or the question implies adding a block with $\lambda$. Looking at the cases, it seems we are adding a new eigenvalue $\lambda$.)*

**Text:**
For every $\lambda \in \mathbb{R}$, determine $G$ with minimum \# of cols ST $(F,G)$ Reachable.

**We have 3 cases:**
1) $\lambda = 2$
2) $\lambda = 3$
3) $\lambda \neq 2, 3$

### Case 1: $\lambda = 2$

If $\lambda = 2$ then $F$ has 2 eigenvalues (The existing structure + new $\lambda=2$ block presumably or $\lambda$ modifies existing? The matrix $F=J$ shown has:
* Block 1: $\lambda=2$ size 2.
* Block 2: $\lambda=2$ size 1.
* Block 3: $\lambda=2$ size 2.
* Block 4: $\lambda=3$ size 2.
Total size shown is 7.
Wait, the matrix in image Exe 2 is:
Diag: $2, 2, 2, 2, 2, 3, 3$.
Blocks of 2:
$\begin{bmatrix} 2 & 1 \\ 0 & 2 \end{bmatrix}$ (Size 2)
$\begin{bmatrix} 2 \end{bmatrix}$ (Size 1)
$\begin{bmatrix} 2 & 1 \\ 0 & 2 \end{bmatrix}$ (Size 2)
So for $\lambda=2$: $n_1 = 5, s_1 = 3$.
For $\lambda=3$: $n_2 = 2, s_2 = 1$.

If the question implies "Consider the matrix F as given, and a parameter $\lambda$...", wait.
The matrix is written as $F=J$. The text says "For every $\lambda \in \mathbb{R}$".
Maybe the last block is $\lambda$? Or maybe we are adding a block?
Looking at the solution for Case 1 ($\lambda=2$):
$\lambda_1=2 \quad n_1=5 \quad s_1=3$
$\lambda_2=3 \quad n_2=2 \quad s_2=1$
Max $s_i = 3 \implies G_1$.

This matches the matrix description I derived.
So where is the $\lambda$ parameter?
Ah, maybe the question is about a matrix that HAS $\lambda$ in it.
Looking at the top matrix again:
It has $3 \ 1, \ 3$ at bottom.
But to the right there is "$\lambda \in \mathbb{R}$".
Maybe the last block is $\lambda$?
Or maybe the example is asking: Given $F$ as shown, what if we had an eigenvalue $\lambda$?
**Re-reading carefully:** "For every $\lambda \in \mathbb{R}$, determine $G$..."
Maybe the matrix $F$ depends on $\lambda$?
Let's look at Case 2: $\lambda=3$.
Then $\lambda_1=2 \ (n_1=3, s_1=2)$ ??
In the matrix shown, for $\lambda=2$ we had $s_1=3$.
Why in Case 2 does it say $n_1=3, s_1=2$?
Perhaps the matrix $F$ is:
Block 1: $\lambda=2$ (2x2)
Block 2: $\lambda=2$ (1x1)
Block 3: $\lambda$ (2x2 or similar?)
Let's look at the structure again.
Top left: 2 1 / 2. (2x2)
Middle: 2 1 / 2. (2x2)
Bottom: 3 1 / 3. (2x2)
This would mean:
$\lambda=2$: 2 blocks.
$\lambda=3$: 1 block.
$\lambda$: ...?

Let's look at the numbers in Case 1 solution again.
$\lambda=2 \implies \lambda_1=2, n_1=5, s_1=3$.
This implies 3 blocks of 2.
We see 2 blocks of 2 in the drawing?
Wait, row 3 has just '2'.
So:
Block 1: 2 1, 2 (2x2)
Block 2: 2 (1x1)
Block 3: 2 1, 2 (2x2)
Block 4: 3 1, 3 (2x2)
Total size: $2+1+2+2 = 7$.
If this is the fixed matrix $F$, why "For every $\lambda$"?
Maybe the "$\lambda$" is one of the diagonal entries?
Ah, the third block is $\lambda \ 1 / \lambda$.
Let's test this hypothesis.
If Block 3 is $\lambda$:
Matrix:
$J_1(2)$ size 2.
$J_2(2)$ size 1.
$J_3(\lambda)$ size 2.
$J_4(3)$ size 2.

**Test Case 1: $\lambda=2$**
Eigenvalues: 2, 3.
For 2: Blocks are $J_1(2), J_2(2), J_3(2)$ (all $\lambda=2$).
Sizes: 2, 1, 2.
$n_1 = 2+1+2 = 5$.
$s_1 = 3$ (3 blocks).
For 3: Block $J_4(3)$. Size 2. $s_2=1$.
Max $s_i = 3$.
This MATCHES Case 1 solution! $\implies$ **Hypothesis Correct: The 3rd block has eigenvalue $\lambda$.**

**Test Case 2: $\lambda=3$**
Eigenvalues: 2, 3.
For 2: Blocks $J_1, J_2$. Sizes 2, 1. $n_1=3, s_1=2$.
For 3: Blocks $J_3(3)$ (size 2), $J_4(3)$ (size 2). $n_2=4, s_2=2$.
Max $s_i = 2$.
Matches Case 2 solution!

**Test Case 3: $\lambda \neq 2, 3$**
Eigenvalues: 2, $\lambda$, 3.
For 2: $s_1=2$.
For $\lambda$: $s_2=1$ (1 block of size 2).
For 3: $s_3=1$ (1 block of size 2).
Max $m=2$.
Matches Case 3 solution!

**Solutions:**

* **Case 1 ($\lambda=2$):** $m=3$.
    $$
    G_1 = \begin{bmatrix}
    0 & 0 & 0 \\
    1 & 0 & 0 \\
    \hline
    0 & 1 & 0 \\
    \hline
    0 & 0 & 0 \\
    0 & 0 & 1 \\
    \hline
    0 & 0 & 0 \\
    1 & 1 & 1
    \end{bmatrix}
    $$
    *(Note: The last block for $\lambda=3$ needs only 1 column to be reachable, but $m=3$ so we fill or reuse columns. The rows corresponding to the end of blocks must be lin. indep.
    End of blocks indices: 2, 3, 5, 7.
    Rows 2, 3, 5 must be indep for $\lambda=2$.
    Row 7 must be non-zero for $\lambda=3$.
    In $G_1$: Row 2=[1 0 0], Row 3=[0 1 0], Row 5=[0 0 1]. Indep!
    Row 7=[1 1 1]. Non-zero!)*

* **Case 2 ($\lambda=3$):** $m=2$.
    $$
    G_2 = \begin{bmatrix}
    0 & 0 \\
    1 & 0 \\
    \hline
    0 & 1 \\
    \hline
    0 & 0 \\
    1 & 0 \\
    \hline
    0 & 0 \\
    0 & 1
    \end{bmatrix}
    $$
    *End indices: 2, 3 (for $\lambda=2$) -> Rows 2, 3. [1 0], [0 1]. Indep.
    End indices: 5, 7 (for $\lambda=3$) -> Rows 5, 7. [1 0], [0 1]. Indep.*

* **Case 3 ($\lambda \neq 2, 3$):** $m=2$.
    Same as $G_2$.

---
## STATE-FEED BACK

Comparison beetween STATE-FEEDBACK SSM and OUTPUT FEEDBACK for I/O MODELS

> [!success] Tracking Error
> $$e(t) \equiv \text{TRACKING ERROR} \to e(t) = r(t) - y(t)$$

### Control Theory

**Diagram Logic:**
![[image-6 2.png]]
	
* **Process is given**
* **Reference signal is given**

> [!info] Goal
> Design a **DYNAMIC CONTROLLER** TRANSFER FUNCTION on I/O MODEL to make $y(t) \approx r(t)$ AS $t \to +\infty$

### State-Space approach

![[image-7.png]]

> [!info] Goal
> Design the **STATE FEEDBACK** in such a way that the eigenvalues (on the elementary modes) of the resulting controlled system are as derived.

Consider a **Strictly Proper** SSM (Matrix $D=0$)

$$
\begin{cases}
\dot{x}(t) = Fx(t) + Gu(t) \\
y(t) = Hx(t)
\end{cases} \quad t \in \mathbb{R}_+ \quad \begin{aligned} \dim x &= n \\ \dim u &= m \\ \dim y &= p \end{aligned}
$$

We will consider **Static-State Feedback Laws**

> [!success] Control Law
> $$u(t) = \underset{\substack{\uparrow \\ \text{Indep.} \\ \text{Input} \\ \text{Component}}}{v(t)} + \underset{\substack{\uparrow \\ K \in \mathbb{R}^{m \times n}}}{K} x(t)$$

Under this system description becomes:

$$
\Sigma_K := \begin{cases}
\dot{x}(t) = Fx(t) + Gv(t) + GKx(t) \\
\quad \quad \triangleq (F+GK)x(t) + Gv(t) \\
y(t) = Hx(t)
\end{cases}
$$

We see that:

$$
\begin{aligned}
\Sigma &= (F,G,H) \\
&\downarrow \ K \in \mathbb{R}^{m \times n} \\
\Sigma_K &= (F+GK, G, H)
\end{aligned}
$$

![[image-8.png]]

> [!info] Reversibility
> The transformation is **Reversable**.
> From $\Sigma_K$ to $\Sigma$ using $-K$.
> *This is always reversable.*

Let us try to understand what feedback leaves invariant.

> [!warning] Proposition 1
> *(This is true in CT and DT)*
> Given pair $(F,G)$ with $F \in \mathbb{R}^{n \times n}$ and $G \in \mathbb{R}^{n \times m}$ for every $K \in \mathbb{R}^{m \times n}$ and every $i \in \mathbb{Z}_+, \ i \ge 1$,
>
> $$\text{Im}[G | (F+GK)G | \dots | (F+GK)^{i-1}G] = \text{Im}[G | FG | \dots | F^{i-1}G]$$

This implies ($i=n$) that:

> [!success] Result
> $$(F+GK, G) \text{ is reachable } \iff (F,G) \text{ is reachable}$$
>
> *(Synthesis: Cannot spoil reachability)*

> [!warning] Proposition 2
> Consider a **Non Reachable** pair $(F,G)$, $F \in \mathbb{R}^{n \times n}$, $G \in \mathbb{R}^{n \times m}$ and assume it's in **Std. Reach. Form**.
>
> We assume:
> $$
> F = \left[ \begin{array}{c|c} F_{11} & F_{12} \\ \hline \mathbb{O} & F_{22} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> \qquad
> G = \left[ \begin{array}{c} G_1 \\ \hline \mathbb{O} \end{array} \right] \begin{array}{l} \}\rho \\ \}n-\rho \end{array}
> $$
>
> With $(F_{11}, G_1)$ **Reach. Pair**.
>
> **Then** $\forall K \in \mathbb{R}^{m \times n}$ the pair $(F+GK, G)$ is **Non Reachable**, in Std. Reach. Form with the **Same Matrix** of the non reachable sub system $F_{22}$ as for $(F,G)$.

### Proof 2:

Assume $K = [\underbrace{K_1}_{\rho} | \underbrace{K_2}_{n-\rho}]$

**Then:**
$$
F + GK = \left[ \begin{array}{c|c} F_{11} & F_{12} \\ \hline \mathbb{O} & F_{22} \end{array} \right] + \left[ \begin{array}{c} G_1 \\ \hline \mathbb{O} \end{array} \right] [K_1 | K_2]
$$

$$
= \left[ \begin{array}{c|c} \mathbf{F_{11} + G_1 K_1} & \mathbf{F_{12} + G_1 K_2} \\ \hline \mathbb{O} & F_{22} \end{array} \right] \qquad G = \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix}
$$

> [!success] In Addition
> $(F_{11} + G_1 K_1, G_1)$ is a **Reachable Pair** by **Prop. 1**.
> *(Corresponds to the green circle "Need to be reachable by Prop 1")*

To relate $K$ and $\bar{K}$ it is sufficient to observe that:
> [!info] Relation
> $$\bar{F} + \bar{G}\bar{K} = T^{-1}FT + T^{-1}G\bar{K} = T^{-1}[F + G\underbrace{\bar{K}T^{-1}}_{K}]T$$

## Complete Eigenvalue Allocation Problem

Let $F \in \mathbb{R}^{n \times n}$ and $G \in \mathbb{R}^{n \times m}$.
Under what conditions on the pair $(F,G)$ I can claim **FOR EVERY CHOICE** of $n$ (not necessarily distinct) complex numbers $\lambda_1, \lambda_2, \dots, \lambda_n \in \mathbb{C}$ I can always determine $K \in \mathbb{R}^{m \times n}$ ST $\sigma(F+GK) = \{\lambda_1, \lambda_2, \dots, \lambda_n\}$?

> [!warning] Constraint
> Since $F+GK$ is real and hence $\Delta_{F+GK}(s) \in \mathbb{R}[s]$ clearly n-tuple of complex numbers could be proposed.
> If $\lambda \in \mathbb{C} \setminus \mathbb{R}$ and it appears $k$ times in the sequence $\{\lambda_1, \dots, \lambda_n\}$ then $\exists j$ ST $\lambda_j = \bar{\lambda}_i$ and also $\lambda_j$ appears $k$ times in $\{\lambda_1, \dots, \lambda_n\}$.
> I can always determine $K \in \mathbb{R}^{m \times n}$ ST $\sigma(F+GK) = \{\lambda_1, \dots, \lambda_n\}$?

**Equivalently:**
Given $F \in \mathbb{R}^{n \times n}$, $G \in \mathbb{R}^{n \times m}$ under what conditions for every monic polynomial $p(s) \in \mathbb{R}[s]$ of degree $n$, $\exists K \in \mathbb{R}^{m \times n}$ ST $\Delta_{F+GK}(s) = p(s)$?

From Prop 2 we deduce that if:

Complete Eigenvalue Allocation Problem is solvable $\implies (F,G)$ IS REACHABLE.

We want to proof if $(F,G)$ Reach. then the complete eigenvalue allocation of the problem is solvable.

1.  **Step 1)** We will prove that the result is true if single reachable systems ($m=1$).
2.  **Step 2)** We will extend the result to the case $m>1$.

## 1st Step: The Case of Single Input Reachable Systems

> [!danger] Theorem [Controllable Canonical Form]
> Assume $F \in \mathbb{R}^{n \times n}$ and $g \in \mathbb{R}^n$.
> Then $(F,g)$ is reachable IFF $\exists T \in \mathbb{R}^{n \times n}$ (Non Singular) ST
>
> $$
> \underbrace{T^{-1}FT}_{F_c} = \begin{bmatrix} 0 & 1 & 0 & \dots & 0 \\ 0 & 0 & 1 & \dots & 0 \\ 0 & 0 & 0 & 1 & \dots \\ \vdots & & \ddots & \vdots \\ -a_0 & -a_1 & -a_2 & \dots & -a_{n-1} \end{bmatrix}
> \quad
> \underbrace{Tg}_{g_c} = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}
> $$
>
> **Controllable Canonical Form**
> *(Matrix $F_c$ is Companion Matrix)*

### Proof:

$\Leftarrow$ If $(F,g)$ is algebraically equivalent to the pair $(F_c, g_c)$ then
$R_c = [g_c | F_c g_c | \dots | F_c^{n-1} g_c]$ is related to $R = [g | Fg | \dots | F^{n-1}g]$ by
$$R_c = T^{-1} R$$

On the other hand:
$$
R_c = \begin{bmatrix} 0 & 0 & 0 & \dots & 1 \\ 0 & 0 & 0 & \dots & * \\ 0 & 0 & 1 & * & * \\ \vdots & 1 & * & & * \\ 1 & * & * & & * \end{bmatrix}
$$
*(I don't care what it is)*

$\implies \text{rank } R_c = n$
$\Downarrow$
$\text{rank } R = n$
$\Downarrow$
$(F,g)$ Reachable.

$\Rightarrow$ We assure $(F,g)$ Reach. $\to$
$R = [g | Fg | \dots | F^{n-1}g]$ has $n$ linearly indep. cols.

Assume that $\Delta_F(s) = s^n + a_{n-1}s^{n-1} + \dots + a_1s + a_0 \in \mathbb{R}[s]$. Based on the cols of $R$ and coeff. of $\Delta_F(s)$ we want to construct the matrix $T$ ST $T$ is non singular and the pair $(T^{-1}FT, T^{-1}g)$ is in controllable canonical form.

Set:
$v_n = g$
*(They are Lin. Ind. cause R has Lin. Ind. Cols)*
*(Always same position)*

$$
\begin{aligned}
v_{n-1} &= Fg + a_{n-1}g \\
v_{n-2} &= F^2g + a_{n-1}Fg + a_{n-2}g \\
&\vdots \\
v_2 &= F^{n-2}g + a_{n-1}F^{n-3}g + \dots + a_2g \\
v_1 &= F^{n-1}g + a_{n-1}F^{n-2}g + \dots + a_1g
\end{aligned}
$$

**This is a linearly independent family!**

Set $T \triangleq [v_1 | v_2 | \dots | v_n] \in \mathbb{R}^{n \times n}$, $T$ Non Singular.

We want to prove that $T^{-1}FT = F_c$, this is equivalent to prove that $FT = TF_c$ namely that $F[v_1 | v_2 | \dots | v_n] = [v_1 | v_2 | \dots | v_n][F_c]$.

To this goal we need to calculate $Fv_i, \ i=1, \dots, n$:

* $Fv_n = Fg = [Fg + a_{n-1}g] - a_{n-1}g = v_{n-1} - a_{n-1}v_n$
* $Fv_{n-1} = F^2g + a_{n-1}Fg = [F^2g + a_{n-1}Fg + a_{n-2}g] - a_{n-2}g = v_{n-2} - a_{n-2}v_n$
    $\vdots$
* $Fv_2 = v_1 - a_1 v_n$
* $Fv_1 = F^n g + a_{n-1}F^{n-1}g + \dots + a_1 Fg =$
    $$
    = [F^n g + a_{n-1}F^{n-1}g + \dots + a_1 Fg + a_0 g] - a_0 g
    $$
    $$
    = [\underbrace{F^n + a_{n-1}F^{n-1} + \dots + a_0 I}_{\Delta_F(F) = \mathbb{O}_{n \times n} \text{ BY CAYLEY-HAMILTON}}]g - a_0 g = -a_0 v_n
    $$

**Therefore:**

$$
[Fv_1 | Fv_2 | \dots | Fv_{n-1} | Fv_n] = [v_1 | \dots | v_{n-1} | v_n]
\begin{bmatrix} 0 & 1 & 0 & \dots & 0 \\ 0 & 0 & 1 & \dots & 0 \\ \vdots & \vdots & & \ddots & \vdots \\ 0 & 0 & 0 & \dots & 1 \\ -a_0 & -a_1 & -a_2 & \dots & -a_{n-1} \end{bmatrix}
$$

**Finally, we have to prove that:** $T^{-1}g = T g_c$
$\iff g = T g_c = [v_1 | \dots | v_n] \begin{bmatrix} 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix} = v_n$. $\square$

### State-Feedback Recap

$\Sigma = (F,G,H) \xrightarrow[u(t) = v(t) + Kx(t), K \in \mathbb{R}^{m \times n}]{} \Sigma_K (F+GK, G, H)$
* $\dim \Sigma = n$
* $m$ inputs, $p$ outputs.

**Propositions:**
1.  $\forall K \in \mathbb{R}^{m \times n} \ (F,G)$ Reach. IFF $(F+GK, G)$ Reach.
2.  If $(F,G)$ is in Std Reach. Form then $\forall K \in \mathbb{R}^{m \times n}, (F+GK, G)$ is in Std. Reach. Form with the **same $F_{22}$**.

### Remark about Prop (2)

If
$F = \begin{bmatrix} F_{11} & F_{12} \\ \mathbb{O} & F_{22} \end{bmatrix}$, $G = \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix}$

$(F_{11}, G_1)$ Reachable.
Then $\forall K = [K_1 | K_2]$:

$$
F+GK = \begin{bmatrix} F_{11} + G_1 K_1 & F_{12} + G_1 K_2 \\ \mathbb{O} & F_{22} \end{bmatrix}, \quad G = \begin{bmatrix} G_1 \\ \mathbb{O} \end{bmatrix}
$$

**This implies that**
$\Delta_{F+GK}(s) = \Delta_{F_{11}+G_1K_1}(s) \underbrace{\Delta_{F_{22}}(s)}_{\text{UNCHANGED}}$.

If we have a generic non reachable pair $(F,G)$ non necessarily in Std Reach. Form this result is still true.

$$
(F,G) \text{ Not Reachable} \xrightarrow[\substack{T \in \mathbb{R}^{n \times n} \\ \text{Non Singular}}]{} (\bar{F}, \bar{G}) = (T^{-1}FT, T^{-1}G) \xrightarrow[\forall \bar{K} \in \mathbb{R}^{m \times n}]{} (\bar{F}+\bar{G}\bar{K}, \bar{G}) \text{ in STD Reach. Form with } \Delta_{\bar{F}+\bar{G}\bar{K}} \text{ of } \Delta_{F_{22}}(s)
$$

$$K = \bar{K} T^{-1}$$

$\rightarrow (F+GK, G)$ Non Reach. with $\Delta_{F+GK}$ is a multiple of $\Delta_{F_{22}}$.

> [!info] Logic Flow
> **Complete Eigenvalue Allocation Problem for a pair (F,G)**
> $\equiv$
> $\forall p(s) \in \mathbb{R}[s]$ Monic of Deg $n$ $\exists K \in \mathbb{R}^{m \times n}$ ST $\Delta_{F+GK}(s) \equiv p(s)$
>
> $\implies$ (Prop 2) **(F,G) IS REACHABLE**
>
> $\Longleftarrow$ **We want to prove that this is true**

## Theorem:

Given $(F,g) \ F \in \mathbb{R}^{n \times n}, \ g \in \mathbb{R}^n$.
$(F,g)$ Reachable $\iff (F,g)$ is algebr. equivalent to a pair $(F_c, g_c)$ in **Controllable Canonical Form**
($\exists T \in \mathbb{R}^{n \times n} \ \det T \neq 0$)

$$
F_c = T^{-1}FT = \begin{bmatrix} 0 & 1 & \dots & 0 \\ \vdots & \ddots & \ddots & \vdots \\ 0 & \dots & \dots & 1 \\ -a_0 & -a_1 & \dots & -a_{n-1} \end{bmatrix} \quad g_c = T^{-1}g = \begin{bmatrix} 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}
$$
*(Companion Form)*

$$
\Delta_{F_c}(s) = s^n + \sum_{i=0}^{n-1} a_i s^i
$$

For $(F_c, g_c)$ in controllable canonical form the complete eigenvalue allocation problem is solvable. Indeed, assume:
$$p(s) = s^n + p_{n-1}s^{n-1} + \dots + p_1 s + p_0$$

Set $K_c = [k_0 \ k_1 \ \dots \ k_{n-1}]$. Then:

$$
F_c + g_c K_c = \begin{bmatrix} 0 & 1 & \dots & 0 \\ \vdots & \ddots & \ddots & \vdots \\ 0 & \dots & \dots & 1 \\ -a_0+k_0 & -a_1+k_1 & \dots & -a_{n-1}+k_{n-1} \end{bmatrix}
$$

**Proof:**
$\implies \exists T \in \mathbb{R}^{n \times n}$ Non Singular ST $T^{-1}FT = F_c$ (in companion form).

We want to prove that for a pair $(F_c, g_c)$ in canonical form the complete eigenvalue allocation problem is always solvable.

**Assume:**
$$
F_c = \begin{bmatrix} 0 & 1 & \\ & \ddots & \\ & & 1 \\ -a_0 & \dots & -a_{n-1} \end{bmatrix} \quad g_c = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}
$$

And we want to obtain $p(s) = s^n + p_{n-1}s^{n-1} + \dots + p_n \in \mathbb{R}[s]$ as charact. polynomial.

Set $K_c = [k_0 \ k_1 \ \dots \ k_{n-1}] \in \mathbb{R}^{1 \times n}$

**Then:**
$$
F_c + g_c K_c = \begin{bmatrix} 0 & 1 & \\ & \ddots & \\ & & 1 \\ -a_0 & \dots & -a_{n-1} \end{bmatrix} + \begin{bmatrix} 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix} [k_0 \ k_1 \ \dots \ k_{n-1}]
$$

$$
= \begin{bmatrix} 0 & 1 & \\ & \ddots & \\ & & 1 \\ -(a_0-k_0) & -(a_1-k_1) & \dots & -(a_{n-1}-k_{n-1}) \end{bmatrix}
$$

$\implies \Delta_{F_c + g_c K_c}(s) = s^n + (a_{n-1}-k_{n-1})s^{n-1} + \dots + (a_1-k_1)s + (a_0-k_0)$

$$
= s^n + p_{n-1} s^{n-1} + \dots + p_1 s + p_0
$$

*(Matching coefficients)*

### Remark:

$F_c + g_c K_c$ is still in companion form and hence $(F_c + g_c K_c, g_c)$ is still in controllable form.

Since $F_c + g_c K_c$ is in companion form:
$$
\Delta_{F_c+g_cK_c}(s) = s^n + \underbrace{(a_{n-1}-k_{n-1})}_{p_{n-1}}s^{n-1} + \dots + \underbrace{(a_1-k_1)}_{p_1}s + \underbrace{(a_0-k_0)}_{p_0}
$$

$$
\implies K_c = [a_0-p_0 \quad a_1-p_1 \quad \dots \quad a_{n-1}-p_{n-1}]
$$

### How do I generalize this result to ANY single input reachable pair (F,g)?

[Diagram of Algebraic Equivalence]

1.  **$(F,g)$ Reachable** $\xrightarrow[T \in \mathbb{R}^{n \times n}, \det T \neq 0]{}$ **$(F_c, g_c) = (T^{-1}FT, T^{-1}g)$ Controllable Canonical Form**.
    
2.  **Right Side:** For $(F_c, g_c)$, $\forall p(s) \in \mathbb{R}[s] \ \exists K_c \in \mathbb{R}^{1 \times n}$ such that $\Delta_{F_c+g_c K_c} \equiv p(s)$.
    $\downarrow$
    $(F_c+g_c K_c, g_c)$ is Reachable (Contr. Can. Form).

3.  **Left Side:** We want $\forall p(s) \in \mathbb{R}[s] \ \exists K \in \mathbb{R}^{1 \times n}$...
    $\downarrow$
    $(F+gK, g)$ Reachable.

4.  **Connecting:** Through $T^{-1}$.
    $K = K_c T^{-1}$.

$\implies \Delta_{F+gK}(s) = p(s) \iff \Delta_{F_c+g_c K_c} \equiv p(s)$.

$$F_c + g_c K_c = T^{-1}FT + T^{-1}g K_c = T^{-1} [F + g \underbrace{K_c T^{-1}}_{=K}] T$$

### Remarks:

(1) From the proof we deduce that once we know that a pair $(F,g)$ is Reach. (if rank $R=n$), we can simply calculate $\Delta_F(s) = s^n + a_{n-1}s^{n-1} + \dots + a_0$ and immediately write the **Controllable Canonical Form** $(F_c, g_c)$ even without calculating $T$.

Indeed, once I've written $(F_c, g_c)$ I can calculate $R_c$ and use:
$$
\boxed{R_c} = \boxed{T^{-1}} \boxed{R} \quad \text{to deduce} \quad \boxed{T} = \boxed{R} \boxed{R_c}^{-1}
$$

### State Feedback: DT vs CT

|                           | Discrete Time (DT)                                | Continuous Time (CT)                        |
| :------------------------ | :------------------------------------------------ | ------------------------------------------- |
| **Control Law**           | $u(k) = Kx(k) + v(k)$                             | $u(t) = Kx(t) + v(t)$                       |
| **Closed Loop Dynamics**  | $x(k+1) = (F+GK)x(k) + Gv(k)$                     | $\dot{x}(t) = (F+GK)x(t) + Gv(t)$           |
| **Reachability Property** | Feedback $u=Kx+v$ preserves Reachability          | Feedback $u=Kx+v$ preserves Reachability    |
| **Eigenvalue Allocation** | Possible iff $(F,G)$ is Reachable                 | Possible iff $(F,G)$ is Reachable           |
| **Target Polynomial**     | $p(z) = z^n + p_{n-1}z^{n-1} + \dots + p_0$       | $p(s) = s^n + p_{n-1}s^{n-1} + \dots + p_0$ |
| **Stability Goal**        | Roots of $p(z)$ inside unit circle ($\lambda< 1$) | Roots of $p(s)$ in LHP ($Re(\lambda) < 0$)  |
| **Canonical Form**        | $F_c, G_c$ structure identical to CT              | $F_c, G_c$ structure identical to DT        |

(2) Since $F_c = T^{-1}FT$ then $\Delta_{F_c}(s) = \Delta_F(s) = s^n + a_{n-1}s^{n-1} + \dots + a_0$.

But this tells us that the Characteristic Polynomial of a matrix $F_c$ in companion form can be **read from the last row**.

(3) $F$ is cyclic $\iff \exists g \in \mathbb{R}^n$ ST $(F,g)$ is reachable.
$\implies \exists g \in \mathbb{R}^n$ and $T \in \mathbb{R}^{n \times n}$ non singular ST $T^{-1}FT = F_c = \begin{bmatrix} 0 & 1 \\ & \ddots & 1 \\ -a_0 & \dots & -a_{n-1} \end{bmatrix}$
$$T^{-1}g = g_c = \begin{bmatrix} 0 \\ \vdots \\ 1 \end{bmatrix}$$

> [!warning] Proposition
> Consider a pair $(F,g)$ with $F \in \mathbb{R}^{n \times n}, g \in \mathbb{R}^n$.
>
> 1) $\forall p(s) \in \mathbb{R}[s]$ monic of deg $n$, $\exists K \in \mathbb{R}^{1 \times n}$ ST $\Delta_{F+gK}(s) \equiv p(s)$
>
> $\iff (F,g)$ IS REACHABLE
>
> If $(F,g)$ is Not Reachable and $F_{22}$ is the matrix of the non reach. subsystem then:
>
> * Given $p(s) \in \mathbb{R}[s]$ monic of deg $n$, $\exists K \in \mathbb{R}^{1 \times n}$ ST $\Delta_{F+gK}(s) \equiv p(s)$
> $\iff p(s)$ is a multiple of $\Delta_{F_{22}}(s)$ (i.e. $p(s) \equiv \Delta_{F_{22}}(s) \bar{p}(s)$ $\exists \bar{p}(s) \in \mathbb{R}[s]$) $\leftarrow$ **Prop. 2**
>
> * Since $(F,g)$ is not reach. then WLOF we can assume
> $$F = \begin{bmatrix} F_{11} & F_{12} \\ \mathbb{O} & F_{22} \end{bmatrix} \quad g = \begin{bmatrix} g_1 \\ \mathbb{O} \end{bmatrix} \quad (F_{11}, g_1) \text{ Reachable}$$
>
> Therefore: $K = [K_1 | \mathbb{O}]$
> $\implies F+gK = \begin{bmatrix} F_{11}+g_1K_1 & F_{12} \\ \mathbb{O} & F_{22} \end{bmatrix}$
> $\implies \Delta_{F+gK}(s) = \Delta_{F_{11}+g_1K_1}(s) \Delta_{F_{22}}(s)$.
>
> By (1) we can make this polynomial equal to $\bar{p}(s)$.
> $\implies \Delta_{F+gK}(s) = p(s) = \bar{p}(s) \Delta_{F_{22}}(s)$.

### Exerc. 1

**Consider the DT SSM**
$$x(t+1) = Fx(t) + Gu(t) = \begin{bmatrix} 0 & 1 & 0 \\ -1 & -2 & 0 \\ 0 & 1 & 1 \end{bmatrix} x(t) + \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} u(t)$$

1) Determine (if $\exists$) the controllable canonical form $(F_c, g_c)$ associated with $(F,g)$.
2) Given $p(z) = (z - \frac{1}{2})^2 z$ determine $K_c \in \mathbb{R}^{1 \times 3}$ ST $\Delta_{F_c+g_cK_c}(z) \equiv p(z)$.
3) Using $K_c$, determine $K \in \mathbb{R}^{1 \times 3}$ ST $\Delta_{F+gK}(z) \equiv p(z)$.

**Sol**
(1) Is $(F,g)$ reachable?
$$R = [g | Fg | F^2g] = \begin{bmatrix} 1 & 0 & -1 \\ 0 & -1 & 2 \\ 0 & 0 & -1 \end{bmatrix}$$
Rank = 3. (It's non sing. cause it's triangular).

$\implies (F,g)$ Reach. Hence algebr. equiv. to a pair $(F_c, g_c)$ in controllable canonical form.

We observe that: $F = \begin{bmatrix} 0 & 1 & 0 \\ -1 & -2 & 0 \\ 0 & 1 & 1 \end{bmatrix} = \begin{bmatrix} F_{11} & \mathbb{O} \\ F_{21} & F_{22} \end{bmatrix}$
*(Wait, block partitioning looks different in image)*
Image shows partitioning top left $2 \times 2$.
$\Delta_F = \Delta_{F_{11}} \Delta_{F_{22}} = (z+1)^2 (z-1) = z^2+2z+1 (z-1) = [z^3+z^2-z-1]$.
$\Delta_{F_{11}} = z^2+2z+1 \implies a_2=1, a_1=2, a_0=1$? No. $z^2 - \text{tr}(F_{11})z + \det(F_{11}) = z^2 - (-2)z + 1 = (z+1)^2$.
$\implies a_2=1, a_1=-1, a_0=-1$ for the whole poly $z^3+z^2-z-1$.

$$F_c = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 1 & -1 \end{bmatrix} \quad g_c = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
*(From coeffs of $z^3+z^2-z-1$: $a_2=1 \to -1$, $a_1=-1 \to 1$, $a_0=-1 \to 1$)*.

(2) We observe that $p(z) = (z - \frac{1}{2})^2 z = z^3 - z^2 + \frac{1}{4}z$.
$a_3=1, a_2=-1, a_1=1/4, a_0=0$.

Set $K_c = [k_0 \ k_1 \ k_2]$
Then $F_c + g_c K_c = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1+k_0 & 1+k_1 & -1+k_2 \end{bmatrix} \equiv \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -a_0 & -a_1 & -a_2 \end{bmatrix} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 0 & -1/4 & 1 \end{bmatrix}$

$\implies 1+k_0 = 0 \to k_0 = -1$
$\implies 1+k_1 = -1/4 \to k_1 = -5/4$
$\implies -1+k_2 = 1 \to k_2 = 2$

$\implies K_c = [-1 \ -5/4 \ 2]$.

(3) We want to find $K$.
We know $K = K_c T^{-1}$. $T^{-1}$? $R_c = T^{-1} R$.
$\implies T^{-1} = R_c R^{-1}$.

$$T^{-1} = \begin{bmatrix} 0 & 0 & 1 \\ 0 & 1 & -1 \\ 1 & -1 & 2 \end{bmatrix} \begin{bmatrix} 1 & 0 & -1 \\ 0 & -1 & -2 \\ 0 & 0 & -1 \end{bmatrix}^{-1} = \begin{bmatrix} 0 & 0 & -1 \\ 0 & -1 & -1 \\ 1 & 1 & -1 \end{bmatrix}$$
*(We know that is block triang.)*

$$K = [-1 \ -5/4 \ 2] \begin{bmatrix} 0 & 0 & -1 \\ 0 & -1 & -1 \\ 1 & 1 & -1 \end{bmatrix} = [2 \ 13/4 \ -1/4]$$

**Fast Solution:**
* Check rank R.
* If rank R=3 $\to$ Probl. Solv.
* Then set $K \in [a \ b \ c]$.
* Calculate $F+gK$ in parametric form.
* Impose $\Delta_{F+gK}(z) \equiv (z-1/2)^2 z = z^3 - z^2 + 1/4 z$.
* $z^3 + a_2(a,b,c)z^2 + a_1(a,b,c)z + a_0(a,b,c)$
* $= -1, = 1/4, = 0$.

### Exer 2:

Given the CT SSM
$$\dot{x}(t) = Fx(t) + Gu(t) = \begin{bmatrix} -1 & 0 & 0 \\ 1 & 0 & 1 \\ 0 & -1 & 2 \end{bmatrix} x(t) + \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} u(t)$$

Determine if possible $K \in \mathbb{R}^{1 \times 3}$ ST $\Delta_{F+gK}(s) = (s+1)^3$.

**Sol**
Check Reach.
$$R = [g | Fg | F^2g] = \begin{bmatrix} 0 & 0 & 0 \\ 0 & 1 & 2 \\ 1 & 2 & 3 \end{bmatrix}$$
**Not Reachable** (We have a 0 row).

$(F,g)$ is Not Reach.
Since $\rho = \text{rank } R = 2 \implies \dim F_{22} = n-\rho = 3-2 = 1$.

What are the eigenvalues of F?
$$F = \begin{bmatrix} -1 & 0 & 0 \\ \hline 1 & 0 & 1 \\ 0 & -1 & 2 \end{bmatrix} \implies \sigma(F) = \sigma(\tilde{F}_{11}) \cup \sigma(\tilde{F}_{22}) = \{-1\} \cup \{1, 1\}$$
$\tilde{F}_{22} = \begin{bmatrix} 0 & 1 \\ -1 & 2 \end{bmatrix} \to s^2 - 2s + 1 = (s-1)^2$.

Since $F_{22}$ is a scalar it has a single eigenvalue.
If $F_{22} = [-1]$ then $\Delta_{F+gK}(s) = (s+1) \dots$ and $p(s)$ is a multiple of it.
Otherwise $F_{22} = [1] \implies$ problem is solvable? No, wait.
If $F_{22}=1$ then non-reachable mode is unstable ($+1$) and we want target poly $(s+1)^3$ (all stable). We cannot change non-reach eigenvalue.
So if $F_{22}=1$, Problem is NOT solvable (unless target poly has root 1, which $(s+1)^3$ does not).

To check what is $F_{22}$ (it's only eigenvalue) we use the PBH Test and evaluate $\text{rank}[\lambda I - F | g]$ for $\lambda = -1$.

$$
\text{rank}[F+I | g] = \text{rank} \begin{bmatrix} 0 & 0 & 0 & 0 \\ 1 & 1 & 1 & 0 \\ 0 & -1 & 3 & 1 \end{bmatrix} < 3
$$
(Rank is 2 because of first row 0).

$\implies \lambda = -1$ is the non-reachable eigenvalue.
$\implies F_{21} = [-1] \implies$ Problem is Solvable.
*(Wait, if rank drops at $\lambda=-1$, then $-1$ is the uncontrollable eigenvalue. Target poly is $(s+1)^3$, which has roots at $-1$. Since uncontrollable mode $-1$ matches target, it works!)*

Set $K = [a \ b \ c]$ Then:
$$F+gK = \begin{bmatrix} -1 & 0 & 0 \\ 1 & 0 & 1 \\ a & b-1 & c+2 \end{bmatrix}$$
*(Last row modified by $gK = [0 \ 0 \ 1]^T [a \ b \ c] = [0 \ 0 \ 0; 0 \ 0 \ 0; a \ b \ c]$)*

$\Delta_{F+gK}(s) = (s+1)^3$.

Must have char. polynomial equal to $(s+1)^2 = s^2+2s+1$ for the reachable part?
$\begin{bmatrix} 0 & 1 \\ -1 & -2 \end{bmatrix}$.

$K = [a \ | \ 0 \ | \ -4 ] \quad \forall a \in \mathbb{R}$.




















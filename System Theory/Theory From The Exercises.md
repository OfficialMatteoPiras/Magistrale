TODO: This is from the NL Exercises, need to add the part before it (From the review PDF)



----------

### Equilibrium points and stability analysis
#### Non linear state-space models
 In a general (nonlinear) state-space model three types of variables are involved:
- m scalar input variables, $u_1,u_2,...,u_m$ or, equivalently, an m-dimensional input vector
$$
u=\begin{bmatrix}u_1\\u_2\\...\\u_m\end{bmatrix}\in\mathbb{R}^m
$$
- p scalar output variables, $y_1,y_2,...,y_p$ or ,equivalently, ap-dimensional output vector
$$
y=\begin{bmatrix}y_1\\y_2\\...\\y_p\end{bmatrix}\in\mathbb{R}^p
$$
- n scalar state variables $x_1, x_2, ..., x_n$ or, equivalently, an n-dimensional state vector
$$
x=\begin{bmatrix}x_1\\x_2\\...\\x_n\end{bmatrix}\in\mathbb{R}^n
$$
A Non Linear ST SSM is described as follows:
$$
\Sigma \triangleq
\begin{cases}
x(t+1) = f(x(t),u(t)) \\
y(t) = h(x(t),u(t))
\end{cases}
\quad t \in \mathbb{Z}
$$
where: 
$$
\begin{align}
f:\mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^n \\
h:\mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^p 
\end{align}
$$
And, similarly, for a NL CT SSM we have:
$$
\Sigma \triangleq
\begin{cases}
\dot{x}(t) = f(x(t),u(t)) \\
y(t) = h(x(t),u(t))
\end{cases}
\quad t \in \mathbb{Z}
$$
#### Equilibrium Points 
Consider the **autonomous** time-invariant DT SSM:
$$
\begin{align}
x(t+1) = f(x(t)) \\
\text{[ or the CT SSM: } \dot{x}(t) = f(x(t)) \text{ ]}
\end{align}
$$
~={red}Definition \[ Equilibrium Point \]:=~
A state vector $x_e$ is an equilibrium point of the system above id, when the initial state is $x(0)=x_e \space \forall t \geq 0$ 

Clearly in the DT case $x_e$ is equilibrium point iff: $f(x_e) = x_e$
In the CT case, condition: $f(x_e) = 0$ is *necessary* to guarantee $x_e$ equilibrium point.

~={red}Definition \[Stable Equilibrium\]=~
Let $x_e$ be an equilibrium point for the DT system (DT or CT). We say tat $x_e$ is a *stable equilibrium point* if, $\forall \epsilon > 0$, $\exists \delta >0 \text{ st if } ||x(0) - x_e || < \delta$ then the evolution $x(t)$ starting from $x(0)$ satisfies for any $t\geq 0$ the inequality $||x(t)-x_e||<\epsilon$ 

~={red}Definition \[Attractive Equilibrium Point\]=~
The equilibrium point $x_e$ is an *attractive equilibrium point* if $\exists \bar{\delta} \text{ st if } ||x(0)-x_e||<\bar{\delta}$ then $\lim_{t\rightarrow +\infty} ||x(t)-x_e||=0$

#### Linearization Method
Consider a CT NL Autonomous system SSM: $\dot(x)(t) = f(x(t)) \space x\in\mathbb{R}_+ \space dim x = n$ 
Assume:
1) $x_e$ is an equilibrium point of the system
2) $f( )$ is CT with it's derivatives
Consider the linearized model:
$$
\frac{d}{dt}[\delta x(t)] = F\delta x(t) \quad F \triangleq \left. \frac{\partial f}{\partial t}   \right|_{x=x_e}
$$
 so:
* if $\forall \lambda \in \sigma(F)$ and $Re(\lambda)<0$ then $x_e$ is an *asymptotically stable equilibrium point*;
* if $\exists \lambda \in \sigma(F)$ and $Re(\lambda)>0$ then $x_e$ is an *unstable equilibrium point*;
* if $\nexists \lambda \in \sigma(F)$ with $Re(\lambda)>0$ but $\exists \lambda \in \sigma(F)$ with $Re(\lambda)=0$ then *this method gives me an answer*.

#### Stability of linear systems
~={red}Definition \[Hurwitz and Schur matrices\]=~
A matrix $F \in \mathbb{R}^{n \times n}$ is said to be **Hurwitz** if all its eigenvalues have negative real part. It is called **Schur** if all its eigenvalues have modulus smaller than 1.

The unforced evolution of a linear system, in both continuous and discrete time, is expressed as
$$x(t) = \Phi(t)x(0)$$
with $\Phi(t) = e^{Ft}$ in the continuous-time case and $\Phi(t) = F^t$ in the discrete-time case.

The following proposition summarizes the fundamental facts concerning the stability and convergence of the equilibrium points of a linear system.
![[image 11.png|Examples For Stability of Linear Systems]]

~={red}Proposition \[Convergence and stability of equilibrium points of linear systems\]=~
In a linear autonomous system:
1.  If the system has an attractive equilibrium point then it must necessarily be the origin. In this case the system cannot have any other equilibrium point, that is $X_e = \{0\}$;
2.  The equilibrium in the origin is attractive if and only if
    * in the continuous-time case the matrix $F$ is **Hurwitz**,
    * in the discrete-time case the matrix $F$ is **Schur**;
3.  If the origin is an attractive equilibrium then convergence is global;
4.  If the system has a stable equilibrium point, then any other equilibrium point has the same stability property;
5.  The equilibrium in the origin is stable if and only if
    * in the continuous-time case the matrix $F$ has all eigenvalues with real part which is non-positive and the eigenvalues with zero real part are simple roots of the minimal polynomial,
    * in the discrete-time case the matrix $F$ has all eigenvalues with modulus less or equal than 1, and the eigenvalues with modulus equal to 1 are simple roots of the minimal polynomial;
6.  If the origin is an attractive equilibrium point, then it is stable and hence also asymptotically stable.

------------

### Reachability and Controllability

#### Reachability for linear DT systems
Let $\Sigma = (F, G, H)$ be a linear *discrete-time* systems, defined as:
$$
\begin{align}
\Sigma &\triangleq
\begin{cases}
x(t+1) = Fx(t) + Gu(t) \\
y(t) = Hx(t) + Du(t)
\end{cases}
\\ \\
&\text{ where: } \\ &dim(x) =n; \\ &dim(u) =m; \\ &dim(y) =p;
\end{align}
$$
~={red}Definition \[Reachability of a System\]=~
Given $k\in\mathbb{Z}$; $k>0$ a state $x_f\in X = \mathbb{R}^n$ is said to be reachable at time t=k (equivalently in k steps) id $\exists u(0), ... ,u(k-1) \in U=\mathbb{R}^n$ that drives the state from $x(0)=0$ to $x(k)=x_f$  

If the initial state is zero, $x(0) = 0$, and if the applied input is:  $u(0), u(1), ..., u(k-1)$, the state that is reached at time k is:
$$
x(k) = x_f(k) = \sum_{i=0}^{k-1} F^{k-1-i}Gu(i) = \underbrace{[ G | FG | ... | F^{k-1}G ]}_{\triangleq \mathcal{R}_k} \begin{bmatrix}u(k-1) \\ u(k-2) \\ \vdots \\ u(0)\end{bmatrix} 
$$
where $R_k$ is the *reachability matrix at time k* (in k steps). It is clear that that, if we define $X^R_k$ as the set of states that are needed in k steps i.e. $X_k^R \triangleq x_f \in X = \{\mathbb{R} : \exists u(0),...,u(k-1)\text{ s.t. } x(0) \xrightarrow[u(0),...,u(k-1)]{} x(k) \}$ then: $X_k^R = Im(\mathcal{R}_k)$ is a vector subspace of the state space $X$, and as such it is called the k-step reachable (sub)space.  If $X^R_k = X$, namely if $rank(R_k) = n$, the system $\Sigma$ is reachable in k steps.

**In General:**
For every $k \in \mathbb{Z} \space k > 0 \space X_k^R \subseteq X_{k+1}^R$ 
In fact: $X_k^R = Im[ G | FG | ... | F^{k-1}G ] \subseteq Im[ G | FG | ... | F^{k-1}G | F^kG ] = X^R_{k+1}$

**Proposition**
1. if $X_k^R = X_{k+1}^R$ then $X_{k+1}^R = X_{k+2}^R$ ($\Rightarrow X_{k+i}^R = X_k^R \space \forall i \geq 0$)
2. if $\bar{k} \triangleq min\{k\in\mathbb{Z} \space k \geq 1 : X_k^R = X_{k+1}^R\}$ then $\bar{k}\geq n$
Consequently: $X_1^R \subset X_2^R \subset ... \subset \underbrace{X_\bar{k}^R = X_\bar{k+1}^R = ... = X = \mathbb{R}^n}_{X_k^R = X_n^R}$ 
#### First Reachability Criteria
$(F,G)$ is reachable iff $\underbrace{rank[G|FG|...|F^{n-1}G]}_{R} = n$
**Proposition:** if $\Sigma$ is a single input reachable system then $\bar{k}=n$
**Remark**
1. Let $A\in\mathbb{R}^{n\times n}$ matrix and $B\in\mathbb{R}^{n\times k}$ then $A(ImB) = Im(AB)$ 
2. Let $F\in\mathbb{R}^{n\times n}$ and $S$ a vector subspace of $X=\mathbb{R}^n$ then S is set to be F-invariant if $FS \subseteq S$ (In other words $\forall S \in S$, $Fs\in S$)
3. [~={red}Cayley-Hamilton’s Theorem=~] Given $F\in D^{n\times n}$ let $\Delta_F(z) = z^n+a_{n-1}z^{n-1}+...+a_0$ be it's characteristic polynomial (i.e. $det(zI_n-F)$) then $\Delta_F(z)$ is an annihilating polynomial of F, i.e.: 
$$
\Delta_F(z) = F^n+a_{n-1}F^{n-1}+...+a_1F+a_0I_n = 0_{n\times m} \Rightarrow F^n = -\sum_{i=0}^{n-1}a_i F^i
$$
**Proposition:** 
Given a pair $(F,G)$, $F\in \mathbb{R}^{n\times n}$ and $G\in\mathbb{R}^{n\times m}$, let: $X^R = Im[G|FG|...|F^{n-1}G]$ be it's reachable subspace then $X^R$ is the smallest F-invariant subspace of $X=\mathbb{R}^n$ including $I_D \sim G$

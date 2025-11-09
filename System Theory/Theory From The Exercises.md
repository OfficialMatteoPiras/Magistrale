TODO: This is from the NL Exercises, need to add the part before it (From the review PDF)

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
## Introduction
#### Optimization Problem
An optimization problem (or model) P can be generally expressed as:
$$
\begin{equation}
	\begin{cases}
		
		min(or \space max)f(x) \\
		S \space \rightarrow \space g_i(x) \leq b_i \space i=1,...,m  \\
		x\in D \rightarrow \space x_jGD_j \space j=1,...,k
	\end{cases}
\end{equation}
$$
where f(x) is a real-valued function on variables x, D is the domain of x, and S is a finite set of constraints. In general, x is a tuple ($x_1,...,x_n$), D is the cartesian product $D_1x···xD_n$, and it holds that $x_j \epsilon D_j$. Formally, a constraint $c\epsilon S$ is a function associated to a subset $x_c$ (the support, or scope, of c) of the variables and whose value can be either true (the constraint is satisfied) or false (the constraint is violated). 

In **mathematical optimization**, we usually assume that each individual domain $D_j$ is numeric, i.e., a subset of R, and constraints can be expressed in algebraic form as inequalities $g_i(x) \epsilon b_i$, for $i \epsilon 1,...,m$.

~={yellow}*Any $x \in D$ is called a solution of $P$. A solution that satisfies all constraints in $S$ is called a feasible solution. We denote the set of feasible solutions to an optimization problem $P$ as $F(P)$.
If the domain D is discrete, we talk about discrete optimization. I n addition, if D is finite, meaning that the set of solutions is finite, we talk about combinatorial optimization.*=~

A feasible solution x* is optimal if:
$$
f(x) \le f(x) \quad \forall x \in F(P)
$$
We denote x* as the best solution to the set of feasible solutions F(P).

>Note that the optimal solution is not necessarily unique

An optimization problem is infeasible if it has no feasible solution, i.e., if $F(P)=\emptyset$. It is called unbounded if there is no lower limit on f(x) for $x \in F(P)$.

#### Linear Programming (LP)
A linear program consists in the minimization of a linear function subject to a f inite list of linear constraints. In general we have the form:
$$
\begin{equation}
	\begin{cases}
		min \space c^Tx = \sum^{n}_{i=1}{c_j x_j} \\ 
		a_i^T x \sim b_i \quad i =1,...,m 
		\\ l_j \leq x_j \leq u_j \quad j=1,...,n
	\end{cases}
\end{equation}
$$
where $\sim \in{\leq,\geq,=}$; $l_j \in \mathbb{R} \cup {-\infty}$; and $uj \in \mathbb{R} \cup {+\infty}$. The domain of a single variable is thus an interval in $\mathbb{R}$.

#### Integer Linear Programming (MIP)
One of the fundamental restrictions of linear programming is its inability to model discrete decisions. This is remedied by integer linear programming, where objective function and constraints are still restricted to be linear, but we are allowed to require that some variables can only take an integer value within their interval. In general we have the form:
$$
\begin{equation}
	\begin{cases}
		LINEAR \space PROGRAMMING: \\
		min \space c^Tx = \sum^{n}_{i=1}{c_j x_j} \\ 
		a_i^T x \sim b_i \quad i =1,...,m \\ 
		l_j \leq x_j \leq u_j \quad j=1,...,n \\ \\
		NEW \space CONSTRAINT: \\
		x_j \in \mathbb{Z} \quad \forall j \in J \subseteq N = {1,...,n}
	\end{cases}
\end{equation}
$$
If J = N we have a pure integer program, otherwise we have a mixed integer linear program. Of course, if  $J=\emptyset$  we are back to linear programming.

#### Convex Optimization
The other direction in which we can extend linear programming is, obviously, nonlinearity. We must be cautious in this direction, though, as allowing arbitrary nonlinearities in the objective (and/or constraints), still gives an intractable problem. It turns out, however, that if we restrict to **convex functions** and constraints, then we can recover most (but not all) of the nice properties of LP, while still giving a very meaningful extension to the paradigm. In general we have the form:

$$
\begin{equation}
	\begin{cases}
		min \space f(x) \\ 
		g_i(x) \leq b_i \quad i =1,...,m \\
		l_j \leq x_j \leq u_j \quad j =1,...,n
	\end{cases}
\end{equation}
$$
where f(x) and all $g_i(x)$ are required to be convex functions.

~={yellow}Note that we can combine the two extensions (convexity and integrality), and obtain what is called mixed integer convex programming (or convex mixed integer nonlinear programming)=~

##### Example $\rightarrow$ Diet problem
Afarmer wants to determine the minimum cost diet for their animals, with the constraint that certain minimal nutritional requirements are met. There are n foods to choose from on the market, each with a unit cost $c_j$. The nutritional requirements consider m basic nutrients, each with a minimum quantity $b_i$. We finally denote with $a_{ij}$ the amount of nutrient i in a unit of food j. 
Data recap:
$$
\begin{aligned}
n &= \text{foods on the market} \\
c_j &= \text{unit cost for each food on the market} \\
m &= \text{basic nutrients} \\
b_i &= \text{minimum quantity of basic nutrients} \\
a_{ij} &= \text{the amount of nutrient } i \text{ in a unit of food } j
\end{aligned}
$$
Using variables $x_j$ to encode the amount of food j in the diet, the problem can be formulated as:
$$
\begin{aligned}
min \sum^{n}_{j=1}c_jx_j \\
\sum^{n}_{j=1}a_{ij}x_j \geq b_i \\
x_j \geq 0
\end{aligned}
$$
#### Knapsack problem
Let a set of n items be given, each with profit pj and weight $w_j$. We also have a container (the nominal knapsack) with capacity B. We want to find a subset of the items of maximum total profit that does not exceed the capacity of the container. Using binary variables $x_j$ with the following meaning:
$$
x_j =
\begin{cases} 
1 & \text{if item $j$ is selected} \\
0 & \text{otherwise}
\end{cases}
$$
the problem can be written as:
$$
\begin{aligned}
min \sum^{n}_{j=1}p_jx_j \\
\sum^{n}_{j=1}w_{j}x_j \geq B \\
x_j \in {0,1} \quad j = 1,...,n
\end{aligned}
$$
~={yellow}As such, the knapsack problem is a (binary) integer linear program.=~

#### Portfolio optimization
Suppose we have a portfolio of n di!erent assets. For each of them, we have the expected return $\mu_j$, usually obtained by averaging some historical data. The risk of the investment is encoded by the covariance matrix R of our assets, again obtained from some historical analysis. We want to optimize our portfolio, i.e., decide which percentage of our budget to allocate to each asset, in order to obtain at least a target average return $\rho$, at the minimum risk. Using continuous variables $x_j$ to encode the percentage of our budget to allocate to asset j, we get the model:
$$
\begin{aligned}
min \space x^TRx \\
\sum^n_{j=1} \mu_j x_j \geq \rho \\
\sum^n_{j=1} x_j = 1 \\
0 \leq x_j \leq 1 \quad j=1,...,n
\end{aligned}
$$
This is a convex optimization problem, as the covariance matrix is positive semidefinite by construction.

#### LQR
We have a discrete-time linear system described by state equations:
$$
x_{t+1} = Ax_t + Bu_t
$$
We assume starting conditions $x_0 = x_{init}$ and a finite horizon T. Inthis setting, we want to compute the control sequence $U=[u_0,...,u_{T-1}]$ such that:
- $x_0,x_1,...,x_T$ is small (good control); 
- $u_0,u_1,...,u_{T-1}$ is small (small effort);
We can assume matrix Q to be symmetric and positive semidefinite, while matrix R is symmetric and positive definite. Note that matrices Q and R act Again, we assume the matrices as relative weights to combine good control and small effort. 
Overall, this optimal control problem can thus be formulated as:
$$
\begin{align}
min \space J(U) = \sum^{T-1}_{t=0}(x_t^TQx_t + u_t^TRu_t) + x_t^TQx_T \\
x_{t+1} = Ax_t + Bu_t \quad t=0,...,T-1 \\
x_0 = x_{init}
\end{align}
$$
 By imposing simple bounds on the state and control variables:
 $$
 \begin{align}
	 \underline{x} \leq x \leq \bar{x} \\
	 \underline{u} \leq u \leq \bar{u} 
 \end{align}
 $$
This alone prevents the usage of the closed form described above, and requires the solution of the problem as a (convex) quadratic program. Another type of change is replacing the quadratic norm in the objective: for example, suppose that we want to minimize the $l_\infty$ norms of x and u.The optimization problem reads:
$$
\begin{align}
min \space ||X||_{\infty} + ||U||_{\infty} \\
x_{t+1} = Ax_t+Bu_t \quad \underline{x} \leq x \leq \bar{x}\\
x_0 = x_{init} \quad \underline{u} \leq u \leq \bar{u}
\end{align}
$$
with $X=[x_0,...,x_T]$. Despite its appearance, this can actually be formu lated as a linear program, because minimizing the ε↔ norm of a vector can be encoded in a linear problem with some artificial variables and constraints.

# Convexity
#### Affine Combinations
~={yellow}Given two points $x,y \in \mathbb{R}^n$, we call affne combination the point obtained as $y = \sigma_1x +\sigma_2y$ for any two multipliers $\sigma_1,\sigma_2 \in \mathbb{R}$  satisfying the condition $\sigma_1 + \sigma_2 = 1$. =~

The geometric interpretation of an affine combination is quite simple. By substituting $\sigma_2 = 1-\sigma_1$ in the equation defining y, we obtain:
$$
z=\sigma_1 x+ \sigma_2 y = \sigma_1 x + (1-\sigma_1) y = y + \sigma_1 (x-y)
$$
so the affine combinations of x and y lie on the line passing through them.
![[affine_line.png]]
In general, given m points $x_1,...,x_m \in \mathbb{R}^n$ and m multipliers $\sigma_1,...,\sigma_m \in \mathbb{R}$ such that $\sum^{m}_{i=1} \sigma_i = 1$, we call $\sum^{m}_{i=1} \sigma_i x_i$  their affine combination.

~={yellow}A set is affine it it contains any affine combination of its points.=~
![[Pasted image 20251009225716.png|400]]
~={yellow}Any affine set C can be expressed as $C = V +x_0$, where $x_0 \in C$ and V is a vector subspace. Where $x_0 \in \mathbb{C}$ and V is a vector subspace.=~ 
Since an affine set is just a translation of a linear space, it is also very natural to define the dimension of the affine set as the dimension of the corresponding subspace, i.e., dim(C)=dim(V).

~={yellow}Given an arbitrary set C, we define its affine hull as the set aff(C) of all points that can be obtained as affine combinations of elements of C.=~

![[affine examples.png|500]]

The relative interior of a set C is defined as the interior of C with respect to its affine hull aff(C). More formally:
$$
relint(C) = {x\in C | B(x,r) \cap aff(C) \subseteq C \space \text{for some} \space r>0}
$$

#### Convex Sets
~={yellow}Given two points $x,y \in \mathbb{R}^n$, we call convex combination the point obtained as $z = \sigma_1x + \sigma_2y$ for any two non-negative multipliers $\sigma_1,\sigma_2 \in \mathbb{R}_+$ satisfying the condition $\sigma_1+\sigma_2=1$.=~

We notice that the difference w.r.t. an affine combination is just that the multipliers are non-negative: from the geometrical point of view, this means that a convex combination is restricted to lie between x and y or, in other words, that the set of convex combinations is no longer described by the line passing through x and y, but rather the segment having x and y as endpoints.

![[convex line endpoint.png|200]]

Simple way to recognize a convex set:
![[Pasted image 20251009233900.png]]
In general, given m points $x_1,...,x_m \in \mathbb{R}^n$ and m non-negative multipliers $\sigma_1,...,\sigma_m \in \mathbb{R}_+$ such that $\sum^{m}_{i=1}\sigma_i = 1$, we call $z=\sum^{m}_{i=1}\sigma_i x_i$ their convex combination.

~={yellow}A set is convex iff it contains any convex combination of its points.=~

![[convex comb example.png]]

~={yellow}Given an arbitrary set C, we define its convex hull as the set conv(C) of all points that can be obtained as convex combinations of elements of C.=~

![[convex hull ex.png|450]]

The following sets are easily shown to be convex: 
- $\emptyset$ and $\mathbb{R}^n$ 
- any affine set (clearly!) 
- hyperplanes $\{x | a^T \in x = b\}$ for any $a \in \mathbb{R}^n$ , $a \neq 0, b \in \mathbb{R}$ 
- halfspaces $\{x | a^T \in x \leq b\}$ for any $a \in \mathbb{R}^n$ , $a \neq 0, b \in \mathbb{R}$  
- Euclidian balls: $B(x_c, r) = \{x| ||x-x_c|| \leq r\}$ 
	for any center $x_c \in \mathbb{R}^n$ and radius r>0
- ellipsoids: $\mathcal{E}(x_c, P, r) = \{x|(x-x_c)^T P^{-1}(x-x_c) \leq r\}$
	for any symmetric positive definite matrix $P \succ  0$, center $x_c \in \mathbb{R}_n$, and radius r>0.
- polyhedra $P = \{x | Ax \leq b,Cx = d\}$

![[Basic simple sets.png|300]]


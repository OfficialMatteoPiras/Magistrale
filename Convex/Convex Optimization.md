- [[#Introduction|Introduction]]
	- [[#Introduction#Optimization Problem|Optimization Problem]]
	- [[#Introduction#Linear Programming (LP)|Linear Programming (LP)]]
	- [[#Introduction#Integer Linear Programming (MIP)|Integer Linear Programming (MIP)]]
	- [[#Introduction#Convex Optimization|Convex Optimization]]
		- [[#Convex Optimization#Example -> Diet problem|Example -> Diet problem]]
	- [[#Introduction#Knapsack problem|Knapsack problem]]
	- [[#Introduction#Portfolio optimization|Portfolio optimization]]
	- [[#Introduction#LQR|LQR]]
- [[#Convexity|Convexity]]
	- [[#Convexity#Affine Combinations|Affine Combinations]]
	- [[#Convexity#Convex Sets|Convex Sets]]
	- [[#Convexity#Calculus of convex sets|Calculus of convex sets]]
	- [[#Convexity#Topological properties|Topological properties]]
	- [[#Convexity#Separation Theorem|Separation Theorem]]
	- [[#Convexity#Convex Functions|Convex Functions]]
	- [[#Convexity#Calculus of convex functions|Calculus of convex functions]]
- [[#Convex Programming|Convex Programming]]
	- [[#Convex Programming#Definition Vertex|Definition Vertex]]
	- [[#Convex Programming#Theorem (Minkowski Weyl)|Theorem (Minkowski Weyl)]]
		- [[#Theorem (Minkowski Weyl)#Corollary|Corollary]]
	- [[#Convex Programming#Proof|Proof]]
	- [[#Convex Programming#Standard form|Standard form]]
	- [[#Convex Programming#Bases|Bases]]
	- [[#Convex Programming#Theorem Bases: Vertex|Theorem Bases: Vertex]]
		- [[#Theorem Bases: Vertex#Proof|Proof]]

### Introduction
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

##### Example -> Diet problem
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

###  Convexity
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

#### Calculus of convex sets
Here is a list of the most common convexity-preserving operators:
1. ~={yellow}Intersection=~: Given an arbitrary family A of convex sets, their intersection $C= \bigcap_{a\in A}C_a$ is a convex set
	eg: te positive semidefinite con $S_{+}^{n} can be expressed as: $\bigcap_{z \neq 0}\{X\in S^n | z^T Xz \geq 0\}$
2. ~={yellow}Affine functions:=~ Let $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$ be an affine function, i.e., $f(x)=Ax+b$ for some $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$. ThenifS is a convex set, then so are:
	$$
	\begin{align}
	f(S)={f(x) | x \in S} \\
	f^{-1}(S)={x | f(x) \in S}
	\end{align}
	$$
3. ~={yellow}Product:=~ Given $C1 \subseteq \mathbb{R}^{n_1}$ and $C_2 \subseteq \mathbb{R}^{n_2}$ convex sets, their (cartesian) product $C_1 \times C_2 \subseteq \mathbb{R}^{n_1+n_2}$ is also convex. 
		![[product.png|300]]
4. ~={yellow}Linear combinations.=~ Given $M_1,...,M_k$ convex sets in $\mathbb{R}^n$ and arbitrary multipliers $\lambda_1,...,\lambda_k$ the set $\sum^{k}_{i=1}\lambda_i M_i$ is a convex set
5. ~={yellow}Projection=~: Let $S \in \mathbb{R}^m \times \mathbb{R}^n$ be a convex set. Then its projection $T =proj_{\mathbb{R}^m}(S) = \{x\in \mathbb{R}^m | (x,y) \in S \space \text{for some} \space y \in \mathbb{R}^n\}$ is a convex set
		![[Projection.png|300]]
	
#### Topological properties
For any subset $M \in \mathbb{R}^n$ we have the natural relations: $relint(M) \subseteq M \subseteq cl(M)$. However, the inclusions can be very non tight on pathological sets.

For convex sets, things are much nicer. In particular, if M is a convex set, then: 
- $relint(M)$, $int(M)$ and $cl(M)$ are all convex sets; 
- $M \neq \emptyset \rightarrow relint(M) \neq \emptyset$
- $cl(M)=cl(relint(M))$ 
- $relint(M)=relint(cl(M))$
~={yellow}If M is convex set, $x \in relint(M)$ and $y \in cl(M)$, then we have that the whole segment $[x,y) \subseteq relint(M)$.=~

#### Separation Theorem
~={green}Let C and D be non-empty convex sets that do not intersect ($C \subseteq D = \emptyset$). Then there exists a separating hyperplane, i.e., there exist $a \in \mathbb{R}^n$, $a \neq 0$ and $b \in R$, such that:
$$
\begin{align}
a^Tx\leq b \forall x \in C \\
a^Tx\geq b \forall x \in D
\end{align}
$$
In order to prove this fundamental result, we need a few intermediate lemmas.=~

**Lemma 1**
Let $A \subseteq \mathbb{R}^n$ be a non-empty set. Define the function $f : \mathbb{R}^n \rightarrow \mathbb{R}$ 
$$
f(x)=d(x,A)=\text{inf}_{y\in A} ||x-y||
$$
as the distance between a point x and the set A. Then f is continuous.

*Proof  lemma 1*
Let $x,y \in \mathbb{R}^n$ and $z \in A$. By definition of distance we have:
$$
d(x,A) \leq d(x,z) \leq d(x,y) + d(y,z)
$$
By taking the infimum w.r.t. $z \in A$ on both sides we get:
$$
\begin{align}
d(x,A) \leq d(x,y) + d(y,A) \\
d(y,A) \leq d(x,y) + d(x,A) 
\end{align}
$$
Now, combining the two we obtain:
$$
||d(x,A) - d(y,A)|| \leq d(x,y)
$$
As $d(x,y) \rightarrow 0$, so does $||f(x)-f(y)||$, and thus f is continuous.

**Lemma 2**
Let $A \in \mathbb{R}^n$ be a non-empty closed set, and let $y \notin A$. Then there exists $\bar{x} \in A$ at minimum distance, i.e.,
$$
d(y,A) = d(y,\bar{x}) \leq d(y,x) \forall x \in A
$$
*Proof lemma 2*
Since $A \neq \emptyset$ ,there exists $\hat{x} \in A \space \text{s.t.} \space d(y,A) \leq d(y,\hat{x})$. Now, let’s define the set: 
$$
A' = A \cap \{x|d(x,y) \leq d(y,\hat{x})\}
$$
Since A' is bounded and closed we can call it compact.
Note that by construction $d(y,A')=d(y,A)$. By definition A' is closed and bounded, while by the previous lemma $f(x)=d(x,A')$ is continuous: by the Weierstrass theorem it attains its minimum on A'.

![[lemma 2 separation theorem.png|300]]

**Lemma 3**
If C is a closed set and D is closed and bounded (i.e., compact), and both are non-empty, then there exist $x \in C$ and $y \in D$ such that $d(x,y)= d(C,D)$.

*Proof lemma 3*
Let $f : D \rightarrow R$ be defined as $f(z)=d(z,C)$. Since D is compact, and f is continuous, then again by Weierstrass there exists $y \in D$ such that $d(D,C)=d(y,C)$. By the previous lemma, since C is closed, there exists $x \in C$such that:
$$
d(x,y) = d(y,C) = d(C,D)
$$
![[Pasted image 20251010163352.png|300]]

**(Enanched) Separation Theorem**
Let C and D be non-empty closed convex sets that do not intersect, with one one of them being compact. Then there exists a separating hyperplane, i.e., there exists $a \in \mathbb{R}^n$,a ↘=0and $b \in R$, such that:
$$
\begin{align}
a^Tx \leq b \quad \forall x \in C \\
a^Tx \geq b \quad \forall x \in D
\end{align}
$$
The geometrical interpretation is given below.
![[Pasted image 20251010164025.png|300]]

*Proof*
Consider the set $C - D:$ this is a linear combination of two convex sets, and thus convex itself. Also, clearly 0 $0 \notin C - D$, as the sets do not intersect. Now, there are two cases:
$$
\begin{align*}
a &= d - c \\
b &= \frac{(d - c)^T (d + c)}{2} = \frac{||d||^2 - ||c||^2}{2}
\end{align*}
$$
case 1)  $C - D$ is closed. Thus, we can separate by Proposition above $C - D$ from $0$: let a be the corresponding hyperplane (clearly, we can pick $b = 0$).
$$
a^T(x-y) \leq 0 \quad \forall x \in C \quad \forall y \in D
$$
But then we can easily construct a separating hyperplane for C and D as: 
$$
a^Tx \leq \sup_{x\in C} a^Tx \leq \inf_{y \in D} a^Ty \leq a^Ty
$$
case 2) $C - D$ is not closed.
		a) If $0 \notin cl(C - D)$, then we can repeat the construction from the previous point and separate $0$ from $cl(C - D)$, and thus C from D.
		b) if $0 \in cl(C - D)$ 
				Consider a sequence of points ${x_k}\rightarrow 0$ converging to 0 from the outside of $cl(C - D)$ . Let then $y_k$ be the corresponding points of minimum This sequence always exists as 0 distance of xk w.r.t. $cl(C - D)$.  Each $x_k$ can be separated by $cl(C - D)$ for a geometrical representation of the construction. Define the normalized separating hyperplane vector as:
				$$
				a_k = \frac{y_k - x_k}{||y_k - x_k||}
				$$
				![[Pasted image 20251010170212.png|200]]

#### Convex Functions
A function $f : \mathbb{R}^n \rightarrow \mathbb{R}$ is convex if its domain $domf$ is a convex set and for all $x,y \in domf$ and for all $0 \leq \sigma \leq 1$ we have :
$$
f(\sigma x + (1-\sigma)y) \leq \sigma f(x) + (1-\sigma) f(y)
$$
![[Jensen’s inequality.png|300]]

There is a strong relation between convex sets and convex functions. An equivalent definition of convex function could indeed be: a function f is convex iff its epigraph 
$$
epif = {(x,t) \in \mathbb{R}^{n+1} | x \in domf, t \geq f(x)} 
$$
is a convex set.

~={yellow}A function $f : \mathbb{R}^n \rightarrow \mathbb{R}$ is concave if - f is convex.=~
Note that any affine function is both convex and concave.
We can give a list of basic functions that are easily shown to be convex by just using the definition. 
- $e^{ax}$ is convex on $\mathbb{R}$ for any $a \in \mathbb{R}$; 
- $x^a$ is convex on $R_{++}$ if $a \geq 1$ and $a \leq 0$, and concave if $0 \leq a \leq 1$;
- $|x|^p$ is convex on $\mathbb{R}$ for $p \geq 1$; 
- $log(x)$ is concave on $R_{++}$; 
- any norm on $\mathbb{R}^n$ is convex; 
- the max function $f(x) = max{x_1,...,x_n}$ is convex
#### Calculus of convex functions
As with convex sets, it is often more convenient to show a function to be convex by showing that it can be obtained from simpler convex functions through convexity-preserving operations. 
1. *Non-negative weighted sum*. Given $f_1,...,f_n$ convex functions and $\omega_1,...,\omega_n \geq 0$ non-negative weights, the function $f = \sum^{n}_{i=1}w_if_i$ is a convex function.
2. *Composition with affine mappings*. If $f : \mathbb{R}^n \rightarrow \mathbb{R}$ is a convex function, $A \in \mathbb{R}^{n\times m}$ and $b \rightarrow \mathbb{R}^n$. Then the composite function $g : \mathbb{R}^m \rightarrow \mathbb{R} = f(Ax+b)$ is a convex function.
3. *Pointwise maximum and supremum.* If $f_1$ and $f_2$ are convex functions, their pointwise maximum $f(x)=max\{f1(x),f2(x)\}$ is a convex function. This extends to any finite number of convex functions $f_1,...,f_k$, and even to infinitely many by taking the supremum. In other words, given an arbitrary family A of convex functions, then the pointwise supremum:
		$$
		g(x) = \sup_{a\in A} f_a(x)
		$$
	is a convex function.
	![[pointwise maximum and suprimum.png|300]]
4. *Partial minimization.* If f(x,y) is a convex function and C is a convex set, then $g(x)=\inf_{y\in C} f(x,y)$ is convex function.

### Convex Programming

It is a special case of convex programming that can be written as:
$$
\begin{cases}
&\min c^Tx\\
&a^T_ix \sim b_i\quad\qquad i=1\dots m\quad \sim\in\{\leq, =, \geq\}&\text{by necessity linear}\\
&l_j\leq x_j\leq u_j\qquad l_j\in \mathbb{R}\cup\{-\infty\}\quad u_j\in \mathbb{R}\cup\{+\infty\}&\text{linear}
\end{cases}
$$
$<$ and $>$ are not allowed, and since these are linear functions, it is possible to invert the function to find the maximum, as it remains linear.


It does not have many uses in itself, but it can be used to solve other types of problems.
- linear equality$\rightarrow$ hyperplane
- linear inequality $\rightarrow$ halfspace
- feasible region of a linear program is a polyhedron

polyhedron is the unbounded version of polytope.
#### Definition Vertex

A vertex is a point of the polyhedron that cannot be represented as a strict combination of the points of $P$.

Given a list of vertices, the unique polyhedron can be obtained.
![[polyhedron.png]]
#### Theorem (Minkowski Weyl)
Every point of the polytope can be expressed as a convex combination of its vertices.
This does not apply to polyhedrons.

In other words, a polytope can be described in two different ways:
- $H$: the intersection of its linear constraints
- $V$: its vertices
##### Corollary
If the feasible set $P$ of a linear program is bounded and non-empty, then there exists at least one optimal vertex.
#### Proof
- $x_1\dots x_k$ the vertices
- $y\in P$ an arbitrary feasible solution
- $z^*=\min \{c^T x^i : i=1\dots k\}$
$$
\begin{align}
c^Ty&=c^T\left(\sum_{i=1}^k\lambda_ix^i\right)\\
&=\sum_{i=1}^k\lambda_i(c^Tx^i)\geq\sum_{i=1}^k\lambda_iz^*\\
\end{align}
$$
- $\sum_{i=1}^k\lambda_i$ is equal to $1$ since we are in a special case of *convex program*
$$
c^Ty\geq z^*
$$
#### Standard form

$$
\begin{cases}
&\min c^Tx\\
&Ax=b\quad \text{no loss of generality}\\
&x\geq 0
\end{cases}
$$

- $a^Tx\geq b$ can be rewritten as $a^Tx+s=b$ at the cost of introducing a variable $s=b-a^Tx\geq 0$
- $x\geq g$ can be seen as $x-g\geq 0$
- A variable $x_j$ that has no restrictions can be expressed as two non-negative variables $x_j=x_j^+-x_j^-$ with $x_j^+,x_j^-\geq 0$

We can also say that the number of columns is greater than or equal to the number of rows in the matrix.$m\leq n$
This means that we have more variables than equations.
The matrix $A$ has $rank(A)=m$

#### Bases
A basis is defined as the set of $m$ linearly independent columns
- $\mathcal B=\{k_1,\dots,k_m\}$ the set of independent columns
- $B$ the matrix formed by the columns of the basis

- $\mathcal R$ the columns not present in the basis
- $R$ the matrix formed by the columns of $\mathcal R$

We can therefore rewrite the problem as:
$$
\begin {align}
Ax&=b\\
Bx_B+Rx_R&=b\\
B^{-1}(Bx_B+Rx_R)&=B^{-1}b\\
x_B&=B^{-1}b-BRx_R
\end{align}
$$
If $x_R =0$, we obtain
- *basic solution*: $x_B=B^{-1}b$
- *basic feasible solution*: if the non-negativity constraint is also satisfied
#### Theorem Bases: Vertex

A point $x\in\mathbb R^n$ is the vertex of a non-empty polyhedron
$$P=\{x|Ax=b,x\geq0\} \iff x \text{ is a b.f.s. of the system } Ax=b$$
##### Proof
- $x$ is a b.f.s. associated with a basis $B$
- it is a set of variables (not vectors)
- we can permute $B$ to obtain the positive values of $x$ on the first $k$ columns
$$
x=[x_1\dots x_k,0\dots 0]^T
$$
- since $k<m$ a variable of the basis can be 0. When this happens, we say that the basis is *degenerate*

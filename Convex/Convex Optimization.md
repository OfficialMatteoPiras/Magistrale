### Optimization Problem
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

### Linear Programming (LP)
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

### Integer Linear Programming (MIP)
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

### Convex Optimization
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

#### Example $\rightarrow$ Diet problem
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
### Knapsack problem
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

### Portfolio optimization
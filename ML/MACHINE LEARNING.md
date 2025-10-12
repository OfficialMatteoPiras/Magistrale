- [[#Introduction|Introduction]]
- [[#Componets of learning:|Componets of learning:]]
- [[#A gentle start|A gentle start]]


#### Introduction
Machine Learning $\rightarrow$ model to predict what comes next by using tokens (tokens $\equiv \mathbb{R}$ numbers / vectors created from a word)
Train (using data) requires a lot deference and clusters of GPU for the comparational cost of training
You cannot trust the answer from a bet apart from particular faccias
Machine (statistical) learning provides extremely useful framework and set of tools to tackle decisions margin (control!) base under
Limited information provided by measured data.

![[Pasted image 20251012160629.png]]

A toolset to "learn" is to assign tasks from measured data following the path: 
~={yellow}Prediction-classification- reinforcement learning-decision in general:
=~
![[Pasted image 20251012160926.png]]

#### Componets of learning:

Input: $x \in X (=\mathbb{R}^d)$ [vector of p values from which we want to predict]
Output: $y \in Y$ [value to predict]
Target Function: $f:X \rightarrow Y$ [formula we would like to learn]
Data:  $(x_1,y_1),...,(x_n,y_n) \in S \rightarrow S=\{z_i=(x_i,y_i) \space i=1,...,n\}$ where S is the *sample set*

~={orange}Hypothesis: $H: X\rightarrow Y$ [formula to be used]=~
Model Classes H ($h \in H$)

Training set (eg iid samples from distribution D), each couple $(x_i, y_i)$ comes fram a different distribution
We want to mesure the frequency of an even (how many times  does it repeats)
I Need a general rule for each sample $\rightarrow$ *Identical Distribution*
We can relax the identical assuptico by increasing the difficucty of the distribution
 Distribution: way to generare data

Rule we decide that belonges to a class of certain set

![[Pasted image 20251012165301.png]]
![[Pasted image 20251012165316.png]]

Goal: the "learned" function h(x) (or for more accurancy $\hat{h}$) should perform well on future unseen data $\equiv$ *"Generalized"*
The learning algorithm should be able to trade off: 
- Available data (quality – quantity) 
- Hyphothesis class (rich or limited)
In order to give *GUARANTEES* on the performance on *FUTURE UNSEEN DATA*

$y_i$’s are known: training set $(x1,y1),(x_2,y_2),…,(x_N,y_N)$ supervised learning $y_i$’s are not known: training set $x_1,x_2,…,x_N$ unsupervised learning.

There can be different types of output: 
- Y is *discrete* 
- Y is *continuous*
![[Pasted image 20251012165902.png|433x251]]
![[Pasted image 20251012165938.png|433x267]]

#### A gentle start
**Binary Classification**
Inputs: $x \in X (=\mathbb{R^d})$  is the *domani set*
Outputs: $y \in Y \rightarrow \{0,1\}$ 
Training set: $S=\{z_i=(x_i,y_i) \space i=1,...,n\}$ 

Assumption on data:
$x \thicksim D_x$ 
$y|x \thicksim D_{y|x}$
$$
p(y|x) = 
\begin{cases} 
1 \quad if \space y=f(x) \\
0 \quad if \space y \neq f(x)
\end{cases}
$$
**Loss (Error) Function**
$$
l(h,z) \geq 0 \quad h \in H \quad h(x) \simeq y
$$
Measure how good is the function h to describe the data point $z = (x,y)$.
For binary classification $Y=\{0,1\}$ a very common loss function is the so called *0-1 Loss*, described as follows:
$$
l(h,z) =
\begin{cases}
1 \quad if \space h(x) \neq y \\
0 \quad if \space h(x) = y
\end{cases}
$$
The larger the loss, the worst my hypothesis works

**Empirical Loss (Risk)**
$$
L_S(h) = \frac{1}{n}\sum^n_{i=1}l(h,z_i) \quad h \in H \quad S=\{(x_i, y_i) \space i=1,...,n\}
$$
This is the training error.
Note that $\frac{1}{n}$ is just the fraction over the number of elements in the training set

**Algorithm ERM: Empirical Risk Minimization**
Given:
$$
\begin{align}
A(s) & \longmapsto h \in H \\
s.t. \\
h: x \in X & \longmapsto y \in Y
\end{align}
$$
where H is as always the hypothesis class. 
The ERM is the empirical minimization of the risk, described as:
$$
\hat{h}_S \in argmin_{h\in H} L_s(h)
$$
and ~={yellow}$\hat{h}_s$ is the "estimate" of h ("good") that can be computed only using data in S.=~

![[image-2.png|303x172]]

**True Risk**
This is the generalization error:
$$
L_D(h) = \mathbb{E}_D [l(h,z)]
$$
Developing it leads to:
$$
\begin{align}
L_D(h) & = \mathbb{E}_D [l(h,z)] = 1\times[\mathbb{P}[l(h,z)]=1]+ 0 \times[\mathbb{P}[l(h,z)]=0] = \\ 
&= 1\times[\mathbb{P}[l(h,z)]=1] = \mathbb{P}[\text{h incorrectly classifies z}]
\end{align}
$$

**Example:**
![[image-4.png|605x175]]

New rule:
$$
l(h,z) =
\begin{cases}
1 \quad \text{if } x_i \text{ for some i such that } y_i = 1\\
0 \quad \text{ otherwise}
\end{cases}
$$

Erm doesn't tell us which B to choose just the best set of B's.
$$
\begin{align}
L_D(\hat{h}_S) &= \mathbb{E}_D [l(\hat{h}_S,z)] = 1\times[\mathbb{P}[l(\hat{h}_S,z)]=1]+ 0 \times[\mathbb{P}[l(\hat{h}_S,z)]=0] = \\ 
&= \mathbb{P}[x\in A] = \mathbb{P}[\hat{h}_S \space \text{classifies a given data point incorrectly}] = \\
&= \frac{1}{2}
\end{align}
$$
We cannot compute this cause the *uncertainty is maximised*.
The alternative is to restrict the freedom of choosing B:
![[image-5.png|288x223]]

**Realizability**
A model class H saturize the realizability assumption (under distribution D)
$$
\exists h* \in H s.t. L_D(h*)=0 \rightarrow L_S(h*)=0 \text{ with probability } \rightarrow min_{h \in H}L_S(h)=0
$$
~={yellow}every data generated (inside $B_x$) the ERM referes to the B choosen.=~

**Theorem -> Binary Class Problems**
Consider a binary classification problem with 0-1 loss. Given a finite model class H and assume that $\exists h* \in H \text{ s.t. }L_D(h*)=0$ (real assumpions holds). $S=\{z_1,...,z_m\} \space z_i \thicksim D$ iid.

If $m>m_H(\epsilon, \delta) =\frac{1}{\epsilon}log(\frac{|H|}{\epsilon}) \longrightarrow$ |H| is the number of elements in the set H
where $\hat{h}_S=argmin_{h\in H}L_S(h)$
then $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$

 This means that if the equation is satisfied, then the rule has an error greater than $\epsilon$  con una probabilità minore di $\delta$.
#### Uniform Convergence & Agnostic PAC-Learning

- [[#Introduction|Introduction]]
- [[#Componets of learning:|Componets of learning:]]
- [[#A gentle start|A gentle start]]
	- [[#A gentle start#Binary Classification|Binary Classification]]
	- [[#A gentle start#Loss (Error) Function|Loss (Error) Function]]
	- [[#A gentle start#Empirical Loss (Risk)|Empirical Loss (Risk)]]
	- [[#A gentle start#Algorithm ERM: Empirical Risk Minimization|Algorithm ERM: Empirical Risk Minimization]]
	- [[#A gentle start#True Risk|True Risk]]
	- [[#A gentle start#Example:|Example:]]
	- [[#A gentle start#Realizability|Realizability]]
	- [[#A gentle start#Theorem -> Binary Class Problems|Theorem -> Binary Class Problems]]
- [[#Binary Classification Problem with Fine Model Classes|Binary Classification Problem with Fine Model Classes]]
- [[#Uniform Convergence & Agnostic PAC-Learning|Uniform Convergence & Agnostic PAC-Learning]]
	- [[#Uniform Convergence & Agnostic PAC-Learning#Main Steps to Follow|Main Steps to Follow]]


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
##### Binary Classification
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
##### Loss (Error) Function
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

##### Empirical Loss (Risk)
$$
L_S(h) = \frac{1}{n}\sum^n_{i=1}l(h,z_i) \quad h \in H \quad S=\{(x_i, y_i) \space i=1,...,n\}
$$
This is the training error.
Note that $\frac{1}{n}$ is just the fraction over the number of elements in the training set

##### Algorithm ERM: Empirical Risk Minimization
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

![[image-2 1.png|303x172]]

##### True Risk
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

##### Example:
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

##### Realizability
A model class H saturize the realizability assumption (under distribution D)
$$
\exists h* \in H s.t. L_D(h*)=0 \rightarrow L_S(h*)=0 \text{ with probability } \rightarrow min_{h \in H}L_S(h)=0
$$
~={yellow}every data generated (inside $B_x$) the ERM referes to the B choosen.=~

##### Theorem -> Binary Class Problems
Consider a binary classification problem with 0-1 loss. Given a finite model class H and assume that $\exists h* \in H \text{ s.t. }L_D(h*)=0$ (real assumpions holds). $S=\{z_1,...,z_m\} \space z_i \thicksim D$ iid.

If $m>m_H(\epsilon, \delta) =\frac{1}{\epsilon}log(\frac{|H|}{\epsilon}) \longrightarrow$ |H| is the number of elements in the set H
where $\hat{h}_S=argmin_{h\in H}L_S(h)$
then $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$

 This means that if the equation is satisfied, then the rule has an error greater than $\epsilon$  con una probabilità minore di $\delta$.
#### Binary Classification Problem with Fine Model Classes
Binary classification: $Y={0,1}$ and $l(h,z)=0-1$ loss
Fine Model Classes: $H={h_1, ..., h_k}$ with $h\in |H|$
Conditions on training data set: $S=\{z_i \space i=1,...,n\} \text{ s.t. } \hat{h} \in argmin_{h\in H}L_s(h)$
PAC-Learning: $\mathbb{P}[L_D(\hat{h}_s) \leq \epsilon] \geq 1-\delta \equiv (\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta)$ 
No risk -> reliability $min_{h}L_D(h)=0$

![[image 1.png|549x170]]

We want to prove that $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$
*remark:* $\hat{h}_S\in H$
Bad HP: $B=\{h\in H \text{ s.t. }L_D(h)>\epsilon\}$ (in the example above are B1 and B5, which are the extremes).

![[image-1 1.png|237x122]]

Choose $h \in B$ (eg B5) and call $M_h$ missleading data that could lead to choose h s.t. $L_S(h)=0$
$$
\begin{align}
\mathbb{P}[L_S(h)=0] &= \mathbb{P}[\frac{1}{m} \sum_{i=1}^{n}\mathbb{1}\{h(x_i) \neq y\}=0] = \quad \text{(no mistake on the training set)} \\
&= \mathbb{P}[S:h(x_i)=y_i \space \forall i=1,...,n] = \\
&= \prod_{i=1}^n\mathbb{P}[h(x_i)=y_i] \leq (1-\epsilon)^n
\end{align}
$$
*remark:* $L_D(h)>\epsilon$
and to find a bound we use:
$$
\mathbb{P}[(h(x)=y)>\epsilon] \rightarrow \mathbb{P}[h(x)=y]=1-\mathbb{P}[h(x)\neq y]<1-\epsilon
$$
*Prove that:* $\mathbb{P}[\exists h \in B, \space L_S(h)=0]$
$$
\mathbb{P}[\bigcup_{h\in B}\{S:L_S(h)=0\}] \leq \sum_{h\in B}[S:L_S(h)=0] \leq |B|e^{-\epsilon n} \leq |H|e^{-\epsilon n}
$$
*remark:* union bound: $\mathbb{P}[A_1 \cup A_2] \leq \mathbb{P}[A_1] + \mathbb{P}[A_2]$ 

$\mathbb{P}[L_D(\hat{h}_S)>\epsilon] \leq |H|e^{-\epsilon n}$ 
Our goal was find a condition on m s.t. $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$
Define $m*$ s.t. $|H|e^{-\epsilon m*}=\delta \rightarrow \frac{|H|}{\delta}e^{-\epsilon m*} \xrightarrow{\text{do the log and divide by delta}} m*=\frac{1}{\epsilon} log(\frac{|H|}{\delta})$
$\mathbb{P}[L_D(\hat{h}_S)>\epsilon] \leq |H|e^{-\epsilon m*} \quad \forall m \geq m* \leq \delta$

$m*=m_H(\epsilon, \delta) \equiv \text{ sample complexity of H }$ (in the book: $\leq m* = \frac{1}{\epsilon}log(\frac{|H|}{\delta})$) 
**$1^{st}$ relaxation** 
a bit more general: agnostic PAC-Learning -> what happens if $min_{h \in H}L_D(H)>0$
*Question:* if $min_{h \in H}L_D(h)>0$ holds, can we hope to make $L_D(\hat{h}_S)<\epsilon \quad \forall\epsilon>0$? 
*Answer:* **NO**
*Instead:*  Hope that $L_D(\hat{h}_S)<min_{h\in H}L_D(h) + \epsilon$ where $min_{h\in H}L_D(h) = L_D(h*)$ and $h* \in argmin_{h \in H}L_D(h)$

![[image-2 1.png]]
#### Uniform Convergence & Agnostic PAC-Learning
We would like to be able to make statements when realixation assumption *does not hold*, i.e.
$$
\begin{align}
\underbrace{\min_{h \in \mathcal{H}} L_D(h)}_{=L_D(h*)}> 0 \\
\text{where }h^* \in \arg\min_{h \in \mathcal{H}} L_D(h) \\
\end{align}
$$

so we can conclude that: 
$$
L_S(h) = \frac{1}{m}\sum_{i=1}^{m}l(h,z_i)
$$
our goal is to guarantee that $L_D(\hat{h}_S)$ is as close as possible to $L_D(h*) + \epsilon$
the lower bound is trivial: $L_D(\hat{h}_S) < L_D(h*) + \epsilon$
If:
$$
m>\frac{2}{\epsilon^2}log(2\frac{|H|}{\delta})
$$
than we can clearly see the form:
$$
\mathbb{P}[L_D(\hat{h}_S > L_D(h*) + \epsilon)] < \delta
$$
or equivalently: $\mathbb{P}[L_D(\hat{h}_S < L_D(h*) + \epsilon)] > 1- \delta$

##### Main Steps to Follow
1. Question: can we guarantee that $\forall h\in H \space |L_S(h)-L_D(h)| < \epsilon$?
	![[image 2.png|312x243]]
2. if so, we can guarantee that: $L_D(\hat{h}_S)<min_hL_D(h) + \epsilon$
3. Give probabilistic guarantees on the stament above ($\forall h\in H \space |L_S(h)-L_D(h)| < \epsilon$)

*Step 1)* \[$\epsilon$ representative\]
Definition $\epsilon-\text{representative sample}$:
We say that $S=\{z_i, \space i=1,...,n\}$ is $\epsilon-\text{representative}$ if $|L_S(h)-L_D(h)|<\epsilon \quad \forall h \in H$

*Step 2)*
[Lemma]  
We show that if S is $\frac{\epsilon}{2}-\text{representative}$ then $L_D(\hat{h}_S)<L_D(h*) + \epsilon$ 
[Proof] 
if S is $\frac{\epsilon}{2}-\text{representative}$  than:
$$
\begin{align}
L_D(\hat{h}_S) - L_D(h*) & \leq \frac{\epsilon}{2} \\
\rightarrow L_D(\hat{h}_S) & \leq L_S(\hat{h}_S) + \frac{\epsilon}{2} \\
& \leq L_S(h*) + \frac{\epsilon}{2} \\
& \leq L_D(h*) + \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
& = L_D(h*) + \epsilon \\
\end{align} 
$$
![[image 3.png|161x79]]

*Step 3)*
With which probability is S $\epsilon-\text{representative}$? (Probability in which we get a representative data set)
In other words: give conditions under which 
$\mathbb{P}[\text{S is }\epsilon-\text{representative}]>1-\delta \equiv \mathbb{P}[|L_S(h) - L_D(h)|<\epsilon, \space \forall]>1-\delta \equiv$ uniform convergence

**Refresh of probability**
$L_S(h) = \frac{1}{m} \sum_{i=1}^m \underbrace{l(h,z_i)}_{w_i} \rightarrow w_i \sim D \text{ iid } \mu=\mathbb{E}[w_i]=p$ 
$\hat{\mu}_m = \frac{1}{m}\sum_{i=1}^{m}w_i \xrightarrow[\text{LLN}]{m\rightarrow \infty} \mu=\mathbb{E}[w_i]=p \space (=\mathbb{E}[l(h,z)]=L_D(h))$  

So, by using the concept above, we can conclude that:
$$
\begin{align}
\mathbb{P}[|\hat{\mu}_m - \mu|>\epsilon] &\underset{\text{chivicev inequality}}{<} \frac{\sigma_{\mu m}^2}{\epsilon^2} \\
\sigma_{\hat{\mu} m}^2 = \frac{m\text{Var}\{w\}}{m^2} &= \frac{\text{Var}\{w\}}{m} \\
\Rightarrow \mathbb{P}[|\hat{\mu}_m - \mu|>\epsilon]&<\frac{c}{m}
\end{align}
$$

**Refresh of probability**
Given x,y s.t. $\mathbb{E}(x) = \mathbb{E}(y) = 0$ and $Var(x+y)=\mathbb{E}[(x+y)^2]=\mathbb{E}[x^2+y^2+2xy]=\underbrace{\mathbb{E}[x^2]}_{Var(x)} + \underbrace{\mathbb{E}[y^2]}_{Var(y)} + \underbrace{2\mathbb{E}[xy]}_{= \space 0 \space \text{(if x,y uncorr.)}}$
we can conclude that: $Var(ax) = a^2Var(x)$ if a=const $\in \mathbb{R}$
##### Uniform Convergence
*Question*: can we guarantee that
$\mathbb{P}[\forall h, |L_s(h) - L_D(h)| < \epsilon]>1-\delta$ = same number of data m $\forall h \in H$
![[image.png|315x144]]

**Proposition:** if $m>\frac{1}{2\epsilon^2}log(2\frac{|H|}{\delta})$ then $\mathbb{P}[\exists h | L_S(h)-L_D(h)|>\epsilon]<\delta$ where $\delta = 2e^{-m^*\epsilon^2}$
To do the proof we need these two results:
1. *Hoeffding Lemma:* 
	Let x random value, $x \in [a,b]$ (with probability 1), i.e. $x=\mu$, then: 
	$\mathbb{E}[e^{t(x-\mu)}] \leq e^{\frac{t^2(b-a)^2}{2}}$ 
2. *Hoeffding Inequality:*
	Let $x_i$ iid random variables and $\mathbb{E}(x_i)=\mu$ then:
	1. $\mathbb{P}[\sum_{i=1}^{m}x_i - m\mu > \epsilon] < e^{\frac{2\epsilon^2}{m(b-a)^2}}$
	2.  $\mathbb{P}[|\sum_{i=1}^{m}x_i - m\mu| > \epsilon] < 2 e^{\frac{2\epsilon^2}{m(b-a)^2}}$
**Proof**

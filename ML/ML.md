
## Introduction
### Gentle Start
**Binary Classification**
Inputs: $x \in X (=\mathbb{R^d})$  is the *domain set*
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
**Loss Function**
> [!success] formula:
> $$
l(h,z) \geq 0 \quad h \in H \quad h(x) \simeq y
$$

Measure how good is the function h to describe the data point $z = (x,y)$.
For binary classification $Y=\{0,1\}$ a very common loss function is the so called *0-1 Loss*, described as follows:

> [!success] formula:
> $$
l(h,z) =
\begin{cases}
1 \quad if \space h(x) \neq y \\
0 \quad if \space h(x) = y
\end{cases}
$$

The larger the loss, the worst my hypothesis works.

**Empirical Loss -> Risk**
> [!success] formula:
> $$
L_S(h) = \frac{1}{n}\sum^n_{i=1}l(h,z_i) \quad h \in H \quad S=\{(x_i, y_i) \space i=1,...,n\}
$$

This is the training error.
Note that $\frac{1}{n}$ is just the fraction over the number of elements in the training set

**ERM (Empirical Risk Minimization)**
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
> [!success] formula:
> $$
\hat{h}_S \in argmin_{h\in H} L_s(h)
$$

and ~={yellow}$\hat{h}_s$ is the "estimate" of h ("good") that can be computed only using data in S.=~

**True Risk**
This is the generalization error:
$$
L_D(h) = \mathbb{E}_D [l(h,z)]
$$
Developing it leads to:

> [!success] formula:
> $$
\begin{align}
L_D(h) & = \mathbb{E}_D [l(h,z)] = 1\times[\mathbb{P}[l(h,z)]=1]+ 0 \times[\mathbb{P}[l(h,z)]=0] = \\ 
&= 1\times[\mathbb{P}[l(h,z)]=1] = \mathbb{P}[\text{h incorrectly classifies z}]
\end{align}
$$

**Realizability**
A model class H saturise the realizability assumption (under distribution D)
> [!success] formula:
> $$ \exists h* \in H s.t. L_D(h*)=0 \rightarrow L_S(h*)=0 \text{ with probability } \rightarrow min_{h \in H}L_S(h)=0 $$

~={yellow}every data generated (inside $B_x$) the ERM referes to the B choosen.=~

#### Theorem -> Binary Class Problems
> [!warning] Theorem
>Consider a binary classification problem with 0-1 loss. Given a finite model class H and assume that $\exists h* \in H \text{ s.t. }L_D(h*)=0$ (real assumpions holds). $S=\{z_1,...,z_m\} \space z_i \thicksim D$ iid.
>
>If $m>m_H(\epsilon, \delta) =\frac{1}{\epsilon}log(\frac{|H|}{\epsilon}) \longrightarrow$ |H| is the number of elements in the set H
>where $\hat{h}_S=argmin_{h\in H}L_S(h)$
>then $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$
>
 >This means that if the equation is satisfied, then the rule has an error greater than $\epsilon$  with a lower probability of $\delta$.
### Binary Classification Problem with Fine Model Classes
> [!info] Recall:
> 1) $\hat{h}_S\in H$ 
> 2) $L_D(h)>\epsilon$
> 3) union bound: $\mathbb{P}[A_1 \cup A_2] \leq \mathbb{P}[A_1] + \mathbb{P}[A_2]$ 

*Binary classification:* $Y={0,1}$ and $l(h,z)=0-1$ loss
*Fine Model Classes:* $H={h_1, ..., h_k}$ with $h\in |H|$
*Conditions on training data set:* $S=\{z_i \space i=1,...,n\} \text{ s.t. } \hat{h} \in argmin_{h\in H}L_s(h)$
*PAC-Learning:* $\mathbb{P}[L_D(\hat{h}_s) \leq \epsilon] \geq 1-\delta \equiv (\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta)$ 
No risk -> reliability $min_{h}L_D(h)=0$

![[image 1.png|549x170]]

We want to prove that $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$
Bad HP: $B=\{h\in H \text{ s.t. }L_D(h)>\epsilon\}$ 

![[image-1 1.png|237x122]]

Choose $h \in B$ (eg B5) and call $M_h$ misleading data that could lead to choose h s.t. $L_S(h)=0$
$$
\begin{align}
\mathbb{P}[L_S(h)=0] &= \mathbb{P}[\frac{1}{m} \sum_{i=1}^{n}\mathbb{1}\{h(x_i) \neq y\}=0] = \quad \text{(no mistake on the training set)} \\
&= \mathbb{P}[S:h(x_i)=y_i \space \forall i=1,...,n] = \\
&= \prod_{i=1}^n\mathbb{P}[h(x_i)=y_i] \leq (1-\epsilon)^n
\end{align}
$$
and to find a bound we use:
$$
\mathbb{P}[(h(x)=y)>\epsilon] \rightarrow \mathbb{P}[h(x)=y]=1-\mathbb{P}[h(x)\neq y]<1-\epsilon
$$
*Prove that:* $\mathbb{P}[\exists h \in B, \space L_S(h)=0]$
$$
\mathbb{P}[\bigcup_{h\in B}\{S:L_S(h)=0\}] \leq \sum_{h\in B}[S:L_S(h)=0] \leq |B|e^{-\epsilon n} \leq |H|e^{-\epsilon n}
$$
> [!success] formula:
> $\mathbb{P}[L_D(\hat{h}_S)>\epsilon] \leq |H|e^{-\epsilon n}$ 

Our goal was find a condition on m s.t. $\mathbb{P}[L_D(\hat{h}_S)>\epsilon]<\delta$
Define $m*$ s.t. $|H|e^{-\epsilon m*}=\delta \rightarrow \frac{|H|}{\delta}e^{-\epsilon m*} \xrightarrow{\text{do the log and divide by delta}} m*=\frac{1}{\epsilon} log(\frac{|H|}{\delta})$
$\mathbb{P}[L_D(\hat{h}_S)>\epsilon] \leq |H|e^{-\epsilon m*} \quad \forall m \geq m* \leq \delta$

$m*=m_H(\epsilon, \delta) \equiv \text{ sample complexity of H }$ (in the book: $\leq m* = \frac{1}{\epsilon}log(\frac{|H|}{\delta})$) 

**$1^{st}$ relaxation** 
a bit more general: agnostic PAC-Learning -> what happens if $min_{h \in H}L_D(H)>0$
> [!question]
> *Question:* if $min_{h \in H}L_D(h)>0$ holds, can we hope to make $L_D(\hat{h}_S)<\epsilon \quad \forall\epsilon>0$? 
> *Answer:* **NO**
> *Instead:*  Hope that $L_D(\hat{h}_S)<min_{h\in H}L_D(h) + \epsilon$ where $min_{h\in H}L_D(h) = L_D(h*)$ and $h* \in argmin_{h \in H}L_D(h)$

**Comparison Between $L_D(h)$  and  $L_S(h)$ **
![[image-2 1.png|553x314]]

### Uniform Convergence & Agnostic PAC-Learning
We would like to be able to make statements when relaxation assumption *does not hold*, i.e.
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
> [!note] Goal:
> Our goal is to guarantee that $L_D(\hat{h}_S)$ is as close as possible to $L_D(h*) + \epsilon$

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

**Main Steps**

> [!info] Recall:
> a) $L_S(h) = \frac{1}{m} \sum_{i=1}^m \underbrace{l(h,z_i)}_{w_i} \rightarrow w_i \sim D \text{ iid } \mu=\mathbb{E}[w_i]=p$ 
> b) Given x,y s.t. $\mathbb{E}(x) = \mathbb{E}(y) = 0$ and $Var(x+y)=\mathbb{E}[(x+y)^2]=\mathbb{E}[x^2+y^2+2xy]=\underbrace{\mathbb{E}[x^2]}_{Var(x)} + \underbrace{\mathbb{E}[y^2]}_{Var(y)} + \underbrace{2\mathbb{E}[xy]}_{= \space 0 \space \text{(if x,y uncorr.)}}$

> [!question]
> 1. *Question*: can we guarantee that $\forall h\in H \space |L_S(h)-L_D(h)| < \epsilon$?
> 2. if so, we can guarantee that: $L_D(\hat{h}_S)<min_hL_D(h) + \epsilon$
> 3. Give probabilistic guarantees on the stament above ($\forall h\in H \space |L_S(h)-L_D(h)| < \epsilon$)

*Step 1)* \[$\epsilon$ representative\]
> [!danger] Definition $\epsilon-\text{representative sample}$:
>We say that $S=\{z_i, \space i=1,...,n\}$ is $\epsilon-\text{representative}$ if $|L_S(h)-L_D(h)|<\epsilon \quad \forall h \in H$

*Step 2)*
>[!danger] Lemma  
> We show that if S is $\frac{\epsilon}{2}-\text{representative}$ then $L_D(\hat{h}_S)<L_D(h*) + \epsilon$ 

*Step 3)*
With which probability is S $\epsilon-\text{representative}$? (Probability in which we get a representative data set)
In other words: give conditions under which 
$\mathbb{P}[\text{S is }\epsilon-\text{representative}]>1-\delta \equiv \mathbb{P}[|L_S(h) - L_D(h)|<\epsilon, \space \forall]>1-\delta \equiv$ uniform convergence

$\hat{\mu}_m = \frac{1}{m}\sum_{i=1}^{m}w_i \xrightarrow[\text{LLN}]{m\rightarrow \infty} \mu=\mathbb{E}[w_i]=p \space (=\mathbb{E}[l(h,z)]=L_D(h))$ -> recall a 

So, by using the concept above, we can conclude that:
$$
\begin{align}
\mathbb{P}[|\hat{\mu}_m - \mu|>\epsilon] &\underset{\text{chivicev inequality}}{<} \frac{\sigma_{\mu m}^2}{\epsilon^2} \\
\sigma_{\hat{\mu} m}^2 = \frac{m\text{Var}\{w\}}{m^2} &= \frac{\text{Var}\{w\}}{m} \\
\Rightarrow \mathbb{P}[|\hat{\mu}_m - \mu|>\epsilon]&<\frac{c}{m}
\end{align}
$$we can conclude that: $Var(ax) = a^2Var(x)$ if a=const $\in \mathbb{R}$ -> recall b

**Uniform Convergence**
> [!question] 
> *Question*: can we guarantee that: $\mathbb{P}[\forall h, |L_s(h) - L_D(h)| < \epsilon]>1-\delta$ = same number of data m $\forall h \in H$

![[image 4.png|315x144]]

> [!danger] Proposition:
> if $m>\frac{1}{2\epsilon^2}log(2\frac{|H|}{\delta})$ then $\mathbb{P}[\exists h | L_S(h)-L_D(h)|>\epsilon]<\delta$ where $\delta = 2e^{-m^*\epsilon^2}$ (see proof below to understand this last relation)

To do the proof we need these two results:
1. *Hoeffding Lemma:* 
	Let x random value, $x \in [a,b]$ (with probability 1), i.e. $x=\mu$, then: 
	$\mathbb{E}[e^{t(x-\mu)}] \leq e^{\frac{t^2(b-a)^2}{2}}$ 
2. *Hoeffding Inequality:*
	Let $x_i$ iid random variables and $\mathbb{E}(x_i)=\mu$ then:
	1. $\mathbb{P}[\sum_{i=1}^{m}x_i - m\mu > \epsilon] < e^{\frac{2\epsilon^2}{m(b-a)^2}}$
	2.  $\mathbb{P}[|\sum_{i=1}^{m}x_i - m\mu| > \epsilon] < 2 e^{\frac{2\epsilon^2}{m(b-a)^2}}$
### Linear models & Classification Problem
![[image 5.png]]

#### Linear Models For Prediction
> [!info] Recall:
> *a)* The ERM is defined by:
> $$\begin{align} \hat{h}_S\in argmin_{h\in H}\underbrace{L_S(h)}_{=\frac{1}{m}\sum_{i=1}^{m}l(h,z_i)} &\rightarrow \hat{h}_{w,b}\in argmin_{h\in H}\frac{1}{m}\sum_{i=1}^{m}y-\underbrace{h(x_i)}_{w^Tx+b} \\ &\rightarrow \hat{h}_{\hat{w},\hat{b}}(x) = \hat{w}^Tx+\hat{b} \\ \text{ which brings us to }&\rightarrow \hat{w},\hat{b} \in argmin_{\substack{w\in\mathbb{R}^d \\ b\in \mathbb{R}}}\sum_{i=1}^{m}(y_i-w^Tx_i-b)^2 \end{align} $$
> *b)* To make the notation simpler:
>$$ \begin{align}\bar{x} &:= \begin{bmatrix}x\\1\end{bmatrix} \in \mathbb{R}^{d+1} \\ \bar{w} &:= \begin{bmatrix}w\\ b\end{bmatrix} \\ h_{w,b}(x) := w^Tx+b &= \begin{bmatrix}w^T & b\end{bmatrix}\begin{bmatrix}x\\1\end{bmatrix} = \bar{w}^T \bar{x} \end{align} $$
> To simplify notation $\bar{x}$ will be called $x$ and $\bar{w}$ will be called $w$.

Given $z_i=(x_i,y_i)$ where $x_i\in \mathbb{R}^d$ and $y_i\in \mathbb{R}$, and the class of model $H=\{h(x)=w^Tx+b, \space w\in\mathbb{R}^d, \space b\in\mathbb{R}\}$ we can defile the loss function (error on the "drawing" of the line / "the minimum distance point-line") as: $l(h,z) = (y-h(x))^2 = |y-h(x)|$ as the *square loss*

**Simple case**
Given: $w\in \mathbb{R}$ and $x_i\in \mathbb{R}$
such that: $L_S(w)=\frac{1}{m} \sum_{i=1}^{m}(y_i-wx_i)^2$

$$
\begin{align}
\text{given: } & x\in \mathbb{R} \\
\hat{w}_S &= argmin_{w\in \mathbb{R}}\frac{1}{m}\sum_{i=1}^{m}\underbrace{(y_i-w_xi)^2}_{y_i^2+w^2x_i^2-2y_iwx_i} \\
&\text{we can write } y_i^2+w^2x_i^2-2y_iwx_i \text{ as:}\\
\frac{1}{m}&[\sum_{i=1}^{m}y_i^2] + w^2[\frac{1}{m}\sum_{i=1}^{m}x_i^2] - 2[\frac{1}{m}\sum_{i=1}^{m}x_iy_i]w
\end{align}
$$
$\hat{w}_S$ is the unique solution to: $\frac{dL_S(w)}{dw}=0$
$$
\begin{align}
\frac{L_S(w)}{dw} &= \frac{1}{m}\sum_{i=1}^{m}2(y_i-wx_i)\underbrace{\frac{d}{dy}(y_i+wx_i)}_{x_i} = -\frac{2}{m}\sum_{i=1}^{m}(y_ix_i-w_ix_i^2) \\
\rightarrow & -\cancel{\frac{2}{m}}[\sum_{i=1}^{m}(y_ix_i) - w[\sum_{i=1}^{m}(x_i^2)] = 0 \\
\Rrightarrow & \hat{w}_S = (\sum_{i=1}^{m}(x_i^2))^{-1} \sum_{i=1}^{m}(y_ix_i) 
\end{align} 
$$

**General Case**
Given $x \in \mathbb{R}^d$ and $w \in \mathbb{R}^d$ such that:
$$
\hat{w}_S = argmin_{w\in\mathbb{R}^d} \frac{1}{m}(y_i-\underbrace{w^T}_{\begin{bmatrix}... & ... \end{bmatrix}}\underbrace{x_i}_{\begin{bmatrix}...\\...\end{bmatrix}})^2
$$
than $\nabla{w}L_S(w)=0$ is the minimum point $\hat{w}_S$ is the unique solution to this equation.
$$
\nabla{w}L_S(w)=\begin{bmatrix}\frac{\partial L_S}{\partial w_1}\\...\\\frac{\partial L_S}{\partial w_d}\end{bmatrix} = 0
$$
We need to compute:
$$
\begin{align}
\frac{\partial L_S}{\partial w_j} & = \frac{\partial}{\partial w_j}[\frac{1}{m}\sum_{i=1}^{m}(y_i-w^Tx_i)^2] = \\
&= \frac{1}{m}\sum_{i=1}^{m}2(y_i-w^Tx_i)\underbrace{-[[x_i]_j]}_{-\frac{\partial}{\partial w_k}(w^Tx_i)} \\
&= - \frac{2}{m}\sum_{i=1}^{m}(y_i-w^Tx_i)[x]_j
\end{align}
$$
By expanding this relation we can arrive to:
$$
\begin{align}
\nabla{w}L_S(w)&=\frac{2}{m}(\sum_{i=1}^{m}y_ix_i-(\sum_{i=1}^{m}x_ix_i^T)w) = \\
\Rrightarrow \underbrace{\nabla{w}L_S(w)}_{\in\mathbb{R}^d} &= -\frac{2}{m}[\underbrace{\sum_{i=1}^{m}y_ix_i}_{\in\mathbb{R}^d}-(\underbrace{\sum_{i=1}^{m}x_ix_i^T}_{\in R^{d\times d}})\underbrace{w}_{\in\mathbb{R}^d}]
\end{align}
$$
same computation with "vector-matrix" notation:
$$
Y=\begin{bmatrix}y_1\\...\\y_m\end{bmatrix} \in \mathbb{R}^n
\quad
X=\begin{bmatrix}x_1^T\\...\\x_m^T\end{bmatrix}\in \mathbb{R}^{m\times d}
$$
#### Errors
> [!info] Recall:
> $\begin{align}L_S(w)&=\frac{1}{m}\sum_{i=1}^{m}\underbrace{e^2_i}_{(y_i-x^2_iw)^2} = \frac{1}{m}(E^TE) = \frac{1}{m}(Y-Xw)^T(Y-Xw) = \frac{1}{m}[Y^TY-Y^TXw-w^TX^TY+w^TX^TXw] = \\ &= \frac{1}{m}[Y^TY-2w^TX^TY+w^TX^TXw]\end{align}$

Define $e_i\triangleq y_i-x_i^Tw$ and $E\triangleq \begin{bmatrix}e_1\\...\\e_m\end{bmatrix} = \begin{bmatrix}y_1-x_1^Tw\\...\\y_m-x_m^Tw\end{bmatrix} = \begin{bmatrix}y_1\\...\\y_m\end{bmatrix} -\begin{bmatrix}x_1^T\\...\\x_m^T\end{bmatrix}w$ with $w \in \mathbb{R}^d$
and doing so we have found the Y and X matrices written above. We can now rewrite the error equation as: 
$$
E\triangleq Y-Xw
$$
### Linear Models (Regression)
> [!info] Recall of the formulas needed:
> $$\begin{align} Y=\begin{bmatrix}y_1\\...\\y_m\end{bmatrix} \in \mathbb{R}^n &\quad X=\begin{bmatrix}x_1^T\\...\\x_m^T\end{bmatrix}\in \mathbb{R}^{m\times d} \quad w \in \mathbb{R}^d \quad h_w(x)=w^Tx = x^T w \\ E&=Y-Xw \quad E = \begin{bmatrix}e_1 \\ \vdots \\ e_m \end{bmatrix} \\ L_S(x) &= \frac{1}{m}[Y^TY-2w^TX^TY+w^TX^TXw] \end{align}$$

$$ \nabla_w L_S(w) = 0 \iff \underbrace{X^TY}_{b} = \underbrace{(X^TX)}_{A}w $$
that in general it hasn't an unique solution.
Now let's ask us some questions:

> [!info] Remarks 
> a) $X^TX \in \mathbb{R}^{d\times d}$
> b) since $b=X^TY$ and $A=X^TX$ where $b\in Im(X^T)=Im(X^TX)=Im(A)$

>[!question]  Rewriting the equation above as $b=Aw$ we cab as ourself some questions:
>1. Has it always a solution?
>2. Here is one solution or more than 1?
>3. How we find the/all the solutions
>*Answers:*
>	1) $\exists w \text{ s.t. } Aw=b \iff b\in ImA = Rang(A) = col \space span(A)$ column spans the entire space with and with the two considerations on the remark we can imply that exist at least one solution to $b=Ax$ (where $\nabla_wL_S(w)=0 \Rrightarrow b=Aw$)
>	2) Has $Aw=b$ an unique solution?
>	Say that $w^*$ is a solution, ie $b=Aw$. if $A=X^TX$ *is not* full rank, A not full rank means that $\exists \tilde{w}\neq 0 \text{ s.t. } A\tilde{w}=0$ (non space of a / $ker(A)$)
>	There is an entire space of $\tilde{w} \Rrightarrow \tilde{w}\in ker(A)$.
>	If $\begin{align}&w^* \text{ s.t. } b=Aw^* \\&\tilde{w} \text{ s.t. } b=A\tilde{w} \end{align}$ $\Rrightarrow b=A(w^*+\tilde{w}) \quad \forall\tilde{w}\in ker(A)$ 
>	Then $w^*+\tilde{w}$ is a solution $\forall \tilde{w} \in ker(A)$ 
>	3) how to find solution to $b=Aw$ when a is not full rank: 
>	(useful to find how sensitive my solutions are to perturbations )




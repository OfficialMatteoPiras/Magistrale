
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
> $$ l(h,z) \geq 0 \quad h \in H \quad h(x) \simeq y $$

Measure how good is the function h to describe the data point $z = (x,y)$.
For binary classification $Y=\{0,1\}$ a very common loss function is the so called *0-1 Loss*, described as follows:

> [!success] formula:
> $$l(h,z) = \begin{cases} 1 \quad if \space h(x) \neq y \\ 0 \quad if \space h(x) = y \end{cases}$$

The larger the loss, the worst my hypothesis works.

**Empirical Loss -> Risk**
> [!success] formula:
> $$ L_S(h) = \frac{1}{n}\sum^n_{i=1}l(h,z_i) \quad h \in H \quad S=\{(x_i, y_i) \space i=1,...,n\} $$

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
> $$ \hat{h}_S \in argmin_{h\in H} L_s(h) $$

and ~={yellow}$\hat{h}_s$ is the "estimate" of h ("good") that can be computed only using data in S.=~

**True Risk**
This is the generalization error:
$$ L_D(h) = \mathbb{E}_D [l(h,z)] $$
Developing it leads to:

> [!success] formula:
> $$ \begin{align} L_D(h) & = \mathbb{E}_D [l(h,z)] = 1\times[\mathbb{P}[l(h,z)]=1]+ 0 \times[\mathbb{P}[l(h,z)]=0] = \\ &= 1\times[\mathbb{P}[l(h,z)]=1] = \mathbb{P}[\text{h incorrectly classifies z}] \end{align} $$

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

----
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
$$\begin{align} \mathbb{P}[|\hat{\mu}_m - \mu| > \epsilon] &\underset{\text{Chebyshev inequality}}{\le} \frac{\sigma_{\hat{\mu} m}^2}{\epsilon^2} \\ \sigma_{\hat{\mu} m}^2 = \frac{m\text{Var}\{w\}}{m^2} &= \frac{\text{Var}\{w\}}{m} \\ \Rightarrow \mathbb{P}[|\hat{\mu}_m - \mu| > \epsilon] &\le \frac{c}{m} \end{align}$$we can conclude that: $Var(ax) = a^2Var(x)$ if a=const $\in \mathbb{R}$ -> recall b

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

-----
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

> [!tip] Summary
>
> This section formulates the **Empirical Risk Minimization (ERM)** problem for linear prediction. It begins by simplifying the notation, where the bias term $b$ is absorbed into the weight vector $w$ (by augmenting the feature vector $x$ with a $1$), allowing the hypothesis to be written simply as $h(x) = w^T x$.
>
>The goal is to minimize the **Square Loss** function $L_S(w)$, which represents the average squared difference between true labels and predictions. The notes derive the optimal solution through two approaches:
>
>1. **Simple Case (Scalar):** For 1-dimensional data ($x \in \mathbb{R}$), the optimal weight $\hat{w}_S$ is found by setting the derivative $\frac{dL_S}{dw}$ to zero, resulting in a closed-form solution based on scalar sums.
  >  
>2. **General Case (Vector):** For $d$-dimensional data ($x \in \mathbb{R}^d$), the solution is found by computing the gradient $\nabla_w L_S(w)$ (a vector of partial derivatives). This leads to an expression relating the sum of outer products $\sum x_i x_i^T$ and the weighted sum $\sum y_i x_i$.
  >  
>Finally, the formulation is translated into **Matrix Notation**. By defining the target vector $Y$, the design matrix $X$, and the error vector $E = Y - Xw$, the loss function is compactly expressed in terms of matrix operations ($E^T E$), setting the stage for solving the system using linear algebra.

-------
### Linear Models (Regression)
> [!info] Recall of the formulas needed:
> $$\begin{align} Y=\begin{bmatrix}y_1\\...\\y_m\end{bmatrix} \in \mathbb{R}^n &\quad X=\begin{bmatrix}x_1^T\\...\\x_m^T\end{bmatrix}\in \mathbb{R}^{m\times d} \quad w \in \mathbb{R}^d \quad h_w(x)=w^Tx = x^T w \\ E&=Y-Xw \quad E = \begin{bmatrix}e_1 \\ \vdots \\ e_m \end{bmatrix} \\ L_S(x) &= \frac{1}{m}[Y^TY-2w^TX^TY+w^TX^TXw] \end{align}$$

$$ \nabla_w L_S(w) = 0 \iff \underbrace{X^TY}_{b} = \underbrace{(X^TX)}_{A}w $$
that in general it hasn't an unique solution.
Now let's ask us some questions:

> [!info] Remarks 
> a) $X^TX \in \mathbb{R}^{d\times d}$
> b) Since $b=X^TY$ and $A=X^TX$ where $b\in Im(X^T)=Im(X^TX)=Im(A)$

>[!question]  Rewriting the equation above as $b=Aw$ we cab as ourself some questions:
>1. Has it always a solution?
>2. Here is one solution or more than 1?
>3. How we find the/all the solutions

*Answers:*
1) $\exists w \text{ s.t. } Aw=b \iff b\in ImA = Rang(A) = col \space span(A)$ column spans the entire space with and with the two considerations on the remark we can imply that exist at least one solution to $b=Ax$ (where $\nabla_wL_S(w)=0 \Rrightarrow b=Aw$)
2) Has $Aw=b$ an unique solution?
	Say that $w^*$ is a solution, ie $b=Aw$. if $A=X^TX$ *is not* full rank, A not full rank means that $\exists \tilde{w}\neq 0 \text{ s.t. } A\tilde{w}=0$ (non space of a / $ker(A)$)
	There is an entire space of $\tilde{w} \Rrightarrow \tilde{w}\in ker(A)$.
	If $\begin{align}&w^* \text{ s.t. } b=Aw^* \\&\tilde{w} \text{ s.t. } b=A\tilde{w} \end{align}$ $\Rrightarrow b=A(w^*+\tilde{w}) \quad \forall\tilde{w}\in ker(A)$ 
	Then $w^*+\tilde{w}$ is a solution $\forall \tilde{w} \in ker(A)$ 
3) how to find solution to $b=Aw$ when a is not full rank:  (useful to find how sensitive my solutions are to perturbations). The singular value decomposition (**SVG**) of a matrix $A\in\mathbb{R}^{n\times m}$
>[!danger] SVG (Singular Value Decomposition)
>$$ \begin{align} &\forall A \in \mathbb{R}^{n \times m} ; \quad \exists U \in \mathbb{R}^{n \times n} , V \in \mathbb{R}^{m \times m} , S \in \mathbb{R}^{n \times m} \\[10pt] &\text{WHERE } U^T U = U U^T = I_n ; \quad V^T V = V V^T = I_m \\[10pt]  &S = \left[ \begin{array}{ccc|c} \sigma_1 & & \varnothing & \varnothing \\ & \ddots & & \\ \varnothing & & \sigma_k & \\ \hline & \varnothing & & \varnothing \end{array} \right] \quad \sigma_1 \ge \sigma_2 \ge \dots \sigma_k > 0 \\[10pt] &\text{WHERE } k = \text{rank}(A) \quad \text{ST} \quad A = U S V^T \end{align}
$$


> [!info] Remarks:
> 1) $$U = \left[ \underbrace{U_1}_{k} \;\bigg|\; \underbrace{U_1^\perp}_{n-k} \right] \in \mathbb{R}^{n \times n} \qquad V = \left[ \underbrace{V_1}_{k} \;\bigg|\; \underbrace{V_1^\perp}_{m-k} \right] \in \mathbb{R}^{m \times m}$$
> $$S_1 = \begin{bmatrix} \sigma_1 & & \varnothing \\ & \ddots & \\ \varnothing & & \sigma_k \end{bmatrix} \in \mathbb{R}^{k \times k} \quad \text{CAUSE } S = \left[ \begin{array}{c|c} S_1 & \varnothing \\ \hline \varnothing & \varnothing \end{array} \right]$$
> 2) $$U_1^T U_1 \implies k \left\{ \underbrace{\begin{bmatrix} \cdots \cdots \end{bmatrix}}_{n} \right. \begin{bmatrix} \vdots \\ \vdots \end{bmatrix} = \begin{bmatrix} 1 & & \varnothing \\ & \ddots & \\ \varnothing & & 1 \end{bmatrix} = I_k$$ 
> $$U_1 U_1^T = \left[ U_1 \;\; U_1^\perp \right] \begin{bmatrix} U_1^T \\ (U_1^\perp)^T \end{bmatrix} = U_1 U_1^T + U_1^\perp (U_1^\perp)^T = I_n$$
>Rows are no longer orthonormal in this case

So by looking at the remarks above, we can conclude that:
> [!danger] USV matrix procedure:
> $$\begin{align*} A &= U S V^T \\ &= \left[ U_1 \; U_1^\perp \right] \left[ \begin{array}{c|c} S_1 & \varnothing \\ \hline \varnothing & \varnothing \end{array} \right] \begin{bmatrix} (V_1)^T \\ (V_1^\perp)^T \end{bmatrix} \\ &= \left[ U_1 S_1 \quad \varnothing \right] \begin{bmatrix} V_1^T \\ (V_1^\perp)^T \end{bmatrix} \\ &= U_1 S_1 V_1^T \end{align*}$$

Why Perp? $\quad \left[ \underbrace{u_1 \; u_2 \dots u_k}_{U_1} \;\bigg|\; \underbrace{u_{k+1} \dots u_n}_{U_1^\perp} \right] \quad u_i \in \mathbb{R}$
Cause all columns are orthogonal to $U_1$ so their span is the $U_1$ vector.

> [!tip] Summary
> This section establishes the mathematical framework for **Linear Regression**. It begins by defining the design matrix $X$, the target vector $Y$, and the parameters $w$ to formulate the **Squared Loss function** ($L_S$).
> 
>By minimizing the loss (setting the gradient $\nabla_w L_S$ to zero), we derive the **Normal Equation**, denoted as $b = Aw$ (where $A = X^TX$ and $b = X^TY$). The notes then analyze the properties of this system:
> - **Existence:** A solution always exists because $b$ lies within the column space of $A$.
> - **Uniqueness:** A unique solution exists only if $A$ is full rank. Otherwise, there are infinite solutions involving the kernel of $A$ ($\text{ker}(A)$). 
> 
> To address cases where $A$ is rank-deficient, the **Singular Value Decomposition (SVD)** is introduced. The matrix $A$ is decomposed into orthogonal matrices ($U, V$) and a diagonal matrix of singular values ($S$). By partitioning these based on the rank $k$, we derive the **compact SVD form** ($A = U_1 S_1 V_1^T$), separating the active subspaces ($U_1, V_1$) from the orthogonal complements ($U_1^\perp, V_1^\perp$) associated with the null space.
>
> *Explanation of lexical choices (for your convenience)*: 
>- *Design matrix*: This is the standard technical name for the matrix $X$ in machine learning. 
>- *Normal Equation*: This is the proper name for the equation $X^TXw = X^TY$. 
>- *Rank-deficient*: This is the English term for “not full rank.” 
>- *Kernel / Null space*: These are synonyms for the core of the matrix. 
>- *Compact SVD form*: This refers to the “reduced” version of the final formula $U_1 S_1 V_1^T$.
#### Geometric Interpretation of SVD

Given $A \in \mathbb{R}^{n \times m}$, $A$ can be thought as the matrix repr. of a linear transformation from $\mathbb{R}^m$ to $\mathbb{R}^n$.

$$
\begin{aligned}
\mathcal{L}(A) : \mathbb{R}^m &\longrightarrow \mathbb{R}^n \quad (\text{Linear}) \\
v &\longmapsto Av
\end{aligned}
$$

> [!question] **Question:** Which is the direction in $\mathbb{R}^m$ along which $\mathcal{L}(A)$ gives the "largest" amplification?

$$
\sup_{\substack{v \in \mathbb{R}^m \\ \|v\|=1}} \| Av \| = \sigma_1
$$

> [!info] Note
> $\sigma_1$ is the $1^{st}$ $\sigma_k$ in the upper left corner.

---
#### Better Overview Singular Value Decomposition (SVD)
**Singular Value Decomposition (SVD)**

> [!danger] Definition
> For any matrix $A \in \mathbb{R}^{n \times m}$:
> $$
> \begin{aligned}
> &\exists U \in \mathbb{R}^{n \times n} \quad \text{where } U^T U = U U^T = I_n \quad (\text{Orthogonal}) \\
> &\exists V \in \mathbb{R}^{m \times m} \quad \text{where } V^T V = V V^T = I_m \quad (\text{Orthogonal}) \\
> &\exists S \in \mathbb{R}^{n \times m} \quad \text{where } S = \left[ \begin{array}{c|c} S_1 & \varnothing \\ \hline \varnothing & \varnothing \end{array} \right], \quad S_1 = \begin{bmatrix} \sigma_1 & \varnothing \\ \varnothing & \sigma_k \end{bmatrix}
> \end{aligned}
> $$
> Where $k = \text{rank}(A)$.
> Such that:
> $$
> A = U S V^T \quad \text{or in reduced form} \quad A = U_1 S_1 V_1^T
> $$
> where $U = [U_1 | U_1^\perp]$ and $V = [V_1 | V_1^\perp]$.

**Geometric Interpretation**
Think of $A$ as the matrix representation of a linear transformation:
$$
\begin{aligned}
\mathcal{L}(A): \mathbb{R}^m &\longrightarrow \mathbb{R}^n \\
v &\longmapsto u = Av
\end{aligned}
$$

> [!question] Question
> Which is the direction in $\mathbb{R}^m$ along which $\mathcal{L}(A)$ gives the **"largest" amplification**?
> $$
> \underset{\substack{v \in \mathbb{R}^m \\ \|v\|=1}}{\text{argmax}} \| Av \| \equiv \underset{\substack{v \in \mathbb{R}^m \\ v \neq 0}}{\text{argmax}} \frac{\|Av\|}{\|v\|}
> $$
> *(Note: normalizing $v$ changes its length but not the direction)*

**Construction of the Matrices**
We try to find the matrices by satisfying the condition $A = U_1 S_1 V_1^T$ iteratively.

**Step (1): The First Dimension**
Find the vector $v_1$ that maximizes the amplification:
$$
v_1 := \underset{\substack{v \in \mathbb{R}^m \\ \|v\|=1}}{\text{argmax}} \| Av \|
$$
*Note: This might be a set of vectors, it's fine to choose one.*

> [!danger] Once we have $v_1$, we define:
>1.  $\sigma_1 := \| A v_1 \|$ (The amplification factor)
>2.  $u_1 := \frac{A v_1}{\| A v_1 \|} = \frac{A v_1}{\sigma_1}$ (The direction in the output space)

**Step (2): The Second Dimension**
I search in which direction my map amplifies the most, **excluding** the direction I already found ($v_1$).
$$
\text{argmax}_{\substack{v \in \mathbb{R}^m \\ v \perp v_1 \\ \|v\|=1}} \| Av \| = v_2
$$
Since it is orthogonal to $v_1$ (by constraint), we define:
$$
\sigma_2 := \| A v_2 \| \quad \text{and} \quad u_2 := \frac{A v_2}{\| A v_2 \|}
$$

> [!info] Remarks
> 1. $v_1 \perp v_2$ (by construction).
> 2. $\sigma_1 \ge \sigma_2$.
>    *Why?* Because $\sigma_k = \|A v_k\|$. Before finding $v_k$ we found $v_{k-1}$ which was the maximum of the entire space. When finding $v_k$ we added a constraint (orthogonality), so the maximum value can only decrease or stay equal.

**General Step**
We repeat this process for $k$ steps until the amplification is 0.
We obtain:
$$
\begin{cases}
u_1 \sigma_1 = A v_1 \\
u_2 \sigma_2 = A v_2 \\
\vdots \\
u_k \sigma_k = A v_k
\end{cases}
$$
With $V_1 = [v_1 \dots v_k]$ where $V_1^T V_1 = I$ (orthonormal columns).

**Matrix Assembly**
We can rewrite the system of equations in matrix form:
$$
[u_1 \sigma_1 \dots u_k \sigma_k] = [A v_1 \dots A v_k]
$$
$$
[u_1 \dots u_k] \begin{bmatrix} \sigma_1 & & \varnothing \\ & \ddots & \\ \varnothing & & \sigma_k \end{bmatrix} = A [v_1 \dots v_k]
$$
$$
\implies U_1 S_1 = A V_1
$$

To get the full SVD, we complete the matrices with their orthogonal complements (Kernels). Define $V := [V_1, V_1^\perp]$.
$$
[U_1 S_1 \quad \varnothing] V^T = A [V_1, V_1^\perp] V^T
$$
Since $V$ is orthogonal ($V V^T = I$), we conclude:
$$
U S V^T = A
$$

**Notation and Properties**

> [!info] Notation
> * $u_1 \dots u_k$: **Left** Singular Vectors
> * $v_1 \dots v_k$: **Right** Singular Vectors
> * $\sigma_1 \ge \dots \ge \sigma_k > 0$: **Singular Values**

**Kernel of A**
$\text{Ker}(A) = ?$
We have to find $v$ such that $Av = 0$.
Since $A = U S V^T$, and $U, S_1$ are full rank on their subspace, the zeros come from the "empty" part of $S$.
$$ v \in \text{span}(V_1^\perp) \quad (\text{The } n-k \text{ vectors orthogonal to } V_1) $$

**Image of A**
How do I repr. the Image of A?
$$\text{Im}(A) = \{ u \text{ s.t. } u = Av, \ v \in \mathbb{R}^m \}$$
Set of vectors that can be written as linear combinations of columns of $A$. Using the decomposition $u = U_1 S_1 V_1^T v$:
$$ \text{Im}(A) = \text{span}(U_1) $$

*Warning*
We haven't proved yet that $U_1^T U_1 = I_k$ (i.e., that the $u$ vectors generated by this method are orthogonal).
We can do it, but for now, **we trust the prof.**

> [!tip] Summary
> This section provides the **geometric intuition** behind SVD, viewing the matrix $A$ as a linear transformation $\mathcal{L}(A): \mathbb{R}^m \to \mathbb{R}^n$.
>
> The decomposition is constructed **iteratively** (a "greedy" approach):
> 1.  **First Component:** We identify the direction $v_1$ in the input space that yields the **maximum amplification** $\|Av\|$. This defines the first singular value $\sigma_1$ and the corresponding output direction $u_1$.
> 2.  **Subsequent Components:** We repeat the process for $k$ steps, searching for the direction of maximum amplification **orthogonal** to the previous ones ($v \perp v_{prev}$).
>
> This construction leads to the factorization $A = U S V^T$ and links the matrices to the fundamental subspaces of $A$:
> * **Singular Values ($\sigma$):** Represent the scaling factors, ordered $\sigma_1 \ge \sigma_2 \ge \dots \ge 0$.
> * **Right Singular Vectors ($V$):** The vectors corresponding to zero singular values ($V_1^\perp$) span the **Kernel** (Null Space).
> * **Left Singular Vectors ($U$):** The vectors corresponding to non-zero singular values ($U_1$) span the **Image** (Range).

---
### Back to Linear Regression
**Back to Linear Regression**

> [!info] Recall: Empirical Risk
> $$
> w \in \text{argmin} \underbrace{L_S(w)}_{\frac{1}{m} \|Y - Xw\|^2}
> $$
> Leading to the **Normal Equation**:
> $$
> (X^T X)w = X^T Y
> $$

> [!question] Problem
> **What if $X^T X$ is not invertible?**
>
> * Given $X \in \mathbb{R}^{m \times d}$ (where $m$ is points, $d$ is dim of space).
> * $\text{dim}(X^T X) \in \mathbb{R}^{d \times d}$.
> * **Case:** $\text{rank}(X) = k < d$.
>
> *Example:* If $d=2$, we need at least $m=2$ points to find a unique line/point. If we don't have enough data, the solution is not unique.

**1. SVD Decomposition**
$$
X = U S V^T \implies X = U_1 S_1 V_1^T
$$
Substituting this into $X^T X$:
$$
\begin{aligned}
X^T X &= (U_1 S_1 V_1^T)^T (U_1 S_1 V_1^T) \\
&= V_1 S_1 \underbrace{U_1^T U_1}_{=I_k} S_1 V_1^T \\
&= V_1 S_1^2 V_1^T
\end{aligned}
$$

**2. Solving the Normal Equation**
We look for $w$ such that:
$$
\underbrace{(V_1 S_1^2 V_1^T)}_{\text{LHS}} w = \underbrace{V_1 S_1 U_1^T Y}_{\text{RHS}} \quad (\Delta)
$$
Which is equivalent to our original problem:
$$
(X^T X)w = X^T Y \quad (\boxtimes)
$$

> [!danger] Lemma
> Define the candidate solution:
> $$
> w^* := V_1 S_1^{-1} U_1^T Y
> $$
> **Claims:**
> 1.  $w^*$ is a solution to $(\boxtimes)$ (equivalent to $(\Delta)$).
> 2.  $w^*$ is the **minimum norm solution** to $(\boxtimes)$.

**Proof (1): $w^*$ is a solution**
Substitute $w^*$ into the LHS of $(\Delta)$:
$$
\begin{aligned}
\text{LHS} &= (V_1 S_1^2 V_1^T) w^* \\
&= (V_1 S_1^2 \underbrace{V_1^T) V_1}_{=I_k} S_1^{-1} U_1^T Y \\
&= V_1 \underbrace{S_1^2 S_1^{-1}}_{S_1} U_1^T Y \\
&= V_1 S_1 U_1^T Y \quad (= \text{RHS})
\end{aligned}
$$
$\implies$ This proves $w^*$ is a valid solution.

**Proof (2): $w^*$ is the minimum norm solution**
Goal: Prove that $\forall \hat{w}$ such that $(X^T X)\hat{w} = X^T Y$, it holds that $\|\hat{w}\| \ge \|w^*\|$.

Since both $\hat{w}$ and $w^*$ are solutions:
$$
\begin{aligned}
(X^T X)\hat{w} &= X^T Y \\
(X^T X)w^* &= X^T Y
\end{aligned}
\implies (X^T X)(\hat{w} - w^*) = 0
$$

Let $\hat{w} = w^* + \tilde{w}$, where $\tilde{w} := \hat{w} - w^*$.
From the equation above, $\tilde{w} \in \text{Ker}(X^T X)$.

> [!info] Remark: Kernel and Image properties
> We know $X^T X = V_1 S_1^2 V_1^T$ (It's already an SVD form).
> $$
> \text{Ker}(X^T X) = \text{Im}(V_1^\perp)
> $$
> Where $V_1^\perp$ comes from the full $V = [V_1, V_1^\perp]$ with $V_1^T V = I$.

Since $\tilde{w} \in \text{Ker}(X^T X)$, implies $\tilde{w} \in \text{Im}(V_1^\perp)$, which means:
$$
\tilde{w} \perp V_1 \quad (\text{and consequently } \tilde{w} \perp \text{Im}(V_1))
$$
On the other hand, $w^* = V_1 (S_1^{-1} U_1^T Y)$, which implies $w^*$ is a linear combination of columns of $V_1$, so:
$$
w^* \in \text{Im}(V_1)
$$

**Conclusion via Pythagorean Theorem:**
Since $w^* \perp \tilde{w}$:
$$
\begin{aligned}
\|\hat{w}\|^2 &= \|w^* + \tilde{w}\|^2 \\
&= (w^* + \tilde{w})^T (w^* + \tilde{w}) \\
&= \|w^*\|^2 + \|\tilde{w}\|^2 + \underbrace{2(w^*)^T \tilde{w}}_{0} \\
&= \|w^*\|^2 + \underbrace{\|\tilde{w}\|^2}_{\ge 0}
\end{aligned}
$$
$$
\implies \|\hat{w}\|^2 \ge \|w^*\|^2 \quad \square
$$

> [!tip] Summary
> When the design matrix $X$ is not full rank (leading to a non-invertible $X^T X$), the normal equation has **infinite solutions**.
>
> By using **SVD**, we identified a specific solution $w^* = V_1 S_1^{-1} U_1^T Y$ which has two key properties:
> 1.  It minimizes the training error (solves the normal equation).
> 2.  Among all possible solutions, it has the **smallest Euclidean norm** ($\|w\|$). This is often desirable for stability and regularization (implicit regularization).

---
### Linear Least Squares & Pseudo-Inverse

> [!info] Recall: Solutions of Linear LS Problems
> $$
> \hat{w} = \text{argmin} \frac{1}{m} \|Y - Xw\|^2
> $$
> Using SVD $X = U S V^T = U_1 S_1 V_1^T$:
> $$
> \hat{w} = V_1 S_1^{-1} U_1^T Y \quad (\text{Minimum Norm Solution})
> $$

**Terminology**
In a general LS problem:
$$
w = \text{argmin} \|b - Aw\|^2 \quad (\Delta)
$$

1.  **If A is invertible:**
    $w^* := A^{-1}b$ such that $Aw^* = A(A^{-1}b) = b$.
    $\implies b - Aw^* = 0$.
2.  **If A is not invertible:**
    (e.g., $A \in \mathbb{R}^{n \times m}$ with $n > m$, tall matrix).

> [!danger] New Concept: Pseudo-Inverse
> A particular pseudo-inverse (or generalized inverse) is the so-called **Moore-Penrose Pseudo-Inverse**.
>
> Given the SVD of $A = U S V^T = U_1 S_1 V_1^T$, then:
> $$
> A^+ := V_1 S_1^{-1} U_1^T
> $$

> [!info] Important Property of M.P. Pseudo-Inverse
> $$
> w^* := A^+ b \quad \text{is the minimum norm solution of } (\Delta)
> $$

> [!question] Homework
> Show that if $A$ is invertible, then $A^+ = A^{-1}$.
> *(Hint)*: Take $A = U S V^T$; $A^{-1} = (U S V^T)^{-1}$. Use the structure of $U, S, V$ when $A$ is invertible (square of course).

#### Perturbation Analysis of Linear LS Problems
We analyze how stable the solution is.
1.  "Deterministic" Worst Case Perturbation Analysis.
2.  "Probabilistic" Analysis.

**Deterministic Worst Case Perturbation Prob.**
$$
\hat{w} = \text{argmin}_w \|Y - Xw\|^2 \qquad X = U_1 S_1 V_1^T
$$
$$
\hat{w} = V_1 S_1^{-1} U_1^T Y
$$

> [!question] Question
> What happens if $Y$ is perturbed? $Y \longmapsto Y + \Delta Y$ (Additive perturbations).
> $$
> \bar{w} = V_1 S_1^{-1} U_1^T (Y + \Delta Y) = \underbrace{V_1 S_1^{-1} U_1^T Y}_{\hat{w}} + \underbrace{V_1 S_1^{-1} U_1^T \Delta Y}_{\Delta w}
> $$
> Which is the **"WORST"** perturbation $\Delta Y$ (that has the largest effect on the solution $\bar{w}$)?
>
> We look for the maximum ratio of relative error on the solution vs relative error on data:
> $$
> \max_{\Delta Y, Y} \frac{\frac{\|\Delta w\|}{\|\hat{w}\|}}{\frac{\|\Delta Y\|}{\|Y\|}}
> $$

> [!danger] Lemma
> We will see that:
> $$
> \max_{\Delta Y, Y} \frac{\|\Delta w\| / \|\hat{w}\|}{\|\Delta Y\| / \|Y\|} = \frac{\sigma_1(X)}{\sigma_k(X)}
> $$
> Where $\sigma_1(X)$ and $\sigma_k(X)$ are the largest ($\sigma_1$) and smallest ($\sigma_k$) non-zero singular values of $X$.
>
> **Condition Number:**
> $$
> \kappa(X) = \frac{\sigma_1(X)}{\sigma_k(X)}
> $$

**Proof of Condition Number**
To solve $\max_{\Delta Y, Y} \frac{\|\Delta w\| / \|\hat{w}\|}{\|\Delta Y\| / \|Y\|}$:
* We can always fix $\|Y\| = 1$.
* We can always fix $\|\Delta Y\| = \delta$.
* We have:
    $$
    \begin{cases}
    \hat{w} = V_1 S_1^{-1} U_1^T Y & \text{Acting on Y we can minimize } \|\hat{w}\| \\
    \Delta w = V_1 S_1^{-1} U_1^T \Delta Y & \text{Acting on } \Delta Y \text{ we can maximize } \|\Delta w\|
    \end{cases}
    $$

**1. Looking to $\Delta w$ (Maximize numerator)**
$$
\max_{\substack{\Delta Y \text{ s.t.} \\ \|\Delta Y\|=\delta}} \| \underbrace{V_1 S_1^{-1} U_1^T}_{A^+} \Delta Y \|
$$
*Reminder:* $\text{argmax}_{v, \|v\|=1} \|Av\| = \sigma_{max}(A)$.
Here we are applying $A^+$. The singular values of $A^+$ are the inverses of $S_1$ ($1/\sigma_k, \dots, 1/\sigma_1$). The maximum singular value of $A^+$ is $1/\sigma_k$.

> [!question] Homework
> Show that:
> $$
> \max_{\substack{\Delta Y \text{ s.t.} \\ \|\Delta Y\|=\delta}} \| V_1 S_1^{-1} U_1^T \Delta Y \| = \delta \frac{1}{\sigma_k(X)}
> $$
> And the max is obtained when $\Delta Y = \delta u_k$ (where $u_k$ is the last column of $U_1$).

**2. Looking to $\hat{w}$ (Minimize denominator)**
With a singular argument we can prove that:
$$
\min_{\substack{Y \\ \|Y\|=1}} \| V_1 S_1^{-1} U_1^T Y \| = \frac{1}{\sigma_1(X)}
$$
And it is achieved for $Y = u_1$.

**Conclusion**
This yields to:
$$
\max_{\substack{\|Y\| \\ \|\Delta Y\|}} \frac{\frac{\|\Delta w\|}{\|\hat{w}\|}}{\frac{\|\Delta Y\|}{\|Y\|}} = \frac{\delta \frac{1}{\sigma_k(X)}}{\delta \frac{1}{\sigma_1(X)}} = \frac{\sigma_1(X)}{\sigma_k(X)}
$$

> [!danger] Definition: Ill-Conditioned
> We say that a Linear Least Squares problem:
> $$
> \hat{w} = \text{argmin} \|Y - Xw\|^2
> $$
> is **ILL-CONDITIONED** if the Condition Number:
> $$
> C(X) = \frac{\sigma_1(X)}{\sigma_k(X)} \gg 1 \quad (\text{e.g., } \approx 10^3, 10^6)
> $$

![[image 12.png|Example]]

> [!tip] Summary
>This section introduced two critical concepts for solving Least Squares when the matrix $A$ (or $X$) is not well-behaved:
>1. **Moore-Penrose Pseudo-Inverse ($A^+$):** It generalizes the concept of matrix inverse to non-square or singular matrices using SVD ($A^+ = V_1 S_1^{-1} U_1^T$). It provides the _minimum norm solution_ to the LS problem.
>2. **Condition Number ($\kappa(X)$):** It measures the stability of the solution. Defined as the ratio between the largest and smallest singular values ($\sigma_1 / \sigma_k$), it tells us how much errors in the input data ($\Delta Y$) are amplified in the solution ($\Delta w$). A large condition number means the problem is **ill-conditioned** (very sensitive to noise).

---
### Probabilistic Analysis of Linear Regression

> [!info] Assumption (Data Generation Process)
> We assume the data is generated by a linear process with additive noise:
> $$
> y_i = x_i^T w + e_i \quad \text{(scalar form)}
> $$
> $$
> Y = Xw + E \quad \text{(matrix form)}
> $$
> Where:
> * $w$: **Unknown** true parameter vector.
> * $e_i$: **Error** (Noise), unobserved.
> * $X$: Design matrix (assumed deterministic/constant).

> [!question] Core Question
> Why do we care about this probabilistic view?
> The goal of Linear Regression is to predict a label $\tilde{y} \approx X^T w$ given an input.
> *Example:* Predicting tomorrow's temperature. $X$ contains features like [pressure, wind direction, exchange rate]. The "exchange rate" feature might have a corresponding weight of 0 in the true model $w$, but our estimator $\hat{w}$ might assign it a small non-zero value due to noise.
>
> We need to **quantify the uncertainty**:
> 1.  How does the noise $E$ affect our estimated weights $\hat{w}$?
> 2.  How to find a range (confidence interval) that likely contains the real $y$?
>    
#### 1. Estimation Error Analysis
We estimate $w$ using the Least Squares solution (ERM):
$$
\hat{w}_S = (X^T X)^{-1} X^T Y
$$
Let's analyze the **estimation error** $\tilde{w}$:
$$
\tilde{w} := \hat{w}_S - w
$$
Substituting $Y = Xw + E$:
$$
\begin{aligned}
\hat{w}_S &= (X^T X)^{-1} X^T (Xw + E) \\
&= \underbrace{(X^T X)^{-1} X^T X}_{I} w + (X^T X)^{-1} X^T E \\
&= w + (X^T X)^{-1} X^T E
\end{aligned}
$$
$$
\implies \tilde{w} = \hat{w}_S - w = (X^T X)^{-1} X^T E
$$
*The error is a linear transformation of the noise $E$.*
#### 2. Assumptions on Noise ($E$)

We typically make assumptions on the error vector $E = [e_1, \dots, e_m]^T$.
##### Assumption 1: Weak Assumptions (Moments)
1.  $\mathbb{E}[e_i] = 0$ (Zero mean)
2.  $\text{Var}\{e_i\} = \sigma^2$ (Homoscedasticity)
3.  $e_i$ are i.i.d. (Independent and Identically Distributed)

**Implications for vector $E$:**
* $\mathbb{E}[E] = 0$ (Vector of zeros)
* $\text{Var}[E] = \mathbb{E}[(E - \mathbb{E}[E])(E - \mathbb{E}[E])^T] = \mathbb{E}[E E^T] = \sigma^2 I_m$

**Properties of $\tilde{w}$ under Assumption 1:**
* **Mean:**
    $$
    \mathbb{E}[\tilde{w}] = \mathbb{E}[(X^T X)^{-1} X^T E] = (X^T X)^{-1} X^T \underbrace{\mathbb{E}[E]}_{0} = 0
    $$
    *(Unbiased Estimator)*
* **Variance:**
    Using the property $\text{Var}(Az) = A \text{Var}(z) A^T$:
    $$
    \begin{aligned}
    \text{Var}\{\tilde{w}\} &= \text{Var}\{ \underbrace{(X^T X)^{-1} X^T}_{A} E \} \\
    &= A \underbrace{\text{Var}\{E\}}_{\sigma^2 I} A^T \\
    &= (X^T X)^{-1} X^T (\sigma^2 I) ((X^T X)^{-1} X^T)^T \\
    &= \sigma^2 (X^T X)^{-1} X^T X (X^T X)^{-1} \\
    &= \sigma^2 (X^T X)^{-1}
    \end{aligned}
    $$

##### Assumption 2: Strong Assumption (Gaussian Noise)
Often motivated by the Central Limit Theorem, we assume:
$$
e_i \sim \mathcal{N}(0, \sigma^2)
$$
Since $e_i$ are i.i.d., the joint probability is the product of marginals:
$$
p(e_1, \dots, e_m) = \prod_{i=1}^m p(e_i) = \left( \frac{1}{\sqrt{2\pi\sigma^2}} \right)^m \exp \left\{ - \frac{1}{2} \frac{\sum e_i^2}{\sigma^2} \right\}
$$
**Implication:** The vector $E$ is a **Gaussian Random Vector**:
$$
E \sim \mathcal{N}(0, \sigma^2 I)
$$
#### 3. Distribution of the Estimator

Since $\tilde{w}$ is a linear transformation of a Gaussian vector $E$ (i.e., $\tilde{w} = A E$ where $A=(X^T X)^{-1} X^T$), then $\tilde{w}$ itself is Gaussian.

> [!warning] Theorem: Distribution of Estimation Error
> Under Assumption 2:
> $$
> \tilde{w} \sim \mathcal{N}(0, \Sigma_{\tilde{w}})
> $$
> Where $\Sigma_{\tilde{w}} = \sigma^2 (X^T X)^{-1}$.

> [!info] Recall: Linear Transformation of Gaussian
> If $z \sim \mathcal{N}(m_z, \Sigma_z)$ and $y = Az + b$, then:
> $y \sim \mathcal{N}(Am_z + b, A \Sigma_z A^T)$.
>
> In our case:
> * Input: $E \sim \mathcal{N}(0, \sigma^2 I)$
> * Transform: $\tilde{w} = (X^T X)^{-1} X^T E$
> * Result: $\tilde{w} \sim \mathcal{N}(0, \sigma^2 (X^T X)^{-1})$

#### 4. Posterior Distribution of $w$ (Bayesian View)

If we consider the true parameter $w$ as a random variable with a prior, or if we just look at the likelihood:

Given $W \sim \mathcal{N}(m_w, \Sigma_w)$, the density function is:
$$
p(w) = \frac{1}{\sqrt{(2\pi)^n \det(\Sigma_w)}} \exp \left\{ -\frac{1}{2} (w - m_w)^T \Sigma_w^{-1} (w - m_w) \right\}
$$
* $n$: Size of the vector.
* $\det(\Sigma_w)$: Determinant of the covariance matrix.

This Gaussian structure allows us to define confidence regions (ellipsoids) around our estimate $\hat{w}$.

##### Why do we care? (And how can we use it?)
> [!question] Q1: Model vs Estimator
> **Linear Regression Model:**
> $$
> Y = Xw + E
> $$
> * $w$: **Unknown** true parameters.
> * $E$: Noise.
>
> **Estimator:**
> $$
> \hat{w}_S = (X^T X)^{-1} X^T Y
> $$
> *Note:* $\hat{w}_S$ typically **cannot contain exact zeros** (even if the true $w$ does) because the matrices contain continuous variables and noise.

**Goal of Linear Regression**
Predict label given the input:
$$
\tilde{y} \approx X^T w = \sum_{i=1}^d [X]_i w_i
$$

**Example: Find the Temperature Tomorrow**
* **Features ($X$):** $\begin{bmatrix} \text{Temp. Today} \\ \text{Pressure} \\ \text{Dir. of Wind} \\ \text{Exchange Rate} \end{bmatrix}$
* **True Weights ($w^T$):** $\begin{bmatrix} * \\ * \\ * \\ 0 \end{bmatrix}$
    * The weight for "Exchange Rate" should be $\mathbf{0}$ because we don't need the exchange rate to predict the temperature.
    * *However*, in our calculated $\hat{w}_S$, due to noise, this might appear as a small non-zero value (e.g., $0.002$).

> [!question] Q2: Combining Result with Uncertainty
>We have to combine the result obtained with the weight of the uncertainty of it.
>* **Visual Goal:** We want to find a **range of Y** which contains the real $Y$ (Confidence Interval).
>* **Analytical Goal:** Evaluate (Quantify) the impact of the estimation error $\tilde{w} = \hat{w}_S - w$ in prediction.

![[image 13.png]]

> [!tip] Summary: Probabilistic Analysis of Linear Regression
>
> While the geometric approach (Least Squares) gives us a method to find a line, the **Probabilistic Analysis** explains *why* that line makes sense and *how trustworthy* it is.
>
> **Key Takeaways:**
> 1.  **Noise Modeling:** We assume data comes from a true process $y = w^Tx + e$. The noise $e$ makes our estimator $\hat{w}$ a **random variable**, not a fixed constant.
> 2.  **Distribution of $\hat{w}$:** If the noise is Gaussian ($e \sim \mathcal{N}(0, \sigma^2)$), then the estimation error is also Gaussian:
>     $$
>     \hat{w} - w \sim \mathcal{N}(0, \sigma^2(X^TX)^{-1})
>     $$
> 3.  **Why it matters:** Knowing this distribution allows us to:
>     * **Quantify Uncertainty:** We can calculate the variance of our error.
>     * **Construct Confidence Intervals:** Instead of just predicting a single value, we can predict a range (e.g., "Temperature will be between 20°C and 22°C with 95% confidence").
>     * **Feature Selection:** If the confidence interval for a weight $w_i$ includes 0, the corresponding feature might be irrelevant (like the "Exchange Rate" in the example), helping us filter out noise.

---
### Confidence Intervals
**Setup:**
* $x$ is a Random Variable (R.V.).
* Assume $x \sim \mathcal{N}(m, \sigma^2)$ (Gaussian distribution).
* Parameters $\theta = (m, \sigma^2)$.
    * $m$: **Unknown**.
    * $\sigma^2$: **Known** (Assumption for this derivation).

**Observation:**
* We observe $x$ (a specific number).

> [!example] Goal
> Construct (based on data $x$) an interval $I_x$ that contains $m$ (the unknown true parameter) with **high probability**.


**Visual Interpretation:**
Imagine the number line with the true mean $m$.
* Different observations ($x$) fall around $m$.
* Around each $x$, we build an interval.
* Some intervals capture $m$ (likely), others might miss it (if $x$ is an outlier).
* *Note in image:* "Much more likely to contain my m".
![[image-1 4.png]]
**Formal Problem:**
Find an interval $I_x$ such that:
$$
\mathbb{P}[I_x \ni m] = 1 - \alpha
$$
*Crucial Note:* The probability $\mathbb{P}$ is on $I_x$ (which is random because it depends on $x$), while $m$ is a constant.

**Derivation**
Given $x \sim \mathcal{N}(m, \sigma^2)$.
Common confidence levels: $\alpha = 0.05$ (95%), $\alpha = 0.01$ (99%).
![[image-2 2.png]]

From the properties of the Normal distribution, we know that $x$ falls within a certain distance $\Delta_\alpha$ from the mean with probability $1-\alpha$:

$$
\mathbb{P}[x \in [m - \Delta_\alpha; \ m + \Delta_\alpha]] = 1 - \alpha
$$

**Inverting the relationship:**
We can rewrite the inequality inside the probability:
$$
x \in [m - \Delta_\alpha, \ m + \Delta_\alpha] \iff m \in [x - \Delta_\alpha; \ x + \Delta_\alpha]
$$
*(Logic: If the data is close to the mean, the mean is close to the data)*.

**Conclusion:**
Substituting this back into the probability statement:
$$
\implies \mathbb{P}[\underbrace{[x - \Delta_\alpha; \ x + \Delta_\alpha]}_{I_x} \ni m] = 1 - \alpha
$$

This interval $I_x = [x - \Delta_\alpha; \ x + \Delta_\alpha]$ is the **Confidence Interval of $m$ with level $1-\alpha$**.

>[!tip] Summary: The Pivot Trick
>This section introduces the core logic of Frequentist Confidence Intervals using a "Pivot" method:
>1. **Start with what we know:** We know how the data $x$ behaves if we knew the mean $m$ (the bell curve centered at $m$).
>2. **Invert the logic:** We algebraically rearrange the inequality. Instead of saying "Data is within distance $\Delta$ of Mean", we say "Mean is within distance $\Delta$ of Data".
>3. **Result:** This allows us to define a range around our _single observation_ $x$ that covers the unknown truth $m$ with a guaranteed probability (e.g., 95%).

#### Confidence Intervals for L.R.
**Setup**
Assume $x \sim \mathcal{N}(m, \sigma^2)$ where $\sigma^2$ is considered unknown (in the general problem), but for this derivation, we use the properties of the Normal distribution.

> [!info] Definition
> An interval $I_x$ is a confidence interval of level $(1-\alpha) \cdot 100\%$ for $m$ if:
> $$
> \mathbb{P}[I_x \ni m] = 1 - \alpha
> $$
> We have seen that the interval is centered around the observation:
> $$
> I_x = [x - \Delta_\alpha, \ x + \Delta_\alpha]
> $$

**Step 1: Standard Normal**
Consider $z \sim \mathcal{N}(0,1)$ (Standard Normal).
We define $z_p$ as the $p$-th level percentile such that:
$$
\mathbb{P}[z \le z_p] = p
$$


We want to find an interval such that the probability is $1-\alpha$.
$$
\mathbb{P}[z \in [-z_{1-\alpha/2}; \ z_{1-\alpha/2}]] = 1 - \alpha
$$
*(Because the tails are symmetric, each tail has area $\alpha/2$, so we look for the quantiles at $1 - \alpha/2$)*.

**Step 2: Normalization & Connection**
Once we find $z_{1-\alpha/2}$, we normalize $x \sim \mathcal{N}(m, \sigma^2)$ to connect it with $z \sim \mathcal{N}(0,1)$.
$$
\frac{x-m}{\sigma} \sim \mathcal{N}(0,1)
$$
Substituting this into the probability statement:
$$
\mathbb{P}\left[ \frac{x-m}{\sigma} \in [-z_{1-\alpha/2}; \ z_{1-\alpha/2}] \right] = 1 - \alpha
$$
By rearranging the inequalities (multiplying by $\sigma$ and shifting by $m$):
$$
\mathbb{P}[x \in [\underbrace{m - z_{1-\alpha/2}\sigma}_{Lower}; \ \underbrace{m + z_{1-\alpha/2}\sigma}_{Upper}]] = 1 - \alpha
$$
Here, the margin of error is defined as:
$$
\Delta_\alpha = z_{1-\alpha/2} \sigma
$$

**Example Calculation**
To complete $\Delta_\alpha$ we need to know $\alpha$ and decide the confidence level we want.
* Let $\alpha = 0.05$ (so confidence level is $0.95$ or 95%).
* $1 - \alpha/2 = 0.975$.
* Looking up the Z-table: $z_{0.975} \approx 1.96$.
* $\implies \Delta_\alpha = 1.96\sigma$.

**Conclusion**
Therefore, given an observation $x \sim \mathcal{N}(\theta, \sigma^2)$:
$$
I_x := [x - z_{1-\alpha/2}\sigma; \ x + z_{1-\alpha/2}\sigma]
$$
is a confidence interval of level $(1-\alpha) \cdot 100\%$.

>[!tip] Summary: Confidence Intervals
>Using the properties of the Gaussian distribution, we can construct a "safe zone" around our observation $x$.
>1. We define a standardized "width" ($z$) based on how confident we want to be (e.g., 1.96 for 95%).
>2. We scale this width by the standard deviation ($\sigma$).
>3. We create the interval $x \pm 1.96\sigma$.
>This guarantees that in 95% of experiments, this constructed interval will "catch" the true unknown mean $m$.

**1. Estimates about Parameters**
We want to make estimates about the parameters found in Linear Regression (LR).
$$
\hat{w} = \text{argmin}_w \frac{1}{m} \|Y - Xw\|^2 \implies \hat{w} = (X^T X)^{-1} X^T Y
$$
$\hat{w}$ is an estimate of my parameters ($\in \mathbb{R}^d$).

> [!question] Question
> How close is $\hat{w}$ to our true $w$?
> Assumption: $Y = Xw + E$ with $E \sim \mathcal{N}(0, \sigma^2 I)$.
>
> We have that:
> $$
> \hat{w} - w \sim \mathcal{N}(0, \Sigma_w) \quad \text{where } \Sigma_w = \sigma^2(X^T X)^{-1}
> $$

**Focus on the i-th component**
Let's focus on the $i$-th component of $\hat{w}$ (to check if it is close to 0, meaning not related to the problem).
Let $e_i$ be the standard basis vector (all zeros except 1 at index $i$).
$$
\hat{w}_i = e_i^T \hat{w}
$$

The error on the single component is:
$$
\hat{w}_i - w_i = e_i^T (\hat{w} - w)
$$
Since linear combinations of Gaussians are Gaussian:
$$
\hat{w}_i - w_i \sim \mathcal{N}(0, \underbrace{e_i^T \Sigma_w e_i}_{\text{scalar variance}})
$$

> [!danger] Definition: Variance of $\hat{w}_i$
> $$
> \sigma_{\hat{w}_i}^2 = e_i^T \Sigma_w e_i = \sigma^2 e_i^T (X^T X)^{-1} e_i
> $$
> Implies:
> $$
> \hat{w}_i \sim \mathcal{N}(w_i, \sigma_{\hat{w}_i}^2)
> $$

**Construction of the Interval**
We have one observation of $\hat{w}_i$ found from the estimated model. We can define a confidence interval for its mean $w_i$ (real model).
The CI of level $1-\alpha$ is given by:
$$
I_{\hat{w}_i} := [\hat{w}_i - \sigma_{\hat{w}_i} z_{1-\alpha/2}; \ \hat{w}_i + \sigma_{\hat{w}_i} z_{1-\alpha/2}]
$$
$$
\mathbb{P}[I_{\hat{w}_i} \ni w_i] = 1 - \alpha
$$

**Interpretation:**
Thus if $0 \in I_{\hat{w}_i}$, then with high probability the true model parameter $w_i$ could be zero (if the interval is small enough).
* Each $I_{\hat{w}_i}$ depends on that particular observation of $\hat{w}_i$.
* The CI means that if we estimate $\hat{w}_i$ 100 times, then 95 of those intervals will contain the true $w_i$.
* The bigger $1-\alpha$ is, the bigger the interval (it also depends on $\sigma_{\hat{w}_i}$).

> [!info] Remark: Dependence on Sample Size ($m$)
> $$
> \sigma_{\hat{w}_i}^2 = \sigma^2 e_i^T (X^T X)^{-1} e_i
> $$
> We can rewrite $(X^T X)$ using the sample covariance/second moment matrix:
> $$
> X^T X = \sum_{i=1}^m x_i x_i^T = m \left( \frac{1}{m} \sum_{i=1}^m x_i x_i^T \right)
> $$
> By the **Law of Large Numbers (LLN)**, $\frac{1}{m} \sum x_i x_i^T \to M_x$ (True 2nd moment of X).
> So:
> $$
> \sigma_{\hat{w}_i}^2 \approx \frac{\sigma^2 e_i^T M_x^{-1} e_i}{m}
> $$
> * The variance depends on $1/m$.
> * The more samples we have ($m \uparrow$), the smaller the variance, and the smaller the confidence interval.


**2. CI for Prediction**
Evaluate confidence of predictions.

**Assumptions:**
* **True Model:** $y_0 = x_0^T w + e_0$ (Ideal Model).
* **Estimated:** $\hat{y}_0 = x_0^T \hat{w}$.
* **Goal:** Evaluate the error $\tilde{y}_0 = \hat{y}_0 - y_0$.

$$
\tilde{y}_0 = \hat{y}_0 - y_0 = x_0^T (\hat{w} - w) - e_0
$$
* $\hat{w} - w$ is Gaussian.
* $e_0 \sim \mathcal{N}(0, \sigma^2)$ is Gaussian and **independent** from previous observations used to train $\hat{w}$.

**Variance of Prediction Error:**
$$
\tilde{y}_0 \sim \mathcal{N}(0, \sigma_{y_0}^2)
$$
We sum the variances (due to independence):
$$
\begin{aligned}
\sigma_{y_0}^2 &= \text{Var}(x_0^T (\hat{w}-w)) + \text{Var}(e_0) \\
&= x_0^T \Sigma_w x_0 + \sigma^2 \\
&= x_0^T (\sigma^2 (X^T X)^{-1}) x_0 + \sigma^2 \\
&= \sigma^2 [ x_0^T (X^T X)^{-1} x_0 + 1 ]
\end{aligned}
$$

**Final Interval for $y_0$:**
We can build an interval centered on the predicted value $\hat{y}_0$:
$$
\mathbb{P} \left[ y_0 \in [\hat{y}_0 - \sigma_{y_0} z_{1-\alpha/2}; \ \hat{y}_0 + \sigma_{y_0} z_{1-\alpha/2}] \right] = 1 - \alpha
$$
> [!tip] Summary: Intervals in Regression
> In Linear Regression, we can calculate Confidence Intervals for two distinct things:
>1. For the Weights ($\hat{w}_i$):
>    We build an interval around each estimated parameter.
>    - **Key Utility:** If the interval for a specific weight includes **0** (e.g., $[-0.1, 0.3]$), it suggests that the feature associated with that weight might be **irrelevant** (statistically insignificant).
>    - **Consistency:** As the number of data points ($m$) increases, these intervals shrink (variance $\propto 1/m$).
>2. For the Predictions ($y_0$):
>    We build an interval around the predicted output for a new input $x_0$.
>    - **Variance Composition:** The uncertainty comes from two sources:
>        1. Uncertainty in the weights ($\hat{w}$ vs $w$).
>        2. Intrinsic noise in the new observation ($e_0$).
>    - Even with infinite data ($m \to \infty$), the interval **cannot shrink to zero** because the intrinsic noise term ($\sigma^2$) always remains.

---
### Risk
**Definition of Risk (True Error):**
$$
L_D(h) = \mathbb{E}_D [\ell(h, z)]
$$

**(1) Loss Function:**
We use the squared loss:
$$
\ell(h_w, z) = (y - h_w(x))^2
$$

**(2) Hypothesis:**
$$
h_w(x) = w^T x
$$
*(The vector $w$ represents the parametrization of the predictor $h$)*

**(3) Resulting Risk Formulation:**
Substituting (1) and (2) into the definition:
$$
L_D(h) = \mathbb{E}_D [(y - w^T x)^2]
$$

> [!info] Note on Distribution
> Here, $D$ represents the **Joint Distribution** over $X$ and $Y$.

> [!question] Open Question
> **How does the assumption on the Linear Regression (LR) model allow us to compute $L_D(h)$?**

---
### Risk Decomposition & Fixed Design Analysis

##### 1. Decomposition of Risk
We start from the definition of Risk $L_D(\bar{w})$ and use the **Generative Model** assumption ($y = x^T w + e$).

$$
L_D(\bar{w}) = \mathbb{E}_D [\ell(\bar{w}, z)] \quad \text{where } z \sim D
$$
Using the chain rule of probability $p(z) = p(x,y) = p(y|x)p(x)$, we can rewrite the expectation as a double integral:

$$
\begin{aligned}
L_D(\bar{w}) &= \iint \ell(\bar{w}, z) p(z) dz \\
&= \iint \ell(\bar{w}, z) p(y|x) p(x) dx dy \\
&= \int \left[ \underbrace{\int \ell(\bar{w}, z) p(y|x) dy}_{\mathbb{E}[\ell(\bar{w},z) | x]} \right] p(x) dx
\end{aligned}
$$

> [!abstract] Result
> The Risk can be viewed as the expected value (over $x$) of the conditional expected loss:
> $$
> L_D(\bar{w}) = \mathbb{E} \Big[ \mathbb{E} [ \ell(\bar{w}, z) \mid x ] \Big] \quad (\Delta)
> $$

##### 2. Computing the Inner Expectation
Let's solve the inner part of $(\Delta)$ given a fixed $x$.
We assume the True Model: $y = x^T w + e$, with $e \sim \mathcal{N}(0, \sigma^2)$.
We want to evaluate the loss for a predictor $\bar{w}$:

$$
\begin{aligned}
\mathbb{E} [ (y - x^T \bar{w})^2 \mid x ] &= \mathbb{E} [ (x^T w + e - x^T \bar{w})^2 \mid x ] \\
&= \mathbb{E} [ (x^T(w - \bar{w}) + e)^2 \mid x ] \\
&= \int (x^T(w - \bar{w}) + e)^2 p(e) de
\end{aligned}
$$

Expanding the square $(A+B)^2 = A^2 + B^2 + 2AB$:
1.  **Term $A^2$ (Fixed):** $[x^T(w-\bar{w})]^2$ (Constant with respect to expectation over $e$).
2.  **Term $B^2$ (Noise):** $\mathbb{E}[e^2] = \sigma^2$.
3.  **Term $2AB$ (Cross):** $2 x^T(w-\bar{w}) \underbrace{\mathbb{E}[e]}_{0} = 0$.

**Result of Inner Expectation:**
$$
\mathbb{E}[\ell(\bar{w}, x) | x] = (w - \bar{w})^T x x^T (w - \bar{w}) + \sigma^2
$$
##### 3. Computing the Total Risk (Outer Expectation)
Now we integrate over $x$ to find $L_D(\bar{w})$:

$$
\begin{aligned}
L_D(\bar{w}) &= \int \left[ (w - \bar{w})^T x x^T (w - \bar{w}) + \sigma^2 \right] p(x) dx \\
&= (w - \bar{w})^T \left[ \int (x x^T) p(x) dx \right] (w - \bar{w}) + \sigma^2
\end{aligned}
$$

> [!danger] Definition: Second Moment Matrix
> We define the population second moment matrix as:
> $$
> M_x = \mathbb{E}[XX^T] = m_x m_x^T + \text{Var}\{x\}
> $$
> *Note:* In the empirical case (dataset), $X^T X \approx m \cdot M_x$.

**Final Risk Formula:**
$$
L_D(\bar{w}) = (w - \bar{w})^T M_x (w - \bar{w}) + \sigma^2
$$

##### 4. Fixed Design Analysis (The "Dataset" View)
Why do we care about specific datasets $\mathcal{X}$?


**Remark on Prediction Error Variance:**
Recall that the variance of the prediction error $\tilde{y}_0$ is:
$$
\text{Var}\{\tilde{y}_0\} = x_0^T \text{Var}\{\hat{w}\} x_0 + \sigma^2
$$
This is equivalent to the Conditional Risk averaged over the dataset generation process:
$$
\text{Var}\{\tilde{y}_0\} = \mathbb{E} [ L_D(\hat{w}|x) \mid \mathcal{X} ]
$$

**What does "Fixed $\mathcal{X}$" mean?**
* **Assumption:** We treat the input points $X$ as fixed constants.
* **Randomness:** The only randomness comes from the $Y$ values (the noise $e$).
* **Interpretation:**
    * **Dataset 1 (Orange):** Points $X$ with labels $y^{(1)}$.
    * **Dataset 2 (Green):** Same points $X$, but new labels $y^{(2)}$ (perturbation on Y only).
    * We calculate the variance of $\hat{w}$ across these hypothetical datasets that share the same input locations.

$$
\text{Var}\{\hat{w}\} = \sigma^2 (X^T X)^{-1} \quad \text{(Valid for fixed } \mathcal{X})
$$

![[image 14.png]]


> [!tip] Summary: Risk & Fixed Design
>This section connects the abstract concept of Risk to the concrete Linear Regression formulas.
>1. **Risk Decomposition:** We proved that the Total Risk equals the "Geometric Error" (distance between estimated parameters $\bar{w}$ and true parameters $w$ weighted by the data distribution $M_x$) plus the **Irreducible Error** ($\sigma^2$).
>    $$\text{Risk} = \text{Parameter Error} + \text{Noise}$$
>2. **Fixed Design:** To analyze the stability of our solution, we often assume the inputs $X$ are fixed. This allows us to visualize different "parallel universes" (Datasets 1, 2, etc.) where the inputs are identical, but the noise changes the output $Y$. This simplifies the calculation of $\text{Var}(\hat{w})$.

---
### Model Selection

>[!info] **ERM Recall**
> $$\hat{h} = \underset{h \in H}{\text{argmin}} \ L_S(h)$$

*Eg.* Linear Regression $H = \{h(x): h(x)=w^T x, \ w \in \mathbb{R}^d\}$.

> [!question] Problem
> What if we have many candidate model classes: $H_j, \quad j=1, \dots, K$?
> **How do we select the best $H_j$?**

**Example: Regression Problem**
We have points that look like an arc.
We want to find $h(x)$ for $x \in \mathbb{R}$ such that $y \approx h(x)$.
![[image-3 1.png]]

**Candidate Classes:**
1.  **Linear ($H_1$):**
    $$H_{LIN} = \{h(x): h(x) = w^T x + b\} \ (= H_1)$$
2.  **Quadratic ($H_2$):**
    $$H_2 = \{h(x): h(x) = w_0 + w_1 x + w_2 x^2\}$$
    *Note:* We only care that the model is linear on $w$, not on $x$.
3.  **Cubic ($H_3$):**
    $$H_3 = \{h(x): h(x) = w_0 + w_1 x + w_2 x^2 + w_3 x^3\}$$

**Generalization (Basis Functions):**
Going one step further, we can define a class $H_\phi$ using a feature map $\phi(x)$:
$$
H_\phi = \left\{ h(x): h(x) = \sum_{i=1}^d w_i \phi_i(x) = [w_1 \dots w_d] \begin{bmatrix} \phi_1(x) \\ \vdots \\ \phi_d(x) \end{bmatrix} \right\}
$$
*Example for $H_3$:* $\phi(x) = [1, x, x^2, x^3]^T$.

**Finding the ERM**
To find the best model in a specific class (e.g., $H_2$):
$$
\hat{h}_2 = \underset{h \in H_2}{\text{argmin}} \ L_S(h) \iff \hat{w} = \underset{w \in \mathbb{R}^3}{\text{argmin}} \ \frac{1}{m} \sum_{i=1}^m \left( y_i - w^T \begin{bmatrix} 1 \\ x_i \\ x_i^2 \end{bmatrix} \right)^2
$$
$\hat{w}$ is obtained solving a set of linear equations.
We do this for all classes: $\hat{h}_1 = \text{argmin}_{H_1} L_S, \ \hat{h}_3 = \text{argmin}_{H_3} L_S$, etc.

**Approach to Model Selection**
> [!danger] Warning: Nested Classes
> If $H_1 \subset H_2 \subset H_3$, then:
> $$
> L_S(\hat{h}_1) \ge L_S(\hat{h}_2) \ge L_S(\hat{h}_3)
> $$
> With this logic (minimizing training loss), **we always choose the more complex model**. This leads to overfitting.

**1st Approach: Train-Validation Split**

We split the data indices into two sets:
$$
i: \underbrace{1, 2, 3, 4 \dots m_s}_{\text{Training } (2/3)} \mid \underbrace{\dots m}_{\text{Validation } (1/3)}
$$
* **Training Set ($S$):** $\{(x_i, y_i) : i \in [1, \dots, m_s]\}$
* **Validation Set ($V$):** $\{(x_i, y_i) : i \in [m_s+1, \dots, m]\}$

We define two losses:
1.  **Training Loss:** $L_S(h) = \frac{1}{|S|} \sum_{(x,y) \in S} \ell(h, (x,y))$
2.  **Validation Loss:** $L_V(h) = \frac{1}{|V|} \sum_{(x,y) \in V} \ell(h, (x,y))$
![[image-2 3.png]]
**Selection Rule:**
$$
\hat{h} = \underset{h \in \{\hat{h}_1, \hat{h}_2, \hat{h}_3\}}{\text{argmin}} \ L_V(h)
$$

**Example Visualization**
* **Best Linear:** Underfits (high bias).
* **Best Cubic:** We have infinitely many solutions. It fits training data perfectly but has high error on validation points (Overfits).
* **Best Quadratic:** Fits the validation points best.

*Sample Complexity Bound (Reference):*
$$
m \ge \frac{1}{\epsilon} \log \left( \frac{|H|}{\delta} \right)
$$
*(For the best we use $w^* = \dots$)*

![[image-1 5.png]]

>[!tip] Summary: Model Selection
>The core issue in model selection is that Training Loss is deceptive: complex models (like high-degree polynomials) can memorize training data, driving $L_S$ to zero, but fail to generalize.
>To solve this, we introduce the **Train-Validation Split**:
>1. **Train** multiple candidate models ($\hat{h}_1, \hat{h}_2, \dots$) on the **Training Set** ($S$).
>2. **Evaluate** them on the **Validation Set** ($V$), which the models haven't seen.
>3. **Select** the model with the lowest **Validation Loss** ($L_V$).
>This simulates the model's performance on "new" data, helping us pick a model that captures the true pattern (like the quadratic curve in the example) rather than the noise.

---
### Linear Classification (Binary Classification)

**Setup:**
* Labels: $y \in \{-1, 1\}$
* Data: $x \in \mathbb{R}^2$ (or generally $\mathbb{R}^d$)
    * $x_i \in \mathbb{R}^d$, with features $[x_i]_j$ where $j \in [1, \dots, d]$.
* Dataset index: $i = 1 \dots$

![[image-5 1.png]]

**Visual Representation:**
* **Blue Crosses ($x$):** Label $+1$
* **Orange Circles ($o$):** Label $-1$


**Goal:**
We want to find the **Hyperplane** that separates the 2 regions.

**The Hyperplane Equation:**
$$
w^T x + b = 0
$$
Given $w, b$ (which is equivalent to being given the partition).

> [!info] Classification Rule
> $$
> h_{w,b}(x) = \text{sign} \{ w^T x + b \}
> $$

##### The Geometry of Linear Classification
Let $d=2$.
* $x \in \mathbb{R}^d$
* $w \in \mathbb{R}^d$
![[image-6 1.png]]
**Key Property:**
$w$ is the vector **perpendicular ($\perp$)** to the hyperplane.

**Decomposition:**
Any vector $x$ can be decomposed into components orthogonal and parallel to the hyperplane:
$$
x = x_\perp + x_{||}
$$

**Proof that $w \perp \text{Hyperplane}$:**
Consider the hyperplane equation $w^T x + b = 0$.
Substituting the decomposition:
$$
w^T (x_\perp + x_{||}) + b = 0 \implies \underbrace{w^T x_\perp + b}_{\text{const. } \forall x} + \underbrace{w^T x_{||}}_{= 0 \ \forall x_{||}} = 0
$$
* $x_{||}$ changes as we move along the hyperplane.
* $x_\perp$ remains the same for all $x$ on the hyperplane relative to the origin.
* Therefore, for the equation to hold for all $x$ on the plane, $w^T x_{||}$ must be 0.
* $\implies w \perp x_{||}$ (w is orthogonal to vectors lying on the plane).

**Distance from Origin:**
$$
w^T x_\perp + b = 0 \implies w^T x_\perp = -b
$$
Using the dot product formula $\langle w, x_\perp \rangle = \pm \|w\| \cdot \|x_\perp\|$:
$$
\|x_\perp\| = \pm \frac{b}{\|w\|}
$$
##### Distance from an Arbitrary Point

Let's compute $w^T x + b$ for a point $x \notin \text{Hyperplane}$.


**Decomposition:**
Let $x = \hat{x} + \tilde{x}$
* $\hat{x}$: The projection of $x$ onto the hyperplane ($w^T \hat{x} + b = 0$).
* $\tilde{x}$: The vector perpendicular to the plane connecting it to $x$.

**Derivation:**
$$
\begin{aligned}
w^T ( \hat{x} + \tilde{x} ) + b &= \underbrace{w^T \hat{x} + b}_{=0} + w^T \tilde{x} \\
&= w^T \tilde{x} \\
&= \langle w, \tilde{x} \rangle = \pm \|w\| \cdot \|\tilde{x}\|
\end{aligned}
$$

Rearranging for the distance $\|\tilde{x}\|$:

> [!tip] Signed Distance Formula
> $$
> \|\tilde{x}\| = \text{dist}(x, \text{Line}) = \pm \frac{w^T x + b}{\|w\|}
> $$
> This represents the **signed distance** of $x$ from the line.

>[!info] Remark: Correctness Check
> **Classification Rule:**
>$$h_w(x) = \text{sign} \{ w^T x + b \} = \begin{cases} 1 & \text{if } w^T x + b > 0 \\ -1 & \text{if } w^T x + b < 0 \end{cases} $$
> **Given a dataset $(x_i, y_i)$:**
>* If $w^T x_i + b > 0 \implies \hat{y}_i = 1$
>* If $w^T x_i + b < 0 \implies \hat{y}_i = -1$

**Compact Expression for Correctness:**
Consider the expression $y_i (w^T x_i + b)$:

$$
y_i (w^T x_i + b) = \begin{cases} > 0 & \implies \hat{y}_i = y_i \quad (\text{Correctly Classified}) \\ < 0 & \implies \hat{y}_i \neq y_i \quad (\text{Incorrectly Classified}) \end{cases}
$$
*(Since multiplying two signs that are the same gives a positive, and different signs gives a negative).*

---
#### The Perceptron Algo (Rosenblatt 1958)

**Binary Classification Setup**
* **Data:** $(x_i, y_i)$ for $i=1, \dots, m$.
* **Labels:** $y_i \in \{-1, 1\}$.
* **Assumption:** Data are **Linearly Separable** ($\implies \exists$ a line/hyperplane that separates the data).


**Notation (Bias Trick):**
To simplify $w^T x + b$, we augment the vectors:
$$
w^T x + b = [w^T \ b] \begin{bmatrix} x \\ 1 \end{bmatrix} = \bar{w}^T \bar{x} \longrightarrow w^T x
$$
*(We will refer to the augmented vector simply as $x$ from now on)*.

> [!info] Perceptron Algorithm
> **Iterative Algorithm:** Generates a sequence $w^{(0)}, w^{(1)}, \dots, w^{(k)}, \dots$
>
> 1.  **Initialization:**
>     $$w^{(0)} = 0$$
> 2.  **Loop:** While $\exists$ misclassified point $(x_j, y_j)$:
>     * Pick $j$ s.t. $(x_j, y_j)$ is misclassified (at random).
>     * **Update Rule:**
>         $$w^{(k+1)} = w^{(k)} + y_j x_j$$

> [!check] Property
> This algorithm terminates in a **FINITE** number of steps.

**Remark:**
A point $(x_i, y_i)$ is misclassified if:
$$
y_i w^T x_i < 0
$$
*(Because signs of $y$ and prediction $w^T x$ disagree)*.

**Proof of Convergence**

>[!warning] **Theorem:**
>Assume data is linearly separable ($\exists w_0 \text{ s.t. } y_i w_0^T x_i > 0 \ \forall i$).
>Then the Perceptron Algorithm terminates in at most **$K = B^2 M^2$ steps**.

> [!danger] **Definitions:**
>1.  **Radius of Data ($B$):**
>    $$B = \max_{i \in [m]} \|x_i\|$$
>2.  **Margin Parameter ($M$):**
>    $$M = \min_w \|w\| \quad \text{s.t. } y_i w^T x_i \ge 1 \ \forall i \in [m]$$
>    Let $w_0$ be the solution to this optimization, so $M = \|w_0\|$.

> [!note] Remark on $M$
> Linearly separable implies $\exists c > 0$ s.t. $y_i \frac{w_{start}^T x_i}{c} \ge 1$. We can define $\bar{w}_0 = w_{start}/c$.

**Proof Strategy:**
Let $w^{(k+1)} = w^{(k)} + y_i x_i$ where $i$ is the index of a misclassified point.
We will analyse the growth of the weight vector in two ways:
1.  **S1:** $\|w^{(k+1)}\|$ doesn't grow too fast (Upper Bound).
2.  **S2:** $\langle w^{(k+1)}, w_0 \rangle$ grows fast enough (Lower Bound).

**Proof of S1 (Upper Bound on Norm):**
We analyse the squared norm of the updated weight:
$$
\begin{aligned}
\|w^{(k+1)}\|^2 &= (w^{(k)} + y_i x_i)^T (w^{(k)} + y_i x_i) \\
&= \|w^{(k)}\|^2 + \underbrace{\|x_i\|^2}_{\le B^2} + 2 \underbrace{y_i (w^{(k)})^T x_i}_{< 0}
\end{aligned}
$$
* $\|x_i\|^2 \le B^2$ by definition of $B$.
* $y_i (w^{(k)})^T x_i < 0$ because the point $i$ was **misclassified** at step $k$ (that's why we updated).

Thus:
$$
\|w^{(k+1)}\|^2 \le \|w^{(k)}\|^2 + B^2
$$

By induction, starting from $w^{(0)} = 0$:
$$
\|w^{(k)}\|^2 \le k B^2
$$
> [!tip] Summary: Perceptron Convergence
>The Perceptron is one of the earliest neural network algorithms. It finds a separating hyperplane by iteratively correcting errors: whenever it makes a mistake, it shifts the weight vector towards the misclassified point.
>
>The **Convergence Theorem** proves that if a solution exists (Linear Separability), the algorithm **will not loop forever**.
>
>- **Key Insight 1 (Upper Bound):** Each update adds at most $B^2$ to the squared length of the weight vector because the correction vector makes an obtuse angle with the current weight (since it was a mistake).
  >  
>- **Key Insight 2 (Lower Bound - Upcoming):** In the next section, we will likely prove that the projection of the weight vector onto the _optimal_ direction grows linearly, forcing the algorithm to stop when the upper and lower bounds collide.

---
#### From The Perceptron To Logistic Regression

**Classification Rule:**
$$
h_w(x) = \text{sign}\{w^T x\}
$$
We can think of the function $w^T x$ as a **"score"** that can be used for classification.

**Defining a Probabilistic Label:**
Instead of a hard threshold, we assume the probability is proportional to the exponential of the score:
$$
\begin{aligned}
\mathbb{P}_w[y=1|x] &\propto e^{w^T x} \\
\mathbb{P}_w[y=-1|x] &\propto e^{-w^T x}
\end{aligned}
$$
*Since probability is at most 1, we need to normalize.*

**Normalization:**
Choose $C$ such that $\mathbb{P}[y=1|x] + \mathbb{P}[y=-1|x] = 1$.
$$
\begin{aligned}
\mathbb{P}_w[y=1|x] &= C e^{w^T x} \\
\mathbb{P}_w[y=-1|x] &= C e^{-w^T x}
\end{aligned}
$$
Solving for $C$:
$$
C (e^{w^T x} + e^{-w^T x}) = 1 \implies C = \frac{1}{e^{w^T x} + e^{-w^T x}}
$$

**Deriving the Probabilities:**
For $y=1$:
$$
\mathbb{P}_w[y=1|x] = \frac{e^{w^T x}}{e^{w^T x} + e^{-w^T x}} \cdot \frac{e^{-w^T x}}{e^{-w^T x}} = \frac{1}{1 + e^{-2w^T x}}
$$
For $y=-1$:
$$
\mathbb{P}_w[y=-1|x] = \frac{e^{-w^T x}}{e^{w^T x} + e^{-w^T x}} = \frac{1}{1 + e^{2w^T x}}
$$

> [!info] Compact Notation (Renaming)
> To simplify the factor 2, we rename the parameter vector: $2w \longmapsto w$.
>
> This gives us the standard forms:
> $$
> \mathbb{P}_w[y=1|x] = \frac{1}{1 + e^{-w^T x}}
> $$
> $$
> \mathbb{P}_w[y=-1|x] = \frac{1}{1 + e^{w^T x}}
> $$
>
> **Unified Formula:**
> $$
> \mathbb{P}_w[y|x] = \frac{1}{1 + e^{-y w^T x}}
> $$

**Remark:**
* Think of $w^T x$ as a "score" for class 1.
* We measure $\mathbb{P}_w[y|x]$ by mapping $w^T x$ (which is in $\mathbb{R}$) into the interval $[0, 1]$.
* This mapping is done via the **Logistic Function** (Sigmoid): $\sigma(z)$.


$$
\mathbb{P}_w[y=1|x] = \sigma(z) \circ w^T x \quad \text{where } \sigma(z) = \frac{1}{1 + e^{-z}}
$$
$$
\mathbb{P}_w[y=1|x] = \frac{1}{1 + e^{-w^T x}}
$$
$$
\mathbb{P}_w[y=-1|x] = 1 - \mathbb{P}_w[y=1|x]
$$

#### Maximum Likelihood Estimation (MLE)

We want to find the weights $w$ that maximize the probability of the observed data.
Assumed I.I.D. data:
$$
\mathbb{P}_w [y_1, x_1, \dots, y_m, x_m] = \prod_{i=1}^m \mathbb{P}_w [y_i, x_i]
$$
Using the chain rule $\mathbb{P}[y,x] = \mathbb{P}[y|x]\mathbb{P}[x]$:
$$
= \left( \prod_{i=1}^m \mathbb{P}_w [y_i | x_i] \right) \left( \prod_{i=1}^m \mathbb{P}_w [x_i] \right)
$$

**Maximum Likelihood Principle:**
We look for the parameters that maximize this probability. Note that $\mathbb{P}_w[x_i]$ does not depend on $w$, so we can ignore it during maximization.

$$
\hat{w}_{MLE} = \underset{w \in \mathbb{R}^d}{\text{argmax}} \ \mathbb{P}_w [(y_i, x_i); i=1, \dots, m]
$$

> [!danger] MLE for Logistic Regression
> Substituting the logistic probability derived above:
> $$
> \hat{w}_{MLE} = \underset{w}{\text{argmax}} \prod_{i=1}^m \frac{1}{1 + e^{-y_i w^T x_i}}
> $$


>[!tip] Summary: Logistic Regression
>1. **Motivation:** The Perceptron gives a hard binary output ($+1/-1$) based on the sign of the score $w^Tx$. Logistic Regression softens this by converting the score into a **probability** $[0,1]$.
>2. **The Sigmoid:** This conversion is done using the sigmoid function $\sigma(z) = \frac{1}{1+e^{-z}}$. A high positive score gives a probability near 1; a high negative score gives a probability near 0.
>3. **Unified Probability:** A clever algebraic trick allows us to write the probability for both classes ($y=1$ and $y=-1$) in a single formula: $P(y|x) = \frac{1}{1+e^{-yw^Tx}}$.
>4. **Training (MLE):** Unlike the Perceptron algorithm which fixes mistakes, Logistic Regression finds the optimal $w$ by maximizing the **Likelihood** of the observed data (finding the $w$ that makes the observed labels most probable).

---


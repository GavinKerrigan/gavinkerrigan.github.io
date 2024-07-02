---
title: "Sobolev Spaces"
topic: "Analysis"
chapter: "PDEs"
section: "sobolev"
layout: note
permalink: "/notes/analysis/pde/sobolev/"

subtitle: Banach spaces with norms that measure derivatives
date: 2024-06-17
keywords: analysis, pdes
published: true
references: "Evans, L. C. (2022). Partial differential equations (2nd ed.).; Calder, J. (2024). The calculus of variations."
---

Let $U \subset \R^d$ be open and bounded with smooth boundary $\partial U$. We write $V \Subset U$ if $V$ is compactly contained within $U$, i.e. $\overline{V}$ is compact and $V \subset \overline{V} \subset U$. 

<div class='definition' name='Local Integrability'>
For $1 \leq p \leq \infty$, we have $u \in L^p_{\text{Loc}}(U)$ if $u \in L^p(V)$ for all $V \Subset U$. 
</div>

## Weak Derivatives

The notion of a weak derivative allows us to extend notions of differential calculus to non-smoooth functions. The key notion here is a generalized integration by parts formula.

<div class='definition' name='Weak Derivatives'>
Let $u, v \in L^1_{\text{Loc}}(U)$ and $1 \leq i \leq n$. Fix a multiindex $\alpha$. We say that $v$ is the $\alpha$-th weak derivative of $u$, written $D^\alpha u = v$, if

\[
\int_U u D^\alpha \varphi \d x = (-1)^{|\alpha|} \int_U v \varphi \d x.
\]

for all $\varphi \in C_c^\infty(U)$. 
</div>

Why do we work with test functions in $C_c^\infty(U)$ and not some other space? Simply put: they're nice functions and results shown on smooth test functions can often be extended to other spaces.

- Smoothness of the test functions means that we don't need to worry about differentiability issues, e.g. when defining higher-order weak derivatives.
- Compact support means that we can avoid having to track boundary data. Note that, since $U$ is open, any test function necessarily dissapears on $\partial U$. This enables a local analysis.
- The set $C_c^\infty(U)$ is dense in $L^p(U)$ for $1 \leq p < \infty$, and in a sense we will soon make precise, smooth functions also approximate functions in the Sobolev spaces $W^{k,p}(U)$. 


<div class='lemma' name='Uniqueness of Weak Derivatives'>
Suppose $u \in L^1_{\text{Loc}}(U)$ has a weak $\alpha$th derivative $D^\alpha u = v$. Then, $v$ is unique up to a set of Lebesgue measure zero. 
</div>
<details class="proof">
<summary> Proof. </summary>
Suppose $v, w$ are two $\alpha$th weak derivatives of $u$. It follows that, for all $\varphi \in C_c^\infty(U)$,

\[
\int_U u D^\alpha \varphi \d x = (-1)^{|\alpha|}\int_U v \varphi \d x = (-1)^{|\alpha|}\int_U w \varphi \d x
\]

and hence 

\[
0 = \int_U (v - w ) \varphi \d x.
\]

Since $\varphi \in C_c^\infty(U)$ was arbitrary, we conclude $v = w$ almost everywhere.
</details>


## Sobolev Spaces

Sobolev spaces are essentially spaces of weakly differentiable functions with a prescribed degree of regularity. Roughly speaking, the norm in these spaces measures the frequency characteristics (or regularity) of the functions, along with the usual $L^p$ notions of size. See [this note](https://terrytao.wordpress.com/2009/04/30/245c-notes-4-sobolev-spaces/) from Terrence Tao for an excellent illustration.

For instance, Tao argues that for a given smooth test function $\varphi$ (in $\R$), the function $A \varphi(x/R) \sin(Nx)$ will have Sobolev $W^{k,p}(\R)$ norm of about $\|A\| R^{1/p} N^k$. This measures the amplitude, "width" $R$ (whose importance is decreasing with $p$), and frequency $N$ (whose importance increases with $k$).

<div class='definition' name='Sobolev Spaces'>
Fix $1 \leq p \leq \infty$ and $k \in \Z_{\geq 0}$. The Sobolev space $W^{k,p}(U)$ is the set

\[
W^{k,p}(U) = \left\{u \in L^1_{\text{Loc}}(U) : \forall |\alpha| \leq k, D^\alpha u \in L^p(U) \right\}.
\]

In other words, it is the space of locally integrable functions which are weakly differentiable up to order $\alpha$, where the weak derivatives live in $L^p(U)$.

<br><br>

We define the norm of $u \in W^{k,p}(U)$ via

\[
\norm{u}_{W^{k,p}(U)} = \begin{cases}   \left(\sum_{|\alpha| \leq k} \int_U |D^\alpha u|^p \d x\right)^{1/p} & 1 \leq p < \infty \\ 
			                 \max_{|\alpha| \leq k} \text{ess sup} |D^\alpha u| & p = \infty
 \end{cases}.
\]
</div>

Note that we may write

\\[
\lvert\lvert u \rvert \rvert_{W^{k,p}(U)}^p = \sum_{\|\alpha\| \leq k} \norm{D^\alpha u}_{L^p(U)}^p \qquad 1 \leq p < \infty 
\\]

and analogously for $p = \infty$. For $k=1$, note that we may conveniently write

\\[
\lvert\lvert u \rvert\rvert_{W^{1,p}(U)}^p = \int_U |u|^p + |\nabla u|^p \d x = \lvert\lvert u \rvert\rvert_{L^p(U)}^p + \lvert\lvert \nabla u \rvert\rvert^p_{L^p(U)}.
\\]



Observe that, informally, the Sobolev norm is just a finite-dimensional $\ell_p$ norm applied to the vector of all weak partial derivatives. Thus, thanks to the equivalence of norms on finite-dimensional spaces, we see that an equivalent norm is given for $1 \leq p \leq \infty$ by

\\[
\lvert\lvert u \rvert\rvert_{W^{k,p}(U)}' = \sum_{\|\alpha\| \leq k} \lvert\lvert D^\alpha u \rvert\rvert_{L^p(U)}.
\\]

Since $W^{k,p}(U)$ is modeled on $L^p(U)$, it is perhaps not surprising that Sobolev spaces inherit the nice properties of $L^p(U)$. Here, we will explore three fundamental topological properties: completeness, separability, and reflexivity. Loosely speaking, these properties can be obtained by exploiting the corresponding property on $L^p(U)$. 

<div class='theorem' name='Sobolev Spaces are Banach'>
For $k = 1, 2, \dots$ and $1 \leq p \leq \infty$, the space $W^{k,p}(U)$ is a Banach space.
</div>
<details class="proof">
<summary> Proof. </summary>
It is straightforward to check that $\norm{-}_{W^{k,p}(U)}$ is a norm. To see that the space is complete, suppose that $(u_m)$ is Cauchy in the $W^{k,p}(U)$ norm. Then, for every $|\alpha| \leq k$, the sequence $(D^\alpha u_m)$ is Cauchy in the $L^p(U)$ norm. Since $L^p(U)$ is complete, we have that $D^\alpha u_m \to v^\alpha$ in the $L^p(U)$ norm for some $v^\alpha \in L^p(U)$. In particular, the $\alpha = 0$ case shows that $u_m \to u$ converges to some $u \in L^p(U)$. We claim that $D^\alpha u = v^\alpha$ for every $|\alpha| \leq k$. Indeed,

\[
\begin{aligned}
\int_U u D^\alpha \varphi \d x &= \lim_{m \to \infty} \int_U u_m D^\alpha \varphi \d x \\
&= \lim_{m \to \infty} (-1)^{|\alpha|} \int_U D^\alpha u_m \varphi \d x \\
&= (-1)^{|\alpha|} \int_U v^\alpha \varphi \d x.
\end{aligned}
\]

This shows that $D^\alpha u_m \to D^\alpha u$ in $L^p(U)$ for $|\alpha| \leq k$, i.e. $u_m \to u$ in the $W^{k,p}(U)$ norm. Note that the limit-integral exchanges are justified thanks to the $L^p(U)$ convergence of the integrands and an application of Holder's inequality.
</details>

The case $p=2$ is typically suggestively denoted by $W^{k,2}(U) = H^k(U)$. Indeed, the spaces $H^k(U)$ are Hilbert spaces.

<div class='theorem' name='Sobolev Spaces are Hilbert when p=2'>
Let $k \in \Z_{\geq 1}$. The space $H^k(U) = W^{k,2}(U)$ is a Hilbert space under the inner product
\[
\langle u, v \rangle_{H^k(U)} = \sum_{|\alpha| \leq k} \langle D^\alpha u, D^\alpha v \rangle_{L^2(U)} = \sum_{|\alpha| \leq k}\int_U D^\alpha u D^\alpha v \d x.
\]
</div>
<details class="proof">
<summary> Proof. </summary>
It is straightforward to check that the form defined is indeed an inner product which induces the specified norm. As we know already that Sobolev spaces are complete, there is nothing more to show.
</details>

Again, when $k=1$ the innner product takes a particularly friendly form:

\\[
\langle u, v \rangle_{H^1(U)} = \int_U [u v + \langle \nabla u, \nabla v \rangle ] \d x= \langle u, v \rangle_{L^2(U)} + \langle \nabla u, \nabla v \rangle_{L^2(U)}.
\\]

The spaces $H^k(U)$ are intimately connected with Fourier transforms, which we will explore in a later note.

<div class='theorem' name='Sobolev Spaces are Separable'>
For $k \in \Z_{\geq 1}$ and $1 \leq p < \infty$, the space $W^{k,p}(U)$ is separable.
</div>
<details class="proof">
<summary> Proof. </summary>
Recall that $L^p(U)$ is separable for $1 \leq p < \infty$. Define the mapping

\[
\iota: W^{k,p}(U) \to L^p(U) \times \bigotimes_{i=1}^n L^p(U) \times \cdots \times \bigotimes_{i=1}^{n^k} L^p(U)
\]
\[
u \mapsto (u, D u, D^2 u, \dots, D^k u).
\]

Observe that $\iota$ is an injective linear isometry into a separable Banach space (as the countable product of separable spaces is separable). Thus, the image $\iota(W^{k,p}(U))$ is separable, and admits a countable dense subset $D \subseteq \iota(W^{k,p}(U))$.

As $\iota$ is injective, $\iota^{-1}(D)$ is countable, and because $\iota$ is an isometry, $\iota^{-1}(D)$ is dense in $W^{k,p}(U)$. Thus, $W^{k,p}(U)$ is separable.
</details>

<div class='theorem' name='Sobolev Spaces are Reflexive'>
For $k \in \Z_{\geq 1}$ and $1 < p < \infty$, the space $W^{k,p}(U)$ is reflexive.
</div>
<details class="proof">
<summary> Proof. </summary>
Recall that $L^p(U)$ is reflexive for $1 < p < \infty$. Using the same mapping $\iota$ from the previous proof, we isometrically embed $W^{k,p}(U)$ into a finite product of $L^p(U)$ spaces. Note the product of finitely many reflexive spaces is reflexive. Now, since $W^{k,p}(U)$ is complete, it is closed, and a closed subspace of a reflexive space is itself reflexive.
</details>

### Absolutely Continuous Characterization

When $U \subset \R$ is an open interval, we obtain a nice characterization of the space $W^{1,p}(U)$. When the dimension $n$ is larger than one, the spaces $W^{1,p}(U)$ can be characterized via *[absolute continuity on lines](https://en.wikipedia.org/wiki/Sobolev_space#Absolutely_continuous_on_lines_(ACL)_characterization_of_Sobolev_functions)*, which we won't cover here.

<div class='proposition' name='Characterization in One Dimension'>
Fix $1 \leq p < \infty$. For an open and bounded interval $U \subset \R$, we have $u \in W^{1,p}(U)$ if and only if $u$ is almost everywhere equal to an absolutely continuous function whose ordinary derivative is in $L^p(U)$. 
</div>
<details class="proof">
<summary> Proof. </summary>
Suppose $u \in W^{1,p}(U)$. Let $w(x) = \int_0^x u' \d \xi$. Note that $w$ is absolutely continuous, and hence $w'$ exists almost everywhere and $w' = u'$ almost everywhere. We thus have for every $\varphi \in C_c^\infty(U)$ that

\[
\int_0^1 u \varphi' \d \xi = - \int_0^1 w' \varphi \d \xi = \int_0^1 w \varphi' \d \xi.
\]

Since $\varphi$ was arbitrary we conclude that $u = w$ almost everywhere.

<br><br>

Conversely, suppose that $u$ is almost everywhere equal to an absolutely continuous function $w$ with $w' \in L^p(0, 1)$. It follows from the almost-everywhere uniqueness of weak derivatives that $u$ has weak derivative $w' \in L^p(0, 1)$, and we thus only need to check that $u \in L^p(0, 1)$. Note that for $1 < p < \infty$ an application of Holder's inequality yields

\[
|u(y) - u(x)| = \left| \int_x^y u' \d \xi \right| \leq |x - y|^{1 - 1/p} \lvert\lvert u' \rvert\rvert_{L^p(U)}.
\]

Hence, we see that $u \in L^p$ via
\[
\begin{aligned}
\lvert\lvert u \rvert \rvert_{L^p(U)}^p &= \int_0^1 |u|^p \d x \\
&= \int_0^1 \lvert u(0) + \int_0^x u' \d \xi \rvert^p \d x  \\
&\leq 2^p \int_0^1 \left(|u(0)|^p + |u(x) - u(0)|^p \right) \d x \\
&\leq 2^p\left( |u(0)|^p + \lvert\lvert u' \rvert\rvert^p_{L^p(U)} \right) < \infty.
\end{aligned}
\]
</details>



## Properties of Weak Derivatives

We now prove some properties of weak derivatives, illustrating that these behave in ways that one might expect from ordinary derivatives. Observe that the fourth result, in the case of $\|\alpha\| = 1$, is the usual product rule: $D^\alpha(\zeta u) = \zeta D^\alpha u + u D^\alpha \zeta$. 

<div class='theorem' name='Properties of Weak Derivatives'>
Fix $u, v \in W^{k,p}(U)$ and let $|\alpha| \leq k$. Then,
	<ol style="PADDING-LEFT: 2em">
		<li> $D^\alpha u \in W^{k-|\alpha|, p}(U)$, and $D^{\beta}(D^\alpha u) = D^{\alpha}(D^{\beta} u) = D^{\alpha + \beta} u$ whenever $|\alpha| + |\beta| \leq k$. </li>
		<li> Linearity: for arbitrary $\lambda, \mu \in \R$, we have $\lambda u + \mu v \in W^{k,p}(U)$ and $D^{\alpha}(\lambda u + \mu v) = \lambda D^{\alpha}u + \mu D^{\alpha} v$.  </li>
		<li> If $V \subset U$ is open, then $u \in W^{k,p}(V)$. </li>
		<li> Product Rule: If $\zeta \in C_c^\infty(U)$, then $\zeta u \in W^{k,p}(U)$ and 
			\[
			D^\alpha(\zeta u) = \sum_{\beta \leq \alpha} \binom{\alpha}{\beta} (D^\beta \zeta) (D^{\alpha - \beta} u).
			\]
		</li>
	</ol>
	</div>
<details class="proof">
<summary> Proof. </summary>
Fix $ \varphi \in C_c^\infty(U)$. 
	<ol style="PADDING-LEFT: 2em">
		<li> For any such $\beta$, we have that $D^\beta \varphi \in C_c^\infty(U)$. Hence,
		\[ 
		\int (D^\alpha u)(D^\beta u) \d x = (-1)^{-|\alpha|} \int u D^{\beta + \alpha } \varphi \d x = (-1)^{|\alpha| + |\beta|} \int (D^{\alpha + \beta} u) \varphi \d x.
		\]
		 </li>
		<li> Trivial. </li>
		<li> Trivial. </li>
		<li> We only prove the $|\alpha| = 1$ case. The general result follows from induction. To that end, we have by the usual product rule for smooth functions that
		\[
		\int_U u D^\alpha(\zeta \varphi) \d x = \int_U u (\zeta D^\alpha \varphi + \varphi D^\alpha \zeta) \d x
		\]
		
		which implies that
		
		\[
		\begin{aligned}
		\int_U (\zeta u) D^\alpha \varphi \d x &= \int_U u D^\alpha(\zeta \varphi) \d x- \int_U u \varphi D^\alpha \zeta \d x \\
		&= - \int_U [(D^\alpha u)(\zeta \varphi) - u \varphi D^\alpha \zeta ]\d x \\
		&= - \int_U [\zeta D^\alpha u + u D^\alpha \zeta] \varphi \d x.
		\end{aligned}
		\]		
		</li>
	</ol>
</details>











---
title: "Operator Classes"
topic: "Analysis"
chapter: "Functional Analysis"
section: "Operator Classes"
layout: note
permalink: "/notes/analysis/functional_analysis/operators/"

subtitle: 
date: 2025-04-07
keywords: gaussian measures, hilbert spaces, pettis integrals, bochner integrals
published: true
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 3."
---

Here we briefly review a few classes of operators which are particularly relevant for the study of Gaussian measures and probability on infinite-dimensional spaces. Throughout, $H$ will be a separable real Hilbert space.


Let $A$ be a linear operator on $H$.

<ol>
	<li> (<strong>Bounded</strong>) $L(H)$ is the class of bounded linear operators on $H$, equipped with the operator norm $|A| = \sup_{|x|\leq 1} |Ax|$. </li>
	<li> (<strong>Compact</strong>) $S_{\infty}(H) \subset L(H)$ is the class of compact operators, where $A$ is compact if it maps bounded sets to precompact sets. $S_\infty(H)$ is a subspace of $L(H)$, i.e., it is a closed vector space. </li>
	<li> (<strong>Hilbert-Schmidt</strong>) $S_2(H) \subset L(H)$ is the class of Hilbert-Schmidt operators, consisting of $A \in L(H)$ with finite Hilbert-Schmidt norm $|A|_2^2 = \sum_{k=1}^\infty |A e_k|^2$ for any orthonormal basis $(e_k)_{k=1}^\infty$ of $H$. The value of $|A|_2$ is independent of the choice of basis. Observe that $|A|_2^2 = \sum_{i,j=1}^\infty a_{ij}^2$, where $a_{ij} = \langle A e_i, e_j \rangle$ are the "entries" of $A$. The space $S_2(H)$ can be equipped with the inner product $\langle A, B \rangle = \sum_{i=1}^\infty \langle A e_i, B e_i \rangle$, under which $S_2(H)$ is a separable Hilbert space.</li>
</ol>

Unlike $S_\infty(H)$, the space of compact operators $L_2(H)$ is only a closed subset of $L(H)$ (in the norm topology) when $H$ is finite dimensional.


<div class='proposition' name='Properties of Hilbert-Schmidt Operators'>
Let $H$ be a separable real Hilbert space.

<ol>
	<li> $A \in S_2(H) \implies |A| \leq |A|_2$. </li>
	<li> $A \in L(H) \implies |A^*|_2 = |A|_2$. </li>
	<li> $A \in L(H), B \in S_2(H) \implies |AB|_2 \leq |A| |B|_2 \quad \textrm{&} \quad |BA|_2 \leq |B|_2 |A|$. </li>
</ol>
</div>

This proposition provides us with a few interpretations. First, the natural embedding $S_2(H) \hookrightarrow L(H)$ is continuous. Second, a bounded linear operator is Hilbert-Schmidt if and only if its adjoint $A^*$ is Hilbert-Schmidt. Third, $S_2(H)$ is a two-sided ideal of $L(H)$ (i.e., closed under multiplication from both sides by elements of $L(H)$).

<div class='proposition' name='Polar Decomposition'>
Recall that $A \in L(H)$ is positive if $\langle Ax, x \rangle \geq 0$ for all $x \in H$. If $A \in S_\infty(H)$, then we may decompose $A$ as $A = UT$, where
<ul>
	<li> $T \in S_{\infty}(H)$ is self-adjoint and positive</li>
	<li> $U \in L(H)$ is an isometry of $T(H)$ </li>
</ul>
</div>

In fact, one can say more. The operator $T$ can be given by the modulus of $A$, i.e., $T = (A^*A)^{1/2}$. Moreover, $U$ can be taken to vanish on the kernel of $T$ and $\|U\| \leq 1$. Recall that we can loosely think of $T$ as a scaling operator and $U$ as a rotation operator.

## Nuclear Operators

Let $A \in S_\infty(H)$ be compact. Since its modulus $T = (A^* A)^{1/2}$ is compact, self-adjoint, and positive, the spectral theorem shows that there exists an orthonormal basis for $H$ consisting of eigenvectors for $H$, and that all eigenvalues are real and non-negative. These non-negative eigenvalues of $(A^* A)^{1/2}$ are called the singular values of $A$.

<div class='definition' name='Nuclear Operators'>
The set $S_1(H) \subset S_\infty(H)$ is the class of nuclear operators, consisting of $A \in S_\infty(H)$ such that $\sum_{n=1}^\infty \alpha_n < \infty$, where $\alpha_n$ are the singular values of $A$ with multiplicity.
</div>

For $A \in S_1(H)$, its trace is given by
\\[
\text{tr} A = \sum_{n=1}^\infty \langle A e_n, e_n \rangle
\\]
which converges absolutely and is independent of the choice of orthonormal basis $(e\_n)\_{n=1}^\infty$. We equip $S\_1(H)$ with the norm $\|A\|\_1 = \sum_{n=1}^\infty \alpha_n$, where $\alpha_n$ are again the eigenvalues of $(A^* A)^{1/2}$ counted with multiplicity. Under this norm, $S_1(H)$ is a Banach space.

<div class='proposition' name='Properties of Nuclear Operators'>
Let $H$ be a separable real Hilbert space.

<ol>
	<li> $A \in S_1(H) \implies |A| \leq |A|_1$. </li>
	<li> $A, B \in S_2(H) \implies |AB|_1 \leq |A|_2 |B|_2 \implies AB \in S_1(H)$. </li>
	<li> $A \in S_1(H) \implies A$ is the product of two Hilbert-Schmidt operators.</li>
	<li> $A \in S_1(H) \implies |A|_2 \leq |A|_1 \implies A \in S_2(H)$. </li>
	<li> $A \in S_1(H) \implies |A^*|_1 = |A|_1$. </li>
	<li> $A \in L(H), B \in S_1(H) \implies |AB|_1 \leq |A| |B|_1 \quad \text{&} \quad |BA|_1 \leq |A| |B|_1$ </li>
</ol>
</div>

In particular, the natural embeddings $S_1(H) \hookrightarrow S_2(H)$ and $S_1(H) \hookrightarrow L(H)$ are continuous. If $A \in S_2(H)$ then $A^2 \in S_1(H)$. The nuclear operators form a two-sided ideal in $L(H)$.

We have the inclusions $S_1(H) \subset S_2(H) \subset S_\infty(H) \subset L(H)$, and generally these inclusions are strict. The set $S_0(H)$ of finite-rank operators (i.e., those with finite-dimensional images) is dense in $S_1(H), S_2(H), S_\infty(H)$ but not $L(H)$.

## S-Operators

<div class='definition' name='S-Operators'>
An operator $A$ is called an $S$-operator if it is nuclear, self-adjoint, and positive.
</div>

For example, in $\ell^2$, the diagonal operator $A = \text{diag}(a_n)_{n=1}^\infty$ is an $S$-operator if and only if $a\_n \geq 0$ and $\sum\_{n=1}^\infty a\_n < \infty$. In this case, $\text{tr}A = \sum\_{n=1}^\infty a_n$.

Now, suppose $A$ is an $S$-operator. In particular, it is compact and self-adjoint, so by the spectral theorem there is an eigenbasis $(e\_n)\_{n=1}^\infty$ with $A e\_n = \lambda\_n e\_n$ and $A x = \sum\_{n=1}^\infty \lambda\_n \langle x, e\_n \rangle e\_n$. By positivity, $\lambda_n \geq 0$. Since $A$ is self-adjoint and positive, $(A^* A)^{1/2} = A$ and in particular its singular values coincide with $(\lambda_n)$. Thus, as $A$ is nuclear, $\|A\|\_1 = \sum_{n=1}^\infty \lambda\_n < \infty$.

In fact, a converse to this holds, and we obtain a characterization of $S$ operators as those with non-negative summable eigenvalues.
<div class='proposition'>
Suppose $A$ is a self-adjoint positive operator in $H$. If there exists an orthonormal basis $(e_n)_{n=1}^\infty$ with
\[
\text{tr} A = \sum_{n=1}^\infty \langle A e_n, e_n \rangle < \infty
\]
then $A$ is nuclear, and in particular, an $S$-operator.
</div>

We use $L\_S(H)$ to denote the set of all $S$-operators. It is a convex cone in $S\_1(H)$ (i.e., closed under linear combinations with non-negative coefficients). Moreover $L\_S(H)$ is closed under the nuclear topology, i.e., if $(S\_n) \subset L_S(H)$ and $\|S\_n - S\|\_1 \to 0$, then $S \in L\_S(H)$. 
---
title: "Covariance Operators and Weak Moments"
topic: "Analysis"
chapter: "Functional Analysis"
section: "covariance"
layout: note
permalink: "/notes/analysis/functional_analysis/covariance/"

subtitle: 
date: 2025-04-16
keywords: gaussian measures, hilbert spaces, banach spaces, covariance operators
published: true
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 3."
---

In this note we study covariance operators in infinite-dimensional spaces. We begin with the Hilbert setting, focusing on strong moments. The main result is that a measure admits a strong second moment if and only if it admits an $S$-class covariance operator. From here, we drop the inner product and study boundedness of the weak moment multilinear forms on general normed spaces.

## Hilbert Setting

Throughout this section, $H$ will be a separable Hilbert space equipped with its Borel $\sigma$-algebra. We will use $L(H)$ to represent the set of bounded linear operators on $H$. It is clear that everything can be stated in terms of either random elements on $H$ or their corresponding (Borel) probability measures on $H$, and we will switch between these views when convenient.

<div class='definition' name='Covariance Operator'>
Let $H$ be a separable Hilbert space and suppose $\xi$ is a random element on $H$. An operator $C \in L(H)$ is called the covariance operator of $\xi$ if

\[
\langle C h_1, h_2 \rangle = \E \langle \xi, h_1 \rangle \langle \xi, h_2 \rangle \qquad \forall h_1, h_2 \in H.
\]

If $\xi$ admits a (weak or strong) mean $m$, then an element $S \in L(H)$ is called the correlation (or centered covariance) operator of $\xi$ if

\[
\langle S h_1, h_2 \rangle = \E \langle \xi - m, h_1 \rangle \langle \xi - m, h_2 \rangle \qquad \forall h_1, h_2 \in H.
\]
</div>

It is easy enough to check that when $\xi$ admits a mean $m$, the existence of a covariance operator is equivalent to the existence of a correlation operator, and the two are related by
\\[
\langle Sh_1, h_2 \rangle = \langle Ch_1, h_2 \rangle - \langle m, h_1 \rangle \langle m, h_2 \rangle
\\]
\\[
S = C - |m|^2 P_{[m]} \qquad P_{[m]}(x) = \frac{\langle x, m \rangle}{|m|^2} m
\\]

where $P_{[m]}: H \to H$ is the projection onto the span of $m$.

### Properties

The following proposition is immediate.
<div class='proposition'>
Let $C$ (resp. $S$) be the covariance (resp. correlation) operator of a random element $\xi$ on $H$. Then, $C$ (resp. $S$) is positive and self-adjoint.
</div>

Recall that an $S$-operator is a bounded linear operator on $H$ which is positive, self-adjoint, and nuclear. In the following we essentially show that existence of a well-behaved covariance operator is equivalent to $\mu$ having a finite strong second moment.

<div class='proposition'>
Suppose that $\mu \in \P(H)$ is a Borel probability measure.
<ol>
	<li> If $\E_\mu |x|^2 < \infty$, then $\mu$ admits a covariance operator $C_\mu$ which is an $S$-operator.</li>
	<li> Conversely, if $\mu$ admits an $S$-operator covariance $C_\mu$, then $\E_{\mu} |x|^2 < \infty$. </li>
</ol>
</div>
<details class='proof'>
<summary> Proof. </summary>
First suppose that $\E_\mu |x|^2 < \infty$. Then, the bilinear form $\sigma(h_1, h_2) = \E_\mu [\langle x, h_1 \rangle \langle x, h_2 \rangle]$ is bounded, and so there exists a bounded linear operator $C_\mu \in L(H)$ representing $\sigma$. Observe that $C_\mu$ is positive and self-adjoint, and moreover, for any orthonormal basis $(e_n)_{n=1}^\infty$,
\[
\begin{align}
\text{tr}(C_\mu) &= \sum_{n=1}^\infty \langle C_\mu e_n, e_n \rangle = \sum_{n=1}^\infty \int \langle x, e_n \rangle \langle x, e_n \rangle d \mu(x) \\
&= \int \left\langle x, \sum_{n=1}^\infty \langle x, e_n \rangle e_n \right\rangle d \mu(x) = \E_\mu |x|^2 < \infty.
\end{align}
\]

It follows (see e.g., the note on operator classes) that $C_\mu$ is nuclear, and thus is an $S$-operator.

The converse follows from running the same calculation backwards, and observing that $\text{tr}(C_\mu) = |C_\mu|_1 < \infty$ for positive self-adjoint operators.
</details>

An easy corollary is that the same result holds for the correlation operator of $\mu$. It is possible to construct probability measures which are compact but not $S$-operators, and such measures will necessarily have infinite strong second moments.

## Banach Setting

We switch now to the weaker setting where $B$ is assumed to be a (possibly non-separable) Banach space. In fact, where possible, we will state things in terms of a normed vector space $X$. We additionally shift our focus to weak moments.

<div class='definition' name='Weak Moments'>
Let $X$ be a normed vector space and $\mu \in \P(X)$ a Borel probability measure. The mapping $\sigma_n: (X^*)^n \to \R$ given by
\[
\sigma_n(z_1^*, \dots, z_n^*) = \int \langle z_1^*, x \rangle \dots \langle z_n^*, x \rangle d \mu(x)
\]

is the $n$th weak moment form of $\mu$.
</div>

It is immediately clear that $\sigma_n$ is a symmetric multilinear form on $X^*$. We will study the boundedness of this multilinear form. The most basic result is obtained when $\sigma_n$ is continuous, but this requires that our space be Banach. 


<div class='lemma' name='Boundedness of Continuous Multilinear Forms'>
Suppose $B$ is a Banach space and $A_n: B^n \to \R$ is a multilinear form which is continuous in each variable individually (i.e., holding all others fixed). Then, $A_n$ is bounded, i.e., there exists $C \geq 0$ with $|A_n(z_1, \dots, z_n)| \leq C |z_1| \cdots |z_n|$. 
</div>
<details class='proof'>
<summary> Proof. </summary>

The basic idea is induction and the Uniform Boundedness Principle. For $n=1$ this is well-known. Suppose the result holds for multilinear forms of order $n - 1$ for an arbitrary $n \geq 2$. Fix $z_1 \in B$. Then, $A_n(z_1, \cdot, \dots, \cdot): B^{n-1} \to \R$ is bounded by assumption, and there exists $C_{z_1} \geq 0$ such that $|A_n(z_1, z_2, \dots, z_n)| \leq C_{z_1}$ for any $|z_2|, \dots, |z_n| \leq 1$.

<br><br>

That is, for any $|z_2|, \dots, |z_n| \leq 1$, we obtain a continuous linear functional $\varphi_{z_2,\dots,z_n}: z_2 \mapsto A_n(z_1, z_2, \dots, z_n)$. Thus, $\sup_{z_2, \dots, z_n} |\varphi_{z_2, \dots, z_n}(z_1)| \leq C_{z_1} < \infty$ and so by the Uniform Boundedness Principle we see that $\sup_{z_2, \dots, z_n} |\varphi_{z_2, \dots, z_n}| \leq C$ is bounded for some $C \geq 0$. This is equivalent to our conclusion.
</details>

On the other hand, when $X$ is not necessarily Banach, it is sufficient that the multilinear form $\sigma_n$ be finite. We will make use of the previous lemma and the fact that $X^*$ is Banach.

<div class='theorem' name='Boundedness of Finite Multilinear Forms'>
Suppose that $\sigma_n: (X^*)^n \to \R$ is finite for every $(z_1^*, \dots, z_n^*) \in (X^*)^n$. Then, $\sigma_n$ is a bounded multilinear form.
</div>
<details class='proof'>
<summary> Proof. </summary>
It is immediate that $\sigma_n$ is a symmetric linear form on the Banach space $X^*$. By the previous lemma, it suffices to show that $\sigma_n$ is continuous in $z_1^*$ when we fix $z_2^*, \dots, z_n^*$.

<br><br>

For any $N \in \Z_{\geq 1}$, introduce the linear functional on $X^*$ given by 
\[
\varphi_N(z_1^*) = \int_{\overline{B}_N(0)} \langle z_1^*, x \rangle \dots \langle z_n^*, x \rangle d \mu(x).
\]

Observe that $\varphi_N$ is bounded, since $|\varphi_N(z_1^*)| \leq N^n |z_1^*| \dots |z_n^*|$. As $|\sigma_n(z_1^*, \dots, z_n^*)| < \infty$ is finite, both its positive and negative parts must be finite, hence

\[
|\varphi_N(z_1^*)| \leq \int_X |\langle z_1^*, x \rangle \dots \langle z_n^*, x \rangle| d \mu(x) =: C_{z_1} < \infty.
\]

By the Uniform Boundedness Principle we conclude $\sup_N |\varphi_N|$ is bounded. Since $\varphi_n(z_1^*) \to \sigma_n(z_1^*, z_2^*, \dots, z_n^*)$ pointwise, we have shown that $\sigma_n$ is continuous in its first argument, and thus we conclude by the previous lemma.
</details>

### First Moments

As an immediate corollary, we see that if $X$ is a reflexive space and $\mu \in \P(B)$ is such that $\sigma_1$ is finite, then $\mu$ admits a weak (Pettis) mean. See the note on Pettis integrals for a simpler proof under the assumption of having a finite strong first moment. It turns out we can even say something about the existence of a weak mean when $B$ is a separable (possibly non-reflexive) Banach space. The proof is quite technical and we skip it here because I'm lazy.

<div class='theorem' name='Existence of Weak Mean'>
Suppose $B$ is a separable Banach space and let $\mu \in \P(B)$ be a Borel probability measure. Assume that $\mu$ has finite strong $p$-th moment for some $1 < p < \infty$, i.e.,

\[
\int |\langle x, z^*\rangle|^p < \infty \qquad \forall z^* \in B^*.
\]

Then, $\mu$ admits a weak mean.
</div>

### Second Moments

At last, we are ready to specialize to the $n=2$ case and study covariance operators. Essentially, a covariance operator is a linear representative of the second order moment form. Covariance operators $C_\mu: X^* \to X^{**}$ are mappings from the dual to the double dual, which in finite dimensions can be thought of as encoding the action $x \mapsto x^T C_\mu$, i.e., the left-hand part of $x^T C_\mu y$. 

<div class='definition' name='Covariance Operator'>
Suppose that $X$ is a normed vector space, $\mu \in \P(X)$ is a Borel probability measure, and $C_\mu: X^* \to X^{**}$ is a bounded linear operator such that
\[
\langle C_\mu z_1^*, z_2^* \rangle = \sigma_2(z_1^*, z_2^*) = \int \langle x, z_1^* \rangle \langle x, z_2^* \rangle d \mu(x) \qquad \forall z_1^*, z_2^* \in X^*.
\]

Then, $C_\mu$ is called a covariance operator of $\mu$.
</div>

The correlation (or centered covariance) operator can analogously be defined via $\langle S\_\mu z\_1^\*, z\_2^\* \rangle = \sigma\_2(z\_1^\*, z\_2^\*) - \sigma\_1(z\_1^\*)\sigma\_1(z\_2^\*)$. Our general theorem yields the following easy corollary. Observe that when $X = H$ is Hilbert the following corollary holds to show the existence of a covariance operator $C_\mu: H \to H$ even in the non-separable case.

<div class='corollary'>
Suppose that $X$ is a normed vector space and $\mu \in \P(X)$. Suppose that $\sigma_2(z_1^*, z_2^*)$ is finite for all $z_1^*, z_2^* \in X^*$. Then, there exists a covariance (viz. correlation) operator $C_\mu: X^* \to X^{**}$. If $X$ is also a reflexive Banach space, there exists a covariance (viz. correlation) operator $C_\mu: X^* \to X$. 
</div>

Similar to the $n=1$ case, we can give existence of covariance operators $C_\mu: B^* \to B$ when $B$ is separable under stronger assumptions. We again skip the (not-so-easy) proof.

<div class='proposition'>
Suppose $B$ is a separable Banach space and $\mu \in \P(B)$ has finite weak second moments. Then, there exists a correlation operator (viz. covariance) $C_\mu: B^* \to B$.
</div>


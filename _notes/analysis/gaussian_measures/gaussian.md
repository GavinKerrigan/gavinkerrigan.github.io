---
title: "Gaussian Measures"
topic: "Analysis"
chapter: "Gaussian Measures"
section: "gaussian"
layout: note
permalink: "/notes/analysis/gaussian_measures/gaussian/"

subtitle: 
date: 2025-05-04
keywords: analysis, measure theory, gaussian measures
published: false
references: "Bogachev, V. (1998). Gaussian Measures, Chapter 2."
---

In this note $X$ is a locally convex topological vector space. Recall the notion of the cylindrical $\sigma$-algebra $\mathcal{C}$ over $X$. In general, this may be smaller than the Borel $\sigma$-algebra on $X$, but it coincides when e.g., $X$ is a separable Banach space. We will write $\P(X, \mathcal{C})$ for the space of cylindrical probability measures on $X$.

## Definitions and Elementary Properties

Gaussian measures are defined through their one-dimensional projections.

<div class='definition' name='Gaussian Measure'>
Let $X$ be a locally convex TVS. A probability measure $\gamma \in \P(\mathcal{C})$ is a Gaussian measure if for any $x^* \in X^*$, we have the pushforward $x^*_{\#} \mu$ is a Gaussian on $\R$.
</div>

An immediate consequence of the definition is that Gaussianity is preserved under affine transformations.

<div class='lemma'>
Let $\gamma \in \P(X, \mathcal{C})$ be a Gaussian measure. Suppose $T: X \to Y$ is a linear mapping to a locally convex space $Y$ such that $y^* \circ T \in X^*$ for all $y^* \in Y^*$. Then, $T_{\#} \gamma$ is a Gaussian measure on $Y$. If $y \in Y$ is fixed, then $S: x \mapsto Tx + y$ also results in a Gaussian measure $S_{\#} \gamma$ on $Y$.
</div>

For a given vector $h \in X$, we will use $\mu_h$ to denote the shift of the (Borel or cylindrical) measure $\mu$ by $h$. That is, $\mu_h(A) = \mu(A - h)$ for all measurable $A$. This is the pushforward of $\mu$ along translation by $h$.

Recall that in a previous note we showed that if two cylindrical measures have equal characteristic functions, then the measures agree. We now characterize Gaussian measures in terms of their characteristic functionals.

<div class='theorem'>
A measure $\gamma \in \P(X, \mathcal{C})$ is Gaussian if and only if its characteristic function has the form
\[
\varphi_\gamma(x^*) = \exp \left( iL(x^*) - \frac{1}{2} B(x^*, x^*) \right)
\]

for some linear $L: X^* \to \R$ and symmetric nonnegative bilinear form $B: X^* \times X^* \to \R$.
</div>
<details class='proof'>
<summary> Proof. </summary>
Suppose $\gamma$ is Gaussian. In particular, $x^* \in L^2(\gamma)$ for any $x^* \in X^*$ and so the centered weak first and second moments of $\gamma$ are well-defined, i.e.,
\[
L(x^*) = \int_X x^*(x) \d \mu(x)
\] 
\[
B(x_1^*, x_2^*) = \int_X (x_1^*(x) - L(x_1^*))(x_2^* - L(x_2^*)) \d \mu(x).
\]

We know that $L, B$ are as desired, and the characteristic function of $\gamma$ can be directly computed from the one-dimensional Gaussian characteristic function. The converse proceeds in the same manner.
</details>


Gaussian measures are called centered if all of their pushforwards along $X^*$ are centered. We obtain the following easy to check corollaries.
<div class='corollary'>
A Gaussian measure $\gamma \in \P(X, \mathcal{C})$ is centered if and only if $\gamma(A) = \gamma(-A)$ for all $A \in \mathcal{C}$. Equivalently, $L = 0$. 
</div>
<div class='corollary' name='Tensoring and Convolving Gaussians'>
Suppose $\gamma_1, \gamma_2 \in \P(X, \mathcal{C})$. The independent product measure $\gamma_1 \otimes \gamma_2$ on $X_1 \times X_2$ is a Gaussian measure. If $X = X_1 = X_2$, the convolution $\gamma_1 \star \gamma_2$ is a Gaussian measure on $X$. 
</div>

## The RKHS and Cameron-Martin Space

Suppose $\mu$ is a measure on $\mathcal{C}(X)$ such that $X^* \subset L^2(\mu)$. Recall that we can define a mean of $\mu$ via its weak first moment form as
\\[
m\_{\mu}(x^*) =  \int\_X x^\*(x) \d \mu(x).
\\]
In general, $m\_\mu$ is only an element of the algebraic dual $(X^\*)'$, i.e., is potentially unbounded (or even taking on infinite values).


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
Let $X$ be a locally convex TVS. A probability measure $\gamma \in \P(X, \mathcal{C})$ is a Gaussian measure if for any $x^* \in X^*$, we have the pushforward $x^*_{\#} \mu$ is a Gaussian on $\R$.
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
<div class='proposition' name='Centered Gaussians'>
A Gaussian measure $\gamma \in \P(X, \mathcal{C})$ is centered if and only if $\gamma(A) = \gamma(-A)$ for all $A \in \mathcal{C}$. Equivalently, $L = 0$. 
</div>
<div class='proposition' name='Tensoring and Convolving Gaussians'>
Suppose $\gamma_1, \gamma_2 \in \P(X, \mathcal{C})$. The independent product measure $\gamma_1 \otimes \gamma_2$ on $X_1 \times X_2$ is a Gaussian measure. If $X = X_1 = X_2$, the convolution $\gamma_1 \star \gamma_2$ is a Gaussian measure on $X$. 
</div>

## The RKHS and Cameron-Martin Space

Suppose $\mu$ is a measure on $\mathcal{C}(X)$ such that $X^* \subset L^2(\mu)$. Recall that we can define a mean of $\mu$ via its weak first moment form as
\\[
m\_{\mu}(x^*) =  \int\_X x^\*(x) \d \mu(x).
\\]
In general, $m\_\mu$ is only an element of the algebraic dual $(X^\*)'$, i.e., is potentially unbounded (or even taking on infinite values). Similarly, the correlation operator is defined via $C\_\mu: X^\* \to (X^\*)'$,
\\[
	C\_\mu(x\_1^\*)(x\_2^\*) = \int\_X (x\_1^\*(x) - m\_\mu(x\_1^\*))(x\_2^\*(x) - m\_\mu(x\_2^\*)) \d \mu(x).
\\]

<div class='definition' name='RKHS'>
 Let $\gamma \in \P(X, \CC)$ be a Gaussian measure on a locally convex space such that $X^* \subset L^2(\gamma)$. The reproducing kernel Hilbert space (RKHS) of $\gamma$ is the space
 \[
	X^*_\gamma = \overline{\{ x^* - m_\gamma(x^*) \mid x^* \in X^* \}^{L^2(\gamma)}}
 \]

equipped with the $L^2(\gamma)$ inner product, where the closure is taken with respect to $L^2(\gamma)$.
</div>
Note that as a closed subspace of a Hilbert space,  $X\_\gamma^\*$ is itself a Hilbert space.

This definition takes a little digesting.  Intuitively, what we have done is taken the dual space $X^\*$ (which is independent of the measure $\gamma$) and equipped it with a geometry that encodes the covariance structure of $\gamma$. Let's assume for a second $\gamma$ is centered so that $m\_\gamma(x^\*) = 0$ for all $x^\*$. Thinking of the dual space $X^\*$ as the collection of "generalized coordinates", the geometry of the RKHS then preicsely corresponds to the correlation between these coordinates, i.e.,
\\[
\langle x\_1^\*, x\_2^\* \rangle\_{L^2(\gamma)} = \int x\_1^\*(x) x\_2^\*(x) \d \gamma(x) = C\_\gamma(x\_1^\*)(x\_2^\*).
\\]
\\[
\|x^\*\|\_{L^2(\gamma)} = \sqrt{C\_\gamma(x^\*, x^\*)}.
\\]

Note that we can extend the correlation operator $C\_\gamma: X^\*\_\gamma \to (X^\*)'$ to all of $X^\*\_\gamma$ via
\\[
C\_\gamma(f)(x^\*) = \int f(x) (x^\*(x) - m\_\gamma(x^\*)) \d \gamma(x).
\\]

When $\gamma$ is centered this just extends the domain. Moreover, even if $\gamma$ is not centered, we can make sense of $C\_\gamma(x\_1^\*)$ for an arbitrary $x\_1^\* \in X^*$, since
\\[
\begin{align}
C\_\gamma(x\_1^\* - m(x\_1^\*))(x\_2^\*) &= \int (x\_1^\*(x) - m(x\_1^\*)) (x\_2^\*(x) - m(x\_2^\*)) \d \gamma(x) \\\\\\
&=  \int x\_1^\*(x) (x\_2^\*(x) - m(x\_2^\*)) \d \gamma(x) - m(x\_2^\*) \int (x\_1^\*(x) - m(x\_1^\*))d \gamma \\\\\\
&= \int x\_1^\*(x) (x\_2^\*(x) - m(x\_2^\*)) \d \gamma(x) \\\\\\
&= C\_\gamma(x\_1^\*)(x\_2^\*). 
\end{align}
\\]

We will also use the notation
\\[
\sigma^2(x^\*) = C\_\gamma(x^\*)(x^\*) = \int (x^\*(x) - m(x^\*))^2 \d \gamma(x) \qquad \forall x^\* \in X^\*
\\]
\\[
\sigma^2(x^\*) = \int x^\*(x)^2 \d \gamma(x) \qquad \forall x^\* \in X^\*\_{\gamma}.
\\]

<div class='definition' name='Cameron-Martin Space'>
	For $h \in X$, define
	\[
	|h|_{H(\gamma)} = \sup \{ x^*(h) \mid x^* \in X, C_\gamma(x^*)(x^*) \leq 1 \}.
	\]
	The Cameron-Martin space $H(\gamma) \subset X$ is defined as
	\[
	H(\gamma) = \{ h \in X \mid |h|_{H(\gamma)} < \infty \}.
	\]
	We will write $U_{H(\gamma)}$ for the closed unit ball in this space.
</div>

### Intuition

Let's take a step back and try to understand more intuitively what is going on. Let's assume $\gamma$ is centered. Moreover, anything involving $X\_\gamma^\*$ can essentially be understood by studying only the elements of $X^\*$ with the $L^2(\gamma)$ inner product and extending to the closure in an appropriate fashion. 

We can view $h \in X$ as acting on the RKHS $X^\*_{\gamma}$ via the evaluation functional
\\[
L\_h: X^\*\_\gamma \to \R \qquad L\_h : x^\*  \mapsto x^\*(h).
\\]
The Cameron-Martin norm $|h|\_{H(\gamma)}$ then corresponds to the operator norm of $L\_h$, and the Cameron-Martin space is the set of points $h \in H$ for which the evaluation functional on the RKHS is bounded. Thus, by the Riesz representation theorem, for any $h \in H(\gamma)$, there is a unique element $K\_h \in X^\*\_\gamma$ with $\langle x^\*, K\_h \rangle\_{L^2(\gamma)} = x^\*(h)$ for all $x^\* \in X^\*\_\gamma$ and $\|K\_h\|\_{L^2(\gamma)} = \|h\|\_{H(\gamma)}$. That is, we have an isometry $X^\*\_\gamma \simeq H(\gamma)$. Hence, what we have managed to do is (a) capture the geometry of $\gamma$ through $X\_\gamma^\*$, and (b) translate this geometry back into the original space via $H(\gamma)$. 

This now starts to resemble a bit our "ususal" notion of an RKHS on finite-dimensional spaces. Recall the usual sense is that a Hilbert space of functions $H$ over a finite dimensional space $X$ is an RKHS if the evaluation functional $L\_x$ is a bounded linear functional on $H$ for **every** $x \in X$. When $X$ is infinite dimensional, this will be far too strong, and we instead restrict our attention to preicsely to those $h \in X$ for which the evaluation functional is bounded, i.e., the Cameron-Martin space.

Here is a lemma to check our intuition further. Essentially, for a fixed $g \in X^\*\_\gamma$, its variance is given by the RKHS norm.
<div class='lemma'>
Let $\gamma \in \P(X, \CC)$ be a Guassian measure and $g \in X^*_\gamma$ be fixed. Then, $g_{\#} \gamma = \mathcal{N}\left(0, |g|^2_{L^2(\gamma)}\right)$. 
</div>
<details class='proof'>
<summary> Proof. </summary>
If $g = x^* - m_\gamma(x^*)$ for some $x^* \in X^*$, then it is not too hard to check that the characteristic function of $g_{\#}\mu$ is
\[
\varphi_{g_{\#}\mu}(t) = \exp\left( -\frac{1}{2} t^2 \sigma^2(g) \right).
\]

Now, for an arbitary $g \in X^*_\gamma$, there exists a sequence $g_k \to g$ in $L^2(\gamma)$ where each $g_k = x_k^* - m_\gamma(x_k^*)$. Convergence in $L^2(\gamma)$ implies convergence in measure, and since $|e^{iz}| \leq 1$, we can apply the Vitali convergence theorem to see that
\[
\varphi_{g_{\# \mu}}(t) = \int \exp(i t g(x)) \d \mu(x) = \lim_{k \to \infty} \int \exp(i t g_k(x)) = \lim_{k \to \infty} \exp \left( -\frac{1}{2} \sigma^2(g_k) \right).
\]

This shows that $d^2 = \lim_{k \to \infty} \sigma^2(g_k)$ exists, and that $g_{\#}\mu = \mathcal{N}(0, d^2)$. To conclude we need to check that $d^2 = \sigma^2(g)$, but this follows from the fact that $g_k \to g$ in $L^2(\gamma)$ and the triangle inequality.
</details>


### Example: Finite Dimensions

Let $X = \R^n$. Let's elaborate on these constructions in this case. Suppose $\gamma = N(0, \Sigma)$. In this case we can identify $X^\* \simeq \R^n$. The RKHS $X\_\gamma^\*$ is then just the space $\R^n$ equipped with the inner product
\\[
\langle a, b \rangle\_{\gamma} = a^{\sf T} \Sigma b = \langle \Sigma^{1/2} a, \Sigma^{1/2} b \rangle.
\\]
The Cameron-Martin norm is then
\\[
|h|\_{H(\gamma)} = \sup\\{ a^{\sf T} h \mid a \in \R^n, a^{\sf T}\Sigma a \leq 1 \\}.
\\]
If $\Sigma$ is invertible, then we can set $u = \Sigma^{-1/2} a$, so that the condition is now $u^{\sf T} u \leq 1$, and the maximization problem can be solved by inspection to yield
\\[
|h|\_{H(\gamma)} = \sqrt{h^{\sf T} \Sigma^{-1} h} = |\Sigma^{-1/2} h|.
\\]
Hence, the geometry on the Cameron-Martin space is actually the Mahalanobis geometry. Essentially, we "whiten" the measure $\gamma$ by applying $\Sigma^{-1}$. Thus, for invertible $\Sigma$, the Cameron-Martin space is all of $\R^n$. For non-invertible $\Sigma$, this is finite only if $h \in \Sigma(\R^n)$ -- or, equivalently, $h \in \Sigma^{1/2}(\R^n)$, since $\Sigma(\R^n) \subset \Sigma^{1/2}(\R^n)$ is clear and the square root of a matrix has the same rank as the original matrix.

Here are a few intuitive ways of thinking about things.
<ul>
 <li> 
When $\Sigma$ has a large eigenvalue in some direction (i.e., has high variance in this direction), then $\Sigma^{-1}$ has a *small* eigenvalue in this direction, and thus the value of $h$ along this direction matters *less*. Conversely, the variability of $h$ along directions with small variance matters a lot. At the extreme, if $h$ is along a direction of *no* variability, then $|h|_{H(\gamma)}$ will be infinite. </li>
<li> Another way of thinking about this is that it measures the "decay of mass" or rate of change of the measure in the direction $h$ -- since a direction with low variance will be concentrated and have a steep density. The Cameron-Martin norm thus measures how much the measure changes when translated in the direction $h$. A direction $h$ with infinite Cameron-Martin norm will therefore be a step in a direction with no mass. </li>
<li> Note that the density $p_\gamma(h) \propto \exp(-\frac{1}{2} |h|_{H(\gamma)}^2)$, and so the Cameron-Martin norm is large when it has small likelihood under $\gamma$, i.e., points in a direction of low mass. </li>
<li> The unit ball of the Cameron-Martin norm is precisely the "one-standard deviation" ellipsoid for $\gamma$. </li>
</ul>


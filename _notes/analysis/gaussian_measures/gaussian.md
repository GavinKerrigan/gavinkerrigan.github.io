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
Similarly, the correlation operator is defined via $C\_\mu: X^\* \to (X^\*)'$,
\\[
	C\_\mu(x\_1^\*)(x\_2^\*) = \int\_X (x\_1^\*(x) - m\_\mu(x\_1^\*))(x\_2^\*(x) - m\_\mu(x\_2^\*)) \d \mu(x).
\\]

In general, $m\_\mu$ and $C\_\gamma(x^\*)$ are only elements of the algebraic dual $(X^\*)'$. That is, it is possible that the mean is not an element of $X$ and that the correlation is not a map $C\_\gamma: X^\* \to X$. However, for Radon Gaussian measures (e.g., on separable Banach spaces), no such obstruction occurs.

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

Note we can also define a correlation operator $\widetilde{C}\_\gamma: X\_\gamma^\* \to (X^\*)'$ via
\\[
	\widetilde{C}\_\gamma(f)(x^\*) = \int f(x) (x^\*(x) - m(x^\*)) \d \gamma(x).
\\]

For centered measures $\gamma$, we have $X^\* \subset X\_\gamma^\*$, and so this is just an extension of $C\_\gamma$. For arbitrary $x^\* \in X^\*$, we also have $C\_\gamma(x^\*) = \widetilde{C}\_\gamma(x^\* - m_\gamma(x^\*))$. We will often just write $C\_\gamma$ for both when it is clear from context.

We will also use the notation
\\[
\sigma^2(x^\*) = C\_\gamma(x^\*)(x^\*) = \int (x^\*(x) - m(x^\*))^2 \d \gamma(x) \qquad \forall x^\* \in X^\*
\\]
\\[
\sigma^2(f) = \widetilde{C}\_\gamma(f)(f) \int f(x)^2 \d \gamma(x) \qquad \forall f \in X^\*\_{\gamma}.
\\]

<div class='definition' name='Cameron-Martin Space'>
	For $h \in X$, define
	\[
	|h|_{H(\gamma)} = \sup \{ x^*(h) \mid x^* \in X^*, C_\gamma(x^*)(x^*) \leq 1 \}.
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


## Example: Finite Dimensions

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

## Example: Separable Hilbert Spaces

When $X$ is a separable Hilbert space, everything is as nice as could be. Here, we identify $X = X^\*$ via Riesz representation. The following theorem shows that Gaussian measures on $X$ are in one-to-one correspondence with a choice of mean and symmetric, nonnegative, nuclear correlation operator.

In this case, the mean is an element $m \in X$ and the correlation operator $K: X \to X$ satisfies
\\[
\langle C\_\gamma x_1, x_2 \rangle = \int_X \langle x\_1, x - m \rangle \langle x\_2, x - m \rangle \d \gamma(x).
\\]

The following theorem is not too hard to prove. In one direction, we already know how the characteristic functionals of Gaussians look, and so we only need to apply Riesz representation and check the covariance is nuclear. This follows from Fernique's theorem which shows Gaussians on separable Banach spaces have finite strong second moments. In the other direction, we directly construct a corresponding Gaussian random variable via the spectrum of $K$.

<div class='theorem'>
Let $X$ be a separable Hilbert space. If $\gamma$ is a Gaussian measure on $X$, then there exists $m \in X$ and a symmetric, nonnegative, nuclear operator $K: X \to X$ such that the characteristic functional of $\gamma$ is
\[
\varphi_\gamma(x) = \exp\left( i \langle m, x \rangle - \frac{1}{2} \langle Kx, x \rangle \right).
\]
The vector $m$ is the mean of $\gamma$ and $K$ is its correlation operator. Conversely, given any $m \in X$ and symmetric nonnegative nuclear $K: X \to X$, there exists a Gaussian measure $\gamma$ with mean $m$ and correlation $K$.
</div>
<details class='proof'>
<summary> Proof. </summary>
Since $\gamma$ is Gaussian, we have $\varphi_\gamma(x) = \exp(i L(x) - \frac{1}{2}B(x, x))$ for some linear $L: X \to \R$ and symmetric bilinear $B: X \times X \to \R$. By the dominated convergence theorem, $\varphi_\gamma$ is continuous. By considering a sequence $x_n \to 0$, we also see that $L, B$ are continuous. By the Riesz representation theorem, there exists $m \in X$ and a bounded nonnegative symmetric operator $K: X \to X$ with
\[
L(x) = \langle m, x \rangle \qquad B(x, x) = \langle Kx , x \rangle.
\]

We first check that $K$ is compact. Suppose $x_n \to 0$ weakly. Then, by dominated convergence, $\varphi_\gamma(x_n) \to 1$. It follows that $|\sqrt{K} x_n|^2 = \langle K x_n, x_n \rangle \to 0$. Thus, $\sqrt{K}$ is compact (as it maps weakly converging sequences to strongly converging sequences) and so $K$ is compact (as the composition of compact operators).

<br><br>

We now need to show that $K$ is nuclear. Using Fernique's theorem, we see that $\int |x|^2 \d \gamma(x) < \infty$. Since $\gamma$ has finite strong second moments, it follows that $K$ is nuclear (see the note on covariance operators).

<br><br> Conversely, suppose $m, K$ are as hypothesized. Then, $K$ admits an orthonormal eigenbasis $(e_n)_{n=1}^\infty$ with $K e_n = \lambda_n e_n$. Since $K$ is nuclear, $\sum_n \lambda_n < \infty$. Recall a sum $\sum a_n e_n$ in a Hilbert space converges iff $\sum |a_n|^2 < \infty$. Now, let $(\xi_n)_{n=1}^\infty$ be a sequence of independent standard Gaussian random variables. Set
\[
\xi(\omega) = m + \sum_{n=1}^\infty \sqrt{\lambda_n} \xi_n(\omega) e_n.
\]
We claim this converges almost surely. Indeed, it suffices to show that $\sum_{n=1}^\infty \lambda_n |\xi_n(\omega)|^2$ converges almost surely. Consider
\[
\lim_{N \to \infty} \int \sum_{n=1}^N \lambda_n |\xi_n(\omega)|^2 \d \P(\omega) = \lim_{N \to \infty} \sum_{n=1}^N \lambda_n < \infty.
\]

By the monotone convergence theorem we conclude. It is easy to check that the distribution of $X$ is Gaussian with the desired mean and covariance.
</details>

An immediate consequence of this is that there is no such thing as white noise on $X$, because the identity operator is not compact.

<div class='proposition'>
If $\textrm{dim}(X) = \infty$, then $\varphi(x) = \exp(-\frac{1}{2} |x|^2)$ is not the Fourier transform of any countably additive measure on $X$. That is, there does not exist a mean-zero Gaussian measure on $X$ whose covariance is $K = \mathrm{Id}$.
</div>

### Identifying the RKHS and Cameron-Martin Spaces

Suppose that $\gamma$ is centered so that the correlation operator $K: X \to X$ satisfies
\\[
\langle K x\_1, x\_2 \rangle = \int \langle x\_1, x \rangle \langle x\_2, x \rangle \d \gamma(x).
\\]

Then, $X^\*\_\gamma$ coincides with the limit points of Cauchy sequences in the norm $\| \cdot \|\_{L^2(\gamma)} = \| \sqrt{K}(\cdot) \|\_X = \| \cdot \|\_{C\_\gamma}$. In other words, the RKHS is the completion of $X$ with respect to this norm. Thus, if $C\_\gamma$ admits an orthonormal eigenbasis $(e\_n)$ with eigenvalues $(\lambda\_n)$, we have $\| x\|\_K^2 = \sum \lambda\_n x\_n^2$. The completion of $X$ with respect to this norm is then the limit points of $x \in X$ with $\|x \|\_{C\_\gamma} < \infty$, i.e., consisting of all elements $x = \sum x\_n e\_n$ represented by formal sequences of the form
\\[
 \left\\{ (x\_n) \mid \sum \lambda\_n x\_n^2 < \infty \right\\}.
\\]

Although $\\{ x \in X \mid \|x \|\_{K} < \infty \\} \subset X$ we will generally not have that the completion is contained within $X$ since this new norm is weaker (as $\lambda\_n \to 0$). Long story short, we can identify the RKHS as
\\[
X^*\_\gamma = \left\\{ x = \sum x\_n e\_n \mid \sum \lambda\_n x\_n^2 < \infty \right\\}.
\\]

We can naturally extend the correlation operator to $C\_\gamma: X^\*\_\gamma \to X^\*\_\gamma$ via
\\[
x = \sum x\_n e\_n \mapsto \sum \lambda\_n x\_n e\_n \qquad \forall x \in X^\*\_\gamma.
\\]
This is an element of $X^\*\_\gamma$ since $\sum \lambda\_n (\lambda\_n x\_n)^2 \leq (\sup \lambda\_n)^2 \sum \lambda\_n x\_n^2 < \infty$.

Now, observe that in a fashion analogous to the finite-dimensional case, we have that $h \in X$ has finite Cameron-Martin norm precisely when $\sum \lambda\_n^{-1} h\_n^2 < \infty$. We can thus identify $H(\gamma) = K(X^\*\_\gamma)$ when this operator is viewed as being defined on the whole of the RKHS, or as $H(\gamma) = \sqrt{K}(X)$ if we only take $K$ to be defined on $X$.

In stark contrast with the finite-dimensional world, the Cameron-Martin space has measure zero under $\gamma$. To see this, note that $\xi(\omega) = \sum \lambda\_n \xi\_n(\omega) e\_n$ is $\xi \sim \gamma$ where $\xi\_n$ are i.i.d. $\mathcal{N}(0, 1)$. Computing $\|\xi\|\_{H(\gamma)}$ shows this quantity is infinite almost surely.

Although the domain of $K^{-1/2}$ is thus of measure zero, for arbitrary $v \in X$ we can define $K^{-1/2} v$ as the element $I(v) \in X^\*\_\gamma$ corresponding to $\sqrt{K}v \in H(\gamma)$, i.e., such that $I(v)(x) = \langle x, \sqrt{K} v \rangle$ for $x \in H(\gamma)$. Loosely, I think the idea here is to write $\langle K y, K^{-1/2} v \rangle = \langle y, K^{1/2} v \rangle$ where $y \in K(X^\*\_\gamma)$. Generally, $\langle I(v), I(w) \rangle\_{L^2(\gamma)} = \langle \sqrt{K} v, \sqrt{K}w \rangle\_{H(\gamma)} = \langle v, w \rangle\_X$. 

### Calculations

For an arbitrary $m \in X$, we have that the characteristic functional of $\gamma$ is
\\[
\varphi\_\gamma(y) = \exp \left( i \sum m\_n y\_n - \frac{1}{2} \sum \lambda\_n y\_n^2 \right).
\\]

For $m=0$ and a cylindrical set $C = P\_n^{-1}(B)$ for $B \in \BB(\R^n)$ with $P\_n: X \to \text{span}\\{e\_1, \dots, e\_n \\}$, we have that
\\[
\gamma(C) = \int_B \prod_{j=1}^n \frac{1}{\sqrt{2 \pi \lambda_j}} \exp \left( - \frac{1}{2} x_j^2 \right) \d x\_1 \dots \d x\_n.
\\]
That is, we may write $\gamma(C)$ in terms of the $n$-dimensional Gaussian density with diagonal covariance $\text{diag}\\{ \lambda\_1, \dots, \lambda\_n \\}$. Similar calculations hold for other cylindrical sets.

## Gaussian Processes

ToDo.

## The Cameron-Martin Space

We now proceed to study the Cameron-Martin space in full generality. The Hilbert case should be kept in mind throughout as a guiding principal. 

Our first lemma shows that the Cameron-Martin space is actually obtained from the RKHS. The notation here is a bit confusing, but recall that $C_\gamma(g) \in X^{**}$, so that $h = C\_\gamma(g)$ really means that $f(h) = C\_\gamma(g)(f)$ for every $f \in X^\*$. That is, $f(h) = \langle g, f - m\_\gamma(f) \rangle\_{L^2(\gamma)}$ for every $f \in X^\*$. Hence, speaking very loosely here, we have $h^{\sf T} = \langle g, \cdot \rangle\_{L^2(\gamma)}$. In other words, if $g = f - m(f)$ for some $f \in X^\*$, then we essentially have $h = C\_\mu(f - m(f))$, thinking of this as a covariance matrix.

So in a sense, the fundamental thing is the RKHS $X^*_\gamma$ equipped with the $L^2(\gamma)$ geometry.  The dual of this space (within $X$) is the Cameron-Martin space. The operator $C\_\gamma$ can (...maybe?) be seen as some kind of Riesz map between these spaces.


<div class='lemma'>
A vector $h \in X$ is an element of the Cameron-Martin space $H(\gamma)$ if and only if there exists $g \in X^*_\gamma$ with $h = C_\gamma(g)$. In this case, $|h|_{H(\gamma)} = |g|_{L^2(\gamma)}$.
</div>
<details class='proof'>
<summary> Proof. </summary>
Fix $h \in X$ with $|h|_\gamma < \infty$. Consider the mapping $\varphi_h: f - m_\gamma(f) \mapsto f(h)$ for $f \in X^*$. Observe that the norm of this functional is
\[
\begin{align}
|\varphi_h| &= \sup\{ \varphi(f - m_\gamma(f)) \mid f \in X^*, C_\gamma(f)(f) \leq 1 \} \\
&= \sup\{ f(h) \mid f \in X^*, C_\gamma(f)(f) \leq 1 \} \\
&= |h|_{H(\gamma)}
\end{align}
\]
and hence it is continuous. Thus this extends to a continuous linear functional $\varphi_h: X^*_\gamma \to \R$ defined on all of the RKHS. By the Riesz representation theorem, there exists an element $g \in X^*_\gamma$ such that $\varphi_h(f - m(f)) = \langle g, f - m(f) \rangle_{L^2(\gamma)}$ for every $f \in X^*$. That is, we have shown $f(h) = C_\gamma(g)(f)$ for every $f \in X^*$, and so $h = C_\gamma(g)$.

<br><br>

Conversely, if $h = C_\gamma(g)$ for some $g \in X^*_\gamma$, then $f(h) = \langle g, f - m_\gamma(f)\rangle_{L^2(\gamma)}$ for all $f \in X^*$. Thus,
\[
\begin{align}
|h|_{H(\gamma)} &= \sup \{ f(h) \mid f \in X^*, C_\gamma(f^*)(f^*) \leq 1 \} \\
&= \sup \{ \langle g, f - m_\gamma(f) \rangle_{L^2(\gamma)} \mid f \in X^*, C_\gamma(f^*)(f^*) \leq 1 \} \\
&= \sup \{ \langle g, x \rangle_{L^2(\gamma)} \mid x \in X^*_\gamma, |x|_{L^2(\gamma)} \leq 1 \} \\
&= |g|_{L^2(\gamma)}.
\end{align}
\]

</details>

When $h = C\_\gamma(g)$, we will say that $g$ is associated with or generated by $h \in H(\gamma)$, and we will write $\hat{h} = g$. In other words, $\hat{h}$ is the element in $X^\*_\gamma$ satisfying
\\[
f(h) = \int \hat{h}(x) (f(x) - m\_\gamma(x)) \d \gamma(x) \qquad \forall f \in X^\*.
\\]

We define an inner product on $H(\gamma)$ via
\\[
\langle k, v \rangle\_{H(\gamma)} = \langle \hat{h}, \hat{k} \rangle\_{L^2(\gamma)}
\\]
with corresponding norm
\\[
\|h\|\_{H(\gamma)} = \|\hat{h}\|\_{L^2(\gamma)}.
\\]

Speaking loosely, we should think of $\hat{h} = C\_\gamma^{-1}h$. That is, when $g = f - m(f)$ is given by some $f \in X^\*$, we should expect to recover $f = C\_\gamma^{-1}(h) + m(f)$.

In this way we have transferred the geometry of $X^\*\_\gamma$ back into $X$. When $C\_\gamma(X^\*\_\gamma) \subset X$, then $H(\gamma) = C\_\gamma(X^\*\_\gamma)$ by the previous lemma. However, in general this inclusion may fail, i.e., there may be elements in this image outside of $X$. In this case, $H(\gamma)$ with the norm $\|C\_\gamma(f)\|\_{H(\gamma)}^2 = C\_\gamma(f)(f)$ makes $H(\gamma)$ into a Hilbert space and $C\_\gamma$ is an isomorphism between $X^\*_\gamma$ and $H(\gamma)$.

### Translations

Suppose that in finite dimensions we have $p = N(m, \Sigma)$ and $q = N(m + h, \Sigma)$. That is, $q$ is obtained by translating $p$ along $h$. It follows from a short calculation that
\\[
\frac{q(x)}{p(x)} = \exp \left( h^{\sf T} \Sigma^{-1}(x - m) - \frac{1}{2} h^{\sf T} \Sigma^{-1} h \right).
\\]

Thus, in infinite dimensions, we should expect that translations along $h \in H(\gamma)$, where this second term is finite, result in measures that admit a density with respect to the original Gaussian.

Note that in finite dimensions it's easy to lose track of the centering terms. What is going on is that, abstractly, the centered functional is $g\_c = g - m(g) = C\_\gamma^{-1}(h)$. In finite dimensions $X^\*\_\gamma$ is identified with $\R^n$ via $g\_c \mapsto g \in \R^n$. The action of $g\_c$ is then $g\_c(x) = g^{\sf T}(x - m)$. You might then expect that $g\_c = \Sigma^{-1}h$ and indeed this is essentially the case, but in fact the vector $\Sigma^{-1}h$ is the **representation** of $g\_c$ under this isomorphism, so that $g\_c(x) = (\Sigma^{-1} h)^{\sf T}(x - m)$.



<div class='proposition'>
Let $\gamma$ be a Gaussian measure on a LCTVS $X$ and let $g \in X^*_\gamma$ be fixed. Define the measure $\nu$ on $X$ by its density with respect to $\gamma$ given by
\[
p(x) = \frac{\d \nu}{\d \gamma}(x) = \exp \left( g(x) - \frac{1}{2} \sigma^2(g) \right).
\]

Then, $\nu$ is a Gaussian measure with characteristic functional
\[
\varphi_\nu(f) = \exp\left( i(C_\gamma(g)(f) + m_\gamma(f)) - \frac{1}{2}\sigma^2(f) \right).
\]

</div>
<details class='proof'>
<summary> Proof. </summary>
Observe that the density $p$ results in a well-defined finite measure $nu$ since $\exp |g| \in L^1(\gamma)$. Its characteristic functional is thus 

\[
\begin{align}
\varphi_\nu(f) &= \int \exp(i f(x)) p(x) \d \gamma(x) \\
&= \exp(i m_\gamma(f) - \frac{1}{2}\sigma^2(g)) \int \exp(i (f - m_\gamma(f) - ig)) \d \gamma(x).
\end{align}
\]
Write $k = \exp(i m_\gamma(f) - \frac{1}{2}\sigma^2(g))$ and consider the function $\psi: \R \to \C$ given by
\[
\psi(z) = k \int \exp(i (f - m_\gamma(f) - z g)) \d \gamma(z).
\]

Since $f - m_\gamma(f) - zg \in X^*_\gamma$, we can calculate via the characteristic functional of $\gamma$ that
\[
\begin{align}
\psi(z) &= k \exp \left( -\frac{1}{2} \int (f - m_\gamma(f) - z g)^2 \right) \\
&= k \exp \left( -\frac{1}{2} \sigma^2(f) - \frac{1}{2}z^2 \sigma^2(g) + zC_\gamma(g)(f) \right)
\end{align}
\]

Extending $\psi$ to $\C$ and taking $z \to i$, the dominated convergence theorem yields $\psi(z) \to \varphi_\nu(f)$, yielding the claimed expression for $\varphi_\nu(f)$.
</details>

<div class='theorem' name='Cameron-Martin Theorem'>
Let $\gamma$ be a Gaussian measure on a LCTVS $X$. Then, for any $h \in H(\gamma)$ with $h = C_\gamma(g)$ for some $g \in X^*_\gamma$, let $T_h: X \to X$ be $x \mapsto x + h$. Then, $\gamma_h = (T_h)_{\#} \gamma$ is equivalent to $\gamma$, and admits density
\[
\frac{\d \gamma_h}{\d \gamma}(x) = \exp \left(g(x) - \frac{1}{2}|h|^2_{H(\gamma)} \right).
\]
</div>
<details class='proof'>
<summary> Proof. </summary>
Observe that since $f(h) = C\_\gamma(g)$ for all $f \in X^*$, we have
\[\begin{align}
\varphi_{\gamma_h}(f) &= \int \exp(i f(x)) \d \gamma_h(x) \\
&= \exp(i f(h)) \int \exp(i f(x)) \d \gamma(x) \\
&= \exp\left(i m(f) + iC_\gamma(g)(f) - \frac{1}{2}C_\gamma(f)(f)\right).
\end{align}
\]

The previous proposition allows us to conclude.

</details>

ToDo: finish this section at some point.

NOTE TO SELF! I think you can think of $C\_\gamma(f) = \int x f(x) \d \gamma$.....
---
title: "Hilbert-Schmidt Independence Criterion"
topic: "Machine Learning"
chapter: "Kernel Methods"
section: "kernel"
layout: note
permalink: "/notes/ml/kernel/hsic/"

subtitle: 
date: 2025-10-29
keywords: hsic, kernel methods, independence criteria
published: true
references: "Gretton, A., Bousequet, O., Smola, A., Scholkopf, B. (2005). Measuring Statistical Dependence with Hilbert-Schmidt Norms.; Song, L., Smola, A., Gretton, A., Borgwardt, K., Bedo, J. (2007). Supervised Feature Selection via Dependence Estimation."
---

How do we quantify the degree to which two random variables $X$ and $Y$ are dependent? And if we only have samples, can we estimate this quantity?

In this note we're going to see how you could have invented the Hilbert-Schmidt Independence Criterion (HSIC) to answer these question. We're going to eschew some of the analytical and technical details in favor of demonstrating how to do calculations and the motivation behind certain steps and definitions. Along the way we'll see some heuristics for how one can "lift" finite-dimensional linear algebra calculations into an RKHS.

Throughout, we'll use $\mathcal{X}, \mathcal{Y}$ to represent two distinct spaces, and we assume there is some joint probability distribution $p(x,y)$ defined over $\mathcal{X} \times \mathcal{Y}$. 

## Warmup: Scalar Covariance

If $X, Y$ are scalars, a natural idea is to measure their covariance.

Let $\mu_x = \E_{p(x)}[x], \mu_y = \E_{p(y)}[y]$ be the means of the marginals of our distribution. The covariance is given by
\\[
\begin{align}
\Sigma_{XY} &= \E_{p(x,y)}\left[ (x - \mu_x)(y - \mu_y) \right] \\\\\\
                 &= \E_{p(x,y)} \left[ xy \right] -\E_{p(x) p(y)}[x y] \\\\\\
                 &= \E_{p(x,y)} \left[ xy \right] - \mu_x \mu_y.
\end{align}
\\]

We can view this in two complementary ways. Thinking of a product as a kind of similarity, the first line shows us that this can be thought of as an expected similarity between centered versions of $x$ and $y$. On the other hand, the second line shows us that the covariance is a kind of "first order" dependency measure, comparing the first moment of $p(x, y)$, under which our data is coupled, and $p(x)p(y)$, under which it is independent.

This is a natural choice, as if $X, Y$ are independent, then their covariance is zero. The converse to this, of course, does not hold -- i.e., zero covariance does not imply independence. Intuitively, this is a failure of first moments to *separate* distributions. The HSIC is designed to alleviate this failure by capturing additional statistics of the distributions via a feature transformation.

## Vector Covariance

Before getting to the HSIC, let's take one step up in complexity and consider vector-valued $X, Y$. We need to do a bit more work to get a scalar measure of dependency. Write $w \otimes z$ for the tensor (i.e., $w \otimes z = w z^T$) product of two vectors -- we're doing this with a bit of foresight, as we'll soon generalize this calculation to infinite dimensional spaces. Computing their covariance now yields a *matrix*
\\[
\begin{align}
\Sigma_{XY} &= \E_{p(x, y)}\left[ (x - \mu_x) \otimes (y - \mu_y) \right] \\\\\\
                 &= \E_{p(x,y)} \left[ x \otimes y \right] - \mu_x \otimes \mu_y.
\end{align}
\\]

How can we turn this matrix into a scalar? Again, we reach for a natural choice, which is its Hilbert-Schmidt (or Frobenius) norm, which essentially treats $\Sigma_{XY}$ as flattened vector and computes its $\ell_2$ norm
\\[
||\Sigma_{XY}||^2_{HS} = \sum\_{i,j} \text{Cov}(X_i,Y_j)^2 = \textrm{tr}(\Sigma\_{XY} \Sigma\_{XY}^T).
\\]

This yields a measure of dependency corresponding to the "size" of the covariance matrix.

### Estimating from Data
Suppose we have i.i.d. samples $\{(x\_i, y\_i)\}\_{i=1}^m \sim p(x,y)$. To estimate $\lvert\lvert \Sigma_{XY} \rvert\rvert_{HS}^2$ from this sample, the idea is to replace $\Sigma_{XY}$ with an empirical version $\widehat{\Sigma}\_{XY}$ and compute its Hilbert-Schmidt norm. From here, it's just linear algebra, but it's useful to see it done out a bit.

In an abuse of notation, let's write $X \in \R^{d_x \times m}, Y \in \R^{d_y \times m}$ for our samples, stacked in the columns of a matrix. We need to center $X, Y$ and take their tensor product. To that end, let $\mathbf{1}$ be the $m$-vector of all ones. An empirical estimate for the means is given by
\\[
\mu_x \approx \frac{1}{m} X \mathbf{1} \qquad \mu_y \approx \frac{1}{m} Y \mathbf{1}.
\\]
We need to broadcast these estimates which can be achieved by right-multiplying with $\mathbf{1}^T$. In short, we get centered data $XH, YH$ by right-multiplying with $H = I - \frac{1}{m} \mathbf{1} \mathbf{1}^T$. It's easy to check that $H$ is symmetric and idempotent ($H^2 = H$). In short, our empirical covariance matrix can be written as 
\\[
\widehat{\Sigma}\_{XY} = \frac{1}{m-1} XH \otimes YH = \frac{1}{m-1} XHH^TU^T = \frac{1}{m-1} X H Y^T
\\]
where we've chosen to normalize by $m-1$ since we lost a degree of freedom in the mean estimate. Now, computing the Hilbert-Schmidt norm simply amounts to using the cyclic property of the trace to see
\\[
||\widehat{\Sigma}\_{XY}||\_{HS}^2 = \frac{1}{(m-1)^2} \textrm{tr}\left( (X^T X) H (Y^T Y) H\right).
\\]

Stepping back, we see that we need to compute the product of centered Gram matrices $X^T X, Y^T X$. These consist of inner products on $\mathcal{X}, \mathcal{Y}$ alone. This suggests that we should be able to successfully replicate this calculation in the RKHS setting, where these Gram matrices are replaced by the appropriate kernel matrices.

## The Hilbert Schmidt Independence Criterion

The main idea behind the HSIC is to lift the feature spaces $\mathcal{X}, \mathcal{Y}$ via feature maps $\phi, \psi$ followed by computing the Hilbert-Schmidt norm of the resulting covariance operator. We need to be a bit careful as our new feature spaces are in general infinite-dimensional, and so some functional analytic ideas come into play -- but we emphasize that the key ideas are present in the finite-dimensional case. The important thing to note is that, as everything depends only on Gram matrices, we can make things tractable when it comes time to compute by choosing our feature spaces to be reproducing kernel Hilbert spaces (RKHS).

We recall that a space $\mathcal{F}$ of functions $f: \mathcal{X} \to \R$ is called an RKHS if the evaluation functionals are bounded. Associated to every $x \in \mathcal{X}$ is an associated *feature* $\phi(x) \in \mathcal{F}$, and moreover, $\langle \phi(x), \phi(x') \rangle_{\mathcal{F}} = k(x, x')$ for some unique positive definite kernel $k: \mathcal{X}^2 \to \R$. We'll similarly use $\mathcal{G}$ for an RKHS over $\mathcal{Y}$ with kernel $\ell: \mathcal{Y}^2 \to \R$ and feature map $\psi: \mathcal{Y} \to \R$. We'll assume both RKHS are separable.

Given $f \in \mathcal{F}, g \in \mathcal{G}$, their tensor product $f \otimes g: \mathcal{G} \to \mathcal{F}$ is the linear operator defined via
\\[
(f \otimes g) h = f \langle g, h \rangle\_{\mathcal{G}}.
\\]
This is a coordinate-free way of taking outer products of vectors, which yields an operator (i.e., a matrix). Very informally, this is $f g^T$, where $g^T$ is a co-vector and should be understood as $\langle g, \cdot \rangle$, whence the expression becomes clear.

### The HSIC
Now, we consider the map $\phi \otimes \psi: \mathcal{X} \times \mathcal{Y} \to \mathcal{F} \times \mathcal{G}$ given by $(\phi \otimes \psi)(x, y) = (\phi(x), \psi(y))$. This results in a new, transformed distribution $q(\phi, \psi)$ on $\mathcal{F} \times \mathcal{G}$, i.e., the pushforward of $p(x, y)$ along $\phi \otimes \psi$. In short, we've embedded our joint distribution via the associated feature maps. The associated covariance operator is
\\[
\begin{align}
\Sigma_{\phi \psi} &= \E\_{q(\phi, \psi)}[ (\phi - \E \phi) \otimes (\psi - \E \psi )] \\\\\\\\
&= \E\_{p(x, y)}[ (\phi(x) - \E \phi(x) ) \otimes (\psi(y) - \E \psi(y) )] \\\\\\\\
&= \E\_{p(x,y)}[\phi(x) \otimes \psi(y)] - \mu_\phi \otimes \mu\_\psi
\end{align}
\\]
where $\mu\_\phi, \mu\_\psi$ are the associated means. Here, we note that some care must be taken when interpreting the mean as a weak mean (see e.g., the note on Pettis integrals). Using the definition of weak means and the reproducing property, it is not hard to check that $\|\| \mu_\phi \|\|\_{\mathcal{F}}^2 = \E_{x,x'}[k(x, x')]$ and analogously for the other variables.

Observe that $\Sigma_{\phi \psi}: \mathcal{G} \to \mathcal{F}$ is a linear operator. Let's assume it has finite Hilbert-Schmidt norm. The **HSIC** is the Hilbert-Schmidt norm of $\Sigma_{\phi\psi}$, i.e., $\lvert\lvert\Sigma_{\phi\psi}\rvert\rvert\_{HS}^2$.

### Kernel Form

Our goal is now to replicate our finite-dimensional calculations while avoiding any explicit appearance of a feature map by using the kernel. Recall that the space of Hilbert-Schmidt operators on a separable Hilbert space is again a separable Hilbert space, and thus has an associate inner product $\langle \cdot, \cdot \rangle\_{HS}$. Thus,
\\[
\begin{align}
||\Sigma_{\phi\psi}||^2\_{HS} &= \langle \E[\phi \otimes \psi] - \mu_\phi \otimes \mu_\psi, \E[\phi \otimes \psi] - \mu_\phi \otimes \mu_\psi \rangle_{HS} \\\\\\\\
&= \underbrace{\E \E [\langle \phi \otimes \psi, \phi \otimes \psi\rangle\_{HS}]}\_{(1)} - 2 \underbrace{\E [\langle \phi \otimes \psi, \mu_\phi \otimes \mu_\psi \rangle\_{HS}]}\_{(2)} + \underbrace{\langle \mu_\phi \otimes \mu_\psi, \mu_\phi \otimes \mu_\psi \rangle\_{HS}}\_{(3)}.
\end{align}
\\]

For (3), recall that $\lvert\lvert f \otimes g \rvert\rvert\_{HS}^2 = \lvert\lvert f \rvert\rvert\_{\mathcal{F}}^2 \lvert\lvert g \rvert\rvert\_{\mathcal{G}}^2$ and that $\lvert\lvert \mu_\phi \rvert\rvert\_{\mathcal{F}}^2 = \E_{x,x'}[k(x, x')]$, and analogously for the other RKHS. This yields
\\[
(3) = \E\_{x,x'}[k(x,x')] \E\_{y,y'}[\ell(y,y')].
\\]

For (2), observe that
\\[
\begin{align}
(2) &= \E_{x,y}[ \langle \phi(x) \otimes \psi(y), \mu_\phi \otimes \mu_\psi \rangle\_{HS} ] \\\\\\\\
	&= \E_{x,y}[ \langle \phi(x), \mu\_\phi \rangle\_{\mathcal{F}} \langle \psi(y), \mu\_\psi \rangle\_{\mathcal{G}} ] \\\\\\\\
	&= \E_{x,y}[\E_{x'}[k(x, x')] \E_{y'}[k(y, y')]]
\end{align}
\\]
where we use the weak definition of the mean and the reproducing kernel property.

Similarly, we have
\\[
\begin{align}
(1) &= \E_{x,y,x',y'}[ \langle \phi(x) \otimes \psi(y), \phi(x') \otimes \psi(y')\rangle\_{HS} ] \\\\\\\\
    & = \E_{x,y,x',y'}[ \langle \phi(x), \phi(x')\rangle\_{\mathcal{F}} \langle \psi(y), \psi(y') \rangle\_{\mathcal{G}} ] \\\\\\\\
    &= \E_{x, y, x', y'}[k(x,x')k(y,y')].
\end{align}
\\]

Thus,
\\[
\begin{align}
||\Sigma_{\phi\psi}||^2\_{HS} &= \E_{x, y, x', y'}[k(x,x')\ell(y,y')] - 2\E_{x,y}[\E_{x'}[k(x, x')] \E_{y'}[\ell(y, y')]] + \E\_{x,x'}[k(x,x')] \E\_{y,y'}[\ell(y,y')].
\end{align}
\\]

This is nice -- we've managed to write everything in terms of only our data generating process and some kernels. 

### Estimating the HSIC from Data

While the expression we have written could in practice be estimated from an i.i.d. sample $\{(x_i, y_i)\}\_{i=1}^m$ from $p(x, y)$, we might wonder if we can obtain a simple expression for the HSIC in terms of only the kernel matrices, as we had done in the finite-dimensional case. 

It turns out that the obvious naive analogy directly works. That is, take $K = (k(x_i, x_j))\_{i,j=1}^m$ and $L = (\ell(y_i, y_j))\_{i,j=1}^m$ to be the Gram matrices associated with our kernels. Then, we obtain an approximation
\\[
||\Sigma_{\phi\psi}||^2\_{HS} \approx \frac{1}{(m-1)^2} \textrm{tr}\left( KHLH \right).
\\]

We emphasize that at this stage, this is merely an educated guess. While we could in principle try to mirror our finite-dimensional calculations (i.e., computing an empirical covariance operator and taking its Hilbert-Schmidt norm), this is potentially tricky as the associated steps take place in our infinite-dimensional RKHS. Instead, we can leverage our finite-dimensional representation from the previous section to get an easier proof.

It turns out that this approximation is, on average, correct, up to a bias of $O(m^{-1})$. We'll skip a lot of the details (since it's a bit tedious), but it's worth noting the key steps. We first write 
\\[
\textrm{tr}(KHLH) = \textrm{tr}(KL) - \frac{2}{m} \mathbf{1}^T KL \mathbf{1} + \frac{1}{m^2} (\mathbf{1}^T K \mathbf{1})(\mathbf{1}^T K \mathbf{1}).
\\]
using the symmetry of $K, L$. Upon expanding out each of these products and grouping by the number of free indices, the highest-order term in each exactly corresponds to the three expectations appearing in the previous section. 

It is worth noting that the bias arises from self-interactions. For instance, writing out $\textrm{tr}(KL)$, you will see that there are $O(m)$ terms of the form $k(x_i, x_i)\ell(y_i, y_i)$ and $O(m^2)$ terms of the form $k(x_i, x_j)\ell(y_i, y_j)$. The former do not have the correct expectation $\E_{x,x',y,y'}[k(x,x')\ell(y,y')]$ while the latter do. An unbiased estimator for the HSIC can be obtained by subtracting out the self-interaction terms, but we don't detail this procedure here.

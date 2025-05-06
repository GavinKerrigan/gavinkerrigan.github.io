---
title: "Differentiation and Integration by Parts"
topic: "Analysis"
chapter: "Gaussian Measures"
section: "differentiation"
layout: note
permalink: "/notes/analysis/gaussian_measures/differentiation/"

subtitle: 
date: 2025-05-04
keywords: analysis, measure theory, gaussian measures, differentiation, integration by parts
published: false
references: "Bogachev, V. (1998). Gaussian Measures, Chapter 5."
---

In this note $X, Y$ are locally convex spaces. Let $\mathcal{M} \subset 2^X$ be a class of nonempty subsets of $X$. 

<div class='definition' name='Differentiability'>
A mapping $F: X \to Y$ is differentiable with respect to $\mathcal{M}$ at the point $x \in X$ if there exists a continuous linear map $DF_x: X \to Y$ such that for every $M \in \mathcal{M}$,

\[
\lim_{t \to 0} \frac{F(x + th) - F(x)}{t} = DF_x (h) 
\]

uniformly over $h \in M$. 
</div>

Spelling things out a bit, if $V \subset Y$ is a neighborhood of the origin, then there exists $\delta > 0$ such that
\\[
\frac{F(x + th) - F(x)}{t} - DF_x(h) \in V \qquad \forall |t| < \delta, h \in M.
\\]

When $Y$ is a normed space, this is equivalent to
\\[
\lim_{t \to 0} \sup_{h \in M} \left| \frac{F(x + th) - F(x)}{t} - DF_x(h) \right| = 0 \qquad \forall M \in \mathcal{M}.
\\]

This definition captures various notions of directional derivatives. Intuitively, the class $\mathcal{M}$ controls the regularity under which the limit is taken. For example:
<ol>
	<li> Taking $\mathcal{M}$ to be the class of all finite subsets of $X$ yields the Gateaux derivative -- i.e., differentiable along any direction $h \in X$. This is essentially because uniform convergence on a finite set is equivalent to pointwise convergence. Note some authors use a slightly different notion for the Gateaux derivative which is only pointwise in $h$, i.e., not requiring the existence of a continuous linear map encoding the directional derivatives. We will call this weaker notion the Gateaux differential to avoid confusion. </li>
	<li> If $\mathcal{M}$ is the class of all compact subsets of $X$, we obtain the notion of compact (or Hadamard) differentiability. </li>
	<li> If $\mathcal{M}$ consists of all bounded sets, then we obtain the notion of Frechet differentiability. </li>
</ol>

For normed spaces, it is easy to see that $\texttt{Frechet} \subseteq \texttt{Hadamard} \subseteq \texttt{Gateaux}$ under this definition. What is more subtle is the strictness of these implications. We note a few of these without proof:
<ul>
	<li> If $X, Y$ are finite dimensional, $\texttt{Frechet} = \texttt{Hadamard} \subsetneq \texttt{Gateaux}$. </li>
	<li> If $F: X \to Y$ is locally Lipschitz, then $\texttt{Hadamard} = \texttt{Gateaux}$. </li>
	<li> If $X, Y$ are infinite dimensional Banach spaces, then $\texttt{Frechet} \subsetneq \texttt{Hadamard} \subsetneq \texttt{Gateaux}$. </li>
</ul>   

### Frechet Differentiability

Note that our definition allows for a notion of Frechet differentiability even when $X, Y$ do not possess a norm. However, in the case that $X, Y$ are normed, we obtain the usual definition. Essentially, a key difference between Gateaux and Frechet differentiability is that the former only allows for limiting sequences along rays, whereas the latter allows for more flexible choices of limiting sequences.

<div class='proposition' name='Frechet Differentiability'>
Suppose $X, Y$ are normed spaces. A mapping $F:X \to Y$ is Frechet differentiable at $x \in X$ in the sense of Definition 1 if and only if there exists a bounded linear map $DF_x: X \to Y$ such that
\[
	\lim_{|k|\to 0} \frac{|F(x + k) - F(x) - DF_x(k)|}{|k|}.
\]
</div>
<details class='proof'>
<summary> Proof. </summary>
First, suppose $F$ is differentiable at $x \in X$ in the norm sense. Fix a bounded set $M \subset X$, so that any $h \in M$ is such that $|h| \leq \lambda$ for some $\lambda > 0$. Fix $\epsilon > 0$. By assumption, there is a $\delta > 0$ such that 
\[
|k| < \delta \implies \frac{|F(x + k) - F(x) - DF_x(k)|}{|k|} < \epsilon.
\]

For $t > 0$, consider $k = th$. Observe that for $t < \delta/\lambda$, we have $|k| < \delta$. In this case,
\[
\begin{align}
\left| \frac{F(x + th) - F(x)}{t} - DF_x(h) \right| &= |h| \frac{|F(x + k) - F(x) - DF_x(k)|}{|k|} \\
& < \lambda \epsilon.
\end{align}
\]

The fact that $M$ was an arbitrary bounded set shows that $F$ is differentiable with respect to the class of bounded subsets (in the sense of Definition 1).

<br><br>

Conversely, suppose $F$ is Frechet differentiable at $x \in X$ in the sense of Definition 1. Fix $\epsilon > 0$. Taking $M$ to be the closed unit ball in $X$, there exists a $\delta > 0$ such that
\[
|t| < \delta \implies \left| \frac{F(x + th) - F(x)}{t} - DF_x(h) \right| \qquad \forall |h| \leq 1.
\]

Now, if $k \in X$ is such that $|k| < \delta$, we have
\[
\frac{|F(x + k) - F(x) - DF_x(k)||}{|k|} = \left| \frac{F(x + |k| \frac{k}{|k|}) - F(x)}{|k|} - DF_x\left(\frac{k}{|k|} \right) \right| < \epsilon.
\]

This shows $F$ is Frechet differentiable in the norm sense.
</details>

### Differentiability Along a Subspace

It will be necessary at times to only allow for derivatives to be taken along particular directions in the input space. Note that generally it will be easier to have a derivative along a subspace than to have a derivative in every direction for two distinct reasons: (1) the subspace is smaller, and (2) often carries a stronger topology.

<div class='definition'>
Suppose $E \subseteq X$ is a linear (closed) subspace, possibly equipped with a stronger locally convex topology (i.e., having more open sets than the subspace topology). We say that $F:X \to Y$ is differentiable at $x \in X$ along $E$ if the mapping
\[
G^x: E \to Y \qquad G^x(h) =  F(x + h)
\]
is differentiable (in the appropriate sense) at $h=0$. We write $D_E F_x$ for the derivative of $F$ at $x$ along $E$.
</div>

This is essentially shorthand for saying that we restrict the class $\mathcal{M}$ of perturbation directions to be subsets of $E$, potentially also allowing for a change in topology. Some care must also be taken to note that we only now require linearity in $E$ of the resulting linear operator $D_E F_x$. When $E$ is one dimensional this gives us a notion of a partial derivative, i.e.,
\\[
\partial_h F_x = \lim_{t \to 0} \frac{F(x + th) - F(x)}{t}.
\\]

Observe that $D_E F: X \to B(E, Y)$ results in a mapping from $E \subseteq X$ to the space of bounded linear operators $B(E, Y)$. Equipping this space with a locally convex topology allows us to thus recurse on our definition and obtain higher order derivatives.


### Examples

Take $X = \R^\infty$ equipped with the topology of pointwise convergence, $E = \ell^2$ with its usual topology, and $Y = \R$. Consider the functions
\\[
F(x) = \sum_{n=1}^\infty x_n/n^2 \qquad G(x) = \sum_{n=1}^\infty x_n^2 / n^2
\\]

and let $F(x) = G(x) = 0$ whenever these sums are not convergent. Then, $F$ and $G$ are both Frechet differentiable along $E$ for every $x$, with derivatives represented by
\\[
D\_E F_x = (2^{-n})\_{n=1}^\infty \qquad D\_E G_x = (2 n^{-2} x\_n)\_{n=1}^\infty
\\]
for $x$ in their respective domains, and zero otherwise. However, neither is Gateaux differentiable along $X$. To see why, take $x$ to be a point in the domain of $X$ and note that for $h = e_k$ we have
\\[
\lim_{t \to 0} \frac{F(x + te_k) - F(x)}{t} = 2^{-k}.
\\]

If the Gateaux derivative $DF_x$ existed, it would have to be linear on $X$, so that for any sequence $h \in \R^\infty$, $DF_x(h) = \sum_{n=1}^\infty h_n / 2^n$ -- but there are endless choices in $h$ that will make this quantity diverge. Intuitively, perturbing along $h \in \ell_2$ results in a finite perturbation of the function value, but perturbing along an arbitrary $h \in X$ can result in infinite variation of the output function value.

For another example, consider $X = L^2[0,1]$ and $F: L^2[0, 1] \to L^2[0, 1]$ given by $F(x_t) = \sin(x_t)$. It is not too hard to see that $F$ is Gateaux differentiable along $X$ with derivative $DF_x(h) = \cos(x_t)h_t$. On the other hand, if $F$ were Frechet differentiable along $X$, then its Frechet derivative would have to coincide with its Gateaux derivative. If we take $x = 0$ and $h(t) = \mathbf{1}[t \in [0, \epsilon^2]]$, then
\\[
\frac{|F(x_t + h_t) - F(x_t)|\_2}{|h|\_2} = \frac{\left(\int_0^1 (\sin h_t - h_t)^2 \right)^{1/2}}{\epsilon} = |\sin(1) - 1|
\\]
which cannot converge to zero as $|h|\_2 \to 0$. Similar constructions show $F$ is in fact nowhere Frechet differentiable along $X$. 

However, if we take $E = C[0, 1] \subset L^2[0, 1]$. the Frechet derivative along $E$ exists for every $x$. This follows because a second order Taylor expansion of $\sin(x_t + h_t)$ yields
\\[
\left|\sin(x\_t + h\_t) - \sin(x\_t) - \cos(x\_t)h\_2\right|\_{L^2[0,1]} \leq \frac{1}{2} |h\_t|\_{\infty}^2
\\]
and hence we may apply Proposition 1.
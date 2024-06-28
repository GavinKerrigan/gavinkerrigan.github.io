---
title: "Topology in Function Spaces"
topic: "Analysis"
chapter: "Functional Analysis"
section: "topology"
layout: note
permalink: "/notes/analysis/functional_analysis/topology/"

subtitle: 
date: 2024-06-27
keywords: analysis, functional analysis, topology
published: false
---

Reference: Folland. 


We are interested in studying the interplay between topology and measure. In particular, we are interested in applications to spaces of probability measures.


## Preliminaries on LCH spaces

The spaces we will start out studying are the locally compact Hausdorff spaces, or LHC spaces.

<div class='definition' name='LCH Space'>
Let $X$ be a topological space. We say that $X$ is an LCH space if it is

<ol>
<li> <strong> Hausdorff: </strong> any two distinct points of $X$ admit disjoint neighborhoods. </li>
<li> <strong> Locally Compact: </strong> every point has a compact neighborhood. </li>
</ol>
</div>

We will henceforth use $X$ to represent a generic LCH space. The spaces $\R^d$ are LCH spaces. However, note that a Hausdorff TVS is locally compact if and only if it is finite dimensional -- thus the Euclidean spaces are the only LCH topological vector spaces. 

<div class='lemma' name="Uryshon's Lemma">
Let $X$ be an LCH space and let $K \subset U \subset X$ be a compact set where $U$ is open. Then, there exists a continuous function $f: X \to [0, 1]$ such that $f=1$ on $K$ and $f=0$ outside of a compact subset of $U$. 
</div>

If $U \subset X$ is open and $f \in C_c(X)$, then we write $f \prec U$ to mean that $0 \leq f \leq 1$ and $\text{supp}(f) \subset U$. This is a little stronger than $0 \leq f \leq 1_U$ which only implies $\text{supp}(f) \subset \overline{U}$. Observe that if $K \subset U \subset X$ is compact, Uryshon's Lemma supplies us with a $\phi \prec U$ with $\phi = 1$ on $K$. Think of $\phi$ as a "soft indicator" function of $K$. 

## Radon Measures

Recall that $C_c(X) = C_c^0(X)$ is the space of continuous compactly supported functions on $X$.

<div class='definition' name='Positive Functionals'>
A linear functional $I: C_c(X) \to \R$ is called positive if $I(f) \geq 0$ whenever $f \geq 0$.
</div>

<div class='proposition' name='Continuity of Positive Functionals'>
If $I$ is a positive linear functional on $C_c(X)$, then for every compact set $K \subset X$ there exists a constant $C_K$ such that
\[
\lvert I(f) \rvert \leq C_k \norm{f}_\infty
\]

for all $f \in C_c(X)$ with $\text{supp}(f) \subset K$. 

</div>
<details class="proof">
<summary> Proof. </summary>
Let $K \subset X$ be compact. By Urhsyon's Lemma, there exists $\phi \in C_c(X)$ such that $0 \leq \phi(x) \leq 1$ and $\phi(x) = 1$ on $K$. Thus, $|f(x)| \leq \norm{f}_\infty \phi(x)$, and note $\norm{f}_\infty \phi \in C_c(X)$. In particular, we have
\[
- \norm{f}_\infty \phi(x) \leq f(x) \leq \norm{f}_\infty \phi(x)
\]

and upon applying the positive functional $I$ we obtain
\[
\lvert I(f) \rvert \leq \norm{f}_{\infty} I(\phi).
\]
</details>

Suppose that $\mu$ is a locally finite Borel measure on $X$, i.e. $\mu(K) < \infty$ for every compact $K \subseteq X$. Then, we have $C_c(X) \subset L^1(\mu)$, because $\int \|f\| \d \mu \leq \norm{f}_\infty \mu(\text{supp} f)$. Observe that continuity is a purely topological notion, whereas integrability is a purely measure-theoretic notion. This gives us a bridge between these two notions. 

In particular, note that the mapping $f \mapsto \int f \d \mu$ is a positive linear functional on $C_c(X)$. It turns out that *every* positive linear functional can be produced in this fashion. This correspondence is unique if we additionally assume that $\mu$ is Radon.

<div class='definition' name='Radon Measues'>
Let $X$ be an LCH space and let $\mu$ be a Borel measure on $X$. Fix a Borel set $E \subset X$.

<ol>
    <li> We say that $\mu$ is outer regular on $E$ if \[ \mu(E) = \inf \left\{ \mu(U) : E \subset U, \; U \text{ is open} \right\} \] </li>
    <li> We say that $\mu$ is inner regular on $E$ if \[ \mu(E) = \sup \left\{ \mu(K) : K \subset E, \; K \text{ is compact} \right\} \] </li>
    <li> The measure $\mu$ is regular if it is outer and inner regular on all Borel sets. </li>
    <li> The measure $\mu$ is Radon if it is finite on all compact sets, outer regular on all Borel sets, and inner regular on open sets. </li>
</ol>
</div>

Regularity essentially allows us to approximate our measure "from above/below" using nice (open or compact) sets. Thus we should expect that many properties of a regular measure $\mu$ can be deduced by studying its behavior on said nice sets. It turns out that regularity alone is not sufficiently nice, particularly when $X$ is not $\sigma$-compact, and we thus have weaker requirements for a Radon measure.



<div class='theorem' name='Riesz Representation'>
If $I$ is a positive linear functional on $C_c(X)$, then there is a unique Radon measure $\mu$ on $X$ such that $I(f) = \int f \d \mu$ for all $f \in C_c(X)$. Moreover,

\[
\mu(U) = \sup\left\{ I(f) : f \in C_c(X), \; f \prec U \right\} \qquad \forall U \subset X \text{ open}. \tag{1}
\]
\[
\mu(K) = \inf \left\{ I(f) : f \in C_c(X), \; f \geq 1_K \right\} \qquad \forall K \subset X \text{ compact}. \tag{2}
\]
</div>
<details class='proof'>
<summary> Proof. </summary>
We first see how to prove uniqueness and then use this to see how to go about constructing such a $\mu$. To that end, suppose $\mu$ is a Radon measure such that $I(f) = \int f \d \mu$ for all $f \in C_c(X)$. Fix an open set $U \subset X$. If $f \prec U$, it is immediate that $I(f) \leq \mu(U)$. Hence,
\[
\sup\left\{ I(f) : f \in C_c(X), \; f \prec U\right\} \leq \mu(U).
\]

On the other hand, for any compact $K \subset U \subset X$, Uryshon's Lemma furnishes us with an $f \in C_c(X)$ such that $f \prec U$ and $f = 1$ on $K$. This means that $\mu(K) \leq I(f)$. Now, since $\mu$ is Radon, it is in particular inner regular on $U$, so that 

\[ 
\begin{aligned}
\mu(U) &= \sup \left\{ \mu(K) : K \subset U, \; K \text{ compact} \right\} \\
&\leq \sup \left\{ I(f) : f \in C_c(X), \; f \prec U \right\}.
\end{aligned}
\]

We have thus obtained (1). From this, we conclude that $\mu$ is unique, as the Radon-ness of $\mu$ means that it is outer regular and thus determined by its values on open sets, and these values are determined by $I$. 


</details>






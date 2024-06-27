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

The spaces $\R^d$ are LCH spaces. However, note that a Hausdorff TVS is locally compact if and only if it is finite dimensional -- thus the Euclidean spaces are the only LCH topological vector spaces. 

<div class='lemma' name="Uryshon's Lemma">
Let $X$ be an LCH space and let $K \subset U \subset X$ be a compact set where $U$ is open. Then, there exists a continuous function $f: X \to [0, 1]$ such that $f=1$ on $K$ and $f=0$ outside of a compact subset of $U$. 
</div>

We will henceforth use $X$ to represent a generic LCH space.

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



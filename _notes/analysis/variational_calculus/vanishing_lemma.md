---
title: "Vanishing Lemmas"
topic: "Analysis"
chapter: "Calculus of Variations"
section: "vanishing_lemma"
layout: note
permalink: "/notes/analysis/variational_calculus/vanishing_lemma/"

subtitle: 
date: 2024-06-18
keywords: calculus of variations, analysis
published: true
---

In the calculus of variations, we are often interested in deducing properties of some function which we can only access through integration. Here, we prove a few lemmas along these lines. Throughout we assume that $U \subset \R^d$ is open and bounded.

<div class='lemma' name='Fundamental Lemma of the Calculus of Variations'>
Suppose $u \in C^0(U)$. If

\[
\int_U u \varphi \d x = 0 \qquad \forall \varphi \in C_c^\infty(U),
\]

then $u(x) = 0$ for all $x \in U$. 
</div>

<details class="proof">
<summary> Proof. </summary>

Assume for the sake of contradiction that there exists some $x_0 \in U$ with $u(x_0) \neq 0$. Without loss of generality we may take $u(x_0) > 0$. As $u \in C^0(U)$, there is a neighborhood $V$ of $x_0$ such that $u(x) > 0$ on $V$. Let $\varphi \in C_c^\infty(U)$ be such that $\varphi > 0$ on $V$ and $\varphi = 0$ on $U \setminus V$. We then have

\[
\int_U u \varphi \d x = \int_V u \varphi \d x > 0
\]

which is a contradiction.

</details>

Note that it suffices to check the lemma on test functions $\varphi \in C^n_c(U)$ for any $0 \leq n < \infty$ as well.

We can use similar techniques to deduce that a given function is constant. Here, we focus on the one-dimensional case $U = (a, b) \subset \R$. 

<div class='lemma' name='Second Fundamental Lemma'>
Suppose $u \in C^0(U)$. If

\[
\int_U u \varphi' \d x = 0 \qquad \forall \varphi \in C_c^1(U),
\]

then $u(x) = c$ is constant for all $x \in U$. 
</div>

<details class="proof">
<summary> Proof. </summary>

Let $c = (b-a)^{-1} \int_a^b u \d x$, and define $\varphi(x) = \int_a^x (u(\xi) - c) \d \xi$. Note that $\varphi \in C_c^1(a, b)$ and in particular $\varphi(a) = \varphi(b) = 0$. Thus,

\[
\int_a^b (u - c) \varphi' \d x = \int_a^b u \varphi' \d x - c [\varphi(b) - \varphi(a)] = 0.
\]

On the other hand,

\[ 
\int_a^b (u - c) \varphi' \d x = \int_a^b (u - c)^2 \d x.
\]

Since this integrand is non-negative, it follows that $u(x) = c$ everywhere on $U$. 
</details>

We remark here that analogous results hold for higher-order expressions, e.g. if $\int u \varphi'' \d x$ vanishes then $u$ is linear. 

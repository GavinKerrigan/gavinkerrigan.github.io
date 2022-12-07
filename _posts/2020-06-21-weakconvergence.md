---
title: Weak Topologies
subtitle: Weak convergence in Banach spaces.
layout: blogpost
date: 2020-11-23
keywords: functional analysis, mathematics, topology
published: true
---
 
# Introduction 

Let $X$ be a normed vector space. Let's first start with the usual notion of convergence, but let's give it a special name to indicitate that we'll be thinking about different modes of convergence.

<div class='definition' name='Strong Convergence'>
A sequence $(x_n)$ in $X$ is said to <b>converge strongly</b> to $x$ if $\norm{x_n - x} \to 0$.
</div>

For the sake of convenience, we'll often simply write $x_n \to x$ to denote that a sequence strongly converges to $x$. 

<div class='definition' name='Weak Convergence'>
A sequence $(x_n)$ in $X$ is said to <b>converge weakly</b> to $x$ if for every bounded linear functional $\varphi \in X'$, we have $\norm{\varphi(x_n) - \varphi(x)} \to 0$.
</div>

We'll use $x_n \weakto x$ to denote weak convergence. Weakly convergent sequences have several properties that we'd hope for in any notion of a convergent sequence -- for example, if $x_n \weakto x$, then (a) its weak limit is unique, (b) any subsequence also converges weakly to $x$, and (c) the sequence is bounded.  Facts (a-b) are easy to prove, and (c) is an application of the Banach-Steinhaus theorem.

Why is this called weak convergence? If $x_n \to x$ converges in the strong sense, then it is true that $\varphi(x_n) \to \varphi(x)$ for every $\varphi \in X'$, as the linear functionals $\varphi$ are continuous. Hence, $x_n \to x$ implies $x_n \weakto x$.  The converse, however, is not true -- weak convergence really is weaker than strong convergence.


<div class='proposition'>
Let $p \in (1, \infty)$ and consider the Banach space $\ell^p$. Consider the sequence $(\delta_n)$, where $\delta_n = (0, 0, \dots, 0, 1, 0, \dots)$ is a sequence which is identically zero except at the $n$th position. Then, $\delta_n \weakto 0$, but the sequence $(\delta_n)$ does not converge strongly.
</div>

<div class='proof'>
We can identify the dual of $\ell^p$ with $\ell^q$, where $q$ satisfies $\frac{1}{p} + \frac{1}{q} = 1$. That is, any $\varphi \in (\ell^p)'$ can be expressed as

[ \varphi(x) = \sum_{k=1}^\infty \varphi_k x_k  \quad \text{s.t.} \quad \sum_{k=1}^\infty |\varphi_k|^q < \infty. ] 

In particular, $|\varphi(\delta_n)| = |\varphi_n|$, which must converge to zero as $\sum_{k=1}^\infty |\varphi_k|^q$ converges. This holds for any $\varphi \in (\ell^p)'$, and so $\delta_n \weakto 0$. On the other hand, for $n \neq m$ we have

[ \norm{\delta_n - \delta_m}_p = 2^{1/p} ] 
which shows that the sequence $(\delta_n)$ is not Cauchy, and hence it does not strongly converge.
</div>

Interestingly, weak convergence *can* imply strong convergence in certain spaces. Such a space is said to have the <b>Schur property</b>. For instance, the space $\ell^1$ has the Schur property -- this is fairly tricky to prove, and we'll skip the proof here.

One might wonder why the notion of weak convergence doesn't show up in standard real analysis. There's a good reason for this: weak convergence implies strong convergence in finite-dimensional spaces.

<div class='proposition'>
Let $X$ be a finite dimensional normed space. If $x_n \weakto x$, then $x_n \to x$. 
</div>
<div class='proof'>
Since $X$ is finite dimensional, it admits a basis $\{e_1, \dots, e_k \}$. If we consider the bounded linear functionals $\varphi_j$ for $j= 1, 2, \dots, k$ defined by $\varphi_j(e_i) = \delta_{ij}$, weak convergence shows that each coordinate of $x_n$ converges (strongly) to the corresponding coordinate of $x$. 
</div>

# Weak Completeness

The standard notion of strong convergence leads us to a notion of Cauchy sequences and completeness, the latter playing a pivotal role in functional analysis. It turns out that weak convergence also gives us a notion of completeness, which unsurprisingly is called weak completeness.

<div class='definition' name='Weak Cauchy; Weak Complete'>
Let $X$ be a normed vector space. A sequence $(x_n) \subset X$ is said to be <b>weak Cauchy</b> if the sequence $(\varphi(x_n)) \subset \mathbb{F}$ is Cauchy in the base field for every $\varphi \in X'$. We say that $X$ is <b>weak complete</b> if every weak Cauchy sequence converges weakly to some point in $X$. 
</div>

Here, we use $\mathbb{F}$ to represent either $\R$ or $\mathbb{C}$. By the Banach-Steinhaus theorem, we see that if $(x_n)$ is a weak Cauchy sequence, then $\sup \norm{x_n} < \infty$, i.e. the sequence is bounded. A natural question one might ask is whether $X$ being complete implies that $X$ is weak complete. It turns out that, in general, the answer is a surprising no. However, there is one fairly general family of spaces where this is true: the reflexive spaces. Note that we don't need to assume that $X$ is Banach, because reflexive normed vector spaces are automatically Banach. 

<div class='proposition'>
Let $X$ be a reflexive normed vector space. Then, $X$ is weakly complete.
</div>
<div class='proof'>
We need to show that every weak Cauchy sequence in $X$ has a weak limit in $X$. To that end, let $(x_n) \subset X$ be a weak Cauchy sequence and fix an arbitrary $\varphi \in X'$. We will show $\varphi(x_n) \to \varphi(x)$ for some $x \in X$ which is chosen independently of $\varphi$. To that end, define the map $\alpha: X' \to \mathbb{F}$ via $\alpha(\varphi) = \lim_{n \to \infty} \varphi(x_n)$. This limit exists because $(\varphi(x_n))$ is Cauchy in $\mathbb{F}$.

<p>
We claim $\alpha$ is a bounded linear map. It is easy to see that $\alpha$ is linear. Since $(x_n)$ is weak Cauchy, it is bounded, say $\norm{x_n} \leq M$. Then,

[\norm{\alpha} = \sup_{\norm{\varphi} = 1} \{ |\alpha(\varphi)| \} = \sup_{\norm{\varphi} = 1} \{ | \lim_{n \to \infty} \varphi(x_n) | \} \leq M.]
</p>

Thus, $\alpha$ is a bounded linear map, i.e. $\alpha \in X''$. Since $X$ is reflexive, $X$ is isometrically isomorphic to $X''$, and we may identify $\alpha$ with evaluation by an element $x \in X$. That is, for every $\varphi \in X'$, we have
[ \alpha(\varphi) = \lim_{n \to \infty} \varphi(x_n) = \varphi(x). ]
</div>
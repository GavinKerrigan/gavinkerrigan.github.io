---
title: Modes of Convergence 2
subtitle: We now turn our attention to the convergence of operators and functionals.
layout: blogpost
date: 2022-12-07
keywords: functional analysis, mathematics, topology
published: true
---
 
# Introduction

In the previous post, we saw that for a sequence $(x_n)$ in a normed vector space $X$, there were two modes of convergence: strong and weak. In this post, we'll explore the various modes of convergence for *operators* between normed vector spaces, with a particular focus on the linear functionals.

# Convergence of Operators

Let $X, Y$ be normed vector spaces. We write $B(X, Y)$ for the space of bounded linear operators from $X$ to $Y$. Recall that if $Y$ is Banach then $B(X, Y)$ is Banach. In this section, we consider a sequence $(T_n) \subset B(X, Y)$ of bounded linear operators $T_n: X \to Y$, and discuss the various modes of convergence for such a sequence.

<div class='definition' name='Operator Convergence'>
Let $(T_n) \subset B(X, Y)$ be a sequence of bounded linear maps between normed vector spaces. We say that $(T_n)$ is:

<ol>

<li><b>Uniformly (operator) convergent</b> if $T_n$ converges in the operator norm; that is, there exists some $T \in B(X, Y)$ such that $\norm{T_n - T} \to 0$.</li>
<li><b>Strongly (operator) convergent</b> if for every $x \in X$, $(T_n(x))$ converges strongly in $Y$; that is, there exists some linear operator $T:X \to Y$ such that for every $x \in X$, $\norm{T_n x - Tx} \to 0$.</li>
<li><b>Weakly (operator) convergent</b> if for every $x \in X$, $(T_n(x))$ converges weakly in $Y$; that is, there exists some linear operator $T:X \to Y$ such that for every $x \in X$ and every $\varphi \in Y'$, $\norm{\varphi(T_n x) - \varphi(Tx)} \to 0.$</li>
</ol>
</div>

Note that we've been a little sneaky in parts (2) and (3) of this definition -- for example, if $(T_n(x))$ converges strongly for every $x \in X$, we technically only a priori know that $T_n(x) \to y$ for some $y \in Y$, but not that $y = Tx$ for some linear $T:X \to Y$. However, we can simply set $T$ to be the operator mapping $x \mapsto \lim_{n \to \infty} T_n x$. As defined, $T$ is clearly linear. However, note that said $T$ may not be bounded even though each $T_n \in B(X, Y)$. 

What is the relationship between these modes of convergence? First, it is easy enough to see that

[\text{uniform} \implies \text{strong} \implies \text{weak} ]

and moreover the limits are the same. However, each of the converse statements is false. For some examples, take $X = Y = \ell^2$. The sequence of operators $(T_n)$ which zero out the first $n$ elements of $x \in \ell^2$ is strongly but not uniformly convergent to the zero operator. Similarly, the sequence of operators $(S_n)$ which append $n$ zeroes to the beginning of $x \in \ell^2$ is weakly but not strongly convergent to the zero operator. We skip the details of checking these here, but encourage any interested readers to try it out for themselves.

Consider now the special case of $\varphi \in B(X, \mathbb{F}) = X'$, i.e. we are restricting our attention to the linear functionals on $X$. This is a special case of what we've discussed so far. However, note that strong operator convergence and weak operator convergence are equivalent for a sequence $(\varphi_n) \subset X'$, because $(\mathbb{F})' \simeq \mathbb{F}$. Thus, for linear functionals, there really are only two modes of convergence to worry about. These are so important that they get their own names; it is somewhat unfortunate that these standard names conflict with the previous definition we gave, but c'est la vie.

<div class='definition' name='Strong and Weak* Convergence'>
Let $X$ be a normed vector space, and $(\varphi_n) \subset X'$ a sequence of bounded linear functionals on $X$. We say that $(\varphi_n)$ is:

<ol>
<li><b>Strongly convergent</b> if there exists $\varphi \in X'$ such that $\norm{\varphi_n - \varphi} \to 0$.</li>
<li><b>Weak* ("weak-star") convergent</b> if there exists $\varphi \in X'$ such that $|\varphi_n(x) - \varphi(x)| \to 0$ for all $x \in X$.</li>
</ol>
</div>

Recall that we already have a notion of weak convergence for $(\varphi_n)$ -- namely, $\varphi_n \weakto \varphi$ if $\alpha(\varphi_n) \to \alpha(\varphi)$ for every $\alpha \in X''$. Using the canonical mapping $X \to X''$, it is eay to see that weak convergence of $(\varphi_n)$ implies weak* convergence. In general, the converse is not true, since $X''$ may be strictly larger than $X$ -- however, the two notions are equivalent if $X$ is reflexive. In practice, weak* convergence tends to be more important than weak convergence for linear functionals. 

# Properties of Limiting Operators

One of the main reasons that we study the various modes of operator convergence is that we often construct an operator via a limiting operation applied to a sequence of simpler operators. The mode under which we take this limiting process has important implications for the properties of the limiting operator, and often tells us which properties of the simpler operators we expect to carry over in the limit. In this section we'll discuss some of these implications. Throughout this section, $(T_n) \subset B(X, Y)$ will be a sequence of bounded linear operators.

First, suppose $(T_n)$ converges to $T$ in the uniform sense. By definition, we must also have $T \in B(X, Y)$ -- otherwise it wouldn't make sense to consider $\norm{T_n - T}$. What if $(T_n)$ only converges strongly or weakly to $T$ -- can we still conclude that $T \in B(X,Y)$? From the discussion in the first section, we know that $T$ must be linear. However, without additional assumptions, we cannot conclude that $T$ is bounded. That being said, if we assume that $X$ is Banach, then by an application of the Banach-Steinhaus theorem, if $(T_n)$ converges strongly to $T$, then $T \in B(X, Y)$.

In the following proposition, we give a useful characterization of strong operator convergence. Note that we assume $X, Y$ to both be Banach spaces in the following.

<div class='prop'>
Let $X, Y$ be Banach spaces. A sequence $(T_n) \subset B(X, Y)$ is strongly operator convergent if and only if:
<ol>
<li>The sequence $(\norm{T_n})$ is bounded. </li>
<li>The sequence $(T_n x)$ is Cauchy in $Y$ for every $X$ in a total subset $M \subset X$. </li>
</ol>
</div>
<div class='proof'>
If $T_n \to T$ strongly, then the forward implication is a straightforward application of Banach-Steinhaus. Conversely, suppose $\sup \norm{T_n} \leq M$ and that there is a total subset $M \subset X$ such that $(T_n x)$ is Cauchy for every $x \in M$. Since $M$ is total, its span is dense in $X$, so we may choose some $y \in \text{span}(M)$ with $\norm{x - y}$ as small as we want. Moreover, we have that $(T_n y)$ is a Cauchy sequence in $Y$. Then, for any indices $n,m$ we have

[ \norm{T_n x - T_m x} \leq \norm{T_n x - T_n y} + \norm{T_m x - T_m y} + \norm{T_n y - T_m y} ]
[ \leq 2M \norm{x - y} + \norm{T_n y - T_m y}. ]

Since $(T_n y)$ is Cauchy and we have control over $\norm{x-y}$, it follows that $(T_n x)$ is a Cauchy sequence in $Y$. Since $Y$ is Banach, this sequence must then have a (strong) limit. That is, we have shown that $T_n x$ has a strong limit in $Y$ for every $x \in X$, so that $T_n$ converges strongly. 
</div>


---
title: "Radon Measures and Topological Duals"
topic: "Analysis"
chapter: "Measure Theory"
section: "topology"
layout: note
permalink: "/notes/analysis/measure/radon/"

subtitle: 
date: 2024-07-01
keywords: analysis, functional analysis, topology
published: true
references: "Folland, G. B. (1999). Real analysis: Modern techniques and their applications (2nd ed.).; "
---


We are interested in studying the interplay between topology and measure. In this note, we study Radon measures, which are nice measures on locally compapct Hausdorff spaces. Many (most?) of the measures we will meet in practice will be Radon. Our main theorem will identify the space of Radon measures on an LCH space with the topological dual of $C_0(X)$, the space of continuous functions on $X$ vanishing at infinity. 


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

Recall that $C_c(X) = C_c^0(X)$ is the space of continuous compactly supported functions on $X$. If $U \subset X$ is open and $f \in C_c(X)$, then we write $f \prec U$ to mean that $0 \leq f \leq 1$ and $\text{supp}(f) \subset U$. This is a little stronger than $0 \leq f \leq 1_U$ which only implies $\text{supp}(f) \subset \overline{U}$. Observe that if $K \subset U \subset X$ is compact, Uryshon's Lemma supplies us with a $\phi \prec U$ with $\phi = 1$ on $K$. Think of $\phi$ as a "soft indicator" function of $K$. 

## Radon Measures

We now single out a class of measures, the Radon measures, which are particularly nice. Most measures we work with in practice will be Radon measures.

<div class='definition' name='Radon Measues'>
Let $X$ be an LCH space and let $\mu$ be a Borel measure on $X$. Fix a Borel set $E \subset X$.

<ol>
    <li> We say that $\mu$ is outer regular on $E$ if \[ \mu(E) = \inf \left\{ \mu(U) : E \subset U, \; U \text{ is open} \right\} \] </li>
    <li> We say that $\mu$ is inner regular on $E$ if \[ \mu(E) = \sup \left\{ \mu(K) : K \subset E, \; K \text{ is compact} \right\} \] </li>
    <li> The measure $\mu$ is regular if it is outer and inner regular on all Borel sets. </li>
    <li> The measure $\mu$ is Radon if it is finite on all compact sets, outer regular on all Borel sets, and inner regular on open sets. </li>
</ol>
</div>

Regularity essentially allows us to approximate our measure "from above/below" using nice (open or compact) sets. Thus we should expect that many properties of a regular measure $\mu$ can be deduced by studying its behavior on said nice sets. It turns out that regularity alone is strong, particularly when $X$ is not $\sigma$-compact, and we thus have weaker requirements for a Radon measure.

We now proceed to give a characterizations of the Radon measures on an LCH space.

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
\lvert I(f) \rvert \leq \norm{f}_{\infty} I(\phi)
\]

thus completing the proof.
</details>

Suppose that $\mu$ is a locally finite Borel measure on $X$, i.e. $\mu(K) < \infty$ for every compact $K \subseteq X$. Then, we have $C_c(X) \subset L^1(\mu)$, because $\int \|f\| \d \mu \leq \norm{f}_\infty \mu(\text{supp} f)$. Observe that continuity is a purely topological notion, whereas integrability is a purely measure-theoretic notion. This gives us a bridge between these two notions. 

In particular, note that the mapping $f \mapsto \int f \d \mu$ is a positive linear functional on $C_c(X)$. It turns out that *every* positive linear functional can be produced in this fashion. This correspondence is unique if we additionally assume that $\mu$ is Radon. In other words, we have identified the space of positive linear functionals on $C_c(X)$ with the Radon measures on $X$.

The proof is hard. For a little intuition on the idea of the proof, note that we have $\mu(U) = \int 1_U \d \mu$. We'd like to obtain a similar notion now, except replacing $1_U$ with a continuous approximation. We can do this by approximating $1_U$ from the above/below with smooth functions. We thus define $\mu$ via (1) on open sets, <a href="../../measure/construction/">extend to the Borel sets</a>, and check the resulting properties. Once we have constructed our measure, we check that integration against $\mu$ agrees with $I$ by decomposing $f$ into $N$ steps each of size $<1/N$, allowing us to obtain identical lower/upper bounds for integration against $\mu$ and $I$, which we combine to show the two values agree.

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

<br><br>

Let's now construct such a $\mu$. For an open set $U \subset X$, define $\mu(U)$ via (1) and define for arbirary $E \subset X$
\[
\mu^*(E) = \inf \left\{ \mu(U) : E \subset U, \; U \text{ open} \right\}
\]

and note this is well-defined as we've already chosen $\mu$ on the open sets. Note that if $U \subset V$ are both open, then $\mu(U) \leq \mu(V)$ and so $\mu^*$ agrees with $\mu$ on the open sets. We will proceed to esbalish the following facts.
<ol>
<li> $\mu^*$ is an outer measure </li>
<li> Every open set is $\mu^*$ measurable </li>
<li> $\mu$ satisfies (2) </li>
<li> $I(f) = \int f \d \mu$ for all $f \in C_c(X)$. </li>
</ol>

In particular, the first two facts will imply (via Caratheadory's Theorem) that $\mu = \mu^*\vert_{\BB(X)}$ is a Borel measure. The measure $\mu$ is outer regular and satisfies (1) by definition. Fact 3 immediately yields that $\mu$ is finite on compact sets, and yields that $\mu$ is inner regular on open sets. Indeed, suppose $U$ is open and $\alpha < \mu(U)$. Then, there exists some $f \in C_c(X)$ with $f \prec U$ and $I(f) > \alpha$. Set $K = \text{supp}(f)$. For any $g \in C_c(X)$ with $g \geq 1_K$, we have $g - f \geq 0$ so that $I(g) \geq I(f) > \alpha$. We then see
\[
\mu(K) = \inf \left\{ I(g) : g \in C_c(X), \; g \geq 1_K \right\} \geq I(f) > \alpha
\]

which implies that $\mu$ is inner regular on $U$.

<br><br>
<strong> Fact 1. </strong> It suffices to check that if $(U_j)_{j=1}^\infty$ is a sequence of open sets and $U = \bigcup_j U_j$, then
\[
\mu^*(U) \leq \sum_{j=1}^\infty \mu^*(U_j).
\]

Indeed, this shows that for every $E \subset X$,
\[
\mu^*(E) = \inf \left\{ \sum_{j=1}^\infty \mu(U_j) : U_j \text{ is open }, \; E \subset \bigcup_{j=1}^\infty U_j \right\}
\]

because the sufficient claim shows one direction of the inequality and set containment shows the other direction. As a consequence $\mu^*$ is an outer measure (see <a href="../../measure/construction/">Proposition 1 here</a>). So, let $f \in C_c(X), f \prec U$, and define $K = \text{supp}(f)$. Since $K \subset U$ is compact, we have $K \subset \bigcup_{j=1}^n U_j$ for some finite $n$. Let $g_1, g_2, \dots, g_n$ be a partition of unity subordinate to $(U_1, \dots, U_j)$, i.e. $g_j \prec U_j$ and $\sum_{j=1}^n g_j = 1$. Note $f = \sum_{j=1}^n f g_j$. Then,
\[
I(f) = \sum_{j=1}^n I(f g_j) \leq \sum_{j=1}^n \mu(U_j) \leq \sum_{j=1}^\infty \mu(U_j).
\]

Taking the supremum over the left-hand side yields the claim.

<br><br>
<strong> Fact 2. </strong> We need to show that if $U$ is open and $E \subset X$ is an arbitrary set such that $\mu^*(E) \subset X$, then $\mu^*(E) \geq \mu^*(E \cap U) + \mu^*(E \cap U^c)$. Fix $\epsilon >0$ and suppose first $E$ is open. Then, $E \cap U$ is open, so there exists $f \in C_c(X), f \prec U$ with $I(f) > \mu^*(E \cap U) - \epsilon$. Similarly, $E \setminus \text{supp}(f)$ is open, so there exists $g \in C_c(X)$ with $I(g) > \mu(E \setminus \text{supp}(f)) - \epsilon$. But then $f + g \prec E$ and 
\[ 
\mu^*(E) \geq I(f) + I(g) \geq \mu(E \cap U) + \mu(E \cap U^c) - 2 \epsilon.
\]

Taking $\epsilon \to 0$ shows the claim for $E$ open. For general $E \subset X$ with $\mu^*(E) < \infty$, we may find an open $V \supset E$ with $\mu(V) < \mu^*(E) + \epsilon$. Thus,
\[
\mu^*(E) + \epsilon > \mu(V) \geq \mu^*(V \cap U) + \mu^*(V \cap U^c) \geq \mu^*(E \cap U) + \mu^*(E \cap U^c).
\]
Again taking $\epsilon \to 0$ shows the claim for arbitrary $E$.

<br><br>

<strong> Fact 3. </strong> Let $K$ be compact, $f \in C_c(X)$, and $f \geq 1_K$. Let $U_\epsilon = \{ x : f(x) > 1 - \epsilon \}$. Then, $U_\epsilon$ is open. If $g \prec U_\epsilon$, then $(1-\epsilon)^{-1}f - g \geq 0$ and so $I(g) \leq (1 - \epsilon)^{-1} I(f)$. Hence, $\mu(K) \leq \mu(U_\epsilon) \leq (1-\epsilon)^{-1} I(f)$. As $\epsilon \to 0$ we see $\mu(K) \leq I(f)$. Conversely, if $U \supset K$ is open, Uryshon's Lemma supplies us with an $f \in C_c(X)$ with $f \prec U$ and $f \geq 1_K$. It follows that $I(f) \leq \mu(U)$. Since $\mu$ is outer regular on $K$, we have that $I(f) \leq \mu(K)$. Taking the supremum over such $f$ yields the claim.

<br><br>

<strong> Fact 4. </strong> It suffices to check this on $f \in C_c(X, [0, 1])$. To that end, for a fixed $N$ and $1 \leq j \leq N$, define $K_j = \{ x : f(x) \geq j/N \}$ and $K_0 = \text{supp}(f)$. Define
\[
f_j(x) = 
\begin{cases}
0 & x \notin K_{j-1} \\
f(x) - (j-1)/N & x \in K_j \setminus K_{j-1} \\
1/N & x \in K_j.
\end{cases}
\]

Observe that $\frac{1}{N} 1_{K_j} \leq f_j \leq \frac{1}{N} 1_{K_{j-1}}$ and $f = \sum_{j=1}^N f_j$. Thus,
\[
\frac{1}{N}\mu(K_j) \leq \int f_j \d \mu \leq \frac{1}{N} \mu(K_{j-1}).
\]

On the other hand, if $U \supset K_{j-1}$ is open, then $N f_j \prec U$, and so $I(f_j) \leq \frac{1}{N} \mu(U)$ by definition. Thus,
\[
\frac{1}{N} \mu(K_j) \leq I(f_j) \leq \frac{1}{N} \mu(K_{j-1})
\]

where the first inequality follows from the characterization (2) and the latter follows from outer regularity and the previous observation. Since $f = \sum_{j=1}^N f_j$ we see

\[
\frac{1}{N} \sum_{j=1}^N \mu(K_j) \leq \int f \d \mu \leq \frac{1}{N} \sum_{j=0}^{n-1}\mu(K_j)
\]


\[
\frac{1}{N} \sum_{j=1}^N \mu(K_j) \leq I(f) \leq \frac{1}{N} \sum_{j=0}^{n-1}\mu(K_j).
\]

Combining these two estimates yields
\[
\lvert I(f) - \int f \d \mu \rvert \leq \frac{\mu(K_0) - \mu(K_N)}{N} \leq \frac{\mu(\text{supp} f)}{N}
\]

and as $\text{supp}(f) < \infty$ we may take $N \to \infty$ to conclude.
</details>



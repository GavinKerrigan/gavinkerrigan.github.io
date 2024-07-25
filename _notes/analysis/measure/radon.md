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

If the space $X$ is not locally compact, we may still define a notion of Radon measures. However, in this situation, it is not always possible to express the Radon measures in terms of continuous linear functionals on $C_c(X)$. Moreover, it is possible to define a notion of Radon measures on non-Hausdorff spaces, but this is not very useful.


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

## Regularity and Approximation

In this section we'll see some further regularity properties of Radon measures. Recall that a Borel set is said to be $\sigma$-finite if it is the countable union of Borel sets with finite measure. Similarly, a Borel set is $\sigma$-compact if it is the countable union of compact sets. In both definitions the covering sets may be taken to be disjoint or increasing. 

First, we see that under a $\sigma$-finite assumption, we gain inner regularity on all Borel sets (and not just the open sets).

<div class='proposition'>
Let $\mu$ be a Radon measure. Then, $\mu$ is inner regular on all of its $\sigma$-finite sets. 
</div>
<details class='proof'>
<summary> Proof. </summary>
Fix $\epsilon > 0$. First, suppose that $E \in \BB(X)$ is such that $\mu(E) < \infty$. By outer regularity, there exists an open set $U \supset E$ with $\mu(U) < \mu(E) + \epsilon$. Because $U$ is open, by inner regularity we may find a compact $F \subset U$ such that $\mu(F) > \mu(U) - \epsilon$. 

<br><br>

Note that $\mu(U \setminus E) < \epsilon$, and so again by outer regularity we can find an open $V \supset U \setminus E$ with $\mu(V) < \epsilon$. Now, set $K = F \setminus V$ and note that $K$ is compact as it is a compact set minus an open set. Moreover, $K \subset E$ because $K = F \cap V^c$ and 
\[
V \supset U \cap E^c \implies V^c \subset U^c \cup E \subset E.
\]


The idea is that we approximate $E$ from the outside with a compact set $F$ "sandwiched" between $E$ and $U$, and that $V$ is the area between $U$ and $E$ that we'd like to throw away -- including some of $E$ near its boundary. We use $F$ as a tool to make sure the remaining bits contained in $E$ are compact.

Then, we have

\[
\begin{aligned}
\mu(K) &= \mu(F) - \mu(F \cap V) \\
&> \mu(U) - \epsilon - \mu(V) \\
&> \mu(E) - \epsilon - \mu(V) \\
&> \mu(E) - 2 \epsilon. 
\end{aligned}
\]

As $\epsilon$ was arbitrary we see that $\mu(E) = \sup\{\mu(K) : K \subset E, \; K \text{ compact} \}$ i.e. $E$ is inner regular.

<br><br>

If $\mu(E) = \infty$ and $E$ is $\sigma$-finite, then $E = \bigcup_{j=1}^\infty E_j$ where the $E_j$'s are increasing, of finite measure, and we may take $\mu(E_j) \to \infty$. In particular, for a given $N$ there is some $j$ with $\mu(E_j) > N$. The previous argument applied to $E_j$ yields a compact set $K \subset E_j \subset E$ with $\mu(K) > N$. Thus $\mu$ is inner regular on $E$ as we may find a sequence of compact sets $K_j \subset E$ with $\mu(K_j) \to \infty$. 
</details>

<div class='corollary'>
Every $\sigma$-finite Radon measure is regular. If $X$ is $\sigma$-compact, every Radon measure on $X$ is regular. 
</div>

Next, we see that we can approximate a Radon measure via closed/open sets.

<div class='proposition'>
Let $\mu$ be a $\sigma$-finite Radon measure and suppose $E \in \BB(X)$. Then, for every $\epsilon > 0$, there exists an open set $U$ and a closed set $F$ such that $F \subseteq E \subseteq U$ and $\mu(U \setminus F) < \epsilon$.
</div>
<details class='proof'>
<summary>Proof. </summary>
Let $E = \bigcup_{j=1}^\infty E_j$ where the $E_j$'s are disjoint and of finite measure. For each $j$, we can choose an open $U_j \supseteq E_j$ with $\mu(U_j) < \mu(E_j) + \epsilon 2^{-j + 1}$. Set $U = \bigcup_{j=1}^\infty U_j$. Observe that $U$ is open, $U \supseteq E$, and
\[
\mu(U \setminus E) = \mu\left(\bigcup_{j=1}^\infty U_j  \cap \left( \bigcap_{j=1}^\infty E_j^c\right) \right) \leq \sum_{j=1}^\infty \mu(U_j \setminus E_j) < \epsilon/2.
\]

The same argument applied to $E^c$ yields an open set $V \supset E^c$ with $\mu(V \setminus E^c) < \epsilon/2$. Set $F = V^c$ and observe that $F$ is closed with $F \subseteq E$. Now, since $V \setminus E^c = V \cap E = F^c \cap E = E \setminus F$, we see
\[
\mu(U \setminus F) = \mu(U \setminus E) + \mu(E \setminus F) < \epsilon
\]

which shows the claim.
</details>

In some cases, the underlying space $X$ is sufficiently nice that our measures are automatically Radon. We single this setting out with a definition.

<div class='definition' name='Radon Space'>
A LCH space $X$ is called a Radon space if every finite Borel measure on $X$ is a Radon measure.
</div>

The following theorem shows that every second-countable space is a Radon space. In fact, we show a slightly stronger statement -- namely, we relax the second-countability assumption and the finiteness assumption. Recall that every separable metric space is second-countable, and hence is a Radon space. 

<div class='theorem'>
Suppose $X$ is an LCH space in which every open set is $\sigma$-compact (e.g., $X$ is second-countable). Then, every Borel measure on $X$ which is finite on compact sets is regular, and hence Radon.
</div>
<details class='proof'>
<summary>Proof. </summary>
For such a measure $\mu$, we have $C_c(X) \subseteq L^1(\mu)$ easily. Hence $I(f) = \int f \d \mu$ is a positive linear functional on $C_c(X)$, and by the Riesz representation theorem, there exists a unique Radon $\nu$ such that $I(f) = \int f \d \nu$ for all $f \in C_c(X)$. We will show $\mu = \nu$.

<br><br>

First suppose $U \subset X$ is open. Then, $U$ is $\sigma$-compact, and so $U = \bigcup_{j=1}^\infty K_j$ for some compact $K_j$. Define the functions
\[
f_1 \in C_c(X) \qquad f_1 \prec U \qquad f_1 = 1 \text{ on K_1}
\]
\[
f_n \in C_c(X) \qquad f_n \prec U \qquad f_n = 1 \text{ on } \bigcup_{j=1}^{n} K_j \cup \bigcup_{j=1}^{n-1} \text{supp} f_j
\]

and note that $f_n \to 1_U$ is an increasing sequence converging pointwise to $1_U$. Thus, by the monotone convergence theorem,
\[
\mu(U) = \lim \int f_n \d \mu = \lim \int f_n \d \nu = \nu(U)
\]
and so $\mu = \nu$ on all open sets.

<br><br>

Now, suppose that $E \in \BB(X)$ is arbitrary. Then, by Proposition 3, there exists a closed set $F$ and an open set $V$ such that $F \subseteq E \subseteq V$ and $\nu(V \setminus F) < \epsilon$. But, since $V \setminus F$ is open, we see that $\nu(V \setminus F) = \mu(V \setminus F) < \epsilon$. In particular,
\[
\mu(V) \leq \mu(F) + \epsilon \leq \mu(E) + \epsilon \qquad \mu(F) \geq \mu(V) - \epsilon \geq \mu(E) - \epsilon. 
\]

The first of these inequalities shows that $\mu$ is outer regular on $E$. Moreover, $F$ is $\sigma$-compact (as a closed subset of $X$ which is $\sigma$-compact) and thus there exists a sequence of compact $K_j \subseteq F$ with $\mu(K_j) \to \mu(F)$. Together with the second inequality above this shows that $\mu$ is inner regular. Hence, $\mu = \nu$ for every $E \in \BB(X)$ by the uniqueness of $\nu$. 
</details>

## Measurable Functions and Radon Measures

We now study integration against Radon measures.

First, we see that $C_c(X)$ is a dense subset of $L^p(\mu)$ when $\mu$ is Radon. The proof is an easy application of Uryshon's Lemma and the approximation theorems we have already proved.

<div class='proposition' name='Density of Compactly Supported Functions'>
If $\mu$ is a Radon measure on $X$, then $C_c(X)$ is dense in $L^p(\mu)$ for $1 \leq p < \infty$.
</div>
<details class='proof'>
<summary> Proof. </summary>
Recall that the simple functions are dense in $L^p$. It suffices to show that for any Borel $E \subset X$ with $\mu(E) < \infty$, the indicator $1_E$ can be approximated in the $L^p(\mu)$ norm by elements of $C_c(X)$. To that end, for a fixed $\epsilon > 0$ we may find a compact $K$ and open $U$ such that $K \subseteq E \subseteq U$ and $\mu(U \setminus K) < \epsilon$. Uryshon's Lemma furnishes us with an $f \in C_c(X)$ such that $1_K \leq f \leq 1_U$. Then,
\[
\norm{1_E - f}_{L^p(\mu)}^p \leq \int 1_{U \setminus K} f^p \d \mu < \epsilon.
\]
</details>

Radon measures are also connected to the class of semicontinuous functions. We focus here on the LSC functions, but statements about LSC functions can typically be translated into USC functions without much hassle.

<div class='definition' name='Semicontinuity'>
Let $X$ be a topological space. A function $f: X \to (-\infty, \infty]$ is called lower semicontinuous (LSC) if $\{x : f(x) > a \}$ is open for every $a \in \R$. Similarly, $f: X \to [-\infty, \infty)$ is called upper semicontinuous (USC) if $\{ x: f(x) < a \}$ is open for every $a \in \R$.
</div>

<div class='proposition' name='Properties of LSC Functions'>
Let $X$ be a topological space.
<ol>
<li>If $U \subset X$ is open, then $1_U$ is LSC. </li>
<li>If $f$ is LSC and $c \in [0, \infty)$, then $cf$ is LSC. </li>
<li>If $\mathcal{G}$ is a collection of LSC functions and $f(x) = \sup \{ g(x) : g \in \mathcal{G} \}$, then $f$ is LSC. In other words, the pointwise supremum of LSC functions is LSC. </li>
<li>If $f_1, f_2$ are LSC, then $f_1 + f_2$ is LSC. </li>
<li>If $X$ is LCH and $f$ is LSC and $f \geq 0$, then \[ f(x) = \sup \{g(x) : g \in C_c(X), \; 0 \leq g \leq f \}. \]</li>
</ol>
</div>
<details class='proof'>
<summary> Proof. </summary>
The first two claims are straightforward. The third claim follows because
\[
f^{-1}(a, \infty] = \bigcup_{g \in \mathcal{G}} g^{-1}(a, \infty].
\]
For the fourth claim, fix an $a \in \R$ and suppose $x_0$ is such that $f_1(x_0) + f_2(x_0) > a$. Then, there is some $\epsilon > 0$ with $f_1(x_0) > a - g(x_0) + \epsilon$. Observe that a neighborhood of $x_0$ is given by
\[
\{ x : f(x_0) > a - f_2(x_0) + \epsilon \} \cap \{ x : f_2(x) > f_2(x_0) - \epsilon \}
\]

and moreover this neighborhood is contained within $\{ x: f_1(x) + f_2(x) > a \}$. Thus this set is open. Lastly, suppose $f(x) > 0$. Then, there exists an $a \in \R$ with $0 < a < f(x)$ and as $f$ is LSC the set $U = \{ y : f(y) > a \} $ is a neighborhood of $x$. Since $X$ is LCH, there is a compact neighborhood $K$ of $x$ which we may assume is contained within $U$. By Uryshon's Lemma, there exists $g \in C_c(X)$ with $g(x) = 1$ and $0 \leq g \leq a 1_U \leq f$. This shows the fifth claim (since $f(x)$ is clearly an upper bound on the set and we may thus find a sequence approaching this upper bound) when $f(x) > 0$. The case $f(x) = 0$ is trivial.
</details>






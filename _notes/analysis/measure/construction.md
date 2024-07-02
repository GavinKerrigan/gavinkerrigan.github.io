---
title: "Construction of Measures"
topic: "Analysis"
chapter: "Measure Theory"
section: "construction"
layout: note
permalink: "/notes/analysis/measure/construction/"

subtitle: 
date: 2024-07-01
keywords: analysis, measure theory
published: true
references: "Folland, G. B. (1999). Real analysis: Modern techniques and their applications (2nd ed.).; "
---


We collect here some tools that are essential when it comes to constructing measures. Morally speaking, the general idea is to approximate the measure of a set from above or from below, and a measure is obtained if these approximations agree in the limit.

Constructions like these are useful, as they allow us to define measures on smaller collections than a full $\sigma$-algebra. This often allows us to sidestep technical arguments when we seek to define specific measures. 

## Outer Measures

An outer measure allows us to approximate the measure of a set from above or from the outside. Note that an outer measure is defined on *all* of the subsets of a given nonempty set $X$. 

<div class='definition' name='Outer Measure'>
Let $X$ be a nonempty set. An outer measure is a function $\mu^*: 2^X \to [0, \infty]$ such that

<ol>
<li> $\mu^*(\varnothing) = 0$ </li>
<li> $\mu^*(A) \leq \mu^*(B)$ if $A \subset B$ </li>
<li> $\mu^*\left(\bigcup_{j=1}^\infty A_j \right) \leq \sum_{j=1}^\infty \mu^*(A_j)$ for any collection of subsets $A_j \subset X$ </li>
</ol>
</div>

In order to define an outer measure, one often specifes the outer measure on some "nice" sets, such as rectangles or balls, followed by approximating arbitrary sets from above using countable unions of these nice sets. In other words, the outer measure of an arbtrary set can be obtained as the smallest measure obtained by covering it in nice sets. The following makes this precise.

<div class='proposition' name='Constructing an Outer Measure'>
Suppose $\mathcal{E} \subset 2^X$ is an arbitrary collection of subsets with $\varnothing, X \in \mathcal{E}$. Let $\rho: \mathcal{E} \to [0, \infty]$ be such that $\rho(\varnothing) = 0$. Then, define $\mu^*: 2^X \to [0, \infty]$ for all $A \subset X$ via
\[
\mu^*(A) = \inf \left\{ \sum_{j=1}^\infty \rho(E_j) : E_j \in \mathcal{E}, \; A \subset \bigcup_{j=1}^\infty E_j \right\}.
\]

Then, $\mu^*$ is an outer measure on $X$.
</div>



<details class='proof'>
<summary> Proof. </summary>
Note that for any $A \subset X$ the set over which we are taking the infimum is nonempty as $X \in \mathcal{E}$. Moreover it is clear that $\mu^*(\varnothing) = 0$. If $A \subset B$, then $\mu^*(A) \leq \mu^*(B)$ as a covering for $B$ induces a covering for $A$, so the set over which we are taking the infimum is thus smaller for $A$.

<br><br>
Let's now check countable subadditivity. Fix $\epsilon > 0$. For any given $A_j \subset X$, there exists a sequence $(E_j^k)_{k=1}^\infty$ with $E_j^k \in \mathcal{E}$ and $A_j \subset \bigcup_k E_j^k$. Moreover, we may choose this sequence so that
\[
\sum_{k=1}^\infty \rho(E_j^k) \leq \mu^*(A_j) + \epsilon 2^{-j}.
\]

Thus, if $A = \bigcup_j A_j$, then $A \subset \bigcup_{j,k} E_j^k$ and moreover
\[
\mu^*(A) \leq \sum_{j,k} \rho(E_j^k) \leq \sum_{j=1}^\infty \mu^*(A_j) + \epsilon.
\]

Since $\epsilon$ was arbitrary we conclude.
</details>

We will often need to obtain a genuine measure from an outer measure. Let's see how to do this.

<div class='definition' name='Outer Measurability'>
Let $\mu^*$ be an outer measure on $X$. A set $A \subset X$ is called $\mu^*$-measurable if
\[
\mu^*(E) = \mu^*(E \cap A) + \mu^*(E \cap A^c) \qquad \forall E \subset X.
\]
</div>

The idea of this definition is a little mysterious. Folland writes the following. Suppose $E \supset A$ is "nice". Then, $\mu^\*(E) - \mu^\*(E \cap A^c)$ is in some sense the "inner measure" of $A$ obtained by discarding the bits outside of $A$. Thus, if $A$ is $\mu^\*$-measurable, its inner and outer measures agree. It is generally not sufficient to only consider the inner measure tested against $X$, though, as shown by the nice example in <a href="https://math.stackexchange.com/questions/4381477/understanding-when-a-set-is-outer-measurable">this link</a>.

Note that we always have
\\[
\mu^\*(E) = \mu^\*\left( (E \cap A) \cup (E \cap A^c) \right) \leq \mu^\*(E \cap A) + \mu^\*(E \cap A^c)
\\]

and so one only needs to check the reverse inequality. If $\mu^\*(E) = \infty$ this is trivially satisfied, and so we have the following lemma.

<div class='lemma'>
Let $\mu^*$ be an outer measure on $X$. A set $A \subset X$ is $\mu^*$ measurable if and only if
\[
\mu^*(E) \geq \mu^*(E \cap A) + \mu^*(E \cap A^c)
\]

for every $E \subset X$ with $\mu^*(E) < \infty$.
</div>

## Extension Theorems

We arrive now at a fundamental theorem, allowing us to obtain genuine measures from outer measures. Intuitively, we take an outer measure and restrict our attention to the $\mu^*$-measurable sets. The proof is long, but largely just requires following your nose and doing some set algebra calculations. The difficulty in proving this theorem is not so much the proof itself but rather getting the right definitions.

<div class='theorem' name='Carath&eacute;adory Theorem'>
Let $\mu^*$ be an outer measure on $X$. The collection $\Sigma$ of $\mu^*$-measurable sets is a $\sigma$-algebra, and the restriction of $\mu^*$ to $\Sigma$ is a complete measure.
</div>
<details class='proof'>
<summary> Proof. </summary>
Observe that $\Sigma$ is closed under complements. We check that it is closed under finite unions, and hence $\Sigma$ is an algebra. Indeed, let $A, B$ be $\mu^*$-measurable sets. Observe that $A \cup B = A \cap B + A \cap B^c + B \cap A^c$, and so the subadditivity of $\mu^*$ yields
\[
\mu^*(E \cap (A \cup B)) \leq \mu^*(E \cap A \cap B) + \mu^*(E \cap A \cap B^c) + \mu^*(E \cap A^c \cap B).
\]

Then, using the definition of $\mu^*$-mesurability and the previous line,
\[
\begin{aligned}
\mu^*(E) &= \mu^*(E \cap A) + \mu^*(E \cap A^c) \\
&= \mu^*(E \cap A \cap B) + \mu^*(E \cap A \cap B^c) + \mu^*(E \cap A^c \cap B) + \mu^*(E \cap A^c \cap B^c) \\
&\geq \mu^*(E \cap (A \cup B)) + \mu^*(E \cap (A \cup B)^c) \\
\end{aligned}
\]

which shows $A \cup B$ is $\mu^*$-measurable, and hence $\Sigma$ is an algebra.

<br><br>

Now, note that if $A, B \in \Sigma$ and $A \cap B = \varnothing$, then
\[
\mu^*(A \cup B) = \mu^*((A \cup B) \cap A) + \mu^*((A \cup B) \cap A^c) = \mu^*(A) + \mu^*(B)
\]
and so $\mu^*$ is finitely additive on disjoint subsets of $\Sigma$.

<br><br>

We check that $\Sigma$ is closed under countable disjoint unions, whence it is a $\sigma$-algebra. Indeed, if $(A_j)_{j=1}^\infty$ is a countable sequence of $\mu^*$-measurable sets, we set $B_n = \bigcup_{j=1}^n A_j$ and $B = \bigcup_{j=1}^\infty A_j$. Then, for any $E \subset X$, we have
\[
\mu^*(E \cap B_n) = \mu^*(E \cap B_n \cap A_n) + \mu^*(E \cap B_n \cap A_n^c) = \mu^*(E \cap A_n) + \mu^*(E \cap B_{n-1}).
\]

Induction shows $\mu^*(E \cap B_n) = \sum_{j=1}^n \mu^*(E \cap A_j)$. As a consequence,
\[
\mu^*(E) = \mu^*(E \cap B_n) + \mu^*(E \cap B_n^c) \geq \sum_{j=1}^n \mu^*(E \cap A_j) + \mu^*(E \cap B^c).
\]

Upon taking $n \to \infty$ we see
\[
\begin{aligned}
\mu^*(E) &\geq \sum_{j=1}^n \mu^*(E \cap A_j) + \mu^*(E \cap B^c) \\
&\geq \mu^*\left( \bigcup_{j=1}^\infty E \cap A_j \right) + \mu^*(E \cap B^c) \\
&= \mu^*(E \cap B) + \mu^*(E \cap B^c) \geq \mu^*(E).
\end{aligned}
\]

This shows $B \in \Sigma$, and so $\Sigma$ is a $\sigma$-algebra. Moreover, all inequalities in the previous calculation are actually equalities. Thus, taking $E = B$ we obtain
\[
\mu^*(B) = \sum_{j=1}^n \mu^*(E \cap A_j)
\]

which shows $\mu^*$ is countably additive on disjoint sets in $\Sigma$.

<br><br>

We have thus far shown that $\Sigma$ is a $\sigma$-algebra and that $\mu^*$ is a measure on $\Sigma$. To conclude, we show that $\mu^*$ is complete. It suffices to check that any $\mu^*$-measure-zero set is in $\Sigma$. Indeed, suppose $\mu^*(A) = 0$. Then,
\[
\mu^*(E) \leq \mu^*(E \cap A) + \mu^*(E \cap A^c) = \mu^*(A \cap A^c) \leq \mu^*(E)
\]

where the equality follows as $0 \leq \mu^*(E \cap A) \leq \mu^*(A) = 0$. 
</details>

We will now apply Carath&eacute;adory's Theorem to extend measures from algebras to $\sigma$-algebras. We first define a premeasure, which essentially is a set-valued function that has the properties of a measure, but is only defined on an algebra. 

<div class='definition' name='Premeasures'>
Let $\AA \subset 2^X$ be an algebra. A function $\mu_0: \AA \to [0, \infty]$ is called a premeasure if
<ol>
<li> $\mu_0(\varnothing) = 0$. </li>
<li> If $(A_j)_{j=1}^\infty$ is a sequence of disjoint sets in $A$ such that $\bigcup_{j=1}^\infty A_j \in \AA$, then \[ \mu_0\left( \bigcup_{j=1}^\infty A_j \right) = \sum_{j=1}^\infty \mu_0(A_j). \] </li>
</ol>
</div>

Observe that we require the assumption that $\bigcup_j A_j \in \mathcal{A}$ which is not necessary for a genuine measure. By Proposition 1, a premeasure $\mu_0$ induces an outer measure $\mu^*$ defined on all of $2^X$. The proof is a straightforward exercise in checking the definitions. 

<div class='proposition'>
Let $\mu_0$ be a premeasure on an algebra $\AA$, and define the outer measure $\mu^*$ on $2^X$ via Proposition 1. Then,
<ol>
<li> $\mu^*\vert_\AA = \mu_0$. </li>
<li> Every set in $\AA$ is $\mu^*$ measurable. </li>
</ol>
</div>
<details class='proof'>
<summary> Proof. </summary>
Let $A \in \AA$. For the first claim, it is clear that $\mu^*(A)\leq \mu_0(A)$. Conversely, if $A \subset \bigcup_{j=1}^\infty A_j$, then we may define
\[
B_n = A \cap \left(A_n \setminus \bigcup_{j=1}^{n-1} A_j\right)
\]

so that the $B_n$'s are disjoint, $B_n \in \AA$, and $\bigcup_{n=1}^\infty B_n = A$. It follows that
\[
\mu_0(A) = \sum_{n=1}^\infty \mu_0(B_n) \leq \sum_{j=1}^\infty \mu_0(A_j) \leq \mu^*(A)
\]

and hence $\mu^*\vert_\AA = \mu_0$.

<br><br>

For the second claim, for a given $E \subset X$ and $\epsilon > 0$ we may find a sequence $(B_j)_{j=1}^\infty$ such that $B_j \in \AA$ and $E \subset \bigcup_{j=1}^\infty B_j$ and
\[
\sum_{j=1}^\infty \mu_0(B_j) \leq \mu^*(E) + \epsilon.
\]

Now, since $\mu_0$ is additive on $\AA$, we have
\[
\begin{aligned}
\mu^*(E) + \epsilon &\geq \sum_{j=1}^\infty \mu_0(B_j) \\
&= \sum_{j=1}^\infty \mu_0(B_j \cap A) + \mu_0(B_j \cap A^c) \\
&\geq \mu^*(E \cap A) + \mu^*(E \cap A^c)
\end{aligned}
\]

where the last line follows from the definition of $\mu^*$. 
</details>

Let's now put everything together. Observe that this theorem actually gives us something a little stronger than what is stated -- namely, we can extend $\mu_0$ to a measure on the $\sigma$-algebra of $\mu^*$ measurable sets, which may be larger than $\sigma(\AA)$ in general. Note that the measure $\mu$ obtained in the following theorem may fail to be complete. 

<div class='theorem' name='Carath&eacute;adory Extension Theorem'>
Let $\AA$ be an algebra and let $\mu_0$ be a premeasure on $\AA$. Let $\Sigma = \sigma(\AA)$ be the $\sigma$-algebra generated by $\AA$. Then, there exists a measure $\mu$ on $\AA$ whose restriction to $\AA$ is given by $\mu_0$. Namely, $\mu = \mu^*\vert_\AA$ where $\mu^*$ is the outer measure produced from $\mu_0$ via Proposition 1.

<br><br>

Moreover, if $\nu$ is another measure on $\Sigma$ which extends $\mu_0$, then $\nu(E) \leq \mu(E)$ for all $E \in \Sigma$, with equality when $\mu(E) < \infty$. If $\mu_0$ is $\sigma$-finite, then $\mu$ is the unique extension of $\mu_0$ to a measure on $\Sigma$.
</div>
<details class='proof'>
<summary> Proof. </summary>
The first claim is a consequence of Theorem 1 and Proposition 2. In particular, the $\sigma$-algebra of $\mu^*$-measurable sets contains $\AA$ and thus $\Sigma$.

<br><br>

We now turn our attention towards uniqueness. Suppose $\nu$ is another measure on $\Sigma$ which extends $\mu_0$. Suppose $E \in \Sigma$ is such that $E \subset \bigcup_{j=1}^\infty A_j$ for $A_j \in \AA$. Then, we have
\[
\mu(E) \leq \nu\left(\bigcup_{j=1}^\infty A_j\right) \leq \sum_{j=1}^\infty \nu(A_j) = \sum_{j=1}^\infty \mu_0(A_j).
\]

Taking an infimum over the right-hand side yields $\nu(E) \leq \mu(E)$.

<br><br>
Now set $A = \bigcup_{j=1}^\infty A_j$ to see that
\[
\nu(A) = \lim_{n \to \infty} \nu \left( \bigcup_{j=1}^n A_j \right) = \lim_{n \to \infty} \mu \left( \bigcup_{j=1}^\infty A_j \right) = \mu(A).
\]

If $\mu(E) < \infty$, choose the $A_j$'s such that $\mu(A) < \mu(E) + \epsilon$ so that $\mu(A \setminus E) < \epsilon$. This yields
\[
\begin{aligned}
\mu(E) &\leq \mu(A) = \nu(A) \\
&= \nu(E) + \nu(A \setminus E) \leq \nu(E) + \mu(A \setminus E) \\
&\leq \nu(E) + \epsilon.
\end{aligned}
\]

As $\epsilon$ was arbitrary we see that $\nu(E) = \mu(E)$ whenever $\mu(E) < \infty$.

<br><br>

Lastly, suppose that $X = \bigcup_{j=1}^\infty A_j$ with $\mu_0(A_j) < \infty$ and $A_j \in \AA$. We may assume WLOG that the $A_j$'s are disjoint. Then, for any $E \in \Sigma$, 
\[
\mu(E) = \sum_{j=1}^\infty \mu(E \cap A_j) = \sum_{j=1}^\infty \nu(E \cap A_j) = \nu(E)
\]

and hence $\mu = \nu$ as claimed.

</details>








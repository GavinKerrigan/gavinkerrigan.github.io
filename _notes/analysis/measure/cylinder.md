---
title: "The Cylindrical Sigma-Algebra"
topic: "Analysis"
chapter: "Measure Theory"
section: "cylinder"
layout: note
permalink: "/notes/analysis/measure/cylinder/"

subtitle: 
date: 2025-04-22
keywords: analysis, measure theory, functional analysis, cylindrical sigma algebra, cylinder sets
published: true
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 2, 4."
---

Cylindrical sets and their associated $\sigma$-algebra are a tool for doing measure theory on infinite-dimensional spaces. The basic philosophy is that we can attempt to do everything in terms of a projection onto some finite-dimensional set.


Throughout this note, $X$ is an arbitrary real normed vector space. For a collection of functionals $(x\_k^\*)\_{k=1}^n$ we will use $(x\_1^\* \times x\_2^\* \times \dots \times x\_n^\*)$ to represent the mapping $X \to \R^n$ obtained by applying each functional to $x \in X$ and stacking, i.e.,
\\[
x \mapsto (\langle x\_1^\*, x \rangle, \dots, \langle x\_n^\*, x \rangle)^{\sf T}.
\\]

## Cylindrical Sets


<div class='definition' name='Cylinder Sets'>
Fix $n \in \Z_{\geq 0}$,, a collection $(x_k^*)_{k=1}^n \subset X^*$, and a measurable Borel set $A_n \in \mathcal{B}(\R^n)$. The set
\[
\hat{A}_n = \left\{ x \in X : [\langle x_1^*, x \rangle, \dots, \langle x_n^*, x \rangle]^{\sf T} \in A_n \right\}
\]

is called a cylinder with base $A_n$. The class of all cylinders is denoted by 
\[

\text{Cyl}(X) = \left\{ A \in X : A = \hat{A}_n \, \text{for some } \, A_n \right\}
\]
</div>

In other words, a cylinder with base $A_n$ is the preimage of the mapping $(x\_1^\* \times \dots \times x\_n^\*): X \to \R^n$. Loosely speaking, we can view this mapping as taking $n$ projections (or coordinates) of $x \in X$. A cylinder set, then, is defined by vectors satisfying finitely many constraints. The canonical example to keep in mind is $X = \ell^2$ and $x\_k^\* = \langle e\_k, \cdot \rangle$ is projection onto the $k$th coordinate. 

It is important to note that a given $A \in \text{Cyl}(X)$ generally has many representatives. For instance, if $A = \hat{A}\_n$, then we also have that $A = (x\_1^\* \times \cdots \times x\_n^\* \times x\_{n+1}^\*)^{-1}(A\_n \times \R)$ for any $x\_{n+1}^\* \in X^\*$.

## The Cylindrical $\sigma$-Algebra

In the following proposition, we show that $\text{Cyl}(X)$ is unforunately not a $\sigma$-algebra. Thus, for the purposes of doing measure theory, it will be necessary to work with $\CC = \sigma\\{ \text{Cyl}(X) \\}$, the cylindrical $\sigma$-algebra.

<div class='proposition'>
The class $\text{Cyl}(X)$ is an algebra of sets. If $\text{dim} X = \infty$, then it is not a $\sigma$-algebra.
</div>
<details class='proof'>
<summary> Proof. </summary>
The set $\text{Cyl}(X)$ clearly contains $X$. If $A \in \text{Cyl}(X)$, then $A = \hat{A}_n$ for some base set $A_n \in \R^n$ and linear functionals $(x_k^*)_{k=1}^n$. Similarly, for $B \in \text{Cyl}(X)$, we have $B = \hat{B}_m$ for some $B_m \in \R^m$ and $(y_k^*)_{k=1}^m$. 


Then,
\begin{align}
X \setminus A &= \left\{x \in X : (x_1^* \times \dots \times x_n^*)(x) \in A_n^c \right\}
\end{align}
\begin{align}
A \cup B = \left\{ x : (x_1^* \times \dots \times x_n^* \times y_1^* \times \dots \times y_m^*)(x) \in (A_n \times \R^m) \cup (\R^n \times B_m) \right\}.
\end{align}

This shows that $\text{Cyl}(X)$ is an algebra.

<br><br> 
Conversely, suppose that $\text{dim}X = \infty$. It follows that the dual space is also infinite dimensional, and thus we can find a linearly independent sequence $(x_k^*)_{k=1}^\infty \subset X^*$. Let $S = \cap_{k=1}^\infty \text{ker}(x_k^*)$. Observe that each of the $\text{ker}(x_k^*)$'s is a cylindrical set. However, $S$ is not cylindrical. To show this, suppose for the sake of contradiction that $S$ takes the form
\begin{equation}
S = \left\{ x \in X : (z_1^* \times \dots \times z_m^*)(x) \in B_m \right\}.
\end{equation}

Let $K = \cap_{k=1}^m \text{ker}(z_k^*)$. We have that $K \subseteq S$. This is because if $x \in S$ and $z \in K$, then $x+z \in S$, and the fact that $0 \in S$. Thus, for any $n$, we see that $K \subseteq \text{ker}(x_n^*)$. A well-known theorem of linear algebra then implies that $x_n^* \in \text{span}(z_1^*, \dots, z_m^*)$. Once $n > m$, this contradicts the assumption that $(x_k^*)_{k=1}^\infty$ is linearly independent. Thus, $S$ cannot be cylindrical.
</details>

In fact, one of the main reasons to work with $\CC$ is that it coincides with the Borel $\sigma$-algebra when $X$ is separable. It is worth appreciating how powerful this is -- studying the Borel sets on a separable space can be reduced to studying the much simpler cylindrical sets.

<div class='lemma'>
Suppose $(x_n) \subset X$ is a dense set in $X$. Then, there exists a collection $(x_n^*) \subset X^*$ with $|x_n^*| = 1$ and $\langle x_n , x_n^* \rangle = |x_n|$. Moreover, for any $x \in X$, we have
\[
|x| = \sup_{n} | \langle x, x_n^* \rangle |.
\]
</div>
<details class='proof'>
<summary> Proof. </summary>
The existence of such a sequence $(x_n^*)_{n=1}^\infty$ is a well-known consequence of the Hahn-Banach theorem. For the second claim, note that $| \langle x_n^*, x \rangle| \leq |x|$ and so the supremum is at most $|x|$. On the other hand, thanks to density, we can find a sequence in $(x_n)_{n=1}^\infty$ converging to $x$. By the reverse triangle inequality,
\begin{align}
| \langle x_n^*, x \rangle| &\geq |\langle x_n, x_n^* \rangle| - |\langle x_n - x, x_n^* \rangle| \\
&\geq |x_n| - |x_n - x|.
\end{align}
Since the supremum is at most the limit, we conclude.
</details>

<div class='theorem' name="Mourier's Theorem">
Let $X$ be a separable real normed vector space. Then, the cylindrical $\sigma$-algebra $\CC$ coincides with the Borel $\sigma$-algebra $\BB$.
</div>
<details class='proof'>
<summary> Proof. </summary>
We first show $\CC \subseteq \BB$. Fix $A \in \CC$, so that $A = (x_1^* \times \dots \times x_n^*)^{-1}(A_n)$ for some Borel $A_n \in \R^n$. It is clear enough that the mapping $(x_1^* \times \dots \times x_n^*): X \to \R^n$ is continuous. In particular, it is then Borel measurable, and thus $A \in \BB$. 

<br><br>
Conversely, recall that since $X$ is separable, $\BB$ is generated by the closed balls in $X$. Moreover, there exists a countable dense subset $(x_n)_{n=1}^\infty \subset X$. By the previous lemma, we obtain a corresponding collection of norming functionals $(x_n^*)_{n=1}^\infty$. For some fixed $x_0 \in X$ and $r > 0$, note that the previous lemma shows that
\[
|x - x_0| \leq r \iff |\langle x -  x_0, x_n^* \rangle| \leq r \quad \forall n.
\]
In other words, we have that
\[
\overline{B}(x_0, r) = \bigcap_{n=1}^\infty \left\{ x \in X : \langle x - x_0, x_n^* \rangle \leq r \right\}.
\]

Thus we see that $\overline{B}(x_0, r) \in \CC$ is actually cylindrical. It follows that $\BB \subseteq \CC$.
</details>

The key lesson to remember in the above proof is that we're trying to show that closed balls are cylindrical, i.e., expressed in terms of some finite collection of functionals. In separable spaces, we can take a "norming net" of functionals to accomplish this. 
---
title: "Trace Operators"
topic: "Analysis"
chapter: "PDEs"
section: "trace"
layout: note
permalink: "/notes/analysis/pde/trace/"

subtitle: Extending the notion of boundary values to Sobolev spaces
date: 2024-06-24
keywords: analysis, pdes
published: true
references: "Evans, L. C. (2022). Partial differential equations (2nd ed.).; "
---

Throughout this note we assume $1 \leq p < \infty$. Suppose $u \in W^{1,p}(U)$. We'd like to have some notion of boundary values for $u$. However this is not straightforward for several reasons. First, $u$ may fail to be continuous, and hence it is unclear how to extend $u$ to the boundary. Even worse, $u \in W^{k,p}(U)$ is only defined up to a set of Lebesgue measure zero, and $\partial U$ has measure zero. 


The notion of a *trace* will serve as a replacement. The following theorem furnishes us with a linear operator that provides the boundary values in the smooth case. The strategy of the proof is a sequence of approximations, structured roughly as follows:
1. First assume $u$ is smooth and $\partial U$ is flat near some $x_0$. Then, in a neighborhood around $x_0$, we will locally control the $L^p$ norm of $u \vert_{\partial U}$ by the $W^{1,p}(U)$ norm. By straightening the boundary, we can relax the flatness assumption.
2. Since $U$ is bounded, $\partial U$ is compact. Use a finite open cover of $\partial U$ to estimate the the $L^p$ norm of $u \vert_{\partial U}$ over the entire boundary.
3. Use the density of the smooth functions in $W^{1,p}(U)$ to relax the smoothness assumption on $u$.

We will use $C$ to denote a generic constant whose value changes throughout the proof.

<div class='theorem' name='Trace Theorem'>
Assume $U \subset \R^n$ is a bounded open set, and $\partial U$ is $C^1$. Then, there exists a bounded linear operator

\[
T: W^{1,p}(U) \to L^p(\partial U)
\]

such that $Tu = u\vert_{\partial U}$ if $u \in W^{1,p}(U) \cap C(\overline{U})$. Moreover, there exists a constant $C = C(p, U)$ such that
\[
\norm{Tu}_{L^p(\partial U)} \leq C \norm{u}_{W^{1,p}(U)}
\]

for all $u \in W^{1,p}(U)$. The function $Tu \in L^p(\partial U)$ is called the trace of $u$. 
</div>
<details class="proof">
<summary> Proof. </summary>
<strong>
Step one: smooth $u$ and flat boundary.
</strong>
Assume $u \in C^1(\overline{U})$. Fix an $x_0 \in \partial U$ and assume $\partial U$ is flat near $x_0$ and lies in the plane $\{x_n = 0\}$. Then, there exists an open ball $B$ of radius $r$ centered at $x_0$. Let $B^+ = B \cap \{x_n \geq 0 \} \subseteq \overline{U}$ and $B^- = B \cap \{ x_n \leq 0\} \subseteq \R^n \setminus U$. Set $\hat{B}$ to be the open ball of radius $r/2$ contained within $B$. Set $\Gamma = \partial U \cap \hat{B}$ be the portion of the boundary contained within $\hat{B}$. 

<br><br>

Let $\zeta \in C_c^\infty(U)$ be $\zeta \geq 0$ in $B$ and $\zeta = 1$ on $\hat{B}$. Set $x' = (x_{1:n-1})$ to be the first $n-1$ coordinates. Now, by an application of integration by parts,

\[
\begin{aligned}
\int_{\Gamma} |u|^p \d x' &\leq \int_{\{x_n = 0\}} \zeta |u|^p \d x' \\
&= -\int_{B^+} \partial_n (\zeta |u|^p) \d x \\
&= -\int_{B^+} |u|^p \partial_n \zeta + \zeta p|u|^{p-1} (\text{sign} u) \partial_n u \d x \\
\end{aligned}
\]

Since $\zeta$ is smooth the first term is bounded by $C \int_{B^+} |u|^p \d x$. Now, by Young's inequality $ab \leq p^{-1} a^p + q^{-1} b^q$ with $a = \partial_n u$, $b = |u|^{p-1}$,

\[
\zeta p|u|^{p-1} (\text{sign} u) \partial_n u \leq C(|u|^{p-1} \partial_n u) \leq C(|u|^p + |D u|^p). 
\]

Overall we see 
\[
\int_{\Gamma} |u|^p \d x' \leq C \int_{B^+} |u|^p + |Du|^p \d x.
\]

<strong>
Step two: relax flatness.
</strong>
When $\partial U$ is not flat near $x_0$, we may use the assumption that $\partial U$ is $C^1$ to flatten the boundary and apply the above result. This yields that for any $x_0 \in \partial U$ there is some open $\Gamma \subset \partial U$ with

\[
\int_{\Gamma} |u|^p \d S \leq C \int_U |u|^p + |D u|^p \d x.
\]

<strong>
Step three: global estimate by compactness.
</strong>
Since $U$ is assumed to be bounded, $\partial U$ is compact. Thus, there exists a finite set of points $x_0^i$ and open $x_0^i \in \Gamma_i \subset \partial U$ such that $\partial U = \bigcup_{i=1}^n \Gamma_i$. Applying step two, we see

\[
\norm{u}_{L^p(\Gamma_i)} \leq C(p, U) \norm{u}_{W^{1,p}(U)}.
\]

Set $Tu = u\vert_{\partial U}$. Then, we have
\[
\norm{Tu}_{L^p(\partial U)}^p \leq \sum_{i=1}^N \int_{\Gamma_i} |u|^p \d S \leq C \norm{u}_{W^{1,p}(U)}^p. 
\]

<strong>
Step four: smooth approximations.
</strong>
Now fix a generic $u \in W^{1,p}(U)$. Then, there exists a sequence $(u_m)$ in $C^{\infty}(\overline{U})$ (see <a href="../sobolev_approx/">this note</a>) with $u_m \to u$ in $W^{1,p}(U)$. By the previous calculations,

\[
\norm{Tu_j - T u_k}_{L^p(\partial U)} \leq C \norm{u_j - u_k}_{W^{1,p}(U)}
\]

whence $(T u_n)$ is a Cauchy sequence in $L^p(\partial U)$. Let us define then $Tu$ to be the $L^p(\partial U)$ limit of this sequence. Observe that this limit is independent of the approximating sequence and that $T$ defined in this way is linear.

To conclude, we note that if $u \in W^{1,p}(U) \cap C(\overline{U})$, then $u_m \to u$ converge uniformly on $\overline{U}$. Thus, $Tu = \lim T(u_m) = \lim u_m \vert_{\partial U} = u\vert_{\partial U}$ where the limit may be taken to be in the uniform topology.
</details>

### Zero-Trace Functions

The functions $u \in W^{1,p}(U)$ for which $Tu = 0$, i.e. those with vanishing trace, are of particular interest. Here, we give an explicit characterization. We will use the notation $W^{k,p}_0(U)$ to denote the closure of $C_c^\infty(U)$ in the $W^{k,p}(U)$ norm.

<div class='theorem' name='Trace-Zero Functions'>
Let $U \subset \R$ be bounded and open with $\partial U$ being $C^1$. Suppose $u \in W^{1,p}(U)$. Then,
\[
u \in W^{1,p}_0(U) \iff T u = 0 \text{ on } \partial U.
\]
</div>
<details class='proof'>
<summary> Proof. </summary>
We only prove the forward direction here. Suppose $u \in W_0^{1,p}(U)$. Then, by defintion, there exists a sequence $(u_m)$ in $C_c^\infty(U)$ such that $u_m \to u$ in the $W^{1,p}(U)$ norm. However, $T u_m = 0$ for every $m = 1, 2, \dots$ and thus
\[
\norm{T u_m - T u}_{L^p(\partial U)} = \norm{Tu}_{L^p(\partial U)} \leq \norm{T} \norm{u_m - u}_{W^{1,p}(U)} \to 0.
\]
</details>


In other words, we can interpret $u \in W_0^{1,p}(U)$ as those functions vanishing at the boundary. By taking weak derivatives, we may conclude (loosely speaking) that in the general case, a function $u \in W_0^{k,p}(U)$ has $D^\alpha u = 0$ on $\partial U$ whenever $\|\alpha\| \leq k - 1$. 









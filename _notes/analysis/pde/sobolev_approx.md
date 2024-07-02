---
title: "Smooth Approximations in Sobolev Spaces"
topic: "Analysis"
chapter: "PDEs"
section: "sobolev_approx"
layout: note
permalink: "/notes/analysis/pde/sobolev_approx/"

subtitle:
date: 2024-06-21
keywords: pdes, analysis, sobolev spaces
published: true
references: "Evans, L. C. (2022). Partial differential equations (2nd ed.).; "
---

## Mollifiers

Let $U \subset \R^d$ be open and fix $\epsilon > 0$. We will write

\\[
U_\epsilon = \left\\{ x \in U : d(x, \partial U) > \epsilon \right\\}
\\]

for the set of points $\epsilon$-far from the boundary.

<div class='definition' name='Standard Mollifier'>
Let $\eta \in C_c^\infty(\R^d)$ be defined by

\[
\eta(x) = \begin{cases}
	   C \exp\left(\frac{1}{|x|^2 - 1}\right) & |x| < 1 \\
	   0 & |x| \geq 1
\end{cases}
\]

where $C>0$ is a constant such that $\int_{\R^d} \eta \d x = 1$. This function is the standard mollifier. For $\epsilon > 0$, we define

\[
\eta_\epsilon(x) = \epsilon^{-n} \eta(x/\epsilon).
\]

Observe that $\eta_\epsilon \in C_c^\infty(\R^n)$, $\int_{\R^n} \eta_\epsilon \d x = 1$ and that the support of $\eta_\epsilon$ is contained within $\overline{B(0, \epsilon)}$. 
</div>

Informally, for small $\epsilon$, $\eta_\epsilon$ is a smooth approximation to $\delta(x)$. 

<div class='definition' name='Mollification'>
Let $f \in L^1_{\text{Loc}}(U)$. The mollification of $f$ is given by
\[
f^\epsilon: U_\epsilon \to \R \qquad f^\epsilon = \eta_\epsilon \star f
\]

\[
f^\epsilon(x) = \int_U \eta_\epsilon(x - y) f(y) \d y = \int_{B(0, \epsilon)} \eta_\epsilon(y) f(x - y) \d y \qquad \forall x \in U_\epsilon
\]
</div>

<div class='theorem' name='Properties of Mollifiers'>
For $f \in L^1_{\text{Loc}}(U)$, we have the following properties:
<ol>
<li> $f^\epsilon \in C^\infty(U_\epsilon)$ </li>
<li> $f^\epsilon \to f$ almost everywhere as $\epsilon \to 0$ </li>
<li> If $f \in C^0(U)$, then $f^\epsilon \to f$ uniformly on compact subsets of $U$ </li>
<li> For $1 \leq p < \infty$ and $f \in L^p_{\text{Loc}}(U)$, $f^{\epsilon}\to f$ in $L^p_{\text{Loc}}(U)$.</li>
</ol>
</div>


## Local Smooth Approximations

Our first approximation theorem is local. By mollifying $u \in W^{k,p}(U)$ we obtain a smooth function which is recovers, at least locally, $u$ in the limit $\epsilon \to 0$. The key idea of the proof is that we can interchange the order of (weak) differentiation and mollification. 

<div class='theorem' name='Local Smooth Approximation'>
Let $u \in W^{k,p}(U_\epsilon)$ for some $1 \leq p < \infty$. Then,
<ol>
<li> $u^\epsilon \in C^\infty(U)$ for every $\epsilon > 0 $. </li>
<li> $u^\epsilon \to u$ in $W^{k,p}_{\text{Loc}}(U)$ as $\epsilon \to 0$. </li>
</ol>
</div>
<details class="proof">
<summary> Proof. </summary>
The first claim is immediate as a property of mollification. For the second claim, we first show that for $|\alpha| \leq k$, 
\[
D^{\alpha} u^\epsilon = \eta_\epsilon \star D^\alpha u \qquad \text{in } \; U_\epsilon
\]

i.e. the ordinary derivative of the smooth function $u^\epsilon$ is the same as mollifying the weak derivative $D^\alpha u$. Indeed, for $x \in U_\epsilon$, we have by ordinary differentiation

\[
\begin{aligned}
D_x^\alpha u^\epsilon(x) &= D_x^\alpha \int_U \eta_\epsilon(x-y) u(y) \d y \\
&= \int_U D_x^\alpha \eta_\epsilon(x - y) u(y) \d y \\
&= (-1)^{|\alpha|} \int_U D_y^\alpha \eta_\epsilon(x - y) u (y) \d y.
\end{aligned}
\]

Now, since $\varphi(y) = \eta_\epsilon(x - y) \in C_c^\infty(U)$, we may weakly differentiate $u$ to obtain

\[
= (-1)^{2 |\alpha|} \int D^\alpha u(y) \eta_\epsilon(x - y) \d y = [\eta_\epsilon \star u](x).
\]

To complete the proof, we now fix $V \Subset U$ open. By Theorem 1,

\[
D^\alpha u^\epsilon = \eta_\epsilon \star u \to D^\alpha u
\]
in $L^p(V)$ as $\epsilon \to 0$. Since this holds for every $|\alpha| \leq k$ and open $V \Subset U$ we see that $u^\epsilon \to u$ in $W_{\text{Loc}}^{k,p}(U)$. 
</details>

## Global Smooth Approximations

We can extend our local approximations to a global approximation. In other words, we have that $W^{k,p}(U)$ is the closure of $C^\infty(U) \cap W^{k,p}(U)$, and so the smooth functions are dense in $W^{k,p}(U)$. 

The main difficulty is that we only have smooth approximations locally since mollifying shrinks the support. Thus, we need some technique for "extending to the boundary". The idea of the proof is to decompose $U$ via a smooth partition of unity, and to apply the local approximation result to each partition. Note that in the approximation, we do not have $u_m \in C^{\infty}(\overline{U})$, i.e. the approximates may be badly behaved on $\partial U$. However, this is because we make no smoothness assumptions on $\partial U$. This weakness can be overcome (as in the subsequent theorem). 

<div class='theorem' name='Global Smooth Approximation (Meyers-Serrin 1964)'>
Assume $U \subset \R^d$ is open and bounded and suppose $u \in W^{k,p}(U)$ for some $1 \leq p < \infty$. Then, there exists a sequence of functions $u_m \in C^{\infty}(U) \cap W^{k,p}(U)$ such that $u_m \to u$ in $W^{k, p}(U)$. 
</div>
<details class="proof">
<summary> Proof. </summary>
Let 

\[
U_i = \{x \in U : d(x, \partial U) > 1/i\} \qquad i = 1, 2, \dots
\]

and $V_i = U_{i+3} \setminus \overline{U}_{i+1}$. Note the $V_i$'s are open and we can choose $V_0 \Subset U$ such that $U = \bigcup_{i=0}^\infty V_i$. Pick a smooth partition of unity $\{ \zeta_i \}_{i=0}^\infty$ that is subordinate to $\{ V_i \}_{i=0}^\infty$, i.e. satisfying

\[
0 \leq \zeta_i \leq 1 \qquad \zeta_i \in C_c^\infty(V_i) \qquad \sum_{i=0}^\infty \zeta_i = 1 \quad \text{on } U.
\]

Fix $\delta > 0$ and set $W_i = U_{i+4} \setminus \overline{U}_i \supset V_i$ for $i = 1, 2, \dots$. For fixed $\epsilon_i > 0$, let $u^i = \eta_{\epsilon_i} \star (\zeta_i u)$. Observe that $\zeta_i u \in W^{k,p}(U)$ and that $\zeta_i u$ is supported on $V_i$. 

<br><br>

Observe that $u^i \to \zeta_i u$ in $W^{k,p}_{\text{Loc}}(U)$ as $\epsilon_i \to 0$. In other words, for any $Z \Subset U$, $\norm{u^i - \zeta_i u}_{W^{k,p}(Z)} \to 0$ as $\epsilon_i \to 0$. 

 If the support of $\zeta_i u$ and $u^i$ are contained in a compactly contained set $Z \Subset U$, then we can conclude $\norm{u^i - \zeta_i u}_{W^{k,p}(U)} \to 0$ as well. Although $\zeta_i u$ is supported on $V_i$, $u^i$ may not be (as it is supported on $B(0, \epsilon_i) + V_i$). However, for $\epsilon_i$ sufficiently small, both are supported on $W_i \supset V_i$ and we thus may conclude that
 
 \[
 \norm{u^i - \zeta_i u}_{W^{k,p}(U)} \leq \frac{\delta}{2^{i+1}} \qquad i = 0, 1, \dots
 \]
 
 for $\epsilon_i$ sufficently small.
 
<br><br>

Now, set $v = \sum_{i=0}^\infty u^i$. Observe that for any open $V \Subset U$, only finitely many terms in this sum are nonzero, and each is smooth, so $v \in C^\infty(U)$. As $u = \sum_{i=0}^\infty \zeta_i u$ (and again, only finitely many terms appear for $V \Subset U$), we have for every $V \Subset U$ that
\[
\norm{v - u}_{W^{k^p}(V)} \leq \delta.
\]

Taking the supremum over $V \Subset U$ we see $\norm{v - u}_{W^{k,p}(U)} \leq \delta$. 
</details>

It turns out that you can also take the approximations to be smooth on the boundary. We'll skip the proof of this and take it for granted. This stronger theorem requires a smoothness condition on the boundary. 

<div class='theorem' name='Smooth Approximation 2'>
Fix $1 \leq p < \infty$ and assume $U \subset \R^d$ is open and bounded and $\partial U$ is $C^1$. Then, $C^\infty(\overline{U})$ is dense in $W^{k,p}(U)$.
</div>







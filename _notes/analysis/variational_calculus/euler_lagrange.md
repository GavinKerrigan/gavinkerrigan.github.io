---
title: "Euler-Lagrange Equations"
topic: "Analysis"
chapter: "Calculus of Variations"
section: "euler_lagrange"
layout: note
permalink: "/notes/analysis/variational_calculus/euler_lagrange/"

subtitle: Classical notions in the calculus of variations
date: 2024-06-17
keywords: calculus of variations, analysis
published: true
---


Let $U \subset \R^d$ be open and bounded, and consider a function $L: U \times \R \times \R^d \to \R$. This function is often called the *Lagrangian*. We will write $L = L(x, z, p)$ for the arguments of this function, where $x \in U, z \in \R$, and $p \in \R^d$. We assume throughout that $L$ is smooth and that $\partial U$ is sufficiently smooth.

Our goal is to find a function $u: U \to \R$ minimizing the functional


\\[
I(u) = \int_U L\left(x, u(x), \nabla u(x)\right) \d x \tag{1}
\\]

subject to boundary condtions $u = g$ on $\partial \Omega$. 

## The Euler-Lagrange Equation

Let's analyze the functional $I(u)$. In the following, we compute what is essentially a directional derivative of $I$ at a point $u \in C^2(\overline{U})$ in the direction specified by $\varphi \in C_c^\infty(U)$. This is typically called the *first variation* of $I$. 

<div class='theorem' name='Euler-Lagrange Equation'>
Suppose $u \in C^2(\overline{U})$. For all $\varphi \in C_c^\infty(U)$, we have

\[
\frac{\d}{\d \epsilon}\Big\vert_{\epsilon=0} I(u + \epsilon \varphi) = \int_U \left(\partial_z L - \nabla \cdot (\nabla_p L) \right) \varphi \d x.
\]

</div>

<details class="proof">
<summary> Proof. </summary>

Since $L$ is smooth, we may compute

\[
\begin{aligned}
\frac{\d }{\d \epsilon}\Big\vert_{\epsilon = 0}I(u + \epsilon \varphi) &= \int_U \frac{\d }{\d \epsilon} \Big\vert_{\epsilon = 0} L(x, u + \epsilon \varphi, \nabla u + \epsilon \nabla \varphi) \d x \\
&= \int_U \partial_z L(x, u, \nabla u) \varphi + \langle \nabla_p L(x, u, \nabla u), \nabla \varphi \rangle \d x.
\end{aligned}
\]

Since $\varphi = 0$ on $\partial U$, we may use the divergence theorem to compute

\[ 
\int_U \langle \nabla_p L, \nabla \varphi \rangle \d x = - \int_U \nabla \cdot (\nabla_p L) \varphi \d x.
\]

Thus, we have

\[
\frac{\d}{\d \epsilon}\Big\vert_{\epsilon=0} I(u + \epsilon \varphi) = \int_U \left(\partial_z L - \nabla \cdot (\nabla_p L) \right) \varphi \d x.
\]

for every $\varphi \in C_c^\infty(U)$ as desired.
</details>



### The Gradient Interpretation

The expression $\partial_z L - \nabla \cdot (\nabla_p L)$ is the *Euler-Lagrange* expression for the Lagrangian $L$. This is often suggestively written as $\nabla I (u)$. Observe that in this language, the previous theorem tells us that for every test function $\varphi \in C_c^\infty(U)$,

\\[
\langle \nabla I(u), \varphi \rangle_{L^2(U)} = \frac{\d}{\d \epsilon}\Big\vert_{\epsilon=0} I(u + \epsilon \varphi).
\\]

This is analogous to the usual notion of a gradient recovering the directional derivatives through an inner product. We will henceforth use the notation $\nabla I(u)$ for the Euler-Lagrange expression of $L$. 

We emphasize that some care should be taken with this notion of a gradient. In particular, the Euler-Lagrange expression for the gradient *depends* on the choice of inner product, and different choices will result in different notions of a functional gradient. Moreover, the functional gradient only recovers directional derivatives for smooth variations $\varphi$. These ideas may be made more precise through the notion of a [Gateaux derivative](https://en.wikipedia.org/wiki/Gateaux_derivative) which we will not expore here.

### A Necessary Condition for Optimality

In finite-dimensional vector calculus, a necessary condition for the optimality of a smooth function $f: \R^d \to \R$ is that $\nabla f = 0$. We prove here an analogous result for the functional $I(u)$.


<div class='theorem' name='Euler-Lagrange Necessary Condition'>
Suppose $u \in C^2(\overline{U})$ minimizes $I$ amongst all admissible functions, i.e.

\[
I(u) \leq I(v)
\]

for all $v \in C^2(\overline{U})$ with $v = g$ on $\partial U$. Then, $\nabla I(u) = 0$ on $U$. 

</div>

<details class="proof">
<summary> Proof. </summary>

Let $\varphi \in C_c^\infty(U)$ be fixed and consider $v = u + \epsilon \varphi$ for $\epsilon \in \R$. Note that $v$ is admissible, as $v = u = g$ on $\partial U$ as $\varphi = 0$ on $\partial U$. Consider the function $h(\epsilon) = I(u + \epsilon \varphi)$. Since $u$ is optimal, it follows that $h$ has a global minimum at $\epsilon = 0$. It follows that

\[
0 = h'(t) = \frac{\d}{\d \epsilon}\Big\vert_{\epsilon=0} I(u + \epsilon \varphi) = \langle \nabla I(u), \varphi \rangle_{L^2(U)}.
\]

Since $\varphi \in C_c^\infty(U)$ was arbitrary, it follows from the <a href="../vanishing_lemma/">vanishing lemma</a> that $\nabla I(u) = 0$ on $U$. 
</details>

The Euler-Lagrange equation $\nabla I(u) = 0$ results in a PDE with boundary conditions for the unknown $u$. Solutions to this PDE are known as *critical points* of the Euler-Lagrange equation. While the Euler-Lagrange equation provides us with a necessary condition, questions of existence and sufficiency are delicate.

In cases where a boundary condition is not specified, we need additional data to actually solve the Euler-Lagrange equation.

<div class='theorem' name='Euler-Lagrange Boundary Conditions'>
Suppose $u \in C^2(\overline{U})$ minimizes $I$ globally, i.e.

\[
I(u) \leq I(v)
\]

for all $v \in C^2(\overline{U})$. Then, $\nabla I(u) = 0$ on $U$ and $\nabla_p L \cdot \nu = 0$ on $\partial U$, where $\nu$ is the outward pointing normal on the boundary. 

</div>

<details class="proof">
<summary> Proof. </summary>
Since our assumptions are stronger than the previous theorem we immediately obtain $\nabla I(u) = 0$ on $U$. Let $\varphi \in C^\infty(\overline{U})$ be a smooth function not necessarily vanishing on the boundary. Since $I(u) \leq I(u + \epsilon \varphi)$ for any $\epsilon > 0$, arguing as in the previous theorem we obtain

\[
0 = \frac{\d }{\d \epsilon}\Big\vert_{\epsilon = 0} I(u + \epsilon \varphi) = \int_U \partial_z L \varphi + \langle \nabla_p L , \nabla \varphi \rangle \d x.
\]

The divergence theorem yields

\[
0 = \int_{\partial U} \varphi \langle \nabla_p L, \nu \rangle \d S + \langle \nabla I(u), \varphi \rangle_{L^2(U)} \d x.
\]

Since $\nabla I(u) = 0$, the second term vanishes and we obtain $\langle \nabla_p L, \nu \rangle = 0$ on $\partial U$ by the <a href="../vanishing_lemma/">vanishing lemma</a>.
</details>

## An Example

Consider the *Dirichlet energy*

\\[
I(u) = \int_U \frac{1}{2} |\nabla u|^2 - uf \d x
\\]

for a given $f: U \to \R$. We seek to minimize $I$ over all $u \in C^2(U)$ such that $u = g$ on $\partial U$. We can straightforwardly calculate the Euler-Lagrange equation to obtain a necessary condition on $u$:

\\[
-\Delta u = f \quad \text{on } U \qquad u = g \quad \text{on } \partial U.
\\]

This is a boundary value problem for the Laplace equation.



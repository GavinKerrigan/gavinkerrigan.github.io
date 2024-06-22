---
title: "The JKO Scheme"
topic: "Analysis"
chapter: "Optimal Transport"
section: "jko_scheme"
layout: note
permalink: "/notes/analysis/optimal_transport/jko/"

subtitle: 
date: 2024-06-20
keywords: calculus of variations, analysis
published: true
---

Many PDEs can be posed as variational problems, where the solution to a PDE can be described as minimizing some functional defined in an appropriate space. For instance, recall that the <a href="../../variational_calculus/euler_lagrange/">Poisson equation can be seen as the minimizer of the Dirichlet energy</a>. This suggets an intimate link between *optimization* and *solving PDEs*.

A fundamental technique in the optimization toolkit is gradient descent. If we are able to phrase a PDE as the minimizer of some functional, then performing gradient descent on this functional in the appropriate space should give us a numerical scheme for solving this PDE.

The Jordan-Kinderlehrer-Otto scheme (JKO) carries out this task for the Fokker-Planck-Kolmogorov equation. It turns out that the right space for doing this is the Wasserstein space, leading to a connection with optimal transport.

## Minimizing Movements Scheme

We begin with some informal preliminaries on gradient flows. Suppose for now that we are working on $\R^d$ and $F: \R^d \to \R$ is smooth. To seek (local) minima of $F$, it is natural to consider the gradient flow

\\[
d X_t = - \nabla F (X_t) \d t \qquad X_0 = x_0 \qquad t \in [0, T].
\\]

If we discretize time with an *implicit* Euler scheme, we obtain updates of the form

\\[
X_{k} = X_{k-1} - \tau \nabla F(X_k) \qquad k = 1, 2, \dots
\\]

As this scheme is implicit, implementing it requires solving an ODE for $X_k$. However, a little rearranging yields

\\[
\frac{X_k - X_{k-1}}{\tau} + \nabla F(X_t) = \nabla \left( \frac{1}{2 \tau} \lvert\lvert X_k - X_{k-1} \rvert\rvert_2^2 + F(X_k) \right) = 0.
\\]

This suggests that $X_k$ can be found via optimization, i.e.

\\[
X_k = \arg\min_{X} \left\\{ \frac{1}{2 \tau} \lvert\lvert X - X_{k-1} \rvert\rvert_2^2 + F(X) \right\\}.
\\]

This approach to minimizing $F$ is called the *minimizing movements scheme*, as the updates seek to decrease $F$ while remaining close in the Euclidean metric to the previous iterates. One benefit of this scheme is that it is possible to generalize to more general metric spaces and is applicable when $F$ is non-smooth.

For a fixed step size $\tau$, we can define a piecewise constant curve on $[0, T]$ via

\\[
X_\tau(t) = X_k \qquad t \in ((k-1)\tau, k\tau]
\\]

and, under appropriate assumptions and notions of convergence, we may obtain a curve in the limit $\tau \to 0$. 

### Example: Heat Equation and Dirichlet Energy

Consider the space $L^2(\R^d)$ and the Dirichlet energy functional $F:L^2(\R^n) \to \R$

\\[
F(p) = \frac{1}{2} \int_{\R^n} | \nabla p |^2 \d x.
\\]

The heat equation $\partial_t p_t = \Delta p_t$ can be seen as the gradient flow of $F$. Indeed, computing the first variation of $F$ we see that $\nabla F(p) = - \Delta(p)$, and the heat equation is $\partial_t p_t = - \nabla F(p) = \Delta (p)$. At equilibrium, we obtain the Poisson equation. 

A minimizing movement scheme for the heat equation is then

\\[
p_{k} = \arg \min_{p} \left\\{ \frac{1}{2 \tau} \lvert\lvert p - p_{k-1} \rvert\rvert_{L^2(\R^d)}^2 + \frac{1}{2} \int_{\R^n} | \nabla p |^2 \d x \right\\}. 
\\]


## The JKO Scheme

The JKO scheme can be viewed as a minimizing movements scheme for the negative differential entropy under the Wasserstein metric. In other words, we will see that diffusion SDEs can be seen as a gradient flow in the Wasserstein space $\mathbb{P}_2(\R^d)$ which seeks to maximize the entropy.

### The FPK Equation

We first recall some notions regarding diffusion SDEs and the Fokker-Planck-Kolmogorov (FPK) equation. In this note, we closey follow [JKO, 1996] and only consider constant-strength diffusions with drift given by the gradient field of a potential. We refer to <a href="../pde/fpk/">this note</a> for a more general outlook and details.

Consider the Ito SDE

\\[
dX_t = - \nabla \psi (X_t) \d t + \sqrt{2 \beta} d W_t \qquad X_0 \sim p_0
\\]

for a given smooth potential $\psi: \R^d \to \R$, constant $\beta > 0$, and initial distribution $p_0$. It is well-known that the marginal densities of the solutions of this SDE solve the FPK equation

\\[
\partial_t p_t = \nabla \cdot (p_t \nabla \psi) + \beta \Delta p \qquad p_0 = p_0.
\\]

As long as the potential $\psi$ grows sufficiently rapidly at infinity, this PDE admits a unique stationary distribution

\\[
p_\infty \propto \exp(- \beta^{-1} \psi).
\\]

Notice that $p_\infty$ minimizes the KL divergence functional

\\[
F(p) = \mathrm{KL}[p \mid\mid p_\infty] = \int p \psi \d x + \beta \int p \log p \d x + \log(Z)  
\\]

where $Z = \int \exp(- \beta \psi) \d x$ is the partition function. This can be seen by considering the constrained variaitonal minimization problem via Lagrange multipliers. This suggests that we may potentially view the FPK equation as a gradient flow of the KL divergence, once properly understood.

### The JKO Scheme

The JKO scheme is a minimizing movement scheme for the FPK equation. Assume that the potential $\psi$ satisfies

\\[
\psi \in C^\infty(\R^n) \qquad \psi \geq 0 \qquad |\nabla \psi(x)| \leq C(\psi(x) + 1)
\\]

where $C < \infty$ is a constant. Note that $\psi = K$ being constant is admissible, recovering the heat PDE -- in this case, the stationary distribution $p_\infty$ is not well defined. However, the functional $F(p)$ is still well-defined (up to dropping the constant $\log(Z)$.) Consider the set $\mathbb{P}_2^\lambda(\R^d)$ consisting of the subspace of the 2-Wasserstein space, consisting of measures admitting a density w.r.t. the Lebesgue measure $\lambda$. The **JKO scheme** is given by

\\[
p_k = \arg \min \left\\{ \frac{1}{2\tau} W_2^2(p, p_{k-1}) + F(p) : p \in \mathbb{P}_2^\lambda(\R^d) \right\\}. \tag{1}
\\]

This scheme is well-defined, and moreover, as the step size $\tau \to 0$, we recover the solution to the FPK equation. We write $p_t^\tau(x)$ for the piecewise constant curve on $[0, T]$ obtained by this scheme with fixed step size $\tau > 0$. 

<div class='theorem' name='JKO Scheme Converges to Solution of the FPK Equation'>
Assume $p_0 \in \mathbb{P}_2^\lambda(\R^d)$. Then,
<ol>
    <li> The minimizer in Equation (1) exists and is unique. </li>
    <li> Suppose further that $F(p_0 < \infty$. As $\tau \to 0$, the minimizing movement scheme curve $p_t^\tau$ converges weakly in $L^1(\R^n)$ to the unique solution $p_t$ of the FPK equation for all $t \in (0, \infty)$.  </li>.
</ol>
</div>

The proof of this theorem requires a fairly involved analysis, and as such we won't reproduce it here. 

It is worth repeating the significance of this result: we have seen that the FPK equation can be viewed, loosely, as the gradient flow of the KL divergence in the Wasserstein metric. This was obtained by a limiting procedure of a discrete-time approximation. Going in the opposite direction, i.e. from a gradient flow to time-discretized dynamics, is quite difficult as the space $\mathbb{P}_2(\R^d)$ cannot be equipped with a genuine differentiable structure. 

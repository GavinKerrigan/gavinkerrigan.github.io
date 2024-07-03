---
title: "Wasserstein Gradient Flows"
topic: "Analysis"
chapter: "Optimal Transport"
section: "wgf"
layout: note
permalink: "/notes/analysis/optimal_transport/wgf/"

subtitle: 
date: 2024-07-02
keywords: analysis, optimal transport, gradient flows
published: true
references: "Jordan, R., Kinderlehrer, D., & Otto, F. (1998). The variational formulation of the Fokker--Planck equation. SIAM journal on mathematical analysis, 29(1), 1-17.; Hamfeldt, B. (2019) Gradient flows in the Wasserstein metric. https://www.youtube.com/watch?v=zzGBxAqJV0Q"
---

We saw in a <a href="../jko/">previous post</a> that the JKO scheme is a time-discretzed flow of the KL divergence functional towards a specified reference prior. In this note, we will generalize this idea to other functionals. This leads to the notion of a Wasserstein gradient flow. We will start out with a formal description to fix the ideas.

Suppose $\Omega \subset \R^d$ is compact and $F: \P_2(\Omega) \to \R$ is LSC and bounded from below. We turn the space $\P_2(\Omega)$ into a metric space by equipping it with the $W_2$ norm. For a fixed $\tau > 0$, define
\\[
p_\tau^n \in \arg\min_{p \in \P_2(\Omega)} \left\\{ \frac{W_2^2(p, p_\tau^n)}{2 \tau} + F(p) \right\\} \qquad n = 1, 2, \dots \tag{1}
\\]
and recall that this can be viewed as a generalized time-discretized gradient flow of $F$. Note that this is a well-defined optimization problem thanks to our assumptions on $F$. Set
\\[
p_\tau(t) = p_\tau^n \qquad t \in ((n-1)\tau, n\tau]
\\]

to be the peicewise-constant curve obtained from this scheme. Our goal is to study the behavior of the resulting curve as $\tau \to 0$, which (provided such a limit exists) is a curve $p: [0, T] \to \P_2(\Omega)$. Such a curve will be called the Wasserstein gradient flow (WGF) of $F$. We assume throughout that all probability measures admit densities with respect to the Lebesgue measure on $\Omega$. 

Here, we note that while we have defined things in terms of the $W_2$ norm, a similar construction can work in more general metric spaces. However, the $W_2$ metric often naturally shows up in applications, as we saw for the JKO scheme.

## The Wasserstein Gradient

Recall the continuity equation is given by $\partial_t p_t + \text{div}(v_t p_t) = 0$. We'd like to obtain a particle-level description of the dyamics of $p_t$ induced by the WGF. To do so, let's see what the vector field $v_t$ should be. We begin by studying the optimality conditions for the discrete scheme (1). In other words, we'd like to compute the first variation of (1).

### First Variation of the Energy
Let's compute the first variation of $F$. Some caution is needed, as we can only handle perturbations which leave us in $\P_2(\Omega)$ -- otherwise, $F$ doesn't make sense. In other words, we seek directions $\chi$ such that $\sigma = p + \epsilon \chi \in \P_2(\Omega)$ for all $\epsilon$ sufficiently small. Upon rescaling let's suppose $\sigma = p + \chi \in \P_2(\Omega)$. This implies that
\\[
p + \epsilon \chi = (1 - \epsilon) p + \epsilon \sigma \in \P_2(\Omega) \qquad \forall 0 \leq \epsilon \leq 1 
\\]
as long as $p, \sigma \in \P_2(\Omega)$. That is, we may restrict our attention to perturbations of the form $\chi = \sigma - p$ for some $\sigma \in \P_2(\Omega)$. For good measure let's assume that $\sigma$ is compactly supported and bounded, so $\sigma \in P(\Omega) \cap L_c^\infty(\Omega)$.

Thus, we seek the first variation $\frac{\delta F}{\delta p}(p): \Omega \to \R$ such that
\\[
\frac{\d }{\d \epsilon}\Big\vert_{\epsilon = 0} F(p + \epsilon \chi) = \left\langle \frac{\delta F}{\delta p}(p), \chi \right\rangle_{L^2(\Omega)} = \int_\Omega \frac{\delta F}{\delta p}(p)(x) \chi(x) \d x
\\]

for all $\chi = \sigma - p, \sigma \in \P_2(\Omega) \cap L_c^\infty(\Omega)$. This, however, does not uniquely define the first variation, but rather only defines it up to an additive constant, since

\\[
\left\langle \frac{\delta F}{\delta p}(p) + C, \chi \right\rangle_{L^2(\Omega)} = \left\langle \frac{\delta F}{\delta p}(p), \chi \right\rangle_{L^2(\Omega)} + \langle C, \chi \rangle_{L^2(\Omega)}
\\]

and the second term is zero as $\chi$ is the difference of two densities. Thus, when we seek to optimize $F$, we must set $\frac{\delta F}{\delta p}(p) = C$ to a constant. This point is subtle, but important -- using the wrong class of perturbations can lead to incorrect notions of the flow. Going any further from here now requires us to choose a specific form for $F$. 

### First Variation of the Metric

Along similar lines, let us now compute the first variation of the $W_2$ metric. Set
\\[
G(p) = W_2^2(p, q) \qquad q \in \P_2(\Omega)
\\]
for some arbitrary given density $q \in \P_2(\Omega)$. We want to compute $\frac{\delta G}{\delta p}(p)$. Let's use the dual formulation of this metric, which we recall as
\\[
\begin{aligned}
W_2^2(p, q) &= 2 \max_{u,v} \left\\{ \int u \d p + \int v \d q : u(x) + v(y) \leq \frac{1}{2} |x-y|^2 \right\\} \\\\\
&= 2 \max_u \left\\{ \int u \d p + \int u^c \d q \right\\}. 
\end{aligned}\tag{2}
\\]

Why use the dual formulation and not the Kantorovich formulation? Well, we'll want to perturb $p$ to $p + \epsilon \chi$, and this is relatively easy to work with under an integral in the dual formulation. Trying to work with this perturbation in the Kantorovich formulation would involve the constraint, which is a little unfriendly. 

Set $u^\*$ to be the maximizer of this problem, i.e. the usual potential for the (half-) quadratic cost between $p$ and $q$. Recall that we may recover the optimal transport map $T$ from the potential $u^\*$ via
\\[
\begin{aligned}
T(x) &= x - (\nabla h)^{-1}(\nabla u^\*(x)) \\\\\
&= x - \nabla u^\*(x)
\end{aligned}
\\]

where $h = \frac{1}{2} \|z\|^2$.

Now, glossing over some details, to differentiate the max in (2) we find the optimal $u^*$ and then differentiate. This leads to
\\[
\frac{\d}{\d \epsilon}\Big\vert_{\epsilon = 0} G(p + \epsilon \chi) = 2 \int u^\* \d \chi
\\]
and thus we see the first variation is given (again, up to an additive constant) by
\\[
\frac{\delta W_2^2(p, q)}{\delta p}(p) = 2 u^\*.
\\]

### Snapping the Pieces Back in Place

Based on our calculations so far, we now know that if $p_\tau^{n+1}$ is a minimizer of the scheme (1), then we first variation (which we have now computed) must be constant, i.e.

\\[
\tau^{-1} u^* + \frac{\delta F}{\delta p}(p_\tau^{n+1}) = C
\\]

where $u^*$ is the potential between $p_\tau^n$ and $p_\tau^{n+1}$. We now feel a compelling urge to take the gradient of the above (to obtain a vector field, to kill the constant, and to relate things to the optimal transport map). A little rearranging yields

\\[
\frac{T(x) - x}{\tau} = \left(\nabla \frac{\delta F}{\delta p}\right).
\\]

The left-hand side looks suggestively like the velocity of a flow from $p_\tau^{n+1}$ to $p_\tau^n$. Our flow should go in the opposite direction, so we negate this to see
\\[
v_\tau(x) = - \frac{T(x) - x}{\tau} = - \nabla \left(\frac{\delta F}{\delta p}\right).
\\]

This $v_\tau(x)$ is the velocity field associate with our discrete-time scheme. If everything works out, then we should expect that in the limit $\tau \to 0$ we should obtain that the JKO scheme converges towards a curve $(p_t) \subset \P_2(\R^d)$ satisfying

\\[
\partial_t p_t - \text{div}\left(p_t \nabla \frac{\delta F}{\delta p}\right) = 0.
\\]

This is the PDE associated with the WGF of $F$, and $\nabla \left( \frac{\delta F}{\delta p} \right)$ is called the Wasserstein gradient of $F$.

## Examples

Let's look at a few examples. This mostly involves computing the first variation of some given functional $F$, and plugging in to our expression for the Wasserstein gradient. In the literature, many more functionals have been studied than those we list here.

### Negative Differential Entropy

Consider the negative differential entropy functional
\\[
F(p) = \int p \log p \d x.
\\]

Intuitively, minimizing $F$ seeks to maximize the entropy of $p$. A straightforward calculation (i.e., plug in to the Euler-Lagrange expression) yields

\\[
\frac{\delta F}{\delta p}(p) = \log p + 1 \qquad \nabla \left( \frac{\delta F}{\delta p} \right) = \frac{1}{p} \nabla p.
\\]

Hence the WGF PDE is
\\[
\partial_t p_t = \text{div} \left(p_t \frac{1}{p_t} \nabla p_t\right) = \Delta p_t
\\]

which is the heat equation. Intriguingly, <a href='../jko/'>we have seen</a> that the heat equation also arises as the gradient flow of the Dirichlet energy under the $L^2$ metric.

### Entropy with a Potential

For a smooth potential $V: \Omega \to \R$, the energy
\\[
F(p) = \int p \log p \d x + \int V(x) p \d x
\\]

yields through a similar calculation
\\[
\frac{\delta F}{\delta p}(p) = 1 + \log p + V \qquad \partial_t p_t = \Delta p - \text{div}(p_t \nabla V)
\\]

which is the FPK equation. When the potential $V(x) = -\log q(x)$ is given by the negative log-likelihood of some density $q$, we see that $F(p) = \text{KL}[p \mid\mid q]$.

### $f$-Divergences

If $f \in C^2(\R)$ and $f(1) = 0$, then we may define a functional through the $f$-divergence, i.e.
\\[
F(p) = D_f[p \mid\mid q] = \int f(p/q) q \d x
\\]
which yields a nonlinear evolution equation
\\[
\frac{\delta F}{\delta p}(p) = f'(p / q) \qquad \partial_t p_t - \text{div}\left( p_t \nabla f'(p/q) \right).
\\]

## Conclusion and Outlook

It's worth stepping back and seeing the big picture of the strategy. In the smooth setting, we can start with the continuous-time gradient flow, which we then discretize in time to obtain something which is gradient-free. This discrete-time scheme is applicable in more general metric spaces, and in particular, in the Wasserstein space $\P_2(\Omega)$. Analysis of this discrete scheme in the Wasserstein space suggests to us an appropriate notion of gradient flows in the limit of zero discretization error.

The WGF gives us a nice toolbox -- given an energy $F$, we now have some techniques for analyzing and simulating the gradient flow on this energy. Numerically, JKO scheme-type methods can provide tools for simulations which preserve some kind of desirable structure in your PDE, such as maximum principles. In terms of theoretical applications, the WGF is often used to prove the existence and uniqueness of solutions to PDEs, and conversely, to study properties of a given evolution equation. 


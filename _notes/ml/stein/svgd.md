---
title: "Stein Variational Gradient Descent"
topic: "Machine Learning"
chapter: "Stein Methods"
section: "stein"
layout: note
permalink: "/notes/ml/stein/svgd/"

subtitle: 
date: 2024-07-24
keywords: analysis, optimal transport, gradient flows
published: true
references: "Liu, Q., Wang, D. (2016). Stein variational gradient descent: A general purpose Bayesian inference algorithm. NeurIPS.; "
---

Suppose $U \subseteq \R^d$ and $T: U \to U$ is invertible. We use $\|D T (x)\|$  to denote the Jacobian determinant of $T:U \to U$ evaluated at $x \in U$. Recall that the inverse function theorem tells us that
\\[
|D T^{-1} (x)| = |D T (T^{-1}(x))|^{-1}.
\\]

Recall further that when $p$ is a probability density with respect to the Lebesgue measure, then the change-of-variables formula gives us the density for the pushforward via
\\[
T\_{\\#} p(x) = p(T^{-1}(x)) \|D T^{-1}(x)\|.
\\]

## Gradients of the KL Divergence along Pushforwards

First we prove a lemma that lets us move a pushforward from one side of the KL to the other. Here, we use measure-theoretic techniques to obtain a quite general statement that is applicable beyond the Lebesgue density setting. A special case of this claim for the Lebesuge setting appears in [1] using a direct argument via the change-of-variables formula for densities. Note that I don't pin down the exact conditions on $T$ under which the lemma holds (as it is apparently rather delicate), but by "sufficiently nice" I mean that all densities appearing in the proof exist. 

<div class='lemma' name='KL Adjoints'>
Suppose $T: U \to U$ is invertbile and that $p, q$ are two probability measures on $U$. If $T, p, q$ are sufficiently nice such that all measures and their transformations along $T, T^{-1}$ are absolutely continuous, then 

\[
\mathsf{KL}[T_{\#} q \mid\mid p ] = \mathsf{KL}[q \mid \mid T^{-1}_{\#} p].
\]
</div>
<details class='proof'>
<summary> Proof.</summary>
We first claim that

\[
\frac{\d T_{\#} p }{\d p}(x) = \frac{\d p}{\d T^{-1}_{\#} p}(T^{-1}(x)). \tag{1}
\]

for $p$-a.e. $x$. Indeed, by basic properties of the Radon-Nikodym derivative, we have for a measurable set $A \subseteq U$ that
\[
\begin{aligned}
T_{\#} p(A) &= p(T^{-1}(A)) = \int_{T^{-1}(A)} \d p(x) \\
&= \int_{T^{-1}(A)} \frac{\d p}{\d T^{-1}_{\#} p}(x) \d T^{-1}_{\#} p(x) \\
&= \int_A \frac{\d p}{\d T_{\#}^{-1}p}\left( T^{-1}(x) \right) \d p(x)
\end{aligned}
\]

which shows the claim due the the $p$-a.e. uniqueness of the Radon-Nikodym derivative.

Similarly, we see by a similar argument that for $p$-a.e. $x$,
\[
\frac{\d T_{\#} q}{\d T_{\#} p} (x) = \frac{\d q}{\d p} (T^{-1}(x)). \tag{2}
\]

Indeed, for any $A \subseteq U$ measurable,
\[
\begin{aligned}
T_{\#} q(A) &= \int_{T^{-1}(A)} \d q = \int_{T^{-1}(A)} \frac{\d q}{\d p}(x) \d p(x) \\
&= \int_A \frac{\d q}{\d p}(T^{-1}(x)) \d T_{\#} p (x).
\end{aligned}
\]

Combining these identities yields
\[
\begin{aligned}
\mathsf{KL}[T_{\#}q \mid\mid p] &= \int \log \left( \frac{\d T_{\#} q}{\d p}(x) \right) \d T_{\#} q(x) \\
&= \int \log \left( \frac{\d T_{\#} q}{\d T_{\#} p}(x) \frac{\d T_{\#} p}{\d p}(x) \right) \d T_{\#} q(x) \\
&= \int \log \left( \frac{\d q}{\d p}(T^{-1}(x)) \frac{\d T_{\#} p}{\d p}(x) \right) \d T_{\#} q(x) \qquad \text{(Eqn. (2))} \\
&= \int \log \left( \frac{\d q}{\d p}(T^{-1}(x)) \frac{\d p}{\d T^{-1}_{\#} p}(T^{-1}(x)) \right) \d T_{\#} q(x) \qquad \text{(Eqn. (1))} \\
&= \int \log \left( \frac{\d q}{\d p}(x) \frac{\d p}{\d T^{-1}_{\#}p}(x) \right) \d q(x) \\
&= \mathsf{KL}[q \mid \mid T^{-1}_{\#} p].
\end{aligned}
\]

This completes the proof.

</details>

Let's now return to the Euclidean setting and suppose everything admits Lebesgue densities. Suppose that $T_\epsilon: U \to U$ is a collection of invertible maps parametrized by $\epsilon \in \R$. For a given density $q$, we can construct a path of densities $q_\epsilon = T_{\\#} q$ where $\epsilon$ is playing the role of a time variable. We can compute directly the rate-of-change in KL divergence along this path, with respect to some fixed reference measure $p$.

<div class='proposition'>
Suppose $T_\epsilon: U \to U$ is a collection of sufficiently smooth, invertible mappings. Then,
\[
\frac{\d }{\d \epsilon} \mathsf{KL} \left[ q_\epsilon \mid\mid p \right] = - \E_{x \sim q} \left[ \langle s_p(T_\epsilon(x)), \frac{\d}{\d \epsilon} T_\epsilon(x) \rangle + \text{tr} \left( (DT_\epsilon(x))^{-1} \cdot \frac{\d}{\d \epsilon} DT_\epsilon(x) \right)  \right]
\]

where $s_p(x) = \nabla \log p(x)$ is the score of $p$, $D T_\epsilon$ is the spatial Jacobian of $T_\epsilon$, and $q_\epsilon = [T_\epsilon]_{\#} q$.
</div>
<details class='proof'>
<summary> Proof. </summary>
Our strategy is to use Lemma 1 to push the $\epsilon$ into the second argument of the KL divergence, followed by a straightforward calculation aided by the Jacobi formula for the derivative of a determinant. To that end,

\[
\begin{aligned}
\frac{\d }{\d \epsilon} \mathsf{KL}[q_\epsilon \mid \mid p ] &= \frac{\d }{\d \epsilon} \mathsf{KL}[q \mid \mid T_{\epsilon \#}^{-1} p] \\
&= - \frac{\d }{\d \epsilon} \int \log(T_{\epsilon \#}^{-1} p) \d q \\
&= - \frac{\d }{\d \epsilon} \int \log \left(p(T_\epsilon(x) | DT_\epsilon(x)| \right) \d q \\
&= - \E_{x \sim q} \left[ \langle s_p(T_\epsilon(x)), \frac{\d}{\d \epsilon} T_\epsilon(x) \rangle + \text{tr} \left( (DT_\epsilon(x))^{-1} \cdot \frac{\d}{\d \epsilon} DT_\epsilon(x) \right)  \right]
\end{aligned}
\]

where the last line follows by differentiating the integrand via Jacobi's rule.
</details>

Suppose now that $T_\epsilon = I + \epsilon \phi$ for some $\phi: U \to U$. Recall that under such a map, $q\_\epsilon = \[T\_\epsilon\]\_{\\#} q$ can be viewed as the exponential mapping at $q$ along the tangent (vector field) $\phi$ in the Wasserstein space. This choice is motivated by ensuring that $T_\epsilon$ is invertible, at least for small $\epsilon$. As a special case of Proposition 1, we see that at $\epsilon = 0$ we have
\\[
\begin{aligned}
\frac{\d}{\d \epsilon} \Bigg|_{\epsilon=0} \mathsf{KL}\[ (I + \epsilon \phi)\_{\\#} q \mid \mid p \] &= - \E\_{x \sim q} \[ \langle s_p, \phi \rangle + \text{div}(\phi) \] \\\\\\
&= - \E\_{x \sim q} \left\[ \text{tr}(\mathcal{A}\_p \phi) \right\] \\\\\\
&= - \E\_{x \sim q} \[ \langle s_q(x) - s_p(x), \phi(x) \rangle \] \\\\\\
&= \E\_{x \sim q} \left\[\langle \nabla\_{W\_2} F(q), \phi \rangle  \right\]
\end{aligned}
\\]

where the second and third equalities follow from calculations relating to the Stein operator shown in a previous note, and the last equality follows from plugging in the Wasserstein gradient of the KL functional $F: q \mapsto \mathsf{KL}\[q \mid \mid p \]$. 

This is quite remarkable and worth staring at for a while. Geometrically, this is reminiscent of a directional derivative, where $\phi$ plays the role of a direction. The precise connection with the Stein operator is yet unclear to me at this stage, but it seems that the Wasserstein gradient of the KL is in some sense a Riesz representation of the Stein operator.

## Stein Variational Gradient Descent

Recall that upon choosing a suitable kernel $k: U \times U \to U$, the kernelized Stein disrepancy (KSD) is 

\\[
S\_k^{1/2}(q, p) = \max \left\\{ \E\_{x \sim q} \[ \text{tr}(\mathcal{A}\_p \phi) )\] : \norm{\phi}\_{\mathcal{H}^2} \leq 1 \right\\}
\\]

which can be expicitly solved for, yielding
\\[
\phi = \frac\{\phi^*\_{q,p} \}\{ \norm{\phi^\*\_{q,p}}\_{\mathcal{H}^d} \} \qquad \phi^\*\_{q,p}(\cdot) = \E_{x \sim q} \[ \mathcal{A}\_p k_x(\cdot) \] = \E\_{x \sim q} \[k\_x(\cdot) s\_p(x) + \nabla\_x k\_x (\cdot) \]
\\]

and moreover $S\_k(q, p) = \norm{\phi^\*\_{q,p}}\_{\mathcal{H}^d}^2$. Hence, upon rescaling, it follows that $\phi^\*\_{q,p}$ is the direction in the ball $B = \\{ \norm{\phi}^2\_{\mathcal{H}^d} \leq S_k(q,p) \\}$ which has the steepest descent for the KL functional. Moreover, upon this choice, the (negative) KSD gives the value of this slope, i.e.
\\[
\frac{\d}{\d \epsilon} \Bigg|\_{\epsilon = 0} \mathsf{KL}\[ (I + \epsilon \phi^\*\_{q,p})\_{\\#} q \mid \mid p \]= - S_k(q, p).
\\]

### An Algorithm

This suggests an iterative procedure, which is essentially a time-discretized gradient descent on the KL functional. Given some fixed initial distribution $q_0$, we iteratively define

\\[
q_k = \[T\_k\]\_{\\#} q\_{k-1} \qquad T\_k = x + \epsilon\_k \phi^{\*}_{q\_{k-1},p}(x).
\\]

It is intuitively clear that for sufficiently small step sizes $\epsilon\_k$, this will monotonically decrease the KL divergenece, and given that the KL function has a unique minimizer, we thus obtain a procedure for iterating $q_0$ towards $p$. The magic here is that these updates are available in *closed form* due to our choice of working in an RKHS!

## Links

Links:
- https://arxiv.org/pdf/1506.03039
- https://arxiv.org/pdf/1608.04471
- https://proceedings.neurips.cc/paper_files/paper/2020/file/16f8e136ee5693823268874e58795216-Paper.pdf
- https://danmackinlay.name/notebook/stein_vgd.html
- https://www.depthfirstlearning.com/2020/SVGD
- https://www.cs.utexas.edu/~lqiang/stein.html
- https://arxiv.org/abs/1807.01750
- https://projecteuclid.org/journals/statistical-science/volume-38/issue-1/Steins-Method-Meets-Computational-Statistics--A-Review-of-Some/10.1214/22-STS863.full
- https://arxiv.org/abs/2105.09994#

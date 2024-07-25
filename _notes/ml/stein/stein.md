---
title: "Stein Operators and Stein Disrepancies"
topic: "Machine Learning"
chapter: "Stein Methods"
section: "stein"
layout: note
permalink: "/notes/ml/stein/stein/"

subtitle: 
date: 2024-07-24
keywords: analysis, optimal transport, gradient flows
published: true
references: "Liu, Q., Lee, J. Jordan, M. (2016). A kernelized Stein discrepancy for goodness-of-fit tests. ICML.; Hyvarinen, A. (2005). Estimation of non-normalized statistical models by score matching. Journal of Machine Learning Research 6.4.; Song, Y., Ermon., S. (2019). Generative modeling by estimating gradients of the data distribution. NeurIPS.; Liu, Q. (2014). A short introduction to kernelized Stein discrepancy. https://www.cs.utexas.edu/~lqiang/PDF/ksd_short.pdf; Chwialkowski, K. Strathmann, H. Gretton, A. (2016). A kernel test of goodness of fit. ICML."
---

In this note we study Stein operators and Stein discrepancies, with a particular focus on kernelized Stein discrepancies. The Stein operator associated with a density $p$ can be seen as a kind of stochastic integration by parts, and the Stein discrepancy can be seen as a tool for comparing two measures via their scores in a weak sense. The Stein discrepancy can be understood variationally, and choosing the space of variations to be an RKHS leads to the kernelized Stein discrepancy. This is particularly useful when we have samples from one density $q$ and access to an unnormalized model $p$, and we would like to compare these distributions e.g. for a goodness-of-fit. Lastly, we will emphasize some connections with score matching.

## Stein Operators

Let $U \subseteq \R^d$ be open and suppose $p \in C^1(U)$ is a smooth probability density. The _Stein operator_ $\mathcal{A}_p$ associated with $p$ acts on sufficiently regular test functions $\varphi: U \to \R$ via

\\[
\[\mathcal{A}_p \varphi\](x) = \varphi(x) \nabla_x \log p(x) + \nabla_x \varphi(x).
\\]

The quantity $\nabla_x \log p(x)$ is called the Stein score of $p$. Observe that $\mathcal{A}_p$ is linear, and that $\mathcal{A}_p f: U \to \R^d$ is vector-valued.

To motivate this definition a little, we are interested in studying the density $p$ through test functions. However, in practice we typically only know $p$ up to a multiplicative constant. A standard trick to handle this is to take a gradient, which will kill the constant. To that end, note that 

\\[
\begin{aligned}
\nabla_x (\varphi p) &= (\nabla_x \varphi) p + \varphi (\nabla_x p) \\\\\\
&= \left\[ \nabla_x \varphi + \varphi \nabla_x \log p\right\] p \\\\\\
&= \[ \mathcal{A}_p \varphi \] p
\end{aligned}
\\]

where we've pulled out a factor of $p$ so that, upon integration, we obtain

\\[
\E_{x \sim p} \[ \mathcal{A}_p \varphi \] = \int \nabla_x(\varphi p) \d x. \tag{1}
\\]

We say that $\varphi \in \mathsf{Stein}(p)$ is in the _Stein class_ of $p$ if the quantity (1) is zero, and _Stein's Identity_ states that

\\[
\E_{x \sim p} \[ \mathcal{A}_p \varphi \] = 0
\\]

for $\varphi$ in the Stein class of $p$. Stein's identity is an easy application of integration by parts, where we impose additional boundary conditions on $\varphi$ depending on the geometry of $U$. For instance, if $U$ is bounded then we need to impose that $\varphi p$ vanishes on $\partial U$, or if $U = \R^d$ we need that $\varphi p$ vanishes at infinity. 


We may extend this notion slightly and consider vector-valued $\varphi: U \to \R^{d'}$, where we say that $\varphi \in \mathsf{Stein}(p)$ if (1) is satisfied for each component of $\varphi$, and Stein's operator applied to $\varphi$ yields $\mathcal{A}_p \varphi: U \to \R^{d \times d'}$ via

\\[
\[\mathcal{A}_p \varphi\](x) =  \nabla_x \log p(x) \varphi(x)^T + D \varphi(x)
\\]

where $D \varphi (x) = (\partial_i \varphi^j)$ is the Jacobian of $\varphi$. Note that this is a matrix whose $j$th column is the Stein operator applied to the $j$th component of $f$, and so this extension is natural. This is the convention followed in [1], but some authors use the transpose of this.


## Stein Discrepancies

The Stein operator is useful in the sense that it characterizes the distribution $p$. That is, if $q \in C^1(U)$ is a density $q \neq p$, there exists a test function $\varphi: U \to \R^{d'}$ such that $\E_{x \sim q}\[A_p \varphi\] \neq 0$. Indeed, if $\varphi \in \mathsf{Stein}(q)$, then

\\[
\begin{aligned}
\E_{x \sim q} \[ \mathcal{A}\_p \varphi \] &= \E_{x \sim q} \[ \mathcal{A}\_p \varphi \] - \E_{x \sim q} \[ \mathcal{A}\_q \varphi \] \\\\\\
&= \E_{x \sim q} \[ (\nabla \log q - \nabla \log p) \varphi^T  \]
\end{aligned} \tag{2}
\\]

which can be made nonzero as long as $p \neq q$. This highlights that the Stein operator allows us to compare two distributions via their scores, in a weak sense. This may be viewed as simultaneously testing all components of the scores against a collection of test functions.

Note further that when $\varphi: U \to \R^d$, we have the identities

\\[
\text{tr}(\mathcal{A}_p \varphi) = \langle \varphi, \nabla \log p \rangle + \text{div}(\varphi)
\\]
\\[
\E\_{x \sim q}\[ \text{tr}(\mathcal{A}\_p \varphi)\] = \E\_{x \sim q} \[ \langle \nabla \log q - \nabla \log p, \varphi \rangle \] = \langle \nabla \log q - \nabla \log p, \varphi \rangle\_{L^2(\d q)}
\\]

where the first line is immediate and the second follows directly from (2). The apperance of a divergence term suggests that a PDE is lurking somewhere in the background. 

It is then natural to consider the $\varphi$ which maximizes (2) as a notion of discrepancy between $p$ and $q$. To that end, for a fixed class of test functions $\mathcal{F}$, we may obtain the _Stein discrepancy_ via

\\[
S^{1/2}(q, p) = \max\_{\varphi \in \mathcal{F}} \E_{x \sim q} \[ \text{tr} (\mathcal{A}\_p \varphi) \]. \tag{3}
\\]

The power of $1/2$ is conventional, and the trace is used to obtain a scalar quantity. This quantity depends crucially on the choice of $\mathcal{F}$, and is analogous to the usual operator norm. Here, there is a tradeoff between expressivity (i.e. large $\mathcal{F}$) and tractability (i.e. small $\mathcal{F}$). Note further that $S(q, p)$ is something we can compute (or at least estimate) provided we have samples from $q$ and that we know $p$ up to a multiplicative constant -- and this is precisely the scenario we often find ourselves in when performing inference.

### Kernelized Stein Discrepancies

When $\mathcal{F}$ is complex, solving the optimization in (3) is non-trivial, limiting practical applications. The key observation is that $\mathcal{A}\_p$ is linear, enabling us to easily perform computations in a fixed basis for $\mathcal{F}$. 


#### One-Dimensional Case
To fix the ideas we can first consider only $U \subseteq \R$ and scalar-valued $\varphi: U \to \R$. If we express $\varphi = \sum_k \alpha_k e_k$ in some fixed and known basis $(e\_k)$, we see that

\\[
\E\_{x \sim q}\[ \mathcal{A}\_p \varphi \] = \sum_k \alpha_k \E\_{x \sim q} \[  \mathcal{A}\_p e_k \] =: \sum_k \alpha_k \beta_k. \tag{4}
\\]

Since we are working over $\R$, the trace is no longer necessary as $\mathcal{A}\_p \varphi: U \to \R$ is scalar valued. Thus, the optimization in (3) amounts to optimizing over $\alpha = (\alpha_k)$, which is a linear problem in $\alpha$. Note that (as in an operator norm) we typically consider $\lvert \alpha \rvert \leq 1$ so that the quantity (3) is finite. For instance, if we use the $\ell^2$ norm, then $\alpha = \beta / \lvert \beta \rvert$ gives us the explicit solution to (3), at least when $\mathcal{F}$ is finite dimensional.

However, to increase the power of the method, we'd like to be able to use infinte-dimensional $\mathcal{F}$'s. A convenient and computationally friendly choice will be to use the RKHS $\mathcal{H}$ associated with a positive definite kernel $k: U \times U \to \R$. Recall that, given such a $k$, the RKHS $\mathcal{H}$ is the closure of the linear span of the kernels, i.e. every $\varphi \in \mathcal{H}$ can be written as a countable sum $\varphi = \sum_i \alpha_i k(x_i, \cdot)$ for some $\alpha_i \in \R, x_i \in U$. <a href="https://thomaszh3.github.io/writeups/RKHS.pdf">These notes</a> are a nice refresher. Rceall that for $f \in \mathcal{H}$,

\\[
f(x) = \langle f, k_x \rangle\_{\mathcal{H}} \qquad \nabla_x f(x) = \langle f, \nabla_x k_x \rangle\_{\mathcal{H}}
\\]

where $k_x: U \to \R$ is given by $x' \mapsto k(x, x')$. As a consequence,

\\[
\begin{aligned}
\E\_{x \sim q} \[ \mathcal{A}\_p \varphi \] &= \E\_{x \sim q} \[ \varphi(x) \nabla\_x \log p(x) + \nabla\_x \varphi(x) \] \\\\\\
&= \E\_{x \sim q} \[ \langle \varphi, k\_x \nabla\_x \log p(x) + \nabla\_x k\_x \rangle\_{\mathcal{H}} \] \\\\\\
&= \langle \varphi, \E\_{x \sim q} \left\[ \mathcal{A}\_p k\_x \right\] \rangle\_{\mathcal{H}}.
\end{aligned}
\\]

This a restatement of (4) using the machinery of our RKHS. In particular, if we define

\\[
\beta\_{q, p}: U \to \R \qquad x' \mapsto \beta\_{q, p}(x') = \E\_{x \sim q} \[\mathcal{A}^{x'}\_p k_{x}(x') \]
\\]

then it is easy to see that maximizing (4) over the unit ball of the RKHS results in $\varphi = \beta_{q,p} / \norm{\beta_{q,p}}_{\mathcal{H}}$, so that $S(q, p) = \norm{\beta\_{q,p}}\_{\mathcal{H}}^2$. In fact, we have that

\\[
S(q, p) = \E\_{x, x' \sim q} \[ \kappa\_p(x, x') \] \qquad \kappa_p(x, x') = \mathcal{A}\_p^x  \mathcal{A}\_p^{x'} k(x, x').
\\]

where $\kappa_p(x, x')$ is the "Steinalized" kernel. This is really a statement about the adjoint of $\mathcal{A}\_p$ -- namely, this operator is self-adjoint, as a short calculation in a basis will show. It follows (at least formally) that
\\[
\begin{aligned}
S(q, p) &= \langle \beta\_{q, p}, \beta\_{q, p} \rangle\_{\mathcal{H}} = \E\_{x, x' \sim q} \langle \mathcal{A}\_p^x k_{x'}, \mathcal{A}\_p^{x'} k\_x \rangle\_{\mathcal{H}} \\\\\\
&= \langle k\_{x'}, \mathcal{A}\_p^x \mathcal{A}\_{p}^{x'} k_{x'} \rangle\_{\mathcal{H}} = \kappa\_p(x, x').
\end{aligned}
\\] 

Observe that $\kappa_p$ can be computed without knowledge of the normalizing constant of $p$.

#### The General Case

Now that we understand the easiest case, it is just a matter of carefully tensorizing to obtain the result for general $U \subseteq \R^d$ and $\varphi: \R^d \to \R^{d'}$. We will skip the detailed proofs here -- see [1] for the details. To that end, for a given positive definite kernel $k: U \times U \to \R$ let $\mathcal{H}^d$ be the space of functions $\varphi: U \to \R^d$ whose components are in the RKHS $\mathcal{H}$ associated to $k$. Define the _kernelized Stein discrepancy_ as
\\[
S^{1/2}\_k(q, p) = \max\_{ \norm{\varphi}\_{\mathcal{H}^d} \leq 1 } \left\\{ \E\_{x \sim q} \[ \text{tr} \left( \mathcal{A}\_p \varphi \right) \] \right\\}
\\]

i.e. we are maximizing the Stein discrepancy (3) over the unit ball in the RKHS $\mathcal{H}^d$. For this to make sense, note that we require that $k \in C^2(U \times U)$ and that $k\_x \in \mathsf{Stein}(q)$ for any fixed $x \in U$. As we saw previously, this optimization problem can be solved explicitly via

\\[
\beta\_{q,p}(x') = \E\_{x \sim q} \[ \mathcal{A}\_p^x k\_{x'} (x) \] \qquad \varphi^* = \beta\_{q,p} / \norm{\beta\_{q, p}}\_{\mathcal{H}^d}
\\]

which allows us to equivalently express the kernelized Stein discrepancy as

\\[
S(q, p) = \norm{\beta\_{q, p}}^2\_{\mathcal{H}^d} = \E\_{x, x' \sim q} \[ \kappa\_p(x, x') \] \tag{5}
\\]
\\[
\qquad \kappa\_p(x, x') = \text{tr}\left( \mathcal{A}\_p^x \mathcal{A}\_p^{x'} k(x, x') \right)
\\]
 
where the Steinalized kernel $\kappa\_p$ is given in its full ugly glory as
\\[
\kappa_p(x, x') = s\_p(x)^T k(x, x') s\_p(x') + s\_p(x)^T \nabla\_{x'} k(x, x') + \nabla\_x k(x, x')^T s\_p(x') + \text{tr} (D k(x, x'))
\\]

where $s_p(x) = \nabla_x \log p(x)$. Interestingly, it may be shown through an application of (2) that
\\[
S_k(q, p) = \E\_{x, x' \sim q} \[ \delta\_{q,p}(x)^T k(x, x') \delta\_{q, p}(x') \] \tag{6}
\\]

where $\delta\_{q,p}(x) = \nabla \log q(x) - \nabla \log p(x)$. This highlights the fact that the kernelized Stein discrepancy is measuring a kernel-weighted comparison of the scores. However, this form requires knowing the score for $q$, and in practice we often only have samples from $q$.

## Relationship with Score Matching

Looking at the form of the KSD, it is clear that it bears some relation to the Fisher divergence 

\\[
F(q, p) = \E\_{x \sim q} \[ \norm{s\_p(x) - s\_q(x)}\_{2}^2 \] = \norm{s_q - s_p}\_{L^2(\d q)}^2.
\\]

In fact, taking $k(x, x') = \delta[x = x']$ in (5) shows that $F(q, p)$ is a special case of the KSD. However, two applications of Cauchy-Schwarz show that
\\[
S^2\_k(q, p) \leq \E\_{x, x' \sim q} \[ k^2(x, x') \] F^2(q, p)
\\] 

and so the Fisher divergence is in general stronger than the KSD in general. Moreover, as the corresponding kernel $k$ for $F$ is not smooth, the Fisher divergence does not enjoy the computationally friendly representation (5). Interestingly, an alternative way to see that $F$ is stronger is to observe that the Fisher divergence can be represented variationally by minimizing (3) over the unit ball of $L^2(\R^d, \d q)$.

Unsurprisingly, the KSD is connected to score-matching techniques. Indeed, a direct argument through integration by parts [2, 3] shows 
\\[
\begin{aligned}
F(q, p) &= \E\_{x \sim q} \[ \norm{s\_q}^2 - 2 \langle s\_p, s\_q \rangle + \norm{s\_p}^2 \] \\\\\\
&= \E\_{x \sim q} \[ \norm{s\_q}^2 + 2 \text{div}(s_p) + \norm{s\_p}^2 \]
\end{aligned}
\\]

which, upon dropping the term $\norm{s\_q}^2$, is the classic score-matching loss used to fit the density $p$ to data samples from $q$. On the other hand, applying Stein's identity yields
\\[
0 = \E\_{x \sim q} \[ \text{tr}(A\_q s\_p) \] \implies \E\_{x \sim q} \[ - \langle s\_p, s\_q \rangle \] = \E\_{x \sim q} \[ \text{div}(s\_p) \].
\\]

While nothing new has happened (as Stein's identity is really an integration by parts), this computation shows how one can use Stein's identity to kill an unknown score function.

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

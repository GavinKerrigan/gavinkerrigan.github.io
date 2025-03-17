---
title: "The Fisher Information Matrix"
topic: "Machine Learning"
chapter: "Information Geometry"
section: "information_geometry"
layout: note
permalink: "/notes/ml/information_geometry/fim/"

subtitle: 
date: 2025-03-17
keywords: information geometry, fisher information
published: false
references: "Liu, Q., Lee, J. Jordan, M. (2016). A kernelized Stein discrepancy for goodness-of-fit tests. ICML.; Hyvarinen, A. (2005). Estimation of non-normalized statistical models by score matching. Journal of Machine Learning Research 6.4.; Song, Y., Ermon., S. (2019). Generative modeling by estimating gradients of the data distribution. NeurIPS.; Liu, Q. (2014). A short introduction to kernelized Stein discrepancy. https://www.cs.utexas.edu/~lqiang/PDF/ksd_short.pdf; Chwialkowski, K. Strathmann, H. Gretton, A. (2016). A kernel test of goodness of fit. ICML."
---

We introduce the Fisher information matrix and study some of its basic interpretations and properties. One of the most interesting aspects of the Fisher information is that it is kaleidoscopic in nature, admitting a wide variety of perspectives. 

The geometric setting here is that of *statistical manifolds* -- that is, manifolds whose points are probability measures over some fixed, shared measurable space. The space of all such measures is, of course, infinite dimensional, and so we often will instead restrict our attention to some fixed-dimensional subspace. 

## Fisher Geometry

Rather than setting all of the geometric details up properly, we will just assume that we are working on some sufficiently regular manifold $\mathcal{M}$ with global coordinates $\theta = (\theta_1, \dots, \theta_n)$. We think of a point $\theta \in \mathcal{M}$ as corresponding to some probability distribution $p(x \mid \theta)$ defined over a state space (either discrete or continuous) $x \in \mathcal{X}$. That is, each $\theta$ gives rise to a *likelihood* in some specified fashion.

<div class='definition' name='Fisher Information Matrix'>
Given a manifold $\mathcal{M}$ of parameters and a choice of likelihoods $\theta \mapsto p(\cdot \mid \theta)$, the Fisher information matrix (FIM) is defined as

\[
\mathcal{I}(\theta) = \E_{p(x \mid \theta)} \left[ \nabla_\theta \log p(x \mid \theta) \otimes \nabla_\theta \log p(x \mid \theta) \right].
\]
</div>

The FIM $\mathcal{I}(\theta)$ is an $n \times n$ matrix, where $(\mathcal{I}(\theta))\_{ij} = \E\_{p(x \mid \theta)}\left\[ \partial_i \log p(x \mid \theta) \partial_j \log p(x \mid \theta) \right\]$. When $\theta$ is one-dimensional, we have $\mathcal{I}(\theta) = \E\_{p(x \mid \theta)}\left\[ (\partial_\theta \log p(x \mid \theta))^2 \right\]$, from which it is easy to see that $I(\theta) \geq 0$.

We can view $\nabla_\theta \log p(x \mid \theta)$ as the "sensitivity" of the likelihood with respect to the parameters, which we average over data $x \sim p(x \mid \theta)$ to obtain the FIM. If this is large, then the data $x$ is informative about $\theta$ (in a maximum likelihood sense), as small changes in $\theta$ lead to large changes in the likelihood. 


### The FIM as the Variance of the Score

For our first interpretation, we note that the FIM can be seen as the covariance matrix of the (Fisher) score $\nabla_\theta \log p(x \mid \theta)$. This is because the mean score is zero, i.e.,

\\[
\E_{p(x \mid \theta)}\left[\nabla_\theta \log p(x \mid \theta) \right] = \nabla_\theta \int p(x \mid \theta) dx = 0.
\\]

---
title: "Covariance Operators"
topic: "Analysis"
chapter: "Gaussian Measures"
section: "covariance"
layout: note
permalink: "/notes/analysis/gaussian_measures/covariance/"

subtitle: 
date: 2025-04-07
keywords: gaussian measures, hilbert spaces, pettis integrals, bochner integrals
published: false
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 3."
---

In this note we study covariance operators in infinite-dimensional spaces. Throughout, $H$ will be a separable Hilbert space equipped with its Borel $\sigma$-algebra. We will use $L(H)$ to represent the set of bounded linear operators on $H$. It is clear that everything can be stated in terms of either random elements on $H$ or their corresponding (Borel) probability measures on $H$, and we will switch between these views when convenient.

<div class='definition' name='Covariance Operator'>
Let $H$ be a separable Hilbert space and suppose $\xi$ is a random element on $H$. An operator $C \in L(H)$ is called the covariance operator of $\xi$ if

\[
\langle C h_1, h_2 \rangle = \E \langle \xi, h_1 \rangle \langle \xi, h_2 \rangle \qquad \forall h_1, h_2 \in H.
\]

If $\xi$ admits a (weak or strong) mean $m$, then an element $S \in L(H)$ is called the correlation (or centered covariance) operator of $\xi$ if

\[
\langle S h_1, h_2 \rangle = \E \langle \xi - m, h_1 \rangle \langle \xi - m, h_2 \rangle \qquad \forall h_1, h_2 \in H.
\]
</div>

It is easy enough to check that when $\xi$ admits a mean $m$, the existence of a covariance operator is equivalent to the existence of a correlation operator, and the two are related by
\\[
\langle Sh_1, h_2 \rangle = \langle Ch_1, h_2 \rangle - \langle m, h_1 \rangle \langle m, h_2 \rangle
\\]
\\[
S = C - |m|^2 P_{[m]} \qquad P_{[m]}(x) = \frac{\langle x, m \rangle}{|m|^2} m
\\]

where $P_{[m]}: H \to H$ is the projection onto the span of $m$.

The following proposition is also immediate.
<div class='proposition'>
Let $C$ (resp. $S$) be the covariance (resp. correlation) operator of a random element $\xi$ on $H$. Then, $C$ (resp. $S$) is positive and self-adjoint.
</div>
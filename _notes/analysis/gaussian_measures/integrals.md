---
title: "Pettis and Bochner Integrals"
topic: "Analysis"
chapter: "Gaussian Measures"
section: "integrals"
layout: note
permalink: "/notes/analysis/gaussian_measures/integrals/"

subtitle: 
date: 2025-03-28
keywords: gaussian measures, hilbert spaces, pettis integrals, bochner integrals
published: false
references: "Jordan, R., Kinderlehrer, D., & Otto, F. (1998). The variational formulation of the Fokker--Planck equation. SIAM journal on mathematical analysis, 29(1), 1-17.; Hamfeldt, B. (2019) Gradient flows in the Wasserstein metric. https://www.youtube.com/watch?v=zzGBxAqJV0Q"
---

Let $H$ be a separable, real Hilbert space and suppose $\mu$ is a Borel probability measure on $H$. Recall that we say $m f
\in H$ is the mean of the measure $\mu$ if

\\[
\langle m, h \rangle = \int \langle x, h \rangle d \mu(x) \qquad \forall h \in H.
\\]

The key thing to observe here is that this is defined through an integral over the real-valued function $\langle h, \cdot \rangle: H \to \R$, which can be thus understood as your run-of-the-mill Lebesgue integral. In this note, we will see that this can be understood as a kind of weak (or *Pettis*) integral of the measure $\mu$ (or its associated random variable). In particular, weak integrals are defined through functionals, i.e., through $f_h \in H^*$ given by $f_h: x \mapsto \langle x, h \rangle$. 

 On the other hand, we would also like to somehow understand $m$ more directly, i.e., we would hope to have that $m$ coincides with $\int x d \mu(x)$. This integral is now over an $H$-valued function and thus must be properly understood. This will give rise to the notion of the strong (or *Bochner*) integral of $\mu$. At least formally, we should hope that Bochner integrals commute with inner products for the two notions to coincide. That is, we hope to be justified in writing

 \\[
\langle m, h \rangle = \int \langle x, h \rangle d \mu(x) = \langle \int x d \mu(x), h \rangle.
 \\]


### The Pettis Integral

We proceed to define the weak (*Pettis*) integral in the general setting. Suppose $(\Omega, \mathcal{F}, \P)$ is a probability space and $X$ is a normed vector space. Let $\xi: \Omega \to X$ be a random element.

<div class='definition'>
We say that $\xi$ has finite weak first moment if for every bounded linear functional $x^* \in X^*$,

\[
\E \left[ \langle x^*, \xi \rangle \right] = \int \langle x^*, x \rangle d \P(x) < \infty
\]
where $\langle \cdot, \cdot \rangle$ represents the dual pairing $X^* \times X \to \R$.
</div>
 

 <div class='definition' name='Pettis Integral'>
Suppose $\xi$ has finite weak first moment. If there exists an element $m \in X$ such that for any $x^* \in X$ we have
\[
\E\left[ \langle x^*, \xi \rangle \right] = \langle x^*, m \rangle,
\]

then we say that $m$ is the weak (or Pettis) integral of $\xi$.
</div>

These notions can clearly be re-stated in terms of the corresponding probability measure $\mu_\xi$ on $X$ associated to $\xi$. When such an element exists, we often write $m = \E[\xi] = \int \xi(\omega) d \P(\omega)$, although this is an abuse of notation and some care must be taken. 
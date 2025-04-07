---
title: "Pettis and Bochner Integrals"
topic: "Analysis"
chapter: "Measure Theory"
section: "integrals"
layout: note
permalink: "/notes/analysis/measure/integrals/"

subtitle: 
date: 2025-04-07
keywords: gaussian measures, hilbert spaces, pettis integrals, bochner integrals
published: true
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 3."
---

Let $H$ be a separable, real Hilbert space and suppose $\mu$ is a Borel probability measure on $H$. Recall that we say $m
\in H$ is the mean of the measure $\mu$ if

\\[
\langle m, h \rangle = \int \langle x, h \rangle d \mu(x) \qquad \forall h \in H.
\\]

The key thing to observe here is that this is defined through an integral over the real-valued function $\langle h, \cdot \rangle: H \to \R$, which can be thus understood as your run-of-the-mill Lebesgue integral. In this note, we will see that this can be understood as a kind of weak (or *Pettis*) integral of the measure $\mu$ (or its associated random variable). In particular, weak integrals are defined through functionals, i.e., through $f_h \in H^*$ given by $f_h: x \mapsto \langle x, h \rangle$. 

 On the other hand, we would also like to somehow understand $m$ more directly, i.e., we would hope to have that $m$ coincides with $\int x d \mu(x)$. This integral is now over an $H$-valued function and thus must be properly understood. This will give rise to the notion of the strong (or *Bochner*) integral of $\mu$. At least formally, we should hope that Bochner integrals commute with inner products for the two notions to coincide. That is, we hope to be justified in writing

 \\[
\langle m, h \rangle = \int \langle x, h \rangle d \mu(x) = \left\langle \int x d \mu(x), h \right\rangle.
 \\]



## The Pettis Integral

We proceed to define the weak (*Pettis*) integral in the general setting. Suppose $(\Omega, \mathcal{F}, \P)$ is a probability space and $X$ is a normed vector space. Let $\xi: \Omega \to X$ be a random element.

<div class='definition'>
We say that $\xi$ has finite weak first moment if for every bounded linear functional $x^* \in X^*$,

\[
\E \left[ \langle x^*, \xi \rangle \right] = \int \langle x^*, \xi(\omega) \rangle d \P(\omega) < \infty
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

The following result gives the existence of weak integrals as long as $X$ is reflexive and $\xi$ has finite strong fist moment.

<div class='proposition' name='Existence of Pettis Integral'>
Suppose $\E|\xi| < \infty$ and $X$ is reflexive. Then, $\E \xi$ exists in the weak sense.
</div>
<details>
<summary> Proof. </summary>
The mapping $M_\xi: x^* \mapsto \E \langle x^*, \xi \rangle$ is linear and bounded as $|M_\xi| \leq \E|\xi| < \infty$. As $X$ is reflexive, there exists an element $m \in X$ such that $\langle x^*, m \rangle = M_\xi(x^*) = \E \langle x^*, \xi \rangle$ for all $x^* \in X^*$.

</details>


The weak integral satisfies some basic notions (e.g., uniqueness and linearity) that we might expect.

<div class='proposition' name='Properties of the Pettis Integral'>
Suppose $\xi, \eta$ are random elements on $X$ with Pettis integrals $\E[\xi], \E[\eta]$. Then,
<ol>
	<li>
		$\E[\xi]$ is unique.
	</li>
	<li>
		We have $| \E \xi | \leq \E |\xi| $.
	</li>
	<li>
		If $\eta + \xi$ is a random variable, then $\E[\xi + \eta]$ exists and  $\E[\xi + \eta] = \E[\xi] + \E[\eta]$.
	</li>
	<li>
		If $Y$ is a normed vector space and $A: X \to Y$ is a bounded linear operator, then $\E[A \xi]$ exists and moreover, $\E[A \xi] = A \E[\xi]$. 
	</li>
</ol>

</div>
<details>
<summary> Proof. </summary>
<ol>
	<li>
		Suppose there exists $m_1 \neq m_2$ which are both Pettis integrals of $\xi$. By the Hahn-Banach theorem, $X^*$ separates points in $X$. Hence, there exists $x^* \in X^*$ with $\langle x^*, m_1 \rangle \neq \langle x^*, m_2 \rangle$. This yields a contradiction.
	</li>
	<li>
		Again by Hahn-Banach, there exists an $x^* \in X^*$ such that $|x^*| = 1$ and $\langle x^*, \E \xi \rangle = |\E \xi|$. Then, we have that
		\[
		\begin{align}
		|\E \xi| &= | \langle x^*, \E \xi \rangle | = | \E \langle x^*, \xi \rangle | \\
		&\leq \E |x^*| |\xi| = \E |\xi|.
		\end{align}
		\]
	</li>
	<li>
		The additivity is immediate from that of the Lebesgue integral.
	</li>
	<li>
		Fix $y^* \in Y^*$ and let $A^*: Y^* \to X^*$ be the adjoint of $A$. Then,
		\[
		\E \langle y^*, A \xi \rangle = \E \langle A^* y^*, \xi \rangle = \langle A^* y^*, \E \xi \rangle = \langle y^*, A \E \xi \rangle.
		\]
	</li>
</ol>
</details>


## The Bochner Integral

We now proceed to construct the strong (or Bochner) integral of a random element. This construction will mirror that of the ordinary Lebesgue integral. We will now make the stronger assumption that we are working on a Banach space $B$.

### Construction: General Case

We first construct the Bochner integral when $B$ is not assumed to be separable. We will later see that existence of a Bochner integral is greatly simplified in the separable case, though.

Recall that a random element $\eta: \Omega \to B$ is called *simple* if it takes only finitely many values. We may express a simple random variable as

\\[
\eta(\omega) = \sum_{k=1}^n c_k \mathbb{1}[\omega \in E_k]
\\]

for some $c_k \in B$ and disjoint $E_k \in \mathcal{F}$. Note further that $\|\eta(\omega)\| = \sum\_{k=1}^n \|c_k\| \mathbb{1}[\omega \in E_k]$ is a simple (scalar) random variable. 

We are now ready to define the Bochner integral. We first explicitly define its value for simple random elements, and then approximate general random elements with simple ones.

<div class='definition' name='Bochner Integral of Simple Random Elements'>
Suppose $\xi$ is a simple random element in $B$ with the form

\[
\xi = \sum_{k=1}^m b_k \mathbb{1}_{E_k}
\]


where the $E_k \in \mathcal{F}$ are disjoint. The strong (or Bochner) integral of $\xi$ is given by

\[
\E\xi = \int \xi(\omega) d \P(\omega) = \sum_{k=1}^m b_k \P(E_k).
\]
</div>

Under additional hypotheses, the Bochner integrals of a sequence of simple random elements will themselves converge.

<div class='proposition'>
Let $\xi$ be a random element in a Banach space $B$. If $(\xi_n)_{n=1}^\infty$ is a sequence of random elements such that $\E |\xi_n - \xi | \to 0$, then the sequence $(\E \xi_n)_{n=1}^\infty$ converges in $B$.
</div>
<details>
<summary> Proof. </summary>
Fix $n, m \in \Z_{> 0}$. One can readily check each of the following inequalities for simple random elements.

\[
| \E \xi_n - \E \xi_m| = |\E (\xi_n - \xi_m)| \leq \E |\xi_n - \xi_m| \leq \E|\xi_n - \xi| + \E|\xi_m - \xi|
\]

Thus, $(\E \xi_n)_{n=1}^\infty$ is Cauchy, and as $B$ is complete, convergent.
</details>

We now simply combine these constructions. Note that the limit in the following definition exists by the previous result. In particular, for the Bochner integral to be well defined, we must be able to find a sequence of simple random elements approximating $\xi$ in expectation. By essentially the same argument, one can easily show that the value of the Bochner integral does not depend on the approximating sequence.

<div class='definition' name='Bochner Integral'>
Let $\xi$ be a random element in a Banach space $B$. Suppose that there exists a sequence $(\xi_n)_{n=1}^\infty$ of simple random elements in $B$ such that $\E|\xi_n - \xi| \to 0$. Then, $\lim \E \xi_n$ is the Bochner integral of $\xi$, denoted by $\E \xi = \int \xi d \P$. 
</div>

As with the Pettis integral, one can seamlessly translate these notions into the notion of a Bochner integral for the corresponding probability measure of $\xi$. That is, the existence of a Bochner integral $m\_\mu = \int x d \mu$ for a Borel probability measure $\mu \in \P(B)$ means there exists a sequence of simple functions $p\_n: B \to B$ with $\E\_{x \sim \mu}\|p_n(x) - x\| \to 0$, and $m_\mu = \lim \int p_n d \mu$.

It is important to note that we have mirrored the construction of the Lebesgue integral, replacing scalar-valued simple functions with $B$-valued simple functions.

### The Separable Case

If we are happy to assume that $B$ is separable, then existence of a Bochner integral is equivalent to having a finite strong first moment. To show this, our strategy is to exhibit a sequence of random simple elements converging to $\xi$ almost surely via analytical techniques. 

We will write $L_0(\Omega)$ for the set of all random elements on $B$, identified if they agree up to a $\P$-null set. It is not too hard to show that $L_0(\Omega)$ is a vector space -- but note that this step requires the separability of $B$. We further equip this space with a bounded metric metrizing convergence in probability. While we are interested in almost sure convergence, this detour through convergence in probability is useful as we can extract almost surely converging subsequences from probabilistically convergent sequences.

<div class='proposition'>
Consider the function $d: L_0(\Omega) \times L_0(\Omega) \to \R$ given by

\[
d(\xi, \eta) = \E \left[ \frac{|\xi - \eta|}{1 + |\xi - \eta|} \right]. 
\]

Then, $(L_0(\Omega), d)$ is a metric space, and convergence in $d$ is equivalent to convergence in probability.
</div>
<details>
<summary> Proof. </summary>
To check the triangle inequality for $d$, use the fact that $\varphi(t) = t / (1+t)$ is monotone increasing. The other properties are straightforward.

<br><br>

If $\eta_n \to \eta$ in probability, then for every $\epsilon > 0$ we have $\P \left\{ |\eta_n - \eta| \geq \epsilon \right\} \to 0$. Hence,
\[
\begin{align}
d(\eta_n, \eta) &= \E \left[ \frac{|\eta_n - \eta|}{1 + |\eta_n - \eta|} \mathbb{1}[|\eta_n - \eta| < \epsilon] +  \frac{|\eta_n - \eta|}{1 + |\eta_n - \eta|} \mathbb{1}[|\eta_n - \eta| \geq \epsilon] \right] \\
&\leq \epsilon + \P\{ |\eta_n - \eta| \geq \epsilon \}
\end{align}
\]

which converges to $\epsilon$ by assumption, and thus $d(\eta_n, \eta) \to 0$.

<br><br>

Conversely, suppose $d(\eta_n, \eta) \to 0$. Then, since $\varphi(t) = 1 / (1 +t)$ is monotone increasing, an application of Markov's inequality yields

\[
\P \{ |\eta_n - \eta| \geq \epsilon \} \leq \frac{1 + \epsilon}{\epsilon} \, \E\left[ \frac{|\eta_n - \eta|}{1 + |\eta_n - \eta|} \right]
\]

which converges to zero by assumption.
</details>

The conceptual advantage of the previous result is that it allows us to translate probabilistic notions (i.e., convergence in probability) into analytic notions (i.e., metric convergence), affording us a set of quite useful tools. We now leverage this idea to show that any random element in $B$ can be approximated almost surely by simple random elements. 

<div class='proposition' name='Approximation by Simple Random Elements'>
Let $\xi$ be a random element in a separable Banach space $B$. Then, there exists a sequence $(\xi_n)_{n=1}^\infty$ of simple random elements such that $\xi_n \to \xi$ almost surely.

</div>
<details>
<summary> Proof. </summary>
There are essentially three steps in the proof: (1) use separability to obtain an approximation to $\xi$ taking countably many values, (2) approximate this further by a simple random variable which converges to $\xi$ in probability, and (3) extract an almost sure convergent subsequence. Fix $\epsilon > 0$. 

<br><br>

(1) Fix $\delta>0$. Since $B$ is separable, we may write $B = \bigcup_{k=1}^\infty B_k$, where the sets $B_k$ are disjoint, Borel, and have diameter at most $\delta$. Choose any $b_k \in B_k$. Define the random variable

\[
\eta_{\delta}(\omega) = \sum_{k=1}^\infty b_k \mathbb{1}[\omega \in \xi^{-1}B_k]
\]

and observe that $\sup_\omega |\eta_\delta(\omega) - \xi(\omega)| \leq \delta$. In particular, choosing a sequence $\delta_n \to 0$, we obtain a sequence of random variables $\eta_{\delta_n}$ converging almost surely to $\xi$. Hence, $\eta_{\delta_n} \to \xi$ in probability, and so for some $N$, we have $d(\eta_{\delta_{N}}, \xi) \leq \epsilon$.

<br><br>

(2) Note that by construction we have

\[
\eta_{\delta_N}(\omega) = \sum_{k=1}^\infty c_k \mathbb{1}[\omega \in \xi^{-1}C_k]
\]

for some $c_k \in C_k$, and disjoint Borel sets $C_k$. Set $\tau_m$ to be the $m$th partial sum of this quantity. Observe that $\tau_m$ is a simple random element on $B$ and that $\tau_m \to \eta_{\delta_N}$ almost surely, and hence in $d$. Thus, for some $M$, we have $d(\tau_M, \xi) \leq 2 \epsilon$. As $\epsilon$ was arbitrary, we may thus obtain a sequence of simple random variables $(\alpha_n)$ converging to $\xi$ in probability.

<br><br>

(3) To conclude, recall that if $\alpha_n \to \xi$ in probability, then there exists a subsequence $(\alpha_{n_k})$ converging to $\xi$ almost surely. This yields our desired result.
</details>

Equipped with this result, we are able to provide a simple characterization of the existence of Bochner integrals.

<div class='proposition'>
Suppose $\xi$ is a random element on a separable Banach space $B$. Then, $\E \xi$ exists in the strong sense if and only if $\E |\xi| < \infty$.
</div>
<details>
<summary> Proof. </summary>
First, suppose $\E \xi$ exists strongly. Then, there exists a sequence $(\xi_n)_{n=1}^\infty$ of simple random elements on $B$ with $\E |\xi_n - \xi| \to 0$. It follows that for $n$ sufficiently large, $\E |\xi_n - \xi|$ must be finite, so that

\[
\E|\xi| \leq \E |\xi_n - \xi| + \E |\xi_n| < \infty.
\]

<br><br>

Conversely, we use the separability of $B$ to obtain a sequence of simple random variables $(\xi_n)_{n=1}^\infty$ such that $|\xi_n - \xi| \to 0$ almost surely. In fact, one may assume without loss of generality that $|\xi_n (\omega)| \leq 2 |\xi(\omega)|$ for all $\omega$; otherwise, construct a new sequence $(\eta_n)$ obtained by only retaining the $\xi_n$'s with this property, and any such sequence must agree with $(\xi_n)$ in the tails. It then follows from the Lebesgue dominated convergence theorem that $\E |\xi_n - \xi| \to 0$, and thus there exists a Bochner integral of $\xi$. 

</details>

### Relationship to the Pettis Integral

As the names might suggest, if the strong integral exists, then the weak integral also exists.

<div class='proposition'>
Suppose $\xi$ is a random element on a Banach space $B$ such that $\E \xi$ exists in the Bochner sense. Then, $\E \xi$ also exists in the Pettis sense, and moreover, their values coincide.
</div>
<details>
<summary> Proof. </summary>
As $\E \xi$ exists in the Bochner sense, there exists a sequence $(\xi_n)_{n=1}^\infty$ of simple random elements on $B$ such that $\E |\xi_n - \xi| \to 0$ and $\E \xi_n \to \E \xi$. Fix an $x^* \in X^*$. Observe that $\langle x^*, \E \xi_n \rangle \to \langle x^*, \E \xi \rangle$. 

<br><br>

Now, note that for $\xi_n = \sum_{k=1}^m c_k \mathbb{1}_{E_k}$,

\[
\langle x^* , \E \xi_n \rangle = \left\langle x^* , \E \sum_{k=1}^m c_k \P(E_k) \right\rangle = \sum_{k=1}^m \P(E_k) \langle x^*, c_k \rangle = \E \langle x^*, \xi_n \rangle.
\]

Thus, we see that $\E \langle x^*, \xi_n \rangle \to \E \langle x^*, \xi \rangle$, as
\[
| \E \langle x^*, \xi_n \rangle - \E \langle x^*, \xi \rangle | \leq \E |\langle x^*, \xi_n - \xi \rangle| \leq |x^*| \E |\xi_n - \xi|
\] 
which converges to zero by assumption. In other words, we have shown that $\langle x^*, \E \xi_n \rangle \to \langle x^*, \E \xi \rangle$ and that $\langle  x^*, \E \xi_n \rangle \to \E \langle x^*, \xi \rangle$, and hence the two values must coincide.
</details>

However, the converse is generally false (even in nice settings), as the following example shows. Take $B = \ell^2$ and recall that $B$ is separable. Take $\xi = s n e_n$ with probability $p(s, n) = \frac{3}{\pi^2} n^{-2}$ where $s \in \\{-1, +1 \\}$ and $e_n$ is the $n$th standard basis element. It is easy enough to check that $\E\| \xi \| = +\infty$ and so $\xi$ does not admit a strong mean. On the other hand, $\E \langle \xi, x \rangle = 0$ for any $x \in \ell^2$, and since $\ell^2$ is self-dual, it follows that the weak mean of $\xi$ is zero. 

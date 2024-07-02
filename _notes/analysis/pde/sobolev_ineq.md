---
title: "Sobolev Inequalities"
topic: "Analysis"
chapter: "PDEs"
section: "sobolev_ineq"
layout: note
permalink: "/notes/analysis/pde/sobolev_ineq/"

subtitle:
date: 2024-06-26
keywords: analysis, pdes
published: true
references: "Evans, L. C. (2022). Partial differential equations (2nd ed.).; "
---

We are interested in understanding the relationship between Sobolev spaces with different parameters $(k, p)$. Our strategy will be to establish various inequalities related to Sobolev norms on smooth functions, extending to the general case by a density argument.

Here's some motivation for the following theorem. Recall that a classically differentiable function is necessarily continuous -- in other words, differentiability implies some regularity on our function. The Sobolev-type inequalities extend this idea to the weak differentiability setting. For instance, if $u \in W^{1,p}(U)$, then $Du \in L^p(U)$. We should expect that $u$ then is "more regular" than $Du$, so we should hope that $u \in L^q(U)$ for some $q > p$. We should not expect *too much* additional regularity though, and the Sobolev conjugate $p^*$ furnishes us with the right degree.  


## First-Order Setting

Consider first $W^{1,p}(U)$ for $U\subset \R^n$ bounded and open. We seek an estimate of the form

\\[
\lvert\lvert u \rvert\rvert_{L^q(\R^n)} \leq C \lvert\lvert{D u}\rvert\rvert_{L^p(\R^n)} \qquad \forall u \in C_c^\infty(\R^n) \tag{1}
\\]

for some $C>0$ and $1 \leq q < \infty$, not depending on $u$. 

### A Scaling Argument

Suppose that $1 \leq p < \infty$ and that $u \in C_c^\infty(\R^n)$. Write $u_\lambda(x) = u(\lambda x)$ for a given $\lambda \geq 0$. Intuitively, increasing $\lambda$ shrinks the support of $u$. Observe that by a straightforward calculation we have

\\[
\lvert\lvert u_\lambda \rvert\rvert_{q} = \lambda^{-n/q} \norm{u}_q
\\]

\\[
\lvert\lvert{Du_\lambda}\rvert\rvert_p = \lambda^{1 - n/p} \lvert\lvert{Du}\rvert\rvert_p.
\\]

If we apply the desired inequality (1) to $u_\lambda$, we obtain

\\[
\lvert\lvert u \rvert\rvert_{q} \leq C \lambda^{1 - n/p + n/q} \lvert\lvert D u \rvert\rvert_p.
\\]

If $1 - \frac{n}{p} + \frac{n}{q} \neq 0$, by taking $\lambda$ to either zero or infinity, we would obtain a contradiction. Thus, we can only hope to have (1) hold if $q = \frac{np}{n-p}$.

Hence, for a given $1 \leq p < n$, we define the *Sobolev conjugate* to be

\\[
p^* = \frac{np}{n-p} \qquad \frac{1}{p^*} = \frac{1}{p} - \frac{1}{n}
\\]

and note $p^* > p$. 

With the following theorem, we prove such an inequality indeed holds. The basic idea of the proof is to consider $p=1$ and calculate the integral on the left-hand-side by integrating one variable at a time. To do so, recognize that $u(x)$ can be bounded by a line integral on $Du$ for each coordinate. One thing that might suggest this is the right idea is that the integral involves a term of the form $\|u\|^{n/(n-1)}$ and so if we can produce $n$ identical estimates we are on the right track. At the end of the day, the proof is essentially "just" a clever application of the fundamental theorem of calculus.

<div class='theorem' name='Gagliardo-Nirenberg-Sobolev Inequality'>
Let $1 \leq p < n$. Then, there exists a constant $C = C(p, n)$ such that
\[
\lvert\lvert u \rvert\rvert_{L^{p^*}(\R^n)} \leq C \lvert\lvert D u \rvert\rvert_{L^p(\R^n)}
\]

for all $u \in C_c^1(\R^n)$. 
</div>
<details class='proof'>
<summary> Proof. </summary>
<strong> Step one: $p=1$. </strong> 

Let $x = (x_1, \dots, x_n) \in \R^n$ be fixed. Since $u$ has compact support, we can integrate along a line to get

\[
u(x) = \int_{-\infty}^{x_i} \partial_i u(x_1, \dots, x_{i-1}, y_i, x_{i+1}, \dots, x_n) \d y_i
\]
and as a result we see
\[
|u(x)| \leq \int_{-\infty}^\infty |D u(x_1, \dots, y_i, \dots, x_n|) \d y_i
\]

which holds for every $i = 1, 2, \dots, n$. As a consequence of the previous inequality, we obtain

\[
|u(x)|^{n/(n-1)} \leq \prod_{i=1}^n \left( \int |D u| \d y_i \right)^{1/(n-1)}.
\]

Now, let's integrate against $x_1$. Let $I_1 = \int |Du| \d y_1$. Since the first term in the product does not depend on $x_1$, we have
\[
\begin{aligned}
\int_{-\infty}^\infty |u|^{n/(n-1)}\d x_1 &\leq \left(I_1^{1 / (n-1)} \right) \int_{-\infty}^\infty \prod_{i=2}^n \left( \int|Du| \d y_i \right)^{1/(n-1)} \d x_1 \\
&\leq \left( I_1 \right)^{1 / (n-1)} \left( \prod_{i=2}^n \int_{-\infty}^\infty \int_{-\infty}^\infty |Du| \d x_1 \d y_i \right)^{1/(n-1)}
\end{aligned}
\]

where the second line follows from (the generalized) Holder's inequality with $p_i = 1/(n-1)$. Set
\[
I_i = \int \int |D u | \d x_1 d y_1 \qquad i = 2, 3, \dots, n.
\]

Noticing again that the second product does not depend on $x_2$, we integrate against $x_2$ to see
\[
\int\int |u|^{n/(n-1)}\d x_1 \d x_2 \leq \left( \int\int |D u| \d x_1 \d y_2 \right)^{1/(n-1)}\int \prod_{i \neq 2} I_i^{1/(n-1)} \d x_2.
\]

Another application of Holder's inequality gives us

\[
\begin{aligned}
\int\int |u|^{n/(n-1)}\d x_1 \d x_2 \leq &\left( \int\int |Du| \d x_1 \d y_2 \right)^{1/(n-1)} \left( \int\int |Du| \d y_1 \d x_2 \right)^{1/(n-1)} \\
&\cdot \prod_{i=3}^n \left( \int\int\int |D u| \d x_1 \d x_2 \d y_i \right)^{1/(n-1)}.
\end{aligned}
\]

Stepping back, we see that repeating this argument reuslts in a term in the product being dropped, yielding

\[
\int |u|^{n/(n-1)} \d x \leq \left( \int |Du| \d x\right)^{n/(n-1)}
\]

which is the claim for $p=1$.

<br><br>
<strong> Step two: $1 < p < n$. </strong> Our strategy now will be to apply the previously obtained inequality to $v = |u|^\gamma$ for some appropriately chosen $\gamma > 1$. Indeed, the result for $p=1$ and an application of Holder's inequality gives us

\[
\left(\int |u|^{(\gamma n) / (n-1)} \right)^{(n-1)/n} \leq \gamma \int |u|^{\gamma-1} |Du| \d x \leq \gamma \lvert\lvert Du \rvert\rvert_p \left( \int |u|^{\frac{(\gamma-1)p}{p-1} } \d x \right)^{(p-1)/p}.
\]

To choose $\gamma$, we'd like that the exponent on $|u|$ on the LHS matches that on the RHS, i.e.

\[
\frac{\gamma n}{n-1} = \frac{(\gamma - 1) p}{p -1} \implies \gamma = \frac{p(n-1)}{n-p} > 1.
\]

Note that upon this choice we have $\frac{\gamma n}{n - 1} = p^*$, giving us the desired estimate
\[
\lvert\lvert u \rvert\rvert_{p^*} \leq \lvert\lvert D u \rvert\rvert_{p}.
\]
</details>

Some observations:
- The assumed compactness of $u$ is necessary, as any constant function would otherwise violate the theorem.
- The constant does not depend on the support of $u$, which is perhaps surprising.





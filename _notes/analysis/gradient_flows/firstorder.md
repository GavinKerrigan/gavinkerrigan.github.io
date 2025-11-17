---
title: "First-Order Calculus in Wasserstein Space"
topic: "Analysis"
chapter: "Gradient Flows"
section: "wgf"
layout: note
permalink: "/notes/analysis/gradient_flows/firstorder/"

subtitle: 
date: 2025-10-29
keywords: analysis, optimal transport, gradient flows
published: false
references: ""
---

A wide range of problems can be cast as minimizing some functional over a space of probability measures. That is, we seek
\\[
\inf_{\mu \in \mathcal{C} \subset \mathcal{P}(\R^d)} J[\mu]
\\]
where $\mathcal{C} \subset \mathcal{P}(\R^d)$ is a constraint set in the space of probability measures over $\R^d$ and $J: \mathcal{C} \to \overline{\R}$ is a (typically non-linear) functional. While the classical calculus of variations studies infinite-dimensional optimization problems, the typical setting is where our variable is in a space of functions, and so some additional tools are needed. 

In this note, we will study a general-purpose first-order differential calculus for such minimization problems. The main result is that we can obtain analogues of the KKT and Lagrange conditions from familiar calculus. 

We assume familiarity with optimal transport throughout. We will equip the space of probability measures with the 2-Wasserstein topology, so that we work on $\mathcal{P}_2(\R^d)$ everywhere.

## Variations

[GAV: is this the Otto calculus?]

We first need an appropriate notion of a *variation* of a measure $\overline{\mu} \in \mathcal{P}_2(\R^d)$, towards defining a notion of a tangent space. In light of the continuity equation, one might venture a guess that a vector field is the appropriate notion. However, this will not be sufficient for our purposes, as it does not allow for mass splitting. Instead, variations themselves should be transport *plans*.

<div class='definition'>
A variation at $\overline{\mu} \in \mathcal{P}_2(\R^d)$ is a probability measure $\xi \in \mathcal{P}_2(\R^d \times \R^d)$ such that $(\pi_1)_{\#} \xi = \overline{\mu}$.
</div>

In other words, if we disintegrate a variation $\xi$ we obtain a collection $\\{ \xi_x \\}_{x \in \text{supp}(\overline{\mu})}$ of probability measures $\xi_x \in \mathcal{P}(\R^d \times)$, which should be thought of as a distribution over tangents at $x \in \R^d$. Informally, $\xi(v \mid x)$ is what fraction of the mass at $x$ is transported along direction $v$. The usual notion of vector fields being tangents can be recovered by only considering distributions concentrated at a single $v$.

We now want a Riemannian-like structure on the space of variations. The basic game we'll play to get the definitions right is to work pointwise and glue things up with the measure $\overline{\mu}$ we're based at. So, at a given $x$, we have two local variations $\xi_{1,x}$ and $\xi_{2,x}$, which are distributions over tangents. If we had only two tangent vectors, we'd just take their inner product, but since we have distributions we need some way of pairing up tangents. That is, we need to select a coupling $\alpha_x \in \Gamma(\xi_{1,x}, \xi_{2,x})$ and average over this coupling. Then, we just average over $x \sim \overline{\mu}$. 

More formally, given variations $\xi_1, \xi_2$ based at $\overline{\mu}$, we select a 3-plan $\alpha \in \mathcal{P}\_2(\R^d \times \R^d \times \R^d)$ such that $\pi\_{12 \\#} \alpha = \xi_1, \pi\_{13  \\#} \alpha = \xi\_2$. We will write
\\[
\Gamma^1(\xi_1, \xi_2) = \left\\{ \alpha \in \mathcal{P}\_2(\R^d \times \R^d \times \R^d) : \pi\_{12 \\#} \alpha = \xi_1, \pi\_{13  \\#} \alpha = \xi\_2\right\\}
\\]
for the set of all such 3-plans, which depends on the base measure $\overline{\mu}$. A point $(x, v_1, v_2) \in \textrm{supp}(\alpha)$ being in the support of such a 3-plan intuitively means that $v_1, v_2$ are tangents at $x$ which are coupled under $\alpha$. To compare variations, we need a concrete choice for this coupling, which can be selected optimally. That is, we obtain a distance between variations as
\\[
\begin{align}
W\_{\overline{\mu}}^2(\xi_1, \xi_2) &= \min_{\alpha \in \Gamma^1(\xi_1, \xi_2)} \int_{(\R^d)^3} |v_1 - v_2|^2 d \alpha(x, v_1, v_2) \\\\\\
&= \E_{x \sim \overline{\mu}}[W_2^2(\xi_{1x}, \xi_{2x})].
\end{align}
\\]

This is precisely a conditional Wasserstein distance! While my paper phrases these as 4-plans, the 3-plan view is obviously equivalent. See also Chapter 12 in [AGS] where the notion of a geometric tangent space is discussed.

We can go beyond a distance metric and introduce an inner product and norm via
\\[
\langle \xi_1, \xi_2 \rangle_{\overline{\mu}} = \max\_{\alpha \in \Gamma^1(\xi_1, \xi_2)} \int_{(\R^d)^3} \langle v_1, v_2 \rangle d \alpha(x, v_1, v_2)
\\]
\\[
|\xi|\_{\overline{\mu}}^2 = \int\_{(\R^d)^2} |v|^2 d \xi(x, v).
\\]
Again, the idea is to do everything locally and glue together with the base measure. The max in the inner product arises from the expansion of the square-norm in the cost function defining the distance $W\_{\overline{\mu}}$. Observe that we have a divergence-style identity
\\[
W\_{\overline{\mu}}^2(\xi_1, \xi_2) = |\xi_1|^2\_{\overline{\mu}} + |\xi_2|^2\_{\overline{\mu}} - 2 \langle \xi_1, \xi_2 \rangle\_{\overline{\mu}}.
\\]

## Tangent Spaces

Given a variation $\xi$ at $\overline{\mu}$, how can we "follow" it? Again, let's put on our local hats. At a point $x$, the variation $\xi(v \mid x)$ tells us how much weight each direction $v$ has. Hence, we may split the mass at $x$ according to these weights and follow $x \mapsto x + v$. Informally, we map the mass $d \overline{\mu}(x) \mapsto \int \delta_{x + v} \d \xi(v \mid x) \d \overline{\mu}(x)$ which yields the perturbed measure
\\[
\begin{align}
\mu(A) &= \int_A \int_{\R^d} \delta_{x+v}\d \xi(v \mid x) \d \overline{\mu}(x) \\\\\\
       &= \int_{\R^d} \int_{\R^d} 1_A[x + v] \d \xi(x, v) \\\\\\
       &= (\pi_1 + \pi_2)\_{\\#} \xi(A).
\end{align}
\\]
From this heuristic calculation we see $\mu = (\pi_1 + \pi_2)\_{\\#} \xi$. This is like an exponential map, but we have to be very careful about geodesics.

Conversely, let's try to identify a kind of log map. That is, given $\mu, \overline{\mu}$, what variation will connect them? Unlike the Euclidean setting, this does not uniquely identify a variation. In fact, any coupling $\gamma \in \Gamma(\overline{\mu}, \mu)$ gives rise to a connecting variation via $\xi = (\pi_1, \pi_2 - \pi_1)\_{\\#}\gamma$. Indeed, we can calculate
\\[
\pi\_{1\\#}\xi = \pi\_{1\\#}\gamma = \overline{\mu} \qquad (\pi_1 + \pi_2)\_{\\#} \xi = \pi\_{2\\#}\gamma = \mu.
\\]

However, arbitrary variations do not give rise to constant speed geodesics (i.e., generally $ \|\xi\|\_{\overline{\mu}} \geq W\_2(\overline{\mu}, \mu)$), and thus cannot rightly be considered tangent vectors.

For convenience we recall some facts about constant speed geodesics in Wasserstein space.
<div class='definition'>
	A curve $(\mu_t)_{t \in [0, T]} \subset \mathcal{P}_2(\R^d)$ is called a constant speed geodesic if
	\begin{equation}
	W_2(\mu_s, \mu_t) = (t - s)W_2(\mu_0, \mu_1) \qquad \forall 0 \leq s \leq t \leq 1.
	\end{equation}
</div>
The following fully characterizes constant speed geodesics as arising from optimal plans [AGS Theorem 7.2.2].
<div class='theorem'>
	If $\gamma \in \Gamma_o(\overline{\mu}, \mu)$ is an optimal $\ell_2$ coupling, then the curve $\mu_t := (\pi_1 + t (\pi_2 - \pi_1))_{\#}\gamma$ is a constant speed geodesic between $\overline{\mu}, \mu$. Conversely, any constant speed geodesic between these measures has a representation of this form.
</div>

Let us set some notation, which at this stage is informal and should be treated with some caution. For a given variation $\xi$ based at $\overline{\mu}$, we define an exponential map $\exp\_{\overline{\mu}}(\xi) := (\pi\_1 + \pi\_2)\_{\\#} \xi$. We can consider the action of a scalar $\tau \in \R$ to be $\tau \xi\_1 := (\pi_1, \tau \pi_2)\_{\\#} \xi$. This has the effect of scaling the local tangents by $\tau$. It is easy to check that $\exp\_{\overline{\mu}}(\tau \xi) = (\pi\_1 + \tau \pi\_2)\_{\\#} \xi$ is consistent. Observe that given a variation $\xi$, we have $\gamma = (\pi_1, \pi_1 + \pi_2)\_{\\#} \xi \in \Gamma(\overline{\mu}, \exp_{\overline{\mu}}(\xi))$.

Theorem 1 says that constant speed geodesics are precisely the McCann interpolants arising from optimal couplings. In our notation, given a $\gamma \in \Gamma_0(\overline{\mu}, \mu)$, this gives rise to the variation $\xi = (\pi_1, \pi_2 - \pi_1)\_{\\#} \gamma$. Then, $\mu_t = \exp_{\overline{\mu}}(t \xi) = (\pi_1 + t(\pi_2 - \pi_1))\_{\\#} \gamma$ is a constant speed geodesic.

<div class='definition'>
The tangent space $T_{\overline{\mu}} \mathcal{P}_2(\R^d)$ of $\mathcal{P}_2(\R^d)$ at $\overline{\mu}$ is the $W^2_{\overline{\mu}}$ closure of the set
\begin{equation}
\Bigg\{ \xi \in \mathcal{P}_2(\R^d \times \R^d) : \pi_{1\#}\xi = \overline{\mu},  \exists \delta > 0, \forall |\epsilon| < \delta, (\pi_1, \pi_1 + \epsilon \pi_2)_{\#} \xi \in \Gamma_o\left(\overline{\mu}, \exp_{\overline{\mu}}(\epsilon \xi)\right) \Bigg\}
\end{equation}

where $\Gamma_o(\cdot, \cdot)$ is the set of $\ell_2$-optimal couplings between two measures.
</div>

It's a mouthful, but not too unintuitive. We just consider all variations such that, when appropriately scaled), yield an optimal coupling, and thus a geodesic. Conversely, we don't allow for variations that would not yield optimal couplings. In short, this restriction is necessary to obtain a "proper" Riemannian-like metric that acts like the local variation of the squared distance.

One of the biggest departures from Riemannian geometry is that the tangent space is generally not a vector space. However, we can equip the tangent space with a quasi-linear structure.

<div class='definition'>
Let $\overline{\mu} \in \mathcal{P}_2(\R^d)$ be fixed and consider tangents $\xi_1, \xi_2 \in T_{\overline{\mu}} \mathcal{P}_2(\R^d)$. We define:
<ol>
<li> A local zero: $0_{\overline{\mu}} := \overline{\mu} \otimes \delta_0$. </li>
<li> Scalar multiplication: $\tau \xi := (\pi_1, \tau \pi_2)_{\#}\xi$. </li>
<li> An addition: For $\alpha \in \Gamma^1(\xi_1, \xi_2)$, $\xi_1 +_\alpha \xi_2 := (\pi_1, \pi_2 + \pi_3)_{\#}\alpha$. </li>
</ol>
</div>

We've already seen that scalar multiplication acts to just scale all of the local tangents. Addition, on the other hand, relies on an external choice of coupling $\alpha \in \Gamma^1(\xi_1, \xi_2)$, as we need a way of selecting how arrows in $\xi_1$ are paired with those in $\xi_2$. It can be thought of as a kind of distributed composition. For sums of more than one element, we do the same thing except with an $n$-plan $\alpha \in \Gamma^1(\xi_1, \dots, \xi_n)$.

The following shows that these operations are well-defined. The proof is instructive: to check optimality, it suffices to check things are supported on the subdifferential of a convex potential. This idea is useful when we want to somehow combine two optimal plans. 

<div class='proposition'>
The tangent space $T_{\overline{\mu}} \mathcal{P}_2(\R^d)$ is closed under addition and scalar multiplication.
</div>
<details class='proof'>
<summary> Proof. </summary>
The scalar operation is easy. For the addition operation, let $\xi_1, \xi_2 \in T_{\overline{\mu}}\mathcal{P}_2(\R^d)$. Fix $a \in \Gamma^1(\xi_1, \xi_2)$. To show $\xi_1 +_a \xi_2$ is tangent, we need to check that this variation induces an optimal coupling for sufficiently short trajectories. To that end, define for $\epsilon > 0$
\[
\gamma := (\pi_1, (\pi_1 + \epsilon \pi_2))_{\#} (\xi_1 +_a \xi_2) = (\pi_1, \pi_1 + \epsilon(\pi_2 + \pi_3))_{\#}\alpha
\]

We need to check that $\gamma$ is an optimal coupling between $\overline{\mu}$ and $\exp_{\overline{\mu}}(\epsilon \gamma)$. It suffices to check that $\gamma$ is supported on the subdifferential graph of a convex function. Since $\xi_i$ is tangent, we may choose $\epsilon$ sufficiently small so that
\[
\text{supp}((\pi_1, \pi_1 + 2 \epsilon \pi_2 )_{\#}\xi_i) \subset \partial \varphi_i
\]

for some convex $\varphi_i$. That is, if $(x, v)$ are in the support of $\xi_i$, then $x + 2\epsilon v \in \partial \varphi_i(x)$ for some convex $\varphi_i$, so that $1/2 x + \epsilon v \in \partial(1/2 \varphi_i)(x)$.

Then, any element in the support of $\gamma$ has the form $(x, x + \epsilon v_1 + \epsilon v_2)$ for some $(x, v_i) \in \text{supp}(\xi_i)$. It follows that $x + \epsilon v_1 + \epsilon v_2 \in \partial(1/2 \varphi_1 + 1/2 \varphi_2)(x)$.
</details>

## An Aside on Geodesics

Why don't we just allow for all possible variations? Why do we care that they're optimal? I'm still wrapping my head around this point, but I think the argument goes like this. We start from $(\mathcal{P}_2(\R^d), W_2)$ and want to give it a Riemannian-like structure. That is, to a tangent vector field $v$ we want to assign a norm such that $\|v\|\_{\mu}^2$ is like an infinitesimal squared distance, so that
\\[
W_2^2(\mu, (\iota + \epsilon v)\_{\\#}\mu) \approx \epsilon^2 \int |v|^2\_{\mu} \d \mu.
\\]

[Gav: In fact, can't I "recover" the metric from $d/dt W_2^2(\mu, \mu_t)\|\_{t=0}$, and then Benamou-Brenier forces me to choose gradient field tangents?]

For an *arbitrary* $v$, one that is not a gradient field, we will in general have that the right-hand side is larger than the squared distance, and so there is an obstruction to getting an appropriate Riemannian-like structure. In fact, by adding a divergence component, we can make this right-hand side arbitrarily large. How can we fix this? 

The insight here is that an arbitrary vector field can be decomposed into a *gradient component*, flowing along which actually affects our measure, and an *divergence* component which only "stirs" the measure without moving it! So, geometrically, you can think of the gradient part as being tangent to $\mathcal{P}_2$, and the divergence part as being normal to $\mathcal{P}_2$. Although, it may still not be quite the right picture; maybe the divergence part should be thought of as a kind of "null" direction along which the measure doesn't change.

You of course want to get rid of this superfluous null directions in your geometry as they are essentially extraneous data, giving you a degenerate metric. The tangent space $T\_\mu \mathcal{P}_2(\R^d)$ then essentially corresponds to quotienting out the divergence part, and the Helmholtz decomposition gives us a unique gradient-field representative in each of the equivalence classes.

One idea/question I had was: there seems to be another way to fix this rather than changing your tangent space. Just change your definition of the metric to only measure the size of the gradient component. This is fine (and numerically equivalent), but the resulting inner product is degenerate, and you're going to want to quotient out this space anyway to get to the geometry. It's also going to make life harder, since you'll be needing to find your Helmholtz decomposition frequently.

## Wasserstein Subgradients

Having set up the basic differential geometry on Wasserstein space, we can finally turn our attention towards optimizing functionals.

<div class='definition' name='Regular Wasserstein Subgradients'>
Let $J:\mathcal{P}_2(\R^d) \to \overline{\R}$ be a functional. Fix $\overline{\mu} \in \mathcal{P}_2(\R^d)$ and suppose $J(\overline{\mu}) \in \R$ is finite. We say $\overline{\xi} \in T_{\overline{\mu}} \mathcal{P}_2(\R^d)$ is a regular subgradient of $J$ at $\overline{\mu}$ if for all $\mu \in \mathcal{P}_2(\R^d)$, we have
\[
J(\mu) - J(\overline{\mu}) \geq \langle \overline{\xi}, \xi \rangle_{\overline{\mu}} + o\left(W_2(\overline{\mu}, \mu)\right)
\]

for all $\xi \in (\pi_1, \pi_2 - \pi_1)_{\#} \Gamma_o(\overline{\mu}, \mu)$. If such an $\overline{\xi}$ exists, we say $J$ is regularly subdifferentiable at $\overline{\mu}$. We write $\hat{\partial}J(\overline{\mu})$ for the set of all such regular subdifferentials.
</div>

This coincides with [AGS Definition 10.3.1], therein called an extended Frechet subdifferential.

To motivate this definition a bit, recall that in Euclidean spaces we say that a vector $v$ is a regular subdifferential of $f: \R^d \to \R$ at $\overline{x}$ if
\\[
f(x) - f(\overline{x}) \geq \langle v, x - \overline{x} \rangle + o( ||x - \overline{x}||)
\\]
for all $x \in \R^d$. Note that this is a local definition (i.e., $f$ is above its supporting hyperplane locally to $\overline{x}$) and does not require convexity.

We have now replaced $v$ with a tangent $\xi$. The displacement $x - \overline{x}$ is now non-unique though, with any $\gamma \in \Gamma_0(\overline{\mu}, \mu)$ giving rise to a displacement $\xi = (\pi_1, \pi_2 - \pi_1)\_{\\#} \gamma$ as previously discussed. For regular subdifferentiability we require the necessary property to hold at all such variations.

<div class='definition' name='General Wasserstein Subgradients'>
	We say that $\overline{\xi} \in \mathcal{P}_2(\R^d \times \R^d)$ is a (general) subgradient of $J$ at $\overline{\mu}$ if there exists sequences $\mu_n \in \mathcal{P}_2(\R^d), \xi_n \in \hat{\partial}J(\overline{\mu})$ with $\mu_n \to \overline{\mu}, \xi_n \to \overline{\xi}$ in the 2-Wasserstein topology and $J(\mu_n) \to J(\overline{\mu})$. We write $\partial J(\overline{\mu})$ for the set of all such elements.
</div>

Alright, this is meaty definition, and my knowledge of nonsmooth optimization is lacking. The general subgradient is built out of limits of regular subgradients. I'm going to venture a guess that a function can fail to have a regular subgradient at a point, but can have a general subgradient, and that this definition is motivated by some kind of closure or approximation need. It's immediate that $\hat{\partial}J(\overline{\mu}) \subset \partial J(\overline{\mu})$ (just take the limiting sequence to be constant).

Another way of writing this is
\\[
\partial J(\overline{\mu}) = \left\\{\lim_{k\to\infty} \xi_k : \xi_k \in \hat{\partial}J(\mu_k), \mu_k \to \overline{\mu}, J(\mu_k) \to J(\overline{\mu}) \right\\}.
\\]
So the general subdifferential is the collection of limit points of nearby subgradients.

For an example of a function that has no regular subgradient, take $f(x) = x^2 \sin(1/x)$ and define $f(0) = 0$. This oscillates rapidly at $x=0$ and so you can't find a local linear subapproximation. On the other hand, the general subdifferential is $\partial f(0) = [-1, 1]$ by taking an appropriate limiting sequence. 

Note that we use Wasserstein convergence (rather than COT convergence) for the variations as the first marginal may vary. Moreover, the general subdifferential may not be tangent!

Regular supergradients are elements of $- \hat{\partial}(-J)(\overline{\mu})$. Supergradients are elements of $- \partial(- J)(\overline{\mu})$. 

<div class='definition' name='Differentiable Functionals'>
A functional $J: \mathcal{P}_2(\R^d) \to \overline{R}$ is differentiable at $\overline{\mu} \in \mathcal{P}_2(\R^d)$ there exists $\xi \in T_{\overline{\mu}}\mathcal{P}_2(\R^d)$ which is both a regular subgradient and a regular supergradient. In other words, $\hat{\partial}(J)(\overline{\mu}) \cap - \hat{\partial}(-J)(\overline \mu) \neq \varnothing$.
</div>

<div class='proposition' name='Characterizing Differentiable Functionals'>
Suppose $J$ is differentiable at $\overline{\mu}$. Then,
<ol>
<li> The intersection of subdifferentials and superdifferentials at $\overline{\mu}$ is a singleton. We call this element the gradient of $J$ at $\overline{\mu}$, written $\nabla J(\overline{\mu})$.</li>
<li> A tangent $\xi \in T_{\overline{\mu}} \mathcal{P}_2(\R^d)$ is $\xi = \nabla J(\overline{\mu})$ if and only if for all $\mu \in \mathcal{P}_2(\R^d)$, $\xi' \in (\pi_1, \pi_2 - \pi_1)_{\#} \Gamma_o(\overline{\mu}, \mu)$, $\alpha \in \Gamma^1(\xi, \xi')$, we have
\[
J(\mu) - J(\overline{\mu}) = \int \langle x_2, x_3 - x_1 \rangle \d \alpha(x_1, x_2, x_3) + o\left( W_2(\overline{\mu}, \mu)\right).
\]
</li>
</ol>
</div>

In other words, gradients are unique. However, a word of caution: general subdifferentials may be nonunique even when $J$ is differentiable. The second claim is essentially saying that the gradient gives us first-order Taylor approximation, where $\xi'$ plays the role of a perturbation $\overline{\mu} \to \mu$ which again may be nonunique. The only somewhat mysterious thing here is the presence of $\alpha$, but note that we can take the optimal choice to get $\max \langle \xi, \xi' \rangle_{\overline{\mu}}$ which helps explain it.

## Example: The Wasserstein Distance

You can show that $\mu \mapsto J[\mu] = \frac{1}{2}W_2^2(\mu, \hat{\mu})$ is, in general, not regularly subdifferentiable, and thus not differentiable. It is, however, always regularly superdifferentiable. However, at a point $\mu$ which is absolutely continuous, it is actually differentiable.

<div class='proposition'>
Let $J: \mathcal{P}_2(\R^d) \to \R$ be given by $J[\mu] = \frac{1}{2}W_2^2(\mu, \hat{\mu})$ for some fixed $\hat{\mu} \in \mathcal{P}_2(\R^d)$. For any $\overline{\mu} \in \mathcal{P}_2(\R^d)$, 
<ol>
<li> $J$ is regularly superdifferentiable at $\overline{\mu}$. If $\gamma \in \Gamma_o(\overline{\mu}, \hat{\mu})$, then $(\pi_1, \pi_1 - \pi_2)_{\#}\gamma$ is a regular supergradient of $J$ at $\overline{\mu}$. </li>
<li> If $\Gamma_0(\overline{\mu}, \hat{\mu})$ is a singleton and induced by a map, then $J$ is regularly subdifferentiable at $\overline{\mu}$. In this case, $J$ is also differentiable there. This happens if $\overline{\mu}$ is absolutely continuous. </li>
<li> If $\xi \in \hat{\partial}J[\overline{\mu}]$ is a subgradient, then the induced plan $(\pi_1, \pi_1 - \pi_2)_{\#}\xi \in \Gamma_o(\overline{\mu}, \hat{\mu})$ is optimal. </li>
<li> If $\Gamma_o(\overline{\mu}, \hat{\mu})$ is not a singleton, then $J$ is not regularly subdifferentiable at $\overline{\mu}$. </li>
</ol>

</div>

In summary, (1) the $W_2$ distance is always regularly superdifferentiable and any optimal coupling will induce such a variation, (2) $J[\mu]$ is differentiable at densities, (3) any subgradient induces an optimal plan (and so by uniqueness of gradients, if its differentiable, there must be a unique optimal plan), and (4) uniqueness of optimal plans is an obstruction to regular subdifferentiability.

Note that (4) says that "subgrad $\implies$ singleton". But (2) says "singleton + map $\implies$ subgrad". This is actually sharp: you can give an example showing that singleton is not sufficient for subgrad.

The reasoning in the example is kinda complex. It goes like this. (1) There is a unique optimal plan in this example. (2) By Prop 3.1 it induces a unique regular supergrad $\xi$. (3) If we had any subgrad, the functional would be differentiable, and thus the subgrad/supergrad is unique and coincide, meaning the only possible choice for a subgrad would actually be $\xi$. (4) Check that $\xi$ is not a subgrad. 

Actually, the authors claim it follows from Prop 3.3 which I didn't see how. But I think my argument in the last paragraph might actually just be reproducing the proof of Prop 3.3. You can apply 3.3 by saying that if $\xi$ is a subgrad then its corresponding map must be the unique optimal thing so the $\xi$ they write down is the only candidate for the subgrad.

## Questions

- Why is the Wasserstein topology the right choice?
- Can we develop a second-order calculus? https://cvgmt.sns.it/media/doc/paper/1274/Secondo.pdf
- What if the base space is Riemannian? I think Eq 9 in the paper now becomes something computed in each local tangent space... 
- Worth reading: ON THE INVERSE IMPLICATION OF BRENIER-MCCANN THEOREMS AND THE STRUCTURE OF... Gigli
- Worth reading on notions of subdifferentiability: https://mathoverflow.net/questions/139142/an-intuition-for-three-different-types-of-subgradients-proximal-regular-limit
- Good intro to DRO with OT: https://arxiv.org/pdf/1810.02403
- Looks cool: https://arxiv.org/pdf/2406.05268v1
- Antonio Terpin's masters thesis (!) might be worth looking at: https://www.research-collection.ethz.ch/server/api/core/bitstreams/f7f97b5a-f327-4da9-b618-be786065f99c/content
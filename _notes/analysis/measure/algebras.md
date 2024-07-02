---
title: "Set Algebras"
topic: "Analysis"
chapter: "Measure Theory"
section: "algebras"
layout: note
permalink: "/notes/analysis/measure/algebras/"

subtitle: 
date: 2024-06-28
keywords: analysis, measure theory
published: true
references: "Folland, G. B. (1999). Real analysis: Modern techniques and their applications (2nd ed.).; "
---

Here, we collect some definitions regarding collections of sets and their algebraic structures.

<div class='definition' name='Algebras'>
Let $X$ be a nonempty set. An algebra of sets on $X$ is a nonempty collection $\mathcal{A}$ of subsets of $X$, $\mathcal{A} \subset 2^X$, such that
<ol>
<li> $\mathcal{A}$ is closed under complements </li>
<li> $\mathcal{A}$ is closed under finite unions. </li>
</ol>

A $\sigma$-algebra on $X$ is an algebra that is closed under countable unions. 
</div>

Some easy properties of algebras are as follows. We'll skip the proof since it is a straightforward consequence of the definitions.

<div class='proposition' name='Properties of Algebras'>
Let $\mathcal{A}$ be an algebra (resp. $\sigma$-algebra). Then,
<ol>
<li> $\varnothing \in \mathcal{A}$ and $X \in \mathcal{A}$. </li>
<li> $\mathcal{A}$ is closed under finite (resp. countable) intersections. </li>
<li> If $\mathcal{A}$ is closed under countable disjoint unions, it is a $\sigma$-algebra. </li>
<li> The intersection of any collection of $\sigma$-algebras on $X$ is a $\sigma$-algebra on $X$. </li>
</ol>
</div>



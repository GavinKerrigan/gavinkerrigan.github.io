---
title: "Operator Classes"
topic: "Analysis"
chapter: "Functional Analysis"
section: "Operator Classes"
layout: note
permalink: "/notes/analysis/functional_analysis/operators/"

subtitle: 
date: 2025-04-07
keywords: gaussian measures, hilbert spaces, pettis integrals, bochner integrals
published: false
references: "Kukush, A. (2020). Gaussian measures in Hilbert space: Construction and properties, Chapter 3."
---

Here we briefly review a few classes of operators which are particularly relevant for the study of Gaussian measures and probability on infinite-dimensional spaces. Throughout, $H$ will be a separable real Hilbert space.

<div class='definition'>
Let $A$ be a linear operator on $H$.

<ol>
	<li> (<strong>Bounded</strong>) $L(H)$ is the class of bounded linear operators on $H$, equipped with the operator norm $|A| = \sup_{|x|\leq 1} |Ax|$. </li>
	<li> (<strong>Compact</strong>) $S_{\infty}(H) \subset L(H)$ is the class of compact operators, where $A$ is compact if it maps bounded sets to precompact sets. $S_\infty(H)$ is a subspace of $L(H)$, i.e., it is a closed vector space. </li>
	<li> (<strong>Hilbert-Schmidt</strong>) $S_2(H) \subset L(H)$ is the class of Hilbert-Schmidt operators, consisting of $A \in L(H)$ with finite Hilbert-Schmidt norm $|A_2| = \sum_{k=1}^\infty |A e_k|^2$ for any orthonormal basis $(e_k)_{k=1}^\infty$ of $H$. </li>
</ol>

</div>
---
layout: post
title: Note 10 - 03/04/2023
parent: Calculus II
grand_parent: Semester I
nav_order: 11
---

{% include toc.md %}

## I. Basic limits

1. $\lim_{n \to \infty} \dfrac{1}{n^\alpha} = 0$ if $\alpha > 0$
2. Let $L=\lim_{n \to \infty} r^n$, then:
* $L=0$ if $\vert r \vert <1$
* $L=1$ if $r=1$
* $L=\infty$ if $r>1$
* $L$ does not exist if $r \leq -1$
3. Squeeze theorem

    If $a_n \leq b_n \leq c_n, \forall n \in \mathbb{N}$ and $\lim a_n = \lim c_n = L$ then $\lim b_n = L$

1. $\lim a_{2n}=\lim a_{2n+1}=L \Rightarrow \lim a_n=L$
$\lim a_{2n} \neq \lim a_{2n+1} \Rightarrow \lim a_n$ does not exist.
1. Weierstrass's theorem
Let $\\{a_n\\}$ be a monotonic bounded sequence then $\\{a_n\\}$ converges.
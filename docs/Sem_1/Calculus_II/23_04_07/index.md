---
layout: post
title: Note 11 - 07/04/2023
parent: Calculus II
grand_parent: Semester I
nav_order: 12
---

{% include toc.md %}

## Theorem

1. If the series $\sum_{n=1}^{\infty} a_n$ is convergent, then $\lim_{n \to \infty} a_n=0$.

## Steps for convergent or divergent test

1. If $\lim_{n \to \infty} a_n \neq 0$ then **STOP**. Summary: the series diverges.
2. If $\lim_{n \to \infty} S_n = S \in \mathbb{R}$ then **STOP**. Summary: the series converges at $S$.

    If $\lim_{n \to \infty} S_n$ does not exist or approaches $\pm \infty$ then **STOP**. Summary: the series diverges.
1. Use convergent tests:

* **Non-negative series**: $\sum_{n=1}^{\infty} a_n$ with $a_n \geq 0$

    * Comparison test: 
    
        If $0 \leq a_n < b_n$ then
        * $\sum_{n=1}^{\infty} a_n$ diverges $\Rightarrow$ $\sum_{n=1}^{\infty} b_n$ diverges.
        * $\sum_{n=1}^{\infty} b_n$ converges $\Rightarrow$ $\sum_{n=1}^{\infty} a_n$ converges.

    * Limit test:
    
        If $\lim_{n \to \infty} \dfrac{a_n}{b_n} = K \neq 0, \infty$
    then $\sum_{n=1}^{\infty} a_n$ and $\sum_{n=1}^{\infty} b_n$ have identical property in convergent testing.
    
    * Integral test:
    
        If $f(n)=a_n$ is a continuous and decreasing function on $[1,\infty)$
        then $\int_1^\infty f(x) \ dx$ and $\sum_{n=1}^{\infty} a_n$ have identical property in convergent testing.
    
* **Alternating series** (aka **Leibniz criterion**):
$\sum_{n=1}^\infty (-1)^nb_n=-b_1+b_2-b_3+b_4-...$ with $b_n>0$
    * If $\\{b_n\\}$ decreases and $\displaystyle \lim_{n \to \infty} b_n=0$ then $\sum_{n=1}^\infty (-1)^nb_n$ converges.
    * If $\\{b_n\\}$ increases and $\displaystyle \lim_{n \to \infty} b_n \neq 0$ then $\sum_{n=1}^\infty (-1)^nb_n$ diverges.

* **Any series**:
    * Absolute convergence:

        If $\sum_{n=1}^\infty \vert a_n \vert$ converges then $\sum_{n=1}^\infty a_n$ converges absolutely.
    
    * Ratio test (aka **d'Alembert criterion**)
    
        If $\displaystyle \lim_{n \to \infty} \left\vert \frac{a_{n+1}}{a_n} \right\vert = D$ then
        *    If $D>1$ then the series diverges.
        *    If $D<1$ then the series converges.
    
    * Root test (aka **Cauchy criterion**)

        If $\displaystyle \lim_{n \to \infty} \sqrt[n]{\left\vert a_n \right\vert} = C$ then
        *    If $C>1$ then the series diverges.
        *    If $C<1$ then the series converges.
        
---
layout: post
title: Note 8 - 27/03/2023
parent: Calculus II
nav_order: 9
---

{% include toc.md %}

## I. Tricks to find a proper function for The Comparison Test

* Given $a > 1$ and $\alpha,\beta>0$

$$
1 << \ln^\alpha x << x^\beta << a^x \ \ \ \ \text{as $x \to \infty$}
$$

* "Nhỏ nhỏ lớn lớn"
Let $a$ be a positive real number
    * $\displaystyle \int_0^a \frac{1}{x^p} \ dx$ is convergent $\Leftrightarrow$ $p<1$
    * $\displaystyle \int_a^\infty \frac{1}{x^p} \ dx$ is convergent $\Leftrightarrow$ $p>1$
    
## II. Exercises
* Determine if $\displaystyle \int_1^\infty \frac{x^2+\ln x+1}{x^5+3x^2+3} \ dx$ is convergent or divergent.
We consider $\displaystyle f(x)=\frac{x^2+\ln x+1}{x^5+3x^2+3}$, $x \geq 1$
We have:
    * $\displaystyle 0 \leq f(x) \leq \frac{x^2+\ln x +1}{x^5} \leq \frac{x^2+x^2+x^2}{x^5} = \frac{3}{x^3}$, $\forall x \geq 1$ 
    * $\displaystyle \int_1^\infty \frac{3}{x^3} \ dx = \lim_{t \to \infty} \int_1^t \frac{3}{x^3} \ dx = \lim_{t \to \infty} \left(\frac{-3}{2x^2}\vert_1^t\right) = \lim_{t \to \infty} \left(\frac{3}{2}-\frac{3}{2t^2}\right) = \frac{3}{2} \in \mathbb{R}$
  
    So this integral is convergent.
    
    By the comparison test, $\displaystyle \int_1^\infty f(x) \ dx$ is convergent.
    
* Determine if $\displaystyle \int_0^\infty \frac{x}{x^3+1} \ dx$ is convergent or divergent.
$\displaystyle \int_0^\infty \frac{x}{x^3+1} \ dx = \int_0^1 \frac{x}{x^3+1} \ dx + \int_1^\infty \frac{x}{x^3+1} \ dx$
Let $\displaystyle I_1=\int_0^1 \frac{x}{x^3+1} \ dx$ and $\displaystyle I_2=\int_1^\infty \frac{x}{x^3+1} \ dx$
We know that $I_1$ is a definite integral so it is convergent.
Now consider the second subintegral, we have:
    * $\displaystyle 0 \leq f(x):=\frac{x}{x^3+1} \leq \frac{x}{x^3} = \frac{1}{x^2}$, $\forall x \geq 1$
    * $\displaystyle \int_1^\infty \frac{1}{x^2} \ dx = \lim_{t \to \infty} \int_1^t \frac{1}{x^2} \ dx = \lim_{t \to \infty} \left(-\frac{1}{x} \vert_1^t\right) = \lim_{t \to \infty} \left(1-\frac{1}{t}\right) = 1 \in \mathbb{R}$
  
    So $I_2$ is convergent.
    
    Hence $\displaystyle \int_1^\infty f(x) \ dx$ is convergent (by the Comparison test).    
    Therefore, $\displaystyle \int_0^\infty \frac{x}{x^3+1} \ dx$ is convergent.
---
layout: post
title: Note 7 - 24/03/2023
parent: Calculus II
nav_order: 8
---

{% include toc.md %}

## I. A Comparison Test for Improper Integrals

Suppose that $f$ and $g$ are continuous functions with $0 \leq g(x) \leq f(x)$ for $a \leq x$.

(a) If $\int_a^\infty f(x) \ dx$ is covergent, then $\int_a^\infty g(x) \ dx$ is covergent.

(b) If $\int_a^\infty g(x) \ dx$ is divergent, then $\int_a^\infty f(x) \ dx$ s divergent.

_**Be careful:**_ the reverse is not necessarily true: If $\int_a^\infty g(x) \ dx$ is convergent, $\int_a^\infty f(x) \ dx$ may or may not be convergent, and if $\int_a^\infty f(x) \ dx$ is divergent, $\int_a^\infty g(x) \ dx$ may or may not be divergent.

## II. Exercises

* Determine $\displaystyle \int_1^\infty \frac{2+e^{-x}}{x} \ dx$ is convergent or divergent.
  
We have:

$$
0 \leq \frac{1}{x} \leq \frac{2+e^{-x}}{x}, \forall x \geq 1
$$

and

$$
\int_1^\infty \frac{1}{x} \ dx
=\lim_{t \to \infty} \int_1^t \frac{1}{x} \ dx
=\lim_{t \to \infty} \left[\ln\vert x \vert\right]_1^t
=\lim_{t \to \infty} \ln t
=\infty
$$

By the Comparison Test, $\displaystyle \int_1^\infty \frac{2+e^{-x}}{x} \ dx$ is divergent.

* Determine $\displaystyle \int_0^\infty \frac{\arctan x}{2+e^x} \ dx$ is convergent or divergent.
  
Observe that $-\dfrac{\pi}{2} \leq \arctan x \leq \dfrac{\pi}{2}$, so

$$
0 \leq \frac{\arctan x}{2+e^x} \leq \frac{2}{2+e^x} \leq \frac{2}{e^x}, \forall x \geq 0
$$

$$
\int_0^\infty \frac{2}{e^x} \ dx
=2\lim_{t \to \infty} \int_0^t e^{-x} \ dx
=2\lim_{t \to \infty} \left[-e^{-x}\right]_0^t
=2\lim_{t \to \infty} (1-e^{-t}) = 2
$$

By the Comparison Test, $\displaystyle \int_0^\infty \frac{\arctan x}{2+e^x} \ dx$ is convergent
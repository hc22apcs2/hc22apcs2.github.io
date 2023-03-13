---
layout: post
title: Note 5 - 10/03/2023
parent: Calculus II
---

{% include toc.md %}

## I. Improper integrals

### 1. Infinite intervals

a) If $\int_a^t f(x) \ dx$ exists for every number $a \leq t$, then

$$
\int_a^{\infty} f(x) \ dx = \lim_{t \to \infty} \int_a^t f(x) \ dx
$$

_provided this limit exists (as a finite number)_

b) If $\int_{t}^b f(x) \ dx$ exists for every number $t \leq b$, then

$$
\int_{-\infty}^b f(x) \ dx = \lim_{t \to -\infty} \int_t^b f(x) \ dx
$$

_provided this limit exists (as a finite number)_

The improper integral $\int_a^t f(x) \ dx$ and $\int_{t}^b f(x) \ dx$ are called **convergent** if the corresponding limit exists and **divergent** if the limit does not exist.

c) If both $\int_a^t f(x) \ dx$ and $\int_{t}^b f(x) \ dx$ are convergent, then we define

$$
\int_{-\infty}^{\infty} f(x) \ dx = \int_{-\infty}^a f(x) \ dx + \int_a^{\infty} f(x) \ dx \ \ \ \ \ \ \ \forall a \in \mathbb{R}
$$

**_Example:_**

1. _Determine whether the integral $\displaystyle \int_1^\infty \frac{1}{x} \ dx$ is convergent or divergent_

$$
\int_1^{\infty} \frac{1}{x} \ dx = \lim_{t \to \infty} \int_1^t \frac{1}{x} \ dx = \lim_{t \to \infty} \left.\ln |x|\right]_1^t = \lim_{t \to \infty} \ln t = \infty 
$$

$ \ \ \ \therefore$ The given integral is divergent.

2. _Evaluate $\displaystyle \mathrm{I} = \int_{-\infty}^\infty \frac{1}{1+x^2} \ dx$_

It is convenient to choose $a=0$ to calculate

$$
\mathrm{I} = \int_{-\infty}^0 \frac{1}{1+x^2} \ dx + \int_0^\infty \frac{1}{1+x^2} \ dx
$$

We have to consider the integrals at the right side seperately:

$$\begin{align*}
\int_{-\infty}^0 \frac{1}{1+x^2} \ dx &= \lim_{t \to -\infty} \int_t^0 \frac{1}{1+x^2} \ dx = \lim_{t \to -\infty} \left.\arctan x\right]_t^0 \\
&= \lim_{t \to -\infty} (\arctan 0 - \arctan t) =\lim_{t \to -\infty} (- \arctan t) = \frac{\pi}{2}
\end{align*}$$

$$\begin{align*}
\int_0^{\infty} \frac{1}{1+x^2} \ dx &= \lim_{t \to \infty} \int_0^t \frac{1}{1+x^2} \ dx = \lim_{t \to \infty} \left. \arctan t \right]_0^t \\
&=\lim_{t \to \infty} (\arctan t -\arctan 0) = \lim_{t \to \infty} \arctan t = \frac{\pi}{2}
\end{align*}$$

So

$$
\int_{-\infty}^{\infty} \frac{1}{1+x^2} \ dx = \frac{\pi}{2} + \frac{\pi}{2} = \pi \Rightarrow \text{I is convergent}
$$


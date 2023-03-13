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

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
\int_{-\infty}^{\infty} f(x) \ dx = \int_{-\infty}^a f(x) \ dx + \int_a^{\infty} f(x) \ dx 
$$

$a$ can be any real number which is available.

**_Example:_**

* Determine whether the integral $\displaystyle \int_1^\infty \frac{1}{x} \ dx$ is convergent or divergent

$$
\int_1^{\infty} \frac{1}{x} \ dx = \lim_{t \to \infty} \int_1^t \frac{1}{x} \ dx = \lim_{t \to \infty} \left.\ln |x|\right]_1^t = \lim_{t \to \infty} \ln t = \infty 
$$

$ \ \ \ \therefore$ The given integral is divergent.

* Evaluate $\displaystyle \mathrm{I} = \int_{-\infty}^\infty \frac{1}{1+x^2} \ dx$

It is convenient to choose $a=0$ to calculate

$$
\mathrm{I} = \int_{-\infty}^0 \frac{1}{1+x^2} \ dx + \int_0^\infty \frac{1}{1+x^2} \ dx
$$

We have to consider the integrals at the right side separately:

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

### 2. Discontinuous integrands

a) If $f$ is continuous on $[a,b)$ and is discontinuous at $b$, then
  
$$
\int_a^b f(x) \ dx = \lim_{t \to b^-} \int_a^t f(x) \ dx
$$

_if this limit exists (as a finite number)_

b) If $f$ is continuous on $(a,b]$ and is discontinuous at $a$, then

$$
\int_a^b f(x) \ dx = \lim_{t \to a^+} \int_t^b f(x) \ dx
$$

_if this limit exists (as a finite number)_

The improper integral $\int_a^b f(x) \ dx$ is called **convergent** if the corresponding limit exists and **divergent** if the limit does not exist.

c) If $f$ has discontinuity at $c$, where $a < c < b$, and both $\int_a^c f(x) \ dx$ and $\int_c^b f(x) \ dx$ are convergent, then we define

$$
\int_a^b f(x) \ dx = \int_a^c f(x) \ dx + \int_c^b f(x) \ dx
$$

**_Example_**

* Evaluate $\mathrm{I}=\displaystyle \int_2^5 \frac{1}{\sqrt{x-2}} \ dx$

Let $\displaystyle f(x)=\frac{1}{\sqrt{x-2}} \Rightarrow f \ \text{is discontinuous at 2}$, so

$$
\mathrm{I} = \lim_{t \to 2^-} \int_t^5 \frac{1}{\sqrt{x-2}} \ dx = \lim_{t \to 2^-} \left.2\sqrt{x-2}\right]_t^5 = \lim_{t \to 2^-} 2(\sqrt{3}-\sqrt{t-2}) = 2\sqrt{3}
$$

$\therefore \text{I is convergent}$

* Evaluate $\displaystyle \mathrm{I}=\int_0^3 \frac{dx}{x-1}$ if possible

Let $\displaystyle f(x)=\frac{1}{1-x} \Rightarrow f \ \text{is discontinuous at 1}$, so

$$
\mathrm{I}=\int_0^1 \frac{dx}{x-1} + \int_1^3 \frac{dx}{x-1}
$$

but

$$
\int_0^1 \frac{dx}{x-1} = \lim_{t \to 1^-} \int_0^t \frac{dx}{x-1} = \lim_{t \to 1^-} \left.\ln|x-1|\right]_0^t = \lim_{t \to 1^-} \ln|t-1|=-\infty
$$

$$
\Rightarrow \int_0^1 \frac{dx}{x-1} \text{ is divergent} \Rightarrow \text{I is divergent}
$$

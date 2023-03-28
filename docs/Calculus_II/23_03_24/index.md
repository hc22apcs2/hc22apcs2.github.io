---
layout: post
title: Note 7 - 24/03/2023
parent: Calculus II
nav_order: 8
---

{% include toc.md %}

## I. A Comparison Test for Improper Integrals

Suppose that $f$ and $g$ are continuous functions with $0 \leq g(x) \leq f(x)$ for $a \leq x$.

(a) If $\int_a^\infty f(x) \ dx$ is convergent, then $\int_a^\infty g(x) \ dx$ is convergent.

(b) If $\int_a^\infty g(x) \ dx$ is divergent, then $\int_a^\infty f(x) \ dx$ s divergent.

_**Be careful:**_ the opposite is not necessarily true: If $\int_a^\infty g(x) \ dx$ is convergent, $\int_a^\infty f(x) \ dx$ may or may not be convergent, and if $\int_a^\infty f(x) \ dx$ is divergent, $\int_a^\infty g(x) \ dx$ may or may not be divergent.

## II. Exercises

* Determine if $\displaystyle \int_1^\infty \frac{2+e^{-x}}{x} \ dx$ is convergent or divergent.
  
We have:

$$
0 < \frac{1}{x} < \frac{2+e^{-x}}{x}, \forall x \geq 1
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

* Determine if $\displaystyle \int_0^\infty \frac{\arctan x}{2+e^x} \ dx$ is convergent or divergent.
  
Observe that $-\dfrac{\pi}{2} \leq \arctan x \leq \dfrac{\pi}{2}$, so

$$
0 \leq \frac{\arctan x}{2+e^x} < \frac{2}{2+e^x} < \frac{2}{e^x}, \forall x \geq 0
$$

$$
\int_0^\infty \frac{2}{e^x} \ dx
=2\lim_{t \to \infty} \int_0^t e^{-x} \ dx
=2\lim_{t \to \infty} \left[-e^{-x}\right]_0^t
=2\lim_{t \to \infty} (1-e^{-t}) = 2
$$

By the Comparison Test, $\displaystyle \int_0^\infty \frac{\arctan x}{2+e^x} \ dx$ is convergent

* Find the values of $p$ for which the integral converges or diverges and evaluate the integral for those values of $p$ if it is convergent

$$
I = \int_0^1 x^p \ln x \ dx
$$

**Case 1:** $p=-1$

$$
I = \int_0^1 \frac{\ln x}{x} \ dx
=\lim_{t \to 0^+} \int_t^1 \frac{\ln x}{x} \ dx
=\lim_{t \to 0^+} \left[\frac{\ln^2 x}{2}\right]_t^1
=\lim_{t \to 0^+} \left(-\frac{\ln^2 t}{2}\right)
=-\infty
$$

**Case 2:** $p \neq -1$

$$\begin{align*}
I &= \lim_{t \to 0^+} \int_0^1 x^p \ln x \ dx \\
&=\lim_{t \to 0^+} \left(\left[\frac{x^{p+1}\ln x}{p+1}\right]_t^1-\int_t^1 \frac{x^p}{p+1} \ dx \right) \\
&= \frac{1}{p+1} \lim_{t \to 0^+} \left(\left[x^{p+1}\ln x\right]_t^1-\int_t^1 x^p \ dx \right) \\
&= \frac{1}{p+1} \lim_{t \to 0^+} \left(-t^{p+1}\ln t -\left[\frac{x^{p+1}}{p+1}\right]_t^1\right) \\
&= \frac{1}{p+1} \lim_{t \to 0^+} \left(-t^{p+1}\ln t - \frac{1-t^{p+1}}{p+1}\right) \\
&= \frac{-1}{p+1} \lim_{t \to 0^+} \left(t^{p+1}\ln t + \frac{1-t^{p+1}}{p+1}\right) \\
\end{align*}$$

* **Subcase 1:** $p>-1$

$\displaystyle \lim_{t \to 0^+} \frac{1-t^{p+1}}{p+1}=\frac{1}{p+1}$

$\displaystyle\lim_{t \to 0^+} t^{p+1}\ln t=\lim_{t \to 0^+} \dfrac{\ln t}{t^{-p-1}}\stackrel{\text{L'H}}{=}\lim_{t \to 0^+} \frac{1}{(-p-1)t^{-p-1}}=-\lim_{t \to 0^+} \frac{t^{p+1}}{p+1}=0$

$\displaystyle\therefore I = \frac{-1}{(p+1)^2}$

* **Subcase 2:** $p<-1$

$$\begin{align*}
I&=\frac{-1}{p+1} \left[\frac{1}{p+1} + \lim_{t \to 0^+} \left(t^{p+1} \ln t - \frac{t^{p+1}}{p+1}\right)\right] \\
&=\frac{-1}{p+1} \left[\frac{1}{p+1} + \lim_{t \to 0^+} \left(t^{p+1} \ln t - \frac{t^{p+1}}{p+1}\right)\right] \\
&=\frac{-1}{p+1} \left[\frac{1}{p+1} + \lim_{t \to 0^+} \left(t^{p+1} \left(\ln t - \frac{1}{p+1}\right)\right)\right] \\
\end{align*}$$

Observe that

$\displaystyle\lim_{t \to 0^+} t^{p+1} = \infty$

$\displaystyle \lim_{t \to 0^+} \left(\ln t - \frac{1}{p+1}\right)= -\infty$

So

$$\begin{align*}
I&=\frac{-1}{p+1} \left[\frac{1}{p+1} + (-\infty)\right]=\infty \\
\end{align*}$$

**Summary:**

* $p>-1$ $\Rightarrow \mathrm{I}$ converges at $\dfrac{-1}{(p+1)^2}$
* $p \leq -1$ $\Rightarrow \mathrm{I}$ is divergent
---
layout: post
title: Note 12 - 14/04/2023
parent: Calculus II
grand_parent: Semester I
nav_order: 13
---

{% include toc.md %}

## I. Power Series

A **power series** is a series of the form:

$$
\sum_{n=0}^\infty c_nx^n=c_0+c_1x+c_2x^2+c_3x^3+\ldots
$$

More generally, a series of the form

$$
\sum_{n=0}^\infty c_n(x-a)^n=c_0+c_1(x-a)+c_2(x-a)^2+c_3(x-a)^3+\ldots
$$

is called **power series in $(x-a)$** or a **power series centered at $a$** or a **power series about $a$**.

### Theorem

For a given power series $\sum_{n=0}^\infty c_n(x-a)^n$ there are only three possibilities:
1. The series converges only when $x=a$.
2. The series converges for all $x$.
3. There is a positive  number $R$ such that the series converges if $\vert x-a \vert < R$ and diverges if $\vert x-a \vert > R$

The number $R$ is called the **radius of convergence** of the power series.

In general, the Ratio Test (or sometimes the Root Test) should be used to determine the radius of convergence $R$. The Ratio Test and Root Test always fail when $x$ is an endpoint of the interval of convergence, so the endpoints must be checked with some other test.

### Example

_Find the radius of convergence and interval of convergence of the series_

a. $\sum_{n=0}^\infty (-1)^nnx^n$

The given power series is centered at $a=0$. Let $a_n=(-1)^nnx^n$ then

$$
\lim_{n \to \infty} \left\vert \frac{a_{n+1}}{a_n} \right\vert=\lim_{n \to \infty} \left\vert \frac{(-1)^{n+1}(n+1)x^{n+1}}{(-1)^nnx^n} \right\vert = \lim_{n \to \infty}  \frac{n+1}{n} \vert x \vert = \vert x \vert
$$

By the Ratio Test, we have:
* The series converges iff $\vert x \vert < 1$
* The series diverges iff $\vert x \vert > 1$

$\Rightarrow$ The radius of convergence is $R=1$

However, we should check if $\vert x \vert=1$ then the power series converges or diverges.

* $x=1$ then the power series $\sum_{n=0}^\infty a_n=\sum_{n=0}^\infty (-1)^nn$ is divergent by using the Alternating Series Test.
* $x=-1$ then the power series $\sum_{n=0}^\infty a_n=\sum_{n=0}^\infty n$ is divergent by using the Test for Divergence.

Hence, the interval of convergence is $I=(-1,1)$

b. $\sum_{n=0}^\infty \dfrac{(-3)^nx^n}{\sqrt{n+1}}$

The provided power series is centered at $a=0$. Let $a_n=\dfrac{(-3)^nx^n}{\sqrt{n+1}}$ then

$$
\lim_{n\to\infty} \left\vert \frac{a_{n+1}}{a_n} \right\vert = \lim_{n\to\infty} \left\vert \frac{(-3)^{n+1}x^{n+1}}{\sqrt{n+2}} \cdot \frac{\sqrt{n+1}}{(-3)^nx^n} \right\vert = 3\lim_{n\to\infty} \sqrt{\frac{n+1}{n+2}} \vert x \vert = 3\vert x \vert
$$

By the Ratio Test, we have:
* The series converges iff $3\vert x \vert<1$
* The series converges iff $3\vert x \vert>1$

So $\vert x \vert < \dfrac{1}{3} \Rightarrow$ The radius of convergence is $R=\dfrac{1}{3}$

However, we should check if $\vert x \vert = \dfrac{1}{3}$ then the power series converges or diverges.
* $x=\dfrac{1}{3}$ then $\sum_{n=0}^\infty a_n = \sum_{n=0}^\infty \dfrac{(-1)^n}{\sqrt{n+1}}$ is convergent by using the Alternating Series Test.
* $x=-\dfrac{1}{3}$ then $\sum_{n=0}^\infty a_n = \sum_{n=0}^\infty \dfrac{1}{\sqrt{n+1}}$ is divergent by using the Integral Test.

Hence, the interval of convergence is $I=\left(-\dfrac{1}{3},\dfrac{1}{3}\right]$

## II. Taylor and Maclaurin Series

Suppose that $f$ is any function that can be represented by a power series

$\displaystyle f(x)=c_0+c_1(x-a)+c_2(x-a)^2+c_3(x-a)^3+c_4(x-a)^4+\cdots \ \ \ \ \ \vert x-a \vert < R$

Subtitute $x=a$ into the above equation and we get

$$
f(a)=c_0
$$

We can differentiate the series term by term:

$\displaystyle f'(x)=c_1+2c_2(x-a)+3c_3(x-a)^2+4c_4(x-a)^3+\cdots \ \ \ \ \ \vert x-a \vert < R$

Again we put $x=a$ in the above equation. The result is

$$
f'(a)=c_1
$$

By now you can see the pattern. If we continue to differentiate and subtitute $x=a$, we obtain

$$
f^{(n)}(a)=2\cdot3\cdot4\cdots nc_n=n!c_n
$$

So

$$
c_n=\frac{f^{(n)}(a)}{n!}
$$

Thus we have proved the following theorem

### Theorem

If $f$ has a power series representation (expansion) at $a$, that is, if

$$
f(x)=\sum_{n=0}^\infty c_n(x-a)^n \ \ \ \ \ \ \ \vert x-a \vert < R
$$

then its coefficients are given by the formula

$$
c_n=\frac{f^{(n)}(a)}{n!}
$$

### Taylor series

$$\begin{align*}
f(x)&=\sum_{n=0}^\infty \frac{f^{(n)}(a)}{n!} (x-a)^n \\
&=f(a)+\frac{f'(a)}{1!}(x-a)+\frac{f''(a)}{2!}(x-a)^2+\frac{f'''(a)}{3!}(x-a)^3+\cdots
\end{align*}$$

Taylor series of the function $f$ at $a$ (or about $a$ or centered at $a$).

For the special case $a=0$ the Taylor series becomes Maclaurin series.

### Maclaurin series

$$
f(x)=\sum_{n=0}^\infty \frac{f^{(n)}(0)}{n!} x^n 
=f(0)+\frac{f'(0)}{1!}x+\frac{f''(0)}{2!}x^2+\frac{f'''(0)}{3!}x^3+\cdots
$$

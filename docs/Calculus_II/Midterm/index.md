---
layout: post
title: Midterm Review
parent: Calculus II
nav_order: 7
---

{% include toc.md %}

## I. Sketch the solid

## II. Find the volume of a solid

### 1. Definition of volume:

Let $S$ be a solid that lies between $x=a$ and $x=b$. If the cross-sectional area of $S$ in the plane $P_x$, through $x$ and perpendcular to the $x$-axis, is $A(x)$, where $A$ is a continous function, then the **volume** of $S$ is:

$$
V=\displaystyle\lim_{n \to \infty} \sum_{i=1}^n A(x_i^*) \Delta x = \int_a^b A(x) dx
$$

### 2. Several formulas:

* Disk method: $y=f(x)$, $a \leq x \leq b$, rotate about the $x$-axis

$$
V=\int_a^b \pi \left[f(x)\right]^2 \ dx
$$

* Shell method: $y=f(x)$, $a \leq x \leq b$, rotate about the $y$-axis

$$
V=\int_a^b 2\pi xf(x) \ dx
$$

## III. Polar curves

### 1. Sketch the curve:

* Lines
  * $\theta=\alpha \ \ \ \ \$ The line from $(0,0)$ set at the angle $\alpha$
  * $r\cos\theta=a \ \ \ \ \$ The vertical line through $x=a$
  * $r\sin\theta=b \ \ \ \ \$ The horizontal line through $y=b$
* Circles
  * $r=a \ \ \ \ \$ The circle centered at $(0,0)$ with radius $a$
  * $r=2a\cos\theta \ \ \ \ \$ The circle centered at $(a,0)$ with radius $\vert a \vert$
  * $r=2b\sin\theta \ \ \ \ \$ The circle centered at $(0,b)$ with radius $\vert b \vert$
  * $r=2a\cos\theta+2b\sin\theta \ \ \ \ \$ The circle centered at $(a,b)$ with radius $\sqrt{a^2+b^2}$

If we are given other form, we should investigate the function $r=f(\theta)$, which means calculating derivative, critical point, ..., in order to have enough infomation for drawing the curve accurately.

### 2. Area:

The formula for the area $A$ of the polar region of the curve $r=f(\theta)$, $a \leq \theta \leq b$, is:

$$
A=\int_a^b \frac{1}{2} r^2 d\theta
$$

## IV. Length of a curve

### 1. Cartesian coordinates:

If $f'$ is continuous on $[a,b]$, then the length of the curve $y=f(x)$, $a \leq x \leq b$, is:

$$
L=\int_a^b \sqrt{1+[f'(x)]^2} \ dx
$$

### 2. Polar coordinates:

If $f'$ is continuous on $[a,b]$, then the length of the curve $r=f(\theta)$, $a \leq \theta \leq b$, is:

$$
L=\int_a^b \sqrt{r^2 + \left(\frac{dr}{d\theta}\right)^2} \ d\theta
$$

## V. The fundamental theorem of Calculus

### 1. Part 1:

If $f$ is continuous on $[a,b]$, then the function $g$ defined by
   
$$
g(x)=\int_a^x f(t) \ dt \ \ \ \ \ \ a \leq x \leq b
$$

is continuous on $[a,b]$ and differentiable on $(a,b)$, and $g'(x)=f(x)$.

### 2. Part 2:

If $f$ is continuous on $[a,b]$, then

$$
\int_a^b f(x) \ dx = F(b)-F(a)
$$

where $F$ is any antiderivative of $f$, that is, a function such that $F'=f$.
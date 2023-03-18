---
layout: post
title: Midterm Review
parent: Calculus II
nav_order: 7
---

{% include toc.md %}

## I. Sketch the solid

## II. Find the volume of a solid

## III. Polar curves

## IV. Length of a curve

### * Cartesian coordinates:

If $f'$ is continuous on $[a,b]$, then the length of the curve $y=f(x)$, $a \leq x \leq b$, is:

$$
L=\int_a^b \sqrt{1+[f'(x)]^2} \ dx
$$

### * Polar coordinates:

If $f'$ is continuous on $[a,b]$, then the length of the curve $r=f(\theta)$, $a \leq \theta \leq b$, is:

$$
L=\int_a^b \sqrt{r^2 + \left(\frac{dr}{d\theta}\right)^2} \ d\theta
$$

## V. The fundamental theorem of Calculus

### * Part 1:

If $f$ is continuous on $[a,b]$, then the function $g$ defined by
   
$$
g(x)=\int_a^x f(t) \ dt \ \ \ \ \ \ a \leq x \leq b
$$

is continuous on $[a,b]$ and differentiable on $(a,b)$, and $g'(x)=f(x)$.

### * Part 2:

If $f$ is continuous on $[a,b]$, then

$$
\int_a^b f(x) \ dx = F(b)-F(a)
$$

where $F$ is any antiderivative of $f$, that is, a function such that $F'=f$.
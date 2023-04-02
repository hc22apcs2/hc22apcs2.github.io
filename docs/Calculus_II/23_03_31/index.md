---
layout: post
title: Note 9 - 31/03/2023
parent: Calculus II
nav_order: 10
---

{% include toc.md %}

## I. Seperable Equations
A **seperable equation** is a first-order differential equation whose expression for $dy/dx$ can be factored as a function of $x$ times a function of $y$. In other word, it can be written in the form

$$
\frac{dy}{dx} = g(x) f(y)    
$$

The name _seperable_ comes from the fact that the expression on the right side can be "seperated" into a function of $x$ and a function of $y$. Equivalently, if $f(y)\neq0$, it can be written as such

$$
\frac{dy}{dx}=\frac{g(x)}{h(y)}
$$

where $h(y)=1/f(y)$. To solve this equation we rewrite it in the differential form

$$
h(y) \ dy = g(x) \ dx
$$

Then we integrate both sides of the equation

$$
\int h(y) \ dy = \int g(x) \ dx
$$

The above equation defines $y$ implicitly as a function of $x$. In some cases, we may be able to solve for $y$ in terms of $x$.

**Note:** Proof that the following statement is true

$$
h(y) \ dy = g(x) \ dx \iff \int h(y) \ dy = \int g(x) \ dx
$$

Based on the expression on the left, we can derive that the esxpression ont he right is true, but we have to consider the reverse one.

We use the Chain Rule and the Fundamental Theorem of Calculus to justify this procedure

$$
\frac{d}{dx}\left(\int h(y) \ dy\right)=\frac{d}{dx}\left(\int g(x) \ dx\right)
$$

so

$$
\frac{d}{dy}\left(\int h(y) \ dy\right)\frac{dy}{dx}=g(x)
$$

and

$$
h(y) \frac{dy}{dx} = g(x)
$$

Thus the given statement is true.

**Be careful:** $f(y)$ must not equal zero.

## II. Orthogonal Trajectories
An **orthogonal trajectory** of a family of curves is a curve that form a right angle with each curve of the family orthogonally.

**Example:**

Find the orthogonal trajectories of the family of curves

$$
y=\frac{k}{x}
$$

We have: $\displaystyle \frac{dy}{dx}=-\frac{k}{x^2}=-\frac{xy}{x^2}=-\frac{y}{x}$

This means that the slope of the tangent line at any point $(x,y)$ on one of the curve is $y'=-y/x$. On an orthogonal trajectory the slope of the tangent line must be the negative reciprocal of this slope. Therefore the orthogonal trajectories must satisfy the differential equation

$$
\frac{dy}{dx}=\frac{x}{y}
$$

This differential equation is seperable, and we solve it as follows:

$$
\int y \ dy=\int x \ dx
$$

$$
\frac{y^2}{2}=\frac{x^2}{2}+C
$$

$$
x^2-y^2=C
$$

where $C$ is an arbitary constant.

## III. Sequences
A **sequence** can be thought of a list of numbers written in a definite order:

$$
a_1, a_2, a_3, ..., a_n, ...
$$

**NOTATION** The sequence $\{a_1,a_2,a_3,...\}$ is denoted by

$$
\{a_n\} \ \ \ \ \text{or} \ \ \ \ \{a_n\}_{n=1}^{\infty}
$$

$\{a_n\}$ is bounded below iff $\exists \ m \in \mathbb{R}$ s.t $m<a_n$, $\forall n$

$\{a_n\}$ is bounded above iff $\exists \ M \in \mathbb{R}$ s.t $a_n<M$, $\forall n$
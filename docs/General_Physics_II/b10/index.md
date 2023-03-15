---
layout: post
title: Physics II - B10
parent: General Physics II
---
*Proofread by Huỳnh Hà Phương Linh*

{% include toc.md %}

## Electromotive force (Suất điện động)

$$
\xi = emf \,\ (volt)
$$

## Internal Battery Resistance
<img src = "CS6AHpT.png" width = 500 height = 300>

$$
\Delta V = \xi - I.r
$$

$$
I = \frac{\xi}{R+r}
$$

$$
\Delta V = R.\frac{\xi}{R+r}
$$

$$
P = I.\xi = I^2.(R+r)
$$

## Load Resistance
<img src = "EpELEBT.png" width = 800 height = 200>

## Combination of resistors
### In Series:
<img src = "fJmYUE1.png" width = 400 height = 300>

$$
I_1 = I_2 = I
$$

$$
\Delta V = \Delta V_1 + \Delta V_2
$$

$$
R = R_1 + R_2
$$

### In parallel:
<img src = "oSZLuFO.png" width = 400 height = 400>

$$
\Delta V_1 = \Delta V_2 = \Delta V
$$

$$
I = I_1 + I_2
$$

$$
\frac{1}{R} = \frac{1}{R_1} + \frac{1}{R_2}
$$

## Kirchhoff’s Rules
* **Juntion rule:** $\sum I_{in} = \sum I_{out}$
* **Loop rule:** $\sum \Delta V = 0$

![](neFNCkr.png)

## RC Circuit
<img src = "3iP6aA5.png" width = 400 height = 300>

* **Loop Rule:**

$$
\xi - \frac{Q}{C} - R.i = 0
$$

$$
\xi - \frac{Q}{C} - R.\frac{dQ}{dt} = 0
$$

$$
\xi - \frac{Q}{C} = R\frac{dQ}{dt}
$$

$$
\xi C - Q = RC\frac{dQ}{dt}
$$

$$
\displaystyle \int_0^t \frac{-dt}{RC} = \int_0^q \frac{dQ}{Q - \xi C}
$$

$$
\ln(\frac{q-C\xi}{-C\xi}) = -\frac{t}{RC}
$$

<span style="color: red">**Notes:**<br>
$q(t) = \xi.C(1-e^{\frac{-t}{RC}}) = Q_{max}.(1-e^{\frac{-t}{RC}})$ <br>
$i(t) = \frac{dQ}{dt} = \frac{\xi}{R}.e^{\frac{-t}{RC}}$<br>
$\tau = RC (s):$ **time constant**</span>

## Other references
* [MIT Physics 2](https://www.youtube.com/playlist?list=PLyQSN7X0ro2314mKyUiOILaOC2hk6Pc3j)
* [Michel van Biezen](https://www.youtube.com/playlist?list=PLX2gX-ftPVXX7BZOcM1Y2gb8IQrTBrmUB)
* [Khan Academy](https://www.khanacademy.org/science/in-in-class-12th-physics-india)
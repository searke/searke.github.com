---
layout: post
title: The Method of Frobenius
---

# Some Examples of the Method of Frobenius
-----
## Motivation

Some differential equations have solutions that we can describe as power series. This is the case for many of the differential equations which define the "special" functions from applied math like the Bessel or Lengendre functions. The method of frobenius works by assuming that the solutions to these equations take the form of an infinite power series. After this, a lot of algebra is done to find the solution. 

Fortunately, computer algebra makes this significantly less error prone and tedious and expands the scope of problems where the use of this method is feasible.   

## Overview

As a first step, assume that the function, say \\(f\\), which satifies the equation has the form:

$$ f(x) = \sum \_{i=0}^{\infty} a(i)\,x^{i} $$

Here\\(a(i)\\) is ith coefficient of the power series. Our goal is to find a definition for \\(a(i)\\) for each \\(i\\).

To do this, replace \\(f\\) with the sum. In many cases, we can rearrange the equation in a way to solve for the values of \\(a(i)\\).

-----
## A Simple Differential Equation
Consider this basic differential equation:

$$ \frac{\partial y(x)}{\partial x}+y(x)=0 $$ 

Replacing \\(y(x)\\) with \\(\sum \_{i=0}^{\infty} a(i)\, x^i\\) gives us this equation:

$$\sum \_{i=0}^{\infty } i\, a(i) \, x^{i-1}+\sum \_{i=0}^{\infty } a(i) \, x^i = 0 $$

Combine all the summations together. This requires playing with the index of summation.

$$ \sum \_{i=0}^{\infty } (i+1)\, a(i+1)\, x^{i}+\sum \_{i=0}^{\infty } a(i) \, x^i = 0 $$

$$ \sum \_{i=0}^{\infty } ((i+1)\, a(i+1)\,+ a(i))\, x^i = 0 $$

Each coefficient of the power series must be equal to zero because the power series is equal to zero. So we have for each \\(i\\):

$$ (i+1)\, a(i+1)\,+ a(i) = 0 $$

Giving us the reccurence relation: $$ a(i+1) = - \frac{a(i)}{i+1} $$

This reccurence relation is solvable and the formula for the ith coefficient is:

$$ a(i) = (-1)^{i-1} \frac{-a(0)}{i!} $$

So, the function satisfying the differential equation is equal to this infinite summation:

$$ \sum \_{i=0}^{\infty } (-1)^{i-1} \frac{-a(0)}{i!}\,x^i $$

If we evaluate the infinite sum, we find the solution to the differential equation:

$$ a(0)\, e^{-x} $$

## A Harder Differential Equation

$$ y'(x)+y(x)+\cos (x)=0 $$

To solve this, it is important to have \\(cos\\) expression as a Taylor series.

$$ \cos (x) = \sum \_{n=0}^{\infty } \frac{(-1)^n\, x^{2 n}}{(2 n)!} $$

$$ \sum \_{n=0}^{\infty } \frac{(-1)^n \, x^{2 n}}{(2 n)!}+\sum
   \_{n=0}^{\infty } n\, x^{n-1}\, a(n)+\sum \_{n=0}^{\infty } x^n\, a(n) = 0$$

A fair amount of work must be done to get each summation into the proper form. They must all sum over \\(x^n\\) instead of \\(x^{n-1}\\) and \\(x^{2n}\\).

$$ \sum \_{n=0}^{\infty } \frac{((n+1) \bmod 2)\, (-1)^{n/2}
  }{n!} x^n +\sum \_{n=0}^{\infty } (n+1)\, (n)\, x^n +\sum
   \_{n=0}^{\infty } a(n) \ x^n =0 $$

$$ \sum \_{n=0}^{\infty } (\frac{((n+1) \bmod 2)\, (-1)^{n/2}
  }{n!} + (n+1)\, (n)+ a(n)) \, x^n =0 $$

All the coefficients must equal zero for all \\(n\\).

$$ \frac{((n+1) \bmod 2)\, (-1)^{n/2}}{n!}+(n+1)\, a(n+1)+a(n)=0 $$

Solve for \\(a(n+1)\\) to get a reccurence relation.

$$ a(1) = -1 $$

$$ a(n+1)=\frac{-a(n)\, n!\, -i^n \,((n+1) \bmod 2)}{(n+1)\, n!} $$

The reccurence relation has a closed form.

$$ a(n) = \frac{\left(\frac{1}{4}-\frac{i}{4}\right) (-1)^n
   \left(e^{-\frac{1}{2} i \pi  n}+i e^{\frac{i \pi 
   n}{2}}+(-1-i)\right)}{n!}$$

The result sum has a closed form as well.

$$ \sum \_{n=0}^{\infty } a(n)\,x^n = -\frac{1}{2} e^{-x} \left(e^x \sin (x)+e^x \cos (x)-1\right) $$

## A Functional Equation

This method allows works on some simple functional equations like the one below. 

$$ f(x) + f(2x) = \sin(x) $$

Replace \\(f\\) with an infinite sum and replace \\(sin\\) with a Taylor series. Then combine them all.

$$ \sum \_{n=0}^{\infty } a(n) \, x^n+\sum \_{n=0}^{\infty } a(n) \, 2^n
   \, x^n- \sum \_{n=0}^{\infty } \frac{(n \bmod 2)\, (-1)^{\frac{n+1}{2}+1}\,
   x^n}{n!} $$

The coefficients must be equal to zero as always.

$$ a(n)+2^n a(n)-\frac{(-1)^{1+\frac{1+n}{2}} \, (n \bmod 2)}{n!}=0 $$

$$ a(n)=\frac{(-1)^{1+\frac{1+n}{2}} \, (n \bmod 2)}{\left(1+2^n\right)\, n!} $$


$$ f(x) = \sum \_{n=0}^{\infty } \frac{\left((-1)^{1+\frac{1+n}{2}}\, (n \bmod
   2)\right)}{\left(1+2^n\right)\, n!} x^n $$

To simplify things, subsitute \\(n = 2k+1 \\)  and simplify:

$$ f(x) = \sum \_{k=0}^{\infty } \frac{(-1)^k\, x^{2 k+1}}{\left(1+2^{2
   k+1}\right)\, (2 k+1)!} $$

There doesn't appear to be any way I know of to simplify this equation.

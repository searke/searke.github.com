---
layout: post
title: The Method of Frobenius
---

# Some Examples of the Method of Frobenius
-----
## Motivation

The method of Frobenius is a powerful tool for solving differntial and functional equations. Many of the "special" functions from applied math like the Bessel or Lengendre functions are defined as a differential equation and then solved using the method. It works by assuming that the solutions are an infinite power series which reduces the problem down to algebra or solving a reccurence relation. 

Solving the resulting algebraic equation or reccurence relation can be tedious. Fortunately, computer algebra systems make using this method less error prone and less painful.

## Overview

As a first step, assume that the function we wish to solve for, say \\(f\\), has the form:

$$ f(x) = \sum \_{i=0}^{\infty} a(i)\,x^{i} $$

Here, \\(a(i)\\) is ith coefficient of the power series. We must define \\(a(i)\\) for each \\(i\\) so that f solves the equation.

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

Finally, we plug this back into the infinite summation:

$$ y(x) = \sum \_{i=0}^{\infty } (-1)^{i-1} \frac{-a(0)}{i!}\,x^i $$

If we evaluate the infinite sum, we find the solution to the differential equation:

$$ y(x) = a(0)\, e^{-x} $$

## A Slightly Harder Differential Equation

$$ y'(x)+y(x)+\cos (x)=0 $$

To solve this, it is important to write \\(cos(x)\\) as a Taylor series and do some algebra with it.

$$ \cos (x) = \sum \_{n=0}^{\infty } \frac{(-1)^n\, x^{2 n}}{(2 n)!} $$

$$ \sum \_{n=0}^{\infty } \frac{(-1)^n \, x^{2 n}}{(2 n)!}+\sum
   \_{n=0}^{\infty } n\, x^{n-1}\, a(n)+\sum \_{n=0}^{\infty } x^n\, a(n) = 0$$

To combine the summations together, they must all sum over \\(x^n\\) instead of \\(x^{n-1}\\) and \\(x^{2n}\\).

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

Putting this into the infinite sum, we can get a closed form as well.

$$ \sum \_{n=0}^{\infty } a(n)\,x^n = -\frac{1}{2} e^{-x} \left(e^x \sin (x)+e^x \cos (x)-1\right) $$

## A Functional Equation

This method also works on some functional equations like the one below. 

$$ f(x) + f(2x) = \sin(x) $$

Replace \\(f\\) with an infinite sum and replace \\(sin\\) with a Taylor series. Then combine them all.

$$ \sum \_{n=0}^{\infty } a(n) \, x^n+\sum \_{n=0}^{\infty } a(n) \, 2^n
   \, x^n- \sum \_{n=0}^{\infty } \frac{(n \bmod 2)\, (-1)^{\frac{n+1}{2}+1}\,
   x^n}{n!} =0 $$

The coefficients must be equal to zero as always.

$$ a(n)+2^n a(n)-\frac{(-1)^{1+\frac{1+n}{2}} \, (n \bmod 2)}{n!}=0 $$

$$ a(n)=\frac{(-1)^{1+\frac{1+n}{2}} \, (n \bmod 2)}{\left(1+2^n\right)\, n!} $$


$$ f(x) = \sum \_{n=0}^{\infty } \frac{\left((-1)^{1+\frac{1+n}{2}}\, (n \bmod
   2)\right)}{\left(1+2^n\right)\, n!} x^n $$

To simplify things, subsitute \\(n = 2k+1 \\)  and simplify:

$$ f(x) = \sum \_{k=0}^{\infty } \frac{(-1)^k\, x^{2 k+1}}{\left(1+2^{2
   k+1}\right)\, (2 k+1)!} $$

This equation doesn't simplify like the others, but this formula may provide useful numerical approximation.

## Why Does This Work?

Short Answer: \\(x^i\\) is the eigenfunction of the operators used the equations used in this article.

In the differential equations, we had the differential operator - let's call it D:  \\(D(y(x)) = \frac{\partial y(x)}{\partial x}\\). In the functional equations we had a "halving" operator, let's call it H: \\(H(y(x)) = y(x/2)\\). Rewriting the equations using these operators, we get:

$$ D(y(x))+y(x)=0 $$

$$ D(y(x))+y(x)+\cos(x)=0 $$

$$ f(x) + H(f(x)) = \sin(X) $$

Both of these are linear operators. One of the key take-aways from linear algebra is that linear things are good because they are easy to work with. Linear operators are just like linear functions except that they operate on functions instead of vectors or numbers. Linear operators have eigenfunctions which are defined in same way as eigenvectors are defined for matrices. An operator, \\(O\\), has an eigenfunction, \\(f\\) if we can find applying the operator to the function preserves the function and just multiplies by some value called the eigenvalue, \\(a\\):

$$ O(f(x)) =  a \\(f(x)\\)

Both of or operators, \\(D\\) and \\(H\\), have \\(x^i\\) as eigenfucntions for values of x^i.

$$ D(x^i) = i x^i $$
$$ H(x^i) = \frac{1}{2}^i x^i $$

This fact allows all the previous examples to work. If we can respresent the answer as a summation using \\(x^i\\), then we will be able to get rid of all the \\(x\\) values as we did in the example and convert the differential or functional equation into an algebra problem. 

Thanks to the fact that \\(D\\) and \\(H\\) are linear, we can nest and compose them together and \\(x^i\\) will still be an eigenfunction.

This is why decomposing a function into a sum with \\(x^i\\) is useful, but are there any other useful ways to decompose functions?

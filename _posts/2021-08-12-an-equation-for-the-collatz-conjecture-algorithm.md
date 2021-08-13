---
layout: default
title: "An Equation for the Collatz conjecture algorithm"
description: "I found a way to represent collatz conjecture as an equation"
date: 2021-08-12 16:15:00 +0530
categories: algorithm maths CS
usemathjax: true
---

today i found a way to represent the collatz conjecture(which was an algorithm till now) as an equation.

if we define $y$ in terms of $x$, the initial value of the Collatz conjecture algorithm:

<div>
$$ x = 2^p \cdot y $$

where $p$ is a whole number, and $y$ is a positive integer
</div>

then, we can represent Collatz conjecture as:

<div>
$$ 3^n \cdot 2 ^ {1 + \sum_{i=0}^{n} a_i} \cdot (3y + 1) = 2^k, a \in \mathbb{Z}^n $$

where $k$ and $n$ are positive integers, and $a_0 := p$
</div>

(I am too lazy to document how i got there, but i will expand it in the following days).

now the only thing left is to prove that this equation holds true for any $x$.


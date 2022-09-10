---
layout: default
title: "An Equation for the Collatz conjecture algorithm"
description: "I found a way to represent collatz conjecture as an equation"
date: 2021-08-12 16:15:00 +0530
categories: algorithm maths CS
usemathjax: true
---

today i found a way to represent the collatz conjecture(which was an algorithm till now) as an equation.

if we define $y$ in terms of $x \in \mathbb{N}$, the initial value of the Collatz conjecture algorithm:

<div>
$$ x = 2^p \cdot y $$
</div>
where,  
    $ p \in \mathbb{N}_0 $,  
    $ y \in \mathbb{N} $  

then, we can represent Collatz conjecture as:

<div>
$$ 3^n x + \displaystyle \sum_{i=0}^n{3^i \cdot 2^{\sum_{j=0}^{n-i-1} a_j}} = 2^k $$

</div>
where,  
    $ a \in \mathbb{N}_0^n $,  
    $ n \in \mathbb{N} $,  
    $ k \in \mathbb{N} $,  
    $ a_0 := p $  

(I am too lazy to document how i got there, but i will expand it in the following days).

now the only thing left is to prove that this equation holds true for any $x$.


---
layout: default
title: "An Equation for the Collatz conjecture algorithm"
description: "I found a way to represent collatz conjecture as an equation"
date: 2021-08-12 16:15:00 +0530
categories: algorithm maths CS
---

today i found a way to represent the collatz conjecture(which was an algorithm till now) as an equation:

{% raw %}

$$ 3^n \cdot 2 ^ {1 + \sum_{i=0}^{n} a_i} \cdot (3y + 1) = 2^k $$

where \(a_0\) is a whole number, and \(a_1, a_2, ... a_n\), \(k\), and \(2^a_0 \cdot y = x\) are positive integers.

{% endraw %}

(I am too lazy to document how i got there, but i will expand it in the following days).

now the only thing left is to prove that this equation holds true for any `\(x\)`.


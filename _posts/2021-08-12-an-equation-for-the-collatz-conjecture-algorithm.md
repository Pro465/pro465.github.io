---
layout: default
title: "An Equation for the Collatz conjecture algorithm"
description: "I found a way to represent collatz conjecture as an equation"
date: 2021-08-12 16:15:00 +0530
categories: algorithm maths CS
usemathjax: true
---

today i found a way to represent the collatz conjecture(which was an algorithm till now) as an equation:
{% raw %}
$$3^n\cdot x + \displaystyle\sum_{i=0}^{n}{3^i \cdot 2^{\sum_{j=n}^{n - i - 1} a_j}}= 2^k$$
where <math>a_0</math> is a whole number, and <math>a_1, a_2, ... a_n</math>, <math>k</math>, and <math>x</math> are positive integers.
{% endraw %}

(I am too lazy to document how i got there, but i will expand it in the following days).

now the only thing left is to prove that this equation holds true for any <math>x</math>.

---
layout: post
title: "An Equation for the Collatz conjecture algorithm"
date: 2021-08-12 16:15:00 +0530
categories: algorithm maths CS
usemathjax: true
---

<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML"></script>
<math>3^n\cdot x + \displaystyle\sum_{i=0}^{n}{3^i \cdot 2^{\sum_{j=n}^{n - i - 1} a_j}}= 2^k</math>

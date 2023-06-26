---
layout: default
title: "what is the yin and yan of computation?"
description: "does duplication and deduplication qualify?"
date: 2023-06-26 22:12:00 +0530
categories: algorithm maths CS turing-completeness
---

Ever since i saw what the simplest of machines could do, i yearned for the universal simplicity - machines beautifully balancing simplicity with universality, like tightrope artists balancing gravity with reaction forces. 

so when i first discovered [Xeroxer](https://esolangs.org/wiki/Xeroxer), a seemingly easy but upon deeper look non-trivial problem, i quickly was thinking of it day and night, trying to simulate different computational mdels in it. and i succeeded at last, showing that it was one of those i yearned...

the language is quite simple, here is it:
> cpyjmp len, offset | (copy the instructions at the address ip-len..ip (exclusive) to the end of the program, then jump to ip + offset + 1).

basically, every command has two arguments: the first instruction specifying the number of instructions to "repeat" at the end, and the second instruction specifies the number of instructions to skip or ignore. that's it.

and yet, it still is turing complete. in a way, it is the yin and yan of imperative paradigm, and computation in general. duplication and deduplication, like the SK combinators of functional paradigm, or the 1 and 0 in cyclic tag.
it can also be united into one operation, like the goto's of unstructured paradigm, or the while loops of the structured. 

_it all comes down to duplication and deduplication..._

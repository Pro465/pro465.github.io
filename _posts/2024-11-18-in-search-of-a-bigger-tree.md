---
layout: default
title: "In search of a bigger Tree"
description: "i got interested in googology, so here goes"
date: 2024-11-18 22:12:00 +0530
categories: algorithm maths CS googology
usemathjax: true
---

A few weeks ago I got awfully interested in googology, and a few days ago i had invented a new notation to denote large numbers based on trees, so here it is:

# definitions
the trees are labelled, so we need a valid set of labels. the rules for them are given below:

(from Discord@TARDIInsanity)

> A decrement-ordered set is a set $S$ equipped with a partial function $p : S -> S$ such that 
> for every element $s in S$, there exists some whole number $n$ such that $p^n(s)$ is not an element of the domain of $p$.
> 
> Derived from the domain of $p$, the subset $Z$ is defined as $S - D(p)$; the set of elements not in the domain of $p$, here known as the set of "Zero" elements of $S$.
> 
> Also derived from $p$ is a partial ordering on $S$ where we define $Ord(s)$ to be that whole number n such that $p^n(s) \in Z$;
> for all $a,b \in S$, $Ord(a) < Ord(b) \iff a < b$
> 
> A shrink-ordered set is a set $S$ equipped with a partial function $p : S \times \mathbf{N} \to S$ such that for every element $s in S$ and every infinite sequence $a_0,a_1...: a_i \in N$: 
> the sequence defined by the relations $s_{i+1} = p(s_i, a_i); s_0 = s$ is undefined at some finite value of $i$;
> additionally we require that for all $(s,a,b) \in S\times\mathbf{N}\times\mathbf{N}$, $p(s,a)$ is defined iff $p(s,b)$ is defined as well;
> $p$ must either always or never be defined for any argument $s \in S$.
> 
> Like decrement-ordered sets, we derive from the domain of $p$ the subset $Z[S]$ of left-arguments of p for which it is never defined.
> 
> Like decrement-ordered sets, we derive a partial ordering based on p with the formal definition:
> 
> $<$ is the minimal transitive relation in $S^2$ such that for all $s,t \in S$, $s < t$ holds if there exists some $k \in \mathbf{N}$ such that $s = p(t, k)$.
> 
> As a result of the definition of p, $<$ must be antisymmetric; by contradiction: if there existed two elements $s,t \in S$
> such that $s < t$ and $t < s$, then there would exist some infinite repeating sequence $a_i \in \mathbf{N}$ 
> such that the sequence $s_{i+1} = p(s_i, a_i)$ is always defined, by cycling between $s$, $t$, and any necessary intermediate values.
>
> we can derive decrement-ordered sets to be a special case of shrink-ordered sets over infinite repetitions of a single natural number $m$. 
> As a result, elements of the set $S$ can be assigned a somewhat stronger partial order in which every element can be assigned a unique 
> (to the element, but not among all elements, and dependent on the choice of $m$) natural number distance from zero.

Whew! That was a long quotation. Thankfully the rest of the post is short (for now)

The tree set itself is a decrement-ordered set, whose labels are members of a particular decrement-ordered set, and its predecessor function is defined as follows:

```
function replace(t: T, r: T) -> T
    return t but each node's label is replaced by pred_S(root(r))
end

function pred_T(t: T) -> Maybe<T>
    if root(T) in Z: return None
    for each index-child subtree pair (i, c) of t:
        if pred_T(c) is not None:
            t[i] = pred_S(c)
            for each index-child subtree pair (j, c) of t before c (j < i)
                replace each node label in c by pred_T(root(t))
            return t
    let oldtree = replace(t, t)
    let s(n) = the subtree of t (the current one) with the node n as its root
    replace each node of t (starting from the bottom and working towards the top)
    by the tree formed from taking oldtree and replacing its leaves by replace(s(n), t)
    return t
end
```

If the label set is shrink ordered then the tree set is too, with an almost identical pred function, 
except it takes an additional argument and passes it to the pred calls.

# Proofs of the above claims

## notes
since the proof that "the tree set itself is a decrement-ordered set if the label set is decrement-ordered" is trivial, we will skip that 
and instead prove the corresponding statement for the shrink-ordered variant:

We will say "A tree $t$ always terminates" to mean "for every infinite sequence $a_0,a_1...$, $a_i \in \mathbf{N}$: 
there exists a number $k$ s.t. $$root(s_k) \in Z$$, where $s_i$ is a sequence of trees defined by the relations $$s_{i+1} = p(s_i, a_i); s_0 = t$$.", with $p$ 
being the tree set's associated predecessor function.

# actual proof

We will prove the first requirement of shrink-ordered sets holds first:

base case: Any tree $t$ with $root(t) \in Z$ always terminates. By definition of the `pred_T` function.
inductive case: If all trees with labels being $< l$, and $t_1, \cdots, t_n$, always terminate, then so does the tree with $root(t) = l$ 
and children being $t_1, \cdots t_n$.
To see why, take some infinite sequence of natural numbers $a_1, a_2, \cdots$.
Notice that the first child is going to terminate at some fixed $i$. after that, the second child gets decremented 
and all of the first child's nodes are resetted to some value less than $l$, which also terminate after a finite number of steps, by the inductive hyothesis.
So essentially, the second child gets an infinite subseries of the series, with long but finite jumps between each chosen number.
By definition, the second child also must also terminate. and so the third child gets decrement, by a similar reasoning, and so on.
Eventually, all the nodes' labels except the root's transform into members of $Z$, and then it resets the tree in a way that the nodes' labels now become $pred(root(t))$,
which always terminates by the inductive hypothesis.

Now that that's done, We will prove the second requirement holds too:

First, let's take a tree $t$, and let's say `pred_T(t, n)` is undefined for some $n$. The only reason this would happen is if $root(t) \in Z[S]$.
Now let's take another number $m$. then, by definition, `pred_T(t, m)` is still undefined. Since $m$ and $n$ are arbitrary, we can swap them to prove the converse,
thus proving the statement "`pred_T(t, n)` is undefined iff `pred_T(t, m)` is undefined, for all natural numbers $m$ and $n$"


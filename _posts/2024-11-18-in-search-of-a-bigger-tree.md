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

> A decrement-ordered set is a set $S$ equipped with a partial function $p : S \to S$ such that 
> for every element $s \in S$, there exists some whole number $n$ such that $p^n(s)$ is not an element of the domain of $p$.
> 
> Derived from the domain of $p$, the subset $Z[S]$ is defined as $S - D(p)$; the set of elements not in the domain of $p$, here known as the set of "Zero" elements of $S$.
> 
> Also derived from $p$ is a partial ordering on $S$ where we define $Ord(s)$ to be that whole number n such that $p^n(s) \in Z$.
> Then for all $a,b \in S$, $Ord(a) < Ord(b) \iff a < b$
> 
> A shrink-ordered set is a set $S$ equipped with a partial function $p : S \times \mathbb{N} \to S$ such that for every element $s \in S$ and every infinite sequence $a_0,a_1...: a_i \in N$: 
> the sequence defined by the relations $s_{i+1} = p(s_i, a_i); s_0 = s$ is undefined at some finite value of $i$;
> additionally we require that for all $(s,a,b) \in S\times\mathbb{N}\times\mathbb{N}$, $p(s,a)$ is defined iff $p(s,b)$ is defined as well;
> $p$ must either always or never be defined for any argument $s \in S$.
> 
> Like decrement-ordered sets, we derive from the domain of $p$ the subset $Z[S]$ of left-arguments of p for which it is never defined.
> 
> Like decrement-ordered sets, we derive a partial ordering based on p with the formal definition:
> 
> $<$ is the minimal transitive relation in $S^2$ such that for all $s,t \in S$, $s < t$ holds if there exists some $k \in \mathbb{N}$ such that $s = p(t, k)$.
> 
> As a result of the definition of p, $<$ must be antisymmetric; by contradiction: if there existed two elements $s,t \in S$
> such that $s < t$ and $t < s$, then there would exist some infinite repeating sequence $a_i \in \mathbb{N}$ 
> such that the sequence $s_{i+1} = p(s_i, a_i)$ is always defined, by cycling between $s$, $t$, and any necessary intermediate values.
>
> we can derive decrement-ordered sets to be a special case of shrink-ordered sets over infinite repetitions of a single natural number $m$. 
> As a result, elements of the set $S$ can be assigned a somewhat stronger partial order in which every element can be assigned a unique 
> (to the element, but not among all elements, and dependent on the choice of $m$) natural number distance from zero.

Whew! That was a long quotation. Thankfully the rest of the post is short (for now)

The tree set itself is a decrement-ordered set, whose labels are members of a particular decrement-ordered set, and its predecessor function is defined as follows:

```
function releaf(base, template) -> T
  return a copy of base except every leaf is replaced by template
end

function replace(t: T, r: T) -> T
    return t but each node's label is replaced by pred_S(root(r))
end

function replace_with_tree(t: T, r: T) -> T 
    return releaf(r, <t but each child c is replaced by replace_with_tree(c, r)>)
end

function pred_T(t: T) -> Maybe<T>
    if root(T) in Z[T]: return None
    for each index-child subtree pair (i, c) of t:
        if pred_T(c) is not None:
            t[i] = pred_T(c)
            for each index-child subtree pair (j, c) of t before c (j < i)
                t[j]=replace(c, t)
            return t
    t = replace(t, t)
    return replace_with_tree(t, t)
end
```

If the label set is shrink ordered then the tree set is too, with an almost identical pred function, 
except it takes an additional argument and passes it to the pred calls.

# Proofs of the above claims

## notes
since the proof that "the tree set itself is a decrement-ordered set if the label set is decrement-ordered" is trivial, we will skip that 
and instead prove the corresponding statement for the shrink-ordered variant:

We will say "A tree $t$ always terminates" to mean "for every infinite sequence $a_0,a_1...$, $a_i \in \mathbb{N}$: 
there exists a number $k$ s.t. $$root(s_k) \in Z$$, where $s_i$ is a sequence of trees defined by the relations $$s_{i+1} = p(s_i, a_i); s_0 = t$$.", with $p$ 
being the tree set's associated predecessor function.

## actual proof

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

# Example implementation

The following program simulates a tree with label set being $\mathbb{N} \cup {\omega}$ with its predecessor being defined as: 

$$p(\omega, n)=n,$$

$$p(m, n)=m-1, 0<m \in \mathbb{N}.$$

(`-1` in the program represents $\omega$.)

```py
from copy import deepcopy

def map_children(t, f):
    return t[:1]+[f(c) for c in t[1:]]

def reset_label(a, x):
    return [x]+[reset_label(c, x) for c in a[1:]]

def replace_leaves(a, x):
    f=lambda c: replace_leaves(c, x)
    if len(a) == 1: return deepcopy(x)
    else: return map_children(a, f)

def reset_tree(t1, t2):
    f=lambda c: reset_tree(c, t2)
    return replace_leaves(t2, map_children(t1, f))

def pn(a, n):
    if a == 0: return None
    return n if a == -1 else a-1

def p(t, n):
    pred=pn(t[0], n)
    if pred is None: return False
    i=-1
    for j in range(1, len(t)):
        if p(t[j], n):
            i=j
            break
    if i>=0:
        for j in range(1, i):
            t[j]=reset_label(t[j], pred)
    else:
        d=reset_label(t, pred)
        t[:]=reset_tree(d, d)
    return True

n=0
a=[-1, [-1]]
while p(a, n):
    print(a, n)
    n+=1
```

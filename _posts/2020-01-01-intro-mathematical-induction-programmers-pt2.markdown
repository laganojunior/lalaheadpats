---
layout: post
title:  Introduction to mathematical induction for programmers part 2 - Trees, Grids, and the necessity of finite dependencies
date: 2019-11-09 00:00:00 -0700
tags: [math, programming, induction]
math: true
---

In a [previous post](/2019/11/09/intro-mathematical-induction-programmers.html), I wrote up
an overview of the concept of induction as a mathematical proof tool and related it to programming
problems and algorithms. My main point is that induction is not just a way to prove cute
mathematical identities, but rather that:

**Mathematical induction is a method for reasoning about finite dependency structures**

I did some quick examples on problems on arrays, and showed that even on just arrays,
the dependency structures of the recursion are not always just simple linear chains. At the end,
I hinted that dependency structures come up quite often in programming, not just in problems
that deal with just arrays. In fact, in other problems, the dependency structure can be even 
easier to see, such as in problems with trees. So I'll be doing examples with other data
structures here.

Also, I want to highlight the importance of the dependency structure being _finite_. In the
problems I did in the last post, the dependency structures just ended up being finite naturally.
However, infinite dependency structures can come up if we're not careful, often resulting in
an infinite loop or recursion in a program. So I'll show an example where an infinite dependency
structure causes problems.

In the previous post, I mentioned that I wrote it up for my roommate Kevin that was learning
algorithms at the time. Kevin wanted some of these follow-ups that I mentioned in this post.
He also wanted me to somehow incorporate his romantic preferences as a theme for an example.
I'm not quite clever enough to do that, so if you want, just imagine that the numbers are
actually female asian coworker graphic designers [^1].

## Induction on tree structures

Let's start with a hopefully easy problem to understand:

**Problem**: Consider a binary tree of numbers `t`, make a function `tree_depth(t)` that returns
the depth of the tree. (The depth of a tree is the maximum length of a path from the root to
any of the leaves).
**Example**: Consider the tree below.

[^1]:
    The female asian coworker graphic designers should be single and available of course.
    For example, I could prove that he'll date all such people by induction:

    * He will date the first such person
    * If he dates one such person, he will date the next such person

    This isn't exactly a mathematical proof because the concept of "will date" isn't
    a rigorous mathematical statement. But empirical evidence has shown that these rules have
    good support.
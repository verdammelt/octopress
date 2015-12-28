---
layout: post
title: "Software Life Span"
date: 2015-12-28 08:28:18 -0500
comments: true
categories: software maintenance
---

> Software maintenance is an extremely important but highly neglected
> activity.

...says Boehm[^1] in the midst of a long paper about the current and
possible future state of Software Engineering at the end of 1976. I
think this statement is just as true today as it was almost 40 years
ago when Boehm wrote it. 

Boehm defines Software Maintenance as "the process of modifying
existing operational software while leaving its primary functions
intact." (which sounds a lot like what we now call Refactoring). He
states the Maintenance has three main 'functions' which imply certain
needs:

> - Understanding the existing software: This implies the need
>   for...well-structured and well-formatted code
> - Modifying the existing software: This implies the need for software,
>   ..., and data structures which are easy to expand and which minimize
>   side effects of changes...
> - Revalidating the modified software: This implies the need for
>   software structures which facilitate selective retest, and aids for
>   making retest more thorough and efficient.

We have the tools today to do these things. They are things like
modular design, the SOLID principles, and TDD. We have learned ways
to write well-structured code which minimize side effects of changes
and which facilitate retest. We've written languages and libraries
which help us do these things.

But yet maintenance is still a problem.

Perhaps we as an industry are focusing only on the "cool" stuff. Or
believe/hope that "someone else" will maintain it. Or focusing on
immediate customer need and not considering long term needs. The
customer themselves may not consider the long term costs.

As professionals we need to consider the life-span of the code we are
writing, and write it accordingly. If a civil engineer is asked to build
a bridge that need only last for a single crossing it will be quite
different than if the bridge needed to last for decades (or longer).
We need to think in same ways.

Currently we often write software as if it only needs to work for
today. No thought is given to tomorrow.

We have the tools to write software that can live as long as it needs
to. But we need to treat the life-span as a requirement.

---

[^1]: Boehm, B. W. "Software Engineering" *Classics in Software
    Engineering.* Ed. Edward Nash Yourdon. New York: YOURDON
    Press, 1979. pp325-361. Print.

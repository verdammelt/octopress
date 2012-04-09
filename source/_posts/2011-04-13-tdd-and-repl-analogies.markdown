---
layout: post
title: "TDD and REPL analogies?"
date: 2011-04-13 22:44
comments: true
categories: repl tdd
---

*(a half-baked thought)*

In a [previous post][learnedwrong] I realized that to me TDD has a little bit
of the same feel as working in a REPL. When I first learned the technique it
really clicked for me since I always preferred what i referred to as
*exploratory* coding, that is, cycles of trying out little changes and moving
toward the solution of the whole problem.

In a language with a REPL this exploratory coding is pretty normal. It is very
natural to try something, **play** with ideas, and periodically save off the
code you want. Without a REPL and TDD the cycle is slower, which leads to
making larger changes since the cost of small changes is so high. Without a
REPL, but with TDD, the cycles can be kept pretty short: short cycles of unit
tests, longer cycles of integration and end-to-end testing.

So TDD gives one the ability to try out ideas quickly like in a REPL. It is
not as good as a REPL.  Of course TDD has other effects so the fact it is not
a REPL is made up for. But, to me, the benefit of being able to *play* with
ideas, trying lots of things, saving the good and discarding the bad should
not be forgotten.

As an example of this sort of REPL/TDD based play I offer [this video][feathers] 
from Mike Feathers doing the [String Calculator][stringcalc] kata in Haskell.

[learnedwrong]: http://code-and-cocktails.herokuapp.com/blog/2011/04/13/how-i-learned-agile-all-wrong-and-still-ended-up-liking-it/
[feathers]: http://michaelfeathers.typepad.com/michael_feathers_blog/2011/01/the-string-calculator-kata-in-haskell.html
[stringcalc]: http://osherove.com/tdd-kata-1/


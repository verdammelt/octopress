---
layout: post
title: "Clojure Project 'Reloaded' Pattern Gotcha"
date: 2015-03-19 11:04:01 -0400
comments: true
categories: Clojure
---

## Abstract ##

Ensure that `user.clj` does not contain dependencies (even transitive)
upon code that needs to be compiled. This file is loaded well before
Leiningen is started enough to compile files.

## Problem Description ##

In my latest learning project with Clojure I decided to try Stuart
Sierra's Reloaded project pattern[^1]. I liked the idea of this
project pattern because it promised to make the REPL driven
development on a web application smoother. Things were going smoothly
as I worked on simple dummy pages for my little application. However
when I connected the data file parsing code with its custom exception
to the application I started getting compilation and class not found
errors related to the custom exception. The reason for this is a
rather simple one - but was difficult for me to find information on or
figure out.

First an aside about custom exceptions. It seems that in the Clojure
community that custom exceptions are avoided[^2]. Either one of the
built-in Java exceptions, `ex-info`[^3] or Slingshot[^4] is used
instead. However it had been my favored approach to create a
domain-specific exception for my application's needed, so I stumbled
forward and learned how to do it. It was relatively simple by using
the `:gen-class` option of `ns` and the `:aot` feature of Leiningen.
And it worked well... until I connected the code using the exception
with the web application that was implemented in the reloaded pattern.

A big part of the reloaded pattern is the use of functions in
`user.clj` to start and stop the system. This file is loaded by
Clojure whenever it is started[^5] so it is perfect for functionality
wanted in a REPL. This file is kept in a directory which is only
included in the class path when the `dev` profile is used (the `repl`
and `compile` tasks use the `dev` profile by default).

Everything is fine until the code in `user.clj` depends upon (even
transitively) code which must be compiled (such as custom exceptions).
Then we hit a annoying chicken-and-egg problem[^6] wherein Leiningen
when trying to compile (or launch the REPL) naturally starts Clojure,
which in turn loads `user.clj` which in turn depends upon code that
needs to be compiled. The error that is reported says that the
compiled class cannot be found.

## The Confusion ##

This error led me to first think that my custom exception was not
written properly and thus wasn't being compiled, then I thought it was
a problem of the `:aot` feature in Leiningen and interaction with the
`dev` profile. But the problem was more fundamental. It was just my
sort of luck that kept me from finding the answer until I spent hours
debugging and researching. Now it is easy to find several reports of
this problem[^7]. It is not a Leiningen problem, not a Clojure
problem, not a reloaded pattern problem, but an annoyingly unfortunate
interaction between them.

## The Workaround ##

Luckily, once the problem was identified, there is a relatively easy
workaround. I took the parts of `user.clj` which depended upon the
custom exception and moved those to a new file `reloaded.clj` which is
then loaded when the REPL starts by using the `:repl-options`
configuration in `project.clj`. `:repl-options` as a `:init`
configuration which can contain an expression which is evaluated when
the REPL is starting. I set it to `(load "reloaded")`.

---

[^1]: http://thinkrelevance.com/blog/2013/06/04/clojure-workflow-reloaded

[^2]: http://tinyurl.com/o5kn5av

[^3]: https://clojuredocs.org/clojure.core/ex-info

[^4]: https://github.com/scgilardi/slingshot/blob/master/README.md

[^5]: http://dev.solita.fi/2014/03/18/pimp-my-repl.html

[^6]: https://en.wikipedia.org/wiki/Chicken_or_the_egg

[^7]: https://github.com/technomancy/leiningen/issues/1245,
      https://github.com/technomancy/leiningen/issues/1477,
      https://github.com/technomancy/leiningen/issues/1764,
      https://github.com/technomancy/leiningen/issues/1787

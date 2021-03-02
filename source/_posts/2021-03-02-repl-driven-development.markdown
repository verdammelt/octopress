---
layout: post
title: "REPL Driven Development"
date: 2021-03-02 08:15:50 -0500
description: Experience report of REPL driven development.
comments: true
categories: repl, tdd
---

(As I was preparing to write this blog I see that 1) a few other people seem to be discussing around this topic (_e.g._ [David Vujic][test-driven-development-deluxe]), [Erik Engheim][tdd-vs-repl], _et al._) and 2) that *I* already discussed this some 10 years ago [TDD and REPL Analogies?][tdd-repl-analogies]! Just adding this note to make it clear that this is nothing new, just my thoughts and experiences.)

## Background

I am the author/maintainer of an [Exericism][exercism] track for [Common Lisp][common-lisp]. Currently we are doing a big push to prepare and release v3 of the platform. During this push I've been doing more Common Lisp coding than usual[^0] which has brought me back to [REPL][repl] driven development. 

I personally find it very useful to be able to "play around" or explore a problem before sitting down to actual produce a software solution. Sometimes the code, as I explore and play, becomes the "real" code I will keep. Thus this is not a [prototype][prototype] or [spike][spike] where the output would be thrown away, or at least not shipped to production[^1].

At the time of my earlier writing I was working in a language which did not have a strong REPL offering (or any at all) and found TDD to be a way for me to do this exploration in a reasonable fashion. I found, lacking a REPL, TDD provided me a fast feedback cycle which was necessary for my exploratory approach. Having a REPL shortens that feedback cycle for exploration.

## What is REPL Driven development

A REPL with full editing features (such as [SLIME][slime] or [SLY][sly] in [GNU Emacs][gnu-emacs]) combines the power of the language, the power of the editor/IDE, with fast feedback that allows me to explore and play with ideas.

Like TDD, REPL Driven Development/Design lets me experiment with different interface designs of how my modules[^2] will fit together. It also allows me to quickly check that my most recent changes haven' t caused any problem.

I can also use it when I'm unclear on what the solution might even be. For example when consuming a JSON formatted configuration file for my [exercism track][exercism-track-config-file], and I want to better understand how the different parts of the data related to each other, where there may be inconsistencies or lacunae in the data.

The general workflow is to work with some code in the REPL, testing and designing it and when it seems 'right', saving it to a source file. The workflow can also include working in source files and evaluating parts of the code to load them into the REPL. In a well integrated REPL there is little difference in the editing experience between the REPL and a source file.

In Common Lisp the REPL includes a debugger with a sophisticated [condition and restart system][common-lisp-condition-system] which lets me write code I *wish* I had, then when I run it I am asked what to do about the undefined functions or variables. I can choose to quickly define them or stub them out and then continue, or I can quit the debugger to start the feedback loop again after making further changes. 

## What it is not

One thing that this cycle does not provide is a a set of tests which can be run repeatedly as you get with TDD. However the interactions at the REPL involve many of the same test cases you'd use in TDD - typical data, empty data, aberrant data, etc. So those can be collected, mixed with some assertions and used as the tests to save for later regression testing / documentation.

## Next steps

To be honest, adding bindings when stopped in the debugger is not part of my workflow because it is still not 'natural' for me to do, my fingers all too quickly dismiss the debugger from lots of habit. This workflow is my next experiment.

[^0]:  I am a hobbyist programmer of the language at best...

[^1]: That *never* happens.

[^2]: By module I mean any 'building block' of the software I am building. These might be functions, classes, packages, modules, sub-modules, all of the above. (_cf._ [Parnas][parnas]).

[common-lisp-condition-system]: https://www.apress.com/gp/book/9781484261330
[common-lisp]: https://en.wikipedia.org/wiki/Common_Lisp
[exercism-track-config-file]: https://raw.githubusercontent.com/exercism/common-lisp/main/config.json
[exercism]: https://exercism.io
[gnu-emacs]: https://www.gnu.org/software/emacs/
[parnas]: https://prl.ccs.neu.edu/img/p-tr-1971.pdf
[prototype]: https://en.wikipedia.org/wiki/Prototype
[repl]: https://en.wikipedia.org/wiki/Read–eval–print_loop
[slime]: https://common-lisp.net/project/slime/
[sly]: https://github.com/joaotavora/sly
[spike]: http://agiledictionary.com/209/spike/
[tdd-repl-analogies]: http://code-and-cocktails.herokuapp.com/blog/2011/04/13/tdd-and-repl-analogies/
[tdd-vs-repl]: https://erik-engheim.medium.com/test-driven-vs-repl-driven-development-809d3c7a681 "Erik Engheim"
[test-driven-development-deluxe]: https://davidvujic.blogspot.com/2021/02/test-driven-development-deluxe.html

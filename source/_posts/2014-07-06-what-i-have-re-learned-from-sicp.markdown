---
layout: post
title: "What I have (re)-learned from SICP"
date: 2014-07-06 14:14:33 -0400
comments: true
categories: sicp learning
---

After about two years of slowly working through Structure and
Interpretation of Computer Programs (SICP)[^1] I finally completed it.
I didn't do every exercise but I did many of them[^2].

## The History

I first worked through SICP back in 1989 as part of my class at
Worcester Polytechnic Institute (where I received my BSCS in 1992). It
is a book that I remember with awe. I remember being, along with most
of the class, mystified by this *dumb* language Scheme. It was so
unlike anything we were used to. I was familiar with BASIC and Pascal
and some very basic Bourne Shell scripting. Scheme was *alien*. Most
of us thought it crazy. But then, somewhere about half-way through the
class it clicked, suddenly I *got it*. Scheme, and Lisp by
association, was amazing. The REPL development, the flexibility, the
lack and regularity of syntax gave it great power. And then... then...
we started on the chapter about the Meta-circular Evaluator[^3];
writing an evaluator of Scheme in Scheme. It was so simple, so
clear[^4].

This was a Freshman class, and the rest of my time at WPI I played
around with Lisp, sometimes doing assignments in it, playing with my
Emacs initialization files, that sort of thing. Never got serious. And
then I joined the work force in 1990 with a summer job doing C/Motif
work at a startup. And then after college a C job connecting their
Windows app to a particular printer for graphs, and then a C/Motif job
on a news ticker for a stock market application. Oh and then I
learned[^5] object-oriented programming with C++... I forgot the
lessons I learned in SICP.

## The Return

I went back to SICP expecting to be *reminded* of a few things. What I
found was that I was *taught* things I never remember being taught.
Things which I so wish I had grokked at the time. Things which I
obviously never understood and then forgot.

A few of the things I learned way back when and then forgot were:

  - Judge a programming language by the means of abstraction and the
    means of composition.
  - The power/utility of REPL development.
  - Lazy streams to deal with infinities are not scary.
  - Functional Programming.
  - Object-Oriented Programming.
  - The Problem of State.

## The Reaction

This is a *Freshman* level textbook, and all of this was taught as
early as the mid-eighties. Looking back I feel like I was caught up in
a great forgetting. There are things we (as Software Engineers[^6])
*knew* and then forgot, or chose to forget/overlook.

Now I see people going back to old papers/books and
re-learning/discovering what we already knew but forgot/ignored. It is
like a wider version of Greenspun's tenth rule[^7]. We had something
and then had to put it aside because it didn't work in our
"*reality*", but now we come back and "*discover*" it all over again.

**OMG** Garbage Collection[^8] **OMG** *interactive* language shells
(aka REPL) **OMG** dynamic languages **OMG** functional programming
**OMG** *OO* is about message passing.

What happened, were we asleep?

It would be one thing if we acted like these are in fact old ideas
that are just now realizing are good/possible - but we act like they
are *new*. Reality has caught up to where the 1960's thought was
possible[^9].

## The Back to the Future

One last thing I (re)learned: The fun of learning and working through
problems. And that leads to what is yet to come.

I'm going to start looking at the old texts of our practice. The
ancients knew things that we have forgotten. I will see what I can
learn from them. I will strive to avoid Argument from Antiquity
however, that is always a danger with this sort of thing.

I can only see so far because I stand upon the shoulders of Giants[^10].

----
[^1]: http://mitpress.mit.edu/sicp/

[^2]: https://github.com/verdammelt/sicp

[^3]: http://mitpress.mit.edu/sicp/full-text/book/book-Z-H-26.html#%_sec_4.1

[^4]: It was in this class I created the joke idea of 'God code'. The
      stereotypical 3 line Lisp code, first line defines function,
      second like is a null check, third line recurses. And *shit* got
      done.

[^5]: *"*learned*"*

[^6]: Software Engineer, Programmer, Coder, Hacker whatever you want
      to call us/ourselves.

[^7]: "Any sufficiently complicated C or FORTRAN program contains an
      ad hoc, informally-specified, bug-ridden, slow implementation of
      half of Common Lisp."

[^8]: http://mitpress.mit.edu/sicp/full-text/book/book-Z-H-33.html#%_sec_5.3

[^9]: http://www-formal.stanford.edu/jmc/recursive.pdf

[^10]: with apologies to Newton.

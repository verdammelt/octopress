---
layout: post
title: "On Implementing a Lisp"
date: 2012-08-13 07:37
comments: true
categories: lisp ruby yarlisp
---

## 0. Background ##

About a year ago I read McCarthy's paper ["Recursive Functions of Symbolic
Expressions and Their Computation by Machine][paper] and I thought about
implementing the Lisp described in it in Ruby (a language I was learning at
the time). The project languished for quite some time until just recently when
I went ahead and implemented the language specification laid out in that
paper.

The project is [yarlisp][], it's name means "Yet Another Ruby Lisp" given an
assumption that I could not possibly be the first person to do this sort of
thing, mixed with the idea that ["Ruby is an acceptable Lisp"][acceptable] and
even a bit of ["Talk Like a Pirate Day"][pirate].

My goal in this project is to try to minimize the amount I need to implement
in my 'assembly language' (Ruby). There is an idea that Lisp needs to have
only seven primitive operations implemented in its assembly language and
everything else can be implemented in the Lisp itself. (Obviously this seven
primitives thing really only implements the symbol processing parts - things
like numbers, IO etc. really need to be implemented in the underlying
language). I have not entirely succeeded in this so far - I was more
interested in the beginning to implement the functionality; I think I can
refactor to more purity.

## 1. Current state of the project ##

I have implemented `ATOM`, `EQ`, `CAR`, `CDR`, `CONS`, `COND`, `QUOTE` and
`EVAL` all in Ruby. The features of Ruby I have used are subroutine
definition, conditionals, boolean true/false, equality and raising exceptions
(for undefined behavior).

The implementation of `EVAL` required some more helper functions due to their
recursive definitions, these too are written with Ruby as I had not yet found
a way to implement subroutine definition - especially not recursive subroutine
definition.

`ATOM`s are symbols (*e.g.* `:foo`); `CONS` cells are arrays of length two
(*e.g.* `[:a, [:b, :NIL]`). Anything not an array is an `ATOM`. All public
methods of the `Yarlisp` module are named in ALL CAPS; these are the Lisp
primitives. Any helper methods are implemented as inner methods and are named
in lowercase. If it is not in ALL CAPS it is not a method available in my Lisp
language.

Currently the only sexp syntax available is `CONS` cells; the *list
shorthand* style of sexp is not yet available. This means I need to write
lists like `[:a, [:b, :NIL]]` instead of `[:a, :b]`. This has become very
annoying, very quickly.

One oddity of my implementation is wherever I call a Lisp primitive I do it in
an oddly Lisp looking way (odd to see in a Ruby file). For example, when the
`CAR` of the expression passed to `EVAL` is `:CDR` it returns: `(EVAL (CAR
args), env)`. While it makes the code look odd for Ruby - it brings out the
*Lispyness* of it. I will continue with this as an aesthetic in the code I
write in this project.

Because of my choice of Ruby as my 'assembly language' I have not needed to
implement memory allocation or garbage collection.

## 2. Thoughts ##

I found this a fun little exercise and want to continue to do it. I think I
will also implement Lisp in other languages. It turned out not to be very
hard and was something that could be easily be broken up into pieces by the
different primitives and clauses in `EVAL`.

Now that I see all of `EVAL` implemented I think I can see a way to
reimplement more of the language in Lisp itself by using the `LABEL` and
`LAMBDA` Lisp functions. Also there are things like `:NIL` and true/false
which I could implement by having `EVAL` append bindings to the environment it
is passed. That way there will be default bindings for these things. Or
perhaps I'll just leave that for the caller of `EVAL` to do.

I ran into an odd issue while finishing my implementation of `LABEL`. There
was a feeling of double evaluation on the arguments the method I was defining.
Since my goal at the time was to implement the spec as written I went along
with it. However I believe there is an superfluous call to `EVAL` in the
definition as given in the paper. I want to hunt that down and fix it.

What I am struck with overall is the cleanliness and sparseness of it. The
logic of simple, regular syntax, and the association list lead to no surprises
during implementing. Each step made sense; although `LABEL` and `LAMBDA` took
longer for me to understand - partly/mostly because the M-expr syntax used in
the paper, along with the formatting of the paper, made that section of the
specification harder to read. In reviewing my implementation I can see the
specification very clearly in it; the definition of Lisp is very clear in its
implementation.

I hope to continue working on this project - and others like it. I'll continue
to write about my adventures with it.

## 3. Next steps ##

The next phase of this project will include the following:

1. Adding the list style sexp shorthand - all these `CONS` cells are getting
   hard to write out.
2. Refactoring to higher purity of the language - implementing more of the
   language in itself - less in Ruby
3. Implementing a reader - which will need to be in Ruby. Although with the
   more comfortable sexp syntax this may not be so necessary.
4. I want to find a more Lisp way of handling the undefined cases - to remove
   the raising of exceptions from Ruby code. This is an extension of the
   purity issue above.

The very next step for me to take is to implement a *real* example method in
my Lisp. Even though I do not have numbers I may implement a Fibonacci or
factorial method using [Church Numerals][churchnumerals]. At the very least I
will implment the `FF` method presented in the paper.

[paper]: http://www-formal.stanford.edu/jmc/recursive.pdf
[yarlisp]: http://github.com/verdammelt/yarlisp
[acceptable]: http://www.randomhacks.net/articles/2005/12/03/why-ruby-is-an-acceptable-lisp
[pirate]: http://en.wikipedia.org/wiki/International_Talk_Like_a_Pirate_Day
[churchnumerals]: http://en.wikipedia.org/wiki/Church_numerals

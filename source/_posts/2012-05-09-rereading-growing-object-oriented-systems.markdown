---
layout: post
title: "Rereading Growing Object Oriented Systems"
date: 2012-05-09 20:22
comments: true
categories: goos tdd design oo goosreview
---

## Why

I read [GOOS][] severals years ago but I have decided to reread it as I felt I
didn't think it really got into my head the first time. Definitely I did
become more comfortable with mocking in tests - but I felt there was probably
more that I missed. So I am rereading it - and more importantly - taking a few
notes. It is those notes that I will be writing about, every chapter or two -
hopefully not a project that will end in a whimper.

## Chapter 1

### A learning process

{% pullquote %}
"{"Software is a learning process."}" I am not sure why I didn't catch this
last time. It is something that makes absolute sense to me now; and moreover I
don't know a time when it would *not* have made sense to me over the last
decade. If software is a learning process, getting feedback on that learning
is of utmost importance.
{% endpullquote %}

### Nothing to lose

The boxed-text about 'nothing to lose but your bugs' strikes me as 'sales
pitch'. Having believed, then being bitten by this catch phrase I don't buy
it. TDD will not help the developers write the right feature - just help
ensure that what they write is what they intended. It is not a silver bullet;
and I'd think that Pryce and Freeman had not intended that; so I hope that
I'll see something that backs up this claim from them.

(However I *do* feel that implementing via TDD helps drive out cases that
might get missed until later exploratory testing. By finding them earlier in
the process we have a big win.)

After finishing the rest of the chapter I see their claim is that all the
levels of TDD practices: end-to-end; integration and unit; could reduce the
chance of writing the wrong code.

### Refactoring

Pryce and Freeman say that refactoring is a local change. This made me
immediately realize that easily fall into *large* refactorings. This is
something I want to keep an eye on. Not just for refactorings - but for any
work - I should work in small chunks.

### A rose by any other name...

It annoys me that there are so many terms for different levels of tests. I
personally use 'Integration' test for any test that integrates two or more
components (except for those sets of components which I consider a Unit - then
of course that would be a Unit test...). They keep talking about 'Acceptance
Tests' which to me are 'User Tests' - and given I just got back from some
training from Jim Shore I am currently at least moderately against automated
user tests. I do like End-to-End tests - that they call Acceptance test - but
need to keep them under control since they have the drawback of slowness and
brittleness.

I really like to have clear terms for things - terms that are understood
generally by people. I think it eases communication. That being said I see in
myself a lacking of clarity when I discuss topics. Reading this book is
bringing this up to me; perhaps it is something I need to work on for myself.

## Chapter 2

### A web of messages

I think the important idea presented in this chapter is the idea the domain
concepts are not embodied by a particular classes in your code but by the
connections of those classes embodied by the messages that they pass each
other. This is an idea I remember having trouble with when I first read this
book and I am again having a little trouble making it concrete in my head.
Hopefully this second read will help solidify it.

### Values & Objects

The authors present a nice terminology for two types of collections of data
and functionality found in code. Simply: *Values* are immutable without
distinct identity; *Objects* have changing state and have distinct identity.

Here again is a reminder to me to have a clear, consistent terminology to aid
in communication.

### Tell don't ask

While I am familiar with the "Law of Demeter", it is one of those things that
seems to quickly fall by the wayside as I code. Another thing to add to my
list of things to improve.

There seems to be a lot of good discussion about this on the internet - one
discussion and explanation of it I like is that from Avdi Grimm in his
blog post [Demeter: It's not a good idea. It's the law][lawofdemeter]. In it
he points to method chaining and points out:

    >Look again at the definition of the Law: it never says anything about the
    >number of methods called, or the number of objects a method uses. It is
    >strictly concerned with the number of /types/ a method deals with.

So it is OK to chain a set of method calls together that all do different
things to collections of objects, or Strings for example; but not when there
are multiple different *types* of objects.

## In Conclusion (for now)

I am looking forward to continuing my rereading of this book. I think I will
gain from this review of important topics (Object Oriented Design and TDD). I
may not end up agreeing with it - but I hope to solidify my thoughts and
practices in this area through it.

Along the way I plan on continuing to take notes and then making blog posts
about it. I think through this process I will do an even better job of
understanding what I have read. I hope you all don't mind too much.


## Postscript - Chapter 3

Chapter 3 was a discussion about using JMock. Nothing really to note or
report.  I have no yet decided what language(s) I will be using while doing
the exercises.  I think I may just do it in Java with JMock so that I can
easily follow along with their examples. However another part of me wants to
do them in Ruby or Groovy or Clojure to help me compare and contrast.

In any case, any code written will of course be published to [my
Github][github].

[GOOS]: http://www.growing-object-oriented-software.com/
[lawofdemeter]: http://devblog.avdi.org/2011/07/05/demeter-its-not-just-a-good-idea-its-the-law/
[github]: https://github.com/verdammelt

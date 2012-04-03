---
layout: post
title: "My thoughts derived from the talk given by @chadfowler at @bostonrb 2012-02-21"
date: 2012-02-21 22:36
comments: true
categories: bostonrb meetup metrics ruby
---
## Overview ##

(I finally went to *another* Boston Ruby meetup.  Only my second -
hopefully it will be less than ~9 months before I go to my third.)

Chad Fowler gave a talk entitled "Measuring &amp; Analyzing Things That
Matter When You Have Too Many Things To Keep Track Of" at tonights
Boston Ruby Meetup.  It was *the* reason why I went to the meetup.(But I
did enjoy the other two talks - but they are not the topic of this post)

His talk was, self-described, half-baked ideas.  Which is fine by me.
At @boston_sc we've started doing "half-baked" ideas talks and they have
been great - I only wish that this talk was more discussion style like
the ones we have at @boston_sc.

He talked about how even with a team of very good developers, good code
is not guaranteed.  The bad stuff builds up, even without people
noticing, via bad habits and laziness.  His person example of gaining a
lot of weight hits very solidly with me and I am again working to drop
my weight which keeps just sneaking back (due to bad habits and laziness
on my part).

## How to measure how readable code is ##

He mentioned several thoughts about how to fight the bad
habits/laziness, but the one that got me thinking was about the
[Flesch-Kincaid Readability
Scale](http://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_test). 

Basically in a nutshell Rudolph Flesch devised a algorithm for English
which let you compute a score which then equates to what level of
English reader could easily read and understand your English.  He
suggested that perhaps some combination of metrics (e.g. flog, flag,
roodi, churn, reek, (i.e. things from metric-fu)) might render a
*number* which would equate to a level of developer (his scale topped
out at Rich Hickey) that could understand your code.

The reason that this got me thinking especially was because it fits into
a less-than-half-baked idea I've had.  A few months ago I was working
with a junior developer at my job and while she was away I had
implemented a nice little bit of Groovy code to do something.  It
involved a chain of collection functions (*e.g.* map, inject, collect
etc.).  I thought it was great.  When she came back and saw it she
couldn't understand it.  I explained it to her and she *started* to
understand.  I explained again and she *sort of* understood.  Then I
said "ok, hold on..." and replaced it with 2 for loops.  Totally dumb
un-cool code that did the same thing.  She immediately understood! So
that is what we committed.

The problem was that I was at a higher level of understanding of that
sort of pseudo-function collection function chaining.  (and also it
the code might have been a bit 'clever' *shudder*).  By shifting to
*ordinary* code it was easy to understand.

The thing I am interested in is if this scale of code comprehensibility
is if it is absolute or relative.  My first thought it is relative.  If
one can raise the base skill of a team then that team can understand
more esoteric code. 

## Other thoughts ##

There were other interesting points in there - obviously rather ruby
specific:  

* Mention of tools like flog, flay, roodi, reek, etc all good
  at giving numbers about your code.
* Measuring whatever worries you
* Graphing everything you can
* (again) Getting information from your commit history

These are also things that will keep me thinking for a bit.  I can use
these ideas both in my for-pay coding and my for-free/me coding.


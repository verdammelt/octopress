---
layout: post
title: "GOOS Review ch 14 &amp; 15"
date: 2012-11-18 19:13
comments: true
categories: goos goosreview oo tdd design
---

(Just a quick post about chapters 14 & 15 of GOOS to get myself back into the
swing of things after a while...)

A few points hit me during these two chapters. Things which I *know* but which
perhaps are not entirely second nature to me yet (even after all these years)

 * In chapter 14 new features were added with little fuss - the relatively
   clean design allowed for this.
 * Chapter 15 showed doing refactorings bit by bit - it kept tests red for a
   while but they got done. Just because it will take a while doesn't mean not
       to do it.
 * Chapter 15 also saw the developers thinking about how to continue down the
   path they were one was going to be pretty annoying/boring. They took this
   to mean that they were doing something wrong. They stopped and thought
   about it and found a better design which allowed their needed changes to be
   easier.

These are three important things to internalize:

 * Good clean design leads to ease in implementing new features.
 * A refactoring might be hard - but that is not a reason not to do it.
 * If the change you need to do is hard / annoying - step back and figure out
   why (see the first point).

These are all things I *know*; but in the heat of the moment will tend to
forget. I need to really get them internalized; then I can *choose* to ignore
them at certain circumstances, but then I'll do it more explicitly and know
the pros and cons.

Also as a side note there were some good points where the OO design skills
shone through. For example the addition of Java `enum` objects which quickly
became feature-ful objects which caused cleaner code elsewhere (`Column` and
`SniperState`)


---
layout: post
title: "How I learned to stop worrying and love the Monad"
date: 2012-06-27 19:43
comments: true
categories: monad
---

(sorry I couldn't help that title)

For a while I've been trying to learn what this *Monad* thing was. Smart
people were talking about them and making them sound important. Smart people I
knew and admired were making them sound like something I should know about.

So I'd try to learn what monads are and it all sounded something like this:

> A Monad is Kleisi triple: an endofunctor, together with two natural
> transformations.

Simple right? I just felt dumb. I didn't think I'd ever understand what they
were or why they were important.

That is until I watched two presentations. While I can't say I *understand*
them yet, I feel like I've had an insight which might be useful so I'd like to
share them.

(Both presentations use Clojure - but don't let that put you off if you don't
know Clojure - the Clojure in the presentations is not very complex.)

## Why is a Monad like a Writing Desk

A few weeks ago I finally watched a presentation by Carin Meier called 
[Why is a Monad like a Writing Desk?][infoq] (presented at Clojure/West 2012). 
Given my big soft-spot for Alice in Wonderland references I was predisposed 
to watch this video. 

Carin presents monads gently via a cute little story of Alice, a programmer,
who is trying to learn about monads but falls asleep and enters a Wonderland
like land of talking doors and Astronaut-hosted tea parties. Through the story
I learned a little bit about monads alongside Alice.

She covered the Identity, Maybe and State monads which I had seen before but
now better understood. 

## Introduction to Monads

At the end of Carin's presentation there was a link to another presentation by
Adam Smyczek called [Introduction to Monads][intro] (presented at a Bay Area
Clojure User Group meeting in 2010).

In this presentation he shows a real case where he used several monads to
create a clean design for a testing DSL he was creating. It involved some live
coding which was good to see.

He also covered the same monads. Seeing them implemented again, helped
solidify my understanding of them.

## Insight

Watching these two presentation I came to a realization:

> Monads are not a **thing**, they are a pattern.

That's it. That was the insight I needed. I realized that previously I was
always looking for some explanation of a *thing*, a language construct, and
object, a function. But that is not what a monad is (although it could be
built in to a language *etc.*). 

Monads are a design pattern. They are a pattern
of flow control, a pattern of chaining functions on sequences of data.

I think my next insight will come about when I consciously implement code
using monads. I hope to create an opportunity for this.

I'd suggest to anyone who wants to learn something about monads but is finding
it tough to watch Carin's presentation (sit back, relax, enjoy and learn) and
then follow that up with Adam's presentation.  I watched them back to back one
evening and I think that really helped.


[infoq]: http://www.infoq.com/presentations/Why-is-a-Monad-Like-a-Writing-Desk
[intro]: http://www.youtube.com/watch?v=ObR3qi4Guys



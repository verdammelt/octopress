---
layout: post
title: "quick thoughts about @david_a_black's presentation at @bostonrb 2012-07-10"
date: 2012-07-10 21:35
comments: true
categories: ruby lisp objects
---

## 0. Overview 

David Black ([@david_a_black][black-twitter]) presented his his "The
Well-Grounded Nuby" presentation to the Boston Ruby Group
([@bostonrb][bostonrb-twitter]) meetup on 2012-07-10. I was unfortunately
unable to attend but I watched/listened in on their 
[live streaming][live-streaming].

He presented seven things about Ruby that every noobie should know. I guess I
am still closer to noobie than expert but I found that his points where very
good for 'levels' above noobie. His seven points were:

* Everything evaluates to an object
* Sending messages to objects
* Objects resolve messages to methods
* Classes and modules are objects
* There is always a "self"
* Variables contain references to objects
* True and false are objects

I thought his talk could be summarized (*flippantly*?) into two points:

1. Ruby is [objects the whole way down][turtles].
1. Ruby is [Lisp][lisp]-y.

## 1. Objects the Whole Way Down

I had the thought that Ruby must be objects the whole way down; but I had not
tested it out, nor thought about it much. I just hadn't needed to worry about
it in my small amount of Ruby work. But this presentation made me much more
aware of this. I need to experiment with this more and become more familiar
with this style. C#/Java (which I am more recently familiar with) just don't
have this feel.

I do a lot of work day-to-day in [Groovy][groovy] and some of the discussion
here sounds familiar. While I *knew* Groovy was like Ruby, I think it might be
more like Ruby than I had been thinking. I need to investigate.

## 2. Lisp-y

Perhaps it is because I've been reading [Let over Lambda][lol] but I
immediately started thinking lispy thoughts during a few points.

Specifically when he was saying that everything evaluates to an object and
discussed how `case` is just as `if...elseif...else` using `===` I wondered
how I might be able to write my own control flow. Does Ruby have
[macros][macro]? I need to investigate.
 
## 3. The Mixture of the Two (and beyond)

His first point, "Everything evaluates to Object" and "`true` and `false` are
Objects" made me think lispy thoughts. On the first point it was simply "duh"
of course *everything* evaluates to *something*, and the second made me think
of the difference between [Scheme][scheme]/[Clojure][clojure] and 
[Common Lisp][lisp] with respect to `t`/`nil` or `true`/`false`.

Lisp has an object system - but it is built on top of an existing language
with the features of the language itself. There is something about this
presentation of Ruby that makes me start feeling that Ruby's object system,
while a much more integral part of the language is still defined in that
language itself as [CLOS][clos] is.

His point about "There is always a `self`" made me think about my recent
forays into [Javascript][javascript] at work. These have revolved around me
trying to understand what `this` was at different points in the code.

## Conclusion

The talk was though-provoking in me; and thus, *IMNHO*, it was good. I have at
least two different things to investigate.

Overall his presentation made me realize there was plenty more in Ruby for me
to learn, and that there was plenty more in Ruby that was, to me,  *worth*
learning.

[black-twitter]: http://www.twitter.com/david_a_black
[bostonrb-twitter]: http://www.twitter.com/bostonrb
[live-streaming]: http://www.youtube.com/watch?v=DVQxmayBWOs
[turtles]: http://en.wikipedia.org/wiki/Turtles_all_the_way_down
[lisp]: http://www.lispworks.com/documentation/common-lisp.html
[lol]: http://letoverlambda.com/
[macro]: http://www.gigamonkeys.com/book/macros-defining-your-own.html
[groovy]: http://groovy.codehaus.org/
[scheme]: http://en.wikipedia.org/wiki/Scheme_(programming_language)
[clojure]: http://clojure.org/
[javascript]: http://en.wikipedia.org/wiki/JavaScript
[clos]: http://en.wikipedia.org/wiki/Common_Lisp_Object_System

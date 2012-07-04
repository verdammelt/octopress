---
layout: post
title: "goos review chapter 12"
date: 2012-07-02 21:25
comments: true
categories: goos tdd design oo goosreview
---

In this chapter we implement our first *real* acceptance test. It is an
end-to-end test of a real user feature.

I tend to run my tests repeatedly as I write them - so I hit a problem before
the Authors revealed it. It was the *surprise* problem of the connection
needing to be closed. I guess my running of tests often led me to find it
earlier than others might - so I'll take that as a win. It was annoying to
hit it before the Author's intended though - I thought I had a broken OpenFire
installation.

There were four things that stood out for me in this chapter:

1. Their note about using the same value in test code and production code
   (*e.g.* JOIN_MESSAGE_FORMAT) on p109.  This is a problem that I struggle
   with in my testing. Sometimes I feel that it is cheating - or not really
   testing anything. Other times I think it is the "Right Thing To Do(TM)". I
   am glad/disappointed that they have conclusive word on if it is good/bad.

2. They start implementation of the new feature by first refactoring the
   existing code into one that will make the needed change easy. This is
   something I'd like to internalize but I haven't yet. I usually start by
   implementing what I need (even if hard/ugly) and then refactoring until it
   is nice and clean. But this often leads to 
   [wailing and gnashing of teeth][wailing]. I also think, in retrospect that
   I have missed the target of the really nice design, which no longer can
   really see, but I *feel* is still out there.

3. There was a phrase on p113 which I think is a good feel for how I usually
   am thinking when I am implementing: "...our immediate concern is to get
   message translation to work, the rest can wait." It is this focusing on the
   immediate problem and 'faking-till-you-make-it' that I do a lot. I like to
   commit often - so I am always working hard to get small bits working and
   committed instead of trying to do bigger chunks of work (although I can't
   say I am always successful in this).

4. On p116 the Authors say that the expectation is the most important line of
   the test. However I find that it is hidden in the Java code needed to
   create it. Perhaps it is because I always look at a test in the 'arrange,
   act, assert' way; so I don't expect to see an expectation in the 'arrange'
   section but in the 'assert' section (as it would be with Spock, Mockito, or
   Moq for example). I wonder how else it could be made more visible?

5. Finally they point out the importance of writing the 'first draft' code and
   then refactoring it after the tests are working. I don't think I could
   agree with this more strongly.

On the whole a good chapter for the first real user-feature. I am still
annoyed with plain old Java code. Maybe I'll need to start re-implementing
this in Ruby or at least Groovy sooner rather than later.

[wailing]: http://bible.cc/matthew/13-42.htm

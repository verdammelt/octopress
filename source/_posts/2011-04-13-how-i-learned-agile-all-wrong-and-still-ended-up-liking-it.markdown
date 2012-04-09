---
layout: post
title: "How I Learned Agile All Wrong and Still Ended Up Liking it."
date: 2011-04-13 00:16
comments: true
categories: agile personal tdd work
---

## History

Up until several years ago I only knew one way to do a software project.
The "usual" way: Requirements document; bunch of coding; deadlines which
were basically impossible; throwing the app at QA; thrashing to "improve
quality"; sending it to the customer and then "firefighting" to fix the
fact that it didn't meet the requirements.  Sure there were glimpse of
other ways; small changes to the process etc.; but generally the same.

Then I learned about "Agile". (I fully intend those quotes). The company
I worked for was bought by another larger company. That company seems to
have had a team which "went Agile" from the bottom up and the company
decided that it was going to be the "new way". I was one of the
"important people" who was on the new project which was going to be one
of the flagship "Agile" projects.

## What I Was Taught

We got two(ish) days of consulting. We were taught story writing,
planning poker, iterations, QA in-iteration, and some TDD examples (damn
Bowling Game). The impression I _got_ was that we'd be working in close
teams, prioritizing every iteration (because requirements are always
changing), working hard to produce only the code we need (and do it
cleanly), release this frequently to get quick feedback. I also was
"taught" the "don't do design" idea.  I know several of my team members
feel they heard the same.

I thought this was **AWESOME**. I drank the Kool-Aid and then went back for
a second cup.

I worked to learn more and more. The company sent me to Agile2008, and I
I took myself to Agile2009. I went to other conferences, I read books,
blogs, I went to meetups and talked with people.

## What I Learned

I learned many things, sometimes the hard way, not all direct lessons.

I learned that "going Agile" isn't going to work unless people want to
give it a try. Imposing "Agile" from above won't work. The people
involved need to want to at least try it. Most important of course is
the by-in from management in and above the team.

I learned, and am still learning, ways to help teach and learn from my
coworkers. At first, being very gung-ho about it, I came off a bit too
"you're doing it wrong!" and that turned people off and probably burned
a few bridges that could have been useful later.

I learned that having QA in-iteration, or even better, "pairing" with QA
on the tests (automated or manual) for a story is very powerful and can
flush out issues (potential or realized) quickly.

I learned that the "don't design" idea doesn't work. (I probably wasn't
intentionally taught that, but I really feel that it came out during our
training. Perhaps an overemphasis on not getting attached to an up-front
design and letting TDD take its course.)  I initially tried it, while my
coworkers rejected it, and TDD, without trying it.  I think by trying -
and not succeeding - at it I have become better at what amount of design
is needed, and how TDD can lead to good designs (at least at the micro
level).

I learned that my ideas about OO design were not good. I was mostly
just doing imperative programming in big bags of loosely related things
I called _classes_.

I learned that clean code is flexible and can be easy to understand and
make changes to. I learned that I had a LOT more to learn about writing
clean code.

## What I Like

I love the idea of transparency. This was not taught. I learned it own
my own and I feel it is one of the most important things about "Agile"
and wonder why it is not presented more.  It can be scary, very scary,
not to be able to hide behind the buffered schedule, or the layers of
management, but in the end I think it is better to be open and up-front
about everything going on in a project.  If there are problems it is
best to get them out in the open earlier, so that they can be addressed
earlier (when it is generally easier to address them).

I like working incrementally. Working on small stories in time-boxed
iterations help me to keep focused.  Each iteration I have to make sure
that we have a (at least potentially) releasable product. I learned long
ago that today's new product is tomorrow's maintenance product. So
bringing out the maintenance problems by practicing the release every
iteration brings out the maintenance problems sooner.

I like working with in-iteration QA. Being able to work with these
professionals closely helps me ensure my code does what it needs to do,
does what it should, and most importantly doesn't do anything else. It
also gives me quick feedback.

I like quick feedback, always have (but I had forgotten over
time). Quick feedback helps me focus on what is needed and keep the aim
true. If the aim is off we know faster and adjustments can be made. Also
obviously easier to fix issues found sooner than later.

I love TDD. Plain and simple. It took me a little while, but after being
taught the TDD technique, I realized I knew it. I used to call that sort
of programming "exploratory". When I had a REPL, I coded by trying
something out, testing, playing; then I'd save it and test the larger
chunk. This would be repeated. Without a REPL I'd do it in a larger
slower edit-compile-debug cycles.

Finally, I like how what I have learned has moved me to much produce
much cleaner code. I still have much to learn here. But the "stressors"
of repeated frequent releases, evolving requirements, and TDD have
pushed me to write, IMHO, much better code. It has also driven me to
think outside the imperative and OO paradigms.

## What I Still Want to Learn

I do still need to learn much more about producing the best code I
can. Also to keep in mind that the "best code" must also be the "right
code" - it must provide the features needed.

I still need to learn some "people" things. I need to learn how to
better learn from, and teach people.

And most importantly I have learned I need to learn much more.


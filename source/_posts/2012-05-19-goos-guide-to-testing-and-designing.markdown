---
layout: post
title: "GOOS guide to Testing and Designing"
date: 2012-05-19 19:52
comments: true
categories: goos tdd design oo goosreview
---

(The second in a [series](/blog/categories/goosreview) in which I reread
Growing Object Oriented Systems and try to digest it better. Overall this
section, Chapters 4-8, is filled with timely reminders to me about several
things about good design.)

## The Walking Skeleton

This is one of the points in this book which seem like such small items but I
think have more importance than initial appears.  In fact I am surprised in my
rereading that the authors advocate the end-to-end tests to be done on
*deployed* systems - that is not something I've ever really tried and seems
very daunting.

The important things to remember here about the Walking Skeleton is that it is
*not* about writing real functionality, but meant to flush out issues both
technological and organizational. It will be definitely smaller than an MMF.
It might take a surprising amount of time to write it nonetheless. This is
because there will be a whole lot of learning happening. The same goes for the
first few features. (Boy is this a timely reminder for me right now...)

Unfortunately this slowness at the beginning of a project can seem like a bad
thing - but it is really not. The beginning feels a bit rocky - but then it
smooths out as deploy and integration issues have been resolved. In a 'normal'
project the beginning might be smooth but the deploy and integration problems
will crop up and make the end rough.

## How to Write a Test

The way they describe to write a test is something I try to do - but it bears
repeating (this is valid for tests at any level):

 1. Write the test you want to read (write helper code to make this possible). 
 1. Watch it fail - keep working on it until it fails for the right reason
    with a good error message).
 1. Now write the production code to make it pass.

By taking the time to do this you will ensure that the goal and intent of the
part you are working on is clear. When done ensure it has a clear intention
revealing name - this is how you will understand the system later.

Start by writing an acceptance test for the feature. Write it in terms of the
domain and the user. An acceptance test gives feedback on the external API of
the system and upon major integration points both with external APIs and
internal components. Since the acceptance test is likely to be failing until
all parts of the code is written it will need to be separated from the main
build. 

Once the acceptance test is well written then start moving down a level to the
objects that the acceptance test uses and unit test their functionality into
existence. This is the idea of testing from inputs to outputs.  Jumping to a
lower level object too soon will lead that object to have an interface which
does not reflect what it really needs to be. Only by building the objects
after building their callers can you know what is really needed.

The Authors have a bit of simple advice as to what to test first: they suggest
going for a simple successful path, and they make a good point why. Tests
provide feedback, if you focus your initial tests around error or edge cases
then your design feedback will be about that instead of the normal work of the
component you are writing.

One final important point the authors make on how to write tests is: "If an
area is hard to test don't just ask *how can we test this?* but *why is it
hard to test?*. If something is hard to test it could be the tests are trying
to tell you something. This is one place I have trouble with - I seem to have
too much tolerance for pain while coding - a tolerance I need to cure myself
of.

## How to Design Code (and How Tests Affect That) 

Obviously writing tests before the code affects how the code is designed - the
pressures to keep each object isolated are very powerful. The book contains a
good set of design points which are not unique to the book and not new to me.
There were a few specific points I thought good to note.

When objects are composed together the interface for the composite object must
be less complex than the union of the interfaces of the composed objects. This
makes it a higher abstraction which hides some of the complexities. Higher
abstractions allow us to manage complexity.

Each object must be context independent *e.g.* everything it needs to do its
job needs to be passed into in via the constructor or the specific method in
question. Thus each object has external knowledge on a "need to know basis".
This leads to the ability to recompose objects to get different behavior.

Create plenty of Value types. This combats Primitive Obsession and also
creates attractors for functionality. 

Object peers (those objects which are communicated with directly) should be
mocked out in tests. This causes coupling and interface problems to be
evident.  Value types should not be mocked.  Neither should third party APIs
be mocked since the feedback provided cannot be used since the API cannot be
changed. Also mocking external APIs runs the danger of testing against
behavior you believe the API has, but may not actually have. Third party APIs
should be wrapped in a thin adapter layer which can be mocked in unit tests.

## Where do Types Come From?

I rather like the Author's descriptions of how types are 'found' when working
in the code. The three ways are valid for both Value and Object types:

  1. Breaking Out: When the code shows that an class is becoming too complex
     that is a sign that it is doing too much.  Some of the functionality
     could be split into helper types.

  2. Budding Off: When there is a new domain object a new type should be
     created, even if is empty or contains only one piece of data.  The type
     will act as an attractor for further data and behavior.

  3. Bundling Up: When a group of classes are always used together they can be
     bundled together.  Remember that composite objects should have a less
     complex interface than their composed parts.

## A Final Note About Mocking

I find that now that I can mock concrete classes in Java that I do not use
interfaces as heavily as I used to. The Authors specifically point out they
use interfaces quite a bit - again because they are concerned with
the communication between objects. I think this is one item I'll keep an eye
on as work through the examples. I have used interfaces in this way before but
it seems lately I have not been doing so.

## Conclusion

I agree with their design ideas. I already try to follow them. I am quite
excited to work through the example with them (something I did not do when I
read the book previously). I hope that by doing (and blogging about it) these
good ideas will sink in more; becoming more normal for me.

I also intend to blog more frequently on it instead of lumping large chunks
together like I did here.

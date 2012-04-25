---
layout: post
title: "My problems bootstrapping Midje"
date: 2012-04-24 20:23
comments: true
categories: code midje clojure retrospective mistakes
---
## (*A Tragedy of My Own Devising*)

## Abstract
I had a lot of problems setting up my first [Midje][] tests for my [Clojure][]
project [(defdrink)][] last night and thought it might be useful for me to
write about it.

(And helpful it was... I see plenty of mistakes I made and summarize the
lessons learned at the end).

## Background

First a quick background. [(defdrink)][] will be/is a web application which
will assist in the choosing of a cocktail based upon the contents of the users
liquor cabinet. I am using this project as a means of learning [Clojure][]. I
have put all the source on [github][defdrink-github] (as one does...) and in
this post will refer to particular commits to illustrate different steps.

## In the Beginning...

At the point where our story begins I had slapped together a quick (and ugly)
prototype. The purpose of the prototype was to get a Clojure project which has
a web page which allowed retrieving and saving data into a database; all
served up on Heroku. Being a prototype - it had not tests (horrors). This
moment in time is [commit 0da77fbafc87634e94e0342e409e5b071b8d6c1f][start].

## Trying to put in the first Midje test.

It took me two tries to get my first Midje test (and that first test merely
proved that Arithmetic worked: `(fact (+ 2 2) => 4)`). 

My first attempt was me doing what I thought was 'obvious' and what I thought
the Midje wiki was telling me I should be able to do: put a bit of magic in my
`projects.clj` file and then a test file with a `(fact ...)` in it.

That attempt ending with frustration at the fact the only feedback I was
getting was a bunch of Java stack traces.

My second attempt was simply making these same stumblings - I had wrongly
assumed that I had I simply not *quite* understood the previous time.

After I realized that my second attempt was heading toward another failure I
finally rolled back and tried to take the next smallest step.  I wanted to run
Midje (with [Lazytest][]) and get it to report something like "0 tests". With
the help of the [lein-midje plugin Readme][lein-midje] I got this
[working][lazytest-success] in not too much time. If you look at that commit
you will notice a glaring error - one that was not obvious to me as I tried to
continue.

## My first Midje test...

### A Problem of My Own Devising

Ages ago when I started this project I ran `lein new defdrink` and then, since
I didn't have any tests, I removed the `test` subdirectory. Now, a month
later, I couldn't remember just how the test directory was supposed to be laid
out, and it was obvious to me that it needed to have some special directory
tree/naming to find the files etc. Mixed into that was a lack of understanding
Clojure namespaces and directory structures (this was just me being dense).
At this point I kept getting stack traces about not finding namespaces, which
all seemed right - but obviously lein, midje, clojure or all three didn't
agree.

Finally I had just ran `lein new foo` in a temp directory and saw the
structure needed.  That was the clue I needed -- the clue  I couldn't find
this little simple piece of information out on the web either for Midje or
Clojure's own test framework. Now that I had the directory structure right,
the namespace in the file right it would work right? *Right?* 

### ...wrong...

As I am sure all of you playing along at home can see - I never added a
dependency on Midje itself in the previous step. That means at this point I
started getting messages that said:

> Could not locate midje/sweet__init.class or midje/sweet.clj on classpath

Let me tell you this was very confusing after all I knew that I already
had Midje working. Now that I added a test it says it can't find Midje?!
Finally I saw my error and fixed it.  Now at long last, I had a Midje test!
Of course it was just a [dummy test][dummy-test] but it was actually running.

## Now, let's do it for reals...

My next step was to get a real test. My premise for these tests was to remove
some hardcoded SQL code in my model class. I was going to push that code down
into a couple helper classes so that I could isolate myself from the database.
The first test was to show that my `defdrink/all` method would delegate down
to my new `sql/select` method with the `:drinks` parameter (that is the
table name).

I once again had some odd and annoying problems with the only feedback being
cryptic stack traces.  I don't remember all the details but they involved
statements such as 'provided not being defined in this context' - which led me
down wild chases to determine if I had all the right modules required etc.
Fortunately/unfortunately the problems resolved themselves (I hate that) and I
got my first [real test running][first-real-test]: 

{% codeblock A Small Step for One Programmer lang:clojure https://github.com/verdammelt/defdrink/blob/dfc494f7b4ea50b67138605308be1967d9d8dcd4/test/defdrink/test/models/drinks.clj defdrink/test/defdrink/test/models/drinks.clj %}
(fact (all) => [...drink1... ...drink2...]
      (provided (sql/select :drinks) => [...drink1... ...drink2...]))
{% endcodeblock %}

(I sort of like how it turned out... I like the [metacontstants][] feature and
am excited to try it out more.)

## And now for my encore...

Now that the select statement was sequestered, I turned my attention to the
insert statement.  This is where I again ran into problems. 

This new test, like the previous, was going to be a simple test of delegation.
Did the model layer properly call down to the database layer to query or
persist the data.  The test I wanted to write was to say that the
`defdrink/save` method called the `sql/insert` method with the correct
parameters.  My first attempt at this ended... (wait for it...) in
frustration.

### What's wrong *THIS* time?!

In Ruby or Java/Groovy I'd simply have my test call my method and test the
expectation on my mock object that the `sql/insert` method was called with the
correct parameters. Unfortunatly for me, I could not figure out how to do that
in Midje. I ended with the following unhappy test: 

{% codeblock An Unhappy Test lang:clojure https://github.com/verdammelt/defdrink/blob/9fbb73b327e7509e2612932dfedc97e8e55330ce/test/defdrink/test/models/drinks.clj defdrink/test/defdrink/test/models/drinks.clj %}
(fact
     (insert ...name...) => ...not-important...
     (provided (sql/insert :drinks {:name ...name...}) => ...not-important...))
{% endcodeblock %}

I'll freely admit that while trying to write this test I began to have doubts
(which I still hold) that perhaps I shouldn't even by *trying* to right this
test. It just seemed like a code smell to me. The way the test ended up seems
to be telling me: "Mark, just what are you thinking?!"

## Conclusion

In conclusion (finally) my problems were much of my own devising. Whether it
was shooting myself in the foot, trying to do something quickly because "its
easy right?", not yet understanding this language/environment I am trying to
work in, or simply because I am trying to write Clojure tests as I would Ruby
or Java tests -- I've had a hard time getting to [this point][tested].

Even admitting my own problems, I have to say, IMNSHO that it would have been
nice to see a tutorial/cookbook out there of how to get started with Midje.
What I'd have liked to have found would be something which stepped me through:

 1. what to put in my `project.clj` file for midje, lazytest, and lien
 1. a simple example of getting one's first tests off the ground
 1. and then a bit more showing mocking for example.

In researching this blog post I see I did overlook some resources on the Midje
wiki that would have helped, at least with the second two points. 

So the moral is: 

 1. slow down 
 1. small steps
 1. *read* the docs, not just look at them.

I do think I might try to contribute this sort of tutorial to the Midje
project. Because I can't be the only dope who thinks he knows what he's
doing, who will get frustrated because there is not a tutorial to hold his
hand through the first steps.


[Midje]: https://github.com/marick/Midje
[Clojure]: http://clojure.org/
[(defdrink)]: http://defdrink.heroku.com
[defdrink-github]: https://github.com/verdammelt/defdrink
[start]: https://github.com/verdammelt/defdrink/tree/0da77fbafc87634e94e0342e409e5b071b8d6c1f
[Lazytest]: https://github.com/stuartsierra/lazytest
[lein-midje]: https://github.com/marick/lein-midje 
[lazytest-success]: https://github.com/verdammelt/defdrink/commit/cd4fad91dbcb7803f49f234474bbb3d3ad3d1295
[dummy-test]: https://github.com/verdammelt/defdrink/commit/0c3840cea7d4f5e1d0258a8cd6b087f949e0c6c2
[first-real-test]: https://github.com/verdammelt/defdrink/commit/dfc494f7b4ea50b67138605308be1967d9d8dcd4
[metacontstants]: https://github.com/marick/Midje/wiki/Metaconstants
[tested]: https://github.com/verdammelt/defdrink/tree/9fbb73b327e7509e2612932dfedc97e8e55330ce

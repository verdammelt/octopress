---
layout: post
title: "On Reading Code"
date: 2013-11-25 22:51
comments: true
categories: 
---

## (Hot It Ought To Be Done. IMNSHO)[0] ##

Being able to read source code[1] is very important. So how does one do it
well? 

Just like reading any other material - first decide why you are reading it.
Why are you reading the listing? Are you debugging a problem or reading to get
general or specific knowledge? One takes different approaches depending upon
the desired goal.

The first step is to find an interesting spot to start.

### For Debugging (or to Gain Specific Knowledge) ###

If one needs to find a specific spot in the code. Perhaps one needs to know
where the widgets are frobbed. 

Start with a skimming of the code, `grep`[2] and `tags`[3] tables are useful
for this. This will help one find the right, or at least likely entry point.
There is a lot of *instinct*[4] involved in this step. One gets better at it
the more one needs to do it[5].

Now that one has found one's entry point the rest of the process is the same
as below.

### To Get General Knowledge (or for Pleasure) ###

Code is for reading[6] so read it. Skim the code (*including* the tests[8]).
Look for something interesting, get the lay of the land, the shape of the
code. Note the *Dramatis Personae*. Perhaps the code seems to be about widgets
and frobbing, oh and here's something about twiddling that looks interesting.

Pick one of these that is most intriguing (e.g. One wonders what happens when
a widget is frobbed.) and use that as your entry point. This is a matter of
personal taste/fetish[a].

### Now that One has One's Entry Point... ###

Now that one is staring in the face a chunk, hopefully a small one, of code;
how does one read it?

**Top Down**. It is as simple as that[9].

Read the code, what does it say? Believe it. That can be risky - but at this
point one must do it. Skip over things that are not, or do not seem relevant.
If one's interest is in frobbing ignore code about tweaking or twiddling.
Perhaps one makes a note that frobbing seems to involve tweaking or twiddling;
but one must know about frobbing now so those are **not relevant**[10]. 

It is this point here which I think is most important. One must gain a sense
of what is relevant when reading code. One cannot read every code path and
think that will lead to understanding. That would be like reading the
dictionary and assuming one knows the language. This is where I have seen
programmers fail in their reading.

This is a very good reason why naming is so important[b].

--
[0] It has occurred to me that my style of reading code is not the same as
other's. I have been told by a person I think highly of that they feel my way
is the/a right way. I have finally gotten around to writing it up as a quick
blog post.

[1] Is it time for us to stop calling it 'code' given its implications of
obfuscation. I think it is still appropriate as long as we remember that the
definition is not about obfuscation but about using a set of symbols to mean
other words/letters/symbols. This is, IMNSHO, exactly what we are doing. 

[2] Or its ilk (*e.g.* `ack`) 

[3] New fangled IDEs effectively keep their own tags table.

[4] Gut feeling, hunch, guess work, randomness, luck *&c.*

[5] Especially when at the client site, trying to figure out why the program
is using up all the CPU and the trades are going through. Take my word on it.

[6] Most often code is for reading (and evaluating/compiling) by the computer;
but also for oneself and one's fellow humans[7]

[7] Apologies for being speciest.

[8] Why do we keep referring to code *and* test. Tests *are* code.

[9] Of course it is not that simple.

[10] See [4]. This is very tied to instinct[4].

[a] https://www.google.com/search?q=cat+photobomb

[b] Perhaps a post/rant for another day.

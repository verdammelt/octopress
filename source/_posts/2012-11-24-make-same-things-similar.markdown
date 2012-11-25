---
layout: post
title: "Make same things similar, different things dissimilar"
date: 2012-11-24 14:46
comments: true
categories: code design
---

## Abstract ##

Whilst fixing some bugs in data file parsing code I found that the bugs lie in
the fact that the types of data files were more similar than not; but the code
said that they were more dissimilar than similar. Refactoring to make same
code same fixed at least part of the bugs on its own.

## A Story ##

On my current project we have some code that reads data files and puts the
data into the database. The files come in different formats and layouts,
however there are only really two different kinds of files. I have always
maintained that the processing of these two types of files are more same than
different. *i.e.* How to read an excel file with the data laid out *just so*
and put that data into the database is all the same whereas the way to
validate if *this* line in the file a data line or something to ignore, or how
to split all the data into larger logical chunks (required before putting into
the database) is perhaps different between these two types of files.

I was very involved in the creation of the code for the reading of the first
type of data file; but not very involved for the second. Recently when we
shook out some bugs in the parsing of the second type of file I found myself
in the code for both types of files fixing the bugs.

I found that the code implied that the two files were more different than I
had imagined. Code that I thought would be similar or even exactly the same
was not. This difference could be seen on multiple levels; from the naming of
things up to the factoring of the code into methods and classes.

As I reviewed the bugs I had to fix I saw that the bugs were stating that the
second type of file was in fact not so different from the first type. As far
as the user was concerned much of the "rules" of parsing were exactly the
same.

The first thing I did was make the code for the second type of file much more
similar to the first type. This involved renaming and refactoring. Then once
things were much more the same I extracted the sameness into the base class
(which had already existed). By doing this refactoring at least parts of the
bugs were fixed. All that was left was some tweaking to the code left behind
which defined the *difference*.

## Conclusion ##

This coding really showed to me the importance of keeping a consistency in the
code. Things which are the same should be named and look the same. Things
which are different should *NOT* named the same or look the same; they must be
kept dissimilar.  The compiler doesn't care of course; but I think it will
help the programmer.

Not keeping to this 'rule' I think will lead to bugs where things which should
be the handled in the same or similar manner are mistakenly not since they
appear to the following developers to be different. Or even more simply
because the commonality was not extracted earlier because it was not noticed.

The way to keep this in mind is not not just think if the code is factored
well or has good naming; but also if the code you wrote is similar or
dissimilar to other code around it - and if that is correct or not.


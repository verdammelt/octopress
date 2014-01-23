---
layout: post
title: "only one way of doing things..."
date: 2014-01-20 19:42:43 -0500
comments: true
categories: 
---

{% blockquote Programming as Experience: The Inspiration of Self (1995) %}

	 When there is only one way of doing things, it is easier to
	 modify and reuse code. When code is reused, programs are easier
	 to change and most importantly, shrink. When a program shrinks
	 its construction and maintenance requires fewer people which
	 allows for more opportunities for reuse to be found. Consistency
	 leads to reuse, reuse leads to conciseness, conciseness leads to
	 understanding.

{% endblockquote %}

## Resuse

I like the meaning of 'reuse' in this quote. This is not the 'reuse'
promised by early OO proponents. They promised[^1]: that one would be
able to create objects which would be reused from one project to
another. This is the reuse which means that code is reused *in* a
project. This is the reuse which I believe to be attainable.

It is like a inward-spiral: the more reuse of code the fewer ways to
do a thing there will be which leads to only one way.

The sentence about fewer people is a bit odd - but I feel it is does
make sense. The fewer people on the team the more likey there will be
only one way to do things which means there is by definition more
reuse. 

## Consistency

Perhaps more important than reuse though is consistency. If code is
consistent I have found it to be easier to reason about, because
reasonable assumptions can be made when reading it. Being able to make
reasonable assumptions, and have those borne out, is very important to
me when reading code.

## Conciseness and Understanding

And it follows that with reuse and consistency one will get
consiceness. But does that necessarily lead to underderstanding? That
is something I *feel* is right, but I have seen some concise code
which is hard to understand.

----
*References:*

* "Programming as Experience: The Inspiration of Self", 1995, Smith,
  Randall B and Ungar, David


----

[^1]: Or perhaps that is not what they said, but what we heard.


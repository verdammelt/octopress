---
layout: post
title: "Reflections Upon the Art of Agile Training"
date: 2012-04-28 16:00
comments: true
categories: agile training
---

## What

I am returning home from the [Art of Agile Boot Camp][ArtOfAgile] presented by
[James Shore][JimShore] and [Diana Larsen][DianaLarsen] in New York City.

The training turned out to be review for me given that most of my coworkers
are [Cyrus Innovations][cyrus] employees and they all attended this training
in October of 2011. They came back and implemented some of the ideas from the
training - so in a way I've been living this stuff since then. Even before
that we were a pretty well functioning agile team.

Even though it was a review I still thought it was very beneficial to me.
There are always opportunities to improve; and details/reasonings that had
been forgotten. Old ideas can become new again through re-iteration.

The training was split into two parts. The first two days covered Agile
Planning and the last three Agile Delivery. The latter was what I was most
interested in - but I think I may have gotten just as much out of the first
section.

### 90 Minute Iterations?! - Crazy!

It was in the second half of the class that we got to "experience" Agile
Delivery for ourselves. In our groups we delivered working software four times
in four iterations; each iteration was 90 minutes long. It seemed crazy and a
few times it felt crazy - but we did deliver running software (a cheesy text
based 'game') in 90 minute iterations. During these 90 minutes we did
everything from release planning, to coding (TDD'd naturally), exploratory
testing, and releasing. 

Crazy as it may seem - it is a brilliant exercise. By making us so focused we
needed to organize ourselves, help each other out and really work to remove
all roadblocks. Also it forced us to make, quickly, decisions about what was
going to be in and what was not. We couldn't let ego get in the way and argue
too much about anything; we could always pivot and change our minds later.

### Relearning what Stories are

Even as a well functioning agile team I have to say that there were some
things related to stories that I now think I/We were doing wrong or not so
well.  Firstly, I was reminded that Stories are not requirements. Stories are
conversations about the requirements and they are negotiable. It is really
important that they are small and independent. A story on its own is not
likely to be a complete feature (MMF) - they ought to be much smaller than
that.

Another point about stories that Jim makes a point of is that they should not
be re-estimated. This seemed odd to me so I made a point to discuss it
further. It seemed to me that one should re-estimate a story if more
information is known. For example we may come to know that the implementation
needed for a story is harder than first thought, or easier (perhaps it is
becoming routine). 

Jim's point is that estimates are always wrong, but they should be consistent.
So if something was estimated as a '1'; then anything like it should also be a
'1'; even if find out that it was easier/harder. The reason is because if we
change our estimations then our velocity becomes less meaningful. It is our
velocity that should be changing to reflect our capability for doing N 1-point
stories. That N will go up and down as 1 point stories are harder/easier.

### Velocity: settling

{% pullquote %}

Instead of simply doing [Yesterday's Weather][yesterdaysweather], Jim
suggests letting velocity 'settle'. The way he put it was: 
{" Decrease velocity easily. Increase velocity pessimistically "}.  
The idea is that if you always use Yesterday's Weather that your velocity may
tend to to be erratic, and more importantly that it prevents the team from
having consistent time for [Slack][slack]. While I can understand this
intellectually I find it hard to grok. Perhaps that is because of long
standing bad habits from previous work environments. It is something I'd like
to experiment with.

{% endpullquote %}

### Focus on Delivering Value

Duh. I just needed to be reminded of this.

### Fluencies

Diana and Jim presented an idea of 'Fluency' in Agile Practices. Each level is
useful, none of them are 'bad'.  They are:

 0. We build code.
 1. We create business value.
 2. We *deliver* business value.
 3. We *optimize* business value.
 4. We optimize *our organization's* business value.

The idea is that you are 'fluent' at a level, as with a language, when you can
easily work at that level, even under pressure. I think our current team, and
myself, is largely fluent at the level of delivering business value and
day-to-day we do some work at the level of optimizing that value.

## So What

### The First Thing to Build...

{% pullquote %}

Diana mentioned a good quote: {" The First thing to build is Trust "}. The
idea is that the first thing the team needs to get good at is delivering on
its commitments - consistently.

{% endpullquote %}

### Iteration Planning is a design activity

This is an interesting idea that I need to think more about. The idea is that
because Iteration Planning involves choices about what will be built; that it
affect design.

### People over...

I always find interacting with people who are interested in or driven to
learning very energizing. A change in this time I realized what that now I was
the person who was answering questions of and encouraging people who were new
to Agile. I am starting to realize that I know this stuff and have something
to offer. It was also great to see a coworker doing the same, and doing a
better job than I did.

## Now What

There are some things I want to try for myself and for my team.

### Demos

Right now on my current project we do not have Customer Demos. I said a few
times during the training that my project does not yet have a Customer, but
what it really doesn't have is a User. I think we could start demoing it now
to whoever wanted to see it. At the least demoing to fellow team members may
help us be focused and see a bigger picture.

### Story sizing

Currently our features are not quite *Minimum* Marketable Features. They tend
to be larger than that. Furthermore it seems our Product Manager (the Customer
Proxy) doesn't care much about anything smaller than that. However that is
leaving us with only a story or two per iteration - which is not helping us
achieve a more stable velocity.

I need to do some brainstorming on how we can (or if we should) shrink our
features. Then figure out ways to split stories into smaller chunks so we can
have several per iteration (at least 4). The important thing here is to keep
business value in each story. While I do not think this will magically cause
my Product Manager to care about the smaller stories; but I hope it will help
engage them more if we can show business value progress with each one.

Related to this is the problem that it seems there may be some expectations
about when the current release will be shippable. My current projections are
much further out from those expectations. I need to use tools like Velocity,
Release Planning with Risk calculations (ala [Rabu][rabu] which I currently
use) to bring data to the table in my discussions with the Product and Project
Managers.

### Root Cause Analysis

Now that I've had this review I feel that I and my team have not been doing a
good job of doing root cause analysis on the issues in our process which we
discuss in our Retrospectives. Furthermore we are not doing a good job of root
cause analysis on any bugs that come up.

(On the topic of bugs I want to more seriously have the "Bugs don't happen
here" attitude.)

## Conclusion

In conclusion the training was fantastic - even for someone who is not new to
Agile methodologies. I am bringing back some good ideas which may help me and
my team achieve even better fluency in our work. It also solidified for me
some existing ideas that I thought I/we already did pretty well.

[ArtOfAgile]: http://www.cyrusinnovation.com/index.php/art-of-agile-nyc 
[JimShore]: http://www.jamesshore.com
[DianaLarsen]: http://www.futureworksconsulting.com
[cyrus]: http://www.cyrusinnovation.com
[yesterdaysweather]: http://c2.com/cgi/wiki?YesterdaysWeather
[slack]: http://jamesshore.com/Agile-Book/slack.html
[rabu]: http://www.teamrabu.com/

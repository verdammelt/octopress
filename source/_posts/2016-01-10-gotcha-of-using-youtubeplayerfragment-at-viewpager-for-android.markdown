---
layout: post
title: "Gotcha of using YouTubePlayerFragment and ViewPager for Android"
date: 2016-01-10 17:19:50 -0500
comments: true
categories: android
---

<small>(Cross posted to the [Cyrus Innovation Blog](http://www.cyrusinnovation.com/gotcha-of-using-youtubeplayerfragment-and-viewpager-for-android/))</small>

Recently I learned some Android programming by writing a simple app
for a client. It was a great opportunity to learn the platform and how
"easy" it is to write an app. I ran into one 'gotcha' that I thought
might be valuable to others.

One feature that was needed was a swipeable carousel of YouTube
videos. Google provides some widgets for showing YouTube videos on an
Android device and
[YouTubePlayerFragment](https://developers.google.com/youtube/android/player/reference/com/google/android/youtube/player/YouTubePlayerFragment?hl=en)
was a (almost) perfect fit for my needs[^1]. Also
[ViewPager](http://developer.android.com/reference/android/support/v4/view/ViewPager.html)
was just the thing for creating the swipeable list of items. It was
easy enough to create a subclass of
[FragmentPageAdapter](http://developer.android.com/reference/android/support/v4/app/FragmentPagerAdapter.html)
which knew the list of videos and created YouTubePlayerFragments as
needed (actually a subclass whose job was to handle the initialization
of the YouTubePlayerFragment).

While this was easy to code - it was not so easy to make it actually
*work*.

Trying to play videos resulted in a cryptic message about the player
not playing because it was not visible on the screen. The coordinates
in the error message made it seem like the object was way to the left
of the visible screen. That was the first clue. It was perplexing
though since the player was quite obviously right there *on the
screen*. 

Some debugging gave me the second clue I needed. When I pressed play
on the player on the screen, *multiple* players were firing events
saying that they were playing. *Multiple* players?

Reading[^2] into the documentation of ViewPager some more told me that
it will request multiple views from the ViewPageAdapter, so that other
views are "ready to go". But why did they all respond when I clicked
on one of them?

More debugging did not solve the mystery but solidified my hypothesis:
The YouTubePlayer and/or YouTubePlayerFragment has state shared
between all their instances. That is the only explanation that would
fit the observed behavior.

So I needed a way to ensure that only one YouTubePlayer was in play at
a time. The ViewPager documentation says you can change the number of
other pages that will be created. Changing that did not work for me -
at least one other view was always created. That left me with ensuring
that only one player was *initialized*.

I tried various event listeners but found that none of them fit the
need. Sometimes I would get an event firing both on the active and the
inactive viewer and it was not possible to tell the difference.
Finally I found one thing that did seem consistent and usable:
`setUserVisibleHint`. It was called on the fragment with a `true`
value when that fragment was the one shown to the user and was called
with `false` when it was not. So I made sure my fragment was not
initialized until it got told that it was visible; and then released
it when it was no longer visible.

---

[^1]: Except for the supremely annoying fact that the YouTube player
    widgets *DO NOT WORK* on emulators. So I had to do all this work
    with a physical device tethered to my machine. Like a savage.
    
[^2]: [Reading is Fundamental](http://www.rif.org/)

---
layout: post
title: "OMG Git is scary and amazing"
date: 2012-05-28 19:13
comments: true
categories: git branch
---

 > I just bought a chainsaw - my problems are solved

I created a modification to [lein-midje](https://github.com/marick/lein-midje)
which allowed it to be a `lein new` template to help people get started with
Midje. I submitted a [pull
request](https://github.com/marick/lein-midje/pull/24) and in doing so
realized that I really ought to have done my work on a branch.  *ugh*.

Knowing that Git is super-awesome(TM) I thought there must be some necromatic
incantation to take previous commit and put them on a branch. I was
surprised/horrified to find out how [easy it was](http://stackoverflow.com/questions/1628563/git-move-recent-commit-to-a-new-branch)! (the first answer, at the time of this posting, is the important one).

For the record this is all you need to do:

    git branch <newbranch>
    git reset --hard HEAD~2 # or however far back you want to go
    git co <new branch>

It seemed to easy to I tested it out. I created a new repository with a file
which was empty on the initial commit. I modified it two times committing each
time. Then did the above steps. Then on the master branch I committed a
different change.  Now `git log --all` looks like this (my personal formatting
stolen from
[garybernhardt](https://www.destroyallsoftware.com/screencasts/catalog/pretty-git-logs)):

    virgil:foo(abranch)> git lg --all
    * 0d4d369    (8 minutes)   <Mark Simpson>   (master) after branch
    | * f0101f4  (9 minutes)   <Mark Simpson>   (HEAD, abranch) third co
    | * d8160bf  (9 minutes)   <Mark Simpson>   second commit
    |/  
    * cceb15b    (10 minutes)  <Mark Simpson>   initial commit

Git is scary and cool at the same time. It is a serious chainsaw and you can
get stuff done, but you could also chop your leg clean off.



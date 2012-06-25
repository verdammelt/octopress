---
layout: post
title: "Problems deploying to Heroku after upgrading Octopress"
date: 2012-06-24 20:10
comments: true
categories: heroku octopress
---

Just a note (perhaps for my future self).

I had considerable problems after upgrading Octopress and then trying
to deploy my blog to Heroku.

The problems stemmed from the update to the Gemfile. There were two problems:

Firstly: everything except for `sinatra` was put into the
`:development` group. Heroku runs `bundle --without=development` so
all those gems will be missing.

Secondly: due to an earlier problem with the `pygment` and python
environments I need to keep the following in my Gemfile

    gem 'pygments.rb', '= 0.2.3'
    gem 'rubypython', '= 0.5.1'
	 
After I fixed those two problems deploying to Heroku worked fine.

One bright side is that I now know how to use `heroku
releases:rollback` to shift back to a previous version. This let me
keep my blog up and running while I tried to figure out the problem.
(Not that anyone actually reads it...)



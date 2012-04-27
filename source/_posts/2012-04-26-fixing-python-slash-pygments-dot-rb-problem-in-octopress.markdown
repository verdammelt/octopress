---
layout: post
title: "Fixing python/pygments.rb problem in Octopress"
date: 2012-04-26 22:38
comments: true
categories: octopress 
---

After I posted my last blog post it was reported to me that my code blocks
were no displaying properly. The readers were seeing an error like: `"Liquid
error: Could not open library ‘/usr/local/lib/libpython2.7.a’: ...".`

Some googling informed me that the problem seemed to be somewhere in
RubyPython. The instructions were relatively straightforward - but it wasn't
clear to me if I needed to do *both* of the directions.

The quick answer is yes. To fix this problem one must do the following:

 1. Make sure RubyPython is locked to 0.5.1 in the Gemfile (*i.e.* `gem
    'rubypython', '= 0.5.1'`
 1. Create a file `plugins/ruby_python_heroku_fix.rb` with the contents:
    `RubyPython.configure :python_exe => 'python2.6'` (the filename is not
    actually important).


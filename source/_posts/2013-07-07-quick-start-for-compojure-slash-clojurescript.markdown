---
layout: post
title: "Quick Start for Compojure/Clojurescript"
date: 2013-07-07 18:10
comments: true
categories: 
---

I am once again jumping into the Clojure world and trying to learn a bit of
it. I am doing so via a small project called [defclink][]
([source][defclink-src]). I am also attempting to get back into blogging. So I
thought I'd combine the two items into this short post.

## Goals of my project.

My goal of this project is to learn some Clojure building a webapp. I decided
to also use Clojurescript since it seemed like an interesting idea. I wanted
to keep the number of libraries and frameworks low to maximize the Clojure
code I would need to write, thus learning Clojure. That being said I allowed
myself the luxury of the Compojure library (with Ring under it) to handle the
HTML protocol stuffs.

I'll start by explaining how to get a brand new Compojure project.

## How to set up a Compojure project

Starting a Compojure project is very simple:

    lein new compojure awesome-thing

This will create:

    README.md    project.clj  resources/   src/         test/
    
    ./resources:
    public/
    
    ./resources/public:
    
    ./src:
    awesome_thing/
    
    ./src/awesome_thing:
    handler.clj
    
    ./test:
    awesome_thing/
    
    ./test/awesome_thing:
    test/
    
    ./test/awesome_thing/test:
    handler.clj

and furthermore will setup your project.clj file to pull in compojure.

It sets up simple tests that going to "/" will result in a [success page][200] with
"Hello World" and that going to a non-existant page will result in a [404][].
There is a defined set of routes to accomplish this.

To run the server at this point it is easy to do:

    lein ring server

and then go to `localhost:3000` to see the `awesome_thing`

### Heroku?

At this point you probably want to push this to awesome thing to [Heroku][] to
start get VC funding. This is easy to do (the pushing part).

First create your heroku app in the usual manner (at the time of this writing
you don't even need to choose the cedar stack - but check the docs to make
sure you are Clojure compatible).

Now create a `Procfile` with the following contents:

    web: lein with-profile production trampoline run -m defclink.main $PORT

Now you should be able to push to Heroku and sit back waiting for the funding
to roll in.

[defclink]: http://defclink.heroku.com
[defclink-src]: http://github.com/verdammelt/defclink
[200]: http://httpcats.herokuapp.com/200
[404]: http://httpcats.herokuapp.com/404
[Heroku]: http://heroku.com


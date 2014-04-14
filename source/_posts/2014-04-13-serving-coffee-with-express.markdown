---
layout: post
title: "Serving Coffee with Express"
date: 2014-04-13 19:45:58 -0400
comments: true
categories: coffeescript node express
---

A few weeks ago I was playing around with a new stack:
Node-Express-Angular all in CoffeeScript[^1]. I found it quite easy to
have the Express server compile my CoffeeScript files and then return
the JavaScript to the browser. I then found myself last week in a
position at work where I wanted a little test page to hang the Angular
directives I was working on so I quickly used the same trick.

I'm not saying this trick is bullet-proof, or even a necessarily good
idea for production. But it seems like a good thing for testing and
perhaps for getting a project off the ground with some prototyping. It
also serves as a small example of how to write an Express
Middleware[^2].

With that caveat I will present you with the code and explanation of
it[^3].

{% codeblock lang:coffeescript %}
express = require 'express'
coffee = require 'coffee-script'
fs = require 'fs'

app = express()

app.configure ->
  app.set 'port', process.env.PORT ? 3000

app.use express.logger()

app.use '/client', (request, response, next) ->
  coffeeFile = path.join __dirname, "../client", request.path
  file = fs.read coffeeFile, "utf-8", (err, data) ->
    return next() if err?
    response
      .contentType('text/javascript')
      .send coffee.compile data

app.listen app.get('port'), ->
  console.log 'listening on port %d', app.get('port')

{% endcodeblock %}

The part that concerns us is lines 12-18.

First, the code is saying that if a file with path staring with
`/client` is requested then we'll serve up the coffeescript file of
the same name in the `../client` directory. Of note here is that
`request.path` does not contain the `/client` part of the path and
`__dirname` is the directory of the currently executing file.

Line 14 sets up the reading of this CoffeeScript file. (It is
important to specify the encoding otherwise the Coffeescript compile
will throw an error.) If there is an error reading the file, such as
the file not existing, then we tell express to run whatever is the
next rule (eventually if no other rules work Express will send a `404`
for us). If we can read the file then we use CoffeeScript to compile
that file and send that data back as the response. (Of note here is
that we set the content type to be `text/javascript` to make sure that
the browser does the right thing; it doesn't appear necessary with
Chrome at least, but probably best to do it.).

Congratulations, we've just written an Express Middleware! 

----

[^1]: It is my current opinion that CoffeeScript is better than
      writing directly in JavaScript. It saves the developer from
      making some very basic stupid mistakes with JavaScript and also
      removes some of the syntatic noise.

[^2]: [](http://expressjs.com/4x/api.html#middleware)

[^3]: The toy app bootstrapping kit I mentioned at the top of this
      post is in my
      [expressular-kit](https://github.com/verdammelt/expressular-kit).


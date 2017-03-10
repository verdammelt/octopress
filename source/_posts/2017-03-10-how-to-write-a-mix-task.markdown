---
layout: post
title: "Writing Mix tasks for fun and profit."
date: 2017-03-10 07:11:29 -0500
comments: true
categories: elixir mix
---

I'm beginning to learn a little Elixir & Phoenix and I ran into a case
where I wish I had a Mix task for something. Specifically I wanted to
run `npm` scripts with mix so I'd only have one command to run instead
of both `mix` and `npm` for my toy Phoenix project.

Writing a Mix task is reasonably straightforward with only a few
steps:

1. If you want to create a mix task called "echo" then create a module
   called `Mix.Tasks.Echo`. The task name seen in `mix help` is based
   upon the name of the module minus `Mix.Tasks`. (The module needs to
   be called `Mix.Tasks.Something` otherwise `mix` will not see it.)
2. Add `use Mix.Task` to this module.
3. Write a public method called `run`. It has the type signature:
   `run([binary]) :: any`. That means that it will get a list of
   strings (the command line arguments) and can return anything.
3. Add a `@shortdoc`. This will be used as the text in `mix
   help`. Without this your task will not appear in `mix help` but
   will still be usable.
4. Optionally add a `@moduledoc`. This will be used if you run `mix
   help YOURTASK`

You can put this module where ever you want in `lib` but typically you
would put it into `lib/mix/tasks`.

That's it.

An interesting thing I found was that step #2 was not actually needed.
That behaviour defines `@shortdoc` so without it you cannot use
`@shortdoc` to add the task to `mix help` output.

Since I was creating a mix task for use in a build I needed to make
sure that if the task was not successful that `mix` would return an
error code so that the shell could see the error and fail a build. At
first I assumed that the return value of the task was how that would
be done; however I didn't find much documentation about this. I
experimented with some likely return values like `:error` or `{:error,
"something"}` but that had no effect, it always returned a zero exit
status to the shell. Ultimately I choose to raise an error when the
task didn't work and that definitely caused a non-zero exit status.

If you want to see the end of result of this experimentation you can
check out my *first ever hex package*:
[mix-npm](https://hex.pm/packages/mix_npm). The source can be found
in the GitHub repository:
[verdammelt/mix_npm](https://github.com/verdammelt/mix_npm). 


---
layout: post
title: How to write a Heroku Buildpack for Fun and / or Profit
date: 2020-11-13 08:55:15 -0500
descrxiption: Summary of how to write a Heroku Buildpack
comments: true
categories: heroku buildpack
---

Heroku buildpacks are used to prepare (/e.g./ build/compile) an application to allow it to be run by Heroku on their dynos. There are many that exist so it is not likely that you will need to write your own. And that is quite true for the one I wrote. But I wrote one partly to find out how to do it, so let me share what I learned.

The [API for Buildpacks][heroku-buildpack-api] is pretty simple and it can be easy to write one. The API is three scripts that will be run by Heroku when it runs the buildpack: `detect`, `compile`, `release`. Buildpacks are [git][git] repositories so it is common to host them on [GitHub][github] (but that is not *required*).

While I say that the API is simple, I hope it is useful to summarize details of the API here. Perhaps restating it with my own words will help others (or just me in the future).

## Environment that the buildpack is run in

Buildpacks are run on the same [stack][heroku-stack] as the application is.

Buildpacks are run in their own directory. This is *not* the directory where the application code is. Also this buildpack directory is not available to later buildpacks nor the application. So if the buildpack creates build artifacts those must be put somewhere else.

Besides the buildpack directory there are three other directories available to the buildpack: 

* `BUILD_DIR`: this is the directory where the application code is.
* `CACHE_DIR`: this is a directory which can be used to cache build artifacts (see below).
* `ENV_DIR`: this is a directory which contains information about the [Heroku Config Vars][heroku-confi-vars] (see blow).

## `bin/detect`

This script's job is to decide if this buildpack should be run. It is passed a single argument, the `BUILD_DIR`. This script typically will work by checking for a particular file in `BUILD_DIR`. If the buildpack should not run the script should return a non-zero value. If the buildpack should run then besides a zero return value it must also print to standard output a "human readable" name. This will show up in the build logs and shows that the buildpack is chosen.

## `bin/compile`

This script is a huge part of a build pack. It has the job of compiling/preparing the application. It is passed three arguments: `BUILD_DIR`, `CACHE_DIR` and `ENV_DIR`.

There are two environment variables available to the compile script:

* `STACK`: which [stack][heroku-stack] the buildpack is running on
* `SOURCE_VERSION`: the "version". For applications deployed via git pushes that will be a commit SHA.

[Heroku Config Vars][heroku-config-vars] *are not* available as environment variables to the buildpack. But they are available via the `ENV_DIR` (see below). 

Any output to standard output will appear in the build log. It is recommended that buildpacks output messages in ways that fit the style of the other parts of the build logs (see below for some shell script functions to help with this).

If a buildpack needs to communicate environment to next buildpack it can write a script `export` in the buildpack's directory which will be executed before the next buildpack is run.

If a buildpack needs to communicate environment to the application (*e.g.* `PATH`) it can write shell scripts to `BUILD_DIR/.profile.d`. These will be run during dyno startup. They will be run *after* the [Heroku Config Vars][heroku-config-vars] are set in the environment. Each script should be named with a `.sh` suffix. There is no guarantee to the ordering which these files will be executed.

## `bin/release`

The release script is run after compilation and returns meta data back to the build process. It is passed a single argument, the `BUILD_DIR`.

It must return, on standard output, a YAML formatted hash with upt to two keys: `addons` and `default_process_types`.

Any `addons` specified will be added to the application the first time it is deployed. The `default_process_types` key defines default `Procfile` entries to use.

A good start is with the following script which creates an empty YAML hash. It can be expanded with the required keys when needed: 

```sh
#!/bin/sh

cat << EOF
---
EOF
```

## `CACHE_DIR`

The `CACHE_DIR` is a directory that can be used to store build artifacts between builds. For example if a buildpack downloads and installs some software, it can store that in `CACHE_DIR` and then skip the download and install the next time.

Note, the API specifies that the `CACHE_DIR` may not exist, so if `bin/compile` wants to use it it should ensure it exists before doing so.

## `ENV_DIR`

This directory contains files for each [Heroku config var][heroku-config-vars]. For a [config var][heroku-config-vars] `FOO=bar` there will be a file `FOO` with the contents `bar`.

## `bin/compile` logging helpers

Since the compile script *should* use output format that is similar to the rest of the build process the following shell functions may be useful

```sh
log_header() {
  echo "-----> " $*
}

indent() {
  sed -u 's/^/       /'
}

log() {
  echo $* | indent
}
```

They can be used like this:

```sh
log_header "Staring Build..."

cat output.txt | indent

log "Build complete."
```

which will produce:

```
-----> Starting Build...
       ...contents of output.txt...
       Build complete.
```


[git]: https://git-scm.com
[github]: https://www.github.com
[heroku-buildpack-api]: https://devcenter.heroku.com/articles/buildpack-api
[heroku-config-vars]: https://devcenter.heroku.com/articles/config-vars
[heroku-stack]: https://devcenter.heroku.com/articles/stack

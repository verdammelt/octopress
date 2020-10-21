---
layout: post
title: "TDD in Common Lisp: recursive yak-shaving"
date: 2013-12-25 17:34:59 -0500
comments: true
categories: commonlisp lisp tdd yakshaving
---

While avoiding family this Christmas-day I started trying to figure out way
for me to do TDD in Common Lisp (as one does...). That led to SLIME[^1] and
    QuickLisp[^2] and lisp-unit[^3] and asdf[^4] (*&c. &c*).

## ...it's yaks the whole way down.

The hardest part for me was to find a simple way to load my code and run the
tests. ASDF ships with `asdf:test-system` defined but it does nothing by
default[^5]. So I did some digging around and saw some other's solutions and
synthesized my version.

Here is an example ASDF system definition for a Game of Life[^6]
implementation.

{% codeblock lang:common-lisp %}
(asdf:defsystem #:gol
  :description "Conways Game of Life in Lisp"
  :author "Mark Simpson <verdammelt@gmail.com>"
  :version "0.0.0"
  :depends-on ("lisp-unit")
  :components ((:module "src"
			:serial t
			:components ((:file "package")
				     (:file "gol"))
                (:module "test"
			:serial t
            :depends-on ("src")
			:components ((:file "package")
				     (:file "gol-test"))))
  :in-order-to ((test-op (load-op :gol)))
  :perform (test-op (o c) 
		    (progv
			(list (intern "*PRINT-ERRORS*" :lisp-unit)
			      (intern "*PRINT-FAILURES*" :lisp-unit))
			'(t t)
		      (funcall (find-symbol "RUN-TESTS" :lisp-unit) 
			       :all :gol-test))))
{% endcodeblock %}

## My God... it's full of yaks

I'm just going to let that sink in for a bit while I get some coffee.

Ok, now that I'm back I will explain each part. The first interesting bit is
on line 6:

{% codeblock depends-on lang:common-lisp %}
  :depends-on ("lisp-unit")
{% endcodeblock %}

This line tells ASDF that it should find and load a system called `lisp-unit`
because our system depends upon it. This is where QuickLisp makes things
simple since that is its job and it does a fine one at that.

Next is the definition of our components:

{% codeblock Defining the Components lang:common-lisp %}
  :components ((:module "src"
			:serial t
			:components ((:file "package")
				     (:file "gol"))
                (:module "test"
			:serial t
            :depends-on ("src")
			:components ((:file "package")
				     (:file "gol-test"))))
{% endcodeblock %}

I've decided that my project should have two main directories, one to contain
all the production source code and one for all the test source code. Each one
will be in their own packages, with the `:gol-test` package `:use`-ing the
`:gol` package. `:serial t` by the way tells ASDF that each item in the
component list depends upon the one before it.

Now the hairier parts which tell ASDF to run our tests:

{% codeblock Telling ASDF How to Test Our System lang:common-lisp %}
  :in-order-to ((test-op (load-op :gol)))
  :perform (test-op (o c) 
		    (progv
			(list (intern "*PRINT-ERRORS*" :lisp-unit)
			      (intern "*PRINT-FAILURES*" :lisp-unit))
			'(t t)
		      (funcall (find-symbol "RUN-TESTS" :lisp-unit) 
			       :all :gol-test))))
{% endcodeblock %}

The first line is simply stating that in order to do `test-op` ASDF needs to
perform `load-op` on the `:gol` system. This way every time we run the tests
we'll reload the system if needed.

Now... this next bit probably shows how rusty my Lisp is. Maybe there is an
easier way. Basically we want to run `(lisp-unit:run-tests :all :gol-test)`
with `lisp-unit:*print-errors*` and `lisp-unit:*print-failures*` both bound to
`t` (they default to `nil` and that doesn't give enough info IMNSHO). However
when Lisp is reading and evaluating this code `lisp-unit` has probably not yet
been loaded - so we have to be crafty and find the symbol by name in the
package then `funcall` it. Binding the variables was trickier but I stumbled
upon `progv`[^7] and that seems to be just what I needed.

`progv` creates new dynamic bindings for the symbols in the list which is its
first argument. These symbols are determined at runtime. That means we can use
`intern` to find or create these symbols in the right package[^8]. `progv`
binds these symbols to the values in the list which is its second parameter
and then finally executes the sexp which is its third argument in an
environment which contains these new bindings.

With this work done I can now type in `(asdf:test-system 'gol)` into my REPL
and it loads and runs my tests and gives me useful output of those tests. I
might go so far as to bind that to a very short function name, or even a key
in Emacs.

## There are still more yaks to shave.

What is left to be determined is if this is the best way to do things. 

Some documentation/blogs I read lead me to believe that putting the tests in
the same system with the production code is *verboten* (or at least a
*no-no*). I tried having the tests be in their own system definition
(depending upon the production code) but then ASDF & QuickLisp both strongly
pushed me to have that definition it its own `.asd` file[^9] which seemed
awkward to me. I personally have no problem shipping tests with the production
code, and I believe that if needed all the symbols of the test package could
be `unintern`-ed before an image was saved if desired.

I'll play around with this setup and see how things go.

--- 
[^1]: http://www.common-lisp.net/project/slime/

[^2]: http://www.quicklisp.org/

[^3]: https://github.com/OdonataResearchLLC/lisp-unit

[^4]: http://common-lisp.net/project/asdf/

[^5]: http://common-lisp.net/project/asdf/asdf/Predefined-operations-of-ASDF.html#test_002dop

[^6]: Really? You don't know what this is already and you had to look in the 
    footnotes? Go look it upon Wikipedia already!

[^7]: http://www.lispworks.com/documentation/HyperSpec/Body/s_progv.htm#progv

[^8]: Perhaps I should use `find-symbol` instead so that I don't create
    symbols that the package doesn't export. I will experiment with that.

[^9]: since they look up the defintion by looking for a file with the same
    name as the system

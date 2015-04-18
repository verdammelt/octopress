---
layout: post
title: "Bootstrapping a Testing Library"
date: 2015-04-18 14:43:22 -0400
comments: true
categories: tdd lisp
---

## Abstract ##

What's a person to do when one prefers developing in a TDD style and
decides to start a project where nothing not directly in the language
needs to be written? Why write a testing library of course! But...
without a testing library how can one write this testing library in a
TDD fashion? Herein is how I went about doing it.

(Full disclosure: this is not the first time I've tried this sort
thing[^1]. But I had forgotten I had done it before until I was
writing this article.)

## Why? ##

> "If you wish to make an apple pie from scratch, you must first
> invent the universe." -- Carl Sagan

I have decided to have a crazy project wherein I'll write an
application in Common Lisp and *only* Common Lisp. That is to say, no
other libraries. I have allowed myself to use extensions provided by
the the implementation SBCL[^2] so luckily I won't need to write my
own socket and threading extensions.

This is a crazy and stupid idea. But the point of the project is to
give me a place to play around with things I don't normally deal with
and in a language that I like to play with.

## Test Driving a Testing Library ##

### Where to start? ###

Common Lisp has no built in testing library, but it does have
`assert`[^3]. If you have `assert` you can write a testing library.
The problem is writing the first test. I puzzled it over a little and
decided I'd need a function which would take an expression to evaluate
(the test) and would return some data structure which would indicate
the results of the test. Given that here is the first test:

```lisp
(assert (assoc :failure (test::collect-test-results (assert nil))))
```

So this is asserting that the return value of `collect-test-results`
when applied to `(assert nil)` will be an alist[^4] which will
have a `cons` cell whose `car` is `:failure`.

This test directly implies the following test:

```lisp
(assert (not (assoc :failure (test::collect-test-results (assert t)))))
```

That is to say: if the expression does not raise an exception there
will *not* be such an element in the returned alist.

After implementing a macro which lets those test pass I wrote some
more tests to round out what I thought would be a useful implmentation
of this base function of the library. I now had these tests to
bootstrap my library.

```lisp
(assert (assoc :failure (test::collect-test-results (assert nil))))
(assert (not (assoc :failure (test::collect-test-results (assert t)))))
(assert (equal (assoc :value (test::collect-test-results 'foo)) '(:value . foo)))
(assert (assoc :duration (test::collect-test-results 'foo)))
(assert (assoc :start (test::collect-test-results 'foo)))
(assert (assoc :end (test::collect-test-results 'foo)))
(format t "~A...PASSED~&" 'test::collect-test-results)
```

With this I felt that I had enough testing to make me feel confident
in my little implementation. It wasn't perfect - but good enough for
me to now *use* this function to test other parts of my library.

### How to write a test ###

With `collect-test-results` I had a way to writing and running
individual simple tests. But it wasn't a very convenient thing to use.
But what it let me do is now write tests for `deftest` which would let
me define tests. I started by writing the sort of test I wanted to
write:

```lisp
(deftest a-simple-failing-test
    "This is a very simple test which fails"
  (assert (= 5 (+ 2 2))))
```

Through a few tests, written using `collect-test-results` I determined
that `deftest` would intern a symbol with the same name as the first
argument of the `deftest`, bind its function property to a function
which when called would, by calling `collect-test-results` evaluate
the body of the `deftest`. These symbols were put into a list which
could be retrieved from the library. Furthermore, defining a test with
the same name as an existing test does not create a duplicate test.

It might be clearest to just show you how these tests (and an
extracted helper function) ended up:

```lisp
(defmacro assert-no-failure (&body assertion)
  (let ((failure (gensym "fail")))
    `(let ((,failure (assoc :failure (test::collect-test-results
                                       (assert ,@assertion)))))
       (assert (not ,failure) () (format nil "~A" ,failure)))))

(deftest a-simple-failing-test
    "This is a very simple test which fails"
  (assert (= 5 (+ 2 2))))

(let ((test-list (test::test-list)))
  (assert-no-failure (equal test-list '(a-simple-failing-test)))
  (assert-no-failure (fboundp (car test-list)))
  (assert-no-failure (assoc :failure (funcall (car test-list))))
  (assert-no-failure (string= "This is a very simple test which fails"
                              (documentation (car test-list) 'function)))
  (assert-no-failure (equal (assoc :test-name (funcall (car test-list)))
                            '(:test-name . test-test::a-simple-failing-test))))

(deftest a-simple-failing-test
    "This is a very simple test which fails"
  (assert (= 5 (+ 2 2))))

(assert-no-failure (= (length (test::test-list)) 1))

(deftest a-simple-passing-test
    "This is a very simple test which passes"
  (assert (= 4 (+ 2 2))))

(assert-no-failure (= (length (test::test-list)) 2))

(format t "~A...PASSED~&" 'test:deftest)
```

### Running tests ###

Now that we can define tests and evaluate them all that is left is to
have a convenient way to run the defined tests. Three quick tests on
the output of `run-all-tests` were proof enough for me (the tests that the
call to `run-all-tests` would run were the ones defined above, one
passing and one failing) that it would execute each test, report which
ones failed and a count of passes and fails to `*standard-output*`.:

```lisp
(let ((*standard-output* (make-string-output-stream)))
  (run-all-tests)
  (let ((output (get-output-stream-string *standard-output*)))
    (assert-no-failure (search "A-SIMPLE-FAILING-TEST...FAILED." output))
    (assert-no-failure (search "PASSED: 1" output))
    (assert-no-failure (search "FAILED: 1" output))))
(format t "~A...PASSED~&" 'test:run-all-tests)
```

### Recap ###

At this point my testing library has two main entry points: `deftest`
and `run-all-tests`. To create them, I first used `assert` to test
drive the creation on a lower-level function `collect-test-results`,
which I then used to test drive `deftest`, which I then used to test
drive `run-all-tests`.

## Next Steps and Thoughts ##

Now that I have this testing library I can use it to test drive the
rest of the application I will write. I'm sure along the way I'll be
extending this library as I find new requirements for it. I'll
probably also be writing some assertion library to make the tests more
expressive.

The resulting tests[^5] and code[^6] are in my GitHub repository for this
project: yakshave[^7].

---

[^1]: <a href="http://code-and-cocktails.herokuapp.com/blog/2011/04/11/writing-a-unit-test-framework-in-a-language-y/">http://code-and-cocktails.herokuapp.com/blog/2011/04/11/writing-a-unit-test-framework-in-a-language-y/</a>

[^2]: <a href="http://www.sbcl.org/">http://www.sbcl.org/</a>

[^3]: <a href="http://www.lispworks.com/documentation/HyperSpec/Body/m_assert.htm#assert">http://www.lispworks.com/documentation/HyperSpec/Body/m_assert.htm#assert</a>

[^4]: <a href="http://www.lispworks.com/documentation/HyperSpec/Body/26_glo_a.htm#association_list">(or association list) "*n. a list of conses representing an association of keys with values, where the car of each cons is the key and the cdr is the value associated with that key.*"</a>

[^5]: <a href="https://github.com/verdammelt/yakshave/blob/53348569c40aed951fbeb90ff78d423e25a39db7/test-test.lisp">https://github.com/verdammelt/yakshave/blob/53348569c40aed951fbeb90ff78d423e25a39db7/test-test.lisp</a>

[^6]: <a href="https://github.com/verdammelt/yakshave/blob/53348569c40aed951fbeb90ff78d423e25a39db7/test.lisp">https://github.com/verdammelt/yakshave/blob/53348569c40aed951fbeb90ff78d423e25a39db7/test.lisp</a>

[^7]: <a href="https://github.com/verdammelt/yakshave">https://github.com/verdammelt/yakshave</a>

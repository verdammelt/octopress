---
layout: post
title: "Mocking class constructor in Python with Mockito"
date: 2015-01-18 20:08:59 -0500
comments: true
categories: python mockito
---

In the current code I'm working on we once and a while want to mock
the constructor of a class. It is only really needed because we have a
few classes who sadly do heavy-lifting in their constructors.

The common wisdom on the team was "you can't do that", but it bugged
me and I eventually googled the right things and found out how to do
it. The moment I did it myself I realized that it was obvious. Let me
explain.

In [Python Mockito][https://code.google.com/p/mockito-python/] the
standard form of stubbing is done with the `when` function, operating
upon an object:

``` python
when(obj).method(arg1, arg2).thenReturn(5)
```

This states that `when` `obj.method` is called with arguments `arg1`
and `arg2` then return `5`. (There are other things to do besides
`thenReturn` but for purposes of this discussion that is enough).

What about if you want to mock a constructor? The naïve approach is to
try:

``` python
when(Klass).__init__(arg1, arg2).thenReturn(fakeKlassInstance)
```

But that doesn't work. It will return an error equivalent to "NoneType
does not have an attribute thenReturn".

Making it work is pretty simple. Let's say that `Klass` is defined in
a module called `klass`. Then we can do the following:

``` python
import klass
when(klass).Klass(arg1, arg2).thenReturn(fakeKlassInstance)
```

It works because a module is an object on which the classes are
methods! It was so obvious when I saw it work. The clues were right in
from of my face, calling the constructor of a class is as simple as
using the class name *as if* it were a function. That's because *it
is*! I'd like to blame too many years of Java & C# where "importing"
is more about telling the linker where to find things than about
creating objects that can be manipulated.

So to sum up: a class is a method on a module which returns an
instance of that class. When you import a module you are creating a
variable of that name bound to an object which represents that module.

---

Here is a test file which can be used to play with this idea. Note it
uses the fact that the name of the current modules is bound to a
variable called `__name__` and that `sys.modules` is a hash of all
modules.

``` python
import sys
import mockito

class Foo(object):
    def __init__(self):
        self.x = 5

    def method(self):
        return 10


f = Foo()
print f.method()
mockito.when(f).method().thenReturn('blah')
print f.method()

# This will not work and throw an error.
# print Foo()
# mockito.when(Foo).__init__(mockito.any()).thenReturn('blah')
# print Foo()

print Foo()
mockito.when(sys.modules[__name__]).Foo().thenReturn('blah')
print Foo()
```

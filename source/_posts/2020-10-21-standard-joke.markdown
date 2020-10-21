---
layout: post
title: "Standard Joke"
date: 2020-10-21 09:10:18 -0400
comments: true
categories: commonlisp lisp
---

Arabic-to-Roman number conversion is a common programming exercise,
often used as a TDD exercise. It is an exercise on many
Exercism.IO[^i] language tracks including my own track for Common
Lisp[^ii].

So how do you solve this in some arbitrary programming language?

Typically people write some code to loop through a mapping of numeric
values to roman numeral digits and do repeated decrements while
accumulating the roman numeral digits. That is to say if you start
with `1970` and your mapping contains `1000 => "M"; 900 => "CM"; 500 =
"D"` you decrement by 1000 and accumulate `"M"`, then since the
resulting number is under 1000 you try the next mapping, decrement by
900 and accumulate `"CM"` etc.

How do you do this in Common Lisp?

`(format t "~@r" 1970)`

Yes: Built. In. To. The. Language. (In fact using `~@:r` will provide
output as using the alternate roman numeral format which does not have
special cases for numbers like 4. _i.e._ it will output "IIII" rather
than "IV".)

Common Lisp[^iii] is a language with an ANSI specification[^iv]. The
specification process went from the early-to-mid 1980's to the
mid-1990s. Its goal was to create a single "common" Lisp collecting
the good bits from all the splintered Lisp languages used at the time.
I've heard that it involved a good amount of "horse-trading" as each
interested party tried to get the resulting language to contain their
special or idiosyncratic feature. So how did it come to have this odd
feature?

With a little digging I have found the real story: It was a _joke_.

In "The Evolution of Lisp"[^v] Richard Gabriel explains that in 1974
Guy Steele Jr put roman numeral handling into MacLisp[^vi] as a hack.
`BASE` and `IBASE` were variables which specified the output and input
bases for numbers. Before his hack they were limited to vales between
2 and 36. Steele added the ability for them to be set to `ROMAN`. Thus
if set code like `(+ i 1)` would evaluate to `ii` since the expression
would have been read in as the equivalent of `(+ 1 1)` and upon output
the value `2` would be represented in roman numerals. (It seems in the
original announcement of this 'feature' that you could also set `BASE`
and `IBASE` to `CUNEIFORM` which would cause your Lisp to become
wedged. Oh so witty.)

From that time this feature became a bit of a traditional hack - being
ported to ZetaLisp[^vii] as part of `FORMAT`.

Thus when Common Lisp was being created this feature was included in
`FORMAT`[^viii] as it was a normal feature of that function in the Lisps
that Common Lisp was being aggregated from.

Since then this feature also found its way into Clojure[^ix] as part
of its `cl-format`[^x] function.

---

[^i]:  https://exercism.io/my/tracks

[^ii]:  https://exercism.io/my/tracks/common-lisp

[^iii]:  https://en.wikipedia.org/wiki/Common_Lisp

[^iv]:  https://webstore.ansi.org/Standards/INCITS/INCITS2261994S2008

[^v]:  https://www.dreamsongs.com/Files/HOPL2-Uncut.pdf p80

[^vi]:  https://en.wikipedia.org/wiki/Maclisp

[^vii]:  https://en.wikipedia.org/wiki/Lisp_Machine_Lisp

[^viii]:  http://l1sp.org/cl/format

[^ix]:  https://clojure.org

[^x]:  https://clojuredocs.org/clojure.pprint/cl-format


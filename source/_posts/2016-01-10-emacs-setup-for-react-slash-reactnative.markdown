---
layout: post
title: "Initial Emacs Setup for React/ReactNative"
date: 2016-01-10 16:09:42 -0500
comments: true
categories: emacs react reactnative
---

It looks likely that I'll be doing some ReactNative work soon so I
took some time to start setting up my Emacs environment. All my
relevant setup can be found in the
[init-react.el file in my GitHub dotfiles repository](https://github.com/verdammelt/dotfiles/blob/master/.emacs.d/init-react.el).
This is likely to change so the previous link may not match the code
below. The code below matches specifically the
[initial version (59e7728)](https://github.com/verdammelt/dotfiles/commit/59e7728c3743961b49fcdd8012703c4a46b9ee65).

Hereinbelow I will add more annotation to those already found in that
file along with snippets of code.

The first thing that needed to be set up was a mode for React code.
React code files can mix Javascript with HTML markup and it does not
appear that js-mode (the built-in JavaScript mode handles that). After
a short Googling it looks like [web-mode](http://web-mode.org/) is a
mode that can handle it. After some brief testing it does appear to
work reasonably. It appears that the React/ReactNative community has
not decided to use `*.js` or `*.jsx` as the extension for the code
files and since `web-mode` appears to handle JavaScript just fine I
chose to use it in all cases.

```lisp
(add-to-list 'auto-mode-alist '("\\.jsx?$" . web-mode))
```
The next thing I wanted to get set up was a linter. I thought this
especially important as React uses an ES6 dialect of JavaScript which I
am not entirely familiar with yet and a linter can help me "do the
right thing". With a suggestion from a coworker (who has done some
React work) I chose [ESLint](http://eslint.org/) with the
[AirBnB](https://www.npmjs.com/package/eslint-config-airbnb)
configuration settings. These defaults prompted me to standardize on two
spaces for indentation. (Setting `js-indent-level` as js-mode is still
in use for JSON files.)

```lisp
  (setq web-mode-markup-indent-offset 2
        web-mode-css-indent-offset 2
        web-mode-code-indent-offset 2)
  (setq js-indent-level 2)
```

Setting up the linter to run via [flycheck](http://www.flycheck.org/)
took a small amount of work since I don't like to install tools used
by a project globally. (I know that this is contrary to current mores,
but I have been tripped up by global vs. local installations before so
I shy away from them when I can.) 

First I needed to integrate NVM with Emacs so that Emacs could run
ESLint at all.

```lisp
(require 'nvm)
(nvm-use (caar (last (nvm--installed-versions))))
```
The choice to use the last version found is totally arbitrary. If and
when I get more versions of Node.js on my machine I'll have to make a
more careful choice.

Next I hooked into [projectile](http://batsov.com/projectile/) to look
for a locally installed ESLint and use it if found. The
`projectile-after-switch-project-hook` functions are called after
Projectile has switched directories to the project so one can simply
check the project for the desired file.

```lisp
(add-hook 'projectile-after-switch-project-hook 'mjs/setup-local-eslint)

(defun mjs/setup-local-eslint ()
    "If ESLint found in node_modules directory - use that for flycheck.
Intended for use in PROJECTILE-AFTER-SWITCH-PROJECT-HOOK."
    (interactive)
    (let ((local-eslint (expand-file-name "./node_modules/.bin/eslint")))
      (setq flycheck-javascript-eslint-executable
            (and (file-exists-p local-eslint) local-eslint))))
```

(Note: the function is interactive because I found at least a few
times I was looking at a JavaScript file which I had come to *not* via
projectile. By making it interactive lets me use it manually in the
rare case I need to.)

Flycheck's ESLint integration is limited to only certain modes and
`web-mode` is not one of them so I needed to add that to the
white-list of modes

```lisp
  (with-eval-after-load 'flycheck
    (push 'web-mode (flycheck-checker-get 'javascript-eslint 'modes))))
```

With that I can easily write React/ReactNative code with all the bells
and whistles I like.

Later I will add support for building and testing I'm sure. But first
I need to determine what building & testing in a ReactNative
environment will even look like.







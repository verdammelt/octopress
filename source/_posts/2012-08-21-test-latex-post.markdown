---
layout: post
title: "test latex post"
date: 2012-08-21 21:21
comments: true
categories: LaTeX
---

I was prompted by [Steven Proctor's post][latex-wordpress] about using
[$$\LaTeX$$][LaTeX] on [WordPress][] to see if it could be done on
[Octopress][]. Of course it can!

A quick googling turned up a [Eason's Blog][panchoat] about doing just this.
His post links to [another][another-post] which is in Chinese but the code
snippets are all you need. Note that Eason's post points out that `config.yml`
needs to be updated... something left out of the other.

(Also a note: leave a blank line above the `$$` starting a multi-line
$$\LaTeX$$ block for best results.)

And now for a test

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
    = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
      & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
            \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
                  \vdots & \ddots & \vdots \\
                        \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
                            \end{array} \right)
        \left( \begin{array}{c}
              y_1 \\
                    \vdots \\
                          y_n
                              \end{array} \right)
        \end{align*}
$$

Looks pretty good.

I think Knuth would be pleased. 

![Knuth][Knuth]


[latex-wordpress]: http://proctorit.wordpress.com/2012/08/21/latex-in-wordpress/
[LaTeX]: http://www.latex-project.org/
[WordPress]: http://wordpress.org/
[Octopress]: http://octopress.org/docs/
[panchoat]: http://panchoat.org/blog/2012/06/03/latex-support-of-octopress/
[another-post]: http://chen.yanping.me/cn/blog/2012/03/10/octopress-with-latex/
[Knuth]: http://www.catonmat.net/blog/wp-content/uploads/2010/02/young-donald-knuth-ibm-650-1958.jpg "Knuth using Emacs"

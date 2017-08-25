## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
*   [4 Resources](#Resources)

## Introduction

[SLIME](http://www.common-lisp.net/project/slime/) (Superior Lisp Interaction Mode for [Emacs](/index.php/Emacs "Emacs")) provides a development environment for [SBCL](http://www.sbcl.org) (detailed in this article), [CMUCL](http://www.cons.org/cmucl/), [CLISP](http://clisp.cons.org/) and other [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language) implementations.

The components required are:

*   **emacs**
*   **sbcl**
*   **slime**

## Installation

[Install](/index.php/Install "Install") the [emacs](https://www.archlinux.org/packages/?name=emacs), [sbcl](https://www.archlinux.org/packages/?name=sbcl), and [slime-git](https://aur.archlinux.org/packages/slime-git/) packages. Alternatively, slime can be installed with [quicklisp](https://www.quicklisp.org/beta/).

## Configuration

*From the [.INSTALL](http://pkgbuild.com/git/aur-mirror.git/plain/slime-cvs/slime.install) file.*

To make use of slime, add the following lines to your [init file](http://www.gnu.org/software/emacs/manual/html_mono/emacs.html#Init-File):

```
(setq inferior-lisp-program "/path/to/lisp-executable")
(add-to-list 'load-path "/usr/share/emacs/site-lisp/slime/")
(require 'slime)
(slime-setup)

```

Then run `M-x slime` from within emacs.

Alternatively, for a fancier slime setup, you can change the above lines to:

```
(setq inferior-lisp-program "/path/to/lisp-executable")
(add-to-list 'load-path "/usr/share/emacs/site-lisp/slime/")
(require 'slime)
(slime-setup '(slime-fancy))

```

## Resources

*   [The Common Lisp wiki](http://www.cliki.net/)
*   [Practical Common Lisp](http://www.gigamonkeys.com/book/)
*   [Structure and Interpretation of Computer Programs](http://mitpress.mit.edu/sicp/full-text/book/book.html)
*   [Paul Graham's Lisp resources](http://www.paulgraham.com/lisp.html).
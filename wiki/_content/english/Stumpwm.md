StumpWM is a tiling, keyboard driven X11 window manager written entirely in Common Lisp.

The successor to the cult classic [Ratpoison](/index.php/Ratpoison "Ratpoison"), StumpWM adds all the flexibility and hackability of Common Lisp, allowing the user to make modifications to the source of the window manager even while it is running. It is also known as "the emacs of WMs."

From [StumpWM's homepage](https://stumpwm.github.io/):

	"StumpWM attempts to be customizable yet visually minimal. There are no window decorations, no icons, and no buttons. It does have various hooks to attach your personal customizations, and variables to tweak.

*   Hack the good hack
*   Debug your good hack
*   Customize your window manager

	While it's running That's right. With a 100% Common Lisp window manager there's no stopping the hacks. Just re-eval and GO!"

Want to see it in action? A StumpWM user created a [video](http://www.archive.org/details/TheStumpWMExperience).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 With SBCL](#With_SBCL)
    *   [1.2 With Clisp](#With_Clisp)
*   [2 Documentation and Support](#Documentation_and_Support)
*   [3 Tweaking](#Tweaking)
*   [4 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/). It supports multiple common-lisp implementations.

SBCL is recommended for maximum performance.

### With SBCL

Install these packages in the following order:

*   [sbcl](https://www.archlinux.org/packages/?name=sbcl)
*   [clx-git](https://aur.archlinux.org/packages/clx-git/)
*   [cl-ppcre](https://aur.archlinux.org/packages/cl-ppcre/)
*   [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

### With Clisp

Install these packages from AUR in the following order:

*   [clisp-new-clx](https://aur.archlinux.org/packages/clisp-new-clx/)
*   [cl-asdf](https://aur.archlinux.org/packages/cl-asdf/)
*   [cl-ppcre](https://aur.archlinux.org/packages/cl-ppcre/)
*   [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

Also, look at [this post](https://bbs.archlinux.org/viewtopic.php?pid=543537#p543537) if you run into troubles.

## Documentation and Support

There is a TeXInfo manual included in the AUR package, the source, and [online](https://stumpwm.github.io/git/stumpwm-git.html).

There is also a [wiki](http://github.com/sabetts/stumpwm/wiki), an IRC channel (#stumpwm) on Freenode, and a mailing list. For more information, of course, see [the project's website](https://stumpwm.github.io/).

## Tweaking

See the wiki for a variety of useful tweaks for your .stumpwmrc.

If you are an emacs user, you will find an emacs minor mode for editing StumpWM files (and interfacing with the program `stumpish`, but more on that below) in the contrib/ directory of the StumpWM source. If you are using clisp, this file can also be found in `/usr/share/stumpwm/`.

`stumpish` is the STUMP window manager Interactive SHell. It is a program that allows the user to interact with StumpWM while it is running, from the comfort of a terminal (or using the emacs mode). It can be found in the contrib/ directory of the StumpWM source. If you use clisp, this file can also be found in `/usr/bin/`.

## Troubleshooting

*   If you have problems configuring multiple monitors, maybe you need to install 'xorg-xdpyinfo' package.

*   If you cannot start stumpwm and get

```
           debugger invoked on a SB-INT:SIMPLE-PARSE-ERROR in thread
       #:
       no non-whitespace characters in string "".
       Type HELP for debugger help, or (SB-EXT:QUIT) to exit from SBCL.
       (no restarts: If you did not do this on purpose, please report it as a bug.)
       (PARSE-INTEGER "" :START 0 :END NIL :RADIX 10 :JUNK-ALLOWED NIL)

```

in the REPL, it can be solved by deleting `~/.Xauthority`. See [this issue on github](https://github.com/sabetts/stumpwm/issues/1)
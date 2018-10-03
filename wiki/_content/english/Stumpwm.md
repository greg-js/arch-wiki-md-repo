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
*   [4 Configuration](#Configuration)
    *   [4.1 Change cursor from default X shape](#Change_cursor_from_default_X_shape)
    *   [4.2 Change window focus on mouse click](#Change_window_focus_on_mouse_click)
    *   [4.3 Enable modeline](#Enable_modeline)
    *   [4.4 Set font for messages and modeline](#Set_font_for_messages_and_modeline)
*   [5 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") [stumpwm](https://aur.archlinux.org/packages/stumpwm/) or [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/). The stable version supports multiple common-lisp implementations. The git version only supports sbcl.

SBCL is recommended for maximum performance.

After installing put `exec stumpwm` in your `~/.xinitrc` and run `startx`.

To quit, with the default configuration press `C-t ;` then type quit and press enter.

### With SBCL

Install these packages in the following order:

*   [sbcl](https://www.archlinux.org/packages/?name=sbcl)
*   [cl-alexandria](https://aur.archlinux.org/packages/cl-alexandria/)
*   [clx-git](https://aur.archlinux.org/packages/clx-git/)
*   [cl-ppcre](https://aur.archlinux.org/packages/cl-ppcre/)
*   [stumpwm](https://aur.archlinux.org/packages/stumpwm/) or [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

### With Clisp

Install these packages from AUR in the following order:

*   [clisp-new-clx](https://aur.archlinux.org/packages/clisp-new-clx/)
*   [asdf](https://aur.archlinux.org/packages/asdf/)
*   [cl-ppcre](https://aur.archlinux.org/packages/cl-ppcre/)
*   [stumpwm](https://aur.archlinux.org/packages/stumpwm/)

Also, look at [this post](https://bbs.archlinux.org/viewtopic.php?pid=543537#p543537) if you run into troubles.

## Documentation and Support

There is a TeXInfo manual included in the AUR package, the source, and [online](https://stumpwm.github.io/git/stumpwm-git.html).

There is also a [wiki](http://github.com/sabetts/stumpwm/wiki), an IRC channel (#stumpwm) on Freenode, and a mailing list. For more information, of course, see [the project's website](https://stumpwm.github.io/).

## Tweaking

See the wiki for a variety of useful tweaks for your .stumpwmrc.

If you are an emacs user, you will find an emacs minor mode for editing StumpWM files (and interfacing with the program `stumpish`, but more on that below) in the contrib/ directory of the StumpWM source. If you are using clisp, this file can also be found in `/usr/share/stumpwm/`.

`stumpish` is the STUMP window manager Interactive SHell. It is a program that allows the user to interact with StumpWM while it is running, from the comfort of a terminal (or using the emacs mode). It can be found in the contrib/ directory of the StumpWM source. If you use clisp, this file can also be found in `/usr/bin/`.

## Configuration

StumpWM stores its configuration in `~/.stumpwmrc` or you can use `~/.config/stumpwm/config`

### Change cursor from default X shape

By default StumpWM leaves the cursor as XOrg's standard X shape with the hotspot in the centre. You can have the more usual left-facing pointer by running

```
xsetroot -cursor_name left_ptr

```

You can also put this in your config file

```
(run-shell-command "xsetroot -cursor_name left_ptr")

```

### Change window focus on mouse click

Clicking on another window will send the click event to that window, but it will not get focus meaning any keyboard input will go to whichever window has focus. The following line makes focus change to any window that is clicked on.

```
(setf *mouse-focus-policy* :click) 

```

### Enable modeline

This sets up a basic modeline with the group name followed by window names on the left and the date and time on the right.

First set the window name format and overall modeline format

```
(setf *window-format* "%m%n%s%c")
(setf *screen-mode-line-format* (list "[^B%n^b] %W^>%d"))

```

The date format is constructed using the same format specifiers as [strftime(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strftime.3) e.g.

```
(setf *time-modeline-string* "%a %b %e %k:%M")

```

Optionally change how often the modeline updates on its own, in seconds (it also updates whenever you do something with StumpWM like switch window).

```
(setf *mode-line-timeout* 2)

```

Finally enable the modeline (this must come *after* you have set the options you wanted)

```
(enable-mode-line (current-screen) (current-head) t)

```

### Set font for messages and modeline

StumpWM uses the default XOrg font which is probably small and pixellated. You can use the ttf-fonts module to set a custom font.

```
(ql:quickload "clx-truetype")
(load-module "ttf-fonts")
(set-font (make-instance 'xft:font :family "DejaVu Sans Mono" :subfamily "Book" :size 11))

```

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

*   If you have an issue with the SBCL_HOME being set to NIL, you may need to set it manually

**Tip:** You can find the path using

`find / | grep sbcl.core`

 `export SBCL_HOME=/usr/lib/sbcl/` 

Then you may reinstall stumpwm

*   If you can't use the mousewheel to scroll in some programs, try adding

```
(setf (getenv "GDK_CORE_DEVICE_EVENTS") "1")

```

to your `.stumpwmrc` (source: [[1]](https://mmk2410.org/2018/02/15/scrolling-doesnt-work-in-gtk-3-apps-in-stumpwm/))

*   Quicklisp won't work in StumpWM if you installed it after installing StumpWM - in that case uninstall and reinstall StumpWM
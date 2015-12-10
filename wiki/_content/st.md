# st

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[st](http://st.suckless.org/) is a simple terminal implementation for [X](/index.php/X "X") by [suckless](http://suckless.org). It is intended to serve as a lightweight replacement for [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt"). It currently supports 256 colors, most VT10X escape sequences, UTF-8, X11 copy/paste, anti-aliased fonts (using fontconfig), fallback fonts, resizing, shortcuts via config.h, and line drawing.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Shell](#Shell)
    *   [2.2 Term](#Term)
    *   [2.3 Font](#Font)
    *   [2.4 Colors](#Colors)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Keyboard](#Keyboard)
        *   [3.1.1 Backspace not working properly](#Backspace_not_working_properly)
    *   [3.2 Vim](#Vim)
        *   [3.2.1 The background colour of text in _vim_ will not fill in anything that is not a character](#The_background_colour_of_text_in_vim_will_not_fill_in_anything_that_is_not_a_character)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") the package [st](https://www.archlinux.org/packages/?name=st) or [st-git](https://aur.archlinux.org/packages/st-git/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Install [st-git-zsh](https://aur.archlinux.org/packages/st-git-zsh/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/st-git-zsh)]</sup> package for a _zsh_ preconfigured _st_.

## Configuration

_st_ is configured through its `config.h` file, which is copied over from `config.h` at compile time. A default `config.def.h` is included with the source.

Consider maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with your `config.h`.

### Shell

To change the default shell for _st_, edit this line:

```
 static char shell[] = "/bin/sh";

```

### Term

To change the terminal type, edit this line:

```
 static char termname[] = "st-256color";

```

_st_ will set the `TERM` variable with the value of `termname`.

**Note:** If you experience trouble with _st_, you can try to set `termname` to `xterm` or `xterm-256color`

### Font

Edit the following line as you prefer:

```
 static char font[] = "Liberation Mono:pixelsize=12:antialias=false:autohint=false";

```

You can also pass the value of the font in the command line:

```
 st -f "Liberation Mono:size=12"

```

### Colors

Edit the following line to set _foreground_, _background_ and _cursor_ colors:

```
 static unsigned int defaultfg = 7;
 static unsigned int defaultbg = 0;
 static unsigned int defaultcs = 256;

```

The values refer to the `*colorname[]` array in the same file, you can use default color or add yours in `#rrggbb`, for example:

```
 static const char *colorname[] = {
   	/* 8 normal colors */
       "black",
       "red3",
       "green3",
       "yellow3",
       "blue2",
       "magenta3",
       "cyan3",
       "gray90",

       /* 8 bright colors */
       "gray50",
       "red",
       "green",
       "yellow",
       "#5c5cff",
       "magenta",
       "cyan",
       "white",

       [255] = 0,

       /* more colors can be added after 255 to use with DefaultXX */
       "#cccccc",
       "#eeeeee",
       "#111111",
 };

 /*
  * Default colors (colorname index)
  * foreground, background, cursor
  */
 static unsigned int defaultfg = 257;
 static unsigned int defaultbg = 258;
 static unsigned int defaultcs = 256;

```

## Troubleshooting

### Keyboard

#### Backspace not working properly

While virtual terminal and most popular terminal emulator for X bind `backscape` key to `^?` escape sequence, `st` bind it to `^H`, as explained in the FAQ.

If hitting the `backspace` key while typing on standard input of some programs (like `read`) prints `^H` instead of erasing, you can fix that with:

```
stty erase '^H'

```

This will make the terminal interprets `^H` as an erase command.

If you want to put the above command in a shell profile, you should consider checking the `$TERM` before launch it.

### Vim

#### The background colour of text in _vim_ will not fill in anything that is not a character

Try setting the value of `termname` in your `config.h` to `st-256color` and recompiling. And do not set the `TERM` var in your shell, at least not to `st-256color` as this seems to cause the issue.

Another solution, perhaps a better one, is to have the following lines in your `.vimrc` file:

```
if &term =~ '256color'
    " disable Background Color Erase (BCE) so that color schemes
    " render properly when inside 256-color tmux and GNU screen.
    " see also [http://sunaku.github.io/vim-256color-bce.html](http://sunaku.github.io/vim-256color-bce.html)
    set t_ut=
endif

```

## See also

*   [Homepage](http://st.suckless.org/)
*   [Frequently asked questions](http://git.suckless.org/st/plain/FAQ)
*   [Official git repository](http://git.suckless.org/st/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=St&oldid=410311](https://wiki.archlinux.org/index.php?title=St&oldid=410311)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Terminal emulators](/index.php/Category:Terminal_emulators "Category:Terminal emulators")
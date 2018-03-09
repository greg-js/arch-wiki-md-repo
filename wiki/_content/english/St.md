[st](https://st.suckless.org/) is a simple terminal implementation for [X.org](/index.php/X.org "X.org") by [suckless](https://suckless.org/). It is intended to serve as a lightweight replacement for [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt"). It currently supports 256 colors, true colors, most VT10X escape sequences, UTF-8, X11 copy/paste, anti-aliased fonts (using fontconfig), fallback fonts, resizing, shortcuts via config.h, and line drawing.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Shell](#Shell)
    *   [2.2 Term](#Term)
    *   [2.3 Font](#Font)
    *   [2.4 Colors](#Colors)
    *   [2.5 Desktop entry](#Desktop_entry)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Keyboard](#Keyboard)
        *   [3.1.1 DEL-Key not working properly in some Application](#DEL-Key_not_working_properly_in_some_Application)
    *   [3.2 Vim](#Vim)
        *   [3.2.1 The background colour of text in *vim* will not fill in anything that is not a character](#The_background_colour_of_text_in_vim_will_not_fill_in_anything_that_is_not_a_character)
        *   [3.2.2 256color and truecolor support not working in tmux or otherwise](#256color_and_truecolor_support_not_working_in_tmux_or_otherwise)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [st](https://aur.archlinux.org/packages/st/) or the [st-git](https://aur.archlinux.org/packages/st-git/) package.

## Configuration

*st* is configured through its `config.h` file, which is copied over from `config.h` at compile time. A default `config.def.h` is included with the source.

Consider maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with your `config.h`.

### Shell

To change the default shell for *st*, edit this line:

```
 static char shell[] = "/bin/sh";

```

### Term

To change the terminal type, edit this line:

```
 static char termname[] = "st-256color";

```

*st* will set the `TERM` variable with the value of `termname`.

**Note:** If you experience trouble with *st*, you can try to set `termname` to `xterm` or `xterm-256color`

### Font

Edit the following line as you prefer:

```
static char font[] = "Liberation Mono:pixelsize=12:antialias=false:autohint=false";

```

You can also pass the value of the font in the command line:

```
$ st -f "Liberation Mono:size=12"

```

### Colors

Edit the following lines to set *foreground*, *background*, and *cursor* colors:

```
 static unsigned int defaultfg = 7;
 static unsigned int defaultbg = 0;
 static unsigned int defaultcs = 256;

```

The values refer to the `*colorname[]` array in the same file; you can use default color or add yours in `#rrggbb`, for example:

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

Tools exists to facilitate the creation of color palettes. e.g. [terminal.sexy](http://terminal.sexy) that has a set of pre-made ones and exports directly to the st config format.

For those wanting the solarized color scheme, there is a patch that implements it at [suckless.org](https://st.suckless.org/patches/solarized/): [st-solarized](https://aur.archlinux.org/packages/st-solarized/).

### Desktop entry

To simplify launching *st* with a decent font e.g. [adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts), you can also create a [desktop entry](/index.php/Desktop_entry "Desktop entry"):

 `~/.local/share/applications/simple-terminal.desktop` 
```
[Desktop Entry]
Name=Simple Terminal
GenericName=Terminal
Comment=standard terminal emulator for the X window system
Exec=st -t "Suckless Terminal" -f "Source Code Pro:style=Semibold:size=12" -g "80x24"
Terminal=false
Type=Application
Encoding=UTF-8
Icon=terminal
Categories=System;TerminalEmulator;
Keywords=shell;prompt;command;commandline;cmd;
```

The menu entry will appear as **Simple Terminal** in the *System Tools* application list.

## Troubleshooting

### Keyboard

#### DEL-Key not working properly in some Application

add following to *~/.inputrc* or */etc/inputrc*:

```
 set enable-keypad on

```

### Vim

#### The background colour of text in *vim* will not fill in anything that is not a character

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

#### 256color and truecolor support not working in tmux or otherwise

First, make sure you are not setting and exporting the value of `TERM` in your `~/.bashrc` as mentioned in this [thread](https://bbs.archlinux.org/viewtopic.php?pid=1755862#p1755862)

**Note:** Please do not explicitly set `TERM`. Do it right by setting the `default-terminal` setting in your `tmux.conf`

Second, make sure the version of `vim` you are using is **`>=7.4.1799`**, which is when `termguicolors` was added.

Finally, add the following to `~/.vimrc`:

```
set t_8f=^[[38;2;%lu;%lu;%lum        " set foreground color
set t_8b=^[[48;2;%lu;%lu;%lum        " set background color
colorscheme Tomorrow-Night-Eighties
set t_Co=256                         " Enable 256 colors
set termguicolors                    " Enable GUI colors for the terminal to get truecolor

```

**Note:** `^[` is a literal escape (<Esc>) character that prefixes each of the values for `t_8f` and `t_8b`. It is a single character, which can be reproduced in `vim`. In **INSERT** mode, press `<C-v>-<Esc>` (Control+v then press Esc). You will still be in **INSERT** mode; press <Esc> again to return to **NORMAL** mode.
**Tip:** It is recommended to set the values for `t_8f` and `t_8b` prior to setting `colorscheme`, `t_Co` and `termguicolors`.

For more information, see the `:help` in `vim` for: `xterm-true-color`, `t_8f`, `t_8b`

## See also

*   [Homepage](https://st.suckless.org/)
*   [Frequently asked questions](https://git.suckless.org/st/plain/FAQ)
*   [Official git repository](https://git.suckless.org/st/)
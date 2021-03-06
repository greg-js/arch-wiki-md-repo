[st](https://st.suckless.org/) is a simple terminal implementation for [Xorg](/index.php/Xorg "Xorg") by [suckless](https://suckless.org/). It is intended to serve as a lightweight replacement for [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt"). It currently supports 256 colors, true colors, most VT10X escape sequences, UTF-8, X11 copy/paste, anti-aliased fonts (using fontconfig), fallback fonts, resizing, shortcuts via config.h, and line drawing.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Shell](#Shell)
    *   [2.2 Term](#Term)
    *   [2.3 Font](#Font)
    *   [2.4 Cursor](#Cursor)
    *   [2.5 Colors](#Colors)
    *   [2.6 Patches](#Patches)
    *   [2.7 Desktop entry](#Desktop_entry)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Keyboard](#Keyboard)
    *   [3.2 Vim](#Vim)
        *   [3.2.1 The background colour of text in *vim* will not fill in anything that is not a character](#The_background_colour_of_text_in_vim_will_not_fill_in_anything_that_is_not_a_character)
        *   [3.2.2 256color and truecolor support not working in tmux or otherwise](#256color_and_truecolor_support_not_working_in_tmux_or_otherwise)
    *   [3.3 Crashing](#Crashing)
        *   [3.3.1 Emojis](#Emojis)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [st](https://aur.archlinux.org/packages/st/) package or [st-git](https://aur.archlinux.org/packages/st-git/) for the development version.

## Configuration

*st* is configured through its `config.h` file which is copied over at compile time. Defaults are stored in `config.def.h` which is included with the source. Consider maintaining your own `config.h` and [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

### Shell

To change the default shell for *st*, edit this line:

```
static char *shell = "/bin/sh";

```

Or start *st* with the desired shell as last argument:

```
$ st *options* fish

```

### Term

To change the terminal type, edit this line:

```
static char *termname = "st-256color";

```

*st* will set the `TERM` variable with the value of `termname`.

### Font

Edit the following line as you prefer:

```
static char *font = "Liberation Mono:pixelsize=12:antialias=false:autohint=false";

```

You can also pass the value of the font in the command line:

```
$ st -f "Liberation Mono:size=12"
$ st -f 'Liberation Mono-12'

```

Font names can be found with `fc-list`.

### Cursor

By default the mouse pointer is `XC_xterm;` which often can be hard to find. To change it to your cursor theme's normal one, edit the following:

```
static unsigned int mouseshape = XC_left_ptr;

```

### Colors

Edit the following lines to set foreground, background, and cursor colors:

```
unsigned int defaultfg = 7;
unsigned int defaultbg = 0;
static unsigned int defaultcs = 256;

```

The values refer to the `*colorname[]` array in the config file. You can use the default colors or add yours in `#rrggbb`:

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
unsigned int defaultfg = 257;
unsigned int defaultbg = 258;
static unsigned int defaultcs = 256;

```

Tools exists to facilitate the creation of color palettes. For example [terminal sexy](http://terminal.sexy) has a set of pre-made ones and exports directly to *st'*s format (see [[1]](https://github.com/stayradiated/terminal.sexy/issues/22#issuecomment-430629424)).

There is a patch for the Solarized color scheme. See [[2]](https://st.suckless.org/patches/solarized/) or [st-solarized](https://aur.archlinux.org/packages/st-solarized/) to install it.

### Patches

There are many patches available from the [suckless website](https://st.suckless.org/patches/alpha/). To apply a patch, download the [diff](https://www.gnu.org/software/diffutils/manual/html_node/Invoking-diff.html) and apply it with `patch -i patch.diff`. This alters the default config file `config.def.h`; if you are maintaining your own `config.h`, copy your configs from `config.h` into a copy of `config.def.h` and rename it `config.h`, then `make clean install`.

### Desktop entry

To simplify launching *st* with a decent font (e.g. [adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts)) in a [desktop environment](/index.php/Desktop_environment "Desktop environment"), you can also create a [desktop entry](/index.php/Desktop_entry "Desktop entry"):

 `~/.local/share/applications/st.desktop` 
```
[Desktop Entry]
Name=Simple Terminal
GenericName=Terminal
Comment=Suckless terminal emulator for X
Exec=st -t "Simple Terminal" -f "Source Code Pro:style=Semibold:size=12"
Terminal=false
Type=Application
Encoding=UTF-8
Icon=utilities-terminal
Categories=System;TerminalEmulator;
Keywords=shell;prompt;command;commandline;cmd;
```

The menu entry will appear as *Simple Terminal* in the *System Tools* application list.

## Troubleshooting

### Keyboard

Add the following to `~/.inputrc` or `/etc/inputrc` if `Delete` is not working properly in some applications:

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

### Crashing

#### Emojis

St may crash if you try to load a page with color emojis that have [no associated glyph](https://lists.suckless.org/dev/1707/31965.html), seen specifically with fonts like [ttf-joypixels](https://www.archlinux.org/packages/?name=ttf-joypixels), returning something similar to this if run from another terminal:

```
X Error of failed request:  BadLength (poly request too large or internal Xlib length error)
 Major opcode of failed request:  139 (RENDER)
 Minor opcode of failed request:  20 (RenderAddGlyphs)
 Serial number of failed request:  5118
 Current serial number in output stream:  5209

```

In order to fix it, simply install [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/) for unicode coverage.

## See also

*   [Homepage](https://st.suckless.org/)
*   [Frequently asked questions](https://git.suckless.org/st/plain/FAQ)
*   [Official git repository](https://git.suckless.org/st/)
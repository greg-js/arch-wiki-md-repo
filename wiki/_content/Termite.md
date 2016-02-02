# Termite

[Termite](https://www.github.com/thestinger/termite) is a minimal [terminal emulator](/index.php/Category:Terminal_emulators "Category:Terminal emulators") designed for use with tiling [window managers](/index.php/Window_manager "Window manager"). It is a _modal_ application, similar to [Vim](/index.php/Vim "Vim"), with an insert mode and command mode where keybindings have different functions. Termite is based on the [VTE](https://developer.gnome.org/vte/unstable/) library.

The configuration file allows to change colors and set some options. Termite supports transparency along with both the 256 color and true color (16 million colors) palettes. It has a similar look and feel to [urxvt](/index.php/Urxvt "Urxvt").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Font](#Font)
    *   [3.2 Colors](#Colors)
*   [4 Transparency](#Transparency)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Colored ls output](#Colored_ls_output)
    *   [5.2 Ctrl+Shift+t](#Ctrl.2BShift.2Bt)
*   [6 See also](#See_also)

## Installation

Install the [termite](https://www.archlinux.org/packages/?name=termite) package, or [termite-git](https://aur.archlinux.org/packages/termite-git/) for the development version.

## Usage

Termite starts in insert mode by default. Text may be selected using the mouse, or by using command-mode keys. In insert mode, `Ctrl+Shift+c` is used to copy selected text to the [X](/index.php/X "X") clipboard, `Ctrl+Shift+v` to paste. `Ctrl+Tab` starts scrollback completion, and `Ctrl+Shift+Up` / `Ctrl+Shift+Down` scroll the screen up or down.

`Ctrl+Shift+Space` enters command-mode. Many commands are borrowed from [Vim](/index.php/Vim "Vim"), for example `v` for visual mode, `Shift+v` for visual line mode, `Ctrl+v` for visual block mode, `y` to copy ("yank") selected text, `/` and `?` for searching, `w`, `b`, `^`, `$` for movement, and `Escape` to go back to insert mode.

## Configuration

Termite looks for configuration files in `$XDG_CONFIG_HOME/termite/config`, `~/.config/termite/config`, `$XDG_CONFIG_DIRS/termite/config` and `/etc/xdg/termite.cfg`. The configuration file is used to change options such as font, colors, window hints, etc. The configuration file is in _ini_ format, with three sections: _options_, _colors_, and _hints_.

### Font

Fonts are specified in the format `font=<font_name> <font_size>` under the _options_ section. `<font_name>` is specified according to [fontconfig](/index.php/Fontconfig "Fontconfig"), not [Xft](/index.php/X_Logical_Font_Description "X Logical Font Description"). Use `fc-list` to see which fonts are available on the system (see also [Font configuration#Font paths](/index.php/Font_configuration#Font_paths "Font configuration")).

 `~/.config/termite/config` 

```
[options]
font = Monospace 9
font = Terminus (TTF) 8
font = Droid Sans Mono 8
```

### Colors

Colors consist of either a 24-bit hex value (e.g. `#4a32b1`), or an rgba vector (e.g. `rgba(16, 32, 64, 0.5)`). Valid properties for colors are `foreground`, `foreground_bold`, `foreground_dim`, `background`, `cursor`, and `colorN` (where N is an integer from zero through 254; used to assign a 24-bit color value to terminal colorN).

 `~/.config/termite/config` 

```
[colors]
foreground = #dcdccc
background  = #3f3f3f
```

## Transparency

As of version 9, Termite supports true transparency via color definitions that specify an alpha channel value [[1]](https://github.com/thestinger/termite/issues/191). This requires a compositor to be running, such as [Compton](/index.php/Compton "Compton") or [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr). Most compositors do not require special configuration for Termite to use transparency.

 `~/.config/termite/config` 

```
[colors]
background = rgba(63, 63, 63, 0.8)
```

**Note:** In [i3](/index.php/I3 "I3"), in stacked/tabbed layout, this shows all windows "stacked" on top of each other, in the order they were most recently in the foreground, rather than showing the desktop (the root window) directly behind Termite. This is due to i3 reordering windows rather than hiding invisible windows in tiling mode. You can configure your compositor to make windows with `_NET_WM_STATE=_NET_WM_STATE_HIDDEN` fully transparent to solve this. For example, for compton use `~/.compton.conf` 

```
opacity-rule = [
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];
```

## Troubleshooting

### Colored ls output

For colored `ls` output it is necessary to use a custom LS_COLORS [environment variable](/index.php/Environment_variable "Environment variable"), which can be set with a `dircolors` file. Generate one with:

```
$ dircolors -p > ~/.dircolors

```

Then edit `~/.dircolors` file, and append

```
TERM xterm-termite

```

to the end of the list of terminals, and save the file.

For [Bash](/index.php/Bash "Bash") in `~/.bashrc` and [Zsh](/index.php/Zsh "Zsh") in `~/.zshrc`, add:

```
eval $(dircolors ~/.dircolors)

```

and restart the terminal. For [fish](/index.php/Fish "Fish"), add

```
eval (dircolors -c ~/.dircolors | sed 's/>&\/dev\/null$//')

```

to `~/.config/fish/config.fish` and relogin or reload the config via:

```
. ~/.config/fish/config.fish

```

### Ctrl+Shift+t

If opening a new tab through `Ctrl+Shift+t` fails with `no directory uri set`, [source](/index.php/Source "Source") `/etc/profile.d/vte.sh`. See [GNOME#New terminals adopt current directory](/index.php/GNOME#New_terminals_adopt_current_directory "GNOME").

## See also

*   [Termite readme](https://github.com/thestinger/termite/blob/master/README.rst)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Termite&oldid=412018](https://wiki.archlinux.org/index.php?title=Termite&oldid=412018)"
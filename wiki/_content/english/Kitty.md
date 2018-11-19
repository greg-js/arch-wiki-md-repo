[Kitty](https://sw.kovidgoyal.net/kitty/index.html) is a scriptable OpenGL based terminal emulator with tiling capabilities, TrueColor, ligatures support and protocol extensions for keyboard input and image rendering.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Kittens](#Kittens)
*   [3 Configuration](#Configuration)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [kitty](https://www.archlinux.org/packages/?name=kitty) package.

## Usage

New tabs and windows can be created and resized through various `ctrl+shift` shortcuts. Layouts are switchable through `ctrl+shift+l` and can be saved/restored.

A *full keyboard mode* provides distinction between ambiguous keys like `ctrl+i` vs `tab`. Moreover, new text effects like curly-underline are also available for applications that support it.

### Kittens

Kitty has a framework for creating subprograms called [kittens](https://sw.kovidgoyal.net/kitty/#kittens). Some of them:

```
$ kitty +kitten icat image.jpeg             # show image in the terminal (needs imagemagick)
$ kitty +kitten diff file1 file2            # show diff of two files
$ kitty +kitten clipboard                   # this kitten allows working with clipboard even over ssh

```

## Configuration

Kitty is configurable in `~/.config/kitty/kitty.conf`. Fonts, colors, cursors and scrollback behaviors can be adjusted. You can see available options in the [official documentation](https://sw.kovidgoyal.net/kitty/conf.html). Also you can find there [configuration file](https://sw.kovidgoyal.net/kitty/conf.html#sample-kitty-conf) used by default.

## See also

*   [GitHub repository](https://github.com/kovidgoyal/kitty)
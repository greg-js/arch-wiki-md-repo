[Textadept](https://foicica.com/textadept/) describes itself as a "a fast, minimalist, and remarkably extensible cross-platform text editor". With a very lightweight code base written in C, it relies on Lua for its extensibility. The editor works both in a graphical (GTK2) and in a CLI environment (Curses).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Modules](#Modules)
*   [4 See also](#See_also)

## Installation

Install [textadept](https://aur.archlinux.org/packages/textadept/) from the [AUR](/index.php/AUR "AUR"). It features 4 different executables:

*   *textadept*
*   *textadept-curses*
*   *textadeptjit*
*   *textadeptjit-curses*

The *jit* versions embed the Lua interpreter LuaJIT, which is notably faster than the official Lua interpreter but does not support Lua 5.2 as of January 2015.[[1]](http://luajit.org/extensions.html#lua52) The *curses* versions run in a CLI environment.

## Configuration

On first start, Textadept will create a `~/.textadept` folder. You can edit `~/.textadept/init.lua` to start customizing the editor. From there you can define new functions, key bindings, themes, and even modules, as explained in the [manual](http://foicica.com/textadept/manual.html) and the [API](http://foicica.com/textadept/api.html).

## Modules

By default, Textadept features modules for its core only, that is ANSI C, Lua and itself, however the AUR package also embeds some of the [official modules](http://foicica.com/hg).

Some more modules are found in the [AUR](/index.php/AUR "AUR"):

*   [Textredux](https://rgieseke.github.io/textredux/) is available as [textadept-textredux](https://aur.archlinux.org/packages/textadept-textredux/)
*   [Textadept common](https://rgieseke.github.io/ta-common/) is available as [textadept-common-git](https://aur.archlinux.org/packages/textadept-common-git/)

You will need to enable these modules in your `init.lua` file as explained in the upstream documentation.

More contributed modules and functions are listed in the [wiki](http://foicica.com/wiki/textadept).

Another convenient way to install modules is by cloning the repository in `~/.textadept/modules`. For instance you can fetch *textadept-vi* from there:

```
$ cd ~/.textadept/modules
$ git clone [https://github.com/jugglerchris/textadept-vi.git](https://github.com/jugglerchris/textadept-vi.git)

```

You can easily keep up to date all your modules with version control tools.

## See also

*   [Manual](http://foicica.com/textadept/manual.html)
*   [Default key bindings](http://foicica.com/textadept/api.html#textadept.keys)
*   [API](http://foicica.com/textadept/api.html)
*   [Wiki](http://foicica.com/wiki/textadept)
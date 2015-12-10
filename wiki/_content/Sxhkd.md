# Sxhkd

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys")
*   [Xmodmap](/index.php/Xmodmap "Xmodmap")

From [sxhkd's Github page](https://github.com/baskerville/sxhkd):

_sxhkd is a simple X hotkey daemon with a powerful and compact configuration syntax._

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") [sxhkd](https://www.archlinux.org/packages/?name=sxhkd) or [sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/)<sup><small>AUR</small></sup>.

## Configuration

sxhkd defaults to `$XDG_CONFIG_HOME/sxhkd/sxhkdrc` for its configuration file. An alternate configuration file can be specified with the `-c` option.

Each line of the configuration file is interpreted as so:

*   If it starts with `#`, it is ignored.
*   If it starts with one or more white space commands, it is read as a command.
*   Otherwise, it is parsed as a hotkey: each key name is separated by spaces and/or `+` characters.

General syntax:

```
[MODIFIER + ]*[@|!]KEYSYM
    COMMAND

```

Where `MODIFIER` is one of the following names: `super`, `hyper`, `meta`, `alt`, `control`, `ctrl`, `shift`, `mode_switch`, `lock`, `mod1`, `mod2`, `mod3`, `mod4`, `mod5`. If `@` is added at the beginning of the keysym, the command will be run on key release events, otherwise on key press events. If `!` is added at the beginning of the keysym, the command will be run on motion notify events and must contain two integer conversion specifications which will be replaced by the x and y coordinates of the pointer relative to the root window referential (the only valid button keysyms for this type of hotkeys are: `button1`, ..., `button5`). The `KEYSYM` names are those your will get from `xev`.

Mouse hotkeys can be defined by using one of the following special keysym names: `button1`, `button2`, `button3`, ..., `button24`. The hotkey can contain a sequence of the form (`STRING_1`,…,`STRING_N`), in which case, the command must also contain a sequence with _N_ elements: the pairing of the two sequences generates _N_ hotkeys. In addition, the sequences can contain ranges of the form `A-Z` where _A_ and _Z_ are alphanumeric characters.

What is actually executed is `SHELL -c COMMAND`, which means you can use environment variables in `COMMAND`. `SHELL` will be the content of the first defined environment variable in the following list: `SXHKD_SHELL`, `SHELL`. If sxhkd receives a `SIGUSR1` signal, it will reload its configuration file.

## Usage

After configuring it, you may wish to setup sxhkd to [autostart](/index.php/Autostart "Autostart").

**Tip:** An example [systemd](/index.php/Systemd "Systemd") service file is found [here](https://github.com/baskerville/sxhkd/blob/master/contrib/systemd/sxhkd.service).

## See Also

*   [Official website](https://github.com/baskerville/sxhkd) - includes configuration options, example bindings, and source code.
*   [ArchLinux forum thread](https://bbs.archlinux.org/viewtopic.php?id=155613)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sxhkd&oldid=391821](https://wiki.archlinux.org/index.php?title=Sxhkd&oldid=391821)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Keyboards](/index.php/Category:Keyboards "Category:Keyboards")
*   [X server](/index.php/Category:X_server "Category:X server")
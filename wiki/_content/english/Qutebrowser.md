[qutebrowser](https://github.com/The-Compiler/qutebrowser) is a lightweight keyboard-driven, vim-like browser based on PyQt5 and QtWebKit.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 User Configuration](#User_Configuration)
    *   [2.2 Keybindings](#Keybindings)

## Installation

Install either the [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser) or the [qutebrowser-git](https://aur.archlinux.org/packages/qutebrowser-git/) package.

## Basic usage

Use `:` to access the command prompt. You can use `Tab` to auto-complete.

On first usage of qutebrowser, a Quickstart page appears. It is later accessible via `:help`. See the [cheatsheet](http://qutebrowser.org/img/cheatsheet-big.png) for keyboard shortcuts.

### User Configuration

You will find the configuration files of qutebrowser under `$XDG_CONFIG_HOME/qutebrowser/`. The main configuration happens in the file `qutebrowser.conf`, which is organized in sections like an ini-file. For example, under `[searchengines]` you can configure your search engines as described by the comment. To add a shortcut for searching the the arch wiki, add these two lines:

```
archwiki = https://wiki.archlinux.org/?search={}
aw = ${archwiki}

```

Now, in qutebrowser you can search the arch wiki for an article about qutebrowser via `:open aw qutebrowser` which will bring you to this page. As per the standard configuration the key mapping `o` will subsitute `:open`, so typing `o aw *your_search_term*` will henceforth allow you to quickly search the arch wiki. Notice that the arguments required to perform a search vary across search engines, for example, to set up Google use:

```
google = https://www.google.com/search?hl=en&q={}
g = ${google}

```

### Keybindings

Keybindings reside in `$XDG_CONFIG_HOME/qutebrowser/keys.conf)`.

You can edit the keybindings directly from the browser with the command `:bind *key* *command*` or you can edit them directly from the file. Notice that there are many, many keybinds already in place. If you notice a lag on one of your keybind it is because some other keybind is also starting with the same key.
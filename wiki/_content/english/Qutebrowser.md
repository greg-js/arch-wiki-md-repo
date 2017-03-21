[qutebrowser](https://github.com/The-Compiler/qutebrowser) is a lightweight keyboard-driven, vim-like browser based on PyQt5 and QtWebKit.

**Warning:** qt5-webkit is considered insecure and outdated, more info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/). Either [use the QtWebEngine backend](#Use_experimental_webengine_backend) or install qt5-webkit-ng.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 User Configuration](#User_Configuration)
    *   [2.2 Keybindings](#Keybindings)
    *   [2.3 Video playback](#Video_playback)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Use experimental webengine backend](#Use_experimental_webengine_backend)
    *   [3.2 dwb-like session handling](#dwb-like_session_handling)
*   [4 See also](#See_also)

## Installation

Install either the [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser) or the [qutebrowser-git](https://aur.archlinux.org/packages/qutebrowser-git/) package.

## Basic usage

Use `:` to access the command prompt. You can use `Tab` to auto-complete.

On first usage of qutebrowser, a Quickstart page appears. It is later accessible via `:help`. See the [cheatsheet](http://qutebrowser.org/img/cheatsheet-big.png) for keyboard shortcuts.

### User Configuration

You will find the configuration files of qutebrowser under `$XDG_CONFIG_HOME/qutebrowser/`. The main configuration happens in the file `qutebrowser.conf`, which is organized in sections like an ini-file. For example, under `[searchengines]` you can configure your search engines as described by the comment. To add a shortcut for searching the the arch wiki, add this line:

```
aw = https://wiki.archlinux.org/?search={}

```

Now, in qutebrowser you can search the arch wiki for an article about qutebrowser via `:open aw qutebrowser` which will bring you to this page. As per the standard configuration the key mapping `o` will subsitute `:open`, so typing `o aw *your_search_term*` will henceforth allow you to quickly search the arch wiki. Notice that the arguments required to perform a search vary across search engines, for example, to set up Google use:

```
g = https://www.google.com/search?hl=en&q={}

```

### Keybindings

Keybindings reside in `$XDG_CONFIG_HOME/qutebrowser/keys.conf)`.

You can edit the keybindings directly from the browser with the command `:bind *key* *command*` or you can edit them directly from the file. Notice that there are many, many keybinds already in place. If you notice a lag on one of your keybind it is because some other keybind is also starting with the same key.

### Video playback

See [Browser plugins#Multimedia playback](/index.php/Browser_plugins#Multimedia_playback "Browser plugins").

## Tips and tricks

### Use experimental webengine backend

To use the more secure webengine backend, use the `--backend` flag:

```
 $ qutebrowser --backend webengine

```

**Note:** The qutebrowser implementation of webengine is experimental and may be missing features. See [this issue](https://github.com/qutebrowser/qutebrowser/issues/2335) for updates.

### dwb-like session handling

To have qutebrowser handle sessions more like in [dwb](/index.php/Dwb "Dwb") with the `--restore` option ("per-window" sessions, multiple simultaneously active sessions), you can use [this wrapper script](https://github.com/ayekat/dotfiles/blob/master/.local/bin/qutebrowser).

## See also

*   [Github repository](https://github.com/qutebrowser/qutebrowser)
*   [Homepage](http://qutebrowser.org/)
*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=191076)
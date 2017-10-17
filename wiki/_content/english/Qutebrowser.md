[qutebrowser](https://github.com/qutebrowser/qutebrowser) is a keyboard-focused web browser based on Python and PyQt5.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 User configuration](#User_configuration)
    *   [2.2 Keybindings](#Keybindings)
    *   [2.3 Video playback](#Video_playback)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Turn on spell checking](#Turn_on_spell_checking)
    *   [3.2 Minimize fingerprinting](#Minimize_fingerprinting)
        *   [3.2.1 Set a common user-agent](#Set_a_common_user-agent)
        *   [3.2.2 Set a common HTTP_ACCEPT header](#Set_a_common_HTTP_ACCEPT_header)
        *   [3.2.3 Disable reading from canvas](#Disable_reading_from_canvas)
    *   [3.3 dwb-like session handling](#dwb-like_session_handling)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") either the [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser) or the [qutebrowser-git](https://aur.archlinux.org/packages/qutebrowser-git/) package.

## Basic usage

Use `:` to access the command prompt. You can use `Tab` to auto-complete.

On first usage of qutebrowser, a Quickstart page appears. It is later accessible via `:help`. See the [cheatsheet](https://qutebrowser.org/img/cheatsheet-big.png) for keyboard shortcuts.

### User configuration

You will find the configuration files of qutebrowser under `$XDG_CONFIG_HOME/qutebrowser/`. The main configuration happens in the file `qutebrowser.conf`, which is organized in sections like an ini-file. For example, under `[searchengines]` you can configure your search engines as described by the comment. To add a shortcut for searching the the arch wiki, add this line:

```
aw = https://wiki.archlinux.org/?search={}

```

Now, in qutebrowser you can search the Arch Linux wiki for an article about qutebrowser via `:open aw qutebrowser` which will bring you to this page. As per the standard configuration the key mapping `o` will subsitute `:open`, so typing `o aw *your_search_term*` will henceforth allow you to quickly search the arch wiki. Notice that the arguments required to perform a search vary across search engines, for example, to set up Google use:

```
g = https://www.google.com/search?hl=en&q={}

```

You can also make this setting from the browser with `:set searchengines *keyword* *your_search_term*`. For example:

```
:set searchengines aw https://wiki.archlinux.org/?search={}

```

### Keybindings

Keybindings reside in `$XDG_CONFIG_HOME/qutebrowser/keys.conf`.

You can edit the keybindings directly from the browser with the command `:bind *key* *command*` or you can edit them directly from the file. Notice that there are many, many keybinds already in place. If you notice a lag on one of your keybind it is because some other keybind is also starting with the same key.

### Video playback

See [Browser plugins#Multimedia playback](/index.php/Browser_plugins#Multimedia_playback "Browser plugins").

## Tips and tricks

### Turn on spell checking

First, download the dictionaries you want using [this script](https://github.com/qutebrowser/qutebrowser/blob/master/scripts/install_dict.py). For example, to install the English dictionary do:

```
# python install_dict.py en-US

```

Then set the following in qutebrowser:

```
:set spellcheck.languages ["en-US"]

```

### Minimize fingerprinting

Websites may be able to identify you based on combining information on screen size, user-agent, HTTP_ACCEPT headers, and more. See [[1]](https://panopticlick.eff.org/) for more information and to test the uniqueness of your browser. Below are a few steps that can be taken to make your qutebrowser installation more "generic".

Additionally see [Firefox/Privacy#Configuration tweaks](/index.php/Firefox/Privacy#Configuration_tweaks "Firefox/Privacy") for more ideas.

#### Set a common user-agent

Several user agents are available as options when using `:set network user-agent`. Another, possibly more generic user-agent is:

```
Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0

```

**Note:**

*   Changing `Linux x86_64` to a non-Linux platform may make your browser more unique, since websites can also gather your platform type via Javascript, and this setting cannot be changed in qutebrowser.
*   Changing your user-agent away from the default will prevent some websites from working properly.

#### Set a common HTTP_ACCEPT header

The following is a common HTTP_ACCEPT header. Under `network` in qutebrowser's settings set:

```
accept-language = en-US,en;q=0.5
custom-headers = {"accept": "text/html, */*; q=0.01"}

```

#### Disable reading from canvas

This option is not currently available in qutebrowser other than by specifying it on the commandline like so:

```
$ qutebrowser --qt-flag disable-reading-from-canvas

```

See [issue #2235](https://github.com/qutebrowser/qutebrowser/issues/2235) for more information.

**Note:** Some websites depend on canvas reading for content rendering and other functionality. Adding this option may cause them to not work properly [[2]](https://github.com/qutebrowser/qutebrowser/issues/2908).

### dwb-like session handling

To have qutebrowser handle sessions more like in [dwb](/index.php/Dwb "Dwb") with the `--restore` option (multiple simultaneously active sessions), you can use [this wrapper script](https://github.com/ayekat/dotfiles/blob/master/bin/qutebrowser). It uses `--basedir` to separate data, cache and runtime for each session, while keeping the configuration shared.

## See also

*   [Github repository](https://github.com/qutebrowser/qutebrowser)
*   [Homepage](https://qutebrowser.org/)
*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=191076)
*   [New config example](https://bitbucket.org/jasonwryan/shiv/src/tip/.config/qutebrowser/config.py)
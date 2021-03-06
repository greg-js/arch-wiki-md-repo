[qutebrowser](https://github.com/qutebrowser/qutebrowser) is a keyboard-focused web browser based on Python and PyQt5.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 User configuration](#User_configuration)
        *   [2.1.1 Configuration in Qutebrowser](#Configuration_in_Qutebrowser)
        *   [2.1.2 Keybindings](#Keybindings)
    *   [2.2 Video playback](#Video_playback)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Automatically enter login information](#Automatically_enter_login_information)
    *   [3.2 Turn on spell checking](#Turn_on_spell_checking)
    *   [3.3 Minimize fingerprinting](#Minimize_fingerprinting)
        *   [3.3.1 Set a common user-agent](#Set_a_common_user-agent)
        *   [3.3.2 Set a common HTTP_ACCEPT header](#Set_a_common_HTTP_ACCEPT_header)
        *   [3.3.3 Disable reading from canvas](#Disable_reading_from_canvas)
        *   [3.3.4 Disable WebGL](#Disable_WebGL)
    *   [3.4 dwb-like session handling](#dwb-like_session_handling)
    *   [3.5 Disable websites](#Disable_websites)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Unreadable tooltips](#Unreadable_tooltips)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") either the [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser) or the [qutebrowser-git](https://aur.archlinux.org/packages/qutebrowser-git/) package.

## Basic usage

Use `:` to access the command prompt. You can use `Tab` to auto-complete.

On first usage of qutebrowser, a Quickstart page appears. It is later accessible via `:help`. See the [cheatsheet](https://qutebrowser.org/img/cheatsheet-big.png) for keyboard shortcuts.

### User configuration

Qutebrowser can be configured via the UI, the qutebrowser command-line or a Python script. Qutebrowser's own documentation explains in detail how to configure qutebrowser with these different methods. To open qutebrowser's help system, type `:help`. On the help page, choose `Configuring qutebrowser`.

To find out the paths where the configuration files will be located, open the special page `qute://version`. On Arch Linux, this will typically be `$XDG_CONFIG_HOME/qutebrowser/`. The configuration made in qutebrowser will be stored in `autoconfig.yml` (which should not be touched by the user) while the user's Python script is `config.py`.

#### Configuration in Qutebrowser

To set a single configuration item, you can simply type `:set` followed by the name of the configuration item and the new value that you would like to set. For example, you could type

```
:set auto_save.session true

```

to open your previous tabs when you reopen qutebrowser.

To open qutebrowser's UI settings page, type

```
:set

```

without further arguments. There, you can edit the different settings in the UI. When you are finished, type `:set` again to store your configuration.

For example, under `url.searchengines` you can configure your search engines which are stored as a list of key-value pairs. When you have not changed this setting yet, this should look something like

```
{"DEFAULT": "https://duckduckgo.com/?q={}"}

```

This configures DuckDuckGo as your default search engine while the placeholder `{}` will be replaced by your search term. To add a shortcut for quickly searching the Arch Linux wiki, you could use

```
{"DEFAULT": "https://duckduckgo.com/?q={}", "wa": "https://wiki.archlinux.org/?search={}"}

```

Then, as described by the comment in the qutebrowser UI, you can search the Arch Linux wiki by typing `o wa <searchterm>`. Notice that the arguments required to perform a search vary across search engines. For example, to set up Google, use `https://www.google.com/search?hl=en&q={}`.

If Tor is installed and running on your system and you wish to use DuckDuckGo onion page instead, the setting should be something like

```
{"DEFAULT": "https://3g2upl4pq6kufc4m.onion/?q={}", "wa": "https://wiki.archlinux.org/?search={}"}

```

#### Keybindings

You can edit the keybindings directly from the browser with the command `:bind *key* *command*` or you can edit them directly from the file. Notice that there are many, many keybinds already in place. If you notice a lag on one of your keybind it is because some other keybind is also starting with the same key.

See the [documentation](http://qutebrowser.org/doc/help/configuring.html#_binding_keys) for examples.

### Video playback

See [Browser plugins#Multimedia playback](/index.php/Browser_plugins#Multimedia_playback "Browser plugins").

## Tips and tricks

### Automatically enter login information

You can use the [qute-pass](https://github.com/qutebrowser/qutebrowser/blob/master/misc/userscripts/qute-pass) userscript to [automatically enter](https://i.imgur.com/KN3XuZP.gif) login information stored in your [Pass](/index.php/Pass "Pass") password-store. You will need a [dmenu](/index.php/Dmenu "Dmenu")-compatible [application launcher](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other") and [python-tldextract](https://www.archlinux.org/packages/?name=python-tldextract). Set up a keybinding which executes `:spawn --userscript qute-pass`.

To quote from the script's description:

```
The domain of the site has to appear as a segment in the pass path, for example: "github.com/cryzed" or "websites/github.com". How the username and password are determined is freely configurable using the CLI arguments. The login information is inserted by emulating key events using qutebrowser's fake-key command in this manner: [USERNAME]<Tab>[PASSWORD], which is compatible with almost all login forms.

```

To further clarify, the pass-structure that is used by default should look something like this:

 ` user@computer$ pass ` 
```
 Password Store 
 ├── example.site1.com 
 │   └── username 
 ├── example.site2.com 
 │   └── username1 
 │   └── username2 

```

This means is that each website is a directory in your ~/.password-store folder. Within each website-named directory is where the files are titled username.gpg, username2.pgp, etc. and each file contains the password associated with each username for the website. For those of you migrating from Firefox, a [modified version of firefox_decrypt](https://github.com/johnabs/firefox_decrypt) should migrate things in this format.

The userscript provides many options to accomodate most workflows and special circumstances (such as only wanting to insert the password or the regular method of inserting the username and password not working).

### Turn on spell checking

First, download the appropriate dictionary using the `dictcli.py` script that comes bundled with qutebrowser.

For example, for English (US):

```
$ /usr/share/qutebrowser/scripts/dictcli.py install en-US

```

The script has other features too, which can be shown by using `--help`.

Then set the following in qutebrowser:

```
:set spellcheck.languages ["en-US"]

```

### Minimize fingerprinting

Websites may be able to identify you based on combining information on screen size, user-agent, HTTP_ACCEPT headers, and more. See [[1]](https://panopticlick.eff.org/) for more information and to test the uniqueness of your browser. Below are a few steps that can be taken to make your qutebrowser installation more "generic".

Additionally see [Firefox/Privacy#Configuration](/index.php/Firefox/Privacy#Configuration "Firefox/Privacy") for more ideas.

#### Set a common user-agent

Several user agents are available as options when using `set content.headers.user_agent`. Another, possibly more generic user-agent is:

```
Mozilla/5.0 (Windows NT 10.0; rv:68.0) Gecko/20100101 Firefox/68.0

```

**Note:**

*   You may want to change `Windows NT 10.0` by `X11; Linux x86_64`, since websites can also gather your platform type via Javascript, and this setting cannot be changed in qutebrowser.
*   Changing your user-agent away from the default will prevent some websites from working properly. For example, CAPTCHA will mention your browser is not supported if the user agent is listed as an out-of-date browser.

#### Set a common HTTP_ACCEPT header

The following is a common HTTP_ACCEPT header (Firefox default). Simply type the following commands at the prompt

```
set content.headers.accept_language en-US,en;q=0.5
set content.headers.custom '{"accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"}'

```

#### Disable reading from canvas

```
set content.canvas_reading false

```

**Note:** Some websites depend on canvas reading for content rendering and other functionality. Adding this option may cause them to not work properly [[2]](https://github.com/qutebrowser/qutebrowser/issues/2908).

#### Disable WebGL

Set `content.webgl` to `false` to disable WebGL.

### dwb-like session handling

To have qutebrowser handle sessions more like in [dwb](/index.php/Dwb "Dwb") with the `--restore` option (multiple simultaneously active sessions), you can use [this wrapper script](https://github.com/ayekat/dotfiles/blob/master/lib/dotfiles/bin/qutebrowser). It uses `--basedir` to separate data, cache and runtime for each session, while keeping the configuration shared.

### Disable websites

Put `c.content.host_blocking.lists.append( str(config.configdir) + "/blockedHosts")` in your `config.py`, and create a `blockedHosts` file in the same directory as the config file. Enter websites you want to block one by one; `127.0.0.1 www.youtube.com` for example. This will keep the built-in adblock list while adding the websites in. Restart qutebrowser, and run `:adblock-update`.

## Troubleshooting

### Unreadable tooltips

Depending on your Qt theme, tooltips might be hard to read. In order to fix this, create a Qt Style Sheet file. For example:

 `~/.local/share/qutebrowser/fix-tooltips.qss` 
```
QToolTip {
	background-color: palette(highlight);
	border: 2px solid palette(highlight);
	color: palette(text);
}
```

Then load the style sheet when launching qutebrowser:

```
qutebrowser --qt-arg stylesheet ~/.local/share/qutebrowser/fix-tooltips.qss

```

**Note:** The style sheet won't be applied if there's an instance of qutebrowser already running.

**Tip:** You can use a [desktop entry](/index.php/Desktop_entries#Application_entry "Desktop entries") to create a convenient launcher when specifying extra arguments, such as in this instance.

See the [bug report](https://github.com/qutebrowser/qutebrowser/issues/4520) for details.

## See also

*   [GitHub repository](https://github.com/qutebrowser/qutebrowser)
*   [Homepage](https://qutebrowser.org/)
*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=191076)
*   [New config example](https://bitbucket.org/jasonwryan/shiv/src/tip/.config/qutebrowser/config.py)
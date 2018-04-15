[Uzbl](http://www.uzbl.org/) is a lightweight browser based on **uzbl-core**. **Uzbl** adheres to the UNIX philosophy of "Write programs that do one thing and do it well". The uzbl-browser package includes uzbl-core, uzbl-browser and uzbl-event-manager. Most users will want to use **uzbl-browser** or **uzbl-tabbed** as they provide the fullest set of tools for browsing. Uzbl-browser allows for a single page per window (with as many windows as you want), while uzbl-tabbed provides a wrapper for uzbl-browser and implements basic tabs with multiple pages per window.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plugins](#Plugins)
*   [2 Commands](#Commands)
    *   [2.1 Navigation](#Navigation)
    *   [2.2 Page Movement](#Page_Movement)
    *   [2.3 Zooming](#Zooming)
    *   [2.4 Searching](#Searching)
    *   [2.5 Inserting Text](#Inserting_Text)
    *   [2.6 Bookmarks and History](#Bookmarks_and_History)
    *   [2.7 Tabs (when using uzbl-tabbed)](#Tabs_.28when_using_uzbl-tabbed.29)
    *   [2.8 Other](#Other)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Caching](#Caching)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Parcellite](#Parcellite)
    *   [4.2 TLS certificates](#TLS_certificates)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [uzbl-browser](https://aur.archlinux.org/packages/uzbl-browser/) or [uzbl-tabbed](https://aur.archlinux.org/packages/uzbl-tabbed/) package.

### Plugins

Uzbl can make use of outside [browser plugins](/index.php/Browser_plugins "Browser plugins") like Flash and Java. Installing these packages will enable their use in uzbl-browser and uzbl-tabbed.

## Commands

One of the biggest advantages of using Uzbl is that nearly everything can be controlled by the keyboard. This is preferable to the traditional mouse/keyboard combo because less moving around of the hands is needed. [Vim](/index.php/Vim "Vim") users will find Uzbl much easier to pick-up, especially as the default bindings loosely resemble Vim keystrokes. For instance, following a link requires the user to type `fl`, and then the keystrokes in the box that appears next to each link on the page. Shortening the command to just `f` in the config file allows for even faster navigation.

Below are basic, default commands that can be used with uzbl-browser and uzbl-tabbed. These commands can all be found in `$XDG_CONFIG_HOME/uzbl/config` (which is usually located in `~/.config/uzbl/config`). The default settings work well, but many users like to edit them to suit their preferences and in fact, it is encouraged to change this file to suit your needs. More help with editing the config file can be found on [the Uzbl readme](http://www.uzbl.org/readme.php).

#### Navigation

```
o         = enter url
O         = edit url
b         = back
m         = forward
S         = stop
r         = reload
R         = reload ignoring cache
fl        = spawn numbers next to each hyperlink. Type the number after typing fl to follow the link.
gh        = go home

```

#### Page Movement

```
j         = scroll up
k         = scroll down
h         = scroll left
l         = scroll right
PgUp      = scroll page up
ctrl+b    = scroll page up
PgDn      = scroll page down
ctrl+f    = scroll page down
Home      = vertical beginning of the page
<<        = vertical beginning of the page
End       = vertical end of the page
>>        = vertical end of the page
Space     = vertical end of the page
^         = horizontal beginning of the page
$         = horizontal end of the page
/         = find in page
?         = find backwards in page
n         = repeat find forward
N         = repeat find backwards

```

#### Zooming

```
+         = zoom_in
-         = zoom_out
T         = toggle_zoom_type
1         = set zoom_level = 1
2         = set zoom_level = 2

```

#### Searching

```
ddg       = search term in DuckDuckGo
gg        = search term in Google
\wiki     = search term in Wikipedia

```

#### Inserting Text

```
i         = toggle_insert_mode   (Esc works to go back to command mode much like vim)
fi        = go to the first input field and enter insert mode

```

#### Bookmarks and History

```
M         = insert bookmark (bookmarks are saved in ~/.local/share/uzbl/bookmarks
U         = load url from history via dmenu
u         = load url from bookmarks via dmenu

```

#### Tabs (when using uzbl-tabbed)

```
go       = load uri in new tab
gt        = go to next tab
gT        = go to previous tab
gn        = open new tab
gi+n     = goto 'n' tab
gC         = close current tab

```

#### Other

```
t         = show/hide status bar
w         = open new window
ZZ        = exit
:         = enter command
Esc       = back to normal mode
ctrl+[    = back to normal mode

```

## Tips and tricks

### Caching

Due to its lightweight nature, uzbl does NOT contain caching functionality. You can install [Polipo](/index.php/Polipo "Polipo") to speed up page loading.

## Troubleshooting

### Parcellite

Parcellite can cause problems at the time of selecting text under uzbl - just disable it.

### TLS certificates

Per [this post](https://bbs.archlinux.org/viewtopic.php?id=185014) set the following in `~/.config/uzbl/config`:

```
set ssl_ca_file /etc/ssl/cert.pem
set ssl_policy fail

```

## See also

*   [Uzbl wiki with user config files and scripts](http://www.uzbl.org/wiki/)
*   [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=70700)
*   [Configuration file](https://github.com/Dieterbe/uzbl/raw/master/examples/config/config)
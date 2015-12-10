# UZBL-Browser

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Uzbl](http://www.uzbl.org/) is a lightweight browser based on **uzbl-core**. **Uzbl** adheres to the UNIX philosophy of "Write programs that do one thing and do it well". The uzbl-browser package includes uzbl-core, uzbl-browser and uzbl-event-manager. Most users will want to use **uzbl-browser** or **uzbl-tabbed** as they provide the fullest set of tools for browsing. Uzbl-browser allows for a single page per window (with as many windows as you want), while uzbl-tabbed provides a wrapper for uzbl-browser and implements basic tabs with multiple pages per window.

## Contents

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
*   [3 Commands](#Commands)
    *   [3.1 Navigation](#Navigation)
    *   [3.2 Page Movement](#Page_Movement)
    *   [3.3 Zooming](#Zooming)
    *   [3.4 Searching](#Searching)
    *   [3.5 Inserting Text](#Inserting_Text)
    *   [3.6 Bookmarks and History](#Bookmarks_and_History)
    *   [3.7 Tabs (when using uzbl-tabbed)](#Tabs_.28when_using_uzbl-tabbed.29)
    *   [3.8 Other](#Other)
*   [4 Tips and tricks](#Tips_and_tricks)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") [uzbl-browser](https://www.archlinux.org/packages/?name=uzbl-browser) or [uzbl-tabbed](https://www.archlinux.org/packages/?name=uzbl-tabbed) available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Plugins

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

*   Create an alias in `~/.bashrc` to start uzbl-tabbed as just uzbl:

```
alias uzbl='uzbl-tabbed'

```

*   If you wish to open uzbl with a program launcher using the trick above:

```
 cd /usr/bin
 sudo ln -s uzbl-tabbed uzbl

```

This creates a [symbolic link](https://en.wikipedia.org/wiki/Symbolic_link "wikipedia:Symbolic link"), called uzbl, which points to uzbl-tabbed.

*   Due to its lightweight nature, uzbl does NOT contain caching functionality. You can install [Polipo](/index.php/Polipo "Polipo") to speed up page loading.

## Troubleshooting

Parcellite can cause problems at the time of selecting text under uzbl - just disable it.

## See also

*   [Uzbl wiki with user config files and scripts](http://www.uzbl.org/wiki/)
*   [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=70700)
*   [Configuration file](https://github.com/Dieterbe/uzbl/raw/master/examples/config/config)

Retrieved from "[https://wiki.archlinux.org/index.php?title=UZBL-Browser&oldid=387909](https://wiki.archlinux.org/index.php?title=UZBL-Browser&oldid=387909)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web browser](/index.php/Category:Web_browser "Category:Web browser")
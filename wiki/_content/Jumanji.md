# Jumanji

[jumanji](http://pwmt.org/projects/jumanji/) is a web browser that provides a minimalistic and space saving interface as well as an easy usage that mainly focuses on keyboard interaction like _vimperator_ does.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 config.h](#config.h)
    *   [2.2 rc file configuration](#rc_file_configuration)
*   [3 Commands](#Commands)
    *   [3.1 Look and feel](#Look_and_feel)
    *   [3.2 Page navigation](#Page_navigation)
    *   [3.3 Zooming](#Zooming)
    *   [3.4 Searching](#Searching)
    *   [3.5 Bookmarks and history](#Bookmarks_and_history)
    *   [3.6 Link following](#Link_following)
    *   [3.7 Tabs](#Tabs)
    *   [3.8 Exit](#Exit)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [jumanji-git](https://aur.archlinux.org/packages/jumanji-git/) package to get a development release.

## Configuration

### config.h

To modify config.h:

*   get jumanji-git PKGBUILD from AUR
*   `makepkg`
*   `git --git-dir src/jumanji/ init`
*   change src/jumanji/config.def.h
*   `makepkg -e`

### rc file configuration

jumanji allows for a lot of user configuration either by modifying the config.def.h file or through a rc file located at `~/.config/jumanji/jumanjirc`. you can set searchengines, homepages, custom stylesheets, user scripts, proxy. Change the default download directory and much more. A sample configuration file below shows how to customize jumanji.

```
# jumanji configuration
# search engines
searchengine ggl [http://www.google.com/search?q=%s](http://www.google.com/search?q=%s)
searchengine wiki [http://en.wikipedia.org/w/index.php?search=%s](http://en.wikipedia.org/w/index.php?search=%s)
# browser settings
set homepage [http://www.google.com/ig](http://www.google.com/ig)
set auto_save 60
set single_instance false
# Use privoxy for adblocking
set proxy localhost:8118 
# look n feel
set font monospace normal 9
set stylesheet file:///home/inxs/.config/jumanji/style.css 
# follow hints
script ~/.config/jumanji/scripts/hinting.js
# downloads
set download-dir ~/downloads/
set download_command urxvt -e sh -c "wget --load-cookies ~/.config/jumanji/cookies '%s' -O '%s'";
# keybindings
map <C-,> navigate_history previous
map <C-.> navigate_history next
bmap ^DD$ quit

```

**Note:** Latest version seems to use "proxy localhost:8118" instead of "_set_ proxy localhost:8118".

## Commands

Below are some basic commands that can be used with jumanji

### Look and feel

```
C-m       = Toggle status bar
C-n       = Toggle tab bar

```

### Page navigation

```
o         = enter url to open in same tab
t         = enter url to open in new tab
j         = scroll down
k         = scroll up
h         = scroll left
l         = scroll right
C-d       = scroll down (half the screen)
C-u       = scroll up (half the screen)
space     = page down
gg        = beginning
G         = end
C-o       = back
C-i       = forward
:stop     = stop
r         = reload

```

### Zooming

```
zI        = zoom_in
zO        = zoom_out
z0        = zoom to original size

```

### Searching

```
/        = search %s
?        = search reverse %s
:open    = start a search with your search engine %s (the first one in your jumanjirc is used)

```

### Bookmarks and history

```
:bmark   = insert bookmark (bookmarks are saved in ~/.config/jumanji/bookmarks)
o <tab>  = show bookmarks and history to open in same tab
t <tab>  = show bookmarks and history to open in new tab

```

### Link following

```
f        = spawn numbers next to each hyperlink. Type the number after typing f to follow the link in the same tab [[1]](http://www.pwmt.org/jumanji/faq/)
F        = spawn numbers next to each hyperlink. Type the number after typing F to follow the link in a new tab
gh       = Go to homepage in the same tab
gH       = open homepage in a new tab
gf, C-s  = view source
gF       = view source in a new tab

```

### Tabs

```
gt  or C-Tab   or   S-k   = go to next tab
gT  or C-S-Tab or   S-j   = go to previous tab
xgt                       = go to tab number x, where x is any number 0-9
C-w                       = close tab

```

### Exit

```
ZZ        = exit
C-q       = exit

```

## See also

*   [Old, closed forum thread](https://bbs.archlinux.org/viewtopic.php?id=100505)
*   [The current forum thread](https://bbs.archlinux.org/viewtopic.php?id=115119)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Jumanji&oldid=415874](https://wiki.archlinux.org/index.php?title=Jumanji&oldid=415874)"
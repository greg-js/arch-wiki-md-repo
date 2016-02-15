[Midori](http://midori-browser.org) is a lightweight Webkit-based web browser developed by Christian Dywan. It is part of the [Xfce](/index.php/Xfce "Xfce") Goodies project.

Some of its features are:

*   Full integration with [GTK+](/index.php/GTK%2B "GTK+") 2 and GTK+ 3.
*   Fast rendering, due to the [WebKitGTK+](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit") engine.
*   Tabs, windows, and **session management**.
*   Flexible, configurable web search.
*   Support for **user scripts and styles**.
*   Straightforward **bookmark management**.
*   Customizable and extensible interface.
*   Common **extensions** such as AdBlock, form history, a speed dial, etc.

## Contents

*   [1 Installation](#Installation)
*   [2 Extensions](#Extensions)
    *   [2.1 AdBlock](#AdBlock)
    *   [2.2 Search engines](#Search_engines)
    *   [2.3 User scripts](#User_scripts)
    *   [2.4 Flash plugin](#Flash_plugin)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Flash Block](#Flash_Block)
    *   [3.2 Personal AdBlock filters](#Personal_AdBlock_filters)
    *   [3.3 Fix Pixelated Fonts](#Fix_Pixelated_Fonts)
    *   [3.4 Customizing Toolbars](#Customizing_Toolbars)
*   [4 See also](#See_also)

## Installation

A GTK+2 and GTK+3 versions of Midori can be [installed](/index.php/Pacman "Pacman") with the respective [midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2) and [midori](https://www.archlinux.org/packages/?name=midori) packages, available in the [official repositories](/index.php/Official_repositories "Official repositories").

Development versions are available in the [AUR](/index.php/AUR "AUR"):

*   [midori-gtk2-bzr](https://aur.archlinux.org/packages/midori-gtk2-bzr/) - GTK+ 2 development version.
*   [midori-bzr](https://aur.archlinux.org/packages/midori-bzr/) - GTK+ 3 and WebKitGTK3-based development version.

## Extensions

### AdBlock

To enable the AdBlock extensions go to _Menu > Preferences > Extensions_ and check the _Advertisement blocker_ box.

The AdBlock extension from Midori uses the same lists as the AdBlock Plus extension for Firefox so you can get more lists from the [AdBlock Plus site](http://easylist.adblockplus.org/en/). You can also block specific images on various sites by right-clicking them and choosing _Block image_.

### Search engines

Midori also supports search engines, much in the fashion other browsers do. Various search engines have shortcuts so that they can be easily used from the address bar. To manage your search engines click on the icon in the search engine box and choose _Manage Search Engines_.

Of course you can do clever things with this features, such as provide various shortcuts for various websites (not just for searching). For example you can add another entry to the _Search Engines_ dialog with the token _arch_ and the necessary information for the Arch Linux homepage. Now you can access the Arch Linux website just by typing _arch_.

Another example can be to add a shortcut for an URL shortener:

*   just add a new search engine with the URL `[http://is.gd/create.php?longurl=](http://is.gd/create.php?longurl=)` (or another shortener with similar functionality).
*   set a token for it (_sh_ here).
*   get the short URL for any link by typing:

```
sh _link_

```

in the address bar.

### User scripts

To enable the user scripts extensions go to _Menu > Preferences > Extensions_ and check the _User addons_ box. Midori's user scripts are compatible with [Firefox's Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) scripts. You can find an extensive list of scripts on [http://userscripts-mirror.org/](http://userscripts-mirror.org/) .

For manual installation, you have to create the folder `~/.local/share/midori/scripts` and copy your scripts there. This folder will be automatically picked up by Midori and any compatible scripts will be loaded.

### Flash plugin

To get the Flash plugin working in Midori you can install the [midori-flash](https://aur.archlinux.org/packages/midori-flash/) package from [AUR](/index.php/AUR "AUR") or follow the instructions at [Epiphany#Flash](/index.php/Epiphany#Flash "Epiphany").

If you're running the i686 architecture, or you don't want to use to the AUR script, then install flashplugin from the main repository, and add `export MOZ_PLUGIN_PATH="/usr/lib/mozilla/plugins"` to your .bashrc, or corresponding shell configuration file.

## Tips and tricks

### Flash Block

You can also get the common FlashBlock extension in the form of a user script either from [userscripts-mirror.org](http://userscripts-mirror.org/scripts/show/46673) or by using the [FlashBlock WannaBe script](http://rightfootin.blogspot.fr/2009/04/flashblock-wannabe.html), this script has to be installed in `~/.local/share/midori/scripts` and `~/.local/share/midori/styles`, for the JavaScript file and the CSS file, respectively.

### Personal AdBlock filters

Midori's AdBlock support is rather basic, you can only use pre-made lists or block some images. We can get around that by creating our own lists and telling Midori where to find them.

For this:

*   create a folder for your filters, such as `~/.local/share/midori/filters`
*   in that folder create a file with the content you want to block:

 `myadblockfilters.txt` 

```
[Adblock]
! Title: Personal AdBlocker v1
! Last modified: 31 Oct 2012 18:14 UTC
! Expires: 365 days

! Comments are made with exclamation marks

! You can filter out some elements directly
[http://forums.fedoraforum.org//forum/images/smilies/smile.gif](http://forums.fedoraforum.org//forum/images/smilies/smile.gif)

! Or use wildcards to filter out a bunch of stuff at once
[http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif](http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif)

! Or use use DOM tags, ids or classes
www.phoronix.com#DIV.phxcms_header_legacy
www.phoronix.com#DIV.phxcms_bar_align

```

*   go to _Menu > Preferences > Extensions_ and click the configuration icon of Adblock and add:

```
file://.local/share/midori/filters/myadblockfilters.txt

```

### Fix Pixelated Fonts

Some websites such as github.com tend to use bitmap font from X11, named Clean.

Easy fix is to disable bitmap fonts, run:

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### Customizing Toolbars

Simple right-click somewhere on the top window to customize toolbars. It is possible to hide/show the statusbar, menubar, bookmarkbar and/or navigationbar.

## See also

*   [Midori FAQ](http://wiki.xfce.org/midori/faq)
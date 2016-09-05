Web is the default web browser for [GNOME](https://live.gnome.org/). Web provides a simple and minimalist interface for accessing the internet. Whilst it is developed primarily for GNOME, Web works acceptably in other [desktop environments](/index.php/Desktop_environments "Desktop environments") as well.

**Note:** Web was known as [Epiphany](http://projects.gnome.org/epiphany/) prior to version 3.4\. The application was given new descriptive names, one for each supported language. The name *Epiphany* is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Blocking advertisements](#Blocking_advertisements)
        *   [2.1.1 Managing Subscriptions](#Managing_Subscriptions)
    *   [2.2 Web Apps](#Web_Apps)
*   [3 Plugins](#Plugins)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Pixelated fonts](#Pixelated_fonts)
    *   [4.2 Font hinting](#Font_hinting)
    *   [4.3 Ad-blocking does not work](#Ad-blocking_does_not_work)
*   [5 See also](#See_also)

## Installation

Web can be installed by [installing](/index.php/Install "Install") the [epiphany](https://www.archlinux.org/packages/?name=epiphany) package from the [official repositories](/index.php/Official_repositories "Official repositories"). If you want to save login passwords, install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

## Configuration

### Blocking advertisements

You can enable filtering by unchecking "Allow advertisements" in application preferences. By default, this will enable the [EasyList](https://easylist-downloads.adblockplus.org/easylist.txt) list and is periodically refreshed.

**Note:** Due to some missing features, for example element hiding, Web misses to block/hide some ads. See the [related bugreport](https://bugzilla.gnome.org/show_bug.cgi?id=757824) for progress.

#### Managing Subscriptions

Create the file `~/.config/epiphany/adblock/filters.list` and populate it with URLs (see [EasyList](https://easylist.to/) and [Known Adblock Plus subscriptions](https://adblockplus.org/en/subscriptions)) in a semicolon formatted list:

 `/home/archie/.config/epiphany/adblock/filters.list` 
```
https://easylist.to/easylist/easylist.txt;
https://easylist-downloads.adblockplus.org/easylistdutch.txt;
https://easylist.to/easylist/easyprivacy.txt;
https://easylist.to/easylist/fanboy-annoyance.txt;
https://easylist-downloads.adblockplus.org/antiadblockfilters.txt;
https://easylist-downloads.adblockplus.org/adwarefilters.txt;
https://easylist-downloads.adblockplus.org/malwaredomains_full.txt;
https://raw.githubusercontent.com/liamja/Prebake/master/obtrusive.txt;
https://www.fanboy.co.nz/enhancedstats.txt;

```

On next startup, the application fetches the subscriptions and should create a file for each entry as `~/.config/epiphany/adblock/*32-hex*`.

### Web Apps

Web can add *web app* launchers to GNOME Shell. To manage and remove them, navigate to `about:applications` in Web.

## Plugins

See the main article: [Browser plugins](/index.php/Browser_plugins "Browser plugins")

To find out what plugins are installed/enabled, enter `about:plugins` in the address bar.

## Troubleshooting

### Pixelated fonts

Some websites such as github.com tend to use a bitmap font from X11, named `Clean`. To disable bitmap fonts, run:

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### Font hinting

Web does not respect GNOME hinting settings, but respects Fontconfig one. Check [Font configuration](/index.php/Font_configuration "Font configuration") for further instructions.

### Ad-blocking does not work

Close Web and delete the current filters configuration:

```
rm -r ~/.config/epiphany/adblock/

```

On restart, the filter should be reset.

## See also

*   [Apps/Web - GNOME Wiki!](https://wiki.gnome.org/Apps/Web)
# GNOME/Web

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GNOME](/index.php/GNOME "GNOME")

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** (Discuss in [Talk:GNOME/Web#](https://wiki.archlinux.org/index.php/Talk:GNOME/Web))

Web is the default web browser for [GNOME](https://live.gnome.org/). Web provides a simple and minimalist interface for accessing the internet. Whilst it is developed primarily for GNOME, Web works acceptably in other [desktop environments](/index.php/Desktop_environments "Desktop environments") as well.

**Note:** Web was known as [Epiphany](http://projects.gnome.org/epiphany/) prior to version 3.4\. The application was given new descriptive names, one for each supported language. The name _Epiphany_ is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Flash](#Flash)
    *   [2.2 Web Apps](#Web_Apps)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Pixelated fonts](#Pixelated_fonts)
    *   [3.2 Font hinting](#Font_hinting)
    *   [3.3 Blocking advertisements](#Blocking_advertisements)
*   [4 See also](#See_also)

## Installation

Web can be installed by [installing](/index.php/Install "Install") the [epiphany](https://www.archlinux.org/packages/?name=epiphany) package from the [official repositories](/index.php/Official_repositories "Official repositories"). If you want to save login passwords, install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

## Configuration

### Flash

See [Flash#Flash Player](/index.php/Flash#Flash_Player "Flash").

### Web Apps

Since version 3.0, Web can add _web app_ launchers to GNOME Shell. To manage and remove them, navigate to `about:applications` in Web.

## Troubleshooting

### Pixelated fonts

Some websites such as github.com tend to use a bitmap font from X11, named `Clean`. To disable bitmap fonts, run:

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### Font hinting

Web does not respect GNOME hinting settings, but respects Fontconfig one. Check [Font configuration](/index.php/Font_configuration "Font configuration") for further instructions.

### Blocking advertisements

You can enable filtering by unchecking "Allow advertisements" in application preferences. By default, this will enable the [EasyList](https://easylist-downloads.adblockplus.org/easylist.txt) list.

If this does not work, close GNOME Web, then delete your filters configuration:

```
rm -r ~/.config/epiphany/adblock/

```

and restart the application.

If more than one adblock list is required, create a file named filters.list in:

```
~/.config/epiphany/adblock/ 

```

and populate it with URLs in a semicolon formatted list. On next startup, the application should fetch and apply the new lists.

## See also

*   [Apps/Web - GNOME Wiki!](https://wiki.gnome.org/Apps/Web)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME/Web&oldid=412083](https://wiki.archlinux.org/index.php?title=GNOME/Web&oldid=412083)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [GNOME](/index.php/Category:GNOME "Category:GNOME")
*   [Web browser](/index.php/Category:Web_browser "Category:Web browser")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
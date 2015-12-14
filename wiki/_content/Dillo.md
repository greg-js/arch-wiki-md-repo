# Dillo

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Dillo](http://www.Dillo.org) is a multi-platform graphical web browser known for its speed and small footprint.

*   Dillo is written in C and C++.
*   Dillo is based on FLTK2, the Fast Light Toolkit (statically-linked by default!).
*   Dillo is free software made available under the terms of the GNU General Public License (GPLv3).
*   Dillo strives to be friendly both to users and developers.
*   Dillo helps web authors to comply with web standards by using the bug meter.

## Contents

*   [1 Installing](#Installing)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 Enabling cookies in Dillo by default](#Enabling_cookies_in_Dillo_by_default)
*   [4 Removing cookies](#Removing_cookies)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") [dillo](https://www.archlinux.org/packages/?name=dillo), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Starting

You can start Dillo using `dillo` command.

## Configuration

### Enabling cookies in Dillo by default

Cookies are disabled by default for privacy reasons. If you want to enable them, read [FAQ entry](http://www.dillo.org/FAQ.html#q8)

## Removing cookies

First, stop your plugins (dpis) with the following command:

 `$ dpidc stop` 

The cookies dpi will write any permanent (`ACCEPT`) cookies to disk, and temporary (`ACCEPT_SESSION`) cookies will be lost as the dpi exits.

Second, get rid of the permanent cookies by removing or editing your ~/.dillo/cookies.txt file. Info from [http://www.dillo.org/FAQ.html#q8](http://www.dillo.org/FAQ.html#q8) .

## See also

*   [Dillo Home Page](http://www.dillo.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dillo&oldid=412064](https://wiki.archlinux.org/index.php?title=Dillo&oldid=412064)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web browser](/index.php/Category:Web_browser "Category:Web browser")
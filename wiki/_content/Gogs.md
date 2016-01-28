# Gogs

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Work in progress (Discuss in [Talk:Gogs#](https://wiki.archlinux.org/index.php/Talk:Gogs))

[Gogs](http://gogs.io/) (Go Git Service) is a Self Hosted Git service, which was written in the [Go](/index.php/Go "Go") programming language.

## Contents

*   [1 Packages](#Packages)
*   [2 Installation](#Installation)
*   [3 First start](#First_start)
*   [4 Configuration](#Configuration)
    *   [4.1 .gitignore and license files](#.gitignore_and_license_files)
    *   [4.2 Database](#Database)
        *   [4.2.1 SQLite](#SQLite)
        *   [4.2.2 PostgreSQL](#PostgreSQL)
        *   [4.2.3 MariaDB](#MariaDB)
    *   [4.3 SMTP](#SMTP)
    *   [4.4 oAuth](#oAuth)
    *   [4.5 Logging](#Logging)
    *   [4.6 Caching](#Caching)
*   [5 Theme](#Theme)
*   [6 See also](#See_also)

## Packages

*   [gogs](https://aur.archlinux.org/packages/gogs/)<sup><small>AUR</small></sup> - Release package
*   [gogs-git](https://aur.archlinux.org/packages/gogs-git/)<sup><small>AUR</small></sup> - Git `master` branch package [GitHub master branch](https://github.com/gogits/gogs)
*   [gogs-git-dev](https://aur.archlinux.org/packages/gogs-git-dev/)<sup><small>AUR</small></sup> - Git `dev` branch package [GitHub dev branch](https://github.com/gogits/gogs/tree/develop)

In all three package is sqlite, redis and memcache activate for compile. To use it, you need to edit the configuration file `app.ini` (see [#Configuration](#Configuration)).

## Installation

Installing Gogs from the [AUR](/index.php/AUR "AUR") instead of manually has the added benefit that lots of steps have been taken care of for you (e.g. permissions and ownership for files, etc).

Make sure you perform a system upgrade (`pacman -Syu`) before installing Gogs from AUR and that you have installed the `base-devel` group, or you may face problems installing Gogs because [base-devel packages are not required to be listed as dependencies in PKGBUILD files](https://wiki.archlinux.org/index.php/Makepkg#Usage).

Also before installing the Gogs package from the [AUR](/index.php/AUR "AUR"), you need to choose a database backend if you're planning to host Gogs it on the same machine as the database:

*   SQLite: [sqlite](https://www.archlinux.org/packages/?name=sqlite) - For configuration of Gogs with SQLite see [#SQLite](#SQLite).
*   PostgreSQL: [postgresql](https://www.archlinux.org/packages/?name=postgresql) - Read [PostgreSQL#Installing PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with PostgreSQL see [#PostgreSQL](#PostgreSQL).
*   MariaDB: [mariadb](https://www.archlinux.org/packages/?name=mariadb) - Read [MariaDB#Installation](/index.php/MariaDB#Installation "MariaDB") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with MariaDB see [#MariaDB](#MariaDB).

## First start

After starting of the Gogs service (`systemctl start gogs.service`), you can access the running service over the url `http://[server]:3000`. At the first execute, you will redirect to the installation page. Here you can configure some minor configuration options. In the configuration file `/srv/gogs/conf/app.ini`, you can change more values (for example the port number).

## Configuration

After the first start, Gogs created a own configuration file in the directory `/srv/gogs/config`. When you want to edit a configuration option, you need to edit this file.

### .gitignore and license files

Add the files into the directory `/srv/gogs/conf/gitignore` or `/srv/gogs/conf/license`. When the directory not exist, you need to created it in the first step.

You can get or create own .gitignore files on this [page](http://www.gitignore.io/).

### Database

#### SQLite

#### PostgreSQL

#### MariaDB

### SMTP

### oAuth

### Logging

### Caching

## Theme

The current package (gogs-git* and gogs>=0.4.2) support custom themes. The location for Gogs themes is `/usr/share/themes/gogs/`. Gogs comes with one default theme, but you can easily create a own theme. Just copy the default `theme` directory and change what every you want. In the `public` directory is every javascript, stylesheet and font file and in the `template` directory are the HTML templates. The current selected theme can be changed over the `app.ini` configuration parameter `STATIC_ROOT_PATH`. Changed it with the absolute path to the new theme.

## See also

*   [Official Documentation](http://gogs.io/docs/intro/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gogs&oldid=411950](https://wiki.archlinux.org/index.php?title=Gogs&oldid=411950)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Version Control System](/index.php/Category:Version_Control_System "Category:Version Control System")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
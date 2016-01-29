# KDevelop 4

_"[KDevelop](http://kdevelop.org/) is a free, open source IDE (Integrated Development Environment) for MS Windows, Mac OS X, Linux, Solaris and FreeBSD. It is a feature-full, plugin extensible IDE for C/C++ and other programming languages. It is based on KDevPlatform, and the [KDE](/index.php/KDE "KDE") and [Qt](/index.php/Qt "Qt") libraries and is under development since 1998."_

## Contents

*   [1 Installation](#Installation)
*   [2 Building additional plugins](#Building_additional_plugins)
    *   [2.1 First: install dependency](#First:_install_dependency)
    *   [2.2 PHP](#PHP)
    *   [2.3 Other plugins](#Other_plugins)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 KDevCMakeManager](#KDevCMakeManager)
*   [4 List of available plugins](#List_of_available_plugins)

## Installation

[Install](/index.php/Install "Install") [kdevelop](https://www.archlinux.org/packages/?name=kdevelop) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Building additional plugins

### First: install dependency

The KDevelop Parser Generator in the official repositories ([kdevelop-pg-qt](https://www.archlinux.org/packages/?name=kdevelop-pg-qt)) is required to build additional plugins. Plugins will not compile if this package is not installed beforehand.

### PHP

The PHP plugin ([kdevelop-php](https://www.archlinux.org/packages/?name=kdevelop-php)) from the official repositories provides autocompletion and other PHP-specific features.

Restart KDevelop 4 and you should now have improved PHP support, including autocomplete for both the PHP functions as well as for your project's functions and classes.

### Other plugins

Other plugins are available from [AUR](/index.php/AUR "AUR"): [kdevelop-extra-plugins](https://aur.archlinux.org/packages/?O=0&C=0&SeB=nd&K=kdevelop-&outdated=&SB=n&SO=a&PP=50&do_Search=Go)

## Troubleshooting

### KDevCMakeManager

If you get an error saying that project management plugin could not be loaded ("Could not load project management plugin KDevCMakeManager.") make sure [cmake](https://www.archlinux.org/packages/?name=cmake) is installed.

## List of available plugins

As of June 18 2009, the following plugins are available from KDE's svn repository.

*   automake
*   bazaar
*   check
*   controlflowgraph
*   cppunit
*   csharp
*   ctest
*   duchainviewer
*   java
*   metrics
*   oldgdb
*   php
*   php-docs
*   python
*   qmake
*   qtdesigner
*   ruby
*   sloc
*   teamwork
*   xdebug

**Warning:** As of June 17 2009, do not install the php-docs plugin because it causes the php plugin to stop working.

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDevelop_4&oldid=412114](https://wiki.archlinux.org/index.php?title=KDevelop_4&oldid=412114)"
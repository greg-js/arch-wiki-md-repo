_"[KDevelop](http://kdevelop.org/) is a free, open source IDE (Integrated Development Environment) for MS Windows, Mac OS X, Linux, Solaris and FreeBSD. It is a feature-full, plugin extensible IDE for C/C++ and other programming languages. It is based on KDevPlatform, and the [KDE](/index.php/KDE "KDE") and [Qt](/index.php/Qt "Qt") libraries and is under development since 1998."_

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plugins](#Plugins)
*   [2 Building additional plugins](#Building_additional_plugins)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 KDevCMakeManager](#KDevCMakeManager)

## Installation

[Install](/index.php/Install "Install") the [kdevelop](https://www.archlinux.org/packages/?name=kdevelop) package.

### Plugins

Install plugins to provide autocompletion and other language-specific features:

*   For PHP, install the [kdevelop-php](https://www.archlinux.org/packages/?name=kdevelop-php) package
*   For Python 2, install the [kdevelop-python2](https://www.archlinux.org/packages/?name=kdevelop-python2) package
*   For QML/JavaScript, install the [kdevelop-qmljs](https://www.archlinux.org/packages/?name=kdevelop-qmljs) package

Other plugins are available from the [AUR](/index.php/AUR "AUR"): [search the AUR](https://aur.archlinux.org/packages/?O=0&K=kdevelop-).

## Building additional plugins

The KDevelop Parser Generator ([kdevelop-pg-qt](https://www.archlinux.org/packages/?name=kdevelop-pg-qt) package) is required to build additional plugins. Plugins will not compile if this package is not installed beforehand.

## Troubleshooting

### KDevCMakeManager

If you get an error saying that project management plugin could not be loaded ("Could not load project management plugin KDevCMakeManager.") make sure [cmake](https://www.archlinux.org/packages/?name=cmake) is installed.
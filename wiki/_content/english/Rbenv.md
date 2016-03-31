[rbenv](https://github.com/sstephenson/rbenv) (Simple Ruby Version Management) lets you easily switch between multiple versions of Ruby. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

Another tool to be used for the same purpose is [RVM](/index.php/RVM "RVM").

## Contents

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Ruby 2.x.x](#Ruby_2.x.x)
*   [4 External links](#External_links)

## Installation

You can install [rbenv](https://aur.archlinux.org/packages/rbenv/) from the [AUR](/index.php/AUR "AUR").

## Plugins

rbenv can be extended via a plugin system, and the rbenv wiki includes a [list of useful plugins](https://github.com/sstephenson/rbenv/wiki/Plugins). The ruby-build plugin is especially useful, as it allows you to install Ruby versions with the `rbenv install` command. You can install [ruby-build](https://aur.archlinux.org/packages/ruby-build/) from the AUR.

## Troubleshooting

### Ruby 2.x.x

Installation of Ruby 2.1.4, 2.1.6, 2.1.7, and 2.2.3 may show this error

```
 ossl_ssl.c:141:27: error: ‘SSLv3_method’ undeclared here (not in a function)

```

This can be solved using the patch as described [here](https://github.com/rbenv/ruby-build/issues/834#issuecomment-160627207)

```
 curl -fsSL https://gist.github.com/mislav/055441129184a1512bb5.txt | rbenv install --patch 2.2.3

```

## External links

*   [Official web site](http://rbenv.org/)
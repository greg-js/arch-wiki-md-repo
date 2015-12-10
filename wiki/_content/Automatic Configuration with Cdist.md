# Automatic Configuration with Cdist

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This page describes how to automatically configure archlinux using [cdist](http://www.nico.schottelius.org/software/cdist).

## Contents

*   [1 Introduction](#Introduction)
*   [2 Preperation](#Preperation)
*   [3 How to use the types](#How_to_use_the_types)
*   [4 Type overview](#Type_overview)
*   [5 Managed Desktop (__nico_managed_desktop)](#Managed_Desktop_.28_nico_managed_desktop.29)
*   [6 Notebook (__nico_notebook)](#Notebook_.28_nico_notebook.29)
*   [7 Dos gaming station (__nico_dosbox)](#Dos_gaming_station_.28_nico_dosbox.29)
*   [8 Multimedia Support (__nico_media)](#Multimedia_Support_.28_nico_media.29)
*   [9 User based network configuration (__nico_network_user_based)](#User_based_network_configuration_.28_nico_network_user_based.29)

## Introduction

Cdist is a configuration management system. The author of cdist is also using Archlinux as a target distribution and has some re-usable example configurations online.

## Preperation

Get the [cdist repository with Nicos modications](http://git.schottelius.org/?p=cdist-nico;a=summary):

```
[git://git.schottelius.org/cdist-nico](git://git.schottelius.org/cdist-nico)

```

If you want to start brewing your own configuration tree, it is recommended to get the clean upstream version:

```
[git://git.schottelius.org/cdist](git://git.schottelius.org/cdist)

```

(you should probably read the documentation on the first in any case)

## How to use the types

Edit **cdist/conf/manifest/init**, add your hostname and use the types as seen on the present hosts. Afterwards run

```
./bin/cdist config -v your-host-name

```

And then the your-host-name will be configured.

## Type overview

The following types are present and have been tested on Archlinux systems.

## Managed Desktop (__nico_managed_desktop)

This type is mainly focussed to create a computer usable by non-geeks.

Features:

*   User can shutdown, suspend the computer (pm-utils)
*   Graphical user login (slim)
*   LXDE Desktop environment
*   Office suite (Libreoffice)
*   Browser (chromium)
*   User can configure network (using wicd)

## Notebook (__nico_notebook)

This is the highly personal tuned notebook configuration. Used every 2-3 years when changing the notebook. It contains everything necessary to work (highy biased opinion there).

Some features:

*   LaTeX, i3, mplayer, nfs, wireshark, ...

## Dos gaming station (__nico_dosbox)

This type contains a dosbox installation + some sample games. If you do not know what dos is, you do not need this type.

## Multimedia Support (__nico_media)

Ever searched for tool X to do multimedia action Y? It is probably included in here.

Features:

*   Image viewer
*   Image manipulation
*   Drawing
*   Video playback
*   CD/DVD backup

## User based network configuration (__nico_network_user_based)

This type allows the user to manage the network using wicd. Included are the cli and gui versions.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Automatic_Configuration_with_Cdist&oldid=371592](https://wiki.archlinux.org/index.php?title=Automatic_Configuration_with_Cdist&oldid=371592)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")
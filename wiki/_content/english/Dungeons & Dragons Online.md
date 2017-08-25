This guide will show you how to install and run Dungeons & Dragons Online using [Wine](/index.php/Wine "Wine") on GNU/Linux.

## Contents

*   [1 About](#About)
*   [2 Installation](#Installation)
    *   [2.1 PyLOTRO](#PyLOTRO)
*   [3 Configuration](#Configuration)
    *   [3.1 DirectX 9](#DirectX_9)
    *   [3.2 Copy settings from Windows](#Copy_settings_from_Windows)
*   [4 Resources](#Resources)

## About

[Dungeons & Dragons Online](https://www.ddo.com/) (DDO) is a [MMORPG](https://en.wikipedia.org/wiki/MMORPG "wikipedia:MMORPG") similar to World of Warcraft. DDO usually appeals to more mature RPG fans and focuses more on exploring and completing quests in dungeons rather than on terrain. DDO is *free to play* and doesn't require month subscription fees like WoW but unlike WoW players will often find that leveling will require buying additional *modules* that grant access to certain quests and areas.

## Installation

First, install [Wine](/index.php/Wine "Wine").

If you have already installed DDO on Windows, you can just mount that partition and run `wine 'Dungeons & Dragons Online/TurbineLauncher.exe'`.

You will need an account to play. Sign up for an account on the [Dungeons & Dragons Online website](https://www.ddo.com/). After you have gotten an account, download the Windows client from the website and start it:

```
$ wine ddolive.exe

```

### PyLOTRO

The official launcher is known to hang sometimes. Some people report better results with the unofficial Python-based *PyLOTRO* launcher.

To use PyLOTRO, [install](/index.php/Install "Install") the [pylotro-git](https://aur.archlinux.org/packages/pylotro-git/) package. Then run *pylotro*, set the right game in *Tools > Switch Game*, and point to the installation directory in *Tools > Options*.

## Configuration

### DirectX 9

As of Wine 2.0 (January 2017), only the DirectX 9 mode works. If you have accidentally set it to DirectX 10 or 11, open `~/Documents/Dungeons and Dragons Online/UserPreferences.ini` and set `GraphicsCore=D3D9`.

(With [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) 2.0, D3D10 and D3D11 *do* work, but with lots of graphics artifact, making the game unplayable.)

### Copy settings from Windows

If you have DDO installed on Windows, DDO run through Wine will not recognize the settings from the Windows DDO install. These will need to copied to your GNU/Linux install:

```
$ mkdir ~/Documents/Dungeons\ and\ Dragons\ Online/
$ cp /mnt/win/Users/<USERNAME>/Documents/Dungeons\ and\ Dragons\ Online/* ~/Documents/Dungeons\ and\ Dragons\ Online/

```

## Resources

*   [Wine](/index.php/Wine "Wine")
*   [WineHQ's AppDB entry](http://appdb.winehq.org/objectManager.php?sClass=application&iId=2910)
*   [Codeweaver Errata](http://www.codeweavers.com/compatibility/browse/name/?app_id=4048;tips=1)
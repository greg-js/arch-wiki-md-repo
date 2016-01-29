# Dungeon & Dragons Online

This guide will show you how to install and run Dungeons & Dragons Online using [Wine](/index.php/Wine "Wine") on GNU/Linux.

## Contents

*   [1 About](#About)
*   [2 What Doesn't Work](#What_Doesn.27t_Work)
*   [3 Installation](#Installation)
    *   [3.1 DDO](#DDO)
    *   [3.2 PyLotRO](#PyLotRO)
*   [4 Configuration](#Configuration)
*   [5 Clean Up](#Clean_Up)
*   [6 Resources](#Resources)

## About

[Dungeons & Dragons Online](http://www.ddo.com/) is a [MMORPG](http://en.wikipedia.org/wiki/Mmorpg) similar to World of Warcraft. DDO usually appeals to more mature RPG fans and focuses more on exploring and completing quests in dungeons rather than on terrain. DDO is _free to play_ and doesn't require month subscription fees like WoW but unlike WoW players will often find that leveling will require buying additional _modules_ that grant access to certain quests and areas.

## What Doesn't Work

*   As with all complex games run in Wine, there is a performance penalty. For medium level graphic cards you're probably better off playing DDO in Windows, or accept changing graphic settings from High to Low.
*   Opening video will be choppy unless clicked on.
*   Opening video will not have sound for users with [OSS](/index.php/OSS "OSS").
*   DirectX 10 support cannot be used as it is not supported in Wine yet.
*   Window Manager will occasionally steal mouse-clicks on startup (pressing another key like PrintScreen can sometimes fix this).

## Installation

First a recent version of [Wine](/index.php/Wine "Wine") will need to be installed, then DDO, and then PyLotRO (Python Lord of the Rings Online) will need to be installed to logon to the Turbine servers.

This guide is based on the [WineHQ AppDB entry](http://appdb.winehq.org/objectManager.php?sClass=version&iId=17785) that may or may not be more up to date than this article.

### DDO

If you have already installed DDO on a Windows version skip to [#PyLotRO](#PyLotRO).

You will need an account to play. Sign up for an account on the [Dungeons & Dragons Online website](http://www.ddo.com/). After you have gotten an account, you will need to download an older installer. The installer you will be directed to download after signing up will not run properly with Wine. The older version of the installer will need to be downloaded and then the game client will need to be updated after that.

```
wget [http://download.ddo.level3.turbine.com/largecontent/ddo/mod8/downloader/live/standardres/DDO-US-Mod8-Downloader-StandardRes.exe](http://download.ddo.level3.turbine.com/largecontent/ddo/mod8/downloader/live/standardres/DDO-US-Mod8-Downloader-StandardRes.exe)
wget [http://download.ddo.level3.turbine.com/largecontent/ddo/mod8/downloader/live/highres/DDO-US-Mod8-Downloader-HighRes.exe](http://download.ddo.level3.turbine.com/largecontent/ddo/mod8/downloader/live/highres/DDO-US-Mod8-Downloader-HighRes.exe)

```

The HighRes installer is recommended as settings can be reduced after that. EU locales will need to use a different installer (and possibly account too). Start the installer by:

```
wine DO-US-Mod8-Downloader-HighRes.exe

```

The installer will first download files of about 4GB before installing. After the download, installing to the default location is fine. When the installer gets to installing the .NET Framework it will error (Application has generated an exception that could not be handled) and the .NET Framework will need to be installed manually. Select to quit the installer and then uncheck the option to launch the game.

Download the Window's version of Mono by:

```
wget [http://ftp.novell.com/pub/mono/archive/2.4.2.3/windows-installer/3/mono-2.4.2.3-gtksharp-2.12.9-win32-3.exe](http://ftp.novell.com/pub/mono/archive/2.4.2.3/windows-installer/3/mono-2.4.2.3-gtksharp-2.12.9-win32-3.exe)

```

And then install it by:

```
wine mono-2.4.2.3-gtksharp-2.12.9-win32-3.exe

```

Again installing the default settings will be fine.

### PyLotRO

PyLotRO will be needed to send login infomation to the Turbine servers because the .NET login application does not work properly in Wine.

Install [pylotro](https://aur.archlinux.org/packages/pylotro/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pylotro)]</sup> from the [AUR](/index.php/AUR "AUR").

PyLotRO will need the game library from LotRO to get login information. You can get this by:

```
wget [http://www.lotrolinux.com/LOTRO_EU_Bk13_PatchClient.tar.bz2](http://www.lotrolinux.com/LOTRO_EU_Bk13_PatchClient.tar.bz2)

```

Then extract it:

```
tar xvf LOTRO_EU_Bk13_PatchClient.tar.bz2

```

The library will need to be moved to the DDO directory and renamed so not to get erased on updates:

```
mv patchclient.dll ~/.wine/drive_c/Program\ Files/Turbine/Dungeons\ \&\ Dragons\ Online\ -\ Stormreach/dndlogin.dll

```

If you already have the game installed on Windows, it will have to be moved there (e.g. `/mnt/win/Program\ Files/Turbine/DDO\ Unlimited`).

PyLorRO will need to know the location of your DDO install. If you installed DDO through Wine, start PyLotRO and define DDO by going to 'Tools > Settings Wizard' then select 'Dungeons & Dragons Online' and then 'Find Games'. This will find the DDO install in the Wine directory after which you will have to click 'Apply'. For a Windows install, you will need to go to 'Tools > Options' and define the directory manually. In 'Options' the patchclient downloaded previously will need to be defined. In this case it would be 'dndlogin.dll' and after which you will need to 'Save' the settings.

After this is done the DDO infomation should come up and the DDO client will need to be updated. This is done by going to 'Tools > Patch'. When updating is done, login and test if DDO runs.

## Configuration

If you have DDO installed on Windows, DDO run through Wine will not recognize the settings from the Windows DDO install. These will need to copied to your GNU/Linux install:

```
mkdir ~/Dungeons\ and\ Dragons\ Online
cd /mnt/win/Users/<USERNAME>/Documents/Dungeons\ and\ Dragons\ Online/
cp UserPreferences.ini ddo.keymap ~/Dungeons\ and\ Dragons\ Online

```

## Clean Up

Installing programs through Wine can install a lot of menu items scattered around. To clean up:

```
cd ~/.local/share/applications/wine/Programs/
mv Mono\ 2.4.2.3\ for\ Windows/Uninstall\ Mono-2.4.2.3\ Win32.desktop .
rm -r Mono\ 2.4.2.3\ for\ Windows/
rm -r Administrative\ Tools/
cd Turbine/Dungeons\ \&\ Dragons\ Online\ -\ Stormreach/
rm [A-C]* [R-S]*

```

## Resources

*   [Wine](/index.php/Wine "Wine")
*   [WineHQ's AppDB entry](http://appdb.winehq.org/objectManager.php?sClass=application&iId=2910)
*   [Codeweaver Errata](http://www.codeweavers.com/compatibility/browse/name/?app_id=4048;tips=1)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dungeon_%26_Dragons_Online&oldid=392081](https://wiki.archlinux.org/index.php?title=Dungeon_%26_Dragons_Online&oldid=392081)"
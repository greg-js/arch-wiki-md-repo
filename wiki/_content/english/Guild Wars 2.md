*Guild Wars 2* is a game developed by ArenaNet and published by NC Soft. Currently a native client is only available for Windows and Mac systems. It is runnable through wine though.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Radeon gpu users](#Radeon_gpu_users)
*   [2 Known issues](#Known_issues)
    *   [2.1 Patcher/launcher window is invisible/flickering](#Patcher.2Flauncher_window_is_invisible.2Fflickering)
    *   [2.2 Patcher/launcher crashes with assertion failed on "m_ioCount"](#Patcher.2Flauncher_crashes_with_assertion_failed_on_.22m_ioCount.22)

## Installation

Install [wine](https://www.archlinux.org/packages/?name=wine) or [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) and [mpg123](https://www.archlinux.org/packages/?name=mpg123). Download the GW2 32bit client from their [website](http://cloudfront.guildwars2.com/client/Gw2.exe), or GW2 64bit client from [here](http://s3.amazonaws.com/gw2cdn/client/branches/Gw2-64.exe) (see [this post in the official forum](https://forum-en.guildwars2.com/forum/support/support/64-bit-Client-Beta-FAQ/first#post5717439)) and run it like this:

```
wine ./Gw2.exe

```

or

```
wine ./Gw2-64.exe

```

(For use the 64bit client need set the WINEARCH to 'win64' or use a 64bit WINEPREFIX bottle. or unset WINEARCH for multiarch installation).

Alternatively you can use [WineGW2](http://boxedfox.org/projects/winegw2/) which is a fork of wine that fixes some issues and provides better performance. You may still want to install [wine](https://www.archlinux.org/packages/?name=wine) package to get the dependencies right.

### Radeon gpu users

In case the default [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) driver does yield low fps you can try catalyst drivers. For installation instructions see [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"). (On HD6670 catalyst drivers give higher fps - 40-50 in open-world and there are no graphical glitches) .

As well as that, you will need to install wine with CSMT patch-set applied [wine-staging](https://github.com/wine-compholio/wine-staging/wiki/Installation#-arch-linux) as mouselook in game without it is extremely laggy. After installing you should create 32bit WINEPREFIX and enable CSMT, run:

```
   WINEARCH=win32 winecfg

```

When winecfg launches, select **staging** tab, and check the checkbox "Enable CSMT for better graphic performance", click apply and exit. Run the game by executing launcher with -dx9single flag which fixes various launcher issues:

```
   wine Gw2.exe -dx9single

```

*   When in game, its a good idea to start tweaking graphical settings from medium/low for each setting until you find optimal settings that give you playable fps.
*   Warning: Enabling Vsync causes the game to lock max fps at 30, enable this feature at your own risk.

## Known issues

### Patcher/launcher window is invisible/flickering

Run it with -dx9single like so:

```
wine ./Gw2.exe -dx9single

```

or

```
wine ./Gw2-64.exe -dx9single

```

if use a 64bit client

### Patcher/launcher crashes with assertion failed on "m_ioCount"

The best known "fix" for this is to just let it crash and restart it, it should continue on where it left off. Some people reports that the installer crashes when approximately 1 GB has been downloaded but some other people reports crashes every few minutes. This however is rarely a problem when installing patches and only the initial installation poses a challenge, reason why some people just copy the Gw2 installation directory or the Gw2.dat from a Windows installation into the GW2 installation directory in Linux (`/wineprefix/GuildWars2/drive_c/Program Files/ArenaNet/Guild Wars 2/`) when installing the game.

The percent of the download resets every time the launcher is started, but the amount that has already downloaded is not accounted into this number; just what remains is. The best number correlates with the total download progress is the **Files Remaining**.

If you have only one file remaining, switch to a language other than english or spanish, let it download that information, and then switch back to English.
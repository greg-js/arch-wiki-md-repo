This page explains how to install Diablo II and play it under Arch Linux. This works as of 2016-08-14.

If you already have a Diablo II installation (for example, installed under Windows on another partition), simply update that version to the latest patch (trying to log into Battle.net will start the update automatically), launch it once (to migrate your characters and the CD-Key, should it still be stored in the registry - newer versions store it next to the game's binary). You may now start playing on Arch with Wine - no additional dependencies are required for the game itself.

## Contents

*   [1 Installing](#Installing)
*   [2 Playing](#Playing)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error "ACCESS_VIOLATION" on start](#Error_.22ACCESS_VIOLATION.22_on_start)
    *   [3.2 Sound option is greyed out](#Sound_option_is_greyed_out)

## Installing

Those packages are needed in order to run the Blizzard Downloader:

*   [lib32-libjpeg-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg-turbo) ([libjpeg-turbo](https://www.archlinux.org/packages/?name=libjpeg-turbo) on i686)
*   [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap) ([libldap](https://www.archlinux.org/packages/?name=libldap) on i686)

If any of those is not installed, downloaders will fail to start. You may download the standalone installers on Windows to avoid installing these.

Set up a working [Wine](/index.php/Wine "Wine") environment. Download Diablo II and Diablo II Lord of Destruction installation files [from Battle.net](https://eu.battle.net/account/management/download/) - launch downloaders, pick a directory to download the installers into. Launch the Diablo II installer, enter your key. Then install Lord of Destruction (the directory will be set automatically, you'll need to enter just the key). Launch the game once and try logging into Battle.net to download the latest patch.

If the installers were downloaded from Battle.net, keys are 26-character, generated for you when you've registered games on Battle.net, available on product pages for [Diablo 2](https://eu.battle.net/account/management/classic-games.html?license=20) and [Lord of Destruction](https://eu.battle.net/account/management/classic-games.html?license=23) - original keys from the CDs will work only with the installers from the CDs themselves. However, the original versions from the CDs have somewhat serious compatibility issues even with newer Windows versions (by newer, think XP), and as such are not recommended anymore.

In the past, a game CD was required to launch the game (with a rather nasty workaround for non-Windows OSes if you didn't want to use a NoCD crack, which was not exactly Battle.net-safe). They're no longer needed - in recent patches, the protection has been removed completely.

## Playing

If you use a desktop, you can create a shortcut. Otherwise just run:

```
$ wine ~/.wine/drive_c/Program\ Files/Diablo\ II/Game.exe

```

## Troubleshooting

### Error "ACCESS_VIOLATION" on start

Try setting `dsoundhw=Emulation`. This can be done by starting winetricks *Select the default wineprefix* and then choose *Change settings* and check the box in front of *dsoundhw=Emulation*. Another thing to try is to add `-w` at the end of the command line. It will launch the game in windowed mode but it should work where fullscreen does not.

### Sound option is greyed out

Fix with: `pacman -S mpg123 lib32-mpg123`
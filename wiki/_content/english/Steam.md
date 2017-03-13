From [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

	Steam is a digital distribution, digital rights management, multiplayer and communications platform developed by Valve Corporation. It is used to distribute games and related media online, from small independent developers to larger software houses.

[Steam](http://store.steampowered.com/about/) is best known as the platform needed to play Source Engine games (e.g. Half-Life 2, Counter-Strike). Today it offers many games from many other developers.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Big Picture Mode](#Big_Picture_Mode)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Launching games with custom commands](#Launching_games_with_custom_commands)
    *   [3.2 Skins for Steam](#Skins_for_Steam)
    *   [3.3 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
        *   [3.3.1 Use a skin](#Use_a_skin)
        *   [3.3.2 On-the-fly patch](#On-the-fly_patch)
    *   [3.4 Silent Mode](#Silent_Mode)
    *   [3.5 Streaming server](#Streaming_server)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

**Note:**

*   Arch Linux is **not** [officially supported](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366).
*   If you have a 64-bit system, enable the [multilib](/index.php/Multilib "Multilib") repository.

[Install](/index.php/Install "Install") the [steam](https://www.archlinux.org/packages/?name=steam) package.

Steam is not supported on this distribution. As such some fixes are needed on the users part to get things functioning properly:

*   If you have a 64-bit system, you will be prompted to install the 32-bit version of your [graphics driver](/index.php/Xorg#Driver_installation "Xorg") (via the `lib32-libgl` dependency)
*   Steam may fail to start due to broken/missing libraries. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").
*   Steam makes heavy usage of the Arial font. A decent Arial font to use is [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [the fonts provided by Steam](/index.php/Steam/Troubleshooting#Text_is_corrupt_or_missing "Steam/Troubleshooting"). Asian languages require [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) to display properly.
*   Several games have dependencies which may be missing from your system. If a game fails to launch (often without error messages) then make sure all of the libraries listed in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") are installed.
*   In case that you are using Arch Linux in your local language, make sure that you also have properly generated en_US locales (see [Locale#Generating locales](/index.php/Locale#Generating_locales "Locale")). Otherwise Steam client wont start with **invalid pointer** error.

## Usage

### Big Picture Mode

To start Steam in Big Picture Mode from a [Display manager](/index.php/Display_manager "Display manager"), create a `/usr/share/xsessions/steam-big-picture.desktop` file with the following contents:

 `/usr/share/xsessions/steam-big-picture.desktop` 
```
[Desktop Entry]
Name=Steam Big Picture Mode
Comment=Start Steam in Big Picture Mode
Exec=/usr/bin/steam -bigpicture
TryExec=/usr/bin/steam
Icon=
Type=Application
```

## Tips and tricks

### Launching games with custom commands

Steam has fortunately added support for launching games using your own custom command. To do so, navigate to the Library page, right click on the selected game, click Properties, and Set Launch Options. Steam replaces the tag `%command%` with the command it actually wishes to run. For example, to launch Team Fortress 2 with primusrun and at resolution 1920x1080, you would enter:

```
primusrun %command% -w 1920 -h 1080

```

The corresponding example for AMD PRIME users is:

```
DRI_PRIME=1 %command%

```

If you are running the [Linux-ck](/index.php/Linux-ck "Linux-ck") kernel, you may have some success in reducing overall latencies and improving performance by launching the game in SCHED_ISO (low latency, avoid choking CPU) via [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% *other arguments*

```

Also keep in mind that Steam [does not really care](http://i.imgur.com/oJcLDBi.png) what you want it to run. By setting `%command%` to an environment variable, you can have Steam run whatever you would like. For example, the Launch Option used in the image above:

```
IGNORE_ME=%command% glxgears

```

### Skins for Steam

**Note:** Using skins that are not up-to-date with the version of the Steam client may cause visual errors.

The Steam interface can be fully customized by copying its various interface files in its skins directory and modifying them.

An extensive list of skins can be found on [Steam's forums](http://forums.steampowered.com/forums/showthread.php?t=1161035).

### Changing the Steam friends notification placement

**Note:** A handful of games do not support this, for example this can not work with XCOM: Enemy Unknown.

#### Use a skin

You can create a skin that does nothing but change the notification corner. First you need to create the directories:

```
 $ mkdir -p $HOME/Top-Right/resource
 $ cp -R $HOME/.steam/steam/resource/styles $HOME/Top-Right/resource/
 $ mv $HOME/Top-Right $HOME/.local/share/Steam/skins/
 $ cd .local/share/Steam/skins/
 $ cp -R Top-Right Top-Left && cp -R Top-Right Bottom-Right

```

Then modify the correct files. `Top-Right/resource/styles/gameoverlay.style` will change the corner for the in-game overlay whereas `steam.style` will change it for your desktop.

Now find the entry: `Notifications.PanelPosition` in whichever file you opened and change it to the appropriate value, for example for Top-Right:

```
 Notifications.PanelPosition     "TopRight"

```

This line will look the same in both files. Repeat the process for all the 3 variants (`Top-Right`, `Top-Left` and `Bottom-Left`) and adjust the corners for the desktop and in-game overlay to your satisfaction for each skin, then save the files.

To finish you will have to select the skin in Steam: *Settings > Interface* and *<default skin>* in the drop-down menu.

You can use these files across distributions and even between Windows and Linux (macOS has its own entry for the desktop notification placement)

#### On-the-fly patch

This method is more compatible with future updates of Steams since the files in the skins above are updated as part of steam and as such if the original files change, the skin will not follow the graphics update to steam and will have to be re-created every time something like that happens. Doing things this way will also give you the ability to use per-game notification locations as you can run a patch changing the location of the notifications by specifying it in the launch options for games.

Steam updates the files we need to edit everytime it updates (which is everytime it is launched) so the most effective way to do this is patching the file after Steam has already been launched.

First you will need a patch:

 `$HOME/.steam/topright.patch` 
```
--- A/steam/resource/styles/gameoverlay.styles	2013-06-14 23:49:36.000000000 +0000
+++ B/steam/resource/styles/gameoverlay.styles	2014-07-08 23:13:15.255806000 +0000
@@ -7,7 +7,7 @@
 		mostly_black "0 0 0 240"
 		semi_black "0 0 0 128"
 		semi_gray "32 32 32 220"
-		Notifications.PanelPosition     "BottomRight"
+		Notifications.PanelPosition     "TopRight"
 	}

 	styles

```

**Note:** The patch file should have all above lines, including the newline at the end.

You can edit the entry and change it between "BottomRight"(default), "TopRight" "TopLeft" and "BottomLeft": the following will assume you used "TopRight" as in the original file.

Next create an alias in `$HOME/.bashrc`:

```
 alias steam_topright='pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd'

```

Log out and back in to refresh the aliases. Launch Steam and wait for it to fully load, then run the alias

```
 $ steam_topright

```

And most games you launch after this will have their notification in the upper right corner.

You can also duplicate the patch and make more aliases for the other corners if you do not want all games to use the same corner so you can switch back.

To automate the process you will need a script file as steam launch options cannot read your aliases. The location and name of the file could for example be **$HOME/.scripts/steam_topright.sh**, and assuming that is the path you used, it needs to be executable:

```
 $ chmod +755 $HOME/.scripts/steam_topright.sh

```

The contents of the file should be the following:

```
 #!/bin/sh
 pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd

```

And the launch options should be something like the following.

```
 $HOME/.scripts/steam_topright.sh && %command%

```

There is another file in the same folder as **gameoverlay.style** folder called **steam.style** which has an entry with the exact same function as the file we patched and will change the notification corner for the desktop only (not in-game), but for editing this file to actually work it has to be set before steam is launched and the folder set to read-only so steam cannot re-write the file. Therefore the only two ways to modify that file is to make the directory read only so steam cannot change it when it is launched (can break updates) or making a skin like in method 1.

### Silent Mode

To stop the main window from showing at startup, use the `-silent` option:

```
$ steam -silent

```

**Tip:** This option can be added to a [desktop entry](/index.php/Desktop_entry "Desktop entry").

### Streaming server

See [https://steamcommunity.com/sharedfiles/filedetails/?id=680514371](https://steamcommunity.com/sharedfiles/filedetails/?id=680514371)

## Troubleshooting

See [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting").

## See also

*   [Steam](https://wiki.gentoo.org/wiki/Steam) at Gentoo wiki
*   [The Big List of DRM-Free Games on Steam](http://pcgamingwiki.com/wiki/The_Big_List_of_DRM-Free_Games_on_Steam) at PCGamingWiki
*   [List of DRM-free games](http://steam.wikia.com/wiki/List_of_DRM-free_games) at wikia
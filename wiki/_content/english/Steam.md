From [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

	*Steam is a digital distribution, digital rights management, multiplayer and communications platform developed by Valve Corporation. It is used to distribute games and related media online, from small independent developers to larger software houses.*

[Steam](http://store.steampowered.com/about/) is best known as the platform needed to play Source Engine games (e.g. Half-Life 2, Counter-Strike). Today it offers many games from many other developers.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Big Picture Mode (with a Display Manager)](#Big_Picture_Mode_.28with_a_Display_Manager.29)
    *   [2.2 Silent Mode](#Silent_Mode)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Launching games with custom commands](#Launching_games_with_custom_commands)
    *   [3.2 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
    *   [3.3 Using native runtime](#Using_native_runtime)
    *   [3.4 Skins for Steam](#Skins_for_Steam)
        *   [3.4.1 Steam skin manager](#Steam_skin_manager)
    *   [3.5 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
        *   [3.5.1 Use a skin](#Use_a_skin)
        *   [3.5.2 On-the-fly patch](#On-the-fly_patch)
*   [4 See also](#See_also)

## Installation

**Note:** Arch Linux is **not** [officially supported](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366).

If you have a 64-bit system, enable the [multilib](/index.php/Multilib "Multilib") repository.

[Install](/index.php/Install "Install") the [steam](https://www.archlinux.org/packages/?name=steam) package.

Steam is not supported on this distribution. As such some fixes are needed on the users part to get things functioning properly:

*   Steam makes heavy usage of the Arial font. A decent Arial font to use is [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [the fonts provided by Steam](#Text_is_corrupt_or_missing). Asian languages require [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) to display properly.

*   If you have a 64-bit system, you **must** install the 32-bit Multilib version of your [graphics driver](/index.php/Xorg#Driver_installation "Xorg").

*   If you have a 64-bit system, you will need to install [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) to enable sound.

*   Several games have dependencies which may be missing from your system. If a game fails to launch (often without error messages) then make sure all of the libraries listed in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") are installed.

## Usage

### Big Picture Mode (with a Display Manager)

To start Steam in Big Picture Mode from a Display Manager (such as LightDM), create a `/usr/share/xsessions/steam-big-picture.desktop` file with the following content:

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

Alternatively, under Steam > Settings > Interface, check 'Start Steam in Big Picture Mode' and start Steam normally. This can behave slightly better with certain window managers than the command line option.

### Silent Mode

To stop the main window from showing at startup, use the `-silent` option:

```
$ steam -silent

```

alternatively, if you launch Steam from a desktop shortcut, you can add this option to a custom [desktop entry](/index.php/Desktop_entry "Desktop entry"):

 `~/.config/autostart/steam.desktop` 
```
[Desktop Entry]
Name=Steam
...
Exec=/usr/bin/steam -silent %U
...

```

## Tips and tricks

### Launching games with custom commands

Steam has fortunately added support for launching games using your own custom command. To do so, navigate to the Library page, right click on the selected game, click Properties, and Set Launch Options. Steam replaces the tag `%command%` with the command it actually wishes to run. For example, to launch Team Fortress 2 with primusrun and at resolution 1920x1080, you would enter:

```
primusrun %command% -w 1920 -h 1080

```

On some systems optirun gives better performances than primusrun, however some games may crash shortly after the launch. This may be fixed preloading the correct version of libGL. Use:

```
locate libGL

```

to find out the available implementations. For a 64 bits game you may want to preload the nvidia 64 bits libGL, then use the launch command:

```
LD_PRELOAD=/usr/lib/nvidia/libGL.so optirun %command%

```

If you are running the [Linux-ck](/index.php/Linux-ck "Linux-ck") kernel, you may have some success in reducing overall latencies and improving performance by launching the game in SCHED_ISO (low latency, avoid choking CPU) via [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% *other arguments*

```

Also keep in mind that Steam [doesn't really care](http://i.imgur.com/oJcLDBi.png) what you want it to run. By setting `%command%` to an environment variable, you can have Steam run whatever you would like. For example, the Launch Option used in the image above:

```
IGNORE_ME=%command% glxgears

```

### Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; compton -b &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

### Using native runtime

Steam, by default, ships with a copy of every library it uses, packaged within itself, so that games can launch without issue. This can be a resource hog, and the slightly out-of-date libraries they package may be missing important features (Notably, the OpenAL version they ship lacks [HRTF](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming") and surround71 support). To use your own system libraries, you can run Steam with:

```
$ STEAM_RUNTIME=0 steam

```

However, if you are missing any libraries Steam makes use of, this will fail to launch properly. An easy way to find the missing libraries is to run the following commands:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ LD_LIBRARY_PATH=".:${LD_LIBRARY_PATH}" ldd $(file *|sed '/ELF/!d;s/:.*//g')|grep 'not found'|sort|uniq

```

**Note:** The libraries will have to be 32-bit, which means you may have to download some from the AUR if on x86_64, such as NetworkManager.

Once you have done this, run steam again with `STEAM_RUNTIME=0 steam` and verify it is not loading anything outside of the handful of steam support libraries:

```
$ < /proc/$(pidof steam)/maps|sed '/\.local/!d;s/.*  //g'|sort|uniq

```

**Convenience repository**

The unofficial [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repository contains all libraries needed to run native steam on x86_64\. Please note that, for some reason, steam does not pick up sdl2 or libav* even if you have them installed. It will still use the ones it ships with.

All you need to install is the meta-package `steam-libs`, it will pull all the libs for you. Please report if there is any missing library, the maintainer already had some lib32 packages installed so a library may have been overlooked.

### Skins for Steam

**Note:** Using skins that are not up-to-date with the version of the Steam client may cause visual errors.

The Steam interface can be fully customized by copying its various interface files in its skins directory and modifying them.

An extensive list of skins can be found on [Steam's forums](http://forums.steampowered.com/forums/showthread.php?t=1161035).

#### Steam skin manager

The process of applying a skin to Steam can be greatly simplified by installing the [steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/) package. The package also comes with a hacked version of the Steam launcher which allows the window manager to draw its borders on the Steam window.

As a result, skins for Steam will come in two flavors, one with and one without window buttons. The skin manager will prompt you whether you use the hacked version or not, and will automatically apply the theme corresponding to your GTK+ theme if it is found. You can of course still apply another skin if you want.

The package ships with two themes for the default Ubuntu themes, Ambiance and Radiance.

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

You can use these files across distributions and even between Windows and Linux (OS X has its own entry for the desktop notification placement)

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

## See also

*   [Steam](https://wiki.gentoo.org/wiki/Steam) at Gentoo wiki
*   [The Big List of DRM-Free Games on Steam](http://pcgamingwiki.com/wiki/The_Big_List_of_DRM-Free_Games_on_Steam) at PCGamingWiki
*   [List of DRM-free games](http://steam.wikia.com/wiki/List_of_DRM-free_games) at wikia
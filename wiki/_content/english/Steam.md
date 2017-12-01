Related articles

*   [Steam/Wine](/index.php/Steam/Wine "Steam/Wine")
*   [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")
*   [Gamepad](/index.php/Gamepad "Gamepad")
*   [Games](/index.php/Games "Games")
*   [List of games](/index.php/List_of_games "List of games")

From [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

	Steam is a digital distribution, digital rights management, multiplayer and communications platform developed by Valve Corporation. It is used to distribute games and related media online, from small independent developers to larger software houses.

[Steam](http://store.steampowered.com/about/) is best known as the platform needed to play Source Engine games (e.g. Half-Life 2, Counter-Strike). Today it offers many games from many other developers.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 SteamCMD](#SteamCMD)
    *   [1.2 Alternative Flatpak installation](#Alternative_Flatpak_installation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Directory structure](#Directory_structure)
    *   [3.2 Launch options](#Launch_options)
    *   [3.3 Big Picture Mode without a window manager](#Big_Picture_Mode_without_a_window_manager)
    *   [3.4 Steam skins](#Steam_skins)
        *   [3.4.1 Creating skins](#Creating_skins)
    *   [3.5 Changing the Steam notification position](#Changing_the_Steam_notification_position)
        *   [3.5.1 Use a skin](#Use_a_skin)
        *   [3.5.2 Live patching](#Live_patching)
    *   [3.6 In-Home Streaming](#In-Home_Streaming)
    *   [3.7 Finding a games AppID](#Finding_a_games_AppID)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

**Note:** Arch Linux is **not** officially supported, the only officially supported distribution is Ubuntu. [[1]](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366)

Enable the [Multilib](/index.php/Multilib "Multilib") repository and [install](/index.php/Install "Install") the [steam](https://www.archlinux.org/packages/?name=steam) package.

The following fixes are needed to get Steam functioning properly on Arch Linux:

*   You need to install the 32-bit version of your [graphics driver](/index.php/Xorg#Driver_installation "Xorg") (the package in the *OpenGL (Multilib)* column).
*   Steam may fail to start due to broken/missing libraries. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").
*   Steam makes heavy usage of the Arial font. A decent Arial font to use is [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [the fonts provided by Steam](/index.php/Steam/Troubleshooting#Text_is_corrupt_or_missing "Steam/Troubleshooting"). Asian languages require [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) to display properly.
*   Several games have dependencies which may be missing from your system. If a game fails to launch (often without error messages) then make sure all of the libraries listed in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") are installed.
*   In case that you are using Arch Linux in your local language, make sure that you also have properly generated en_US locales (see [Locale#Generating locales](/index.php/Locale#Generating_locales "Locale")). Otherwise Steam client wont start with **invalid pointer** error.

### SteamCMD

For the [SteamCMD](https://developer.valvesoftware.com/wiki/SteamCMD), a command-line version of the Steam client, that is primarily used to install and update dedicated servers, [install](/index.php/Install "Install") the [steamcmd](https://aur.archlinux.org/packages/steamcmd/) package.

**Note:** The AUR package installs files owned by root, so you must be root to update SteamCMD itself.

### Alternative Flatpak installation

Steam can also be installed with [Flatpak](/index.php/Flatpak "Flatpak") as `com.valvesoftware.Steam` from [Flathub](https://flathub.org/).

```
pacman -S flatpak

```

```
flatpak install --from [https://flathub.org/repo/appstream/com.valvesoftware.Steam.flatpakref](https://flathub.org/repo/appstream/com.valvesoftware.Steam.flatpakref)

```

The Flatpak application currently does not support themes. Also you currently can't run games via `optirun`/`primusrun`, see [Issue#869](https://github.com/flatpak/flatpak/issues/869) for more details.

By default Steam won't be able to access your home directory, you can run the following command to allow it, so that it behaves like on Ubuntu or SteamOS:

```
flatpak override com.valvesoftware.Steam --filesystem=/home/$USER

```

Note: Some games don't work fully or at all. May be wise to use a flatpak steam install, as a backup way to access steam, in case an arch update prevents Steam from launching correctly.

## Usage

To start Steam simply run `steam`.

*   `-bigpicture` to start in Big Picture Mode
*   `-silent` don't open the main window

## Tips and tricks

### Directory structure

`~/.steam/` by default contains the following symlinks:

```
bin   -> ~/.steam/bin32
bin32 -> ~/.local/share/Steam/ubuntu12_32
bin64 -> ~/.local/share/Steam/ubuntu12_64
root  -> ~/.local/share/Steam
sdk32 -> ~/.local/share/Steam/linux32
sdk64 -> ~/.local/share/Steam/linux64
steam -> ~/.local/share/Steam

```

As you can see Steam stores its files in `~/.local/share/Steam/` by default. You can change where Steam stores its content by moving `~/.local/share/Steam/` and starting Steam, which will prompt you if you have moved your Steam content. You can then browse to the new location and Steam will update the symlinks in `~/.steam/`.

Games are installed in `~/.steam/root/steamapps/common/`.

### Launch options

To set custom launch options for a game, right-click on it in your library, select Properties and click on the Set Launch Options button.

When your launch options contain `%command%` Steam will replace it with the game's launch command, otherwise Steam will prefix the launch command to your launch options. The resulting command is then run in a [Bash](/index.php/Bash "Bash") shell, allowing you to set environment variables before `%command%`.

### Big Picture Mode without a window manager

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

### Steam skins

The Steam interface can be customized using skins. Skins can overwrite interface-specific files in `~/.steam/steam`.

To install a skin:

1.  Place its directory in `~/.local/share/Steam/skins`.
2.  Open *Steam > Settings > Interface* and select it.
3.  Restart Steam.

An extensive list of skins can be found in [this Steam forums post](http://forums.steampowered.com/forums/showthread.php?t=1161035).

**Note:** Using an outdated skin may cause visual errors.

#### Creating skins

Nearly all Steam styles are defined in `~/.steam/steam/resource/styles/steam.styles` (the file is over 3,500 lines long). For a skin to be recognized it needs its own `resource/styles/steam.styles`. When a Steam update changes the official `steam.styles` your skin may become outdated, potentially resulting in visual errors.

See `~/.local/share/Steam/skins/skins_readme.txt` for a primer on how to create skins.

### Changing the Steam notification position

The default Steam notification position is bottom right.

You can change the Steam notification position by altering `Notifications.PanelPosition` in

*   `resource/styles/steam.styles` for desktop notifications, and
*   `resource/styles/gameoverlay.styles` for in-game notifications

Both files are overwritten by Steam on startup and `steam.styles` is only read on startup.

**Note:** Some games do not respect the setting in `gameoverlay.styles` e.g. XCOM: Enemy Unknown.

#### Use a skin

You can create a skin to change the notification position to your liking. For example to change the position to top right:

```
$ cd ~/.local/share/Steam/skins
$ mkdir -p Top-Right/resource
$ cp -r ~/.steam/steam/resource/styles Top-Right/resource
$ sed -i '/Notifications.PanelPosition/ s/"[A-Za-z]*"/"TopRight"/' Top-Right/resource/styles/*

```

#### Live patching

`gameoverlay.styles` can be overwritten while Steam is running, allowing you to have game-specific notification positions.

 `~/.steam/notifpos.sh` 
```
sed -i "/Notifications.PanelPosition/ s/\"[A-Za-z]*\"/\"$1\"/" ~/.steam/steam/resource/styles/gameoverlay.styles

```

And the [#Launch options](#Launch_options) should be something like:

```
~/.steam/notifpos.sh TopLeft && %command%

```

### In-Home Streaming

Steam has built-in support for [In-Home Streaming](http://store.steampowered.com/streaming/).

See [this Steam Community guide](https://steamcommunity.com/sharedfiles/filedetails/?id=680514371) on how to setup a headless In-Home Streaming server on Linux.

### Finding a games AppID

Every Steam application has a unique AppID.

To find the AppID of an installed game:

1.  Right click on the game in your library, select create desktop shortcut.
2.  Open the created file `~/Desktop/<game>.desktop` with a text editor.
3.  Find the AppID in the Exec command `Exec=steam steam://rungameid/<appid>`.

Alternatively find the game's [Steam Store](http://store.steampowered.com/) page and check out the URL:

```
http://store.steampowered.com/app/<appid>/<name>/

```

## Troubleshooting

See [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting").

## See also

*   [Gentoo Wiki article](https://wiki.gentoo.org/wiki/Steam)
*   [The Big List of DRM-Free Games on Steam](https://pcgamingwiki.com/wiki/The_Big_List_of_DRM-Free_Games_on_Steam) at PCGamingWiki
*   [List of DRM-free games](http://steam.wikia.com/wiki/List_of_DRM-free_games) at Wikia
*   [Steam Linux store](http://store.steampowered.com/browse/linux)
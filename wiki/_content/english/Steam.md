Related articles

*   [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")
*   [Gaming](/index.php/Gaming "Gaming")
*   [Gamepad](/index.php/Gamepad "Gamepad")
*   [List of games](/index.php/List_of_games "List of games")

[Steam](http://store.steampowered.com/about/) is a popular game distribution platform by Valve.

**Note:** Steam for Linux only supports Ubuntu LTS.[[1]](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366) Thus, do not turn to Valve for support for issues with Steam on Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 SteamCMD](#SteamCMD)
    *   [1.2 Alternative Flatpak installation](#Alternative_Flatpak_installation)
        *   [1.2.1 Asian Font Problems with Flatpak](#Asian_Font_Problems_with_Flatpak)
*   [2 Directory structure](#Directory_structure)
    *   [2.1 Library folders](#Library_folders)
*   [3 Usage](#Usage)
*   [4 Launch options](#Launch_options)
    *   [4.1 Examples](#Examples)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Fsync patch](#Fsync_patch)
    *   [5.2 Proton Steam-Play](#Proton_Steam-Play)
    *   [5.3 Big Picture Mode without a window manager](#Big_Picture_Mode_without_a_window_manager)
    *   [5.4 Steam skins](#Steam_skins)
        *   [5.4.1 Creating skins](#Creating_skins)
    *   [5.5 Changing the Steam notification position](#Changing_the_Steam_notification_position)
        *   [5.5.1 Use a skin](#Use_a_skin)
        *   [5.5.2 Live patching](#Live_patching)
    *   [5.6 Steam Remote Play](#Steam_Remote_Play)
        *   [5.6.1 Different subnets](#Different_subnets)
    *   [5.7 Steam Controller](#Steam_Controller)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 See also](#See_also)

## Installation

Enable the [multilib](/index.php/Multilib "Multilib") repository and [install](/index.php/Install "Install") the [steam](https://www.archlinux.org/packages/?name=steam) package.

The following requirements must be fulfilled in order to run Steam on Arch Linux:

*   Installed 32-bit version [OpenGL graphics driver](/index.php/Xorg#Driver_installation "Xorg").
*   Generated [en_US.UTF-8](/index.php/Locale#Generating_locales "Locale") locale, preventing invalid pointer error.
*   The GUI heavily uses the Arial font. See [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts"). An alternative is to use [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [fonts provided by Steam](/index.php/Steam/Troubleshooting#Text_is_corrupt_or_missing "Steam/Troubleshooting") instead.
*   Install [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) to add support for Asian languages.

### SteamCMD

Install [steamcmd](https://aur.archlinux.org/packages/steamcmd/) for the command-line version of [Steam](https://developer.valvesoftware.com/wiki/SteamCMD).

### Alternative Flatpak installation

Steam can also be installed with [Flatpak](/index.php/Flatpak "Flatpak") as `com.valvesoftware.Steam` from [Flathub](https://flathub.org/). The easiest way to install it for the current user is by using the Flathub repo and flatpak command:

```
 flatpak --user remote-add --if-not-exists flathub [https://dl.flathub.org/repo/flathub.flatpakrepo](https://dl.flathub.org/repo/flathub.flatpakrepo)
 flatpak --user install flathub com.valvesoftware.Steam
 flatpak run com.valvesoftware.Steam

```

The Flatpak application currently does not support themes. Also you currently can't run games via `optirun`/`primusrun`, see [Issue#869](https://github.com/flatpak/flatpak/issues/869) for more details.

By default Steam won't be able to access your home directory, you can run the following command to allow it, so that it behaves like on Ubuntu or SteamOS:

```
flatpak override com.valvesoftware.Steam --filesystem=$HOME

```

#### Asian Font Problems with Flatpak

If you are having problem getting Asian fonts to show in game, it's because org.freedesktop.Platform does not include it. First try mounting your local font :

```
flatpak run --filesystems=~/.local/share/fonts --filesystem=~/.config/fontconfig  com.valvesoftware.Steam

```

If that doesn't work, consider this hack: make the fonts available by directly copying the font files into org.freedesktop.Platform's directories, e.g.

```
# replace ? with your version and hash
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/etc/fonts/conf.avail
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/etc/fonts/conf.d 
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/share/fonts

```

## Directory structure

The default Steam install location is `~/.local/share/Steam`. If Steam cannot find it, it will prompt you to reinstall it or select the new location. This article uses the `~/.steam/root` symlink to refer to the install location.

### Library folders

Every Steam application has a unique AppID, which you can find out by looking at its [Steam Store](http://store.steampowered.com/) page path.

Steam installs games into a directory under `*LIBRARY*/steamapps/common/`. `*LIBRARY*` normally is `~/.steam/root` but you can also have multiple library folders (*Steam > Settings > Downloads > Steam Library Folders*).

In order for Steam to recognize a game it needs to have an `appmanifest_*AppId*.acf` file in `*LIBRARY*/steamapps/`. The appmanifest file uses the [KeyValues](https://developer.valvesoftware.com/wiki/KeyValues) format and its `installdir` property determines the game directory name.

## Usage

```
steam [ -options ] [ steam:// URL ]

```

For the available command-line options see the [Command Line Options article on the Valve Developer Wiki](https://developer.valvesoftware.com/wiki/Command_Line_Options#Steam_.28Windows.29).

Steam also accepts an optional Steam URL, see the [Steam browser procotol](https://developer.valvesoftware.com/wiki/Steam_browser_protocol).

## Launch options

When you launch a Steam game, Steam executes its **launch command** in a [Bash](/index.php/Bash "Bash") shell. To let you alter the launch command Steam provides **launch options**, which can be set for a game by right-clicking on it in your library, selecting Properties and clicking on *Set Launch Options*.

By default Steam simply appends your option string to the launch command. To set environment variables or pass the launch command as an argument to another command you can use the `%command%` substitute.

### Examples

*   only arguments: `-foo`
*   environment variables: `FOO=bar BAZ=bar %command% -baz`
*   completely different command: `othercommand # %command%`

## Tips and tricks

### Fsync patch

Valve has [released](https://steamcommunity.com/app/221410/discussions/0/3158631000006906163/) a special kernel patch that should help increase FPS in massively-threaded applications. There are few methods to get and use this patch:

*   Use binary kernel provided directly from Valve. See [Unofficial user repositories#valveaur](/index.php/Unofficial_user_repositories#valveaur "Unofficial user repositories") and once you add this repository, kernel packages [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) and [linux-fsync-headers](https://aur.archlinux.org/packages/linux-fsync-headers/) become available. You will likely need to replace some regular packages (e.g. [nvidia](https://www.archlinux.org/packages/?name=nvidia)) with [DKMS](/index.php/DKMS "DKMS") packages (e.g. [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)) as well.
*   Install [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) kernel.

### Proton Steam-Play

Valve developed a compatibility tool for Steam Play based on Wine and additional components. It allows you to launch many Windows games (see [compatibility list](https://www.protondb.com/)).

It's open-source and available on [Github](https://github.com/ValveSoftware/Proton/). Steam will install its own versions of Proton when Steam Play is enabled.

Proton needs to be enabled on Steam client : `Steam > Settings > Steam Play`. You can enable Steam Play for games that have and have not been whitelisted by Valve in that dialog.

If needed, to force enable Proton or a specific version of Proton for a game, right click on the game, click `Properties > General > Force the use of a specific Steam Play compatibility tool`, and select the desired version. Doing so can also be used to force games that have a Linux port to use the Windows version.

You can also install Proton from AUR with [proton](https://aur.archlinux.org/packages/proton/) or [proton-git](https://aur.archlinux.org/packages/proton-git/), but extra setup is required for them to work with Steam. See the Proton Github for details on how Steam recognizes Proton installs.

### Big Picture Mode without a window manager

To start Steam in Big Picture Mode from a [Display manager](/index.php/Display_manager "Display manager"), you can either:

*   Install [steamos-compositor](https://aur.archlinux.org/packages/steamos-compositor/)
*   Alternatively, install [steamos-compositor-plus](https://aur.archlinux.org/packages/steamos-compositor-plus/), which hides the annoying color flashing on startup of Proton games and adds a fix for games that start in the background
*   Manually add a Steam entry (*but you lose the steam compositor advantages: mainly you **can't** control Big Picture mode with keyboard or gamepad*):

create a `/usr/share/xsessions/steam-big-picture.desktop` file with the following contents:

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

The Steam interface can be customized using skins. Skins can overwrite interface-specific files in `~/.steam/root`.

To install a skin:

1.  Place its directory in `~/.steam/root/skins`.
2.  Open *Steam > Settings > Interface* and select it.
3.  Restart Steam.

An extensive list of skins can be found in [this Steam forums post](http://forums.steampowered.com/forums/showthread.php?t=1161035).

**Note:** Using an outdated skin may cause visual errors.

#### Creating skins

Nearly all Steam styles are defined in `~/.steam/root/resource/styles/steam.styles` (the file is over 3,500 lines long). For a skin to be recognized it needs its own `resource/styles/steam.styles`. When a Steam update changes the official `steam.styles` your skin may become outdated, potentially resulting in visual errors.

See `~/.steam/root/skins/skins_readme.txt` for a primer on how to create skins.

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
$ cd ~/.steam/root/skins
$ mkdir -p Top-Right/resource
$ cp -r ~/.steam/root/resource/styles Top-Right/resource
$ sed -i '/Notifications.PanelPosition/ s/"[A-Za-z]*"/"TopRight"/' Top-Right/resource/styles/*

```

#### Live patching

`gameoverlay.styles` can be overwritten while Steam is running, allowing you to have game-specific notification positions.

 `~/.steam/notifpos.sh` 
```
sed -i "/Notifications.PanelPosition/ s/\"[A-Za-z]*\"/\"$1\"/" ~/.steam/root/resource/styles/gameoverlay.styles

```

And the [#Launch options](#Launch_options) should be something like:

```
~/.steam/notifpos.sh TopLeft && %command%

```

### Steam Remote Play

**Note:** Steam In-Home Streaming [has become Steam Remote Play](https://store.steampowered.com/news/51761/).

Steam has built-in support for [remote play](http://store.steampowered.com/streaming/).

See [this Steam Community guide](https://steamcommunity.com/sharedfiles/filedetails/?id=680514371) on how to setup a headless streaming server on Linux.

#### Different subnets

Steam client will not be able to detect host if both are on different subnets, which is common case when using VPN to your home network. Even if both client and server can ping each other - steam client would still not be able to detect host, so you need to force it. To do it, start Steam with below command:

```
$ steam -console

```

Wait until Steam starts. Once it loaded, you will find extra tab named "Console". Open it and then paste below command with correct host IP address:

```
connect_remote <host_ip>:27036

```

You will see notification that you can now stream games from host machine.

**Note:** If above doesn't work - Windows is likely blocking all incoming traffic from different subnets, which means any connections coming from VPN tunnel will be dropped. This also can be confirmed by simply performing ping requests without any response to Windows machine from your VPN client. To workaround this, configure (or disable) all Windows firewalls (including existing antiviruses).

**Tip:** See [Gaming#Remote gaming](/index.php/Gaming#Remote_gaming "Gaming") for alternatives if above solution does not work.

### Steam Controller

Normally a Steam controller requires the use of the Steam-overlay. In non-Steam native Linux games however the overlay may not be practical. For that, while the Steam client is running it will maintain a "desktop configuration". With your Steam controller, configure the desktop configuration for it as a generic XBOX controller. As long as the Steam client is running you can then use your Steam controller in other games, such as GOG games, as an XBOX controller. Make sure to select your type of controller to map to in "general controller settings".

## Troubleshooting

See [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting").

## See also

*   [Gentoo Wiki article](https://wiki.gentoo.org/wiki/Steam)
*   [The Big List of DRM-Free Games on Steam](https://pcgamingwiki.com/wiki/The_Big_List_of_DRM-Free_Games_on_Steam) at PCGamingWiki
*   [List of DRM-free games](http://steam.wikia.com/wiki/List_of_DRM-free_games) at Wikia
*   [Steam Linux store](http://store.steampowered.com/browse/linux)
*   [Proton](https://github.com/ValveSoftware/Proton/) Compatibility tool for Steam Play based on Wine and additional components.
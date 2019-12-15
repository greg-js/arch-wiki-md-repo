相关文章

*   [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")
*   [Gaming](/index.php/Gaming "Gaming")
*   [Gamepad](/index.php/Gamepad "Gamepad")
*   [List of games (简体中文)](/index.php/List_of_games_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of games (简体中文)")

[Steam](http://store.steampowered.com/about/) 是维尔福公司推出的著名游戏分发平台。

**注意:** 对于 Linux 平台，Steam 只支持 Ubuntu 的长期支持版本[[1]](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366)。 因此，请不要向维尔福公司提交 issue 以获得 Steam 对 Arch Linux 的支持。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 SteamCMD](#SteamCMD)
    *   [1.2 可选 Flatpak 安装](#可选_Flatpak_安装)
        *   [1.2.1 Flatpak 的亚洲字体问题](#Flatpak_的亚洲字体问题)
*   [2 目录结构](#目录结构)
    *   [2.1 库文件夹](#库文件夹)
*   [3 用法](#用法)
*   [4 启动选项](#启动选项)
    *   [4.1 实例](#实例)
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

## 安装

启用 [multilib](/index.php/Multilib "Multilib") 仓库并[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#安装软件包 "Help:Reading (简体中文)") [steam](https://www.archlinux.org/packages/?name=steam) 软件包。

你需要满足下列要求从而在 Arch Linux 上运行 Steam：

*   安装 32 位版本的 [OpenGL 图形驱动](/index.php/Xorg#Driver_installation "Xorg")。
*   生成 [en_US.UTF-8](/index.php/Locale#Generating_locales "Locale") 语言环境，以避免非法指针错误。
*   其图形界面大量使用 Arial 字体。详见 [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts") 。你可以通过安装 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 或使用 [Steam 支持的字体问题](/index.php/Steam/Troubleshooting#Text_is_corrupt_or_missing "Steam/Troubleshooting") 中的方法来解决。
*   安装 [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) 以支持亚洲地区语言。

### SteamCMD

安装 [steamcmd](https://aur.archlinux.org/packages/steamcmd/) 以使用命令行版本的 [Steam](https://developer.valvesoftware.com/wiki/SteamCMD)。

### 可选 Flatpak 安装

Steam 也可以作为 `com.valvesoftware.Steam` 使用 [Flatpak](/index.php/Flatpak "Flatpak") 从 [Flathub](https://flathub.org/) 中安装。使用 Flathub 仓库和 flatpak 命令行安装是目前最简单的安装方式：

```
 flatpak --user remote-add --if-not-exists flathub [https://dl.flathub.org/repo/flathub.flatpakrepo](https://dl.flathub.org/repo/flathub.flatpakrepo)
 flatpak --user install flathub com.valvesoftware.Steam
 flatpak run com.valvesoftware.Steam

```

目前 Flatpak 应用还不支持主题。并且你不能通过 `optirun`/`primusrun` 来运行游戏，更多细节详见 [Issue#869](https://github.com/flatpak/flatpak/issues/869)。

默认情况下 Steam 不会有访问你的家目录的权限，你可以运行下列命令来授予权限，以获得更类似于在 Ubuntu 或 SteamOS 下的运行效果：

```
flatpak override com.valvesoftware.Steam --filesystem=$HOME

```

#### Flatpak 的亚洲字体问题

如果你遇到了游戏中无法显示亚洲字体的问题，这是因为 org.freedesktop.Platform 并没有包含合适的字体文件进去。首先尝试挂载你的本地字体：

```
flatpak run --filesystems=~/.local/share/fonts --filesystem=~/.config/fontconfig  com.valvesoftware.Steam

```

如果上述命令不起作用，考虑动手 hack 一下：直接将字体文件复制进 org.freedesktop.Platform 的目录下以启用字体，例如

```
# replace ? with your version and hash
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/etc/fonts/conf.avail
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/etc/fonts/conf.d 
/var/lib/flatpak/runtime/org.freedesktop.Platform/x86_64/?/?/files/share/fonts

```

## 目录结构

Steam 的默认安装位置是 `~/.local/share/Steam`。如果 Steam 无法找到该目录，它会引导你重新安装或选择一个新的安装位置。这篇文章使用 `~/.steam/root` 符号链接来表示 Steam 的安装位置。

### 库文件夹

每一个 Steam 应用都有一个独一无二的应用 ID，你可以通过 [Steam Store](http://store.steampowered.com/) 页面路径来找到它。

Steam 将游戏安装到 `*LIBRARY*/steamapps/common/` 目录下。库文件夹 `*LIBRARY*` 一般会是 `~/.steam/root`，但是你依然可以选择拥有多个库文件夹如 (*Steam > Settings > Downloads > Steam Library Folders*)。

为了 Steam 能够正确识别游戏，它需要在 `*LIBRARY*/steamapps/` 目录下找到 `appmanifest_*AppId*.acf` 文件。此文件使用了 [KeyValues](https://developer.valvesoftware.com/wiki/KeyValues) 格式，并且它的 `installdir` 的内容决定了游戏的目录名称。

## 用法

```
steam [ -options ] [ steam:// URL ]

```

对于可用的命令行选择，详见 [Command Line Options article on the Valve Developer Wiki](https://developer.valvesoftware.com/wiki/Command_Line_Options#Steam_.28Windows.29)。

Steam 也可以接受可选的 Steam URL，详见 [Steam browser procotol](https://developer.valvesoftware.com/wiki/Steam_browser_protocol)。

## 启动选项

当你运行一个 Steam 游戏时，Steam 会使用 [Bash](/index.php/Bash "Bash") shell 执行它的 **启动命令**。 为了让你随意修改启动命令，Steam 提供了 **启动选项**。 **启动选项**可以通过右键点击你的游戏库中的游戏，选择属性后点击**设置启动选项**进行修改。

默认情况下 Steam 只是简单的把你设置的参数字符串添加到游戏的启动命令后。想要设置环境变量或者将一个启动命令作为参数传递给另一个命令，你可以使用 `%command%` 以表示原启动命令。

### 实例

*   仅设置参数： `-foo`
*   设置环境变量： `FOO=bar BAZ=bar %command% -baz`
*   设置与默认完全不同的命令： `othercommand # %command%`

## Tips and tricks

### Fsync patch

Valve has [released](https://steamcommunity.com/app/221410/discussions/0/3158631000006906163/) a special kernel patch that should help increase FPS in massively-threaded applications. There are few methods to get and use this patch:

*   Use binary kernel provided directly from Valve. See [Unofficial user repositories#valveaur](/index.php/Unofficial_user_repositories#valveaur "Unofficial user repositories") and once you add this repository, kernel packages [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) and [linux-fsync-headers](https://aur.archlinux.org/packages/linux-fsync-headers/) become available. You will likely need to replace some regular packages (e.g. [nvidia](https://www.archlinux.org/packages/?name=nvidia)) with [DKMS](/index.php/DKMS "DKMS") packages (e.g. [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)) as well.
*   Install [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) kernel.
*   Install [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel that includes the fsync patches since the 5.2 release[[2]](https://github.com/zen-kernel/zen-kernel/commit/f39367fdbc68e8b1e623239d13db6efaa5a67ae1)

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
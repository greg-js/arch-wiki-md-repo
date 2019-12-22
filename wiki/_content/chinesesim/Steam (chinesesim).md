相关文章

*   [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")
*   [Gaming](/index.php/Gaming "Gaming")
*   [Gamepad](/index.php/Gamepad "Gamepad")
*   [List of games (简体中文)](/index.php/List_of_games_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of games (简体中文)")

**翻译状态：** 本文是英文页面 [Steam](/index.php/Steam "Steam") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-12-17，点击[这里](https://wiki.archlinux.org/index.php?title=Steam&diff=0&oldid=591269)可以查看翻译后英文页面的改动。

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
*   [5 提示与技巧](#提示与技巧)
    *   [5.1 Fsync 补丁](#Fsync_补丁)
    *   [5.2 Proton Steam-Play](#Proton_Steam-Play)
    *   [5.3 无需窗口管理器的大屏幕模式](#无需窗口管理器的大屏幕模式)
    *   [5.4 Steam 皮肤](#Steam_皮肤)
        *   [5.4.1 自创皮肤](#自创皮肤)
    *   [5.5 改变 Steam 的通知位置](#改变_Steam_的通知位置)
        *   [5.5.1 使用一个皮肤](#使用一个皮肤)
        *   [5.5.2 实时更新](#实时更新)
    *   [5.6 Steam 远程同乐](#Steam_远程同乐)
        *   [5.6.1 不同子网](#不同子网)
    *   [5.7 Steam 控制器](#Steam_控制器)
*   [6 故障排除](#故障排除)
*   [7 另见](#另见)

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

## 提示与技巧

### Fsync 补丁

维尔福公司 [发布](https://steamcommunity.com/app/221410/discussions/0/3158631000006906163/) 了一个可以帮助提升大量多线程应用运行帧率的特殊内核补丁。这里有一些使用这个补丁的方法：

*   直接使用维尔福公司提供的二进制内核。详见 [Unofficial user repositories#valveaur](/index.php/Unofficial_user_repositories#valveaur "Unofficial user repositories") 并且一旦你添加了这个仓库，内核软件 [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) 和 [linux-fsync-headers](https://aur.archlinux.org/packages/linux-fsync-headers/) 便可使用。你将可能需要替换某些常用软件包 (例如 [nvidia](https://www.archlinux.org/packages/?name=nvidia)) 和 [DKMS](/index.php/DKMS "DKMS") 软件包 (例如 [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms))。
*   安装 [linux-fsync](https://aur.archlinux.org/packages/linux-fsync/) 内核。
*   安装 [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) 内核，其从 5.2 版本开始已包括 fsync 补丁。[[2]](https://github.com/zen-kernel/zen-kernel/commit/f39367fdbc68e8b1e623239d13db6efaa5a67ae1)

### Proton Steam-Play

维尔福公司开发了一个兼容性工具，用来使 Steam 可以在 Wine 和其他额外组件上运行。这使得你可以运行很多只能在 Windows 平台上运行的游戏 (详见 [compatibility list](https://www.protondb.com/))。

此工具开源并且可以从 [Github](https://github.com/ValveSoftware/Proton/) 获得。Steam 将在 Steam Play 启用后安装它相适应的 Proton 版本。

Proton 需要在 Steam 客户端启用： `Steam > 设置 > Steam Play`。你可以为了上述那些没有被维尔福公司列入白名单的游戏启用 Steam Play。

如果需要的话，为了在启动游戏时强制启用 Proton 或者指定一个确定的 Proton 版本，在游戏处右击，点击 `属性 > 常规 > 强制使用特定 Steam Play 兼容性工具`，然后选择所需版本。这样做同样可以用来强制游戏生成一个 Linux 入口用以运行 Windows 版本的游戏。

你同样可以从 AUR 通过安装 [proton](https://aur.archlinux.org/packages/proton/) 或 [proton-git](https://aur.archlinux.org/packages/proton-git/) 来安装 Proton，但是需要一些额外的配置才能使 Steam 良好运行。想要了解 Steam 如何识别已安装的 Proton 的更多细节，可以前往 Proton 的 Github 页面。

### 无需窗口管理器的大屏幕模式

想要从 [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") 运行 Steam 的大屏幕模式，你可以选择以下任意一个方案：

*   安装 [steamos-compositor](https://aur.archlinux.org/packages/steamos-compositor/)
*   或者，安装 [steamos-compositor-plus](https://aur.archlinux.org/packages/steamos-compositor-plus/)，这可以隐藏 Proton 游戏启动时恼人的颜色闪烁，并修复游戏在后台运行的问题。
*   手动添加一个 Steam 入口 (*但是你会失去 Steam 的混合平台优势：主要体现在你**不能**使用键盘或手柄控制大屏幕模式*):

创建一个 `/usr/share/xsessions/steam-big-picture.desktop` 文件，其中包含：

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

### Steam 皮肤

使用皮肤可以自定义 Steam 界面。皮肤可以被位于 `~/.steam/root` 的界面定义文件所覆盖。

想要安装一个皮肤：

1.  将皮肤的目录放于 `~/.steam/root/skins`。
2.  按照 *Steam > 设置 > 界面* 依次点击并选择该皮肤。
3.  重启 Steam。

你可以在 [Steam 论坛](http://forums.steampowered.com/forums/showthread.php?t=1161035) 获得比较完备的皮肤列表。

**注意:** 使用一个过期的皮肤可能会引起一些可视化错误。

#### 自创皮肤

几乎所有的 Steam 风格会定义在 `~/.steam/root/resource/styles/steam.styles` (此文件超过 3,500 行)。对于一个可以被 Steam 识别的皮肤，它需要自己的 `resource/styles/steam.styles` 文件。 当一个 Steam 的更新改变了官方的 `steam.styles` 文件，你的皮肤可能会过期，会有造成可视化错误的潜在风险。

详见 `~/.steam/root/skins/skins_readme.txt` 以获得如何创建皮肤的初步指引。

### 改变 Steam 的通知位置

默认情况下 Steam 的通知会在屏幕底端右侧出现。

你可以改变 Steam 通知出现的位置，通过更改 `Notifications.PanelPosition` 文件，具体位于

*   `resource/styles/steam.styles` 以调整桌面通知
*   `resource/styles/gameoverlay.styles` 以调整游戏中通知

以上两个文件都将在 Steam 启动时被覆写，且 `steam.styles` 只会在启动时被读取。

**注意:** 一些游戏并不遵守位于 `gameoverlay.styles` 里的设置。如《幽浮:未知敌人》。

#### 使用一个皮肤

你可以创建一个皮肤去将通知位置改变成你想要的那样。比如你想要将位置设置成顶部右侧：

```
$ cd ~/.steam/root/skins
$ mkdir -p Top-Right/resource
$ cp -r ~/.steam/root/resource/styles Top-Right/resource
$ sed -i '/Notifications.PanelPosition/ s/"[A-Za-z]*"/"TopRight"/' Top-Right/resource/styles/*

```

#### 实时更新

`gameoverlay.styles` 文件可以在 Steam 运行时更改，这允许你对不同游戏设置不同的通知位置。

 `~/.steam/notifpos.sh` 
```
sed -i "/Notifications.PanelPosition/ s/\"[A-Za-z]*\"/\"$1\"/" ~/.steam/root/resource/styles/gameoverlay.styles

```

由此 [#启动选项](#启动选项) 应该像下面这样：

```
~/.steam/notifpos.sh TopLeft && %command%

```

### Steam 远程同乐

**注意:** Steam 家庭流媒体 [已变为 Steam 远程同乐](https://store.steampowered.com/news/51761/)。

Steam 内置对于 [远程同乐](http://store.steampowered.com/streaming/) 的支持。

前往 [Steam 社区指南](https://steamcommunity.com/sharedfiles/filedetails/?id=680514371) 以了解如何在 Linux 上设置 headless 模式的流式服务器。

#### 不同子网

Steam 客户端如果处在不同的子网中，那么将不能检测到主机，这种情况常见于当你使用 VPN 去连接你的家庭网络时。就算服务端与服务器都可以互相 ping 通 —— Steam 客户端将仍然不会检测主机，因此你需要去强制检测。想要达到目标，你需要使用下面的命令启动 Steam：

```
$ steam -console

```

请耐心等待，直到 Steam 已经启动。一旦它加载完成，你会发现一个名为“控制台”的额外标签。打开它并将已替换为正确主机 IP 的下列命令粘贴上去：

```
connect_remote <host_ip>:27036

```

你将会看到通知说：你可以从主机来流式运行游戏了。

**注意:** 如果上述的命令不起作用 —— Windows 可能会屏蔽来自不同子网的所有流入流量，这意味着所有来自 VPN 管道的连接将会被丢弃。如果你向你的 VPN 客户端发出了 ping 的请求但没有任何的应答，那么就可以确定是上述的问题。要解决它，配置（或关闭）所有 Windows 防火墙（包括已经运行的杀毒软件）。

**提示：** 如果上述方案均不起作用，参见 [Gaming#Remote gaming](/index.php/Gaming#Remote_gaming "Gaming") 以查找其他方法。

### Steam 控制器

通常一个 Steam 控制器需要使用 Steam 界面。不过在非 Steam 的原生 Linux 游戏中这种界面并不很实用。对此，当 Steam 客户端运行时，其会保持一个“桌面配置”。如果你有 Steam 控制器，请在桌面配置中将其设置为通用 XBOX 控制器。只要 Steam 客户端在运行，你可以在其他游戏中使用 Steam 控制器，例如 GOG 的游戏， 就像一个 XBOX 控制器。确保已经选择了你的控制器类型以实现“常规控制器设置”的映射。

## 故障排除

参见 [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting").

## 另见

*   [Gentoo Wiki article](https://wiki.gentoo.org/wiki/Steam)
*   [The Big List of DRM-Free Games on Steam](https://pcgamingwiki.com/wiki/The_Big_List_of_DRM-Free_Games_on_Steam) 位于 PCGamingWiki
*   [List of DRM-free games](http://steam.wikia.com/wiki/List_of_DRM-free_games) 位于 Wikia
*   [Steam Linux store](http://store.steampowered.com/browse/linux)
*   [Proton](https://github.com/ValveSoftware/Proton/) 支持 Steam Play 运行的基于 Wine 以及其他额外组件的兼容性工具
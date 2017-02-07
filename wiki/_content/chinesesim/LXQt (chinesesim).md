**翻译状态：** 本文是英文页面 [LXQt](/index.php/LXQt "LXQt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-15，点击[这里](https://wiki.archlinux.org/index.php?title=LXQt&diff=0&oldid=446770)可以查看翻译后英文页面的改动。

2013年间，洪任諭（“PCMan”）启动了将 LXDE 移植到 Qt 的项目。LXDE-Qt 的首个预览版发布于2013年7月3日。而在2013年7月21日，Razor-qt（一个与LXDE类似的桌面）与 LXDE 宣布合并，产生了 LXQt。这个桌面集合了 Razor-qt 和 LXDE 的组件。尽管 LXDE 目前的精力已经集中到 LXQt，GTK+ 2 的版本依然在维护。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动桌面](#.E5.90.AF.E5.8A.A8.E6.A1.8C.E9.9D.A2)
    *   [2.1 使用 xinit](#.E4.BD.BF.E7.94.A8_xinit)
    *   [2.2 图形界面登入](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.99.BB.E5.85.A5)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 替换 Openbox](#.E6.9B.BF.E6.8D.A2_Openbox)
    *   [3.2 自动启动应用程序](#.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [3.3 设置环境变量](#.E8.AE.BE.E7.BD.AE.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
    *   [3.4 编辑应用程序菜单](#.E7.BC.96.E8.BE.91.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E8.8F.9C.E5.8D.95)
*   [4 建议应用](#.E5.BB.BA.E8.AE.AE.E5.BA.94.E7.94.A8)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Desktop icons are grouped together](#Desktop_icons_are_grouped_together)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/) 包组。 你还需要安装一个图标主题。 默认的是 *Oxygen*, 可以从 [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) 包安装。

你还可以安装以下附加功能包：

*   **[Connman](/index.php/Connman "Connman")** — 类似 [NetworkManager](/index.php/NetworkManager "NetworkManager") 的网络管理器。

	[http://git.kernel.org/cgit/network/connman](http://git.kernel.org/cgit/network/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **LXQt Connman applet** — LXQt [Connman](/index.php/Connman "Connman") 的系统托盘小程序。

	[https://github.com/surlykke/lxqt-connman-applet](https://github.com/surlykke/lxqt-connman-applet) || [lxqt-connman-applet-git](https://aur.archlinux.org/packages/lxqt-connman-applet-git/)

*   **LXImage-Qt** — LXQt 的图像查看器和截图工具。

	[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt)

*   **ObConf-Qt** — Qt 版 ObConf，[Openbox](/index.php/Openbox "Openbox") 的配置工具。

	[https://github.com/lxde/obconf-qt](https://github.com/lxde/obconf-qt) || [obconf-qt](https://www.archlinux.org/packages/?name=obconf-qt)

*   **QTerminal** — 基于 Qt 的轻量级终端模拟器。

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://www.archlinux.org/packages/?name=qterminal)

*   **[SDDM](/index.php/SDDM "SDDM")** — LXQt 推荐的显示管理器。

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — LXQt 的锁屏组件所需的屏幕保护程序。

	[https://www.jwz.org/xscreensaver/](https://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

某些 LXQt 面板插件的某些功能需要安装额外的包。可查阅 [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel) 的 [可选依赖](/index.php/PKGBUILD#optdepends "PKGBUILD")。

## 启动桌面

### 使用 xinit

在[Xinitrc](/index.php/Xinitrc "Xinitrc")中添加:

```
exec startlxqt

```

### 图形界面登入

在[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")的桌面菜单中选择 *LXQt Desktop*.

## 配置

LXQt 尝试提供 GUI 应用程序修改其设置。配置文件位于 `~/.config/lxqt` 目录中。这个目录被自动初始化，新用户的默认配置可在 `/etc/xdg/lxqt` 中找到。

### 替换 Openbox

虽然 [Openbox](/index.php/Openbox "Openbox") 是 LXQt 默认的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，你仍可以在“会话设置”（`lxqt-config-session`）中指定一个不同的窗口管理器用于 LXQt。也可以编辑 `~/.config/lxqt/session.conf`，将下面这行：

```
window_manager=openbox

```

改为你所选择的某个[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")：

```
window_manager=*你选择的窗口管理器*

```

### 自动启动应用程序

要在登录的时候启动 X 程序，在 LXQt 主菜单中依次点击 -> 首选项 -> LXQt 设置 -> LXQt 会话设置。此外也可以通过下面命令启动：

```
lxqt-config-session

```

从这个窗口中,点击左侧的"自动启动"，添加程序到全局自动启动（使用这个规范的所有会话都将启动此程序） 或本地自动启动（标签 LXQt 自动启动）（这个选项有个 Bug，见[issue 746](https://github.com/lxde/lxqt/issues/746)）。

`lxqt-config-session` 会在 `~/.config/autostart` 目录中为每个自启动项创建一个桌面配置项文件（.desktop）。登录时自启动的预安装应用位于 `/etc/xdg/autostart` 目录。所以你可以自己修改这些文件满足自己的配置需求。Besides, the distinction between "Global Autostart" and "LXQt Autostart" does not depend on the directory in which the corresponding .desktop-file is located, but rather on the `OnlyShowIn`-setting. If it is `OnlyShowIn=true`, it is considered an "LXQt Autostart". Furthermore, if `X-LXQt-Module=true`, the item is not shown in `lxqt-config-session`.

### 设置环境变量

LXQt 会话的环境变量在“会话设置”中定义。

例如：用 `SAL_USE_VCLPLUGIN=gtk` 可以强制 libreoffice 以 gtk2 启动。

### 编辑应用程序菜单

可以通过编辑`/usr/share/applications/lxqt-*.desktop`中的桌面文件修改菜单，参阅[桌面配置项](/index.php/Desktop_entries_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop entries (简体中文)")。

## 建议应用

LXQt是一个轻量级桌面，作为一个简单的安装不会提供很多桌面应用程序。它留给用户选择他们想要安装的应用程序。[Razor-qt wiki](https://github.com/Razor-qt/razor-qt/wiki/3rd-party-applications) 上有一个网页，其中列出了一些有用的 Qt 应用程序可按需选装。另请参阅[应用程序清单](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")页面中 Arch 可用应用程序的完整列表。

## Troubleshooting

### Desktop icons are grouped together

When moving icons on the desktop it is possible to place them a bit too close to each other making them connected. If unable to separate them Stop Desktop from Session Settings, remove `.config/pcmanfm-qt/lxqt/desktop-items-0.conf` and Start Desktop again.

## 参阅

*   [LXQt homepage](http://lxqt.org)
*   [LXQt development](https://github.com/lxde/lxqt)
*   [LXQt on deviantART](http://lxqt-de.deviantart.com/)
*   [LXQt wiki on GitHUb](https://github.com/lxde/lxqt/wiki)
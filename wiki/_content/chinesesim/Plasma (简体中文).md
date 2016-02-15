**翻译状态：** 本文是英文页面 [Plasma](/index.php/Plasma "Plasma") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-24，点击[这里](https://wiki.archlinux.org/index.php?title=Plasma&diff=0&oldid=374211)可以查看翻译后英文页面的改动。

Plasma是 [KDE](/index.php/KDE "KDE") 提供桌面(比如 wallpapers and panels)项目的一个组成部分，它使用[containments](https://techbase.kde.org/Projects/Plasma/Vocabulary#Containment)。containments能够包含其它 [plasmoids](https://techbase.kde.org/Projects/Plasma/Vocabulary#Plasmoid) 部件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动 Plasma](#.E5.90.AF.E5.8A.A8_Plasma)
    *   [2.1 使用 Display Manager](#.E4.BD.BF.E7.94.A8_Display_Manager)
    *   [2.2 使用 xinitrc](#.E4.BD.BF.E7.94.A8_xinitrc)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 主题](#.E4.B8.BB.E9.A2.98)
        *   [3.1.1 Qt 和 GTK+ 应用外观](#Qt_.E5.92.8C_GTK.2B_.E5.BA.94.E7.94.A8.E5.A4.96.E8.A7.82)
    *   [3.2 Plasmoids](#Plasmoids)
        *   [3.2.1 系统托盘图标](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98.E5.9B.BE.E6.A0.87)

## 安装

**注意:** Plasma 5 和 KDE 4 Workspace 冲突，安装前请先删除[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/).

从 [官方软件仓库](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Pacman "Pacman") [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 或 [plasma](https://www.archlinux.org/groups/x86_64/plasma/)。

## 启动 Plasma

可以使用 [Display manager](/index.php/Display_manager "Display manager") 或者 [xinitrc](/index.php/Xinitrc "Xinitrc") 去启动Plasma。

### 使用 Display Manager

**提示:** KDE 上游 [推荐](http://blog.davidedmundson.co.uk/blog/display_managers_finale)使用 [SDDM](/index.php/SDDM "SDDM") 显示管理器，因为它能够与 Plasma 5主题更好的整合。

在你的[display manager](/index.php/Display_manager "Display manager")菜单选择 Plasma 5 去启动它。

**注意:** 为了能够更好的整合 SDDM 和Plasma，推荐修改 `/etc/sddm.conf` 使用[plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 或者 [plasma](https://www.archlinux.org/groups/x86_64/plasma/)自动安装的微风（breeze）主题。 请参阅 [SDDM#Theme_settings](/index.php/SDDM#Theme_settings "SDDM") 的说明。

### 使用 xinitrc

_参阅 [xinitrc](/index.php/Xinitrc "Xinitrc") 页面获取更多信息。_

在你的 `.xinitrc` 文件中添加下面的内容：

 `~/.xinitrc` 

```
exec startkde

```

执行 _startx_ 或者 _xinit_ 启动 Plasma。

**注意:** 如果你想开机时启动 Xorg，请参阅 [Start X at login](/index.php/Start_X_at_login "Start X at login") article。

## 配置

[Plasma](/index.php/Plasma "Plasma") 是一个提供很多展示壁纸的功能集成化的桌面，它添加小插件到桌面,并处理面板(s), or "任务栏(s)"。

### 主题

[Plasma 主题](http://kde-look.org/index.php?xcontentmode=76)定义面板和 Plasma 看起来的样子。官方资料库和 [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go) 提供了很多主题，这样你就能够很简单的安装它。

通过桌面设置控制面板来安装主题是最简单的方法了：

```
 Workspace Theme > Desktop Theme > Get new Themes

```

如果你安装，卸载，或者简单的点击一下更新第三方 Plasma 脚本，这都将为 [kde-look.org](http://www.kde-look.org/) 呈现出一个更好的前端。

#### Qt 和 GTK+ 应用外观

**提示:** 为了 Qt 和 GTK 主题的一致性，请参见 [外观统一的 QT 和 GTK 应用](/index.php?title=%E5%A4%96%E8%A7%82%E7%BB%9F%E4%B8%80%E7%9A%84_QT_%E5%92%8C_GTK_%E5%BA%94%E7%94%A8&action=edit&redlink=1 "外观统一的 QT 和 GTK 应用 (page does not exist)")。

	Qt4

对于有一个一致的外观的Qt4应用程序，您需要安装[breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4)，然后从{ { IC | qtconfig - Qt4的} }中挑选微风作为图形用户界面风格。

	GTK+

目前 GTK 中没有 breeze-based 主题。在 GTK 中推荐外形美观的主题是[gtk-theme-orion](https://aur.archlinux.org/packages/gtk-theme-orion/)。安装然后在 System Settings / Application Style / GNOME Application Style 中选 Orion 作为 GTK2 and GTK3 主题。

### Plasmoids

在面板或桌面右击鼠标安装 plasmoid ，没错这是最简单的安装方法。

```
 Add Widgets > Get new Widgets > Download Widgets

```

这是作为 [kde-look.org](http://www.kde-look.org/) 的一个很好的前端，你只点击一次就可以选择安装，卸载或更新第三方 plasmoid 脚本。

你可以从 [kde-look.org](http://www.kde-look.org/index.php?xsortmode=new&logpage=0&xcontentmode=70x77x78&page=0) 上取得新的 plasmoids 组件。 AUR 中也有很多 plasmoids 组件, 包括 [kde-extragear-plasmoids](https://aur.archlinux.org/packages.php?ID=21084) 。 这个包是从 [kde-look.org](http://www.kde-look.org/index.php?xsortmode=new&logpage=0&xcontentmode=70x77x78&page=0) 获取流行的 plasmoid 并且将它们打成一个包。

#### 系统托盘图标

Plasma 5 在系统托盘区域使用一个叫做[状态通知](http://blog.martin-graesslin.com/blog/2014/03/system-tray-in-plasma-next/)的新显示规范。当然允许应用软件使用老的 xembed 显示规范， (GTK2) [libappindicator-gtk2](https://aur.archlinux.org/packages/libappindicator-gtk2/), (GTK3) [libappindicator-gtk3](https://aur.archlinux.org/packages/libappindicator-gtk3/), (Qt4) [sni-qt](https://www.archlinux.org/packages/?name=sni-qt), 或者 (For 32-bit Qt applications like Skype) [lib32-sni-qt](https://www.archlinux.org/packages/?name=lib32-sni-qt)是你需要的。可以参考["Where are my systray icons?"](http://blog.martin-graesslin.com/blog/2014/06/where-are-my-systray-icons/)获得更多信息。
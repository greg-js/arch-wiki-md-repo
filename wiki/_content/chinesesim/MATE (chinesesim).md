**MATE 桌面环境** 是 GNOME 2 的一个分支,旨在使用传统的方式，为Linux用户提供一个有吸引力的和直观的桌面. 更多信息, 请看 [this forum thread.](https://bbs.archlinux.org/viewtopic.php?id=121162)

## Contents

*   [1 获得](#.E8.8E.B7.E5.BE.97)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 GTK+ 3 版本](#GTK.2B_3_.E7.89.88.E6.9C.AC)
    *   [2.2 MATE 不稳定版本](#MATE_.E4.B8.8D.E7.A8.B3.E5.AE.9A.E7.89.88.E6.9C.AC)
*   [3 启动](#.E5.90.AF.E5.8A.A8)
    *   [3.1 图形方式](#.E5.9B.BE.E5.BD.A2.E6.96.B9.E5.BC.8F)
    *   [3.2 手动](#.E6.89.8B.E5.8A.A8)
*   [4 应用程序](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.1 核心应用程序](#.E6.A0.B8.E5.BF.83.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.2 扩展应用程序](#.E6.89.A9.E5.B1.95.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [5 Using Compiz Fusion sans Emerald](#Using_Compiz_Fusion_sans_Emerald)
*   [6 已知问题](#.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [6.1 Qt 应用程序不风格化](#Qt_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E4.B8.8D.E9.A3.8E.E6.A0.BC.E5.8C.96)
    *   [6.2 Evolution Email 不工作](#Evolution_Email_.E4.B8.8D.E5.B7.A5.E4.BD.9C)

## 获得

MATE 现在位于 [GitHub](https://github.com/mate-desktop):

*   基于发布版本编号的的稳定版：[http://repo.mate-desktop.org/archlinux/](http://repo.mate-desktop.org/archlinux/).

## 安装

要通过 [pacman](/index.php/Pacman "Pacman") 安装稳定版本的 MATE ， 添加下面几行到 `/etc/pacman.conf`:

```
[mate]
Server = http://packages.mate-desktop.org/repo/archlinux/$arch

```

运行

```
# pacman -Syy

```

然后

```
# pacman -S mate

```

一些人可能对从**mate-extra** 组 (大部分是 [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) 组里的包的副本)安装某些包感兴趣:

**Note:** 目前, MATE 的pacman 仓库里有两个扩展组: **mate-extra** 和 **mate-extras**. It is advised to look in both for the needed applications until it gets properly merged/fixed into a single extra group.

```
# pacman -S mate-extra

```

**或者**

```
# pacman -S mate-extras

```

You are very likely to get file conflicts when installing. Simply rename the offending files or install with the `--force` flag. You will also require [dbus](/index.php/Dbus "Dbus").

**Note:** Currently, many MATE packages do not provide, conflict or replace any GNOME packages.

### GTK+ 3 版本

An experimental GTK+ 3 build of MATE can be installed with [mate-gtk3](https://www.archlinux.org/groups/x86_64/mate-gtk3/) and [mate-extra-gtk3](https://www.archlinux.org/groups/x86_64/mate-extra-gtk3/) groups. While it works mostly, there are few known issues with [caja](https://github.com/mate-desktop/caja/milestones/Gtk+3), [eom](https://github.com/mate-desktop/eom/milestones/Gtk+3), [marco](https://github.com/mate-desktop/marco/milestones/Gtk+3), [mate-control-center](https://github.com/mate-desktop/mate-control-center/milestones/Gtk+3), [mate-netbook](https://github.com/mate-desktop/mate-netbook/milestones/Gtk+3), [mate-notification-daemon](https://github.com/mate-desktop/mate-notification-daemon/milestones/Gtk+3), [mate-panel](https://github.com/mate-desktop/mate-panel/milestones/Gtk+3) and [pluma](https://github.com/mate-desktop/pluma/milestones/Gtk+3).

### MATE 不稳定版本

Consider the following community efforts, cf. [forum](https://bbs.archlinux.org/viewtopic.php?pid=1624557#p1624557):

*   [mate-desktop-dev](https://aur.archlinux.org/packages/mate-desktop-dev/) ([https://github.com/nicman23/arch_mate](https://github.com/nicman23/arch_mate))

## 启动

### 图形方式

在 [显示管理器](/index.php/Display_manager "Display manager") 中选择 MATE 即可，推荐的显示管理器是 [LightDM](/index.php/LightDM "LightDM") 加 [lightdm-gtk2-greeter](https://aur.archlinux.org/packages/lightdm-gtk2-greeter/) 提供的 GTK+ (2) greeter。

### 手动

为了手动启动 MATE , 需要添加

```
exec mate-session

```

到你的 `[~/.xinitrc](/index.php/Xinitrc "Xinitrc")` 文件,然后运行

```
$ startx

```

**注意:** [xinitrc](/index.php/Xinitrc "Xinitrc")有详细介绍，例如保持 logind 会话等。

## 应用程序

### 核心应用程序

It is important to note that many GNOME core applications are rebranded for MATE, as per the licensing terms. Here is a simple Rosetta Stone of GNOME -> MATE applications.

*   Nautilus 重命名为 **caja**
*   Metacity 重命名为 **marco**
*   Gconf 重命名为 **mate-conf**

Other applications and core components prefixed with GNOME (such as GNOME Panel, GNOME Menus etc) have simply had the prefix renamed "MATE" and become MATE Panel and MATE Menus.

### 扩展应用程序

Not all of the GNOME extra applications (built for GTK2) have been forked yet. 下面的扩展应用程序在 MATE 中可用:

*   Totem (mate-video-player)
*   Eye of GNOME (mate-image-viewer)
*   Gedit (mate-text-editor)
*   File Roller (mate-file-archiver)
*   GNOME Panel applets (mate-applets)
*   GNOME Terminal (mate-terminal)

如果你使用 NetworkManager 连接互联网, 可以为 GTK2 nm-applet 从 AUR 安装 [network-manager-applet-gtk2](https://aur.archlinux.org/packages/network-manager-applet-gtk2/). You will need to modify the PKGBUILD to depend on mate-bluetooth rather than gnome-bluetooth to prevent a recursive dependency on gnome-desktop.

## Using Compiz Fusion sans Emerald

If you would like to use Marco with [Compiz Fusion](/index.php/Compiz_Fusion "Compiz Fusion"), install and start Compiz Fusion as you would normally and install the package *gtk-window-decorator* and run the following command to create a symlink:

```
# ln -s /usr/lib/libmarco-private.so.0 /usr/lib/libmetacity-private.so.0

```

Enable the Window Decoration plugin in the Compiz Fusion settings manager and use

```
gtk-window-decorator --replace

```

as the command. However, without recompiling gtk-window-decorator, the necessary mateconf keys will not be created and you will be stuck with Cairo based decorations. It may be possible to create these keys yourself.

## 已知问题

### Qt 应用程序不风格化

You may find that Qt4 applications are not inheriting the GTK2 theme like they should. This can be fixed easily by installing [libgnomeui](https://aur.archlinux.org/packages/libgnomeui/) with the `--force` flag. If the problem persists, run qtconfig and setting GTK+ as GUI style under System ⇒ Preferences ⇒ QT4 Settings.

### Evolution Email 不工作

请看 [Evolution#Using Evolution Outside Of Gnome](/index.php/Evolution#Using_Evolution_Outside_Of_Gnome "Evolution").
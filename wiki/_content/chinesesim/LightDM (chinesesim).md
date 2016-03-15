**翻译状态：** 本文是英文页面 [Lightdm](/index.php/Lightdm "Lightdm") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-09，点击[这里](https://wiki.archlinux.org/index.php?title=Lightdm&diff=0&oldid=364746)可以查看翻译后英文页面的改动。

[LightDM](http://www.freedesktop.org/wiki/Software/LightDM) 是一个跨桌面环境的[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")，其目的是为[X窗口系统](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")提供一个标准的显示管理器。它的特点有:

*   代码轻量
*   符合标准 (如 PAM, logind, 等)
*   为用户提供一个良好的界面。
*   跨桌面（用户可以使用各种各样的桌面环境）.

更多关于LightDM的特点可以在[这里](http://www.freedesktop.org/wiki/Software/LightDM/Design)找到。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Greeter](#Greeter)
*   [2 启用 LightDM](#.E5.90.AF.E7.94.A8_LightDM)
*   [3 命令行工具](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.B7.A5.E5.85.B7)
*   [4 测试](#.E6.B5.8B.E8.AF.95)
*   [5 配置和调整](#.E9.85.8D.E7.BD.AE.E5.92.8C.E8.B0.83.E6.95.B4)
    *   [5.1 更改背景图片/颜色](#.E6.9B.B4.E6.94.B9.E8.83.8C.E6.99.AF.E5.9B.BE.E7.89.87.2F.E9.A2.9C.E8.89.B2)
        *   [5.1.1 GTK+ greeter](#GTK.2B_greeter)
        *   [5.1.2 Unity greeter](#Unity_greeter)
        *   [5.1.3 KDE greeter](#KDE_greeter)
    *   [5.2 改变你的头像](#.E6.94.B9.E5.8F.98.E4.BD.A0.E7.9A.84.E5.A4.B4.E5.83.8F)
        *   [5.2.1 .face 方法](#.face_.E6.96.B9.E6.B3.95)
        *   [5.2.2 AccountsService 方法](#AccountsService_.E6.96.B9.E6.B3.95)
    *   [5.3 Arch 为中心的 64x64 图标来源](#Arch_.E4.B8.BA.E4.B8.AD.E5.BF.83.E7.9A.84_64x64_.E5.9B.BE.E6.A0.87.E6.9D.A5.E6.BA.90)
    *   [5.4 启用自动登录](#.E5.90.AF.E7.94.A8.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95)
    *   [5.5 隐藏系统和服务用户](#.E9.9A.90.E8.97.8F.E7.B3.BB.E7.BB.9F.E5.92.8C.E6.9C.8D.E5.8A.A1.E7.94.A8.E6.88.B7)
    *   [5.6 从 SLiM 迁移](#.E4.BB.8E_SLiM_.E8.BF.81.E7.A7.BB)
    *   [5.7 默认打开小键盘](#.E9.BB.98.E8.AE.A4.E6.89.93.E5.BC.80.E5.B0.8F.E9.94.AE.E7.9B.98)
    *   [5.8 Xfce4 下多用户切换](#Xfce4_.E4.B8.8B.E5.A4.9A.E7.94.A8.E6.88.B7.E5.88.87.E6.8D.A2)
    *   [5.9 默认会话](#.E9.BB.98.E8.AE.A4.E4.BC.9A.E8.AF.9D)
*   [6 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [6.1 显示错误语言环境](#.E6.98.BE.E7.A4.BA.E9.94.99.E8.AF.AF.E8.AF.AD.E8.A8.80.E7.8E.AF.E5.A2.83)
    *   [6.2 Xresources 未被正常解析](#Xresources_.E6.9C.AA.E8.A2.AB.E6.AD.A3.E5.B8.B8.E8.A7.A3.E6.9E.90)
    *   [6.3 使用 GTK greeter 丢失图标](#.E4.BD.BF.E7.94.A8_GTK_greeter_.E4.B8.A2.E5.A4.B1.E5.9B.BE.E6.A0.87)
    *   [6.4 更新 GTK greeter 到 2.0.0 后白屏](#.E6.9B.B4.E6.96.B0_GTK_greeter_.E5.88.B0_2.0.0_.E5.90.8E.E7.99.BD.E5.B1.8F)
    *   [6.5 LightDM 在登录提示符处冻结](#LightDM_.E5.9C.A8.E7.99.BB.E5.BD.95.E6.8F.90.E7.A4.BA.E7.AC.A6.E5.A4.84.E5.86.BB.E7.BB.93)
    *   [6.6 LigthDM 显示在错误的显示器上](#LigthDM_.E6.98.BE.E7.A4.BA.E5.9C.A8.E9.94.99.E8.AF.AF.E7.9A.84.E6.98.BE.E7.A4.BA.E5.99.A8.E4.B8.8A)
    *   [6.7 Pulseaudio 不自动启动](#Pulseaudio_.E4.B8.8D.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8)
*   [7 另见](#.E5.8F.A6.E8.A7.81)

## 安装

从官方软件仓库安装 [lightdm](https://www.archlinux.org/packages/?name=lightdm). 注意稳定版版本号是偶数的 (1.8, 1.10) 而开发版是奇数的 (1.9, 1.11). 开发版可以从 [AUR](/index.php/AUR "AUR") 安装 [lightdm-devel](https://aur.archlinux.org/packages/lightdm-devel/) 或者 [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/).

### Greeter

你需要安装一个 greeter (LightDM 的用户界面). 参考的 greeter 是 [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter). KDE 用户可以安装 [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter), 一个基于 Qt 的 greeter.

其他的 greeter 可以从 [AUR](/index.php/AUR "AUR") 安装:

*   [lightdm-another-gtk-greeter](https://aur.archlinux.org/packages/lightdm-another-gtk-greeter/): 一个支持自定义主题的 GTK3 greeter.
*   [lightdm-webkit-greeter](https://aur.archlinux.org/packages/lightdm-webkit-greeter/): 一个使用 Webkit 来主题化的 greeter.
*   [lightdm-crowd-greeter](https://aur.archlinux.org/packages/lightdm-crowd-greeter/): 一个让您在运动 3D 字符界面中选择配置文件的 greeter.
*   [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/): Ubuntu [Unity](/index.php/Unity "Unity") 使用的 greeter.
*   [lightdm-razor-greeter](https://aur.archlinux.org/packages/lightdm-razor-greeter/): 一个使用 [Razor-qt](/index.php/Razor-qt "Razor-qt") 桌面环境的 greeter.
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/): 一个来自 ElementaryOS Project 的 greeter.

你可以通过更改默认配置文件 `[SeatDefaults]` 部分下的内容来更改默认 greeter:

 `/etc/lightdm/lightdm.conf` 
```
[SeatDefaults]
...
greeter-session=lightdm-yourgreeter-greeter
```

## 启用 LightDM

确保[使用 systemctl](/index.php/Systemd#Using_units "Systemd") 启用 `lightdm.service`, 如此 LightDM 将会开机启动。

## 命令行工具

LightDM 提供一个命令行工具, `dm-tool`. 它可用来锁定当前 seat, 切换会话，等等。这对'极简'窗口管理器和测试非常有用。要列出可用命令，运行:

```
$ dm-tool --help

```

## 测试

首先，从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/Pacman "Pacman") [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr).

之后，把 LightDM 作为 X 程序启动:

```
$ lightdm --test-mode --debug

```

## 配置和调整

某些 greeter 拥有自己的配置文件。例如 [lightdm-gtk3-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk3-greeter) 有:

```
/etc/lightdm/lightdm-gtk-greeter.conf

```

[lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter) 有:

```
/etc/lightdm/lightdm-kde-greeter.conf

```

以及在 KDE 系统设置里的一个部分 (推荐).

可以直接修改 LightDM 的配置文件，或者使用位于 `/usr/lib/lightdm/lightdm/` 的 `lightdm-set-defaults`程序。想知道一些可用选项，执行:

```
$ man lightdm-set-defaults

```

然而一大部分变量要直接编辑配置文件而不是使用 `lightdm-set-defaults` 程序。

### 更改背景图片/颜色

如果您想使用一个纯色 (非图片) 的背景，只需将 `background` 变量设置为十六进制的颜色。

例如:

```
background=#000000

```

如果你想用图像来代替，请看下文。

#### GTK+ greeter

如果需要在 greeter 上使用自定义图片，请修改 `/etc/lightdm/lightdm-gtk-greeter.conf` 中的 `background` 变量值。

例如:

```
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg

```

#### Unity greeter

如果使用的是 [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)，请修改 `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml`，然后执行:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

可以参考[这个](https://bbs.archlinux.org/viewtopic.php?id=149945)页面。

**注意:** 最好将 PNG 或 JPG 文件放在 `/usr/share/pixmaps`，以便于 LightDM 读取。

#### KDE greeter

转到 *系统设置 > 登录界面 (LightDM)* 设置你的主题与背景图片。

### 改变你的头像

#### .face 方法

如果你想自定义 greeter 上的头像，需要把一张叫做 `.face` 或 `.face.icon` 的 PNG 图片放到家目录下。确保它可被 LightDM 读取。

**注意:** 自从2013年12月起，某些用户可能无法使得图片被拾取。更好的方法是安装 [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) 并使用下面的 AccountsService 方法。

#### AccountsService 方法

.face 方法会导致一些问题，幸运的是 LightDM 能够自动使用 AccountsService. 首先确保已安装 [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) 软件包，然后如下设置，把 `*username*` 替换为目标用户的登录名。使用 *.png* 文件插件必然就成了可选选项了。如果你使用 KDE, 你也可通过 KDE 系统设置更改图片。

*   编辑或创建 `/var/lib/AccountsService/users/*username*`, 添加如下内容:

```
[User]
Icon=/var/lib/AccountsService/icons/*username*.png

```

*   使用 96x96 PNG 图表文件来创建 `/var/lib/AccountsService/icons/*username*.png`.

**注意:** 确保创建的文件都是 644 权限，使用 [chmod](/index.php/Chmod "Chmod") 来更正。

### Arch 为中心的 64x64 图标来源

[AUR](/index.php/AUR "AUR") 的 [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) 软件包包含了一些不错的例子。它们被安装到 `/usr/share/archlinux/icons`, 可如下复制到 `/usr/share/icons/hicolor/64x64/devices`:

```
# find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

```

复制之后，可删除 [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/).

### 启用自动登录

编辑 LightDM 配置文件并确保以下内容已经取消注释并配置正确:

 `/etc/lightdm/lightdm.conf` 
```
[SeatDefaults]
pam-service=lightdm-autologin
autologin-user=*username*
autologin-user-timeout=0
session-wrapper=/etc/lightdm/Xsession
```

LightDM 能通过 PAM 即使 `autologin` 已启用。你必须是 `autologin` 组的成员来使得自己登录时不用输入密码:

```
# groupadd autologin
# gpasswd -a *username* autologin

```

**注意:** GNOME 用户, 更一般地 gnome-keyring 用户需要把他们的密码环设置一个空白密码以自动禁用。

### 隐藏系统和服务用户

为防止系统用户出现在登录界面，安装可选依赖 [accountsservice](https://www.archlinux.org/packages/?name=accountsservice), 或者把这些用户名添加到 `/etc/lightdm/users.conf` 下的 `hidden-users` 里。前者优势在于添加/删除用户时不用更新列表。

### 从 SLiM 迁移

把 [xinitrc](/index.php/Xinitrc "Xinitrc") 的内容搬到 [xprofile](/index.php/Xprofile "Xprofile"), 删除调用[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")或[桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")的部分。

### 默认打开小键盘

安装 [numlockx](https://www.archlinux.org/packages/?name=numlockx), 编辑 `/etc/lightdm/lightdm.conf` 添加以下几行:

```
greeter-setup-script=/usr/bin/numlockx on

```

### Xfce4 下多用户切换

如果您使用 [Xfce](/index.php/Xfce "Xfce") 桌面，在应用程序启动器/Whisker Menu 的活动按钮的多用户切换功能会特别关注 *gdmflexiserver* 可执行程序以启用自身。如果你提供了一个可执行 Shell 脚本 `/usr/bin/gdmflexiserver` 并且它包含

```
#!/bin/sh
/usr/bin/dm-tool switch-to-greeter

```

如此 Xfce 下多用户切换应该在 Lightdm 有效。

你也可从 [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") 锁屏界面切换用户 - 参见 [XScreenSaver#Lightdm](/index.php/XScreenSaver#Lightdm "XScreenSaver").

### 默认会话

Lightdm, 像其他 DM 一样，把上次选择的 xsession 存储在 `~/.dmrc`. 更多信息见 [Display manager#Session_list](/index.php/Display_manager#Session_list "Display manager").

## 疑难问题

如果你一直屏幕闪烁并且启动后没有 lightdm, 确保你已在 lightdm 的配置文件里正确设置了 greeter. 如果你正确设置了 GTK greeter, 确保 `xsessions-directory` (默认是: `/usr/share/xsessions`) 存在并且至少包含一个 .desktop 文件。

如果你上次选择的会话永久失效了，lightdm 启动时也可能有同样问题 (例如上次使用的是 gnome 并删除了 gnome-session 软件包): 最简单的解决方法就是恢复删掉的软件包。另一个可能的解决是:

```
# dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.Accounts /org/freedesktop/Accounts/User1000 org.freedesktop.Accounts.User.SetXSession string:xfce

```

此例为用户 1000 设置默认会话为 "xfce".

### 显示错误语言环境

如果 Lightdm 未正常显示你的语言环境，把你的语言环境添加到 `/etc/environment` (自己酌情更改)

```
 LANG=pt_PT.utf8

```

### Xresources 未被正常解析

当你的 [Xresources](/index.php/Xresources "Xresources") 文件未被预处理器加载时，会导致一个 LightDM 的上游 bug. 在实际中，这意味着使用 `#define` 设置的变量在之后调用时没有被扩展。如果你使用 urxvt 的自定义颜色时，这会表现为一个全粉色的屏幕。要修复，编辑 `/etc/lightdm/Xsession` 并搜索以下内容:

```
xrdb -nocpp -merge "$file"

```

更改为读取:

```
xrdb -merge "$file"

```

你的 Xresources 会正常加载并且变量会正常扩展。

### 使用 GTK greeter 丢失图标

如果你把 [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) 作为 greeter 并且它把占位符图像显示为图标，确保已安装和正确配置有效的图标主题和主题。检查如下文件:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
theme-name=mate      # this should be the name of a directory under /usr/share/themes/
icon-theme-name=mate # this should be the name of a fully featured icons set directory under /usr/share/icons/
```

### 更新 GTK greeter 到 2.0.0 后白屏

2.0.0 greeter 在某个特定配置下可能会只显示一个白屏。修复只能等待下一个版本，在此期间你可以设置 `/etc/lightdm/lightdm-gtk-greeter.conf` 的 `active-monitor=0` 把 "0" 改变为你真实的活动显示器。

参见 [FS#43999](https://bugs.archlinux.org/task/43999).

### LightDM 在登录提示符处冻结

你会发现当输入正确的用户名和密码尝试登录时 LightDM 冻结，你无法进入桌面。为修复，重新安装 [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) 软件包。参见 [这个](https://bbs.archlinux.org/viewtopic.php?id=179031)论坛帖子。

### LigthDM 显示在错误的显示器上

如果你使用的多显示器，LightDM 可能会显示在不该出现的那一个上 (例如: 主显示器在左边). 为强制 LightDM 登录界面显示在特定的显示器上，编辑 `/etc/lightdm/lightdm.conf` 更改 *display-setup-script* 参数如下:

 `/etc/lightdm/lightdm.conf`  `display-setup-script=xrandr --output *HDMI1* --primary` 

替换 *HDMI1* 为你的正确的显示器 ID, 可从 **xrandr** 命令输出获取。

### Pulseaudio 不自动启动

见 [PulseAudio#Running](/index.php/PulseAudio#Running "PulseAudio")。

## 另见

*   [light-locker](https://www.archlinux.org/packages/?name=light-locker), a screen locker using LightDM.
*   [Ubuntu Wiki article](https://wiki.ubuntu.com/LightDM)
*   [Gentoo Wiki article](http://wiki.gentoo.org/wiki/LightDM)
*   [Launchpad Page](https://launchpad.net/lightdm)
*   [LightDM blog](http://www.mattfischer.com/blog/?tag=lightdm)
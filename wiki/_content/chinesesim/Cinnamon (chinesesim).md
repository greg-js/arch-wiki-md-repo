**翻译状态：** 本文是英文页面 [Cinnamon](/index.php/Cinnamon "Cinnamon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-07，点击[这里](https://wiki.archlinux.org/index.php?title=Cinnamon&diff=0&oldid=339113)可以查看翻译后英文页面的改动。

[Cinnamon](http://cinnamon.linuxmint.com/) 是一个提供先进创新的特点和传统的用户体验的Linux桌面。桌面布局类似GNOME面板（GNOME 2）；然而，底层的技术又是基于GNOME Shell（GNOME 3）。给使用者提供了一个易于使用的和舒适的桌面体验。在Cinnamon 2.2版本中，Cinnamon已经是一个完整的桌面环境，不仅仅是一个GNOME的前端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动 Cinnamon](#.E5.90.AF.E5.8A.A8_Cinnamon)
    *   [2.1 图形化登录](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.99.BB.E5.BD.95)
    *   [2.2 手动启动Cinnamon](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8Cinnamon)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 Cinnamon系统设置](#Cinnamon.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE)
        *   [3.1.1 网络](#.E7.BD.91.E7.BB.9C)
        *   [3.1.2 蓝牙](#.E8.93.9D.E7.89.99)
    *   [3.2 应用程序和扩展](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E5.92.8C.E6.89.A9.E5.B1.95)
*   [4 小贴士](#.E5.B0.8F.E8.B4.B4.E5.A3.AB)
    *   [4.1 创建自定义应用程序/主题](#.E5.88.9B.E5.BB.BA.E8.87.AA.E5.AE.9A.E4.B9.89.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.2F.E4.B8.BB.E9.A2.98)
    *   [4.2 默认的桌面背景壁纸路径](#.E9.BB.98.E8.AE.A4.E7.9A.84.E6.A1.8C.E9.9D.A2.E8.83.8C.E6.99.AF.E5.A3.81.E7.BA.B8.E8.B7.AF.E5.BE.84)
    *   [4.3 添加“计算机”“主目录”“回收站”等常用图标与新的启动器](#.E6.B7.BB.E5.8A.A0.E2.80.9C.E8.AE.A1.E7.AE.97.E6.9C.BA.E2.80.9D.E2.80.9C.E4.B8.BB.E7.9B.AE.E5.BD.95.E2.80.9D.E2.80.9C.E5.9B.9E.E6.94.B6.E7.AB.99.E2.80.9D.E7.AD.89.E5.B8.B8.E7.94.A8.E5.9B.BE.E6.A0.87.E4.B8.8E.E6.96.B0.E7.9A.84.E5.90.AF.E5.8A.A8.E5.99.A8)
    *   [4.4 工作区](#.E5.B7.A5.E4.BD.9C.E5.8C.BA)
    *   [4.5 隐藏桌面图标](#.E9.9A.90.E8.97.8F.E6.A1.8C.E9.9D.A2.E5.9B.BE.E6.A0.87)
    *   [4.6 GTK主题和图标](#GTK.E4.B8.BB.E9.A2.98.E5.92.8C.E5.9B.BE.E6.A0.87)
    *   [4.7 调整窗口的大小](#.E8.B0.83.E6.95.B4.E7.AA.97.E5.8F.A3.E7.9A.84.E5.A4.A7.E5.B0.8F)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 qgtkstyle无法检测到当前主题](#qgtkstyle.E6.97.A0.E6.B3.95.E6.A3.80.E6.B5.8B.E5.88.B0.E5.BD.93.E5.89.8D.E4.B8.BB.E9.A2.98)
    *   [5.2 按下电源键时系统自动挂起](#.E6.8C.89.E4.B8.8B.E7.94.B5.E6.BA.90.E9.94.AE.E6.97.B6.E7.B3.BB.E7.BB.9F.E8.87.AA.E5.8A.A8.E6.8C.82.E8.B5.B7)
    *   [5.3 音量没有保存](#.E9.9F.B3.E9.87.8F.E6.B2.A1.E6.9C.89.E4.BF.9D.E5.AD.98)
    *   [5.4 cinnamon设置无法找到一个特定的模块](#cinnamon.E8.AE.BE.E7.BD.AE.E6.97.A0.E6.B3.95.E6.89.BE.E5.88.B0.E4.B8.80.E4.B8.AA.E7.89.B9.E5.AE.9A.E7.9A.84.E6.A8.A1.E5.9D.97)
    *   [5.5 无法添加/删除/修改Cinnamon语言](#.E6.97.A0.E6.B3.95.E6.B7.BB.E5.8A.A0.2F.E5.88.A0.E9.99.A4.2F.E4.BF.AE.E6.94.B9Cinnamon.E8.AF.AD.E8.A8.80)

## 安装

Cinnamon通过包 [cinnamon](https://www.archlinux.org/packages/?name=cinnamon) [安装](/index.php/%E5%AE%89%E8%A3%85 "安装").

## 启动 Cinnamon

### 图形化登录

在你喜欢的 [display manager](/index.php/Display_manager "Display manager") 选择 *Cinnamon* 或者是 *Cinnamon (Software Rendering)* 。Cinnamon选项是3D加速的版本，一般使用这个。如果你的显卡驱动出现问题，试试“'cinnamon（软件渲染）”，这个禁用了3D加速。

### 手动启动Cinnamon

如果你喜欢控制台启动Cinnamon, 添加以下行到 [Xinitrc](/index.php/Xinitrc "Xinitrc") (cinnamon 1.9 或更高版本):

 `~/.xinitrc` 
```
 exec cinnamon-session

```

如果你想用 *Cinnamon (Software Rendering)* , 用 `cinnamon-session-cinnamon2d` 代替 `cinnamon-session`.

## 配置

Cinnamon很容易配置，很多的配置正如大多数人所希望的那样可以在图形化界面下完成. 更多详情可查看以下网站[applets](http://cinnamon-spices.linuxmint.com/applets)/ [extensions](http://cinnamon-spices.linuxmint.com/extensions)/[theming](http://cinnamon-spices.linuxmint.com/themes).

### Cinnamon系统设置

启动*cinnamon系统设置* 、

```
$ cinnamon-settings

```

查看设置界面的模块：

```
$ pacman -Ql cinnamon | grep -o "cs_.*\.py" | awk -F'[_.]' '{ print $2 }'

```

打开其中的一个模块

```
$ cinnamon-settings 模块名称

```

示例：

```
$ cinnamon-settings panel

```

#### 网络

添加网络模块的支持, 请看 [Network Manager](/index.php/NetworkManager#Configuration "NetworkManager").

#### 蓝牙

Cinnamon的蓝牙前端可以在AUR中找到： [cinnamon-bluetooth](https://aur.archlinux.org/packages/cinnamon-bluetooth/).

### 应用程序和扩展

许多cinnamon的应用程序和扩展可以在 [AUR](/index.php/AUR "AUR"), ([package search](https://aur.archlinux.org/packages.php?O=0&K=cinnamon-&do_Search=Go))找到,也可以在Cinnamon的“小程序”和“拓展”中找到 (*在线获取更多*选项卡中):

```
$ cinnamon-settings applets
$ cinnamon-settings extensions

```

也可以从 [Cinnamon spices](http://cinnamon-spices.linuxmint.com/)下载并手动安装.

**Note:** 如果你安装后没有发现这些拓展或者是应用程序, 用 `Alt+F2` 并在对话框键入 `r` 重启 Cinnamon .

## 小贴士

### 创建自定义应用程序/主题

关于创建自定义应用程序/主题，可以在 [这里](http://cinnamon.linuxmint.com/?p=156)和[这里](http://cinnamon.linuxmint.com/?p=144).找到教程

### 默认的桌面背景壁纸路径

当你在Cinnamon设置自定义的路径的壁纸，, Cinnamon 会将其复制到 `~/.cinnamon/backgrounds`. 因此， 每一个改变你的壁纸，你都得再次在设置菜单添加你的墙纸到或将其复制到 `~/.cinnamon/backgrounds`.

### 添加“计算机”“主目录”“回收站”等常用图标与新的启动器

你可以在“设置”=>“桌面”添加部分常有图标，如“计算机”“主目录”“回收站”等。如要添加其它的启动器，右击桌面并选择“在此创建一个新的启动器”即可。

### 工作区

默认情况下，有2个工作区。增加，按Ctrl+ Alt +上键显示所有的工作区。然后点击右边的加号按钮在屏幕添加更多的工作区。

### 隐藏桌面图标

用下面的命令更改设置：

```
$ gsettings set org.nemo.desktop show-desktop-icons false

```

### GTK主题和图标

Linux Mint风格的主题和图标可以在AUR安装： [mint-themes](https://aur.archlinux.org/packages/mint-themes/) and [mint-x-icons](https://aur.archlinux.org/packages/mint-x-icons/). 可以在 `Settings → Themes → Other settings`编辑主题.

### 调整窗口的大小

用Alt+右键调整窗口的大小，使用gsettings：gsettings set org.cinnamon.desktop.wm.preferences resize-with-right-button true

## 故障排除

### qgtkstyle无法检测到当前主题

Installing [libgnome-data](https://www.archlinux.org/packages/?name=libgnome-data) solves the problem partially, and QGtkStyle will detect the current GTK+ theme. However, to set the same icon and cursor theme, users must specify them explicitly.

The icon theme for Qt apps can be configured by the following command:

```
$ gconftool-2 --set --type string /desktop/gnome/interface/icon_theme Faenza-Dark

```

This sets the icon theme to Faenza-Dark located in `/usr/share/icons/Faenza-Dark`.

The cursor theme for Qt apps can be selected by creating a symbolic link:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/Adwaita ~/.icons/default

```

This sets the cursor theme to Adwaita located in `/usr/share/icons/Adwaita`.

### 按下电源键时系统自动挂起

This is the default behaviour. To change the setting open the `cinnamon-settings` panel and click on the "Power Management" option. Change the "When the power button is pressed" option to your desired behaviour.

### 音量没有保存

The volume level is not be saved after reboot. The volume will be at 0 but not muted. Installing [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) will solve the problem.

### cinnamon设置无法找到一个特定的模块

If `cinnamon-settings` does not start with the message that it cannot find a certain module, e.g. the Image module, it is likely that it uses outdated compiled files which refer to no longer existing file locations. In this case remove all `*.pyc` files in `/usr/lib/cinnamon-settings` and its sub-folders.

### 无法添加/删除/修改Cinnamon语言

The language module was removed from the Cinnamon Control Panel with the release of Cinnamon 2.2 and provided a new package for changing the language settings.

**To add/remove languages**, see [Locale](/index.php/Locale "Locale").

**To change between enabled languages**, install the [mintlocale](https://aur.archlinux.org/packages/mintlocale/) package.
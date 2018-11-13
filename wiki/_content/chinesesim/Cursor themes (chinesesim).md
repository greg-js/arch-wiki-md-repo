**翻译状态：** 本文是英文页面 [Cursor_themes](/index.php/Cursor_themes "Cursor themes") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-01，点击[这里](https://wiki.archlinux.org/index.php?title=Cursor_themes&diff=0&oldid=347138)可以查看翻译后英文页面的改动。

图形显示服务器有一个“光标主题”以辅助浏览和操作。显示管理器提供了光标主题，此外还有很多主题可以自行安装和使用。

## Contents

*   [1 安装](#安装)
    *   [1.1 软件包](#软件包)
    *   [1.2 手动安装](#手动安装)
*   [2 配置](#配置)
    *   [2.1 LXAppearance](#LXAppearance)
    *   [2.2 XDG 规则](#XDG_规则)
    *   [2.3 桌面环境](#桌面环境)
        *   [2.3.1 GNOME](#GNOME)
    *   [2.4 X resources](#X_resources)
    *   [2.5 环境变量](#环境变量)
    *   [2.6 显示管理器](#显示管理器)
        *   [2.6.1 GDM](#GDM)
*   [3 问题处理](#问题处理)
    *   [3.1 创建需要的光标链接](#创建需要的光标链接)
    *   [3.2 Supplying missing cursors](#Supplying_missing_cursors)
        *   [3.2.1 rdesktop](#rdesktop)
    *   [3.3 Awesome 窗口管理器](#Awesome_窗口管理器)
*   [4 参阅](#参阅)

## 安装

### 软件包

*   [官方软件仓库](/index.php/Official_repositories "Official repositories") — ["xcursor-" 搜索](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR "AUR") — ["cursor" 搜索](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

### 手动安装

如果光标主题不在软件仓库或 AUR 中，可以手动进行安装. 下面这些网站提供了下载，下载后需要放到*icons* 目录：

*   [GNOME Look](http://gnome-look.org/index.php?xcontentmode=36)
*   [KDE Look](http://kde-look.org/index.php?xcontentmode=36)
*   [Customize.org](http://www.customize.org/list/xcursors)
*   [Deviant Art](http://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)

如果只为一个用户安装，就使用 `~/.icons/` 目录，主题目录格式是 `theme-name/cursors`, 大部分压缩包解压到这个目录即可使用：

```
$ bsdtar xvf foobar-cursor-theme.tar.gz --directory ~/.icons

```

**注意:** *系统级安装* 使用 `/usr/share/icons` 目录，不建议直接将文件放到这个目录。建议创建一个 [软件包](/index.php/PKGBUILD "PKGBUILD") 以便将文件放到 pacman 的数据库。

通过下面目录查看已经安装的光标主题：

```
find /usr/share/icons ~/.icons -type d -name "cursors"

```

如果软件包提供了 `index.theme` 文件，请查看是否包含 "Inherits" 行，如果有，需要确保依赖的主题已经安装到系统。

## 配置

### LXAppearance

See [LXDE#Cursors](/index.php/LXDE#Cursors "LXDE").

### XDG 规则

此方法同时适用于 [X11](/index.php/X11 "X11") 和 [Wayland](/index.php/Wayland "Wayland") 光标主题。

要编辑单个用户的设置，创建或编辑文件 `~/.icons/default/index.theme`. 要编辑系统配置，编辑 `/usr/share/icons/default/index.theme`; 此文件属于 [libxcursor](https://www.archlinux.org/packages/?name=libxcursor)，升级时可能会被替换。

在 `index.theme` 文件中，定义主题的目录：

```
[icon theme] 
Inherits=*theme-name*

```

重新登录生效.

### 桌面环境

[桌面环境](/index.php/Desktop_environments "Desktop environments") 使用 [XSETTINGS 协议](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html)，通常有一个守护进程。光标的修改可以立即生效，但是有些程序中可能显示的不一致。

#### GNOME

要在 [GNOME](/index.php/GNOME "GNOME") 中修改主题，可以使用 [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) 或通过下面命令直接修改：

```
gsettings set org.gnome.desktop.interface cursor-theme *theme-name*

```

### X resources

要给当前用户修改鼠标光标主题，之需要在 `~/.Xresources` 文件中添加以下这一行即可:

```
Xcursor.theme: cursor-theme

```

窗口管理器需要正确加载光标主题，如果有问题，可以在 `~/.xinitrc` 或 [.xprofile](/index.php/.xprofile ".xprofile") 加入下面命令(根据个人设置):

```
$ xrdb ~/.Xresources &

```

此外可以在 `~/.Xresources` 中设置需要的大小:

```
Xcursor.size:  16       !  32, 48 or 64 may also be good values

```

如果你不知道所用的鼠标光标支持的尺寸，可以不用添加这一行，直接启动X，他会自动选择的。

### 环境变量

可以通过 [环境变量](/index.php/Environment_variable "Environment variable") 修改主题，这样就可以临时测试主题：

```
$ XCURSOR_THEME=SomeThemeName xclock

```

### 显示管理器

显示管理器的光标主题可以单独设置，注意这里的设置不一定会用于登录的账号。

#### GDM

[GDM](/index.php/GDM "GDM") 不遵守 [GNOME](/index.php/GNOME "GNOME") 光标主题设置，也不遵照XDG 规则。要修改 GDM 光标主题，创建下面内容：

 `/etc/dconf/db/gdm.d/10-cursor-settings` 
```
[org/gnome/desktop/interface]
cursor-theme=*theme-name*
```

然后执行命令：

```
# dconf update

```

## 问题处理

### 创建需要的光标链接

如果主题中缺少文件，程序可能使用默认的主题，可以通过增加链接的方式解决：

```
$ cd ~/.icons/*theme*/cursors/
$ ln -s right_ptr arrow
$ ln -s cross crosshair
$ ln -s right_ptr draft_large
$ ln -s right_ptr draft_small
$ ln -s cross plus
$ ln -s left_ptr top_left_arrow
$ ln -s cross tcross
$ ln -s hand hand1
$ ln -s hand hand2
$ ln -s left_side left_tee
$ ln -s left_ptr ul_angle
$ ln -s left_ptr ur_angle
$ ln -s left_ptr_watch 08e8e1c95fe2fc01f976f1e063a24ccd

```

如果上面方法不起作用，请对比查看 `/usr/share/icons/whiteglass/cursors`，看看是否有缺少的主题。

也可以用这个方式删除不需要的文件， 例如删除 "watch" 光标：

```
$ cd ~/.icons/*theme*/cursors/
$ rm watch left_ptr_watch
$ ln -s left_ptr watch
$ ln -s left_ptr left_ptr_watch

```

### Supplying missing cursors

Some programs set their own custom cursors which you may want to override. A common example of this is rdesktop, which connects to a Microsoft Windows computer and uses the cursors obtained from the remote machine, which can often be difficult to see due to protocol limitations yielding poor conversion quality.

This can be resolved by replacing these cursors with ones from the same (or another) cursor theme. In order to do this, the **hash** of the image must be obtained. This is done by setting the `XCURSOR_DISCOVER` environment variable prior to launching the application that sets these cursors:

```
$ XCURSOR_DISCOVER=1 rdesktop ...

```

The first time (and only the first time) the cursor is set, some details will be displayed, like this:

```
Cursor image name: 24020000002800000528000084810000
...
Cursor image name: 7bf1cc07d310bf080118007e08fc30ff
...
Cursor hash 24020000002800000528000084810000 returns 0x0

```

When Xcursor looks for missing cursors, the search path includes `~/.icons/default/cursors` so this is where an image can be placed for Xcursor to find. First, create this directory if it doesn't already exist:

```
$ mkdir -p ~/.icons/default/cursors

```

Then link the hash to the target image. Here we are using the `left_ptr` image from the `Vanilla-DMZ` cursor theme:

```
$ ln -s /usr/share/icons/Vanilla-DMZ/cursors/left_ptr ~/.icons/default/cursors/24020000002800000528000084810000

```

The change will be visible as soon as the application is restarted. No special method of launching the application is required.

#### rdesktop

Here are some common Microsoft Windows cursors that rdesktop uses when connecting to a remote machine running Windows 7\. Unfortunately animated cursors are difficult to override as they are sent frame-by-frame, so one mapping will be needed for every frame!

```
$ ln -s /usr/share/icons/$THEME/cursors/00000000017e000002fc000000000000 ~/.icons/default/cursors/xterm
$ ln -s /usr/share/icons/$THEME/cursors/00000093000010860000631100006609 ~/.icons/default/cursors/right_ptr
$ ln -s /usr/share/icons/$THEME/cursors/01e00000201c00004038000080300000 ~/.icons/default/cursors/plus
$ ln -s /usr/share/icons/$THEME/cursors/24020000002800000528000084810000 ~/.icons/default/cursors/left_ptr
$ ln -s /usr/share/icons/$THEME/cursors/6ce0180090108e0005814700a0021400 ~/.icons/default/cursors/left_ptr_watch
$ ln -s /usr/share/icons/$THEME/cursors/d2201000a2c622004385440041308800 ~/.icons/default/cursors/hand
$ ln -s /usr/share/icons/$THEME/cursors/fc618c00da110f0034fd0e004e082400 ~/.icons/default/cursors/watch

```

### Awesome 窗口管理器

Xcursor 在 awesome 窗口管理器中不一定能正常工作。问题处理参考 [Awesome wiki](http://awesome.naquadah.org/wiki/FAQ#How_to_change_the_cursor_theme.3F).

## 参阅

*   [man Xcursor](http://www.x.org/releases/current/doc/man/man3/Xcursor.3.xhtml) — For more information about cursors in X (supported directories, formats, compatibility, etc.).
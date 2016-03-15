**翻译状态：** 本文是英文页面 [Tint2](/index.php/Tint2 "Tint2") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-09-07，点击[这里](https://wiki.archlinux.org/index.php?title=Tint2&diff=0&oldid=221864)可以查看翻译后英文页面的改动。

[Tint2](http://code.google.com/p/tint2/) 是一个 Linux 下的面板程序，被开发者称为“简洁轻量的面板/任务栏”。虽然不依赖什么软件包，它也可以配置成系统托盘、任务列表、电源监视器甚至时钟；外观配置也很简单。因此，对于默认的 WM 没有面板（比如 [Openbox](/index.php/Openbox "Openbox") ）的用户来说， Tinit2 是个不错的选择。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 tint2-svn(AUR)的面板启动程序](#tint2-svn.28AUR.29.E7.9A.84.E9.9D.A2.E6.9D.BF.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [2.2 OpenBox3的应用菜单](#OpenBox3.E7.9A.84.E5.BA.94.E7.94.A8.E8.8F.9C.E5.8D.95)
*   [3 运行tint2](#.E8.BF.90.E8.A1.8Ctint2)
    *   [3.1 Openbox](#Openbox)
    *   [3.2 Gnome 3](#Gnome_3)
*   [4 启用透明](#.E5.90.AF.E7.94.A8.E9.80.8F.E6.98.8E)

## 安装

tint2 可以通过[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包[tint2](https://www.archlinux.org/packages/?name=tint2)获得，软件包位于[官方软件仓库](/index.php/Official_repositories "Official repositories")。

## 配置

tint2 有个配置文件`~/.config/tint2/tint2rc`。一个结构化的具有默认设定的配置文件将在tint2第一次运行时被创建。你可以按你的偏好来修改这个文件。在[这里](http://code.google.com/p/tint2/wiki/Configure)能找到tint2的完整的配置文档。可以配置字体，颜色，外观，位置，以及配置文件中更多的其他条目。tint2包现在包含一个GUI的配置工具可以通过下列命令访问：

```
$ tint2conf

```

另外，你可以通过图形界面 tintwizard 编辑你的tint2rc配置文件。

### tint2-svn(AUR)的面板启动程序

在[AUR](/index.php/AUR "AUR")的[tint2-svn](https://aur.archlinux.org/packages/tint2-svn/)的版本中，tint2-svn已经可以在面板中添加启动项。你需要手动修改配置文件来实现这个功能，因为 tintwizard 不提供添加启动器支持。

**注意:** 当你手动修改添加启动器后又使用tintwizard来编辑你的tint2的配置文件，tintwizard将删除一切它无法识别的选项。比方说你的启动器。

把如下配置添加到你的tint2配置文件： 找到# `Panel:`

```
# Panel
panel_items = LTSBC

```

找到新的一节# `Launchers:`

```
# Launchers
launcher_icon_theme = LinuxLex-8
launcher_padding = 5 0 10
launcher_background_id = 9
launcher_icon_size = 85
launcher_item_app = /some/where/application.desktop
launcher_item_app = /some/where/anotherapplication.desktop

```

`launcher_icon_theme`似乎还没有相关描述。

`panel_items`是一个新的配置选项，它定义了tint2用下面的方式以便显示：

	L

	显示启动器

	T

	显示任务栏

	S

	显示系统托盘

	B

	显示电池状态

	C

	显示时钟

### OpenBox3的应用菜单

如果运行AUR里的[tint2-svn](https://aur.archlinux.org/packages/tint2-svn/)，你可以在tint2面板上创建程序启动器。然而tint2还不支持嵌套菜单，所以没法使用程序启动菜单。这有个小技巧，你可以从tint2上启动OpenBox3的右键菜单作为程序启动菜单。接下来介绍如何为OpenBox3创建这样一个菜单。 首先，你需要安装[openbox](https://www.archlinux.org/packages/?name=openbox)，[tint2-svn](https://aur.archlinux.org/packages/tint2-svn/)和[xdotool](https://www.archlinux.org/packages/?name=xdotool)。然后，为Openbox的右键菜单创建一个键绑定。在`~/.config/openbox/rc.xml`的<keyboard>和</keyboard>之间添加下列代码:

```
 <keybind key="C-A-space">
   <action name="ShowMenu"><menu>root-menu</menu></action>
 </keybind>

```

这就设置了启动OpenBox右键菜单的快捷键`Ctrl+Alt+Space`。测试快捷键是否生效：

```
$ xdotool key ctrl+alt+space

```

如果右键菜单顺利弹出，说明生效了。现在，在`/usr/share/applications/`目录下创建一个`tint2.desktop`文件。把这行添加到文件里`Exec=xdotool key ctrl+alt+space`。然后从文件管理器重新打开你的新的`tint2.desktop`文件，你将看到右键菜单弹出。最后，将这个文件作为启动器添加到tint2。这样就得到了tint2上的程序启动菜单。

更多的帮助请参考[Openbox Menus](http://openbox.org/wiki/Help:Menus)来创建你的个性菜单，menumaker可以为大多数（几乎所有）你安装的程序生成一个完满的menu.xml文件。

## 运行tint2

### Openbox

你可以简单的通过这条命令运行tint2:

```
$ tint2

```

如果你想在[X](/index.php/X "X")启动时启动tint2，添加这下列到~/.xinitrc。例如配合[openbox](/index.php/Openbox "Openbox")运行tint2:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
**tint2 &**
exec openbox-session

```

如果你想在[Openbox](/index.php/Openbox "Openbox")启动的时候启动tint2，修改~/.config/openbox/autostart添加如下:

```
tint2 &

```

注意：如果在~/.config/openbox没有autostart文件，你可以从/etc/xdg/openbox/autostart复制一份。

OpenBox autostart选项的更多信息参见[Openbox help](http://openbox.org/wiki/Help:Autostart)。

### Gnome 3

Gnome 3中，底部面板和任务栏被Activities视图所替代。要在原底部面板位置使用tint2，运行

```
# gnome-session-properties

```

并添加

```
# /usr/bin/tint2

```

使tint2作为gnome3启动时运行的程序。gnome下次启动时，tint2将自动运行。

## 启用透明

你需要些compositing效果来实现tint2的最佳视觉效果。如果你的tint2的周围出现巨大的黑死的矩形盒子而你使用的窗口管理器(比如Openbox)又没有内置的 compositing效果，或是compositing未启用。

为在OpenBox下启用composting你可以安装[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")或者[Cairo Compmgr](/index.php/Cairo_Compmgr "Cairo Compmgr"), 对应的软件包分别是：[xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) 和 [cairo-compmgr](https://aur.archlinux.org/packages/cairo-compmgr/).

Xcompmgr 可以通过这样启动:

```
$ xcompmgr

```

你必须关闭并重启tint2来启用透明。

如果Xcompmgr被单独用来为tint2提供透明效果，通过像这样修改`~/.config/openbox/autostart`里autostart的段落来让它在系统启动时运行：

```
# Launch Xcomppmgr and tint2 with openbox
if which tint2 >/dev/null 2>&1; then
  (sleep 2 && xcompmgr) &
  (sleep 2 && tint2) &
fi

```

各种其他的（更好的）让Xcompmgr在启动时运行的办法在这篇[Openbox](/index.php/Openbox "Openbox")文章里有所讨论。
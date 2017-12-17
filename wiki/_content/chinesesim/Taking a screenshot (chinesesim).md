## Contents

*   [1 import](#import)
*   [2 scrot](#scrot)
    *   [2.1 安装](#.E5.AE.89.E8.A3.85)
    *   [2.2 一般用法](#.E4.B8.80.E8.88.AC.E7.94.A8.E6.B3.95)
    *   [2.3 高级用法](#.E9.AB.98.E7.BA.A7.E7.94.A8.E6.B3.95)
*   [3 GIMP](#GIMP)
*   [4 xwd](#xwd)
*   [5 KDE](#KDE)
*   [6 GNOME](#GNOME)

## import

一个很简单的抓取当前系统屏幕截图的方法就是使用 import 命令：

```
import -window root screenshot.jpg

```

import 命令包含在 imagemagick 软件包内。

如果你的是多屏和双头显示，只要截两次屏，然后用imagemagick把它们粘贴在一起：

```
import -window root -display :0.0 -screen /tmp/0.png
import -window root -display :0.1 -screen /tmp/1.png
convert +append /tmp/0.png /tmp/1.png screenshot.png
rm /tmp/{0,1}.png

```

## scrot

**注意:** 根据 [这个帖子](http://comments.gmane.org/gmane.comp.misc.suckless/6901), [scrot](https://www.archlinux.org/packages/?name=scrot)无法与[dwm](https://aur.archlinux.org/packages/dwm/)或[xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys)一起工作.

**注意：本节 scrot 内容来自[Linuxtoy](http://linuxtoy.org/)上的[scrot从入门到精通](http://linuxtoy.org/archives/mastering-scrot.html)一文，为了适应 Arch Linux 的使用环境和 Wiki 版面要求，对其部分内容和格式重新做了编排。**

[scrot](http://linuxbrit.co.uk/scrot/)是屏幕抓图工具中的佼佼者，它小巧而不失为强大，精练而不缺少灵活。scrot 主要用在命令行下，它使用 imlib2 来抓取并保存图像。

### 安装

使用以下命令安装：

```
pacman -S scrot

```

### 一般用法

scrot 的使用格式为：

```
scrot [options] [file]

```

它可以抓取整个桌面、某个指定的窗口、以及选择的矩形区域。

*   抓取桌面：

```
scrot desktop.png

```

该命令将当前的整个桌面抓取下来，并保存为 desktop.png 文件。可以在当前的目录中找到此图像文件。

*   抓取窗口：

```
scrot -bs window.png

```

选项 b 使 scrot 在抓取窗口时一同将外边框抓取下来，而 s 选项则让用户选择所要抓取的是何窗口。

*   抓取区域：

```
scrot -s rectangle.png

```

在执行此命令后，使用鼠标拖曳的矩形区域将被 scrot 抓取下来。

### 高级用法

对于普通的抓取使用 scrot 的基础便足以应付了。但在某些特殊情况之下，使用 scrot 抓取图像需要讲究一些技巧。

*   延时抓取：

```
scrot -cd 10 menu.png

```

此命令中的 d 选项用于延时抓取图像，其后的 10 代表延时 10 秒；前面的选项 c 显示倒计时。在抓取菜单或是命令提示时，该技巧将充分展示其魔力。

*   生成缩图：

```
scrot -t 50% thumb.png

```

这个命令在抓取图像的同时生成该图像的缩略图。选项 t 将打开此功能，其后的 50% 为原图的缩放百分比。

*   更改品质：

```
scrot -q 70 quality.jpg

```

此命令中的 q 选项用于更改所抓图像的品质，其数值介于 1-100 之间，默认为 75。数值越大，意味着图像品质越高；同时，图像的压缩率也就越低，占用空间越大。

*   操作抓图：

```
scrot action.png -e 'mv $f ~/images/'

```

该命令将抓取的图像移动到 ~/images/ 目录。显然，操作图像的功能由 e 选项开启，其中的 $f 代表原图的路径／文件名。

以上示例皆指定了需要保存的抓图的文件名称。实际上，如果不指定名称，那么 scrot 在抓取图像后会自动使用当前的日期时间、宽度高度的组合来生成文件名称。

## GIMP

你也可以用gimp来截图(文件 -> 获取 -> 屏幕截图 ...)。

## xwd

xwd是xorg-apps软件包的一部分。

对root window进行屏幕截图：

```
xwd -root -out screenshot.xwd

```

## KDE

如果你用KDE，可以使用[spectacle](https://www.archlinux.org/packages/?name=spectacle)。

## GNOME

你可以按<Prt Scr>或者Apps->Accessories->Take Screenshot。

*注意：如果<Prt Scr>提示找不到gnome-screenshot或者没有你的菜单项里没有“Take Screenshot”，那表示你需要安装[gnome-utils](https://www.archlinux.org/packages/?name=gnome-utils)软件包。*
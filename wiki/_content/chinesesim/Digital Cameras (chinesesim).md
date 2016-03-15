**翻译状态：** 本文是英文页面 [Digital_Cameras](/index.php/Digital_Cameras "Digital Cameras") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-05-28，点击[这里](https://wiki.archlinux.org/index.php?title=Digital_Cameras&diff=0&oldid=317217)可以查看翻译后英文页面的改动。

本文阐述如何配置`libgphoto2`，以便访问数码相机。某些数码相机可以直接按U盘模式挂载，无需libghoto2。

## Contents

*   [1 libgphoto2](#libgphoto2)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.2 GPhoto2用法](#GPhoto2.E7.94.A8.E6.B3.95)
        *   [1.2.1 其它前端程序](#.E5.85.B6.E5.AE.83.E5.89.8D.E7.AB.AF.E7.A8.8B.E5.BA.8F)
*   [2 排除故障](#.E6.8E.92.E9.99.A4.E6.95.85.E9.9A.9C)
    *   [2.1 组](#.E7.BB.84)

## libgphoto2

[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/)是实现访问数码相机的核心库，它为Digikam、gphoto2等应用程序提供接口。当前版本的官方支持列表在[这里](http://www.gphoto.org/proj/libgphoto2/support.php)。这份列表比较保守，某些相机其实也能工作。

### 安装

用户可以直接从[官方软件源](/index.php/Official_repositories "Official repositories")[安装](/index.php/Pacman "Pacman")[libgphoto2](https://www.archlinux.org/packages/?name=libgphoto2)。可选的包还有[gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2)以及[gphoto2](https://www.archlinux.org/packages/?name=gphoto2)。前者提供了Nautilus整合功能，后者提供了命令行界面。

### GPhoto2用法

GPhoto2是libgphoto2的命令行版客户端，它可以让用户从终端或者脚本中访问libgphoto2，从而操作数码相机。另外，GPhoto2也为驱动开发者提供了方便的调试功能。

**常用操作**

*   `gphoto2 --list-ports`
*   `gphoto2 --auto-detect`
*   `gphoto2 --summary`
*   `gphoto2 --list-files`
*   `gphoto2 --get-all-files`

更高级的文件操作

*   `gphoto2 --shell`

#### 其它前端程序

*   [gphotofs](http://www.gphoto.org/proj/gphotofs/)
*   [darktable](http://darktable.org/)
*   [Digikam](/index.php/Digikam "Digikam")
*   [F-Spot](http://f-spot.org/)
*   [Gthumb](http://live.gnome.org/gthumb)
*   [GTKam](http://www.gphoto.org/proj/gtkam/)

## 排除故障

### 组

v2.14.13以前的版本，用户需要加入camera组，以后的版本改为[storage group](/index.php/Users_and_groups#Groups "Users and groups")。
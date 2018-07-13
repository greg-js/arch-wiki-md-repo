Related articles

*   [Jalbum](/index.php/Jalbum "Jalbum")

**翻译状态：** 本文是英文页面 [Libgphoto2](/index.php/Libgphoto2 "Libgphoto2") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-13，点击[这里](https://wiki.archlinux.org/index.php?title=Libgphoto2&diff=0&oldid=529363)可以查看翻译后英文页面的改动。

[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/)是实现访问数码相机的核心库，它为Digikam、gphoto2等应用程序提供接口。当前版本的官方支持列表在[这里](http://www.gphoto.org/proj/libgphoto2/support.php)。这份列表比较保守，某些相机其实也能工作。

本文阐述如何配置`libgphoto2`，以便访问数码相机。某些数码相机可以直接按[U盘模式](/index.php/USB_storage_devices "USB storage devices")挂载，无需libghoto2。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 前端程序](#.E5.89.8D.E7.AB.AF.E7.A8.8B.E5.BA.8F)
*   [2 GPhoto2用法](#GPhoto2.E7.94.A8.E6.B3.95)
    *   [2.1 使用 gvfs](#.E4.BD.BF.E7.94.A8_gvfs)
*   [3 权限问题](#.E6.9D.83.E9.99.90.E9.97.AE.E9.A2.98)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Pacman "Pacman") 软件包 [libgphoto2](https://www.archlinux.org/packages/?name=libgphoto2)。可选的包还有 [gphoto2](https://www.archlinux.org/packages/?name=gphoto2)，提供了命令行界面。

### 前端程序

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Utility to organize and develop raw images.

	[http://darktable.org/](http://darktable.org/) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **[digiKam](/index.php/Digikam "Digikam")** — Digital photo management application for [KDE](/index.php/KDE "KDE").

	[https://www.digikam.org/](https://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **Entangle** — Provides a graphical interface for “tethered shooting”, aka taking photographs with a digital camera completely controlled from the computer.

	[https://entangle-photo.org/](https://entangle-photo.org/) || [entangle](https://aur.archlinux.org/packages/entangle/)

*   **gphotofs** — [Fuse](/index.php/Fuse "Fuse") module to mount camera as a filesystem.

	[http://www.gphoto.org/proj/gphotofs/](http://www.gphoto.org/proj/gphotofs/) || [gphotofs](https://aur.archlinux.org/packages/gphotofs/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image browser and viewer for [GNOME](/index.php/GNOME "GNOME").

	[http://wiki.gnome.org/gthumb](http://wiki.gnome.org/gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **GTKam** — Graphical [GTK+](/index.php/GTK%2B "GTK+") 2 front-end to gphoto2.

	[http://www.gphoto.org/proj/gtkam/](http://www.gphoto.org/proj/gtkam/) || [gtkam](https://aur.archlinux.org/packages/gtkam/)

*   **gvfs-gphoto2** — gphoto2 backend for GVfs to mount camera as a filesystem from a file manager that supports GVfs such as [GNOME Files](/index.php/GNOME_Files "GNOME Files"), [Nemo](/index.php/Nemo "Nemo"), [PCManFM](/index.php/PCManFM "PCManFM") and [Thunar](/index.php/Thunar "Thunar").

	[https://wiki.gnome.org/Projects/gvfs](https://wiki.gnome.org/Projects/gvfs) || [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2)

*   **Kamera** — [KDE](/index.php/KDE "KDE") integration for gphoto2 cameras.

	[https://github.com/KDE/kamera](https://github.com/KDE/kamera) || [kamera](https://www.archlinux.org/packages/?name=kamera)

*   **Pantheon Photos** — Image viewer for Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **[Rawstudio](https://en.wikipedia.org/wiki/Rawstudio "wikipedia:Rawstudio")** — An open source raw-image converter written in GTK+. Supports tethered shooting with gphoto2.

	[https://rawstudio.org/](https://rawstudio.org/) || [rawstudio](https://aur.archlinux.org/packages/rawstudio/)

*   **[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")** — Digital photo organizer designed for [GNOME](/index.php/GNOME "GNOME").

	[http://wiki.gnome.org/Apps/Shotwell](http://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

## GPhoto2用法

GPhoto2是libgphoto2的命令行版客户端，它可以让用户从终端或者脚本中访问libgphoto2，从而操作数码相机。另外，GPhoto2也为驱动开发者提供了方便的调试功能。

**常用操作**

*   `gphoto2 --list-ports`
*   `gphoto2 --auto-detect`
*   `gphoto2 --summary`
*   `gphoto2 --list-files`
*   `gphoto2 --get-all-files`

更高级的文件操作

*   `gphoto2 --shell`

### 使用 gvfs

用下面命令检测连接的摄像头和端口:

```
$ gphoto2 --auto-detect
Model                          Port                                            
----------------------------------------------------------
Canon Digital IXUS 980 IS      usb:006,011 

```

在文件管理器中使用下面地址进行访问: "gphoto2://[usb:006,011]" - 摄像头会被 gvfs 挂载并通过文件管理器进行管理。

## 权限问题

有本地会话的用户会通过 [ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list") 获得摄像头权限，有问题请查看 [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")。

## 参阅

*   [gPhoto 支持的摄像头列表](http://www.gphoto.org/proj/libgphoto2/support.php)
*   [更详细的列表](http://www.teaser.fr/~hfiguiere/linux/digicam.html)
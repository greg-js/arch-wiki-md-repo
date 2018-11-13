Related articles

*   [PCManFM](/index.php/PCManFM "PCManFM")
*   [Thunar](/index.php/Thunar "Thunar")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Udisks](/index.php/Udisks "Udisks")

**翻译状态：** 本文是英文页面 [File_manager_functionality](/index.php/File_manager_functionality "File manager functionality") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-04-06，点击[这里](https://wiki.archlinux.org/index.php?title=File_manager_functionality&diff=0&oldid=363455)可以查看翻译后英文页面的改动。

本文介绍扩展文件管理器功能的相关软件，特别是使用窗口管理器如[Openbox](/index.php/Openbox "Openbox")的时候。还提供了在没有密码的情况下访问分区和可移动媒体的能力（如果受到影响）。

## Contents

*   [1 概要](#概要)
*   [2 附加功能](#附加功能)
    *   [2.1 挂载](#挂载)
        *   [2.1.1 文件管理守护程序](#文件管理守护程序)
        *   [2.1.2 独立](#独立)
    *   [2.2 网络](#网络)
        *   [2.2.1 Windows 访问](#Windows_访问)
        *   [2.2.2 Apple 访问](#Apple_访问)
    *   [2.3 缩略图预览](#缩略图预览)
        *   [2.3.1 Dolphin 和 Konqueror 以外的文件管理器](#Dolphin_和_Konqueror_以外的文件管理器)
        *   [2.3.2 Dolphin and Konqueror (KDE)](#Dolphin_and_Konqueror_(KDE))
    *   [2.4 解压文件](#解压文件)
    *   [2.5 NTFS 读/写 支持](#NTFS_读/写_支持)
    *   [2.6 桌面通知](#桌面通知)
    *   [2.7 在不同的文件系统上开启回收站功能 (外部驱动器)](#在不同的文件系统上开启回收站功能_(外部驱动器))
*   [3 故障排除](#故障排除)
    *   [3.1 "Not Authorized" 尝试挂载驱动时](#"Not_Authorized"_尝试挂载驱动时)
    *   [3.2 访问分区所需的密码](#访问分区所需的密码)
    *   [3.3 目录未在文件管理器中打开](#目录未在文件管理器中打开)

## 概要

**注意:** 安装后, 下面列出的软件包将自动由所有已安装且功能强大的文件管理器, 以及所有的桌面环境和/或窗口管理器提供

单独的文件管理器将不会提供完整的桌面环境如[Xfce](/index.php/Xfce "Xfce")或[KDE](/index.php/KDE "KDE")的那些用户习惯的特性和功能。这是因为需要额外的软件包才能使给定的文件管理器能够:

*   显示和访问其他分区
*   显示、挂载和访问可移动媒体(例如USB记忆棒，光盘和数码相机)
*   启用或分享与其他已安装的操作系统的网络
*   启用缩略图
*   归档和提取压缩文件
*   自动挂载可移动媒体

当文件管理器作为完整桌面环境的一部分安装时，通常会自动安装大多数的这些软件包。 因此，在为独立的窗口管理器安装文件管理器的情况下——就像窗口管理器本身一样——只提供基本的支持。那么用户必须确认要添加的特性和功能的性质和范围。

## 附加功能

特别是在使用或打算使用轻量级环境的地方，应当注意更多的文件管理器的特性和功能通常意味着使用更多的内存。参见[udisks](/index.php/Udisks "Udisks")。

### 挂载

*   [gvfs](https://www.archlinux.org/packages/?name=gvfs): Gnome虚拟文件系统(gvfs)提供挂载和回收站功能。GVFS使用[udisks2](https://www.archlinux.org/packages/?name=udisks2)来提供挂载功能，是大多数文件管理器推荐的解决方案。

**提示：** 对于某些文件管理器，安装软件包[gamin](https://www.archlinux.org/packages/?name=gamin)可能很管用。[Gamin](/index.php/Gamin "Gamin")是一个文件和目录监控系统。

GVFS使用的文件夹：

*   `/usr/lib/gvfs/`包含`gvfsd-*`文件, 其中`*`表示支持各种文件系统类型。
*   `/usr/share/gvfs/mounts/`包含GVFS股灾规则。要使用自己的规则，请创建`~/.gvfs/mounts`。

安装附加安装包通常遵循如下[gvfs-* pattern](https://www.archlinux.org/packages/?q=gvfs-)模式，例如：

*   [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc): 苹果移动设备
*   [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp): 媒体播放器和移动设备使用[MTP](/index.php/MTP "MTP")
*   [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2): 数码相机和移动设备使用[PTP](https://en.wikipedia.org/wiki/Picture_Transfer_Protocol "wikipedia:Picture Transfer Protocol")

#### 文件管理守护程序

第一种是简单地以守护进程[daemon](/index.php/Daemon "Daemon")模式自动启动或运行已安装的文件管理器(即作为后台进程)。例如，在[Openbox](/index.php/Openbox "Openbox")中使用[PCManFM](/index.php/PCManFM "PCManFM")时，以下命令将添加到 `~/.config/openbox/autostart` 文件中：

```
pcmanfm -d &

```

还需要在卷管理方面配置文件管理器本身(例如，当安装时检测到某些文件类型时，它将执行什么操作以及将启动哪些应用程序)。

**Tip:** Most desktop environments will start the file manager in daemon mode by default so manual intervention will not be required in these use cases.

#### 独立

Another option is to install a separate [mount application](/index.php/List_of_applications#Mount_tools "List of applications"). The advantages of using this are:

*   Less memory may be required to run as a background / [daemon](/index.php/Daemon "Daemon") process than a file manager
*   It is not file manager specific, allowing them to be freely added, removed, and switched
*   [gvfs](https://www.archlinux.org/packages/?name=gvfs) may not have to be installed for mounting, lessening memory use.

### 网络

**Note:** It will also be necessary to enable [Bluetooth](/index.php/Bluetooth "Bluetooth") and/or networking with [Windows](/index.php/Samba "Samba") to enable the relevant file manager functionality in turn.

*   [obexfs](https://aur.archlinux.org/packages/obexfs/): Bluetooth device mounting and file transfers (see [Bluetooth](/index.php/Bluetooth "Bluetooth"))
*   [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb): Windows File and printer sharing for **Non-KDE** desktops (see [Samba](/index.php/Samba "Samba"))
*   [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing): Windows File and printer sharing for [KDE](/index.php/KDE "KDE") (see [Samba#KDE](/index.php/Samba#KDE "Samba"))
*   [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp): Apple file and printer sharing
*   [sshfs](https://www.archlinux.org/packages/?name=sshfs): FUSE client based on the SSH File Transfer Protocol

#### Windows 访问

If using [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), to access Windows/CIFS/Samba file shares first open the file manager, and enter the following into the path name, changing <sever name> and <share name> as appropriate:

```
smb://<server name>/<share name>

```

#### Apple 访问

If using [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc), to access AFP files first open the file manager, and enter the following into the path name, changing <sever name> and <share name> as appropriate:

```
afp://<server name>/<share name>

```

### 缩略图预览

Some file managers may not support thumbnailing, even when the packages listed have been installed. Check the documentation for the relevant file manager.

#### Dolphin 和 Konqueror 以外的文件管理器

These packages apply to most file managers, such as [PCManFM](/index.php/PCManFM "PCManFM"), [SpaceFM](/index.php/SpaceFM "SpaceFM"), [Thunar](/index.php/Thunar "Thunar") and [xfe](https://aur.archlinux.org/packages/xfe/). The exceptions are Dolphin and Konqueror, used in the [KDE](/index.php/KDE "KDE") desktop environment.

*   [tumbler](https://www.archlinux.org/packages/?name=tumbler): Image files. This **<u>must</u>** also be installed to expand thumbnailing capabilities to other file types
*   [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib): Adobe `.pdf` files
*   [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer): Video files
*   [freetype2](https://www.archlinux.org/packages/?name=freetype2): Font files
*   [libgsf](https://www.archlinux.org/packages/?name=libgsf): `.odf` files
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` files

#### Dolphin and Konqueror (KDE)

See [Dolphin#File previews](/index.php/Dolphin#File_previews "Dolphin").

### 解压文件

To extract compressed files such as tarballs (`.tar` and `.tar.gz`) within a file manager, it will first be necessary to install a GUI archiver such as [file-roller](https://www.archlinux.org/packages/?name=file-roller). See [List of applications#Archiving and compression tools](/index.php/List_of_applications#Archiving_and_compression_tools "List of applications") for further information. An additional package such as [unzip](https://www.archlinux.org/packages/?name=unzip) must also be installed to support the use of zipped `.zip` files. Once an archiver has been installed, files in the file manager may consequently be right-clicked to be archived or extracted.

### NTFS 读/写 支持

见 [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") 文章.

### 桌面通知

Some file managers make use of [desktop notifications](/index.php/Desktop_notifications "Desktop notifications") to confirm various events and statuses like mounting, unmounting and ejection of removable media.

### 在不同的文件系统上开启回收站功能 (外部驱动器)

Make [trash directories](http://www.ramendik.ru/docs/trashspec.html) `.Trash-*<uid>*` for each users on the top level of filesystems:

For example (mount point: /media/sdc1, uid: 1000, gid: 1000):

```
# mkdir /media/sdc1/.Trash-1000

```

and `chown` them:

```
# chown 1000:1000 /media/sdc1/.Trash-1000

```

## 故障排除

### "Not Authorized" 尝试挂载驱动时

File managers using [udisks](/index.php/Udisks "Udisks") require a [polkit](/index.php/Polkit "Polkit") authentication agent. See [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

### 访问分区所需的密码

The need to enter a password to access other partitions or mounted removable media will likely be due to the default permission settings of [udisks2](https://www.archlinux.org/packages/?name=udisks2). More specifically, permission may be set to the root account only, not the user account. See [Udisks#Configuration](/index.php/Udisks#Configuration "Udisks") for details.

### 目录未在文件管理器中打开

You may find that an application that is not a file manager, [Audacious](/index.php/Audacious "Audacious") for example, is set as the default application for opening directories — an application that specifies that it can handle the `inode/directory` MIME type in its desktop entry can become the default. You can query the default application for opening directories with the following command:

```
$ xdg-mime query default inode/directory

```

To ensure that directories are opened in the file manager, run the following command:

```
$ xdg-mime default *my_file_manager*.desktop inode/directory

```

where `*my_file_manager*.desktop` is the desktop entry for your file manager — `org.gnome.Nautilus.desktop` for example.

**Tip:** If you want the change to be system-wide, run the command above as root or create/edit the following file: `/usr/share/applications/mimeapps.list` 
```
[Default Applications]
inode/directory=*my_file_manager*.desktop
```
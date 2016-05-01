来自 [ROX Desktop | ROX Desktop](http://roscidus.com/desktop/):

	*ROX 是一个快速,广泛使用拖放的友好的桌面. 文件管理器或接口, following the traditional Unix view that '所有的东西都是一个文件' rather than trying to hide the filesystem beneath start menus, wizards, or druids. The aim is to make a system that is well designed and clearly presented. The ROX style favors using several small programs together instead of creating all-in-one mega-applications.*

来自 [About ROX | ROX Desktop](http://roscidus.com/desktop/about_rox):

	*Traditionally, Unix users have always based their activities around the filesystem. Just about everything that's anything appears as a file: regular files, hardware devices, and even processes on many systems (for example, inside the `/proc` filesystem on Linux).*

	*However, recent desktop efforts (such as KDE and GNOME) seem to be following the Windows approach of trying to hide the filesystem and get users to do things via a Start-menu or similar. Modern desktop users, on Windows or Unix, often have no idea where their programs are installed, or even where their data files are saved. This leads to a feeling of not being in control, and a poor understanding of how the system works.*

	*The ROX Desktop, however, is based around the filesystem. Its core component is ROX-Filer, a powerful graphical file manager which, in addition to being a popular filer in its own right, provides a couple of extra features which allow it to solve the above problems...*

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Pacman](#Pacman)
    *   [1.2 从零安装](#.E4.BB.8E.E9.9B.B6.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.1 文件管理器](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.2 桌面环境](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [2.3 用静态挂载点挂载](#.E7.94.A8.E9.9D.99.E6.80.81.E6.8C.82.E8.BD.BD.E7.82.B9.E6.8C.82.E8.BD.BD)
    *   [2.4 用pmount挂载](#.E7.94.A8pmount.E6.8C.82.E8.BD.BD)

## 安装

有两个方式安装它：正常方式或从零安装。

### Pacman

The package, though it doesn't seem like it, has the desktop stuff with it. Install it with:

 `pacman -S rox` 

### 从零安装

Arch Linux does not exactly have a zero-install package (that I am aware of), so this can be a potential PITA.

Make sure you have the packages 'python' 'gnupg' 'pygtk' installed.

Download the GPG key

 ` gpg --recv-key --keyserver www.keyserver.net 59A53CC1 ` 

Download the actual 'injector'.

 ` wget http://osdn.dl.sourceforge.net/sourceforge/zero-install/zeroinstall-injector-0.26.tar.gz.gpg ` 

Check the signature using GPG, if you care.

 `gpg zeroinstall-injector-0.26.tar.gz.gpg` 

You can stuff everything in a new directory like I did, or sit in $HOME. Then extract and cd into the extracted directory.

Fun python install stuff (as root).

 ` python setup.py install ` 

Actually installing and using things is a little different, just read their stuff: [http://www.0install.net/injector-using.html](http://www.0install.net/injector-using.html)

## 用法

### 文件管理器

输入以下命令执行ROX文件管理器:

 `rox` 

### 桌面环境

你需要在运行你的窗口管理器前运行ROX. 这是我的方式, 使用[Openbox (简体中文)](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")作为窗口管理器

 `rox -b Default -p default ; exec openbox` 

### 用静态挂载点挂载

Rox支持用/etc/fstab挂载与卸载分区, 只需点击一下挂载目录。举个例子,你可以创建一个目录 /mnt/cdrom, 并且在fstab设置一个入口像这样:

 ` /dev/cdrom /mnt/cdrom auto noauto,user,ro 0 0 ` 

打开/mnt/cdrom目录时将会自动挂载/dev/cdrom到/mnt/cdrom.

### 用pmount挂载

fstab静态挂载点有一些问题; 不能一次挂载两个usb设备, 举个例子, 要挂载两个usb设备必须在fstab里写两条内容. 幸好, Rox可以让你自定义挂载方式, 导入设备节点在/dev. 从而, 你可以使用自定义pmount和pumount命令挂在或卸载设备。

To do this, install the pmount package, then open up /dev in Rox and right-click on a block device node (e.g. /dev/sr0). Enter the file menu and click on "Customize Menu." A window will appear in which you can create files that will invoke the necessary commands. Create, and then make executable, the following files:

mount.sh:

```
#!/bin/sh
pmount "$@"
```

umount.sh:

```
#!/bin/sh
pumount "$@"
```

If you want your mount directories to use device labels or UUID use this mount script instead: mount.sh:

```
#!/bin/bash

#Get device label using blkid
blkid -o value -s LABEL  "$@" > /tmp/roxmount.tmp.$$
LABEL=`cat /tmp/roxmount.tmp.$$`

#Use UUID if no label is set
if [ -z $LABEL ]
   then
   blkid -o value -s UUID  "$@" > /tmp/roxmount.tmp.$$
   LABEL=`cat /tmp/roxmount.tmp.$$`
fi

#Ask for mount name if no LABEL/UUID is found (NEEDS xdialog package installed)
if [ -z $LABEL ]
   then
   Xdialog --title "Input Parameters" --inputbox "Enter a mount name" 0 0 2> /tmp/roxmount.tmp.$$
   LABEL=`cat /tmp/roxmount.tmp.$$`
fi

#Mount the device
pmount "$@" $LABEL

```

You will now be able to mount device nodes to appropriately named directories in /media, and unmount them as necessary, using the new menu entries. For convenience, you should probably also change the mount and unmount commands in Rox's configuration (under "Action Windows") to "pmount" and "pumount"; this will let you unmount devices via the mount directory's right-click menu.
**翻译状态：** 本文是英文页面 [Change_Root](/index.php/Change_Root "Change Root") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-20，点击[这里](https://wiki.archlinux.org/index.php?title=Change_Root&diff=0&oldid=261088)可以查看翻译后英文页面的改动。

[Chroot](https://en.wikipedia.org/wiki/Chroot "wikipedia:Chroot") 是将当前磁盘根路径(和当前进程和它们的子进程)更改到另一个根目录。当你更改根路径到另一个目录下时，你不能在那个目录外存取文件和使用命令。这个目录叫作 _chroot jail_。切换根目录通常为了系统维护，例如重装引导程序或者重置遗忘的密码。

## Contents

*   [1 必要条件](#.E5.BF.85.E8.A6.81.E6.9D.A1.E4.BB.B6)
*   [2 挂载分区](#.E6.8C.82.E8.BD.BD.E5.88.86.E5.8C.BA)
*   [3 Change root](#Change_root)
*   [4 运行图形化的chroot应用](#.E8.BF.90.E8.A1.8C.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.9A.84chroot.E5.BA.94.E7.94.A8)
*   [5 系统维护](#.E7.B3.BB.E7.BB.9F.E7.BB.B4.E6.8A.A4)
*   [6 退出chroot环境](#.E9.80.80.E5.87.BAchroot.E7.8E.AF.E5.A2.83)
*   [7 示例](#.E7.A4.BA.E4.BE.8B)

## 必要条件

*   你需要从另一个运行的linux环境启动(例如从liveCD或USB闪存介质，或者从另一个已经安装的linux发行版中)。

*   为了chroot需要root特权。

*   确定你启动进的linux环境的架构符合你想要更改的根路径的架构(例如，i686,x86_64)。你可以用以下命令得到你的当前环境架构：

	 `# uname -m` 

*   如果你需要任何在chroot环境中使用的内核模块，在chroot之前加载它。初始化你的swap (`swapon /dev/sdxY`)估计也很有用，并且在chroot之前建立网络连接。

## 挂载分区

你想尝试chroot进去的linux系统根分区需要先被挂载。为了找出内核分配的设备名称，运行：

```
# lsblk /dev/sda

```

你也能运行如下命令获取你的分区布局

```
# fdisk -l

```

现在创建一个你想要挂载root分区的目录并且挂载到它：

```
# mkdir /mnt/arch
# mount /dev/sda3 /mnt/arch

```

接着，如果你的系统的其它分区有单独分区(比如说 `/boot`， `/home`，`/var`等等)，你也需要挂载他们：

```
# mount /dev/sda1 /mnt/arch/boot/
# mount /dev/sdb5 /mnt/arch/home/
# mount ...

```

尽管你chroot之后可以挂载文件系统，之前完事更加方便。原因就是你将不得不在退出chroot之前卸载临时文件系统，而这样做将让你用一个单个命令卸载所有文件系统。这也使得关机更加安全。因为外部linux环境知道所有挂载的分区，它能安全的在关机时卸载他们。

## Change root

作为root挂载临时文件系统：

**Note:** 使用更新的 (2012) Arch

发行版，以下`mount`命令可以被`arch-chroot`

`/mnt/arch`取代。你必须安装了[arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)才能运行arch-chroot。如果你在使用其它不同的Linux发行版以下命令应该仍可以使用。

```
# cd /mnt/arch
# mount -t proc proc proc/
# mount -t sysfs sys sys/
# mount -o bind /dev dev/
# mount -t devpts pts dev/pts/

```

如果你已经建立了一个网络连接并且想要在chroot环境中使用它，你可能不得不拷贝你的DNS服务器配置让你能够解析主机名：

```
# cp -L /etc/resolv.conf etc/resolv.conf

```

现在chroot到你之前安装的系统中并且指定你的shell

```
# chroot /mnt/arch /usr/bin/bash

```

**Note:** 如果你遇到错误 `chroot: cannot run command '/bin/bash': Exec format error`，很可能两个环境架构不匹配。

**Note:** 如果你遇到错误 `chroot: '/usr/bin/bash': permission denied`,用执行权限重新挂载: `mount -o remount,exec /mnt/arch`。

可选地，source你的Bash配置文件(`~/.bashrc`和`/etc/bash.bashrc`)，运行：

```
# source ~/.bashrc
# source /etc/profile

```

可选的，创建一个独特的提示符来区别你的chroot环境：

```
# export PS1="(chroot) $PS1"

```

## 运行图形化的chroot应用

如果你在系统上运行了[X](/index.php/X "X")，你可以在chroot环境启动图形应用。

为了chroot环境能连接到你的X服务器，在X服务器中打开一个终端(例如，在用户当前登录的桌面中)，然后运行如下命令给任何人连接到用户X服务器的权限：

```
$ xhost +

```

然后，从chroot环境中将应用指向你的X服务器，将chroot中的DISPLAY环境变量设定成和拥有X服务器的用户DISPLAY变量相匹配。例如，运行：

```
$ echo $DISPLAY

```

作为拥有X服务器的用户查看DISPLAY的值。如果是“:0”(例如是)，然后在chroot环境中运行

```
# export DISPLAY=:0

```

现在你可以从chroot命令行启动图形界面应用;）

## 系统维护

此时你可以执行任何你需要在chroot环境中执行的系统维护操作。一些常见的例子是：

*   重装引导。
*   重新构建[initramfs](/index.php/Mkinitcpio "Mkinitcpio")镜像。
*   升级或[降级](/index.php/Downgrading_Packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Downgrading Packages (简体中文)")软件包。
*   重置[遗忘的密码](/index.php/Password_Recovery_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Password Recovery (简体中文)").

## 退出chroot环境

当你完成系统维护后，退出chroot：

```
# exit

```

然后卸载临时文件系统和任何挂载的设备：

```
# umount {proc,sys,dev/pts,boot,[...],}

```

最后，尝试卸载你的根分区：

```
# cd ..
# umount arch/

```

**Note:** 如果你得到错误说`/mnt`(或其它任何分区) is busy, 这可能意味着两种情况：

*   chroot环境中残留了一个运行的程序。

*   或者，更常见的是，仍然存在子挂载(例如 `/mnt/arch/boot`挂载在`/mnt/arch`)。通过`lsblk`检查是否还存在任何挂载点(你也可以单输入一个mount查看):

	 `lsblk /dev/sda` 

	如果你仍然不能卸载分区，使用`--force`选项：

	 `# umount -f /mnt` 

这之后，你可以安全地的重启了。

## 示例

这也许能在浏览期间保护你的系统免于网络攻击：

```
# # as root: 
# cd /home/user
# mkdir myroot
# pacman -S arch-install-scripts
# # pacstrap must see myroot as mounted: 
# mount --bind myroot myroot
# pacstrap -i myroot base base-devel
# mount -t proc proc myroot/proc/
# mount -t sysfs sys myroot/sys/
# mount -o bind /dev myroot/dev/
# mount -t devpts pts myroot/dev/pts/
# cp -i /etc/resolv.conf myroot/etc/
# chroot myroot
# # inside chroot: 
# passwd # set a password 
# useradd -m -s /usr/bin/bash user
# passwd user # set a password
# # in a shell outside the chroot: 
# pacman -S xorg-server-xnest
# # in a shell outside the chroot you can run this as user: 
$ Xnest -ac -geometry 1024x716+0+0 :1
# # continue inside the chroot: 
# pacman -S xterm
# DISPLAY=:1
# xterm
# # xterm is now running in Xnest 
# pacman -S xorg-server xorg-xinit xorg-server-utils
# pacman -S openbox
# # for java we need icedtea-web which requires some fonts: 
# nano /etc/locale.gen
# # uncomment en_US.UTF-8 UTF-8, save and exit 
# locale-gen
# echo LANG=en_US.UTF-8 > /etc/locale.conf
# export LANG=en_US.UTF-8
# pacman -S ttf-dejavu
# pacman -S icedtea-web
# pacman -S firefox
# firefox
# # firefox is now running in Xnest 
# exit
# # outside chroot: 
# chroot --userspec=user myroot
# # inside chroot as user: 
$ DISPLAY=:1
$ openbox &
$ HOME="/home/user"
$ firefox
```

参见: [Basic Chroot](https://help.ubuntu.com/community/BasicChroot)
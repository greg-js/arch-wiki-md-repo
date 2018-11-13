## Contents

*   [1 简介](#简介)
*   [2 从安装媒体启动](#从安装媒体启动)
*   [3 为使用SSH设置live安装环境](#为使用SSH设置live安装环境)
*   [4 通过SSH连接到目标PC](#通过SSH连接到目标PC)
    *   [4.1 注意](#注意)
*   [5 下一步](#下一步)

## 简介

这篇文章主要是介绍在使用SSH连接的情况下安装Arch。考虑到以下几种场景下的该安装方法的一个标准情况：

在以下情况安装Arch...

*   没有显示器的HTPC(比如一个SDTV)。
*   一个在另外城市、省份、国家的PC。(朋友的家、父母的家等等)
*   一个你想要远程安装的PC，比如从一个可以方便的从 Arch Wiki 复制/粘贴的自己的工作站上远程安装。

**注意:** 前2步需要直接的物理控制PC。显然，如果PC在别处，就需要另外一个人的协调。

## 从安装媒体启动

使用[最新的安装媒介](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#获得最新的安装媒介 "Beginners' guide (简体中文)")启动PC到Arch的live环境，并且以**root**登陆。

## 为使用SSH设置live安装环境

**注意:** 下面的命令必须以root账户执行。**#**提示是为了复制/粘贴方便而故意忽略了。

现在你的眼前应该可以看到**[root@archiso~]#**的提示。

首先，建立目标机器的网络设置：

```
aif -p partial-configure-network

```

这个命令会列出所有已知的网络接口，输入你想使用的网络接口(比如，eth0作为有线以太网的接口)

第2步，同步安装环境与源，安装openssh包，然后启动它：

```
pacman -Syy openssh
rc.d start sshd

```

**注意:** 根据安装介质的年龄，pacman也许会抱怨它自己要首先被更新。考虑到我们只是简单的要安装openssh包，推荐取消pacman的更新要求从而只安装这一个包。

最后，设定一个建立ssh链接需要的root密码；默认root的arch密码是空的。

```
passwd

```

## 通过SSH连接到目标PC

使用下面的命令以链接到目标机器:

```
$ ssh root@ip.address.of.target

```

从现在开始尽管我们在本地，也可以通过我们自己的键盘控制远程的机器显示安装画面了。

```
ssh root@10.1.10.105
root@10.1.10.105's password: 
Last login: Thu Dec 23 08:33:02 2010 from 10.1.10.200
**************************************************************
* To begin installation, run /arch/setup                     *
* You can find documentation at                              *
*  /usr/share/aif/docs/official_installation_guide_en        *
*                                                            *
* i18n: Use the 'km' utility to change your keyboard layout  *
*       and console font.                                    *
*                                                            *
* If you are looking to install Arch on something more       *
* exotic, such as your kerosene-powered cheese grater,       *
* please consult [https://wiki.archlinux.org](https://wiki.archlinux.org).                  *
*                                                            *
**************************************************************
[root@archiso ~]#
```

### 注意

*   如果目标机器处在防火墙/路由的后面，ssh默认的22端口需要转发给目标机器在的本地LAN IP地址。这个端口的转发不在本文的讨论范围。
*   你也可以在启动守护进程前编辑 Live 环境上的`/etc/ssh/sshd_config`，比如如果想在非标准端口运行的话。

## 下一步

没有限制。如果只是想从这个安装介质安装Arch，只需要运行 `/arch/setup`。如果想编辑一个已有的损坏的安装，参见[Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")的wiki文章。

想要[grub2](/index.php/Grub2 "Grub2")或者使用[GPT](/index.php/GPT "GPT")硬盘?

*   如果想要在运行安装环境的机器上，重新通过**pacman -S gdisk**安装的**gdisk**来手工的对目标机器的HDD/SDD硬盘分区，只要简单的回答no然后返回live安装环境的root提示符。
*   安装grub2是很容易的。只需要简单的chroot进新安装的arch环境(如果从安装环境出来了就已经挂载了)然后安装grub2：

```
 cd /mnt
 rm console ; mknod -m 600 console c 5 1
 rm null ; mknod -m 666 null c 1 3
 rm zero ; mknod -m 666 zero c 1 5
 mount -t proc proc /mnt/proc
 mount -t sysfs sys /mnt/sys
 mount -o bind /dev /mnt/dev
 chroot /mnt /bin/bash

```

现在进入这个新的Arch的chroot:

```
 pacman -S grub2
 grep -v rootfs /proc/mounts > /etc/mtab

```

按照你喜欢的方式编辑`/etc/default/grub`。 安装grub并且生成一个grub.cfg

```
 grub-install /dev/sdX --no-floppy
 grub-mkconfig -o /boot/grub/grub.cfg

```

**注意:** 上面的命令假设用户想要从GPT硬盘上启动，并且充分的理解了上述wiki文章，而且还有可供grub2使用的1Mb的ef02分区。

当准备好重启新的Arch机器前，离开chroot环境，并且在重启前卸载掉前面挂载的分区。

```
 exit
 umount /mnt/boot   # if mounted this or any other separate partitions
 umount /mnt/{proc,sys,dev}
 umount /mnt

```
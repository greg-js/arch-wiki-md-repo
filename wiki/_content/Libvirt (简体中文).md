# Libvirt (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [QEMU](/index.php/QEMU "QEMU")
*   [KVM](/index.php/KVM "KVM")
*   [VirtualBox](/index.php/VirtualBox "VirtualBox")
*   [Xen](/index.php/Xen "Xen")
*   [VMware](/index.php/VMware "VMware")

**翻译状态：** 本文是英文页面 [Libvirt](/index.php/Libvirt "Libvirt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-06-07，点击[这里](https://wiki.archlinux.org/index.php?title=Libvirt&diff=0&oldid=318100)可以查看翻译后英文页面的改动。

libvirt 是一个虚拟化 API 和虚拟机(VMs)管理后台，支持远程或本地访问，支持多种虚拟化后端 ([QEMU](/index.php/QEMU "QEMU")/[KVM](/index.php/KVM "KVM")， [VirtualBox](/index.php/VirtualBox "VirtualBox")， [Xen](/index.php/Xen "Xen")，等等) 。本文并不打算涉及有关 libvirt 的方方面面，仅讨论那些与通常的认知不同的地方或文档论述不详之处。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [1.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 运行后台进程](#.E8.BF.90.E8.A1.8C.E5.90.8E.E5.8F.B0.E8.BF.9B.E7.A8.8B)
    *   [2.2 认证策略](#.E8.AE.A4.E8.AF.81.E7.AD.96.E7.95.A5)
    *   [2.3 Unix 文件权限](#Unix_.E6.96.87.E4.BB.B6.E6.9D.83.E9.99.90)
    *   [2.4 为 QEMU 打开 KVM 加速](#.E4.B8.BA_QEMU_.E6.89.93.E5.BC.80_KVM_.E5.8A.A0.E9.80.9F)
    *   [2.5 宿主机关机/启动时停止/恢复客户机](#.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.85.B3.E6.9C.BA.2F.E5.90.AF.E5.8A.A8.E6.97.B6.E5.81.9C.E6.AD.A2.2F.E6.81.A2.E5.A4.8D.E5.AE.A2.E6.88.B7.E6.9C.BA)
    *   [2.6 引导时启动 KVM 虚拟机](#.E5.BC.95.E5.AF.BC.E6.97.B6.E5.90.AF.E5.8A.A8_KVM_.E8.99.9A.E6.8B.9F.E6.9C.BA)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
    *   [3.1 创建一个新虚拟机](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E6.96.B0.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [3.2 在virt-manager中创建存储池](#.E5.9C.A8virt-manager.E4.B8.AD.E5.88.9B.E5.BB.BA.E5.AD.98.E5.82.A8.E6.B1.A0)
    *   [3.3 用virt-manager管理VirtualBox](#.E7.94.A8virt-manager.E7.AE.A1.E7.90.86VirtualBox)
    *   [3.4 在线快照](#.E5.9C.A8.E7.BA.BF.E5.BF.AB.E7.85.A7)
*   [4 远程访问libvirt](#.E8.BF.9C.E7.A8.8B.E8.AE.BF.E9.97.AElibvirt)
    *   [4.1 使用未加密的 TCP/IP socket (最简单，最不安全)](#.E4.BD.BF.E7.94.A8.E6.9C.AA.E5.8A.A0.E5.AF.86.E7.9A.84_TCP.2FIP_socket_.28.E6.9C.80.E7.AE.80.E5.8D.95.EF.BC.8C.E6.9C.80.E4.B8.8D.E5.AE.89.E5.85.A8.29)
    *   [4.2 使用 SSH](#.E4.BD.BF.E7.94.A8_SSH)
    *   [4.3 使用 Python](#.E4.BD.BF.E7.94.A8_Python)
*   [5 桥接网络](#.E6.A1.A5.E6.8E.A5.E7.BD.91.E7.BB.9C)
    *   [5.1 宿主机配置](#.E5.AE.BF.E4.B8.BB.E6.9C.BA.E9.85.8D.E7.BD.AE)
    *   [5.2 客户机配置](#.E5.AE.A2.E6.88.B7.E6.9C.BA.E9.85.8D.E7.BD.AE)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

由于守护进程/客户端的架构, libvirt只需要安装在将虚拟化的机器上。 注意，在服务器和客户端可以是相同的物理机。

### 服务端

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [libvirt](https://www.archlinux.org/packages/?name=libvirt)，以及至少一个管理程序

*   截至 2015-02-01, `libvirtd` **要求** [qemu](https://www.archlinux.org/packages/?name=qemu)在系统上安装启动 (参见 [FS#41888](https://bugs.archlinux.org/task/41888)). Fortunately, the [libvirt KVM/QEMU driver](http://libvirt.org/drvqemu.html) is the primary _libvirt_ driver and if [KVM is enabled](/index.php/QEMU#Enabling_KVM "QEMU"), fully virtualized, hardware accelerated guests will be available. See the [QEMU](/index.php/QEMU "QEMU") article for more informations.

*   其他虚拟机后端包括 [LXC](/index.php/LXC "LXC"), [VirtualBox](/index.php/VirtualBox "VirtualBox")和 [Xen](/index.php/Xen "Xen")。请参见它们各自的安装说明。

**Note:** The [libvirt LXC driver](http://libvirt.org/drvlxc.html) has no dependency on the [LXC](/index.php/LXC "LXC") userspace tools provided by [lxc](https://www.archlinux.org/packages/?name=lxc), therefore there is no need to install it if planning on using this driver.

**Warning:** [Xen](/index.php/Xen "Xen") support is available but not by default. You need to use the [ABS](/index.php/ABS "ABS") to modify [libvirt](https://www.archlinux.org/packages/?name=libvirt)'s [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and build it without the `--without-xen` option.

其它虚拟机管理程序 [[1]](http://libvirt.org/drivers.html).

用于网络连接：

*   [ebtables](https://www.archlinux.org/packages/?name=ebtables) **和** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 默认 [default](http://wiki.libvirt.org/page/VirtualNetworking#The_default_configuration) NAT/DHCP网络
*   [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) 桥接网络
*   [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat)通过 [SSH](/index.php/SSH "SSH")远程管理

### 客户端

客户端是用于管理和访问虚拟机的用户界面。

*   _virsh_用于管理和配置域的命令行程序; 它包含在 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 包中。
*   [virt-manager](https://www.archlinux.org/packages/?name=virt-manager)用于管理虚拟机的图形用户界面。
*   [virtviewer](https://www.archlinux.org/packages/?name=virtviewer)轻量级界面，用于显示并与虚拟化客户机系统进行交互
*   [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes) 简单的 GNOME 3 程序，访问远程虚拟系统
*   [virt-manager-qt4](https://aur.archlinux.org/packages/virt-manager-qt4/)<sup><small>AUR</small></sup> [virt-manager-qt5](https://aur.archlinux.org/packages/virt-manager-qt5/)<sup><small>AUR</small></sup>
*   [libvirt-sandbox](https://aur.archlinux.org/packages/libvirt-sandbox/)<sup><small>AUR</small></sup> 应用程序沙箱工具包

兼容 libvirt 的软件列表 [here](http://libvirt.org/apps.html).

## 配置

Libvirt 不是“开箱即用”的。你至少需要[运行后台进程](#Run_daemon)并且配置[认证策略](#.E8.AE.A4.E8.AF.81.E7.AD.96.E7.95.A5)或者配置[Unix 文件权限](#Unix_.E6.96.87.E4.BB.B6.E6.9D.83.E9.99.90)。同样也需要[为 QEMU 打开 KVM 加速](#.E4.B8.BA_QEMU_.E6.89.93.E5.BC.80_KVM_.E5.8A.A0.E9.80.9F).

### 运行后台进程

在 `/etc/libvirt/qemu.conf`中修改默认的用户和用户组。 QEMU 默认是 nobody:nobody。

用 [Systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")打开和启动 `libvirtd.service`

**注意:** Avahi 后台进程用于通过 DNS组播发现本地 libvirt 主机。可以在`/etc/libvirt/libvirtd.conf`中设置`mdns_adv = 0` 禁用此功能。

### 认证策略

创建下列文件，使_libvirt_用户组里面的非root用户可以管理虚拟机：

 `/etc/polkit-1/rules.d/50-org.libvirt.unix.manage.rules` 

```
polkit.addRule(function(action, subject) {
    if (action.id == "org.libvirt.unix.manage" &&
        subject.isInGroup("libvirt")) {
            return polkit.Result.YES;
    }
});

```

或者，用下列语句授予非root用户仅查看虚拟机的权限

`org.libvirt.unix.monitor`。

更多信息请参阅：[libvirt 的 wiki 站点](http://wiki.libvirt.org/page/SSHPolicyKitSetup#Configuring_management_access_via_PolicyKit)。

### Unix 文件权限

**注意:** 这是[#认证策略](#.E8.AE.A4.E8.AF.81.E7.AD.96.E7.95.A5)的替代方案

如果希望通过配置 Unix 文件权限的方式允许某些非 root 用户使用 libvirt，需按下列步骤设置：

首先，创建_libvirt_ [用户组](/index.php/Users_and_Groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and Groups (简体中文)")并将需授权访问 libvirt 的用户加入该组：

```
# groupadd libvirt
# gpasswd -a _user_ libvirt

```

如果被加入的用户当前已登录，则需要注销后重新登录。或者，该用户也可以执行下列命令更新所属组：

```
$ newgrp libvirt

```

将`/etc/libvirt/libvirtd.conf`文件中下列行的注释符（#号）删除（这些行可能位于文件中不同位置）：

 `/etc/libvirt/libvirtd.conf` 

```
 #unix_sock_group = "libvirt"
 #unix_sock_ro_perms = "0777"
 #unix_sock_rw_perms = "0770"
 #auth_unix_ro = "none"
 #auth_unix_rw = "none"

```

**注意:** 还应当将 `unix_sock_ro_perms` 参数的值由 `0777` 改为 `0770` ，目的是取消非 libvirt 组的其他用户的只读访问权限

### 为 QEMU 打开 KVM 加速

**注意:** [KVM](/index.php/KVM "KVM") 与 [VirtualBox](/index.php/VirtualBox "VirtualBox") 有冲突，二者不能同时使用。

以惯常方式（不带 KVM 支持）运行 [QEMU](/index.php/QEMU "QEMU") 模拟器会变态地慢！如果 CPU 支持，你一定要打开 KVM 支持。执行下列命令查看 CPU 是否支持 KVM：

```
egrep --color "vmx|svm" /proc/cpuinfo

```

如果上述命令有输出结果返回，则说明 CPU 支持 KVM 硬件加速。如果**没有**返回任何信息，则**无法使用 KVM**

KVM 无效时，可在 `/var/log/libvirt/qemu/VIRTNAME.log` 这个文件中读到下列信息：

 `/var/log/libvirt/qemu/VIRTNAME.log` 

```
Could not initialize KVM, will disable KVM support

```

[KVM 官方 FAQ](http://www.linux-kvm.org/page/FAQ)中包含更多相关信息

### 宿主机关机/启动时停止/恢复客户机

Systemd 的 `libvirt-guests.service` 这个服务程序可以支持在宿主机关机时自动地挂起或关闭客户机。同样也支持宿主机开机时自动恢复或启动客户机。

请查阅 `/etc/conf.d/libvirtd-guests` 中的 libvirt-guests 相关选项。

### 引导时启动 KVM 虚拟机

如果用 _virt-manager_ 和 _virsh_ 作为虚拟机管理工具，则很简单即可实现。

开机自动启动的命令：

```
$ virsh autostart <domain>

```

禁用开机自动启动的命令：

```
$ virsh autostart --disable <domain>

```

_virt-manager_ 中，在**引导** 选项页下同样也有个**自动启动**勾选项。

**注意:** 以命令行方式通过 QEMU 或 KVM 启动的虚拟机不能通过 _virt-manager_ 管理

## 使用

### 创建一个新虚拟机

创建新虚拟机需要准备安装介质，通常是一个标准的`.iso`文件。将其复制到`/var/lib/libvirt/images/` 目录即可（或者在 virt-manager 中新建一个 **存储池** 目录，将其复制到该目录）。

**注意:** [SELinux](/index.php/SELinux "SELinux")要求虚拟机默认存储在`/var/lib/libvirt/images/`目录。如果启用了 SELinux并且 are having issues with virtual machines，需确保虚拟机位于该目录或确保添加了指向非默认目录的正确标签（译注：本段译文需斟酌）

然后运行`virt-manager`连接到服务器，右击**连接**、选择**新建**。 输入自定义的连接名，选择 **本地安装介质**，按照向导继续。

在**第四步**中，应当取消 **分配全部磁盘空间** 选项。当虚拟机并不需要使用全部磁盘时，这样做可以节约空间，但也会导致磁盘碎片增多。此时，应密切关注宿主机的剩余磁盘空间总量，否则很容易导致为虚拟机分配了过量磁盘空间。

在**第五步**中，打开 **高级选项** 并确认 **虚拟类型** 选择了 **kvm**。如果该选项无效，查阅前文 [为 QEMU 打开 KVM 加速](#.E4.B8.BA_QEMU_.E6.89.93.E5.BC.80_KVM_.E5.8A.A0.E9.80.9F) 一节

### 在virt-manager中创建存储池

首先连接到一个现有的服务器。连接后，右击**详情**，进入**存储**，点击左下方的**+**图标，然后按向导指示继续。

### 用virt-manager管理VirtualBox

**注意:** Libvirt对[VirtualBox](/index.php/VirtualBox "VirtualBox")的支持尚不完备，有可能导致 libvirtd 进程崩溃。但通常这并不会导致灾难，重启进程即可恢复

virt-manager 不允许从图形用户界面程序连接 VirtualBox。但可以从命令行加载：

```
virt-manager -c vbox:///system

```

或者通过 SSH 管理远程系统：

```
virt-manager -c vbox+[ssh://username@host/system](ssh://username@host/system)

```

### 在线快照

Libvirt 可以在无需关闭虚拟机的情况下抓取虚拟机快照，这个功能称为**外部快照(external snapshotting)**。 当前该功能仅支持基于 qcow2 和 raw 文件的虚拟机镜像。

一旦快照创建完毕，KVM 将新建一个仅包含快照内容的块设备挂载到虚拟机，新产生的数据将直接写入这个新的磁盘，原始磁盘镜像将被置为离线，以便复制或备份。以后还可以重新将含快照的镜像与原始镜像融合而无需关闭虚拟机。（本段译文存疑-Aaron Chen）

以下演示其工作原理：

当前运行中的虚拟机：

 `# virsh list --all` 

```
 Id    Name                           State
 ----------------------------------------------------
 3     archey                            running

```

查看虚拟机的全部镜像文件：

 `# virsh domblklist archey` 

```
 Target     Source
 ------------------------------------------------
 vda        /vms/archey.img

```

**注意看镜像文件的属性**

 `# qemu-img info /vms/archey.img` 

```
 image: /vms/archey.img
 file format: qcow2
 virtual size: 50G (53687091200 bytes)
 disk size: 2.1G
 cluster_size: 65536

```

创建一个 disk-only 类型的快照。开关参数`--atomic`将确保万一快照创建失败时虚拟机不被篡改

```
# virsh snapshot-create-as archey snapshot1 --disk-only --atomic

```

查看快照清单：

 `# virsh snapshot-list archey` 

```
 Name                 Creation Time             State
 ------------------------------------------------------------
 snapshot1           2012-10-21 17:12:57 -0700 disk-snapshot

```

virsh 创建了一个新的镜像文件。**注意观察它的属性：只有几 MB 大小，并且链接到其原始的“后备镜像/链”**

 `# qemu-img info /vms/archey.snapshot1` 

```
 image: /vms/archey.snapshot1
 file format: qcow2
 virtual size: 50G (53687091200 bytes)
 disk size: 18M
 cluster_size: 65536
 backing file: /vms/archey.img

```

在这里，可以回过头来复制原始镜像（通过`cp -sparse=true`或`rsync -S`参数），然后就可以将原始镜像融合进快照。

```
# virsh blockpull --domain archey --path /vms/archey.snapshot1

```

现在，数据块被从原始镜像中抽离出来，`/vms/archey.snapshot1` 这个文件成为新的虚拟机磁盘的镜像文件。查看其磁盘容量就知道。这些都完成后，原始磁盘镜像`/vms/archey.img` 以及快照元数据就可以安全地删除了。

`virsh blockcommit`是`blockpull`的反向操作，不过似乎在当前的 qemu-kvm 1.3 版中（连同**快照恢复(snapshot-revert)**）功能都还处于开发阶段，按开发日程安排是在明年发布。

对于需要频繁在线备份的需求者来说，KVM的这一新功能十分便利而又不必冒文件系统损坏的风险。

## 远程访问libvirt

### 使用未加密的 TCP/IP socket (最简单，最不安全)

**警告:** 这一操作**仅可**应用于安全、私密、可信的网络环境

编辑`/etc/libvirt/libvirtd.conf`：

 `/etc/libvirt/libvirtd.conf` 

```
listen_tls = 0
listen_tcp = 1
auth_tcp=none

```

**警告:** 这里的设置没有打开 SASL，因而**所有的 TCP 传输都是明文传输！**在真实的应用环境中，一定要**始终**打开 SASL。

另外还要编辑`/etc/conf.d/libvirtd`，以监听模式启动libvirtd服务

 `/etc/conf.d/libvirtd`  `LIBVIRTD_ARGS="--listen"` 

### 使用 SSH

通过[SSH](/index.php/SSH "SSH")远程管理，需要[openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat)软件包。

用`virsh`连接到远程系统：

```
$ virsh -c qemu+ssh://_username_@_host/IP address_/system

```

如果出错了，可以如下方式获取日志：

```
$ LIBVIRT_DEBUG=1 virsh -c qemu+ssh://_username_@_host/IP address_/system

```

显示图形界面虚拟机控制台：

```
$ virt-viewer --connect qemu+ssh://_username_@_host/IP address_/system myvirtualmachine

```

显示虚拟机桌面管理工具：

```
$ virt-manager -c qemu+ssh://_username_@_host/IP address_/system

```

**注意:** 如果连接到远程的 RHEL （或者其他非 Arch 系统）服务器有问题，参阅[FS#30748](https://bugs.archlinux.org/task/30748)以及[FS#22068](https://bugs.archlinux.org/task/22068)。

### 使用 Python

[libvirt-python](https://www.archlinux.org/packages/?name=libvirt-python)软件包中的`/usr/lib/python2.7/site-packages/libvirt.py`提供了[python2](https://www.archlinux.org/packages/?name=python2) 的 API。

`/usr/share/doc/libvirt-python-_your_libvirt_version_/examples/`中给出了若干通用范例。

使用[qemu](https://www.archlinux.org/packages/?name=qemu) 和 [openssh](https://www.archlinux.org/packages/?name=openssh) 的非官方范例：

```
#! /usr/bin/env python2
# -*- coding: utf-8 -*-
import socket
import sys
import libvirt
if (__name__ == "__main__"):
   conn = libvirt.open("qemu+[ssh://xxx/system](ssh://xxx/system)")
   print "Trying to find node on xxx"
   domains = conn.listDomainsID()
   for domainID in domains:
       domConnect = conn.lookupByID(domainID)
       if domConnect.name() == 'xxx-node':
           print "Found shared node on xxx with ID " + str(domainID)
           domServ = domConnect
           break

```

## 桥接网络

如果要在虚拟机中使用宿主机的物理网卡，需要在物理网卡（此处为eth0）和虚拟机的虚拟网卡之间创建**网桥**。

### 宿主机配置

由于 libvirt 会创建一个名为**virbr0**的 NAT 网络，所以应该使用其他的名字比如**br0**或者**virbr1**创建网桥。 应当创建一个 [Netctl](/index.php/Netctl "Netctl") 或 [Systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 的配置文件配置新创建的网桥，例如(使用 DHCP 的配置)：

 `/etc/netctl/br0` 

```
Description="Bridge connection for kvm"
Interface=br0
Connection=bridge
BindsToInterfaces=(eno1)
IP=dhcp

```

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**这篇文章或章节的内容已经[过期](/index.php/Template:%E8%BF%87%E6%9C%9F "Template:过期").**

请通过更新这篇文章和改正错误帮助改善 wiki。

**小贴士:** 建议在新建的虚拟网桥（例如**br0**）配置中打开生成树(STP-[Spanning Tree Protocol](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol "wikipedia:Spanning Tree Protocol"))功能，以避免产生潜在的桥接环路。You can automatically enable STP by appending `POST_UP="brctl stp $INTERFACE on"` to the netcfg profile.

### 客户机配置

现在可以在虚拟机中激活**桥接网卡**了。

如果还有其它的 Linux 虚拟机要使用这个桥接网卡，可以把下面这段代码复制到该虚拟机的**.xml**配置文件中：

```
 [...]
 <interface type='bridge'>
   <source bridge='br0'/>
   <mac address='24:42:53:21:52:49'/>
   <model type='virtio' />
 </interface>
 [...]

```

这段代码在虚拟机中激活了一个**virtio**设备，因而在Windows虚拟机中需要为它安装额外的驱动程序(位于[Windows KVM VirtIO drivers](http://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers))或者移去`<model type='virtio' />`这行：

```
 [...]
 <interface type='bridge'>
   <source bridge='br0'/>
   <mac address='24:42:53:21:52:49'/>
 </interface>
 [...]

```

## 参阅

*   [libvirt 网站](http://libvirt.org/drvqemu.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Libvirt_(简体中文)&oldid=414864](https://wiki.archlinux.org/index.php?title=Libvirt_(简体中文)&oldid=414864)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [Virtualization (简体中文)](/index.php/Category:Virtualization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Virtualization (简体中文)")
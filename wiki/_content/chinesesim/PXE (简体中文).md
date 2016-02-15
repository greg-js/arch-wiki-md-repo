**翻译状态：** 本文是英文页面 [PXE](/index.php/PXE "PXE") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=PXE&diff=0&oldid=332953)可以查看翻译后英文页面的改动。

[维基百科：预启动执行环境](https://en.wikipedia.org/wiki/Preboot_Execution_Environment "wikipedia:Preboot Execution Environment")：

	_预启动执行环境（Preboot eXecution Environment，PXE，也被称为预执行环境)提供了一种使用网络接口（Network Interface）启动计算机的机制。这种机制让计算机的启动可以不依赖本地数据存储设备（如硬盘）或本地已安装的操作系统。_

在本指南中，PXE 用于通过支持 PXE 的 Option ROM 在目标机器上启动安装介质。

## Contents

*   [1 准备](#.E5.87.86.E5.A4.87)
*   [2 服务器搭建](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.90.AD.E5.BB.BA)
    *   [2.1 网络](#.E7.BD.91.E7.BB.9C)
    *   [2.2 DHCP + TFTP](#DHCP_.2B_TFTP)
    *   [2.3 HTTP](#HTTP)
*   [3 安装](#.E5.AE.89.E8.A3.85)
    *   [3.1 启动](#.E5.90.AF.E5.8A.A8)
    *   [3.2 启动后工作](#.E5.90.AF.E5.8A.A8.E5.90.8E.E5.B7.A5.E4.BD.9C)
*   [4 备用方法](#.E5.A4.87.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [4.1 NFS](#NFS)
    *   [4.2 NBD](#NBD)
    *   [4.3 小内存](#.E5.B0.8F.E5.86.85.E5.AD.98)

## 准备

从[here 这里](https://www.archlinux.org/download/)下载最新的官方安装镜像并挂载：

```
# mkdir -p /mnt/archiso
# mount -o loop,ro archlinux-2013.11.01-dual.iso /mnt/archiso
```

## 服务器搭建

为了配置网络、加载 pxelinux/kernel/initramfs 并最终加载根文件系统，您需要分别搭建 DHCP、IFTP 和 HTTP 服务器。

### 网络

激活网卡，并分配一个合适的地址。

```
# ip link set eth0 up
# ip addr add 192.168.0.1/24 dev eth0
```

### DHCP + TFTP

为了在安装目标上配置网络并在 PXE 服务端和客户端之间传输文件，需要搭建 DHCP 和 TFTP 服务器；dnsmasq 能做到这两点，也很容易配置。

从[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq)。

配置 dnsmasq：

 `# /etc/dnsmasq.conf` 

```
port=0
interface=eth0
bind-interfaces
dhcp-range=192.168.0.50,192.168.0.150,12h
dhcp-boot=/arch/boot/syslinux/lpxelinux.0
dhcp-option-force=209,boot/syslinux/archiso.cfg
dhcp-option-force=210,/arch/
enable-tftp
tftp-root=/mnt/archiso
```

参见 `dnsmasq` [systemd 服务](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)").

### HTTP

[ArchISO](/index.php/Archiso_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Archiso (简体中文)")的改进使其能从 HTTP（archiso_pxe_http initcpio hook）或 NFS（archiso_pxe_nfs initcpio hook）启动；在所有备选方案中，darkhttpd 是最容易设置的（也是最轻量的）。

首先，从[官方软件仓库](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd)。

然后用`/mnt/archiso`作文件根目录并启动 [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd)：

 `# darkhttpd /mnt/archiso --no-keepalive` 

```
darkhttpd/1.8, copyright (c) 2003-2011 Emil Mikulic.
listening on: http://0.0.0.0:80/
```

## 安装

在本小节，您需要知道如何让客户端进行 PXE 启动。屏幕显示 POST 信息时，某个角落通常会有提示，按哪个键进行 PXE 启动。在 IBM x3650 上，_F12_ 会调出启动菜单，第一个选项就是 _Network_；在 Dell PE 1950/2950 上，按下 _F12_ 会直接开始 PXE 启动。

### 启动

通过[journald](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.97.A5.E5.BF.97 "Systemd (简体中文)")，可以查看 PXE 服务器早期 PXE 启动过程的信息：

 `# journalctl -u dnsmasq -f` 

```
dnsmasq-dhcp[2544]: DHCPDISCOVER(eth1) 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPOFFER(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPREQUEST(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPACK(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/pxelinux.0 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/whichsys.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_choose.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/ifcpu64.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_both_inc.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_head.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe32.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe64.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_tail.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/vesamenu.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/splash.png to 192.168.0.110
```

加载完 `pxelinux.0` 和 `archiso.cfg` 文件后，您会看到 [syslinux](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 启动菜单。

根据 CPU 构架，选择 _Boot Arch Linux (x86_64) (HTTP)_ 或 _Boot Arch Linux (i686) (HTTP)_。

接着会传送内核和 initramfs：

```
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/vmlinuz to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/archiso.img to 192.168.0.110
```

如果一切顺利，就能从 PXE 目标机器上看到 darkhttpd 活动了：这时，内核就能在 PXE 目标机器上加载并初始化：

```
1348347586 192.168.0.110 "GET /arch/aitab" 200 678 "" "curl/7.27.0"
1348347587 192.168.0.110 "GET /arch/x86_64/root-image.fs.sfs" 200 107860206 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/x86_64/usr-lib-modules.fs.sfs" 200 36819181 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/any/usr-share.fs.sfs" 200 63693037 "" "curl/7.27.0"
```

根文件系统下载完后就能看到使用 [grml](https://www.archlinux.org/packages/extra/any/grml-zsh-config/) 的 [zsh](/index.php/Zsh "Zsh") 的提示符了。

### 启动后工作

除非想让所有流量都走 PXE 服务器（没有[恰当的配置](/index.php/Simple_stateful_firewall#Setting_up_a_NAT_gateway "Simple stateful firewall")这是不可能的），请停止 [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 服务并在新安装的系统上重新获取适合当前网络架构的租约。

```
systemctl stop dnsmasq.service

```

您也可以关闭 [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd)；因为目标机器已经下载好根文件系统了，它也就不再需要了。同时您也可以卸载安装镜像了：

```
# umount /mnt/archiso

```

接着请跳转至[安装指南](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")。

## 备用方法

syslinux 菜单中暗含着其他方法：

### NFS

您需搭建 [NFS 服务器](/index.php/NFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NFS (简体中文)")并将安装镜像的挂载点作为出口（export）。如果您按照[前面的小节](#Preparation)做了的话，出口就是 `/mnt/archiso`。服务器搭建起来后，往 `/etc/exports` 写入这行：

 `/etc/exports`  `/mnt/archiso 192.168.0.0/24(ro,no_subtree_check)` 

如果服务器已经在运行了，用`exportfs -r -a -v` 重新导入文件系统。

安装程序会在 `/run/archiso/bootmnt` 查找 NFS，因此您需要编辑启动选项。在启动菜单按下 Tab 修改 `archiso_nfs_srv`：

 `archiso_nfs_srv=${pxeserver}:/mnt/archiso` 

或者，您也可以整个过程中都使用 `/run/archiso/bootmnt`。

在内核加载后，Arch bootstrap 镜像会复制根文件系统到引导主机（booting host）。这需要一定的额时间。一旦复制完成，您就有可运作的系统了。

### NBD

安装 [nbd](https://www.archlinux.org/packages/?name=nbd) 并配置：

 `# vim /etc/nbd-server/config` 

```
[generic]
[archiso]
    readonly = true
    exportname = /srv/archlinux-2013.02.01-dual.iso
```

### 小内存

`copytoram` [initramfs](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)") 选项可以控制是否在启动时将根文件系统整个复制到内存中。

强烈建议不去改动该选项，且只在必要的时候禁用（物理内存小于 ~256MB）。 如果要这么做，向内核参数加入 `copytoram=n`。请注意，该选项不支持通过 HTTP 传输文件；必须使用 NFS 或 NBD。
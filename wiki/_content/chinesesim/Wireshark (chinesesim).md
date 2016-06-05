**翻译状态：** 本文是英文页面 [Wireshark](/index.php/Wireshark "Wireshark") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-04，点击[这里](https://wiki.archlinux.org/index.php?title=Wireshark&diff=0&oldid=416216)可以查看翻译后英文页面的改动。

Wireshark 是一款免费开源的包分析器。可用于网络排错、网络分析、软件和通讯协议开发以及教学等。Wireshark 原名 Ethereal，2006年五月该项目因商标纠纷而改名。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 以普通用户身份抓包](#.E4.BB.A5.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E8.BA.AB.E4.BB.BD.E6.8A.93.E5.8C.85)
    *   [2.1 将用户加入 wireshark 组](#.E5.B0.86.E7.94.A8.E6.88.B7.E5.8A.A0.E5.85.A5_wireshark_.E7.BB.84)
    *   [2.2 使用 sudo](#.E4.BD.BF.E7.94.A8_sudo)
*   [3 一些抓包技巧](#.E4.B8.80.E4.BA.9B.E6.8A.93.E5.8C.85.E6.8A.80.E5.B7.A7)
    *   [3.1 过滤 TCP 包](#.E8.BF.87.E6.BB.A4_TCP_.E5.8C.85)
    *   [3.2 过滤 UDP 包](#.E8.BF.87.E6.BB.A4_UDP_.E5.8C.85)
    *   [3.3 过滤指定 IP 地址的包](#.E8.BF.87.E6.BB.A4.E6.8C.87.E5.AE.9A_IP_.E5.9C.B0.E5.9D.80.E7.9A.84.E5.8C.85)

## 安装

The wireshark package has been split into the CLI version as well as GTK and Qt frontends, which depend on the CLI.

CLI version can be [installed](/index.php/Pacman "Pacman") with the package [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli), available in the [official repositories](/index.php/Official_repositories "Official repositories").

GTK frontend can be [installed](/index.php/Pacman "Pacman") with the package [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk), available in the [official repositories](/index.php/Official_repositories "Official repositories").

Qt frontend can be [installed](/index.php/Pacman "Pacman") with the package [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## 以普通用户身份抓包

Running Wireshark as root is insecure.

Arch Linux uses [method from Wireshark wiki](http://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods) to separate privileges. When [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) is installed, [install script](/index.php/PKGBUILD#install "PKGBUILD") sets `/usr/bin/dumpcap` capabilities.

 `$ getcap /usr/bin/dumpcap`  `/usr/bin/dumpcap = cap_net_admin,cap_net_raw+eip` 

`/usr/bin/dumpcap` is the only process that has privileges to capture packets. `/usr/bin/dumpcap` can only be run by root and members of the `wireshark` group.

There are two methods to capture as a normal user :

### 将用户加入 wireshark 组

To use wireshark as a normal user, add user to the wireshark group:

 `# gpasswd -a *username* wireshark` 

To make your session aware of this new group without having to log in again, you can use this command before launching wireshark:

 `$ newgrp wireshark` 

### 使用 sudo

You can use [sudo](/index.php/Sudo "Sudo") to temporarily change group to `wireshark`. The following line allows all users in the wheel group to run programs with GID set to wireshark GID:

 `%wheel ALL=(:wireshark) /usr/bin/wireshark, /usr/bin/tshark` 

Then run wireshark with

 `$ sudo -g wireshark wireshark` 

## 一些抓包技巧

There are a number of different ways to capture exactly what you are looking for in Wireshark, by applying filters.

**Note:** To learn the filter syntax, see man pcap-filter(7).

### 过滤 TCP 包

If you want to see all the current TCP packets, type `tcp` into the "Filter" bar.

### 过滤 UDP 包

If you want to see all the current UDP packets, type `udp` into the "Filter" bar.

### 过滤指定 IP 地址的包

*   If you would like to see all the traffic going to a specific address, enter `ip.dst == 1.2.3.4`, replacing `1.2.3.4` with the IP address the outgoing traffic is being sent to.

*   If you would like to see all the incoming traffic for a specific address, enter `ip.src == 1.2.3.4`, replacing `1.2.3.4` with the IP address the incoming traffic is being sent to.

*   If you would like to see all the incoming and outgoing traffic for a specific address, enter `ip.addr == 1.2.3.4`, replacing `1.2.3.4` with the relevant IP address.
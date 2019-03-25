**翻译状态：** 本文是英文页面 [Wireshark](/index.php/Wireshark "Wireshark") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-14，点击[这里](https://wiki.archlinux.org/index.php?title=Wireshark&diff=0&oldid=438097)可以查看翻译后英文页面的改动。

Wireshark 是一款免费开源的包分析器。可用于网络排错、网络分析、软件和通讯协议开发以及教学等。Wireshark 原名 Ethereal，2006年五月该项目因商标纠纷而改名。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 以普通用户身份抓包](#以普通用户身份抓包)
    *   [2.1 将用户加入 wireshark 组](#将用户加入_wireshark_组)
    *   [2.2 使用 sudo](#使用_sudo)
*   [3 一些抓包技巧](#一些抓包技巧)
    *   [3.1 过滤 TCP 包](#过滤_TCP_包)
    *   [3.2 过滤 UDP 包](#过滤_UDP_包)
    *   [3.3 过滤指定 IP 地址的包](#过滤指定_IP_地址的包)

## 安装

wireshark 软件包分成了 CLI 版本和依赖 CLI 版本的 GTK，Qt 前端界面.

*   CLI 版本 - [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli).
*   GTK 前端 - [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk).
*   Qt 前端 - [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt).

## 以普通用户身份抓包

以 root 身份运行 Wireshark 是不安全的。Arch Linux 使用 [Wireshark wiki](http://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods) 提供的方法分离权限。[wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) 的 [安装脚本](/index.php/PKGBUILD#install "PKGBUILD") 会设置 `/usr/bin/dumpcap` capabilities.

 `$ getcap /usr/bin/dumpcap`  `/usr/bin/dumpcap = cap_net_admin,cap_net_raw+eip` 

`/usr/bin/dumpcap` 是唯一有权限进行数据包抓取的进程，仅能被 root 或 `wireshark` 群组用户执行。有两种方式可以让普通用户能够抓包: :

### 将用户加入 wireshark 组

将用户加入 wireshark 群组：

 `# gpasswd -a *username* wireshark` 

可以用下面命令不重新登录就可以执行 wireshark:

 `$ newgrp wireshark` 

### 使用 sudo

可以用 [sudo](/index.php/Sudo "Sudo") 临时将群组切换为`wireshark`. 下面 sudo 设置允许所有 wheel 群组中的用户用 wireshark GID： group to run programs with GID set to wireshark GID:

 `%wheel ALL=(:wireshark) /usr/bin/wireshark, /usr/bin/tshark` 

启动 wireshark:

 `$ sudo -g wireshark wireshark` 

## 一些抓包技巧

用一些过滤参数可以抓到你想要的包，过滤器语法请参考 man pcap-filter(7).

### 过滤 TCP 包

只想看到 TCP 数据包，在 "Filter" 拦输入 `tcp`。

### 过滤 UDP 包

只想看到 UDP 数据包，在 "Filter" 拦输入 `udp`。

### 过滤指定 IP 地址的包

将 `1.2.3.4` 替换为要查看的 IP 地址。

*   只想查看发到某个特定地址的数据包，输入 `ip.dst == 1.2.3.4`。

*   只想查看从某个特定地址发出的数据包，输入 `ip.src == 1.2.3.4`。

*   要查看某个特定地址的所有数据包，输入 `ip.addr == 1.2.3.4`。
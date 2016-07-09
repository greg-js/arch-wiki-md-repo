**翻译状态：** 本文是英文页面 [Virtual_Private_Server](/index.php/Virtual_Private_Server "Virtual Private Server") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-1-19，点击[这里](https://wiki.archlinux.org/index.php?title=Virtual_Private_Server&diff=0&oldid=356784)可以查看翻译后英文页面的改动。

摘自 [Wikipedia:Virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server "wikipedia:Virtual private server"):

	*Virtual private server (VPS) is a term used by Internet hosting services to refer to a virtual machine. The term is used for emphasizing that the virtual machine, although running in software on the same physical computer as other customers' virtual machines, is in many respects functionally equivalent to a separate physical computer, is dedicated to the individual customer's needs, has the privacy of a separate physical computer, and can be configured to run server software.*

本文主要讨论Arch Linux在VPS方面的应用, 并且包括了一些VPS的详细的安装于维护的指南.

**警告:** systemd从版本205开始就不再支持Linux 2.6.32了(system-212或更高的版本也不行). 因为很多基于容器的虚拟环境依赖较老版本的内核, 在这样的环境下想要保证Arch Linux 随时都是最新版本是不现实的. 然而截止[kernel build 042stab094.7](http://openvz.org/Download/kernel/rhel6/042stab094.7), OpenVZ已经对 CLOCK_BOOTTIME 特性进行了backport, 并且现在他可以和最新的systemd一起正常运行.

## Contents

*   [1 支持Arch Linux的提供商](#.E6.94.AF.E6.8C.81Arch_Linux.E7.9A.84.E6.8F.90.E4.BE.9B.E5.95.86)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 KVM](#KVM)
    *   [2.2 OpenVZ](#OpenVZ)
        *   [2.2.1 在任意OpenVZ提供商上安装Arch Linux](#.E5.9C.A8.E4.BB.BB.E6.84.8FOpenVZ.E6.8F.90.E4.BE.9B.E5.95.86.E4.B8.8A.E5.AE.89.E8.A3.85Arch_Linux)
            *   [2.2.1.1 前置知识](#.E5.89.8D.E7.BD.AE.E7.9F.A5.E8.AF.86)
            *   [2.2.1.2 搭建一个干净的Arch Linux](#.E6.90.AD.E5.BB.BA.E4.B8.80.E4.B8.AA.E5.B9.B2.E5.87.80.E7.9A.84Arch_Linux)
            *   [2.2.1.3 把VPS上的所有东西都Arch Arch掉](#.E6.8A.8AVPS.E4.B8.8A.E7.9A.84.E6.89.80.E6.9C.89.E4.B8.9C.E8.A5.BF.E9.83.BDArch_Arch.E6.8E.89)
            *   [2.2.1.4 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.3 Xen](#Xen)

## 支持Arch Linux的提供商

**警告:** 我们无法为提供商的质量与诚信做担保. 请在下订单前自行进行调查.

**注意:** 这个列表只列出了那些提供便捷的Arch Linux模板的提供商. 在其他提供商的环境中试用Arch Linux仍然是可行的, 只是相比之下需要更多的工作. 比如我们可以加载自定义的光盘映像 (这需要硬件层面的虚拟化, 比如Xen or KVM), [installing under chroot](/index.php/Installation_guide "Installation guide"), 或者 [using rsync to synchronize Arch over the top of another distribution](/index.php/Virtual_Private_Server#Installing_the_latest_Arch_Linux_on_any_OpenVZ_provider "Virtual Private Server").

| 提供商名 | Arch 版本 | 虚拟化环境 | 地理地点 | 注意事项 |
| [A MilesWeb VPS](http://www.milesweb.com/vps-hosting.php) | 2013.10.14 | OpenVZ | 欧洲, 印度, 美利坚 | Latest Arch Linux available on OpenVZ platform. Quick setup, 24/7 support via Live Chat, Email and Phone. VPS starts from $20 / mo |
| [123 Systems](http://123systems.net) | 2010.05.xx | OpenVZ | 达拉斯, 美国-德克萨斯 | Arch available as a selection upon reinstall. Very old (2.6.18-308) kernel - See [OpenVZ troubleshooting](/index.php/Virtual_Private_Server#OpenVZ:_kernel_too_old_for_glibc "Virtual Private Server"). Limited information available before purchase. Cannot verify Arch Linux version without purchase. |
| [AUSWEB](http://ausweb.com.au) | 一律最新 (啥?) | VMware ESXi | 悉尼, 澳大利亚 | Latest ISO (clarify?) of Arch Available. Enterprise Service. |
| [affinity.net.nz](https://www.affinity.net.nz) | 2013.08.01 | KVM | 奥克兰, 新西兰 | IRC channel is #affinity on ircs.kiwicon.org |
| [Afterburst](http://afterburst.com/) | 2012.12.01 | OpenVZ | 迈阿密, 美国-佛罗里达; 纽伦堡, 德国 | Formerly FanaticalVPS, kernel version depends on what node your VPS is on, the ones in Miami are fine (2.6.32-042stab072.10) but some of the ones in Germany require a [custom glibc](/index.php/Virtual_Private_Server#OpenVZ:_kernel_too_old_for_glibc "Virtual Private Server"). |
| [BuyVM](http://www.buyvm.net/) | 2013.07.01 | KVM | 洛杉矶, 水牛城 纽约 | Must chose a different OS at sign up. Once accessible, choose to mount the latest Arch ISO and reboot to install manually. |
| [Edis](http://en.edis.at/) | [2013.03.01](http://www.edis.at/en/support-and-service/faq/server-faq/which-distributions-are-available-with-edis-kvm-vps-plans/) | vServer, KVM, OpenVZ | [大量国际节点](http://www.edis.at/en/server/kvm-vps/austria/). | Also offer dedicated server options as well as an "off-shore" location at the Isle of Man (IM). |
| [DirectVPS](https://www.directvps.nl/) | 2014.01.xx | OpenVZ | 阿姆斯特丹, 荷兰; 洛特丹, 荷兰 | Dutch language site. Version verifyable by clicking through [https://www.directvps.nl/try-1.plp?p=31](https://www.directvps.nl/try-1.plp?p=31) |
| [Gandi](https://www.gandi.net/hosting/) | 2013.10.27 | Xen | 巴黎, 法国; 巴尔地摩, 马里兰, 美国; 比森, 卢森堡 | Very granular scaling of system resources (e.g. RAM, disk space); IPv6-only option available; you can supply your own install image, version based on keyring package version |
| [GigaTux](https://www.gigatux.com/virtual.php) | [2013.06.01](https://www.gigatux.com/distro/) | Xen | 芝加哥, 美国-伊利诺伊; 法兰克福, 德国, 伦敦, 大不列颠; 圣琼斯, 美国-加州 |
| [Host Virtual](http://www.vr.org/) | [2011.08.19](http://www.vr.org/os/linux-vps/archlinux-vps) | KVM | [大量国际节点](http://www.vr.org/cloud-locations/) | Appears to use KVM virtualization. Site lists "Xen based virtualization" and [features](http://www.vr.org/features/) lists ability to install from ISO. |
| [Hostigation](https://hostigation.com/) | [2010.05 i686](https://hostigation.com/wiki/index.php?title=KVM:Install) | OpenVZ, KVM | 夏洛特, 美国-北卡; 洛杉矶, 美国-加州 | You can [migrate to x86_64](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling"). |
| [IntoVPS](http://www.intovps.com) | 2012.09.xx | OpenVZ | 阿姆斯特丹, 荷兰; 布加列斯特, 罗马尼亚; 达拉斯, 美国-德克萨斯; 费利蒙, 美国-加州; 伦敦, 大不列颠 | Blog has not been updated since September, 2012 which included the Arch Linux update. |
| [Leapswitch Networks](https://leapswitch.com) | [2013.10.xx] | OpenVZ/KVM | 美利坚, 印度, 葡萄牙, 西班牙, 乌克兰, 德国 | ArchLinux currently available in Control Panel for reinstall, not on order form. |
| [Linode.com](https://www.linode.com) | [2013.06.xx](https://www.linode.com/faq.cfm) | Xen | [东京, 日本; 美国; 伦敦, 大不列颠](https://www.linode.com/speedtest/) | To run a custom kernel, install [linux-linode](https://aur.archlinux.org/packages/linux-linode/). ([linux](https://www.archlinux.org/packages/?name=linux) will break on a 32-bit Linode.) |
| [LYLIX](http://lylix.net/) | [2014.01.xx](http://lylix.net/archlinux) | OpenVZ | 美利坚; 欧洲 | 32-bit and 64-bit available |
| [Node Deploy](http://www.nodedeploy.com) | 2014.10.01 | OpenVZ, KVM | 德国; 洛杉矶, 美国-加州; 亚特兰大, 美国-佐治亚; 凤凰城, 美国-亚利桑那 | "At NodeDeploy we support virtually every linux distribution." Arch Linux is listed under their Operating Systems. No version information. |
| [Netcup](http://netcup.de) | 2012.11.xx | KVM | 德国 | German language site. |
| [OnePoundWebHosting](http://onepoundwebhosting.co.uk) | 2013.05.xx | Xen PV, Xen HVM | 英国 | They are a registrar too. Unable to verify server locations. |
| [proPlay.de](https://www.proplay.biz/) | 2012.12.xx | OpenVZ, KVM | 德国 | German language site. |
| [QuickVZ](https://www.quickvz.com) | 2013.10 | OpenVZ, Xen | 阿姆斯特丹, 荷兰; 斯德哥尔摩, 瑞典 | Provide hardened Arch Linux images along with Enterprise services (e,g. VPN, Virtual Private LAN Service (VPLS) and Virtual Routers. |
| [Rackspace Cloud](http://www.rackspace.com/cloud/cloud_hosting_products/servers/) | 2013.6 | Xen | [大量国际节点](https://www.rackspace.com/whyrackspace/network/datacenters/) | Billed per hour. Use their "next gen" VPSes (using the mycloud.rackspace.com panel); the Arch image on the first gen Rackspace VPSes is out of date. |
| [RamHost.us](http://www.ramhost.us) | [2013.05.01](http://www.ramhost.us/?page=news) | OpenVZ, KVM | 洛杉矶, 美国-加州; 大不列颠; 亚特兰大, 美国-佐治亚; 德国 | You can request a newer ISO on RamHost's IRC network. |
| [RamNode](http://www.ramnode.com) | [2013.07.01](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=48) | [SSD and SSD Cached:](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=39) [OpenVZ, KVM](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=52) | [西雅图, 华盛顿 美国, 亚特兰大, 佐治亚 美国](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=18) | You can request Host/CPU passthrough with KVM service.[[1]](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=66) Frequent use of discount promotions.[[2]](https://twitter.com/search?q=ramnode%20code&src=typd) |
| [Tilaa](http://www.tilaa.nl/) | 2014.10.01 | [KVM](https://www.tilaa.com/pages/vps/technology) | 阿姆斯特丹, 荷兰 | English or Dutch language site. |
| [TransIP](https://www.transip.eu/) | [2013.05.01](https://www.transip.eu/vps/vps-os/) | [KVM](https://www.transip.eu/vps/vps-technology/) | 阿姆斯特丹, 荷兰 | English language site. Registrar. |
| [XenVZ](http://www.xenvz.co.uk/) | 2009.12.07 | OpenVZ, Xen | 英国, 美利坚 | [Hardware](http://www.xenvz.co.uk/faq.php#use2) |
| [Virpus](http://www.virpus.com/) | [2014.11.07](http://virpus.com/linux-vps.php) | Xen | 堪萨斯城, 美国-堪萨斯; 洛杉矶, 美国-加州 | A subcompany of Wow Technologies, Inc. 24/7 support via Live Chat, Email, Phone, and Ticket System. Service starts at $5/month. |
| [Vmline](http://www.vmline.pl/) | 2013.09.01 | KVM, OpenVZ | 克拉科夫, 波兰 | [S-Net](http://www.s-net.pl/en/) reseller. Full virtualization. Polish language site. |
| [VPSBG.eu](https://vpsbg.eu/) | 2013.10 | OpenVZ | [索菲亚, 保加利亚](https://vpsbg.eu/en/index.php?page=vps-datacenter) | Offshore VPS in Bulgaria - anonymous registrations and Bitcoin are accepted. |
| [VPS6.NET](https://vps6.net/) | 2013.01.xx | OpenVZ, Xen, HVM-ISO | [美国](http://vps6.net/network/); 法兰克福, 德国; 布加列斯特, 罗马尼亚; 伊斯坦布尔, 土耳其 | Registrar. |
| [VPS.NET](http://www.vps.net/) | 2014.01.xx | OpenVZ, Xen, HVM-ISO | [US, 加拿大, 英国, 巴西, 荷兰, 法国, 德国, 日本, 新加坡, 印度, 澳大利亚](http://vps.net/cloud-datacenter-locations) | Managed & Un managed VPS service provider, multiple OS and configurations.. |

## 安装

### KVM

参阅 [QEMU#Preparing an (Arch) Linux guest](/index.php/QEMU#Preparing_an_.28Arch.29_Linux_guest "QEMU").

### OpenVZ

#### 在任意OpenVZ提供商上安装Arch Linux

**警告:** 阅读 [最上的警告](#top) 来了解关于较老版本内核和systemd的相关信息.

It's possible to directly copy an installation of Arch Linux over the top of a working OpenVZ VPS. This tutorial explains how to create a basic installation of Arch Linux with `pacstrap` (as used in a standard install) and then replace the contents of a target VPS with it using [rsync](/index.php/Rsync "Rsync").

This process (with minor modification) also works to migrate existing Arch installations between various environments and has been confirmed to work in migrating from OpenVZ to Xen and from Xen to OpenVZ. For an install to Xen, other hardware-virtualized platforms, or probably even to physical hardware (unconfirmed), extra steps (basically running `mkinitcpio` and [installing a bootloader](/index.php/Boot_loaders "Boot loaders")) are needed.

##### 前置知识

*   A working Arch Linux installation
    *   To keep things simple, it should match the architecture you want to install on your VPS (x86_64 or i686).
    *   To build from other distributions, [arch-bootstrap.sh](/index.php/Archbootstrap "Archbootstrap") can be used in place of `pacstrap`.
*   The [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), [rsync](https://www.archlinux.org/packages/?name=rsync), and [openssh](https://www.archlinux.org/packages/?name=openssh) packages from the [official repositories](/index.php/Official_repositories "Official repositories")
    *   SSH isn't strictly required, but rsync over SSH is the method used here.
*   A VPS running any distribution, with `rsync` and a working SSH server
    *   Its architecture (x86_64 or i686) doesn't matter as long as the OpenVZ installation can support your target architecture.
*   OpenVZ's serial console feature (usually accessible via your provider's control panel)
    *   Without this, any network configuration for the target VPS will have to be done immediately after the "Build" step below.

##### 搭建一个干净的Arch Linux

As root, build the installation (optionally replacing `build` with your preferred target directory):

```
# mkdir build
# pacstrap -cd build

```

Other tweaks for the `pacstrap` command:

*   `-C custom-pacman-config.conf` - Use a custom pacman configuration file. By default, pacstrap builds according to your local pacman.conf. This determines the architecture (i686 or x86_64) of the build, the mirror list, etc.
*   `-B` - Prevent pacstrap from copying your system's pacman keyring to the new build. If you use this option, you'll need to run `pacman-key --init` and `pacman-key --populate archlinux` in the [Configuration](/index.php/Virtual_Private_Server#Configuration "Virtual Private Server") step to set up the keyring.
*   `-M` - Prevent pacstrap from copying your system's pacman mirror list to the new build.

##### 把VPS上的所有东西都Arch Arch掉

把目标VPS上所有的文件, 目录和其它各种东西都用你的`build`目录的内容替换掉 (把下面的 "YOUR.VPS.IP.ADDRESS" 换掉):

**警告:** 处理下面的命令的时候当心点. `rsync`这个命令根据设计就是极具毁灭性的, 特别是带上 `--delete` 选项的时候.

```
# rsync -ax --delete-delay -e ssh --stats -P build/ YOUR.VPS.IP.ADDRESS:/

```

选项的解释:

At minimum, only the `-a` (preserve timestamps, permissions, etc.), `-x` (don't cross filesystem boundaries), and `--delete` (delete anything in the target that doesn't exist in the source) options are required. The `--delete-delay` option is an alternate deletion mode which waits to delete anything until the synchronization is otherwise complete; this isn't necessary but may reduce the risk of a slow transfer causing the target VPS to lock-up. The `-e ssh` (use rsync over SSH) option is recommended and makes things simple. The `--stats` and `-P` options are just to show more information.

##### 配置

1.  将VPS从外部重启 (比如你可以利用provider的控制面板来干这件事).
2.  使用 OpenVZ 的端口控制特性来配置 [网络](/index.php/Network_configuration "Network configuration") 和 [基本系统设定](/index.php/Installation_guide#Configure_the_system "Installation guide") (无视 fstab 的生成和 arch-chroot 的相关步骤).
    *   如果你接触不到端口控制特性, 那你在把Arch Linux同步到VPS前就提前配置好你的网络设定.

### Xen

参阅 [Xen#Arch as Xen guest (PVHVM mode)](/index.php/Xen#Arch_as_Xen_guest_.28PVHVM_mode.29 "Xen") 及/或 [Xen#Arch as Xen guest (PV mode)](/index.php/Xen#Arch_as_Xen_guest_.28PV_mode.29 "Xen").
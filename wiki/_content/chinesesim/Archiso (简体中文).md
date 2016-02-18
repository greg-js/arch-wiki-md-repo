**翻译状态：** 本文是英文页面 [Archiso](/index.php/Archiso "Archiso") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-08，点击[这里](https://wiki.archlinux.org/index.php?title=Archiso&diff=0&oldid=336304)可以查看翻译后英文页面的改动。

“Archiso”是一组 bash 脚本，它能够建立功能全面的基于 Arch Linux 的 Live CD 和 USB 映像。它是用来生成官方 CD/USB 映像的工具，但它是一个非常通用的工具，并且它可以——潜在地——被用来生成从救援系统、安装盘，到特殊爱好的 Live CD/DVD/USB 系统——无人知晓还有其他什么。简单地说，如果要将 Arch 放在一条闪光的船上，它可以帮你做到这一点。Archiso 的核心以及灵魂是 mkarchiso。它的所有选项都写在它的用法输出上，所以它的直接使用方法将不在这里讨论。相反，这篇 wiki 文章将导引你迅速建立你的 Live 介质。

## Contents

*   [1 安装和配置](#.E5.AE.89.E8.A3.85.E5.92.8C.E9.85.8D.E7.BD.AE)
*   [2 配置我们的Live介质](#.E9.85.8D.E7.BD.AE.E6.88.91.E4.BB.AC.E7.9A.84Live.E4.BB.8B.E8.B4.A8)
    *   [2.1 安装包](#.E5.AE.89.E8.A3.85.E5.8C.85)
        *   [2.1.1 自定义本地库](#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.9C.AC.E5.9C.B0.E5.BA.93)
        *   [2.1.2 避免安装属于base组的包](#.E9.81.BF.E5.85.8D.E5.AE.89.E8.A3.85.E5.B1.9E.E4.BA.8Ebase.E7.BB.84.E7.9A.84.E5.8C.85)
    *   [2.2 添加账户](#.E6.B7.BB.E5.8A.A0.E8.B4.A6.E6.88.B7)
    *   [2.3 向映像里添加文件](#.E5.90.91.E6.98.A0.E5.83.8F.E9.87.8C.E6.B7.BB.E5.8A.A0.E6.96.87.E4.BB.B6)
    *   [2.4 aitab](#aitab)
    *   [2.5 mkinitcpio.conf](#mkinitcpio.conf)
    *   [2.6 引导器](#.E5.BC.95.E5.AF.BC.E5.99.A8)
    *   [2.7 登录管理器](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.8 改变自动登录状态](#.E6.94.B9.E5.8F.98.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95.E7.8A.B6.E6.80.81)
*   [3 构建ISO](#.E6.9E.84.E5.BB.BAISO)
    *   [3.1 重建ISO](#.E9.87.8D.E5.BB.BAISO)
*   [4 使用ISO](#.E4.BD.BF.E7.94.A8ISO)
    *   [4.1 CD](#CD)
    *   [4.2 USB](#USB)
    *   [4.3 grub4dos](#grub4dos)
*   [5 安装](#.E5.AE.89.E8.A3.85)
    *   [5.1 在沒有互联网连接的情况下安装Archiso](#.E5.9C.A8.E6.B2.92.E6.9C.89.E4.BA.92.E8.81.94.E7.BD.91.E8.BF.9E.E6.8E.A5.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E5.AE.89.E8.A3.85Archiso)
        *   [5.1.1 安装 archiso 到新的根](#.E5.AE.89.E8.A3.85_archiso_.E5.88.B0.E6.96.B0.E7.9A.84.E6.A0.B9)
        *   [5.1.2 Chroot 并配置基本系统](#Chroot_.E5.B9.B6.E9.85.8D.E7.BD.AE.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F)
            *   [5.1.2.1 恢复 journald 的配置](#.E6.81.A2.E5.A4.8D_journald_.E7.9A.84.E9.85.8D.E7.BD.AE)
            *   [5.1.2.2 重设 pam 的配置](#.E9.87.8D.E8.AE.BE_pam_.E7.9A.84.E9.85.8D.E7.BD.AE)
            *   [5.1.2.3 移除特殊 udev 规则](#.E7.A7.BB.E9.99.A4.E7.89.B9.E6.AE.8A_udev_.E8.A7.84.E5.88.99)
            *   [5.1.2.4 禁用和移除 archiso 创建的服务](#.E7.A6.81.E7.94.A8.E5.92.8C.E7.A7.BB.E9.99.A4_archiso_.E5.88.9B.E5.BB.BA.E7.9A.84.E6.9C.8D.E5.8A.A1)
            *   [5.1.2.5 移除 Live 环境的特殊脚本](#.E7.A7.BB.E9.99.A4_Live_.E7.8E.AF.E5.A2.83.E7.9A.84.E7.89.B9.E6.AE.8A.E8.84.9A.E6.9C.AC)
            *   [5.1.2.6 修复 root 的 home 目录的权限](#.E4.BF.AE.E5.A4.8D_root_.E7.9A.84_home_.E7.9B.AE.E5.BD.95.E7.9A.84.E6.9D.83.E9.99.90)
            *   [5.1.2.7 设置 arch 的密码](#.E8.AE.BE.E7.BD.AE_arch_.E7.9A.84.E5.AF.86.E7.A0.81)
            *   [5.1.2.8 创建初始ramdisk环境](#.E5.88.9B.E5.BB.BA.E5.88.9D.E5.A7.8Bramdisk.E7.8E.AF.E5.A2.83)
            *   [5.1.2.9 常规配置](#.E5.B8.B8.E8.A7.84.E9.85.8D.E7.BD.AE)
*   [6 另请参见](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E8.A7.81)

## 安装和配置

**注意:** 以下操作请在ROOT权限下使用，在错误的权限下操作会造成一下问题。

当我们开始之前, 我们需要从 [官方仓库](/index.php/Official_repositories "Official repositories") [安装](/index.php/Pacman "Pacman") [archiso](https://www.archlinux.org/packages/?name=archiso) 。除此之外，可以在 [AUR](/index.php/AUR "AUR") 中找到 [archiso-git](https://aur.archlinux.org/packages/archiso-git/)。

创建一个用于工作的目录, 实时镜像将会在这里被处理。 `~/archlive` 是一个好选择。

```
$ mkdir ~/archlive

```

现在要将早先安装到主机的 archiso 脚本复制到你新建的工作目录内。

Archiso 附带2个预定义配置（ profiles ）: *releng* 和*baseline*。

如果您想要创建完全定制的 Live Arch Linux ，并预装所有您喜爱的程序和配置，使用 *releng*。

如果您只是想构建一个简易 Live 镜像，无预装软件并仅有基础配置，那么使用 *baseline*。

所以，取决于你的需求，将下面命令中的 **PROFILE** 换成 *releng* 或是 *baseline* 并执行。

```
# cp -r /usr/share/archiso/configs/**PROFILE**/ ~/archlive

```

如果你使用 *releng* 配置文件来创建一个完全自定义的镜像，那么你可以继续到：[#配置我们的Live介质](#.E9.85.8D.E7.BD.AE.E6.88.91.E4.BB.AC.E7.9A.84Live.E4.BB.8B.E8.B4.A8)。

如果您使用 *baseline* 配置文件创建一个简易映像，那么你不需要做任何定制，并可以直接继续到[#构建ISO](#.E6.9E.84.E5.BB.BAISO).

## 配置我们的Live介质

本节详细介绍该如何配置您将创建的映像，允许您定义哪些包以及配置将被您的 Live 映像所包含。 切换到我们早些时候创建的目录 (~/archlive/releng/ 如果你一直按照本向导在执行），你将会看到若干文件和目录；我们只关注其中一部分，主要是 packages.*——在这里一行行列出你想要安装的包——和 airootfs 目录——这是一个覆盖目录，你将在这里完成所有的定制工作。 一般来说，您在全新安装之后所执行的每个管理任务（不包括软件包安装）可以被写入这个脚本： `~/archlive/releng/airootfs/root/customize-airootfs.sh`。您必须从新环境的角度来写该脚本，所以脚本中的 / 代表方才被创建的 Live ISO 的根。

### 安装包

你将在你的 Live CD 系统上创建一个列表，它包含你想要安装的包。该文件的格式为：每行一个包名，且没有其他内容。这对于某些特殊需求的 Live CD 来说很***有帮助***——仅需在 packages.both 中列出你想要的包并制作映像。你可以分别在 packages.i686 或 packages.x86_64 中列出仅在 32 位或 64 位系统中安装的软件。

若你准备在没有互联网连接的设备上安装系统，我建议你安装"rsync"，要不然就重新跳过下载它. ([#安装](#.E5.AE.89.E8.A3.85))

#### 自定义本地库

若需准备自定义包或是自 [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS") 安装包，你也可以[创建自定义本地资源库](/index.php/Custom_local_repository "Custom local repository")。当这样处理两种架构的软件包时，您应该遵循一定的目录顺序，才不会出现问题。 例如：

*   `~/customrepo`
    *   `~/customrepo/x86_64`
        *   ~/customrepo/x86_64/foo-x86_64.pkg.tar.xz
        *   ~/customrepo/x86_64/customrepo.db.tar.gz
        *   ~/customrepo/x86_64/customrepo.db (symlink created by `repo-add`)
    *   `~/customrepo/i686`
        *   ~/customrepo/i686/foo-i686.pkg.tar.xz
        *   ~/customrepo/i686/customrepo.db.tar.gz
        *   ~/customrepo/i686/customrepo.db (symlink created by `repo-add`)

如此后，您可以添加您的仓库——把下面的句子加入 `~/archlive/releng/pacman.conf`，并置于其他仓库条目上面（优先级最高）：

```
# 自定义仓库
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch

```

这样，构建脚本将会寻找合适的包。

如果不是这样，你将得到与此类似的错误消息：

```
error: failed to prepare transaction (package architecture is not valid)
:: package foo-i686 does not have a valid architecture

```

#### 避免安装属于base组的包

默认情况下，`/usr/bin/mkarchiso`——一个被 `~/archlive/releng/build.sh` 使用的脚本——会调用 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) 中一个名为 `pacstrap` 的程序，且在调用时不使用 `-i` 标志——这将使 [Pacman](/index.php/Pacman "Pacman") 在安装过程中不等待用户输入。

当 base 组软件包被加入黑名单——把它们写到 `~/archlive/releng/pacman.conf` 中的 `IgnorePkg` 行——时，[Pacman](/index.php/Pacman "Pacman") 会询问是否仍然安装它们——意味着如果用户输入被跳过，它们就会被安装。为了避免安装这些包，这里有一些选择：

*   **丑陋**方案（Dirty）：在 `/usr/bin/mkarchiso` 中每次调用 `pacstrap` 的行上加入 `i` 标志。

*   **整洁**方案（Clean）：创建 `/usr/bin/mkarchiso` 的一份复制。在该复制中增加此标志，并修改 `~/archlive/releng/build.sh` 以使其调用修改过的 mkarchiso 脚本。

*   **高级**方案（Advanced）: 在 `~/archlive/releng/build.sh` 中创建一个函数，该函数将在基础安装结束后显式移除那些包。若这样做，可以免去在安装过程中多次按回车键的麻烦。

### 添加账户

可以使用和常规安装相同的方式来管理用户——除非你把你的命令放到 `~/archlive/releng/airootfs/root/customize-airootfs.sh` 脚本中。详情参阅 [用户管理](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86 "Users and groups (简体中文)")。

### 向映像里添加文件

**注意:** 你必须使用 root 权限来完成这件事，不要改变任何你复制过来的文件的所有权，airootfs 中的**所有**文件必须为 root 用户所有。适当的所有制将在不久被解决。

airootfs 目录作为要覆盖的文件，把它看作是在当前系统上的根目录'/'，所以你在这个目录中放置的任何文件都将在开机时被复制。

所以，如果你在当前系统上有一组 iptables 脚本且想要在 Live 映像上使用，请这样复制:

```
# cp -r /etc/iptables ~/archlive/releng/airootfs/etc

```

在用户 home 文件夹里放置文件的方法有些许不同。不要把它们放在 airootfs/home，而是在 airootfs/ 里创建 skel 目录并将其放置在那里。然后我们会将相关命令添加到 customize_root_image.s——我们要使用它在引导时复制文件以及梳理权限。

首先，创建 skel 目录；确保你在 ~/archlive/releng/airootfs/etc 目录 (如果这是你工作之地):

```
# cd ~/archlive/releng/airootfs/etc && mkdir skel

```

现在，复制（预期的） 'home' 文件到 skel 目录（依然使用 root 权限做所有事！）。 例如，对于 .bashrc：

```
# cp ~/.bashrc ~/archlive/releng/airootfs/etc/skel/

```

当 `~/archlive/releng/airootfs/root/customize-airootfs.sh` 被执行，并且一个新用户已被创建, skel 目录中的文件将自动被复制到新的 home 文件夹中，并被设置正确的权限。

### aitab

默认的文件应该没有问题，所以你应该不需要去碰它。

该aitab 文件保存有关必须创建的 mkarchiso 和 initramfs 阶段从 archiso 钩挂载的文件系统映像信息。

它包含一些定义映像行为的字段。

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>

```

	<img>

	不带扩展名的映像名称 (.fs .fs.sfs .sfs).

	<mnt>

	挂载点.

	<arch>

	结构{ i686 | x86_64 | any }.

	<sfs_comp>

	SquashFS 压缩格式 { gzip | lzo | xz }.

	<fs_type>

	设置映像的文件系统格式 { ext4 | ext3 | ext2 | xfs | btrfs }. 一个特殊的值"none"表示没有使用文件系统. 在这种情况下所有文件都是直接推向 SquashFS 文件系统

	<fs_size>

	在 MiB 中的文件系统映像大小绝对值 (比如: 100, 1000, 4096, 等) 文件系统中的可用空间的相对值[百分比] {1%..99%} (比如 50%, 10%, 7%这是估计值，并以一种简单的方式计算出来。. 已用空间 + 10% (估计为元数据开销) + 所需 %

**注意:** 有些组合是无效的. 这两个示例 `sfs_comp` 和 `fs_type` 都设置为 none

### mkinitcpio.conf

默认的文件应该可以正常工作，所以你不应该需要去碰它。

一个'Initcpio ' 有必要创建一个系统，能够从 CD/DVD/USB，"唤醒"

默认列表将让你可以从CD/ DVD或USB设备的系统启动。硬件的自动检测和这种性质的东西在这里不做深入研究。只有必要让系统在它的foot部分 。“initcpio”真正属于这里，反正票友东东可以在引导系统上来完成。

### 引导器

默认的文件应该可以正常工作，所以你应该不需要去碰它。

由于 isolinux 的模块化性质，你能够使用很多插件，因为所有 *.c32 都被复制且可以可供您使用。看看[syslinux 官方网站](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) 和 [Archiso Git Repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files)。使用所述插件，便有可能做出更具视觉吸引力及复杂的菜单。参见 [此处](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32)。

### 登录管理器

通过启用您登录管理器的 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 服务来做到在引导时启动 X 。如果您知道哪一个 .service 文件需要软链接，那就太好了。如果不知道，你也可以轻松找出——如果你在创建 iso 所用的系统上使用相同的程序的话。只需使用

```
# systemctl disable **登录管理器名**

```

来暂时关闭。接下来键入相同的命令，并使用“enable”来替换“disable”以重新激活它。Systemctl 会打印它所创建软链接的信息。现在切换到 ~/archiso/releng/airootfs/etc/systemd/system，并在那里创建相同的软链接。

一个例子 (请确保你是在 ~/archiso/releng/airootfs/etc/systemd/system 或者将其添加到该命令)：

```
# ln -s /usr/lib/systemd/system/lxdm.service display-manager.service

```

这将启用 LXDM 以使其在 Live 系统启动时运行。

### 改变自动登录状态

Getty 的自动登录配置位于 airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf。

您可以修改这个文件来更改自动登录用户：

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

或者干脆删除它来禁用自动登录。

## 构建ISO

现在，你已经准备好把你的文件转换成 .iso，以便可以刻录到 CD 或 USB。

在你工作的目录内（无论是 ~/archlive/releng，还是 ~/archlive/baseline），执行：

```
# ./build.sh -v

```

该脚本将现在下载并安装你指定的软件包到 work/*/airootfs，创建内核和 init 映像（initramfs），应用您的修改，并最终把 ISO 建立到 out/。

**注意:** 如果想要在你的 Live CD 中使用[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，那么你需要添加必要且正确的[显示驱动](/index.php/Video_drivers "Video drivers")，否则窗口管理器会在载入时冻结。

### 重建ISO

如果你在进行了一些修改后，想要重建你的 ISO，你需要删除 work 目录下的一些锁文件：

```
# rm -v work/build.make_*

```

## 使用ISO

### CD

就是把 ISO 刻录到光盘。如有需要，可以看看 [CD Burning](/index.php/CD_Burning "CD Burning")。

### USB

参见 [USB flash installation media (简体中文)](/index.php/USB_flash_installation_media_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "USB flash installation media (简体中文)").

### grub4dos

Grub4dos 是一个实用程序，可以用于创建能多重引导的 usb 设备——可以从相同的 usb 棒启动多个 linux 发行版。

若要在已安装 grub4dos 的条件下从 USB 设备引导已生成的 ISO 映像，则以 loop（回环） 方式挂载 ISO ，并复制整个 `/arch` 目录到 **usb 设备的根目录**。然后编辑来自 grub4dos 的 `menu.lst` 文件（该文件必定在 usb 根目录上）并添加这些行：

```
title Archlinux x86_64
kernel /arch/boot/x86_64/vmlinuz archisolabel=<your usb label>
initrd /arch/boot/x86_64/archiso.img

```

根据需要更改 `x86_64` 部分，并把你**真实的** usb 设备标签放在这儿。

## 安装

引导你创建的CD/DVD/USB；若欲原封不动的安装Archiso，请看下面的[#离线安装范例](#.E5.9C.A8.E6.B2.92.E6.9C.89.E4.BA.92.E8.81.94.E7.BD.91.E8.BF.9E.E6.8E.A5.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E5.AE.89.E8.A3.85Archiso)。我们所讲述的方法大部分的操作步骤都与[新手指南](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' guide (简体中文)")一致，所以建议先阅读新手指南。

你也可以试试采用图形界面安装程式的[Archboot](/index.php/Archboot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Archboot (简体中文)")。

### 在沒有互联网连接的情况下安装Archiso

若你想在没有互联网连接或者你不想重复下载你想要的包的情况下安装 archiso（例如[官方的每月发布版](https://www.archlinux.org/download/)）：

首先，跟随[新手指南](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' guide (简体中文)")，并跳过一些步骤（如[#建立网络连接](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.BB.BA.E7.AB.8B.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5 "Beginners' guide (简体中文)")），直到[#安装基本系统](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F "Beginners' guide (简体中文)")之前。

#### 安装 archiso 到新的根

由于没有网络连接以从远程仓库下载每个包，我们不使用 `pacstrap`，而是复制 Live 环境的*所有文件*到新的根目录：

```
# time (cp -a /{usr,bin,lib,lib64,sbin,etc,home,opt,root,srv,var} /mnt)

```

**注意:** 这个命令排除了一些特殊目录，因为它们不应该被复制到新的根目录。

然后，创建一些目录并复制内核映像到新的根，以保证新系统的完整性：

```
# mkdir -vm755 /mnt/{boot,dev,run,mnt}
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux
# mkdir -vm1777 /mnt/tmp
# mkdir -vm555 /mnt/{sys,proc}

```

完成之后，请按[Beginners' guide (简体中文)#生成 fstab](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.94.9F.E6.88.90_fstab "Beginners' guide (简体中文)")所述生成 fstab。

#### Chroot 并配置基本系统

下一步，chroot 到您新安装的系统：

```
# arch-chroot /mnt /bin/bash

```

请注意，在您配置 locale、键盘映射等之前，你仍然需要为了避免延续 Live 环境的轨迹——或者说对 archiso 所做的一些不适用于非 Live 环境的修改——而做一些事情。

##### 恢复 journald 的配置

[archiso 的这个修改](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19)会导致日志存储在 RAM 上——它意味着在重启后日志便会丢失。为了解决这个问题，执行：

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

##### 重设 pam 的配置

[pam 的这个设置](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/pam.d/su)可能会危及您新系统的安全性，建议使用默认配置：

 `# nano /etc/pam.d/su` 
```
#%PAM-1.0
auth            sufficient      pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
**#auth           sufficient      pam_wheel.so trust use_uid**
# Uncomment the following line to require a user to be in the "wheel" group.
#auth           required        pam_wheel.so use_uid
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_unix.so

```

##### 移除特殊 udev 规则

[udev 的这个规则](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)也许对于 Live 系统和您的新系统都有用，因为它会在探测到有任何有线网络接口时启动 dhcpcd。如果您不在有线网络接口上使用 dhcpcd，可以删除它（`rm /etc/udev/rules.d/81-dhcpcd.rules`）。

##### 禁用和移除 archiso 创建的服务

有一些服务文件是为 Live 环境创建的，请禁用这些服务并移除文件——因为它们对于新系统来说没必要存在：

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

##### 移除 Live 环境的特殊脚本

Archiso 有一些脚本，并且依然对于新系统来说没有意义：

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/sudoers.d/g_wheel
# rm /etc/mkinitcpio-archiso.conf
# pacman -S --force archiso && pacman -R archiso

```

##### 修复 root 的 home 目录的权限

**注意:** 该问题已在 v17（在官方每月发布版：2014.08.01）版本被修复，除非你在使用旧版的 Live 映像。

```
# chmod 700 /root

```

##### 设置 arch 的密码

[本自定义脚本](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n13)为 Live 环境创建了一个名为 `arch` 的普通用户。你可以为它创建一个密码（默认情况下没有密码），以便使用这个用户名登录：

```
# passwd arch

```

或者，如果你不想使用这个用户名，请移除这个用户：

```
# userdel -r arch

```

##### 创建初始ramdisk环境

请按照 [Beginners' guide (简体中文)#创建初始 ramdisk 环境](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E5.88.9D.E5.A7.8B_ramdisk_.E7.8E.AF.E5.A2.83 "Beginners' guide (简体中文)")]所述创建一个初始ramdisk。

##### 常规配置

在做完这一切后，你可以继续跟随[新手指南](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Locale "Beginners' guide (简体中文)")，并完成安装。

## 另请参见

*   [Archiso project page](https://projects.archlinux.org/?p=archiso.git;a=summary)
*   [Offical documentation](https://projects.archlinux.org/archiso.git/tree/docs)
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Creating a custom Arch Linux live USB tutorial](http://blog.jak.me/2011/09/07/creating-a-custom-arch-linux-live-usb/)
*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://didjix.blogspot.com/)
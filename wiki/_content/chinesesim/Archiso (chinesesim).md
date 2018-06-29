**翻译状态：** 本文是英文页面 [Archiso](/index.php/Archiso "Archiso") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-06-27，点击[这里](https://wiki.archlinux.org/index.php?title=Archiso&diff=0&oldid=527427)可以查看翻译后英文页面的改动。

相关文章

*   [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")
*   [PXE](/index.php/PXE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PXE (简体中文)")
*   [Archboot](/index.php/Archboot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Archboot (简体中文)")

**Archiso** 是一组 bash 脚本，它能够建立功能全面的 Arch Linux 的 Live CD/DVD/USB 映像。它同样是用来生成官方映像的工具，但由于它是一个非常通用的工具，所以它可以被用来生成从救援系统、安装盘，到特殊爱好的 Live CD/DVD/USB 系统——无人知晓还有其他什么。简单地说，如果要将 Arch 放在一条闪光的船上，它可以帮你做到这一点。Archiso 的核心以及灵魂是 *mkarchiso*。它的所有选项都写在它的用法输出上，所以它的直接使用方法将不在这里讨论。相反，这篇 wiki 文章将导引你迅速建立你的 Live 介质。

## Contents

*   [1 安装和配置](#.E5.AE.89.E8.A3.85.E5.92.8C.E9.85.8D.E7.BD.AE)
*   [2 配置 Live 介质](#.E9.85.8D.E7.BD.AE_Live_.E4.BB.8B.E8.B4.A8)
    *   [2.1 安装包](#.E5.AE.89.E8.A3.85.E5.8C.85)
        *   [2.1.1 自定义本地库](#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.9C.AC.E5.9C.B0.E5.BA.93)
        *   [2.1.2 避免安装属于base组的包](#.E9.81.BF.E5.85.8D.E5.AE.89.E8.A3.85.E5.B1.9E.E4.BA.8Ebase.E7.BB.84.E7.9A.84.E5.8C.85)
        *   [2.1.3 Installing packages from multilib](#Installing_packages_from_multilib)
    *   [2.2 向映像里添加文件](#.E5.90.91.E6.98.A0.E5.83.8F.E9.87.8C.E6.B7.BB.E5.8A.A0.E6.96.87.E4.BB.B6)
    *   [2.3 引导器](#.E5.BC.95.E5.AF.BC.E5.99.A8)
    *   [2.4 登录管理器](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.5 改变自动登录状态](#.E6.94.B9.E5.8F.98.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95.E7.8A.B6.E6.80.81)
*   [3 构建ISO](#.E6.9E.84.E5.BB.BAISO)
    *   [3.1 重建ISO](#.E9.87.8D.E5.BB.BAISO)
*   [4 使用ISO](#.E4.BD.BF.E7.94.A8ISO)
*   [5 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [5.1 在沒有互联网连接的情况下安装 Archiso](#.E5.9C.A8.E6.B2.92.E6.9C.89.E4.BA.92.E8.81.94.E7.BD.91.E8.BF.9E.E6.8E.A5.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E5.AE.89.E8.A3.85_Archiso)
        *   [5.1.1 安装 archiso 到新的 root](#.E5.AE.89.E8.A3.85_archiso_.E5.88.B0.E6.96.B0.E7.9A.84_root)
        *   [5.1.2 Chroot 并配置基本系统](#Chroot_.E5.B9.B6.E9.85.8D.E7.BD.AE.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F)
            *   [5.1.2.1 恢复 journald 的配置](#.E6.81.A2.E5.A4.8D_journald_.E7.9A.84.E9.85.8D.E7.BD.AE)
            *   [5.1.2.2 删除特殊的 udev 规则](#.E5.88.A0.E9.99.A4.E7.89.B9.E6.AE.8A.E7.9A.84_udev_.E8.A7.84.E5.88.99)
            *   [5.1.2.3 禁用和移除 archiso 创建的服务](#.E7.A6.81.E7.94.A8.E5.92.8C.E7.A7.BB.E9.99.A4_archiso_.E5.88.9B.E5.BB.BA.E7.9A.84.E6.9C.8D.E5.8A.A1)
            *   [5.1.2.4 移除 Live 环境的特殊脚本](#.E7.A7.BB.E9.99.A4_Live_.E7.8E.AF.E5.A2.83.E7.9A.84.E7.89.B9.E6.AE.8A.E8.84.9A.E6.9C.AC)
            *   [5.1.2.5 导入archlinux密钥](#.E5.AF.BC.E5.85.A5archlinux.E5.AF.86.E9.92.A5)
            *   [5.1.2.6 配置系统](#.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.BB.9F)
            *   [5.1.2.7 启用图形登录（可选）](#.E5.90.AF.E7.94.A8.E5.9B.BE.E5.BD.A2.E7.99.BB.E5.BD.95.EF.BC.88.E5.8F.AF.E9.80.89.EF.BC.89)
*   [6 参阅](#.E5.8F.82.E9.98.85)
    *   [6.1 文档和教程](#.E6.96.87.E6.A1.A3.E5.92.8C.E6.95.99.E7.A8.8B)
    *   [6.2 示例自定义模板](#.E7.A4.BA.E4.BE.8B.E8.87.AA.E5.AE.9A.E4.B9.89.E6.A8.A1.E6.9D.BF)

## 安装和配置

**注意:** 以下操作请在ROOT权限下使用，在错误的权限下操作会造成问题。

当你开始之前, [安装](/index.php/Install "Install") [archiso](https://www.archlinux.org/packages/?name=archiso) 或 [archiso-git](https://aur.archlinux.org/packages/archiso-git/)。

Archiso 附带2个预定义配置（profiles）: *releng* 和*baseline*。

*   如果您想要创建完全定制的 Live Arch Linux ，并预装所有您喜爱的程序和配置，使用 *releng*。

*   如果您只是想构建一个简易 Live 镜像，无预装软件并仅有基础配置，那么使用 *baseline*。

现在，将您选择的配置文件复制到目录（在下面的示例中为 *archlive*），您可以在其中进行调整和构建。 执行以下操作，用 `releng` 或 `baseline` 替换 `**profile**`。

```
# cp -r /usr/share/archiso/configs/**profile** *archlive*

```

*   如果你使用 `releng` 配置文件来创建一个完全自定义的镜像，那么你可以继续到：[#配置 Live 介质](#.E9.85.8D.E7.BD.AE_Live_.E4.BB.8B.E8.B4.A8)。

*   如果您使用 `baseline` 配置文件创建一个简易映像，那么你不需要做任何定制，并可以直接继续到 [#构建ISO](#.E6.9E.84.E5.BB.BAISO).

## 配置 Live 介质

本节详细介绍该如何配置您将创建的映像，允许您定义哪些包以及配置将被您的 Live 映像所包含。 在 [#安装和配置](#.E5.AE.89.E8.A3.85.E5.92.8C.E9.85.8D.E7.BD.AE) 中创建的`*archlive*`目录中有许多文件和目录; 我们只关注其中一部分，主要是

*   `packages.*` - 在这里一行行列出你想要安装的包，和
*   `airootfs` 目录——这是一个覆盖目录，你将在这里完成所有的定制工作。

一般来说，您在全新安装之后所执行的每个管理任务（不包括软件包安装）可以被写入这个脚本： `*archlive*/airootfs/root/customize_airootfs.sh`。您必须从新环境的角度来写该脚本，所以脚本中的 / 代表方才被创建的 Live ISO 的根。

### 安装包

[编辑](/index.php/Edit "Edit") `packages.i686`，`packages.x86_64` 或 `packages.both` 中的程序包列表，以指示要在 live 媒体上安装那些程序包。这里的后缀表示包可用的架构。

**Note:** 如果要在 Live CD 中使用 [窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，则必须添加必要且正确的 [video drivers](/index.php/Video_drivers "Video drivers")，否则 WM 可能在加载时冻结。

#### 自定义本地库

为了准备自定义包或是从 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")/[ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 安装包，你也可以 [创建自定义本地资源库](/index.php/Custom_local_repository "Custom local repository")。如果您希望支持多种体系结构，则应采取预防措施来防止发生错误。每个架构应该有自己的目录树：

 `$ tree ~/customrepo/ | sed "s/$(uname -m)/<arch>/g"` 
```
/home/archie/customrepo/
└── <arch>
    ├── customrepo.db -> customrepo.db.tar.xz
    ├── customrepo.db.tar.xz
    ├── customrepo.files -> customrepo.files.tar.xz
    ├── customrepo.files.tar.xz
    └── personal-website-git-b99cce0-1-<arch>.pkg.tar.xz

1 directory, 5 files

```

如此后，您可以添加您的仓库——把下面的句子加入 `~/archlive/pacman.conf`，并置于其他仓库条目上面（优先级最高）：

 `~/archlive/pacman.conf` 
```
...
# custom repository
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch
...
```

*repo-add* 可执行文件检查软件包是否合适。如果不，那么你将得到与此类似的错误消息：

```
==> ERROR: '/home/archie/customrepo/<arch>/foo-<arch>.pkg.tar.xz' does not have a valid database archive extension.

```

#### 避免安装属于base组的包

默认情况下，`/usr/bin/mkarchiso`——一个被 `~/archlive/build.sh` 使用的脚本——会调用 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) 中一个名为 `pacstrap` 的程序，且在调用时不使用 `-i` 标志——这将使 [Pacman](/index.php/Pacman "Pacman") 在安装过程中不等待用户输入。

当 base 组软件包被加入黑名单——把它们写到 `~/archlive/pacman.conf` 中的 `IgnorePkg` 行——时，[Pacman](/index.php/Pacman "Pacman") 会询问是否仍然安装它们——意味着如果用户输入被跳过，它们就会被安装。为了避免安装这些包，这里有一些选择：

*   **丑陋**方案（Dirty）：在 `/usr/bin/mkarchiso` 中每次调用 `pacstrap` 的行上加入 `i` 标志。

*   **整洁**方案（Clean）：创建 `/usr/bin/mkarchiso` 的一份复制。在该复制中增加此标志，并修改 `~/archlive/build.sh` 以使其调用修改过的 mkarchiso 脚本。

*   **高级**方案（Advanced）: 在 `~/archlive/build.sh` 中创建一个函数，该函数将在基础安装结束后显式移除那些包。若这样做，可以免去在安装过程中多次按回车键的麻烦。

#### Installing packages from multilib

要从 [Multilib](/index.php/Multilib_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Multilib (简体中文)") 资源库安装软件包，您必须创建两个 pacman 配置文件：一个用于 x86_64，一个用于 i686。 将 `pacman.conf` 复制到 `pacmanx86_64.conf` 和 `pacmani686.conf`。 取消注释以下行以`pacmanx86_64.conf` 中启用 *multilib*）：

 `pacmanx86_64.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

然后用编辑器编辑 `build.sh`。 把：

 `build.sh` 
```
run_once make_pacman_conf

# Do all stuff for each airootfs
for arch in i686 x86_64; do
    run_once make_basefs
    run_once make_packages
done

run_once make_packages_efi

for arch in i686 x86_64; do
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

改为：

 `build.sh` 
```
cp -v releng/pacmanx86_64.conf releng/pacman.conf
run_once make_pacman_conf

# Do all stuff for each airootfs
for arch in x86_64; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

echo make_pacman_conf i686
cp -v releng/pacmani686.conf releng/pacman.conf
cp -v releng/pacmani686.conf ${work_dir}/pacman.conf

for arch in i686; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

这样，x86_64 和 i686 的软件包将安装有自己的pacman配置文件。

### 向映像里添加文件

**注意:** 你必须使用 root 权限来完成这件事，不要改变任何你复制过来的文件的所有权，airootfs 中的**所有**文件必须为 root 用户所有。适当的所有制将在不久被解决。

airootfs 目录作为要覆盖的文件，把它看作是在当前系统上的根目录'/'，所以你在这个目录中放置的任何文件都将在开机时被复制。

所以，如果你在当前系统上有一组 iptables 脚本且想要在 Live 映像上使用，请这样复制:

```
# cp -r /etc/iptables ~/archlive/airootfs/etc

```

在用户 home 文件夹里放置文件的方法有些许不同。不要把它们放在 `airootfs/home`，而是在 airootfs/ 里创建 skel 目录并将其放置在那里。然后我们会将相关命令添加到 `customize_airootfs.sh`——我们要使用它在引导时复制文件以及梳理权限。

首先，创建 skel 目录

```
# mkdir ~/archlive/airootfs/etc/skel

```

现在，复制 'home' 的文件到 skel 目录。例如，对于 `.bashrc`：

```
# cp ~/.bashrc ~/archlive/airootfs/etc/skel/

```

当 `~/archlive/airootfs/root/customize_airootfs.sh` 被执行，并且一个新用户已被创建, skel 目录中的文件将自动被复制到新的 home 文件夹中，并被设置正确的权限。

类似地，需要注意位于层次结构下方的特殊配置文件。作为示例，配置文件 `/etc/X11/xinit/xinitrc` 位于可能被安装包覆盖的路径上。要将 `xinitrc` 的配置文件放在 `~/archlive/airootfs/etc/skel/` ，然后修改 `customize_airootfs.sh` 以适当地移动。

### 引导器

默认的文件应该可以正常工作，所以你应该不需要去碰它。

由于 isolinux 的模块化性质，你能够使用很多插件，因为所有 *.c32 都被复制且可以可供您使用。看看[syslinux 官方网站](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) 和 [Archiso Git Repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files)。使用所述插件，便有可能做出更具视觉吸引力及复杂的菜单。参见 [此处](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32)。

### 登录管理器

通过启用您登录管理器的 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 服务来做到在引导时启动 X 。如果您知道哪一个 .service 文件需要软链接，那就太好了。如果不知道，你也可以轻松找出——如果你在创建 iso 所用的系统上使用相同的程序的话。只需使用：

```
 $ ls -l /etc/systemd/system/display-manager.service

```

现在在 `~/archlive/airootfs/etc/systemd/system` 中创建相同的软链接。如 LXDM：

```
# ln -s /usr/lib/systemd/system/lxdm.service ~/archlive/airootfs/etc/systemd/system/display-manager.service

```

这将使您在 live 系统启用在系统上启动 LXDM。(This will enable LXDM at system start on your live system.)

或者，您也可以启用 `airootfs/root/customize_airootfs.sh` 中的服务以及其中启用的其他服务。

如果您希望图形环境在启动过程中自动启动，请确保编辑 `airootfs/root/customize_airootfs.sh` 并替换

```
systemctl set-default multi-user.target

```

为

```
systemctl set-default graphical.target

```

### 改变自动登录状态

Getty 的自动登录配置位于 `airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf`。

您可以修改这个文件来更改自动登录用户：

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

或者干脆删除它来禁用自动登录。

## 构建ISO

现在，你已经准备好把你的文件转换成 .iso，以便可以刻录到 CD 或 USB：

首先创建 `out/` 目录（可选，如果没有的话 build.sh 将会创建它），

```
# mkdir ~/archlive/out/

```

然后在 `~/archlive` 里面执行：

```
# ./build.sh -v

```

该脚本将现在下载并安装你指定的软件包到 `work/*/airootfs`，创建内核和 init 映像（initramfs），应用您的修改，并最终把 ISO 建立到 `out/`。

### 重建ISO

在修改之后重建 ISO 不被官方支持。但是，通过应用两个步骤很容易。首先，您必须删除工作目录中的锁定文件：

```
# rm -v work/build.make_*

```

此外，需要编辑脚本 `airootfs/root/customize_airootfs.sh`，并在 `useradd` 行的开头添加 `id` 命令，如下所示。否则，重建将在此处停止，因为要添加的用户已经存在 [[1]](https://bugs.archlinux.org/task/41865)。

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

同时删除创建的用户或符号链接，如 `/etc/sudoers` 等持久性数据。

通过编辑 pacstrap 脚本（位于 /bin/pacstrap）并在第 361 行更改以下内容，可以稍微加快重建速度：

修改前:

```
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then

```

修改后:

```
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then

```

这增加了初始引导的速度，因为它不必下载和安装任何已经安装的基础包。

## 使用ISO

有关各种选项，请参见 [Category:Getting_and_installing_Arch_(简体中文)#安装方式](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E6.96.B9.E5.BC.8F "Category:Getting and installing Arch (简体中文)") 部分。

## 提示和技巧

### 在沒有互联网连接的情况下安装 Archiso

若你想在没有互联网连接或者你不想重复下载你想要的包的情况下安装 archiso（例如[官方的每月发布版](https://www.archlinux.org/download/)）：

首先，按照[安装指南](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")，并跳过一些步骤（如[连接到因特网](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BF.9E.E6.8E.A5.E5.88.B0.E5.9B.A0.E7.89.B9.E7.BD.91 "Installation guide (简体中文)")），直到[安装基本系统](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F "Installation guide (简体中文)")之前。

#### 安装 archiso 到新的 root

复制 Live 环境的*所有文件*到新的根目录，而不是使用 `pacstrap`(这将尝试从远程存储库下载)：

```
 # cp -ax / /mnt

```

**注意:** The option (`-x`)排除了一些特殊目录，因为它们不应该被复制到新的根目录。

然后，创建一些目录并复制内核映像到新的根，以保证新系统的完整性：

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

完成之后，请按[Installation guide (简体中文)#Fstab](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Fstab "Installation guide (简体中文)")所述生成 fstab。

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

##### 删除特殊的 udev 规则

如果有任何有线网络接口，[udev 的这个规则](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)会自动启动dhcpcd。

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

##### 禁用和移除 archiso 创建的服务

有一些服务文件是为 Live 环境创建的，请禁用这些服务并移除文件——因为它们对于新系统来说没必要存在：

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

##### 移除 Live 环境的特殊脚本

在 live 系统中通过 archiso 脚本安装了一些脚本，这对于新系统是不必要的：

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

##### 导入archlinux密钥

为了使用官方存储库，我们需要导入 archlinux 主密钥（[Pacman/Package signing (简体中文)#初始化密钥环](/index.php/Pacman/Package_signing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9D.E5.A7.8B.E5.8C.96.E5.AF.86.E9.92.A5.E7.8E.AF "Pacman/Package signing (简体中文)")）。这一步通常是通过 pacstrap 完成的，但是可以通过

```
# pacman-key --init
# pacman-key --populate archlinux

```

**注意:** Keyboard or mouse activity is needed to generate entropy and speed-up the first step.

##### 配置系统

现在，您可以按照 [Installation guide (简体中文)#配置系统](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.BB.9F "Installation guide (简体中文)") 中跳过的步骤（设置语言环境，时区，主机名等），并通过创建初始 ramdisk 来完成安装，如 [Installation guide (简体中文)#Initramfs](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Initramfs "Installation guide (简体中文)")。

##### 启用图形登录（可选）

如果使用像GDM这样的显示管理器，则可能需要将 systemd 默认目标从 multi-user.target 更改为允许图形登录的目标。

```
# systemctl disable multi-user.target
# systemctl enable graphical.target

```

## 参阅

### 文档和教程

*   [Archiso 项目页面](https://projects.archlinux.org/archiso.git)
*   [官方文档](https://projects.archlinux.org/archiso.git/tree/docs)

### 示例自定义模板

*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://easy.open.and.free.fr/didjix/)
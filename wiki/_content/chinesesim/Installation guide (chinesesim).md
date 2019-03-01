**翻译状态：** 本文是英文页面 [Installation_guide](/index.php/Installation_guide "Installation guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-02-27，点击[这里](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=565601)可以查看翻译后英文页面的改动。

本文将指导如何用官方安装镜像启动的 Live 系统安装 [Arch Linux](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。建议在安装前阅读 [FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。对于本文中使用的惯用术语，请参阅 [Help:Reading](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Reading (简体中文)")。请注意，代码段可能会有占位符（格式是 `*italics*`），你可能需要手动去掉它们。

有关更详细的说明，请阅读本指南内相应的 [ArchWiki](/index.php/ArchWiki:About_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki:About (简体中文)") 文章或各类程序的[手册](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")。有关配置的概述，请参阅 [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)。若需要交互帮助，可以使用 [IRC 频道](/index.php/IRC_channel "IRC channel") 和 [论坛](https://bbs.archlinux.org/)。

Arch Linux 能在任何内存空间不小于 512MB 的 [x86_64](https://en.wikipedia.org/wiki/zh:X86-64 "w:zh:X86-64") 兼容机上运行。用 [base](https://www.archlinux.org/groups/x86_64/base/) 组内的软件包进行的基本安装将占用小于 800MB 的存储空间。由于安装过程中需要从远程存储库获取软件包，机器将需要一个有效的互联网连接。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装前的准备](#安装前的准备)
    *   [1.1 验证签名](#验证签名)
    *   [1.2 启动到 live 环境](#启动到_live_环境)
    *   [1.3 键盘布局](#键盘布局)
    *   [1.4 验证启动模式](#验证启动模式)
    *   [1.5 连接到因特网](#连接到因特网)
    *   [1.6 更新系统时间](#更新系统时间)
    *   [1.7 建立硬盘分区](#建立硬盘分区)
        *   [1.7.1 分区示例](#分区示例)
    *   [1.8 格式化分区](#格式化分区)
    *   [1.9 挂载分区](#挂载分区)
*   [2 安装](#安装)
    *   [2.1 选择镜像](#选择镜像)
    *   [2.2 安装基本系统](#安装基本系统)
*   [3 配置系统](#配置系统)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 时区](#时区)
    *   [3.4 本地化](#本地化)
    *   [3.5 网络](#网络)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root 密码](#Root_密码)
    *   [3.8 安装引导程序](#安装引导程序)
*   [4 重启](#重启)
*   [5 安装后的工作](#安装后的工作)

## 安装前的准备

安装文件和它的 [GnuPG](/index.php/GnuPG "GnuPG") 签名可以从[下载](https://archlinux.org/download/)页面获取。

### 验证签名

一般建议先验证所下载文件的签名，特别是从 *HTTP 镜像源* 下载的文件，因为通常会受到恶意镜像的拦截。 [[1]](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation)

在一台已经安装 [GnuPG](/index.php/GnuPG "GnuPG") 的系统上，通过下载 *PGP 签名* (under *Checksums*) 到 ISO 文件所在的路径，可以通过以下方式[验证](/index.php/GnuPG#Verify_a_signature "GnuPG")：

```
$ gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

另外，在一台已经安装 Arch Linux 的计算机上可以通过以下方式验证：

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

**注意:**

*   如果你是从镜像站点下载，而不是从 [archlinux.org](https://archlinux.org/download/) 下载的话，则签名是可以被伪造的。在这种情况下，确保用来解码签名的公钥是被另一个可信的 key 签署的。`gpg` 命令会输出公钥的指纹。
*   另一种验证签名的方法是确保公钥的指纹等于其中一位签署了 ISO 文件 [Arch Linux 开发者](https://www.archlinux.org/people/developers/)的指纹。请参阅 [Wikipedia:Public-key_cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") 获取更多关于公钥加密的信息。

### 启动到 live 环境

live 环境可以从 [USB 安装 U 盘](/index.php/USB_flash_installation_media "USB flash installation media")、[光盘](/index.php/Optical_disc_drive#Burning "Optical disc drive") 或带有 [PXE](/index.php/PXE "PXE") 的网络启动进入。其他安装方法请参考[Category:Installation process (简体中文)](/index.php/Category:Installation_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Installation process (简体中文)").

*   选择从带有 Arch 安装文件的媒介启动通常是在[电脑开机自检](https://en.wikipedia.org/wiki/Power-on_self_test "w:Power-on self test")的时候按下某个按键，一般会在启动画面有提示。具体参考你主板的手册。
*   当 Arch 菜单出现时，选择 *Boot Arch Linux* 并按 `Enter` 进入安装环境。
*   参阅 [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) 获取一系列的 [启动参数](/index.php/Kernel_parameters#Configuration "Kernel parameters")，参阅 [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) 获取已经被包含的包。
*   你将会以 root 身份登录进一个[虚拟控制台](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")，默认的 SHELL 是 [Zsh](/index.php/Zsh "Zsh")。

如果想一边安装，一边使用 [ELinks](/index.php/ELinks "ELinks") 查看本指南，可以使用 `Alt+*箭头*` [快捷键](/index.php/Keyboard_shortcuts "Keyboard shortcuts")切换不同的控制台，[编辑](/index.php/Textedit "Textedit")配置文件，可以使用[nano](/index.php/Nano#Usage "Nano")、[vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") 或 [vim](/index.php/Vim#Usage "Vim")。

### 键盘布局

[控制台键盘布局](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 默认为 `us`（美式键盘映射）。列出所有可用的键盘布局，可以使用：

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

如果您想要更改键盘布局，可以将一致的文件名添加进 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1)，但请省略路径和扩展名。比如，要添加 [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") 键盘布局：

```
# loadkeys de-latin1

```

[Console fonts](/index.php/Console_fonts "Console fonts") 位于 `/usr/share/kbd/consolefonts/`，设置方式请参考 [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8)。

根据 [Getting and installing Arch](/index.php/Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Getting and installing Arch (简体中文)") 中所述，下载并引导安装介质。启动完成后将会自动以 root 身份登录虚拟控制台并进入 [Zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)") 命令提示符。

### 验证启动模式

如果以在 UEFI 主板上启用 [UEFI](/index.php/UEFI "UEFI") 模式，[Archiso](/index.php/Archiso "Archiso") 将会使用 [systemd-boot](/index.php/Systemd-boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-boot (简体中文)") 来 [启动](/index.php/Boot "Boot") Arch Linux。可以列出 [efivars](/index.php/UEFI#UEFI_variables "UEFI") 目录以验证启动模式：

```
# ls /sys/firmware/efi/efivars

```

如果目录不存在，系统可能以 [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") 或 CSM 模式启动，详见您的主板手册。

### 连接到因特网

守护进程 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 已被默认启用来探测 [有线网络设备](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)，并会尝试连接。可以使用 [ping](/index.php/Ping "Ping") 验证连接是否正常：

```
# ping archlinux.org

```

如果没有可用网络连接，利用 `systemctl stop dhcpcd@*网络接口*`，`TAB` [停用](/index.php/Systemd#Using_units "Systemd") *dhcpcd* 进程，`*网络接口*` 名可以通过 [Tab补全](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion")。要配置网络，详见 [网络配置](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")。

### 更新系统时间

使用 [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) 确保系统时间是准确的：

```
# timedatectl set-ntp true

```

可以使用 `timedatectl status` 检查服务状态。

### 建立硬盘分区

磁盘若被系统识别到，就会被分配为一个 [块设备](https://en.wikipedia.org/wiki/zh:%E8%AE%BE%E5%A4%87%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F#.E5.91.BD.E5.90.8D.E7.BA.A6.E5.AE.9A "wikipedia:zh:设备文件系统")，如 `/dev/sda` 或者 `/dev/nvme0n1`。可以使用 [lsblk](/index.php/Lsblk "Lsblk") 或者 *fdisk* 查看：

```
# fdisk -l

```

结果中以 `rom`，`loop` 或者 `airoot` 结束的可以被忽略。

对于一个选定的设备，以下的*分区*是必须要有的：

*   一个根分区（挂载在根目录）`/`；
*   如果 [UEFI](/index.php/UEFI "UEFI") 模式被启用，你还需要一个 [EFI 系统分区](/index.php/EFI_system_partition "EFI system partition")。

如果需要创建多级存储例如 [LVM](/index.php/LVM "LVM")、[disk encryption](/index.php/Disk_encryption "Disk encryption") 或 [RAID](/index.php/RAID "RAID")，请在此时完成。

#### 分区示例

| BIOS 和 [MBR](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Master_Boot_Record "Partitioning (简体中文)") |
| 挂载点 | 分区 | [分区类型](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | 建议大小 |
| `/mnt` | `/dev/sd*X*1` | Linux | 剩余空间 |
| [SWAP] | `/dev/sd*X*2` | Linux swap (交换空间) | 大于 512 MiB |
| UEFI with [GPT](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#GUID_分区表 "Partitioning (简体中文)") |
| 挂载点 | 分区 | [分区类型](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | 建议大小 |
| `/mnt/boot` or `/mnt/efi` | `/dev/sd*X*1` | [EFI 系统分区](/index.php/EFI_system_partition_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "EFI system partition (简体中文)") | 256–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 根目录 (/) | 剩余空间 |
| [SWAP] | `/dev/sd*X*3` | Linux swap (交换空间) | 大于 512 MiB |

参阅[布局示例](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#布局示例 "Partitioning (简体中文)")。

**注意:**

*   请使用 [fdisk](/index.php/Fdisk_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fdisk (简体中文)") 或 [parted](/index.php/Parted_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Parted (简体中文)") 修改分区表，例如 `fdisk /dev/sd*X*`。
*   如果文件系统支持，[交换空间](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)")也可以设在[交换文件](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#交换文件 "Swap (简体中文)")上。

### 格式化分区

当分区建立好了，这些分区都需要使用适当的[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")进行格式化。举个例子，如果根分区在 `/dev/sd*X*1` 上并且会使用 `*ext4*` 文件系统，运行：

```
 # mkfs.*ext4* /dev/sd*X*1

```

如果您创建了交换分区（例如 `/dev/*sda3*`），使用 mkswap 将其初始化：

```
 # mkswap /dev/sd*X*2
 # swapon /dev/sd*X*2

```

详情参见[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#创建文件系统 "File systems (简体中文)")。

### 挂载分区

将根分区[挂载](/index.php/Mount "Mount")到 `/mnt`，例如：

```
# mount /dev/sd*X*1 /mnt

```

创建其他剩余的挂载点（比如 `/mnt/efi`）并挂载其相应的分区。

接下来 [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) 将会自动检测挂载的文件系统和交换空间。

## 安装

### 选择镜像

文件 `/etc/pacman.d/mirrorlist` 定义了软件包会从哪个 [镜像源](/index.php/Mirrors "Mirrors") 下载。在 LiveCD 启动的系统上，所有的镜像都被启用，并且在镜像被制作时，我们已经通过他们的同步情况和速度排序。

在列表中越前的镜像在下载软件包时有越高的优先权。你可以相应的修改文件 `/etc/pacman.d/mirrorlist`，并将地理位置最近的镜像源挪到文件的头部，同时你也应该考虑一些其他标准。

这个文件接下来还会被 *pacstrap* 拷贝到新系统里，所以请确保设置正确。

### 安装基本系统

使用 [pacstrap](https://git.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 脚本，安装 [base](https://www.archlinux.org/groups/x86_64/base/) 组：

```
# pacstrap /mnt base

```

这个组并没有包含全部 live 环境中的程序，有些需要额外安装，例如 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)。[packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) 页面包含了它们的差异。

如果你还想安装其他软件包组比如 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)，请将他们的名字添加到 *pacstrap* 后，并用空格隔开。你也可以在 [#Chroot](#Chroot) 之后使用 [pacman](/index.php/Pacman "Pacman") 手动安装软件包或组。

## 配置系统

### Fstab

用以下命令生成 [fstab](/index.php/Fstab "Fstab") 文件 (用 `-U` 或 `-L` 选项设置UUID 或卷标)：

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

**强烈建议** 在执行完以上命令后，后检查一下生成的 `/mnt/etc/fstab` 文件是否正确。

### Chroot

[Change root](/index.php/Change_root "Change root") 到新安装的系统：

```
# arch-chroot /mnt

```

### 时区

设置 [时区](/index.php/Time_zone "Time zone")：

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

例如：

```
# ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

运行 [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) 以生成 `/etc/adjtime`：

```
# hwclock --systohc

```

这个命令假定硬件时间已经被设置为 [UTC时间](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC")。详细信息请查看 [System time#Time standard](/index.php/System_time#Time_standard "System time")。

### 本地化

本地化的程序与库若要本地化文本，都依赖 [Locale](/index.php/Locale "Locale")，后者明确规定地域、货币、时区日期的格式、字符排列方式和其他本地化标准等等。在下面两个文件设置：`locale.gen` 与 `locale.conf`。

`/etc/locale.gen` 是一个仅包含注释文档的文本文件。指定您需要的本地化类型，只需移除对应行前面的注释符号（`＃`）即可，建议选择带 `UTF-8` 的项：

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_TW.UTF-8 UTF-8

```

接着执行 `locale-gen` 以生成 locale 讯息：

```
# locale-gen

```

`/etc/locale.gen` 会生成指定的本地化文件。

创建 `locale.conf` 并编辑 `LANG` 这一 [变量](/index.php/Variable "Variable")，比如：

**Tip:** 将系统 locale 设置为 `en_US.UTF-8`，系统的 Log 就会用英文显示，这样更容易问题的判断和处理。用户可以设置自己的 locale，详情参阅 [Locale](/index.php/Locale#Overriding_system_locale_per_user_session "Locale") 或 [Locale_(简体中文)#设置 locale](/index.php/Locale_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.AE.BE.E7.BD.AE_locale "Locale (简体中文)")。
 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 
**警告:** 不推荐在此设置任何中文 locale，会导致 TTY 乱码。

另外，如果你需要修改 [#键盘布局](#键盘布局)，并想让这个设置持续生效，编辑 [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5)，例如：

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### 网络

创建 [hostname](/index.php/Hostname "Hostname") 文件:

 `/etc/hostname` 
```
*myhostname*

```

添加对应的信息到 [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

如果系统有一个永久的 IP 地址，请使用这个永久的 IP 地址而不是 `127.0.1.1`。

对新安装的系统，需要再次设置网络。具体请参考 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")。

### Initramfs

你通常不需要创建 *initramfs*，因为在你执行 *pacstrap* 时已经安装 [linux](https://www.archlinux.org/packages/?name=linux)，这时 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 会被自动运行。

对于 [LVM](/index.php/LVM#Configure_mkinitcpio "LVM")、 [system encryption](/index.php/Dm-crypt "Dm-crypt") 或 [RAID](/index.php/RAID#Configure_mkinitcpio "RAID")，修改 [mkinitcpio.conf](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)") 并用以下命令重新创建一个 Initramfs：

```
# mkinitcpio -p linux

```

### Root 密码

设置 Root [密码](/index.php/Password "Password")：

```
# passwd

```

### 安装引导程序

你需要安装 Linux 引导程序以在安装后启动系统，你可以使用的的引导程序在 [启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)") 中，请选择一个并且安装并配置它，比如 [GRUB](/index.php/GRUB "GRUB")。

**注意:** 如果你使用 Intel 或者 AMD 的 CPU，请[启用微码更新](/index.php/Microcode "Microcode")。

## 重启

输入 `exit` 或按 `Ctrl+D` 退出 chroot 环境。

可选用 `umount -R /mnt` 手动卸载被挂载的分区：这有助于发现任何「繁忙」的分区，并通过 [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) 查找原因。

最后，通过执行 `reboot` 重启系统，*systemd* 将自动卸载仍然挂载的任何分区。不要忘记移除安装介质，然后使用 root 帐户登录到新系统。

## 安装后的工作

系统管理引导，图形用户界面的安装、声音管理、触摸板支持等后期工作参见 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")。

感兴趣的各类程序，请参见 [List of applications (简体中文)](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")。
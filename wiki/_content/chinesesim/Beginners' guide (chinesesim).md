**翻译状态：** 本文是英文页面 [Beginners'_Guide](/index.php/Beginners%27_Guide "Beginners' Guide") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-07，点击[这里](https://wiki.archlinux.org/index.php?title=Beginners'_Guide&diff=0&oldid=440464)可以查看翻译后英文页面的改动。

欢迎，本向导写给 Arch 新用户，但是会尽量做到成为所有用户的参考和信息库。 本文档指导您使用[Arch安装脚本](https://projects.archlinux.org/arch-install-scripts.git/)来安装[Arch Linux](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")：一个简单、轻量级、适合计算机水平较高用户使用的发行版。建议在安装前先浏览一下[FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")。 社区维护的[ArchWiki](/index.php/Main_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Main page (简体中文)")应该有办法解决遇到的疑难。若在其它地方找不到解决办法，[IRC 频道](/index.php/IRC_channel "IRC channel")([irc://irc.freenode.net/#archlinux-cn](irc://irc.freenode.net/#archlinux-cn)) 和[论坛](https://bbs.archlinux.org/)都是求助的好地方。为了贯彻[Arch之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")，如遇陌生的命令，可输入`man *command*`以查询相关`man`手册页。

**Tip:** This guide is accessible from the live installation with the [ELinks](/index.php/ELinks "ELinks") browser, after the [#Connect to the Internet](#Connect_to_the_Internet) step. This can be done in a new [virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console"), switching (`Alt+arrow`) between the console containing the web page, and the console where you are performing the installation. Similarly, the `#archlinux` [IRC](/index.php/IRC "IRC") can be accessed using [irssi](/index.php/Irssi "Irssi").

## Contents

*   [1 准备](#.E5.87.86.E5.A4.87)
    *   [1.1 UEFI 模式](#UEFI_.E6.A8.A1.E5.BC.8F)
    *   [1.2 设置键盘布局](#.E8.AE.BE.E7.BD.AE.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [1.3 连接到因特网](#.E8.BF.9E.E6.8E.A5.E5.88.B0.E5.9B.A0.E7.89.B9.E7.BD.91)
    *   [1.4 更新系统时间](#.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.BB.9F.E6.97.B6.E9.97.B4)
*   [2 准备存储设备](#.E5.87.86.E5.A4.87.E5.AD.98.E5.82.A8.E8.AE.BE.E5.A4.87)
    *   [2.1 识别设备](#.E8.AF.86.E5.88.AB.E8.AE.BE.E5.A4.87)
    *   [2.2 分区工具](#.E5.88.86.E5.8C.BA.E5.B7.A5.E5.85.B7)
    *   [2.3 格式化文件系统并使用swap](#.E6.A0.BC.E5.BC.8F.E5.8C.96.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E5.B9.B6.E4.BD.BF.E7.94.A8swap)
    *   [2.4 挂载分区](#.E6.8C.82.E8.BD.BD.E5.88.86.E5.8C.BA)
*   [3 安装](#.E5.AE.89.E8.A3.85)
    *   [3.1 选择安装镜像](#.E9.80.89.E6.8B.A9.E5.AE.89.E8.A3.85.E9.95.9C.E5.83.8F)
    *   [3.2 安装基本软件包](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 fstab](#fstab)
    *   [4.2 chroot](#chroot)
    *   [4.3 Locale](#Locale)
    *   [4.4 终端字体和键盘映射](#.E7.BB.88.E7.AB.AF.E5.AD.97.E4.BD.93.E5.92.8C.E9.94.AE.E7.9B.98.E6.98.A0.E5.B0.84)
    *   [4.5 时间](#.E6.97.B6.E9.97.B4)
    *   [4.6 Initramfs](#Initramfs)
    *   [4.7 设置 Root 密码](#.E8.AE.BE.E7.BD.AE_Root_.E5.AF.86.E7.A0.81)
    *   [4.8 安装 bootloader](#.E5.AE.89.E8.A3.85_bootloader)
    *   [4.9 配置网络](#.E9.85.8D.E7.BD.AE.E7.BD.91.E7.BB.9C)
        *   [4.9.1 主机名](#.E4.B8.BB.E6.9C.BA.E5.90.8D)
        *   [4.9.2 有线网络](#.E6.9C.89.E7.BA.BF.E7.BD.91.E7.BB.9C)
        *   [4.9.3 无线网络](#.E6.97.A0.E7.BA.BF.E7.BD.91.E7.BB.9C)
    *   [4.10 设置 root 密码](#.E8.AE.BE.E7.BD.AE_root_.E5.AF.86.E7.A0.81_2)
    *   [4.11 卸载分区并重启系统](#.E5.8D.B8.E8.BD.BD.E5.88.86.E5.8C.BA.E5.B9.B6.E9.87.8D.E5.90.AF.E7.B3.BB.E7.BB.9F)
*   [5 安装之后](#.E5.AE.89.E8.A3.85.E4.B9.8B.E5.90.8E)

## 准备

理论上，Arch Linux能在任何内存空间不小于 256MB 的[i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")兼容机上运行。最基本的[base](https://www.archlinux.org/groups/x86_64/base/)组中包含的包将占用约 800MB 存储空间。

官方 Arch Linux 安装媒介的准备方法在[此分类](/index.php/Category:Getting_and_installing_Arch_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (简体中文)")中介绍，建议始终使用最新的 ISO 镜像。

启动完成后会自动以 root 登录并进入[zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")命令提示， [grml config](http://grml.org/zsh/)提供了额外的配置。编辑配置文件时可以使用 [nano](/index.php/Nano#Usage "Nano") 或 [vim](/index.php/Vim#Usage "Vim") 。

### UEFI 模式

如果您使用 [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)") 主板，且 UEFI 启动模式（优于 BIOS/Legacy 模式）已启用，CD/USB 会自动通过[systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/) 启动 Arch Linux。要确认是否已进入UEFI模式，检查下面目录是否有文件：

```
# ls /sys/firmware/efi/efivars

```

详情参阅 [UEFI#UEFI Variables](/index.php/UEFI#UEFI_Variables "UEFI") 。

早期的设备对 UEFI 的支持并不规范，请通过主板，机型等关键字在网络和 Wiki 中进行搜索，看看有没有需要注意的事项。

### 设置键盘布局

**提示:** 此步骤只对该安装过程生效。

[控制台键盘布局](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 默认为`us`（美式键盘映射）。如果您正在使用非[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")键盘布局，通过以下的命令选择相应的键盘映射表：

 `# loadkeys *layout*` 

将 *layout* 转换为您的键盘布局，如`fr`，`uk`，`dvorak`或`be-latin1`。[这里](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2")有国家的二位字母编码表。使用命令 `ls /usr/share/kbd/keymaps/**/*.map.gz` 列出所有可用的键盘布局。

**Note:** `localectl list-keymaps` does not work due to bug [FS#46725](https://bugs.archlinux.org/task/46725).

要修改终端字体，请阅读 [Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)").

### 连接到因特网

安装程序会在启动时自动运行 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 守护进程以尝试‘’‘有线连接’‘’。需要网页验证的网络可以通过[ELinks](/index.php/ELinks "ELinks")浏览器进行登录。

可以用 [ping 命令检查网络是否正常](/index.php/Network_configuration#Check_the_connection "Network configuration")，如果网络不可用，需要 [手动配置网络](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")。下面用 [netctl](/index.php/Netctl "Netctl") 做示例。

	Netctl 准备

在设置网络之前，请先查明自己的网卡名称，[网络设备名](/index.php/Network_configuration#Device_names "Network configuration")可以通过 `ip link` 或 `iw dev`(无线网络)查到设备名称。通常以 `en` (ethernet), `wl` (WLAN) 或 `ww` (WWAN)开头。

为了防止冲突，首先停用 *dhcpcd* 服务，将 `enp0s25` 替换为正确的有线接口：

```
# systemctl stop dhcpcd@*enp0s25*.service

```

要保存设置，在配置基本系统之前将修改过的文件复制到新系统中。详见 。[Category:Network configuration](/index.php/Category:Network_configuration "Category:Network configuration")包含了其它配置方法，比如拨号连接。

	无线网络连接

使用 [netctl](/index.php/Netctl "Netctl") 的 *wifi-menu* 连接到[无线网络](/index.php/Wireless_network_configuration "Wireless network configuration"):

```
# wifi-menu -o *wlp2s0*

```

生成的配置文件位于 `/etc/netctl`中，对于需要用户名和密码的网络，请参考 [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise") 页面。

如果网络还不可用，可以尝试手动配置网络，除了驱动，大多无线网卡还需要固件。按照 [检查驱动状态](/index.php/Wireless_network_configuration#Check_the_driver_status "Wireless network configuration")中列出的方法设置无线固件。然后按照[手动设置](/index.php/Wireless_network_configuration#Manual_setup "Wireless network configuration") 中的步骤配置网络。[iw](https://www.archlinux.org/packages/?name=iw) 和 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) 都已经位于安装介质中。

	其它

有其它配置示例，[静态 IP 地址](/index.php/Network_configuration#Static_IP_address "Network configuration")，将 *netctl* 示例文件复制到 `/etc/netctl`：

```
# cp /etc/netctl/examples/ethernet-static /etc/netctl

```

然后启用配置:

```
# netctl start ethernet-static

```

### 更新系统时间

用 [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") 确保系统时间是正确的：

```
# timedatectl set-ntp true

```

用 `timedatectl status` 检查服务状态.详情阅读 [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)").

## 准备存储设备

**警告:** 分区可能会毁掉原数据。**强烈建议**先备份重要的数据。

此部分为新系统准备存储空间，更详细的介绍请阅读[Partitioning (简体中文)](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")。

*   如果您打算安装在 USB 上，请阅读 [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").
*   如果您打算为 [LVM](/index.php/LVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LVM (简体中文)")、[磁盘加密](/index.php/Disk_encryption "Disk encryption") 或 [RAID](/index.php/RAID "RAID") 创建堆栈式块设备，请在此部分加入需要的步骤。

### 识别设备

[识别](/index.php/File_systems#Identify_the_devices "File systems")目标设备，下面命令会显示所有连接到系统的设备和分区状况：

```
# lsblk

```

结果中会包含 Arch 安装设备(例如 USB 安装盘)，不是所有设备都适合安装。`rom`, `loop` 或 `airoot` 格式的分区可以忽略。

文章后面会用 `sd*xY*` 表示磁盘和分区，请按照您系统的实际状况修改命令。不要直接复制和执行。如果不需要重新分区，可以跳到 [#创建文件系统](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)，否则继续。

### 分区工具

[分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")是将磁盘话分成可以独立访问的部分。需要的信息会被保存到分区表中，有两种分区表类型：

*   [GUID 分区表(GPT)](/index.php/GUID_Partition_Table_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GUID Partition Table (简体中文)")
*   [主引导记录](/index.php/Master_Boot_Record_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Master Boot Record (简体中文)")（MBR）

Arch 安装盘中包含了多种 [分区工具](/index.php/Partitioning#Partitioning_tools "Partitioning")，需要根据分区表的类型进行选择。如果使用不兼容分区表格式的工具，会造成分区表损坏和所有数据丢失。

| 名称 | MBR | GPT | 变体 |
| [fdisk](/index.php/Fdisk "Fdisk") | Yes | Yes | *sfdisk*, *cfdisk* |
| [gdisk](/index.php/Gdisk "Gdisk") | No | Yes | *cgdisk*, *sgdisk* |
| [parted](/index.php/Parted "Parted") | Yes | Yes | [GParted](/index.php/GParted "GParted") |

下面是一个[partition scheme|分区格式]]的例子，包含两种分区表，使用一个新的连续分区方式，占据整个 `/dev/sd**x**` 设备. 请根据需要修改设备名、分区号。

| UEFI/GPT 分区示例 |
| 挂载点 | 分区 | [分区类型 (GUID)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | 启动标记 | 建议大小 |
| /boot | /dev/sd**x**1 | [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") | Yes | 260–512 MiB |
| [SWAP] | /dev/sd**x**2 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**3 | Linux | No | Remainder of the device |
| MBR/BIOS example layout |
| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | Bootable flag | Suggested size |
| [SWAP] | /dev/sd**x**1 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**2 | Linux | Yes | Remainder of the device |

### 格式化文件系统并使用swap

如果您想实现与 Windows 共存的双启动，在 UEFI/GPT 系统上不要格式化 UEFI 分区，因为这个分区包含 Windows *.efi* 启动文件。而且 Arch 应该按照同样的固件启动模式和本区组合。详见[Dual boot with Windows#Important information](/index.php/Dual_boot_with_Windows#Important_information "Dual boot with Windows").

仅仅分区是不够的，还需要 `mkfs` 将分区格式化为指定的[文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")。

先查看所有分区：

```
# lsblk /dev/sd*x*

```

建议用 `ext4` 文件系统格式化其它分区：

```
# mkfs.ext4 /dev/sd*xY*

```

若您分了一个 [swap](/index.php/Swap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Swap (简体中文)") 区，也不要忘了格式化并启用它：

```
# mkswap /dev/sda*X*
# swapon /dev/sda*X*

```

如果新创建了 UEFI 系统分区，需要格式化成 `fat32` 或 `vfat32` 文件系统，否则无法启动。Windows 双启动系统不要再格式化。

```
# mkfs.vfat -F32 /dev/sd*xY*

```

### 挂载分区

先挂载 `/` (root) 分区，其它目录都要在 / 分区中创建然后再挂载。在安装环境中用 `/mnt` 目录挂载 root：

```
# mount /dev/sd*xR* /mnt

```

然后挂载其余单独分区(除了 Swap)，比如 `/boot`，`/var`。先创建目录，然后挂载分区：

```
# mkdir /mnt/home
# mount /dev/sda2 /mnt/home

```

建议将 EFI 系统分区挂载到 `/mnt/boot`，其它方式参阅[EFISTUB](/index.php/EFISTUB "EFISTUB")。

```
# mkdir -p /mnt/boot
# mount /dev/sd*XY* /mnt/boot

```

挂载好设备，就可以安装 Arch 了.

## 安装

### 选择安装镜像

如果想要安装某个软件，必须先从 `/etc/pacman.d/mirrorlist` 中定义的[镜像](/index.php/Mirrors "Mirrors")站中下载安装包到本地。在live系统里，该文件中所有的镜像站都默认开启，并且按照镜像系统被创建时各镜像站的与官方镜像站的同步状态和速度来排序。

当系统在下载软件包的时候，列表中排的越靠前的镜像站优先级越高。你可以手动调整`/etc/pacman.d/mirrorlist`文件来将地理位置上离你比较近的镜像站放在文件最开头，当然，调整该文件应该以获得尽量大的下载速度为主要的标准。

mirrorlist 文件也会被 `pacstrap` 复制到新系统，所以最好现在就设置，以中科大源为例：

 `# nano /etc/pacman.d/mirrorlist` 
```
Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
...
```

如果您愿意，您可以只使用一个镜像并全删光其他行，但为保险，还是留其他几个离您较近的镜像作备用好。 更改镜像列表后请务必使用 `pacman -Syy` 强制刷新，详见 [Mirrors (简体中文)](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)").

### 安装基本软件包

使用 **pacstrap** 安装 [base](https://www.archlinux.org/groups/x86_64/base/) 软件组。这个组并没有包含全部 live 环境中的程序，有些需要额外安装，例如[btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)。[packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) 页面包含了它们的差异。

如果您想通过 [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 或者 [ABS (简体中文)](/index.php/ABS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ABS (简体中文)") 编译安装软件包,需要装上 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)：

```
# pacstrap -i /mnt base base-devel

```

使用 `-i` 选项时会在实际安装前进行确认。此章节会给您安装好最基本的 Arch 系统，其它软件以后会用 [pacman (简体中文)](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装得到。With the base group, the first [initramfs](/index.php/Initramfs "Initramfs") will be generated and installed to the new system's boot path; double-check output prompts `==> Image creation successful` for it.

## 配置

### fstab

用以下命令生成 [fstab](/index.php/Fstab "Fstab"). 之所以用 [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier "wikipedia:Universally unique identifier") 是因为它们能唯一且独立地标识，详见 [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab"). 如果您想用卷标，用 `-L` 代替 `-U` 即可。

```
# genfstab -U -p /mnt >> /mnt/etc/fstab

```

**强烈建议** 在执行完以上命令后，后检查一下生成的 `/mnt/etc/fstab` 文件是否正确。若在运行 *genfstab* 或是之后发生错误，后续修改请直接手动编辑 `fstab` 文件。详见 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")。

### chroot

将配置文件复制到`/mnt`的新系统 (例如 netctl 配置文件在 `/etc/netctl`), 然后 [chroot](/index.php/Change_root_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Change root (简体中文)") 到新系统：

```
# arch-chroot /mnt /bin/bash

```

### Locale

本地化的程序与库若要本地化文本，都依赖 [Locale](/index.php/Locale "Locale"), 后者明确规定地域、货币、时区日期的格式、字符排列方式和其他本地化标准等等。在下面两个文件设置：`locale.gen` 与 `locale.conf`.

`/etc/locale.gen`是一个仅包含注释文档的文本文件。指定您需要的本地化类型，只需移除对应行前面的注释符号（`＃`）即可，建议选择帶`UTF-8`的項：

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_TW.UTF-8 UTF-8

```

接着执行`locale-gen`以生成locale讯息：

```
# locale-gen

```

`/etc/locale.gen` 生成指定的本地化文件，每次 [glibc](https://www.archlinux.org/packages/?name=glibc) 更新之后也会运行 `locale-gen`。

创建 `locale.conf` 并提交您的本地化选项：

**Tip:** 将系统 locale 设置为`en_US.UTF-8`，系统的 Log 就会用英文显示，这样更容易问题的判断和处理。用户可以设置自己的 locale，详情参阅[Locale#Per user](/index.php/Locale#Per_user "Locale").

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf

```

**警告:** 不推荐在此设置任何中文locale，或导致tty乱码。

### 终端字体和键盘映射

**提示:** 对于大多中文用户，可忽略此章节。

如果您在[#设置键盘布局](#.E8.AE.BE.E7.BD.AE.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80) 时就已修改键盘布局和字体过，您就得再相应地编辑 `/etc/vconsole.conf` 以使该变动对新系统生效，比如：

 `/etc/vconsole.conf` 
```
KEYMAP=de-latin1
FONT=lat9w-16
```

**警告:** 如果您设置的 `KEYMAP` 与 *loadkeys* 变量并不一样，那当您 [#Set the root password](#Set_the_root_password) 并重启后，可能没法再正常登录新系统了，因为一些键在两种布局的映射下并不一致。

此章节只对您的虚拟终端生效，即对 [Xorg](/index.php/Xorg "Xorg") 无效，详见 [Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### 时间

可用的时区全集中在 `/usr/share/*Zone*/*SubZone*` 目录里了。选择时区：

```
 # tzselect

```

将 `/etc/localtime` 软链接到 `/usr/share/zoneinfo/*Zone*/*SubZone*`，以上海为例：

```
# ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

建议设置[时间标准](/index.php/Time_standard "Time standard") 为 UTC，并调整 [时间漂移](/index.php/Time_skew "Time skew"):

```
# hwclock --systohc --utc

```

系统上安装的其它操作系统也应该一起调整。

### Initramfs

因为用 *pacstrap* 安装 {[linux](https://www.archlinux.org/packages/?name=linux) 时就会自动运行 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")，大部分用户都不需要重新生成 intramfs 镜像。

如果有定制需求，请阅读[re-generate the initramfs image](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")。然后运行：

```
# mkinitcpio -p linux

```

### 设置 Root 密码

用 `passwd` 设置一个 root 密码：

```
# passwd

```

### 安装 bootloader

[启动加载器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")页面介绍了可用选项和配置方法。包括 [grub](/index.php/Grub "Grub") (BIOS/UEFI), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (UEFI) 和 [syslinux](/index.php/Syslinux "Syslinux") (BIOS)等.

Intel CPU 也需要安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) 并根据 [Microcode](/index.php/Microcode "Microcode") 配置 boot loader.

### 配置网络

该过程与[#建立网络连接](#.E5.BB.BA.E7.AB.8B.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5)基本一致，只不过该配置在新系统每次开机时都会自动生效。

**注意:** 了解更多网络配置相关信息，请访问 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)") 及 [Wireless network configuration (简体中文)](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)").

#### 主机名

要设置 [hostname](/index.php/Hostname "Hostname")，将其[添加](/index.php/Add "Add") 到 `/etc/hostname`, *myhostname* 是需要的主机名:

```
# echo ***myhostname*** > /etc/hostname

```

建议在 `/etc/hosts` 添加同样的主机名：

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost	 *myhostname*	
::1		localhost.localdomain	localhost	 *myhostname*
```

#### 有线网络

如果您只用单一且固定的有线网络连接，启动 [dhcpcd](/index.php?title=Ic&action=edit&redlink=1 "Ic (page does not exist)") 服务，`*interface*` 是您的网络接口名：

```
# systemctl enable dhcpcd@*interface*.service

```

#### 无线网络

安装 [iw](https://www.archlinux.org/packages/?name=iw), [dialog](https://www.archlinux.org/packages/?name=dialog) 和 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), 您要靠它们连网：

```
# pacman -S iw wpa_supplicant dialog

```

可能还需要[安装固件](/index.php/Wireless_network_configuration#Installing_driver.2Ffirmware "Wireless network configuration")。

如果使用*wifi-menu* 配置网络，在执行完所有设置之后、重启然后再进行设置，以避免进程间冲突。详情请阅读 [Netctl](/index.php/Netctl "Netctl")。

### 设置 root 密码

设置 root [密码](/index.php/Password "Password"):

```
 # passwd

```

### 卸载分区并重启系统

离开 chroot 环境：

```
# exit

```

*systemd* 在关机时会自动卸载分区，为了确保安全，可以用 `umount -R /mnt` 手动卸载分区。如果分区被占用，可以用 [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)")检查原因。

重启计算机：

```
# reboot

```

移除安装媒介，并还原 BIOS 中的启动选项。

## 安装之后

您现在应该有了一个完全可用的 Arch 系统，以此为起点，您可以将这些优雅的工具加以改造成理想的样子。*强烈*建议您阅读 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")，特别是前两个部分.

请继续阅读 [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)") 的剩余页面，它包含了安装后的众多教程，包括设置图形用户界面，声卡和触摸板等等。

如果想捣鼓一大堆应用程序，详见 [List of applications (简体中文)](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)").

[Arch Linux 中文化](/index.php/Arch_Linux_%E4%B8%AD%E6%96%87%E5%8C%96 "Arch Linux 中文化") 页面还包含了关于系统、软件中文支持的内容。
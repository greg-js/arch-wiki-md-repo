相关文章

*   [Boot loaders (简体中文)](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")
*   [Master Boot Record (简体中文)](/index.php/Master_Boot_Record_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Master Boot Record (简体中文)")
*   [GUID Partition Table (简体中文)](/index.php/GUID_Partition_Table_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GUID Partition Table (简体中文)")
*   [Unified Extensible Firmware Interface (简体中文)](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)")
*   [mkinitcpio (简体中文)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")
*   [init](/index.php/Init "Init")
*   [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")
*   [fstab (简体中文)](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")
*   [Autostarting](/index.php/Autostarting "Autostarting")

**翻译状态：** 本文是英文页面 [Arch boot process](/index.php/Arch_boot_process "Arch boot process") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Arch+boot+process&diff=0&oldid=477810)可以查看翻译后英文页面的改动。

为了启动 Arch Linux，一个与 Linux 兼容的 [启动引导器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")，比如 [GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") 或者 [Syslinux](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 必须事先被安装到[主引导记录](/index.php/%E4%B8%BB%E5%BC%95%E5%AF%BC%E8%AE%B0%E5%BD%95 "主引导记录")或者 [GUID 分区表](/index.php/GUID_Partition_Table_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GUID Partition Table (简体中文)")。启动引导程序负责在初始化启动进程之前，加载好内核和 [initial ramdisk](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")。具体过程因 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 和 [UEFI](/index.php/UEFI "UEFI") 系统而异，细节在正文中给出。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 固件种类](#固件种类)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 系统初始化](#系统初始化)
    *   [2.1 BIOS](#BIOS_2)
    *   [2.2 UEFI](#UEFI_2)
    *   [2.3 UEFI 的多重引导](#UEFI_的多重引导)
*   [3 启动加载器](#启动加载器)
    *   [3.1 功能比较](#功能比较)
*   [4 内核](#内核)
*   [5 initramfs](#initramfs)
*   [6 Init 流程](#Init_流程)
*   [7 Getty](#Getty)
*   [8 显示管理器](#显示管理器)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI、 xinit 或者 wayland](#GUI、_xinit_或者_wayland)
*   [12 参见](#参见)

## 固件种类

### BIOS

所谓 BIOS 或 Basic Input-Output System, 就是开机时第一个被执行的程序，又名固件。一般来说它储存在主板上的一块闪存中，与硬盘彼此独立。

BIOS 被启动后，会按启动顺序加载磁盘的前 512 字节，即[主引导记录](/index.php/%E4%B8%BB%E5%BC%95%E5%AF%BC%E8%AE%B0%E5%BD%95 "主引导记录")，前 440 字节包含某个启动引导器，像 [GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") 、[Syslinux](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 和 [LILO](/index.php/LILO "LILO") 之类的第一启动阶段代码。因为空间太小了，后续的启动代码保存在磁盘上，最后启动引导器又通过「链式引导」，或是直接加载内核，以加载一个操作系统。

### UEFI

UEFI 不仅能读取分区表，还能自动支持文件系统。所以它不像 BIOS，已经没有仅仅 440 字节可执行代码即 MBR 的限制了，它完全用不到 MBR。

UEFI 主流都支持 MBR 和 GPT 分区表。Apple-Intel Macs 上的 EFI 还支持 Apple 专用分区表。绝大部分 UEFI 固件支持软盘上的 FAT12，硬盘上的 FAT16、FAT32 文件系统，以及 CD/DVDs 的 IS09660 和 UDF。Intel Macs 的 EFI 还额外支持 HFS/HFS+ 文件系统。

不管第一块上有没有 MBR，UEFI 都不会执行它。相反，它依赖分区表上的一个特殊分区，叫 EFI 系统分区，里面有 UEFI 所要用到的一些文件。计算机供应商可以在 `<EFI 系统分区>/EFI/<VENDOR NAME>/` 文件夹里放官方指定的文件，还能用固件或它的 shell，即 UEFI shell，来启动引导程序。EFI 系统分区一般被格式化成 FAT32，或比较非主流的 FAT16。

## 系统初始化

### BIOS

1.  开机时[加电自检](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test")。
2.  加电自检后，BIOS 初始化一些必要的硬件以准备引导，比如硬盘和键盘等。
3.  BIOS 执行在「BIOS 硬盘顺序」中的第一块硬盘上的前 440 字节代码，即[主引导记录](/index.php/%E4%B8%BB%E5%BC%95%E5%AF%BC%E8%AE%B0%E5%BD%95 "主引导记录")。
4.  MBR 接管后，执行它之后的第二阶段代码，如果后者存在的话，它一般就是[启动引导器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")。
5.  第二阶段代码会读取它的支持文件和配置文件。

### UEFI

1.  系统开机 - 上电自检（Power On Self Test 或 POST）。
2.  UEFI 固件被加载，并由它初始化启动要用的硬件。
3.  固件读取其引导管理器以确定从何处（比如，从哪个硬盘及分区）加载哪个 UEFI 应用。
4.  固件按照引导管理器中的启动项目，加载UEFI 应用。
5.  已启动的 UEFI 应用还可以启动其他应用（对应于 UEFI shell 或 rEFInd 之类的引导管理器的情况）或者启动内核及initramfs（对应于GRUB之类引导器的情况），这取决于 UEFI 应用的配置。

**Note:** 在有些 UEFI 系统中，唯一可行的启动时（如果应用没有在 UEFI 启动菜单定制条目的话）加载 UEFI 应用的方法是把它放在此固定位置：`<EFI SYSTEM PARTITION>/EFI/boot/bootx64.efi` （对于 64 位的 x86 系统）

### UEFI 的多重引导

因为每个操作系统或者提供者都可以维护自己的 EFI 系统分区中的文件，同时不影响其他系统，所以 UEFI 的多重启动只是简单的运行不同的UEFI 程序，对应于特定操作系统的引导程序。这避免了依赖 chainloading 机制（通过一个[启动引导程序](/index.php/Boot_loader "Boot loader")加载另一个引导程序，来切换操作系统）。

参阅 [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## 启动加载器

启动加载器是 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 或 [UEFI](/index.php/UEFI "UEFI") 启动的第一个程序。它负责使用正确的 [内核参数](/index.php/Kernel_parameters "Kernel parameters") 加载内核, 并根据配置文件加载 [初始化 RAM disk](/index.php/Mkinitcpio "Mkinitcpio")。对于 UEFI，内核本身可以由 UEFI 使用 EFI boot stub 直接启动，也可以使用单独的引导加载程序或引导管理器来在引导之前编辑内核参数。

**Note:** 加载 [Microcode](/index.php/Microcode "Microcode") 补丁要求对启动加载器的配置进行调整。[[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

### 功能比较

**Note:**

*   只需要启动加载器兼容内核和initramfs所处的位置（`/boot`）的文件系统兼容即可。
*   因为GPT是UEFI规范的一部分，所以所有的UEFI启动加载器都支持GPT磁盘。在BIOS上使用GPT磁盘是可行的，要么根据[Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html)使用 "hybrid booting"，要么使用新的 [GPT-only](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt) 协议。但是这个协议可能在某些BIOS实现上出问题，参考 [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios)。
*   在文件系统支持中提到的“加密”是[filesystem级别加密](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption")，和[block级别加密](/index.php/Dm-crypt "Dm-crypt")没有任何关系。

| Name | Firmware | [Partition table](/index.php/Partition_table "Partition table") | Multi-boot | [File systems](/index.php/File_systems "File systems") | Notes |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [MBR](/index.php/MBR "MBR") | [GPT](/index.php/GPT "GPT") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4 "Ext4") | ReiserFS | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | – | Yes | Yes | Yes | – | – | – | – | 仅 ESP | – | 内核会变成一个 EFI executable 来被 [UEFI](/index.php/UEFI "UEFI") 固件或者其他启动加载器加载。 |
| [Clover](/index.php/Clover "Clover") | 模拟 UEFI | Yes | Yes | Yes | Yes | No | 不支持加密 | No | Yes | No | 修改版的 rEFIt，用来运行[黑苹果](https://en.wikipedia.org/wiki/Hackintosh "wikipedia:Hackintosh")。 |
| [GRUB](/index.php/GRUB "GRUB") | Yes | Yes | Yes | Yes | Yes | 不支持 zstd 压缩 | Yes | Yes | Yes | Yes | 在 BIOS/GPT 配置下需要一个 [BIOS启动分区](/index.php/BIOS_boot_partition "BIOS boot partition")。
支持RAID, LUKS1 和 LVM (但是不支持thin provisioned volumes)。 |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes | Yes | Yes | 不支持加密和 zstd 压缩 | 不支持加密 | 不支持 tail-packing 功能 | Yes | No | 支持自动寻找内核和确定内核参数而不需要手动配置。 |
| [Syslinux](/index.php/Syslinux "Syslinux") | Yes | [有限支持](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | Yes | Yes | [有限支持](/index.php/Syslinux#Chainloading "Syslinux") | 不支持: 跨设备卷、压缩、加密 | 不支持加密 | No | Yes | 仅限MBR；不支持 sparse inodes | 不支持某些 [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)") 功能 [[2]](https://wiki.syslinux.org/wiki/index.php?title=Filesystem)
启动加载器只能够访问它所处的文件系统。[[3]](https://bugzilla.syslinux.org/show_bug.cgi?id=33) |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | No | Yes | [仅限手动安装](https://github.com/systemd/systemd/issues/1125) | Yes | Yes | No | No | No | 仅 ESP | No | [ESP](/index.php/ESP "ESP")以外的分区上的binaries它都启动不了. |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Yes | No | Yes | No | Yes | No | No | Yes | Yes | 仅 v4 | [停止开发](https://www.gnu.org/software/grub/grub-legacy.html) in favor of [GRUB](/index.php/GRUB "GRUB"). |
| [LILO](/index.php/LILO "LILO") | Yes | No | Yes | No | Yes | No | 不支持加密 | Yes | Yes | [Yes](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [停止开发](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) 因为某些局限性 (e.g. with Btrfs, GPT, RAID). |

1.  一种 [启动管理器](https://www.rodsbooks.com/efi-bootloaders/principles.html)。它只能启动其他 EFI 应用程序，例如，使用 `CONFIG_EFI_STUB=y` 和 Windows `bootmgfw.efi` 构建 Linux kernel images。

更多信息，参见 [Wikipedia:Comparison of boot loaders](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders")。

## 内核

内核是操作系统的核心。它运行于一个叫「内核空间」的底层上，负责机器硬件和应用程序之间的交流。为了尽可能充分地压榨 CPU 性能，内核使用调度器，通过一定的优先级算法将 CPU 按照时间动态的分配给各个程序。让我们感觉就像所有程序都在同时使用 CPU 一样。

## initramfs

在 [boot loader](#Boot_loader) 加载 kernel 和可用的 initramfs 文件，并执行 kernel 之后，kernel 将 initramfs（初始RAM文件系统）压缩包解压缩到（然后清空）rootfs（初始根文件系统，特别是ramfs或tmpfs）。首先提取的 initramfs 是在 kernel 构建过程中嵌入 kernel 二进制Update translation.的 initramfs，然后提取可用的外部 initramfs 文件。因此，外部 initramfs 中的文件会覆盖嵌入式 initramfs 中具有相同名称的文件。然后， kernel 执行 `/init` （在rootfs中）作为第一个进程。*early userspace*开始。

Arch Linux 对内置的 initramfs 使用一个空的存档（在构建Linux时是默认的）。有关外部 initramfs 的更多信息和 Arch 特定的信息，请参见 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")。

initramfs 之所以存在，是为了帮系统访问真正的根文件系统（参见 [Arch filesystem hierarchy (简体中文)](/index.php/Arch_filesystem_hierarchy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch filesystem hierarchy (简体中文)")）。也就是说，那些硬件 IDE, SCSI, SATA, USB/FW 所要求的 kernel 模块，如果并没有内置在 kernel 里，就会被 initramfs 负责加载。一旦通过 [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)") 之类的程序或脚本加载好模块，启动流程才会继续下去。所以，initramfs 只要有能够让系统访问真实根文件系统的模块就可以了，不用尽可能地包含一切模块。当然，其它真正有用的模块之后会在 init 流程中被 udev 加载好。

## Init 流程

在「早期用户空间」的最终环节里，**真正**的根文件系统被挂载好后，就会替换掉原来的**伪**根文件系统。接着 `/sbin/init` 被执行，同样也替换掉原来的 `/init` 进程。Arch 御用的 [init](/index.php/Init "Init") 就是 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)").

## Getty

[init](/index.php/Init "Init") 为每一个 [虚拟终端](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 调用 [getty](/index.php/Getty "Getty")，前者一般有六个，每个虚拟终端都会初始化 tty 并请求输入用户名和密码。当在某虚拟终端输入用户名和密码后，其 getty 会通过 `/etc/passwd` 检查是否正确，如果正确，就接着调用 [login](#Login), 此外 getty 也可能会改启动一个显示管理器。

## 显示管理器

[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)"), 可以配置为代替原来的 getty 登录命令行提示符。

为了在引导后自动初始化显示管理器，必须通过[systemd](/index.php/Systemd "Systemd")手动启用服务单元。 有关启用和启动服务单元的更多信息，请参见[systemd＃使用单元](/index.php?title=Systemd%EF%BC%83%E4%BD%BF%E7%94%A8%E5%8D%95%E5%85%83&action=edit&redlink=1 "Systemd＃使用单元 (page does not exist)")。

## Login

所谓的 *login* 程序会为用户启动一个设置了环境变量的「会话」，接着根据 `/etc/passwd` 的配置启动用户专用 shell。

在成功登录后，刚刚启动登录 shell 之前，*login* 程序显示 [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) 。在这里，您可以显示服务条款，以提醒用户您的本地政策或您想告诉他们的任何内容。

## Shell

一旦用户专用的 [shell](/index.php/Shell "Shell") 启动了，它会在显示命令行提示符前，执行一个「有可执行性的配置文件」，比如 [.bashrc](/index.php/.bashrc ".bashrc"). 如果用户有设定了 [Start X at login](/index.php/Start_X_at_login "Start X at login"), 原来那个「有可执行性的配置文件」会调用 [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## GUI、 xinit 或者 wayland

[xinit](/index.php/Xinit "Xinit") 也会调用用户的 [.xinitrc](/index.php/.xinitrc ".xinitrc") 这个「有可执行性的配置文件」，后者一般用来启动一个 [窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")。如果用户退出了窗口管理器、xinit、 startx 和 shell login 就会先后中断，返回到 [getty](#Getty).

## 参见

*   [Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
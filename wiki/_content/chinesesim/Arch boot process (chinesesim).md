**翻译状态：** 本文是英文页面 [Arch_Boot_Process](/index.php/Arch_Boot_Process "Arch Boot Process") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-25，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Boot_Process&diff=0&oldid=326515)可以查看翻译后英文页面的改动。

为了启动 Arch Linux，一个与 Linux 兼容的 [启动引导程序](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")，比如 [GRUB (简体中文)](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)")或者 [Syslinux (简体中文)](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)")，必须事先被安装到 [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") 或者 [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). 启动引导程序负责在初始化启动进程之前，加载好内核和 [initial ramdisk](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)"). 具体过程因 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 和 [UEFI](/index.php/UEFI "UEFI") 系统而异，细节在正文中给出。

## Contents

*   [1 固件种类](#.E5.9B.BA.E4.BB.B6.E7.A7.8D.E7.B1.BB)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 引导过程](#.E5.BC.95.E5.AF.BC.E8.BF.87.E7.A8.8B)
    *   [2.1 BIOS](#BIOS_2)
    *   [2.2 UEFI](#UEFI_2)
*   [3 内核](#.E5.86.85.E6.A0.B8)
*   [4 initramfs](#initramfs)
*   [5 Init 流程](#Init_.E6.B5.81.E7.A8.8B)
*   [6 Getty](#Getty)
*   [7 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
*   [8 Login](#Login)
*   [9 Shell](#Shell)
*   [10 xinit](#xinit)
*   [11 参见](#.E5.8F.82.E8.A7.81)

## 固件种类

### BIOS

所谓 BIOS 或 Basic Input-Output System, 就是开机时第一个被执行的程序，又名固件。一般来说它被储存在主板上的一块闪存，与硬盘彼此独立。BIOS 被启动后，它接着会执行第一个硬盘上的前 440 字节代码，即 [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), 由于代码的储存空间实在太小了，所以实际代码常常是某个启动引导器，像 [GRUB (简体中文)](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)"), [Syslinux (简体中文)](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 和 [LILO](/index.php/LILO "LILO") 之类的。最后启动引导器又通过「链式引导」，或是直接加载内核，以加载一个操作系统

### UEFI

UEFI 不光能读取分区表，还能自动支持文件系统。所以它不像 BIOS, 已经没有只能执行 440 字节代码即 MBR 的限制了，它完全用不到 MBR.

UEFI 主流都支持 MBR 和 GPT 分区表。Apple-Intel Macs 上的 EFI 还支持 Apple 专用分区表。绝大部分 UEFI 固件支持软盘上的 FAT12, 硬盘上的 FAT16, FAT32 文件系统，以及 CD/DVDs 的 IS09660 和 UDF. Intel Macs 的 EFI 还额外支持 HFS/HFS+ 文件系统。

不管第一块上有没有 MBR, UEFI 都不会执行它。相反，它依赖分区表上的一个特殊分区，叫 EFI 系统分区，里面有 UEFI 所要用到的一些文件。计算机供应商可以在 `<EFI 系统分区>/EFI/<VENDOR NAME>/` 文件夹里放官方指定的文件，还能用固件或它的 shell, 即 UEFI shell, 来启动引导程序。EFI 系统分区一般被格式化成 FAT32, 或比较非主流的 FAT16.

UEFI 下每一个程序，无论它是某个 OS 引导器还是某个内存测试或数据恢复的工具，都要兼容于 EFI 固件位数或体系结构。目前主流的 UEFI 固件，包括近期的 Apple Macs, 都采用了 x86_64 EFI 固件。目前还在用 IA32 即 32 位的 EFI 的已知设备只有于 2008 年前生产的 Apple Macs, 一些 Intel Cloverfield 超级本和采用 EFI 1.10 固件的 Intel 服务器主板。

不像 x86_64 Linux 和 Windows 操作系统，x86_64 EFI 不能兼容 32 位 EFI 程序。所以 UEFI 应用程序必须依固件处理器位数／体系结构编译而成。

## 引导过程

### BIOS

1.  开机时[加电自检](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test")。
2.  加电自检后，BIOS 初始化一些必要的硬件以准备引导，比如硬盘和键盘等。
3.  BIOS 执行在「BIOS 硬盘顺序」中的第一块硬盘上的前 440 字节代码，即 [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record").
4.  MBR 接管后，执行它之后的第二阶段代码，如果后者存在的话，它一般就是[启动引导器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")。
5.  被执行的第二阶段代码会读取它的支持以及配置文件。
6.  启动引导器按着配置文件，加载内核和 initramfs 进内存并启动前者。

### UEFI

参见 [Unified Extensible Firmware Interface#Boot Process under UEFI](/index.php/Unified_Extensible_Firmware_Interface#Boot_Process_under_UEFI "Unified Extensible Firmware Interface").

## 内核

内核是操作系统的核心。它运行于一个叫「内核空间」的底层上，负责机器硬件和应用程序之间的交流。为了尽可能充分地压榨 CPU 性能，内核使用调度器，通过一定的优先级算法将 CPU 按照时间动态的分配给各个程序。让我们感觉就像所有程序都在同时使用 CPU 一样。

## initramfs

内核被加载后，它就会解压 [mkinitcpio (简体中文)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")， 又名 initial RAM filesystem, 后者会伪装成一个被初始化了的根文件系统。内核接着会执行 `/init` 作为第一条进程。传说中的「用户空间」就这么被启动了。

initramfs 之所以存在，是为了帮系统访问真正的根文件系统（参见 [Arch filesystem hierarchy (简体中文)](/index.php/Arch_filesystem_hierarchy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch filesystem hierarchy (简体中文)")）。也就是说，那些硬件 IDE, SCSI, SATA, USB/FW 所要求的内核模块，如果并没有内置在内核里，就会被 initramfs 负责加载。一旦通过 [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)") 之类的程序或脚本加载好模块，启动流程才会继续下去。所以啊，initramfs 只要有能够让系统访问真・根文件系统的模块就可以了，不用尽可能地包含一切模块。当然，其它真正有用的模块之后会在 init 流程中被 udev 加载好。

## Init 流程

在「早期用户空间」的最终环节里，真・根文件系统被挂载好后，就会替换掉原来的伪・根文件系统。接着 `/sbin/init` 被执行，同样也替换掉原来的 `/init` 进程。Arch 御用的 [init](/index.php/Init "Init") 就是 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)").

## Getty

[init](/index.php/Init "Init") 为每一个 [虚拟终端](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 调用 [getty](/index.php/Getty "Getty")，前者一般有六个，每个虚拟终端都会初始化 tty 并请求输入用户名和密码。当在某虚拟终端输入用户名和密码后，其 getty 会通过 `/etc/passwd` 检查是否正确，如果正确，就接着调用 [login](#Login), 即为用户启动一个「会话」，接着根据 `/etc/passwd` 文件启动用户专用 shell. 此外，getty 也可能会改启动一个显示管理器。

## 显示管理器

如果事先装了某个 [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)"), 它会代替原来的 getty 登录命令行提示符而启动。如果没有显示管理器，getty 只会显示向用户请求用户名和密码以登录的若干命令行，以准备调用 [login](#Login).

## Login

所谓的 *login* 程序会为用户启动一个设置了环境变量的「会话」，接着根据 `/etc/passwd` 配置以启动用户专用 shell.

## Shell

一旦用户专用的 [shell](/index.php/Shell "Shell") 启动了，它会在显示命令行提示符前，执行一个「有可执行性的配置文件」，比如 [.bashrc](/index.php/.bashrc ".bashrc"). 如果用户有设定了 [Start X at login](/index.php/Start_X_at_login "Start X at login"), 原来那个「有可执行性的配置文件」会调用 [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## xinit

[xinit](/index.php/Xinit "Xinit") 也会调用用户的 [.xinitrc](/index.php/.xinitrc ".xinitrc")这个「有可执行性的配置文件」，后者一般用来启动一个 [窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")。如果用户退出了窗口管理器，xinit, startx, shell login 就会先后中断，返回到 getty.

## 参见

*   [Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
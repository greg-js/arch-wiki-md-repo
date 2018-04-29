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

**翻译状态：** 本文是英文页面 [Arch_Boot_Process](/index.php/Arch_Boot_Process "Arch Boot Process") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Boot_Process&diff=0&oldid=477810)可以查看翻译后英文页面的改动。

为了启动 Arch Linux，一个与 Linux 兼容的 [启动引导器](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")，比如 [GRUB](/index.php/GRUB_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB (简体中文)") 或者 [Syslinux](/index.php/Syslinux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Syslinux (简体中文)") 必须事先被安装到[主引导记录](/index.php/%E4%B8%BB%E5%BC%95%E5%AF%BC%E8%AE%B0%E5%BD%95 "主引导记录")或者 [GUID 分区表](/index.php/GUID_Partition_Table_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GUID Partition Table (简体中文)")。启动引导程序负责在初始化启动进程之前，加载好内核和 [initial ramdisk](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")。具体过程因 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 和 [UEFI](/index.php/UEFI "UEFI") 系统而异，细节在正文中给出。

## Contents

*   [1 固件种类](#.E5.9B.BA.E4.BB.B6.E7.A7.8D.E7.B1.BB)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 系统初始化](#.E7.B3.BB.E7.BB.9F.E5.88.9D.E5.A7.8B.E5.8C.96)
    *   [2.1 BIOS](#BIOS_2)
    *   [2.2 UEFI](#UEFI_2)
    *   [2.3 UEFI 的多重引导](#UEFI_.E7.9A.84.E5.A4.9A.E9.87.8D.E5.BC.95.E5.AF.BC)
*   [3 启动加载器](#.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)
*   [4 内核](#.E5.86.85.E6.A0.B8)
*   [5 initramfs](#initramfs)
*   [6 Init 流程](#Init_.E6.B5.81.E7.A8.8B)
*   [7 Getty](#Getty)
*   [8 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
*   [9 Login](#Login)
    *   [9.1 每日信息](#.E6.AF.8F.E6.97.A5.E4.BF.A1.E6.81.AF)
*   [10 Shell](#Shell)
*   [11 xinit](#xinit)
*   [12 参见](#.E5.8F.82.E8.A7.81)

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

因为每个操作系统或者提供者都可以维护自己的 EFI 系统分区中的文件，同时不影响其他系统，所以 UEFI 的多重启动只是简单的运行不同的UEFI 程序，对应于特定操作系统的引导程序。这避免了依赖 chainloading 机制（通过一个[启动引导程序](/index.php/Boot_loaders "Boot loaders")加载另一个引导程序，来切换操作系统）。

参阅 [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## 启动加载器

启动加载器是 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 或 [UEFI](/index.php/UEFI "UEFI") 启动的第一个程序。负责使用正确的[内核](/index.php/Kernel_parameters "Kernel parameters")加载设备模块, 并[启动初始 RMA](/index.php/Mkinitcpio "Mkinitcpio")。

## 内核

内核是操作系统的核心。它运行于一个叫「内核空间」的底层上，负责机器硬件和应用程序之间的交流。为了尽可能充分地压榨 CPU 性能，内核使用调度器，通过一定的优先级算法将 CPU 按照时间动态的分配给各个程序。让我们感觉就像所有程序都在同时使用 CPU 一样。

## initramfs

内核被加载后，它就会解压 [mkinitcpio (简体中文)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")， 又名 initial RAM filesystem, 后者会伪装成一个已初始化的根文件系统。内核接着会执行 `/init` 作为第一条进程。传说中的「用户空间」就这么被启动了。

initramfs 之所以存在，是为了帮系统访问真正的根文件系统（参见 [Arch filesystem hierarchy (简体中文)](/index.php/Arch_filesystem_hierarchy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch filesystem hierarchy (简体中文)")）。也就是说，那些硬件 IDE, SCSI, SATA, USB/FW 所要求的内核模块，如果并没有内置在内核里，就会被 initramfs 负责加载。一旦通过 [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)") 之类的程序或脚本加载好模块，启动流程才会继续下去。所以，initramfs 只要有能够让系统访问真实根文件系统的模块就可以了，不用尽可能地包含一切模块。当然，其它真正有用的模块之后会在 init 流程中被 udev 加载好。

## Init 流程

在「早期用户空间」的最终环节里，**真正**的根文件系统被挂载好后，就会替换掉原来的**伪**根文件系统。接着 `/sbin/init` 被执行，同样也替换掉原来的 `/init` 进程。Arch 御用的 [init](/index.php/Init "Init") 就是 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)").

## Getty

[init](/index.php/Init "Init") 为每一个 [虚拟终端](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 调用 [getty](/index.php/Getty "Getty")，前者一般有六个，每个虚拟终端都会初始化 tty 并请求输入用户名和密码。当在某虚拟终端输入用户名和密码后，其 getty 会通过 `/etc/passwd` 检查是否正确，如果正确，就接着调用 [login](#Login), 此外 getty 也可能会改启动一个显示管理器。

## 显示管理器

[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)"), 可以配置为代替原来的 getty 登录命令行提示符。

## Login

所谓的 *login* 程序会为用户启动一个设置了环境变量的「会话」，接着根据 `/etc/passwd` 配置以启动用户专用 shell.

### 每日信息

*login* 程序会在成功登录后显示 [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) 的内容，可以显示服务协议或希望告诉用户的信息。

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
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
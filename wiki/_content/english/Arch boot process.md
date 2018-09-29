Related articles

*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init "Init")
*   [systemd](/index.php/Systemd "Systemd")
*   [fstab](/index.php/Fstab "Fstab")
*   [Autostarting](/index.php/Autostarting "Autostarting")

In order to boot Arch Linux, a Linux-capable [boot loader](#Boot_loader) such as [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") must be installed to the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") or the [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). The boot loader is responsible for loading the kernel and [initial ramdisk](/index.php/Initial_ramdisk "Initial ramdisk") before initiating the boot process. The procedure is quite different for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") and [UEFI](/index.php/UEFI "UEFI") systems, the detailed description is given on this or linked pages.

## Contents

*   [1 Firmware types](#Firmware_types)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 System initialization](#System_initialization)
    *   [2.1 Under BIOS](#Under_BIOS)
    *   [2.2 Under UEFI](#Under_UEFI)
    *   [2.3 Multibooting in UEFI](#Multibooting_in_UEFI)
*   [3 Boot loader](#Boot_loader)
    *   [3.1 Feature comparison](#Feature_comparison)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 Init process](#Init_process)
*   [7 Getty](#Getty)
*   [8 Display Manager](#Display_Manager)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI, xinit or wayland](#GUI.2C_xinit_or_wayland)
*   [12 See also](#See_also)

## Firmware types

### BIOS

A [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or Basic Input-Output System is the very first program (firmware) that is executed once the system is switched on. In most cases it is stored in a flash memory in the motherboard itself and independent of the system storage.

The BIOS loads the beginning 512 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) of the first valid disk in the BIOS disk order. Of these 512 bytes, the first 440 contains the first stage of a [boot loader](#Boot_loader) like [GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") or [LILO](/index.php/LILO "LILO"). Since very little can be achieved by a program of this size, the second stage (residing on the next disk sectors) is loaded from here and looks up a file stored on the partition itself (the actual boot loader). This then loads an operating system by either chain-loading or directly loading the operating system kernel.

### UEFI

UEFI has support for reading both the partition table as well as understanding filesystems. Hence it is not limited by 440 byte code limitation (MBR boot code) as in BIOS systems. It does not use the MBR boot code at all.

The commonly used UEFI firmwares support both MBR and GPT [partition table](/index.php/Partition_table "Partition table"). EFI in Apple-Intel Macs are known to also support Apple Partition Map besides MBR and GPT. Most UEFI firmwares have support for accessing FAT12 (floppy disks), FAT16 and FAT32 filesystems in HDDs and ISO9660 (and UDF) in CD/DVDs. EFI in Intel Macs can also access HFS/HFS+ filesystems, in addition to the mentioned ones.

UEFI does not launch any boot code in the MBR whether it exists or not. Instead it uses a special partition in the partition table called [EFI system partition](/index.php/EFI_system_partition "EFI system partition") in which files required to be launched by the firmware are stored. Each vendor can store its files under `<EFI SYSTEM PARTITION>/EFI/<VENDOR NAME>/` folder and can use the firmware or its shell ([UEFI shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface")) to launch the boot program. An EFI System Partition is usually formatted as [FAT32](/index.php/FAT32 "FAT32") or (less commonly) FAT16.

## System initialization

### Under BIOS

1.  System switched on - [Power-on self-test](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") or POST process.
2.  After POST, BIOS initializes the necessary system hardware for booting (disk, keyboard controllers etc.).
3.  BIOS launches the first 440 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) of the first disk in the BIOS disk order.
4.  The MBR boot code then takes control from BIOS and launches its next stage code (if any) (mostly [boot loader](#Boot_loader) code).
5.  The actual [boot loader](#Boot_loader), such as [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux"), is launched.

### Under UEFI

1.  System switched on. The Power On Self Test (POST) is executed.
2.  UEFI firmware is loaded. Firmware initializes the hardware required for booting.
3.  Firmware reads the boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. from which disk and partition). A boot entry could simply be a disk. In this case the firmware looks for an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") on that disk and tries to find the fallback UEFI application `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` on [32-bit EFI systems](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). This is how UEFI bootable thumb drives work.
4.  Firmware launches the UEFI application.
    *   This could be a boot loader, e.g. the Arch kernel itself (since [EFISTUB](/index.php/EFISTUB "EFISTUB") is enabled by default).
    *   It could be some other application such as a shell or a boot manager like [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), [rEFInd](/index.php/REFInd "REFInd").

If [Secure Boot](/index.php/Secure_Boot "Secure Boot") is enabled, the boot process will verify authenticity of the EFI binary by signature.

**Note:** Some UEFI systems have a very basic boot manager, which can only use the fallback UEFI application path.

### Multibooting in UEFI

Since each OS or vendor can maintain its own files within the EFI System Partition without affecting the other, multi-booting using UEFI is just a matter of launching a different UEFI application corresponding to the particular OS's boot loader. This removes the need for relying on chainloading mechanisms of one [boot loader](#Boot_loader) to load another OS.

See also [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Boot loader

The boot loader is the first piece of software started by the [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or [UEFI](/index.php/UEFI "UEFI"). It is responsible for loading the kernel with the wanted [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and [initial RAM disk](/index.php/Mkinitcpio "Mkinitcpio") based on config files.

**Note:** Loading [Microcode](/index.php/Microcode "Microcode") updates requires adjustments in boot loader configuration. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

### Feature comparison

**Note:**

*   Boot loaders only need to support the file system on which kernel and initramfs reside (the file system on which `/boot` is located).
*   As GPT is part of the UEFI specification, all UEFI boot loaders support GPT disks. GPT on BIOS systems is possible, using either "hybrid booting" with [Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html), or the new [GPT-only](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt) protocol. This protocol may however cause issues with certain BIOS implementations; see [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) for details.
*   Encryption mentioned in file system support is [filesystem-level encryption](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption"), it has no bearing on [block-level encryption](/index.php/Dm-crypt "Dm-crypt").

| Name | Firmware | Multi-boot | [File systems](/index.php/File_systems "File systems") | Notes |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4 "Ext4") | ReiserFS v3 | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | – | Yes | – | – | – | – | ESP only | – | Kernel turned into EFI executable to be loaded directly from [UEFI](/index.php/UEFI "UEFI") firmware or another boot loader. |
| [Clover](/index.php/Clover "Clover") | emulates UEFI | Yes | Yes | No | without encryption | No | Yes | No | Fork of rEFIt modified to run [macOS on non-Apple hardware](https://en.wikipedia.org/wiki/Hackintosh "wikipedia:Hackintosh"). |
| [GRUB](/index.php/GRUB "GRUB") | Yes | Yes | Yes | without zstd compression | Yes | Yes | Yes | Yes | On BIOS/GPT configuration requires a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition").
Supports RAID, LUKS1 and LVM (but not thin provisioned volumes). |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes | without: encryption, zstd compression | without encryption | without tail-packing feature | Yes | No | Supports auto-detecting kernels and parameters without explicit configuration. |
| [Syslinux](/index.php/Syslinux "Syslinux") | Yes | [Partial](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | [Partial](/index.php/Syslinux#Chainloading "Syslinux") | without: multi-device volumes, compression, encryption | without encryption | No | Yes | v4 on [MBR](/index.php/MBR "MBR") only | No support for certain [file system](/index.php/File_system "File system") features [[2]](http://www.syslinux.org/wiki/index.php?title=Filesystem) |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | No | Yes | Yes | No | No | No | ESP only | No | Cannot launch binaries from partitions other than [ESP](/index.php/ESP "ESP"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | without GPT | No | Yes | No | No | Yes | Yes | v4 only | [Discontinued](https://www.gnu.org/software/grub/grub-legacy.html) in favor of [GRUB](/index.php/GRUB "GRUB"). |
| [LILO](/index.php/LILO "LILO") | without GPT | No | Yes | No | without encryption | Yes | Yes | MBR only [[3]](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Discontinued](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) due to limitations (e.g. with Btrfs, GPT, RAID). |

See also [Wikipedia:Comparison of boot loaders](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders").

## Kernel

The [kernel](/index.php/Kernel "Kernel") is the core of an operating system. It functions on a low level (*kernelspace*) interacting between the hardware of the machine and the programs which use the hardware to run. To make efficient use of the CPU, the kernel uses a scheduler to arbitrate which tasks take priority at any given moment, creating the illusion of many tasks being executed simultaneously.

## initramfs

After the kernel is loaded, it unpacks the [initramfs](/index.php/Initramfs "Initramfs") (initial RAM filesystem), which becomes the initial root filesystem. The kernel then executes `/init` as the first process. The *early userspace* starts.

The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem (see [FHS](/index.php/FHS "FHS") for details). This means that any modules that are required for devices like IDE, SCSI, SATA, USB/FW (if booting from an external drive) must be loadable from the initramfs if not built into the kernel; once the proper modules are loaded (either explicitly via a program or script, or implicitly via [udev](/index.php/Udev "Udev")), the boot process continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem; it does not need to contain every module one would ever want to use. The majority of modules will be loaded later on by udev, during the init process.

## Init process

At the final stage of early userspace, the real root is mounted, and then replaces the initial root filesystem. `/sbin/init` is executed, replacing the `/init` process. Arch uses [systemd](/index.php/Systemd "Systemd") as the default [init](/index.php/Init "Init").

## Getty

[init](/index.php/Init "Init") calls [getty](/index.php/Getty "Getty") once for each [virtual terminal](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (typically six of them), which initializes each tty and asks for a username and password. Once the username and password are provided, getty checks them against `/etc/passwd` and `/etc/shadow`, then calls [login](#Login). Alternatively, getty may start a display manager if one is present on the system.

## Display Manager

A [display manager](/index.php/Display_manager "Display manager") can be configured to replace the getty login prompt on a tty.

## Login

The *login* program begins a session for the user by setting environment variables and starting the user's shell, based on `/etc/passwd`.

The *login* program displays the contents of [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) after a successful login, just before it executes the login shell. It is a good place to display your Terms of Service to remind users of your local policies or anything you wish to tell them.

## Shell

Once the user's [shell](/index.php/Shell "Shell") is started, it will typically run a runtime configuration file, such as [bashrc](/index.php/Bashrc "Bashrc"), before presenting a prompt to the user. If the account is configured to [Start X at login](/index.php/Start_X_at_login "Start X at login"), the runtime configuration file will call [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## GUI, xinit or wayland

[xinit](/index.php/Xinit "Xinit") runs the user's [xinitrc](/index.php/Xinitrc "Xinitrc") runtime configuration file, which normally starts a [window manager](/index.php/Window_manager "Window manager"). When the user is finished and exits the window manager, xinit, startx, the shell, and login will terminate in that order, returning to getty.

## See also

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)
*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
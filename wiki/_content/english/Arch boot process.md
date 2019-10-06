Related articles

*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init "Init")
*   [systemd](/index.php/Systemd "Systemd")
*   [fstab](/index.php/Fstab "Fstab")
*   [Autostarting](/index.php/Autostarting "Autostarting")

In order to boot Arch Linux, a Linux-capable [boot loader](#Boot_loader) must be set up. The boot loader is responsible for loading the kernel and [initial ramdisk](/index.php/Initial_ramdisk "Initial ramdisk") before initiating the boot process. The procedure is quite different for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") and [UEFI](/index.php/UEFI "UEFI") systems, the detailed description is given on this or linked pages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
*   [6 init process](#init_process)
*   [7 getty](#getty)
*   [8 Display manager](#Display_manager)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI, xinit or wayland](#GUI,_xinit_or_wayland)
*   [12 See also](#See_also)

## Firmware types

### BIOS

A [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or Basic Input-Output System is the very first program (firmware) that is executed once the system is switched on. In most cases it is stored in a flash memory in the motherboard itself and independent of the system storage.

### UEFI

[Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") has support for reading both the partition table as well as file systems. UEFI does not launch any [boot code from the Master Boot Record (MBR)](/index.php/Partitioning#Master_Boot_Record_(bootstrap_code) "Partitioning") whether it exists or not, instead booting relies on boot entries in the [NVRAM](https://en.wikipedia.org/wiki/Non-volatile_random-access_memory "wikipedia:Non-volatile random-access memory").

The UEFI specification mandates support for the [FAT12, FAT16, and FAT32](/index.php/FAT "FAT") file systems (see [UEFI specification version 2.8, section 13.3.1.1](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1019485)), but any conformant vendor can optionally add support for additional filesystems; for example, Apple [Macs](/index.php/Mac "Mac") support (and by default use) their own HFS+ filesystem drivers. UEFI implementations also support ISO-9660 for optical discs.

UEFI launches EFI applications, e.g. [boot loaders](#Boot_loader), boot managers, [UEFI shell](/index.php/UEFI_shell "UEFI shell"), etc. These applications are usually stored as files in the [EFI system partition](/index.php/EFI_system_partition "EFI system partition"). Each vendor can store its files in the EFI system partition under the `/EFI/*vendor_name*` folder. The applications can be launched by adding a boot entry to the NVRAM or from the UEFI shell.

The UEFI specification has support for legacy BIOS booting with its [Compatibility Support Module (CSM)](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#CSM_booting "wikipedia:Unified Extensible Firmware Interface"). If CSM is enabled in the UEFI, the UEFI will generate CSM boot entries for all drives. If a CSM boot entry is chosen to be booted from, the UEFI's CSM will attempt to boot from the drive's MBR bootstrap code.

## System initialization

### Under BIOS

1.  System switched on, the [power-on self-test (POST)](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") is executed.
2.  After POST, BIOS initializes the necessary system hardware for booting (disk, keyboard controllers etc.).
3.  BIOS launches the first 440 bytes ([the Master Boot Record bootstrap code area](/index.php/Partitioning#Master_Boot_Record_(bootstrap_code) "Partitioning")) of the first disk in the BIOS disk order.
4.  The boot loader's first stage in the MBR boot code then launches its second stage code (if any) from either:
    *   next disk sectors after the MBR, i.e. the so called post-MBR gap (only on a MBR partition table).
    *   a partition's or a partitionless disk's [volume boot record (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record").
    *   the [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") ([GRUB](/index.php/GRUB "GRUB") on BIOS/GPT only).
5.  The actual [boot loader](#Boot_loader) is launched.
6.  The boot loader then loads an operating system by either chain-loading or directly loading the operating system kernel.

### Under UEFI

1.  System switched on, the [power-on self-test (POST)](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") is executed.
2.  UEFI initializes the hardware required for booting.
3.  Firmware reads the boot entries in the NVRAM to determine which EFI application to launch and from where (e.g. from which disk and partition).
    *   A boot entry could simply be a disk. In this case the firmware looks for an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") on that disk and tries to find an EFI application in the fallback boot path `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` on [systems with a IA32 (32-bit) UEFI](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). This is how UEFI bootable removable media work.
4.  Firmware launches the EFI application.
    *   This could be a [boot loader](#Boot_loader) or the Arch [kernel](/index.php/Kernel "Kernel") itself using [EFISTUB](/index.php/EFISTUB "EFISTUB").
    *   It could be some other EFI application such as a UEFI shell or a [boot manager](#Boot_loader) like [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or [rEFInd](/index.php/REFInd "REFInd").

If [Secure Boot](/index.php/Secure_Boot "Secure Boot") is enabled, the boot process will verify authenticity of the EFI binary by signature.

**Note:** Some UEFI systems can only boot from the fallback boot path.

### Multibooting in UEFI

Since each OS or vendor can maintain its own files within the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") without affecting the other, multi-booting using UEFI is just a matter of launching a different EFI application corresponding to the particular operating system's boot loader. This removes the need for relying on [chain loading](https://en.wikipedia.org/wiki/Chain_loading "wikipedia:Chain loading") mechanisms of one [boot loader](#Boot_loader) to load another OS.

See also [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Boot loader

A boot loader is a piece of software started by the [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or [UEFI](/index.php/UEFI "UEFI"). It is responsible for loading the kernel with the wanted [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and [initial RAM disk](/index.php/Mkinitcpio "Mkinitcpio") based on configuration files. In the case of UEFI, the kernel itself can be directly launched by the UEFI using the EFI boot stub. A separate boot loader or boot manager can still be used for the purpose of editing kernel parameters before booting.

**Note:** Loading [Microcode](/index.php/Microcode "Microcode") updates requires adjustments in boot loader configuration. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

### Feature comparison

**Note:**

*   Boot loaders only need to support the file system on which kernel and initramfs reside (the file system on which `/boot` is located).
*   As GPT is part of the UEFI specification, all UEFI boot loaders support GPT disks. GPT on BIOS systems is possible, using either "hybrid booting" with [Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html), or the new [GPT-only](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt) protocol. This protocol may however cause issues with certain BIOS implementations; see [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) for details.
*   Encryption mentioned in file system support is [filesystem-level encryption](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption"), it has no bearing on [block-level encryption](/index.php/Dm-crypt "Dm-crypt").

| Name | Firmware | [Partition table](/index.php/Partition_table "Partition table") | Multi-boot | [File systems](/index.php/File_systems "File systems") | Notes |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [MBR](/index.php/MBR "MBR") | [GPT](/index.php/GPT "GPT") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4 "Ext4") | ReiserFS | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | – | Yes | Yes | Yes | – | – | – | – | ESP only | – | Kernel turned into EFI executable to be loaded directly from [UEFI](/index.php/UEFI "UEFI") firmware or another boot loader. |
| [Clover](/index.php/Clover "Clover") | emulates UEFI | Yes | Yes | Yes | Yes | No | without encryption | No | Yes | No | Fork of rEFIt modified to run [macOS on non-Apple hardware](https://en.wikipedia.org/wiki/Hackintosh "wikipedia:Hackintosh"). |
| [GRUB](/index.php/GRUB "GRUB") | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | On BIOS/GPT configuration requires a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition").
Supports RAID, LUKS1 and LVM (but not thin provisioned volumes). |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes | Yes | Yes | without: encryption, zstd compression | without encryption | without tail-packing feature | Yes | No | Supports auto-detecting kernels and parameters without explicit configuration. |
| [Syslinux](/index.php/Syslinux "Syslinux") | Yes | [Partial](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | Yes | Yes | [Partial](/index.php/Syslinux#Chainloading "Syslinux") | without: multi-device volumes, compression, encryption | without encryption | No | Yes | MBR only; without sparse inodes | No support for certain [file system](/index.php/File_system "File system") features [[2]](https://wiki.syslinux.org/wiki/index.php?title=Filesystem)
The boot loader can only access the file system it is installed to.[[3]](https://bugzilla.syslinux.org/show_bug.cgi?id=33) |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | No | Yes | [Manual install only](https://github.com/systemd/systemd/issues/1125) | Yes | Yes | No | No | No | ESP only | No | Cannot launch binaries from partitions other than [ESP](/index.php/ESP "ESP"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Yes | No | Yes | No | Yes | No | No | Yes | Yes | v4 only | [Discontinued](https://www.gnu.org/software/grub/grub-legacy.html) in favor of [GRUB](/index.php/GRUB "GRUB"). |
| [LILO](/index.php/LILO "LILO") | Yes | No | Yes | No | Yes | No | without encryption | Yes | Yes | [Yes](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Discontinued](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) due to limitations (e.g. with Btrfs, GPT, RAID). |

1.  A [boot manager](https://www.rodsbooks.com/efi-bootloaders/principles.html). It can only launch other EFI applications, for example, Linux kernel images built with `CONFIG_EFI_STUB=y` and Windows `bootmgfw.efi`.

See also [Wikipedia:Comparison of boot loaders](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders").

## Kernel

The [kernel](/index.php/Kernel "Kernel") is the core of an operating system. It functions on a low level (*kernelspace*) interacting between the hardware of the machine and the programs which use the hardware to run. To make efficient use of the CPU, the kernel uses a scheduler to arbitrate which tasks take priority at any given moment, creating the illusion of many tasks being executed simultaneously.

## initramfs

After the [boot loader](#Boot_loader) loads the [kernel](/index.php/Kernel "Kernel") and possible initramfs files and executes the kernel, the kernel unpacks the initramfs (initial RAM filesystem) archives into the (then empty) rootfs (initial root filesystem, specifically a ramfs or tmpfs). The first extracted initramfs is the one embedded in the kernel binary during the kernel build, then possible external initramfs files are extracted. Thus files in the external initramfs overwrite files with the same name in the embedded initramfs. The kernel then executes `/init` (in the rootfs) as the first process. The *early userspace* starts.

Arch Linux uses an empty archive for the builtin initramfs (which is the default when building Linux). See [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") for more and Arch-specific info about the external initramfs.

The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem (see [FHS](/index.php/FHS "FHS") for details). This means that any modules that are required for devices like IDE, SCSI, SATA, USB/FW (if booting from an external drive) must be loadable from the initramfs if not built into the kernel; once the proper modules are loaded (either explicitly via a program or script, or implicitly via [udev](/index.php/Udev "Udev")), the boot process continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem; it does not need to contain every module one would ever want to use. The majority of modules will be loaded later on by udev, during the init process.

## init process

At the final stage of early userspace, the real root is mounted, and then replaces the initial root filesystem. `/sbin/init` is executed, replacing the `/init` process. Arch uses [systemd](/index.php/Systemd "Systemd") as the default [init](/index.php/Init "Init").

## getty

[init](/index.php/Init "Init") calls [getty](/index.php/Getty "Getty") once for each [virtual terminal](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (typically six of them), which initializes each tty and asks for a username and password. Once the username and password are provided, getty checks them against `/etc/passwd` and `/etc/shadow`, then calls [login](#Login). Alternatively, getty may start a display manager if one is present on the system.

## Display manager

A [display manager](/index.php/Display_manager "Display manager") can be configured to replace the getty login prompt on a tty.

In order to automatically initialize a display manager after booting, it is necessary to manually enable the service unit through [systemd](/index.php/Systemd "Systemd"). For more information on enabling and starting service units, see [systemd#Using units](/index.php/Systemd#Using_units "Systemd").

## Login

The *login* program begins a session for the user by setting environment variables and starting the user's shell, based on `/etc/passwd`.

The *login* program displays the contents of [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) after a successful login, just before it executes the login shell. It is a good place to display your Terms of Service to remind users of your local policies or anything you wish to tell them.

## Shell

Once the user's [shell](/index.php/Shell "Shell") is started, it will typically run a runtime configuration file, such as [bashrc](/index.php/Bashrc "Bashrc"), before presenting a prompt to the user. If the account is configured to [Start X at login](/index.php/Start_X_at_login "Start X at login"), the runtime configuration file will call [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## GUI, xinit or wayland

[xinit](/index.php/Xinit "Xinit") runs the user's [xinitrc](/index.php/Xinitrc "Xinitrc") runtime configuration file, which normally starts a [window manager](/index.php/Window_manager "Window manager"). When the user is finished and exits the window manager, *xinit*, *startx*, the shell, and login will terminate in that order, returning to [getty](#getty).

## See also

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)
*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
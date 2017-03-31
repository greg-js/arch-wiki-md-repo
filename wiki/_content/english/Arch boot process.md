In order to boot Arch Linux, a Linux-capable [boot loader](/index.php/Boot_loader "Boot loader") such as [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") must be installed to the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") or the [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). The boot loader is responsible for loading the kernel and [initial ramdisk](/index.php/Initial_ramdisk "Initial ramdisk") before initiating the boot process. The procedure is quite different for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") and [UEFI](/index.php/UEFI "UEFI") systems, the detailed description is given on this or linked pages.

## Contents

*   [1 Firmware types](#Firmware_types)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 System initialization](#System_initialization)
    *   [2.1 Under BIOS](#Under_BIOS)
    *   [2.2 Under UEFI](#Under_UEFI)
    *   [2.3 Multibooting in UEFI](#Multibooting_in_UEFI)
*   [3 Boot loader](#Boot_loader)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 Init process](#Init_process)
*   [7 Getty](#Getty)
*   [8 Display Manager](#Display_Manager)
*   [9 Login](#Login)
    *   [9.1 Message of the day](#Message_of_the_day)
*   [10 Shell](#Shell)
*   [11 xinit](#xinit)
*   [12 See also](#See_also)

## Firmware types

### BIOS

A BIOS or Basic Input-Output System is the very first program (firmware) that is executed once the system is switched on. In most cases it is stored in a flash memory in the motherboard itself and independent of the system storage.

The BIOS loads the beginning 512 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) of the first valid disk in the BIOS disk order. Of these 512 bytes, the first 440 contains the first stage of a boot loader like [GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") or [LILO](/index.php/LILO "LILO"). Since very little can be achieved by a program of this size, the second stage (residing on the next disk sectors) is loaded from here and looks up a file stored on the partition itself (the actual bootloader). This then loads an operating system by either chain-loading or directly loading the operating system kernel.

### UEFI

UEFI has support for reading both the partition table as well as understanding filesystems. Hence it is not limited by 440 byte code limitation (MBR boot code) as in BIOS systems. It does not use the MBR boot code at all.

The commonly used UEFI firmwares support both MBR and GPT [partition table](/index.php/Partition_table "Partition table"). EFI in Apple-Intel Macs are known to also support Apple Partition Map besides MBR and GPT. Most UEFI firmwares have support for accessing FAT12 (floppy disks), FAT16 and FAT32 filesystems in HDDs and ISO9660 (and UDF) in CD/DVDs. EFI in Intel Macs can also access HFS/HFS+ filesystems, in addition to the mentioned ones.

UEFI does not launch any boot code in the MBR whether it exists or not. Instead it uses a special partition in the partition table called **EFI System Partition** in which files required to be launched by the firmware are stored. Each vendor can store its files under `<EFI SYSTEM PARTITION>/EFI/<VENDOR NAME>/` folder and can use the firmware or its shell (UEFI shell) to launch the boot program. An EFI System Partition is usually formatted as FAT32 or (less commonly) FAT16.

## System initialization

### Under BIOS

1.  System switched on - [Power-on self-test](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") or POST process
2.  After POST, BIOS initializes the necessary system hardware for booting (disk, keyboard controllers etc.)
3.  BIOS launches the first 440 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) of the first disk in the BIOS disk order
4.  The MBR boot code then takes control from BIOS and launches its next stage code (if any) (mostly [boot loader](/index.php/Boot_loader "Boot loader") code)
5.  The launched actual boot loader

### Under UEFI

1.  System switched on. The Power On Self Test (POST) is executed.
2.  UEFI firmware is loaded. Firmware initializes the hardware required for booting.
3.  Firmware reads the boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. from which disk and partition).
4.  Firmware launches the UEFI application.
    *   This could be the Arch kernel itself (since [EFISTUB](/index.php/EFISTUB "EFISTUB") is enabled by default).
    *   It could be some other application such as a shell or a graphical boot manager.
    *   Or the boot entry could simply be a disk. In this case the firmware looks for an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") on that disk and tries to run the fallback UEFI application `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` on 32-bit systems). This is how UEFI bootable thumb drives work.

If [Secure Boot](/index.php/Secure_Boot "Secure Boot") is enabled, the boot process will verify authenticity of the EFI binary by signature.

**Note:** On some (poorly-designed) UEFI systems the only way to boot is using a disk boot entry with the fallback UEFI application path.

### Multibooting in UEFI

Since each OS or vendor can maintain its own files within the EFI System Partition without affecting the other, multi-booting using UEFI is just a matter of launching a different UEFI application corresponding to the particular OS's bootloader. This removes the need for relying on chainloading mechanisms of one [boot loader](/index.php/Boot_loader "Boot loader") to load another OS.

See also [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Boot loader

The boot loader is the first piece of software started by the [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or [UEFI](/index.php/UEFI "UEFI"). It is responsible for loading the kernel with the wanted [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and [initial RAM disk](/index.php/Mkinitcpio "Mkinitcpio") based on config files.

## Kernel

The kernel is the core of an operating system. It functions on a low level (*kernelspace*) interacting between the hardware of the machine and the programs which use the hardware to run. To make efficient use of the CPU, the kernel uses a scheduler to arbitrate which tasks take priority at any given moment, creating the illusion of many tasks being executed simultaneously.

## initramfs

After the kernel is loaded, it unpacks the [initramfs](/index.php/Initramfs "Initramfs") (initial RAM filesystem), which becomes the initial root filesystem. The kernel then executes `/init` as the first process. The *early userspace* starts.

The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem (see [FHS](/index.php/FHS "FHS") for details). This means that any modules that are required for devices like IDE, SCSI, SATA, USB/FW (if booting from an external drive) must be loadable from the initramfs if not built into the kernel; once the proper modules are loaded (either explicitly via a program or script, or implicitly via [udev](/index.php/Udev "Udev")), the boot process continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem; it does not need to contain every module one would ever want to use. The majority of modules will be loaded later on by udev, during the init process.

## Init process

At the final stage of early userspace, the real root is mounted, and then replaces the initial root filesystem. `/sbin/init` is executed, replacing the `/init` process. Arch uses [systemd](/index.php/Systemd "Systemd") as the default [init](/index.php/Init "Init").

## Getty

[init](/index.php/Init "Init") calls [getty](/index.php/Getty "Getty") once for each [virtual terminal](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (typically six of them), which initializes each tty and asks for a username and password. Once the username and password are provided, getty checks them against `/etc/passwd`, then calls [login](#Login), which begins a session for the user, and executes the user's shell according to `/etc/passwd`. Alternatively, getty may start a display manager if one is present on the system.

## Display Manager

A [display manager](/index.php/Display_manager "Display manager") can be configured to replace the getty login prompt on a tty.

## Login

The *login* program begins a session for the user by setting environment variables and starting the user's shell, based on `/etc/passwd`.

### Message of the day

The *login* program displays the contents of [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) after a successful login, just before it executes the login shell.

It is a good place to display your Terms of Service to remind users of your local policies or anything you wish to tell them.

## Shell

Once the user's [shell](/index.php/Shell "Shell") is started, it will typically run a runtime configuration file, such as [bashrc](/index.php/Bashrc "Bashrc"), before presenting a prompt to the user. If the account is configured to [Start X at login](/index.php/Start_X_at_login "Start X at login"), the runtime configuration file will call [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## xinit

[xinit](/index.php/Xinit "Xinit") runs the user's [xinitrc](/index.php/Xinitrc "Xinitrc") runtime configuration file, which normally starts a [window manager](/index.php/Window_manager "Window manager"). When the user is finished and exits the window manager, xinit, startx, the shell, and login will terminate in that order, returning to getty.

## See also

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
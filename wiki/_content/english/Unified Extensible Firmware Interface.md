**Warning:** While the choice to install in EFI mode is forward looking, early vendor UEFI implementations may carry more bugs than their BIOS counterparts. It is advised to do a search relating to your particular mainboard model before proceeding.

**Unified Extensible Firmware Interface** (or UEFI for short) is a new type of firmware. It introduces new ways of booting an OS that is distinct from the commonly used "[MBR](/index.php/MBR "MBR") boot code" method followed for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems. See [Arch boot process#Firmware types](/index.php/Arch_boot_process#Firmware_types "Arch boot process") for their differences. This page explains **What is UEFI** and **UEFI support in Linux kernel**. To set up UEFI Boot Loaders, see [Boot loaders](/index.php/Boot_loaders "Boot loaders").

## Contents

*   [1 UEFI versions](#UEFI_versions)
*   [2 Boot Process under UEFI](#Boot_Process_under_UEFI)
    *   [2.1 Multibooting in UEFI](#Multibooting_in_UEFI)
    *   [2.2 Detecting UEFI Firmware bitness](#Detecting_UEFI_Firmware_bitness)
        *   [2.2.1 Non Macs](#Non_Macs)
        *   [2.2.2 Apple Macs](#Apple_Macs)
*   [3 Linux Kernel Config options for UEFI](#Linux_Kernel_Config_options_for_UEFI)
*   [4 UEFI Variables](#UEFI_Variables)
    *   [4.1 UEFI Variables Support in Linux Kernel](#UEFI_Variables_Support_in_Linux_Kernel)
    *   [4.2 Requirements for UEFI variable support](#Requirements_for_UEFI_variable_support)
        *   [4.2.1 Mount efivarfs](#Mount_efivarfs)
    *   [4.3 Userspace tools](#Userspace_tools)
        *   [4.3.1 efibootmgr](#efibootmgr)
*   [5 EFI System Partition](#EFI_System_Partition)
    *   [5.1 GPT partitioned disks](#GPT_partitioned_disks)
    *   [5.2 MBR partitioned disks](#MBR_partitioned_disks)
    *   [5.3 ESP on RAID](#ESP_on_RAID)
*   [6 UEFI Shell](#UEFI_Shell)
    *   [6.1 Obtaining UEFI Shell](#Obtaining_UEFI_Shell)
    *   [6.2 Launching UEFI Shell](#Launching_UEFI_Shell)
    *   [6.3 Important UEFI Shell Commands](#Important_UEFI_Shell_Commands)
        *   [6.3.1 bcfg](#bcfg)
        *   [6.3.2 map](#map)
        *   [6.3.3 edit](#edit)
*   [7 UEFI Linux Hardware Compatibility](#UEFI_Linux_Hardware_Compatibility)
*   [8 UEFI Bootable Media](#UEFI_Bootable_Media)
    *   [8.1 Create UEFI bootable USB from ISO](#Create_UEFI_bootable_USB_from_ISO)
    *   [8.2 Remove UEFI boot support from Optical Media](#Remove_UEFI_boot_support_from_Optical_Media)
*   [9 Testing UEFI in systems without native support](#Testing_UEFI_in_systems_without_native_support)
    *   [9.1 OVMF for Virtual Machines](#OVMF_for_Virtual_Machines)
    *   [9.2 DUET for BIOS only systems](#DUET_for_BIOS_only_systems)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Windows 7 will not boot in UEFI Mode](#Windows_7_will_not_boot_in_UEFI_Mode)
    *   [10.2 Windows changes boot order](#Windows_changes_boot_order)
    *   [10.3 USB media gets struck with black screen](#USB_media_gets_struck_with_black_screen)
        *   [10.3.1 Using GRUB](#Using_GRUB)
    *   [10.4 UEFI boot loader does not show up in firmware menu](#UEFI_boot_loader_does_not_show_up_in_firmware_menu)
*   [11 See also](#See_also)

## UEFI versions

*   UEFI started as Intel's EFI in versions 1.x.
*   Later, a group of companies called the UEFI Forum took over its development, which renamed it as Unified EFI starting with version 2.0\.
*   Unless specified as EFI 1.x, EFI and UEFI terms are used interchangeably to denote UEFI 2.x firmware.
*   As of 15 April 2015, UEFI Specification 2.5 is the most recent version.
*   Apple's EFI implementation is neither a EFI 1.x version nor UEFI 2.x version but mixes up both. This kind of firmware does not fall under any one (U)EFI specification and therefore is not a standard UEFI firmware. Unless stated explicitly, these instructions are general and some of them may not work or may be different in [Apple Macs](/index.php/MacBook "MacBook").

## Boot Process under UEFI

1.  System switched on. The Power On Self Test (POST) is executed.
2.  UEFI firmware is loaded. Firmware initializes the hardware required for booting.
3.  Firmware reads the boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. from which disk and partition).
4.  Firmware launches the UEFI application.
    *   This could be the Arch kernel itself (since [EFISTUB](/index.php/EFISTUB "EFISTUB") is enabled by default).
    *   It could be some other application such as a shell or a graphical boot manager.
    *   Or the boot entry could simply be a disk. In this case the firmware looks for an EFI system partition on that disk and tries to run the fallback UEFI application `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` on 32-bit systems). This is how UEFI bootable thumb drives work.

If [Secure Boot](/index.php/Secure_Boot "Secure Boot") is enabled, the boot process will verify authenticity of the EFI binary by signature.

**Note:** On some (poorly-designed) UEFI systems the only way to boot is using a disk boot entry with the fallback UEFI application path.

### Multibooting in UEFI

Since each OS or vendor can maintain its own files within the EFI System Partition without affecting the other, multi-booting using UEFI is just a matter of launching a different UEFI application corresponding to the particular OS's bootloader. This removes the need for relying on chainloading mechanisms of one [boot loader](/index.php/Boot_loader "Boot loader") to load another to switch OSes.

See also [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

### Detecting UEFI Firmware bitness

#### Non Macs

Check whether the dir `/sys/firmware/efi` exists, if it exists it means the kernel has booted in EFI mode. In that case the UEFI bitness is same as kernel bitness. (ie. i686 or x86_64)

**Note:** Intel Atom System-on-Chip systems ship with 32-bit UEFI (as on 2 November 2013). See [#Using GRUB](#Using_GRUB) for more info.

#### Apple Macs

Pre-2008 Macs mostly have i386-efi firmware while >=2008 Macs have mostly x86_64-efi. All Macs capable of running Mac OS X Snow Leopard 64-bit Kernel have x86_64 EFI 1.x firmware.

To find out the arch of the efi firmware in a Mac, type the following into the Mac OS X terminal:

```
ioreg -l -p IODeviceTree | grep firmware-abi

```

If the command returns EFI32 then it is IA32 (32-bit) EFI firmware. If it returns EFI64 then it is x86_64 EFI firmware. Most of the Macs do not have UEFI 2.x firmware as Apple's EFI implementation is not fully compliant with UEFI 2.x Specification.

## Linux Kernel Config options for UEFI

The required Linux Kernel configuration options for UEFI systems are :

```
CONFIG_RELOCATABLE=y
CONFIG_EFI=y
CONFIG_EFI_STUB=y
CONFIG_FB_EFI=y
CONFIG_FRAMEBUFFER_CONSOLE=y

```

UEFI Runtime Variables Support (**efivarfs** filesystem - `/sys/firmware/efi/efivars`). This option is important as this is required to manipulate UEFI Runtime Variables using tools like `/usr/bin/efibootmgr`. The below config option has been added in kernel 3.10 and above.

```
CONFIG_EFIVAR_FS=y

```

UEFI Runtime Variables Support (old **efivars sysfs** interface - `/sys/firmware/efi/vars`). This option should be disabled to prevent any potential issues with both efivarfs and sysfs-efivars enabled.

```
CONFIG_EFI_VARS=n

```

GUID Partition Table [GPT](/index.php/GPT "GPT") config option - mandatory for UEFI support

```
CONFIG_EFI_PARTITION=y

```

**Note:** All of the above options are required to boot Linux via UEFI, and are enabled in Archlinux kernels in official repos.

Retrieved from [https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt) .

## UEFI Variables

UEFI defines variables through which an operating system can interact with the firmware. UEFI Boot Variables are used by the boot-loader and used by the OS only for early system start-up. UEFI Runtime Variables allow an OS to manage certain settings of the firmware like the UEFI Boot Manager or managing the keys for UEFI Secure Boot Protocol etc. You can get the list using

```
$ efivar -l

```

### UEFI Variables Support in Linux Kernel

Linux kernel exposes EFI variables data to userspace via **efivarfs** (**EFI** **VAR**iable **F**ile**S**ystem) interface (CONFIG_EFIVAR_FS) - mounted using `efivarfs` kernel module at `/sys/firmware/efi/efivars` - it has no maximum per-variable size limitation and supports UEFI Secure Boot variables. Introduced in kernel 3.8.

### Requirements for UEFI variable support

1.  EFI Runtime Services support should be present in the kernel (`CONFIG_EFI=y`, check if present with `zgrep CONFIG_EFI /proc/config.gz`).
2.  Kernel processor [bitness](#Detecting_UEFI_Firmware_bitness) and EFI processor bitness should match
3.  Kernel should be booted in EFI mode (via [EFISTUB](/index.php/EFISTUB "EFISTUB") or any [EFI boot loader](/index.php/Boot_loaders "Boot loaders"), not via BIOS/CSM or Apple's "bootcamp" which is also BIOS/CSM)
4.  EFI Runtime Services in the kernel SHOULD NOT be disabled via kernel cmdline, i.e. `noefi` kernel parameter SHOULD NOT be used
5.  `efivarfs` filesystem should be mounted at `/sys/firmware/efi/efivars`, otherwise follow [#Mount efivarfs](#Mount_efivarfs) section below.
6.  `efivar` should list (option `-l`) the EFI Variables without any error.

If EFI Variables support does not work even after the above conditions are satisfied, try the below workarounds:

1.  If any userspace tool is unable to modify efi variables data, check for existence of `/sys/firmware/efi/efivars/dump-*` files. If they exist, delete them, reboot and retry again.
2.  If the above step does not fix the issue, try booting with `efi_no_storage_paranoia` kernel parameter to disable kernel efi variable storage space check that may prevent writing/modification of efi variables.

**Note:** `efi_no_storage_paranoia` should only be used when needed and should not be left as a normal boot option. The effect of this kernel command line parameter turns off a safeguard that was put in place to help avoid the bricking of machines when the NVRAM gets too full.

#### Mount efivarfs

**Warning:** *efivars* is mounted writeable by default [[1]](https://github.com/systemd/systemd/issues/2402), which may cause permanent damage to the system. [[2]](https://bbs.archlinux.org/viewtopic.php?id=207549) As such, consider mounting *efivars* read-only (`-o ro`) as described below. Note that when it is mounted read-only, tools such as *efibootmgr* and bootloaders will not be able to change boot settings, nor will commands like `systemctl reboot --firmware-setup` work.

If `efivarfs` is not automatically mounted at `/sys/firmware/efi/efivars` by [systemd](/index.php/Systemd "Systemd") during boot, then you need to manually mount it to expose UEFI variables to [#Userspace tools](#Userspace_tools) like `efibootmgr`:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivarsb

```

**Note:** The above command should be run both **outside** (**before**) and **inside** the [chroot](/index.php/Chroot "Chroot"), if any.

To mount `efivarfs` read-only during boot, add to `/etc/fstab`:

 `/etc/fstab`  `efivarfs    /sys/firmware/efi/efivars    efivarfs    **ro**,nosuid,nodev,noexec,noatime 0 0` 

To remount with write support, run:

```
# mount -o remount /sys/firmware/efi/efivars -o **rw**,nosuid,nodev,noexec,noatime

```

### Userspace tools

There are few tools that can access/modify the UEFI variables, namely

1.  **efivar** - Library and Tool to manipulate UEFI Variables (used by efibootmgr) - [https://github.com/vathpela/efivar](https://github.com/vathpela/efivar) - [efivar](https://www.archlinux.org/packages/?name=efivar) or [efivar-git](https://aur.archlinux.org/packages/efivar-git/)
2.  **efibootmgr** - Tool to manipulate UEFI Firmware Boot Manager Settings - [https://github.com/vathpela/efibootmgr](https://github.com/vathpela/efibootmgr) - [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) or [efibootmgr-git](https://aur.archlinux.org/packages/efibootmgr-git/)
3.  **uefivars** - Dumps list of EFI variables with some additional PCI related info (uses efibootmgr code internally) - [https://github.com/fpmurphy/Various/tree/master/uefivars-2.0](https://github.com/fpmurphy/Various/tree/master/uefivars-2.0) supports only efivarfs and [https://github.com/fpmurphy/Various/tree/master/uefivars-1.0](https://github.com/fpmurphy/Various/tree/master/uefivars-1.0) supports only sysfs-efivars . AUR package [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/)
4.  **efitools** - Tools to Create and Setup own UEFI Secure Boot Certificates, Keys and Signed Binaries (requires efivarfs) - [efitools-git](https://aur.archlinux.org/packages/efitools-git/)
5.  **Ubuntu's Firmware Test Suite** - [https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) - [fwts](https://aur.archlinux.org/packages/fwts/) (along with [fwts-efi-runtime-dkms](https://aur.archlinux.org/packages/fwts-efi-runtime-dkms/)) or [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

#### efibootmgr

**Note:**

*   If `efibootmgr` completely fails to work in your system, you can reboot into UEFI Shell v2 and use `bcfg` command to create a boot entry for the bootloader.
*   If you are unable to use `efibootmgr`, some UEFI firmwares allow users to directly manage uefi boot entries from within its boot-time interface. For example, some ASUS firmwares have an "Add New Boot Option" choice which enables you to select a local EFI System Partition and manually enter the EFI stub location. (for example `\EFI\refind\refind_x64.efi`).
*   The below commands use [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) boot-loader as example.

Assuming the boot-loader file to be launched is `/boot/efi/EFI/refind/refind_x64.efi`, `/boot/efi/EFI/refind/refind_x64.efi` can be split up as `/boot/efi` and `/EFI/refind/refind_x64.efi`, wherein `/boot/efi` is the mountpoint of the EFI System Partition, which is assumed to be `/dev/sdXY` (here `X` and `Y` are just placeholders for the actual values - eg:- in `/dev/sda1` , `X==a` `Y==1`).

To determine the actual device path for the EFI System Partition (assuming mountpoint `/boot/efi` for example) (should be in the form `/dev/sdXY`), try :

```
# findmnt /boot/efi
TARGET SOURCE  FSTYPE OPTIONS
/boot/efi  /dev/sdXY  vfat         rw,flush,tz=UTC

```

Verify that uefi variables support in kernel is working properly by running:

```
# efivar -l

```

If efivar lists the uefi variables without any error, then you can proceed. If not, check whether all the conditions in [#Requirements for UEFI variable support](#Requirements_for_UEFI_variable_support) are met.

Then create the boot entry using efibootmgr as follows:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd"

```

**Note:** UEFI uses backward slash `\` as path separator (similar to Windows paths), but the official [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) pkg support passing unix-style paths with forward-slash `/` as path-separator for the `-l` option. Efibootmgr internally converts `/` to `\` before encoding the loader path. The relevant git commit that incorporated this feature in efibootmgr is [http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378) .

In the above command `/boot/efi/EFI/refind/refind_x64.efi` translates to `/boot/efi` and `/EFI/refind/refind_x64.efi` which in turn translate to drive `/dev/sdX` -> partition `Y` -> file `/EFI/refind/refind_x64.efi`.

The 'label' is the name of the menu entry shown in the UEFI boot menu. This name is user's choice and does not affect the booting of the system. More info can be obtained from [efibootmgr GIT README](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/plain/README) .

FAT32 filesystem is case-insensitive since it does not use UTF-8 encoding by default. In that case the firmware uses capital 'EFI' instead of small 'efi', therefore using `\EFI\refind\refindx64.efi` or `\efi\refind\refind_x64.efi` does not matter (this will change if the filesystem encoding is UTF-8).

## EFI System Partition

The EFI System Partition (also called ESP or EFISYS) is a FAT32 formatted physical partition (in the main partition table of the disk, not LVM or software raid etc.) from where the UEFI firmware launches the UEFI bootloader and application.

It is an OS independent partition that acts as the storage place for the EFI bootloaders and applications to be launched by the EFI firmware. It is mandatory for UEFI boot. It should have the EFI System partition type (see [#GPT partitioned disks](#GPT_partitioned_disks)). It is recommended to keep ESP size at 512 MiB although smaller/larger sizes are fine (see note below). For more information see [Wikipedia:EFI System partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition").

**Note:**

*   It is recommended to use always GPT for UEFI boot as some UEFI firmwares do not allow UEFI-MBR boot.
*   In [GNU Parted](/index.php/GNU_Parted "GNU Parted"), `boot` flag (not to be confused with `legacy_boot` flag) has different effect in MBR and GPT disk. In MBR disk, it marks the partition as active. In GPT disk, it changes the type code of the partition to `EFI System Partition` type. [Parted](/index.php/Parted "Parted") has no flag to mark a partition as ESP in MBR disk (this can be done using fdisk though).
*   According to a Microsoft note[[3]](http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules), the minimum size for the EFI System Partition (ESP) would be 100 MB, though this is not stated in the UEFI Specification. Note that for Advanced Format 4K Native drives (4-KB-per-sector) drives, the size is at least 260 MB, because it is the minimum partition size of FAT32 drives (calculated as sector size (4KB) x 65527 = 256 MB), due to a limitation of the FAT32 file format.
*   In case of [EFISTUB](/index.php/EFISTUB "EFISTUB"), the kernels and initramfs files should be stored in the EFI System Partition. For sake of simplicity, you can also use the ESP as the `/boot` partition itself instead of a separate `/boot` partition, for EFISTUB booting.

### GPT partitioned disks

*   **fdisk**/**gdisk**: Create a partition with partition type EFI System (`EFI System` in *fdisk* or `ef00` in *gdisk*). Then format that partition as FAT32 using `mkfs.fat -F32 /dev/<THAT_PARTITION>`

(or)

*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Create a FAT32 partition and in Parted set/activate the `boot` flag (not `legacy_boot` flag) on that partition

**Note:** If you get the message `WARNING: Not enough clusters for a 32 bit FAT!`, reduce cluster size with `mkfs.fat -s2 -F32 ...` or `-s1`, otherwise the partition may be unreadable by UEFI.

### MBR partitioned disks

*   **fdisk**: Create a partition with partition type *EFI System* using fdisk. Then format that partition as FAT32 using `mkfs.fat -F32 /dev/<THAT_PARTITION>`

### ESP on RAID

It is possible to make the ESP part of a RAID1 array, but doing so brings the risk of data corruption, and further considerations need to be taken when creating the ESP. See [https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) and [https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) for details.

## UEFI Shell

The UEFI Shell is a shell/terminal for the firmware which allows launching uefi applications which include uefi bootloaders. Apart from that, the shell can also be used to obtain various other information about the system or the firmware like memory map (memmap), modifying boot manager variables (bcfg), running partitioning programs (diskpart), loading uefi drivers, editing text files (edit), hexedit etc.

### Obtaining UEFI Shell

You can download a BSD licensed UEFI Shell from Intel's Tianocore UDK/EDK2 Sourceforge.net project:

*   [AUR](/index.php/AUR "AUR") package [uefi-shell-git](https://aur.archlinux.org/packages/uefi-shell-git/) (recommended) - provides x86_64 Shell in x86_64 system and IA32 Shell in i686 system - compiled directly from latest Tianocore EDK2 SVN source
*   There are copies of Shell v1 and Shell v2 in the EFI directory on the Arch install media image.
*   [Precompiled x86_64 UEFI Shell v2 binary](https://github.com/tianocore/edk2-ShellBinPkg/blob/master/UefiShell/X64/Shell.efi?raw=true) (may not be up-to-date)
*   [Precompiled x86_64 UEFI Shell v1 binary](https://github.com/tianocore/edk2-EdkShellBinPkg/blob/master/FullShell/X64/Shell_Full.efi?raw=true) (not updated anymore upstream)
*   [Precompiled IA32 UEFI Shell v2 binary](https://github.com/tianocore/edk2-ShellBinPkg/blob/master/UefiShell/Ia32/Shell.efi?raw=true) (may not be up-to-date)
*   [Precompiled IA32 UEFI Shell v1 binary](https://github.com/tianocore/edk2-EdkShellBinPkg/blob/master/FullShell/Ia32/Shell_Full.efi?raw=true) (not updated anymore upstream)

Shell v2 works best in UEFI 2.3+ systems and is recommended over Shell v1 in those systems. Shell v1 should work in all UEFI systems irrespective of the spec. version the firmware follows. More info at [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) and [this mail](http://sourceforge.net/mailarchive/message.php?msg_id=28690732)

### Launching UEFI Shell

Few Asus and other AMI Aptio x86_64 UEFI firmware based motherboards (from Sandy Bridge onwards) provide an option called `"Launch EFI Shell from filesystem device"` . For those motherboards, download the x86_64 UEFI Shell and copy it to your EFI System Partition as `<EFI_SYSTEM_PARTITION>/shellx64.efi` (mostly `/boot/efi/shellx64.efi`) .

Systems with Phoenix SecureCore Tiano UEFI firmware are known to have embedded UEFI Shell which can be launched using either `F6`, `F11` or `F12` key.

**Note:** If you are unable to launch UEFI Shell from the firmware directly using any of the above mentioned methods, create a FAT32 USB pen drive with `Shell.efi` copied as `(USB)/efi/boot/bootx64.efi`. This USB should come up in the firmware boot menu. Launching this option will launch the UEFI Shell for you.

### Important UEFI Shell Commands

UEFI Shell commands usually support `-b` option which makes output pause after each page. Run `help -b` to list available commands.

More info at [http://software.intel.com/en-us/articles/efi-shells-and-scripting/](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)

#### bcfg

`bcfg` modifies the UEFI NVRAM entries which allows the user to change the boot entries or driver options. This command is described in detail in page 83 (Section 5.3) of "UEFI Shell Specification 2.0" PDF document.

**Note:**

*   Try `bcfg` only if `efibootmgr` fails to create working boot entries on your system.
*   UEFI Shell v1 official binary does not support `bcfg` command. You can download a [modified UEFI Shell v2 binary](http://dl.dropbox.com/u/17629062/Shell2.zip) which may work in UEFI pre-2.3 firmwares.

To dump a list of current boot entries:

```
Shell> bcfg boot dump -v

```

To add a boot menu entry for rEFInd (for example) as 4th (numbering starts from zero) option in the boot menu:

```
Shell> bcfg boot add 3 fs0:\EFI\refind\refind_x64.efi "rEFInd"

```

where `fs0:` is the mapping corresponding to the EFI System Partition and `fs0:\EFI\refind\refind_x64.efi` is the file to be launched.

To remove the 4th boot option:

```
Shell> bcfg boot rm 3

```

To move the boot option #3 to #0 (i.e. 1st or the default entry in the UEFI Boot menu):

```
Shell> bcfg boot mv 3 0

```

For bcfg help text:

```
Shell> help bcfg -v -b

```

or:

```
Shell> bcfg -? -v -b

```

#### map

`map` displays a list of device mappings i.e. the names of available file systems (`fs0`) and storage devices (`blk0`).

Before running file system commands such as `cd` or `ls`, you need to change the shell to the appropriate file system by typing its name:

```
  Shell> fs0:
  fs0:\> cd EFI/

```

#### edit

`edit` provides a basic text editor with an interface similar to nano, but slightly less functional. It handles UTF-8 encoding and takes care or LF vs CRLF line endings.

For example, to edit rEFInd's `refind.conf` in the EFI System Partition (`fs0:` in the firmware),

```
Shell> fs0:
FS0:\> cd \EFI\arch\refind
FS0:\EFI\arch\refind\> edit refind.conf

```

Type `Ctrl-E` for help.

## UEFI Linux Hardware Compatibility

See [Unified Extensible Firmware Interface/Hardware](/index.php/Unified_Extensible_Firmware_Interface/Hardware "Unified Extensible Firmware Interface/Hardware") for more information.

## UEFI Bootable Media

### Create UEFI bootable USB from ISO

Follow [USB flash installation media#BIOS and UEFI Bootable USB](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media")

### Remove UEFI boot support from Optical Media

**Note:** This section mentions removing UEFI boot support from a **CD/DVD only** (Optical Media), not from a USB flash drive.

Most of the 32-bit EFI Macs and some 64-bit EFI Macs refuse to boot from a UEFI(X64)+BIOS bootable CD/DVD. If one wishes to proceed with the installation using optical media, it might be necessary to remove UEFI support first.

*   Mount the official installation media and obtain the `archisolabel` as shown in the previous section.

```
# mount -o loop *input.iso* /mnt/iso

```

*   Then rebuild the ISO, excluding the UEFI Optical Media booting support, using `xorriso` from [libisoburn](https://www.archlinux.org/packages/?name=libisoburn). Be sure to set the correct archisolabel, e.g. "ARCH_201411" or similar:

```
$ xorriso -as mkisofs -iso-level 3 \
    -full-iso9660-filenames\
    -volid "*archisolabel*" \
    -appid "Arch Linux CD" \
    -publisher "Arch Linux <[https://www.archlinux.org](https://www.archlinux.org)>" \
    -preparer "prepared by $USER" \
    -eltorito-boot isolinux/isolinux.bin \
    -eltorito-catalog isolinux/boot.cat \
    -no-emul-boot -boot-load-size 4 -boot-info-table \
    -isohybrid-mbr "/mnt/iso/isolinux/isohdpfx.bin" \
    -output *output.iso* /mnt/iso/
```

*   Burn `*output.iso*` to optical media and proceed with installation normally.

## Testing UEFI in systems without native support

### OVMF for Virtual Machines

[OVMF](https://tianocore.github.io/ovmf/) is a tianocore project to enable UEFI support for Virtual Machines. OVMF contains a sample UEFI firmware for QEMU.

You can build OVMF (with Secure Boot support) from AUR [ovmf-svn](https://aur.archlinux.org/packages/ovmf-svn/) and run it as follows:

```
$ qemu-system-x86_64 -enable-kvm -net none -m 1024 -drive file=/usr/share/ovmf/x86_64/bios.bin,format=raw,if=pflash,readonly

```

### DUET for BIOS only systems

DUET is a tianocore project that enables chainloading a full UEFI environment from a BIOS system, in a way similar to BIOS OS booting. This method is being discussed extensively in [http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/](http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/). Pre-build DUET images can be downloaded from one of the repos at [https://gitorious.org/tianocore_uefi_duet_builds](https://gitorious.org/tianocore_uefi_duet_builds). Specific instructions for setting up DUET is available at [https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt](https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt).

You can also try [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/) which provides modified DUET images that may contain some system specific fixes and is more frequently updated compared to the gitorious repos.

## Troubleshooting

### Windows 7 will not boot in UEFI Mode

If you have installed Windows to a different hard disk with GPT partitioning and still have a MBR partitioned hard disk in your computer, then it is possible that the firmware (UEFI) is starting its CSM support (for booting MBR partitions) and therefore Windows will not boot. To solve this merge your MBR hard disk to GPT partitioning or disable the SATA port where the MBR hard disk is plugged in or unplug the SATA connector from this hard disk.

Mainboards with this kind of problem:

*   Gigabyte Z77X-UD3H rev. 1.1 (UEFI version F19e)
    *   The firmware option for booting "UEFI Only" does not prevent the firmware from starting CSM.

### Windows changes boot order

In some motherboards (confirmed in ASRock Z77 Extreme4) Windows 8 changes the boot order in the NVRAM everytime is booted. This can be fixed making the Windows Boot Manager to load another loader instead of booting Windows. Run this command in a Administrator mode console in Windows:

```
bcdedit /set {bootmgr} path \EFI\boot_app_dir\boot_app.efi

```

### USB media gets struck with black screen

*   This issue can occur either due to [KMS](/index.php/KMS "KMS") issue. Try [Disabling KMS](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") while booting the USB.

*   If the issue is not due to KMS, then it may be due to bug in [EFISTUB](/index.php/EFISTUB "EFISTUB") booting (see [FS#33745](https://bugs.archlinux.org/task/33745) and [[4]](https://bbs.archlinux.org/viewtopic.php?id=156670) for more information.). Both Official ISO ([Archiso](/index.php/Archiso "Archiso")) and [Archboot](/index.php/Archboot "Archboot") iso use EFISTUB (via [Gummiboot](/index.php/Gummiboot "Gummiboot") Boot Manager for menu) for booting the kernel in UEFI mode. In such a case you have to use [GRUB](/index.php/GRUB "GRUB") as the USB's UEFI bootloader by following the below section.

#### Using GRUB

**Tip:** The given configuration entries can also be entered inside a [GRUB command-shell](/index.php/GRUB#Using_the_command_shell "GRUB").

*   [Create an USB Flash Installation](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media")

*   Backup `EFI/boot/loader.efi` to `EFI/boot/gummiboot.efi`

*   [Create a GRUB standalone image](/index.php/GRUB#GRUB_standalone "GRUB") and copy the generate `grub*.efi` to the USB as `EFI/boot/loader.efi`, `EFI/boot/bootx64.efi` and/or `EFI/boot/bootia32.efi` (useful when running on a 32-bit UEFI)

*   Create `EFI/boot/grub.cfg` with the following contents (replace `ARCH_YYYYMM` with the required archiso label e.g. `ARCH_201507`):

 `grub.cfg for Official ISO` 
```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux archiso x86_64" {
    set gfxpayload=keep
    search --no-floppy --set=root --label ARCH_YYYYMM
    linux /arch/boot/x86_64/vmlinuz archisobasedir=arch archisolabel=ARCH_YYYYMM add_efi_memmap
    initrd /arch/boot/x86_64/archiso.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --label ARCH_YYYYMM
    chainloader /EFI/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --label ARCH_YYYYMM
    chainloader /EFI/shellx64_v1.efi
}

```
 `grub.cfg for Archboot ISO` 
```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux x86_64 Archboot" {
    set gfxpayload=keep
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    linux /boot/vmlinuz_x86_64 cgroup_disable=memory loglevel=7 add_efi_memmap
    initrd /boot/initramfs_x86_64.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v1.efi
}

```

### UEFI boot loader does not show up in firmware menu

On some UEFI motherboards like boards with an Intel Z77 chipset, adding entries with `efibootmgr` or `bcfg` from the EFI Shell will not work because they do not show up on the boot menu list after being added to NVRAM.

This issue is caused because the motherboards can only load Microsoft Windows. To solve this you have to place the `.efi` file in the location that Windows uses.

Copy the `bootx64.efi` file from the Arch Linux installation medium (`FSO:`) to the Microsoft directory your ESP partition on your hard drive (`FS1:`). Do this by booting into EFI shell and typing:

```
FS1:
cd EFI
mkdir Microsoft
cd Microsoft
mkdir Boot
cp FS0:\EFI\BOOT\bootx64.efi FS1:\EFI\Microsoft\Boot\bootmgfw.efi

```

After reboot, any entries added to NVRAM should show up in the boot menu.

## See also

*   [Wikipedia:UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   [UEFI Forum](http://www.uefi.org/home/) - contains the official [UEFI Specifications](http://uefi.org/specifications) - GUID Partition Table is part of UEFI Specification
*   [UEFI boot: how does that actually work, then? - A blog post by AdamW](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
*   [Wikipedia:EFI System partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition")
*   [The EFI System Partition and the Default Boot Behavior](http://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)
*   [Linux Kernel x86_64 UEFI Documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt)
*   [Intel's page on EFI](http://www.intel.com/technology/efi/)
*   [Intel UEFI Community Resource Center](http://uefidk.intel.com/)
*   [Matt Fleming - The Linux EFI Boot Stub](http://uefidk.intel.com/blog/linux-efi-boot-stub)
*   [Matt Fleming - Accessing UEFI Variables from Linux](http://uefidk.intel.com/blog/accessing-uefi-variables-linux)
*   [Rod Smith - Linux on UEFI: A Quick Installation Guide](http://www.rodsbooks.com/linux-uefi/)
*   [UEFI Boot problems on some newer machines (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [LPC 2012 Plumbing UEFI into Linux](http://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : part 1](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : part 2](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)
*   [Intel's Tianocore Project](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome_to_TianoCore) for Open-Source UEFI firmware which includes DuetPkg for direct BIOS based booting and OvmfPkg used in QEMU and Oracle VirtualBox
*   [FGA: The EFI boot process](http://homepage.ntlworld.com/jonathan.deboynepollard/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)
*   [UEFI Shell v2 binary with bcfg modified to work with UEFI pre-2.3 firmware - from Clover efiboot](http://dl.dropbox.com/u/17629062/Shell2.zip)
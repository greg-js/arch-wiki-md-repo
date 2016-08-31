**Warning:** While the choice to install in UEFI mode is forward looking, early vendor UEFI implementations may carry more bugs than their BIOS counterparts. It is advised to do a search relating to your particular mainboard model before proceeding.

The [Unified Extensible Firmware Interface](http://www.uefi.org/) (EFI or UEFI for short) is a new model for the interface between operating systems and firmware. It provides a standard environment for booting an operating system and running pre-boot applications.

It is distinct from the commonly used "[MBR](/index.php/MBR "MBR") boot code" method followed for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems. See [Arch boot process](/index.php/Arch_boot_process "Arch boot process") for their differences and the boot process using UEFI. To set up UEFI Boot Loaders, see [Boot loaders](/index.php/Boot_loaders "Boot loaders").

## Contents

*   [1 UEFI versions](#UEFI_versions)
*   [2 UEFI Firmware bitness](#UEFI_Firmware_bitness)
    *   [2.1 Non Macs](#Non_Macs)
    *   [2.2 Apple Macs](#Apple_Macs)
*   [3 Linux Kernel Config options for UEFI](#Linux_Kernel_Config_options_for_UEFI)
*   [4 UEFI Variables](#UEFI_Variables)
    *   [4.1 UEFI Variables Support in Linux Kernel](#UEFI_Variables_Support_in_Linux_Kernel)
    *   [4.2 Requirements for UEFI variable support](#Requirements_for_UEFI_variable_support)
        *   [4.2.1 Mount efivarfs](#Mount_efivarfs)
    *   [4.3 Userspace tools](#Userspace_tools)
        *   [4.3.1 efibootmgr](#efibootmgr)
*   [5 UEFI Shell](#UEFI_Shell)
    *   [5.1 Obtaining UEFI Shell](#Obtaining_UEFI_Shell)
    *   [5.2 Launching UEFI Shell](#Launching_UEFI_Shell)
    *   [5.3 Important UEFI Shell Commands](#Important_UEFI_Shell_Commands)
        *   [5.3.1 bcfg](#bcfg)
        *   [5.3.2 map](#map)
        *   [5.3.3 edit](#edit)
*   [6 UEFI Linux Hardware Compatibility](#UEFI_Linux_Hardware_Compatibility)
*   [7 UEFI Bootable Media](#UEFI_Bootable_Media)
    *   [7.1 Create UEFI bootable USB from ISO](#Create_UEFI_bootable_USB_from_ISO)
    *   [7.2 Remove UEFI boot support from Optical Media](#Remove_UEFI_boot_support_from_Optical_Media)
*   [8 Testing UEFI in systems without native support](#Testing_UEFI_in_systems_without_native_support)
    *   [8.1 OVMF for Virtual Machines](#OVMF_for_Virtual_Machines)
    *   [8.2 DUET for BIOS only systems](#DUET_for_BIOS_only_systems)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Windows 7 will not boot in UEFI Mode](#Windows_7_will_not_boot_in_UEFI_Mode)
    *   [9.2 Windows changes boot order](#Windows_changes_boot_order)
    *   [9.3 USB media gets struck with black screen](#USB_media_gets_struck_with_black_screen)
    *   [9.4 Booting 64-bit kernel on 32-bit UEFI](#Booting_64-bit_kernel_on_32-bit_UEFI)
        *   [9.4.1 Using GRUB](#Using_GRUB)
    *   [9.5 UEFI boot loader does not show up in firmware menu](#UEFI_boot_loader_does_not_show_up_in_firmware_menu)
*   [10 See also](#See_also)

## UEFI versions

*   UEFI started as Intel's EFI in versions 1.x.
*   Later, a group of companies called the UEFI Forum took over its development, which renamed it as Unified EFI starting with version 2.0.
*   Unless specified as EFI 1.x, EFI and UEFI terms are used interchangeably to denote UEFI 2.x firmware.
*   Apple's EFI implementation is neither a EFI 1.x version nor UEFI 2.x version but mixes up both. This kind of firmware does not fall under any one (U)EFI specification and therefore is not a standard UEFI firmware. Unless stated explicitly, these instructions are general and some of them may not work or may be different in [Apple Macs](/index.php/MacBook "MacBook").

The latest UEFI Specification can be found at [http://uefi.org/specifications](http://uefi.org/specifications).

## UEFI Firmware bitness

Under UEFI, every program whether it is an OS loader or a utility (e.g. a memory testing app or recovery tool), should be a UEFI Application corresponding to the EFI firmware bitness/architecture.

The vast majority of UEFI firmwares, including recent Apple Macs, use x86_64 EFI firmware. The only known devices that use IA32 (32-bit) EFI are older (pre 2008) Apple Macs, some Intel Cloverfield ultrabooks and some older Intel Server boards that are known to operate on Intel EFI 1.10 firmware.

An x86_64 EFI firmware does not include support for launching 32-bit EFI apps (unlike x86_64 Linux and Windows versions which include such support). Therefore the UEFI application must be compiled for that specific firmware processor bitness/architecture.

### Non Macs

Check whether the dir `/sys/firmware/efi` exists, if it exists it means the kernel has booted in EFI mode. In that case the UEFI bitness is same as kernel bitness. (ie. i686 or x86_64)

**Note:** Intel Atom System-on-Chip systems ship with 32-bit UEFI (as on 2 November 2013). See [#Booting 64-bit kernel on 32-bit UEFI](#Booting_64-bit_kernel_on_32-bit_UEFI) for more info.

### Apple Macs

Pre-2008 Macs mostly have i386-efi firmware while >=2008 Macs have mostly x86_64-efi. All Macs capable of running Mac OS X Snow Leopard 64-bit Kernel have x86_64 EFI 1.x firmware.

To find out the arch of the efi firmware in a Mac, type the following into the Mac OS X terminal:

```
$ ioreg -l -p IODeviceTree | grep firmware-abi

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

Linux kernel exposes EFI variables data to userspace via **efivarfs** (**EFI** **VAR**iable **F**ile**S**ystem) interface (`CONFIG_EFIVAR_FS`) - mounted using `efivarfs` kernel module at `/sys/firmware/efi/efivars` - it has no maximum per-variable size limitation and supports UEFI Secure Boot variables. Introduced in kernel 3.8.

### Requirements for UEFI variable support

1.  Kernel processor [bitness](#UEFI_Firmware_bitness) and EFI processor bitness should match.
2.  Kernel should be booted in EFI mode (via [EFISTUB](/index.php/EFISTUB "EFISTUB") or any [EFI boot loader](/index.php/Boot_loaders "Boot loaders"), not via BIOS/CSM or Apple's "bootcamp" which is also BIOS/CSM).
3.  EFI Runtime Services support should be present in the kernel (`CONFIG_EFI=y`, check if present with `zgrep CONFIG_EFI /proc/config.gz`).
4.  EFI Runtime Services in the kernel SHOULD NOT be disabled via kernel cmdline, i.e. `noefi` kernel parameter SHOULD NOT be used.
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
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

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

*   **efivar** — Library and Tool to manipulate UEFI Variables (used by efibootmgr)

	[https://github.com/vathpela/efivar](https://github.com/vathpela/efivar) || [efivar](https://www.archlinux.org/packages/?name=efivar), [efivar-git](https://aur.archlinux.org/packages/efivar-git/)

*   **efibootmgr** — Tool to manipulate UEFI Firmware Boot Manager Settings

	[https://github.com/vathpela/efibootmgr](https://github.com/vathpela/efibootmgr) || [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr), [efibootmgr-git](https://aur.archlinux.org/packages/efibootmgr-git/)

*   **uefivars** — Dumps list of EFI variables with some additional PCI related info (uses efibootmgr code internally)

	[https://github.com/fpmurphy/Various/tree/master/uefivars-2.0](https://github.com/fpmurphy/Various/tree/master/uefivars-2.0) || [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/)

*   **efitools** — Tools for manipulating UEFI secure boot platforms

	[http://git.kernel.org/cgit/linux/kernel/git/jejb/efitools.git](http://git.kernel.org/cgit/linux/kernel/git/jejb/efitools.git) || [efitools](https://www.archlinux.org/packages/?name=efitools), [efitools-git](https://aur.archlinux.org/packages/efitools-git/)

*   **Ubuntu's Firmware Test Suite** — Test suite that performs sanity checks on Intel/AMD PC firmware

	[https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) || [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

#### efibootmgr

**Note:**

*   If `efibootmgr` completely fails to work in your system, you can reboot into UEFI Shell v2 and use `bcfg` command to create a boot entry for the bootloader.
*   If you are unable to use `efibootmgr`, some UEFI firmwares allow users to directly manage uefi boot entries from within its boot-time interface. For example, some ASUS firmwares have an "Add New Boot Option" choice which enables you to select a local EFI System Partition and manually enter the EFI stub location. (for example `\EFI\refind\refind_x64.efi`).
*   The below commands use [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) boot-loader as example.

Assuming the boot-loader file to be launched is `/boot/efi/EFI/refind/refind_x64.efi`, `/boot/efi/EFI/refind/refind_x64.efi` can be split up as `/boot/efi` and `/EFI/refind/refind_x64.efi`, wherein `/boot/efi` is the mountpoint of the EFI System Partition, which is assumed to be `/dev/sdXY` (here `X` and `Y` are just placeholders for the actual values - eg:- in `/dev/sda1` , `X==a` `Y==1`).

To determine the actual device path for the EFI System Partition (assuming mountpoint `/boot/efi` for example) (should be in the form `/dev/sdXY`), try :

 `# findmnt /boot/efi` 
```
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
# efibootmgr --create --disk /dev/sdX --part Y --loader /EFI/refind/refind_x64.efi --label "rEFInd Boot Manager"

```

**Note:** UEFI uses backward slash `\` as path separator (similar to Windows paths), but the official [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) pkg support passing unix-style paths with forward-slash `/` as path-separator for the `-l`/`--loader` option. Efibootmgr internally converts `/` to `\` before encoding the loader path.

In the above command `/boot/efi/EFI/refind/refind_x64.efi` translates to `/boot/efi` and `/EFI/refind/refind_x64.efi` which in turn translate to drive `/dev/sdX` -> partition `Y` -> file `/EFI/refind/refind_x64.efi`.

The 'label' is the name of the menu entry shown in the UEFI boot menu. This name is user's choice and does not affect the booting of the system. More info can be obtained from [efibootmgr GIT README](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/plain/README) .

FAT32 filesystem is case-insensitive since it does not use UTF-8 encoding by default. In that case the firmware uses capital 'EFI' instead of small 'efi', therefore using `\EFI\refind\refindx64.efi` or `\efi\refind\refind_x64.efi` does not matter (this will change if the filesystem encoding is UTF-8).

## UEFI Shell

The UEFI Shell is a shell/terminal for the firmware which allows launching uefi applications which include uefi bootloaders. Apart from that, the shell can also be used to obtain various other information about the system or the firmware like memory map (memmap), modifying boot manager variables (bcfg), running partitioning programs (diskpart), loading uefi drivers, editing text files (edit), hexedit etc.

### Obtaining UEFI Shell

You can download a BSD licensed UEFI Shell from Intel's Tianocore UDK/EDK2 Sourceforge.net project:

*   [AUR](/index.php/AUR "AUR") package [uefi-shell-git](https://aur.archlinux.org/packages/uefi-shell-git/) (recommended) - provides x86_64 Shell in x86_64 system and IA32 Shell in i686 system - compiled directly from latest Tianocore EDK2 SVN source
*   There are copies of Shell v1 and Shell v2 in the EFI directory on the Arch install media image.
*   [Precompiled UEFI Shell v2 binaries](https://github.com/tianocore/edk2/tree/master/ShellBinPkg) (may not be up-to-date)
*   [Precompiled UEFI Shell v1 binaries](https://github.com/tianocore/edk2/tree/master/EdkShellBinPkg) (not updated anymore upstream)
*   [Precompiled UEFI Shell v2 binary with bcfg modified to work with UEFI pre-2.3 firmware](http://dl.dropbox.com/u/17629062/Shell2.zip) - from Clover EFI bootloader

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
*   UEFI Shell v1 official binary does not support `bcfg` command. See [#Obtaining UEFI Shell](#Obtaining_UEFI_Shell) for a modified UEFI Shell v2 binary which may work in UEFI pre-2.3 firmwares.

To dump a list of current boot entries:

```
Shell> bcfg boot dump -v

```

To add a boot menu entry for rEFInd (for example) as 4th (numbering starts from zero) option in the boot menu:

```
Shell> bcfg boot add 3 fs0:\EFI\refind\refind_x64.efi "rEFInd"

```

where `fs0:` is the mapping corresponding to the EFI System Partition and `fs0:\EFI\refind\refind_x64.efi` is the file to be launched.

To add an entry to boot directly into your system without a bootloader, configure a boot option using your kernel as an [EFISTUB](/index.php/EFISTUB#UEFI_Shell "EFISTUB"):

```
Shell> bcfg boot add **N** fs**V**:\vmlinuz-linux "Arch Linux"
Shell> bcfg boot -opt **N** "root=**/dev/sdX#** initrd=\initramfs-linux.img"

```

where `N` is the priority, `V` is the volume number of your EFI partition, and `/dev/sdX#` is your root partition.

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
Shell> edit FS0:\EFI\refind\refind.conf

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

You can install [ovmf](https://www.archlinux.org/packages/?name=ovmf) from the extra repository and run it as follows:

```
$ qemu-system-x86_64 -enable-kvm -net none -m 1024 -drive file=/usr/share/ovmf/ovmf_x64.bin,format=raw,if=pflash,readonly

```

As shorter alternative, [ovmf](https://www.archlinux.org/packages/?name=ovmf) can be loaded using `-bios` parameter

```
$ qemu-system-x86_64 -enable-kvm -m 1G -bios /usr/share/ovmf/ovmf_x64.bin

```

### DUET for BIOS only systems

DUET is a tianocore project that enables chainloading a full UEFI environment from a BIOS system, in a way similar to BIOS OS booting. This method is being discussed extensively in [http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/](http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/). Pre-build DUET images can be downloaded from one of the repos at [https://gitorious.org/tianocore_uefi_duet_builds](https://gitorious.org/tianocore_uefi_duet_builds) . Specific instructions for setting up DUET is available at [https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt](https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt) .

You can also try [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/) which provides modified DUET images that may contain some system specific fixes and is more frequently updated compared to the gitorious repos.

## Troubleshooting

### Windows 7 will not boot in UEFI Mode

If you have installed Windows to a different hard disk with GPT partitioning and still have a MBR partitioned hard disk in your computer, then it is possible that the firmware (UEFI) is starting its CSM support (for booting MBR partitions) and therefore Windows will not boot. To solve this merge your MBR hard disk to GPT partitioning or disable the SATA port where the MBR hard disk is plugged in or unplug the SATA connector from this hard disk.

Mainboards with this kind of problem:

*   Gigabyte Z77X-UD3H rev. 1.1 (UEFI version F19e)
    *   The firmware option for booting "UEFI Only" does not prevent the firmware from starting CSM.

### Windows changes boot order

If you [dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") and your motherboard just boots Windows immediately instead of your chosen UEFI application, there are several possible causes and workarounds.

*   Ensure [Fast Startup](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") is disabled in your Windows power options
*   Ensure [Secure Boot](/index.php/Secure_Boot "Secure Boot") is disabled in your BIOS (if you are not using a signed boot loader)
*   Ensure your UEFI boot order does not have Windows Boot Manager set first e.g. using [#efibootmgr](#efibootmgr) and what you see in the configuration tool of the UEFI. Some motherboards override by default any settings set with efibootmgr by Windows if it detects it. This is confirmed in a Packard Bell laptop.
*   If your motherboard is booting the default UEFI path (`\EFI\BOOT\BOOTX64.EFI`), this file may have been overwritten with the Windows boot loader. Try setting the correct boot path e.g. using [#efibootmgr](#efibootmgr).
*   If the previous steps do not work, you can tell the Windows boot loader to run a different UEFI application. From a Windows Administrator command prompt: `# bcdedit /set {bootmgr} path \EFI\*path*\*to*\*app.efi*` 
*   Alternatively, you can set a startup script in Windows that ensures that the boot order is set correctly every time you boot Windows.
    1.  Open a command prompt with admin privlages. Run `bcdedit /enum firmware` and find your desired boot entry.
    2.  Copy the Identifier, including the brackets, e.g. `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`
    3.  Create a batch file with the command `bcdedit /set {fwbootmgr} DEFAULT *{copied boot identifier}*`
    4.  Open *gpedit* and under *Local Computer Policy > Computer Configuration > Windows Settings > Scripts(Startup/Shutdown)*, choose *Startup*
    5.  Under the *Scripts* tab, choose the *Add* button, and select your batch file

### USB media gets struck with black screen

This issue can occur due to [KMS](/index.php/KMS "KMS") issue. Try [Disabling KMS](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") while booting the USB.

### Booting 64-bit kernel on 32-bit UEFI

Both Official ISO ([Archiso](/index.php/Archiso "Archiso")) and [Archboot](/index.php/Archboot "Archboot") iso use EFISTUB (via [systemd-boot](/index.php/Systemd-boot "Systemd-boot") Boot Manager for menu) for booting the kernel in UEFI mode. In such a case you have to use [GRUB](/index.php/GRUB "GRUB") as the USB's UEFI bootloader by following the below section.

#### Using GRUB

**Tip:** The given configuration entries can also be entered inside a [GRUB command-shell](/index.php/GRUB#Using_the_command_shell "GRUB").

*   [Create an USB Flash Installation](/index.php/USB_flash_installation_media#BIOS_and_UEFI_Bootable_USB "USB flash installation media")

*   Backup `EFI/boot/loader.efi` to `EFI/boot/gummiboot.efi`

*   [Create a GRUB standalone image](/index.php/GRUB#GRUB_standalone "GRUB") and copy the generate `grub*.efi` to the USB as `EFI/boot/loader.efi` and/or `EFI/boot/bootia32.efi`

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

On certain UEFI motherboards like some boards with an Intel Z77 chipset, adding entries with `efibootmgr` or `bcfg` from the EFI Shell will not work because they do not show up on the boot menu list after being added to NVRAM.

This issue is caused because the motherboards can only load Microsoft Windows. To solve this you have to place the `.efi` file in the location that Windows uses.

Copy the `bootx64.efi` file from the Arch Linux installation medium (`FSO:`) to the Microsoft directory your [ESP](/index.php/ESP "ESP") partition on your hard drive (`FS1:`). Do this by booting into EFI shell and typing:

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
*   [Linux Kernel x86_64 UEFI Documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt)
*   [Intel's page on EFI](http://www.intel.com/technology/efi/)
*   [Intel Architecture Firmware Resource Center](http://firmware.intel.com/)
*   [Matt Fleming - The Linux EFI Boot Stub](http://firmware.intel.com/blog/linux-efi-boot-stub)
*   [Matt Fleming - Accessing UEFI Variables from Linux](http://firmware.intel.com/blog/accessing-uefi-variables-linux)
*   [Rod Smith - Linux on UEFI: A Quick Installation Guide](http://www.rodsbooks.com/linux-uefi/)
*   [UEFI Boot problems on some newer machines (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [LPC 2012 Plumbing UEFI into Linux](http://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : part 1](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : part 2](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)
*   [Intel's Tianocore Project](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome_to_TianoCore) for Open-Source UEFI firmware which includes DuetPkg for direct BIOS based booting and OvmfPkg used in QEMU and Oracle VirtualBox
*   [FGA: The EFI boot process](https://jdebp.eu/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)
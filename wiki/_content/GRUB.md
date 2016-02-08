# GRUB

[GRUB](https://www.gnu.org/software/grub/) — not to be confused with [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") — is the next generation of the GRand Unified Bootloader. GRUB is derived from [PUPA](http://www.nongnu.org/pupa/) which was a research project to develop the next generation of what is now GRUB Legacy. GRUB has been rewritten from scratch to clean up everything and provide modularity and portability [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1).

## Contents

*   [1 Preface](#Preface)
*   [2 BIOS systems](#BIOS_systems)
    *   [2.1 GUID Partition Table (GPT) specific instructions](#GUID_Partition_Table_.28GPT.29_specific_instructions)
    *   [2.2 Master Boot Record (MBR) specific instructions](#Master_Boot_Record_.28MBR.29_specific_instructions)
    *   [2.3 Installation](#Installation)
        *   [2.3.1 Install boot files](#Install_boot_files)
            *   [2.3.1.1 Install to disk](#Install_to_disk)
            *   [2.3.1.2 Install to external USB stick](#Install_to_external_USB_stick)
            *   [2.3.1.3 Install to partition or partitionless disk](#Install_to_partition_or_partitionless_disk)
            *   [2.3.1.4 Generate core.img alone](#Generate_core.img_alone)
*   [3 UEFI systems](#UEFI_systems)
    *   [3.1 Check if you have GPT and an ESP](#Check_if_you_have_GPT_and_an_ESP)
    *   [3.2 Create an ESP](#Create_an_ESP)
    *   [3.3 Installation](#Installation_2)
    *   [3.4 Further reading](#Further_reading)
        *   [3.4.1 Alternative install method](#Alternative_install_method)
        *   [3.4.2 UEFI firmware workaround](#UEFI_firmware_workaround)
        *   [3.4.3 Create a GRUB entry in the firmware boot manager](#Create_a_GRUB_entry_in_the_firmware_boot_manager)
        *   [3.4.4 GRUB standalone](#GRUB_standalone)
        *   [3.4.5 Technical information](#Technical_information)
*   [4 Generate the main configuration file](#Generate_the_main_configuration_file)
*   [5 Configuration](#Configuration)
    *   [5.1 Additional arguments](#Additional_arguments)
    *   [5.2 Dual-booting](#Dual-booting)
        *   [5.2.1 Automatically generating using /etc/grub.d/40_custom and grub-mkconfig](#Automatically_generating_using_.2Fetc.2Fgrub.d.2F40_custom_and_grub-mkconfig)
            *   [5.2.1.1 GNU/Linux menu entry](#GNU.2FLinux_menu_entry)
            *   [5.2.1.2 FreeBSD menu entry](#FreeBSD_menu_entry)
                *   [5.2.1.2.1 Loading the kernel directly](#Loading_the_kernel_directly)
                *   [5.2.1.2.2 Chainloading the embedded boot record](#Chainloading_the_embedded_boot_record)
                *   [5.2.1.2.3 Running the traditional BSD 2nd stage loader](#Running_the_traditional_BSD_2nd_stage_loader)
            *   [5.2.1.3 Windows installed in UEFI-GPT Mode menu entry](#Windows_installed_in_UEFI-GPT_Mode_menu_entry)
            *   [5.2.1.4 "Shutdown" menu entry](#.22Shutdown.22_menu_entry)
            *   [5.2.1.5 "Restart" menu entry](#.22Restart.22_menu_entry)
            *   [5.2.1.6 Windows installed in BIOS-MBR mode](#Windows_installed_in_BIOS-MBR_mode)
        *   [5.2.2 With Windows via EasyBCD and NeoGRUB](#With_Windows_via_EasyBCD_and_NeoGRUB)
        *   [5.2.3 parttool for hide/unhide](#parttool_for_hide.2Funhide)
    *   [5.3 LVM](#LVM)
    *   [5.4 RAID](#RAID)
    *   [5.5 Multiple entries](#Multiple_entries)
    *   [5.6 Encryption](#Encryption)
        *   [5.6.1 Root partition](#Root_partition)
        *   [5.6.2 Boot partition](#Boot_partition)
*   [6 Using the command shell](#Using_the_command_shell)
    *   [6.1 Pager support](#Pager_support)
    *   [6.2 Using the command shell environment to boot operating systems](#Using_the_command_shell_environment_to_boot_operating_systems)
        *   [6.2.1 Chainloading a partition](#Chainloading_a_partition)
        *   [6.2.2 Chainloading a disk/drive](#Chainloading_a_disk.2Fdrive)
        *   [6.2.3 Chainloading Windows/Linux installed in UEFI mode](#Chainloading_Windows.2FLinux_installed_in_UEFI_mode)
        *   [6.2.4 Normal loading](#Normal_loading)
    *   [6.3 Using the rescue console](#Using_the_rescue_console)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Intel BIOS not booting GPT](#Intel_BIOS_not_booting_GPT)
        *   [7.1.1 MBR](#MBR)
        *   [7.1.2 EFI path](#EFI_path)
    *   [7.2 Enable debug messages](#Enable_debug_messages)
    *   [7.3 "No suitable mode found" error](#.22No_suitable_mode_found.22_error)
    *   [7.4 msdos-style error message](#msdos-style_error_message)
    *   [7.5 UEFI](#UEFI)
        *   [7.5.1 Common installation errors](#Common_installation_errors)
        *   [7.5.2 Drop to rescue shell](#Drop_to_rescue_shell)
        *   [7.5.3 GRUB UEFI not loaded](#GRUB_UEFI_not_loaded)
    *   [7.6 Invalid signature](#Invalid_signature)
    *   [7.7 Boot freezes](#Boot_freezes)
    *   [7.8 Arch not found from other OS](#Arch_not_found_from_other_OS)
    *   [7.9 Warning when installing in chroot](#Warning_when_installing_in_chroot)
    *   [7.10 GRUB loads slowly](#GRUB_loads_slowly)
    *   [7.11 error: unknown filesystem](#error:_unknown_filesystem)
    *   [7.12 grub-reboot not resetting](#grub-reboot_not_resetting)
    *   [7.13 Old BTRFS prevents installation](#Old_BTRFS_prevents_installation)
*   [8 See also](#See_also)

## Preface

*   A _bootloader_ is the first software program that runs when a computer starts. It is responsible for loading and transferring control to the Linux kernel. The kernel, in turn, initializes the rest of the operating system.
*   The name _GRUB_ officially refers to version _2_ of the software, see [[2]](https://www.gnu.org/software/grub/). If you are looking for the article on the legacy version, see [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").
*   GRUB supports [Btrfs](/index.php/Btrfs "Btrfs") as root (without a separate `/boot` file system) compressed with either zlib or LZO
    *   GRUB currently (Sep 2015) supports booting from [Btrfs](/index.php/Btrfs "Btrfs") RAID 0/1/10, but _not_ RAID 5/6\. You may use [mdadm](/index.php/Mdadm "Mdadm") for RAID 5/6, which is supported by GRUB.
*   GRUB does not support [F2FS](/index.php/F2FS "F2FS") as root so you will need a separate `/boot` with a supported file system.

## BIOS systems

### GUID Partition Table (GPT) specific instructions

On a BIOS/[GPT](/index.php/GPT "GPT") configuration a [BIOS boot partition](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) is required. GRUB embeds its `core.img` into this partition.

**Note:**

*   Before attempting this method keep in mind that not all systems will be able to support this partitioning scheme, read more on [GUID partition tables](/index.php/GUID_Partition_Table#BIOS_systems "GUID Partition Table").
*   This additional partition is only needed on a GRUB, BIOS/GPT partitioning scheme. Previously, for a GRUB, BIOS/MBR partitioning scheme, GRUB used the Post-MBR gap for the embedding the `core.img`). GRUB for GPT, however, does not use the Post-GPT gap to conform to GPT specifications that require 1_megabyte/2048_sector disk boundaries.
*   For [UEFI](/index.php/UEFI "UEFI") systems this extra partition is not required as no embedding of boot sectors takes place in that case.

Create a mebibyte partition (`+1M` with `fdisk` or `gdisk`) on the disk with no file system and type BIOS boot (_BIOS boot_ in fdisk, `ef02` in gdisk, `bios_grub` in `parted`). This partition can be in any position order but has to be on the first 2 TiB of the disk. This partition needs to be created before GRUB installation. When the partition is ready, install the bootloader as per the instructions below.

The post-GPT gap can also be used as the BIOS boot partition though it will be out of GPT alignment specification. Since the partition will not be regularly accessed performance issues can be disregarded (though some disk utilities will display a warning about it). In `fdisk` or `gdisk` create a new partition starting at sector 34 and spanning to 2047 and set the type. To have the viewable partitions begin at the base consider adding this partition last.

### Master Boot Record (MBR) specific instructions

Usually the post-[MBR](/index.php/MBR "MBR") gap (after the 512 byte MBR region and before the start of the first partition) in many MBR (or 'msdos' disklabel) partitioned systems is 31 KiB when DOS compatibility cylinder alignment issues are satisfied in the partition table. However a post-MBR gap of about 1 to 2 MiB is recommended to provide sufficient room for embedding GRUB's `core.img` ([FS#24103](https://bugs.archlinux.org/task/24103)). It is advisable to use a partitioning tool that supports 1 MiB partition alignment to obtain this space as well as to satisfy other non-512 byte sector issues (which are unrelated to embedding of `core.img`).

### Installation

[Install](/index.php/Install "Install") the [grub](https://www.archlinux.org/packages/?name=grub) package. It will replace [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), where already installed.

**Note:** Simply installing the package will not update the `/boot/grub/i386-pc/core.img` file and the GRUB modules in `/boot/grub/i386-pc`. You need to update them manually using `grub-install` as explained below.

#### Install boot files

There are 4 ways to install GRUB boot files in BIOS booting:

*   [Install to disk](#Install_to_disk) (recommended)
*   [Install to external USB stick](#Install_to_external_USB_stick) (for recovery)
*   [Install to partition or partitionless disk](#Install_to_partition_or_partitionless_disk) (not recommended)
*   [Generate core.img alone](#Generate_core.img_alone) (safest method, but requires another BIOS bootloader like [Syslinux](/index.php/Syslinux "Syslinux") to be installed to chainload `/boot/grub/i386-pc/core.img`)

**Note:** See [https://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](https://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) for additional documentation.

##### Install to disk

**Note:** The method is specific to installing GRUB to a partitioned (MBR or GPT) disk, with GRUB files installed to `/boot/grub` and its first stage code installed to the 440-byte MBR boot code region (not to be confused with MBR partition table).

The following commands will:

*   Set up GRUB in the 440-byte Master Boot Record boot code region
*   Populate the `/boot/grub` directory
*   Generate the `/boot/grub/i386-pc/core.img` file
*   Embed it in the 31 KiB (minimum size - varies depending on partition alignment) post-MBR gap in case of MBR partitioned disk
*   In the case of a GPT partitioned disk it will embed it in the BIOS Boot Partition , denoted by `bios_grub` flag in parted and EF02 type code in gdisk

```
# grub-install --target=i386-pc /dev/sd_x_
# grub-mkconfig -o /boot/grub/grub.cfg

```

If you use [LVM](/index.php/LVM "LVM") for your `/boot`, you can install GRUB on multiple physical disks.

##### Install to external USB stick

Assume your USB stick's first partition is FAT32 and its partition is /dev/sdy1

```
# mkdir -p /mnt/usb ; mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

```
# optional, backup config files of grub.cfg
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
# sync; umount /mnt/usb

```

##### Install to partition or partitionless disk

**Warning:** GRUB **strongly discourages** installation to a partition boot sector or a partitionless disk as GRUB Legacy or Syslinux does. This setup is prone to breakage, especially during updates, and is **not supported** by the Arch developers.

To set up grub to a partition boot sector, to a partitionless disk (also called superfloppy) or to a floppy disk, run (using for example `/dev/sdaX` as the `/boot` partition):

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

**Note:**

*   `/dev/sdaX` used for example only.
*   `--target=i386-pc` instructs `grub-install` to install for BIOS systems only. It is recommended to always use this option to remove ambiguity in _grub-install_.

You need to use the `--force` option to allow usage of blocklists and should not use `--grub-setup=/bin/true` (which is similar to simply generating `core.img`).

`grub-install` will give out warnings like which should give you the idea of what might go wrong with this approach:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

Without `--force` you may get the below error and `grub-setup` will not setup its boot code in the partition boot sector:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

With `--force` you should get:

```
Installation finished. No error reported.

```

The reason why `grub-setup` does not by default allow this is because in case of partition or a partitionless disk is that GRUB relies on embedded blocklists in the partition bootsector to locate the `/boot/grub/i386-pc/core.img` file and the prefix directory `/boot/grub`. The sector locations of `core.img` may change whenever the file system in the partition is being altered (files copied, deleted etc.). For more info, see [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) and [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

The workaround for this is to set the immutable flag on `/boot/grub/i386-pc/core.img` (using `chattr` command as mentioned above) so that the sector locations of the `core.img` file in the disk is not altered. The immutable flag on `/boot/grub/i386-pc/core.img` needs to be set only if GRUB is installed to a partition boot sector or a partitionless disk, not in case of installation to MBR or simple generation of `core.img` without embedding any bootsector (mentioned above).

Unfortunately, the `grub.cfg` file that is created will not contain the proper UUID in order to boot, even if it reports no errors. see [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604). In order to fix this issue the following commands:

```
# mount /dev/sdxY /mnt        #Your root partition.
# mount /dev/sdxZ /mnt/boot   #Your boot partition (if you have one).
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

##### Generate core.img alone

To populate the `/boot/grub` directory and generate a `/boot/grub/i386-pc/core.img` file **without** embedding any GRUB bootsector code in the MBR, post-MBR region, or the partition bootsector, add `--grub-setup=/bin/true` to `grub-install`:

```
# grub-install --target=i386-pc --grub-setup=/bin/true --debug /dev/sda

```

**Note:**

*   `/dev/sda` used for example only.
*   `--target=i386-pc` instructs `grub-install` to install for BIOS systems only. It is recommended to always use this option to remove ambiguity in grub-install.

You can then chainload GRUB's `core.img` from GRUB Legacy or syslinux as a Linux kernel or as a multiboot kernel (see also [Syslinux#Chainloading](/index.php/Syslinux#Chainloading "Syslinux")).

## UEFI systems

**Note:**

*   It is recommended to read and understand the [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") pages.
*   When installing to use UEFI it is important to start the install with your machine in UEFI mode. The Arch Linux install media must be UEFI bootable.

### Check if you have GPT and an ESP

An EFI System Partition (ESP) is needed on every disc you want to boot using EFI. GPT is not strictly necessary, but it is highly recommended and is the only method currently supported in this article. If you are installing Arch Linux on an EFI-capable computer with an already-working operating system, like Windows 8 for example, it is very likely that you already have an ESP. To check for GPT and for an ESP, use `parted` as root to print the partition table of the disk you want to boot from. (We are calling it `/dev/sda`.)

```
# parted /dev/sda print

```

For GPT, you are looking for "Partition Table: GPT". For EFI, you are looking for a small (512 MiB or less) partition with a vfat file system and the _boot_ flag enabled. On it, there should be a directory named "EFI". If these criteria are met, this is your ESP. Make note of the partition number. You will need to know which one it is, so you can mount it later on while installing GRUB to it.

### Create an ESP

If you do not have an ESP, you will need to create one. See [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")

### Installation

**Note:** UEFI firmware are not implemented consistently by hardware manufacturers. The installation examples provided are intended to work on the widest range of UEFI systems possible. Those experiencing problems despite applying these methods are encouraged to share detailed information for their hardware-specific cases, especially where solving these problems. A [GRUB/EFI examples](/index.php/GRUB/EFI_examples "GRUB/EFI examples") article has been provided for such cases.

This section assumes you are installing GRUB for x86_64 systems (x86_64-efi). For i686 systems, replace `x86_64-efi` with `i386-efi` where appropriate.

Make sure you are in a [bash](/index.php/Bash "Bash") shell. For example, when booting from the Arch ISO:

```
# arch-chroot /mnt /bin/bash

```

[Install](/index.php/Install "Install") the packages [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr). _GRUB_ is the bootloader, _efibootmgr_ creates bootable `.efi` stub entries used by the GRUB installation script.

The following steps install the GRUB UEFI application to `**$esp**/EFI/grub`, install its modules to `/boot/grub/x86_64-efi`, and place the bootable `grubx64.efi` stub in `**$esp**/EFI/grub`.

First, tell GRUB to use UEFI, set the boot directory and set the bootloader ID. Change `$esp` to your efi partition (usually `/boot`):

```
# grub-install --target=x86_64-efi --efi-directory=**$esp** --bootloader-id=**grub**

```

The `--bootloader-id` is what appears in the boot options to identify the GRUB EFI boot option; make sure this is something you will recognize later. The install will create a directory of the same name under `$esp/EFI/` where the EFI binary bootloader will be placed.

After the above install finished the main GRUB directory is located at `/boot/grub/`.

Remember to [#Generate the main configuration file](#Generate_the_main_configuration_file) after finalizing further setup dependant [#Configuration](#Configuration).

**Note:**

*   While some distributions require a `/boot/efi` or `/boot/EFI` directory, Arch does not.
*   `--efi-directory` and `--bootloader-id` are specific to GRUB UEFI. `--efi-directory` specifies the mountpoint of the ESP. It replaces `--root-directory`, which is deprecated.
*   You might note the absence of a <device_path> option (e.g.: `/dev/sda`) in the `grub-install` command. In fact any <device_path> provided will be ignored by the GRUB install script, as UEFI bootloaders do not use a MBR or partition boot sector at all.

See [UEFI troubleshooting](#UEFI) in case of problems.

### Further reading

Below is other relevant information regarding installing Arch via UEFI

#### Alternative install method

Usually, GRUB keeps all files, including configuration files, in `/boot`, regardless of where the EFI System Partition is mounted.

If you want to keep these files inside the EFI System Partition itself, add `--boot-directory=$esp` to the grub-install command:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub --boot-directory=$esp --debug

```

This puts all GRUB files in `$esp/grub`, instead of in `/boot/grub`. When using this method, make sure you have _grub-mkconfig_ put the configuration file in the same place:

```
# grub-mkconfig -o $esp/grub/grub.cfg

```

Configuration is otherwise the same.

#### UEFI firmware workaround

Some UEFI firmware requires that the bootable `.efi` stub have a specific name and be placed in a specific location: `$esp/EFI/boot/bootx64.efi` (where `$esp` is the UEFI partition mountpoint). Failure to do so in such instances will result in an unbootable installation. Fortunately, this will not cause any problems with other firmware that does not require this.

To do so, first create the necessary directory, and then copy across the grub `.efi` stub, renaming it in the process:

```
# mkdir $esp/EFI/boot
# cp $esp/EFI/grub_uefi/grubx64.efi  $esp/EFI/boot/bootx64.efi

```

#### Create a GRUB entry in the firmware boot manager

`grub-install` automatically tries to create a menu entry in the boot manager. If it does not, then see [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI") for instructions to use `efibootmgr` to create a menu entry. However, the problem is likely to be that you have not booted your CD/USB in UEFI mode, as in [UEFI#Create UEFI bootable USB from ISO](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

#### GRUB standalone

This section assumes you are creating a standalone GRUB for x86_64 systems (x86_64-efi). For i686 systems, replace `x86_64-efi` with `i386-efi` where appropriate.

It is possible to create a `grubx64_standalone.efi` application which has all the modules embedded in a tar archive within the UEFI application, thus removing the need for having a separate directory populated with all of the GRUB UEFI modules and other related files. This is done using the `grub-mkstandalone` command (included in [grub](https://www.archlinux.org/packages/?name=grub)) as follows:

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg
# grub-mkstandalone -d /usr/lib/grub/x86_64-efi/ -O x86_64-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="en@quot" --themes="" -o "$esp/EFI/grub/grubx64_standalone.efi"  "boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

Then copy the GRUB config file to `$esp/EFI/grub/grub.cfg` and create a UEFI Boot Manager entry for `$esp/EFI/grub/grubx64_standalone.efi` using [efibootmgr](/index.php/UEFI#efibootmgr "UEFI").

**Note:**

The option `--modules="part_gpt part_msdos"` (with the quotes) is necessary for the `${cmdpath}` feature to work properly.

**Warning:** You may find that the `grub.cfg` file is not loaded due to `${cmdpath}` missing a slash (i.e. `(hd1,msdos2)EFI/Boot` instead of `(hd1,msdos2)/EFI/Boot`) and so you are dropped into a GRUB shell. If this happens determine what `${cmdpath}` is set to (`echo ${cmdpath}` ) and then load the config file manually (e.g. `configfile (hd1,msdos2)/EFI/Boot/grub.cfg`).

#### Technical information

The GRUB EFI file always expects its config file to be at `${prefix}/grub.cfg`. However in the standalone GRUB EFI file, the `${prefix}` is located inside a tar archive and embedded inside the standalone GRUB EFI file itself (inside the GRUB environment, it is denoted by `"(memdisk)"`, without quotes). This tar archive contains all the files that would be stored normally at `/boot/grub` in case of a normal GRUB EFI install.

Due to this embedding of `/boot/grub` contents inside the standalone image itself, it does not rely on actual (external) `/boot/grub` for anything. Thus in case of standalone GRUB EFI file `${prefix}==(memdisk)/boot/grub` and the standalone GRUB EFI file reads expects the config file to be at `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`.

Hence to make sure the standalone GRUB EFI file reads the external `grub.cfg` located in the same directory as the EFI file (inside the GRUB environment, it is denoted by `${cmdpath}` ), we create a simple `/tmp/grub.cfg` which instructs GRUB to use `${cmdpath}/grub.cfg` as its config (`configfile ${cmdpath}/grub.cfg` command in `(memdisk)/boot/grub/grub.cfg`). We then instruct grub-mkstandalone to copy this `/tmp/grub.cfg` file to `${prefix}/grub.cfg` (which is actually `(memdisk)/boot/grub/grub.cfg`) using the option `"boot/grub/grub.cfg=/tmp/grub.cfg"`.

This way, the standalone GRUB EFI file and actual `grub.cfg` can be stored in any directory inside the EFI System Partition (as long as they are in the same directory), thus making them portable.

## Generate the main configuration file

After the installation, the main configuration file `grub.cfg` needs to be generated. The generation process can be influenced by a variety of options in `/etc/default/grub` and scripts in `/etc/grub.d/`; see [#Configuration](#Configuration).

If you have not done additional configuration, the automatic generation will determine the root filesystem of the system to boot for the configuration file. For that to succeed it is important that the system is either booted or chrooted into.

**Note:** Remember that `grub.cfg` has to be re-generated after any change to `/etc/default/grub` or files in `/etc/grub.d/`.

Use the _grub-mkconfig_ tool to generate `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:**

*   The default file path is `/boot/grub/grub.cfg`, not `/boot/grub/i386-pc/grub.cfg`. The [grub](https://www.archlinux.org/packages/?name=grub) includes a sample `/boot/grub/grub.cfg`; ensure your intended changes were written to this file.
*   If you are trying to run _grub-mkconfig_ in a chroot or _systemd-nspawn_ container, you might notice that it does not work, complaining that _grub-probe_ cannot get the "canonical path of /dev/sdaX". In this case, try using _arch-chroot_ as described in the [BBS post](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

By default the generation scripts automatically add menu entries for Arch Linux to any generated configuration. See [#Dual-booting](#Dual-booting) for configuration with other systems.

## Configuration

This section only covers editing the `/etc/default/grub` configuration file. See [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks") for more information.

Remember to always [#Generate the main configuration file](#Generate_the_main_configuration_file) after making changes to `/etc/default/grub`.

### Additional arguments

To pass custom additional arguments to the Linux image, you can set the `GRUB_CMDLINE_LINUX` + `GRUB_CMDLINE_LINUX_DEFAULT` variables in `/etc/default/grub`. The two are appended to each other and passed to kernel when generating regular boot entries. For the _recovery_ boot entry, only `GRUB_CMDLINE_LINUX` is used in the generation.

It is not necessary to use both, but can be useful. For example, you could use `GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` where `sda**X**` is your swap partition to enable resume after hibernation. This would generate a recovery boot entry without the resume and without _quiet_ suppressing kernel messages during a boot from that menu entry. Though, the other (regular) menu entries would have them as options.

By default _grub-mkconfig_ determines the [UUID](/index.php/UUID "UUID") of the root filesystem for the configuration. To disable this, uncomment `GRUB_DISABLE_LINUX_UUID=true`.

For generating the GRUB recovery entry you also have to comment out `#GRUB_DISABLE_RECOVERY=true` in `/etc/default/grub`.

You can also use `GRUB_CMDLINE_LINUX="resume=UUID=uuid-of-swap-partition"`

See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

### Dual-booting

**Tip:** To have _grub-mkconfig_ search for other installed systems, [install](/index.php/Install "Install") [os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### Automatically generating using /etc/grub.d/40_custom and grub-mkconfig

The best way to add other entries is editing the `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg`. The entries in this file will be automatically added when running `grub-mkconfig`. After adding the new lines, run:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

or, for UEFI-GPT Mode (As per [#Alternative install method](#Alternative_install_method)):

 `# grub-mkconfig -o /boot/efi/EFI/GRUB/grub.cfg` 

to generate an updated `grub.cfg`.

For example, a typical `/etc/grub.d/40_custom` file, could appear similar to the following one, created for [HP Pavilion 15-e056sl Notebook PC](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&destPage=product&lc=en&product=5402703&tmp_docname=), originally with Microsoft Windows 8 preinstalled. Each `menuentry` should maintain a structure similar to the following ones. Note that the UEFI partition `/dev/sda2` within GRUB is called `hd0,gpt2` and `ahci0,gpt2` (see [here](#Windows_installed_in_UEFI-GPT_Mode_menu_entry) for more info).

 `/etc/grub.d/40_custom` 

```
#!/bin/sh
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.

menuentry "HP / Microsoft Windows 8.1" {
	echo "Loading HP / Microsoft Windows 8.1..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "HP / Microsoft Control Center" {
	echo "Loading HP / Microsoft Control Center..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/HP/boot/bootmgfw.efi
}

menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}

menuentry "System restart" {
	echo "System rebooting..."
	reboot
}
```

##### GNU/Linux menu entry

Assuming that the other distro is on partition `sda2`:

```
menuentry "Other Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (add other options here as required)
	initrd /boot/initrd.img (if the other kernel uses/needs one)
}
```

Alternatively let grub search for the right partition by _UUID_ or _label_:

```
menuentry "Other Linux" {
        # assuming that UUID is 763A-9CB6
	search --set=root --fs-uuid 763A-9CB6

        # search by label OTHER_LINUX (make sure that partition label is unambiguous)
        #search --set=root --label OTHER_LINUX

	linux /boot/vmlinuz (add other options here as required, for example: root=UUID=763A-9CB6)
	initrd /boot/initrd.img (if the other kernel uses/needs one)
}
```

##### FreeBSD menu entry

The following three methods require that FreeBSD is installed on a single partition with UFS(v2). Assuming the nested BSD partition table is on `sda4`:

###### Loading the kernel directly

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	## or 'hd0,msdos4,bsd1', if using an IBM-PC (MS-DOS) style partition table
	kfreebsd /boot/kernel/kernel
	kfreebsd_loadenv /boot/device.hints
	set kFreeBSD.vfs.root.mountfrom=ufs:/dev/ada0s4a
	set kFreeBSD.vfs.root.mountfrom.options=rw
}
```

###### Chainloading the embedded boot record

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	chainloader +1
}
```

###### Running the traditional BSD 2nd stage loader

```
menuentry 'FreeBSD' {
  insmod ufs2
  set root='(hd0,4)'
  kfreebsd /boot/loader
}
```

##### Windows installed in UEFI-GPT Mode menu entry

**Note:** This menuentry will work only in UEFI boot mode and only if the Windows bitness matches the UEFI bitness. It **WILL NOT WORK** in BIOS installed GRUB. See [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") and [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") for more info.

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 UEFI-GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

where `$hints_string` and `$fs_uuid` are obtained with the following two commands. `$fs_uuid`'s command:

 `# grub-probe --target=fs_uuid $esp/EFI/Microsoft/Boot/bootmgfw.efi`  `1ce5-7f28` 

`$hints_string`'s command:

 `# grub-probe --target=hints_string $esp/EFI/Microsoft/Boot/bootmgfw.efi`  `--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1` 

These two commands assume the ESP Windows uses is mounted at `$esp`. There might be case differences in the path to Windows's EFI file, what with being Windows, and all.

##### "Shutdown" menu entry

```
menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}
```

##### "Restart" menu entry

```
menuentry "System restart" {
	echo "System rebooting..."
	reboot
}
```

##### Windows installed in BIOS-MBR mode

**Note:** GRUB supports booting `bootmgr` directly and chainload of partition boot sector is no longer required to boot Windows in a BIOS-MBR setup.

**Warning:** It is the **system partition** that has `/bootmgr`, not your "real" Windows partition (usually C:). In `blkid` output, the system partition is the one with `LABEL="SYSTEM RESERVED"` or `LABEL="SYSTEM"` and is only about 100 to 200 MB in size (much like the boot partition for Arch). See [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") for more info.

Throughout this section, it is assumed your Windows partition is `/dev/sda1`. A different partition will change every instance of hd0,msdos1\. First, find the UUID of the NTFS file system of the Windows's SYSTEM PARTITION where the `bootmgr` and its files reside. For example, if Windows `bootmgr` exists at `/media/SYSTEM_RESERVED/bootmgr`:

For Windows Vista/7/8/8.1:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**Note:** For Windows XP, replace `bootmgr` with `NTLDR` in the above commands. And note that there may not be a separate SYSTEM_RESERVED partition; just probe the file NTLDR on your Windows partition.

Then, add the below code to `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg` and regenerate `grub.cfg` with `grub-mkconfig` as explained above to boot Windows (XP, Vista, 7 or 8) installed in BIOS-MBR mode:

**Note:** These menuentries will work only in Legacy BIOS boot mode. It WILL NOT WORK in uefi installed grub(2). See [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") and [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows").

For Windows Vista/7/8/8.1:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows Vista/7/8/8.1 BIOS-MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi

```

For Windows XP:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /ntldr
  }
fi

```

**Note:** In some cases, mine I have installed GRUB before a clean Windows 8, you cannot boot Windows having an error with `\boot\bcd` (error code `0xc000000f`). You can fix it going to Windows Recovery Console (cmd from install disk) and executing:

```
x:\> "bootrec.exe /fixboot" 
x:\> "bootrec.exe /RebuildBcd".

```

Do **not** use `bootrec.exe /Fixmbr` because it will wipe GRUB out.

`/etc/grub.d/40_custom` can be used as a template to create `/etc/grub.d/nn_custom`. Where `nn` defines the precendence, indicating the order the script is executed. The order scripts are executed determine the placement in the grub boot menu.

**Note:** `nn` should be greater than 06 to ensure necessary scripts are executed first.

#### With Windows via EasyBCD and NeoGRUB

Since EasyBCD's NeoGRUB currently does not understand the GRUB menu format, chainload to it by replacing the contents of your `C:\NST\menu.lst` file with lines similar to the following:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

Finally, [#Generate the main configuration file](#Generate_the_main_configuration_file).

#### parttool for hide/unhide

If you have a Windows 9x paradigm with hidden `C:\` disks GRUB can hide/unhide it using `parttool`. For example, to boot the third `C:\` disk of three Windows 9x installations on the CLI enter the CLI and:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot

```

### LVM

If you use [LVM](/index.php/LVM "LVM") for your `/boot`, make sure that the `lvm` module is preloaded:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="lvm"` 

### RAID

GRUB provides convenient handling of RAID volumes. You need to add `insmod mdraid` which allows you to address the volume natively. For example, `/dev/md0` becomes:

```
set root=(md/0)

```

whereas a partitioned RAID volume (e.g. `/dev/md0p1`) becomes:

```
set root=(md/0,1)

```

To install grub when using RAID1 as the `/boot` partition (or using `/boot` housed on a RAID1 root partition), on devices with GPT ef02/'BIOS boot partition', simply run _grub-install_ on both of the drives, such as:

```
# grub-install --target=i386-pc --debug /dev/sda
# grub-install --target=i386-pc --debug /dev/sdb

```

Where the RAID 1 array housing `/boot` is housed on `/dev/sda` and `/dev/sdb`.

### Multiple entries

For tips on managing multiple GRUB entries, for example when using both [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels, see [GRUB/Tips and tricks#Multiple entries](/index.php/GRUB/Tips_and_tricks#Multiple_entries "GRUB/Tips and tricks").

### Encryption

#### Root partition

For an encrypted root filesystem, it is necessary to edit `/etc/default/grub` with the parameters required to unlock the encrypted filesystem during boot. For example, if the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") `encrypt` hook is used, the `cryptdevice` parameter must be added to `GRUB_CMDLINE_LINUX=""` command. In the example below, the `sda2` partition has been encrypted as `/dev/mapper/cryptroot`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:cryptroot"` 

Once `/etc/default/grub` has been amended, it will then be necessary to [#Generate the main configuration file](#Generate_the_main_configuration_file).

For further information about bootloader configuration for encrypted devices, see [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

**Tip:** If you are upgrading from a working GRUB Legacy configuration, check `/boot/grub/menu.lst.pacsave` for the correct device/label to add. Look for them after the text `kernel /vmlinuz-linux`.

#### Boot partition

The GRUB [parameter](https://www.gnu.org/software/grub/manual/grub.html#Simple-configuration) `GRUB_ENABLE_CRYPTODISK` can be used to enable GRUB to ask for a password to open a [LUKS](/index.php/LUKS "LUKS") blockdevice in order to read its configuration and load any [initramfs](/index.php/Initramfs "Initramfs") and [kernel](/index.php/Kernel "Kernel") from it. This option tries to solve the issue of having an [unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

The feature is enabled by adding:

```
GRUB_ENABLE_CRYPTODISK=y

```

to `/etc/default/grub`. After this configuration a subsequent run of _grub-mkconfig_ to [#Generate the main configuration file](#Generate_the_main_configuration_file) is required while the encrypted `/boot` is mounted.

**Note:** `GRUB_ENABLE_CRYPTODISK=1` [will not work](https://savannah.gnu.org/bugs/?41524) as opposed to the request shown in GRUB 2.02-beta2.

Depending on the system's setup, note the following:

*   For the feature to work it is not required that `/boot` is kept in a separate partition, it may also stay under the system's root `/` directory tree.

*   Without further changes you will be prompted twice for a passhrase: the first for GRUB to unlock the `/boot` mount point in early boot, the second to unlock the root filesystem itself as described in [#Root partition](#Root_partition).

    **Tip:** See [Dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") for a workaround.

*   In order to perform system updates involving the `/boot` mount point, it must be ensured that the encrypted `/boot` is unlocked to be re-mounted by the initramfs and kernel during boot. With a separate `/boot` partition, this may be accomplished by adding an entry to `/etc/crypttab` with a keyfile. See [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

*   If you use a special keymap, a default GRUB installation will not know it. This is relevant for how to enter the passphrase to unlock the LUKS blockdevice.

*   If you experience issues getting the prompt for a password to display (errors regarding cryptouuid, cryptodisk, or "device not found"), try reinstalling grub as below appending the following to the end of your installation command:

```
 grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub **--modules="part_gpt part_msdos"**

```

## Using the command shell

Since the MBR is too small to store all GRUB modules, only the menu and a few basic commands reside there. The majority of GRUB functionality remains in modules in `/boot/grub`, which are inserted as needed. In error conditions (e.g. if the partition layout changes) GRUB may fail to boot. When this happens, a command shell may appear.

GRUB offers multiple shells/prompts. If there is a problem reading the menu but the bootloader is able to find the disk, you will likely be dropped to the "normal" shell:

```
grub>

```

If there is a more serious problem (e.g. GRUB cannot find required files), you may instead be dropped to the "rescue" shell:

```
grub rescue>

```

The rescue shell is a restricted subset of the normal shell, offering much less functionality. If dumped to the rescue shell, first try inserting the "normal" module, then starting the "normal" shell:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal

```

### Pager support

GRUB supports pager for reading commands that provide long output (like the `help` command). This works only in normal shell mode and not in rescue mode. To enable pager, in GRUB command shell type:

```
sh:grub> set pager=1

```

### Using the command shell environment to boot operating systems

```
grub>

```

The GRUB's command shell environment can be used to boot operating systems. A common scenario may be to boot Windows / Linux stored on a drive/partition via **chainloading**.

_Chainloading_ means to load another boot-loader from the current one, ie, chain-loading.

The other bootloader may be embedded at the starting of the disk(MBR) or at the starting of a partition.

#### Chainloading a partition

```
set root=(hdX,Y)
chainloader +1
boot

```

X=0,1,2... Y=1,2,3...

For example to chainload Windows stored in the first partiton of the first hard disk,

```
set root=(hd0,1)
chainloader +1
boot

```

Similarly GRUB installed to a partition can be chainloaded.

#### Chainloading a disk/drive

```
set root=hdX
chainloader +1
boot

```

#### Chainloading Windows/Linux installed in UEFI mode

```
insmod ntfs
set root=(hd0,gpt4)
chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
boot

```

_insmod ntfs_ used for loading the ntfs file system module for loading Windows. (hd0,gpt4) or /dev/sda4 is my EFI System Partition (ESP). The entry in the _chainloader_ line specifies the path of the .efi file to be chain-loaded.

#### Normal loading

See the examples in [#Using the rescue console](#Using_the_rescue_console)

### Using the rescue console

See [#Using the command shell](#Using_the_command_shell) first. If unable to activate the standard shell, one possible solution is to boot using a live CD or some other rescue disk to correct configuration errors and reinstall GRUB. However, such a boot disk is not always available (nor necessary); the rescue console is surprisingly robust.

The available commands in GRUB rescue include `insmod`, `ls`, `set`, and `unset`. This example uses `set` and `insmod`. `set` modifies variables and `insmod` inserts new modules to add functionality.

Before starting, the user must know the location of their `/boot` partition (be it a separate partition, or a subdirectory under their root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

where X is the physical drive number and Y is the partition number.

To expand console capabilities, insert the `linux` module:

```
grub rescue> insmod i386-pc/linux.mod

```

**Note:** With a separate boot partition, omit `/boot` from the path, (i.e. type `set prefix=(hdX,Y)/grub`).

This introduces the `linux` and `initrd` commands, which should be familiar.

An example, booting Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

With a separate boot partition, again change the lines accordingly:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot

```

**Note:** If you experienced `error: premature end of file /YOUR_KERNEL_NAME` during execution of `linux` command, you can try `linux16` instead.

After successfully booting the Arch Linux installation, users can correct `grub.cfg` as needed and then reinstall GRUB.

To reinstall GRUB and fix the problem completely, changing `/dev/sda` if needed. See [#Installation](#Installation) for details.

## Troubleshooting

### Intel BIOS not booting GPT

#### MBR

Some Intel BIOS's require at least one bootable MBR partition to be present at boot, causing GPT-partitioned boot setups to be unbootable.

This can be circumvented by using (for instance) fdisk to mark one of the GPT partitions (preferably the 1007 KiB partition you have created for GRUB already) bootable in the MBR. This can be achieved, using fdisk, by the following commands: Start fdisk against the disk you are installing, for instance `fdisk /dev/sda`, then press `a` and select the partition you wish to mark as bootable (probably #1) by pressing the corresponding number, finally press `w` to write the changes to the MBR.

**Note:** The bootable-marking must be done in `fdisk` or similar, not in GParted or others, as they will not set the bootable flag in the MBR.

With cfdisk, the steps are similar, just `cfdisk /dev/sda`, choose bootable (at the left) in the desired hard disk, and quit saving.

More information is available [here](http://www.rodsbooks.com/gdisk/bios.html)

#### EFI path

Some UEFI firmwares require a bootable file at a known location before they will show UEFI NVRAM boot entries. If this is the case, `grub-install` will claim `efibootmgr` has added an entry to boot GRUB, however the entry will not show up in the VisualBIOS boot order selector. The solution is to place a file at one of the known locations. Assuming the EFI partition is at `/boot/efi/` this will work:

```
mkdir /boot/efi/EFI/boot
cp /boot/efi/EFI/grub/grubx64.efi /boot/efi/EFI/boot/bootx64.efi

```

This solution worked for an Intel DH87MC motherboard with firmware dated Jan 2014.

### Enable debug messages

**Note:** This change is overwritten when [#Generate the main configuration file](#Generate_the_main_configuration_file).

Add:

```
set pager=1
set debug=all

```

to `grub.cfg`.

### "No suitable mode found" error

If you get this error when booting any menuentry:

```
error: no suitable mode found
Booting however

```

Then you need to initialize GRUB graphical terminal (`gfxterm`) with proper video mode (`gfxmode`) in GRUB. This video mode is passed by GRUB to the linux kernel via 'gfxpayload'. In case of UEFI systems, if the GRUB video mode is not initialized, no kernel boot messages will be shown in the terminal (atleast until KMS kicks in).

Copy `/usr/share/grub/unicode.pf2` to ${GRUB_PREFIX_DIR} (`/boot/grub/` in case of BIOS and UEFI systems). If GRUB UEFI was installed with `--boot-directory=$esp/EFI` set, then the directory is `$esp/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

If `/usr/share/grub/unicode.pf2` does not exist, install [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), create the `unifont.pf2` file and then copy it to `${GRUB_PREFIX_DIR}`:

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Then, in the `grub.cfg` file, add the following lines to enable GRUB to pass the video mode correctly to the kernel, without of which you will only get a black screen (no output) but booting (actually) proceeds successfully without any system hang.

BIOS systems:

```
insmod vbe

```

UEFI systems:

```
insmod efi_gop
insmod efi_uga

```

After that add the following code (common to both BIOS and UEFI):

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

As you can see for gfxterm (graphical terminal) to function properly, `unicode.pf2` font file should exist in `${GRUB_PREFIX_DIR}`.

### msdos-style error message

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding will not be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

This error may occur when you try installing GRUB in a VMware container. Read more about it [here](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). It happens when the first partition starts just after the MBR (block 63), without the usual space of 1 MiB (2048 blocks) before the first partition. Read [#Master Boot Record (MBR) specific instructions](#Master_Boot_Record_.28MBR.29_specific_instructions)

### UEFI

#### Common installation errors

*   If you have a problem when running grub-install with sysfs or procfs and it says you must run `modprobe efivars`, try [Unified Extensible Firmware Interface#Switch to efivarfs](/index.php/Unified_Extensible_Firmware_Interface#Switch_to_efivarfs "Unified Extensible Firmware Interface").
*   Without `--target` or `--directory` option, grub-install cannot determine for which firmware to install. In such cases `grub-install` will print `source_dir does not exist. Please specify --target or --directory`.
*   If after running grub-install you are told your partition does not look like an EFI partition then the partition is most likely not `Fat32`.

#### Drop to rescue shell

If GRUB loads but drops you into the rescue shell with no errors, it may be because of a missing or misplaced `grub.cfg`. This will happen if GRUB UEFI was installed with `--boot-directory` and `grub.cfg` is missing OR if the partition number of the boot partition changed (which is hard-coded into the `grubx64.efi` file).

#### GRUB UEFI not loaded

An example of a working EFI:

 `# efibootmgr -v` 

```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte BIOS(2,0,00)P0: SAMSUNG HD204UI

```

If the screen only goes black for a second and the next boot option is tried afterwards, according to [this post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), moving GRUB to the partition root can help. The boot option has to be deleted and recreated afterwards. The entry for GRUB should look like this then:

```
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### Invalid signature

If trying to boot Windows results in an "invalid signature" error, e.g. after reconfiguring partitions or adding additional hard drives, (re)move GRUB's device configuration and let it reconfigure:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` should now mention all found boot options, including Windows. If it works, remove `/boot/grub/device.map-old`.

### Boot freezes

If booting gets stuck without any error message after GRUB loading the kernel and the initial ramdisk, try removing the `add_efi_memmap` kernel parameter.

### Arch not found from other OS

Some have reported that other distributions have trouble finding Arch Linux automatically with `os-prober`. If this problem arises, it has been reported that detection can be improved with the presence of `/etc/lsb-release`. This file and updating tool is available with the package [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) in the [official repositories](/index.php/Official_repositories "Official repositories").

### Warning when installing in chroot

When installing GRUB on a LVM system in a chroot environment (e.g. during system installation), you may receive warnings like `/run/lvm/lvmetad.socket: connect failed: No such file or directory` or `WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.` This is because `/run` is not available inside the chroot. These warnings will not prevent the system from booting, provided that everything has been done correctly, so you may continue with the installation.

### GRUB loads slowly

GRUB can take a long time to load when disk space is low. Check if you have sufficient free disk space on your `/boot` or `/` partition when you are having problems.

### error: unknown filesystem

GRUB may output `error: unknown filesystem` and refuse to boot for a few reasons. If you are certain that all [UUIDs](/index.php/UUID "UUID") are correct and all filesystems are valid and supported, it may be because your [BIOS Boot Partition](#GUID_Partition_Table_.28GPT.29_specific_instructions) is located outside the first 2TB of the drive [[3]](https://bbs.archlinux.org/viewtopic.php?id=195948). Use a partitioning tool of your choice to ensure this partition is located fully within the first 2TB, then reinstall and reconfigure GRUB.

### grub-reboot not resetting

GRUB seems to be unable to write to root BTRFS partitions [[4]](https://bbs.archlinux.org/viewtopic.php?id=166131). If you use grub-reboot to boot into another entry it will therefore be unable to update its on-disk environment. Either run grub-reboot from the other entry (for example when switching between various distributions) or consider a different file system. You can reset a "sticky" entry by executing `grub-editenv create` and setting `GRUB_DEFAULT=0` in your `/etc/default/grub` (don't forget `grub-mkconfig`).

### Old BTRFS prevents installation

If a drive is formatted with BTRFS without creating a partition table (eg. /dev/sdx), then later has partition table written to, there are parts of the BTRFS format that persist. Most utilities and OS's do not see this, but GRUB will refuse to install, even with --force

```
# grub-install: warning: Attempting to install GRUB to a disk with multiple partition labels. This is not supported yet..
# grub-install: error: filesystem `btrfs' doesn't support blocklists.

```

You can zero the drive, but the easy solution that leaves your data alone is to erase the BTRFS superblock with `wipefs -o 0x10040 /dev/sdx`

## See also

*   Official GRUB Manual - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
*   Ubuntu wiki page for GRUB - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
*   GRUB wiki page describing steps to compile for UEFI systems - [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
*   Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html) - quite complete description of how to configure GRUB

Retrieved from "[https://wiki.archlinux.org/index.php?title=GRUB&oldid=419482](https://wiki.archlinux.org/index.php?title=GRUB&oldid=419482)"
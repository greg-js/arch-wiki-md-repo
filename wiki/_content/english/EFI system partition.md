Related articles

*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [Boot loader](/index.php/Boot_loader "Boot loader")

The [EFI system partition](https://en.wikipedia.org/wiki/EFI_system_partition "wikipedia:EFI system partition") (also called ESP) is an OS independent partition that acts as the storage place for the EFI bootloaders, applications and drivers to be launched by the UEFI firmware. It is mandatory for UEFI boot.

The UEFI specification mandates support for the FAT12, FAT16, and FAT32 file systems (see [UEFI specification version 2.8, section 13.3.1.1](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1019485)), but any conformant vendor can optionally add support for additional file systems; for example, the firmware in Apple [Macs](/index.php/Mac "Mac") supports the HFS+ file system.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Check for an existing partition](#Check_for_an_existing_partition)
*   [2 Create the partition](#Create_the_partition)
    *   [2.1 GPT partitioned disks](#GPT_partitioned_disks)
    *   [2.2 MBR partitioned disks](#MBR_partitioned_disks)
*   [3 Format the partition](#Format_the_partition)
*   [4 Mount the partition](#Mount_the_partition)
    *   [4.1 Typical mount points](#Typical_mount_points)
    *   [4.2 Alternative mount points](#Alternative_mount_points)
        *   [4.2.1 Using bind mount](#Using_bind_mount)
        *   [4.2.2 Using systemd](#Using_systemd)
        *   [4.2.3 Using filesystem events](#Using_filesystem_events)
        *   [4.2.4 Using mkinitcpio hook](#Using_mkinitcpio_hook)
        *   [4.2.5 Using mkinitcpio preset](#Using_mkinitcpio_preset)
            *   [4.2.5.1 Replacing the above mkinitcpio hook](#Replacing_the_above_mkinitcpio_hook)
            *   [4.2.5.2 Another example](#Another_example)
        *   [4.2.6 Using pacman hook](#Using_pacman_hook)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 ESP on software RAID1](#ESP_on_software_RAID1)
*   [6 See also](#See_also)

## Check for an existing partition

If you are installing Arch Linux on an UEFI-capable computer with an installed operating system, like [Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") 10 for example, it is very likely that you already have an EFI system partition.

To find out the disk partition scheme and the system partition, use [fdisk](/index.php/Fdisk "Fdisk") as root on the disk you want to boot from:

```
# fdisk -l /dev/sd*x*

```

The command returns:

*   The disk's partition table: it indicates `Disklabel type: gpt` if the partition table is [GPT](/index.php/GPT "GPT") or `Disklabel type: dos` if it is [MBR](/index.php/MBR "MBR").
*   The list of partitions on the disk: Look for the EFI system partition in the list, it is a small (usually about 100–550 MiB) partition with a type `EFI System` or `EFI (FAT-12/16/32)`. To confirm this is the ESP, [mount](/index.php/Mount "Mount") it and check whether it contains a directory named `EFI`, if it does this is definitely the ESP.

**Tip:** To find out whether it is a FAT12, FAT16 or FAT32 file system, use `minfo` from [mtools](https://www.archlinux.org/packages/?name=mtools).
```
# minfo -i /dev/sd*xY* :: | grep 'disk type'

```

**Warning:** When dual-booting, avoid reformatting the ESP, as it may contain files required to boot other operating systems.

If you found an existing EFI system partition, simply proceed to [#Mount the partition](#Mount_the_partition). If you did not find one, you will need to create it, proceed to [#Create the partition](#Create_the_partition).

## Create the partition

The following two sections show how to create an EFI system partition (ESP).

**Warning:** The EFI system partition must be a physical partition in the main partition table of the disk, not under LVM or software RAID etc.

**Note:** It is recommended to use [GPT](/index.php/GPT "GPT") since some firmwares might not support UEFI/MBR booting due to it not being supported by [Windows Setup](/index.php/Dual_boot_with_Windows "Dual boot with Windows"). See also [Partitioning#Choosing between GPT and MBR](/index.php/Partitioning#Choosing_between_GPT_and_MBR "Partitioning") for the advantages of GPT in general.

To provide adequate space for storing boot loaders and other files required for booting, and to prevent interoperability issues with other operating systems[[1]](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions#diskpartitionrules)[[2]](https://superuser.com/questions/1310927/what-is-the-absolute-minimum-size-a-uefi-partition-can-be/1310938) the partition should be at least 260 MiB. For early and/or buggy UEFI implementations the size of at least 512 MiB might be needed.[[3]](https://www.rodsbooks.com/efi-bootloaders/principles.html)

### GPT partitioned disks

EFI system partition on a [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") is identified by the [partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") `C12A7328-F81F-11D2-BA4B-00A0C93EC93B`.

**Choose one** of the following methods to create an ESP for a GPT partitioned disk:

*   [fdisk](/index.php/Fdisk "Fdisk"): Create a partition with partition type `EFI System`.
*   [gdisk](/index.php/Gdisk "Gdisk"): Create a partition with partition type `EF00`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Create a partition with `fat32` as the file system type and set the `esp` flag on it.

Proceed to [#Format the partition](#Format_the_partition) section below.

### MBR partitioned disks

EFI system partition on a [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") partition table is identified by the [partition type ID](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") `EF`.

**Choose one** of the following methods to create an ESP for a MBR partitioned disk:

*   [fdisk](/index.php/Fdisk "Fdisk"): Create a primary partition with partition type `EFI (FAT-12/16/32)`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Create a primary partition with `fat32` as the file system type and set the `esp` flag on it.

Proceed to [#Format the partition](#Format_the_partition) section below.

## Format the partition

The UEFI specification mandates support for the FAT12, FAT16, and FAT32 file systems[[4]](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1019485). To prevent potential issues with other operating systems and also since the UEFI specification only mandates supporting FAT16 and FAT12 on removable media[[5]](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1345080), it is recommended to use FAT32.

After creating the partition, [format](/index.php/Format "Format") it as [FAT32](/index.php/FAT32 "FAT32"). To use the `mkfs.fat` utility, [install](/index.php/Install "Install") [dosfstools](https://www.archlinux.org/packages/?name=dosfstools).

```
# mkfs.fat -F32 /dev/sd*xY*

```

If you get the message `WARNING: Not enough clusters for a 32 bit FAT!`, reduce cluster size with `mkfs.fat -s2 -F32 ...` or `-s1`; otherwise the partition may be unreadable by UEFI. See [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) for supported cluster sizes.

## Mount the partition

The kernels, initramfs files, and, in most cases, the processor's [microcode](/index.php/Microcode "Microcode"), need to be accessible by the [boot loader](/index.php/Boot_loader "Boot loader") or UEFI itself to successfully boot the system. Thus if you want to keep the setup simple, your boot loader choice limits the available mount points for EFI system partition.

### Typical mount points

The simplest scenarios for mounting EFI system partition are:

*   [mount](/index.php/Mount "Mount") ESP to `/efi` and use a [boot loader](/index.php/Boot_loader "Boot loader") which is capable of accessing the kernel(s) and initramfs image(s) that are stored elsewhere (typically [/boot](/index.php/Partitioning#/boot "Partitioning")). See [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process") for more information on boot loader requirements and capabilities.
*   [mount](/index.php/Mount "Mount") ESP to `/boot`. This is the preferred method when directly booting a [EFISTUB](/index.php/EFISTUB "EFISTUB") kernel from UEFI.

**Tip:**

*   `/efi` is a replacement[[6]](https://github.com/systemd/systemd/pull/3757#issuecomment-234290236) for the previously popular (and possibly still used by other Linux distributions) ESP mountpoint `/boot/efi`.
*   The `/efi` directory is not available by default, you will need to first create it with [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) before mounting the ESP to it.

### Alternative mount points

If you do not use one of the simple methods from [#Mount the partition](#Mount_the_partition), you will need to copy your boot files to ESP (referred to hereafter as `*esp*`).

```
# mkdir -p *esp*/EFI/arch
# cp -a /boot/vmlinuz-linux *esp*/EFI/arch/
# cp -a /boot/initramfs-linux.img *esp*/EFI/arch/
# cp -a /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Note:** You may also need to copy the [Microcode](/index.php/Microcode "Microcode") to the boot-entry location.

Furthermore, you will need to keep the files on the ESP up-to-date with later kernel updates. Failure to do so could result in an unbootable system. The following sections discuss several mechanisms for automating it.

**Note:** If ESP is not mounted to `/boot`, make sure to not rely on the [systemd automount mechanism](/index.php/Fstab#Automount_with_systemd "Fstab") (including that of [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8)). Always have it mounted manually prior to the any system or kernel update, otherwise you may not be able to mount it after the update, locking you in the currently running kernel with no ability to update the copy of kernel on ESP.

Alternatively [preload the required kernel modules on boot](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module"), e.g.:

 `/etc/modules-load.d/vfat.conf` 
```
vfat
nls_cp437
nls_iso8859-1

```

#### Using bind mount

Instead of mounting the ESP itself to `/boot`, you can mount a directory of the ESP to `/boot` using a bind [mount](/index.php/Mount "Mount") (see [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)). This allows [pacman](/index.php/Pacman "Pacman") to update the kernel directly while keeping the ESP organized to your liking.

**Note:**

*   This requires a [kernel](/index.php/FAT#Kernel_configuration "FAT") and [bootloader](/index.php/Bootloader "Bootloader") compatible with FAT32\. This is not an issue for a regular Arch install, but could be problematic for other distributions (namely those that require symlinks in `/boot/`). See the forum post [here](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).
*   You *must* use the `root=` [kernel parameter](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") in order to boot using this method.

Just like in [#Alternative mount points](#Alternative_mount_points), copy all boot files to a directory on your ESP, but mount the ESP **outside** `/boot`. Then bind mount the directory:

```
# mount --bind *esp*/EFI/arch /boot

```

After verifying success, edit your [Fstab](/index.php/Fstab "Fstab") to make the changes persistent:

 `/etc/fstab` 
```
*esp*/EFI/arch /boot none defaults,bind 0 0

```

#### Using systemd

[Systemd](/index.php/Systemd "Systemd") features event triggered tasks. In this particular case, the ability to detect a change in path is used to sync the EFISTUB kernel and initramfs files when they are updated in `/boot/`. The file watched for changes is `initramfs-linux-fallback.img` since this is the last file built by mkinitcpio, to make sure all files have been built before starting the copy. The *systemd* path and service files to be created are:

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI system partition

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target
WantedBy=system-update.target
```
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI system partition

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/
```

Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `efistub-update.path`.

**Tip:** For [Secure Boot](/index.php/Secure_Boot "Secure Boot") with your own keys, you can set up the service to also sign the image using [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools): `ExecStart=/usr/bin/sbsign --key */path/to/db.key* --cert */path/to/db.crt* --output *esp*/EFI/arch/vmlinuz-linux /boot/vmlinuz-linux` 

#### Using filesystem events

[Filesystem events](/index.php/Autostarting#On_filesystem_events "Autostarting") can be used to run a script syncing the EFISTUB Kernel after kernel updates. An example with [incron](/index.php/Incron "Incron") follows.

 `/usr/local/bin/efistub-update` 
```
#!/bin/sh
cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Note:** The first parameter `/boot/initramfs-linux-fallback.img` is the file to watch. The second parameter `IN_CLOSE_WRITE` is the action to watch for. The third parameter `/usr/local/bin/efistub-update` is the script to execute.
 `/etc/incron.d/efistub-update.conf` 
```
/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update

```

In order to use this method, [enable](/index.php/Enable "Enable") the `incrond.service`.

#### Using mkinitcpio hook

Mkinitcpio can generate a hook that does not need a system level daemon to function. It spawns a background process which waits for the generation of `vmlinuz`, `initramfs-linux.img`, and `initramfs-linux-fallback.img` before copying the files.

Add `efistub-update` to the list of hooks in `/etc/mkinitcpio.conf`.

 `/etc/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/usr/local/bin/efistub-copy $$ &
}

help() {
	cat <<HELPEOF
This hook waits for mkinitcpio to finish and copies the finished ramdisk and kernel to the ESP
HELPEOF
}

```
 `/usr/local/bin/efistub-copy` 
```
#!/usr/bin/env bash

if [[ $1 -gt 0 ]]
then
	while [ -e /proc/$1 ]
	do
		sleep .5
	done
fi

rsync -a /boot/ *esp*/

echo "Synced /boot with ESP"

```

#### Using mkinitcpio preset

As the presets in `/etc/mkinitcpio.d/` support shell scripting, the kernel and initramfs can be copied by just editing the presets.

##### Replacing the above mkinitcpio hook

Edit the file `/etc/mkinitcpio.d/linux.preset`:

 `/etc/mkinitcpio.d/linux.preset` 
```
# mkinitcpio preset file for the 'linux' package

# Directory to copy the kernel, the initramfs...
ESP_DIR="''esp''/EFI/arch"

ALL_config="/etc/mkinitcpio.conf"
ALL_kver="${ESP_DIR}/vmlinuz-linux"
cp -af /boot/vmlinuz-linux "${ESP_DIR}/"
[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "${ESP_DIR}/"
[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "${ESP_DIR}/"

PRESETS=('default' 'fallback')

#default_config="/etc/mkinitcpio.conf"
default_image="${ESP_DIR}/initramfs-linux.img"
default_options="-A esp-update-linux"

#fallback_config="/etc/mkinitcpio.conf"
fallback_image="${ESP_DIR}/initramfs-linux-fallback.img"
fallback_options="-S autodetect"

```

To test that, just run:

```
# rm /boot/initramfs-linux-fallback.img
# rm /boot/initramfs-linux.img
# mkinitcpio -p linux

```

##### Another example

 `/etc/mkinitcpio.d/0.preset` 
```
ESP_DIR="*esp*/EFI/arch"
cp -af "/boot/vmlinuz-linux${suffix}" "$ESP_DIR/"
ALL_config="/etc/mkinitcpio.conf"
ALL_kver="$ESP_DIR/vmlinuz-linux${suffix}"
PRESETS=('default')
default_config="/etc/mkinitcpio.conf"
default_image="$ESP_DIR/initramfs-linux${suffix}.img"
```
 `/etc/mkinitcpio.d/linux.preset` 
```
source /etc/mkinitcpio.d/0.preset

```
 `/etc/mkinitcpio.d/linux-zen.preset` 
```
suffix='-zen'
source /etc/mkinitcpio.d/0.preset
```

#### Using pacman hook

A last option relies on the [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") that are run at the end of the transaction.

The first file is a hook that monitors the relevant files, and it is run if they were modified in the former transaction.

 `/etc/pacman.d/hooks/999-kernel-efi-copy.hook` 
```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/lib/modules/*/vmlinuz
Target = usr/lib/initcpio/*
Target = boot/*-ucode.img

[Action]
Description = Copying linux and initramfs to EFI directory...
When = PostTransaction
Exec = /usr/local/bin/kernel-efi-copy.sh

```

The second file is the script itself. Create the file and make it [executable](/index.php/Executable "Executable"):

 `/usr/local/bin/kernel-efi-copy.sh` 
```
#!/usr/bin/env bash
#
# Copy kernel and initramfs images to EFI directory
#

ESP_DIR="*esp*/EFI/arch"

for file in /boot/vmlinuz*
do
        cp -af "$file" "$ESP_DIR/$(basename "$file").efi"
        [[ $? -ne 0 ]] && exit 1
done

for file in /boot/initramfs*
do
        cp -af "$file" "$ESP_DIR/"
        [[ $? -ne 0 ]] && exit 1
done

[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "$ESP_DIR/"
[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "$ESP_DIR/"

exit 0

```

## Troubleshooting

### ESP on software RAID1

It is possible to make the ESP part of a RAID1 array, but doing so brings the risk of data corruption, and further considerations need to be taken when creating the ESP. See [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) and [[8]](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) for details.

See [UEFI booting and RAID1](https://outflux.net/blog/archives/2018/04/19/uefi-booting-and-raid1/) for a in-depth guide.

The key part is to use `--metadata 1.0` in order to keep the RAID metadata at the end of the partition, otherwise the firmware will not be able to access it:

```
# mdadm --create --verbose --level=1 **--metadata=1.0** --raid-devices=2 /dev/md/ESP /dev/sda*X* /dev/sdb*Y*

```

## See also

*   [The EFI system partition and the default boot behavior](https://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)
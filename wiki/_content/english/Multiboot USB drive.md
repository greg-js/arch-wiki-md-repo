Related articles

*   [GRUB](/index.php/GRUB "GRUB")
*   [Syslinux](/index.php/Syslinux "Syslinux")
*   [Archiso](/index.php/Archiso "Archiso")

A multiboot USB flash drive allows booting multiple ISO files from a single device. The ISO files can be copied to the device and booted directly without unpacking them first. There are multiple methods available, but they may not work for all ISO images.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Using GRUB and loopback devices](#Using_GRUB_and_loopback_devices)
    *   [1.1 Preparation](#Preparation)
    *   [1.2 Installing GRUB](#Installing_GRUB)
        *   [1.2.1 Simple installation](#Simple_installation)
        *   [1.2.2 Hybrid UEFI GPT + BIOS GPT/MBR boot](#Hybrid_UEFI_GPT_+_BIOS_GPT/MBR_boot)
    *   [1.3 Configuring GRUB](#Configuring_GRUB)
        *   [1.3.1 Using a template](#Using_a_template)
        *   [1.3.2 Manual configuration](#Manual_configuration)
    *   [1.4 Boot entries](#Boot_entries)
        *   [1.4.1 Arch Linux monthly release](#Arch_Linux_monthly_release)
        *   [1.4.2 archboot](#archboot)
*   [2 Using Syslinux and memdisk](#Using_Syslinux_and_memdisk)
    *   [2.1 Preparation](#Preparation_2)
    *   [2.2 Install the memdisk module](#Install_the_memdisk_module)
    *   [2.3 Configuration](#Configuration)
    *   [2.4 Caveat for 32-bit systems](#Caveat_for_32-bit_systems)
*   [3 Automated tools](#Automated_tools)
*   [4 See also](#See_also)

## Using GRUB and loopback devices

Advantages:

*   only a single partition required
*   all ISO files are found in one directory
*   adding and removing ISO files is simple

Disadvantages:

*   not all ISO images are compatible
*   the original boot menu for the ISO file is not shown
*   it can be difficult to find a working boot entry

### Preparation

Create at least one partition and a filesystem supported by [GRUB](/index.php/GRUB "GRUB") on the USB drive. See [Partitioning](/index.php/Partitioning "Partitioning") and [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems"). Choose the size based on the total size of the ISO files that you want to store on the drive, and plan for extra space for the bootloader.

### Installing GRUB

#### Simple installation

Mount the filesystem located on the USB drive:

```
# mount /dev/sdXY /mnt

```

Create the directory /boot:

```
# mkdir /mnt/boot

```

Install GRUB on the USB drive:

```
# grub-install --target=i386-pc --recheck --boot-directory=/mnt/boot /dev/sdX

```

In case you want to boot ISOs in UEFI mode, you have to install grub for the UEFI target:

```
# grub-install --target=x86_64-efi --removable --boot-directory=/mnt/boot --efi-directory=/mnt

```

For UEFI, the partition has to be the first one in an MBR partition table and formatted with FAT32.

#### Hybrid UEFI GPT + BIOS GPT/MBR boot

This configuration is useful for creating a universal USB key, bootable everywhere. First of all you must create a [GPT](/index.php/GPT "GPT") partition table on your device. You need at least 3 partitions:

1.  A BIOS boot partition (gdisk type code `EF02`). This partition must be 1 MiB in size
2.  An EFI System partition (gdisk type code `EF00` with a [FAT32 filesystem](/index.php/EFI_system_partition#Format_the_partition "EFI system partition")). This partition can be as small as 50 MiB.
3.  Your data partition (use a filesystem supported by [GRUB](/index.php/GRUB "GRUB")). This partition can take up the rest of the space of your drive.

Next you must create a hybrid MBR partition table, as setting the boot flag on the protective MBR partition might not be enough.

Hybrid MBR partition table creation example using [gdisk](/index.php/Gdisk "Gdisk"):

```
# gdisk /dev/sdX

Command (? for help): r
Recovery/transformation command (? for help): h

WARNING! Hybrid MBRs are flaky and dangerous! If you decide not to use one,
just hit the Enter key at the below prompt and your MBR partition table will
be untouched.

Type from one to three GPT partition numbers, separated by spaces, to be added to the hybrid MBR, in sequence: 1 2 3
Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N): N

Creating entry for GPT partition #1 (MBR partition #1)
Enter an MBR hex code (default EF): 
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #2 (MBR partition #2)
Enter an MBR hex code (default EF): 
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #3 (MBR partition #3)
Enter an MBR hex code (default 83): 
Set the bootable flag? (Y/N): Y

Recovery/transformation command (? for help): x
Expert command (? for help): h
Expert command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): Y

```

Do not forget to format the partitions :

```
# mkfs.fat -F32 /dev/sdX2
# mkfs.ext4 /dev/sdX3

```

You can now install GRUB to support both EFI + GPT and BIOS + GPT/MBR. The GRUB configuration (--boot-directory) can be kept in the same place.

First, you need to mount the EFI system partition and the data partition of your USB drive.

An example of this would be as follows:

```
# mount /dev/sdX3 /mnt
# mkdir -p /mnt/boot/EFI
# mount /dev/sdX2 /mnt/boot/EFI

```

Then, you can install GRUB for UEFI with:

In most cases `EFI_MOUNTPOINT` will correspond to the `/mnt/boot/EFI` subdirectory on your mounted USB disk.

```
# grub-install --target=x86_64-efi --recheck --removable --efi-directory=/*EFI_MOUNTPOINT* --boot-directory=/*DATA_MOUNTPOINT*/boot

```

And for BIOS with:

```
# grub-install --target=i386-pc --recheck --boot-directory=/*DATA_MOUNTPOINT*/boot /dev/sd*X*

```

As an additional fallback, you can also install GRUB on your MBR-bootable data partition:

```
# grub-install --target=i386-pc --recheck --boot-directory=/*DATA_MOUNTPOINT*/boot /dev/*sdX3*

```

### Configuring GRUB

#### Using a template

There are some git projects which provide some pre-existing GRUB configuration files, and a nice generic `grub.cfg` which can be used to load the other boot entries on demand, showing them only if the specified ISO files - or folders containing them - are present on the drive.

Multiboot USB: [https://github.com/aguslr/multibootusb](https://github.com/aguslr/multibootusb)

GLIM (GRUB2 Live ISO Multiboot): [https://github.com/thias/glim](https://github.com/thias/glim)

#### Manual configuration

For the purpose of multiboot USB drive it is easier to edit `grub.cfg` by hand instead of generating it. Alternatively, make the following changes in `/etc/grub.d/40_custom` or `/mnt/boot/grub/custom.cfg` and generate `/mnt/boot/grub/grub.cfg` using [grub-mkconfig](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

As it is recommend to use a [persistent name](/index.php/Persistent_block_device_naming "Persistent block device naming") instead of `/dev/sd*xY*` to identify the partition on the USB drive where the image files are located, define a variable for convenience to hold the value. If the ISO images are on the same partition as GRUB, use the following to read the UUID at boot time:

 `/mnt/boot/grub/grub.cfg` 
```
# path to the partition holding ISO images (using UUID)
probe -u $root --set=rootuuid
set imgdevpath="/dev/disk/by-uuid/$rootuuid"
```

Or specify the UUID explicitly:

 `/mnt/boot/grub/grub.cfg` 
```
# path to the partition holding ISO images (using UUID)
set imgdevpath="/dev/disk/by-uuid/*UUID_value*"
```

Alternatively, use the device label instead of UUID:

 `/mnt/boot/grub/grub.cfg` 
```
# path to the partition holding ISO images (using labels)
set imgdevpath="/dev/disk/by-label/*label_value*"
```

The necessary UUID or label can be found using `lsblk -f`. Do not use the same label as the Arch ISO for the USB device, otherwise the boot process will fail.

To complete the configuration, a boot entry for each ISO image has to be added below this header, see the next section for examples.

### Boot entries

It is assumed that the ISO images are stored in the `boot/iso/` directory on the same filesystem where GRUB is installed. Otherwise it would be necessary to prefix the path to ISO file with device identification when using the `loopback` command, for example `loopback loop **(hd1,2)**$isofile`. As this identification of devices is not [persistent](/index.php/Persistent_block_device_naming "Persistent block device naming"), it is not used in the examples in this section.

One can use persistent block device naming like so. Replace the UUID according to your ISO filesystem UUID.

```
# define globally (i.e outside any menuentry)
insmod search_fs_uuid
search --no-floppy --set=**isopart** --fs-uuid *123-456*
# later use inside each menuentry instead
loopback loop **($isopart)**$isofile
```

**Tip:** For a list of kernel parameters, see [kernel-parameters.rst](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.rst) and [kernel-parameters.txt](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt) (still incomplete). For more examples of boot entries, see the [GRUB upstream documentation](https://www.gnu.org/software/grub/manual/grub.html#Multi_002dboot-manual-config) or the documentation for the distribution you wish to boot.

#### Arch Linux monthly release

Also see [archiso](/index.php/Archiso "Archiso").

```
menuentry '[loopback]archlinux-2017.10.01-x86_64.iso' {
	set isofile='/boot/iso/archlinux-2017.10.01-x86_64.iso'
	loopback loop $isofile
	linux (loop)/arch/boot/x86_64/vmlinuz img_dev=$imgdevpath img_loop=$isofile earlymodules=loop
	initrd (loop)/arch/boot/intel_ucode.img (loop)/arch/boot/amd_ucode.img (loop)/arch/boot/x86_64/archiso.img
}
```

See [README.bootparams](https://git.archlinux.org/archiso.git/tree/docs/README.bootparams) for archiso options supported in kernel command line.

#### archboot

Also see [archboot](/index.php/Archboot "Archboot").

```
menuentry '[loopback]archlinux-2014.11-1-archboot' {
	set isofile='/boot/iso/archlinux-2014.11-1-archboot.iso'
	loopback loop $isofile
	linux (loop)/boot/vmlinuz_**x86_64** iso_loop_dev=$imgdevpath iso_loop_path=$isofile
	initrd (loop)/boot/initramfs_**x86_64**.img
}
```

## Using Syslinux and memdisk

Using the [memdisk](https://wiki.syslinux.org/wiki/index.php/MEMDISK) module, the ISO image is loaded into memory, and its bootloader is loaded. Make sure that the system that will boot this USB drive has sufficient amount of memory for the image file and running operating system.

### Preparation

Make sure that the USB drive is properly [partitioned](/index.php/Partitioning "Partitioning") and that there is a partition with [file system](/index.php/File_system "File system") supported by Syslinux, for example fat32 or ext4\. Then install Syslinux to this partition, see [Syslinux#Installation on BIOS](/index.php/Syslinux#Installation_on_BIOS "Syslinux").

### Install the memdisk module

The memdisk module was not installed during Syslinux installation, it has to be installed manually. Mount the partition where Syslinux is installed to `/mnt/` and copy the memdisk module to the same directory where Syslinux is installed:

```
# cp /usr/lib/syslinux/bios/memdisk /mnt/boot/syslinux/

```

### Configuration

After copying the ISO files on the USB drive, edit the [Syslinux configuration file](/index.php/Syslinux#Configuration "Syslinux") and create menu entries for the ISO images. The basic entry looks like this:

 `boot/syslinux/syslinux.cfg` 
```
LABEL *some_label*
    LINUX memdisk
    INITRD */path/to/image.iso*
    APPEND iso

```

See [memdisk on Syslinux wiki](https://wiki.syslinux.org/wiki/index.php/MEMDISK) for more configuration options.

### Caveat for 32-bit systems

When booting a 32-bit system from an image larger than 128MiB, it is necessary to increase the maximum memory usage of vmalloc. This is done by adding `vmalloc=*value*M` to the kernel parameters, where `*value*` is larger than the size of the ISO image in MiB.[[1]](https://wiki.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

For example when booting the 32-bit system from the [Arch installation ISO](https://www.archlinux.org/download/), press the `Tab` key over the `Boot Arch Linux (i686)` entry and add `vmalloc=768M` at the end. Skipping this step will result in the following error during boot:

```
modprobe: ERROR: could not insert 'phram': Input/output error

```

## Automated tools

*   **liveusb-builder** — A script suite to create multiboot USB stick for GNU/Linux distributions

	[https://github.com/mytbk/liveusb-builder](https://github.com/mytbk/liveusb-builder) || [liveusb-builder-git](https://aur.archlinux.org/packages/liveusb-builder-git/)

*   **MultiSystem** — A graphical tool that allows to install, manage, and remove multiple ISO images on a USB device.

	[http://liveusb.info/dotclear/](http://liveusb.info/dotclear/) || [multisystem](https://aur.archlinux.org/packages/multisystem/)

*   **MultiBootUSB** — A cross platform Python software with CLI and GUI interfaces which allows you to install and remove multiple live Linux images on a USB stick.

	[http://multibootusb.org/](http://multibootusb.org/) || [multibootusb](https://aur.archlinux.org/packages/multibootusb/)

## See also

*   GRUB:
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot/Examples](https://help.ubuntu.com/community/Grub2/ISOBoot/Examples)
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot](https://help.ubuntu.com/community/Grub2/ISOBoot)
    *   [GRUB Live ISO Multiboot](https://github.com/thias/glim) - GRUB configurations for booting ISO images
*   Syslinux:
    *   [Boot an ISO image](https://wiki.syslinux.org/wiki/index.php?title=Boot_an_Iso_image)
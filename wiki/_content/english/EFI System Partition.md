The [EFI System Partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition") (also called ESP or EFISYS) is a FAT32 formatted physical partition (in the main partition table of the disk, not under LVM or software RAID etc.) from where the [UEFI](/index.php/UEFI "UEFI") firmware launches the UEFI bootloader and application.

It is an OS independent partition that acts as the storage place for the EFI bootloaders and applications to be launched by the EFI firmware. It is mandatory for UEFI boot.

**Warning:** If [dual-booting](/index.php/Dual_boot_with_Windows "Dual boot with Windows") with an existing installation of Windows on a UEFI/GPT system, avoid reformatting the UEFI partition, as this includes the Windows *.efi* file required to boot it. In other words, use the existing partition as is and simply [#Mount the partition](#Mount_the_partition).

## Contents

*   [1 Create the partition](#Create_the_partition)
    *   [1.1 GPT partitioned disks](#GPT_partitioned_disks)
    *   [1.2 MBR partitioned disks](#MBR_partitioned_disks)
*   [2 Format the partition](#Format_the_partition)
*   [3 Mount the partition](#Mount_the_partition)
*   [4 Known issues](#Known_issues)
    *   [4.1 ESP on RAID](#ESP_on_RAID)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Using bind mount](#Using_bind_mount)
*   [6 See also](#See_also)

## Create the partition

The following two sections show how to create an EFI System Partition (ESP).

**Note:** It is recommended to use [GPT](/index.php/GPT "GPT") for UEFI boot, because some UEFI firmwares do not allow UEFI-MBR boot.

It is recommended to keep ESP size at 512 MiB although smaller/larger sizes are fine. [[1]](http://www.rodsbooks.com/efi-bootloaders/principles.html)

According to a Microsoft note[[2]](http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules), the minimum size for the EFI System Partition (ESP) would be 100 MB, though this is not stated in the UEFI Specification. Note that for Advanced Format 4K Native drives (4-KB-per-sector) drives, the size is at least 260 MB, because it is the minimum partition size of FAT32 drives (calculated as sector size (4KB) x 65527 = 256 MB), due to a limitation of the FAT32 file format.

### GPT partitioned disks

**Choose one** of the following methods to create an ESP for a GPT partitioned disk:

*   [fdisk/gdisk](/index.php/Fdisk "Fdisk"): Create a partition with partition type EFI System (`EFI System` in *fdisk* or `EF00` in *gdisk*). Proceed to [#Format the partition](#Format_the_partition).
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Create a FAT32 partition and in Parted set/activate the `boot` flag (not `legacy_boot` flag) on that partition. Proceed to [#Mount the partition](#Mount_the_partition).

### MBR partitioned disks

Create a partition with partition type *EFI System* using fdisk. Proceed to [#Format the partition](#Format_the_partition).

## Format the partition

After creating the ESP, you **must** [format](/index.php/File_systems#Formatting "File systems") it as FAT32:

```
# mkfs.fat -F32 /dev/sd*xY*

```

If you used GNU Parted above, it should already be formatted.

If you get the message `WARNING: Not enough clusters for a 32 bit FAT!`, reduce cluster size with `mkfs.fat -s2 -F32 ...` or `-s1`; otherwise the partition may be unreadable by UEFI.

## Mount the partition

In case of [EFISTUB](/index.php/EFISTUB "EFISTUB"), the kernels and initramfs files should be stored in the EFI System Partition. For sake of simplicity, you can also use the ESP as the `/boot` partition itself instead of a separate `/boot` partition, for EFISTUB booting. In other words, after creating and formatting the EFI System Partition as instructed above, simply [mount](/index.php/Mount "Mount") it at `/boot`.

Also see [#Using bind mount](#Using_bind_mount).

## Known issues

### ESP on RAID

It is possible to make the ESP part of a RAID1 array, but doing so brings the risk of data corruption, and further considerations need to be taken when creating the ESP. See [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) and [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) for details.

## Tips and tricks

### Using bind mount

Instead of mounting the ESP itself to `/boot`, you can mount a directory of the ESP to `/boot` using a bind mount (see [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html)). This allows pacman to update the kernel directly while keeping the ESP organized to your liking. If it works for you, this method is much simpler than the other approaches which copy files.

**Note:** This requires a kernel and bootloader compatible with FAT32\. This is not an issue for a regular Arch install, but could be problematic for other distributions (namely those that require symlinks in `/boot`). Forum post [here](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).

As [EFISTUB#Alternative ESP Mount Points](/index.php/EFISTUB#Alternative_ESP_Mount_Points "EFISTUB"), copy all boot files to a directory on your ESP, but mount the ESP **outside** `/boot` (e.g. `/esp`). Then bind mount the directory:

```
# mount --bind /esp/EFI/arch/ /boot

```

If your files appear in `/boot` as desired, edit your [Fstab](/index.php/Fstab "Fstab") to make it persistent:

 `/etc/fstab` 
```
/esp/EFI/arch /boot none defaults,bind 0 0

```

**Warning:** You *must* use the `root=*system_root*` [kernel parameter](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") in order to boot using this method.

## See also

*   [The EFI System Partition and the Default Boot Behavior](http://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)
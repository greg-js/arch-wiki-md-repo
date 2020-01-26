Related articles

*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")

From [Wikipedia](https://en.wikipedia.org/wiki/Device_file "wikipedia:Device file"):

	In Unix-like operating systems, a device file or special file is an interface to a device driver that appears in a file system as if it were an ordinary file.

On Linux they are in the `/dev` directory, according to the [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard").

On Arch Linux the device nodes are managed by [udev](/index.php/Udev "Udev").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Block devices](#Block_devices)
    *   [1.1 Block device names](#Block_device_names)
        *   [1.1.1 SCSI](#SCSI)
        *   [1.1.2 NVMe](#NVMe)
        *   [1.1.3 MMC](#MMC)
        *   [1.1.4 SCSI optical disc drive](#SCSI_optical_disc_drive)
    *   [1.2 Utilities](#Utilities)
        *   [1.2.1 lsblk](#lsblk)
        *   [1.2.2 wipefs](#wipefs)
*   [2 Pseudo-devices](#Pseudo-devices)
*   [3 See also](#See_also)

## Block devices

[Block devices](https://en.wikipedia.org/wiki/Device_file#Block_devices "wikipedia:Device file") provide buffered access to hardware devices and allow reading and writing blocks of any size and alignment.

### Block device names

The beginning of the device name specifies the kernel's used driver subsystem to operate the block device.

**Warning:** Kernel name descriptors for block devices are not [persistent](/index.php/Persistent_block_device_naming "Persistent block device naming") and can change each boot, they should not be used in configuration files.

#### SCSI

Storage devices, like hard disks, [SSDs](/index.php/SSD "SSD") and flash drives, that support the [SCSI command](https://en.wikipedia.org/wiki/SCSI_command "wikipedia:SCSI command") ([SCSI](https://en.wikipedia.org/wiki/SCSI "wikipedia:SCSI"), [SAS](https://en.wikipedia.org/wiki/Serial_Attached_SCSI "wikipedia:Serial Attached SCSI"), [UASP](https://en.wikipedia.org/wiki/USB_Attached_SCSI "wikipedia:USB Attached SCSI")), ATA ([PATA](https://en.wikipedia.org/wiki/Parallel_ATA "wikipedia:Parallel ATA"), [SATA](https://en.wikipedia.org/wiki/Serial_ATA "wikipedia:Serial ATA")) or [USB mass storage](https://en.wikipedia.org/wiki/USB_mass_storage_device_class "wikipedia:USB mass storage device class") connection are handled by the kernel's SCSI driver subsystem. They all share the same naming scheme.

The name of these devices starts with `sd`. It is then followed by a lower-case letter starting from `a` for the first discovered device (`sda`), `b` for the second discovered device (`sdb`), and so on. Existing [partitions](/index.php/Partition "Partition") on each device will be listed with the number that is assigned to them in the partition table, e.g. `sda1` for the partition `1`, `sda2` for partition `2`, and so on.

Summary:

*   `/dev/sda` - device `a`, the first discovered device.
*   `/dev/sda1` - partition `1` on device `a`.
*   `/dev/sde` - device `e`, the fifth discovered device.
*   `/dev/sde7` - partition `7` on device `e`.

#### NVMe

The name of storage devices, like [SSDs](/index.php/SSD "SSD"), that are attached via [NVM Express](/index.php/NVM_Express "NVM Express") (NVMe) starts with `nvme`. It is then followed by a number starting from `0` for the device controller, `nvme0` for the first discovered NVMe controller, `nvme1` for the second, and so on. Next is the letter "n" and a number starting from `1` expressing the device on a controller, i.e. `nvme0n1` for first discovered device on first discovered controller, `nvme0n2` for second discovered device on first discovered controller, and so on. Existing [partitions](/index.php/Partition "Partition") on each device will be listed with the letter "p" and the number that is assigned to them in the partition table. For example, `nvme0n1p1` for the partition with number `1` on first discovered device on first discovered controller, `nvme0n1p2` for partition `2`, and so on.

Summary:

*   `/dev/nvme0n1` - device `1` on controller `0`, the first discovered device on the first discovered controller.
*   `/dev/nvme0n1p1` - partition `1` on device `1` on controller `0`.
*   `/dev/nvme2n5` - device `5` on controller `2`, the fifth discovered device on the third discovered controller.
*   `/dev/nvme2n5p7` - partition `7` on device `5` on controller `2`.

#### MMC

[SD cards](https://en.wikipedia.org/wiki/SD_card "wikipedia:SD card"), [MMC cards](https://en.wikipedia.org/wiki/MultiMediaCard "wikipedia:MultiMediaCard") and [eMMC storage devices](https://en.wikipedia.org/wiki/MultiMediaCard#eMMC "wikipedia:MultiMediaCard") are handled by the kernel's `mmc` driver and name of those devices start with `mmcblk`. It is then followed by a number starting from `0` for the device, i.e. `mmcblk0` for first discovered device, `mmcblk1` for second discovered device and so on. Existing [partitions](/index.php/Partition "Partition") on each device will be listed with the letter "p" and the number that is assigned to them in the partition table. The partition with number `1` in the partition table would be `mmcblk0p1`, partition with number `2` would be `mmcblk0p2`, and so on.

Summary:

*   `/dev/mmcblk0` - device `0`, the first discovered device.
*   `/dev/mmcblk0p1` - partition `1` on device `0`.
*   `/dev/mmcblk4` - device `4`, the fifth discovered device.
*   `/dev/mmcblk4p7` - partition `7` on device `4`.

#### SCSI optical disc drive

The name of [optical disc drives](/index.php/Optical_disc_drive "Optical disc drive") (ODDs), that are attached using one of the interfaces supported by the [SCSI](#SCSI) driver subsystem, start with `sr`. The name is then followed by a number starting from `0` for the device, ie. `sr0` for the first discovered device, `sr1` for the second discovered device, and so on.

[Udev](/index.php/Udev "Udev") also provides `/dev/cdrom` that is a symbolic link to `/dev/sr0`. The name will always be `cdrom` regardless of the drive's supported disc types or the inserted media.

Summary:

*   `/dev/sr0` - optical disc drive `0`, the first discovered optical disc drive.
*   `/dev/sr4` - optical disc drive `4`, the fifth discovered optical disc drive.
*   `/dev/cdrom` - a symbolic link to `/dev/sr0`.

### Utilities

#### lsblk

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package provides the [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) utility which lists block devices, for example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

In the example above, only one device is available (`sda`), and that device has three partitions (`sda1` to `sda3`), each with a different [file system](/index.php/File_system "File system").

#### wipefs

*wipefs* can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device to make the signatures invisible for [libblkid(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libblkid.3). It does not erase the file systems themselves nor any other data from the device.

See [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## Pseudo-devices

Device nodes that do not have a physical device.

*   [/dev/random](/index.php//dev/random "/dev/random"), see [random(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/random.4)
*   [/dev/shm](/index.php//dev/shm "/dev/shm")
*   [/dev/null](https://en.wikipedia.org/wiki//dev/null "wikipedia:/dev/null"), [/dev/zero](https://en.wikipedia.org/wiki//dev/zero "wikipedia:/dev/zero"), see [null(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/null.4)
*   [/dev/full](https://en.wikipedia.org/wiki//dev/full "wikipedia:/dev/full"), see [full(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/full.4)
*   [/dev/ttyX](/index.php//dev/ttyX "/dev/ttyX"), where X is a number

## See also

*   [Linux allocated devices — The Linux Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)
*   [Gentoo:Device file](https://wiki.gentoo.org/wiki/Device_file "gentoo:Device file")
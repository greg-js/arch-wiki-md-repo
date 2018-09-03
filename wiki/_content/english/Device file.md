From [Wikipedia](https://en.wikipedia.org/wiki/Device_file "wikipedia:Device file"):

	In Unix-like operating systems, a device file or special file is an interface to a device driver that appears in a file system as if it were an ordinary file.

On Linux they are in the `/dev` directory, according to the [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard").

On Arch Linux the device nodes are managed by [udev](/index.php/Udev "Udev").

## Contents

*   [1 Block devices](#Block_devices)
    *   [1.1 lsblk](#lsblk)
    *   [1.2 wipefs](#wipefs)
*   [2 Pseudo-devices](#Pseudo-devices)
*   [3 See also](#See_also)

## Block devices

[Block devices](https://en.wikipedia.org/wiki/Device_file#Block_devices "wikipedia:Device file") provide buffered access to hardware devices and allow reading and writing blocks of any size and alignment.

The beginning of the device name specifies the type of block device. Most modern storage devices (e.g. hard disks, [SSDs](/index.php/SSD "SSD") and USB flash drives) are recognised as [SCSI](https://en.wikipedia.org/wiki/SCSI "wikipedia:SCSI") disks (`sd`). The type is followed by a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. *Existing* [partitions](/index.php/Partition "Partition") on each device will be listed with a number starting from `1` for the first partition (`sda1`), `2` for the second (`sda2`), and so on. Other common block device types include for example `mmcblk` for memory cards and `nvme` for [NVMe](/index.php/NVMe "NVMe") devices.

See also [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

### lsblk

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package provides the [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) utility to lists block devices, for example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

In the example above, only one device is available (`sda`), and that device has three partitions (`sda1` to `sda3`), each with a different [file system](/index.php/File_system "File system").

### wipefs

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
*   [/dev/null](https://en.wikipedia.org/wiki//dev/null "w:/dev/null"), [/dev/zero](https://en.wikipedia.org/wiki//dev/zero "w:/dev/zero"), see [null(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/null.4)
*   [/dev/full](https://en.wikipedia.org/wiki//dev/full "w:/dev/full"), see [full(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/full.4)

## See also

*   [Linux allocated devices — The Linux Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)
*   [Gentoo:Device file](https://wiki.gentoo.org/wiki/Device_file "gentoo:Device file")
From [Wikipedia](https://en.wikipedia.org/wiki/Floppy_disk "wikipedia:Floppy disk"):

	A floppy disk, also called a diskette, is a disk storage medium composed of a disk of thin and flexible magnetic storage medium, sealed in a rectangular plastic carrier lined with fabric that removes dust particles. Floppy disks are read and written by a floppy disk drive (FDD).

Common tasks with floppy disks are described bellow, with available tools to accomplish them.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Kernel module](#Kernel_module)
    *   [1.2 Packages](#Packages)
*   [2 Common tasks](#Common_tasks)
    *   [2.1 Format](#Format)
    *   [2.2 Mount](#Mount)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Unable to get diskette geometry](#Unable_to_get_diskette_geometry)
*   [4 See also](#See_also)

## Installation

### Kernel module

Most of the floppy drives should be supported by stock kernel. The module `floppy` is used as a driver for floppy drives.

The `floppy` module could not be loaded by default. In such case, it could be loaded with the following command:

1.  modprobe floppy

### Packages

There are two packages in the Arch package repository related with floppy disks:

*   [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)
*   [mtools](https://www.archlinux.org/packages/?name=mtools).

## Common tasks

Here are the commands needed to perform the most common tasks. In all examples is assumed that `/dev/fd0` is linux device for the floppy drive. By default, all these tasks need to be performed as *root*.

### Format

```
# mkfs.fat /dev/fd0

```

### Mount

```
# mount -t vfat /dev/fd0 /media/floppy

```

## Troubleshooting

### Unable to get diskette geometry

```
# mkfs.fat /dev/fd0
mkfs.fat 4.1 (2017-01-24)
mkfs.fat: unable to get diskette geometry for '/dev/fd0'

```

In such case, is probably that the diskette is physically damaged.

## See also

*   [https://github.com/dosfstools/dosfstools](https://github.com/dosfstools/dosfstools) - DOS filesystem utilities
*   [http://www.gnu.org/software/mtools/](http://www.gnu.org/software/mtools/) - a collection of utilities to access MS-DOS disks from Unix without mounting them
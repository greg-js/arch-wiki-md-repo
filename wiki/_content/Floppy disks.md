# Floppy disks

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Floppy disks#](https://wiki.archlinux.org/index.php/Talk:Floppy_disks))

From [Wikipedia](https://en.wikipedia.org/wiki/Floppy_disk "wikipedia:Floppy disk"):

NaN

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
*   [4 More Resources](#More_Resources)
*   [5 Todo](#Todo)

## Installation

### Kernel module

Most of the floppy drives should be supported by stock kernel. The module `floppy` is used as a driver for floppy drives.

The `floppy` module could not be loaded by default. In such case, it could be loaded with the following command:

```
$ modprobe floppy

```

### Packages

There are two packages in the Arch package repository related with floppy disks:

*   [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)
*   [mtools](https://www.archlinux.org/packages/?name=mtools).

## Common tasks

Here are the commands needed to perform the most common tasks. In all examples is assumed that `/dev/fd0` is linux device for the floppy drive. By default, all these tasks need to be performed as _root_.

### Format

```
# mkfs.msdos /dev/fd0

```

### Mount

```
# mount -t vfat /dev/fd0 /media/floppy

```

## Troubleshooting

### Unable to get diskette geometry

```
$ mkfs.msdos /dev/fd0
mkfs.msdos 3.0.5 (27 Jul 2009)
mkfs.msdos: unable to get diskette geometry for '/dev/fd0'

```

In such case, is probably that the diskette is physically damaged.

## More Resources

*   [http://www.daniel-baumann.ch/software/dosfstools/](http://www.daniel-baumann.ch/software/dosfstools/) - DOS filesystem utilities (not so verbosely documented IMHO)
*   [http://www.gnu.org/software/mtools/](http://www.gnu.org/software/mtools/) - a collection of utilities to access MS-DOS disks from Unix without mounting them

## Todo

*   [floppy(8)](http://linux.die.net/man/8/floppy)
*   [fdformat(8)](http://linux.die.net/man/8/fdformat)
*   recovering a "dead" floppy

Retrieved from "[https://wiki.archlinux.org/index.php?title=Floppy_disks&oldid=364996](https://wiki.archlinux.org/index.php?title=Floppy_disks&oldid=364996)"
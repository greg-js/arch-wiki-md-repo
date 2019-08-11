[Bcachefs](https://bcachefs.org/) is a next-generation CoW filesystem that aims to provide features from [Btrfs](/index.php/Btrfs "Btrfs") and [ZFS](/index.php/ZFS "ZFS") with a cleaner codebase, more stability, greater speed and a GPL-compatible license.

It is built upon [Bcache](/index.php/Bcache "Bcache") and is mainly developed by Kent Overstreet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Single drive](#Single_drive)
    *   [2.2 Multiple drives in RAID0/1](#Multiple_drives_in_RAID0/1)
    *   [2.3 Using ssds as a caching layer](#Using_ssds_as_a_caching_layer)
*   [3 Tips and Tricks](#Tips_and_Tricks)
*   [4 See also](#See_also)

## Installation

Bcachefs is not in the upstream [Kernel](/index.php/Kernel "Kernel") yet but the [linux-bcachefs-git](https://aur.archlinux.org/packages/linux-bcachefs-git/) kernel can be installed from the [AUR](/index.php/AUR "AUR").

The Bcachefs userspace tools are available from [bcachefs-tools-git](https://aur.archlinux.org/packages/bcachefs-tools-git/).

## Setup

### Single drive

```
# bcachefs format /dev/sda1
# mount -t bcachefs /dev/sda1 /mnt

```

### Multiple drives in RAID0/1

```
# bcachefs format /dev/sda1 /dev/sdb1 --data_replicas=*n* --metadata_replicas=*n*
# mount -t bcachefs /dev/sda1:/dev/sdb1 /mnt

```

### Using ssds as a caching layer

```
# bcachefs format \
    --group=ssds /dev/sda1 /dev/sdb1 
    --group=hdds /dev/sdc1 /dev/sdd1 /dev/sde1 /dev/sdf1
    --foreground_target=ssds \
    --background_target=hdds \
    --promote-target=ssds
# mount -t bcachefs /dev/sda1:/dev/sdb1:/dev/sdc1:/dev/sdd1/dev/sde1:/dev/sdf1 /mnt
```

## Tips and Tricks

Up-to-date documentation is only available via `bcachefs --help`. The man page, for instance, includes the now-useless `--tier` option.

## See also

*   [Kent Overstreet's Patreon page](https://www.patreon.com/bcachefs)
*   [Wikipedia:Bcachefs](https://en.wikipedia.org/wiki/Bcachefs "wikipedia:Bcachefs")
Related articles

*   [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Prepare live CD/DVD/USB](#Prepare_live_CD/DVD/USB)
*   [3 Backup in live environment](#Backup_in_live_environment)
*   [4 Restore (decompress)](#Restore_(decompress))
*   [5 Restore (mount and copy)](#Restore_(mount_and_copy))

## Overview

[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS") [[1]](http://squashfs.sourceforge.net/) makes highly compressed read-only backup archives of complete systems. It is convenient since you can mount it and find/grep/cp/tree in it without decompressing the whole SquashFS archive. Backup takes less time and overhead of file retrieval/traversal is lower compared to tar, but modifying an existing archive is impossible as a penalty.

## Prepare live CD/DVD/USB

You should have [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) installed in live CD/DVD/USB to make SquashFS archives. Please refer to [Archiso#Configure the live medium](/index.php/Archiso#Configure_the_live_medium "Archiso") on how to configure `packages.x86_64` and build live CD/DVD/USB with [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) installed.

## Backup in live environment

Boot into live CD/DVD/USB and mount filesystems you would like to backup.

**Note:** The following example is for an EFI-grub Arch installation with sdb1 as EFI partition and sdb2 as root partition.

```
# fsck /dev/sdb2
# fsck /dev/sdb1
# mount /dev/sdb2 /mnt
# mount /dev/sdb1 /mnt/boot/efi
# /somewhere/mksquashfs.sh SOURCE_DIRECTORY BACKUP_ARCHIVE_DIRECTORY

```

where

 `/somewhere/mksquashfs.sh` 
```
#!/usr/bin/env bash

# Sanity
if [ $# -ne 2 ]; then
  echo "invoke: mksquashfs.sh SOURCE_DIRECTORY BACKUP_ARCHIVE_DIRECTORY"
  exit 1
fi
echo -ne "

Have you fsck'd? "
read

# Backup
mksquashfs \
  "$1" "$2/$(date +%Y%m%d_%a).sfs" \
  -comp gzip \
  -xattrs \
  -progress \
  -mem 5G \
  -wildcards \
  -e \
  boot/efi \
  boot/grub \
  boot/vmlinuz-linux \
  boot/initramfs-linux"*".img

```

## Restore (decompress)

**Warning:** The following is complete but not yet tested. Do not use before this warning sign is removed.

```
#!/bin/bash

# Path to extract files
target=/mnt

# Path to backup SquashFS archive file
archive=/somewhere/backup.sfs

unsquashfs -stat $archive
unsquashfs -force -dest $target $archive
```

**Note:** To make system bootable after restore, you should:

1.  Fix fstab
2.  arch-chroot
    1.  mkinitcpio -p linux
    2.  grub-install
    3.  grub-mkconfig

## Restore (mount and copy)

**Warning:** The following is complete but not yet tested. Do not use before this warning sign is removed.

1.  mount somewhere/backup.sfs /mnt
2.  cp /mnt/somefile /somewhere/damaged-somefile
Related articles

*   [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar")

**Warning:** The following method is complete but not yet tested. Do not use before this warning sign is removed.

## Contents

*   [1 Overview](#Overview)
*   [2 Prepare live CD/DVD/USB](#Prepare_live_CD/DVD/USB)
*   [3 Backup in live environment](#Backup_in_live_environment)
*   [4 Restore(decompress)](#Restore(decompress))
*   [5 Restore(mount and copy)](#Restore(mount_and_copy))

## Overview

[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS") [[1]](http://squashfs.sourceforge.net/) makes highly-compressed read-only backup archives of complete systems. It is convenient since you can mount it and find/grep/cp/tree in it without decompressing the whole SquashFS archive. Backup takes less time and overhead of file retrieval/traversal is lower compared to tar, but you may never make changes to an existing archive.

## Prepare live CD/DVD/USB

You should have [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) installed in live CD/DVD/USB to make SquashFS archives. Please refer to [Archiso#Configure_the_live_medium](/index.php/Archiso#Configure_the_live_medium "Archiso") on how to configure `packages.x86_64` and build live CD/DVD/USB to with [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) installed.

## Backup in live environment

Boot into live CD/DVD/USB and mount filesystems you'd like to backup.

**Note:** The following example is for an EFI-grub Arch installation with sdb1 as EFI partition and sdb2 as root partition.

```
mount /dev/sdb2 /mnt
mount /dev/sdb1 /mnt/boot/efi
/somewhere/backup.sh /mnt /somewhere/$(date +%Y%m%d_%a).sfs
```

where

 `/somewhere/backup.sh` 
```
#!/bin/bash
# SYNTAX:backup.sh SOURCE_DIRECTORY BACKUP_ARCHIVE_FILE

# Paths to exclude
exclude='
boot/efi
boot/grub
boot/initramfs-linux*.img
'

# Backup
mksquashfs \
  "$1" "$2" \
  -comp gzip \
  -xattrs \
  -ef <(echo $exclude) \
  -wildcards \
  -progress \
  -mem 7G

```

## Restore(decompress)

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

## Restore(mount and copy)

```
#!/bin/bash
mount somewhere/backup.sfs /mnt
cp /mnt/somefile /somewhere/damaged-somefile

```
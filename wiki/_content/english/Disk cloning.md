Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [System backup](/index.php/System_backup "System backup")

Disk cloning is the process of making an image of a partition or of an entire hard drive. This can be useful for copying the drive to other computers and for [backup](/index.php/Backup "Backup") and [recovery](/index.php/File_recovery "File recovery") purposes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Using dd](#Using_dd)
*   [2 Using ddrescue](#Using_ddrescue)
*   [3 File system cloning](#File_system_cloning)
    *   [3.1 Using e2image](#Using_e2image)
*   [4 Disk cloning software](#Disk_cloning_software)
    *   [4.1 dd spin-offs](#dd_spin-offs)
*   [5 See also](#See_also)

## Using dd

See [dd#Disk cloning and restore](/index.php/Dd#Disk_cloning_and_restore "Dd").

## Using ddrescue

[ddrescue](https://www.archlinux.org/packages/?name=ddrescue) is a tool designed for cloning and recovering data. It copies data from one file or block device (hard disc, cdrom, etc) to another, trying to rescue the good parts first in case of read errors, to maximize the recovered data.

To clone a faulty or dying drive, run *ddrescue* twice. First round, copy every block without read error and log the errors to `rescue.log`.

```
# ddrescue -f -n /dev/sd*X* /dev/sd*Y* rescue.log

```

where `*X*` and `*Y*` are the desired partition letters of the [block devices](/index.php/Block_device "Block device").

Second round, copy only the bad blocks and try 3 times to read from the source before giving up.

```
# ddrescue -d -f -r3 /dev/sd*X* /dev/sd*Y* rescue.log

```

Now you can check the file system for corruption and mount the new drive.

```
# fsck -f /dev/sd*Y*

```

## File system cloning

### Using e2image

*e2image* is a tool included in [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) for debugging purposes. It can be used to copy ext2, ext3, and ext4 partitions efficiently by only copying the used blocks. Note that this only works for ext2, ext3, and ext4 filesystems, and the unused blocks are not copied so this may not be a useful tool if one is hoping to recover deleted files.

To clone a partition from physical disk `/dev/sda`, partition 1, to physical disk `/dev/sdb`, partition 1 with e2image, run

```
# e2image -ra -p /dev/sda1 /dev/sdb1

```

**Tip:** [GParted](/index.php/GParted "GParted") uses *e2image* to efficiently copy ext2/3/4 partitions.

## Disk cloning software

These applications allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. They contain complete system images from one or more specific points in time and are frequently used to record known good configurations. See [Wikipedia:Comparison of disk cloning software](https://en.wikipedia.org/wiki/Comparison_of_disk_cloning_software "wikipedia:Comparison of disk cloning software") for their comparison.

See also [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for other applications that can take full system snapshots, among other functionality.

*   **Arch Backup** — A trivial backup script with simple configuration.
    *   Configurable compression method.
    *   Multiple backup targets.

	[https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/](https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs, FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.
    *   Included on the Arch Linux installation media.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **Deepin Clone** — Tool by Deepin to backup and restore. It supports to clone, backup and restore disk or partition.

	[https://www.deepin.org/en/original/deepin-clone/](https://www.deepin.org/en/original/deepin-clone/) || [deepin-clone](https://www.archlinux.org/packages/?name=deepin-clone)

*   **FSArchiver** — A safe and flexible file-system backup and deployment tool
    *   Support for basic file attributes (permissions, owner, ...).
    *   Support for multiple file systems per archive.
    *   Support for extended attributes (they are used by SELinux).
    *   Support the basic file system attributes (label, uuid, block-size) for all Linux file systems.
    *   Support for [NTFS filesystem](http://www.fsarchiver.org/Cloning-ntfs) (ability to create flexible clones of Windows partitions).
    *   Checksumming of everything which is written in the archive (headers, data blocks, whole files).
    *   Ability to restore an archive which is corrupt (it will just skip the current file).
    *   Multi-threaded lzo, gzip, bzip2, lzma compression.
    *   Support for splitting large archives into several files with a fixed maximum size.
    *   Encryption of the archive using a password. Based on blowfish from libcrypto from [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Support backup of a mounted root filesystem (`-A` option).
    *   Can be found on the [System Rescue CD](http://www.sysresccd.org/Main_Page).

	[http://www.fsarchiver.org/](http://www.fsarchiver.org/) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — A disaster recovery solution to create backup media that can be used to redeploy the damaged system.
    *   Image-based backups, supporting Linux/Windows.
    *   Compression rate is adjustable.
    *   Can backup live systems (without having to halt it).
    *   Can split image over many files.
    *   Supports booting to a Live CD to perform a full restore.
    *   Can backup/restore over NFS, from CDs, tape drives and other media.
    *   Can verify backups.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports ext2, ext3, ext4, hfs+, reiserfs, reiser4, btrfs, vmfs3, vmfs5, xfs, jfs, ufs, ntfs, fat(12/16/32), exfat.
    *   Supports compression.
    *   Optionally, an *ncurses* interface can be used.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — An *ncurses* disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.
    *   Development stopped in favor of FSArchiver.

	[http://www.partimage.org](http://www.partimage.org) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **J7Z** — GUI for Linux in java which attempts to simplify data compression and backup. It can create 7z, BZip2, Zip, GZip, Tar archives.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

	[http://j7z.xavion.name/](http://j7z.xavion.name/) || [j7z](https://aur.archlinux.org/packages/j7z/)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) ||

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   GUI and CLI interfaces
    *   Creates *.tar.gz*, *.tar.bz2*, *.tar.xz* or *.tar* archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2, Syslinux, EFISTUB/efibootmgr and Systemd/bootctl

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

### dd spin-offs

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) is a dd replacement with on-the-fly hashing capability helping to ensure integrity. It accepts most of dd's parameters and includes status output. A stable version of *dcfldd* was [last released in 2006](http://dcfldd.sourceforge.net/).

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) is a data recovery tool capable of ignoring read errors. *ddrescue* is not related to dd in any way except that both can be used for copying data from one device to another. The key difference is that *ddrescue* uses a sophisticated algorithm to copy data from failing drives causing them as little additional damage as possible. See the [ddrescue manual](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) for details.

## See also

*   [Wikipedia:List of disk cloning software](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Arch Linux forum thread](https://bbs.archlinux.org/viewtopic.php?id=4329)
[SnapRAID](http://www.snapraid.it/) is a folder-based backup tool that behaves like a software or hardware RAID5/6 disk raid, but is not a disk raid itself. There is no realtime recovery, free space between disks cannot be combined and manual excution of backup is needed.

Because of the nature of folder-based backup, SnapRAID is more flexible and simpler than software raids. Although disk raids have advantages such as realtime backup, increased complexity or reduced performance are the drawback. Not to mention a two-disk failure or a SATA URE (Unrecoverable Read Error) happening to RAID5 could damage all data, which is not the case with SnapRAID. Thus the use of SnapRAID is logical when backup is the main goal rather than preventing a system from going offline due to disk failure.

SnapRAID works by storing parity of all folders to another disk. The destination disk which the parity file is stored on should be the largest. Other disks do not have this restriction and can be of any size. Summing up, SnapRAID is suitable for media centers where files are usually large and rarely changed. SnapRAID is highly flexible and can be configured to add/remove disk at any time. Also, more than one redundant disks are supported.

**Tip:**

*   If you want to combine folders into a larger one without setting up disk raid, FUSE-based filesystems is the best option. (e.g. MHDDFS, MergerFS, unionfs-fuse ) Overlayfs is another interesting choice and has been merged into kernel since 3.18\. Although it has less features and limitations such as having only one writable path and the need to specify a workdir. Other filesystems such as AUFS often involve kernel patching or unsupported or outdated software.
*   [mergerfs](https://aur.archlinux.org/packages/mergerfs/) is similar to mhddfs, but more recently updated and has more choices for drive-selection policies. It also has excellent speeds.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Backup](#Backup)
    *   [2.2 Undeletion](#Undeletion)
    *   [2.3 Disk recovery](#Disk_recovery)

## Installation

Install [snapraid](https://aur.archlinux.org/packages/snapraid/) from the [AUR](/index.php/AUR "AUR").

## Usage

See also [Manual for SnapRAID](http://snapraid.sourceforge.net/manual.html).

We have four disks with data on them, and want to save a redundant just in case. These four disks are mounted at:

*   /mnt/sda
*   /mnt/sdb
*   /mnt/sdc
*   /mnt/sdd

And an empty redundant disk mounted at:

*   /mnt/sde

Let us create a configuration file! Lines begining with "content" designate the path to a content file that stores SnapRAID metadata.

**Warning:** SnapRAID will need a content file to build a recovery. Multiple copies of this file are essential for maximum data safety. It would be wise to have this file on all disks and make backups elsewhere.
 `/etc/snapraid.conf` 
```
disk d1 /mnt/sda
disk d2 /mnt/sdb
disk d3 /mnt/sdc
disk d4 /mnt/sdd/I_only_want_to_backup_this_folder
parity /mnt/sde/SnapRAID.parity
content /mnt/sda/SnapRAID.content
content /mnt/sdb/SnapRAID.content
content /mnt/sdc/SnapRAID.content
content /var/snapraid/SnapRAID.content
exclude /lost+found/

```

**Warning:** The order of disks is relevant for parity.

**Tip:** The exclude line means the path to exclude. It is relative to *all* mount point

### Backup

To begin backup process, run:

```
# snapraid sync

```

### Undeletion

To revert a file or folder to an earlier version (undelete):

```
# snapraid fix -f FILENAME

```

( using compelete PATH of file or dir is better. file path is relative to all root dir )

### Disk recovery

If the disk is mounted at `/mnt/sda` is dead and being replaced, edit `/etc/snapraid.conf` before doing a recovery.

Change the line

```
disk d1 /mnt/sda

```

to

```
disk d1 /mnt/sda_new

```

To begin recovery

```
# snapraid -d d1 -l recovery.log fix

```
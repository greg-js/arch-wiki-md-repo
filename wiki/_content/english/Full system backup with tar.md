Related articles

*   [Full system backup with SquashFS](/index.php/Full_system_backup_with_SquashFS "Full system backup with SquashFS")

This article will show you how to do a full system backup with [tar](/index.php/Tar "Tar").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Boot with LiveCD](#Boot_with_LiveCD)
*   [3 Changing Root](#Changing_Root)
*   [4 Mount Other Partitions](#Mount_Other_Partitions)
*   [5 Exclude File](#Exclude_File)
*   [6 Backup Script](#Backup_Script)
*   [7 Restoring](#Restoring)
*   [8 Backup with parallel compression](#Backup_with_parallel_compression)

## Overview

Backing up with tar has the advantages of using compression that can help save disk space, and simplicity. The process only requires several steps, they are:

1.  Boot from a LiveCD
2.  Change root to the Linux install
3.  Mount additional (if any) partitions/drives
4.  Add exclusions
5.  Use the backup script to backup

To minimize downtime the backup can alternatively be performed on a running system using [LVM snapshots](/index.php/LVM#Snapshots "LVM"), if all filesystems reside on LVM volumes.

## Boot with LiveCD

Many Linux bootable CDs, USBs... have the ability to let you change root to your install. While changing root isn't necessary to do a backup, it provides the ability to just run the script without need to transfer it to a temporary drive or having to locate it on the filesystem. The Live medium must be of the same architecture that your Linux install currently is (i.e. i686 or x86_64).

## Changing Root

First you should have a scripting environment set up on your current Linux install. If you do not know what that is, it means that you are able to execute any scripts that you may have as if they are regular programs. If you do not, see this [article](http://linuxtidbits.wordpress.com/2009/12/03/setting-up-a-scripting-environment/) on how to do that. What you'll need to do next is change root, to learn more about what changing root is, read [this](/index.php/Change_root "Change root"). When you change root, you do not need to mount any temporary file systems (<tt>/proc</tt>, <tt>/sys</tt>, and <tt>/dev</tt>). These temporary file systems get populated on boot and you actually do not want to backup them up because they can interfere with the normal (and necessary) population process which can change on any upgrade. To change root, you'll need to mount your current Linux installs root partition. For example:

```
mkdir /mnt/arch
mount /dev/<your-partition-or-drive>

```

Use `fdisk -l` to discover you partitions and drives. Now `chroot`:

```
cd /mnt/arch
chroot . /bin/bash

```

**Warning:** Do not use <tt>arch-chroot</tt> to chroot into the target system - the backup process will fail as it'll try to back up temporary file systems, all system memory and other interesting things. Use plain <tt>chroot</tt> instead.

This example obviously uses bash but you can use other shells if available. Now you will be in your scripted environment (this is provided that you have your `~/.bashrc` sourced on entry):

```
cat ~/.bash_profile
# If using bash, source the local .bashrc
source ~/.bashrc

```

## Mount Other Partitions

Other partitions that you use (if any) will need to be mounted in their proper places (e.g. if you have a separate <tt>/home</tt> partition).

## Exclude File

`tar` has the ability to ignore specified files and directories. The syntax is one definition per line. `tar` also has the capability to understand regular expressions (regexps). For example:

```
# Not old backups                                                               
/opt/backup/arch-full*                                                                   

# Not temporary files                                                           
/tmp/*

# Not the cache for pacman
/var/cache/pacman/pkg/
...

```

## Backup Script

Backing up with tar is straight-forward process. Here is a basic script that can do it and provides a couple checks. You'll need to modify this script to define your backup location, and exclude file (if you have one), and then just run this command after you've `chroot`ed and mounted all your partitions.

```
#!/bin/bash
# full system backup

# Backup destination
backdest=/opt/backup

# Labels for backup name
#PC=${HOSTNAME}
pc=pavilion
distro=arch
type=full
date=$(date "+%F")
backupfile="$backdest/$distro-$type-$date.tar.gz"

# Exclude file location
prog=${0##*/} # Program name from filename
excdir="/home/<user>/.bin/root/backup"
exclude_file="$excdir/$prog-exc.txt"

# Check if chrooted prompt.
echo -n "First chroot from a LiveCD.  Are you ready to backup? (y/n): "
read executeback

# Check if exclude file exists
if [ ! -f $exclude_file ]; then
  echo -n "No exclude file exists, continue? (y/n): "
  read continue
  if [ $continue == "n" ]; then exit; fi
fi

if [ $executeback = "y" ]; then
  # -p and --xattrs store all permissions and extended attributes. 
  # Without both of these, many programs will stop working!
  # It is safe to remove the verbose (-v) flag. If you are using a 
  # slow terminal, this can greatly speed up the backup process.
  tar --exclude-from=$exclude_file --xattrs -czpvf $backupfile /
fi

```

## Restoring

To restore from a previous backup, mount all relevant partitions, change the current working directory to the root directory, and execute

```
bsdtar --xattrs -xpf $backupfile

```

replacing $backupfile with the backup archive. Removing all files that had been added since the backup was made must be done manually. Recreating the filesystem(s) is an easy way to do this.

## Backup with parallel compression

To back up using parallel compression ([SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing")), use [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) (Parallel bzip2):

```
# tar -cvf /path/to/chosen/directory/etc-backup.tar.bz2 -I pbzip2 /etc

```

Store `etc-backup.tar.bz2` on one or more offline media, such as a USB stick, external hard drive, or CD-R. Occasionally verify the integrity of the backup process by comparing original files and directories with their backups. Possibly maintain a list of hashes of the backed up files to make the comparison quicker.

Restore corrupted `/etc` files by extracting the `etc-backup.tar.bz2` file in a temporary working directory, and copying over individual files and directories as needed. To restore the entire `/etc` directory with all its contents execute the following command as root:

```
tar -xvf etc-backup.tar.bz2 -C /

```
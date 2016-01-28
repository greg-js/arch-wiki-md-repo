# Full System Backup with tar

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Uses a half-baked script instead of explaining basic options and referring to the manual, duplication with articles such as [Help:Reading](/index.php/Help:Reading "Help:Reading"), numerous [Help:Style](/index.php/Help:Style "Help:Style") issues (Discuss in [Talk:Full System Backup with tar#](https://wiki.archlinux.org/index.php/Talk:Full_System_Backup_with_tar))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [tar](/index.php/Tar "Tar").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Full System Backup with tar#](https://wiki.archlinux.org/index.php/Talk:Full_System_Backup_with_tar))

This article will show you how to do a full system backup with [tar](/index.php/Tar "Tar").

## Contents

*   [1 Overview](#Overview)
*   [2 Boot with LiveCD](#Boot_with_LiveCD)
*   [3 Changing Root](#Changing_Root)
*   [4 Mount Other Partitions](#Mount_Other_Partitions)
*   [5 Exclude File](#Exclude_File)
*   [6 Backup Script](#Backup_Script)
*   [7 Restoring](#Restoring)

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
tar --xattrs -xpf $backupfile

```

replacing $backupfile with the backup archive. Removing all files that had been added since the backup was made must be done manually. Recreating the filesystem(s) is an easy way to do this.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Full_System_Backup_with_tar&oldid=405336](https://wiki.archlinux.org/index.php?title=Full_System_Backup_with_tar&oldid=405336)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
**翻译状态：** 本文是英文页面 [Rsync](/index.php/Rsync "Rsync") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-09-15，点击[这里](https://wiki.archlinux.org/index.php?title=Rsync&diff=0&oldid=222954)可以查看翻译后英文页面的改动。

[rsync](http://samba.anu.edu.au/rsync/) 是一个开源工具，可以进行快速的增量的文件传输。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [2.1 作为 cp 的替代](#.E4.BD.9C.E4.B8.BA_cp_.E7.9A.84.E6.9B.BF.E4.BB.A3)
    *   [2.2 作为备份工具](#.E4.BD.9C.E4.B8.BA.E5.A4.87.E4.BB.BD.E5.B7.A5.E5.85.B7)
        *   [2.2.1 自动备份](#.E8.87.AA.E5.8A.A8.E5.A4.87.E4.BB.BD)
        *   [2.2.2 自动用 SSH 备份](#.E8.87.AA.E5.8A.A8.E7.94.A8_SSH_.E5.A4.87.E4.BB.BD)
        *   [2.2.3 自动与 NetworkManager 备份](#.E8.87.AA.E5.8A.A8.E4.B8.8E_NetworkManager_.E5.A4.87.E4.BB.BD)
        *   [2.2.4 Differential backup on a week](#Differential_backup_on_a_week)
        *   [2.2.5 快照备份](#.E5.BF.AB.E7.85.A7.E5.A4.87.E4.BB.BD)

## 安装

使用[pacman](/index.php/Pacman "Pacman")安装[rsync](https://www.archlinux.org/packages/?name=rsync):

```
# pacman -S rsync

```

**注意:** *rsync* 必须同时安装在源(服务器)和目的(客户端)的机器上．

## 使用方法

For more examples, search the [Community Contributions](https://bbs.archlinux.org/viewforum.php?id=27) and [General Programming](https://bbs.archlinux.org/viewforum.php?id=33) forums.

### 作为 cp 的替代

rsync can be used as an advanced cp alternative, especially for copying larger files:

```
$ rsync -P source destination

```

The `-P` option is the same as `--partial --progress`, which keeps partially transferred files and shows a progress bar during transfer.

You may want to use the `-r --recursive` option to recurse into directories, or the `-R` option for using relative path names (recreating entire folder hierarchy on the destination folder).

### 作为备份工具

The rsync protocol can easily be used for backups, only transferring files that have changed since the last backup. This section describes a very simple scheduled backup script using rsync, typically used for copying to removable media. For a more thorough example, see [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

#### 自动备份

For the sake of this example, the script is created in the `/etc/cron.daily` directory, and will be run on a daily basis if a cron [daemon](/index.php/Daemon "Daemon") is installed and properly configured. Configuring and using [cron](/index.php/Cron "Cron") is outside the scope of this article.

First, create a script containing the appropriate command options:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete /folder/to/backup /location/to/backup &> /dev/null
```

	`-a` 

	indicates that files should be archived, meaning that most of their characteristics are preserved (but **not** ACLs, hard links or extended attributes such as capabilities)

	`--delete` 

	means files deleted on the source are to be deleted on the backup aswell

Here, `/folder/to/backup` should be changed to what needs to be backed-up (`/home`, for example) and `/location/to/backup` is where the backup should be saved (`/media/disk`, for instance).

Finally, the script must be executable:

```
# chmod +x /etc/cron.daily/rsync.backup

```

#### 自动用 SSH 备份

If backing-up to a remote host using [SSH](/index.php/SSH "SSH"), use this script instead:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete -e ssh /folder/to/backup remoteuser@remotehost:/location/to/backup &> /dev/null
```

	`-e ssh` 

	tells rsync to use SSH

	`remoteuser` 

	is the user on the host `remotehost`

	`-a` 

	groups all these options `-rlptgoD` (recursive, links, perms, times, group, owner, devices)

#### 自动与 NetworkManager 备份

This script starts a backup when you plugin your wire.

First, create a script containing the appropriate command options:

 `/etc/NetworkManager/dispatcher.d/backup` 
```
#!/bin/bash

if [ x"$2" = "xup" ] ; then
  rsync --force --ignore-errors -a --delete --bwlimit=2000 --files-from=files.rsync /folder/to/backup /location/to/backup
fi
```

	`-a` 

	group all this options `-rlptgoD` recursive, links, perms, times, group, owner, devices

	`--files-from` 

	read the relative path of */folder/to/backup* from this file

	`--bwlimit` 

	limit I/O bandwidth; KBytes per second

#### Differential backup on a week

This is a useful option of rsync, creating a full backup and a differential backup for each day of a week.

First, create a script containing the appropriate command options:

 `/etc/cron.daily/backup` 
```
#!/bin/bash

DAY=$(date +%A)

if [ -e /location/to/backup/incr/$DAY ] ; then
  rm -fr /location/to/backup/incr/$DAY
fi

rsync -a --delete --inplace --backup --backup-dir=/location/to/backup/incr/$DAY /folder/to/backup/ /location/to/backup/full/ &> /dev/null
```

	`--inplace` 

	implies `--partial` update destination files in-place

#### 快照备份

The same idea can be used to maintain a tree of snapshots of your files. In other words, a directory with date-ordered copies of the files. The copies are made using hardlinks, which means that only files that did change will occupy space. Generally speaking, this is the idea behind Apple's TimeMachine.

This script implements a simple version of it:

 `/usr/local/bin/rsnapshot.sh` 
```
#!/bin/bash

## my own rsync-based snapshot-style backup procedure
## (cc) marcio rps AT gmail.com

# config vars

SRC="/home/username/files/" #dont forget trailing slash!
SNAP="/snapshots/username"
OPTS="-rltgoi --delay-updates --delete --chmod=a-w"
MINCHANGES=20

# run this process with real low priority

ionice -c 3 -p $$
renice +12  -p $$

# sync

rsync $OPTS $SRC $SNAP/latest >> $SNAP/rsync.log

# check if enough has changed and if so
# make a hardlinked copy named as the date

COUNT=$( wc -l $SNAP/rsync.log|cut -d" " -f1 )
if [ $COUNT -gt $MINCHANGES ] ; then
   DATETAG=$(date +%Y-%m-%d)
   if [ ! -e $SNAP/$DATETAG ] ; then
      cp -al $SNAP/latest $SNAP/$DATETAG
      mv $SNAP/rsync.log $SNAP/$DATETAG
   fi
fi

```

To make things really, really simple this script can be run out of `/etc/rc.local`.
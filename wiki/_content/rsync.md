# rsync

Related articles

*   [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync")
*   [Backup programs](/index.php/Backup_programs "Backup programs")

[rsync](https://rsync.samba.org/) is an open source utility that provides fast incremental file transfer.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 As a cp alternative](#As_a_cp_alternative)
        *   [2.1.1 Trailing slash caveat](#Trailing_slash_caveat)
    *   [2.2 As a backup utility](#As_a_backup_utility)
        *   [2.2.1 Automated backup](#Automated_backup)
        *   [2.2.2 Automated backup with SSH](#Automated_backup_with_SSH)
        *   [2.2.3 Automated backup with NetworkManager](#Automated_backup_with_NetworkManager)
        *   [2.2.4 Automated backup with systemd and inotify](#Automated_backup_with_systemd_and_inotify)
        *   [2.2.5 Differential backup on a week](#Differential_backup_on_a_week)
        *   [2.2.6 Snapshot backup](#Snapshot_backup)
*   [3 Graphical frontends](#Graphical_frontends)

## Installation

[Install](/index.php/Install "Install") the [rsync](https://www.archlinux.org/packages/?name=rsync) package.

**Note:** _rsync_ must be installed on both the source and the destination machine.

## Usage

For more examples, search the [Community Contributions](https://bbs.archlinux.org/viewforum.php?id=27) and [General Programming](https://bbs.archlinux.org/viewforum.php?id=33) forums.

### As a cp alternative

rsync can be used as an advanced alternative for the `cp` command, especially for copying larger files:

```
$ rsync -P source destination

```

The `-P` option is the same as `--partial --progress`, which keeps partially transferred files and shows a progress bar during transfer.

You may want to use the `-r --recursive` option to recurse into directories.

Files can be copied locally as with cp, but the motivating purpose of rsync is to copy files remotely, i.e. between two different hosts. Remote locations can be specified with a host-colon syntax:

```
$ rsync source host:destination

```

or

```
$ rsync host:source destination

```

Network file transfers use the SSH protocol by default.

Whether transferring files locally or remotely, rsync first creates an index of block checksums of each source file. This index is used to find any identical blocks of data which might exist in the destination. Such blocks are used in-place, rather than being copied from the source. This can greatly accelerate the synchronization of large files with small changes. For more information, see [official documentation](https://rsync.samba.org/documentation.html), [how rsync works](https://rsync.samba.org/how-rsync-works.html).

#### Trailing slash caveat

Arch by default uses GNU cp (part of [GNU coreutils](https://www.archlinux.org/packages/?name=coreutils)). However, rsync follows the convention of BSD cp, which gives special treatment to source directories with a trailing slash "/". Although

```
$ rsync -r source destination

```

creates a directory "destination/source" with the contents of "source", the command

```
$ rsync -r source/ destination

```

copies all of the files in "source/" directly into "destination", with no intervening subdirectory - just as if you had invoked it as

```
$ rsync -r source/. destination

```

This behavior is different from that of GNU cp, which treats "source" and "source/" identically (but not "source/."). Also, some shells automatically append the trailing slash when tab-completing directory names. Because of these factors, there can be a tendency among new or occasional rsync users to forget about rsync's different behavior, and inadvertently create a mess or even overwrite important files by leaving the trailing slash on the command line.

Thus it can be prudent to use a wrapper script to automatically remove trailing slashes before invoking rsync:

```
#!/bin/zsh
new_args=();
for i in "$@"; do
    case $i in /) i=/;; */) i=${i%/};; esac
    new_args+=$i;
done
exec rsync "${(@)new_args}"

```

This script can be put somewhere in the path, and aliased to rsync in the shell init file.

### As a backup utility

The rsync protocol can easily be used for backups, only transferring files that have changed since the last backup. This section describes a very simple scheduled backup script using rsync, typically used for copying to removable media. For a more thorough example and **additional options required to preserve some system files**, see [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

#### Automated backup

For the sake of this example, the script is created in the `/etc/cron.daily` directory, and will be run on a daily basis if a cron [daemon](/index.php/Daemon "Daemon") is installed and properly configured. Configuring and using [cron](/index.php/Cron "Cron") is outside the scope of this article.

First, create a script containing the appropriate command options:

 `/etc/cron.daily/backup` 

```
#!/bin/bash
rsync -a --delete /folder/to/backup /location/of/backup &> /dev/null
```

	`-a` 

	indicates that files should be archived, meaning that most of their characteristics are preserved (but **not** ACLs, hard links or extended attributes such as capabilities)

	`--delete` 

	means files deleted on the source are to be deleted on the backup as well

Here, `/folder/to/backup` should be changed to what needs to be backed-up (`/home`, for example) and `/location/to/backup` is where the backup should be saved (`/media/disk`, for instance).

Finally, the script must be executable:

```
# chmod +x /etc/cron.daily/backup

```

#### Automated backup with SSH

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

#### Automated backup with NetworkManager

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

	read the relative path of _/folder/to/backup_ from this file

	`--bwlimit` 

	limit I/O bandwidth; KBytes per second

Also, the script must have write permission for owner (root, of course) only (see [NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") for details).

#### Automated backup with systemd and inotify

**Note:**

*   Due to the limitations of inotify and systemd (see [this question and answer](http://www.quora.com/Linux-Kernel/Inotify-monitoring-of-directories-is-not-recursive-Is-there-any-specific-reason-for-this-design-in-Linux-kernel)), recursive filesystem monitoring is not possible. Although you can watch a directory and its contents, it will not recurse into subdirectories and watch the contents of them; you must explicitly specify every directory to watch, even if that directory is a child of an already watched directory.
*   This setup is based on a [systemd/User](/index.php/Systemd/User "Systemd/User") instance.

Instead of running time interval backups with time based schedules, such as those implemented in [cron](/index.php/Cron "Cron"), it is possible to run a backup every time one of the files you are backing up changes. `systemd.path` units use `inotify` to monitor the filesystem, and can be used in conjunction with `systemd.service` files to start any process (in this case your **rsync** backup) based on a filesystem event.

First, create the `systemd.path` file that will monitor the files you are backing up:

 `~/.config/systemd/user/backup.path` 

```
[Unit]
Description=Checks if paths that are currently being backed up have changed

[Path]
PathChanged=%h/documents
PathChanged=%h/music

[Install]
WantedBy=default.target
```

Then create a `systemd.service` file that will be activated when it detects a change. By default a service file of the same name as the path unit (in this case `backup.path`) will be activated, except with the `.service` extension instead of `.path` (in this case `backup.service`).

**Note:** If you need to run multiple rsync commands, use `Type=oneshot`. This allows you to specify multiple `ExecStart=` parameters, one for each **rsync** command, that will be executed. Alternatively, you can simply write a script to perform all of your backups, just like [cron](/index.php/Cron "Cron") scripts.

 `~/.config/systemd/user/backup.service` 

```
[Unit]
Description=Backs up files

[Service]
ExecStart=/usr/bin/rsync %h/./documents %h/./music -CERrltm --delete ubuntu:
```

Now all you have to do is [start](/index.php/Start "Start")/enable `backup.path` like a normal systemd service and it will start monitoring file changes and automatically starting `backup.service`.

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

#### Snapshot backup

The same idea can be used to maintain a tree of snapshots of your files. In other words, a directory with date-ordered copies of the files. The copies are made using hardlinks, which means that only files that did change will occupy space. Generally speaking, this is the idea behind Apple's TimeMachine.

This basic script is easy to implement and creates quick incremental snapshots using the `--link-dest` option to hardlink unchanged files:

 `/usr/local/bin/snapbackup.sh` 

```
#!/bin/bash

# Basic snapshot-style rsync backup script 

# Config
OPT="-aPh"
LINK="--link-dest=/snapshots/username/last/" 
SRC="/home/username/files/"
SNAP="/snapshots/username/"
LAST="/snapshots/username/last"
date=`date "+%Y-%b-%d:_%T"`

# Run rsync to create snapshot
rsync $OPT $LINK $SRC ${SNAP}$date

# Remove symlink to previous snapshot
rm -f $LAST

# Create new symlink to latest snapshot for the next backup to hardlink
ln -s ${SNAP}$date $LAST 

```

There must be a symlink to a full backup already in existence as a target for `--link-dest`. If the most recent snapshot is deleted, the symlink will need to be recreated to point to the most recent snapshot. If `--link-dest` does not find a working symlink, rsync will proceed to copy all source files instead of only the changes.

A more sophisticated version checks to see if a certain number of changes have been made before making the backup and utilizes `cp -al` to hardlink unchanged files:

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
                chmod u+w $SNAP/$DATETAG
                mv $SNAP/rsync.log $SNAP/$DATETAG
               chmod u-w $SNAP/$DATETAG
         fi
fi

```

To make things really, really simple this script can be run from a [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") unit.

## Graphical frontends

[Install](/index.php/Install "Install") the [grsync](https://www.archlinux.org/packages/?name=grsync) package.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rsync&oldid=411738](https://wiki.archlinux.org/index.php?title=Rsync&oldid=411738)"
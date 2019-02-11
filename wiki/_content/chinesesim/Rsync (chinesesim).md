**翻译状态：** 本文是英文页面 [Rsync](/index.php/Rsync "Rsync") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-17，点击[这里](https://wiki.archlinux.org/index.php?title=Rsync&diff=0&oldid=450999)可以查看翻译后英文页面的改动。

相关文章

*   [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync")
*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[rsync](http://samba.anu.edu.au/rsync/) 是一个开源工具，可以进行快速的增量的文件传输。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 使用方法](#使用方法)
    *   [2.1 作为 cp 的替代](#作为_cp_的替代)
        *   [2.1.1 注意尾随下划](#注意尾随下划)
    *   [2.2 作为备份工具](#作为备份工具)
        *   [2.2.1 自动备份](#自动备份)
        *   [2.2.2 自动用 SSH 备份](#自动用_SSH_备份)
        *   [2.2.3 自动使用NetworkManager备份](#自动使用NetworkManager备份)
        *   [2.2.4 使用systemd和inotify自动备份](#使用systemd和inotify自动备份)
        *   [2.2.5 一个星期差异备份](#一个星期差异备份)
        *   [2.2.6 快照备份](#快照备份)
*   [3 图形前端](#图形前端)

## 安装

[安装](/index.php/Pacman "Pacman") [rsync](https://www.archlinux.org/packages/?name=rsync) 包。

**Note:** 必须在源计算机和目标计算机上都安装 *rsync*

## 使用方法

搜索 [Community Contributions](https://bbs.archlinux.org/viewforum.php?id=27) 和 [General Programming](https://bbs.archlinux.org/viewforum.php?id=33) 可以得到更多的例子。

### 作为 cp 的替代

rsync 可以作为 `cp` 命令的高级替代品，特别在复制较大的文件的场景中：

```
$ rsync -P source destination

```

其中 `-P` 与 `--partial --progress` 选项的作用是相同的，该选项使得文件可以分块传输并显示传输过程中的进度。

您可能需要使用 `-r --recursive` 选项使目录被递归地传输。

通过 cp 命令，可以本地复制文件，但 rsync 令人激动的一个特性是可以远程复制文件，例如，在两个不同的主机之间。远程位置可以用主机加冒号进行指定：

```
$ rsync source host:destination

```

或者

```
$ rsync host:source destination

```

网络文件传输默认使用SSH协议。

无论是本地或远程文件传输， rsync 首先创建每个源文件块校验的索引。此索引用于查找可能存在于目标中的任何相同数据块。一旦这种块存在，块就被就地使用，而不是从源复制。这大大加快了存在小差异的大文件的同步。欲了解更多信息，请参见 [official documentation](https://rsync.samba.org/documentation.html), [how rsync works](https://rsync.samba.org/how-rsync-works.html) 。

#### 注意尾随下划

Arch 默认使用 GNU cp (part of [GNU coreutils](https://www.archlinux.org/packages/?name=coreutils)). 然而，rsync 遵循 BSD cp 的约定, 源目录后面带有一个斜杠“/”有着特定的处理。比如：

```
$ rsync -r source destination

```

创建一个有着 "source"内容的 "destination/source"目录，命令：

```
$ rsync -r source/ destination

```

把"source/"目录下的所有文件全部复制到"destination"目录下，而没有中间的子目录 - 就像你调用了：

```
$ rsync -r source/. destination

```

这与 GNU cp 的行为是不同的，在GNU cp中"source" 与 "source/" 意义相同 (不是"source/.")。此外，一些shell可以在你键入Tab补全的时候自动自动给目录追加尾部下划线。由于这些因素，可以有新的或不熟练的rsync用户倾向于忘记的rsync的不同行为，在命令行上留下了结尾的下划线，从而无意间创造一个烂摊子，甚至覆盖重要文件。

谨慎起见，可以使用包装脚在调用rsync之前自动删除尾部斜杠：

```
#!/bin/zsh
new_args=();
for i in "$@"; do
    case $i in /) i=/;; */) i=${i%/};; esac
    new_args+=$i;
done
exec rsync "${(@)new_args}"

```

该脚本可以放在某个路径下，并在shell的init文件中把别名改为rsync。

### 作为备份工具

rsync协议可以很容易地用于备份，只传输自上次备份以来已更改的文件。本节将介绍一个非常简单的基于rsync的计划备份脚本，通常用于复制到可移动介质。对于更详尽的例子， **保留一些系统文件所需的附加选项**, 参见 [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

#### 自动备份

以下面的脚本为例，该脚本放置于 `/etc/cron.daily` 目录下，如果 cron [daemon](/index.php/Daemon "Daemon") 被正确安装和配置，它将每天运行。配置和使用 [cron](/index.php/Cron "Cron") 是本文的范围之外。

首先，创建一个包含相应命令选项的脚本：

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete /folder/to/backup /location/of/backup &> /dev/null
```

	`-a` 

	表示文件应被存档，这意味着他们的大部分特性被保留 (**不**包括ACLs, 硬链接或扩展属性，如capabilities)

	`--delete` 

	指同步源文件的删除操作。

在这里，`/folder/to/backup` 应该改成需要被备份的路径 (比如 `/home`)，`/location/to/backup` 是备份应存放的位置 (比如 `/media/disk`).

最后，脚本必须是可执行的：

```
# chmod +x /etc/cron.daily/backup

```

#### 自动用 SSH 备份

如果是通过 [SSH](/index.php/SSH "SSH") 备份到远程主机，改为使用此脚本：

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete -e ssh /folder/to/backup remoteuser@remotehost:/location/of/backup &> /dev/null
```

	`-e ssh` 

	告诉rsync的使用SSH

	`remoteuser` ：远程主机 `remotehost` 上的用户名

	`-a` 

	组中的所有这些选项 `-rlptgoD` (recursive, links, perms, times, group, owner, devices)

#### 自动使用NetworkManager备份

该脚本在你接入网络后开始备份。

首先，创建一个包含相应命令选项的脚本：

 `/etc/NetworkManager/dispatcher.d/backup` 
```
#!/bin/bash

if [ x"$2" = "xup" ] ; then
        rsync --force --ignore-errors -a --delete --bwlimit=2000 --files-from=files.rsync /folder/to/backup /location/to/backup
fi
```

	`-a` 

	组中的所有选项 `-rlptgoD` recursive, links, perms, times, group, owner, devices

	`--files-from` 

	从文件中读取到备份路径/folder/to/backup的相对路径

	`--bwlimit` 

	限I / O带宽;每秒千字节

Also, the script must have write permission for owner (root, of course) only (see [NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") for details).

#### 使用systemd和inotify自动备份

**Note:**

*   Due to the limitations of inotify and systemd (see [this question and answer](http://www.quora.com/Linux-Kernel/Inotify-monitoring-of-directories-is-not-recursive-Is-there-any-specific-reason-for-this-design-in-Linux-kernel)), recursive filesystem monitoring is not possible. Although you can watch a directory and its contents, it will not recurse into subdirectories and watch the contents of them; you must explicitly specify every directory to watch, even if that directory is a child of an already watched directory.
*   This setup is based on a [systemd/User](/index.php/Systemd/User "Systemd/User") instance.

Instead of running time interval backups with time based schedules, such as those implemented in [cron](/index.php/Cron "Cron"), it is possible to run a backup every time one of the files you are backing up changes. `systemd.path` units use `inotify` to monitor the filesystem, and can be used in conjunction with `systemd.service` files to start any process (in this case your [rsync](/index.php/Rsync "Rsync") backup) based on a filesystem event.

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

**Note:** If you need to run multiple rsync commands, use `Type=oneshot`. This allows you to specify multiple `ExecStart=` parameters, one for each [rsync](/index.php/Rsync "Rsync") command, that will be executed. Alternatively, you can simply write a script to perform all of your backups, just like [cron](/index.php/Cron "Cron") scripts.
 `~/.config/systemd/user/backup.service` 
```
[Unit]
Description=Backs up files

[Service]
ExecStart=/usr/bin/rsync %h/./documents %h/./music -CERrltm --delete ubuntu:
```

Now all you have to do is [start](/index.php/Start "Start")/enable `backup.path` like a normal systemd service and it will start monitoring file changes and automatically starting `backup.service`.

#### 一个星期差异备份

这个 rsync 选项很有用，可以每日创建全量或增量备份。

首先，创建一个包含相应命令选项的脚本：

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

## 图形前端

[安装](/index.php/Pacman "Pacman") [grsync](https://www.archlinux.org/packages/?name=grsync) 。
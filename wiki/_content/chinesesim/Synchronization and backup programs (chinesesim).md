Related articles

*   [System backup](/index.php/System_backup "System backup")
*   [Disk cloning (简体中文)](/index.php/Disk_cloning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disk cloning (简体中文)")
*   [List of applications#File sharing](/index.php/List_of_applications#File_sharing "List of applications")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [Dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles")
*   [File recovery (简体中文)](/index.php/File_recovery_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File recovery (简体中文)")

这个页面列出并比较了在两个或多个位置之间同步数据的应用程序，以及在此功能之上建立的以备份为目的的制作重要数据的增量副本的应用程序。因为它们的关系，这两组程序共享许多特征所有在同一篇文章里解释描述它们.

## Contents

*   [1 备份概览](#备份概览)
*   [2 数据同步](#数据同步)
    *   [2.1 说明](#说明)
    *   [2.2 表格](#表格)
*   [3 增量备份](#增量备份)
    *   [3.1 单机器](#单机器)
        *   [3.1.1 基于块的增量](#基于块的增量)
        *   [3.1.2 基于文件的增量](#基于文件的增量)
    *   [3.2 面向网络](#面向网络)
*   [4 版本控制系统](#版本控制系统)
*   [5 也可查阅](#也可查阅)

## 备份概览

备份重要数据是必须采取的措施，因为人和机器的处理错误随着时间推移非常可能产生损坏,并且存储数据的物理媒体也不可避免的注定损坏. 为了选择满足每个人的需求的程序，下面的一些问题要考虑:

*   存储数据的备份媒介, 比如. CD, DVD, 远程服务器, 外部硬盘, 等的种类.
*   计划的备份频率, 比如. 每天, 每周, 每月, 等等.
*   希望从备份获取的功能，比如，压缩，加密，处理重命名等.
*   如果需要的话存储重命名的方式.

## 数据同步

这些应用做的只是以一种“镜像”的方式在多地点/多机器间保持目录同步。 尽管如此，它们中的大多数仍然运行存储和转换到老版本的修改过的或者删除的文件.

也可查阅:

*   [List of applications/Utilities#File synchronization](/index.php/List_of_applications/Utilities#File_synchronization "List of applications/Utilities")
*   [List of applications/Internet#Cloud synchronization clients](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet")
*   [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software")

### 说明

	名字

	应用的名字，链接到archwiki文章或者官方网站.

	包

	到包的链接.

	实现

	应用程序基于的编程语言，库或者实用程序.

	增量传输

	仅仅文件修改过的 *部分* 会被传输.

	加密传输

	当通过网络传输时默认加密.

	FS元数据

	文件的权限和属性是同步的 .

	可恢复

	同步能继续，如果被打断的话.

	处理重命名

	移动过/或重命名过的文件会被监测并不会存储或者传输两次. 它通常意味着会计算文件或文件块的校验和.程序如果没有这项功能能通过和 [hsync](https://aur.archlinux.org/packages/hsync/)结合起来来实现, 这个程序 *只做* 同步命名.

	版本控制

	旧版本的文件也被备份了 (*反向增量备份*).

	改变传播

	指定能传播多少地点.

*   *单向* 意味着两地点的单向传播,
*   *双向* 意味着两地点的双向传播
*   *多向* 意味着多地点的完全同步.

	冲突解决方案

	这个程序会要么自动要么交互的处理文件冲突, 即是它不静默的丢弃冲突文件. 这项属性不适应于只支持单方向传播的程序.

	FS监听

	应用程序监听文件系统的变化来触发同步.

	CLI

	应用程序提供命令行界面.

	其它界面

	应用有的特殊用户界面, 比如. GUI, TUI, 或者基于网页.

	证书

	服务器程序和客户端程序的证书.

	其它平台

	不仅仅支持Linux.

	维护

	项目还在被维护.

	特性

	特别是能将应用程序和其它的区分开的特性的说明.

### 表格

| 名字 | 安装包 | 实现 | 增量传输 | 加密传输 | FS元数据 | 可恢复 | 处理重命名 | 版本控制 | 改变传播 | 冲突解决方案 | FS监听 | CLI | 其它界面 | 证书 | 其它平台 | 维护 | 特性 |
| [FreeFileSync](https://www.freefilesync.org/) | [freefilesync](https://aur.archlinux.org/packages/freefilesync/) | C++ | ? | SFTP [[1]](http://www.freefilesync.org/faq.php#features) | ? | ? | Yes [[2]](http://www.freefilesync.org/faq.php#features) | Yes [[3]](http://www.freefilesync.org/manual.php?topic=versioning) | **uni**directional / **multi**directional | Yes | ? | No | Yes | GPL | Windows, macOS | Yes |
| [git-annex](https://git-annex.branchable.com/) | [git-annex](https://www.archlinux.org/packages/?name=git-annex) | Haskell, git | rsync [[4]](http://git-annex.branchable.com/transferring_data/) | rsync [[5]](http://git-annex.branchable.com/transferring_data/) | ? | ? | ? | Yes | **multi**directional; with git remotes [[6]](http://git-annex.branchable.com/sync/) | 重命名冲突文件 [[7]](http://git-annex.branchable.com/automatic_conflict_resolution/) | ? | Yes | [git-annex assistant](http://git-annex.branchable.com/assistant/) | GPLv3 | macOS, Android | Yes | 用git管理文件 |
| [osync.sh](http://www.netpower.fr/osync) | [osync](https://aur.archlinux.org/packages/osync/) | Bash, based on rsync | rsync | rsync | ? | Yes | No | Yes | **bi**directional | 保存多版本的文件 [[8]](http://www.netpower.fr/sites/default/files/soft/html-doc/osync_v1.2.html#toc-Subsubsection-1.3.1) | 可选的 [[9]](https://github.com/deajan/osync#daemon-mode) | Yes | No | BSD | Yes |
| [rclone](https://rclone.org/) | [rclone](https://www.archlinux.org/packages/?name=rclone) | Go | No [[10]](https://rclone.org/faq/#why-doesn-t-rclone-support-partial-transfers-binary-diffs-like-rsync) | ? | ? | ? | ? | ? | **uni**directional [[11]](https://rclone.org/faq/#can-rclone-do-bi-directional-sync) | ? | ? | Yes | [RcloneBrowser](https://github.com/mmozeiko/RcloneBrowser) | MIT | *BSD, Plan9, Solaris, Windows, macOS | Yes | 针对与云存储同步进行了优化, 表现因远程位置支持的特性而异. |
| [rdiff-backup](http://www.nongnu.org/rdiff-backup/) | [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) | Python 2, librsync | rsync | rsync | Yes | ? | No | Yes | **uni**directional | No | Yes | No | GPL | Win32 | ? |
| [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") | [rslsync](https://aur.archlinux.org/packages/rslsync/) | C++ | Yes | Yes | ? | Yes | ? | Yes | **multi**directional | ? | ? | No | Web | Proprietary freemium | FreeBSD, Windows, macOS, Android, iOS, Windows Phone, Amazon Kindle Fire | Yes | P2P 同步 |
| [Rsync (简体中文)](/index.php/Rsync_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Rsync (简体中文)") | [rsync](https://www.archlinux.org/packages/?name=rsync) | C | Yes | SSH or native protocol | Yes | Yes | No | 

*   `--link-dest` with hard links [[12]](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup)
*   `--backup`

 | **uni**directional | No | Yes | [Rsync#Front-ends](/index.php/Rsync#Front-ends "Rsync") | GPLv3 | Win32 | Yes | 在所有Linux发行本上的标准工具. |
| [SparkleShare](https://sparkleshare.org/) | [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare) | C#, git | Yes | AES-256 [[13]](https://github.com/hbons/SparkleShare/wiki/Client-Side-Encryption) | ? | ? | Yes | Yes | ? | ? | ? | No | Yes | GPLv3 | Windows, macOS | Yes | 能通过SSH和任何Git服务器同步. |
| [Syncany](https://www.syncany.org/) | [syncany](https://aur.archlinux.org/packages/syncany/) | Java | ? | ? | ? | ? | ? | ? | ? | ? | ? | Yes | Yes | GPLv3 | No [[14]](https://github.com/syncany/syncany/graphs/contributors) |
| [Syncthing](/index.php/Syncthing "Syncthing") | [syncthing](https://www.archlinux.org/packages/?name=syncthing) | Go | Yes [[15]](http://docs.syncthing.net/users/faq.html#is-synchronization-fast) | Yes [[16]](http://docs.syncthing.net/users/security.html) | partial [[17]](http://docs.syncthing.net/users/faq.html#what-things-are-synced) | Yes | ? | Yes [[18]](http://docs.syncthing.net/users/versioning.html), previous versions moved to archive folder | **multi**directional | 重命名一个文件 [[19]](https://docs.syncthing.net/users/faq.html#what-if-there-is-a-conflict) | Yes | Yes | Web, GTK | MPL v2 | BSD, Windows, macOS, Android, Kindle Paperwhite | Yes | P2P sync |
| [Synkron](http://synkron.sourceforge.net/) | [synkron](https://aur.archlinux.org/packages/synkron/) | C++ | ? | ? | ? | ? | ? | ? | **multi**directional | ? | ? | No | Qt | GPLv2 | Windows, macOS | [No](https://sourceforge.net/projects/synkron/) |
| [taskd](/index.php/Taskd "Taskd") | [taskd](https://aur.archlinux.org/packages/taskd/) | C++, Python | Yes | Yes | ? | Yes | ? | ? | **multi**directional | ? | No | Yes | No | MIT | Android | Yes |
| [Unison (简体中文)](/index.php/Unison_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unison (简体中文)") | [unison](https://www.archlinux.org/packages/?name=unison) | OCaml | Yes | Yes | partial [[20]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#perms) | optional [[21]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#speeding) | No | Yes [[22]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#backups) | **bi**directional | interactive | No | Yes | GTK2 | GPL | FreeBSD, Windows, macOS, Android | Yes [[23]](http://www.cis.upenn.edu/~bcpierce/unison/status.html) |

## 增量备份

那些能 [增量备份](https://en.wikipedia.org/wiki/Incremental_backup "wikipedia:Incremental backup")的程序会记住并考虑上次账户运行期间备份的数据(所谓的 "差异") 并消除重复未更改数据的需要.将数据还原到特定时间点需要定位上次完整备份和所有增量备份到赢应恢复的时刻 . 这种备份方法对经常备份的人很有用.

可查阅:

*   [List of applications/Security#Backup programs](/index.php/List_of_applications/Security#Backup_programs "List of applications/Security")
*   [Wikipedia:List of backup software](https://en.wikipedia.org/wiki/List_of_backup_software "wikipedia:List of backup software")
*   [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software")
*   [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services")

**说明:**

*   **名字**: 应用名字, 链接到archwiki文章或者官方网站.
*   **包**: 链接到安装包.
*   **实现**: 程序基于的编程语言、库或者实用工具.
*   **压缩存储**: 用作存储的压缩方法.
*   **加密存储**: 加密被用作存储.
*   **增量传输**: 只有文件修改过的 *部分* 会被传输.
*   **加密传输**: 当通过网络传输时数据默认加密.
*   **文件系统元数据**: 文件系统权限和属性也备份了.
*   **易访问**: 备份明确地存储在文件系统中，或者可以挂载.
*   **可恢复**: 如果中断备份可以不重启继续.
*   **处理重命名**: 移动/重命名的文件会被监测并不会存储或转移两次; 它通常意味着它会计算文件或文件块的校验和.
*   **命令行**: 应用程序是命令行驱动的，即它可用来编写脚本.
*   **其它界面**: 这个应用有其它特定的用户界面，比如 GUI, TUI, 或者基于网络的接口.
*   **证书**: 服务器或客户端程序的证书.
*   **其它平台**: 除了Linux之外支持的操作系统.
*   **维护**: 这个项目是否还在维护.
*   **特性**: 特别是能将应用程序和其它的区分开的特性的说明.

### 单机器

这些程序针对把数据从它们安装的机器备份, 尽管备份目的可能在外部机器或者是存储媒体.

#### 基于块的增量

如果一个文件被修改, 下次快照这些程序只存储修改过的 *部分* . 与 [#File-based increments](#File-based_increments) 的程序相比, 它们在磁盘方面效率更高, 特别是大文件但是只有小修改; 另一方面,存档的快照必须能用创造它们的备份程序打开 , 因为文件必须从二进制差异中重建.

| 名字 | 包 | 实现 | 压缩存储 | 加密存储 | 增量传输 | 加密传输 | 文件元数据 | 容易访问 | 可恢复 | 处理重命名 | 命令行 | 其他界面 | 证书 | 其它平台 | 维护 | 特性 |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/) | Java | Zip, Zip64 | AES128, AES256 | Yes | Yes | Yes | No | 只可以暂停 | No | Yes | Yes | GPLv2 | Windows | Yes |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Python, C (Cython) | lz4, zlib, lzma, zstd | AES256 | Yes | SSH | Yes [[24]](http://borgbackup.readthedocs.org/en/stable/faq.html#which-file-types-attributes-etc-are-preserved) | Yes [[25]](http://borgbackup.readthedocs.org/en/stable/usage.html#borg-mount) | Yes [[26]](http://borgbackup.readthedocs.org/en/stable/faq.html#if-a-backup-stops-mid-way-does-the-already-backed-up-data-stay-there) | Yes | Yes | third party | BSD | *BSD, macOS, Windows (Cygwin / WSL)[[27]](https://borgbackup.readthedocs.io/en/stable/#main-features) | Yes | 基于可变长度块的重复数据删除；支持本地和基于ssh的远程备份目的地. |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/) | C | Yes | Yes | Yes | Yes | ? | No | ? | ? | Yes | No | GPLv3 | Yes | 冗余、索引提取、多核压缩、输入和输出的序列化、对部分存档错误的容忍度. |
| [bup](https://bup.github.io/) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/) | C, Python, git | Yes | No | Yes | Yes | 不成熟 | Yes [[28]](https://bup.github.io/man/bup-fuse.html) | 在你离开的地方继续 [[29]](https://github.com/bup/bup/blob/master/README.md#reasons-bup-is-awesome) | Yes | Yes | [bups](https://aur.archlinux.org/packages/bups/) | GPLv2 | NetBSD, Windows, macOS | Yes | 和git一样的存储格式. |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/) | C# | Yes | Yes | Yes | Yes | scheduled for 2.0 release | No | Pausing only | No | Yes | Yes | LGPL | Windows | Yes |
| [Duplicity](/index.php/Duplicity "Duplicity") | [duplicity](https://www.archlinux.org/packages/?name=duplicity) | librsync | gzip | gpg | Yes | Yes | ? | No | Yes | No | Yes | [Yes](/index.php/Duplicity#Front-ends "Duplicity") | GPL | Yes |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | Yes | Yes | Yes | Yes | Immature | Yes | No | Yes | bup | Qt | GPLv2 | Yes |
| [obnam](https://obnam.org/) | [obnam](https://aur.archlinux.org/packages/obnam/) | Python | Yes | GnuPG | Yes | Yes | ? | Yes | checkpoints every 100MB | ? | Yes | No | GPLv3 | [No](https://blog.liw.fi/posts/2017/08/13/retiring_obnam/) |
| [restic](https://restic.net/) | [restic](https://www.archlinux.org/packages/?name=restic) [restic-git](https://aur.archlinux.org/packages/restic-git/) | Go | No [[30]](https://github.com/restic/restic/issues/21) | AES-256 [[31]](https://github.com/restic/restic/blob/master/doc/Design.md) | Yes | Yes | Yes [[32]](https://restic.readthedocs.io/en/latest/manual_rest.html#metadata-handling) | Yes [[33]](https://restic.readthedocs.io/en/stable/050_restore.html#restore-using-mount) | Yes [[34]](https://github.com/restic/restic/pull/310) | Yes | Yes | No [[35]](https://github.com/restic/restic/issues/60) | BSD | OpenBSD, Windows, macOS | Yes | 支持多种通过本地或通过 [rclone](https://www.archlinux.org/packages/?name=rclone)的云服务存储. |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/) | C++ | LZMA, LZO | AES | Yes | Yes | ? | planned [[36]](https://github.com/zbackup/zbackup#improvements) | No | Kinda through tar | Yes | No | GPLv2 | Yes | 库由不可变文件组成. |

#### 基于文件的增量

如果文件被修改, 这些文件会在下次快照存储整个版本的文件. 与 [#Chunk-based increments](#Chunk-based_increments) 应用相比, 它们对存储空间的利用率不够高, 特别是备份大文件但是修改小时; 另一方面, 通常存档的快照没有备份程序安装的时候也能打开.

**特殊说明:**

*   **硬链接**: 是否将为修改的文件存储为之前版本的硬链接.

| 名字 | 包 | 实现 | 压缩存储 | 加密存储 | 增量传输 | 加密传输 | 文件系统元数据 | 易访问 | 可恢复 | 处理重命名 | 硬链接 | 命令行 | 其他界面 | 证书 | 其它平台 | 维护 | 特性 |
| [Back In Time](/index.php/Back_In_Time "Back In Time") | [backintime](https://aur.archlinux.org/packages/backintime/) | Python, rsync, diff | No | No | rsync | rsync | rsync | Yes | No | No | Yes [[37]](http://backintime.le-web.org/documentation/) | Yes | Qt | GPLv2 | Yes |
| [DAR](http://dar.linux.free.fr/) (Disk ARchive) | [dar](https://aur.archlinux.org/packages/dar/) | C++ | special archive format | Yes | Yes | Yes | ? | ? | ? | ? | No [[38]](http://dar.linux.free.fr/doc/Features.html) | Yes | [dargui](https://aur.archlinux.org/packages/dargui/) | GPL | FreeBSD, NetBSD, Windows, macOS | Yes |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/) | Python 2 | No | No | ? | SSH | ? | ? | Yes | Yes | No [[39]](http://www.scottlu.com/Content/Link-Backup.html) | Yes | No | MIT | No | 把它自己复制到服务器. |
| [rdup](https://github.com/miekg/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/) | C | tar.gz | gpg, blowfish and others | ? | ? | ? | Yes | ? | No | Yes | Yes | No | GPLv3 | No | 一套命令行工具. |
| [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | [rsnapshot](https://www.archlinux.org/packages/?name=rsnapshot) | rsync | No | No | Yes | Yes | ? | ? | ? | ? | Yes [[40]](http://rsnapshot.org/rsnapshot/docs/docbook/rest.html) | Yes | No | GPLv2 | Win32 | No [[41]](https://github.com/rsnapshot/rsnapshot/issues/191) |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/) | Python | gzip, bzip2 | No | ? | SSH | ? | No | No | No | No | No | GTK | GPLv3 | No |
| [TimeShift](https://github.com/teejee2008/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/) | rsync | No | No | rsync | rsync | ? | ? | ? | ? | Yes | No | GTK | GPLv3 | 专门为完整系统备份到专用设备而设计的. | Yes |

### 面向网络

这些程序被设计为旨在集中链接到网络的多台计算机的备份, 通过一种服务器-客户端模型. 通常，它们部署更复杂, 与 [#Single machine](#Single_machine) 解决方案相比.

**特殊说明:**

*   **控制方向**: 拉取: 服务器登录客户端. 推动: 客户端启动会话.
*   **增量类型**: 通过删除重复数据来减少已用空间的策略 (i.e., 除了压缩之外).
    *   **基于文件**: 如果文件被修改, 整个新版本将存在每个快照中.
        *   **硬链接**: 未修改的文件是否被存为之前版本的硬链接.
    *   **基于块**: 只有文件修改过的 *部分* 被存在每个快照中.

| 名字 | 包 | 实现 | 控制方向 | 压缩存储 | 加密存储 | 增量传输 | 加密传输 | 文件系统元数据 | 易访问 | 可恢复 | 处理重命名 | 增量种类 | 命令行 | 其它界面 | 证书 | 其它平台 | 维护 | 特性 |
| [BackupPC](/index.php/BackupPC "BackupPC") | [backuppc](https://www.archlinux.org/packages/?name=backuppc) | Perl | Pull | Yes | No | Yes | Yes | Yes | No | Yes | ? | 基于文件, 硬链接 [[42]](http://backuppc.sourceforge.net/faq/BackupPC.html#Backup-basics) | No | Web | GPLv2 | 任何平台 (不需要客户端) | Yes | 相同或不同客户端的备份中相同文件仅存储一次. |
| [Bacula](http://www.bacula.org) | [bacula*](https://aur.archlinux.org/packages/?K=bacula) in [AUR](/index.php/AUR "AUR") | C++ | Pull | Yes | Yes | ? | Yes | ? | ? | Yes | ? | 基于文件 [[43]](http://burp.grke.org/why.html) | Yes | GUI, Web | AGPLv3 | Windows, macOS | Yes |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/) | librsync | Push | Yes | Yes | Yes | Yes | Yes | ? | Yes | ? | 基于块 [[44]](http://burp.grke.org/why.html) | Yes | [burp-ui](https://git.ziirish.me/ziirish/burp-ui) | AGPLv3 | Windows, macOS | Yes |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/) | rdiff-backup | Pull | No | No | ? | Yes | ? | ? | ? | ? | 基于块 [[45]](http://safekeep.sourceforge.net/safekeep.html) | Yes | Yes | GPL | No | 与 [LVM](/index.php/LVM "LVM") 和数据库集成以创建一致的备份. 带宽限制. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/) | C | Push or Pull | Yes | No | ? | Yes | ? | ? | ? | ? | 基于文件 [[46]](http://www.snebu.com/#_concepts) | Yes | No | GPLv3 | ? | 支持任意保留计划. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | Multitool wrapper | ? | Yes | No | Yes | Yes | Yes | ? | ? | ? | ? | No | Web | GPLv3 | Yes | 统一许多备份方法. |
| [UrBackup](https://www.urbackup.org) | [urbackup*](https://aur.archlinux.org/packages/?K=urbackup) in [AUR](/index.php/AUR "AUR") | C++ | Pull | No | No | Yes | Internet transfers only | Yes | Yes | Yes | Yes | 基于文件,硬链接和符号链接[[47]](http://blog.urbackup.org/156/symbolically-linking-directories-during-incremental-file-backups)/基于块的 CoW-Snapshots[[48]](http://blog.urbackup.org/83/file-backup-storage-with-btrfs-snapshots) | Yes (client) | GUI, Web | AGPLv3+ | Windows, macOS | Yes | 相同或不同客户端的相同文件的备份只存储一次. 在文件系统快照里集成了 LVM, dattobd 和 btrfs . |

## 版本控制系统

虽然 [版本控制系统](https://en.wikipedia.org/wiki/version_control_system "wikipedia:version control system")大多数时候用于源代码, 但它们可以跟踪目录里的任何文件.

查阅 [List of applications/Utilities#Version control systems](/index.php/List_of_applications/Utilities#Version_control_systems "List of applications/Utilities") 和 [dotfiles](/index.php/Dotfiles "Dotfiles").

## 也可查阅

*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Exhaustive list of backup solutions for Linux](https://github.com/restic/others)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [rsync-snapshot.sh](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) — Local and remote snapshot backup using rsync with hard links
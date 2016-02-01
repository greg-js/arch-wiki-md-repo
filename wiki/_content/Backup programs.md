# Backup programs

Related articles

*   [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync")
*   [Full System Backup with tar](/index.php/Full_System_Backup_with_tar "Full System Backup with tar")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [List of applications#File sharing](/index.php/List_of_applications#File_sharing "List of applications")
*   [Snapper](/index.php/Snapper "Snapper")

This wiki page contains information about various backup programs. It is a good idea to have regular backups of important data, most notably configuration files (`/etc/*`) and the local pacman database (usually `/var/lib/pacman/local/*`).

## Contents

*   [1 Overview](#Overview)
*   [2 Data synchronization](#Data_synchronization)
*   [3 Incremental backups](#Incremental_backups)
*   [4 Cloud storage](#Cloud_storage)
    *   [4.1 Third-party services](#Third-party_services)
        *   [4.1.1 Multi-service clients](#Multi-service_clients)
    *   [4.2 Cooperative](#Cooperative)
    *   [4.3 Custom infrastructure](#Custom_infrastructure)
*   [5 Distributed file systems](#Distributed_file_systems)
*   [6 Data cloning](#Data_cloning)
*   [7 Version control systems](#Version_control_systems)
*   [8 See also](#See_also)

## Overview

Before you start trying various programs out, try to think about your needs, e.g. consider the following questions:

*   What backup medium do I have available? (CD, DVD, remote server, external hard drive, etc.)
*   How often do I plan to backup? (daily, weekly, monthly, etc.)
*   What features do I expect from the backup solution? (compression, encryption, handles renames, etc.)
*   How do I plan to restore backups if needed?

## Data synchronization

These applications simply keep directories synchronized between multiple locations/machines, in a "mirror" fashion. Nonetheless, most of them still allow storing and reverting to old revisions of modified or deleted files.

See also [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software").

*   **Free File Sync** — Free File Sync helps you synchronize files and synchronize folders for Windows, Linux and Mac OS X. It is designed to save your time setting up and running backup jobs while having nice visual feedback along the way.

NaN

*   **git-annex** — Creates a synchronised folder on each of your OSX and Linux computers, Android devices, removable drives, NAS appliances, and cloud services.

NaN

*   **Grsync** — GTK+ interface to rsync

NaN

*   **osync.sh** — Osync is a robust bidirectional file synchronization tool written in bash and based on rsync. It works on local and / or remote directories via ssh tunnels. It's mainly targeted to be launched as cron task, with features turned towards automation among:
    *   Execution time control
    *   Fault tolerance with possibility to resume on error
    *   Soft deletion, on-conflict backups with automatic cleanup
    *   Alert notifications via email
    *   Before and /or after time controlled local and / or remote command execution
    *   File monitor mode

NaN

*   **[rsync](/index.php/Rsync "Rsync")** — A file transfer program to keep remote files in sync.
    *   rsync almost always makes a mirror of the source.
    *   It is possible to restore a full backup before the most recent backup if hardlinks are allowed in the backup file system. See [Back up your data with rsync](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup) for more information.
    *   If hard links are not allowed, it is impossible to restore a full backup before the most recent backup (but you can use --backup to keep old versions of the files).
    *   Standard install on all distros.
    *   Can run over SSH (port 22) or native rsync protocol (port 873).
    *   Win32 version available.

NaN

*   **SparkleShare** — Collaboration and sharing tool based on git written in C Sharp.

NaN

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open-source file synchronization client/server application, written in Go, implementing its own, equally free Block Exchange Protocol.

NaN

*   **Synkron** — A folder synchronization tool.
    *   Syncs multiple folders.
    *   Can exclude files from sync based on wildcards.
    *   Restores files.
    *   Cross-platform support.

NaN

*   **[Unison](/index.php/Unison "Unison")** — A program that synchronizes files between two machines over network (LAN or Inet) using a smart diff method + rsync. Allows the user to interactively choose which changes to push, pull, or merge.

NaN

## Incremental backups

Applications that can do incremental backups remember and take into account what data has been backed up during the last run (so-called "diffs") and eliminate the need to have duplicates of unchanged data. Restoring the data to a certain point in time would require locating the last full backup and all the incremental backups from then to the moment when it is supposed to be restored. This sort of backup is useful for those who do it very often.

Some do not apply compression or encryption: on one hand, a working copy of everything is immediately available, no decompression/decryption needed; a downside to rsync-type programs is that they cannot be easily burned and restored from a CD or DVD.

Others tend to create (big) archive files and (of course) keep track of what has been archived: creating `.tar.bz2` or `.tar.gz` archives has the advantage that you can extract the backups with just tar/bzip2/gzip, so you do not need to have the backup program around.

See also [Dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles").

**Legend:**

*   **Name**: the application name, linking to the official website.
*   **Installation**: a link to the main ArchWiki article, if existing, or directly to the package pages.
*   **Implementation**: the programming language, library, or utility that the application is based on.
*   **Compressed storage**: compression is used for storage.
*   **Encrypted storage**: encryption is used for storage.
*   **Delta transfer**: only the modified _parts_ of files are incrementally backed up.
*   **Encrypted transfer**: data is encrypted by default when transferred over a network.
*   **FS metadata**: file system permissions and attributes are backed up.
*   **FS monitoring**: the file system is monitored for changes to trigger automatic snapshots.
*   **Easy access**: the backup is stored plainly in the file system, or is mountable as such.
*   **Resumable**: the backup can be resumed without restarting it if interrupted.
*   **Handles renames**: moved/renamed files are detected and not reuploaded.
*   **CLI**: the application is command-line driven, i.e. it is scriptable.
*   **Other interfaces**: the application has the specified user interfaces, e.g. GUI, TUI, or web-based.
*   **Licence**: the licence of the server and client applications.
*   **Other platforms**: supported operating systems other than Linux.
*   **Active**: whether the project is currently maintained.
*   **Notes**: additional notes.

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Enter values in the cells marked with "?". Also replace the "Yes" with more specific values. (Discuss in [Talk:Backup programs#](https://wiki.archlinux.org/index.php/Talk:Backup_programs))

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The values in the table need double-checking. (Discuss in [Talk:Backup programs#](https://wiki.archlinux.org/index.php/Talk:Backup_programs))

| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | FS monitoring | Easy access | Resumable | Handles renames | CLI | Other interfaces | Licence | Other platforms | Active | Notes |
| [Arch Backup](http://code.google.com/p/archlinux-stuff/) | [arch-backup](https://www.archlinux.org/packages/?name=arch-backup)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> |  ? | configurable | ? | ? | ? | ? | ? | ? | ? | ? | Yes | No |  ? | ? | Multiple backup targets. |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/)<sup><small>AUR</small></sup> | Java | Zip, Zip64 | AES128, AES256 | Yes | Yes | Yes | No | ? | ? | ? | Yes | Yes | GPLv2 | Windows | Yes |
| [Attic](https://github.com/jborg/attic/) | [attic](https://aur.archlinux.org/packages/attic/)<sup><small>AUR</small></sup> | Python | Yes | AES | Yes | Yes | Yes | No | Yes | Yes | ? | Yes | No | BSD | Yes |
| [Back In Time](https://github.com/bit-team/backintime) | [Back In Time](/index.php/Back_In_Time "Back In Time") | python, rsync, diff | No | No | ? | SSH | ? | ? | ? | ? | ? | No | Qt | GPL | Yes |
| [Backerupper](http://sourceforge.net/projects/backerupper/) | [backerupper](https://aur.archlinux.org/packages/backerupper/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/backerupper)]</sup> |  ? | .tar.gz | No | ? | ? | ? | ? | ? | ? | ? | No | Yes | GPLv2 | No |
| [BackupPC](http://backuppc.sourceforge.net/index.html) | [BackupPC](/index.php/BackupPC "BackupPC") | Perl | Yes | ? | No | Yes | Yes | ? | ? | Yes | ? | No | Web | GPLv2 | Any (no client needed) | Yes | High-performance, enterprise-grade system for backing up Unix, Linux, Windows, and Mac OS X desktops and laptops to a remote server. Deduplication: identical files across multiple backups of the same or different PCs are stored only once resulting in substantial savings in disk storage and disk I/O. |
| [Bacula](http://www.bacula.org) | [bacula-*](https://aur.archlinux.org/packages/?K=bacula-) in [AUR](/index.php/AUR "AUR") | C++ | Yes | Yes | ? | Yes | ? | ? | ? | Yes | ? | Yes | GUI, Web | AGPLv3 | Windows, OS X | Yes |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Attic | Yes | Yes | Yes | SSH | ? | ? | Yes | ? | ? | Yes | No | BSD | *BSD, OS X | Yes | Local caching of files; quick detection of unmodified files. |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/btar)]</sup> | C | Yes | Yes | ? | ? | ? | ? | ? | ? | ? | Yes | No | GPLv3 | Yes | Tar-compatible archiver which allows arbitrary compression and ciphering, redundancy, differential backup, indexed extraction, multicore compression, input and output serialisation, and tolerance to partial archive errors. |
| [bup](https://github.com/bup/bup) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/)<sup><small>AUR</small></sup> | C, Python, git | No | No | Yes | Yes | ? | ? | ? | ? | ? | Yes | third party | GPLv2 | Windows, OS X, NetBSD, Solaris | Yes |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/)<sup><small>AUR</small></sup> | librsync | Yes | Yes | Yes | Yes | ? | ? | ? | ? | ? | Yes | ? | AGPLv3 | Windows | Yes |
| [ColdStorage](http://gitorious.org/coldstorage) | [coldstorage-git](https://aur.archlinux.org/packages/coldstorage-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/coldstorage-git)]</sup> | git | ? | ? | ? | ? | ? | ? | ? | ? | ? | ? | Qt |  ? | ? |
| [DAR](http://dar.linux.free.fr/) | [dar](https://aur.archlinux.org/packages/dar/)<sup><small>AUR</small></sup> [kdar](https://aur.archlinux.org/packages/kdar/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdar)]</sup> (front-end) | C++ | special archive format | Yes | ? | Yes | ? | ? | ? | ? | ? | Yes | DarGUI | GPL | Windows, Solaris, FreeBSD, NetBSD, MacOS X | Yes | Short for Disk ARchive. Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sarab)]</sup>. |
| [DarGUI](http://dargui.sourceforge.net/) | [dargui](https://aur.archlinux.org/packages/dargui/)<sup><small>AUR</small></sup> | DAR front-end | Yes | Yes | ? | Yes | ? | ? | ? | ? | ? | No | GTK |  ? | Windows | No |
| [Déjà Dup](https://launchpad.net/deja-dup) | [Déjà Dup](/index.php/D%C3%A9j%C3%A0_Dup "Déjà Dup") | duplicity | Yes | Yes | ? | Yes | ? | ? | ? | ? | ? | No | GTK+ | GPLv3 | Yes | Integrated into the GNOME Files file manager. |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/)<sup><small>AUR</small></sup> | C# | Yes | Yes | ? | Yes | ? | ? | ? | ? | ? | Yes | Yes | LGPL | Windows | Yes |
| [Duplicity](http://www.nongnu.org/duplicity/) | [Duplicity](/index.php/Duplicity "Duplicity") | librsync | gzip | gpg | ? | Yes | ? | ? | ? | ? | ? | Yes | Duply | GPL | Yes |
| [Duply](http://www.duply.net/) | [Duply](/index.php/Duply "Duply") | duplicity front-end | Yes | Yes | ? | Yes | ? | ? | ? | ? | ? | Yes | No | GPLv2 | Yes |
| [Gibak](https://github.com/pangloss/gibak) | [gibak](https://aur.archlinux.org/packages/gibak/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gibak)]</sup> | git, rsync | Yes | No | Yes | Yes | Yes | ? | ? | ? | ? | Yes | No | GPLv2 | No | Uses all of Git's features (such as `.gitignore` for filtering files). Uses Git's hook system to save information that Git does not (permissions, mtime, empty directories, etc). |
| [gutbackup](https://github.com/gutenye/gutbackup) | [gutbackup](https://aur.archlinux.org/packages/gutbackup/)<sup><small>AUR</small></sup> | rsync wrapper | No | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No | MIT | Yes |
| [hdup](http://miek.nl/projects/hdup2/) | [hdup](/index.php/Hdup "Hdup") |  ? | tar.gz, tar.bz2 | gpg | ? | SSH | ? | ? | ? | ? | ? | Yes | No | GPLv2 | No | Multiple backup targets. |
| [keepconf](https://github.com/rfrail3/keepconf) |  ? | rsync, git | No | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No |  ? | Yes |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | No | No | ? | Yes | ? | ? | ? | ? | ? | No | Qt | GPLv2 | Yes |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/)<sup><small>AUR</small></sup> |  ? | No | No | ? | SSH | ? | ? | ? | Yes | Yes | Yes | No | MIT | No | Similar to rsync-based scripts, but which does not use rsync. It copies itself to the server; it does not need to be installed on the server. It can be told to run for an arbitrary number of minutes. |
| [luckyBackup](http://luckybackup.sourceforge.net/index.html) | [luckybackup](https://aur.archlinux.org/packages/luckybackup/)<sup><small>AUR</small></sup> | C++ | No | No | ? | Yes | ? | ? | ? | ? | ? | limited | Qt | GPLv3 | FreeBSD, Windows, OS X | No |
| [Manent](http://code.google.com/p/manent/) | [manent](https://aur.archlinux.org/packages/manent/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/manent)]</sup> |  ? | ? | Yes | ? | ? | ? | ? | Yes | ? | ? | Yes | No | GPLv3 | Windows | No | Several computers can use the same storage for backup, automatically sharing data. |
| [obnam](http://liw.fi/obnam/) | [obnam](https://aur.archlinux.org/packages/obnam/)<sup><small>AUR</small></sup> |  ? | Yes | GnuPG | Yes | Yes | ? | ? | ? | ? | ? | Yes | No | GPLv3 | Yes | FUSE-mountable backup repository. |
| [Packrat](http://www.zeroflux.org/projects) | [packrat](https://aur.archlinux.org/packages/packrat/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/packrat)]</sup> | DAR wrapper | ? | ? | ? | SSH | ? | ? | ? | ? | ? | Yes | No |  ? | No |
| [rdiff-backup](http://www.nongnu.org/rdiff-backup/) | [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) | librsync | No | No | Yes | Yes | ? | ? | ? | ? | ? | Yes | No | GPL | Win32 | No |
| [rdup](http://miek.nl/projects/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/)<sup><small>AUR</small></sup> | C | tar.gz | gpg, blowfish and others | n/a | n/a | n/a | n/a | n/a | n/a | n/a | Yes | No | GPLv3 | No | Does not backup anything, only prints a list of absolute filenames to standard output. |
| [rsnapshot](http://www.rsnapshot.org/) | [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | rsync | No | No | No | Yes | ? | ? | ? | ? | ? | Yes | No | GPLv2 | Win32 | Yes | Destination filesystem must support hard links. |
| [rsync-snapshot.sh](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) |  ? | rsync | Yes | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No |  ? | ? | Smart rotation (non-linear distribution) of backups, integrity protection, quotas, rules and many more features. |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/)<sup><small>AUR</small></sup> | rdiff-backup | No | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No | GPL | No | Integrates with Linux LVM and databases to create consistent backups. Bandwidth throttling. |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/)<sup><small>AUR</small></sup> | Python | Yes | ? | ? | ? | ? | ? | ? | ? | ? | No | GTK | GPLv3 | Yes | All configuration is accessable via Gnome interface. File and paths can be included and excluded directly or by regex. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/snebu)]</sup> | C | Yes | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No | GPLv3 | ? | Supports arbitrary retention schedules (such as daily/weekly/monthly) which can be individually expired. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | multitool wrapper | Yes | No | ? | Yes | ? | ? | ? | ? | ? | No | Web | GPLv3 | Yes | Meant to unify several backup methods in a single application while supplying a powerful reporting system. |
| [syncBackup](http://www.darhon.com/syncbackup) | [syncbackup](https://aur.archlinux.org/packages/syncbackup/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/syncbackup)]</sup> | C++, rsync front-end | No | No | ? | Yes | ? | ? | ? | ? | ? | No | Qt | GPL | No |
| [TimeShift](https://launchpad.net/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/)<sup><small>AUR</small></sup> | rsync | No | No | ? | Yes | ? | ? | ? | ? | ? | No | GTK | GPLv3 | Yes |
| [trinkup](https://gist.github.com/ei-grad/7610406/) | [trinkup](https://aur.archlinux.org/packages/trinkup/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/trinkup)]</sup> | rsync wrapper | No | No | ? | Yes | ? | ? | ? | ? | ? | Yes | No | DWTFYWWI | Yes |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/)<sup><small>AUR</small></sup> | C++ | LZMA, LZO | AES | ? | ? | ? | ? | ? | ? | ? | Yes | No | GPLv2 | Yes | Repository consists of immutable files. No existing files are ever modified. |
| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | FS monitoring | Easy access | Resumable | Handles renames | CLI | Other interfaces | Licence | Other platforms | Active | Notes |

## Cloud storage

### Third-party services

See also [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services").

*   **Amazon S3** — Amazon Simple Storage Service (Amazon S3), provides developers and IT teams with secure, durable, highly-scalable object storage. Amazon S3 is easy to use, with a simple web service interface to store and retrieve any amount of data from anywhere on the web. With Amazon S3, you pay only for the storage you actually use. There is no minimum fee and no setup cost.

NaN

*   **CloudBacko** — Enterprise-grade cloud backup tool for Linux, Mac and Windows.
    *   Closed source. Free, Lite and Pro versions available.
    *   Written in Java.
    *   Encrypted backup to multiple cloud destinations.
    *   Supports multiple cloud destinations combined as one storage pool.
    *   No installation required in Free version.
    *   GUI frontend for Linux in Pro version.
    *   Virtual machine backup available in Pro version.

NaN

*   **[Copy](https://en.wikipedia.org/wiki/Barracuda_Networks#Products "wikipedia:Barracuda Networks")** — A fair solution to shared folders.
    *   15GB free.
    *   Shared folders size are split between people.
    *   Daemon to sync files between the cloud and the computer.
    *   Almost any platform supported.
    *   Offers AES-256 encryption.

NaN

*   **[CrashPlan](/index.php/CrashPlan "CrashPlan")** — An online/offsite backup solution.
    *   Unlimited online space for very reasonable pricing.
    *   Automatic and incremental backups to multiple destinations.
    *   Intuitive GUI.
    *   Offers encryption and de-duplication.
    *   Software is free for local use.
    *   Restore prevents simultaneous backing up

NaN

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — A popular file-sharing service.
    *   A daemon monitors a specified directory, and uploads incremental changes to dropbox.com.
    *   Changes automatically show up on your other computers.
    *   Includes file sharing and a public directory.
    *   You can recover deleted files.
    *   Community written add-ons.
    *   Free accounts have 2GB storage.

NaN

*   **[Google Drive](https://en.wikipedia.org/wiki/Google_Drive "wikipedia:Google Drive")** — A file storage and synchronization service provided by Google.
    *   Provides cloud storage, file sharing and collaborative editing.
    *   Multiple clients are available.

NaN

*   **[iDrive](https://en.wikipedia.org/wiki/IDrive_Inc. "wikipedia:IDrive Inc.")** — Universal Online Backup.
    *   Multiple Device Backup.
    *   Online File Sync.
    *   Real-Time Backup.
    *   Backup and Access from Mobile Devices.
    *   Remote Manage.
    *   No GUI Front end for Linux, command line based. A wrapper script is available to make it easier to use.

NaN

*   **[Jungle Disk](https://en.wikipedia.org/wiki/Jungle_Disk "wikipedia:Jungle Disk")** — An online backup tool that stores its data in Amazon S3 or Rackspace Cloud Files.
    *   A GNOME Files extension.
    *   Only paid plans available.

NaN

*   **[MEGA](https://en.wikipedia.org/wiki/Mega_(website) "wikipedia:Mega (website)")** — Successor to the MegaUpload file-sharing service.
    *   Free accounts are 50GB with paid plans available for more space.
    *   Offers encryption and de-duplication.
    *   Usually accessed through its web interface but other tools exist.

NaN

*   **Nutstore** — A cloud service that lets you sync and share files anywhere.
    *   Multiple file folders sync.
    *   Service for Chinese users.

NaN

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak")** — An online backup tool for Windows, Mac and Linux users to back up, share, sync, access and store their data.
    *   Free account holds 2GB as a 60-day trial.
    *   Includes file sharing and a public directory.
    *   Incremental backup and sync are both supported.

NaN

*   **[Storage Made Easy](https://en.wikipedia.org/wiki/Storage_Made_Easy "wikipedia:Storage Made Easy")** — Provides unified access to numerous cloud storage services, as well as its own storage.
    *   Free and paid version available.
    *   Free account holds 5GB and allows access to up to three other cloud storage providers.
    *   Supports local directory via fuse, as well as web access.
    *   Supports many cloud storage services, such as Box, Dropbox, Google Drive, Onedrive, and others.

NaN

*   **[Tarsnap](https://en.wikipedia.org/wiki/Tarsnap "wikipedia:Tarsnap")** — A secure online backup service for BSD, Linux, OS X, Solaris and Windows (through Cygwin).
    *   Compressed encrypted backups to Amazon S3 Servers.
    *   Automate via [cron](/index.php/Cron "Cron").
    *   Incremental backups.
    *   Backup any files or directories.
    *   Command line only client.
    *   Pay only for usage (bandwidth and storage).

NaN

*   **[Yandex Disk](/index.php/Yandex_Disk "Yandex Disk")** — Free cloud storage service created by Yandex.ru that gives you access to your photos, videos and documents from any internet-enabled device.

NaN

#### Multi-service clients

*   **[Déjà Dup](/index.php/Duplicity "Duplicity")** — A simple GTK+ backup program. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses duplicity as the backend.
    *   Automatic, timed backup configurable in GUI.
    *   Restore wizard.
    *   Integrated into the GNOME Files file manager.
    *   Inherits several features of duplicity.

NaN

*   **Duplicati** — Backup client that securely stores encrypted, incremental, compressed backups on cloud storage services and remote file servers. It works with Amazon S3, Windows Live SkyDrive, Google Drive (Google Docs), Rackspace Cloud Files or WebDAV, SSH, FTP (and many more). Duplicati is open source and free.

NaN

*   **[Duplicity](/index.php/Duplicity "Duplicity")** — A simple command-line utility which allows encrypted compressed incremental backup to nearly any storage.
    *   Supports gpg encryption and signing.
    *   Supports gzip compression.
    *   Supports full or incremental backups, incremental backup stores only difference between new and old file.
    *   Supports pushing over [many protocols](http://duplicity.nongnu.org/duplicity.1.html#sect7).

NaN

*   **[Duply](/index.php/Duply "Duply")** — Front-end for duplicity which simplifies running it by:
    *   keeping recurring settings in profiles per backup job;
    *   automated import/export of keys between profile and keyring;
    *   enabling batch operations eg. backup_verify_purge;
    *   executing pre/post scripts;
    *   precondition checking for flawless duplicity operation.

NaN

*   **rclone** — Rclone is a command line program to sync files and directories to and from Google Drive, Amazon S3, Openstack Swift / Rackspace cloud files / Memset Memstore, Dropbox, Google Cloud Storage and The local filesystem.

NaN

### Cooperative

A [cooperative storage cloud](https://en.wikipedia.org/wiki/Cooperative_storage_cloud "wikipedia:Cooperative storage cloud") is a decentralized model of networked online storage where data is stored on multiple computers, hosted by the participants cooperating in the cloud.

*   **[Symform](http://www.symform.com)** — A peer-to-peer cloud backup service.
    *   Unlimited free backup in exchange for 2:1 storage space contribution with an always-connected device (at least 80% uptime).
    *   [Payment options exist](http://www.symform.com/our-solutions/pricing/).
    *   First 10GB of backup storage is free (no contribution needed).
    *   In addition to paid support, support plans in exchange for extended contribution (300GB+) exist.
    *   Automatic and incremental backups.
    *   Data is encrypted before leaving the computer, though keys are also stored on the Symform's servers.[[1]](http://virtualserverguy.com/blog/2012/12/19/symform-security-analysis)
    *   Customizable limits for bandwidth consumption.
    *   Ability to have a local copy ("Hot Copy") of the backed up data on a different disk or computer.
    *   Ability to have synchronized folders between nodes (Dropbox-like).
    *   Closed source, using mono. Windows clients available.

NaN

### Custom infrastructure

*   **Cozy** — A personal cloud you can hack, host and delete.

NaN

*   **[OpenStack](/index.php/OpenStack "OpenStack")** — Controls large pools of compute, storage, and networking resources throughout a datacenter, managed through a dashboard or via the OpenStack API. OpenStack works with popular enterprise and open source technologies making it ideal for heterogeneous infrastructure.

NaN

*   **[ownCloud](/index.php/OwnCloud "OwnCloud")** — Software suite that provides a location-independent storage area for data.

NaN

*   **[Pydio](/index.php/Pydio "Pydio")** — Mature open source web application for file sharing and synchronization.

NaN

*   **[Seafile](/index.php/Seafile "Seafile")** — Open source cloud storage system, with advanced support for file syncing, privacy protection and teamwork.

NaN

*   **StackSync** — Open-source scalable Personal Cloud that can adapt to the necessities of organizations. It puts a special emphasis on security by encrypting data on the client side before it is sent to the server.

NaN

*   **Syncany** — Cloud storage and filesharing application with a focus on security and abstraction of storage.

NaN

## Distributed file systems

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [File systems](/index.php/File_systems "File systems").**

**Notes:** Somebody knowledgeable on clustered/distributed file systems should consider the merge. (Discuss in [Talk:Backup programs#Distributed file systems](https://wiki.archlinux.org/index.php/Talk:Backup_programs#Distributed_file_systems))

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Is the section heading correct? Is this a too heteregenous group of software pieces? (Discuss in [Talk:Backup programs#Distributed file systems](https://wiki.archlinux.org/index.php/Talk:Backup_programs#Distributed_file_systems))

*   **[Ceph](/index.php/Ceph "Ceph")** — Distributed object store and file system designed to provide excellent performance, reliability and scalability.

NaN

*   **GlusterFS** — Cluster file system capable of scaling to several peta-bytes.

NaN

*   **Sheepdog** — Distributed object storage system for volume and container services and manages the disks and nodes intelligently.

NaN

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

NaN

## Data cloning

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Disk cloning#Disk cloning software](/index.php/Disk_cloning#Disk_cloning_software "Disk cloning").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Backup programs#](https://wiki.archlinux.org/index.php/Talk:Backup_programs))

Another type of backups are those used in case of a disaster. These include application that allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. The contains complete system images from one or more specific points in time and are frequently used by to record known good configurations.

See also [Disk cloning](/index.php/Disk_cloning "Disk cloning").

*   **[Areca Backup](https://en.wikipedia.org/wiki/Areca_Backup "wikipedia:Areca Backup")** — An easy to use and reliable backup solution for Linux and Windows.
    *   Written in Java.
    *   Primarily archive-based (zip), but will do file-based backup as well.
    *   Delta backup supported (stores only changes).

NaN

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive, or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.

NaN

*   **[DAR](https://en.wikipedia.org/wiki/DAR_(Disk_Archiver) "wikipedia:DAR (Disk Archiver)")** — A full-featured command-line backup tool, short for Disk ARchive.
    *   It uses its own format for archives (so you need to have it around when you want to restore).
    *   Supports splitting backups into more files by size.
    *   Makefile-type config files, some custom scripts are available along with it.
    *   Supports basic encryption.
    *   Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sarab)]</sup>.

NaN

*   **FSArchiver** — A safe and flexible file-system backup and deployment tool
    *   Support for basic file attributes (permissions, owner, ...).
    *   Support for multiple file-systems per archive.
    *   Support for extended attributes (they are used by SELinux).
    *   Support the basic file-system attributes (label, uuid, block-size) for all linux file-systems.
    *   Support for [ntfs filesystems](http://www.fsarchiver.org/Cloning-ntfs) (ability to create flexible clones of a Windows partitions).
    *   Checksumming of everything which is written in the archive (headers, data blocks, whole files).
    *   Ability to restore an archive which is corrupt (it will just skip the current file).
    *   Multi-threaded lzo, gzip, bzip2, lzma compression.
    *   Support for splitting large archives into several files with a fixed maximum size.
    *   Encryption of the archive using a password. Based on blowfish from libcrypto from [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Support backup of a mounted root filesystem (-A option).

NaN

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — A disaster recovery solution to create backup media that can be used to redeploy the damaged system.
    *   Image-based backups, supporting Linux/Windows.
    *   Compression rate is adjustable.
    *   Can backup live systems (without having to halt it).
    *   Can split image over many files.
    *   Supports booting to a Live CD to perform a full restore.
    *   Can backup/restore over NFS, from CDs, tape drives and and other media.
    *   Can verify backups.

NaN

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports ext2, ext3, hfs+, reiser3.5, reiser3.6, reiser4, ext4 and btrfs.
    *   Supports compression.

NaN

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — A disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.

NaN

*   **Q7Z** — P7Zip GUI for Linux, which attempts to simplify data compression and backup. It can create the following archive types: 7z, BZip2, Zip, GZip, Tar.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

NaN

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

NaN

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   CLI and Dialog interfaces
    *   Easy backup and restore wizards
    *   Creates _.tar.gz_, _.tar.bz2_, _.tar.xz_ or _.tar_ archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2, Syslinux, EFISTUB/efibootmgr and Systemd/bootctl

NaN

## Version control systems

These are traditionally used for keeping track of software development; but if you want to have a simple way to manage your config files in one directory, it might be a good solution.

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Bazaar](https://en.wikipedia.org/wiki/Bazaar_(software) "wikipedia:Bazaar (software)")** — A distributed version control system that helps you track project history over time and to collaborate easily with others.
    *   Similar commands to Subversion.
    *   Supports working with or without a central server.
    *   Support for working with some other revision control systems
    *   Complete Unicode support.

NaN

*   **[Darcs](https://en.wikipedia.org/wiki/Darcs "wikipedia:Darcs")** — A distributed revision control system that was designed to replace traditional, centralized source control systems such as CVS and Subversion.
    *   Offline mode.
    *   Easy branching and merging.
    *   Written in Haskell.
    *   Not very fast.

NaN

*   **[Git](/index.php/Git "Git")** — A distributed revision control and source code management system with an emphasis on speed.
    *   Very easy creation, merging, and deletion of branches.
    *   Nearly all operations are performed locally, giving it a huge speed advantage on centralized systems.
    *   Has a "staging area" or "index", this is an intermediate area where commits can be formatted and reviewed before completing the commit.
    *   Does not handle binary files very well.

NaN

*   **[Mercurial](/index.php/Mercurial "Mercurial")** — A distributed version control system written in Python and similar in many ways to Git.
    *   Platform independent.
    *   Support for [extensions](http://mercurial.selenic.com/wiki/UsingExtensions).
    *   A set of commands consistent with Subversion.
    *   Supports tags.

NaN

*   **[Subversion](/index.php/Subversion "Subversion")** — A full-featured centralized version control system originally designed to be a better CVS.
    *   Renamed/copied/moved/removed files retain full revision history.
    *   Native support for binary files, with space-efficient binary-diff storage.
    *   Costs proportional to change size, not to data size.
    *   Allows arbitrary metadata ("properties") to be attached to any file or directory.

NaN

## See also

*   [Wikipedia:List of backup software](https://en.wikipedia.org/wiki/List_of_backup_software "wikipedia:List of backup software")
*   [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software")
*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Backup_programs&oldid=418624](https://wiki.archlinux.org/index.php?title=Backup_programs&oldid=418624)"
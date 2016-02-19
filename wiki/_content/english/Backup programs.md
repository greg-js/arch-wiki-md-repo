Having backups of important data is a necessary measure to take, since human and machine processing errors are very likely to generate corruption as time passes, and also the physical media where the data is stored is inevitably destined to fail. This page introduces many applications available for the task, subdivided in categories to best suit most use cases.

## Contents

*   [1 Overview](#Overview)
*   [2 Data synchronization](#Data_synchronization)
*   [3 Incremental backups](#Incremental_backups)
    *   [3.1 Single machine](#Single_machine)
    *   [3.2 Network oriented](#Network_oriented)
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

*   **[BitTorrent Sync](/index.php/BitTorrent_Sync "BitTorrent Sync")** — File sharing system that relies on the BitTorrent protocol.

	[https://www.getsync.com/](https://www.getsync.com/) || [btsync](https://aur.archlinux.org/packages/btsync/)

*   **Free File Sync** — Free File Sync helps you synchronize files and synchronize folders for Windows, Linux and Mac OS X. It is designed to save your time setting up and running backup jobs while having nice visual feedback along the way.

	[http://freefilesync.sourceforge.net/](http://freefilesync.sourceforge.net/) || [freefilesync](https://aur.archlinux.org/packages/freefilesync/)

*   **git-annex** — Creates a synchronised folder on each of your OSX and Linux computers, Android devices, removable drives, NAS appliances, and cloud services.

	[http://git-annex.branchable.com/](http://git-annex.branchable.com/) || [git-annex](https://www.archlinux.org/packages/?name=git-annex)

*   **Grsync** — GTK+ interface to rsync

	[http://www.opbyte.it/grsync/](http://www.opbyte.it/grsync/) || [grsync](https://www.archlinux.org/packages/?name=grsync)

*   **gutbackup** — The simplest rsync wrapper for backup Linux system.

	[https://github.com/gutenye/gutbackup](https://github.com/gutenye/gutbackup) || [gutbackup](https://aur.archlinux.org/packages/gutbackup/)

*   **osync.sh** — Osync is a robust bidirectional file synchronization tool written in bash and based on rsync. It works on local and / or remote directories via ssh tunnels. It's mainly targeted to be launched as cron task, with features turned towards automation among:
    *   Execution time control
    *   Fault tolerance with possibility to resume on error
    *   Soft deletion, on-conflict backups with automatic cleanup
    *   Alert notifications via email
    *   Before and /or after time controlled local and / or remote command execution
    *   File monitor mode

	[http://www.netpower.fr/osync](http://www.netpower.fr/osync) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[rdiff-backup](https://en.wikipedia.org/wiki/Rsync#Variations "wikipedia:Rsync")** — A utility for local/remote mirroring and reverse incremental backups.
    *   Stores the most recent backup as regular files.
    *   To revert to older versions, you apply the diff files to recreate the older versions.
    *   It is granularly incremental (delta backup), it only stores changes to a file; will not create a new copy of a file upon change.
    *   Win32 version available.

	[http://www.nongnu.org/rdiff-backup/](http://www.nongnu.org/rdiff-backup/) || [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup)

*   **[rsync](/index.php/Rsync "Rsync")** — A file transfer program to keep remote files in sync.
    *   rsync almost always makes a mirror of the source.
    *   It is possible to restore a full backup before the most recent backup if hardlinks are allowed in the backup file system. See [Back up your data with rsync](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup) for more information.
    *   If hard links are not allowed, it is impossible to restore a full backup before the most recent backup (but you can use --backup to keep old versions of the files).
    *   Standard install on all distros.
    *   Can run over SSH (port 22) or native rsync protocol (port 873).
    *   Win32 version available.

	[http://rsync.samba.org/](http://rsync.samba.org/) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **SparkleShare** — Collaboration and sharing tool based on git written in C Sharp.

	[http://sparkleshare.org/](http://sparkleshare.org/) || [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare)

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open-source file synchronization client/server application, written in Go, implementing its own, equally free Block Exchange Protocol.

	[https://syncthing.net/](https://syncthing.net/) || [syncthing](https://www.archlinux.org/packages/?name=syncthing) [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk)

*   **Synkron** — A folder synchronization tool.
    *   Syncs multiple folders.
    *   Can exclude files from sync based on wildcards.
    *   Restores files.
    *   Cross-platform support.

	[http://synkron.sourceforge.net/](http://synkron.sourceforge.net/) || [synkron](https://aur.archlinux.org/packages/synkron/)

*   **[Unison](/index.php/Unison "Unison")** — A program that synchronizes files between two machines over network (LAN or Inet) using a smart diff method + rsync. Allows the user to interactively choose which changes to push, pull, or merge.

	[http://www.cis.upenn.edu/~bcpierce/unison/](http://www.cis.upenn.edu/~bcpierce/unison/) || [unison](https://www.archlinux.org/packages/?name=unison)

## Incremental backups

Applications that can do incremental backups remember and take into account what data has been backed up during the last run (so-called "diffs") and eliminate the need to have duplicates of unchanged data. Restoring the data to a certain point in time would require locating the last full backup and all the incremental backups from then to the moment when it is supposed to be restored. This sort of backup is useful for those who do it very often.

Some do not apply compression or encryption: on one hand, a working copy of everything is immediately available, no decompression/decryption needed; a downside to this type of programs is that they cannot be easily burned and restored from a CD or DVD.

Others tend to create (big) archive files and (of course) keep track of what has been archived: creating `.tar.bz2` or `.tar.gz` archives has the advantage that you can extract the backups with just tar/bzip2/gzip, so you do not need to have the backup program around.

See also [Dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles").

**Legend:**

*   **Name**: the application name, linking to the official website.
*   **Installation**: a link to the main ArchWiki article, if existing, or directly to the package pages.
*   **Implementation**: the programming language, library, or utility that the application is based on.
*   **Compressed storage**: compression is used for storage.
*   **Encrypted storage**: encryption is used for storage.
*   **Delta transfer**: only the modified *parts* of files are transferred.
*   **Encrypted transfer**: data is encrypted by default when transferred over a network.
*   **FS metadata**: file system permissions and attributes are backed up.
*   **Easy access**: the backup is stored plainly in the file system, or is mountable as such.
*   **Resumable**: the backup can be resumed without restarting it if interrupted.
*   **Handles renames**: moved/renamed files are detected and not stored or transferred twice; it typically means that a checksum is computed for files or chunks thereof.
*   **CLI**: the application is command-line driven, i.e. it is scriptable.
*   **Other interfaces**: the application has the specified user interfaces, e.g. GUI, TUI, or web-based.
*   **Increment type**: the strategy used to reduce used space by deduplicating data (i.e., besides compression).
    *   **file-based**: if a file is modified, the entire new version is stored at each snapshot.
        *   **hard-links**: unmodified files are stored as hard links to previous versions.
    *   **chunk-based**: only the modified *parts* of files are stored at each snapshot.
*   **Licence**: the licence of the server and client applications.
*   **Other platforms**: supported operating systems other than Linux.
*   **Active**: whether the project is currently maintained.
*   **Specificity**: brief notes about special features that notably set the application apart from the others.

### Single machine

These applications are aimed at backing up data from the machine they are installed on, although the backup destination can be located on an external machine or storage media.

| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Increment type | Licence | Other platforms | Active | Specificity |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/) | Java | Zip, Zip64 | AES128, AES256 | Yes | Yes | Yes | No | Pausing only | No | Yes | Yes | chunk-based | GPLv2 | Windows | Yes |
| [Attic](https://github.com/jborg/attic/) | [attic](https://aur.archlinux.org/packages/attic/) | Python | Yes | AES256 | Yes | SSH | Yes | Yes | Yes | Yes | Yes | No | chunk-based | BSD | Yes |
| [Back In Time](https://github.com/bit-team/backintime) | [Back In Time](/index.php/Back_In_Time "Back In Time") | Python, rsync, diff | No | No | rsync | rsync | rsync | Yes | No | No | No | Qt | file-based, hard links | GPL | Yes |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Python (Attic fork) | lz4, zlib, lzma | AES256 | Yes | SSH | Yes[[1]](http://borgbackup.readthedocs.org/en/stable/faq.html#which-file-types-attributes-etc-are-preserved) | Yes | Yes[[2]](http://borgbackup.readthedocs.org/en/stable/faq.html#if-a-backup-stops-mid-way-does-the-already-backed-up-data-stay-there) | Yes | Yes | No | chunk-based | BSD | *BSD, OS X | Yes |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/) | C | Yes | Yes | Yes | Yes | ? | ? | ? | ? | Yes | No | chunk-based (optional) | GPLv3 | Yes | Redundancy, indexed extraction, multicore compression, input and output serialisation, tolerance to partial archive errors. |
| [bup](https://bup.github.io/) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/) | C, Python, git | No | No | Yes | Yes | ? | ? | ? | ? | Yes | third party | chunk-based | GPLv2 | Windows, OS X, NetBSD, Solaris | Yes |
| [DAR](http://dar.linux.free.fr/) (Disk ARchive) | [dar](https://aur.archlinux.org/packages/dar/) | C++ | special archive format | Yes | ? | Yes | ? | ? | ? | ? | Yes | DarGUI | file-based | GPL | Windows, Solaris, FreeBSD, NetBSD, MacOS X | Yes | Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/). |
| [DarGUI](http://dargui.sourceforge.net/) | [dargui](https://aur.archlinux.org/packages/dargui/) | DAR front-end | Yes | Yes | ? | Yes | ? | ? | ? | ? | No | GTK | file-based | GPL | Windows | ? |
| [Déjà Dup](https://launchpad.net/deja-dup) | [Déjà Dup](/index.php/D%C3%A9j%C3%A0_Dup "Déjà Dup") | duplicity front-end | Yes | Yes | Yes | Yes | ? | ? | ? | ? | No | GTK+ | chunk-based | GPLv3 | Yes | Integrated into [GNOME Files](/index.php/GNOME_Files "GNOME Files"). |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/) | C# | Yes | Yes | Yes | Yes | ? | ? | ? | ? | Yes | Yes | chunk-based | LGPL | Windows | Yes |
| [Duplicity](http://www.nongnu.org/duplicity/) | [Duplicity](/index.php/Duplicity "Duplicity") | librsync | gzip | gpg | Yes | Yes | ? | ? | ? | ? | Yes | Déjà Dup, Duply | chunk-based | GPL | Yes |
| [Duply](http://www.duply.net/) | [Duply](/index.php/Duply "Duply") | duplicity front-end | Yes | Yes | Yes | Yes | ? | ? | ? | ? | Yes | No | chunk-based | GPLv2 | Yes |
| [hdup](http://miek.nl/projects/hdup2/) | [hdup](/index.php/Hdup "Hdup") | C | tar.gz, tar.bz2 | gpg | ? | SSH | ? | ? | ? | ? | Yes | No |  ? | GPLv2 | No | Multiple backup targets. |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | No | No | ? | Yes | ? | ? | ? | ? | No | Qt |  ? | GPLv2 | Yes |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/) | Python | No | No | ? | SSH | ? | ? | Yes | Yes | Yes | No |  ? | MIT | No | It copies itself to the server. |
| [luckyBackup](http://luckybackup.sourceforge.net/index.html) | [luckybackup](https://aur.archlinux.org/packages/luckybackup/) | C++ | No | No | ? | Yes | ? | ? | ? | ? | limited | Qt |  ? | GPLv3 | FreeBSD, Windows, OS X | No |
| [obnam](http://liw.fi/obnam/) | [obnam](https://aur.archlinux.org/packages/obnam/) | Python | Yes | GnuPG | Yes | Yes | ? | Yes | ? | ? | Yes | No |  ? | GPLv3 | Yes |
| [rdup](https://github.com/miekg/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/) | C | tar.gz | gpg, blowfish and others | ? | ? | ? | ? | ? | ? | Yes | No |  ? | GPLv3 | No | Set of simple command-line tools. |
| [rsnapshot](http://www.rsnapshot.org/) | [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | rsync | No | No | Yes | Yes | ? | ? | ? | ? | Yes | No | file-based, hard links | GPLv2 | Win32 | Yes |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/) | Python | Yes | ? | ? | ? | ? | ? | ? | ? | No | GTK |  ? | GPLv3 | Yes |
| [syncBackup](http://www.darhon.com/syncbackup) | [syncbackup](https://aur.archlinux.org/packages/syncbackup/) | C++, rsync front-end | No | No | ? | Yes | ? | ? | ? | ? | No | Qt |  ? | GPL | No |
| [TimeShift](https://launchpad.net/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/) | rsync | No | No | ? | Yes | ? | ? | ? | ? | No | GTK |  ? | GPLv3 | Yes |
| [trinkup](https://gist.github.com/ei-grad/7610406/) | [trinkup](https://aur.archlinux.org/packages/trinkup/) | rsync wrapper | No | No | ? | Yes | ? | ? | ? | ? | Yes | No |  ? | DWTFYWWI | Yes |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/) | C++ | LZMA, LZO | AES | ? | ? | ? | ? | ? | ? | Yes | No |  ? | GPLv2 | Yes | Repository consists of immutable files. |
| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Increment type | Licence | Other platforms | Active | Specificity |

### Network oriented

These applications have been designed to centralize the backup of several machines connected to a network, through a server-client model. In general they are more complicated to deploy, compared to [#Single machine](#Single_machine) solutions.

| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Increment type | Licence | Other platforms | Active | Specificity |
| [BackupPC](http://backuppc.sourceforge.net/index.html) | [BackupPC](/index.php/BackupPC "BackupPC") | Perl | Yes | No | Yes | Yes | Yes | No | Yes | ? | No | Web | file-based, hard links | GPLv2 | Any (no client needed) | Yes | Identical files across backups of the same or different clients are stored only once. |
| [Bacula](http://www.bacula.org) | [bacula-*](https://aur.archlinux.org/packages/?K=bacula-) in [AUR](/index.php/AUR "AUR") | C++ | Yes | Yes | ? | Yes | ? | ? | Yes | ? | Yes | GUI, Web |  ? | AGPLv3 | Windows, OS X | Yes |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/) | librsync | Yes | Yes | Yes | Yes | ? | ? | ? | ? | Yes | [burp-ui](https://git.ziirish.me/ziirish/burp-ui) |  ? | AGPLv3 | Windows | Yes |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/) | rdiff-backup | No | No | ? | Yes | ? | ? | ? | ? | Yes | No |  ? | GPL | No | Integrates with [LVM](/index.php/LVM "LVM") and databases to create consistent backups. Bandwidth throttling. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/) | C | Yes | No | ? | Yes | ? | ? | ? | ? | Yes | No |  ? | GPLv3 | ? | Supports arbitrary retention schedules. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | Multitool wrapper | Yes | No | Yes | Yes | Yes | ? | ? | ? | No | Web |  ? | GPLv3 | Yes | Unifies several backup methods. |
| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Increment type | Licence | Other platforms | Active | Specificity |

## Cloud storage

### Third-party services

See also [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services").

*   **Amazon S3** — Amazon Simple Storage Service (Amazon S3), provides developers and IT teams with secure, durable, highly-scalable object storage. Amazon S3 is easy to use, with a simple web service interface to store and retrieve any amount of data from anywhere on the web. With Amazon S3, you pay only for the storage you actually use. There is no minimum fee and no setup cost.

	[http://aws.amazon.com/s3/](http://aws.amazon.com/s3/) || [s3cmd](https://www.archlinux.org/packages/?name=s3cmd)

*   **CloudBacko** — Enterprise-grade cloud backup tool for Linux, Mac and Windows.
    *   Closed source. Free, Lite and Pro versions available.
    *   Written in Java.
    *   Encrypted backup to multiple cloud destinations.
    *   Supports multiple cloud destinations combined as one storage pool.
    *   No installation required in Free version.
    *   GUI frontend for Linux in Pro version.
    *   Virtual machine backup available in Pro version.

	[http://www.cloudbacko.com/](http://www.cloudbacko.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[CrashPlan](/index.php/CrashPlan "CrashPlan")** — An online/offsite backup solution.
    *   Unlimited online space for very reasonable pricing.
    *   Automatic and incremental backups to multiple destinations.
    *   Intuitive GUI.
    *   Offers encryption and de-duplication.
    *   Software is free for local use.
    *   Restore prevents simultaneous backing up

	[http://www.crashplan.com/](http://www.crashplan.com/) || [crashplan](https://aur.archlinux.org/packages/crashplan/)

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — A popular file-sharing service.
    *   A daemon monitors a specified directory, and uploads incremental changes to dropbox.com.
    *   Changes automatically show up on your other computers.
    *   Includes file sharing and a public directory.
    *   You can recover deleted files.
    *   Community written add-ons.
    *   Free accounts have 2GB storage.

	[http://www.dropbox.com](http://www.dropbox.com) || [dropbox](https://aur.archlinux.org/packages/dropbox/) [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/)

*   **[Google Drive](https://en.wikipedia.org/wiki/Google_Drive "wikipedia:Google Drive")** — A file storage and synchronization service provided by Google.
    *   Provides cloud storage, file sharing and collaborative editing.
    *   Multiple clients are available.

	[https://drive.google.com](https://drive.google.com) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/) (free), [drive](https://aur.archlinux.org/packages/drive/) (free), [grive](https://aur.archlinux.org/packages/grive/) (free), [insync](/index.php/Insync "Insync") (non-free)

*   **[iDrive](https://en.wikipedia.org/wiki/IDrive_Inc. "wikipedia:IDrive Inc.")** — Universal Online Backup.
    *   Multiple Device Backup.
    *   Online File Sync.
    *   Real-Time Backup.
    *   Backup and Access from Mobile Devices.
    *   Remote Manage.
    *   No GUI Front end for Linux, command line based. A wrapper script is available to make it easier to use.

	[https://www.idrive.com/](https://www.idrive.com/) || [idevsutil](https://aur.archlinux.org/packages/idevsutil/), [idrive-wrapper](https://aur.archlinux.org/packages/idrive-wrapper/)

*   **[Jungle Disk](https://en.wikipedia.org/wiki/Jungle_Disk "wikipedia:Jungle Disk")** — An online backup tool that stores its data in Amazon S3 or Rackspace Cloud Files.
    *   A GNOME Files extension.
    *   Only paid plans available.

	[http://www.jungledisk.com/](http://www.jungledisk.com/) || [nautilus-jungledisk](https://aur.archlinux.org/packages/nautilus-jungledisk/)

*   **[MEGA](https://en.wikipedia.org/wiki/Mega_(website) "wikipedia:Mega (website)")** — Successor to the MegaUpload file-sharing service.
    *   Free accounts are 50GB with paid plans available for more space.
    *   Offers encryption and de-duplication.
    *   Usually accessed through its web interface but other tools exist.

	[https://mega.co.nz](https://mega.co.nz) || [megatools](https://aur.archlinux.org/packages/megatools/), [megasync](https://aur.archlinux.org/packages/megasync/), [megafuse](https://aur.archlinux.org/packages/megafuse/)

*   **Nutstore** — A cloud service that lets you sync and share files anywhere.
    *   Multiple file folders sync.
    *   Service for Chinese users.

	[http://jianguoyun.com/](http://jianguoyun.com/) || [nutstore](https://aur.archlinux.org/packages/nutstore/)

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak")** — An online backup tool for Windows, Mac and Linux users to back up, share, sync, access and store their data.
    *   Free account holds 2GB as a 60-day trial.
    *   Includes file sharing and a public directory.
    *   Incremental backup and sync are both supported.

	[https://spideroak.com/](https://spideroak.com/) || [spideroak-one](https://aur.archlinux.org/packages/spideroak-one/)

*   **[Storage Made Easy](https://en.wikipedia.org/wiki/Storage_Made_Easy "wikipedia:Storage Made Easy")** — Provides unified access to numerous cloud storage services, as well as its own storage.
    *   Free and paid version available.
    *   Free account holds 5GB and allows access to up to three other cloud storage providers.
    *   Supports local directory via fuse, as well as web access.
    *   Supports many cloud storage services, such as Box, Dropbox, Google Drive, Onedrive, and others.

	[http://storagemadeeasy.com/](http://storagemadeeasy.com/) || [smestorage](https://aur.archlinux.org/packages/smestorage/)

*   **[Tarsnap](https://en.wikipedia.org/wiki/Tarsnap "wikipedia:Tarsnap")** — A secure online backup service for BSD, Linux, OS X, Solaris and Windows (through Cygwin).
    *   Compressed encrypted backups to Amazon S3 Servers.
    *   Automate via [cron](/index.php/Cron "Cron").
    *   Incremental backups.
    *   Backup any files or directories.
    *   Command line only client.
    *   Pay only for usage (bandwidth and storage).

	[http://www.tarsnap.com](http://www.tarsnap.com) || [tarsnap](https://www.archlinux.org/packages/?name=tarsnap)

*   **[Yandex Disk](/index.php/Yandex_Disk "Yandex Disk")** — Free cloud storage service created by Yandex.ru that gives you access to your photos, videos and documents from any internet-enabled device.

	[https://disk.yandex.ru/](https://disk.yandex.ru/) || [yandex-disk](https://aur.archlinux.org/packages/yandex-disk/)

#### Multi-service clients

*   **[Déjà Dup](/index.php/Duplicity "Duplicity")** — A simple GTK+ backup program. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses duplicity as the backend.
    *   Automatic, timed backup configurable in GUI.
    *   Restore wizard.
    *   Integrated into the GNOME Files file manager.
    *   Inherits several features of duplicity.

	[https://launchpad.net/deja-dup](https://launchpad.net/deja-dup) || [deja-dup](https://www.archlinux.org/packages/?name=deja-dup)

*   **Duplicati** — Backup client that securely stores encrypted, incremental, compressed backups on cloud storage services and remote file servers. It works with Amazon S3, Windows Live SkyDrive, Google Drive (Google Docs), Rackspace Cloud Files or WebDAV, SSH, FTP (and many more). Duplicati is open source and free.

	[http://www.duplicati.com/](http://www.duplicati.com/) || [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/)

*   **[Duplicity](/index.php/Duplicity "Duplicity")** — A simple command-line utility which allows encrypted compressed incremental backup to nearly any storage.
    *   Supports gpg encryption and signing.
    *   Supports gzip compression.
    *   Supports full or incremental backups, incremental backup stores only difference between new and old file.
    *   Supports pushing over [many protocols](http://duplicity.nongnu.org/duplicity.1.html#sect7).

	[http://www.nongnu.org/duplicity/](http://www.nongnu.org/duplicity/) || [duplicity](https://www.archlinux.org/packages/?name=duplicity)

*   **[Duply](/index.php/Duply "Duply")** — Front-end for duplicity which simplifies running it by:
    *   keeping recurring settings in profiles per backup job;
    *   automated import/export of keys between profile and keyring;
    *   enabling batch operations eg. backup_verify_purge;
    *   executing pre/post scripts;
    *   precondition checking for flawless duplicity operation.

	[http://www.duply.net/](http://www.duply.net/) || [duply](https://aur.archlinux.org/packages/duply/)

*   **rclone** — Rclone is a command line program to sync files and directories to and from Google Drive, Amazon S3, Openstack Swift / Rackspace cloud files / Memset Memstore, Dropbox, Google Cloud Storage and The local filesystem.

	[http://rclone.org/](http://rclone.org/) || [rclone](https://www.archlinux.org/packages/?name=rclone)

### Cooperative

A [cooperative storage cloud](https://en.wikipedia.org/wiki/Cooperative_storage_cloud "wikipedia:Cooperative storage cloud") is a decentralized model of networked online storage where data is stored on multiple computers, hosted by the participants cooperating in the cloud.

*   **[Symform](http://www.symform.com)** — A peer-to-peer cloud backup service.
    *   Unlimited free backup in exchange for 2:1 storage space contribution with an always-connected device (at least 80% uptime).
    *   [Payment options exist](http://www.symform.com/our-solutions/pricing/).
    *   First 10GB of backup storage is free (no contribution needed).
    *   In addition to paid support, support plans in exchange for extended contribution (300GB+) exist.
    *   Automatic and incremental backups.
    *   Data is encrypted before leaving the computer, though keys are also stored on the Symform's servers.[[3]](http://virtualserverguy.com/blog/2012/12/19/symform-security-analysis)
    *   Customizable limits for bandwidth consumption.
    *   Ability to have a local copy ("Hot Copy") of the backed up data on a different disk or computer.
    *   Ability to have synchronized folders between nodes (Dropbox-like).
    *   Closed source, using mono. Windows clients available.

	[http://www.symform.com/](http://www.symform.com/) || [symform](https://aur.archlinux.org/packages/symform/)

### Custom infrastructure

*   **Cozy** — A personal cloud you can hack, host and delete.

	[https://cozy.io](https://cozy.io) || [cozy-standalone](https://aur.archlinux.org/packages/cozy-standalone/) [cozy-nginx](https://aur.archlinux.org/packages/cozy-nginx/) [cozy-apache](https://aur.archlinux.org/packages/cozy-apache/)

*   **[OpenStack](/index.php/OpenStack "OpenStack")** — Controls large pools of compute, storage, and networking resources throughout a datacenter, managed through a dashboard or via the OpenStack API. OpenStack works with popular enterprise and open source technologies making it ideal for heterogeneous infrastructure.

	[http://www.openstack.org/](http://www.openstack.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[ownCloud](/index.php/OwnCloud "OwnCloud")** — Software suite that provides a location-independent storage area for data.

	[http://owncloud.org/](http://owncloud.org/) || [owncloud](https://www.archlinux.org/packages/?name=owncloud)

*   **[Pydio](/index.php/Pydio "Pydio")** — Mature open source web application for file sharing and synchronization.

	[https://pydio.com/](https://pydio.com/) || [pydio](https://aur.archlinux.org/packages/pydio/)

*   **[Seafile](/index.php/Seafile "Seafile")** — Open source cloud storage system, with advanced support for file syncing, privacy protection and teamwork.

	[http://seafile.com/](http://seafile.com/) || [seafile-server](https://aur.archlinux.org/packages/seafile-server/) [seafile-client](https://aur.archlinux.org/packages/seafile-client/) [seafile-client-cli](https://aur.archlinux.org/packages/seafile-client-cli/) [seafile-client-qt5](https://aur.archlinux.org/packages/seafile-client-qt5/)

*   **StackSync** — Open-source scalable Personal Cloud that can adapt to the necessities of organizations. It puts a special emphasis on security by encrypting data on the client side before it is sent to the server.

	[http://stacksync.org/](http://stacksync.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Syncany** — Cloud storage and filesharing application with a focus on security and abstraction of storage.

	[https://www.syncany.org/](https://www.syncany.org/) || [syncany](https://aur.archlinux.org/packages/syncany/)

## Distributed file systems

*   **[Ceph](/index.php/Ceph "Ceph")** — Distributed object store and file system designed to provide excellent performance, reliability and scalability.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **GlusterFS** — Cluster file system capable of scaling to several peta-bytes.

	[http://www.gluster.org/](http://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **Sheepdog** — Distributed object storage system for volume and container services and manages the disks and nodes intelligently.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## Data cloning

Another type of backups are those used in case of a disaster. These include application that allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. The contains complete system images from one or more specific points in time and are frequently used by to record known good configurations.

See also [Disk cloning](/index.php/Disk_cloning "Disk cloning").

*   **Arch Backup** — A trivial backup script with simple configuration.
    *   Configurable compression method.
    *   Multiple backup targets.

	[http://code.google.com/p/archlinux-stuff/](http://code.google.com/p/archlinux-stuff/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **[Areca Backup](https://en.wikipedia.org/wiki/Areca_Backup "wikipedia:Areca Backup")** — An easy to use and reliable backup solution for Linux and Windows.
    *   Written in Java.
    *   Primarily archive-based (zip), but will do file-based backup as well.
    *   Delta backup supported (stores only changes).

	[http://areca.sourceforge.net/](http://areca.sourceforge.net/) || [areca](https://aur.archlinux.org/packages/areca/)

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive, or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **[DAR](https://en.wikipedia.org/wiki/DAR_(Disk_Archiver) "wikipedia:DAR (Disk Archiver)")** — A full-featured command-line backup tool, short for Disk ARchive.
    *   It uses its own format for archives (so you need to have it around when you want to restore).
    *   Supports splitting backups into more files by size.
    *   Makefile-type config files, some custom scripts are available along with it.
    *   Supports basic encryption.
    *   Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/).

	[http://dar.linux.free.fr/](http://dar.linux.free.fr/) || [dar](https://aur.archlinux.org/packages/dar/) [kdar](https://aur.archlinux.org/packages/kdar/) (fontend)

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

	[http://www.fsarchiver.org/Main_Page](http://www.fsarchiver.org/Main_Page) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — A disaster recovery solution to create backup media that can be used to redeploy the damaged system.
    *   Image-based backups, supporting Linux/Windows.
    *   Compression rate is adjustable.
    *   Can backup live systems (without having to halt it).
    *   Can split image over many files.
    *   Supports booting to a Live CD to perform a full restore.
    *   Can backup/restore over NFS, from CDs, tape drives and and other media.
    *   Can verify backups.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports ext2, ext3, hfs+, reiser3.5, reiser3.6, reiser4, ext4 and btrfs.
    *   Supports compression.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — A disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.

	[http://www.partimage.org/Main_Page](http://www.partimage.org/Main_Page) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **Q7Z** — P7Zip GUI for Linux, which attempts to simplify data compression and backup. It can create the following archive types: 7z, BZip2, Zip, GZip, Tar.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

	[http://k7z.sourceforge.net/](http://k7z.sourceforge.net/) || [q7z](https://aur.archlinux.org/packages/q7z/)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   CLI and Dialog interfaces
    *   Easy backup and restore wizards
    *   Creates *.tar.gz*, *.tar.bz2*, *.tar.xz* or *.tar* archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2, Syslinux, EFISTUB/efibootmgr and Systemd/bootctl

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

## Version control systems

These are traditionally used for keeping track of software development; but if you want to have a simple way to manage your config files in one directory, it might be a good solution.

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Bazaar](https://en.wikipedia.org/wiki/Bazaar_(software) "wikipedia:Bazaar (software)")** — A distributed version control system that helps you track project history over time and to collaborate easily with others.
    *   Similar commands to Subversion.
    *   Supports working with or without a central server.
    *   Support for working with some other revision control systems
    *   Complete Unicode support.

	[http://bazaar.canonical.com/en/](http://bazaar.canonical.com/en/) || [bzr](https://www.archlinux.org/packages/?name=bzr)

*   **[Darcs](https://en.wikipedia.org/wiki/Darcs "wikipedia:Darcs")** — A distributed revision control system that was designed to replace traditional, centralized source control systems such as CVS and Subversion.
    *   Offline mode.
    *   Easy branching and merging.
    *   Written in Haskell.
    *   Not very fast.

	[http://darcs.net/](http://darcs.net/) || [darcs](https://www.archlinux.org/packages/?name=darcs)

*   **[Git](/index.php/Git "Git")** — A distributed revision control and source code management system with an emphasis on speed.
    *   Very easy creation, merging, and deletion of branches.
    *   Nearly all operations are performed locally, giving it a huge speed advantage on centralized systems.
    *   Has a "staging area" or "index", this is an intermediate area where commits can be formatted and reviewed before completing the commit.
    *   Does not handle binary files very well.

	[http://git-scm.com/](http://git-scm.com/) || [git](https://www.archlinux.org/packages/?name=git)

*   **[Mercurial](/index.php/Mercurial "Mercurial")** — A distributed version control system written in Python and similar in many ways to Git.
    *   Platform independent.
    *   Support for [extensions](http://mercurial.selenic.com/wiki/UsingExtensions).
    *   A set of commands consistent with Subversion.
    *   Supports tags.

	[http://mercurial.selenic.com/](http://mercurial.selenic.com/) || [mercurial](https://www.archlinux.org/packages/?name=mercurial)

*   **[Subversion](/index.php/Subversion "Subversion")** — A full-featured centralized version control system originally designed to be a better CVS.
    *   Renamed/copied/moved/removed files retain full revision history.
    *   Native support for binary files, with space-efficient binary-diff storage.
    *   Costs proportional to change size, not to data size.
    *   Allows arbitrary metadata ("properties") to be attached to any file or directory.

	[http://subversion.apache.org/](http://subversion.apache.org/) || [subversion](https://www.archlinux.org/packages/?name=subversion)

## See also

*   [Wikipedia:List of backup software](https://en.wikipedia.org/wiki/List_of_backup_software "wikipedia:List of backup software")
*   [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software")
*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)
*   [rsync-snapshot.sh](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) — Local and remote snapshot backup using rsync with hard links
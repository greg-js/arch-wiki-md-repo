This page lists and compares applications that synchronize data between two or more locations, and those that build on top of such functionality to make incremental copies of important data for backup purposes. Because of their relationship, the two groups share several traits that justify describing them in the same article.

## Contents

*   [1 Backup overview](#Backup_overview)
*   [2 Data synchronization](#Data_synchronization)
*   [3 Incremental backups](#Incremental_backups)
    *   [3.1 Single machine](#Single_machine)
        *   [3.1.1 Chunk-based increments](#Chunk-based_increments)
        *   [3.1.2 File-based increments](#File-based_increments)
    *   [3.2 Network oriented](#Network_oriented)
*   [4 Cloud storage](#Cloud_storage)
    *   [4.1 Third-party services](#Third-party_services)
        *   [4.1.1 Multi-service clients](#Multi-service_clients)
    *   [4.2 Custom infrastructure](#Custom_infrastructure)
*   [5 Version control systems](#Version_control_systems)
*   [6 See also](#See_also)

## Backup overview

Having backups of important data is a necessary measure to take, since human and machine processing errors are very likely to generate corruption as time passes, and also the physical media where the data is stored is inevitably destined to fail. In order to choose the best program for one's own needs, the following aspects should be considered:

*   The type of backup medium that is going to store the data, e.g. CD, DVD, remote server, external hard drive, etc.
*   The planned frequency of backups, e.g. daily, weekly, monthly, etc.
*   The features expected from the backup solution, e.g. compression, encryption, handles renames, etc.
*   The planned method to restore backups if needed.

## Data synchronization

These applications simply keep directories synchronized between multiple locations/machines, in a "mirror" fashion. Nonetheless, most of them still allow storing and reverting to old revisions of modified or deleted files.

See also [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software").

**Legend:**

*   **Name**: the application name, linking to the official website.
*   **Installation**: a link to the main ArchWiki article, if existing, or directly to the package pages.
*   **Implementation**: the programming language, library, or utility that the application is based on.
*   **Delta transfer**: only the modified *parts* of files are transferred.
*   **Encrypted transfer**: data is encrypted by default when transferred over the network.
*   **FS metadata**: file system permissions and attributes are synchronized.
*   **Resumable**: the synchronization can be resumed without restarting it if interrupted.
*   **Handles renames**: moved/renamed files are detected and not stored or transferred twice; it typically means that a checksum is computed for files or chunks thereof.
*   **Version control**: the old version of files are backed up (**reverse incremental backup**).
*   **Conflict resolution**: the application handles file conflicts, either automatically or interactively, i.e. it does not silently discard conflicting files.
*   **Multidirectional**: *more* than 2 locations can be kept in sync together.
*   **FS monitoring**: the application listens to file system events to trigger the synchronization.
*   **CLI**: the application is command-line driven, i.e. it is scriptable.
*   **Other interfaces**: the application has the specified user interfaces, e.g. GUI, TUI, or web-based.
*   **Licence**: the licence of the server and client applications.
*   **Other platforms**: supported operating systems other than Linux.
*   **Active**: whether the project is currently maintained.
*   **Specificity**: brief notes about special features that notably set the application apart from the others.

| Name | Installation | Implementation | Delta transfer | Encrypted transfer | FS metadata | Resumable | Handles renames | Version control | Conflict resolution | Multidirectional | FS monitoring | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |
| [Resilio Sync](https://www.resilio.com/individuals/) (formerly BitTorrent Sync) | [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") | Closed source | Yes | Yes, also LAN transfer encryption option |  ? | Yes |  ? | Yes, previous versions moved to archive folder |  ? | Yes |  ? | No | Web | Proprietary freemium | OS X, Windows, Android, iOS, Windows Phone, Amazon Kindle Fire, FreeBSD | Yes | P2P sync |
| [FreeFileSync](http://freefilesync.sourceforge.net/) | [freefilesync](https://aur.archlinux.org/packages/freefilesync/) | C++ |  ? | SFTP [[1]](http://www.freefilesync.org/faq.php#features) |  ? |  ? | Yes [[2]](http://www.freefilesync.org/faq.php#features) | Yes [[3]](http://www.freefilesync.org/manual.php?topic=versioning) |  ? | No |  ? | No | Yes | GPL | Windows, OS X | Yes |
| [git-annex](http://git-annex.branchable.com/) | [git-annex](https://www.archlinux.org/packages/?name=git-annex) | Haskell, git | rsync [[4]](http://git-annex.branchable.com/transferring_data/) | rsync [[5]](http://git-annex.branchable.com/transferring_data/) |  ? |  ? |  ? | Yes |  ? | git remotes [[6]](http://git-annex.branchable.com/sync/) |  ? | Yes | [git-annex assistant](http://git-annex.branchable.com/assistant/) | GPLv3 | OS X, Android | Yes | Manage files with git |
| [Grsync](http://www.opbyte.it/grsync/) | [grsync](https://www.archlinux.org/packages/?name=grsync) | rsync front-end | rsync | rsync |  ? |  ? |  ? |  ? |  ? | No |  ? | No | GTK+ | GPLv2 |  ? |
| [gutbackup](https://github.com/gutenye/gutbackup) | [gutbackup](https://aur.archlinux.org/packages/gutbackup/) | rsync wrapper | rsync | rsync |  ? |  ? |  ? |  ? |  ? | No |  ? | Yes | No | MIT |  ? |
| [Jotasync](http://jotasync.trixon.se/) | [jotasync](https://aur.archlinux.org/packages/jotasync/) | Java gui for rsync | rsync | rsync |  ? |  ? |  ? |  ? |  ? | No |  ? | limited | Swing | Apache v2 | OS X, Windows | Yes | Integrated scheduler. |
| [luckyBackup](http://luckybackup.sourceforge.net/index.html) | [luckybackup](https://aur.archlinux.org/packages/luckybackup/) | C++ | rsync [[7]](http://luckybackup.sourceforge.net/features.html) | rsync [[8]](http://luckybackup.sourceforge.net/features.html) |  ? |  ? |  ? | Yes |  ? | No |  ? | limited [[9]](http://luckybackup.sourceforge.net/manual.html#terminal) | Qt | GPLv3 | frozen [[10]](http://luckybackup.sourceforge.net/index.html) |
| [osync.sh](http://www.netpower.fr/osync) | [osync](https://aur.archlinux.org/packages/osync/) | Shell | rsync | rsync |  ? | Yes |  ? | Yes |  ? | Yes | optional [[11]](https://github.com/deajan/osync#daemon-mode) | Yes | No | BSD | Yes |
| [rdiff-backup](http://www.nongnu.org/rdiff-backup/) | [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) | Python 2 | Yes | Yes | Yes |  ? | No | Yes | preview changes | No | No | Yes | No | GPL | Win32 |  ? |
| [rsync](http://rsync.samba.org/) | [rsync](/index.php/Rsync "Rsync") | C | Yes | SSH or native protocol | Yes | Yes | No | 

*   `--link-dest` with hard links [[12]](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup)
*   `--backup`

 | preview changes | No | No | Yes | grsync | GPLv3 | Win32 | Yes | Standard install on all Linux distributions. |
| [SparkleShare](http://sparkleshare.org/) | [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare) | C# |  ? |  ? |  ? |  ? |  ? |  ? |  ? |  ? |  ? | No | Yes | GPLv3 | Windows, OS X |  ? |
| [Syncthing](https://syncthing.net/) | [Syncthing](/index.php/Syncthing "Syncthing") | Go | Yes [[13]](http://docs.syncthing.net/users/faq.html#is-synchronization-fast) | Yes [[14]](http://docs.syncthing.net/users/security.html) | partial [[15]](http://docs.syncthing.net/users/faq.html#what-things-are-synced) |  ? |  ? | Yes [[16]](http://docs.syncthing.net/users/versioning.html), previous versions moved to archive folder | renames one file [[17]](https://docs.syncthing.net/users/faq.html#what-if-there-is-a-conflict) | Yes | Yes with [syncthing-inotify](https://github.com/syncthing/syncthing-inotify) | Yes | Web, GTK | MPL v2 | Windows, OS X, Android, BSD, Solaris | Yes | P2P sync |
| [Synkron](http://synkron.sourceforge.net/) | [synkron](https://aur.archlinux.org/packages/synkron/) | C++ |  ? |  ? |  ? |  ? |  ? |  ? |  ? | Yes |  ? | No | Qt | GPLv2 | Windows, OS X | [No](https://sourceforge.net/projects/synkron/) |
| [taskd](https://tasktools.org/projects/taskd.html) | [Taskd](/index.php/Taskd "Taskd") | C++, python, | Yes | Yes |  ? | Yes |  ? |  ? |  ? | Yes | No | Yes | No | MIT | Android | Yes |
| [Unison](http://www.cis.upenn.edu/~bcpierce/unison/) | [Unison](/index.php/Unison "Unison") | OCaml | Yes | Yes | partial [[18]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#perms) | optional [[19]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#speeding) | No | Yes [[20]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#backups) | interactive | No | No | Yes | GTK2 | GPL | Windows, OS X, FreeBSD, Android | Yes [[21]](http://www.cis.upenn.edu/~bcpierce/unison/status.html) |
| Name | Installation | Implementation | Delta transfer | Encrypted transfer | FS metadata | Resumable | Handles renames | Version control | Conflict resolution | Multidirectional | FS monitoring | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |

## Incremental backups

Applications that can do incremental backups remember and take into account what data has been backed up during the last run (so-called "diffs") and eliminate the need to have duplicates of unchanged data. Restoring the data to a certain point in time would require locating the last full backup and all the incremental backups from then to the moment when it is supposed to be restored. This sort of backup is useful for those who do it very often.

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
*   **Licence**: the licence of the server and client applications.
*   **Other platforms**: supported operating systems other than Linux.
*   **Active**: whether the project is currently maintained.
*   **Specificity**: brief notes about special features that notably set the application apart from the others.

### Single machine

These applications are aimed at backing up data from the machine they are installed on, although the backup destination can be located on an external machine or storage media.

#### Chunk-based increments

If a file is modified, these applications store only its changed *parts* at the next snapshot. Compared to [#File-based increments](#File-based_increments) applications, these are more space-efficient, especially when large files receive small modifications; on the other hand, the archived snapshots have to be opened with the backup application that created them, since the files have to be reconstructed from the stored binary diffs.

| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/) | Java | Zip, Zip64 | AES128, AES256 | Yes | Yes | Yes | No | Pausing only | No | Yes | Yes | GPLv2 | Windows | Yes |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Python (Attic fork) | lz4, zlib, lzma | AES256 | Yes | SSH | Yes[[22]](http://borgbackup.readthedocs.org/en/stable/faq.html#which-file-types-attributes-etc-are-preserved) | Yes[[23]](http://borgbackup.readthedocs.org/en/stable/usage.html#borg-mount) | Yes[[24]](http://borgbackup.readthedocs.org/en/stable/faq.html#if-a-backup-stops-mid-way-does-the-already-backed-up-data-stay-there) | Yes | Yes | third party | BSD | *BSD, OS X | Yes |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/) | C | Yes | Yes | Yes | Yes |  ? | No |  ? |  ? | Yes | No | GPLv3 | Yes | Redundancy, indexed extraction, multicore compression, input and output serialisation, tolerance to partial archive errors. |
| [bup](https://bup.github.io/) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/) | C, Python, git | Yes | No | Yes | Yes | Immature | Yes[[25]](https://bup.github.io/man/bup-fuse.html) | pick up where you left off [[26]](https://github.com/bup/bup/blob/master/README.md#reasons-bup-is-awesome) | Yes | Yes | third party | GPLv2 | Windows, OS X, NetBSD, Solaris | Yes | Same storage format as git |
| [bups](https://github.com/emersion/bups) | [bups](https://aur.archlinux.org/packages/bups/) | bup frontend | Yes | No | Yes | Yes | Immature | Yes | pick up where you left off [[27]](https://github.com/bup/bup/blob/master/README.md#reasons-bup-is-awesome) | Yes | Yes | GTK 3 | MIT | Yes |
| [Déjà Dup](https://launchpad.net/deja-dup) | [Déjà Dup](/index.php/D%C3%A9j%C3%A0_Dup "Déjà Dup") | duplicity front-end | Yes | Yes | Yes | Yes |  ? | No | Yes | No | Yes | GTK+ | GPLv3 | Yes | Integrated into [GNOME Files](/index.php/GNOME_Files "GNOME Files"). |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/) | C# | Yes | Yes | Yes | Yes | scheduled for 2.0 release | No | Pausing only | No | Yes | Yes | LGPL | Windows | Yes |
| [Duplicity](http://www.nongnu.org/duplicity/) | [Duplicity](/index.php/Duplicity "Duplicity") | librsync | gzip | gpg | Yes | Yes |  ? | No | Yes | No | Yes | Déjà Dup | GPL | Yes |
| [Duply](http://www.duply.net/) | [Duply](/index.php/Duply "Duply") | duplicity front-end | Yes | Yes | Yes | Yes |  ? | No | Yes | No | Yes | No | GPLv2 | Yes |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | Yes | Yes | Yes | Yes | Immature | Yes | No | Yes | bup | Qt | GPLv2 | Yes |
| [obnam](http://liw.fi/obnam/) | [obnam](https://aur.archlinux.org/packages/obnam/) | Python | Yes | GnuPG | Yes | Yes |  ? | Yes | checkpoints every 100MB |  ? | Yes | No | GPLv3 | Yes |
| [restic](https://restic.github.io/) | [restic](https://aur.archlinux.org/packages/restic/) [restic-git](https://aur.archlinux.org/packages/restic-git/) | Go | No [[28]](https://github.com/restic/restic/issues/21) | AES-256 [[29]](https://github.com/restic/restic/blob/master/doc/Design.md) |  ? | Yes |  ? |  ? |  ? |  ? |  ? |  ? | BSD | Yes |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/) | C++ | LZMA, LZO | AES | Yes | Yes |  ? | planned [[30]](https://github.com/zbackup/zbackup#improvements) | No | Kinda through tar | Yes | No | GPLv2 | Yes | Repository consists of immutable files. |
| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |

#### File-based increments

If a file is modified, these applications store its new version entirely at the next snapshot. Compared to [#Chunk-based increments](#Chunk-based_increments) applications, these are less space-efficient, especially when large files receive small modifications; on the other hand, often the archived snapshots can be opened without the need to have the backup application installed.

**Specific legend:**

*   **Hard links**: whether unmodified files are stored as hard links to previous versions.

| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Hard links | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |
| [Back In Time](https://github.com/bit-team/backintime) | [Back In Time](/index.php/Back_In_Time "Back In Time") | Python, rsync, diff | No | No | rsync | rsync | rsync | Yes | No | No | Yes [[31]](http://backintime.le-web.org/documentation/) | Yes | Qt | GPLv2 | Yes |
| [DAR](http://dar.linux.free.fr/) (Disk ARchive) | [dar](https://aur.archlinux.org/packages/dar/) | C++ | special archive format | Yes |  ? | Yes |  ? |  ? |  ? |  ? | No [[32]](http://dar.linux.free.fr/doc/Features.html) | Yes | DarGUI | GPL | Windows, Solaris, FreeBSD, NetBSD, MacOS X | Yes | Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/). |
| [DarGUI](http://dargui.sourceforge.net/) | [dargui](https://aur.archlinux.org/packages/dargui/) | DAR front-end | Yes | Yes |  ? | Yes |  ? |  ? |  ? |  ? | No [[33]](http://dar.linux.free.fr/doc/Features.html) | No | GTK | GPL | Windows |  ? |
| [hdup](http://miek.nl/projects/hdup2/) | [hdup](https://aur.archlinux.org/packages/hdup/) | C | bzip, gzip, lzop | gpg |  ? | SSH |  ? | No | No | No | No | Yes | No | GPLv2 | No | Multiple backup targets. |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/) | Python | No | No |  ? | SSH |  ? |  ? | Yes | Yes | No [[34]](http://www.scottlu.com/Content/Link-Backup.html) | Yes | No | MIT | No | It copies itself to the server. |
| [rdup](https://github.com/miekg/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/) | C | tar.gz | gpg, blowfish and others |  ? |  ? |  ? | Yes |  ? | No | Yes | Yes | No | GPLv3 | No | Set of command-line tools. |
| [rsnapshot](http://www.rsnapshot.org/) | [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | rsync | No | No | Yes | Yes |  ? |  ? |  ? |  ? | Yes [[35]](http://rsnapshot.org/rsnapshot/docs/docbook/rest.html) | Yes | No | GPLv2 | Win32 | Yes |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/) | Python | gzip, bzip2 | No |  ? | SSH |  ? | No | No | No | No | No | GTK | GPLv3 | Yes |
| [TimeShift](https://launchpad.net/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/) | rsync | No | No | rsync | rsync |  ? |  ? |  ? |  ? | Yes | No | GTK | GPLv3 | Designed for full-system backups to dedicated devices. | Yes |
| Name | Installation | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Hard links | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |

### Network oriented

These applications have been designed to centralize the backup of several machines connected to a network, through a server-client model. In general they are more complicated to deploy, compared to [#Single machine](#Single_machine) solutions.

**Specific legend:**

*   **Control direction**: Pull: server logs into client. Push: client initiates backup session.
*   **Increment type**: the strategy used to reduce used space by deduplicating data (i.e., besides compression).
    *   **file-based**: if a file is modified, the entire new version is stored at each snapshot.
        *   **hard-links**: whether unmodified files are stored as hard links to previous versions.
    *   **chunk-based**: only the modified *parts* of files are stored at each snapshot.

| Name | Installation | Implementation | Control direction | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Increment type | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |
| [BackupPC](http://backuppc.sourceforge.net/index.html) | [BackupPC](/index.php/BackupPC "BackupPC") | Perl | Pull | Yes | No | Yes | Yes | Yes | No | Yes |  ? | file-based, hard links [[36]](http://backuppc.sourceforge.net/faq/BackupPC.html#Backup-basics) | No | Web | GPLv2 | Any (no client needed) | Yes | Identical files across backups of the same or different clients are stored only once. |
| [Bacula](http://www.bacula.org) | [bacula*](https://aur.archlinux.org/packages/?K=bacula) in [AUR](/index.php/AUR "AUR") | C++ | Pull | Yes | Yes |  ? | Yes |  ? |  ? | Yes |  ? | file-based [[37]](http://burp.grke.org/why.html) | Yes | GUI, Web | AGPLv3 | Windows, OS X | Yes |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/) | librsync | Push | Yes | Yes | Yes | Yes |  ? |  ? |  ? |  ? | chunk-based [[38]](http://burp.grke.org/why.html) | Yes | [burp-ui](https://git.ziirish.me/ziirish/burp-ui) | AGPLv3 | Windows | Yes |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/) | rdiff-backup | Pull | No | No |  ? | Yes |  ? |  ? |  ? |  ? | chunk-based [[39]](http://safekeep.sourceforge.net/safekeep.html) | Yes | Yes | GPL | No | Integrates with [LVM](/index.php/LVM "LVM") and databases to create consistent backups. Bandwidth throttling. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/) | C | Push or Pull | Yes | No |  ? | Yes |  ? |  ? |  ? |  ? | file-based [[40]](http://www.snebu.com/#_concepts) | Yes | No | GPLv3 |  ? | Supports arbitrary retention schedules. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | Multitool wrapper |  ? | Yes | No | Yes | Yes | Yes |  ? |  ? |  ? |  ? | No | Web | GPLv3 | Yes | Unifies several backup methods. |
| [UrBackup](https://www.urbackup.org) | [urbackup*](https://aur.archlinux.org/packages/?K=urbackup) in [AUR](/index.php/AUR "AUR") | C++ | Pull | No | No | Yes | Internet transfers only | Yes | Yes | Yes | Yes | file-based,hard-links and symlinks[[41]](http://blog.urbackup.org/156/symbolically-linking-directories-during-incremental-file-backups)/chunk-based CoW-Snapshots[[42]](http://blog.urbackup.org/83/file-backup-storage-with-btrfs-snapshots) | Yes (client) | GUI, Web | AGPLv3+ | Windows, macOS | Yes | Identical files across backups of the same or different clients are stored only once. Integrates with LVM, dattobd and btrfs for file system snapshots. |
| Name | Installation | Implementation | Control direction | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Increment type | CLI | Other interfaces | Licence | Other platforms | Active | Specificity |

## Cloud storage

### Third-party services

See also [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services").

**Tip:** [cryptomator](https://aur.archlinux.org/packages/cryptomator/) is an open-source, multi-platform program designed to add client-side transparent encryption on cloud-shared files.

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

	[https://drive.google.com](https://drive.google.com) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/) (free), [drive](https://aur.archlinux.org/packages/drive/) (free), [grive](https://aur.archlinux.org/packages/grive/) (free), [gdrivefs](https://aur.archlinux.org/packages/gdrivefs/) (free), [insync](/index.php/Insync "Insync") (non-free), [gdrive](https://aur.archlinux.org/packages/gdrive/) (free)

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

*   **rsync.net** — Cloud storage for offsite backups.
    *   ZFS filesystem, accessible with any SSH/SFTP/SCP tool, running on a UNIX system.
    *   Simple rsync synchronization with daily automatic ZFS snapshots.
    *   [Special discounted price](http://www.rsync.net/products/attic.html) if used with borg or attic.

	[http://www.rsync.net/](http://www.rsync.net/) || [rsync](/index.php/Rsync "Rsync")/[SSH](/index.php/SSH "SSH"), [borg](https://www.archlinux.org/packages/?name=borg)/[attic](https://aur.archlinux.org/packages/attic/)

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

*   **[Déjà Dup](/index.php/D%C3%A9j%C3%A0_Dup "Déjà Dup")** — A simple GTK+ backup program. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses duplicity as the backend.
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

### Custom infrastructure

*   **[Cozy](/index.php/Cozy "Cozy")** — A personal cloud you can hack, host and delete.

	[https://cozy.io](https://cozy.io) || [cozy-standalone](https://aur.archlinux.org/packages/cozy-standalone/) [cozy-nginx](https://aur.archlinux.org/packages/cozy-nginx/) [cozy-apache](https://aur.archlinux.org/packages/cozy-apache/)

*   **[OpenStack](/index.php/OpenStack "OpenStack")** — Controls large pools of compute, storage, and networking resources throughout a datacenter, managed through a dashboard or via the OpenStack API. OpenStack works with popular enterprise and open source technologies making it ideal for heterogeneous infrastructure.

	[http://www.openstack.org/](http://www.openstack.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[ownCloud](/index.php/OwnCloud "OwnCloud")** — Software suite that provides a location-independent storage area for data.

	[http://owncloud.org/](http://owncloud.org/) || [owncloud](https://www.archlinux.org/packages/?name=owncloud)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud")** — Fork of ownCloud.

	[http://nextcloud.com/](http://nextcloud.com/) || [nextcloud](https://www.archlinux.org/packages/?name=nextcloud)

*   **[Pydio](/index.php/Pydio "Pydio")** — Mature open source web application for file sharing and synchronization.

	[https://pydio.com/](https://pydio.com/) || [pydio](https://aur.archlinux.org/packages/pydio/)

*   **[Seafile](/index.php/Seafile "Seafile")** — Open source cloud storage system, with advanced support for file syncing, privacy protection and teamwork.

	[http://seafile.com/](http://seafile.com/) || [seafile-server](https://aur.archlinux.org/packages/seafile-server/) [seafile-client](https://aur.archlinux.org/packages/seafile-client/) [seafile-client-cli](https://aur.archlinux.org/packages/seafile-client-cli/) [seafile-client-qt5](https://aur.archlinux.org/packages/seafile-client-qt5/)

*   **StackSync** — Open-source scalable Personal Cloud that can adapt to the necessities of organizations. It puts a special emphasis on security by encrypting data on the client side before it is sent to the server.

	[http://stacksync.org/](http://stacksync.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Syncany** — Cloud storage and filesharing application with a focus on security and abstraction of storage.

	[https://www.syncany.org/](https://www.syncany.org/) || [syncany](https://aur.archlinux.org/packages/syncany/)

## Version control systems

These are traditionally used for keeping track of software development; but if you want to have a simple way to manage your config files in one directory, it might be a good solution.

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Bazaar](/index.php/Bazaar "Bazaar")** — A distributed version control system that helps you track project history over time and to collaborate easily with others.
    *   Similar commands to Subversion.
    *   Supports working with or without a central server.
    *   Support for working with some other revision control systems
    *   Complete Unicode support.

	[http://bazaar.canonical.com/en/](http://bazaar.canonical.com/en/) || [bzr](https://www.archlinux.org/packages/?name=bzr)

*   **Darcs** — A distributed revision control system that was designed to replace traditional, centralized source control systems such as CVS and Subversion.
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
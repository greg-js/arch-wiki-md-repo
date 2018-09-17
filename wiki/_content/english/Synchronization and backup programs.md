Related articles

*   [System backup](/index.php/System_backup "System backup")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [List of applications#File sharing](/index.php/List_of_applications#File_sharing "List of applications")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [Dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles")
*   [File recovery](/index.php/File_recovery "File recovery")

This page lists and compares applications that synchronize data between two or more locations, and those that build on top of such functionality to make incremental copies of important data for backup purposes. Because of their relationship, the two groups share several traits that justify describing them in the same article.

## Contents

*   [1 Backup overview](#Backup_overview)
*   [2 Data synchronization](#Data_synchronization)
    *   [2.1 Legend](#Legend)
    *   [2.2 Table](#Table)
*   [3 Incremental backups](#Incremental_backups)
    *   [3.1 Single machine](#Single_machine)
        *   [3.1.1 Chunk-based increments](#Chunk-based_increments)
        *   [3.1.2 File-based increments](#File-based_increments)
    *   [3.2 Network oriented](#Network_oriented)
*   [4 Version control systems](#Version_control_systems)
*   [5 See also](#See_also)

## Backup overview

Having backups of important data is a necessary measure to take, since human and machine processing errors are very likely to generate corruption as time passes, and also the physical media where the data is stored is inevitably destined to fail. In order to choose the best program for one's own needs, the following aspects should be considered:

*   The type of backup medium that is going to store the data, e.g. CD, DVD, remote server, external hard drive, etc.
*   The planned frequency of backups, e.g. daily, weekly, monthly, etc.
*   The features expected from the backup solution, e.g. compression, encryption, handles renames, etc.
*   The planned method to restore backups if needed.

## Data synchronization

These applications simply keep directories synchronized between multiple locations/machines, in a "mirror" fashion. Nonetheless, most of them still allow storing and reverting to old revisions of modified or deleted files.

See also:

*   [List of applications/Utilities#File synchronization](/index.php/List_of_applications/Utilities#File_synchronization "List of applications/Utilities")
*   [List of applications/Internet#Cloud synchronization clients](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet")
*   [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software")

### Legend

	Name

	The application name, linking to the ArchWiki article or the official website.

	Package

	A link to the package.

	Implementation

	The programming language, library, or utility that the application is based on.

	Delta transfer

	Only the modified *parts* of files are transferred.

	Encrypted transfer

	Data is encrypted by default when transferred over the network.

	FS metadata

	File system permissions and attributes are synchronized.

	Resumable

	The synchronization can be resumed if interrupted.

	Handles renames

	Moved/renamed files are detected and not stored or transferred twice. It typically means that a checksum of files or its chunks is computed. Applications missing this functionality can be supplemented by combining with [hsync](https://aur.archlinux.org/packages/hsync/), which *only* synchronizes renames.

	Version control

	The old version of files are backed up (*reverse incremental backup*).

	Change propagation

	Specifies in how many directions changes can be propagated.

*   *unidirectional* means one-way synchronization of two locations,
*   *bidirectional* means two-way synchronization of two locations and
*   *multidirectional* means full synchronization of more than two locations.

	Conflict resolution

	The application handles file conflicts, either automatically or interactively, i.e. it does not silently discard conflicting files. This attribute does not apply to applications that only propagate changes in one direction.

	FS monitoring

	The application listens to file system events to trigger the synchronization.

	CLI

	The application provides a command-line interface.

	Other interfaces

	The application has the specified user interfaces, e.g. GUI, TUI, or web-based.

	License

	The license of the server and client applications.

	Other platforms

	Supported operating systems other than Linux.

	Maintained

	The project is maintained.

	Specificity

	Brief notes about special features that notably set the application apart from the others.

### Table

| Name | Package | Implementation | Delta transfer | Encrypted transfer | FS metadata | Resumable | Handles renames | Version control | Change propagation | Conflict resolution | FS monitoring | CLI | Other interfaces | License | Other platforms | Maintained | Specificity |
| [FreeFileSync](https://www.freefilesync.org/) | [freefilesync](https://aur.archlinux.org/packages/freefilesync/) | C++ |  ? | SFTP [[1]](http://www.freefilesync.org/faq.php#features) |  ? |  ? | Yes [[2]](http://www.freefilesync.org/faq.php#features) | Yes [[3]](http://www.freefilesync.org/manual.php?topic=versioning) | **uni**directional / **multi**directional | Yes |  ? | No | Yes | GPL | Windows, macOS | Yes |
| [git-annex](https://git-annex.branchable.com/) | [git-annex](https://www.archlinux.org/packages/?name=git-annex) | Haskell, git | rsync [[4]](http://git-annex.branchable.com/transferring_data/) | rsync [[5]](http://git-annex.branchable.com/transferring_data/) |  ? |  ? |  ? | Yes | **multi**directional; with git remotes [[6]](http://git-annex.branchable.com/sync/) | renames conflicting files [[7]](http://git-annex.branchable.com/automatic_conflict_resolution/) |  ? | Yes | [git-annex assistant](http://git-annex.branchable.com/assistant/) | GPLv3 | macOS, Android | Yes | Manage files with git |
| [osync.sh](http://www.netpower.fr/osync) | [osync](https://aur.archlinux.org/packages/osync/) | Bash, based on rsync | rsync | rsync |  ? | Yes | No | Yes | **bi**directional | keeps multiple versions of a file [[8]](http://www.netpower.fr/sites/default/files/soft/html-doc/osync_v1.2.html#toc-Subsubsection-1.3.1) | optional [[9]](https://github.com/deajan/osync#daemon-mode) | Yes | No | BSD | Yes |
| [rclone](https://rclone.org/) | [rclone](https://www.archlinux.org/packages/?name=rclone) | Go | No [[10]](https://rclone.org/faq/#why-doesn-t-rclone-support-partial-transfers-binary-diffs-like-rsync) |  ? |  ? |  ? |  ? |  ? | **uni**directional [[11]](https://rclone.org/faq/#can-rclone-do-bi-directional-sync) |  ? |  ? | Yes | [RcloneBrowser](https://github.com/mmozeiko/RcloneBrowser) | MIT | *BSD, Plan9, Solaris, Windows, macOS | Yes | Optimized for synchronization with cloud storage, behavior varies with the features supported by the remote location. |
| [rdiff-backup](http://www.nongnu.org/rdiff-backup/) | [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) | Python 2, librsync | rsync | rsync | Yes |  ? | No | Yes | **uni**directional | No | Yes | No | GPL | Win32 |  ? |
| [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") | [rslsync](https://aur.archlinux.org/packages/rslsync/) | C++ | Yes | Yes |  ? | Yes |  ? | Yes | **multi**directional |  ? |  ? | No | Web | Proprietary freemium | FreeBSD, Windows, macOS, Android, iOS, Windows Phone, Amazon Kindle Fire | Yes | P2P sync |
| [rsync](/index.php/Rsync "Rsync") | [rsync](https://www.archlinux.org/packages/?name=rsync) | C | Yes | SSH or native protocol | Yes | Yes | No | 

*   `--link-dest` with hard links [[12]](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup)
*   `--backup`

 | **uni**directional | No | Yes | [Rsync#Front-ends](/index.php/Rsync#Front-ends "Rsync") | GPLv3 | Win32 | Yes | Standard tool present on all Linux distributions. |
| [SparkleShare](https://sparkleshare.org/) | [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare) | C#, git | Yes | AES-256 [[13]](https://github.com/hbons/SparkleShare/wiki/Client-Side-Encryption) |  ? |  ? | Yes | Yes |  ? |  ? |  ? | No | Yes | GPLv3 | Windows, macOS | Yes | It can sync with any Git server over SSH. |
| [Syncany](https://www.syncany.org/) | [syncany](https://aur.archlinux.org/packages/syncany/) | Java |  ? |  ? |  ? |  ? |  ? |  ? |  ? |  ? |  ? | Yes | Yes | GPLv3 | No [[14]](https://github.com/syncany/syncany/graphs/contributors) |
| [Syncthing](/index.php/Syncthing "Syncthing") | [syncthing](https://www.archlinux.org/packages/?name=syncthing) | Go | Yes [[15]](http://docs.syncthing.net/users/faq.html#is-synchronization-fast) | Yes [[16]](http://docs.syncthing.net/users/security.html) | partial [[17]](http://docs.syncthing.net/users/faq.html#what-things-are-synced) | Yes |  ? | Yes [[18]](http://docs.syncthing.net/users/versioning.html), previous versions moved to archive folder | **multi**directional | renames one file [[19]](https://docs.syncthing.net/users/faq.html#what-if-there-is-a-conflict) | Yes | Yes | Web, GTK | MPL v2 | BSD, Windows, macOS, Android, Kindle Paperwhite | Yes | P2P sync |
| [Synkron](http://synkron.sourceforge.net/) | [synkron](https://aur.archlinux.org/packages/synkron/) | C++ |  ? |  ? |  ? |  ? |  ? |  ? | **multi**directional |  ? |  ? | No | Qt | GPLv2 | Windows, macOS | [No](https://sourceforge.net/projects/synkron/) |
| [taskd](/index.php/Taskd "Taskd") | [taskd](https://aur.archlinux.org/packages/taskd/) | C++, Python | Yes | Yes |  ? | Yes |  ? |  ? | **multi**directional |  ? | No | Yes | No | MIT | Android | Yes |
| [Unison](/index.php/Unison "Unison") | [unison](https://www.archlinux.org/packages/?name=unison) | OCaml | Yes | Yes | partial [[20]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#perms) | optional [[21]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#speeding) | No | Yes [[22]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#backups) | **bi**directional | interactive | No | Yes | GTK2 | GPL | FreeBSD, Windows, macOS, Android | Yes [[23]](http://www.cis.upenn.edu/~bcpierce/unison/status.html) |

## Incremental backups

Applications that can do [incremental backups](https://en.wikipedia.org/wiki/Incremental_backup "wikipedia:Incremental backup") remember and take into account what data has been backed up during the last run (so-called "diffs") and eliminate the need to have duplicates of unchanged data. Restoring the data to a certain point in time would require locating the last full backup and all the incremental backups from then to the moment when it is supposed to be restored. This sort of backup is useful for those who do it very often.

See also:

*   [List of applications/Security#Backup programs](/index.php/List_of_applications/Security#Backup_programs "List of applications/Security")
*   [Wikipedia:List of backup software](https://en.wikipedia.org/wiki/List_of_backup_software "wikipedia:List of backup software")
*   [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software")
*   [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services")

**Legend:**

*   **Name**: the application name, linking to the ArchWiki article or the official website.
*   **Package**: a link to the package.
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
*   **Maintained**: whether the project is maintained.
*   **Specificity**: brief notes about special features that notably set the application apart from the others.

### Single machine

These applications are aimed at backing up data from the machine they are installed on, although the backup destination can be located on an external machine or storage media.

#### Chunk-based increments

If a file is modified, these applications store only its changed *parts* at the next snapshot. Compared to [#File-based increments](#File-based_increments) applications, these are more space-efficient, especially when large files receive small modifications; on the other hand, the archived snapshots have to be opened with the backup application that created them, since the files have to be reconstructed from the stored binary diffs.

| Name | Package | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | CLI | Other interfaces | Licence | Other platforms | Maintained | Specificity |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/) | Java | Zip, Zip64 | AES128, AES256 | Yes | Yes | Yes | No | Pausing only | No | Yes | Yes | GPLv2 | Windows | Yes |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Python, C (Cython) | lz4, zlib, lzma, zstd | AES256 | Yes | SSH | Yes [[24]](http://borgbackup.readthedocs.org/en/stable/faq.html#which-file-types-attributes-etc-are-preserved) | Yes [[25]](http://borgbackup.readthedocs.org/en/stable/usage.html#borg-mount) | Yes [[26]](http://borgbackup.readthedocs.org/en/stable/faq.html#if-a-backup-stops-mid-way-does-the-already-backed-up-data-stay-there) | Yes | Yes | third party | BSD | *BSD, macOS, Windows (Cygwin / WSL)[[27]](https://borgbackup.readthedocs.io/en/stable/#main-features) | Yes | Deduplication based on variable length chunks; support both local and SSH-based remote backup destination. |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/) | C | Yes | Yes | Yes | Yes |  ? | No |  ? |  ? | Yes | No | GPLv3 | Yes | Redundancy, indexed extraction, multicore compression, input and output serialisation, tolerance to partial archive errors. |
| [bup](https://bup.github.io/) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/) | C, Python, git | Yes | No | Yes | Yes | Immature | Yes [[28]](https://bup.github.io/man/bup-fuse.html) | pick up where you left off [[29]](https://github.com/bup/bup/blob/master/README.md#reasons-bup-is-awesome) | Yes | Yes | [bups](https://aur.archlinux.org/packages/bups/) | GPLv2 | NetBSD, Windows, macOS | Yes | Same storage format as git. |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/) | C# | Yes | Yes | Yes | Yes | scheduled for 2.0 release | No | Pausing only | No | Yes | Yes | LGPL | Windows | Yes |
| [Duplicity](/index.php/Duplicity "Duplicity") | [duplicity](https://www.archlinux.org/packages/?name=duplicity) | librsync | gzip | gpg | Yes | Yes |  ? | No | Yes | No | Yes | [Yes](/index.php/Duplicity#Front-ends "Duplicity") | GPL | Yes |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | Yes | Yes | Yes | Yes | Immature | Yes | No | Yes | bup | Qt | GPLv2 | Yes |
| [obnam](https://obnam.org/) | [obnam](https://aur.archlinux.org/packages/obnam/) | Python | Yes | GnuPG | Yes | Yes |  ? | Yes | checkpoints every 100MB |  ? | Yes | No | GPLv3 | [No](https://blog.liw.fi/posts/2017/08/13/retiring_obnam/) |
| [restic](https://restic.net/) | [restic](https://www.archlinux.org/packages/?name=restic) [restic-git](https://aur.archlinux.org/packages/restic-git/) | Go | No [[30]](https://github.com/restic/restic/issues/21) | AES-256 [[31]](https://github.com/restic/restic/blob/master/doc/Design.md) | Yes | Yes | Yes [[32]](https://restic.readthedocs.io/en/latest/manual_rest.html#metadata-handling) | Yes [[33]](https://restic.readthedocs.io/en/stable/050_restore.html#restore-using-mount) | Yes [[34]](https://github.com/restic/restic/pull/310) | Yes | Yes | No [[35]](https://github.com/restic/restic/issues/60) | BSD | OpenBSD, Windows, macOS | Yes | Supports storage on various cloud services natively and through [rclone](https://www.archlinux.org/packages/?name=rclone). |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/) | C++ | LZMA, LZO | AES | Yes | Yes |  ? | planned [[36]](https://github.com/zbackup/zbackup#improvements) | No | Kinda through tar | Yes | No | GPLv2 | Yes | Repository consists of immutable files. |

#### File-based increments

If a file is modified, these applications store its new version entirely at the next snapshot. Compared to [#Chunk-based increments](#Chunk-based_increments) applications, these are less space-efficient, especially when large files receive small modifications; on the other hand, often the archived snapshots can be opened without the need to have the backup application installed.

**Specific legend:**

*   **Hard links**: whether unmodified files are stored as hard links to previous versions.

| Name | Package | Implementation | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Hard links | CLI | Other interfaces | Licence | Other platforms | Maintained | Specificity |
| [Back In Time](/index.php/Back_In_Time "Back In Time") | [backintime](https://aur.archlinux.org/packages/backintime/) | Python, rsync, diff | No | No | rsync | rsync | rsync | Yes | No | No | Yes [[37]](http://backintime.le-web.org/documentation/) | Yes | Qt | GPLv2 | Yes |
| [DAR](http://dar.linux.free.fr/) (Disk ARchive) | [dar](https://aur.archlinux.org/packages/dar/) | C++ | special archive format | Yes | Yes | Yes |  ? |  ? |  ? |  ? | No [[38]](http://dar.linux.free.fr/doc/Features.html) | Yes | [dargui](https://aur.archlinux.org/packages/dargui/) | GPL | FreeBSD, NetBSD, Windows, macOS | Yes |
| [hdup](http://miek.nl/projects/hdup2/) | [hdup](https://aur.archlinux.org/packages/hdup/) | C | bzip, gzip, lzop | gpg |  ? | SSH |  ? | No | No | No | No | Yes | No | GPLv2 | No | Multiple backup targets. |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/) | Python 2 | No | No |  ? | SSH |  ? |  ? | Yes | Yes | No [[39]](http://www.scottlu.com/Content/Link-Backup.html) | Yes | No | MIT | No | It copies itself to the server. |
| [rdup](https://github.com/miekg/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/) | C | tar.gz | gpg, blowfish and others |  ? |  ? |  ? | Yes |  ? | No | Yes | Yes | No | GPLv3 | No | Set of command-line tools. |
| [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | [rsnapshot](https://www.archlinux.org/packages/?name=rsnapshot) | rsync | No | No | Yes | Yes |  ? |  ? |  ? |  ? | Yes [[40]](http://rsnapshot.org/rsnapshot/docs/docbook/rest.html) | Yes | No | GPLv2 | Win32 | No [[41]](https://github.com/rsnapshot/rsnapshot/issues/191) |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/) | Python | gzip, bzip2 | No |  ? | SSH |  ? | No | No | No | No | No | GTK | GPLv3 | No |
| [TimeShift](https://github.com/teejee2008/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/) | rsync | No | No | rsync | rsync |  ? |  ? |  ? |  ? | Yes | No | GTK | GPLv3 | Designed for full-system backups to dedicated devices. | Yes |

### Network oriented

These applications have been designed to centralize the backup of several machines connected to a network, through a server-client model. In general they are more complicated to deploy, compared to [#Single machine](#Single_machine) solutions.

**Specific legend:**

*   **Control direction**: Pull: server logs into client. Push: client initiates backup session.
*   **Increment type**: the strategy used to reduce used space by deduplicating data (i.e., besides compression).
    *   **file-based**: if a file is modified, the entire new version is stored at each snapshot.
        *   **hard-links**: whether unmodified files are stored as hard links to previous versions.
    *   **chunk-based**: only the modified *parts* of files are stored at each snapshot.

| Name | Package | Implementation | Control direction | Compressed storage | Encrypted storage | Delta transfer | Encrypted transfer | FS metadata | Easy access | Resumable | Handles renames | Increment type | CLI | Other interfaces | Licence | Other platforms | Maintained | Specificity |
| [BackupPC](/index.php/BackupPC "BackupPC") | [backuppc](https://www.archlinux.org/packages/?name=backuppc) | Perl | Pull | Yes | No | Yes | Yes | Yes | No | Yes |  ? | file-based, hard links [[42]](http://backuppc.sourceforge.net/faq/BackupPC.html#Backup-basics) | No | Web | GPLv2 | Any (no client needed) | Yes | Identical files across backups of the same or different clients are stored only once. |
| [Bacula](http://www.bacula.org) | [bacula*](https://aur.archlinux.org/packages/?K=bacula) in [AUR](/index.php/AUR "AUR") | C++ | Pull | Yes | Yes |  ? | Yes |  ? |  ? | Yes |  ? | file-based [[43]](http://burp.grke.org/why.html) | Yes | GUI, Web | AGPLv3 | Windows, macOS | Yes |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/) | librsync | Push | Yes | Yes | Yes | Yes |  ? |  ? |  ? |  ? | chunk-based [[44]](http://burp.grke.org/why.html) | Yes | [burp-ui](https://git.ziirish.me/ziirish/burp-ui) | AGPLv3 | Windows | Yes |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/) | rdiff-backup | Pull | No | No |  ? | Yes |  ? |  ? |  ? |  ? | chunk-based [[45]](http://safekeep.sourceforge.net/safekeep.html) | Yes | Yes | GPL | No | Integrates with [LVM](/index.php/LVM "LVM") and databases to create consistent backups. Bandwidth throttling. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/) | C | Push or Pull | Yes | No |  ? | Yes |  ? |  ? |  ? |  ? | file-based [[46]](http://www.snebu.com/#_concepts) | Yes | No | GPLv3 |  ? | Supports arbitrary retention schedules. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | Multitool wrapper |  ? | Yes | No | Yes | Yes | Yes |  ? |  ? |  ? |  ? | No | Web | GPLv3 | Yes | Unifies several backup methods. |
| [UrBackup](https://www.urbackup.org) | [urbackup*](https://aur.archlinux.org/packages/?K=urbackup) in [AUR](/index.php/AUR "AUR") | C++ | Pull | No | No | Yes | Internet transfers only | Yes | Yes | Yes | Yes | file-based,hard-links and symlinks[[47]](http://blog.urbackup.org/156/symbolically-linking-directories-during-incremental-file-backups)/chunk-based CoW-Snapshots[[48]](http://blog.urbackup.org/83/file-backup-storage-with-btrfs-snapshots) | Yes (client) | GUI, Web | AGPLv3+ | Windows, macOS | Yes | Identical files across backups of the same or different clients are stored only once. Integrates with LVM, dattobd and btrfs for file system snapshots. |

## Version control systems

While [version control systems](https://en.wikipedia.org/wiki/version_control_system "wikipedia:version control system") are mostly used for source code, they can track any files in a directory.

See [List of applications/Utilities#Version control systems](/index.php/List_of_applications/Utilities#Version_control_systems "List of applications/Utilities") and [dotfiles](/index.php/Dotfiles "Dotfiles").

## See also

*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Exhaustive list of backup solutions for Linux](https://github.com/restic/others)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [rsync-snapshot.sh](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) — Local and remote snapshot backup using rsync with hard links
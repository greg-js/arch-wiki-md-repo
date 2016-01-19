# Backup programs

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync")
*   [Full System Backup with tar](/index.php/Full_System_Backup_with_tar "Full System Backup with tar")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [Snapper](/index.php/Snapper "Snapper")

This wiki page contains information about various backup programs. It's a good idea to _have_ regular backups of important data, most notably configuration files (`/etc/*`) and the local pacman database (usually `/var/lib/pacman/local/*`).

## Contents

*   [1 Introduction](#Introduction)
*   [2 Incremental backups](#Incremental_backups)
    *   [2.1 Rsync-type backups](#Rsync-type_backups)
        *   [2.1.1 Console](#Console)
        *   [2.1.2 Graphical](#Graphical)
    *   [2.2 Other backups](#Other_backups)
        *   [2.2.1 Console](#Console_2)
        *   [2.2.2 Graphical](#Graphical_2)
        *   [2.2.3 Console and graphical](#Console_and_graphical)
*   [3 Cloud backups](#Cloud_backups)
*   [4 Cooperative storage cloud backups](#Cooperative_storage_cloud_backups)
*   [5 Non-incremental backups](#Non-incremental_backups)
*   [6 Versioning systems](#Versioning_systems)
    *   [6.1 Version control systems](#Version_control_systems)
    *   [6.2 VCS-based backups](#VCS-based_backups)
*   [7 See also](#See_also)

## Introduction

Before you start trying various programs out, try to think about your needs, e.g. consider the following questions:

*   What backup medium do I have available? (CD, DVD, remote server, external hard drive, etc.)
*   How often do I plan to backup? (daily, weekly, monthly, etc.)
*   What features do I expect from the backup solution? (compression, encryption, handles renames, etc.)
*   How do I plan to restore backups if needed?

## Incremental backups

Applications that can do incremental backups remember and take into account what data has been backed up during the last run and eliminate the need to have duplicates of unchanged data. Restoring the data to a certain point in time would require locating the last full backup and all the incremental backups from then to the moment when it is supposed to be restored. This sort of backup is useful for those who do it very often.

### Rsync-type backups

The main characteristic of this type of backups is that they maintain a copy of the directory you want to keep a backup of, in a traditional "mirror" fashion.

Certain rsync-type packages also do snapshot backups by storing files which describe how the contents of files and folders changed from the last backup (so-called 'diffs'). Hence, they are inherently incremental, but usually they do not have compression or encryption. On the other hand, a working copy of everything is immediately available, no decompression/decryption needed. A downside to rsync-type programs is that they cannot be easily burned and restored from a CD or DVD.

#### Console

*   **[rsync](/index.php/Rsync "Rsync")** — A file transfer program to keep remote files in sync.
    *   rsync almost always makes a mirror of the source.
    *   It is possible to restore a full backup before the most recent backup if hardlinks are allowed in the backup file system. See [Back up your data with rsync](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup) for more information.
    *   If hard links are not allowed, it is impossible to restore a full backup before the most recent backup (but you can use --backup to keep old versions of the files).
    *   Standard install on all distros.
    *   Can run over SSH (port 22) or native rsync protocol (port 873).
    *   Win32 version available.

[http://rsync.samba.org/](http://rsync.samba.org/) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[rdiff-backup](https://en.wikipedia.org/wiki/Rsync#Variations "wikipedia:Rsync")** — A utility for local/remote mirroring and incremental backups.
    *   Stores the most recent backup as regular files.
    *   To revert to older versions, you apply the diff files to recreate the older versions.
    *   It is granularly incremental (delta backup), it only stores changes to a file; will not create a new copy of a file upon change.
    *   Win32 version available.

[http://www.nongnu.org/rdiff-backup/](http://www.nongnu.org/rdiff-backup/) || [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup)

*   **[rsnapshot](/index.php/Rsnapshot "Rsnapshot")** — A remote filesystem snapshot utility.
    *   Does not store diffs, instead it copies entire files if they have changed.
    *   Creates hard links between a series of backed-up trees (snapshots).
    *   It is differential in that the size of the backup is only the original backup size plus the size of all files that have changed since the last backup.
    *   Destination filesystem must support hard links.
    *   Win32 version available.

[http://www.rsnapshot.org/](http://www.rsnapshot.org/) || [rsnapshot](https://www.archlinux.org/packages/?name=rsnapshot)

*   **SafeKeep** — A client/server backup system which uses rdiff-backup.
    *   Integrates with Linux LVM and databases to create consistent backups.
    *   Bandwidth throttling.

[http://safekeep.sourceforge.net/](http://safekeep.sourceforge.net/) || [safekeep](https://aur.archlinux.org/packages/safekeep/)<sup><small>AUR</small></sup>

*   **Link-Backup** — A tool similar to rsync based scripts, but which does not use rsync. NOTE: no upstream activity since 2008\.
    *   Creates hard links between a series of backed-up trees (snapshots).
    *   Intelligently handles renames, moves, and duplicate files without additional storage or transfer.
    *   The backup directory contains `.catalog`, a catalog of all unique file instances; backup trees hard-link to this catalog.
    *   Transfer occurs over standard I/O locally or remotely between a client and server instance of this script.
    *   It copies itself to the server; it does not need to be installed on the server.
    *   Requires SSH for remote backups.
    *   It resumes stopped backups; it can even be told to run for an arbitrary number of minutes.

[http://www.scottlu.com/Content/Link-Backup.html](http://www.scottlu.com/Content/Link-Backup.html) || [link-backup](https://aur.archlinux.org/packages/link-backup/)<sup><small>AUR</small></sup>

*   **[Unison](https://en.wikipedia.org/wiki/Unison_(file_synchronizer) "wikipedia:Unison (file synchronizer)")** — A program that synchronizes files between two machines over network (LAN or Inet) using a smart diff method + rsync. Allows the user to interactively choose which changes to push, pull, or merge.

[http://www.cis.upenn.edu/~bcpierce/unison/](http://www.cis.upenn.edu/~bcpierce/unison/) || [unison](https://www.archlinux.org/packages/?name=unison)

*   **rsync-snapshot.sh** — Another rsync shellscript with smart rotation (non-linear distribution) of backups. Integrity protection, Quotas, Rules and many more features.

[http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **osync.sh** — Osync is a robust bidirectional file synchronization tool written in bash and based on rsync. It works on local and / or remote directories via ssh tunnels. It's mainly targeted to be launched as cron task, with features turned towards automation among:
    *   Execution time control
    *   Fault tolerance with possibility to resume on error
    *   Soft deletion, on-conflict backups with automatic cleanup
    *   Alert notifications via email
    *   Before and /or after time controlled local and / or remote command execution
    *   File monitor mode

[http://www.netpower.fr/osync](http://www.netpower.fr/osync) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **gutbackup** — The simplest rsync wrapper for backup Linux system.

[https://github.com/gutenye/gutbackup](https://github.com/gutenye/gutbackup) || [gutbackup](https://aur.archlinux.org/packages/gutbackup/)<sup><small>AUR</small></sup>

*   **trinkup** — A 60-lines bash script which holds specified amount of incremental backups using rsync and "cp -al" to minimize amount of disk operations.

[https://gist.github.com/ei-grad/7610406/raw/trinkup](https://gist.github.com/ei-grad/7610406/raw/trinkup) || [trinkup](https://aur.archlinux.org/packages/trinkup/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/trinkup)]</sup>

*   **keepconf** — Is a wrapper over rsync and git, easy and simple to use

[https://github.com/rfrail3/keepconf](https://github.com/rfrail3/keepconf) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### Graphical

*   **[Areca Backup](https://en.wikipedia.org/wiki/Areca_Backup "wikipedia:Areca Backup")** — An easy to use and reliable backup solution for Linux and Windows.
    *   Written in Java.
    *   Primarily archive-based (zip), but will do file-based backup as well.
    *   Delta backup supported (stores only changes).

[http://areca.sourceforge.net/](http://areca.sourceforge.net/) || [areca](https://aur.archlinux.org/packages/areca/)<sup><small>AUR</small></sup>

*   **[BackupPC](/index.php/BackupPC "BackupPC")** — A high-performance, enterprise-grade system for backing up Unix, Linux, Windows, and Mac OS X desktops and laptops to a remote server.
    *   Deduplication: Identical files across multiple backups of the same or different PCs are stored only once resulting in substantial savings in disk storage and disk I/O.
    *   Optional compression support further reducing disk storage.
    *   No client-side software is needed.
    *   Simple but powerful web-based UI.

[http://backuppc.sourceforge.net/index.html](http://backuppc.sourceforge.net/index.html) || [backuppc](https://www.archlinux.org/packages/?name=backuppc)

*   **[Back In Time](/index.php/Back_In_Time "Back In Time")** — A simple backup tool for Linux inspired by the [FlyBack](https://en.wikipedia.org/wiki/FlyBack "wikipedia:FlyBack") and [TimeVault](https://wiki.ubuntu.com/TimeVault/) projects.
    *   Creates hard links between a series of backed-up trees (snapshots).
    *   Really is just a front-end to `rsync`, `diff`, `cp`.
    *   A new snapshot is created only if something changed since the last snapshot.

[http://backintime.le-web.org/](http://backintime.le-web.org/) || [backintime](https://aur.archlinux.org/packages/backintime/)<sup><small>AUR</small></sup> or as a prebuild package from [coderkun's repo](http://arch.coderkun.de/)

*   **Free File Sync** — Free File Sync helps you synchronize files and synchronize folders for Windows, Linux and Mac OS X. It is designed to save your time setting up and running backup jobs while having nice visual feedback along the way.

[http://freefilesync.sourceforge.net/](http://freefilesync.sourceforge.net/) || [freefilesync](https://aur.archlinux.org/packages/freefilesync/)<sup><small>AUR</small></sup>

*   **Grsync** — GTK+ interface to rsync

[http://www.opbyte.it/grsync/](http://www.opbyte.it/grsync/) || [grsync](https://www.archlinux.org/packages/?name=grsync)

*   **[luckyBackup](https://en.wikipedia.org/wiki/LuckyBackup "wikipedia:LuckyBackup")** — An easy program to backup and sync your files.
    *   It is written in Qt and C++.
    *   It has sync, backup (with include and exclude options) and restore capabilities.
    *   It can do remote connection backups, scheduled backups.
    *   A command line mode.

[http://luckybackup.sourceforge.net/index.html](http://luckybackup.sourceforge.net/index.html) || [luckybackup](https://aur.archlinux.org/packages/luckybackup/)<sup><small>AUR</small></sup>

*   **syncBackup** — A front-end for rsync that provides a fast and extraordinary copying tool. It offers the most common options that control its behavior and permit very flexible specification of the set of files to be copied.

[http://www.darhon.com/syncbackup](http://www.darhon.com/syncbackup) || [syncbackup](https://aur.archlinux.org/packages/syncbackup/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/syncbackup)]</sup>

*   **TimeShift** — TimeShift is a system restore utility which takes incremental snapshots of the system using rsync and hard-links. These snapshots can be restored at a later date to undo all changes that were made to the system after the snapshot was taken. Snapshots can be taken manually or at regular intervals using scheduled jobs.

[https://launchpad.net/timeshift](https://launchpad.net/timeshift) || [timeshift](https://aur.archlinux.org/packages/timeshift/)<sup><small>AUR</small></sup>

### Other backups

Most other backup applications tend to create (big) archive files and (of course) keep track of what's been archived. Creating `.tar.bz2` or `.tar.gz` archives has the advantage that you can extract the backups with just tar/bzip2/gzip, so you do not need to have the backup program around.

#### Console

*   **Arch Backup** — A trivial backup script with simple configuration.
    *   Configurable compression method.
    *   Multiple backup targets.

[http://code.google.com/p/archlinux-stuff/](http://code.google.com/p/archlinux-stuff/) || [arch-backup](https://www.archlinux.org/packages/?name=arch-backup)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>

*   **BorgBackup** — A deduplicating backup program (based on Attic).
    *   Space efficient storage: Deduplication based on content-defined chunking is used to reduce the number of bytes stored
    *   Speed: Local caching of files; quick detection of unmodified files.
    *   Supports pushing over SSH.
    *   Backups mountable: Backup archives are mountable as userspace filesystems.

[http://borgbackup.readthedocs.org/en/stable/](http://borgbackup.readthedocs.org/en/stable/) || [borg](https://www.archlinux.org/packages/?name=borg)

*   **[hdup](/index.php/Backup_with_hdup "Backup with hdup")** — A very simple command line backup tool.
    *   Creates tar.gz or tar.bz2 archives.
    *   Supports gpg encryption.
    *   Supports pushing over SSH.
    *   Multiple backup targets.

[http://miek.nl/projects/hdup2/](http://miek.nl/projects/hdup2/) || [hdup](https://aur.archlinux.org/packages/hdup/)<sup><small>AUR</small></sup>

*   **rdup** — A platform for backups that provides scripts to facilitate backups and delegates the encryption, compression, transfer and packaging to other utilities in a true Unix-way.
    *   Creates tar.gz archives or rsync-type copy.
    *   Encryption (gpg, blowfish and others); also applies for rsync-type copy.
    *   Compression (also for rsync-type copy).

[http://miek.nl/projects/rdup](http://miek.nl/projects/rdup) || [rdup](https://aur.archlinux.org/packages/rdup/)<sup><small>AUR</small></sup>

*   **[Duplicity](/index.php/Duplicity "Duplicity")** — A simple command-line utility which allows encrypted compressed incremental backup to nearly any storage.
    *   Supports gpg encryption and signing.
    *   Supports gzip compression.
    *   Supports full or incremental backups, incremental backup stores only difference between new and old file.
    *   Supports pushing over FTP, SSH, rsync, WebDAV, WebDAVs, HSi and Amazon S3 or local filesystem.

[http://www.nongnu.org/duplicity/](http://www.nongnu.org/duplicity/) || [duplicity](https://www.archlinux.org/packages/?name=duplicity)

*   **[DAR](https://en.wikipedia.org/wiki/DAR_(Disk_Archiver) "wikipedia:DAR (Disk Archiver)")** — A full-featured command-line backup tool, short for Disk ARchive.
    *   It uses its own format for archives (so you need to have it around when you want to restore).
    *   Supports splitting backups into more files by size.
    *   Makefile-type config files, some custom scripts are available along with it.
    *   Supports basic encryption.
    *   Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sarab)]</sup>.

[http://dar.linux.free.fr/](http://dar.linux.free.fr/) || [dar](https://aur.archlinux.org/packages/dar/)<sup><small>AUR</small></sup> [kdar](https://aur.archlinux.org/packages/kdar/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdar)]</sup> (fontend)

*   **Manent** — An algorithmically strong backup and archival program. NOTE: no upstream activity since 2009.
    *   Efficient backup to anything that looks like a storage.
    *   Works well over a slow and unreliable network.
    *   Offers online access to the contents of the backup.
    *   Backed up storage is completely encrypted.
    *   Several computers can use the same storage for backup, automatically sharing data.
    *   Not reliant on timestamps of the remote system to detect changes.
    *   Cross-platform support for Unicode file names.

[http://code.google.com/p/manent/](http://code.google.com/p/manent/) || [manent](https://aur.archlinux.org/packages/manent/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/manent)]</sup>

*   **btar** — tar-compatible archiver
    *   Fast archive creation (multicore compression or ciphering)
    *   Arbitrary chain of compression/ciphers (calls any compression/ciphering programs)
    *   Indexed archive retrieval or listing
    *   Redundancy
    *   Serialization through pipes (and only one file per backup)
    *   Can be extracted or checked with gnutar
    *   Differential backups of multiple levels
    *   Optional encoding of big files with rsync-differences

[http://viric.name/cgi-bin/btar](http://viric.name/cgi-bin/btar) || [btar](https://aur.archlinux.org/packages/btar/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/btar)]</sup>

*   **burp** — Burp is a network backup and restore program
    *   Uses librsync in order to save network traffic and to save on the amount of space that is used by each backup.
    *   It also uses VSS (Volume Shadow Copy Service) to make snapshots when backing up Windows computers.
    *   deduplication
    *   SSL/TLS connections
    *   automation the process of generating SSL certificates
    *   data encryption
    *   security models [[1]](http://burp.grke.org/txt/security-models.txt)

[http://burp.grke.org](http://burp.grke.org) || [burp-backup](https://aur.archlinux.org/packages/burp-backup/)<sup><small>AUR</small></sup>

*   **obnam** — Easy, secure backup program
    *   Snapshot backups. Every generation looks like a complete snapshot.
    *   Data chunk de-duplication, across files, and backup generations. This results in incremental backups.
    *   Optionally encrypted backups, using GnuPG.
    *   FUSE mountable backup repository.

[http://liw.fi/obnam/](http://liw.fi/obnam/) || [obnam](https://aur.archlinux.org/packages/obnam/)<sup><small>AUR</small></sup>

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   CLI and Dialog interfaces
    *   Easy backup and restore wizards
    *   Creates _.tar.gz_, _.tar.bz2_, _.tar.xz_ or _.tar_ archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2, Syslinux, EFISTUB/efibootmgr and Systemd/bootctl

[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)<sup><small>AUR</small></sup>

*   **Packrat** — A simple, modular backup system using [DAR](https://en.wikipedia.org/wiki/DAR_(Disk_Archiver) "wikipedia:DAR (Disk Archiver)")
    *   Full or incremental backups stored locally, on a remote system via SSH, or on Amazon S3

[http://www.zeroflux.org/projects](http://www.zeroflux.org/projects) || [packrat](https://aur.archlinux.org/packages/packrat/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/packrat)]</sup>

*   **Attic** — A deduplicating backup program for efficient and secure backups.
    *   Space efficient storage: Variable block size deduplication is used to reduce the number of bytes stored by detecting redundant data.
    *   Optional data encryption: All data can be protected using 256-bit AES encryption and data integrity and authenticity is verified using HMAC-SHA256.
    *   Off-site backups: Any data can be stored on any remote host accessible over SSH (as long as Attic is installed).
    *   Backups mountable as filesystems: Backup archives are mountable as userspace filesystems for easy backup verification and restores.

[https://github.com/jborg/attic/](https://github.com/jborg/attic/) || [attic](https://aur.archlinux.org/packages/attic/)<sup><small>AUR</small></sup>

*   **Snebu** — File-level deduplicating snapshot backup with SQLite3 catalog db.
    *   Functionally similar to rsync/snapshot style backups, however doesn't use hardlinks in the filesystem.
    *   Backed up files are stored in lzop-compatible files, in the designated "vault" directory.
    *   Metadata stored in SQLite3 db, linking backup sets to file metadata to compressed files in the vault.
    *   Supports arbitrary retention schedules (such as daily/weekly/monthly) which can be individually expired

[http://www.snebu.com](http://www.snebu.com) || [snebu](https://aur.archlinux.org/packages/snebu/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/snebu)]</sup>

*   **ZBackup** — A globally-deduplicating backup tool, based on the ideas found in rsync.
    *   Parallel LZMA or LZO compression of the stored data
    *   Built-in AES encryption of the stored data
    *   Possibility to delete old backup data
    *   Use of a 64-bit rolling hash, keeping the amount of soft collisions to zero
    *   Repository consists of immutable files. No existing files are ever modified
    *   Possibility to exchange data between repos without recompression

[http://zbackup.org/](http://zbackup.org/) || [zbackup](https://aur.archlinux.org/packages/zbackup/)<sup><small>AUR</small></sup>

#### Graphical

*   **Backerupper** — A simple program for backing up selected directories over a local network. Its main intended purpose is backing up a user's personal data.
    *   Creates `.tar.gz` archives.
    *   Configurable backup frequency, backup time and max copies.

[http://sourceforge.net/projects/backerupper/](http://sourceforge.net/projects/backerupper/) || [backerupper](https://aur.archlinux.org/packages/backerupper/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/backerupper)]</sup>

*   **[Déjà Dup](/index.php/Duplicity "Duplicity")** — A simple GTK+ backup program. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses duplicity as the backend.
    *   Automatic, timed backup configurable in GUI.
    *   Restore wizard.
    *   Integrated into the GNOME Files file manager.
    *   Inherits several features of duplicity.

[https://launchpad.net/deja-dup](https://launchpad.net/deja-dup) || [deja-dup](https://www.archlinux.org/packages/?name=deja-dup)

*   **Synkron** — A folder synchronization tool.
    *   Syncs multiple folders.
    *   Can exclude files from sync based on wildcards.
    *   Restores files.
    *   Cross-platform support.

[http://synkron.sourceforge.net/](http://synkron.sourceforge.net/) || [synkron](https://aur.archlinux.org/packages/synkron/)<sup><small>AUR</small></sup>

#### Console and graphical

*   **[Bacula](https://en.wikipedia.org/wiki/Bacula "wikipedia:Bacula")** — A client-server enterprise level computer backup system for heterogeneous networks.
    *   This is the Swiss army knife of backup solutions.
    *   Can be run on a single machine or used to back up an entire network.
    *   Supports Linux, UNIX, Windows, and Mac OS X backup clients.
    *   Supports a variety of backup devices, including tape libraries.
    *   Can be used to backup to multiple removable storage devices.
    *   Provides or supports command line console, GUI, and web interfaces.
    *   The back-end is a catalog stored in MySQL, PostgreSQL, or SQLite.
    *   Provides extensive documentation.
    *   Appears to be the most downloaded open source backup solution

[http://www.bacula.org](http://www.bacula.org) || [bacula-common](https://aur.archlinux.org/packages/bacula-common/)<sup><small>AUR</small></sup>

## Cloud backups

See also [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services").

*   **[Copy](https://en.wikipedia.org/wiki/Barracuda_Networks#Products "wikipedia:Barracuda Networks")** — A fair solution to shared folders.
    *   15GB free.
    *   Shared folders size are split between people.
    *   Daemon to sync files between the cloud and the computer.
    *   Almost any platform supported.
    *   Offers AES-256 encryption.

[https://www.copy.com/home/](https://www.copy.com/home/) || [copy-agent](https://aur.archlinux.org/packages/copy-agent/)<sup><small>AUR</small></sup>

*   **[CrashPlan](/index.php/CrashPlan "CrashPlan")** — An online/offsite backup solution.
    *   Unlimited online space for very reasonable pricing.
    *   Automatic and incremental backups to multiple destinations.
    *   Intuitive GUI.
    *   Offers encryption and de-duplication.
    *   Software is free for local use.
    *   Restore prevents simultaneous backing up

[http://www.crashplan.com/](http://www.crashplan.com/) || [crashplan](https://aur.archlinux.org/packages/crashplan/)<sup><small>AUR</small></sup>

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — A popular file-sharing service.
    *   A daemon monitors a specified directory, and uploads incremental changes to dropbox.com.
    *   Changes automatically show up on your other computers.
    *   Includes file sharing and a public directory.
    *   You can recover deleted files.
    *   Community written add-ons.
    *   Free accounts have 2GB storage.

[http://www.dropbox.com](http://www.dropbox.com) || [dropbox](https://aur.archlinux.org/packages/dropbox/)<sup><small>AUR</small></sup> [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/)<sup><small>AUR</small></sup>

*   **[Google Drive](https://en.wikipedia.org/wiki/Google_Drive "wikipedia:Google Drive")** — A file storage and synchronization service provided by Google.
    *   Provides cloud storage, file sharing and collaborative editing.
    *   Multiple clients are available.

[https://drive.google.com](https://drive.google.com) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/)<sup><small>AUR</small></sup> (free), [drive](https://aur.archlinux.org/packages/drive/)<sup><small>AUR</small></sup> (free), [insync](https://aur.archlinux.org/packages/insync/)<sup><small>AUR</small></sup> (non-free)

*   **[Jungle Disk](https://en.wikipedia.org/wiki/Jungle_Disk "wikipedia:Jungle Disk")** — An online backup tool that stores its data in Amazon S3 or Rackspace Cloud Files.
    *   A GNOME Files extension.
    *   Only paid plans available.

[http://www.jungledisk.com/](http://www.jungledisk.com/) || [nautilus-jungledisk](https://aur.archlinux.org/packages/nautilus-jungledisk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/nautilus-jungledisk)]</sup>

*   **[MEGA](https://en.wikipedia.org/wiki/Mega_(website) "wikipedia:Mega (website)")** — Successor to the MegaUpload file-sharing service.
    *   Free accounts are 50GB with paid plans available for more space.
    *   Offers encryption and de-duplication.
    *   Usually accessed through its web interface but other tools exist.

[https://mega.co.nz](https://mega.co.nz) || [megatools](https://aur.archlinux.org/packages/megatools/)<sup><small>AUR</small></sup>, [megasync](https://aur.archlinux.org/packages/megasync/)<sup><small>AUR</small></sup>, [megafuse](https://aur.archlinux.org/packages/megafuse/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/megafuse)]</sup>

*   **Nutstore** — A cloud service that lets you sync and share files anywhere.
    *   Multiple file folders sync.
    *   Service for Chinese users.

[http://jianguoyun.com/](http://jianguoyun.com/) || [nutstore](https://aur.archlinux.org/packages/nutstore/)<sup><small>AUR</small></sup>

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak")** — An online backup tool for Windows, Mac and Linux users to back up, share, sync, access and store their data.
    *   Free account holds 2GB as a 60-day trial.
    *   Includes file sharing and a public directory.
    *   Incremental backup and sync are both supported.

[https://spideroak.com/](https://spideroak.com/) || [spideroak-one](https://aur.archlinux.org/packages/spideroak-one/)<sup><small>AUR</small></sup>

*   **[Storage Made Easy](https://en.wikipedia.org/wiki/Storage_Made_Easy "wikipedia:Storage Made Easy")** — Provides unified access to numerous cloud storage services, as well as its own storage.
    *   Free and paid version available.
    *   Free account holds 5GB and allows access to up to three other cloud storage providers.
    *   Supports local directory via fuse, as well as web access.
    *   Supports many cloud storage services, such as Box, Dropbox, Google Drive, Onedrive, and others.

[http://storagemadeeasy.com/](http://storagemadeeasy.com/) || [smestorage](https://aur.archlinux.org/packages/smestorage/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/smestorage)]</sup>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)<sup><small>AUR</small></sup>

*   **[Tarsnap](https://en.wikipedia.org/wiki/Tarsnap "wikipedia:Tarsnap")** — A secure online backup service for BSD, Linux, OS X, Solaris and Windows (through Cygwin).
    *   Compressed encrypted backups to Amazon S3 Servers.
    *   Automate via [cron](/index.php/Cron "Cron").
    *   Incremental backups.
    *   Backup any files or directories.
    *   Command line only client.
    *   Pay only for usage (bandwidth and storage).

[http://www.tarsnap.com](http://www.tarsnap.com) || [tarsnap](https://www.archlinux.org/packages/?name=tarsnap)

*   **[iDrive](https://en.wikipedia.org/wiki/IDrive_Inc. "wikipedia:IDrive Inc.")** — Universal Online Backup.
    *   Multiple Device Backup.
    *   Online File Sync.
    *   Real-Time Backup.
    *   Backup and Access from Mobile Devices.
    *   Remote Manage.
    *   No GUI Front end for Linux, command line based. A wrapper script is available to make it easier to use.

[https://www.idrive.com/](https://www.idrive.com/) || [idevsutil](https://aur.archlinux.org/packages/idevsutil/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/idevsutil)]</sup>, [idrive-wrapper](https://aur.archlinux.org/packages/idrive-wrapper/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/idrive-wrapper)]</sup>

*   **CloudBacko** — Enterprise-grade cloud backup tool for Linux, Mac and Windows.
    *   Closed source. Free, Lite and Pro versions available.
    *   Written in Java.
    *   Encrypted backup to multiple cloud destinations.
    *   Supports multiple cloud destinations combined as one storage pool.
    *   No installation required in Free version.
    *   GUI frontend for Linux in Pro version.
    *   Virtual machine backup available in Pro version.

[http://www.cloudbacko.com/](http://www.cloudbacko.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Cooperative storage cloud backups

A [cooperative storage cloud](https://en.wikipedia.org/wiki/Cooperative_storage_cloud "wikipedia:Cooperative storage cloud") is a decentralized model of networked online storage where data is stored on multiple computers, hosted by the participants cooperating in the cloud.

*   **[Symform](http://www.symform.com)** — A peer-to-peer cloud backup service.
    *   Unlimited free backup in exchange for 2:1 storage space contribution with an always-connected device (at least 80% uptime).
    *   [Payment options exist](http://www.symform.com/our-solutions/pricing/).
    *   First 10GB of backup storage is free (no contribution needed).
    *   In addition to paid support, support plans in exchange for extended contribution (300GB+) exist.
    *   Automatic and incremental backups.
    *   Data is encrypted before leaving the computer, though keys are also stored on the Symform's servers.[[2]](http://virtualserverguy.com/blog/2012/12/19/symform-security-analysis)
    *   Customizable limits for bandwidth consumption.
    *   Ability to have a local copy ("Hot Copy") of the backed up data on a different disk or computer.
    *   Ability to have synchronized folders between nodes (Dropbox-like).
    *   Closed source, using mono. Windows clients available.

[http://www.symform.com/](http://www.symform.com/) || [symform](https://aur.archlinux.org/packages/symform/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/symform)]</sup>

## Non-incremental backups

Another type of backups are those used in case of a disaster. These include application that allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. The contains complete system images from one or more specific points in time and are frequently used by to record known good configurations.

*   **Q7Z** — P7Zip GUI for Linux, which attempts to simplify data compression and backup. It can create the following archive types: 7z, BZip2, Zip, GZip, Tar.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

[http://k7z.sourceforge.net/](http://k7z.sourceforge.net/) || [q7z](https://aur.archlinux.org/packages/q7z/)<sup><small>AUR</small></sup>

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports ext2, ext3, hfs+, reiser3.5, reiser3.6, reiser4, ext4 and btrfs.
    *   Supports compression.

[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

[http://www.redobackup.org/](http://www.redobackup.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive, or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.

[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — A disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.

[http://www.partimage.org/Main_Page](http://www.partimage.org/Main_Page) || [partimage](https://www.archlinux.org/packages/?name=partimage)

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

[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)<sup><small>AUR</small></sup>

## Versioning systems

These are traditionally used for keeping track of software development; but if you want to have a simple way to manage your config files in one directory, it might be a good solution.

### Version control systems

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Git](/index.php/Git "Git")** — A distributed revision control and source code management system with an emphasis on speed.
    *   Very easy creation, merging, and deletion of branches.
    *   Nearly all operations are performed locally, giving it a huge speed advantage on centralized systems.
    *   Has a "staging area" or "index", this is an intermediate area where commits can be formatted and reviewed before completing the commit.
    *   Does not handle binary files very well.

[http://git-scm.com/](http://git-scm.com/) || [git](https://www.archlinux.org/packages/?name=git)

*   **[Subversion](/index.php/Subversion "Subversion")** — A full-featured centralized version control system originally designed to be a better CVS.
    *   Renamed/copied/moved/removed files retain full revision history.
    *   Native support for binary files, with space-efficient binary-diff storage.
    *   Costs proportional to change size, not to data size.
    *   Allows arbitrary metadata ("properties") to be attached to any file or directory.

[http://subversion.apache.org/](http://subversion.apache.org/) || [subversion](https://www.archlinux.org/packages/?name=subversion)

*   **[Mercurial](/index.php/Mercurial "Mercurial")** — A distributed version control system written in Python and similar in many ways to Git.
    *   Platform independent.
    *   Support for [extensions](http://mercurial.selenic.com/wiki/UsingExtensions).
    *   A set of commands consistent with Subversion.
    *   Supports tags.

[http://mercurial.selenic.com/](http://mercurial.selenic.com/) || [mercurial](https://www.archlinux.org/packages/?name=mercurial)

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

### VCS-based backups

*   **Gibak** — A backup system based on [Git](/index.php/Git "Git").
    *   Supports binary diffs.
    *   Uses all of Git's features (such as `.gitignore` for filtering files).
    *   Uses Git's hook system to save information that Git does not (permissions, mtime, empty directories, etc).

[https://github.com/pangloss/gibak](https://github.com/pangloss/gibak) || [gibak](https://aur.archlinux.org/packages/gibak/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gibak)]</sup>

*   **bup** — A fledgling Git-based backup solution written in Python and C.
    *   Uses a rolling checksum algorithm (similar to rsync) to split large files into chunks.
    *   Can back up directly to a remote bup server.
    *   Has an improved index format to allow you to track many files.

[https://github.com/bup/bup](https://github.com/bup/bup) || [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/)<sup><small>AUR</small></sup>

*   **ColdStorage** — Another backup tool using Git at its core, written in [Qt](/index.php/Qt "Qt").

[http://gitorious.org/coldstorage](http://gitorious.org/coldstorage) || [coldstorage-git](https://aur.archlinux.org/packages/coldstorage-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/coldstorage-git)]</sup>

## See also

*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Backup_programs&oldid=416028](https://wiki.archlinux.org/index.php?title=Backup_programs&oldid=416028)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Data compression and archiving](/index.php/Category:Data_compression_and_archiving "Category:Data compression and archiving")
*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")

Hidden categories:

*   [Pages with missing package links](/index.php/Category:Pages_with_missing_package_links "Category:Pages with missing package links")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
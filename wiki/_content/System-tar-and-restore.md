# System-tar-and-restore

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**System-tar-and-restore** contains two bash scripts, **backup.sh** and **restore.sh**. The former makes a tar backup of your system. The latter restores the backup or transfers your system using [rsync](https://www.archlinux.org/packages/?name=rsync) in desired partition(s). The scripts include two interfaces, **cli** and **dialog** (ncurses). If you plan to use the second, install [dialog](https://www.archlinux.org/packages/?name=dialog) from the [official repositories](/index.php/Official_repositories "Official repositories"). Also a [gui wrapper](https://github.com/tritonas00/system-tar-and-restore#gui) is available. Install [gtkdialog](https://www.archlinux.org/packages/?name=gtkdialog) and run `star-gui.sh` as root in order to use it.

## Contents

*   [1 Installation](#Installation)
*   [2 Features](#Features)
*   [3 Backup](#Backup)
*   [4 Restore/Transfer](#Restore.2FTransfer)

## Installation

Install [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") or from [archlinuxgr-any](https://wiki.archlinux.org/index.php/Unofficial_user_repositories#archlinuxgr-any) repo.

## Features

*   Full or partial backup
*   Restore or transfer to the same or different disk/partition layout.
*   Restore or transfer to an external device such as usb flash drive, sd card etc.
*   Restore a BIOS-based system to UEFI and vice versa.
*   Prepare a system in a virtual machine (such as [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)), back it up and restore it in a normal machine.

## Backup

The _backup.sh_ script makes a tar backup of your system. You will be asked for:

*   **Destination directory**: Where you want to save the backup. Default is `/`.
*   **Archive name**: A desired name for the backup. Default is `Backup-$(hostname)-$(date +%Y-%m-%d-%T)`.
*   **/home directory options**: You have three options: fully include it, keep only its hidden files and folders (which are necessary to login and keep basic settings) or completely exclude it (in case it's located in separate partition and you want to use that in restore).
*   **Compression**: You can choose between gzip, bzip2, xz and none (for no compression). Gzip should be fine.
*   **Archiver options**: You can pass your own extra options in the archiver. See `tar --help` for more info.
*   **Passphrase and encryption method**: Enter a passphrase if you want to encrypt the archive and select encryption method (openssl or gpg). Leave empty for no encryption.

**Note:**

*   The script excludes all dynamically populated directories and some tmpfs locations: `/run/*`, `/proc/*`, `/dev/*`, `/media/*`, `/sys/*`, `/tmp/*`, `/mnt/*`, `.gvfs`, `/var/run/*`, `/var/lock/*`, `lost+found`.
*   It's advisable to add `--acls --xattrs` and `--selinux` (if available) in additional tar options.

You can review all your settings in the summary and also view the supported bootloaders found on your system ([grub](https://www.archlinux.org/packages/?name=grub) and [syslinux](https://www.archlinux.org/packages/?name=syslinux)).

Also you can set all the options in `/etc/backup.conf`. Copy from the sample file `/usr/share/system-tar-and-restore/backup.conf` and edit it to your needs.

All options can also be passed using arguments. See `backup.sh --help`, `man system-tar-and-restore` or [here](https://github.com/tritonas00/system-tar-and-restore#examples-using-arguments).

When the process completes, you may want to check `backup.log` file in the same directory with the backup archive.

**Warning:**

*   If you plan to restore in [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID") or [Dm-crypt](/index.php/Dm-crypt "Dm-crypt") you need to add the corresponding hooks in `/etc/mkinitpcio.conf` **before** the backup.
*   If you plan to restore in [GPT](https://wiki.archlinux.org/index.php/GUID_Partition_Table) with [syslinux](https://www.archlinux.org/packages/?name=syslinux), make sure you have [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) installed **before** the backup.
*   If you plan to restore in [UEFI](https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface) make sure you have [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) and [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) installed **before** the backup.

## Restore/Transfer

The _restore.sh_ script has two modes: **Restore** and **Transfer**. The first uses the above created archive to extract it in desired partition(s). The second transfers your system in desired partition(s) using [rsync](https://www.archlinux.org/packages/?name=rsync). Then, in both cases, generates the target system's fstab, rebuilds initramfs for every available kernel, generates locales and finally installs and configures the selected bootloader.

**Note:** In order to restore a backup in UEFI, you must run the script from a UEFI environment.

**Warning:** The system running the restore script and the target system (the one you want to restore), must have the same architecture (for chroot to work).

Boot from a livecd (preferably an Arch Linux based) or another system, prepare your target partition(s) and start the script. You will be asked for:

*   **Target partitions**: You must specify at least one target root partition. Optionally you can choose any other partition for your /home, /boot, swap or custom mount points (/var /opt etc.) and in case of UEFI a target [ESP](https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition) partition and it's mount point.
*   **Mount options**: You can specify alternative comma-seperated mount options for the target root partition. Defaults are `defaults,noatime`.
*   **Btrfs subvolumes**: If the target root filesystem is [Btrfs](/index.php/Btrfs "Btrfs"), you will be prompted for root subvolume name. Leave empty if you dont want subvolumes. Also you can specify other subvolumes. Just enter the paths (/home /var /usr etc.) seperated by space. Recommended root subvolume name is `__active`.
*   **Bootloader**: In BIOS systems you can choose [grub](https://www.archlinux.org/packages/?name=grub) or [syslinux](https://www.archlinux.org/packages/?name=syslinux) and the target disk. If you select a raid array as bootloader disk, the script will install the bootloader in all disks that the array contains. In case of UEFI you can choose grub, EFISTUB/efibootmgr or Systemd/bootctl. Also you can define additional kernel options.
*   **Select mode**: In _Restore mode_ you have to specify the backup archive location, local or remote (you will need [wget](https://www.archlinux.org/packages/?name=wget)). If the archive is encrypted you will be prompted for the passphrase. In _Transfer mode_ you will have to specify if you want to transfer your entire /home directory or only it's hidden files and folders (which are necessary to login and keep basic settings).
*   **Tar/Rsync options**: You may want to specify any additional options. See `tar --help` or `rsync --help` for more info.

**Note:**

In Transfer mode the script excludes all dynamically populated directories and some tmpfs locations: `/run/*`, `/proc/*`, `/dev/*`, `/media/*`, `/sys/*`, `/tmp/*`, `/mnt/*`, `/home/*/.gvfs`, `/var/run/*`, `/var/lock/*`, `lost+found`.

**Warning:** If you specified any of these GNU Tar options: `--acls --xattrs --selinux` in the backup process, you must specify them again here.

You can review all your settings in the summary.

All options can also be passed using arguments. See `restore.sh --help`, `man system-tar-and-restore` or [here](https://github.com/tritonas00/system-tar-and-restore#examples-using-arguments).

When the process completes, you may want to check `/tmp/restore.log`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=System-tar-and-restore&oldid=414895](https://wiki.archlinux.org/index.php?title=System-tar-and-restore&oldid=414895)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")
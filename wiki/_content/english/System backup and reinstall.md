This tutorial is to explain how to backup the system configurations and other likewise items in order to expedite a reinstall process.

## Contents

*   [1 Justification](#Justification)
*   [2 Notes](#Notes)
*   [3 Backup](#Backup)
    *   [3.1 Configurations](#Configurations)
    *   [3.2 Package lists](#Package_lists)
    *   [3.3 Package tarballs](#Package_tarballs)
*   [4 Reinstall](#Reinstall)
    *   [4.1 Base install](#Base_install)
    *   [4.2 Locale generation](#Locale_generation)
    *   [4.3 Package reinstall](#Package_reinstall)
    *   [4.4 Restore configurations](#Restore_configurations)
*   [5 Details](#Details)

## Justification

The justification for this tutorial generally is:

*   The system architecture is desired to be changed (e.g. 32-bit to 64-bit)
*   A system problem has occurred and troubleshooting has failed (external help from the wiki or forums is unavailable)

The discouragement for this tutorial is:

*   The system installation that is extremely outdated. Because package and configurations change over time this method may be ineffectual and possibly even harmful (in terms of dataloss). For installations older than six months (and sometimes even less) consider reinstalling from the onset according to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or the [Installation guide](/index.php/Installation_guide "Installation guide").

## Notes

A few things to know about this tutorial before reading:

*   A backup destination has been throughout defined:

```
/mnt/backup/amiga_$(date +%F).../

```

*   The system installation is recommended to be updated and configurations merged (if doable). This will keep backup configurations equivocal with their reinstalled counterparts.
*   The backup is recommended to be saved on a separate storage disk. This will ease the process of the backup.

## Backup

The backup process will involve these steps:

1.  Backup system configurations
2.  Record the package list(s)
3.  Backup the package tarballs

### Configurations

To create a backup in Linux, two common utilities are generally employed [tar](/index.php/Tar "Tar") and [rsync](/index.php/Rsync "Rsync").

A typical method to do multi-file backups is to create a list of the required files. `tar` and `rsync` both have the ability to define a file-list in an include and an exclude file. The format to use is one file per line with the full path. For example:

```
include.txt
/etc/fstab
/etc/modules-load.d/
/etc/pacman.conf
...

```

```
exclude.txt
# only testing
/etc/modules-load.d/loop*

```

To create a backup from the file-list, with `tar` and `rsync` respectively do:

```
tar --create --xz --files-from=include.txt --exclude-from=exclude.txt --file /mnt/backup/amiga_$(date +%F)_syscfg.tar.xz
rsync --archive --files-from=include.txt --exclude-from=exclude.txt / /mnt/backup/amiga_$(date +%F)_syscfg/

```

(The include file _must_ list valid files or the programs will exit with an error. However, the exclude file does _not_ have to list valid files because it allows glob pattern matches.)

(The `rsync` command defines the source directory as the root directory (`/`), this is necessary to coincide with the full path specified in the file listing.)

See also [Full System Backup with tar](/index.php/Full_System_Backup_with_tar "Full System Backup with tar") and [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

### Package lists

A listing can be created of installed packages of both _official_ repository packages and _local_ packages. These lists can be used upon the reinstall to define the package selection.

To create a list of all _official_ repository installed packages do:

```
$ pacman -Qqe | grep -v "$(pacman -Qqm)" > /mnt/backup/amiga_$(date +%F)_pkglist-off.txt

```

To create a list of all _local_ installed packages do (includes packages installed from the [AUR](/index.php/AUR "AUR")):

```
$ pacman -Qqm > /mnt/backup/amiga_$(date +%F)_pkglist-loc.txt

```

See also [Pacman tips#Backing up and retrieving a list of installed packages](/index.php/Pacman_tips#Backing_up_and_retrieving_a_list_of_installed_packages "Pacman tips").

### Package tarballs

By creating a backup of package tarballs that have been previously downloaded time can be saved. During a reinstall a package cache can be defined to the package manager of the previous package tarballs.

To remove package tarballs that are uninstalled or older versions do:

```
# pacman -Sc

```

To backup package tarballs:

```
# cp /var/cache/pacman/pkg/* /mnt/backup/amiga_$(date +%F)_pkg/

```

## Reinstall

The reinstall process will involve these steps:

1.  Install the base system
2.  Generate a locale
3.  Install previous packages
4.  Restore previous configurations

### Base install

Install the base system normally as directed in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or [Installation guide](/index.php/Installation_guide "Installation guide") except without editing the configurations.

### Locale generation

Generating a locale will be the one exception where editing a configuration will be necessary (a few packages use scripts to install certain features that require a locale be present). Read [Locale](/index.php/Locale "Locale") to learn more.

### Package reinstall

To reinstall packages from the _official_ repositories (using the backup package cache and the package list):

```
pacman --needed --cachedir /mnt/backup/amiga_$(date +%F)_pkg/ -S - < /mnt/backup/amiga_$(date +%F)_pkglist-off.txt

```

To reinstall packages that are _local_ will depend on the method or program that was originally used. If the package tarballs exist for them and they are in the same cache, the above command can be used with the `...pkglist-loc.txt` file. If the packages do not have a package tarball and are AUR packages, use a [AUR Helper](/index.php/AUR_Helper "AUR Helper") to reinstall them:

```
AURHELPER ... < /mnt/backup/amiga_$(date +%F)_pkglist-off.txt

```

### Restore configurations

When all the packages have been installed the configurations can be restored with `tar` and `rsync` respectively:

```
tar --extract --verbose --file /mnt/backup/amiga_$(date +%F)_syscfg.tar.xz -C /mnt/install
rsync --archive /mnt/backup/amiga_$(date +%F)_syscfg/ /mnt/install/

```

## Details

*   Installation guide procedures should still be observed and keep in mind that they change temporally.
*   Partition layout changes will need to be attention paid to. If device designation has changed `/etc/fstab`, bootloader configuration will need to be updated.
*   Non-default options for the kernel ram disk will require the rebuilding if it before rebooting.
*   Edits in the kernel ram disk configuration will necessitate its rebuilding before rebooting.
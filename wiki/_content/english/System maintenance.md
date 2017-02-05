Regular system maintenance is necessary for the proper function of Arch over a period of time. Timely maintenance is a practice many users get accustomed to.

## Contents

*   [1 Check for errors](#Check_for_errors)
    *   [1.1 Failed systemd services](#Failed_systemd_services)
    *   [1.2 Logfiles](#Logfiles)
*   [2 Backup](#Backup)
    *   [2.1 Configuration files](#Configuration_files)
    *   [2.2 List of installed packages](#List_of_installed_packages)
    *   [2.3 Pacman database](#Pacman_database)
    *   [2.4 LUKS headers](#LUKS_headers)
*   [3 Upgrading the system](#Upgrading_the_system)
    *   [3.1 Avoid certain pacman commands](#Avoid_certain_pacman_commands)
    *   [3.2 Partial upgrades are unsupported](#Partial_upgrades_are_unsupported)
    *   [3.3 Read before upgrading the system](#Read_before_upgrading_the_system)
    *   [3.4 Act on alerts during an upgrade](#Act_on_alerts_during_an_upgrade)
    *   [3.5 Deal promptly with new configuration files](#Deal_promptly_with_new_configuration_files)
    *   [3.6 Revert broken updates](#Revert_broken_updates)
*   [4 Use the package manager to install software](#Use_the_package_manager_to_install_software)
    *   [4.1 Choose open-source drivers](#Choose_open-source_drivers)
    *   [4.2 Be careful with unofficial packages](#Be_careful_with_unofficial_packages)
    *   [4.3 Update the mirrorlist](#Update_the_mirrorlist)
*   [5 Clean the filesystem](#Clean_the_filesystem)
    *   [5.1 Package cache](#Package_cache)
    *   [5.2 Unused packages (orphans)](#Unused_packages_.28orphans.29)
    *   [5.3 Old configuration files](#Old_configuration_files)
    *   [5.4 Broken symlinks](#Broken_symlinks)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Use proven software packages](#Use_proven_software_packages)
    *   [6.2 Install the linux-lts package](#Install_the_linux-lts_package)
*   [7 See Also](#See_Also)

## Check for errors

### Failed systemd services

Check if any systemd services have entered in a failed state:

```
$ systemctl --failed

```

See [Systemd#Analyzing the system state](/index.php/Systemd#Analyzing_the_system_state "Systemd") for more information.

### Logfiles

Look for errors in the log files located at `/var/log`, as well as high priority errors in the systemd journal:

```
# journalctl -p 3 -xb

```

See [Systemd#Journal](/index.php/Systemd#Journal "Systemd") for more information.

See [Xorg#Troubleshooting](/index.php/Xorg#Troubleshooting "Xorg") for information on where and how [Xorg](/index.php/Xorg "Xorg") logs errors.

## Backup

Create backups of important data at regular intervals. Those data include configuration files, installed packages and directories such as `/etc`, `/home`, `/var` and for server installations, also `/srv`.

See [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for many alternative applications that may better suit your case. See [Category:System recovery](/index.php/Category:System_recovery "Category:System recovery") for other articles of interest.

Backups may be automated with [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

### Configuration files

Before editing any configuration files, create a backup so that you can revert to a working version in case of problems. Editors like [vim](/index.php/Vim "Vim") and [emacs](/index.php/Emacs "Emacs") can do this automatically, as well as tools like [etckeeper](/index.php/Etckeeper "Etckeeper") which keep `/etc` in a version control system (VCS); see [dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles") for more.

### List of installed packages

Maintain a list of all installed packages, so that if a complete re-installation is inevitable, it is easier to re-create the original environment.

See [Pacman tips#List of installed packages](/index.php/Pacman_tips#List_of_installed_packages "Pacman tips") for details.

### Pacman database

See [Pacman tips#Back-up the pacman database](/index.php/Pacman_tips#Back-up_the_pacman_database "Pacman tips").

### LUKS headers

It can make sense to periodically check and synchronize the backups of LUKS-encrypted partition headers, especially if passphrases have been revoked. See [Dm-crypt/Device encryption#Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## Upgrading the system

It is recommended to perform full system upgrades regularly, to enjoy both the latest bug fixes and security updates, and also to avoid having to deal with too many package upgrades that require manual intervention at once. See [Pacman#Upgrading packages](/index.php/Pacman#Upgrading_packages "Pacman") for details.

Make sure to have the Arch install media or another Linux "live" CD/USB available so you can easily rescue your system if there is a problem after updating. If you are running Arch in a production environment, or cannot afford downtime for any reason, test changes to configuration files, as well as updates to software packages, on a non-critical duplicate system first. Then, if no problems arise, roll out the changes to the production system.

If the system has packages from the [AUR](/index.php/AUR "AUR"), carefully upgrade all of them.

### Avoid certain pacman commands

Avoid doing [partial upgrades](#Partial_upgrades_are_unsupported), i.e. never run `pacman -Sy` and instead use `pacman -Syu`.

Avoid using the `--force` option with pacman, **especially** in commands such as `pacman -Syu --force` involving more than one package. The `--force` option ignores file conflicts and can even cause file loss when files are relocated between different packages! In a properly maintained system, it should only be used when explicitly recommended by the Arch developers (see [#Read before upgrading the system](#Read_before_upgrading_the_system)).

Avoid using the `-d` option with pacman. `pacman -Rdd package` skips dependency checks during package removal. As a result, a package providing a critical dependency could be removed, resulting in a broken system.

### Partial upgrades are unsupported

Arch Linux is a [rolling release](https://en.wikipedia.org/wiki/rolling_release versions are pushed to the repositories, the developers and Trusted Users rebuild all the packages in the repositories that need to be rebuilt against the libraries. For example, if two packages depend on the same library, upgrading only one package might also upgrade the library (as a dependency), which might then break the other package which depends on an older version of the library.

That is why partial upgrades are **not supported**. Do not use `pacman -Sy package` or any equivalent such as `pacman -Sy` followed by `pacman -S package`, **always** upgrade (with `pacman -Syu`) before installing a package. Be very careful when using `IgnorePkg` and `IgnoreGroup` for the same reason. If the system has locally installed packages (such as [AUR](/index.php/AUR "AUR") packages), users will need to rebuild them when their dependencies receive a [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bump.

If a partial upgrade scenario has been created, and binaries are broken because they cannot find the libraries they are linked against, **do not "fix" the problem simply by symlinking**. Libraries receive [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bumps when they are **not backwards compatible**. A simple `pacman -Syu` to a properly synced mirror will fix the problem as long as *pacman* is not broken.

The bash script *checkupdates*, included with the pacman package, provides a safe way to check for upgrades to installed packages without running a system update at the same time. See also [BBS##1563725](https://bbs.archlinux.org/viewtopic.php?pid=1563725#p1563725).

### Read before upgrading the system

Before upgrading Arch, always read the latest [Arch News](https://www.archlinux.org/news/) to find out if there are any major software or configuration changes with the latest packages. Before upgrading fundamental software (such as the [kernel](/index.php/Kernel "Kernel"), [xorg](/index.php/Xorg "Xorg"), [systemd](/index.php/Systemd "Systemd"), or [glibc](https://www.archlinux.org/packages/?name=glibc)) to a new version, look over the appropriate [forum](https://bbs.archlinux.org/) to see if there have been any reported problems.

### Act on alerts during an upgrade

When upgrading the system, be sure to pay attention to the alert notices provided by [pacman](/index.php/Pacman "Pacman"). If any additional actions are required by the user, be sure to take care of them right away. If a pacman alert is confusing, search the forums and the recent news posts for more detailed instructions.

### Deal promptly with new configuration files

When pacman is invoked, `.pacnew` and `.pacsave` files can be created. Pacman provides notice when this happens and users must deal with these files promptly. Users are referred to the [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") wiki page for detailed instructions.

Also, think about other configuration files you may have copied or created. If a package had an example configuration that you copied to your home directory, check to see if a new one has been created.

### Revert broken updates

If a package update is expected/known to cause problems, packagers will ensure that pacman displays an appropriate message when the package is updated. If experiencing trouble after an update, double-check pacman's output by looking at `/var/log/pacman.log`.

At this point, only after ensuring there is no information available through pacman, there is no relative news on [https://www.archlinux.org/](https://www.archlinux.org/), and there are no forum posts regarding the update, consider seeking help on the [forum](https://bbs.archlinux.org), over [IRC](/index.php/IRC "IRC"), or by [downgrading](/index.php/Downgrading "Downgrading") the offending package.

## Use the package manager to install software

[Pacman](/index.php/Pacman "Pacman") does a much better job than you at keeping track of files. If you install things manually you *will*, sooner or later, forget what you did, forget where you installed to, install conflicting software, install to the wrong locations, etc. Instead, learn how to [create a package](/index.php/Creating_packages "Creating packages").

To clean up improperly installed files, use [lostfiles](https://aur.archlinux.org/packages/lostfiles/) or see [Pacman/Tips and tricks#Identify files not owned by any package](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks").

See also [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)), which allows creating a commented configuration file with package lists and changed files. This allows documenting the reason why a package is installed, so it's clear when it's no longer needed.

### Choose open-source drivers

Always try open source drivers before resorting to proprietary drivers. Most of the time, open source drivers are more stable and reliable than proprietary drivers. Open source driver bugs are fixed more easily and quickly. While proprietary drivers can offer more features and capabilities, this can come at the cost of stability. To avoid this dilemma, try to choose hardware components known to have mature open source driver support with full features. Information about hardware with open source Linux drivers is available at [linux-drivers.org](http://www.linux-drivers.org/).

### Be careful with unofficial packages

Use precaution when using packages from the [AUR](/index.php/AUR "AUR") or an [unofficial user repository](/index.php/Unofficial_user_repository "Unofficial user repository"). Most are supplied by regular users and thus may not have the same standards as those in the official repositories. Be careful with [AUR helpers](/index.php/AUR_helpers "AUR helpers") which automate installation of AUR packages. **Always** check PKGBUILDs for sanity and signs of mistake or malicious code before building and/or installing the package.

To simplify maintenance, limit the amount of unofficial packages used. Make periodic checks on which are in actual use, and remove (or replace with their official counterparts) any others. See [pacman/Tips and tricks#Maintenance](/index.php/Pacman/Tips_and_tricks#Maintenance "Pacman/Tips and tricks") for useful commands.

### Update the mirrorlist

Update pacman's mirrorlist, as the quality of mirrors can vary over time, and some might go offline or their download rate might degrade.

See [mirrors](/index.php/Mirrors "Mirrors") for details.

## Clean the filesystem

When looking for files to remove, it is important to find the files that take up the most disk space. Programs that help with this are found in:

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications").
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications").

### Package cache

Remove unwanted `.pkg` files from `/var/cache/pacman/pkg/` to free up disk space.

See [Pacman#Cleaning the package cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman") for more information.

### Unused packages (orphans)

Remove unused packages from the system to free up disk space and simplify maintenance.

See [Pacman/Tips and tricks#Removing unused packages (orphans)](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29 "Pacman/Tips and tricks") for details.

### Old configuration files

Old configuration files may conflict with newer software versions, or corrupt over time. Remove unneeded configurations periodically, particularly in your home folder and `~/.config`. For similar reasons, be careful when sharing home folders between installations.

Look for the following folders:

*   `~/.config/` -- where apps stores their configuration
*   `~/.cache/` -- cache of some programs may grow in size
*   `~/.local/share/` -- old files may be lying there

See [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support") for more information.

To keep the home directory clean from temporary files created at the wrong place, it is a good idea to manage a list of unwanted files and remove them regularly, for example with [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) can be used to find and optionally remove duplicate files, empty files, recursive empty directories and broken symlinks.

### Broken symlinks

Old, broken symbolic links might be sitting around your system; you should remove them. Examples on achieving this can be found [here](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) and [here](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

To quickly list all the broken symlinks of your system, use:

```
 # find -xtype l -print

```

Then inspect and remove unnecessary entries from this list.

## Tips and tricks

The following tips are generally not required, but certain users may find them useful.

### Use proven software packages

Arch's rolling releases can be a boon for users who want to try the latest features and get upstream updates as soon as possible, but they can also make system maintenance more difficult. To simplify maintenance and improve stability, try to avoid cutting edge software and install only mature and proven software. Such packages are less likely to receive difficult upgrades such as major configuration changes or feature removals. Prefer software that has a strong and active development community, as well as a high number of competent users, in order to simplify support in the event of a problem.

Avoid any use of the testing repository, even individual packages from testing. These packages are experimental and not suitable for a stable system. Similarly, avoid development packages which are built directly from upstream sources. These are usually found in the [AUR](/index.php/AUR "AUR"), with names including things like: "dev", "devel", "svn", "cvs", "git", etc.

### Install the linux-lts package

The [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) package is an alternative Arch kernel package, and is available in the [core](/index.php/Official_repositories#core "Official repositories") repository. This particular kernel version has long-term support (LTS) from upstream, including security fixes and some feature backports. It is useful if you prefer the stability of less-frequent kernel updates or if you want a fallback kernel in case a new kernel version causes problems.

To make it available as a boot option, you will need to update your [bootloader](/index.php/Bootloader "Bootloader")'s configuration file to use the LTS kernel and ram disk: `vmlinuz-linux-lts` and `initramfs-linux-lts.img`.

## See Also

*   [Arch News Bash Script](https://bbs.archlinux.org/viewtopic.php?id=146850)
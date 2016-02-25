The [pacman](https://www.archlinux.org/pacman/) [package manager](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") is one of the major distinguishing features of Arch Linux. It combines a simple binary package format with an easy-to-use [build system](/index.php/Arch_Build_System "Arch Build System"). The goal of *pacman* is to make it possible to easily manage packages, whether they are from the [official repositories](/index.php/Official_repositories "Official repositories") or the user's own builds.

*pacman* keeps the system up to date by synchronizing package lists with the master server. This server/client model also allows the user to download/install packages with a simple command, complete with all required dependencies.

*pacman* is written in the C programming language and uses the *.pkg.tar.xz* package format.

**Tip:** The [pacman](https://www.archlinux.org/packages/?name=pacman) package contains other useful tools such as **makepkg**, **pactree**, **vercmp**, and [checkupdates](/index.php/Checkupdates "Checkupdates"). Run `pacman -Qlq pacman | grep bin` to see the full list.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Installing packages](#Installing_packages)
        *   [1.1.1 Installing specific packages](#Installing_specific_packages)
        *   [1.1.2 Installing package groups](#Installing_package_groups)
    *   [1.2 Removing packages](#Removing_packages)
    *   [1.3 Upgrading packages](#Upgrading_packages)
    *   [1.4 Querying package databases](#Querying_package_databases)
        *   [1.4.1 Database structure](#Database_structure)
    *   [1.5 Cleaning the package cache](#Cleaning_the_package_cache)
    *   [1.6 Additional commands](#Additional_commands)
*   [2 Configuration](#Configuration)
    *   [2.1 General options](#General_options)
        *   [2.1.1 Color output](#Color_output)
        *   [2.1.2 Comparing versions before updating](#Comparing_versions_before_updating)
        *   [2.1.3 Skip package from being upgraded](#Skip_package_from_being_upgraded)
        *   [2.1.4 Skip package group from being upgraded](#Skip_package_group_from_being_upgraded)
        *   [2.1.5 Skip files from being installed to system](#Skip_files_from_being_installed_to_system)
        *   [2.1.6 Maintain several configuration files](#Maintain_several_configuration_files)
    *   [2.2 Repositories](#Repositories)
    *   [2.3 Package security](#Package_security)
    *   [2.4 Hooks](#Hooks)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 "Failed to commit transaction (conflicting files)" error](#.22Failed_to_commit_transaction_.28conflicting_files.29.22_error)
    *   [3.2 "Failed to commit transaction (invalid or corrupted package)" error](#.22Failed_to_commit_transaction_.28invalid_or_corrupted_package.29.22_error)
    *   [3.3 "Failed to init transaction (unable to lock database)" error](#.22Failed_to_init_transaction_.28unable_to_lock_database.29.22_error)
    *   [3.4 Packages cannot be retrieved on installation](#Packages_cannot_be_retrieved_on_installation)
    *   [3.5 The same package is upgraded repeatedly](#The_same_package_is_upgraded_repeatedly)
    *   [3.6 Search for a package that contains a specific file](#Search_for_a_package_that_contains_a_specific_file)
    *   [3.7 pacman is broken beyond repair](#pacman_is_broken_beyond_repair)
    *   [3.8 pacman crashes during an upgrade](#pacman_crashes_during_an_upgrade)
    *   [3.9 pacman crashes the official installation media](#pacman_crashes_the_official_installation_media)
    *   [3.10 "Unable to find root device" error after rebooting](#.22Unable_to_find_root_device.22_error_after_rebooting)
    *   [3.11 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [3.12 Request on importing PGP keys](#Request_on_importing_PGP_keys)
    *   [3.13 Signature from "User <email@archlinux.org>" is invalid, installation failed](#Signature_from_.22User_.3Cemail.40archlinux.org.3E.22_is_invalid.2C_installation_failed)
    *   [3.14 "Warning: current locale is invalid; using default "C" locale" error](#.22Warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.22_error)
    *   [3.15 pacman does not honor proxy settings](#pacman_does_not_honor_proxy_settings)
    *   [3.16 How do I reinstall all packages, retaining information on whether something was explicitly installed or as a dependency?](#How_do_I_reinstall_all_packages.2C_retaining_information_on_whether_something_was_explicitly_installed_or_as_a_dependency.3F)
    *   [3.17 "Cannot open shared object file" error](#.22Cannot_open_shared_object_file.22_error)
    *   [3.18 Freeze of package downloads](#Freeze_of_package_downloads)
    *   [3.19 Failed retrieving file 'core.db' from mirror](#Failed_retrieving_file_.27core.db.27_from_mirror)
*   [4 See also](#See_also)

## Usage

What follows is just a small sample of the operations that *pacman* can perform. To read more examples, refer to [man pacman](https://www.archlinux.org/pacman/pacman.8.html).

**Tip:** For those who have used other Linux distributions before, there is a helpful [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") article.

### Installing packages

**Note:** Packages often have a series of [optional dependencies](/index.php/PKGBUILD#optdepends "PKGBUILD") which are packages that provide additional functionality to the application, albeit not strictly required for running it. When installing a package, *pacman* will list its optional dependencies among the output messages, but they will not be found in `pacman.log`: use the [pacman -Si](#Querying_package_databases) command to view the optional dependencies of a package, together with short descriptions of their functionality.

**Warning:** When installing packages in Arch, avoid refreshing the package list without [upgrading the system](#Upgrading_packages) (for example, when a [package is no longer found](#Packages_cannot_be_retrieved_on_installation) in the official repositories). In practice, do **not** run `pacman -Sy *package_name*` instead of `pacman -Sy**u** *package_name*`, as this could lead to dependency issues. See [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") and [BBS#89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

#### Installing specific packages

To install a single package or list of packages (including dependencies), issue the following command:

```
# pacman -S *package_name1* *package_name2* ...

```

To install a list of packages with regex (see [pacman tips#Operations and Bash syntax](/index.php/Pacman_tips#Operations_and_Bash_syntax "Pacman tips") and [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=7179)):

```
# pacman -S $(pacman -Ssq *package_regex*)

```

Sometimes there are multiple versions of a package in different repositories, e.g. *extra* and *testing*. To install the former version, the repository needs to be defined in front:

```
# pacman -S extra/*package_name*

```

#### Installing package groups

Some packages belong to a [group of packages](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages") that can all be installed simultaneously. For example, issuing the command:

```
# pacman -S gnome

```

will prompt you to select the packages from the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group that you wish to install.

Sometimes a package group will contain a large amount of packages, and there may be only a few that you do or do not want to install. Instead of having to enter all the numbers except the ones you do not want, it is sometimes more convenient to select or exclude packages or ranges of packages with the following syntax:

```
Enter a selection (default=all): 1-10 15

```

which will select packages 1 through 10 and 15 for installation, or:

```
Enter a selection (default=all): ^5-8 ^2

```

which will select all packages except 5 through 8 and 2 for installation.

To see what packages belong to the gnome group, run:

```
# pacman -Sg gnome

```

Also visit [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) to see what package groups are available.

**Note:** If a package in the list is already installed on the system, it will be reinstalled even if it is already up to date. This behavior can be overridden with the `--needed` option.

### Removing packages

To remove a single package, leaving all of its dependencies installed:

```
# pacman -R *package_name*

```

To remove a package and its dependencies which are not required by any other installed package:

```
# pacman -Rs *package_name*

```

To remove a package, its dependencies and all the packages that depend on the target package:

**Warning:** This operation is recursive, and must be used with care since it can remove many potentially needed packages.

```
# pacman -Rsc *package_name*

```

To remove a package, which is required by another package, without removing the dependent package:

```
# pacman -Rdd *package_name*

```

*pacman* saves important configuration files when removing certain applications and names them with the extension: *.pacsave*. To prevent the creation of these backup files use the `-n` option:

```
# pacman -Rn *package_name*

```

**Note:** *pacman* will not remove configurations that the application itself creates (for example "dotfiles" in the home folder).

### Upgrading packages

**Warning:** Arch only supports full system upgrades. See [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") and [#Installing packages](#Installing_packages) for details.

It is recommended that users [upgrade their system regularly](/index.php/System_maintenance#Upgrading_the_system "System maintenance"). When requesting support from the community, it will usually be assumed that the system is up to date.

Before upgrading, users are expected to visit the [Arch Linux home page](https://www.archlinux.org/) to check the latest news, or alternatively subscribe to the [RSS feed](https://www.archlinux.org/feeds/news/), [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), or follow [@archlinux](https://twitter.com/archlinux) on Twitter: when updates require out-of-the-ordinary user intervention (more than what can be handled simply by following the instructions given by *pacman*), an appropriate news post will be made. Users must equally be aware that upgrading packages can raise **unexpected** problems that could need immediate intervention, therefore it is discouraged to upgrade a stable system shortly before it is required for carrying out an important task: it is wise to wait instead to have enough time in order to be able to deal with possible post-upgrade issues.

*pacman* can update all packages on the system with just one command. This could take quite a while depending on how up-to-date the system is. This command can synchronize the repository databases *and* update the system's packages (excluding "local" packages that are not in the configured repositories):

```
# pacman -Syu

```

*pacman* is a powerful package management tool, but it does not attempt to handle all corner cases. Users must be vigilant and take responsibility for maintaining their own system. **When performing a system update, it is essential that users read all information output by *pacman* and use common sense.** If a user-modified configuration file needs to be upgraded for a new version of a package, a *.pacnew* file will be created to avoid overwriting settings modified by the user. *pacman* will prompt the user to merge them. These files require manual intervention from the user and it is good practice to handle them right after every package upgrade or removal. See [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") for more information.

**Tip:**

*   Remember that *pacman'*s output is logged in `/var/log/pacman.log`.
*   You can use a log viewer such as [wat-git](https://aur.archlinux.org/packages/wat-git/) to search the pacman logs.

If one encounters problems that cannot be solved by these instructions, make sure to search the forum. It is likely that others have encountered the same problem and have posted instructions for solving it.

### Querying package databases

*pacman* queries the local package database with the `-Q` flag; see:

```
$ pacman -Q --help

```

and queries the sync databases with the `-S` flag; see:

```
$ pacman -S --help

```

*pacman* can search for packages in the database, searching both in packages' names and descriptions:

```
$ pacman -Ss *string1* *string2* ...

```

To search for already installed packages:

```
$ pacman -Qs *string1* *string2* ...

```

To display extensive information about a given package:

```
$ pacman -Si *package_name*

```

For locally installed packages:

```
$ pacman -Qi *package_name*

```

Passing two `-i` flags will also display the list of backup files and their modification states:

```
$ pacman -Qii *package_name*

```

To retrieve a list of the files installed by a package:

```
$ pacman -Ql *package_name*

```

For packages not installed, use [pkgfile](/index.php/Pkgfile "Pkgfile").

To verify the presence of the files installed by a package:

```
$ pacman -Qk *package_name*

```

Passing the `k` flag twice will perform a more thorough check.

One can also query the database to know which package a file in the file system belongs to:

```
$ pacman -Qo */path/to/file_name*

```

To list all packages no longer required as dependencies (orphans):

```
$ pacman -Qdt

```

To list all packages explicitly installed and not required as dependencies:

```
$ pacman -Qet

```

To list a dependency tree of a package:

```
$ pactree *package_name*

```

To list all the packages recursively depending on an *installed* package, use *whoneeds* from [pkgtools](https://aur.archlinux.org/packages/pkgtools/):

```
$ whoneeds *package_name*

```

or the reverse flag to *pactree*:

```
$ pactree -r *package_name*

```

See [pacman tips](/index.php/Pacman_tips "Pacman tips") for more examples.

#### Database structure

The pacman databases are normally located at `/var/lib/pacman/sync`. For each repository specified in `/etc/pacman.conf` there will be a corresponding database file located there. Database files are tar-gzipped archives containing one directory for each package, for example for the [which](https://www.archlinux.org/packages/?name=which) package:

```
% tree which-2.20-6 
which-2.20-6
|-- depends
`-- desc

```

The `depends` file lists the packages this package depends on, while `desc` has a description of the package such as the file size and the MD5 hash.

### Cleaning the package cache

*pacman* stores its downloaded packages in `/var/cache/pacman/pkg/` and does not remove the old or uninstalled versions automatically, therefore it is necessary to deliberately clean up that folder periodically to prevent such folder to grow indefinitely in size.

The built-in option to remove all the cached packages that are not currently installed is:

```
# pacman -Sc

```

**Warning:**

*   Only do this when certain that previous package versions are not required, for example for a later [downgrade](/index.php/Downgrade "Downgrade"). `pacman -Sc` only leaves the versions of packages which are *currently installed* available, older versions would have to be retrieved through other means, such as the [Archive](/index.php/Archive "Archive").
*   It is possible to empty the cache folder fully with `pacman -Scc`. In addition to the above, this also prevents from reinstalling a package directly *from* the cache folder in case of need, thus requiring a new download. It should be avoided unless there is an immediate need for disk space.

Because of the above limitations, consider an alternative for more control over which packages, and how many, are deleted from the cache:

The *paccache* script, provided by the [pacman](https://www.archlinux.org/packages/?name=pacman) package itself, deletes all cached versions of each package, except for the most recent 3, by default:

```
# paccache -r

```

Used this way, it will *not* check whether a package is still installed or not, and uninstalled packages will remain in the cache. To remove all cached versions of uninstalled packages, re-run *paccache* with:

```
# paccache -ruk0

```

See `paccache -h` for more options.

[pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/) and [pacleaner](https://aur.archlinux.org/packages/pacleaner/) are two further alternatives.

### Additional commands

Download a package without installing it:

```
# pacman -Sw *package_name*

```

Install a 'local' package that is not from a remote repository (e.g. the package is from the [AUR](/index.php/AUR "AUR")):

```
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

```

To keep a copy of the local package in *pacman'*s cache, use:

```
# pacman -U file:///path/to/package/package_name-version.pkg.tar.xz

```

Install a 'remote' package (not from a repository stated in *pacman'*s configuration files):

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

To inhibit the `-S`, `-U` and `-R` actions, `-p` can be used.

*pacman* always lists packages to be installed or removed and asks for permission before it takes action.

## Configuration

*pacman'*s settings are located in `/etc/pacman.conf`. This is the place where the user configures the program to work in the desired manner. In-depth information about the configuration file can be found in [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### General options

General options are in the `[options]` section. Read the [man page](/index.php/Man_page "Man page") or look in the default `pacman.conf` for information on what can be done here.

#### Color output

Pacman has a color option. Uncomment the "Color" line in `/etc/pacman.conf`.

#### Comparing versions before updating

To see old and new versions of available packages, uncomment the "VerbosePkgLists" line in `/etc/pacman.conf`. The output of `pacman -Syu` will be like this:

```
Package (6)             Old Version  New Version  Net Change  Download Size

extra/libmariadbclient  10.1.9-4     10.1.10-1      0.03 MiB       4.35 MiB
extra/libpng            1.6.19-1     1.6.20-1       0.00 MiB       0.23 MiB
extra/mariadb           10.1.9-4     10.1.10-1      0.26 MiB      13.80 MiB

```

#### Skip package from being upgraded

To have a specific package skipped when [upgrading](#Upgrading_packages) the system, specify it as such:

```
IgnorePkg=linux

```

For multiple packages use a space-separated list, or use additional `IgnorePkg` lines. Also, glob patterns can be used. If you want to skip packages just once, you can also use the `--ignore` option on the command-line - this time with a comma-separated list.

It will still be possible to upgrade the ignored packages using `pacman -S`: in this case *pacman* will remind you that the packages have been included in an `IgnorePkg` statement.

#### Skip package group from being upgraded

As with packages, skipping a whole package group is also possible:

```
IgnoreGroup=gnome

```

#### Skip files from being installed to system

To always skip installation of specific directories list them under `NoExtract`. For example, to avoid installation of [systemd](/index.php/Systemd "Systemd") units use this:

```
NoExtract=usr/lib/systemd/system/*

```

Or as a preemptive alternative to [localepurge](https://aur.archlinux.org/packages/localepurge/), to avoid installing non-English localizations:

```
NoExtract = usr/share/help/* !usr/share/help/en*
NoExtract = usr/share/locale/* !usr/share/locale/en* !usr/share/locale/locale.alias
NoExtract = usr/share/man/* !usr/share/man/man*
NoExtract = usr/share/vim/vim74/lang/*

```

Later rules override previous ones, and you can negate a rule by prepending `!` — this allows you to keep the locales you need.

**Tip:** Since pacman 5, while updating a package for which locales have been cleared by *localepurge* or *bleachbit*, *pacman* issues warning messages about the missing locales. Commenting the `CheckSpace` option in `pacman.conf` suppresses such warnings, but consider that the space-checking functionality will be disabled for all packages.

#### Maintain several configuration files

If you have several configuration files (e.g. main configuration and configuration with [testing](/index.php/Testing "Testing") repository enabled) and would have to share options between configurations you may use `Include` option declared in the configuration files, e.g.:

```
Include = /path/to/common/settings

```

where `/path/to/common/settings` file contains the same options for both configurations.

### Repositories

This section defines which [repositories](/index.php/Official_repositories "Official repositories") to use, as referred to in `/etc/pacman.conf`. They can be stated here directly or included from another file (such as `/etc/pacman.d/mirrorlist`), thus making it necessary to maintain only one list. See [Mirrors](/index.php/Mirrors "Mirrors") article for mirror configuration.

The order of repositories in the configuration files matters; repositories listed first will take precedence over those listed later in the file when packages in two repositories have identical names, regardless of version number.

### Package security

*pacman* 4 supports package signatures, which add an extra layer of security to the packages. The default configuration, `SigLevel = Required DatabaseOptional`, enables signature verification for all the packages on a global level: this can be overridden by per-repository `SigLevel` lines as shown above. For more details on package signing and signature verification, take a look at [pacman-key](/index.php/Pacman-key "Pacman-key").

### Hooks

*pacman* can run pre- and post-transaction hooks from the `/usr/share/libalpm/hooks/` directory; more directories can be specified with the `HookDir` option in `pacman.conf`.

For more information on the alpm hooks, see the alpm-hooks(5) man page.

## Troubleshooting

### "Failed to commit transaction (conflicting files)" error

If you see the following error: [[2]](https://bbs.archlinux.org/viewtopic.php?id=56373)

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
*package*: */path/to/file* exists in filesystem
Errors occurred, no packages were upgraded.

```

Why this is happening: *pacman* has detected a file conflict, and by design, will not overwrite files for you. This is a design feature, not a flaw.

The problem is usually trivial to solve. A safe way is to first check if another package owns the file (`pacman -Qo */path/to/file*`). If the file is owned by another package, [file a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). If the file is not owned by another package, rename the file which 'exists in filesystem' and re-issue the update command. If all goes well, the file may then be removed.

If you had installed a program manually without using *pacman* or a frontend, for example through `make install`, you have to remove it and all its files and reinstall properly using *pacman*. See also [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips").

Every installed package provides a `/var/lib/pacman/local/*$package-$version*/files` file that contains metadata about this package. If this file gets corrupted, is empty or goes missing, it results in `file exists in filesystem` errors when trying to update the package. Such an error usually concerns only one package. Instead of manually renaming and later removing all the files that belong to the package in question, you may exceptionally run `pacman -S --force $package` to force *pacman* to overwrite these files.

**Warning:** Take care when using the `--force` switch (for example `pacman -Syu --force`) as it can cause major problems if used improperly. It is highly recommended to only use this option when the Arch news instructs the user to do so.

### "Failed to commit transaction (invalid or corrupted package)" error

Look for *.part* files (partially downloaded packages) in `/var/cache/pacman/pkg` and remove them (often caused by usage of a custom `XferCommand` in `pacman.conf`).

```
# find /var/cache/pacman/pkg/ -iname "*.part" -exec rm {} \;

```

### "Failed to init transaction (unable to lock database)" error

When *pacman* is about to alter the package database, for example installing a package, it creates a lock file at `/var/lib/pacman/db.lck`. This prevents another instance of *pacman* from trying to alter the package database at the same time.

If *pacman* is interrupted while changing the database, this stale lock file can remain. If you are certain that no instances of *pacman* are running then delete the lock file:

```
# rm /var/lib/pacman/db.lck

```

### Packages cannot be retrieved on installation

This error manifests as `Not found in sync db`, `Target not found` or `Failed retrieving file`.

Firstly, ensure the package actually exists (and watch out for typos!). If certain the package exists, your package list may be out-of-date or your repositories may be incorrectly configured. Try running `pacman -Syyu` to force a refresh of all package lists and upgrade.

It could also be that the repository containing the package is not enabled on your system, e.g. the package could be in the *multilib* repository, but *multilib* is not enabled in your *pacman.conf*.

See also [FAQ#Why is there only a single version of each shared library in the official repositories?](/index.php/FAQ#Why_is_there_only_a_single_version_of_each_shared_library_in_the_official_repositories.3F "FAQ").

### The same package is upgraded repeatedly

**Note:** *pacman* version 3.4 should display an error in case of duplicate entries, which should make this note obsolete.

This is due to duplicate entries in `/var/lib/pacman/local/`, such as two `linux` instances. `pacman -Qi` outputs the correct version, but `pacman -Qu` recognizes the old version and therefore will attempt to upgrade.

The solution is to delete the offending entry in `/var/lib/pacman/local/`.

### Search for a package that contains a specific file

Install [pkgfile](/index.php/Pkgfile "Pkgfile") which uses a separate database with all files and their associated packages.

### pacman is broken beyond repair

In the case that *pacman* is broken beyond repair, manually download the necessary packages ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), and [pacman](https://www.archlinux.org/packages/?name=pacman)) and extract them to root. The *pacman* binary will be restored along with its default configuration file. Afterwards, reinstall these packages with *pacman* to maintain package database integrity. Additional information and an example (outdated) script that automates the process is available in [this](https://bbs.archlinux.org/viewtopic.php?id=95007) forum post.

Alternatively, you can also use an Arch live media and follow [#pacman crashes during an upgrade](#pacman_crashes_during_an_upgrade) to re-install pacman.

### pacman crashes during an upgrade

In the case that *pacman* crashes with a "database write" error while removing packages, and reinstalling or upgrading packages fails thereafter, do the following:

1.  Boot using the Arch installation media. Preferably use a recent media so that the *pacman* version matches/is newer than the system.
2.  Mount the system's root filesystem, e.g. `mount /dev/sdaX /mnt` as root, and check the mount has sufficient space with `df -h`
3.  If the system uses default database and directory locations, you can now update the system's pacman database and upgrade it via `pacman --root=/mnt --cachedir=/mnt/var/cache/pacman/pkg -Syyu` as root.
4.  After the upgrade, one way to double-check for not upgraded but still broken packages: `find /mnt/usr/lib -size 0`
5.  Followed by a re-install of any still broken package via `pacman --root /mnt --cachedir=/mnt/var/cache/pacman/pkg -S *package*`.

### pacman crashes the official installation media

The official installation media (ISO) before version 10.2015 are not setup to be updated itself at runtime. Running `pacman -Syu` from a booted install media console may crash unexpectedly any time, as soon as memory is depleted. This happens because the install media image build reports an arbitrary capacity (of 32GB) to pacman, regardless of available free memory.[[3]](https://bugs.archlinux.org/task/45618#comment137346) At the same time the ISO reserves only a low static memory allotment for operations (`/run/archiso/cowspace` of `256MB` RAM) of the live system, in order to allow installation on machines with low resources. If the machine has more RAM available, you can override the allotment by setting the `cow_spacesize=` kernel option for the ISO manually, e.g. `cow_spacesize=2GB`.

If you use the install media to update an installed system, you simply have to use the `--root=` option along with a `--cachedir=` path to point pacman to available real storage. For example, see [#pacman crashes during an upgrade](#pacman_crashes_during_an_upgrade).

If you *require* an install media with persistent dataspace, the [Archiso](/index.php/Archiso "Archiso") build script can be used to create one along with its [boot options](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams).

### "Unable to find root device" error after rebooting

Most likely your initramfs got broken during a kernel update (improper use of *pacman'*s `--force` option can be a cause). You have two options; first, try the *Fallback* entry:

**Tip:** In case you removed this entry for whatever reason, you can always press the `Tab` key when the bootloader menu shows up (for Syslinux) or `e` (for GRUB or gummiboot), rename it `initramfs-linux-fallback.img` and press `Enter` or `b` (depending on your bootloader) to boot with the new parameters.

Once the system starts, run this command (for the stock [linux](https://www.archlinux.org/packages/?name=linux) kernel) either from the console or from a terminal to rebuild the initramfs image:

```
# mkinitcpio -p linux

```

If that does not work, from a current Arch release (CD/DVD or USB stick), run:

**Note:** If you do not have a current release or if you only have some other "live" Linux distribution laying around, you can [chroot](/index.php/Chroot "Chroot") using the old fashioned way. Obviously, there will be more typing than simply running the `arch-chroot` script.

```
# mount /dev/sdxY /mnt         # Your root partition.
# mount /dev/sdxZ /mnt/boot    # If you use a separate /boot partition.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux

```

**Note:** If *pacman* fails with `Could not resolve host`, please [check your internet connection](/index.php/Network_configuration#Check_the_connection "Network configuration").

Reinstalling the kernel (the [linux](https://www.archlinux.org/packages/?name=linux) package) will automatically re-generate the initramfs image with `mkinitcpio -p linux`. There is no need to do this separately.

Afterwards, it is recommended that you run `exit`, `umount /mnt/{boot,}` and `reboot`.

**Note:** If you cannot enter the arch-chroot or chroot environment but need to re-install packages you can use the command `pacman -r /mnt -Syu foo bar` to use *pacman* on your root partition.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Follow [pacman-key#Resetting all the keys](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key"). Or you can try to either:

*   update the known keys, i.e. `pacman-key --refresh-keys`;
*   or manually upgrade [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) package first, i.e. `pacman -S archlinux-keyring`.

### Request on importing PGP keys

If [installing](/index.php/Installation_guide "Installation guide") Arch with an outdated ISO, you are likely prompted to import PGP keys. Agree to download the key to proceed. If you are unable to add the PGP key successfully, update the keyring or upgrade [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) (see [above](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)).

### Signature from "User <email@archlinux.org>" is invalid, installation failed

When the system time is faulty, signing keys are considered expired (or invalid) and signature checks on packages will fail with the following error:

```
error: *package*: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```

Make sure to correct the [time](/index.php/Time "Time"), for example with `ntpd -qg` run as root, and run `hwclock -w` as root before subsequent installations or upgrades.

### "Warning: current locale is invalid; using default "C" locale" error

As the error message says, your locale is not correctly configured. See [Locale](/index.php/Locale "Locale").

### pacman does not honor proxy settings

Make sure that the relevant environment variables (`$http_proxy`, `$ftp_proxy` etc.) are set up. If you use *pacman* with [sudo](/index.php/Sudo "Sudo"), you need to configure sudo to [pass these environment variables to pacman](/index.php/Sudo#Environment_variables "Sudo").

### How do I reinstall all packages, retaining information on whether something was explicitly installed or as a dependency?

To reinstall all the native packages: `pacman -Qnq | pacman -S -` (the `-S` option preserves the installation reason by default).

You will then need to reinstall all the foreign packages, which can be listed with `pacman -Qmq`.

### "Cannot open shared object file" error

It looks like previous *pacman* transaction removed or corrupted shared libraries needed for pacman itself.

To recover from this situation you need to unpack required libraries to your filesystem manually. First find what package contains the missed library and then locate it in the *pacman* cache (`/var/cache/pacman/pkg/`). Unpack required shared library to the filesystem. This will allow to run *pacman*.

Now you need to [reinstall](#Installing_specific_packages) the broken package. Note that you need to use `--force` flag as you just unpacked system files and *pacman* does not know about it. *pacman* will correctly replace our shared library file with one from package.

That's it. Update the rest of the system.

### Freeze of package downloads

Some issues have been reported regarding network problems that prevent *pacman* from updating/synchronizing repositories. [[4]](https://bbs.archlinux.org/viewtopic.php?id=68944) [[5]](https://bbs.archlinux.org/viewtopic.php?id=65728) When installing Arch Linux natively, these issues have been resolved by replacing the default *pacman* file downloader with an alternative (see [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance") for more details). When installing Arch Linux as a guest OS in [VirtualBox](/index.php/VirtualBox "VirtualBox"), this issue has also been addressed by using *Host interface* instead of *NAT* in the machine properties.

### Failed retrieving file 'core.db' from mirror

If you receive this error message with correct [mirrors](/index.php/Mirrors "Mirrors"), try setting a different [name server](/index.php/Resolv.conf "Resolv.conf").

## See also

*   [Pacman's homepage](https://www.archlinux.org/pacman/)
*   [libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html)
*   [pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html)
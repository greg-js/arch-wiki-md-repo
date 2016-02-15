This guide will show you how to downgrade a package to a previous version. Downgrading a package isn't normally recommended and is often only necessary when a bug is introduced in the current package.

Before downgrading, consider why you are doing so. If it is because of a bug, please help both Arch and upstream developers by spending a few minutes reporting the bug on the Arch bug tracker or on the parent project itself. Because Arch is a rolling release distribution you will likely be continously working with new packages and will experience a bug from time to time.

Both we and the upstream developers would appreciate the effort. That extra bit of information could save us hours of testing and debugging and also helps us release more stable software.

## Contents

*   [1 Reason](#Reason)
*   [2 The Details](#The_Details)
*   [3 How to downgrade a package](#How_to_downgrade_a_package)
*   [4 Finding Your Older Version](#Finding_Your_Older_Version)
    *   [4.1 Out-Of-Sync Mirrors](#Out-Of-Sync_Mirrors)
    *   [4.2 ARM](#ARM)
    *   [4.3 Re-Compile The Package](#Re-Compile_The_Package)
*   [5 Other Information](#Other_Information)
*   [6 What about dependencies?](#What_about_dependencies.3F)
*   [7 Stopping Pacman from updating certain packages](#Stopping_Pacman_from_updating_certain_packages)
*   [8 Reverting to a Savepoint](#Reverting_to_a_Savepoint)
*   [9 See Also](#See_Also)

## Reason

The process of downgrading is that of uninstalling the current package and installing a previous version. The previous version can be an immediate version (the package version directly before it) or to a number of versions prior.

The reasons for downgrading include (among others): that the current version has a bug, does not yet contain the desired functionality, or was done for experimental reasons. In any of these cases, the user has chosen that it would be less problematic to revert to a previous version than to wait for a new release.

Downgrading a package may mean that other packages may have to be downgraded with it. For those that have installed a good amount of experimental or testing packages, and edited a good deal of configurations, it may be preferable to re-install the system rather than trying to downgrade.

## The Details

However, the user must keep in mind the following points. First, there is going to be the need to consider the dependencies of each program. The required libraries and such often change with each version, and the functionality of associated files may be completely different from previous ones. The solution will require changing these to earlier versions as well.

Second, one must consider if the necessary files have been removed from the system and are even going to be available from any source. Arch Linux's rolling release system of repositories are automatically upgraded without saving any older versions. See more about this problem below.

Third, we must be careful with changes to configuration files and scripts. At this point in time, we will rely upon pacman to handle this for us, as long as we do not bypass any safeguards it contains.

Please keep in mind that this issue brings us to the cutting edge of pacman package management development. The Arch Rollback Machine concept is being developed and awaiting useful incorporation into pacman. Once that occurs, this will become automated. Until then, please follow the instructions following this.

## How to downgrade a package

*   Q: I just ran **pacman -Syu** and package XYZ was upgraded to version N from version M. This package is causing problems on my computer, how can I downgrade from version N to the older version M?
*   A: You may be able to downgrade the package trivially by visiting **/var/cache/pacman/pkg** on your system and seeing if the older version of the package is stored there. (If you have not run **pacman -Scc** recently, it should be there). If the package is there, you can install that version using **pacman -U /var/cache/pacman/pkg/pkgname-olderpkgver.pkg.tar.gz**.

This process will remove the current package, it will carefully calculate all of the dependency changes, and it will install the older version you have chosen with the proper dependencies down the line.

**Note:** If you change a fundamental part of the OS, you may end up with the need to take out literally dozens of packages and replace them with their older version. Or they may just be gone and you will have to put them back in a manual, piece-meal fashion, while being careful that a particular upgrade does not want to re-install the undesirable package version you didn't want in the first place.

There is also a package in the AUR called [downgrade](https://aur.archlinux.org/packages.php?ID=31937). This is a simple bash script which will look in your cache for older versions of packages. It will also search the [A.R.M.](/index.php/Downgrade#ARM "Downgrade") if there is no package in your cache. You can then select a package to install. It basically just automates the processes outlined here. Check **downgrade --help** for usage information.

One more powerful tool names [downgrader](https://aur.archlinux.org/packages.php?ID=50246), it works with pacman log`s also, can downgrade packages from ARM, local cache, and work with list of packages (if your system unstable after upgrade of some packages, and you unsure about package name)

## Finding Your Older Version

There are three ways to do this.

#### Out-Of-Sync Mirrors

If you can not find older versions on your system, check if one of the mirrors is out of sync, and get it from there. Click here to see the [status of mirrors](http://users.archlinux.de/~gerbra/mirrorcheck.html).

You can also check of this mirror, which stores old packages:

*   [http://schlunix.org/?page_id=11](http://schlunix.org/?page_id=11)

#### ARM

The [Arch Rollback Machine](http://arm.konnichi.com/) (ARM) contains archived snapshots of all the repos going back to 1 November 2009\. The site is in a state of flux as of this date (21 November 2009), and now has lost the items back thru 1 October 2008, as previously reported.

If you are interested in ARM, it would be best to view the introductory forum announcement and discussion, so as to stay abreast of the current progress of the project. The introductory forum thread is [here](https://bbs.archlinux.org/viewtopic.php?id=53665).

It is said that the goal was to construct the urls in such a way as to facilitate easy wget+pacman scripting to "roll back" your system to a particular date. The automation process is not yet explained. To just manually search for a particular package, one can use the search page which has been provided at [ARM Search](http://arm.konnichi.com/search/).

#### Re-Compile The Package

In worst-case scenario, if the package is not located anywhere else, you will need to compile the older version yourself. To do this you will need a PKGBUILD for the file; you could edit the existing PKGBUILD provided by ABS to use older sources, or you can visit [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) and search for the package you wish to downgrade. Once you find it, click "View SVN entries" and select "View Log". Locate the version you need and click on the path. Then just download the files located in that directory and build it with makepkg.

## Other Information

The basic concept of user control in pacman package management is to edit the pacman.conf file by logging in as root at the command prompt and using "nano /etc/pacman.conf" (without the quotes) to edit that file. (While this can often be done from within your GUI frontend of choice, such as Shaman, sometimes it is more accurate to do it right from the CLI. It is suggested that you clean up any accumulated junk while in the file.)

One is simply going to be changing the locations of repositories in which pacman searches for programs. Remarking out any existing repos by the use of the pound sign at the begining of the line will leave the current ones without making them accessible to pacman and the package management system.

For instance, to add a repository from the ARM, one simply remarks-out the old line and adds the appropriate directory location in the format:

```
[core]
#Server=[http://mirrors.gigenet.com/archlinux/core/os/i686](http://mirrors.gigenet.com/archlinux/core/os/i686)
Server=[http://arm.konnichi.com/2009/11/01/core/os/i686](http://arm.konnichi.com/2009/11/01/core/os/i686)

```

In this example, the date section is taking whatever packages are available as of the date of November 1st, 2009\. Please note that all repositories are snapshots of the official repositories. You need only change the mirror in `/etc/pacman.d/mirrorlist`, placing an ARM mirror at the top. e.g [http://arm.konnichi.com/2009/11/01/$repo/os/i686](http://arm.konnichi.com/2009/11/01/$repo/os/i686) to sync all official repositories listed in `/etc/pacman.conf` to the chosen ARM mirror then update with:

```
pacman -Syy  # refresh the sync databases
pacman -Suu  # downgrade all packages with a lower version in the repos

```

This alone does not guarantee a seemless rollback as there are sometimes package conflicts with regards to verion numbers, etc. If you know the repository it may be easier to visit the global mirror, e.g [http://arm.konnichi.com/core/os/i686](http://arm.konnichi.com/core/os/i686), note the omission of the date.

## What about dependencies?

*   Q: I can not downgrade a package, because of dependencies.
*   A: You can ignore dependencies when upgrading or removing with 'd'. e.g. **pacman -Ud pkgpkgname-olderpkgver.pkg.tar.gz** but this might break your system further.

## Stopping Pacman from updating certain packages

*   Q: How do I stop Pacman from upgrading downgraded packages?
*   A: With the "IgnorePkg" variable in `/etc/pacman.conf`.

`"IgnorePkg = package1 package2 ..."` in your `pacman.conf` instructs Pacman to ignore any upgrades for selected packages when performing a --sysupgrade.

## Reverting to a Savepoint

*   Q: I want to go back to how my system was yesterday.
*   A: It is easy provided you enabled periodic snapshots.

You can rely on a logical volume manager ([LVM](/index.php/LVM "LVM")) for creating and maintaining snapshots. These snapshots should not be confused with CVS snapshots. LVM snapshots are kernel-level filesystem snapshots that, unlike a full backup, use a COW (copy-on-write) scheme which means that it occupies very little disk space so long as no files were modified, and if files were modified, the snapshot occupies only a little more than the disk space needed to store the pre-modified files. This usually means that you can snapshot a 35GB system with only 2GB free space, considering that pacman -Sy will likely modify far less than 2GB of data. If the state of your system after the upgrade is undesirable, you can quickly rollback to previous snapshot images of your system.

## See Also

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System") for more information.
*   [LVM](/index.php/LVM "LVM") for how to enable snapshots and how to revert to their state.
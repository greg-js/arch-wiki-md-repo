# Downgrading packages

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [pacman](/index.php/Pacman "Pacman")
*   [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** soname bumps, cf. [Frequently_asked_questions#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F](/index.php/Frequently_asked_questions#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F "Frequently asked questions") (Discuss in [Talk:Downgrading packages#](https://wiki.archlinux.org/index.php/Talk:Downgrading_packages))

Before downgrading a single or multiple packages, consider why you wish to do so. If it is due to a bug, search the [Bugtracker](https://bugs.archlinux.org/) for existing tasks. If there is none, add a new task; it is better to correct bugs, or at least warn other users of possible issues.

**Warning:**

*   Downgrading one package may require that its dependencies be downgraded as well. When the number of packages to downgrade is large, consider using a snapshot. See [Arch Linux Archive#How to restore all my packages at a specific date](/index.php/Arch_Linux_Archive#How_to_restore_all_my_packages_at_a_specific_date "Arch Linux Archive").
*   Be careful with changes to configuration files and scripts. For now pacman will handle this for us, as long as we do not bypass its safeguards.

## Contents

*   [1 Return to an earlier package version](#Return_to_an_earlier_package_version)
    *   [1.1 Using the pacman cache](#Using_the_pacman_cache)
    *   [1.2 Downgrading the kernel](#Downgrading_the_kernel)
    *   [1.3 Arch Linux Archive](#Arch_Linux_Archive)
    *   [1.4 Rebuild the package](#Rebuild_the_package)
    *   [1.5 Using the downgrade script](#Using_the_downgrade_script)
*   [2 Return from [testing]](#Return_from_.5Btesting.5D)

## Return to an earlier package version

### Using the pacman cache

If a package was installed at an earlier stage, and the [pacman cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman") was not cleaned, install an earlier version from `/var/cache/pacman/pkg/`.

This process will remove the current package and install the older version. Dependency changes will be handled, but [pacman](/index.php/Pacman "Pacman") will not handle version conflicts. If a library or other package needs to be downgraded with the packages, please be aware that you will have to downgrade this package yourself as well.

```
# cd /var/cache/pacman/pkg/
# pacman -U <file_name_of_the_package>

```

Once the package is reverted, temporarily add it to the [IgnorePkg section](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman") of `pacman.conf`, until the difficulty with the updated package is resolved.

### Downgrading the kernel

If you are unable to boot after a kernel update, then you can downgrade the kernel via a live CD. Use a fairly recent Arch Linux installation medium. Once it has booted, mount the partition where your system is installed to `/mnt`, and if you have `/boot` or `/var` on separate partitions, mount them there as well (e.g. `mount /dev/sdc3 /mnt/boot`). Then [chroot](/index.php/Chroot "Chroot") into the system:

```
# arch-chroot /mnt /bin/bash

```

Here you can go to `/var/cache/pacman/pkg` and downgrade the packages. At least downgrade [linux](https://www.archlinux.org/packages/?name=linux), [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) and any kernel modules. For example:

```
# pacman -U linux-3.5.6-1-x86_64.pkg.tar.xz linux-headers-3.5.6-1-x86_64.pkg.tar.xz virtualbox-host-modules-4.2.0-5-x86_64.pkg.tar.xz

```

Exit the chroot (with `exit`), reboot and you should be done.

### Arch Linux Archive

The [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") is a daily snapshot of the [official repositories](/index.php/Official_repositories "Official repositories").

The _ALA_ can be used to install a previous package version, or restore the system to an earlier date.

### Rebuild the package

If the package is unavailable, find the correct [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and rebuild it with [makepkg](/index.php/Makepkg "Makepkg").

For packages from the [official repositories](/index.php/Official_repositories "Official repositories"), retrieve the PKGBUILD with [ABS](/index.php/ABS "ABS") and change the software version. Alternatively, find the package on the [Packages](https://www.archlinux.org/packages) website, click "View Changes", and navigate to the desired version. The files are available through a `.tar.gz` snapshot, and via the _Tree_ view.

See also [Getting PKGBUILDS From SVN#Checkout an older revision of a package](/index.php/Getting_PKGBUILDS_From_SVN#Checkout_an_older_revision_of_a_package "Getting PKGBUILDS From SVN").

Old AUR packages can be obtained from [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/). See [Arch User Repository#Git repositories for AUR3 packages](/index.php/Arch_User_Repository#Git_repositories_for_AUR3_packages "Arch User Repository") for details.

### Using the downgrade script

The [downgrade](https://aur.archlinux.org/packages/downgrade/)<sup><small>AUR</small></sup> package is a Bash script to downgrade one (or multiple) packages, by using the pacman cache or the [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine"). See `man downgrade` for details.

Another tool is [downgrader](https://aur.archlinux.org/packages/downgrader/)<sup><small>AUR</small></sup>, which supports the pacman log, can downgrade packages from ARM and local cache, and handle package lists. This tool may be particularly useful to identify problematic packages.

## Return from [testing]

See [Official repositories#Disabling testing repositories](/index.php/Official_repositories#Disabling_testing_repositories "Official repositories").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Downgrading_packages&oldid=409718](https://wiki.archlinux.org/index.php?title=Downgrading_packages&oldid=409718)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")
This page documents two potential methods of migrating installed systems from i686 (32-bit) to x86_64 (64-bit) architectures. The methods avoid a *complete* reinstall (i.e. wiping the hard drive). One method uses a liveCD, the other modifies the system from within.

**Note:** Technically this process still involves "reinstalling" since every package on the system must be replaced. These methods simply attempt to preserve as much as they can from your existing system.

**Warning:** Unless explicitly stated, all these methods are **untested** and may irreparably damage your system. Continue at your own risk.

## Contents

*   [1 General preparation](#General_preparation)
    *   [1.1 Confirm 64-bit architecture](#Confirm_64-bit_architecture)
    *   [1.2 Disk space](#Disk_space)
    *   [1.3 Power supply](#Power_supply)
    *   [1.4 Fallback packages](#Fallback_packages)
*   [2 Method 1: using the Arch LiveCD](#Method_1:_using_the_Arch_LiveCD)
*   [3 Method 2: from a running system](#Method_2:_from_a_running_system)
    *   [3.1 Package preparation](#Package_preparation)
        *   [3.1.1 Cache old packages](#Cache_old_packages)
        *   [3.1.2 Install busybox](#Install_busybox)
        *   [3.1.3 Change Pacman architecture](#Change_Pacman_architecture)
        *   [3.1.4 Download new packages](#Download_new_packages)
    *   [3.2 Package installation](#Package_installation)
        *   [3.2.1 Install kernel (64-bit)](#Install_kernel_(64-bit))
        *   [3.2.2 Install lib32-glibc](#Install_lib32-glibc)
        *   [3.2.3 Reboot](#Reboot)
        *   [3.2.4 Switch to Console Terminal](#Switch_to_Console_Terminal)
        *   [3.2.5 Install Pacman](#Install_Pacman)
        *   [3.2.6 Install remaining packages](#Install_remaining_packages)
*   [4 Cleanup](#Cleanup)
    *   [4.1 Makepkg compiler flags](#Makepkg_compiler_flags)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Busybox](#Busybox)
    *   [5.2 Lib32-glibc](#Lib32-glibc)
    *   [5.3 Migrating from old system 2017 and before](#Migrating_from_old_system_2017_and_before)
    *   [5.4 KDE does not start after switching from 32-bit to 64-bit](#KDE_does_not_start_after_switching_from_32-bit_to_64-bit)
    *   [5.5 Mutt issues with cache enabled](#Mutt_issues_with_cache_enabled)
*   [6 See also](#See_also)

## General preparation

### Confirm 64-bit architecture

In order to run 64-bit software, you must have a 64-bit capable CPU. Most modern CPUs are capable of running 64-bit software. You may check your CPU with the following command:

```
grep --color -w lm /proc/cpuinfo

```

For CPUs that support x86_64, this will return the `lm` flag (“long mode”) highlighted. Beware that *lahf_lm* is a different flag and does not indicate 64-bit capability itself.

### Disk space

You should be prepared for `/var/cache/pacman/pkg` to grow approximately twice its current size during the migration. This is assumes only packages that are currently installed are in the cache, as if “pacman -Sc” (clean) was recently run. The disk space increase is due to duplication between the i686 and x86_64 versions of each package.

If you have not enough disk, please use [GParted](/index.php/GParted "GParted") to resize the relevant partition, or mount another partition to `/var/cache/pacman`.

Please do not remove packages of the old architecture from the cache until the system is fully operating in the new architecture. Removing the packages too early may leave you unable to fall back and revert changes.

### Power supply

The migration may take a substantial amount of time, and it would be inconvenient to interrupt the process. You should plan on at least an hour, depending on the number and size of your installed packages and internet connection speed (although you can download everything before starting the critical part). Please make sure you are connected to a stable power source, preferably with some sort of failover or battery backup.

### Fallback packages

If the migration fails halfway through, there are packages that can help sort out the situation, but they should be installed before the main packages are migrated. More details about using them under [#Troubleshooting](#Troubleshooting) below.

One package is [busybox](https://www.archlinux.org/packages/?name=busybox), which can be used to revert changes. It is statically linked and does not depend on any libraries. The 32-bit (i686) version should be installed.

Another package is [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc), from the [multilib](/index.php/Multilib "Multilib") x86_64 repository. It is probably only useful when migrating *away* from 32 bits; in any case you may safely skip this package. You can use the package to run 32 bit programs by explicitly calling `/lib/ld-linux.so.2`.

## Method 1: using the Arch LiveCD

1.  [Download](https://www.archlinux.org/download/) and burn the latest Arch Linux ISO.
2.  Boot the Arch LiveCD in x86_64 mode.
3.  Configure your network on the LiveCD.
4.  Mount your existing installation. For example: `mount /dev/sda1 /mnt`.
5.  Edit the LiveCD `/etc/pacman.conf` repositories to match the existing `/mnt/etc/pacman.conf` repositories.
6.  Use the following commands to update the local pacman database and clear the cache directory.

```
 # pacman --root /mnt -Syy
 # pacman --root /mnt -Scc

```

	6\. You might first re-install the [base](https://www.archlinux.org/groups/x86_64/base/) group alone, then install any package that triggered an install error, identified using `pacman --root /mnt -Qo <error file>`. Then repeat the [base](https://www.archlinux.org/groups/x86_64/base/) group install, until it installs cleanly without errors.

```
 # pacman --root /mnt -S base

```

	7\. Use the following command to get a list of all your installed packages and then reinstall them.

```
 # pacman --root /mnt -Qnq | pacman --root /mnt -S -

```

	8\. You could run the command twice, because many packages fail to run their post-install scripts first time. This is due to sed, grep, perl, etc. being of the wrong architecture. Or you can make note of any individual package-re-install that throws an error and then go back after the upgrade completes to re-install just those packages.

	Also, if you see an error about not enough disk space, you can filter the package list alphabetically and upgrade in stages, with for instance `...| grep '^[a-k]' |...`, then perhaps `'^l'` and `'^[m-z]'`. In this case you would also have to run `pacman --root /mnt -Scc` after each install stage to free disk space. Or since all packages are downloaded in the Live CD ramfs, you can also mount a partition or make a symlink pointing to `/var/cache/pacman/pkg` (e.g. `ln -s /mnt/var/cache/pacman/pkg /var/cache/pacman/pkg`).

	9\. Finally, run

```
 # arch-chroot /mnt 
 # mkinitcpio -p linux

```

	10\. Also, see if your boot loader needs to be migrated. For instance:

```
 # grub-install --recheck /dev/sda

```

	11\. After rebooting to your new 64-bit system, edit and then move `/etc/makepkg.conf.pacnew` to `/etc/makepkg.conf`, to migrate the CPU architecture. Then rebuild the "foreign" packages, which will include packages from the [AUR](/index.php/AUR "AUR").

	You might first want to remove certain orphaned foreign packages before trying to rebuild them. Run this command to find out what 32-bit binaries you still have and reinstall them:

```
 $ LC_ALL=C pacman -Qo `find /usr/bin -type f -exec bash -c 'file "{}" | grep 32-bit' \; | cut -d':' -f1` | cut -d' ' -f5 | sort | uniq | tee list

```

## Method 2: from a running system

Ensure that your system is fully updated and functioning before proceeding.

```
# pacman -Syu

```

### Package preparation

#### Cache old packages

**Note:** If you have any packages installed from the [AUR](/index.php/AUR "AUR") or third-party repositories without new architecture availability, pacman will let you know it cannot find a suitable replacement. Make a list of these packages so you may re-install them after the update process and then remove them using `pacman -Rsn package_name`.

If you do not have all your installed packages in your cache, download them (for the old architecture) for fallback purposes.

```
# pacman -Qqn | pacman -Sw -

```

or use [fakepkg](https://aur.archlinux.org/packages/fakepkg/) package to generate them.

#### Install busybox

If you are migrating from 32 bits to 64 bits, now is the time to install 32-bit [busybox](https://www.archlinux.org/packages/?name=busybox).

```
# pacman -S busybox

```

#### Change Pacman architecture

Edit the `/etc/pacman.conf` file and change *Architecture* from `auto` to `x86_64`.

Make sure the server lists in `/etc/pacman.conf` and `/etc/pacman.d/mirrorlist` use `$arch` instead of explicitly specifying `i686` or `x86_64`. Now force Pacman to synchronize with the new repositories:

```
# pacman -Syy                     # force sync new architecture repositories

```

#### Download new packages

Download the new architecture versions of all our currently installed packages:

```
# pacman -Sw $(pacman -Qqn|sed '/^lib32-/ d')  # download new package versions

```

If migrating to 32 bits, install the 32-bit [busybox](https://www.archlinux.org/packages/?name=busybox) fallback now that Pacman has been configured with the 32-bit architecture.

**Warning:** Do not install the *lib32-glibc* package now. After a *ldconfig*, when you install *linux*, the generated image will have libraries like *librt.so* in '`/usr/lib32`, where binaries during boot will not search, resulting in a boot failure.

### Package installation

#### Install kernel (64-bit)

Upgrading the kernel to 64 bits (x86_64) is safe and straightforward: 32 bit and 64 bit applications run equally well under a 64-bit kernel.

Install the [linux](https://www.archlinux.org/packages/?name=linux) package.

```
# pacman -S linux

```

#### Install lib32-glibc

Install the [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) fallback together with the 64-bit version of [glibc](https://www.archlinux.org/packages/?name=glibc). You will need to add the [multilib](/index.php/Multilib "Multilib") repository in `/etc/pacman.conf` if you have not done so already.

```
# pacman -S glibc lib32-glibc 

```

**Warning:** If you do not install the 64-bit version of glibc at the same time as lib32-glibc, the lib32-glibc install will not be able to function. However, pacman will not warn you about this, as the 32-bit glibc package also satisfies the dependency.

#### Reboot

Verify that you are running the x86_64 architecture:

 `$ uname -m` 
```
x86_64

```

#### Switch to Console Terminal

Switch to a text-mode virtual console (e.g. Ctrl+Alt+F1) for the rest of the process, if possible. If you receive an error trying to use the 1st console, use the 2nd one (Ctrl-Alt+F2) instead. Pseudo-terminals like SSH should work, but direct access is recommended as a precaution. There will be several packages removed and replaced during the update process that may cause X11 desktops to become unstable and leave your system in an unbootable state.

#### Install Pacman

**Warning:** Once you start updating pacman and its dependencies it must not be interrupted! Pacman and all of its dependencies must be installed at the same time in a single command line.

**Warning:** Immediately following this command only Busybox, Bash and Pacman will be executable until the other packages are migrated below. If you are using sudo, you should obtain root previlige prior to next command

Use pactree to install Pacman and all its dependencies:

```
# pactree -l pacman | pacman -S -

```

Errors may be printed but they will not cause a problem as long as Pacman works.

**Warning:** You must not reboot your system until the following commands have been completed. If you failed to do so, you should continue installing by [chrooting](/index.php/Chroot "Chroot") from another linux environment(e.g. from live install medium)

#### Install remaining packages

Install all of the previously downloaded replacements for the new architecture. (Go get a drink and make a sandwich; this could take a while.)

```
# pacman -Qqn | pacman -S -

```

If some packages did not install correctly, you should now be able to reinstall them successfully; if you are lazy, you can just re-run the last command to reinstall everything.

After this step the migration in either direction should be complete and it should be safe to reboot the computer.

However, if you have any AUR packages on your system, you must reinstall all of them. A list of those can be obtained by executing:

```
$ pacman -Qqm

```

## Cleanup

You are now free to remove **busybox** and *lib32-glibc*.

#### Makepkg compiler flags

During the upgrade the new version of `/etc/makepkg.conf` may be stored as `/etc/makepkg.conf.pacnew`. If so, you will have to replace the old version or modify it in order to compile anything with [makepkg](/index.php/Makepkg "Makepkg") in the future.

```
# mv /etc/makepkg.conf /etc/makepkg.conf.backup && mv /etc/makepkg.conf.pacnew /etc/makepkg.conf

```

It might also be a good idea to just get a list of "new" additions to `/etc`. You can get a list with the following command:

```
# find /etc/ -type f -name \*.pac\*

```

## Troubleshooting

During the upgrade, when glibc is replaced by the new architecture version, old architecture versions of many programs will not run. If problems occur, you can solve them with [busybox](https://www.archlinux.org/packages/?name=busybox) and [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc).

### Busybox

In Arch, Busybox is statically linked; it can run without any libraries. There are many commands available to you. For example, to extract an i686 version of Pacman from a cached package:

```
# busybox tar xf /var/cache/pacman/pkg/pacman-3.3.2-1-i686.pkg.tar.gz -C <some folder>

```

### Lib32-glibc

Example run 32 bit `/bin/ls`:

```
# /lib/ld-linux.so.2 /bin/ls

```

### Migrating from old system 2017 and before

You might face issue with updating old 32-bit system since in 2017 ArchLinux dropped support for i686\. To make that update safe you may want use [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"). I.e. fix repo snapshot, then update current system and then switch to 64-bit flavor of packages corresponding to **same version**.

Note that you may need to downgrade required trust level in `pacman.conf` (like `PackageTrustAll` to include marginal trust) since not all GPG keys which were used to sign package are still valid. Though you may want to ensure that you use HTTPS to at least ensure that packages comes from `archlinux.org` domain.

### KDE does not start after switching from 32-bit to 64-bit

KDE will crash when starting after switching from 32-bit to 64-bit. The cause are some leftover cached files from the 32 bit KDE packages in /var/tmp To fix this remove all kdecache folders in with

```
# rm -rf /var/tmp/kdecache-*

```

### Mutt issues with cache enabled

If, after completion, you find that mutt hangs on opening mail folders, try renaming the cache directory. If this works, the renamed one can be deleted as mutt will have recreated a new one.

## See also

*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")
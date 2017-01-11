[Linux-pf](http://pf.natalenko.name/) is a kernel package based on the stock -ARCH kernel, with the following patches applied:

*   [The latest Con Kolivas' -ck patchset, including BFS](http://ck-hack.blogspot.com/)
*   [BFQ](http://algo.ing.unimo.it/people/paolo/disk_sched/) (as default I/O scheduler)
*   [UKSM](http://kerneldedup.org/projects/uksm/)
*   [AUFS3](http://aufs.sourceforge.net/)

## Contents

*   [1 Installation](#Installation)
    *   [1.1 From the unofficial repository](#From_the_unofficial_repository)
    *   [1.2 From the AUR](#From_the_AUR)
    *   [1.3 Manual compilation](#Manual_compilation)
        *   [1.3.1 Install compiled package](#Install_compiled_package)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Forum thread for linux-pf](#Forum_thread_for_linux-pf)
*   [5 See also](#See_also)

## Installation

### From the unofficial repository

Precompiled packages are available from the [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") unofficial repository. See [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") for configuration details.

After an [upgrade](/index.php/Pacman#Upgrading_packages "Pacman"), running `pacman -Sl *repo_name*` will show the packages available in the given repository. Afterwards, just install the *linux-pf* and *linux-pf-headers* packages (for generic binaries - platform-specific binaries are also available in some repositories and will be listed in the output from the aforementioned pacman command). See the [#Configuration](#Configuration) section for additional configuration steps.

### From the AUR

Install [linux-pf](https://aur.archlinux.org/packages/linux-pf/) from the [AUR](/index.php/AUR "AUR"). A long-term support version of linux-pf is available with [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/).

### Manual compilation

There are a number of options a user is asked to choose from, should he/she select to compile from the PKGBUILD:

```
==> Hit <Y> to use your running kernel's config
    (needs IKCONFIG and IKCONFIG_PROC)
==> Hit <L> to run 'make localmodconfig'
==> Hit <N> (or just <ENTER>) to build an all-inclusive kernel like stock -ARCH
    (warning: it can take a looong time)

```

The <Y> option is for users who have already compiled and are running a custom kernel. The PKGBUILD reads the running kernel's configuration and uses it for the subsequent compilation. The <L> option tries some kind of autodetection of the user's hardware: it first tries to use the [modprobed-db](/index.php/Modprobed-db "Modprobed-db") module database, then falls back to the linux kernel's `make localmodconfig` functionality. The last option is self-explanatory.

```
==> Kernel configuration options before build:
    <M> make menuconfig (console menu)
    <N> make nconfig (newer alternative to menuconfig)
    <G> make gconfig (needs gtk)
    <X> make xconfig (needs qt)
    <O> make oldconfig
    <ENTER> to skip configuration and start compiling

```

Choose one of these to use your favourite user interface for configuring the kernel. Note that the last option might still prompt with unresolved/new configuration options, if you have selected <Y> or <L> in the previous step.

```
==> An non-generic CPU was selected for this kernel.
==> Hit <G>     :  to create a generic package named linux-pf
==> Hit <ENTER> :  to create a package named after the selected CPU
                   (e.g. linux-pf-core2 - recommended)
==> This option affects ONLY the package name. Whether or not the
==> kernel is optimized was determined at the previous config step.

```

If you have selected a specific CPU optimization for your kernel in the previous step, the default action is to append the CPU to the package name. This way, a subsequent package update from the repository will pull the optimized package and not the generic one. This also will help better compatibility with 3rd party precompiled modules (e.g. nvidia-pf), which might break things if loaded on optimized linux-pf kernels.

#### Install compiled package

After the compilation finishes, an additional *linux-pf-headers[-cpu]* package will be created. Do not forget to install it too, if you plan on using additional modules like [NVIDIA](/index.php/NVIDIA "NVIDIA") or [VirtualBox](/index.php/VirtualBox "VirtualBox").

```
# pacman -U linux-pf-core2-3.3.2-1-$CPUTYPE.pkg.tar.xz linux-pf-headers-core2-3.3.2-1-$CPUTYPE.pkg.tar.xz

```

During the kernel installation, [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") will be called by the install script to recreate the initramfs.

**Note:** If you make any changes to `/etc/mkinitcpio.conf` after the installation, you must run `mkinitcpio -p linux-pf` to have the initial ramdisk recreated.

## Configuration

Then, you need to add a boot entry in [boot loader configuration file](/index.php/Boot_Loader#Configuration_files "Boot Loader") which points to linux-pf (the following example is from one of the maintainer's boxes):

```
title  Linux-pf 3.2
root   (hd0,4)
kernel (hd0,0)/vmlinuz-linux-pf root=/dev/disk/by-label/ROOT ro vga=0x318 lapic resume=/dev/disk/by-label/SWAP video=vesafb:ywrap,mtrr:3 fastboot quiet
initrd (hd0,0)/initramfs-linux-pf.img

```

## Tips and tricks

*   If you notice disk-related performance problems or occasional hiccups, it might be an I/O scheduler issue. Try a different one than the linux-pf default (BFQ) by echoing to `/sys/block/sda/queue/scheduler` *cfq*, *noop* or *deadline*: `# echo noop >`. Note, the aforementioned command only sets the I/O scheduler for the 1st hard drive and additional *echoes* will be needed if you have more. If the situation improves, then append "*elevator*=***cfq***" (or ***noop*** or ***deadline***) to the linux-pf command line in `/boot/grub/menu.lst`, to make the change permanent.
*   For people who build their own tailored kernels and compilation aborts with with an error about "missing include/config/dvb/*.h files", setting *[*] Digital TV support* at *Device Drivers / <M> Multimedia support* and leaving everything else out, creates just the necessary dvb.h, which allows the compilation to continue.

## Forum thread for linux-pf

There is a [discussion thread](https://bbs.archlinux.org/viewtopic.php?id=103462) at the BBS for reporting errors, impressions, ideas and requests.

## See also

*   [linux-pf mercurial repository](https://bitbucket.org/nous/linux-pf/)
*   [Patchset homepage](http://pf.natalenko.name/)
*   [Patchset community forum](http://pf.natalenko.name/forum)
*   [Patchset changelog](http://freecode.com/projects/pf-kernel)
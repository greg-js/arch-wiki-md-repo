The Yocto Project (YP) is a popular open-source collaboration project focused on embedded Linux developers. In early versions of YP it could be problematic to get it running on Arch Linux. In later versions this is no longer the case, and hopefully in the future it will be even easier. For information about how to get it running on older version, there is a good guide [here](http://wor.github.io/bash/2013/08/11/embedded-excursions-part-1.html).

To use bitbake as a standalone tool, install [bitbake](https://aur.archlinux.org/packages/bitbake/). To edit bitbake recipes in vim, install [bitbake-vim](https://aur.archlinux.org/packages/bitbake-vim/).

For this guide the focus will be on YP Core 1.8 (Fido) and newer.

**Note:** Arch Linux is not validated to work with Yocto/Poky.

## Installation

[Install](/index.php/Install "Install") the [git](https://www.archlinux.org/packages/?name=git), [diffstat](https://www.archlinux.org/packages/?name=diffstat), [unzip](https://www.archlinux.org/packages/?name=unzip), [texinfo](https://www.archlinux.org/packages/?name=texinfo), [python2](https://www.archlinux.org/packages/?name=python2), [chrpath](https://www.archlinux.org/packages/?name=chrpath), [wget](https://www.archlinux.org/packages/?name=wget), [xterm](https://www.archlinux.org/packages/?name=xterm), [sdl](https://www.archlinux.org/packages/?name=sdl), [socat](https://www.archlinux.org/packages/?name=socat) and [cpio](https://www.archlinux.org/packages/?name=cpio) packages.

**Note:** For the 64-bit version of Arch Linux, [Install](/index.php/Install "Install") the [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) package from the official [multilib](/index.php/Multilib "Multilib") repository.

You may receive the following conflicts:

```
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y

```

Resolve these by choosing `y` (we actually want the multilib versions).

Clone the official git repository. In this example the *fido* branch is used.

```
$ git clone --branch fido git://git.yoctoproject.org/poky.git ~/poky

```

YP Core requires the use of [python2](https://www.archlinux.org/packages/?name=python2), from the [Python](/index.php/Python#Python_2 "Python") page:

```
$ mkdir -p ~/bin
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config
$ export PATH=~/bin:$PATH

```

**Note:** You will probably not get notified with **any message** if building the environment script fails because of invalid Python version.

## Build core-image-minimal

Time to build the *core-image-minimal* target. First place yourself in the `poky` directory and source the environment script. Then build it with *bitbake*:

```
$ cd ~/poky
$ source oe-init-build-env build-qemux86

```

**Tip:**

In `~/poky/build-qemux86/conf/local.conf`:

*   Change the directory for downloads in order to reuse them, example `DL_DIR ?= "~/poky-downloads"`.
*   The build system can use a substantial amount of disk space during the build process, in order to preserve disk space add the line `INHERIT += "rm_work"`.

 `$ bitbake core-image-minimal` 
```
WARNING: Host distribution "Arch-Linux" has not been validated with this version of the build system; you may possibly experience unexpected failures. It is recommended that you use a tested distribution.
Parsing recipes: 100%
|########################################################################################################################################################################################################################################################################################| Time: 00:02:42
Parsing of 884 .bb files complete (0 cached, 884 parsed). 1285 targets, 41 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION        = "1.26.0"
BUILD_SYS         = "x86_64-linux"
NATIVELSBSTRING   = "Arch-Linux"
TARGET_SYS        = "i586-poky-linux"
MACHINE           = "qemux86"
DISTRO            = "poky"
DISTRO_VERSION    = "1.8"
TUNE_FEATURES     = "m32 i586"
TARGET_FPU        = ""
meta              
meta-yocto        
meta-yocto-bsp    = "fido:08d32590411568e7bf11612ac695a6e9c6df6286"

NOTE: Preparing RunQueue
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
WARNING: Failed to fetch URL http://downloads.sourceforge.net/project/libpng/libpng16/1.6.16/libpng-1.6.16.tar.xz, attempting MIRRORS if available
NOTE: Tasks Summary: Attempted 1989 tasks of which 9 didn't need to be rerun and all succeeded.

Summary: There were 2 WARNING messages shown.

```

This will take some time to complete. For more details about yocto there is a [Quick Start Guide](http://www.yoctoproject.org/docs/1.8/yocto-project-qs/yocto-project-qs.html).

**Note:** The first warning about Arch Linux not been validated is expected. The second warning can happen when failing to download a resource, the build system will then attempt to get that resource from the next mirror.

## Run core-image-minimal

To run this image in [QEMU](/index.php/QEMU "QEMU"), start it with the *runqemu* command as follows:

 `$ runqemu qemux86` 
```
Continuing with the following parameters:
KERNEL: [/home/user/poky/build-qemux86/tmp/deploy/images/qemux86/bzImage-qemux86.bin]
ROOTFS: [/home/user/poky/build-qemux86/tmp/deploy/images/qemux86/core-image-minimal-qemux86-20150804095542.rootfs.ext4]
FSTYPE: [ext4]
Setting up tap interface under sudo
[sudo] password for user: 
Acquiring lockfile for tap0...
Running qemu-system-i386...
/home/user/poky/build-qemux86/tmp/sysroots/x86_64-linux/usr/bin/qemu-system-i386 -kernel /home/user/poky/build-qemux86/tmp/deploy/images/qemux86/bzImage-qemux86.bin -net nic,vlan=0 -net tap,vlan=0,ifname=tap0,script=no,downscript=no -cpu qemu32 -hda /home/user/poky/build-qemux86/tmp/deploy/images/qemux86/core-image-minimal-qemux86-20150804095542.rootfs.ext4 -show-cursor -usb -usbdevice wacom-tablet -vga vmware -no-reboot -m 256 --append "vga=0 uvesafb.mode_option=640x480-32 root=/dev/hda rw mem=256M ip=192.168.7.2::192.168.7.1:255.255.255.0 oprofile.timer=1 rootfstype=ext4 "
Set 'tap0' nonpersistent
Releasing lockfile of preconfigured tap device 'tap0'
```

**Tip:** If the kernel was recently updated, rebooting might help you avoid issues with *tunctl*.
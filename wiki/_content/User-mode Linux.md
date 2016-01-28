# User-mode Linux

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Dead project (last activity in 2007), [inaccurate information](/index.php/Talk:User-mode_Linux "Talk:User-mode Linux") (Discuss in [Talk:User-mode Linux#Needs work](https://wiki.archlinux.org/index.php/Talk:User-mode_Linux#Needs_work))

User-mode-Linux (UML) is a method to run Linux inside Linux as a normal process. Please check [[1]](http://user-mode-linux.sourceforge.net/) for in-depth information what UML is and how it works.

## Contents

*   [1 Why use UML?](#Why_use_UML.3F)
*   [2 HOWTO](#HOWTO)
    *   [2.1 Setup by hostfs + vde2](#Setup_by_hostfs_.2B_vde2)
        *   [2.1.1 Required packages](#Required_packages)
        *   [2.1.2 Launch script](#Launch_script)
    *   [2.2 Setup by rootfs + tap](#Setup_by_rootfs_.2B_tap)
        *   [2.2.1 Required packages](#Required_packages_2)
        *   [2.2.2 Build rootfs image](#Build_rootfs_image)

## Why use UML?

Running UML is a safe way to run multiple instances of (Arch-)Linux at the same time. The single processes are separated from each other, which makes it secure to run, for example, a testing instance and a production instance on the same machine. If something goes wrong inside the testing instance, it does not interfere with the host Linux or the productive instance.

## HOWTO

There are two methods:

*   Use hostfs with vde2 network (all UMLs use same file system)
*   Use rootfs with tap network (require build image)

Both methods are workable on Linux 3.4.4-3 (Jul 3 2012)

### Setup by hostfs + vde2

Hostfs means use the host's file system in read-only mode.

#### Required packages

*   [linux-usermode](https://aur.archlinux.org/packages/linux-usermode/)<sup><small>AUR</small></sup>
*   Utility packages: [vde2](https://www.archlinux.org/packages/?name=vde2) [screen](https://www.archlinux.org/packages/?name=screen) [start-stop-daemon](https://aur.archlinux.org/packages/start-stop-daemon/)<sup><small>AUR</small></sup> [rsyslog](https://www.archlinux.org/packages/?name=rsyslog)

#### Launch script

*   download [http://pastebin.com/qDE0D7Lk](http://pastebin.com/qDE0D7Lk) script as 2vm.bash
*   use normal user to launch 2vm.bash (there are two VMs named as 'C1' & 'C2')
*   modify the 2vm.bash to fit your requirements

### Setup by rootfs + tap

#### Required packages

*   [linux-usermode](https://aur.archlinux.org/packages/linux-usermode/)<sup><small>AUR</small></sup>
*   Utility packages: [vde2](https://www.archlinux.org/packages/?name=vde2) [uml_utilities_tunpatch](https://aur.archlinux.org/packages/uml_utilities_tunpatch/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/uml_utilities_tunpatch)]</sup>

#### Build rootfs image

1.) First you have to create a single, big file into which you will install Arch Linux. This command creates a single 1 GB file, only containing zeros, which should be enough for a basic Arch Linux installation.

```
dd if=/dev/zero of=rootfs bs=1MB count=1000

```

or

```
fallocate -l 1GB ./rootfs

```

2.) After the build process you have to format the root file system image:

```
mke2fs -F rootfs

```

3.) After formatting the file, you have to mount it. Executing the following command as root does the job (you have also to load the `loop` module with `modprobe`):

```
mount -o loop rootfs /mnt

```

4.) Now the installation of the basic system may start:

```
mkdir -p /mnt/var/lib/pacman
pacman -Sy base -r /mnt
cd /mnt/dev
mknod --mode=660 ubd0 b 98 0
chown root:disk ubd0

```

5.) Before the system can be booted with user-mode-Linux, some files inside the Arch basic system have to be customised. Add this line to `/mnt/etc/fstab`:

```
/dev/ubd0 / ext2 defaults 0 0

```

6.) Now unmount the file system.

**Warning:** If you change _anything_ inside your mounted file system (e.g. `/mnt`) while it is _running_, it may lead to significant file system corruption inside your virtual machine and _kill_ it!

```
umount /mnt

```

7.) Next step is to set up networking. Therefore, you create a so called tun device (Please visit the [UML how-to](http://user-mode-linux.sourceforge.net/old/UserModeLinux-HOWTO.html) for further information about tun/tap), and give it an IP address. The following lines load the necessary `tun` module, create a tun/tap device that is readable by the `users` group, and sets it up with the given IP address. For security, you should consider creating a certain UML group with read permissions for the network device.

```
modprobe tun
ip tuntap add tap0 mode tap group users
chown root.users /dev/net/tun
ip addr add 192.168.0.100/24 dev tap0

```

8.) Now you can boot the image. To use the network, you have to announce the proper device to the UML kernel. (Mind that the user running the UML command needs enough rights to access the tun device!)

```
vmlinux ubd0=rootfs eth0=tuntap,,,192.168.0.100

```

The `,,,` means:

```
eth0=transport,tuntap device,MAC address,ip

```

Example:

```
eth0=tuntap,tap0,3f:2a:bb:00:00:00,192.168.0.100

```

Headless example:

```
 vmlinux ubd0=rootfs eth0=tuntap,,,192.168.0.100 mem=128M con=pty

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=User-mode_Linux&oldid=392770](https://wiki.archlinux.org/index.php?title=User-mode_Linux&oldid=392770)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtualization](/index.php/Category:Virtualization "Category:Virtualization")

Hidden categories:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
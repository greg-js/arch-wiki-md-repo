User-mode-Linux (UML) is a method to run Linux inside Linux as a normal process. Please check [[1]](http://user-mode-linux.sourceforge.net/) for in-depth information what UML is and how it works.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Why use UML?](#Why_use_UML?)
*   [2 HOWTO](#HOWTO)
    *   [2.1 Setup by hostfs + vde2](#Setup_by_hostfs_+_vde2)
        *   [2.1.1 Required packages](#Required_packages)
        *   [2.1.2 Launch script](#Launch_script)
    *   [2.2 Setup by rootfs + tap](#Setup_by_rootfs_+_tap)
        *   [2.2.1 Required packages](#Required_packages_2)
        *   [2.2.2 Build rootfs image](#Build_rootfs_image)
    *   [2.3 Marionnet](#Marionnet)

## Why use UML?

Running UML is a safe way to run multiple instances of (Arch-)Linux at the same time. The single processes are separated from each other, which makes it secure to run, for example, a testing instance and a production instance on the same machine. If something goes wrong inside the testing instance, it does not interfere with the host Linux or the productive instance.

## HOWTO

There are three methods:

*   Use hostfs with vde2 network (all UMLs use same file system)
*   Use rootfs with tap network (require build image)
*   Use [Marionnet](https://www.marionnet.org/)

Both methods are workable on Linux 3.4.4-3 (Jul 3 2012)

### Setup by hostfs + vde2

Hostfs means use the host's file system in read-only mode.

#### Required packages

*   [linux-usermode](https://aur.archlinux.org/packages/linux-usermode/)
*   Utility packages: [vde2](https://www.archlinux.org/packages/?name=vde2) [screen](https://www.archlinux.org/packages/?name=screen) [start-stop-daemon](https://aur.archlinux.org/packages/start-stop-daemon/) [rsyslog](https://aur.archlinux.org/packages/rsyslog/)

#### Launch script

*   download [http://pastebin.com/qDE0D7Lk](http://pastebin.com/qDE0D7Lk) script as 2vm.bash
*   use normal user to launch 2vm.bash (there are two VMs named as 'C1' & 'C2')
*   modify the 2vm.bash to fit your requirements

### Setup by rootfs + tap

#### Required packages

*   [linux-usermode](https://aur.archlinux.org/packages/linux-usermode/)
*   Utility packages: [vde2](https://www.archlinux.org/packages/?name=vde2) [uml_utilities_tunpatch](https://aur.archlinux.org/packages/uml_utilities_tunpatch/)

#### Build rootfs image

1.) First you have to create a single, big file into which you will install Arch Linux. This command creates a single 1 GiB file, only containing zeros, which should be enough for a basic Arch Linux installation.

```
dd if=/dev/zero of=rootfs bs=1M count=1024

```

or

```
fallocate -l 1GiB ./rootfs

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

**Warning:** If you change *anything* inside your mounted file system (e.g. `/mnt`) while it is *running*, it may lead to significant file system corruption inside your virtual machine and *kill* it!

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

### Marionnet

For use [Marionnet](https://www.marionnet.org/), you must install [uml_utilities](https://aur.archlinux.org/packages/uml_utilities/), and see [https://bugs.launchpad.net/marionnet/+bug/1580349](https://bugs.launchpad.net/marionnet/+bug/1580349).
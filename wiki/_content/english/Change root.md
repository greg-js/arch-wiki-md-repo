[Chroot](https://en.wikipedia.org/wiki/Chroot "wikipedia:Chroot") is an operation that changes the apparent root directory for the current running process and their children. A program that is run in such a modified environment cannot access files and commands outside that environmental directory tree. This modified environment is called a *chroot jail*.

## Contents

*   [1 Reasoning](#Reasoning)
*   [2 Requirements](#Requirements)
*   [3 Partition(s) mount](#Partition.28s.29_mount)
*   [4 Change root](#Change_root)
    *   [4.1 Using arch-chroot](#Using_arch-chroot)
    *   [4.2 Using chroot](#Using_chroot)
    *   [4.3 Using systemd-nspawn](#Using_systemd-nspawn)
*   [5 Run graphical applications from chroot](#Run_graphical_applications_from_chroot)
*   [6 Exit from the chroot environment](#Exit_from_the_chroot_environment)
*   [7 Without root privileges](#Without_root_privileges)
    *   [7.1 Proot](#Proot)
    *   [7.2 Fakechroot](#Fakechroot)
*   [8 See also](#See_also)

## Reasoning

Changing root is commonly done for performing system maintenance on systems where booting and/or logging in is no longer possible. Common examples are:

*   Reinstalling the [bootloader](/index.php/Bootloader "Bootloader").
*   Rebuilding the [initramfs image](/index.php/Mkinitcpio "Mkinitcpio").
*   Upgrading or [downgrading packages](/index.php/Downgrading_packages "Downgrading packages").
*   Resetting a [forgotten password](/index.php/Password_recovery "Password recovery").

See also [Wikipedia:Chroot#Limitations](https://en.wikipedia.org/wiki/Chroot#Limitations "wikipedia:Chroot").

## Requirements

*   Root privilege.

*   Another Linux environment, e.g. a LiveCD or USB flash media, or from another existing Linux distribution.

*   Matching architecture environments; i.e. the chroot from and chroot to. The architecture of the current environment can be discovered with: `uname -m` (e.g. i686 or x86_64).

*   Kernel modules loaded that are needed in the chroot environment.

*   Swap enabled if needed: `# swapon /dev/sdxY` 

*   Internet connection established if needed.

## Partition(s) mount

The root partition of the Linux system that you are trying to chroot into needs to be mounted first. To find out the device name assigned by the kernel, run:

```
# lsblk

```

Then create a directory for mounting the root partition to, and mount it:

```
# mkdir /mnt/arch
# mount /dev/sdx1 /mnt/arch

```

Next, if there are separate filesystems for other system directories (e.g. `/boot`, `/home`...) mount them too:

```
# mount /dev/sdx2 /mnt/arch/boot/
# mount /dev/sdx3 /mnt/arch/home/

```

**Note:** If trying to access an [encrypted](/index.php/Disk_encryption "Disk encryption") filesystem, do not forget to first unlock its container (e.g. with `# cryptsetup open /dev/sdX# *name*` for [dm-crypt/LUKS](/index.php/Disk_encryption#Block_device_encryption "Disk encryption")-based encryption), then mount the device using its previously supplied device-mapper *name* (under the form `# mount /dev/mapper/*name* /mnt/arch/...`). More info: [Unlocking/Mapping LUKS partitions with the device mapper](/index.php/Dm-crypt/Device_encryption#Unlocking.2FMapping_LUKS_partitions_with_the_device_mapper "Dm-crypt/Device encryption").

## Change root

**Note:** Some [systemd](/index.php/Systemd "Systemd") tools such as *localectl* and *timedatectl* do not work inside a chroot, as they require an active [dbus](/index.php/Dbus "Dbus") connection. [[1]](https://github.com/systemd/systemd/issues/798#issuecomment-126568596)

### Using arch-chroot

The bash script `arch-chroot` is part of the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) package from the [official repositories](/index.php/Official_repositories "Official repositories"). Before running `/usr/bin/chroot` the script mounts api filesystems like `/proc` and makes `/etc/resolv.conf` available from the chroot.

Run arch-chroot with the new root directory as first argument:

```
# arch-chroot /mnt/arch

```

To run a bash shell instead of the default sh:

```
# arch-chroot /mnt/arch /bin/bash

```

To run `mkinitcpio -p linux` from the chroot, and exit again:

```
# arch-chroot /mnt/arch /usr/bin/mkinitcpio -p linux

```

### Using chroot

Mount the temporary api filesystems:

```
# cd /mnt/arch
# mount -t proc proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/

```

And optionally:

```
# mount --rbind /run run/

```

To use an internet connection in the chroot environment copy over the DNS details:

```
# cp /etc/resolv.conf etc/resolv.conf

```

To change root into a bash shell:

```
# chroot /mnt/arch /bin/bash

```

**Note:** If you see the error:

*   `chroot: cannot run command '/usr/bin/bash': Exec format error`, it is likely that the architectures of the host environment and chroot environment do not match.
*   `chroot: '/usr/bin/bash': permission denied`, remount with the exec permission: `mount -o remount,exec /mnt/arch`.

After chrooting it may be necessary to load the local bash configuration:

```
# source /etc/profile
# source ~/.bashrc

```

**Tip:** Optionally, create a unique prompt to be able to differentiate your chroot environment: `# export PS1="(chroot) $PS1"` 

### Using systemd-nspawn

systemd-nspawn may be used to run a command or OS in a light-weight namespace container. In many ways it is similar to chroot, but more powerful since it fully virtualizes the file system hierarchy, as well as the process tree, the various IPC subsystems and the host and domain name.

Change directory to the mountpoint of the root partition and run systemd-nspawn:

```
# cd /mnt/arch
# systemd-nspawn

```

It is not necessary to mount api filesystems like `/proc` manually, as systemd-nspawn starts a new init process in the contained environment which takes care of everything. It is like booting up a second Linux OS on the same machine, but it is not a virtual machine.

To quit, just log out or issue the poweroff command. You can then unmount the partitions as described in [#Exit from the chroot environment](#Exit_from_the_chroot_environment).

## Run graphical applications from chroot

If you have an [X server](/index.php/X_server "X server") running on your system, you can start graphical applications from the chroot environment.

To allow the chroot environment to connect to an X server, open a virtual terminal inside the X server (i.e. inside the desktop of the user that is currently logged in), then run the [xhost](/index.php/Xhost "Xhost") command, which gives permission to anyone to connect to the user's X server:

```
$ xhost +local:

```

Then, to direct the applications to the X server from chroot, set the DISPLAY environment variable inside the chroot to match the DISPLAY variable of the user that owns the X server. So for example, run

```
$ echo $DISPLAY

```

as the user that owns the X server to see the value of DISPLAY. If the value is ":0" (for example), then in the chroot environment run

```
# export DISPLAY=:0

```

## Exit from the chroot environment

When you are finished with system maintenance, exit from the chroot:

```
# exit

```

Last, unmount the temporary filesystems and the root partition:

```
# cd /
# umount --recursive /mnt/arch/

```

**Note:** If there is an error mentioning something like: `umount: /path: device is busy` this usually means that either: a program (even a shell) was left running in the chroot or that a sub-mount still exists. Quit the program and use `mount` to find and `umount` sub-mounts). It may be tricky to `umount` some things and one can hopefully have `umount --force` work, as a last resort use `umount --lazy` which just releases them. In either case to be safe, `reboot` as soon as possible if these are unresolved to avoid future, possible conflicts.

## Without root privileges

Chroot requires root privileges, which may not be desirable or possible for the user to obtain in certain situations. There are, however, various ways to simulate chroot-like behavior using alternative implementations.

### Proot

[Proot](/index.php/Proot "Proot") may be used to change the apparent root directory and use `mount --bind` without root privileges. This is useful for confining applications to a single directory or running programs built for a different CPU architecture, but it has limitations due to the fact that all files are owned by the user on the host system. Proot provides a `--root-id` argument that can be used as a workaround for some of these limitations in a similar (albeit more limited) manner to *fakeroot*.

### Fakechroot

[fakechroot](https://www.archlinux.org/packages/?name=fakechroot) is a library shim which intercepts the chroot call and fakes the results. It can be used in conjunction with [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) to simulate a chroot as a regular user.

```
# fakechroot fakeroot chroot ~/my-chroot bash

```

## See also

*   [Basic Chroot](https://help.ubuntu.com/community/BasicChroot)
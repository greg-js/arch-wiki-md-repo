[udisks](http://www.freedesktop.org/wiki/Software/udisks/) provides a daemon *udisksd*, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool *udisksctl*, used to query and use the daemon.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Mount helpers](#Mount_helpers)
    *   [3.1 devmon](#devmon)
    *   [3.2 udevadm monitor](#udevadm_monitor)
    *   [3.3 udiskie](#udiskie)
    *   [3.4 udisksvm](#udisksvm)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Mount to /media (udisks2)](#Mount_to_.2Fmedia_.28udisks2.29)
    *   [4.2 Mount loop devices](#Mount_loop_devices)
    *   [4.3 Hide selected partitions](#Hide_selected_partitions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Hidden devices (udisks2)](#Hidden_devices_.28udisks2.29)
    *   [5.2 Devices do not remain unmounted (udisks)](#Devices_do_not_remain_unmounted_.28udisks.29)
*   [6 See also](#See_also)

## Installation

There are two versions of *udisks* called [udisks](https://www.archlinux.org/packages/?name=udisks) and [udisks2](https://www.archlinux.org/packages/?name=udisks2). Development of *udisks* has ceased in favor of *udisks2*. [[1]](http://davidz25.blogspot.be/2012/03/simpler-faster-better.html)

*udisksd* ([udisks2](https://www.archlinux.org/packages/?name=udisks2)) and *udisks-daemon* ([udisks](https://www.archlinux.org/packages/?name=udisks)) are started on-demand by [D-Bus](/index.php/D-Bus "D-Bus"), and should not be enabled explicitly (see `man udisksd` and `man udisks-daemon`). They can be controlled through the command-line with *udisksctl* and *udisks*, respectively. See `man udisksctl` and `man udisks` for more information.

## Configuration

Actions a user can perform using udisks are restricted with [Polkit](/index.php/Polkit "Polkit"). If your [session](/index.php/Session "Session") is not activated or present, for example, when controlling udisks from [systemd/User](/index.php/Systemd/User "Systemd/User"), configure policykit manually.

See [[2]](https://github.com/coldfix/udiskie/wiki/Permissions) for common udisks permissions for the `storage` group, and [[3]](https://gist.github.com/grawity/3886114#file-udisks2-allow-mount-internal-js) for a more restrictive example.

## Mount helpers

The automatic mounting of devices is easily achieved with udisks wrappers. See also [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications") and [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality").

### devmon

[udevil](https://www.archlinux.org/packages/?name=udevil) includes [devmon](http://igurublog.wordpress.com/downloads/script-devmon), which is compatible with *udisks* and *udisks2*. It uses mount helpers with the following priority:

1.  [udevil](http://ignorantguru.github.io/udevil/) (SUID)
2.  pmount (SUID)
3.  udisks
4.  udisks2

To mount devices with *udisks* or *udisks2*, remove the SUID permission from *udevil*:

```
# chmod -s /usr/bin/udevil

```

**Note:** `chmod -x /usr/bin/udevil` as root causes devmon to use *udisks* for device monitoring

**Tip:** To run devmon in the background and automatically mount devices, [enable](/index.php/Enable "Enable") it with `devmon@.service`, taking the user name as argument: `devmon@*user*.service`. Keep in mind that services run outside the [session](/index.php/Session "Session"). Adjust [Polkit](/index.php/Polkit "Polkit") rules where appropriate, or run *devmon* from the user session (see [Autostart](/index.php/Autostart "Autostart")).

### udevadm monitor

You may use `udevadm monitor` to monitor block events and mount drives when a new block device is created. Stale mount points are automatically removed by *udisksd*, such that no special action is required on deletion.

```
#!/bin/bash

pathtoname() {
    udevadm info -p "/sys/$1" | awk -v FS== '/DEVNAME/ {print $2}'
}

while read -r _ _ event devpath _; do
        if [[ $event == add ]]; then
            devname=$(pathtoname "$devpath")
            udisksctl mount --block-device "$devname" --no-user-interaction
        fi
done < <(stdbuf -o L udevadm monitor --udev -s block)

```

### udiskie

[udiskie](https://github.com/coldfix/udiskie) is a mount helper using either [udisks](https://www.archlinux.org/packages/?name=udisks) or [udisks2](https://www.archlinux.org/packages/?name=udisks2). It includes support for password protected [LUKS devices](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption"). See the udiskie wiki for [usage details](https://github.com/coldfix/udiskie/wiki/Usage).

### udisksvm

[udisksvm](https://aur.archlinux.org/packages/udisksvm) is a graphical udisks2 wrapper application written in Python3 and using the Qt5 framework. It uses only mouse clicks to mount, unmount removable devices or eject a CD/DVD. It is well adapted to light weight graphical environments, like Openbox with Tint2. It is a stand-alone mounting/automounting application running in background (see the README file in the package for details).

## Tips and tricks

### Mount to /media (udisks2)

By default, udisks2 mounts removable drives under the ACL controlled directory `/run/media/$USER/`. If you wish to mount to `/media` instead, use this rule:

 `/etc/udev/rules.d/99-udisks2.rules` 
```
# UDISKS_FILESYSTEM_SHARED
# ==1: mount filesystem to a shared directory (/media/VolumeName)
# ==0: mount filesystem to a private directory (/run/media/$USER/VolumeName)
# See udisks(8)
ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1"

```

### Mount loop devices

To easily mount ISO images, use the following command:

```
$ udisksctl loop-setup -r -f *image.iso*

```

This will create a loop device and show the ISO image ready to mount. Once unmounted, the loop device will be terminated by [udev](/index.php/Udev "Udev").

**Note:** This mounts a read only image. To mount raw disk images, such as for [QEMU](/index.php/QEMU "QEMU"), remove the `-r` flag, and release the image after use with `udisksctl loop-delete -b */dev/loop0*`. Substitute `/dev/loop0` with the name of the loop device.

### Hide selected partitions

If you wish to prevent certain partitions or drives appearing on the desktop, you can create a udev rule, for example `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

shows all partitions with the exception of `sda1` and `sda2` on your desktop. Note that if you are using [udisks2](https://www.archlinux.org/packages/?name=udisks2), the above will not work as `UDISKS_PRESENTATION_HIDE` is no longer supported. Instead, use `UDISKS_IGNORE` as follows:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

Because block device names can change between reboots, it is also possible to use UUIDs (as gathered from executing the `blkid /dev/sdX` command) to hide partitions or whole devices:

For example:

```
# blkid /dev/sdX
/dev/sdX: LABEL="Filesystem Label" UUID="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXX" UUID_SUB="YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY" TYPE="btrfs"

```

Then the following line can be used:

```
ENV{ID_FS_UUID}=="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXX", ENV{UDISKS_IGNORE}="1"

```

The above line is also useful to hide multi device btrfs filesystems, as all the devices from a single btrtfs filesystem will share the same UUID across the devices but will have different SUB_UUID for each individual device.

## Troubleshooting

### Hidden devices (udisks2)

Udisks2 hides certain devices from the user by default. If this is undesired or otherwise problematic, copy `/usr/lib/udev/rules.d/80-udisks2.rules` to `/etc/udev/rules.d/80-udisks2.rules` and remove the following section in the copy:

```
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# Devices which should not be display in the user interface
[...]

```

### Devices do not remain unmounted (udisks)

*udisks* remounts devices after a given period, or *polls* those devices. This can cause unexpected behaviour, for example when formatting drives, sharing them in a [virtual machine](/index.php/Virtual_machine "Virtual machine"), power saving, or removing a drive that was not detached with `--detach` before.

To disable polling for a given device, for example a CD/DVD device:

```
# udisks --inhibit-polling /dev/sr*0*

```

or for all devices:

```
# udisks --inhibit-all-polling

```

See `man udisks` for more information.

## See also

*   [gentoo wiki: udisks](http://wiki.gentoo.org/wiki/Udisks)
*   [Introduction to udisks](http://blog.fpmurphy.com/2011/08/introduction-to-udisks.html?output=pdf)
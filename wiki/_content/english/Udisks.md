[udisks](http://www.freedesktop.org/wiki/Software/udisks/) provides a daemon _udisksd_, that implements D-Bus interfaces used to query and manipulate storage devices, and a command-line tool _udisksctl_, used to query and use the daemon.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Mount helpers](#Mount_helpers)
    *   [3.1 Devmon](#Devmon)
    *   [3.2 inotify](#inotify)
    *   [3.3 udiskie](#udiskie)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Mount to /media (udisks2)](#Mount_to_.2Fmedia_.28udisks2.29)
    *   [4.2 Mount an ISO image](#Mount_an_ISO_image)
    *   [4.3 Hide selected partitions](#Hide_selected_partitions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Hidden devices (udisks2)](#Hidden_devices_.28udisks2.29)
    *   [5.2 Devices do not remain unmounted (udisks)](#Devices_do_not_remain_unmounted_.28udisks.29)
    *   [5.3 Devices no longer mounted after physical removal](#Devices_no_longer_mounted_after_physical_removal)
*   [6 See also](#See_also)

## Installation

There are two versions of _udisks_ called [udisks](https://www.archlinux.org/packages/?name=udisks) and [udisks2](https://www.archlinux.org/packages/?name=udisks2). Development of _udisks_ has ceased in favor of _udisks2_. [[1]](http://davidz25.blogspot.be/2012/03/simpler-faster-better.html)

_udisksd_ ([udisks2](https://www.archlinux.org/packages/?name=udisks2)) and _udisks-daemon_ ([udisks](https://www.archlinux.org/packages/?name=udisks)) are started on-demand by [D-Bus](/index.php/D-Bus "D-Bus"), and should not be enabled explicitly (see `man udisksd` and `man udisks-daemon`). They can be controlled through the command-line with _udisksctl_ and _udisks_, respectively. See `man udisksctl` and `man udisks` for more information.

## Configuration

Actions a user can perform using udisks are restricted with [Polkit](/index.php/Polkit "Polkit"). If your [session](/index.php/Session "Session") is not activated or present, for example, when controlling udisks from [systemd/User](/index.php/Systemd/User "Systemd/User"), configure policykit manually.

See [[2]](https://github.com/coldfix/udiskie/wiki/Permissions) for common udisks permissions for the `storage` group, and [[3]](https://gist.github.com/grawity/3886114#file-udisks2-allow-mount-internal-js) for a more restrictive example.

## Mount helpers

Automatic mounting of devices is easily achieved with udisks wrappers. See also [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications") and [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality").

### Devmon

[udevil](https://www.archlinux.org/packages/?name=udevil) includes [devmon](http://igurublog.wordpress.com/downloads/script-devmon), which is compatible to _udisks_ and _udisks2_. It uses mount helpers with the following priority:

1.  [udevil](http://ignorantguru.github.io/udevil/) (SUID)
2.  pmount (SUID)
3.  udisks
4.  udisks2

To mount devices with _udisks_ or _udisks2_, remove the SUID permission from _udevil_:

```
# chmod -s /usr/bin/udevil

```

**Note:** `chmod -x /usr/bin/udevil` as root causes devmon to use _udisks_ for device monitoring

**Tip:** To run devmon in the background and automatically mount devices, [enable](/index.php/Enable "Enable") it with `devmon@.service`, taking the user name as argument: `devmon@_user_.service`. Keep in mind services run outside the [session](/index.php/Session "Session"). Adjust [Polkit](/index.php/Polkit "Polkit") rules where appropriate, or run _devmon_ from the user session (see [Autostart](/index.php/Autostart "Autostart")).

### inotify

You may use [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) to monitor `/dev`, and mount drives when a new block device is created. Stale mount points are automatically removed by _udisksd_, such that no special action is required on deletion.

```
#!/bin/bash
pattern='sd[b-z][1-9]$'
coproc inotifywait --monitor --event create,delete --format '%e %w%f' /dev

while read -r -u "${COPROC[0]}" event file; do
    if [[ $file =~ $pattern ]]; then
	case $event in
	    CREATE)
		echo "Settling..."; sleep 1
		udisksctl mount --block-device $file --no-user-interaction
		;;
	    DELETE)
		;;
	esac
    fi
done

```

### udiskie

[udiskie](https://github.com/coldfix/udiskie) is a mount helper using either [udisks](https://www.archlinux.org/packages/?name=udisks) or [udisks2](https://www.archlinux.org/packages/?name=udisks2). It includes support for password protected [LUKS devices](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption"). See the udiskie wiki for [usage details](https://github.com/coldfix/udiskie/wiki/Usage).

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

### Mount an ISO image

To easily mount ISO images, use the following command:

```
$ udisksctl loop-setup -r -f _image.iso_

```

This will create a loop device and show the ISO image ready to mount. Once unmounted, the loop device will be terminated by [udev](/index.php/Udev "Udev").

### Hide selected partitions

If you wish to prevent certain partitions or drives appearing on the desktop, you can create a udev rule, for example `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

shows all partitions with the exception of `sda1` and `sda2` on your desktop. Notice if you are using [udisks2](https://www.archlinux.org/packages/?name=udisks2) the above will not work as `UDISKS_PRESENTATION_HIDE` is no longer supported. Instead use `UDISKS_IGNORE` as follows:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

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

_udisks_ remounts devices after a given period, or _polls_ those devices. This can cause unexpected behaviour, for example when formatting drives, sharing them in a [virtual machine](/index.php/Virtual_machine "Virtual machine"), power saving, or removing a drive that was not detached with `--detach` before.

To disable polling for a given device, for example a CD/DVD device:

```
# udisks --inhibit-polling /dev/sr_0_

```

or for all devices:

```
# udisks --inhibit-all-polling

```

See `man udisks` for more information.

### Devices no longer mounted after physical removal

This may happen when both udisks and [systemd](/index.php/Systemd "Systemd") try to unmount a device that is no longer present. [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1588027#p1588027) [[5]](https://github.com/systemd/systemd/issues/1741) Example error messages:

```
Jan 16 18:46:04 thinkpad systemd[1]: media-ASMT_2105.mount: Unit is bound to inactive unit dev-sdc2.device. Stopping, too.
Jan 16 18:46:04 thinkpad systemd[1]: Unmounting /media/ASMT_2105...

```

To reset the state of the mount unit, run:

```
# systemctl reset-failed

```

## See also

*   [gentoo wiki: udisks](http://wiki.gentoo.org/wiki/Udisks)
*   [Introduction to udisks](http://blog.fpmurphy.com/2011/08/introduction-to-udisks.html?output=pdf)
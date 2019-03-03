Related articles

*   [Android#Transferring files](/index.php/Android#Transferring_files "Android")
*   [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

The [Media Transfer Protocol](https://en.wikipedia.org/wiki/Media_Transfer_Protocol "wikipedia:Media Transfer Protocol") (MTP) can be used to transfer media files to and from many mobile phones (all Windows Phone 7/8/10 devices, most newer [Android](/index.php/Android "Android") devices) and media players (e.g. Creative Zen).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Connecting](#Connecting)
*   [2 FUSE filesystems](#FUSE_filesystems)
    *   [2.1 mtpfs](#mtpfs)
    *   [2.2 jmtpfs](#jmtpfs)
    *   [2.3 simple-mtpfs](#simple-mtpfs)
    *   [2.4 go-mtpfs](#go-mtpfs)
    *   [2.5 Android File Transfer](#Android_File_Transfer)
*   [3 libmtp](#libmtp)
*   [4 Media players](#Media_players)
*   [5 File manager integration](#File_manager_integration)
    *   [5.1 gvfs-mtp](#gvfs-mtp)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 jmtpfs: Input/output error upon first access](#jmtpfs:_Input/output_error_upon_first_access)
    *   [6.2 kio-mtp: cannot use "Open with File Manager" action](#kio-mtp:_cannot_use_"Open_with_File_Manager"_action)
    *   [6.3 kio-mtp being called simultaneously by different services](#kio-mtp_being_called_simultaneously_by_different_services)
    *   [6.4 Android File Transfer: connect failed: no MTP device found](#Android_File_Transfer:_connect_failed:_no_MTP_device_found)

## Connecting

To connect your computer to a device via MTP:

*   the device needs to be connected to your computer via USB
*   MTP needs to be enabled on the device
*   the device's screen needs to be unlocked (for security reasons)

## FUSE filesystems

The following programs let you access MTP devices via a [FUSE](/index.php/FUSE "FUSE") filesystem:

*   **[#Android File Transfer](#Android_File_Transfer)** — MTP client with CLI, Qt UI, and FUSE wrapper; uses custom MTP implementation

	[https://whoozle.github.io/android-file-transfer-linux/](https://whoozle.github.io/android-file-transfer-linux/) || [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer)

*   **[#go-mtpfs](#go-mtpfs)** — FUSE filesystem with custom MTP implementation, written in Go

	[https://github.com/hanwen/go-mtpfs](https://github.com/hanwen/go-mtpfs) || [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/)

*   [#libmtp](#libmtp) based FUSE filesystems:
    *   [#mtpfs](#mtpfs), [mtpfs](https://www.archlinux.org/packages/?name=mtpfs), [https://www.adebenham.com/mtpfs/](https://www.adebenham.com/mtpfs/)
    *   [#jmtpfs](#jmtpfs), [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/), [https://github.com/JasonFerrara/jmtpfs](https://github.com/JasonFerrara/jmtpfs)
    *   [#simple-mtpfs](#simple-mtpfs), [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/), [https://github.com/phatina/simple-mtpfs/](https://github.com/phatina/simple-mtpfs/)

**Note:** MTP is messy and its implementation varies between devices. Try the above clients to see which one works best with your device.

**Tip:** It is recommended to reboot your computer after installing MTP related packages.

For the FUSE-based file systems, you might need to create the mount-point directory first. The directory `~/mnt` is used as an example below.

FUSE mounts can generally be unmounted using `fusermount -u *mountpoint*`.

### mtpfs

**Note:** The following is likely to not work and you might have to resort to [libgphoto2](/index.php/Libgphoto2 "Libgphoto2") or a file manager with gvfs support like [PCManFM](/index.php/PCManFM "PCManFM").

First edit your `/etc/fuse.conf` and uncomment the following line:

```
user_allow_other

```

Mount your device on `~/mnt`:

```
$ mtpfs -o allow_other ~/mnt

```

### jmtpfs

Mount device on `~/mnt`:

```
$ jmtpfs ~/mnt

```

Make this cohere to the rest of Linux (use regular mount/umount commands) by doing two steps

```
$# ln -s <actual mount command's path/name>  <a name consistent with Linux's mount convention>
$  ln -s /sbin/jmtpfs                        /sbin/mount.jmtpfs

```

add this line to /etc/fstab;

```
 #jmtpfs <mount path>        fuse nodev,allow_other,<other options>                             0    0
  jmtpfs /home/sam/run/motog fuse nodev,allow_other,rw,user,noauto,noatime,uid=1000,gid=1000    0    0

```

Now mount the device and see if the options "took"

```
 $ mount /home/sam/run/motog
 Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
 Android device detected, assigning default bug flags
 $ mount 
  ...
  jmtpfs on /home/sam/run/motog type fuse.jmtpfs (rw,nosuid,nodev,noexec,noatime,user_id=1000,group_id=1000,allow_other,user=sam)

```

### simple-mtpfs

Run `simple-mtpfs -l` to list detected devices.

To mount the first device in the list to `~/mnt`, run `simple-mtpfs --device 1 ~/mnt`.

### go-mtpfs

**Note:** Mounting with `go-mtpfs` might fail if an external SD Card is present. If you try to access your device while having an SD card and go-mtpfs complains, try removing the SD card and mounting again.

Install [android-udev](https://www.archlinux.org/packages/?name=android-udev), which will allow you to edit `/etc/udev/rules.d/51-android.rules` and apply to your `idVendor` and `idProduct`, which you can see after running *mtp-detect*. To the end of the line, add your user `OWNER="<user>"`.

Mount device on `~/mnt`:

```
$ go-mtpfs ~/mnt

```

**Note:** When using multiple devices you may want to use the `-d` flag to specify a device (id can be found by running `mtp-detect`)

### Android File Transfer

	FUSE interface

Mount your device on `~/my-device`:

```
$ mkdir ~/my-device
$ aft-mtp-mount ~/my-device

```

If you want album art to be displayed, it must be named `albumart.xxx` and placed first in the destination folder. Then copy other files. Also, note that fuse could be 7-8 times slower than ui/cli file transfer.

	Qt user interface

Start the application, choose a destination folder and click any button on the toolbar. Available options are: *Upload Album*, *Upload Directory* and *Upload Files*. The latter two are self-explanatory. *Upload album* searches the source directory for album covers, and sets the best available cover.

## libmtp

[libmtp](http://libmtp.sourceforge.net/) is a library MTP implementation, which also comes with some example command-line tools (which you can list using `pacman -Ql libmtp`).

[Install](/index.php/Install "Install") the [libmtp](https://www.archlinux.org/packages/?name=libmtp) package.

Run `mtp-detect` to detect your device.

If an error is returned, make sure your user is in the `uucp` [user group](/index.php/User_group "User group").

You can transfer files using the `mtp-connect` command.

## Media players

You can also use your MTP device in music players such as [Amarok](/index.php/Amarok "Amarok"). To achieve this, you might have to edit `/etc/udev/rules.d/51-android.rules` (the MTP device used in the following example is a Galaxy Nexus). Run:

```
$ lsusb

```

Search for your device. It should be something like that:

```
Bus 003 Device 011: ID 04e8:6860 Samsung Electronics Co., Ltd GT-I9100 Phone [Galaxy S II], GT-P7500 [Galaxy Tab 10.1]

```

And entry to `/etc/udev/rules.d/51-android.rules` will be this:

```
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", ATTR{idProduct}=="6860", MODE="0666", OWNER="[username]"

```

Also reload udev rules:

```
# udevadm control --reload

```

## File manager integration

To view the contents of your Android device's storage via MTP in your file manager, install the corresponding plugin:

*   For file managers that use [GVFS](/index.php/GVFS "GVFS") (GNOME Files), install [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) for MTP or [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) for PTP support.
*   For file managers that use KIO (KDE's Dolphin), MTP support is included in [kio-extras](https://www.archlinux.org/packages/?name=kio-extras) (dependency of dolphin).

After installing the required package, the device should show up in the file manager automatically and be accessible via an URL, for example `mtp://[usb:002,013]/`.

### gvfs-mtp

The [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) is available in the official repositories.

With `lsusb` you can get information about your device where Bus and Device numbers can be used with `gvfs-mtp` and device ID for creating of an [udev](/index.php/Udev "Udev") rule.

```
Bus **002** Device **018**: ID **04b7**:**88a9** Compal Electronics, Inc.
(...)

```

To see detected device with enabled MTP

Use *gvfs-mount*:

 `gvfs-mount -li | grep -e ^Volume -e activation_root` 
```
Volume(0): MT65xx Android Phone
  activation_root=mtp://[usb:**002**,**018**]/
```

Use *lsusb*:

 `lsusb -v 2> /dev/null | grep -e Bus -e iInterface -e bInterfaceProtocol` 
```
(......
......)
Bus 002 Device 018: ID 04b7:88a9 Compal Electronics, Inc. 
      bInterfaceProtocol      0 
      iInterface              5 MTP
(......
......)

```

To mount all available connected MTP devices use inline script

```
gvfs-mount -li | awk -F= '{if(index($2,"mtp") == 1)system("gvfs-mount "$2)}'

```

To mount or dismount from a command with gvfs-mtp use Bus and Device numbers, e.g. to mount `gvfs-mount mtp://[usb:001,007]/` and to unmount `gvfs-mount -u mtp://[usb:001,007]/`. The mounted device will be available in a directory that begins with *mtp:host=* and is located under */run/user/$UID/gvfs/*.

Disable automount of MTP devises with gvfs you will need to change value *true* to *false* for variable *AutoMount* that is located in `/usr/share/gvfs/mounts/mtp.mount`.

**Note:** The file managers can have own options for automount. On start they checking for all available mountable devices.

If your device isn't showing up in the file manager then [#libmtp](#libmtp) is missing a native support and is not currently available in the list of the [supported devices](https://sourceforge.net/p/libmtp/code/ci/HEAD/tree/src/music-players.h). If you will try to mount by using command line you may also get an error

```
Device 0 (VID=*XXXX* and PID=*XXXX*) is UNKNOWN.
Please report this VID/PID and the device model to the libmtp development team
```

The workaround to make it shown in the file manager is to write an [udev](/index.php/Udev "Udev") rule for the device but it is no guaranty that you will be able to mount it with by using MTP connection.

Use ID number that represents by pattern **vendorId**:**productID**,e.g. **04b7**:**88a9**, and make an udev rule by creating a configuration file

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="04b7", ATTR{idProduct}=="88a9", MODE="0660", GROUP="uucp", ENV{ID_MTP_DEVICE}="1", SYMLINK+="libmtp"

```

Reload the udev rules.

```
# udevadm control --reload

```

The file managers with support for [gvfs](/index.php/Gvfs "Gvfs") will be able to show MTP devices and mount them if supported by [#libmtp](#libmtp) but if has no support and cannot be opened then change settings in the phone to PTP and install [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) for having access at least to the photos, command line mounting of PTP is a little similar to mounting of the MTP devices: `gvfs-mount gphoto2://[usb:002,019]/`.

**Note:** If you getting limited access to the device and cannot use standard commands from command line such as e.g. `cp`,`ls` then look for [gvfs](/index.php/Gvfs "Gvfs") own alternatives, `ls -1 /usr/bin/gvfs-*`.

## Troubleshooting

### jmtpfs: Input/output error upon first access

Symptoms: jmtpfs successfully mounts, but as soon as one attempts to access files on the device (e.g. via `ls`), an error is reported:

```
 cannot access <mount-point>: Input/output error

```

This appears to be a security feature: MTP does not work when the phone is locked by the lockscreen. Unlock the phone and it should work again as long as the cord remains connected.

### kio-mtp: cannot use "Open with File Manager" action

If you are not able to use the action "Open with File Manager", you may work around this problem by editing the file `/usr/share/solid/actions/solid_mtp.desktop`.

Change the line `Exec=kioclient exec mtp:udi=%i/` to `Exec=dolphin "mtp:/"`.

### kio-mtp being called simultaneously by different services

Parallel usage of mtpfs and kio-mtp, as well as conflicting services using kio-mtp -music players included- should be avoided, as mentioned in [this forum](https://bbs.archlinux.org/viewtopic.php?pid=1657736#p1657736).

Amarok's plugin for MTP services, for example, might be preventing Dolphin (plasma) to access different phone model's files. Switching it off was a solution for at least one user.

### Android File Transfer: connect failed: no MTP device found

After installing [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer), while trying to mount any MTP device if you get the following error:

 `$ aft-mtp-mount /path/to/folder` 
```
connect failed: no MTP device found

```

then install the package: [android-udev](https://www.archlinux.org/packages/?name=android-udev). This package contains per manufacturer/device [udev rules](/index.php/Udev_rules "Udev rules") for MTP devices, making it easier to use [ADB](/index.php/ADB "ADB") or MTP.
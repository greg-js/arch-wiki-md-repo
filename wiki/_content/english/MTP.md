[MTP](https://en.wikipedia.org/wiki/Media_Transfer_Protocol "wikipedia:Media Transfer Protocol"), or the *Media Transfer Protocol*, is a USB device class which is used by many mobile phones (all Windows Phone 7/8/10 devices, most newer Android devices) and media players (e.g. Creative Zen).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Functionality](#Functionality)
    *   [1.2 Integration with file managers](#Integration_with_file_managers)
*   [2 Usage](#Usage)
    *   [2.1 libmtp](#libmtp)
    *   [2.2 simple-mtpfs](#simple-mtpfs)
    *   [2.3 jmtpfs](#jmtpfs)
    *   [2.4 go-mtpfs](#go-mtpfs)
    *   [2.5 mtpfs](#mtpfs)
    *   [2.6 Android File Transfer](#Android_File_Transfer)
    *   [2.7 Media players](#Media_players)
    *   [2.8 gvfs-mtp](#gvfs-mtp)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 libmtp](#libmtp_2)
        *   [3.1.1 Unable to enumerate USB device](#Unable_to_enumerate_USB_device)
    *   [3.2 jmtpfs](#jmtpfs_2)
        *   [3.2.1 Input/output error upon first access](#Input.2Foutput_error_upon_first_access)
    *   [3.3 kio-mtp](#kio-mtp)

## Installation

### Functionality

Linux MTP support is provided by [installing](/index.php/Installing "Installing") the [libmtp](https://www.archlinux.org/packages/?name=libmtp) package. It can be installed on its own and used to access devices. However, a number of packages are available that use it as a dependency and add additional convenience (e.g. filemanager) functionalities and compatibility with particular device types - which includes improving transfer access speeds.

These packages to choose from all implement a [Wikipedia:Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace"):

*   [mtpfs](https://www.archlinux.org/packages/?name=mtpfs)
*   [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) - is reported to work well for newer Android 4+ devices
*   [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) - is reported to work well for newer Android 3+ devices
*   [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/)
*   [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer) - MTP client with minimalistic UI

All of them aim at better functionality and performance over `libmtp`. Since there are a lot of different USB devices, you might want to research first which one looks most suitable for yours.

**Warning:** `libmtp` does not handle newer Android devices well - hanging transfers and problems with remote file system browsing are very common, poor performance is expected with most devices. Furthermore, if you have a damaged USB cable, programs utilizing libmtp may crash or hang indefinitely until you disconnect the device. It is recommended to connect your device with the USB Mass Storage (if available), or using [ADB](/index.php/ADB "ADB") (for example [adbfs-rootless-git](https://aur.archlinux.org/packages/adbfs-rootless-git/)) to transfer files, which performs better on most devices and supports additional Android-specific features (like installing APKs, managing packages on the device, backing up data or accessing the device's shell).

**Tip:** It is recommended to reboot your computer after installing MTP related packages.

### Integration with file managers

To view the contents of your Android device's storage via MTP in your file manager, install the corresponding plugin:

*   For file managers that use [GVFS](/index.php/GVFS "GVFS") (GNOME Files), install [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) for MTP or [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) for PTP support.
*   For file managers that use KIO (KDE's Dolphin), MTP support is included in [kio-extras](https://www.archlinux.org/packages/?name=kio-extras) (dependency of dolphin).

After installing the required package, the device should show up in the file manager automatically and be accessible via an URL, for example `mtp://[usb:002,013]/`.

## Usage

It might be required to create a mount-point directory first. The directory `~/mnt` is used as an example below. Also do not forget to unlock your phone's screen before connecting it to the computer.

### libmtp

Detect your device:

```
# mtp-detect

```

If an error is returned, see [troubleshooting libmtp](#libmtp_2).

**Note:** Your regular user must be in the `uucp` [group](/index.php/Users_and_groups#Example_adding_a_user "Users and groups").

Connect to your device:

```
# mtp-connect

```

If connection is successful, there are several switch options to use in conjunction with *mtp-connect* to access data on the device. You might want to use some stand alone commands:

```
 mtp-albumart        mtp-emptyfolders    mtp-getplaylist     mtp-reset           mtp-trexist
 mtp-albums          mtp-files           mtp-hotplug         mtp-sendfile
 mtp-connect         mtp-folders         mtp-newfolder       mtp-sendtr
 mtp-delfile         mtp-format          mtp-newplaylist     mtp-thumb
 mtp-detect          mtp-getfile         mtp-playlists       mtp-tracks

```

### simple-mtpfs

List MTP devices:

```
$ simple-mtpfs -l

```

Your list of device(s) may look like this:

```
1: AsusZenfone 2 (MTP)

```

To mount the device with index 1 in the list to `~/mnt`:

```
$ simple-mtpfs --device 1 ~/mnt

```

Unmount device mounted on `~/mnt`:

```
$ fusermount -u ~/mnt

```

### jmtpfs

Mount device on `~/mnt`:

```
$ jmtpfs ~/mnt

```

Unmount device mounted on `~/mnt`:

```
$ fusermount -u ~/mnt

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

### go-mtpfs

**Note:** Mounting with `go-mtpfs` might fail if an external SD Card is present. If you try to access your device while having an SD card and go-mtpfs complains, try removing the SD card and mounting again.

Install [android-udev](https://www.archlinux.org/packages/?name=android-udev), which will allow you to edit `/etc/udev/rules.d/51-android.rules` and apply to your `idVendor` and `idProduct`, which you can see after running *mtp-detect*. To the end of the line, add your user `OWNER="<user>"`.

Mount device on `~/mnt`:

```
$ go-mtpfs ~/mnt

```

Unmount device mounted on `~/mnt`:

```
$ fusermount -u ~/mnt

```

### mtpfs

**Note:** The following is likely to not work and you might have to resort to [gphoto2](/index.php/Digital_Cameras#libgphoto2 "Digital Cameras") or a file manager with gvfs support like [PCManFM](/index.php/PCManFM "PCManFM").

First edit your `/etc/fuse.conf` and uncomment the following line:

```
user_allow_other

```

Mount your device on `~/mnt`:

```
$ mtpfs -o allow_other ~/mnt

```

Unmount device mounted on `~/mnt`:

```
$ fusermount -u ~/mnt

```

### Android File Transfer

	FUSE interface

Mount your device on `~/my-device`:

```
$ mkdir ~/my-device
$ aft-mtp-mount ~/my-device

```

If you want album art to be displayed, it must be named `albumart.xxx` and placed first in the destination folder. Then copy other files. Also, note that fuse could be 7-8 times slower than ui/cli file transfer.

Unmount device mounted on `~/my-device`:

```
$ fusermount -u ~/my-device

```

	Qt user interface

Start the application, choose a destination folder and click any button on the toolbar. Available options are: *Upload Album*, *Upload Directory* and *Upload Files*. The latter two are self-explanatory. *Upload album* searches the source directory for album covers, and sets the best available cover.

### Media players

You can also use your MTP device in music players such as Amarok. To achieve this, you might have to edit `/etc/udev/rules.d/51-android.rules` (the MTP device used in the following example is a Galaxy Nexus). Run:

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

If your device isn't showing up in the file manager then the [libmtp](https://www.archlinux.org/packages/?name=libmtp) is missing a native support and is not currently available in the list of the [supported devices](https://sourceforge.net/p/libmtp/code/ci/HEAD/tree/src/music-players.h). If you will try to mount by using command line you may also get an error

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

The file managers with support for [gvfs](/index.php/Gvfs "Gvfs") will be able to show MTP devices and mount them if supported by [libmtp](https://www.archlinux.org/packages/?name=libmtp) but if has no support and cannot be opened then change settings in the phone to PTP and install [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) for having access at least to the photos, command line mounting of PTP is a little similar to mounting of the MTP devices: `gvfs-mount gphoto2://[usb:002,019]/`.

**Note:** If you getting limited access to the device and cannot use standard commands from command line such as e.g. `cp`,`ls` then look for [gvfs](/index.php/Gvfs "Gvfs") own alternatives, `ls -1 /usr/bin/gvfs-*`.

## Troubleshooting

### libmtp

#### Unable to enumerate USB device

If you see a message like this in system log (`journalctl`)

```
 usb usb4-port2: unable to enumerate USB device

```

You can try following temporary [workaround](https://bbs.archlinux.org/viewtopic.php?pid=1087323#p1087323)

```
 # modprobe -vr uhci_hcd
 # modprobe -va ohci_hcd
 # modprobe -va uhci_hcd

```

If it works you should create `/etc/modprobe.d/usb_hci_order.conf` with following content

```
 # create a dependency on ohci for uhci, which fixes problems
 # with external usb devices not showing up
 #
 softdep uhci_hcd pre: ohci_hcd

```

### jmtpfs

#### Input/output error upon first access

Symptoms: jmtpfs successfully mounts, but as soon as one attempts to access files on the device (e.g. via `ls`), an error is reported:

```
 cannot access <mount-point>: Input/output error

```

This appears to be a security feature: MTP does not work when the phone is locked by the lockscreen. Unlock the phone and it should work again as long as the cord remains connected.

### kio-mtp

If you are not able to use the action "Open with File Manager", you may work around this problem by editing the file `/usr/share/apps/solid/actions/solid_mtp.desktop`.

Change the line

```
Exec=kioclient exec mtp:udi=%i/

```

To

```
Exec=dolphin "mtp:/"

```
[MTP](https://en.wikipedia.org/wiki/MTP "wikipedia:MTP"), or the *Media Transfer Protocol*, is a USB device class which is used by many mobile phones (e.g. Android 3+ devices) and media players (e.g. Creative Zen).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Using media players](#Using_media_players)
*   [4 mtpfs](#mtpfs)
*   [5 jmtpfs](#jmtpfs)
*   [6 go-mtpfs](#go-mtpfs)
*   [7 simple-mtpfs](#simple-mtpfs)
*   [8 gvfs-mtp troubleshooting](#gvfs-mtp_troubleshooting)
*   [9 kio-mtp troubleshooting](#kio-mtp_troubleshooting)

## Установка

Поддержка MTP осуществляется с помощью [libmtp](http://libmtp.sourceforge.net/), для этого [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [libmtp](https://www.archlinux.org/packages/?name=libmtp) из [официальные репозитории](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории").

**Совет:** После установки рекомендуется перезагрузить компьютер.

Чтобы просматривать содержимое накопителя вашего Android устройства через MTP в файловом менеджере, установите соответствующий плагин:

*   Для файловых менеджеров, которые используют [GVFS](/index.php/GVFS "GVFS") ([GNOME Files](/index.php/GNOME_Files "GNOME Files"), Xfce's [Thunar](/index.php/Thunar "Thunar")), установите [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) для поддержки MTP и [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) для поддержки PTP.
*   Для файловых менеджеров, которые используют KIO (KDE's Dolphin), установите [kio-mtp](https://www.archlinux.org/packages/?name=kio-mtp) (поддержка PTP уже включена в него).

Также существует альтернатива плагинам: минималистичный MTP клиент [android-file-transfer](https://www.archlinux.org/packages/?name=android-file-transfer).

После установки необходимых пакетов, ваше устройство должно отобразиться в файловом менеджере автоматически, и вы сможете получать доступ к файлам по URL наподобие такого: `mtp://[usb:002,013]/`.

**Примечание:** Если у вас более новое Android устройство, которое не поддерживает UMS (USB-накопитель) и вы считаете что [mtpfs](https://www.archlinux.org/packages/?name=mtpfs) очень медленный или работает некорректно, то вы можете установить [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) из AUR.

## Использование

**Примечание:** Не забудьте разблокировать ваш телефон (лок-скрин) перед подключением, потому что иначе вы увидите сообщения об ошибке.

After installation, you have several MTP tools available. Upon connecting your MTP device, you use:

```
# mtp-detect

```

to see if your MTP device is detected. If you get errors about permission, remember that you need to be in the uucp group to access the USB system in general.

To connect to your MTP device, you use:

```
# mtp-connect

```

If connection is successful, there are several switch options to use in conjunction with `mtp-connect` to access data on the device.

There are also several stand alone commands you can use to access your MTP device such as,

**Warning:** Some commands may be harmful to your MTP device!!!

```
 mtp-albumart        mtp-emptyfolders    mtp-getplaylist     mtp-reset           mtp-trexist
 mtp-albums          mtp-files           mtp-hotplug         mtp-sendfile
 mtp-connect         mtp-folders         mtp-newfolder       mtp-sendtr
 mtp-delfile         mtp-format          mtp-newplaylist     mtp-thumb
 mtp-detect          mtp-getfile         mtp-playlists       mtp-tracks

```

If you see a message like:

```
Device 0 (VID=XXXX and PID=XXXX) is UNKNOWN.
Please report this VID/PID and the device model to the libmtp development team

```

You should check whether your device has been already in this list: [Supported devices list[[1]](http://sourceforge.net/p/libmtp/code/ci/HEAD/tree/src/music-players.h)] If it is not, you should report it to the development team. If it already is, your libmtp might be slightly outdated. To allow it to be properly used by libmtp, you can add your device to:

```
/usr/lib/udev/rules.d/69-libmtp.rules

```

## Using media players

You can also use your MTP device in music players such as Amarok. To do this you may have to edit `/usr/lib/udev/rules.d/51-android.rules` (the MTP device used in the following example is a Galaxy Nexus): To do this run:

```
$ lsusb

```

and look for your device, it will be something like:

```
Bus 003 Device 011: ID 04e8:6860 Samsung Electronics Co., Ltd GT-I9100 Phone [Galaxy S II], GT-P7500 [Galaxy Tab 10.1]

```

in which case the entry would be:

```
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", ATTR{idProduct}=="6860", MODE="0666", OWNER="[username]"

```

Then, reload udev rules:

```
# udevadm control --reload

```

**Note:** After installing MTP you may have to reboot for your device to be recognised

## mtpfs

**Warning:** The following is likely to not work and you might have to resort to [gphoto2](/index.php/Digital_Cameras#libgphoto2 "Digital Cameras") or a file manager with gvfs support like [PCManFM](/index.php/PCManFM "PCManFM").

Mtpfs is FUSE filesystem that supports reading and writing from any MTP device. Basically it allows you to mount your device as an external drive.

Mtpfs can be installed with the packge [mtpfs](https://www.archlinux.org/packages/?name=mtpfs), available from the [official repositories](/index.php/Official_repositories "Official repositories").

*   First edit your `/etc/fuse.conf` and uncomment the following line:

```
user_allow_other

```

*   To mount your device

```
$ mtpfs -o allow_other /media/YOURMOUNTPOINT

```

*   To unmount your device

```
$ fusermount -u /media/YOURMOUNTPOINT

```

*   To unmount your device as root

```
# umount /media/YOURMOUNTPOINT

```

Also, you can put them into your ~/.bashrc:

```
alias android-connect="mtpfs -o allow_other /media/YOURMOUNTPOINT"
alias android-disconnect="fusermount -u /media/YOURMOUNTPOINT"

```

Or, with sudo

```
alias android-disconnect="sudo umount -u /media/YOURMOUNTPOINT"

```

**Note:** if you want not be asked for password when using sudo, please refer to [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

## jmtpfs

[jmtpfs](http://research.jacquette.com/jmtpfs-exchanging-files-between-android-devices-and-linux/) is a FUSE and libmtp based filesystem for accessing MTP (Media Transfer Protocol) devices. It was specifically designed for exchanging files between Linux systems and newer Android devices that support MTP but not USB Mass Storage. jmtpfs is available as [jmtpfs](https://aur.archlinux.org/packages/jmtpfs/) in the [AUR](/index.php/AUR "AUR").

Use this commands to mount your device:

```
$ jmtpfs ~/mtp

```

And this command to unmount it:

```
$ fusermount -u ~/mtp

```

## go-mtpfs

**Note:** Go-mtpfs gives a better performance while writing files to some devices than mtpfs/jmtpfs. Try it if you have slow speeds.

**Note:** Mounting with Go-mtpfs fails if external SD Card is present. If you have also external SD Card please remove it and then try mounting again.

If the above instructions do not show any positive results one should try [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) from the [AUR](/index.php/AUR "AUR"). The following has been tested on a Samsung Galaxy Nexus GSM, Asus/Google Nexus 7 (2012 1st gen model), Samsung Galaxy S 3 mini and Google Nexus 4\. (This is the only mtp software which worked for me on Nexus 4\. Settings are usb debugging enabled, connected as media device.)

If you want do it simpler, install [go](https://www.archlinux.org/packages/?name=go), [libmtp](https://www.archlinux.org/packages/?name=libmtp) and [git](https://www.archlinux.org/packages/?name=git) from the [official repositories](/index.php/Official_repositories "Official repositories"). After that install [go-mtpfs-git](https://aur.archlinux.org/packages/go-mtpfs-git/) from the [AUR](/index.php/AUR "AUR").

As in the section above install [android-udev](https://www.archlinux.org/packages/?name=android-udev) which will provide you with "/usr/lib/udev/rules.d/51-android.rules" edit it to apply to your idVendor and idProduct, which you can see after running mtp-detect. To the end of the line add with a comma OWNER="yourusername". Save the file.

*   Add yourself to the "fuse" group:

```
gpasswd -a [user] fuse

```

*   If the group "fuse" does not exist create it with:

```
groupadd fuse

```

Logout or reboot to apply these changes.

*   To create a mount point called "Android" issue the following commands:

```
mkdir Android

```

*   To mount your phone use:

```
go-mtpfs Android

```

*   To unmount your phone:

```
fusermount -u Android

```

You can create a .bashrc alias as in the example above for easier use.

## simple-mtpfs

This is another FUSE filesystem for MTP devices. You may find this to be more reliable than [mtpfs](https://www.archlinux.org/packages/?name=mtpfs). [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/) is available in the AUR or can be built from source. Do not run the following commands as root.

To list MTP devices run

```
$ simple-mtpfs --list-devices

```

To mount a MTP devices (in this example device 0) run

```
$ simple-mtpfs /path/to/your/mount/point

```

To un mount run

```
$ fusermount -u /path/to/your/mount/point

```

## gvfs-mtp troubleshooting

If you have installed the [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) package, and your device doesn't show up in the file manager, you might need to write a udev rule in order to auto-mount the device.

Plug your device and get the vendor-id and product-id,respectively:

```
$ lsusb
Bus 001 Device 007: ID 0421:0661 Nokia Mobile Phones Lumia 920
(...)

```

The two numbers after ID are *vendorId* : *productID*

Then make a udev rule, e.g.

```
# nano /usr/lib/udev/rules.d/51-android.rules

```

and type this rule:

```
ATTR{idVendor}=="YOUR VENDOR ID HERE", ATTR{idProduct}=="YOUR PRODUCT ID HERE", SYMLINK+="libmtp",  MODE="660", ENV{ID_MTP_DEVICE}="1"

```

Reload the udev rules.

```
# udevadm control --reload

```

And reboot the system. Now file managers (like Thunar) should be able to automount the MTP Device. [[2]](https://bbs.archlinux.org/viewtopic.php?id=180719)

## kio-mtp troubleshooting

If you are not able to use the action "Open with File Manager", you may work around this problem by editing the file /usr/share/apps/solid/actions/solid_mtp.desktop

Change the line

```
Exec=kioclient exec mtp:udi=%i/

```

To

```
Exec=dolphin "mtp:/"

```
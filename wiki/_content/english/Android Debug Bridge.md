The [Android Debug Bridge](https://developer.android.com/studio/command-line/adb) (ADB) is a command-line tool that can be used to install, uninstall and debug apps, transfer files and access the device's shell.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Connect device](#Connect_device)
    *   [2.2 Figure out device IDs](#Figure_out_device_IDs)
    *   [2.3 Adding udev Rules](#Adding_udev_Rules)
    *   [2.4 Configuring adb](#Configuring_adb)
    *   [2.5 Detect the device](#Detect_the_device)
    *   [2.6 Transferring files](#Transferring_files)
*   [3 Tools building on ADB](#Tools_building_on_ADB)
*   [4 Troubleshooting](#Troubleshooting)

## Installation

ADB is part of the Platform-Tools [SDK package](/index.php/Android#SDK_packages "Android") and the [android-tools](https://www.archlinux.org/packages/?name=android-tools) package.

## Usage

### Connect device

**Tip:**

*   For some devices, you may have to enable MTP on the device, before ADB will work. Some other devices require enable PTP mode to work.
*   Many devices' [udev](/index.php/Udev "Udev") rules are included in [libmtp](https://www.archlinux.org/packages/?name=libmtp), so if you have this installed, the following steps may not be necessary.
*   Make sure your USB cable is capable of both charge and data. Many USB cables bundled with mobile devices do not include the USB data pin.

To connect to a real device or phone via ADB under Arch, you must:

1.  You might want to install [android-udev](https://www.archlinux.org/packages/?name=android-udev) if you wish to connect the device to the proper `/dev/` entries.
2.  plug in your android device via USB.
3.  Enable USB Debugging on your phone or device:
    *   Jelly Bean (4.2) and newer: Go to *Settings > About Phone* tap *Build Number* 7 times until you get a popup that you have become a developer. Then go to *Settings > Developer > USB debugging* and enable it. The device will ask to allow the computer with its fingerprint to connect. allowing it permanent will copy `$HOME/.android/adbkey.pub` onto the devices `/data/misc/adb/adb_keys` folder.
    *   Older versions: This is usually done from *Settings > Applications > Development > USB debugging*. Reboot the phone after checking this option to make sure USB debugging is enabled.

If [ADB recognizes your device](#Detect_the_device) (`adb devices` shows it as `"device" and not as "unauthorized"`, or it is visible and accessible in IDE), you are done. Otherwise see instructions below.

### Figure out device IDs

Each Android device has a USB vendor/product ID. An example for HTC Evo is:

```
vendor id: 0bb4
product id: 0c8d

```

Plug in your device and execute:

```
$ lsusb

```

It should come up something like this:

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

### Adding udev Rules

Use the rules from [android-udev](https://www.archlinux.org/packages/?name=android-udev) (or [android-udev-git](https://aur.archlinux.org/packages/android-udev-git/)), install them manually from [Android developer](https://source.android.com/source/initializing#configuring-usb-access), or use the following template for your [udev rules](/index.php/Udev_rules "Udev rules"), just replace `[VENDOR ID]` and `[PRODUCT ID]` with yours. Copy these rules into `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0660", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"

```

Then, to reload your new udev rules, execute:

```
# udevadm control --reload-rules

```

Make sure you are member of `adbusers` [group](/index.php/Group "Group") to access `adb` devices.

### Configuring adb

Instead of using udev rules, you may create/edit `~/.android/adb_usb.ini` which contains a list of vendor IDs.

 `~/.android/adb_usb.ini` 
```
0x27e8

```

### Detect the device

After you have setup the udev rules, unplug your device and replug it.

After running:

```
$ adb devices

```

you should see something like:

```
List of devices attached 
HT07VHL00676    device

```

### Transferring files

You can now use adb to transfer files between the device and your computer. To transfer files to the device, use

```
$ adb push *<what-to-copy>* *<where-to-place>*

```

To transfer files from the device, use

```
$ adb pull *<what-to-pull>* *<where-to-place>*

```

Also see [#Tools building on ADB](#Tools_building_on_ADB).

## Tools building on ADB

*   [adbfs-rootless-git](https://aur.archlinux.org/packages/adbfs-rootless-git/) - a [FUSE](/index.php/FUSE "FUSE") filesystem over ADB
*   [adb-sync](https://github.com/google/adb-sync) (available as [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/)) – a tool to synchronize files between a PC and an Android device using the ADB protocol.
*   [AndroidScreencast](http://xsavikx.github.io/AndroidScreencast) (available as [androidscreencast-bin](https://aur.archlinux.org/packages/androidscreencast-bin/)) – view and control your Android device from a PC (via ADB).

## Troubleshooting

*   If you are getting an empty list (your device is not there), it may be because you have not enabled USB debugging on your device. You can do that by going to *Settings > Applications > Development* and enabling USB debugging. On Android 4.2 (Jelly Bean) the Development menu is hidden; to enable it go to *Settings > About phone* and tap Build number 7 times.

*   On Moto E, the device could have a different vendor/product ID in the sideload and fastboot modes; if you get the "no permission" error, verify the device's ID with `lsusb`.
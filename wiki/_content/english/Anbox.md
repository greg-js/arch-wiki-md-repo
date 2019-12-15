Anbox is a free and open-source compatibility layer that aims to allow mobile applications and mobile games developed for Android to run on GNU/Linux distributions. It executes the Android runtime environment by using LXC (Linux Containers), recreating the directory structure of Android as a mountable loop image, whilst using the native Linux kernel to execute applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Note](#Note)
*   [2 Network](#Network)
*   [3 Usage](#Usage)
    *   [3.1 Installing apps through adb](#Installing_apps_through_adb)
    *   [3.2 Installing apps through apps stores](#Installing_apps_through_apps_stores)

## Installation

Make sure you have had the header files for your kernel installed (e.g. [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) for Linux kernel).

[Install](/index.php/Install "Install") [anbox-git](https://aur.archlinux.org/packages/anbox-git/), [anbox-image](https://aur.archlinux.org/packages/anbox-image/) (or [anbox-image-gapps](https://aur.archlinux.org/packages/anbox-image-gapps/) if you want to include Google's Apps and houdini), [anbox-modules-dkms-git](https://aur.archlinux.org/packages/anbox-modules-dkms-git/) and [anbox-bridge](https://aur.archlinux.org/packages/anbox-bridge/)

[Start/enable](/index.php/Start/enable "Start/enable") the following services:

*   `anbox-container-manager.service`

If you don't want to reboot your computer to enable the required DKMS modules, you can load them manually:

```
$ sudo modprobe ashmem_linux
$ sudo modprobe binder_linux

```

### Note

There has been cases of conflicting packages while Installing [anbox-git](https://aur.archlinux.org/packages/anbox-git/).

So make sure you install the Android Image ([anbox-image-gapps](https://aur.archlinux.org/packages/anbox-image-gapps/) or [anbox-image](https://aur.archlinux.org/packages/anbox-image/)) first and then proceed to install the other Anbox packages.

See [this](https://bbs.archlinux.org/viewtopic.php?id=249747/) link if you run into a common `logger.cpp` error.

## Network

You must execute `anbox-bridge` every time before starting `anbox-container-manager.service` in order to get network working in anbox.

The easiest solution is create a drop-in file `enable-anbox-bridge.conf`.

 `/etc/systemd/system/anbox-container-manager.service.d/enable-anbox-bridge.conf` 
```
[Service]
ExecStartPre=/usr/bin/anbox-bridge
```

## Usage

You can run the Android applications on your desktop's launcher on **Other** category.

If you want to use adb to debug, install [android-tools](https://www.archlinux.org/packages/?name=android-tools)

```
$ adb shell

```

### Installing apps through adb

By default, Anbox doesn't support for ARM applications. So apps must have a x86_64 architecture.

To install `*/path/to/app.apk*`

```
$ adb install */path/to/app.apk*

```

To get the list of installed applications

```
$ adb shell pm list packages

```

Note that output will be similar to `*package:app.name*`, where `*app.name*` is different from the one displayed in anbox container.

To uninstall `*app.name*`

```
$ adb uninstall *app.name*

```

If `*app.name*` is a system app

```
$ adb uninstall --user 0 *app.name*

```

### Installing apps through apps stores

Apps can be easily installed throught apps stores. In [anbox-image-gapps](https://aur.archlinux.org/packages/anbox-image-gapps/) PlayStore is included.
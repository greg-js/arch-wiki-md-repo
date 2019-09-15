Anbox is a free and open-source compatibility layer that aims to allow mobile applications and mobile games developed for Android to run on GNU/Linux distributions. It executes the Android runtime environment by using LXC (Linux Containers), recreating the directory structure of Android as a mountable loop image, whilst using the native Linux kernel to execute applications.

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

## Usage

You must execute `anbox-bridge` every time before starting `anbox` in order to get network working in anbox.

Now, you can run the android applications on your desktop's launcher on **Other** category.

If you want to use adb to debug, install [android-tools](https://www.archlinux.org/packages/?name=android-tools)

```
$ adb shell

```
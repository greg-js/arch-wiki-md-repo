Anbox is a free and open-source compatibility layer that aims to allow mobile applications and mobile games developed for Android to run on GNU/Linux distributions. It executes the Android runtime environment by using LXC (Linux Containers), recreating the directory structure of Android as a mountable loop image, whilst using the native Linux kernel to execute applications.

## Installation

[Install](/index.php/Install "Install") [anbox-git](https://aur.archlinux.org/packages/anbox-git/), [anbox-image-gapps](https://aur.archlinux.org/packages/anbox-image-gapps/), [anbox-modules-dkms-git](https://aur.archlinux.org/packages/anbox-modules-dkms-git/) and [anbox-bridge](https://aur.archlinux.org/packages/anbox-bridge/).

[Start/enable](/index.php/Start/enable "Start/enable") the following services:

*   `systemd-resolved.service` for internet to work in apps
*   `systemd-networkd.service` for internet to work in apps
*   `anbox-container-manager.service`

[Edit](/index.php/Edit "Edit") config file for anbox-session-manger:

 `/etc/systemd/user/anbox-session-manager.service.d/host_driver.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/anbox session-manager --gles-driver=host
```

login in **normal** user to launch user service and enable network bridge:

```
$ systemctl --user start anbox-session-manager.service
$ anbox-bridge

```

Now, you can run the android applications on your desktop's launcher on **Other** category.

If you want to use adb to debug, install [android-tools](https://www.archlinux.org/packages/?name=android-tools)

```
$ adb shell

```
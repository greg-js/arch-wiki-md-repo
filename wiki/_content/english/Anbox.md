Anbox is a free and open-source compatibility layer that aims to allow mobile applications and mobile games developed for Android to run on GNU/Linux distributions. It executes the Android runtime environment by using LXC (Linux Containers), recreating the directory structure of Android as a mountable loop image, whilst using the native Linux kernel to execute applications.

## Installation

[Install](/index.php/Install "Install") [anbox-git](https://aur.archlinux.org/packages/anbox-git/), [anbox-image](https://aur.archlinux.org/packages/anbox-image/), [anbox-modules-dkms-git](https://aur.archlinux.org/packages/anbox-modules-dkms-git/) and [anbox-bridge](https://aur.archlinux.org/packages/anbox-bridge/).

[Start/enable](/index.php/Start/enable "Start/enable") `systemd-resolved.service` and `systemd-networkd.service` for internet to work in apps.

Start `anbox-container-manager.service`.

[Edit](/index.php/Edit "Edit") `anbox-session-manager.service` to add the host driver:

 `/etc/systemd/user/anbox-session-manager.service.d/host_driver.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/anbox session-manager --gles-driver=host
```

Finally start the user service:

```
$ systemctl --user start anbox-session-manager.service

```
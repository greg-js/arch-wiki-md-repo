Related articles

*   [Offline installation of packages](/index.php/Offline_installation_of_packages "Offline installation of packages")
*   [Archiso offline](/index.php/Archiso_offline "Archiso offline")

If you wish to install the [Archiso](/index.php/Archiso "Archiso") (e.g. [the official monthly release](https://www.archlinux.org/download/)) as it is without an Internet connection, or, if you do not want to download the packages you want again:

First, follow the [Installation guide](/index.php/Installation_guide "Installation guide"), skipping the [Installation guide#Connect to the Internet](/index.php/Installation_guide#Connect_to_the_Internet "Installation guide") section, until the [Installation guide#Install the base packages](/index.php/Installation_guide#Install_the_base_packages "Installation guide") step.

## Contents

*   [1 Install the archiso to the new root](#Install_the_archiso_to_the_new_root)
*   [2 Chroot and configure the base system](#Chroot_and_configure_the_base_system)
    *   [2.1 Restore the configuration of journald](#Restore_the_configuration_of_journald)
    *   [2.2 Remove special udev rule](#Remove_special_udev_rule)
    *   [2.3 Disable and remove the services created by archiso](#Disable_and_remove_the_services_created_by_archiso)
    *   [2.4 Remove special scripts of the Live environment](#Remove_special_scripts_of_the_Live_environment)
    *   [2.5 Importing archlinux keys](#Importing_archlinux_keys)
    *   [2.6 Configure the system](#Configure_the_system)
    *   [2.7 Enable graphical login (optional)](#Enable_graphical_login_(optional))

## Install the archiso to the new root

Instead of installing the packages with `pacstrap` (which would try to download from the remote repositories), copy *everything* in the live environment to the new root:

```
# cp -ax / /mnt

```

**Note:** The option (`-x`) excludes some special directories, as they should not be copied to the new root.

Then, copy the kernel image to the new root, in order to keep the integrity of the new system:

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

After that, generate a fstab as described in [Installation guide#Fstab](/index.php/Installation_guide#Fstab "Installation guide").

## Chroot and configure the base system

Next, chroot into your newly installed system:

```
# arch-chroot /mnt /bin/bash

```

**Note:** Before performing the other [Installation guide#Configure the system](/index.php/Installation_guide#Configure_the_system "Installation guide") steps (e.g. locale, keymap, etc.), it is necessary to get rid of the trace of the Live environment (in other words, the customization of archiso which does not fit a non-Live environment).

### Restore the configuration of journald

[This customization of archiso](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19) will lead to storing the system journal in RAM, it means that the journal will not be available after reboot:

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

### Remove special udev rule

[This rule of udev](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) starts the dhcpcd automatically if there are any wired network interfaces.

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

### Disable and remove the services created by archiso

Some service files are created for the Live environment, please disable the services and remove the file as they are unnecessary for the new system:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

### Remove special scripts of the Live environment

There are some scripts installed in the live system by archiso scripts, which are unnecessary for the new system:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

### Importing archlinux keys

In order to use the official repositories, we need to import the archlinux master keys ([pacman/Package signing#Initializing the keyring](/index.php/Pacman/Package_signing#Initializing_the_keyring "Pacman/Package signing")). This step is usually done by pacstrap but can be achieved with

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Note:** Keyboard or mouse activity is needed to generate entropy and speed-up the first step.

### Configure the system

Now you can follow the skipped steps of the [Installation guide#Configure the system](/index.php/Installation_guide#Configure_the_system "Installation guide") section (setting a locale, timezone, hostname, etc.) and finish the installation by creating an initial ramdisk as described in [Installation guide#Initramfs](/index.php/Installation_guide#Initramfs "Installation guide").

### Enable graphical login (optional)

If using a display manager like GDM, you may want to change the systemd default target from multi-user.target to one that allows graphical login.

```
# systemctl disable multi-user.target
# systemctl enable graphical.target

```
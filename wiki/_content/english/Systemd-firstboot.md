Starting with version 216 of [systemd](/index.php/Systemd "Systemd"), the command *systemd-firstboot* allows for setting of basic system settings before or during the first boot of a newly created system. The tool is able of initialize the following system settings: [timezone](/index.php/Timezone "Timezone"), [locale](/index.php/Locale "Locale"), [hostname](/index.php/Hostname "Hostname"), the root password, as well as automated generation of a machine ID.

As *systemd-firstboot* interacts with the filesystem directly and doesn't make use of the related systemd services (such as timedatectl, hostnamectl or localectl), it should not be executed on an already running system.

Settings can be specified non-interactively when externally used on filesystem images, or interactively if executed during the early boot process.

A default Arch Linux installation will set most variables *systemd-firstboot* is able to manipulate, or facilitate the creation of skeleton files which prevent its use when installing the systemd package through pacstrap.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage Example](#Usage_Example)
    *   [2.1 Interactively configure system settings during boot of a fresh Arch Linux installation](#Interactively_configure_system_settings_during_boot_of_a_fresh_Arch_Linux_installation)
        *   [2.1.1 Delete existing settings](#Delete_existing_settings)
        *   [2.1.2 Modify and enable systemd-firstboot.service](#Modify_and_enable_systemd-firstboot.service)
        *   [2.1.3 Finalize installation](#Finalize_installation)
*   [3 See also](#See_also)

## Installation

*systemd-firstboot* is part of and packaged with [systemd](https://www.archlinux.org/packages/?name=systemd).

## Usage Example

**Warning:** Doing this on an existing Arch Linux instance may break your system. The following steps should only be used on new installations.

### Interactively configure system settings during boot of a fresh Arch Linux installation

Allowing *systemd-firstboot* to manipulate a previously un-booted Arch Linux installation is particularly useful in situations where installation is undertaken by an individual other than the eventual end user, such as in the distribution of laptops with a pre-loaded install.

The following steps should be appended to the end of the [Configure the system section](/index.php/Installation_guide#Configure_the_system "Installation guide") of the [Installation guide](/index.php/Installation_guide "Installation guide"), before the target partitions are unmounted, thus taking place within the chroot of the new installation. Make sure all locales you want available have been generated, non-generated ones will not be offered as a possible setting.

#### Delete existing settings

If the following files are present, *systemd-firstboot* will not prompt for the setting they relate to.

```
# rm /etc/{machine-id,localtime,hostname,shadow,locale.conf}

```

#### Modify and enable systemd-firstboot.service

Changes from the packaged service file are indicated in bold. Use of `--prompt` makes *systemd-firstboot* query for all possible settings. The `[Install]` section is needed to specify where in the boot process the service is to be activated.

 `/usr/lib/systemd/system/systemd-firstboot.service` 
```
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

[Unit]
Description=First Boot Wizard
Documentation=man:systemd-firstboot(1)
DefaultDependencies=no
Conflicts=shutdown.target
After=systemd-remount-fs.service
Before=systemd-sysusers.service sysinit.target shutdown.target
ConditionPathIsReadWrite=/etc
ConditionFirstBoot=yes

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/systemd-firstboot **--prompt**
StandardOutput=tty
StandardInput=tty
StandardError=tty

**[Install]**
**WantedBy=sysinit.target**

```

```
# systemctl enable systemd-firstboot.service

```

#### Finalize installation

Continue installing as per the [Installation guide](/index.php/Installation_guide "Installation guide"). Unless more configuration is to be undertaken, exit the chroot, unmount the partitions and shut down. Upon the next boot, *systemd-firstboot* will execute. Presuming **no other changes to system configuration are made**, removing the files above and rebooting will trigger systemd-firstboot again, in case you wish to test whether the installation worked.

## See also

*   [systemd-firstboot man page](https://www.freedesktop.org/software/systemd/man/systemd-firstboot.html)
This document is a guide for installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") from the live system booted with the official installation image. Before installing, it would be advised to view the [FAQ](/index.php/FAQ "FAQ"). If looking for a more detailed installation guide see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide"), or [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for specific installation cases.

Most help can be found on the wiki or through the various programs' [man pages](/index.php/Man_page "Man page"); see [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) for an overview of the configuration. For interactive help, the [IRC channel](/index.php/IRC_channel "IRC channel") and the [forums](https://bbs.archlinux.org/) are also available.

## Contents

*   [1 Pre-installation](#Pre-installation)
    *   [1.1 Verify the boot mode](#Verify_the_boot_mode)
    *   [1.2 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [1.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [1.4 Update the system clock](#Update_the_system_clock)
    *   [1.5 Partition the disks](#Partition_the_disks)
    *   [1.6 Format the partitions](#Format_the_partitions)
    *   [1.7 Mount the partitions](#Mount_the_partitions)
*   [2 Installation](#Installation)
    *   [2.1 Select the mirrors](#Select_the_mirrors)
    *   [2.2 Install the base packages](#Install_the_base_packages)
*   [3 Configure the system](#Configure_the_system)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Locale](#Locale)
    *   [3.5 Network configuration](#Network_configuration)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root password](#Root_password)
    *   [3.8 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## Pre-installation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

Download and boot the installation medium as explained in [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). You will be logged in as the root user, and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt. To [edit](/index.php/Edit "Edit") configuration files, [nano](/index.php/Nano#Usage "Nano"), *vi* and [vim](/index.php/Vim#Usage "Vim") are available.

The installation process needs to retrieve packages from a remote repository, therefore a working internet connection is required.

### Verify the boot mode

As instructions differ for [UEFI](/index.php/UEFI "UEFI") systems, verify if the system is booted in UEFI mode by checking [efivars](/index.php/Efivars "Efivars"):

```
# ls /sys/firmware/efi/efivars

```

### Set the keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available choices can be listed with `ls /usr/share/kbd/keymaps/**/*.map.gz`.

The layout can be changed with *loadkeys*, appending a file name (path and file extension can be omitted). For example:

```
# loadkeys *de-latin1*

```

[Console fonts](/index.php/Fonts#Console_fonts "Fonts") are located in `/usr/share/kbd/consolefonts/`, and can likewise be set with *setfont*.

### Connect to the Internet

Internet service via DHCP discovery is enabled on boot for supported wired devices; read more at [Network configuration](/index.php/Network_configuration "Network configuration"). For supported wireless devices run `wifi-menu` to set up the network; read more with [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration"). If needing a static IP or network management tools, [stop](/index.php/Stop "Stop") `dhcpcd@*eth0*.service` and read [Netctl](/index.php/Netctl "Netctl").

### Update the system clock

Use [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") to ensure the system clock is accurate:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

### Partition the disks

See [Partitioning](/index.php/Partitioning "Partitioning") for details; some special partitions may be needed, see [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") and [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). If wanting to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), do it now.

### Format the partitions

See [File systems](/index.php/File_systems#Create_a_filesystem "File systems") and optionally [Swap](/index.php/Swap "Swap") for details.

### Mount the partitions

Mount the root partition on `/mnt`. After that, create directories for and mount any other partitions (`/mnt/boot`, `/mnt/home`, ...) and activate your *swap* partition if you want them to be detected later by *genfstab*.

## Installation

### Select the mirrors

Edit `/etc/pacman.d/mirrorlist` and select a download mirror(s). Regional mirrors usually work best; however, other criteria may be necessary to discern, read more on [Mirrors](/index.php/Mirrors "Mirrors"). This copy of the `mirrorlist` file will later be copied on the new system by *pacstrap*, so it is worth getting it right.

### Install the base packages

Use the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script to install the [base](https://www.archlinux.org/groups/x86_64/base/) group:

```
# pacstrap /mnt base

```

Other packages or groups can be installed by appending their names to the above command (space separated), possibly including the boot loader.

## Configure the system

### Fstab

Generate an [fstab](/index.php/Fstab "Fstab") file (use `-U` or `-L` to define by UUID or labels):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

### Chroot

[Change root](/index.php/Change_root "Change root") into the new system:

```
# arch-chroot /mnt

```

### Time zone

Set the [time zone](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

### Locale

Uncomment the needed [locales](/index.php/Locale "Locale") in `/etc/locale.gen`, then generate them with:

```
# locale-gen

```

Add at least `LANG=*your_locale*` in `/etc/locale.conf` and possibly `$HOME/.config/locale.conf`.

Add console [keymap](/index.php/Keymap "Keymap") and [font](/index.php/Fonts#Console_fonts "Fonts") preferences in `/etc/vconsole.conf`.

### Network configuration

[Create](/index.php/Create "Create") the [/etc/hostname](/index.php//etc/hostname "/etc/hostname") file.

Configure the network for the newly installed environment: see [Network configuration](/index.php/Network_configuration "Network configuration") and [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Initramfs

Configure [/etc/mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio") if additional features are needed. Create a new initial RAM disk with:

```
# mkinitcpio -p linux

```

### Root password

Set the root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader

See [Boot loaders](/index.php/Boot_loaders "Boot loaders") for the available choices and configuration.

## Reboot

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`.

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)").

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").
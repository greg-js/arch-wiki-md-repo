This document is a guide for installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") from the live system booted with the official installation image. Before installing, it would be advised to view the [FAQ](/index.php/FAQ "FAQ"). For conventions used in this document, see [Help:Reading](/index.php/Help:Reading "Help:Reading").

For more detailed instructions, see the respective [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") articles or the various programs' [man pages](/index.php/Man_page "Man page"), both linked from this guide. See [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) for an overview of the configuration. For interactive help, the [IRC channel](/index.php/IRC_channel "IRC channel") and the [forums](https://bbs.archlinux.org/) are also available.

## Contents

*   [1 Pre-installation](#Pre-installation)
    *   [1.1 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [1.2 Verify the boot mode](#Verify_the_boot_mode)
    *   [1.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [1.4 Update the system clock](#Update_the_system_clock)
    *   [1.5 Partition the disks](#Partition_the_disks)
    *   [1.6 Format the partitions](#Format_the_partitions)
    *   [1.7 Mount the file systems](#Mount_the_file_systems)
*   [2 Installation](#Installation)
    *   [2.1 Select the mirrors](#Select_the_mirrors)
    *   [2.2 Install the base packages](#Install_the_base_packages)
*   [3 Configure the system](#Configure_the_system)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Locale](#Locale)
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Network configuration](#Network_configuration)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root password](#Root_password)
    *   [3.9 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## Pre-installation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "w:P6 (microarchitecture)") or [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space. As the installation process needs to retrieve packages from a remote repository, a working internet connection is required.

Download and boot the installation medium as explained in [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). You will be logged in on the first [virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") as the root user, and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt; common commands such as [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) can be [tab-completed](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

To switch to a different console—for example, to view this guide with [ELinks](/index.php/ELinks "ELinks") alongside the installation—use the `Alt+*arrow*` [shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts"). To [edit](/index.php/Textedit "Textedit") configuration files, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") and [vim](/index.php/Vim#Usage "Vim") are available.

### Set the keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). To list available layouts, run `ls /usr/share/kbd/keymaps/**/*.map.gz`.

To modify the layout, append a file name to [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html), omitting path and file extension. For example, run `loadkeys de-latin1` to set a [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "w:File:KB Germany.svg") keyboard layout.

[Console fonts](/index.php/Fonts#Console_fonts "Fonts") are located in `/usr/share/kbd/consolefonts/` and can likewise be set with [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### Verify the boot mode

If UEFI mode is enabled on an [UEFI](/index.php/UEFI "UEFI") motherboard, [Archiso](/index.php/Archiso "Archiso") will [boot](/index.php/Boot "Boot") Arch Linux accordingly via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). To verify this, list the [efivars](/index.php/UEFI#UEFI_Variables "UEFI") directory:

```
# ls /sys/firmware/efi/efivars

```

If the directory does not exist, the system is booted in [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") (or CSM) mode.

### Connect to the Internet

The [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon is [enabled](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) on boot for **wired** devices, and will attempt to start a connection. Verify a connection was established, for example with [ping](/index.php/Ping "Ping"):

```
# ping archlinux.org

```

If none is available, [stop](/index.php/Systemd#Using_units "Systemd") the *dhcpcd* service with `systemctl stop dhcpcd@<TAB>` and see [Network configuration](/index.php/Network_configuration#Device_driver "Network configuration").

For **wireless** connections, iw(8), wpa_supplicant(8) and [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") are available. See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Update the system clock

Use [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html) to ensure the system clock is accurate:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

### Partition the disks

When recognized by the live system, disks are assigned to a *block device* such as `/dev/sda`. To identify these devices, use [lsblk](/index.php/Core_utilities#lsblk "Core utilities") or *fdisk* — results ending in `rom`, `loop` or `airoot` may be ignored:

```
# fdisk -l

```

The following *partitions* (shown with a numerical suffix) are required for a chosen device:

*   One partition for the root directory `/`.
*   If [UEFI](/index.php/UEFI "UEFI") is enabled, an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   [Swap space](/index.php/Swap_space "Swap space") can be set on a separate partition or a [swap file](/index.php/Swap#Swap_file "Swap").

To modify *partition tables*, use [fdisk](/index.php/Fdisk "Fdisk") or [parted](/index.php/Parted "Parted"). See [Partitioning](/index.php/Partitioning "Partitioning") for more information.

If wanting to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), do it now.

### Format the partitions

Once the partitions have been created, each must be formatted with an appropriate [file system](/index.php/File_system "File system"). For example, to format the root partition on `/dev/*sda1*` with `*ext4*`, run:

```
# mkfs.*ext4* /dev/*sda1*

```

See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for details.

### Mount the file systems

[Mount](/index.php/File_systems#Mount_a_filesystem "File systems") the file system on the root partition to `/mnt`, for example:

```
# mount /dev/*sda1* /mnt

```

Create mount points for any remaining partitions and mount them accordingly, for example:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) will later detect mounted file systems and swap space.

## Installation

### Select the mirrors

Packages to be installed must be downloaded from [mirror servers](/index.php/Mirrors "Mirrors"), which are defined in `/etc/pacman.d/mirrorlist`. On the live system, all mirrors are enabled, and sorted by their synchronization status and speed at the time the installation image was created.

The higher a mirror is placed in the list, the more priority it is given when downloading a package. You may want to edit the file accordingly, and move the geographically closest mirrors to the top of the list, although other criteria should be taken into account.

This file will later be copied to the new system by *pacstrap*, so it is worth getting right.

### Install the base packages

Use the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script to install the [base](https://www.archlinux.org/groups/x86_64/base/) package group:

```
# pacstrap /mnt base

```

This group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) or specific wireless firmware; see [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) for comparison.

To [install](/index.php/Help:Reading#Installation_of_packages "Help:Reading") packages and other groups such as [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), append the names to *pacstrap* (space separated) or to individual [pacman](/index.php/Pacman "Pacman") commands after the [#Chroot](#Chroot) step.

## Configure the system

### Fstab

Generate an [fstab](/index.php/Fstab "Fstab") file (use `-U` or `-L` to define by [UUID](/index.php/UUID "UUID") or labels, respectively):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Check the resulting file in `/mnt/etc/fstab` afterwards, and edit it in case of errors.

### Chroot

[Change root](/index.php/Change_root "Change root") into the new system:

```
# arch-chroot /mnt

```

### Time zone

Set the [time zone](/index.php/Time#Time_zone "Time"):

```
# ln -s /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Run [hwclock(8)](http://man7.org/linux/man-pages/man8/hwclock.8.html) to generate `/etc/adjtime`:

```
# hwclock --systohc

```

This command assumes the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"). See [Time#Time standard](/index.php/Time#Time_standard "Time") for details.

### Locale

Uncomment `en_US.UTF-8 UTF-8` and other needed [localizations](/index.php/Localization "Localization") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Set the `LANG` [variable](/index.php/Variable "Variable") in [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html) accordingly, for example:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Hostname

Create the [hostname(5)](http://man7.org/linux/man-pages/man5/hostname.5.html) file with the desired [hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration"):

 `/etc/hostname` 
```
*myhostname*

```

Consider adding a [matching entry](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") to `/etc/hosts`:

```
127.0.1.1 *myhostname*.localdomain *myhostname*

```

### Network configuration

Configure the network for the newly installed environment: see [Network configuration](/index.php/Network_configuration "Network configuration").

For [Wireless configuration](/index.php/Wireless_configuration "Wireless configuration"), [install](/index.php/Help:Reading#Installation_of_packages "Help:Reading") the [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), and [dialog](https://www.archlinux.org/packages/?name=dialog) packages, as well as needed [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

### Initramfs

When making configuration changes to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), create a new initial RAM disk with:

```
# mkinitcpio -p linux

```

### Root password

Set the root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader

See [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") for available choices and configurations. For example, set up the boot loader with [systemd-boot](/index.php/Systemd-boot "Systemd-boot") if your system supports UEFI, and [GRUB](/index.php/GRUB#BIOS_systems "GRUB") when not.

If you have an Intel CPU, install the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package in addition, and [enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reboot

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`.

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](http://man7.org/linux/man-pages/man1/fuser.1.html).

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").
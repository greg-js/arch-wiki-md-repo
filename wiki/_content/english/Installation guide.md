This document is a guide for installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") from the live system booted with the official installation image. Before installing, it would be advised to view the [FAQ](/index.php/FAQ "FAQ"). For conventions used in this document, see [Help:Reading](/index.php/Help:Reading "Help:Reading").

For more detailed instructions, see the respective [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") articles (accessible from the installation environment with [ELinks](/index.php/ELinks "ELinks")), or the various programs' [man pages](/index.php/Man_page "Man page"); see [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) for an overview of the configuration. For interactive help, the [IRC channel](/index.php/IRC_channel "IRC channel") and the [forums](https://bbs.archlinux.org/) are also available.

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
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Network configuration](#Network_configuration)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root password](#Root_password)
    *   [3.9 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## Pre-installation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

Download and boot the installation medium as explained in [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). You will be logged in as the root user, and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt; common commands such as [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) can be [tab-completed](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

To [edit](/index.php/Textedit "Textedit") configuration files, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") and [vim](/index.php/Vim#Usage "Vim") are available.

The installation process needs to retrieve packages from a remote repository, therefore a working internet connection is required.

### Verify the boot mode

As instructions differ for [UEFI](/index.php/UEFI "UEFI") systems, verify the boot mode by checking [efivars](/index.php/Efivars "Efivars"):

```
# ls /sys/firmware/efi/efivars

```

### Set the keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available choices can be listed with `ls /usr/share/kbd/keymaps/**/*.map.gz`.

The layout can be changed with [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html), appending a file name (path and file extension can be omitted). For example:

```
# loadkeys *de-latin1*

```

[Console fonts](/index.php/Console_fonts "Console fonts") are located in `/usr/share/kbd/consolefonts/`, and can likewise be set with [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### Connect to the Internet

Internet service via [dhcpcd](/index.php/Dhcpcd "Dhcpcd") is enabled on boot for supported wired devices; check the connection using a tool such as [ping](/index.php/Ping "Ping").

If a different [network configuration](/index.php/Network_configuration "Network configuration") tool is needed, [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [netctl](/index.php/Netctl "Netctl") are available. See [systemd.network(5)](http://man7.org/linux/man-pages/man5/systemd.network.5.html) and [netctl.profile(5)](https://git.archlinux.org/netctl.git/tree/docs/netctl.profile.5.txt) for examples. When using either service, [stop](/index.php/Stop "Stop") `dhcpcd@*interface*.service` first.

### Update the system clock

Use [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html) to ensure the system clock is accurate:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

### Partition the disks

To modify and print [partition tables](/index.php/Partition_table "Partition table"), use [fdisk](/index.php/Fdisk "Fdisk") or [parted](/index.php/Parted "Parted") for both [MBR](/index.php/MBR "MBR") and [GPT](/index.php/GPT "GPT"), or [gdisk](/index.php/Gdisk "Gdisk") for GPT only.

At least one partition must be available for the `/` directory. [UEFI](/index.php/UEFI "UEFI") systems additionally require an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition"). Other partitions may be needed, such as a [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").

If wanting to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), do it now.

### Format the partitions

[File systems](/index.php/File_systems "File systems") are created using [mkfs(8)](http://man7.org/linux/man-pages/man8/mkfs.8.html), or [mkswap(8)](http://man7.org/linux/man-pages/man8/mkswap.8.html) in case of the [swap](/index.php/Swap "Swap") area. See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for details.

### Mount the partitions

[mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html) the root partition on `/mnt`. After that, create directories for and mount any other partitions (`/mnt/boot`, `/mnt/home`, ...) and activate your *swap* partition with [swapon(8)](http://man7.org/linux/man-pages/man8/swapon.8.html), if you want them to be detected later by *genfstab*.

## Installation

### Select the mirrors

Edit `/etc/pacman.d/mirrorlist` and select a download mirror(s). Regional mirrors usually work best; however, other criteria may be necessary to discern, read more on [Mirrors](/index.php/Mirrors "Mirrors").

This file will later be copied to the new system by *pacstrap*, so it is worth getting right.

### Install the base packages

Use the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script to install the [base](https://www.archlinux.org/groups/x86_64/base/) package group:

```
# pacstrap /mnt base

```

The group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) or specific wireless firmware; see [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) for comparison.

To [install](/index.php/Install "Install") other packages or groups to the new system, append their names to *pacstrap* (space separated) or to individual [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html) commands after the [#Chroot](#Chroot) step.

## Configure the system

### Fstab

Generate an [fstab](/index.php/Fstab "Fstab") file (use `-U` or `-L` to define by [UUID](/index.php/UUID "UUID") or labels):

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

Set the [time zone](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

Run [hwclock(8)](http://man7.org/linux/man-pages/man8/hwclock.8.html) to generate `/etc/adjtime`. If the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"), other operating systems should be [configured accordingly](/index.php/Time_standard "Time standard").

```
# hwclock --systohc --*utc*

```

### Locale

Uncomment `en_US.UTF-8 UTF-8` and other needed [localizations](/index.php/Localization "Localization") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Set the `LANG` [variable](/index.php/Variable "Variable") in [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html) accordingly, for example:

```
# echo LANG=*en_US.UTF-8* > /etc/locale.conf

```

If required, set the [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [font](/index.php/Fonts#Console_fonts "Fonts") in [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html).

### Hostname

Create an entry for your hostname in `/etc/hostname`:

```
# echo *myhostname* > /etc/hostname

```

A matching entry in `/etc/hosts` is recommended: see [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Network configuration

Configure the network for the newly installed environment: see [Network configuration](/index.php/Network_configuration "Network configuration").

For [Wireless configuration](/index.php/Wireless_configuration "Wireless configuration"), [install](/index.php/Install "Install") the [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), and [dialog](https://www.archlinux.org/packages/?name=dialog) packages, as well as needed [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

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
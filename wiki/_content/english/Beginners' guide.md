This document will guide you through the process of installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") using the [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Before installing, you are advised to skim over the [FAQ](/index.php/FAQ "FAQ").

The community-maintained [ArchWiki](/index.php/Main_page "Main page") is the primary resource that should be consulted if issues arise. The [IRC channel](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) and the [forums](https://bbs.archlinux.org/) are also excellent resources if an answer cannot be found elsewhere. In accordance with [the Arch Way](/index.php/The_Arch_Way "The Arch Way"), you are encouraged to type `man *command*` to read the [man page](/index.php/Man_page "Man page") of any command you are unfamiliar with.

**Tip:** This guide is accessible from the live installation with the [ELinks](/index.php/ELinks "ELinks") browser, after the [#Connect to the Internet](#Connect_to_the_Internet) step. This can be done in a new [virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console"), switching (`Alt+arrow`) between the console containing the web page, and the console where you are performing the installation. Similarly, the `#archlinux` [IRC](/index.php/IRC "IRC") can be accessed using [irssi](/index.php/Irssi "Irssi").

## Contents

*   [1 Preparation](#Preparation)
    *   [1.1 UEFI mode](#UEFI_mode)
    *   [1.2 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [1.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [1.4 Update the system clock](#Update_the_system_clock)
*   [2 Prepare the storage devices](#Prepare_the_storage_devices)
    *   [2.1 Identify the devices](#Identify_the_devices)
    *   [2.2 Partition the devices](#Partition_the_devices)
    *   [2.3 Format the partitions](#Format_the_partitions)
    *   [2.4 Mount the partitions](#Mount_the_partitions)
*   [3 Installation](#Installation)
    *   [3.1 Select the mirrors](#Select_the_mirrors)
    *   [3.2 Install the base packages](#Install_the_base_packages)
*   [4 Configuration](#Configuration)
    *   [4.1 fstab](#fstab)
    *   [4.2 Change root](#Change_root)
    *   [4.3 Locale](#Locale)
    *   [4.4 Time](#Time)
    *   [4.5 Initramfs](#Initramfs)
    *   [4.6 Boot loader](#Boot_loader)
    *   [4.7 Network configuration](#Network_configuration)
        *   [4.7.1 Hostname](#Hostname)
        *   [4.7.2 Wired](#Wired)
        *   [4.7.3 Wireless](#Wireless)
    *   [4.8 Root password](#Root_password)
*   [5 Unmount the partitions and reboot](#Unmount_the_partitions_and_reboot)
*   [6 Post-installation](#Post-installation)

## Preparation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for instructions on downloading the installation medium, and methods for booting it to the target machine(s). This guide assumes you use the latest available version.

After booting into the installation media, you will be automatically logged in as the root user and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt. For [modifying or creating](/index.php/Create "Create") configuration files, typically in `/etc`, [nano](/index.php/Nano#Usage "Nano") or [vim](/index.php/Vim#Usage "Vim") are suggested.

### UEFI mode

In case you have a [UEFI](/index.php/UEFI "UEFI") motherboard with UEFI mode enabled, the CD/USB will automatically launch Arch Linux via [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

To verify you are booted in UEFI mode, check that the following directory is populated:

```
# ls /sys/firmware/efi/efivars

```

See [UEFI#UEFI Variables](/index.php/UEFI#UEFI_Variables "UEFI") for details.

### Set the keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is set to [us](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available choices can be listed with `ls /usr/share/kbd/keymaps/**/*.map.gz`.

**Note:** `localectl list-keymaps` does not work due to bug [FS#46725](https://bugs.archlinux.org/task/46725).

For example, to change the layout to `de-latin1`, run:

```
# loadkeys *de-latin1*

```

If certain characters appear as white squares or other symbols, change the [console font](/index.php/Console_fonts "Console fonts"). For example:

```
# setfont *lat9w-16*

```

### Connect to the Internet

The [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon is enabled on boot for **wired** devices, and will attempt to start a connection. To access captive portal login forms, use the [ELinks](/index.php/ELinks "ELinks") browser.

Verify a connection was established, for example with `ping archlinux.org`. If no connection is available, see [Network configuration](/index.php/Network_configuration "Network configuration") or follow the below [netctl](/index.php/Netctl "Netctl") examples. Otherwise, continue to [#Update the system clock](#Update_the_system_clock).

	Netctl preparation

To prevent conflicts, [stop](/index.php/Stop "Stop") the enabled *dhcpcd* service first, replacing `*enp0s25*` with the correct wired interface:

```
# systemctl stop dhcpcd@*enp0s25*.service

```

[Interfaces](/index.php/Network_configuration#Device_names "Network configuration") can be listed using `ip link`, or `iw dev` for wireless devices. They are prefixed with `en` (ethernet), `wl` (WLAN), or `ww` (WWAN).

	Wireless

[List available networks](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration"), and make a connection for a specified interface:

```
# wifi-menu -o *wlp2s0*

```

The resulting configuration file is stored in `/etc/netctl`. For networks which require both a username and password, see [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

	Other

Several example profiles, such as for configuring a [static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration"), are available. Copy the required one to `/etc/netctl`, for example `*ethernet-static*`:

```
# cp /etc/netctl/examples/*ethernet-static* /etc/netctl

```

Adjust the copy as needed, and enable it:

```
# netctl start *ethernet-static*

```

### Update the system clock

Use [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") to ensure that your system clock is accurate. To start it:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

## Prepare the storage devices

**Warning:** In general, partitioning or formatting will make existing data inaccessible and subject to being overwritten, i.e. destroyed, by subsequent operations. For this reason, all data that needs to be preserved must be backed up before proceeding.

In this step, the storage devices that will be used by the new system will be prepared. Read [Partitioning](/index.php/Partitioning "Partitioning") for a more general overview.

Users intending to create stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), should keep those instructions in mind when preparing the partitions. If intending to install to a USB flash key, see [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

### Identify the devices

[Identify the devices](/index.php/File_systems#Identify_the_devices "File systems") where the new system will be installed:

```
# lsblk

```

Not all devices listed are viable mediums for installation; results ending in `rom`, `loop` or `airoot` can be ignored.

**Note:** In the sections below, the `sd**xy**` notation will be used (`**x**` for the device, `**y**` for an existing partition).

If the existing partition scheme does not need to be changed, you may skip to [#Format the partitions](#Format_the_partitions).

### Partition the devices

[Partitioning](/index.php/Partition "Partition") a hard drive divides the available space into sections that can be accessed independently. The required information is stored in a *partition table* using a format such as [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT"). Existing tables can be printed with `parted /dev/sd**x** print` or `fdisk -l /dev/sd**x**`.

To partition devices, use a [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning") compatible to the chosen type of partition table. Incompatible tools may result in the destruction of that table, along with existing partitions or data. Choices include:

| Name | MBR | GPT | Variants |
| [fdisk](/index.php/Fdisk "Fdisk") | Yes | Yes | *sfdisk*, *cfdisk* |
| [gdisk](/index.php/Gdisk "Gdisk") | No | Yes | *cgdisk*, *sgdisk* |
| [parted](/index.php/Parted "Parted") | Yes | Yes | [GParted](/index.php/GParted "GParted") |

The examples below demonstrate a basic [partition scheme](/index.php/Partition_scheme "Partition scheme") for both types of partition tables. They assume that a new, contiguous layout is applied to a single device in `/dev/sd**x**`. Necessary changes to device names and partition numbers must be done beforehand.

| UEFI/GPT example layout |
| Mount point | Partition | [Partition type (GUID)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | Bootable flag | Suggested size |
| /boot | /dev/sd**x**1 | [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") | Yes | 260–512 MiB |
| [SWAP] | /dev/sd**x**2 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**3 | Linux | No | Remainder of the device |
| MBR/BIOS example layout |
| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | Bootable flag | Suggested size |
| [SWAP] | /dev/sd**x**1 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**2 | Linux | Yes | Remainder of the device |

### Format the partitions

**Warning:** If [dual-booting](/index.php/Dual_boot_with_Windows "Dual boot with Windows") with an existing installation of Windows on a UEFI/GPT system, avoid reformatting the UEFI partition, as this includes the Windows *.efi* file required to boot it.

Once the partitions have been created, each **must** be formatted with an appropriate [file system](/index.php/File_system "File system"), *except* for [swap](/index.php/Swap "Swap") partitions. All available partitions on the intended installation device can be listed with the following command:

```
# lsblk /dev/sd**x**

```

With the exceptions noted below, it is recommended to use the `ext4` file system:

```
# mkfs.ext4 /dev/sd**xy**

```

If a swap partition was created, it must be set up and activated with:

```
# mkswap /dev/sd**xy**
# swapon /dev/sd**xy**

```

If a **new** UEFI system partition has been created on a UEFI/GPT system, it **must** be formatted with a `fat32` file system:

```
# mkfs.fat -F32 /dev/sd**xy**

```

### Mount the partitions

Mount the *root* partition to the `/mnt` directory of the live system:

```
# mount /dev/sd**xy** /mnt

```

Remaining [partitions](/index.php/Partitioning#Partition_scheme "Partitioning") except *swap* may be mounted in any order, after creating the respective mount points. For example, when using a `/boot` partition:

```
# mkdir -p /mnt/boot
# mount /dev/sd**xy** /mnt/boot

```

`/mnt/boot` is also recommended for mounting the (formatted or already existing) EFI System Partition on a UEFI/GPT system. See [EFISTUB](/index.php/EFISTUB "EFISTUB") and related articles for alternatives.

## Installation

### Select the mirrors

Packages to be installed must be downloaded from [mirror](/index.php/Mirror "Mirror") servers, which are defined in `/etc/pacman.d/mirrorlist`. On the live system, all mirrors are enabled, and sorted by their synchronization status and speed at the time the installation image was created.

The higher a mirror is placed in the list, the more priority it is given when downloading a package. You may want to edit the file accordingly, and move the geographically closest mirrors to the top of the list, although other criteria should be taken into account.

The *pacstrap* tool used in the next step also installs a copy of the file to the new system, so it is worth getting right.

### Install the base packages

The *pacstrap* script installs the [base](https://www.archlinux.org/groups/x86_64/base/) group of packages. This group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs); see [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) for comparison.

To build packages from the [AUR](/index.php/AUR "AUR") or with the [ABS](/index.php/ABS "ABS"), the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group is also required. Packages can be [installed](/index.php/Install "Install") with *pacman* anytime after the [#Change root](#Change_root) step later, or by appending their names to the *pacstrap* command.

```
# pacstrap -i /mnt base base-devel

```

The `-i` switch ensures prompting before package installation. With the base group, the first [initramfs](/index.php/Initramfs "Initramfs") will be generated and installed to the new system's boot path; double-check output prompts `==> Image creation successful` for it.

## Configuration

### fstab

Generate an [fstab](/index.php/Fstab "Fstab") file. The `-U` option indicates [UUIDs](/index.php/UUID "UUID"). Labels can be used instead through the `-L` option.

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Check the resulting file in `/mnt/etc/fstab` afterwards, and edit it in case of errors.

### Change root

[Chroot](/index.php/Chroot#Change_root "Chroot") to the new system:

```
# arch-chroot /mnt /bin/bash

```

### Locale

The [Locale](/index.php/Locale "Locale") defines which language the system uses, and other regional considerations such as currency denomination, numerology, and character sets.

Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen`, as well as other needed localisations. Save the file, and generate the new locales:

```
# locale-gen

```

[Create](/index.php/Create "Create") `/etc/locale.conf`, where `*en_US.UTF-8*` refers to the **first column** of an uncommented entry in `/etc/locale.gen`:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in `/etc/vconsole.conf`. For example, if `de-latin1` was set with *loadkeys*, and `lat9w-16` with *setfont*, assign the `KEYMAP` and `FONT` variables accordingly:

 `/etc/vconsole.conf` 
```
KEYMAP=*de-latin1*
FONT=*lat9w-16*
```

### Time

Select a [time zone](/index.php/Time_zone "Time zone"):

```
# tzselect

```

Create the symbolic link `/etc/localtime`, where `Zone/Subzone` is the `TZ` value from *tzselect*:

```
# ln -s /usr/share/zoneinfo/*Zone*/*SubZone* /etc/localtime

```

It is recommended to adjust the time skew, and set the time standard to UTC:

```
# hwclock --systohc --utc

```

If other operating systems are installed on the machine, they must be configured accordingly. See [Time](/index.php/Time "Time") for details.

### Initramfs

Because [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of [linux](https://www.archlinux.org/packages/?name=linux) with *pacstrap*, most users do not need to regenerate the intramfs image so this step can be skipped.

For special configurations, set the correct [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") in `/etc/mkinitcpio.conf` and [re-generate](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") the initramfs image:

```
# mkinitcpio -p linux

```

### Boot loader

See [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") for available choices and configurations. Choices include [GRUB](/index.php/GRUB "GRUB") (BIOS/UEFI), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (UEFI) and [syslinux](/index.php/Syslinux "Syslinux") (BIOS).

If you have an Intel CPU, in addition to installing a boot loader, install the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package and [enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

### Network configuration

The procedure is similar to [#Connect to the Internet](#Connect_to_the_Internet) for the live installation environment, except made persistent for subsequent boots.

#### Hostname

Set the [hostname](/index.php/Hostname "Hostname") by [adding](/index.php/Add "Add") an entry to `/etc/hostname`, where *myhostname* is the desired host name:

 `/etc/hostname`  `*myhostname*` 

It is recommended to append the same host name to `/etc/hosts`, for example:

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost	 *myhostname*
::1		localhost.localdomain	localhost	 *myhostname*
```

#### Wired

When only requiring a single wired connection, [enable](/index.php/Enable "Enable") the [dhcpcd](/index.php/Dhcpcd "Dhcpcd") service:

```
# systemctl enable dhcpcd@*interface*.service

```

Where `*interface*` is an ethernet [device name](/index.php/Network_configuration#Device_names "Network configuration").

See [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") for other available methods.

#### Wireless

[Install](/index.php/Install "Install") the [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), and (for [wifi-menu](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl")) [dialog](https://www.archlinux.org/packages/?name=dialog) packages:

```
# pacman -S iw wpa_supplicant dialog

```

Additional [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless") may also be required. When using *wifi-menu*, do so after [#Unmount the partitions and reboot](#Unmount_the_partitions_and_reboot).

See [Wireless#Wireless management](/index.php/Wireless#Wireless_management "Wireless") for other available methods.

### Root password

Set the root [password](/index.php/Password "Password") with:

```
# passwd

```

## Unmount the partitions and reboot

Exit from the chroot environment by running `exit` or pressing `Ctrl+D`.

Partitions will be unmounted automatically by *systemd* on shutdown. You may however unmount manually as a safety measure:

```
# umount -R /mnt

```

If the partition is "busy", you can find the cause with [fuser](/index.php/Fuser "Fuser"). Reboot the computer.

```
# reboot

```

Remove the installation media, or you may boot back into it. You can log into your new installation as *root*, using the password you specified with *passwd*.

## Post-installation

Your new Arch Linux base system is now a functional GNU/Linux environment ready to be built into whatever you wish or require for your purposes. You are now *strongly* advised to read the [General recommendations](/index.php/General_recommendations "General recommendations") article, especially the first two sections. Its other sections provide links to post-installation tutorials like setting up a graphical user interface, sound or a touchpad.

For particular areas of interest, see the [List of applications](/index.php/List_of_applications "List of applications").
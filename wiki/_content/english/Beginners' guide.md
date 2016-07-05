This document will guide you through the process of installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") using the [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Before installing, you are advised to skim over the [FAQ](/index.php/FAQ "FAQ").

The community-maintained [ArchWiki](/index.php/Main_page "Main page") is the primary resource that should be consulted if issues arise. The [IRC channel](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) and the [forums](https://bbs.archlinux.org/) are also excellent resources if an answer cannot be found elsewhere. In accordance with [the Arch Way](/index.php/The_Arch_Way "The Arch Way"), you are encouraged to type `man *command*` to read the [man page](/index.php/Man_page "Man page") of any command you are unfamiliar with.

**Tip:**

*   You can access this page from the live installation using the [elinks](/index.php/Elinks "Elinks") browser once [connected to the internet](#Connect_to_the_Internet). For example, you could open this page with elinks in a new [virtual console](https://en.wikipedia.org/wiki/Virtual_Console "wikipedia:Virtual Console") as a reference, switching between the console containing the webpage and the console where you are performing the installation as needed.
*   You can access the IRC channel from the live installation media using [irssi](/index.php/Irssi "Irssi") once connected to the internet. As above, this can be done in a different virtual console if needed.

## Contents

*   [1 Preparation](#Preparation)
    *   [1.1 UEFI mode](#UEFI_mode)
    *   [1.2 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [1.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [1.4 Update the system clock](#Update_the_system_clock)
*   [2 Prepare the storage devices](#Prepare_the_storage_devices)
    *   [2.1 Identify the devices](#Identify_the_devices)
    *   [2.2 Partitioning tools](#Partitioning_tools)
    *   [2.3 Partitioning layout](#Partitioning_layout)
        *   [2.3.1 UEFI/GPT example](#UEFI.2FGPT_example)
        *   [2.3.2 BIOS/MBR example](#BIOS.2FMBR_example)
    *   [2.4 Format the file systems](#Format_the_file_systems)
*   [3 Installation](#Installation)
    *   [3.1 Select the mirrors](#Select_the_mirrors)
    *   [3.2 Install the base packages](#Install_the_base_packages)
*   [4 Configuration](#Configuration)
    *   [4.1 fstab](#fstab)
    *   [4.2 Change root](#Change_root)
    *   [4.3 Locale](#Locale)
    *   [4.4 Time](#Time)
    *   [4.5 Initramfs](#Initramfs)
    *   [4.6 Install a boot loader](#Install_a_boot_loader)
        *   [4.6.1 UEFI/GPT](#UEFI.2FGPT)
        *   [4.6.2 BIOS/MBR](#BIOS.2FMBR)
    *   [4.7 Configure the network](#Configure_the_network)
        *   [4.7.1 Hostname](#Hostname)
        *   [4.7.2 Wired](#Wired)
        *   [4.7.3 Wireless](#Wireless)
    *   [4.8 Root password](#Root_password)
*   [5 Unmount the partitions and reboot](#Unmount_the_partitions_and_reboot)
*   [6 Post-installation](#Post-installation)

## Preparation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for instructions on downloading the installation medium, and methods for booting it to the target machine(s). This guide assumes you use the latest available version.

You will be logged in as the root user and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt. *Zsh* provides advanced [tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html) and other features as part of the [grml config](http://grml.org/zsh/). For [modifying or creating](/index.php/Create "Create") configuration files, typically in `/etc`, [nano](/index.php/Nano#Usage "Nano") and [vim](/index.php/Vim#Usage "Vim") are suggested.

### UEFI mode

In case you have a [UEFI](/index.php/UEFI "UEFI") motherboard with UEFI mode enabled, the CD/USB will automatically launch Arch Linux via [systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/).

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

	Wired

The [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon is enabled on boot for wired devices, and will attempt to start a connection. To access captive portal login forms, use the [ELinks](/index.php/ELinks "ELinks") browser.

Verify a connection was established, for example with *ping*. If none is available, proceed to [configure the network](/index.php/Network_configuration "Network configuration"); the examples below use [netctl](/index.php/Netctl "Netctl") to this purpose. To prevent conflicts, [stop](/index.php/Stop "Stop") the *dhcpcd* service (replacing `enp0s25` with the correct wired interface):

```
# systemctl stop dhcpcd@*enp0s25*.service

```

[Interfaces](/index.php/Network_configuration#Device_names "Network configuration") can be listed using `ip link`, or `iw dev` for wireless devices. They are prefixed with `en` (ethernet), `wl` (WLAN), or `ww` (WWAN).

	Wireless

List [available networks](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration"), and make a connection for a specified interface:

```
# wifi-menu -o *wlp2s0*

```

The resulting configuration file is stored in `/etc/netctl`. For networks which require both a username and password, see [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

	Other

Several example profiles, such as for configuring a [static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration"), are available. Copy the required one to `/etc/netctl`, for example `ethernet-static`:

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

In the sections below, the `sd**xy**` convention will be followed (`**x**` for the device, `**y**` for an existing partition).

If the existing partition scheme does not need to be changed, skip to [#Format the file systems and enable swap](#Format_the_file_systems_and_enable_swap), otherwise continue reading the following section.

### Partitioning tools

**Warning:** If dual-booting with an existing installation of Windows on a UEFI/GPT system, avoid reformatting the UEFI partition, as this includes the Windows *.efi* file required to boot it. Furthermore, Arch must follow the same firmware boot mode and partitioning combination as Windows. See [Dual boot with Windows#Important information](/index.php/Dual_boot_with_Windows#Important_information "Dual boot with Windows").

Partitioning a hard drive divides the available space into sections that can be accessed independently. The required information is stored in a *partition table* using a format such as [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT").

To print an existing partition table, such as from an earlier installed system, run `parted /dev/sd**x** print` or `fdisk -l /dev/sd**x**`.

To partition devices, use a [partitioning tool](/index.php/Partitioning#Partitioning_tool "Partitioning") which matches the chosen type of partition table. An incompatible tool may result in the destruction of that table, along with existing partitions or data. Choices include:

| Name | MBR | GPT |
| [fdisk](/index.php/Fdisk "Fdisk"), (*sfdisk*, *cfdisk*) | Yes | Yes |
| [gdisk](/index.php/Gdisk "Gdisk"), (*cgdisk*, *sgdisk*) | No | Yes |
| [parted](/index.php/Parted "Parted") | Yes | Yes |

Devices may also be partitioned before booting the installation media, for example through tools such as [GParted](/index.php/GParted "GParted") (also provided as a [live CD](http://gparted.sourceforge.net/livecd.php)).

### Partitioning layout

To decide the number and size of the partitions the devices should be split into, and which directories will be used to mount the partitions in the installed system (also known as *mount points*). This mapping from partitions is referred to as *partitioning layout* or [partitioning scheme](/index.php/Partitioning#Partition_scheme "Partitioning"), and must comply with the following requirements:

*   At least a partition for the `/` (*root*) directory,
*   When using a UEFI motherboard, one [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

In the examples below it is assumed that a new and contiguous partitioning scheme is applied to a single device, here in `**/dev/sda**`. Make any necessary changes to device names, partition numbers, partition sizes, and others where appropriate; **do not copy and paste commands blindly**.

Optional partitions will also be created for the `/home` (otherwise contained in the `/` partition) and [Swap](/index.php/Swap "Swap") directories (otherwise included as a [swap file](/index.php/Swap_file "Swap file")). See [Partitioning#Mount_points](/index.php/Partitioning#Mount_points "Partitioning") for more information.

#### UEFI/GPT example

A special *bootable* [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") is required, here assumed in `/boot`.

| Mount point | Partition | [Partition type (GUID)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | Bootable flag | Suggested size |
| /boot | /dev/sda1 | EFI System partition | Yes | 260 - 512 MiB |
| /swap | /dev/sda2 | Linux swap | No | 512 MiB - RAM size |
| / | /dev/sda3 | Linux | No | 15 - 20 GiB |
| /home | /dev/sda4 | Linux | No | Remainder of the partition |

#### BIOS/MBR example

| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | Bootable flag | Suggested size |
| /swap | /dev/sda2 | Linux swap | No | 512 MiB - RAM size |
| / | /dev/sda3 | Linux | Yes | 15 - 20 GiB |
| /home | /dev/sda4 | Linux | No | Remainder of the partition |

### Format the file systems

Once the partitions have been created, each **must** be formatted with an appropriate [file system](/index.php/File_system "File system"), *except* for swap partitions. All available partitions on the intended installation device can be listed with the following command:

```
# lsblk /dev/sd**x**

```

With the exceptions noted below, it is recommended to use the `ext4` file system:

```
# mkfs.ext4 /dev/sd**xy**

```

*If* a new UEFI system partition has been created on a UEFI/GPT system, it **must** be formatted with a `fat32` file system:

```
# mkfs.fat -F32 /dev/sd**xy**

```

*If* a swap partition was created, it must be set up and activated with:

```
# mkswap /dev/sd**xy**
# swapon /dev/sd**xy**

```

Mount the root partition to the `/mnt` directory of the live system:

```
# mount /dev/sd**xy** /mnt

```

Remaining [partitions](/index.php/Partitioning#Partition_scheme "Partitioning") (except *swap*) may be mounted in any order, after creating the respective mount points. For example, when using a `/boot` partition:

```
# mkdir -p /mnt/boot
# mount /dev/sd**xy** /mnt/boot

```

`/mnt/boot` is also recommended for mounting the (formatted or already existing) EFI System Partition on a UEFI/GPT system. See [EFISTUB](/index.php/EFISTUB "EFISTUB") and related articles for alternatives.

## Installation

### Select the mirrors

Packages to be installed must be downloaded from mirror servers, which are defined in `/etc/pacman.d/mirrorlist`. On the live system, all mirrors are enabled, and sorted by their synchronization status and speed at the time the installation image was created.

The higher a mirror is placed in the list, the more priority it is given when downloading a package. You may want to edit the file accordingly, and move the geographically closest mirrors to the top of the list, although other criteria should be taken into account. See [Mirrors](/index.php/Mirrors "Mirrors") for details.

*pacstrap* will also install a copy of this file to the new system, so it is worth getting right.

### Install the base packages

The *pacstrap* script installs the base system. To build packages from the [AUR](/index.php/AUR "AUR") or with [ABS](/index.php/ABS "ABS"), the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group is also required.

Not all tools from the live installation (see [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both)) are part of the base group. Packages can later be [installed](/index.php/Install "Install") with *pacman*, or by appending their names to the *pacstrap* command.

```
# pacstrap -i /mnt base base-devel

```

The `-i` switch ensures prompting before package installation.

## Configuration

### fstab

Generate an [fstab](/index.php/Fstab "Fstab") file. The `-U` option indicates UUIDs: see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"). Labels can be used instead through the `-L` option.

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Check the resulting file in `/mnt/etc/fstab` afterwards, and edit it in case of errors.

### Change root

Copy netctl profiles in `/etc/netctl` to the new system in `/mnt` (when applicable), then [chroot](/index.php/Chroot#Change_root "Chroot") to it:

```
# arch-chroot /mnt /bin/bash

```

### Locale

The [Locale](/index.php/Locale "Locale") defines which language the system uses, and other regional considerations such as currency denomination, numerology, and character sets.

Possible values are listed in `/etc/locale.gen`. Uncomment `en_US.UTF-8 UTF-8`, as well as other needed localisations. Save the file, and generate the new locales:

```
# locale-gen

```

[Create](/index.php/Create "Create") `/etc/locale.conf`, where `LANG` refers to the *first column* of an uncommented entry in `/etc/locale.gen`:

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

As [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of [linux](https://www.archlinux.org/packages/?name=linux) with *pacstrap*, most users can use the defaults provided in `mkinitcpio.conf`.

For special configurations, set the correct [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") in `/etc/mkinitcpio.conf` and [re-generate](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") the initramfs image:

```
# mkinitcpio -p linux

```

### Install a boot loader

See [Boot loaders](/index.php/Boot_loaders "Boot loaders") for available choices and configurations. If you have an Intel CPU, install the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package, and [enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

| Name | BIOS | UEFI | Dual-boot |
| [grub](/index.php/Grub "Grub") | Yes | Yes | Yes |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | Yes | Yes | Yes |
| [syslinux](/index.php/Syslinux "Syslinux") | Yes | Partial | Partial |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | No | Yes | Yes |
| [rEFInd](/index.php/REFInd "REFInd") | No | Yes | Yes |
| [Clover](/index.php/Clover "Clover") | No | Yes | Yes |

#### UEFI/GPT

Here, the installation drive is assumed to be GPT-partioned, and have the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") (gdisk type `EF00`, formatted with FAT32) mounted at `/boot`.

Install [systemd-boot](/index.php/Systemd-boot "Systemd-boot") to the EFI system partition:

```
# bootctl install

```

When successful, create a boot entry as described in [systemd-boot#Configuration](/index.php/Systemd-boot#Configuration "Systemd-boot") (replacing `$esp` with `/boot`), or adapt the examples in `/usr/share/systemd/bootctl/`.

#### BIOS/MBR

Install the [grub](https://www.archlinux.org/packages/?name=grub) package. To search for other operating systems, also install [os-prober](https://www.archlinux.org/packages/?name=os-prober):

```
# pacman -S grub os-prober

```

Install the bootloader to the *drive* Arch was installed to:

```
# grub-install --target=i386-pc */dev/sda*

```

Generate `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

See [GRUB](/index.php/GRUB "GRUB") for more information.

### Configure the network

The procedure is similar to [#Connect to the Internet](#Connect_to_the_Internet), except made persistent for subsequent boots. Select **one** daemon to handle the network.

#### Hostname

Set the [hostname](/index.php/Hostname "Hostname") to your liking by [adding](/index.php/Add "Add") *myhostname* to the following file, where *myhostname* is the hostname you wish to set:

 `/etc/hostname`  `*myhostname*` 

It is recommended to [append](/index.php/Append "Append") the same hostname to `localhost` entries in `/etc/hosts`. See [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration") for details.

#### Wired

When only requiring a single wired connection, [enable](/index.php/Enable "Enable") the [dhcpcd](/index.php/Dhcpcd "Dhcpcd") service:

```
# systemctl enable dhcpcd@*interface*.service

```

Where `*interface*` is an ethernet [device name](/index.php/Network_configuration#Device_names "Network configuration").

See [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") for other available methods.

#### Wireless

Install [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), and (for *wifi-menu*) [dialog](https://www.archlinux.org/packages/?name=dialog):

```
# pacman -S iw wpa_supplicant dialog

```

Additional [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless") may also be required. When using *wifi-menu*, do so after [#Unmount_the_partitions_and_reboot](#Unmount_the_partitions_and_reboot).

See [Netctl](/index.php/Netctl "Netctl") and [Wireless#Wireless management](/index.php/Wireless#Wireless_management "Wireless") for more information.

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

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").
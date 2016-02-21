This document will guide you through the process of installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") using the [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Before installing, you are advised to skim over the [FAQ](/index.php/FAQ "FAQ").

The community-maintained [ArchWiki](/index.php/Main_page "Main page") is the primary resource that should be consulted if issues arise. The [IRC channel](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) and the [forums](https://bbs.archlinux.org/) are also excellent resources if an answer cannot be found elsewhere. In accordance with [the Arch Way](/index.php/The_Arch_Way "The Arch Way"), you are encouraged to type `man *command*` to read the [man page](/index.php/Man_page "Man page") of any command you are unfamiliar with.

## Contents

*   [1 Preparation](#Preparation)
*   [2 Boot the installation medium](#Boot_the_installation_medium)
    *   [2.1 UEFI mode](#UEFI_mode)
    *   [2.2 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [2.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [2.4 Update the system clock](#Update_the_system_clock)
*   [3 Prepare the storage devices](#Prepare_the_storage_devices)
    *   [3.1 Identify the devices](#Identify_the_devices)
    *   [3.2 Partition table types](#Partition_table_types)
    *   [3.3 Partitioning tools](#Partitioning_tools)
        *   [3.3.1 Using parted in interactive mode](#Using_parted_in_interactive_mode)
    *   [3.4 Create new partition table](#Create_new_partition_table)
    *   [3.5 Partition schemes](#Partition_schemes)
        *   [3.5.1 UEFI/GPT examples](#UEFI.2FGPT_examples)
        *   [3.5.2 BIOS/MBR examples](#BIOS.2FMBR_examples)
    *   [3.6 Format the file systems and enable swap](#Format_the_file_systems_and_enable_swap)
*   [4 Installation](#Installation)
    *   [4.1 Select the mirrors](#Select_the_mirrors)
    *   [4.2 Install the base packages](#Install_the_base_packages)
*   [5 Configuration](#Configuration)
    *   [5.1 fstab](#fstab)
    *   [5.2 Change root](#Change_root)
    *   [5.3 Locale](#Locale)
    *   [5.4 Time](#Time)
    *   [5.5 Initramfs](#Initramfs)
    *   [5.6 Install a boot loader](#Install_a_boot_loader)
        *   [5.6.1 UEFI/GPT](#UEFI.2FGPT)
        *   [5.6.2 BIOS/MBR](#BIOS.2FMBR)
    *   [5.7 Configure the network](#Configure_the_network)
        *   [5.7.1 Hostname](#Hostname)
        *   [5.7.2 Wired](#Wired)
        *   [5.7.3 Wireless](#Wireless)
*   [6 Unmount the partitions and reboot](#Unmount_the_partitions_and_reboot)
*   [7 Post-installation](#Post-installation)

## Preparation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for instructions on downloading the installation medium, and methods for booting it to the target machine(s). This guide assumes you use the latest available version.

## Boot the installation medium

Point the current boot device to the drive containing the Arch installation media. This is typically achieved by pressing a key during the [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") phase, as indicated on the splash screen. Refer to your motherboard's manual for details.

When the Arch menu appears, select *Boot Arch Linux* and press `Enter` to enter the installation environment. See [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) for a list of [boot parameters](/index.php/Kernel_parameters#Configuration "Kernel parameters").

You will be logged in as the root user and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt. *Zsh* provides advanced [tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html) and other features as part of the [grml config](http://grml.org/zsh/). For modifying or creating configuration files, typically in `/etc`, [nano](/index.php/Nano#Usage "Nano") and [vim](/index.php/Vim#Usage "Vim") are suggested.

### UEFI mode

In case you have a [UEFI](/index.php/UEFI "UEFI") motherboard with UEFI mode enabled, the CD/USB will automatically launch Arch Linux via [systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/).

To verify you are booted in UEFI mode, check that the following directory is populated:

```
# ls /sys/firmware/efi/efivars

```

See [UEFI#UEFI Variables](/index.php/UEFI#UEFI_Variables "UEFI") for details.

### Set the keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is set to [us](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available choices can be listed with `localectl list-keymaps`.

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

**Warning:**

*   In general, partitioning or formatting will make existing data inaccessible and subject to being overwritten, i.e. destroyed, by subsequent operations. For this reason, all data that needs to be preserved must be backed up before proceeding.
*   If dual-booting with an existing installation of Windows on a UEFI/GPT system, avoid reformatting the UEFI partition, as this includes the Windows *.efi* file required to boot it. Furthermore, Arch must follow the same firmware boot mode and partitioning combination as Windows. See [Dual boot with Windows#Important information](/index.php/Dual_boot_with_Windows#Important_information "Dual boot with Windows").

In this step, the storage devices that will be used by the new system will be prepared. Read [Partitioning](/index.php/Partitioning "Partitioning") for a more general overview.

Users intending to create stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), should keep those instructions in mind when preparing the partitions. If intending to install to a USB flash key, see [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

### Identify the devices

The first step is to identify the devices where the new system will be installed. The following command will show all the available devices:

```
# lsblk

```

This will list all devices connected to your system along with their partition schemes, including that used to host and boot live Arch installation media (e.g. a USB drive). Not all devices listed will therefore be viable or appropriate mediums for installation. Results ending in `rom`, `loop` or `airoot` can be ignored.

Devices (e.g. hard disks) will be listed as `sd*x*`, where `*x*` is a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. Existing partitions on those devices will be listed as `sd*xY*`, where `*Y*` is a number starting from `1` for the first partition, `2` for the second, and so on. In the example below, only one device is available (`sda`), and that device has only one partition (`sda1`):

```
NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda               8:0    0    80G  0 disk
└─sda1            8:1    0    80G  0 part

```

The `sd*xY*` convention will be used in the examples provided below for partition tables, partitions, and file systems. As they are just examples, it is important to ensure that any necessary changes to device names, partition numbers, and/or partition sizes (etc.) are made. Do not just blindly copy and paste the commands.

If the existing partition scheme does not need to be changed, skip to [#Format the file systems and enable swap](#Format_the_file_systems_and_enable_swap), otherwise continue reading the following section.

### Partition table types

If you are installing alongside an existing installation (i.e. dual-booting), a partition table will already be in use. If the devices are not partitioned, or the current partitions table or scheme needs to be changed, you will first have to determine the partition tables (one for each device) in use or to be used.

There are two types of partition table:

*   [GPT](/index.php/GPT "GPT")
*   [MBR](/index.php/MBR "MBR")

Any existing partition table can be identified with the following command for each device:

```
# parted /dev/sd*x* print

```

### Partitioning tools

**Warning:** Using a partitioning tool that is incompatible with your partition table type will likely result in the destruction of that table, along with any existing partitions/data.

For each device to be partitioned, a proper tool must be chosen according to the partition table to be used. Several partitioning tools are provided by the Arch installation medium, including:

*   [parted](/index.php/Parted "Parted"): GPT and MBR
*   [fdisk](/index.php/Fdisk#Fdisk_usage_summary "Fdisk"), **cfdisk**, **sfdisk**: GPT and MBR
*   [gdisk](/index.php/Gdisk#Gdisk_usage_summary "Gdisk"), **cgdisk**, **sgdisk**: GPT

Devices may also be partitioned before booting the installation media, for example through tools such as [GParted](/index.php/GParted "GParted") (also provided as a [live CD](http://gparted.sourceforge.net/livecd.php)).

#### Using parted in interactive mode

All the examples provided below make use of *parted*, as it can be used for both UEFI/GPT and BIOS/MBR. It will be launched in *interactive mode*, which simplifies the partitioning process and reduces unnecessary repetition by automatically applying all partitioning commands to the specified device.

In order to start operating on a device, execute:

```
# parted /dev/sd*x*

```

You will notice that the command-line prompt changes from a hash (`#`) to `(parted)`: this also means that the new prompt is not a command to be manually entered when running the commands in the examples.

To see a list of the available commands, enter:

```
(parted) help

```

When finished, or if wishing to implement a partition table or scheme for another device, exit from parted with:

```
(parted) quit

```

After exiting, the command-line prompt will change back to `#`.

### Create new partition table

You need to (re)create the partition table of a device when it has never been partitioned before, or when you want to change the type of its partition table. Recreating the partition table of a device is also useful when the partition scheme needs to be restructured from scratch.

Open each device whose partition table must be (re)created with:

```
# parted /dev/sd*x*

```

To then create a new GPT partition table for UEFI systems, use the following command:

```
(parted) mklabel gpt

```

To create a new MBR/msdos partition table for BIOS systems instead, use:

```
(parted) mklabel msdos

```

### Partition schemes

You can decide the number and size of the partitions the devices should be split into, and which directories will be used to mount the partitions in the installed system (also known as *mount points*). The mapping from partitions to directories is the [partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning"), which must comply with the following requirements:

*   At least a partition for the `/` (*root*) directory **must** be created.
*   When using a UEFI motherboard, one [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") **must** be created.

In the examples below it is assumed that a new and contiguous partitioning scheme is applied to a single device. Some optional partitions will also be created for the `/boot` and `/home` directories which otherwise would simply be contained in the `/` partition. See the [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") for an explanation of the purpose of the various directories. Also the creation of an optional partiton for [swap space](/index.php/Swap_space "Swap space") will be illustrated.

If not already open in a *parted* interactive session, open each device to be partitioned with:

```
# parted /dev/sd*x*

```

The following command will be used to create partitions:

```
(parted) mkpart *part-type* *fs-type* *start* *end*

```

*   `*part-type*` is one of `primary`, `extended` or `logical`, and is meaningful only for MBR partition tables.
*   `*fs-type*` is an identifier chosen among those listed by entering `help mkpart` as the closest match to the file system that you will use in [#Format the file systems and enable swap](#Format_the_file_systems_and_enable_swap). The *mkpart* command does not actually create the file system: the `*fs-type*` parameter will simply be used by *parted* to set a 1-byte code that is used by boot loaders to "preview" what kind of data is found in the partition, and act accordingly if necessary. See also [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

**Tip:** Most [Linux native file systems](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") map to the same partition code ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), so it is perfectly safe to e.g. use `ext2` for an *ext4*-formatted partition.

*   `*start*` is the beginning of the partition from the start of the device. It consists of a number followed by a [unit](http://www.gnu.org/software/parted/manual/parted.html#unit), for example `1M` means start at 1MiB.
*   `*end*` is the end of the partition from the start of the device (*not* from the `*start*` value). It has the same syntax as `*start*`, for example `100%` means end at the end of the device (use all the remaining space).

**Warning:** It is important that the partitions do not overlap each other: if you do not want to leave unused space in the device, make sure that each partition starts where the previous one ends.

**Note:** *parted* may issue a warning like:
```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```
In this case, read [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning") and follow [GNU Parted#Alignment](/index.php/GNU_Parted#Alignment "GNU Parted") to fix it.

The following command will be used to flag the partition that contains the `/boot` directory as bootable:

```
(parted) set *partition* boot on

```

*   `*partition*` is the number of the partition to be flagged (see the output of the `print` command).

#### UEFI/GPT examples

In every instance, a special bootable [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") is required.

If creating a new EFI System Partition, use the following commands (a size of 512MiB is suggested):

```
(parted) mkpart ESP fat32 1MiB 513MiB
(parted) set 1 boot on

```

The remaining partition scheme is entirely up to you. For one other partition using 100% of remaining space:

```
(parted) mkpart primary ext4 513MiB 100%

```

For separate `/` (20GiB) and `/home` (all remaining space) partitions:

```
(parted) mkpart primary ext4 513MiB 20.5GiB
(parted) mkpart primary ext4 20.5GiB 100%

```

And for separate `/` (20GiB), swap (4GiB), and `/home` (all remaining space) partitions:

```
(parted) mkpart primary ext4 513MiB 20.5GiB
(parted) mkpart primary linux-swap 20.5GiB 24.5GiB
(parted) mkpart primary ext4 24.5GiB 100%

```

#### BIOS/MBR examples

For a minimum single primary partition using all available disk space, the following command would be used:

```
(parted) mkpart primary ext4 1MiB 100%
(parted) set 1 boot on

```

In the following instance, a 20GiB `/` partition will be created, followed by a `/home` partition using all the remaining space:

```
(parted) mkpart primary ext4 1MiB 20GiB
(parted) set 1 boot on
(parted) mkpart primary ext4 20GiB 100%

```

In the final example below, separate `/boot` (100MiB), `/` (20GiB), swap (4GiB), and `/home` (all remaining space) partitions will be created:

```
(parted) mkpart primary ext4 1MiB 100MiB
(parted) set 1 boot on
(parted) mkpart primary ext4 100MiB 20GiB
(parted) mkpart primary linux-swap 20GiB 24GiB
(parted) mkpart primary ext4 24GiB 100%

```

### Format the file systems and enable swap

Once the partitions have been created, each **must** be formatted with an appropriate [file system](/index.php/File_system "File system"), *except* for swap partitions. All available partitions on the intended installation device can be listed with the following command:

```
# lsblk /dev/sd*x*

```

With the exceptions noted below, it is recommended to use the `ext4` file system:

```
# mkfs.ext4 /dev/sd*xY*

```

*If* a new UEFI system partition has been created on a UEFI/GPT system, it **must** be formatted with a `fat32` file system:

```
# mkfs.fat -F32 /dev/sd*xY*

```

*If* a swap partition has been created, it must be set up and activated with:

```
# mkswap /dev/sd*xY*
# swapon /dev/sd*xY*

```

Mount the root partition to the `/mnt` directory of the live system:

```
# mount /dev/sd*xY* /mnt

```

Remaining [partitions](/index.php/Partitioning#Partition_scheme "Partitioning") (except *swap*) may be mounted in any order, after creating the respective mount points. For example, when using a `/boot` partition:

```
# mkdir -p /mnt/boot
# mount /dev/sd*xZ* /mnt/boot

```

`/boot` is also recommended for mounting the EFI System Partition on a UEFI/GPT system. See [EFISTUB](/index.php/EFISTUB "EFISTUB") and related articles for alternatives.

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

Copy any other configuration files to the new system in `/mnt` (such as netctl profiles in `/etc/netctl`), then [chroot](/index.php/Chroot "Chroot") to it:

```
# arch-chroot /mnt /bin/bash

```

### Locale

The [Locale](/index.php/Locale "Locale") defines which language the system uses, and other regional considerations such as currency denomination, numerology, and character sets.

Possible values are listed in `/etc/locale.gen`. Uncomment `en_US.UTF-8 UTF-8`, as well as other needed localisations. Save the file, and generate the new locales:

```
# locale-gen

```

Create `/etc/locale.conf`, where `LANG` refers to the *first column* of an uncommented entry in `/etc/locale.gen`:

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

#### UEFI/GPT

Here, the installation drive is assumed to be GPT-partioned, and have the [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (gdisk type `EF00`, formatted with FAT32) mounted at `/boot`.

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
# grub-install */dev/sda*

```

Generate `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

See [GRUB](/index.php/GRUB "GRUB") for more information.

### Configure the network

The procedure is similar to [#Connect to the Internet](#Connect_to_the_Internet), except made persistent for subsequent boots. Select **one** daemon to handle the network.

#### Hostname

Set the [hostname](/index.php/Hostname "Hostname") to your liking:

 `/etc/hostname`  `*myhostname*` 

It is recommended to append the same hostname to `localhost` entries in `/etc/hosts`. See [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration") for details.

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

Additional [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless") may also be required.

If you used *wifi-menu* priorly, repeat the steps **after** finishing the rest of this installation and rebooting, to prevent conflicts with the existing processes.

See [Netctl](/index.php/Netctl "Netctl") and [Wireless#Wireless management](/index.php/Wireless#Wireless_management "Wireless") for more information.

## Unmount the partitions and reboot

Set the root [password](/index.php/Password "Password") with:

```
# passwd

```

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
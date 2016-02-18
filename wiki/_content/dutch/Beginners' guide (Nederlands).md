This document will guide you through the process of installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") using the [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Before installing, you are advised to skim over the [FAQ](/index.php/FAQ "FAQ").

The community-maintained [ArchWiki](/index.php/Main_page "Main page") is the primary resource that should be consulted if issues arise. The [IRC channel](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) and the [forums](https://bbs.archlinux.org/) are also excellent resources if an answer cannot be found elsewhere. In accordance with [the Arch Way](/index.php/The_Arch_Way "The Arch Way"), you are encouraged to type `man *command*` to read the [man page](/index.php/Man_page "Man page") of any command you are unfamiliar with.

## Contents

*   [1 Preparation](#Preparation)
*   [2 Boot the installation medium](#Boot_the_installation_medium)
    *   [2.1 UEFI mode](#UEFI_mode)
    *   [2.2 Keyboard layout](#Keyboard_layout)
*   [3 Establish an internet connection](#Establish_an_internet_connection)
    *   [3.1 Wireless](#Wireless)
    *   [3.2 Wired (Static IP)](#Wired_.28Static_IP.29)
*   [4 Update the system clock](#Update_the_system_clock)
*   [5 Prepare the storage devices](#Prepare_the_storage_devices)
    *   [5.1 Identify the devices](#Identify_the_devices)
    *   [5.2 Partition table types](#Partition_table_types)
    *   [5.3 Partitioning tools](#Partitioning_tools)
        *   [5.3.1 Using parted in interactive mode](#Using_parted_in_interactive_mode)
    *   [5.4 Create new partition table](#Create_new_partition_table)
    *   [5.5 Partition schemes](#Partition_schemes)
        *   [5.5.1 UEFI/GPT examples](#UEFI.2FGPT_examples)
        *   [5.5.2 BIOS/MBR examples](#BIOS.2FMBR_examples)
    *   [5.6 File systems and swap](#File_systems_and_swap)
*   [6 Select a mirror](#Select_a_mirror)
*   [7 Install the base system](#Install_the_base_system)
*   [8 Generate an fstab](#Generate_an_fstab)
*   [9 Configure the base system](#Configure_the_base_system)
    *   [9.1 Locale](#Locale)
    *   [9.2 Time](#Time)
    *   [9.3 Initramfs](#Initramfs)
    *   [9.4 Boot loader](#Boot_loader)
        *   [9.4.1 BIOS/MBR](#BIOS.2FMBR)
        *   [9.4.2 UEFI/GPT](#UEFI.2FGPT)
    *   [9.5 Network configuration](#Network_configuration)
        *   [9.5.1 Hostname](#Hostname)
        *   [9.5.2 Wired](#Wired)
        *   [9.5.3 Wireless](#Wireless_2)
*   [10 Unmount the partitions and reboot](#Unmount_the_partitions_and_reboot)
*   [11 Post-installation](#Post-installation)

## Preparation

Arch Linux should run on any [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) compatible machine with a minimum of 256 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space.

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") for instructions on downloading the installation medium, and methods for booting it to the target machine(s). This guide assumes you use the latest available version.

As the installation process retrieves packages from a remote repository, these methods require an internet connection; see [Offline installation of packages](/index.php/Offline_installation_of_packages "Offline installation of packages") when none is available.

## Boot the installation medium

Point the current boot device to the drive containing the Arch installation media. This is typically achieved by pressing a key during the [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") phase, as indicated on the splash screen. Refer to your motherboard's manual for details.

When the Arch menu appears, select *Boot Arch Linux* and press `Enter` to enter the installation environment. See [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) for a list of [boot parameters](/index.php/Kernel_parameters#Configuration "Kernel parameters"). For example, when planning to install large packages not included in the medium **before** installation, increase the default COW space reserved in memory with `cow_spacesize=` to [prevent kernel locks](/index.php/Pacman#pacman_crashes_the_official_installation_media "Pacman").

If the live system fails to launch, see [Boot problems](/index.php/Boot_problems "Boot problems") for possible workarounds.

You will be logged in as the root user and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt. *Zsh* provides advanced [tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html) and other features as part of the [grml config](http://grml.org/zsh/). For modifying or creating configuration files, [nano](/index.php/Nano#Usage "Nano") and [vim](/index.php/Vim#Usage "Vim") are suggested.

### UEFI mode

In case you have a [UEFI](/index.php/UEFI "UEFI") motherboard with UEFI mode enabled, the CD/USB will automatically launch Arch Linux via [systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/).

To verify you are booted in UEFI mode, run:

```
# efivar -l

```

See [UEFI#UEFI_Variables](/index.php/UEFI#UEFI_Variables "UEFI") for details.

### Keyboard layout

The default [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") is set to [us](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available choices can be listed with `localectl list-keymaps`.

For example, to change the layout to `de-latin1`, run:

```
# loadkeys *de-latin1*

```

If certain characters appear as white squares or other symbols, change the [console font](/index.php/Console_fonts "Console fonts"). For example:

```
# setfont *lat9w-16*

```

## Establish an internet connection

The [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon is enabled on boot, and will attempt to start a wired connection. The [ELinks](/index.php/ELinks "ELinks") browser is included with the installation media, and can be used to access captive portal login forms.

Should [checking the connection](/index.php/Network_configuration#Check_the_connection "Network configuration") with *ping* fail, configure the network as explained below. See [Category:Network configuration](/index.php/Category:Network_configuration "Category:Network configuration") for other methods, such as a modem connection.

To preserve settings, copy modified configuration files to the new system before [configuring the base system](#Configure_the_base_system).

### Wireless

Use [netctl](/index.php/Netctl "Netctl")'s *wifi-menu* to list available networks and make a connection:

```
# wifi-menu

```

If your computer has more than one Wi-Fi device, list the [wireless devices](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration") with `iw dev`. Names are likely to start with `wl`, for example `wlp3s0`. Relay the name to *wifi-menu*:

```
# wifi-menu *wlp3s0*

```

For networks which require both a username and password, see [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

See [Wireless](/index.php/Wireless "Wireless") for more information.

### Wired (Static IP)

A [static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration") is only required when regular [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") is not supported, or used by the network.

When configuring a static profile with *dhcpcd*, it is typically required to set the `interface`, `static ip_address`, `static routers` and `statics domain_name_servers` variables in `/etc/dhcpcd.conf`. Examples are available in `man dhcpcd.conf` and [Dhcpcd#Static profile](/index.php/Dhcpcd#Static_profile "Dhcpcd").

[Interface names](/index.php/Network_configuration#Device_names "Network configuration") can be identified by issuing `ip link`. For ethernet interfaces, names are likely to start with `en`, for example `enp0s25`.

When finished, restart `dhcpcd.service`:

```
# systemctl restart dhcpcd.service

```

## Update the system clock

Use [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") to ensure that your system clock is accurate. To start it:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`. See [Time](/index.php/Time "Time") for more information.

## Prepare the storage devices

**Warning:**

*   In general, partitioning or formatting will make existing data inaccessible and subject to being overwritten, i.e. destroyed, by subsequent operations. For this reason, all data that needs to be preserved must be backed up before proceeding.
*   If dual-booting with an existing installation of Windows on a UEFI/GPT system, avoid reformatting the UEFI partition, as this includes the Windows *.efi* file required to boot it. Furthermore, Arch must follow the same firmware boot mode and partitioning combination as Windows. See [Windows and Arch dual boot#Important information](/index.php/Windows_and_Arch_dual_boot#Important_information "Windows and Arch dual boot").

In this step, the storage devices that will be used by the new system will be prepared. Read [Partitioning](/index.php/Partitioning "Partitioning") for a more general overview.

Users intending to create stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), should keep those instructions into consideration when preparing the partitions. If intending to install to a USB flash key, see [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

### Identify the devices

The first step is to identify the devices where the new system will be installed. The following command will show all the available devices:

```
# lsblk

```

This will list all devices connected to your system along with their partition schemes, including that used to host and boot live Arch installation media (e.g. a USB drive). Not all devices listed will therefore be viable or appropriate mediums for installation. Results ending in `rom`, `loop` or `airoot` can be ignored.

Devices (e.g. hard disks) will be listed as `sd*x*`, where `*x*` is a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. Existing partitions on those devices will be listed as `sd*xY*`, where `*Y*` is a number starting from `1` for the first partition, `2` for the second, and so on. In the example below, only one device is available (`sda`), and that device uses only one partition (`sda1`):

```
NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda               8:0    0    80G  0 disk
└─sda1            8:1    0    80G  0 part

```

The `sd*xY*` convention will be used in the examples provided below for partition tables, partitions, and file systems. As they are just examples, it is important to ensure that any necessary changes to device names, partition numbers, and/or partition sizes (etc.) are made. Do not just blindly copy and paste the commands.

If the existing partition scheme needs not be changed, skip to [#File systems and swap](#File_systems_and_swap), otherwise continue reading the following section.

### Partition table types

If you are installing alongside an existing installation (i.e. dual-booting), a partition table will already be in use. If the devices are not partitioned, or the current partitions table or scheme needs to be changed, you will first have to determine the partition tables (one for each device) in use or to be used.

There are two types of partition table:

*   [MBR](/index.php/MBR "MBR")
*   [GPT](/index.php/GPT "GPT")

Any existing partition table can be identified with the following command for each device:

```
# parted /dev/sd*x* print

```

### Partitioning tools

**Warning:** Using a partitioning tool that is incompatible with your partition table type will likely result in the destruction of that table, along with any existing partitions/data.

For each device to be partitioned, a proper tool must be chosen according to the partition table to be used. Several partitioning tools are provided by the Arch installation medium, including:

*   [parted](/index.php/Parted "Parted"): MBR and GPT
*   [fdisk](/index.php/Fdisk#Fdisk_usage_summary "Fdisk"), **cfdisk**, **sfdisk**: MBR and GPT
*   [gdisk](/index.php/Gdisk#Gdisk_usage_summary "Gdisk"), **cgdisk**, **sgdisk**: GPT

Devices may also be partitioned before booting the installation media, for example through tools such as [GParted](/index.php/GParted "GParted") (also provided as a [live CD](http://gparted.sourceforge.net/livecd.php)).

#### Using parted in interactive mode

All the examples provided below make use of *parted*, as it can be used for both BIOS/MBR and UEFI/GPT. It will be launched in *interactive mode*, which simplifies the partitioning process and reduces unnecessary repetition by automatically applying all partitioning commands to the specified device.

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

To then create a new MBR/msdos partition table for BIOS systems, use the following command:

```
(parted) mklabel msdos

```

To create a new GPT partition table for UEFI systems instead, use:

```
(parted) mklabel gpt

```

### Partition schemes

You can decide the number and size of the partitions the devices should be split into, and which directories will be used to mount the partitions in the installed system (also known as *mount points*). The mapping from partitions to directories is the [partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning"), which must comply with the following requirements:

*   At least a partition for the `/` (*root*) directory **must** be created.
*   When using a UEFI motherboard, one [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") **must** be created.

In the examples below it is assumed that a new and contiguous partitioning scheme is applied to a single device. Some optional partitions will also be created for the `/boot` and `/home` directories: see also [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") for an explanation of the purpose of the various directories; if separate partitions for directories like `/boot` or `/home` are not created, these will simply be contained in the `/` partition. Also the creation of an optional partiton for [swap space](/index.php/Swap_space "Swap space") will be illustrated.

If not already open in a *parted* interactive session, open each device to be partitioned with:

```
# parted /dev/sd*x*

```

The following command will be used to create partitions:

```
(parted) mkpart *part-type* *fs-type* *start* *end*

```

*   `*part-type*` is one of `primary`, `extended` or `logical`, and is meaningful only for MBR partition tables.
*   `*fs-type*` is an identifier chosen among those listed by entering `help mkpart` as the closest match to the file system that you will use in [#File systems and swap](#File_systems_and_swap). The *mkpart* command does not actually create the file system: the `*fs-type*` parameter will simply be used by *parted* to set a 1-byte code that is used by boot loaders to "preview" what kind of data is found in the partition, and act accordingly if necessary. See also [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

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

### File systems and swap

Once the partitions have been created, each must be formatted with an appropriate [file system](/index.php/File_system "File system"), *except* for swap partitions. All available partitions on the intended installation device can be listed with the following command:

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

## Select a mirror

You may want to edit the `mirrorlist` file and place your preferred mirror first. A copy of this file will be installed on your new system by *pacstrap* as well, so it is worth getting it right.

 `# nano /etc/pacman.d/mirrorlist` 
```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on YYYY-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

If you want, you can make it the *only* mirror available by deleting all other lines, but it is usually a good idea to have a few more, in case the first one goes offline. Should you change your mirror list at a later stage, refresh all package lists with `pacman -Syyu`. See [Mirrors](/index.php/Mirrors "Mirrors") for more information.

## Install the base system

The *pacstrap* script installs the base system. To build packages from the [AUR](/index.php/AUR "AUR") or with [ABS](/index.php/ABS "ABS"), the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group is also required.

```
# pacstrap -i /mnt base base-devel

```

The `-i` switch ensures prompting before package installation. Other packages can later be [installed](/index.php/Install "Install") with *pacman*.

See the [pacman](/index.php/Pacman#Troubleshooting "Pacman") and [pacman-key](/index.php/Pacman-key#Troubleshooting "Pacman-key") articles in case of errors.

## Generate an fstab

[UUIDs](https://en.wikipedia.org/wiki/Universally_unique_identifier "wikipedia:Universally unique identifier") are used because they have certain advantages (see [Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")). If you prefer labels instead, replace the `-U` option with `-L`:

```
# genfstab -U /mnt > /mnt/etc/fstab

```

The `fstab` file should always be checked after generating it, and edited in case of errors. See [Field definitions](/index.php/Fstab#Field_definitions "Fstab") for syntax information.

```
# cat /mnt/etc/fstab

```

## Configure the base system

[Change root](/index.php/Change_root "Change root") into the new system:

```
# arch-chroot /mnt /bin/bash

```

The close following and understanding of these steps is key to a properly configured system. Tools from the live installation, such as *dialog* and *wpa_supplicant*, are **not** automatically installed. The following sections specify such cases.

### Locale

The [Locale](/index.php/Locale "Locale") defines which language the system uses, and other regional considerations such as currency denomination, numerology, and character sets.

Possible values are listed in `/etc/locale.gen`. Uncomment `en_US.UTF-8 UTF-8`, as well as other needed localisations. `UTF-8` is highly recommended over other options.

 `# nano /etc/locale.gen` 
```
...
#en_SG ISO-8859-1
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...

```

Before locales can be enabled, they must be [generated](/index.php/Locale#Generating_locales "Locale"):

```
# locale-gen

```

Create `/etc/locale.conf`, where `LANG` refers to the *first column* of an uncommented entry in `/etc/locale.gen`:

 `# nano /etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [changed the keyboard layout](#Keyboard_layout), make the changes persistent in `/etc/vconsole.conf`. For example, if `de-latin1` was set with *loadkeys*, and `lat9w-16` with *setfont*, assign the `KEYMAP` and `FONT` variables:

 `# nano /etc/vconsole.conf` 
```
KEYMAP=*de-latin1*
FONT=*lat9w-16*
```

### Time

[Time zones](/index.php/Time#Time_zone "Time") are available in the `/usr/share/zoneinfo` directory. Select a timezone:

```
# tzselect

```

Create the symbolic link `/etc/localtime`, where `Zone/Subzone` is the `TZ` value from *tzselect*:

```
# ln -sf /usr/share/zoneinfo/*Zone*/*SubZone* /etc/localtime

```

It is highly recommended to set the [Time standard](/index.php/Time_standard "Time standard") to UTC, and adjust the [Time skew](/index.php/Time_skew "Time skew"):

```
# hwclock --systohc --utc

```

If other operating systems are installed on the machine, they must be configured accordingly.

### Initramfs

As [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of [linux](https://www.archlinux.org/packages/?name=linux) with *pacstrap*, most users can use the defaults provided in `mkinitcpio.conf`.

For special configurations, set the correct [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") in `/etc/mkinitcpio.conf` and [re-generate](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") the initramfs image:

```
# mkinitcpio -p linux

```

### Boot loader

See [Boot loaders](/index.php/Boot_loaders "Boot loaders") for available choices and configurations. If you have an Intel CPU, [microcode](/index.php/Microcode "Microcode") updates **must** be configured after installing the boot loader.

#### BIOS/MBR

Install the [grub](https://www.archlinux.org/packages/?name=grub) package. To search for other operating systems, also install [os-prober](https://www.archlinux.org/packages/?name=os-prober):

```
# pacman -S grub os-prober

```

Install the bootloader to the *drive* Arch was installed to:

```
# grub-install --recheck */dev/sda*

```

Generate `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

See [GRUB](/index.php/GRUB "GRUB") for more information.

#### UEFI/GPT

Here, the installation drive is assumed to be GPT-partioned, and have the [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (gdisk type `EF00`, formatted with FAT32) mounted at `/boot`.

*bootctl* is part of systemd, and as such part of the base installation.

```
# bootctl install

```

Create a boot entry in `/boot/loader/entries/arch.conf`, replacing `/dev/sda2` with the **root** partition:

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sda2** rw
```

Modify `/boot/loader/loader.conf` to select the default entry (without `.conf`) suffix:

 `# nano /boot/loader/loader.conf` 
```
timeout 3
default arch
```

See [systemd-boot](/index.php/Systemd-boot "Systemd-boot") for more information.

### Network configuration

Configure the network for the newly installed environment. The procedure is similar to [#Establish an internet connection](#Establish_an_internet_connection), except made persistent for subsequent boots. Select **one** daemon to handle the network.

#### Hostname

Set the [hostname](/index.php/Hostname "Hostname") to your liking:

```
# echo *myhostname* > /etc/hostname

```

Add the same hostname to `/etc/hosts`:

 `# nano /etc/hosts` 
```
#<ip-address> <hostname.domain.org> <hostname>
127.0.0.1 localhost.localdomain localhost *myhostname*
::1   localhost.localdomain localhost *myhostname*
```

#### Wired

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") is the default method in the install medium, and part of the base installation. When only requiring a single wired connection, enable the *dhcpcd* service:

```
# systemctl enable dhcpcd@*interface*.service

```

Where `*interface*` is an ethernet [device name](/index.php/Network_configuration#Device_names "Network configuration"). If static IP settings are required, adjust the profile configuration as described in [#Wired (Static IP)](#Wired_.28Static_IP.29).

See [Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") for more information.

#### Wireless

For wireless, *dhcpcd* and *systemd-networkd* require a separate configuration of the connection in the wireless backend, [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), first. If you anticipate to connect the machine to different wireless networks over time, a tool which provides its own connection management may be easier to handle. Aside from [netctl](/index.php/Netctl "Netctl") introduced below, [Wireless#Automatic setup](/index.php/Wireless#Automatic_setup "Wireless") lists other choices.

Wireless chipset firmware packages (for cards which require them) are pre-installed under `/usr/lib/firmware` in the live environment, but must be installed separately on the new system. See [Wireless#Installing driver/firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless") for details.

	Using wifi-menu

Install [iw](https://www.archlinux.org/packages/?name=iw) and [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), which you will need to connect to a network, and [dialog](https://www.archlinux.org/packages/?name=dialog) which is required for *wifi-menu*:

```
# pacman -S iw wpa_supplicant dialog

```

If you used *wifi-menu* in the [#Wireless](#Wireless) section, repeat the steps **after** finishing the rest of this installation and rebooting. Using wifi-menu now will not work because a process spawned by this command will conflict with the one you have running outside of the chroot.

See [Netctl](/index.php/Netctl "Netctl") for more information.

## Unmount the partitions and reboot

Set the root [password](/index.php/Password "Password") with:

```
# passwd

```

Exit from the chroot environment:

```
# exit

```

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
This document is a guide for installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") from the live system booted with the official installation image. Before installing, it would be advised to view the [FAQ](/index.php/FAQ "FAQ"). For conventions used in this document, see [Help:Reading](/index.php/Help:Reading "Help:Reading"). In particular, code examples may contain placeholders (formatted in `*italics*`) that must be replaced manually.

For more detailed instructions, see the respective [ArchWiki](/index.php/ArchWiki "ArchWiki") articles or the various programs' [man pages](/index.php/Man_page "Man page"), both linked from this guide. For interactive help, the [IRC channel](/index.php/IRC_channel "IRC channel") and the [forums](https://bbs.archlinux.org/) are also available.

Arch Linux should run on any [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64")-compatible machine with a minimum of 512 MiB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MiB of disk space. As the installation process needs to retrieve packages from a remote repository, this guide assumes a working internet connection is available.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pre-installation](#Pre-installation)
    *   [1.1 Verify signature](#Verify_signature)
    *   [1.2 Boot the live environment](#Boot_the_live_environment)
    *   [1.3 Set the keyboard layout](#Set_the_keyboard_layout)
    *   [1.4 Verify the boot mode](#Verify_the_boot_mode)
    *   [1.5 Connect to the internet](#Connect_to_the_internet)
    *   [1.6 Update the system clock](#Update_the_system_clock)
    *   [1.7 Partition the disks](#Partition_the_disks)
        *   [1.7.1 Example layouts](#Example_layouts)
    *   [1.8 Format the partitions](#Format_the_partitions)
    *   [1.9 Mount the file systems](#Mount_the_file_systems)
*   [2 Installation](#Installation)
    *   [2.1 Select the mirrors](#Select_the_mirrors)
    *   [2.2 Install the base packages](#Install_the_base_packages)
*   [3 Configure the system](#Configure_the_system)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Localization](#Localization)
    *   [3.5 Network configuration](#Network_configuration)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root password](#Root_password)
    *   [3.8 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## Pre-installation

The installation media and their [GnuPG](/index.php/GnuPG "GnuPG") signatures can be acquired from the [Download](https://archlinux.org/download/) page.

### Verify signature

It is recommended to verify the image signature before use, especially when downloading from an *HTTP mirror*, where downloads are generally prone to be intercepted to [serve malicious images](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html).

On a system with [GnuPG](/index.php/GnuPG "GnuPG") installed, do this by downloading the *PGP signature* (under *Checksums*) to the ISO directory, and [verifying](/index.php/GnuPG#Verify_a_signature "GnuPG") it with:

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

Alternatively, from an existing Arch Linux installation run:

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

**Note:**

*   The signature itself could be manipulated if it is downloaded from a mirror site, instead of from [archlinux.org](https://archlinux.org/download/) as above. In this case, ensure that the public key, which is used to decode the signature, is signed by another, trustworthy key. The `gpg` command will output the fingerprint of the public key.
*   Another method to verify the authenticity of the signature is to ensure that the public key's fingerprint is identical to the key fingerprint of the [Arch Linux developer](https://www.archlinux.org/people/developers/) who signed the ISO-file. See [Wikipedia:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") for more information on the public-key process to authenticate keys.

### Boot the live environment

The live environment can be booted from a [USB flash drive](/index.php/USB_flash_installation_media "USB flash installation media"), an [optical disc](/index.php/Optical_disc_drive#Burning "Optical disc drive") or a network with [PXE](/index.php/PXE "PXE"). For alternative means of installation, see [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

*   Pointing the current boot device to a drive containing the Arch installation media is typically achieved by pressing a key during the [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") phase, as indicated on the splash screen. Refer to your motherboard's manual for details.
*   When the Arch menu appears, select *Boot Arch Linux* and press `Enter` to enter the installation environment.
*   See [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) for a list of [boot parameters](/index.php/Kernel_parameters#Configuration "Kernel parameters"), and [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) for a list of included packages.
*   You will be logged in on the first [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") as the root user, and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt.

To switch to a different console—for example, to view this guide with [ELinks](/index.php/ELinks "ELinks") alongside the installation—use the `Alt+*arrow*` [shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts"). To [edit](/index.php/Textedit "Textedit") configuration files, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") and [vim](/index.php/Vim#Usage "Vim") are available.

### Set the keyboard layout

The default [console keymap](/index.php/Console_keymap "Console keymap") is [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available layouts can be listed with:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

To modify the layout, append a corresponding file name to [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitting path and file extension. For example, to set a [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") keyboard layout:

```
# loadkeys de-latin1

```

[Console fonts](/index.php/Console_fonts "Console fonts") are located in `/usr/share/kbd/consolefonts/` and can likewise be set with [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verify the boot mode

If UEFI mode is enabled on an [UEFI](/index.php/UEFI "UEFI") motherboard, [Archiso](/index.php/Archiso "Archiso") will [boot](/index.php/Boot "Boot") Arch Linux accordingly via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). To verify this, list the [efivars](/index.php/UEFI#UEFI_variables "UEFI") directory:

```
# ls /sys/firmware/efi/efivars

```

If the directory does not exist, the system may be booted in [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or CSM mode. Refer to your motherboard's manual for details.

### Connect to the internet

To set up a network connection, go through the following steps:

1.  Ensure your [network interface](/index.php/Network_interface "Network interface") is listed and enabled, for example with [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
2.  Connect to the network. Plug in the Ethernet cable or [connect to the wireless LAN](/index.php/Wireless_network_configuration "Wireless network configuration").
3.  Configure your network connection:
    *   [Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration")
    *   Dynamic IP address: use [DHCP](/index.php/DHCP "DHCP").

    **Note:** The installation image enables [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`) for [wired network devices](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) on boot.

4.  The connection may be verified with [ping](https://en.wikipedia.org/wiki/ping "wikipedia:ping"): `# ping archlinux.org` 

### Update the system clock

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) to ensure the system clock is accurate:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

### Partition the disks

When recognized by the live system, disks are assigned to a [block device](/index.php/Block_device "Block device") such as `/dev/sda` or `/dev/nvme0n1`. To identify these devices, use [lsblk](/index.php/Lsblk "Lsblk") or *fdisk*.

```
# fdisk -l

```

Results ending in `rom`, `loop` or `airoot` may be ignored.

The following [partitions](/index.php/Partition "Partition") are **required** for a chosen device:

*   One partition for the root directory `/`.
*   If [UEFI](/index.php/UEFI "UEFI") is enabled, an [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

If you want to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [system encryption](/index.php/Dm-crypt "Dm-crypt") or [RAID](/index.php/RAID "RAID"), do it now.

#### Example layouts

| BIOS with [MBR](/index.php/MBR "MBR") |
| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | Suggested size |
| `/mnt` | `/dev/sd*X*1` | Linux | Remainder of the device |
| [SWAP] | `/dev/sd*X*2` | Linux swap | More than 512 MiB |
| UEFI with [GPT](/index.php/GPT "GPT") |
| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | Suggested size |
| `/mnt/boot` or `/mnt/efi` | `/dev/sd*X*1` | [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Remainder of the device |
| [SWAP] | `/dev/sd*X*3` | Linux swap | More than 512 MiB |

See also [Partitioning#Example layouts](/index.php/Partitioning#Example_layouts "Partitioning").

**Note:**

*   Use [fdisk](/index.php/Fdisk "Fdisk") or [parted](/index.php/Parted "Parted") to modify partition tables, for example `fdisk /dev/sd*X*`.
*   [Swap](/index.php/Swap "Swap") space can be set on a [swap file](/index.php/Swap_file "Swap file") for file systems supporting it.

### Format the partitions

Once the partitions have been created, each must be formatted with an appropriate [file system](/index.php/File_system "File system"). For example, if the root partition is on `/dev/sd*X*1` and will contain the `*ext4*` file system, run:

```
# mkfs.*ext4* /dev/sd*X1*

```

If you created a partition for swap, initialize it with *mkswap*:

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for details.

### Mount the file systems

[Mount](/index.php/Mount "Mount") the file system on the root partition to `/mnt`, for example:

```
# mount /dev/sd*X1* /mnt

```

Create any remaining mount points (such as `/mnt/efi`) and mount their corresponding partitions.

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

This group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) or specific wireless firmware; see [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) for comparison.

To [install](/index.php/Install "Install") packages and other groups such as [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), append the names to *pacstrap* (space separated) or to individual [pacman](/index.php/Pacman "Pacman") commands after the [#Chroot](#Chroot) step.

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

Set the [time zone](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Run [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) to generate `/etc/adjtime`:

```
# hwclock --systohc

```

This command assumes the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). See [System time#Time standard](/index.php/System_time#Time_standard "System time") for details.

### Localization

Uncomment `en_US.UTF-8 UTF-8` and other needed [locales](/index.php/Locale "Locale") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Create the [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) file, and set the `LANG` [variable](/index.php/Variable "Variable") accordingly:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Network configuration

Create the [hostname](/index.php/Hostname "Hostname") file:

 `/etc/hostname` 
```
*myhostname*

```

Add matching entries to [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

If the system has a permanent IP address, it should be used instead of `127.0.1.1`.

Complete the [network configuration](/index.php/Network_configuration "Network configuration") for the newly installed environment.

### Initramfs

Creating a new *initramfs* is usually not required, because [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of the [linux](https://www.archlinux.org/packages/?name=linux) package with *pacstrap*.

For [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [system encryption](/index.php/Dm-crypt "Dm-crypt") or [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), modify [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) and recreate the initramfs image:

```
# mkinitcpio -p linux

```

### Root password

Set the root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader

Choose and install a Linux-capable [boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process"). If you have an Intel or AMD CPU, enable [microcode](/index.php/Microcode "Microcode") updates in addition.

## Reboot

Exit the chroot environment by typing `exit` or pressing `Ctrl+d`.

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").
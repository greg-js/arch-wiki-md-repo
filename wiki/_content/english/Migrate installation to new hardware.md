This article discusses the steps required for moving an Arch Linux system to new hardware. The goal is to achieve the same ArchLinux installation, as far as installed software and configuration is concerned.

There are two different approaches to migrating an installation:

1.  *Bottom to Top*: Install a fresh Arch Linux system on the new hardware, afterwards restore the installed packages and configuration files.
2.  *Top to Bottom*: Clone the old harddrive to the new harddrive, or place the old harddrive into the new system; modify configuration files where necessary.

Which way you choose depends heavily on how the new system differs from your old and how exact you want to reproduce the system.

**Warning:** Some of the following instructions can be dangerous: you are advised to backup all of your important data on the old system before continuing.

## Contents

*   [1 Bottom to Top](#Bottom_to_Top)
    *   [1.1 On the old system](#On_the_old_system)
        *   [1.1.1 What software?](#What_software.3F)
        *   [1.1.2 Copy to some backup space.](#Copy_to_some_backup_space.)
    *   [1.2 On the new system](#On_the_new_system)
        *   [1.2.1 Wiki articles](#Wiki_articles)
        *   [1.2.2 Copy from backup space](#Copy_from_backup_space)
        *   [1.2.3 Install software](#Install_software)
*   [2 Top to Bottom](#Top_to_Bottom)
    *   [2.1 Move the system to the new HDDs](#Move_the_system_to_the_new_HDDs)
        *   [2.1.1 Update fstab](#Update_fstab)
    *   [2.2 Reconfigure the bootloader](#Reconfigure_the_bootloader)
    *   [2.3 Regenerate kernel image](#Regenerate_kernel_image)
    *   [2.4 Update the graphic drivers](#Update_the_graphic_drivers)
    *   [2.5 Reconfigure audio](#Reconfigure_audio)
    *   [2.6 Reconfigure network](#Reconfigure_network)
*   [3 See also](#See_also)

## Bottom to Top

### On the old system

#### What software?

```
$ pacman -Qqe | grep -vx "$(pacman -Qqm)" > Packages
$ pacman -Qqm > Packages.aur

```

gives you a nice list of explicitly installed packages. Don't forget the software *not* installed through pacman (also see [AUR FAQ](/index.php/Arch_User_Repository#Why_has_foo_disappeared_from_the_AUR.3F "Arch User Repository")). You may also use the following script to give you a better overview of the binaries and libraries installed unbeknownst to pacman (e. g. installed via Steam, Desura or using their own install methods):

```
find / -regextype posix-extended -regex "/(sys|srv|proc)|.*/\.ccache/.*" -prune -o -type f \
-exec bash -c 'file "{}" | grep -E "(32|64)-bit"' \; | \
awk -F: '{print $1}' | \
while read -r bin; \
do pacman -Qo "$bin" &>/dev/null || echo "$bin"; \
done

```

#### Copy to some backup space.

*   You can consider backing up /var/cache/pacman/pkg if you do not change architectures (example: from x86 to x86_64)
*   /etc should be backed up, in order to peek if necessary.

### On the new system

#### Wiki articles

*   Read some Wiki articles concerning new hardware, for examples your new [SSD](/index.php/SSD "SSD").
*   Stick to the well-written installation guidelines here in this wiki. Since you are experienced, the [Installation guide](/index.php/Installation_guide "Installation guide") could be enough.
*   Try to configure as much as possible sticking to *current* wiki articles and forum posts.

#### Copy from backup space

*   Copy the pacman cache to var/cache/pacman/pkg
*   Don't forget to edit /etc/pacman.d/mirrorlist

#### Install software

As root, grab a cup of coffee and execute:

```
# xargs -a Packages pacman -S --noconfirm --needed

```

## Top to Bottom

*   See these forum threads:
    *   [https://bbs.archlinux.org/viewtopic.php?id=71038](https://bbs.archlinux.org/viewtopic.php?id=71038)
    *   [https://bbs.archlinux.org/viewtopic.php?pid=543214](https://bbs.archlinux.org/viewtopic.php?pid=543214)

### Move the system to the new HDDs

**Note:** If you are planning to keep the hard drive where the system is already installed, you can skip this section.

There are two fundamental methods for copying data between two disks, cloning an entire disk, and copying single files. For details see [Disk cloning](/index.php/Disk_cloning "Disk cloning"). If you want to clone the entire disk, it is required to use a live cd to do so.

At the same time there are many different methods for how to transport the data between the two drives:

*   Connect origin and destination HDDs to the same computer, either the old or the new one. Data link: old HDD -> computer -> new HDD.
*   Make use of temporary storage devices like external HDDs, or cloud backups. Data link: old HDD -> old computer -> storage -> new computer -> new HDD.
*   Transfer data over network, for example with [rsync](/index.php/Rsync "Rsync"). Data link: old HDD -> old computer -> network -> new computer -> new HDD.

For the first two options, consider that you might need adapters to connect the HDDs (PATA->SATA, USB-HDD-Cases, etc.), and choose a connection that is sufficiently fast. The last two options require you to use a live system on the new computer, as it is not possible to boot from the new harddrive at this point.

#### Update fstab

*   using /dev paths: this should change depending on how the new drives are connected to the mainboard, on the BIOS and on the new partitions scheme
*   using fs labels: should be safe
*   using UUIDs

### Reconfigure the bootloader

*   because of:
    *   new HDD and partitions configuration
    *   new BIOS configuration
*   GRUB allows to edit entries with 'e'
*   use a live system?
*   update framebuffer mode (if new gpu)

### Regenerate kernel image

*   initially the Fallback image could work
*   regenerate image
    *   mkinitcpio -p linux

### Update the graphic drivers

*   if changed driver (e.g. from ATI to NVIDIA) can uninstall the old drivers

### Reconfigure audio

*   alsamixer volume
    *   save settings

### Reconfigure network

*   if need to change hostname:
    *   [hostnamectl](/index.php/Network_configuration#Set_the_hostname "Network configuration")
    *   /etc/hosts
    *   other apps using hostname: synergy, nut (network ups tools)
        *   "`# grep -Ri 'hostname' /etc`" should give some hints on the files to be updated

## See also

*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")
*   [Howto clone a linux system](http://positon.org/clone-a-linux-system-install-to-another-computer)
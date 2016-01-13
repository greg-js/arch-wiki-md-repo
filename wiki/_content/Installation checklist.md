# Installation checklist

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

**This article is being considered for redirection to [Installation guide](/index.php/Installation_guide "Installation guide").**

**Notes:** Serves the same purpose (Discuss in [Talk:Installation checklist#](https://wiki.archlinux.org/index.php/Talk:Installation_checklist))

This page is an install checklist meant to be printed out or referred to by experienced users who do not require a detailed install guide.

1.  Get the install media and boot it. [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")
2.  Set keyboard layout with `loadkeys _keymap_file_`
3.  Connect to the internet. [Network_configuration](/index.php/Network_configuration "Network configuration")
4.  Update the clock with `timedatectl set-ntp true` see [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")
5.  Partition the disks. [Partitioning](/index.php/Partitioning "Partitioning")
6.  Format partitions. For ext4 the command would be `mkfs.ext4 /dev/sdxY` more informatino here: [File_systems#Create_a_filesystem](/index.php/File_systems#Create_a_filesystem "File systems")
7.  Mount the paritions. `mount /dev/sdxY /mnt`
8.  Select mirrors in `/etc/pacman.d/mirrorlist` see [Mirrors](/index.php/Mirrors "Mirrors")
9.  Install the base packages with `pacstrap /mnt base base-devel`
10.  Generate fstab file with `genfstab -U /mnt > /mnt/etc/fstab`
11.  Chroot to the new system `arch-chroot /mnt`
12.  Set hostname with `echo computer_name > /etc/hostname`
13.  Edit `/etc/locale.conf` and generate locals `locale-gen`
14.  Set the timezone. `ln -s /usr/share/zoneinfo/zone/subzone /etc/localtime`
15.  Configure keymap and fonts in `/etc/vconsole.conf`
16.  Generate Initramfs `mkinitcpio -p linux`
17.  Configure the network for new install
18.  Set root password with `passwd`
19.  Install and configure boot loader. More info: [Boot loaders](/index.php/Boot_loaders "Boot loaders")
20.  Reboot

Retrieved from "[https://wiki.archlinux.org/index.php?title=Installation_checklist&oldid=415065](https://wiki.archlinux.org/index.php?title=Installation_checklist&oldid=415065)"
# Multiboot USB drive

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GRUB](/index.php/GRUB "GRUB")
*   [Syslinux](/index.php/Syslinux "Syslinux")
*   [Archiso](/index.php/Archiso "Archiso")

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [Multiboot disk images](/index.php?title=Multiboot_disk_images&action=edit&redlink=1 "Multiboot disk images (page does not exist)").**

**Notes:** See discussion (Discuss in [Talk:Multiboot USB drive#Scope and title](https://wiki.archlinux.org/index.php/Talk:Multiboot_USB_drive#Scope_and_title))

A multiboot USB flash drive allows booting multiple ISO files from a single device. The ISO files can be copied to the device and booted directly without unpacking them first. There are multiple methods available, but they may not work for all ISO images.

## Contents

*   [1 Using GRUB and loopback devices](#Using_GRUB_and_loopback_devices)
    *   [1.1 Preparation](#Preparation)
    *   [1.2 Installing GRUB](#Installing_GRUB)
    *   [1.3 Configuring GRUB](#Configuring_GRUB)
    *   [1.4 Boot entries](#Boot_entries)
        *   [1.4.1 Alt Linux](#Alt_Linux)
        *   [1.4.2 Arch Linux](#Arch_Linux)
            *   [1.4.2.1 monthly release](#monthly_release)
            *   [1.4.2.2 archboot](#archboot)
        *   [1.4.3 CentOS](#CentOS)
            *   [1.4.3.1 Stock installation medium](#Stock_installation_medium)
            *   [1.4.3.2 Desktop live medium](#Desktop_live_medium)
        *   [1.4.4 Clonezilla Live](#Clonezilla_Live)
        *   [1.4.5 Debian](#Debian)
            *   [1.4.5.1 Stock install medium](#Stock_install_medium)
            *   [1.4.5.2 Live install medium](#Live_install_medium)
        *   [1.4.6 Elementary OS](#Elementary_OS)
        *   [1.4.7 Fedora](#Fedora)
            *   [1.4.7.1 Stock installation medium](#Stock_installation_medium_2)
            *   [1.4.7.2 Workstation live medium](#Workstation_live_medium)
        *   [1.4.8 Gentoo](#Gentoo)
            *   [1.4.8.1 Desktop LiveDVD](#Desktop_LiveDVD)
        *   [1.4.9 GParted Live](#GParted_Live)
        *   [1.4.10 Kali Linux](#Kali_Linux)
        *   [1.4.11 Knoppix](#Knoppix)
        *   [1.4.12 Linux Mint](#Linux_Mint)
        *   [1.4.13 openSUSE](#openSUSE)
            *   [1.4.13.1 Stock installation medium](#Stock_installation_medium_3)
            *   [1.4.13.2 Desktop Live medium](#Desktop_Live_medium_2)
        *   [1.4.14 Parabola GNU/Linux-libre](#Parabola_GNU.2FLinux-libre)
        *   [1.4.15 Sabayon](#Sabayon)
        *   [1.4.16 Slackware Linux](#Slackware_Linux)
        *   [1.4.17 SystemRescueCD](#SystemRescueCD)
        *   [1.4.18 Ubuntu](#Ubuntu)
        *   [1.4.19 Slitaz](#Slitaz)
        *   [1.4.20 Slax](#Slax)
        *   [1.4.21 Tails](#Tails)
*   [2 Chainloading Windows](#Chainloading_Windows)
*   [3 Using Syslinux and memdisk](#Using_Syslinux_and_memdisk)
    *   [3.1 Preparation](#Preparation_2)
    *   [3.2 Install the memdisk module](#Install_the_memdisk_module)
    *   [3.3 Configuration](#Configuration)
    *   [3.4 Caveat for 32-bit systems](#Caveat_for_32-bit_systems)
*   [4 See also](#See_also)

## Using GRUB and loopback devices

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** multiple [style](/index.php/Help:Style "Help:Style") issues (Discuss in [Talk:Multiboot USB drive#](https://wiki.archlinux.org/index.php/Talk:Multiboot_USB_drive))

advantages:

*   only a single partition required
*   all ISO files are found in one directory
*   adding and removing ISO files is simple

disadvantages:

*   not all ISO images are compatible
*   the original boot menu for the ISO file is not shown
*   it can be difficult to find a working boot entry

### Preparation

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** How much extra space is needed for the bootloader? (Discuss in [Talk:Multiboot USB drive#](https://wiki.archlinux.org/index.php/Talk:Multiboot_USB_drive))

Create at least one partition and a filesystem supported by [GRUB](/index.php/GRUB "GRUB") on the USB drive. See [Partitioning](/index.php/Partitioning "Partitioning") and [File systems#Create a filesystem](/index.php/File_systems#Create_a_filesystem "File systems"). Choose the size based on the total size of the ISO files that you want to store on the drive, and plan for extra space for the bootloader.

### Installing GRUB

Mount the filesystem located on the USB drive:

```
# mount /dev/sdXY /mnt

```

Create the directory /boot:

```
# mkdir /mnt/boot

```

Install grub on the USB drive:

```
# grub-install --target=i386-pc --recheck --boot-directory=/mnt/boot /dev/sdX

```

In case you want to boot ISOs in UEFI mode, you have to install grub for the UEFI target:

```
# grub-install --target x86_64-efi --efi-directory /mnt --boot-directory=/mnt/boot --removable

```

For UEFI, the partition has to be the first one in an MBR partition table and formatted with FAT32.

### Configuring GRUB

For the purpose of multiboot USB drive it is easier to edit `grub.cfg` by hand instead of generating it. Alternatively, make the following changes in `/etc/grub.d/40_custom` or `/mnt/boot/grub/custom.cfg` and generate `/mnt/boot/grub/grub.cfg` using [grub-mkconfig](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

As it is recommend to use a [persistent name](/index.php/Persistent_block_device_naming "Persistent block device naming") instead of `/dev/sd_xY_` to identify the partition on the USB drive where the image files are located, define a variable for convenience to hold the value. If the ISO images are on the same partition as grub, use the following to read the UUID at boot time:

 `/mnt/boot/grub/grub.cfg` 

```
# path to the partition holding ISO images (using UUID)
probe -u $root --set=rootuuid
set imgdevpath="/dev/disk/by-uuid/$rootuuid"
```

Or specify the UUID explicitly:

 `/mnt/boot/grub/grub.cfg` 

```
# path to the partition holding ISO images (using UUID)
set imgdevpath="/dev/disk/by-uuid/_UUID_value_"
```

Alternatively, use the device label instead of UUID:

 `/mnt/boot/grub/grub.cfg` 

```
# path to the partition holding ISO images (using labels)
set imgdevpath="/dev/disk/by-label/_label_value_"
```

The necessary UUID or label can be found using `lsblk -f`. Do not use the same label as the Arch ISO for the USB device, otherwise the boot process will fail.

To complete the configuration, a boot entry for each ISO image has to be added below this header, see the next section for examples.

### Boot entries

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** The only boxes used should be code blocks, otherwise the section will be unreadable. Anything else should be plain text. (Discuss in [Talk:Multiboot USB drive#](https://wiki.archlinux.org/index.php/Talk:Multiboot_USB_drive))

It is assumed that the ISO images are stored in the `boot/iso/` directory on the same filesystem where GRUB is installed. Otherwise it would be necessary to prefix the path to ISO file with device identification when using the `loopback` command, for example `loopback loop **(hd1,2)**$isofile`. As this identification of devices is not [persistent](/index.php/Persistent_block_device_naming "Persistent block device naming"), it is not used in the examples in this section.

One can use persistent block device naming like this:

```
# define globally (i.e outside any menuentry)
insmod search_fs_uuid
search --no-floppy --set=**isopart** --fs-uuid d6de9100-1981-11e5-9fb9-74867a652f05         # your iso fs uuid here
# later use inside each menuentry instead
loopback loop **($isopart)**$isofile
```

**Tip:** For a list of kernel parameters, see [https://www.kernel.org/doc/Documentation/kernel-parameters.txt](https://www.kernel.org/doc/Documentation/kernel-parameters.txt) (still incomplete)

#### Alt Linux

*   Initramfs framework: ???
*   Live framework: ???
*   Init system: ???

```
menuentry "[loopback]altlinux-7.0.5-simply-x86_64-install-dvd5.iso" {
        set gfxpayload=keep
	insmod gzio
	insmod part_msdos
	insmod ext2
	insmod xfs
        set bootpart=uuid:df46d821-e7f9-4e35-bbd2-728bdce8d89a
        set isodir=/boot/iso
        set isofile=altlinux-7.0.5-simply-x86_64-install-dvd5.iso
        loopback loop (${root})${isodir}/${isofile}
        linux (loop)/syslinux/alt0/vmlinuz automatic=method:disk,${bootpart},directory:${isodir}/${isofile} ramdisk_size=183210 changedisk lang=ru_RU splash noeject xdriver=auto quiet=1 showopts
        initrd (loop)/syslinux/alt0/full.cz
}
```

#### Arch Linux

**Tip:** If you want to boot into a 32-bit system, replace `x86_64` with `i686`.

##### monthly release

*   Initramfs framework: [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") (cmdline: [[1]](https://projects.archlinux.org/mkinitcpio.git/tree/man/mkinitcpio.8.txt#n212))
*   Live framework: [archiso](/index.php/Archiso "Archiso") (cmdline: [[2]](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams))
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[3]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry '[loopback]archlinux-2014.12.01-dual.iso' {
	set isofile='/boot/iso/archlinux-2014.12.01-dual.iso'
	loopback loop $isofile
	linux (loop)/arch/boot/**x86_64**/vmlinuz archisodevice=/dev/loop0 img_dev=$imgdevpath img_loop=$isofile
	initrd (loop)/arch/boot/**x86_64**/archiso.img
}
```

**Note:** As of archiso v23 (monthly release 2015.10.01), the parameter `archisodevice=/dev/loop0` is no longer necessary when boot using GRUB and loopback devices.

##### archboot

*   Initramfs framework: [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") (cmdline: [[4]](https://projects.archlinux.org/mkinitcpio.git/tree/man/mkinitcpio.8.txt#n212))
*   Live framework: [archboot](/index.php/Archboot "Archboot") (cmdline: none? _RFD_)
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[5]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry '[loopback]archlinux-2014.11-1-archboot' {
	set isofile='/boot/iso/archlinux-2014.11-1-archboot.iso'
	loopback loop $isofile
	linux (loop)/boot/vmlinuz_**x86_64** iso_loop_dev=$imgdevpath iso_loop_path=$isofile
	initrd (loop)/boot/initramfs_**x86_64**.img
}
```

#### CentOS

##### Stock installation medium

*   Initramfs framework: [Dracut](https://fedoraproject.org/wiki/Dracut) (cmdline: [[6]](https://git.kernel.org/cgit/boot/dracut/dracut.git/tree/dracut.cmdline.7.asc))
*   Installation program: [Anaconda](https://fedoraproject.org/wiki/Anaconda) (cmdline: [[7]](https://github.com/rhinstaller/anaconda/blob/master/docs/boot-options.rst))
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[8]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry "[loopback]CentOS-7.0-1406-x86_64-**DVD**" {
	set isofile='/boot/iso/CentOS-7.0-1406-x86_64-**DVD**.iso'
	loopback loop $isofile
	linux (loop)/isolinux/vmlinuz noeject inst.stage2=hd:**/dev/sdb2**:/$isofile
	initrd (loop)/isolinux/initrd.img
}
```

**Tip:** The boot parameter of second stage install image location `/dev/sdb2` which is used by Anaconda, is similar to [fstab](/index.php/Fstab "Fstab")'s first field (fs_spec), could be replaced with one of:

*   `/dev/sd_**xY**_`
*   `LABEL=MYUSBSTICK`
*   `UUID=00000000-0000-0000-0000-0000deadbeef`

For example, `linux (loop)/isolinux/vmlinuz noeject inst.stage2=hd:**LABEL=MYUSBSTICK**:/$isofile`.

When using some special disk label (e.g. GPT), it's also possible to use `PARTUUID=` and/or `PARTLABEL=`.

##### Desktop live medium

*   Initramfs framework: [Dracut](https://fedoraproject.org/wiki/Dracut) (cmdline: [[9]](https://git.kernel.org/cgit/boot/dracut/dracut.git/tree/dracut.cmdline.7.asc))
*   Live framework: fedora [livecd-tools](https://fedoraproject.org/wiki/FedoraLiveCD) (cmdline: none)
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[10]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry '[loopback]CentOS-7.0-1406-x86_64-GnomeLive' {
	set isofile='/boot/iso/CentOS-7.0-1406-x86_64-GnomeLive.iso'
	loopback loop $isofile
	linux (loop)/isolinux/vmlinuz0 root=live:CDLABEL=CentOS-7-live-GNOME-x86_64 iso-scan/filename=$isofile rd.live.image
	initrd (loop)/isolinux/initrd0.img
}
```

#### Clonezilla Live

**Tip:** Since 2014.01.05[[11]](https://projects.archlinux.org/archiso.git/commit/?id=5cd02c704046cdb6974f6b10f0cac366eeebec0e), the Arch Linux monthly release contains clonezilla.

*   Initramfs framework: [initramfs-tools](https://anonscm.debian.org/cgit/kernel/initramfs-tools.git/) (cmdline: _RFD_)
*   Live framework: [Debian Live](http://live.debian.net/) (cmdline: [[12]](http://manpages.debian.org/cgi-bin/man.cgi?query=live-boot&apropos=0&sektion=7&manpath=Debian+unstable+sid&format=html&locale=en))
*   Init system: [sysvinit](https://savannah.nongnu.org/projects/sysvinit) (cmdline: _RFD_)

```
menuentry "[loopback]clonezilla-live-2.2.3-25-amd64" {
	set isofile="/boot/iso/clonezilla-live-2.2.3-25-amd64.iso"
	loopback loop $isofile
	linux (loop)/live/vmlinuz findiso=$isofile boot=live union=overlay username=user config
	initrd (loop)/live/initrd.img
}
```

#### Debian

##### Stock install medium

*   Initramfs framework: [initramfs-tools](https://anonscm.debian.org/cgit/kernel/initramfs-tools.git/) (cmdline: _RFD_)
*   Installation program: [debian-installer](https://wiki.debian.org/DebianInstaller#Development) (cmdline: _exists but missing online documentation_)
*   Init system: [sysvinit](https://savannah.nongnu.org/projects/sysvinit) (cmdline: _RFD_)

**Tip:** To install debian from any stock install medium on a non-optical medium (e.g. usb stick, HDD), it's necessary to use a different initramfs instead of the default one on the installation medium which is located at `(loop)/install.amd/initrd.gz`. If you boot with the default one, the installer will unable to find or mount the proper iso image for installation. Please download the initramfs for hard disk installation from [an official mirror site](https://mirrors.kernel.org/debian/dists/stable/main/installer-amd64/current/images/hd-media/initrd.gz), put it in the same directory with the image file and give it a suitable name (`debian-7.8.0-amd64-DVD-1.hdd.initrd.gz` in this example).

```
menuentry '[loopback]debian-7.8.0-amd64-DVD-1' {
	set isofile='/boot/iso/debian-7.8.0-amd64-DVD-1.iso'
	set initrdfile='/boot/iso/debian-7.8.0-amd64-DVD-1.hdd.initrd.gz'
	loopback loop $isofile
	linux (loop)/install.amd/vmlinuz vga=791 iso-scan/ask_second_pass=true iso-scan/filename=$isofile
	initrd $initrdfile
}
```

##### Live install medium

*   Initramfs framework: [initramfs-tools](https://anonscm.debian.org/cgit/kernel/initramfs-tools.git/) (cmdline: _RFD_)
*   Live framework: [Debian Live](http://live.debian.net/) (cmdline: [[13]](http://manpages.debian.org/cgi-bin/man.cgi?query=live-boot&apropos=0&sektion=7&manpath=Debian+unstable+sid&format=html&locale=en))
*   Init system: [sysvinit](https://savannah.nongnu.org/projects/sysvinit) (cmdline: _RFD_)

```
menuentry '[loopback]debian-live-7.8.0-amd64-xfce-desktop' {
	set isofile='/boot/iso/debian-live-7.8.0-amd64-xfce-desktop.iso'
	loopback loop $isofile
	linux (loop)/live/vmlinuz boot=live config fromiso=**/dev/sdb2**/$isofile
	initrd (loop)/live/initrd.img
}
```

**Note:** It's also OK to use `findiso=$isofile` instead of the longer `fromiso=/dev/disk/by-.../.../$isofile`. Anyway, using `fromiso=` instead of `findiso=` may speed up the initialization progress because it avoids unnecessary mounting.

#### Elementary OS

*   Initramfs framework: _RFD_
*   Live framework or installation program: _RFD_
*   Init system: upstart (cmdline: _RFD_)

```
menuentry '[loopback]elementaryos-freya-amd64.20150411' {
	set isofile='/boot/iso/elementaryos-freya-amd64.20150411.iso'
	loopback loop $isofile
	linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile locale=**en_US.UTF-8**
	initrd (loop)/casper/initrd.lz
}
```

#### Fedora

##### Stock installation medium

*   Initramfs framework: [Dracut](https://fedoraproject.org/wiki/Dracut) (cmdline: [[14]](https://git.kernel.org/cgit/boot/dracut/dracut.git/tree/dracut.cmdline.7.asc))
*   Installation program: [Anaconda](https://fedoraproject.org/wiki/Anaconda) (cmdline: [[15]](https://github.com/rhinstaller/anaconda/blob/master/docs/boot-options.rst))
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[16]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry '[loopback]Fedora-20-x86_64-DVD' {
	set isofile='/boot/iso/Fedora-20-x86_64-DVD.iso'
	loopback loop $isofile
	linux (loop)/isolinux/vmlinuz noeject inst.stage2=hd:**/dev/sdb2**:/$isofile
	initrd (loop)/isolinux/initrd.img
}
```

##### Workstation live medium

*   Initramfs framework: [Dracut](https://fedoraproject.org/wiki/Dracut) (cmdline: [[17]](https://git.kernel.org/cgit/boot/dracut/dracut.git/tree/dracut.cmdline.7.asc))
*   Live framework: fedora [livecd-tools](https://fedoraproject.org/wiki/FedoraLiveCD) (cmdline: none)
*   Init system: [systemd](/index.php/Systemd "Systemd") (cmdline: [[18]](http://www.freedesktop.org/software/systemd/man/kernel-command-line.html))

```
menuentry '[loopback]Fedora-Live-Workstation-x86_64-21-5' {
	set isofile='/boot/iso/Fedora-Live-Desktop-x86_64-21-5.iso'
	loopback loop $isofile
	linux (loop)/isolinux/vmlinuz0 root=live:CDLABEL=Fedora-Live-WS-x86_64-21-5 iso-scan/filename=$isofile rd.live.image
	initrd (loop)/isolinux/initrd0.img
}
```

#### Gentoo

##### Desktop LiveDVD

*   Initramfs framework: [genkernel](https://wiki.gentoo.org/wiki/Genkernel) (cmdline: [[19]](https://gitweb.gentoo.org/proj/genkernel.git/tree/doc/genkernel.8.txt#n393))
*   Live framework: [livecd-tools](https://gitweb.gentoo.org/proj/livecd-tools.git/) (cmdline: _RFD_)
*   Init system: [OpenRC](https://wiki.gentoo.org/wiki/Project:OpenRC) (cmdline: _RFD_)

```
menuentry "[loopback]livedvd-amd64-multilib-20140826" {
	set isofile="/boot/iso/livedvd-amd64-multilib-20140826.iso"
	loopback loop $isofile
	linux (loop)/isolinux/gentoo root=/dev/ram0 init=/linuxrc aufs looptype=squashfs loop=/image.squashfs cdroot isoboot=$isofile vga=**791** splash=silent,theme:default console=tty0
	initrd (loop)/isolinux/gentoo.igz 
}
```

**Tip:** This should also works for minimal medium.

#### GParted Live

*   Initramfs framework: [initramfs-tools](https://anonscm.debian.org/cgit/kernel/initramfs-tools.git/) (cmdline: _RFD_)
*   Live framework: [Debian Live](http://live.debian.net/) (cmdline: [[20]](http://manpages.debian.org/cgi-bin/man.cgi?query=live-boot&apropos=0&sektion=7&manpath=Debian+unstable+sid&format=html&locale=en))
*   Init system: [sysvinit](https://savannah.nongnu.org/projects/sysvinit) (cmdline: _RFD_)

```
menuentry "[loopback]gparted-live-0.22.0-2-**amd64**" {
	set isofile="/boot/iso/gparted-live-0.22.0-2-**amd64**.iso"
	loopback loop $isofile
	linux (loop)/live/vmlinuz boot=live union=overlay username=user config components quiet noswap noeject toram=filesystem.squashfs ip=  nosplash findiso=$isofile
	initrd (loop)/live/initrd.img
}
```

#### Kali Linux

*   Initramfs framework: [initramfs-tools](https://anonscm.debian.org/cgit/kernel/initramfs-tools.git/) (cmdline: _RFD_)
*   Live framework: [Debian Live](http://live.debian.net/) (cmdline: [[21]](http://manpages.debian.org/cgi-bin/man.cgi?query=live-boot&apropos=0&sektion=7&manpath=Debian+unstable+sid&format=html&locale=en))
*   Init system: [sysvinit](https://savannah.nongnu.org/projects/sysvinit) (cmdline: _RFD_)

```
menuentry "[loopback]kali-linux-1.0.7-**amd64**" {
	set isofile='/boot/iso/kali-linux-1.0.7-**amd64**.iso'
	loopback loop $isofile
	linux (loop)/live/vmlinuz boot=live findiso=$isofile noconfig=sudo username=root hostname=kali
	initrd (loop)/live/initrd.img
}
```

#### Knoppix

*   Initramfs framework: _Unknown_
*   Live framework: _Unknown_
*   Init system: _Unknown_

```
menuentry "[loopback]KNOPPIX_V7.4.2DVD-2014-09-28-EN" {
        set isofile="/boot/iso/KNOPPIX_V7.4.2DVD-2014-09-28-EN.iso"
        loopback loop $isofile
        linux (loop)/boot/isolinux/linux bootfrom=/mnt-iso/$isofile acpi=off keyboard=us lang=us
        initrd (loop)/boot/isolinux/minirt.gz
}
```

#### Linux Mint

*   Initramfs framework: _RFD_
*   Live framework or installation program: _RFD_
*   Init system: _RFD_

```
menuentry "[loopback]linuxmint-201403-cinnamon-dvd-**32**bit" {
	set isofile="/boot/iso/linuxmint-201403-cinnamon-dvd-**32**bit.iso"
	loopback loop $isofile
	linux (loop)/live/vmlinuz isofrom=**/dev/sdb2**/iso/$isofile boot=live live-config live-media-path=/live quiet splash noeject noprompt
	initrd (loop)/live/initrd.img
}
```

If you boot with the above configuration and get the error message '/live/vmlinuz not found' try the below

```
menuentry "Linux Mint 17.2 Cinnamon LTS RC (x64)" {
    set iso=/boot/iso/linuxmint-17.2-cinnamon-64bit.iso
    loopback loop $iso
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$iso noeject noprompt 
    initrd (loop)/casper/initrd.lz
}
```

#### openSUSE

##### Stock installation medium

*   Initramfs framework: _RFD_
*   Live framework or installation program: Kiwi? _RFD_
*   Init system: _RFD_

```
menuentry '[loopback]openSUSE-13.1-DVD-x86_64' {
	set isofile='/boot/iso/openSUSE-13.1-DVD-x86_64.iso'
	loopback loop $isofile
	linux (loop)/boot/x86_64/loader/linux install=hd:$isofile
	initrd (loop)/boot/x86_64/loader/initrd
}
```

##### Desktop Live medium

*   Initramfs framework: _RFD_
*   Live framework or installation program: Kiwi? _RFD_
*   Init system: _RFD_

```
menuentry '[loopback]openSUSE-13.1-KDE-Live-x86_64' {
	set isofile='/boot/iso/openSUSE-13.1-KDE-Live-x86_64.iso'
	loopback loop $isofile
	linux (loop)/boot/x86_64/loader/linux isofrom_device=$imgdevpath isofrom_system=$isofile LANG=**en_US.UTF-8**
	initrd (loop)/boot/x86_64/loader/initrd
}
```

#### Parabola GNU/Linux-libre

**Tip:** If you want to boot into a 32-bit system, replace `x86_64` with `i686`.

```
menuentry '[loopback]parabola-2015.07.01-dual.iso' {
	set isofile='/boot/iso/parabola-2015.07.01-dual.iso'
	loopback loop $isofile
	linux (loop)/parabola/boot/**x86_64**/vmlinuz parabolaisolabel=PARA_**201507** img_dev=$imgdevpath img_loop=$isofile earlymodules=loop
	initrd (loop)/parabola/boot/**x86_64**/parabolaiso.img
}
```

**Tip:** The label string after `parabolaisolabel=` needs to be edited when a newer release is used.

#### Sabayon

*   Initramfs framework: genkernel? _RFD_
*   Live framework or installation program: _RFD_
*   Init system: openrc? _RFD_

```
menuentry '[loopback]Sabayon_Linux_14.05_amd64_KDE' {
	set isofile='/boot/iso/Sabayon_Linux_14.05_amd64_KDE.iso'
	loopback loop $isofile
	linux (loop)/boot/sabayon root=/dev/ram0 aufs cdroot locale=**en_US** loop=/livecd.squashfs looptype=squashfs isoboot=$isofile
	initrd (loop)/boot/sabayon.igz
}
```

#### Slackware Linux

*   Initramfs framework: _RFD_
*   Live framework or installation program: _RFD_
*   Init system: _RFD_

```
menuentry '[loopback]slackware64-14.1-install-dvd' {
	set isofile='/boot/iso/slackware64-14.1-install-dvd.iso'
	loopback loop $isofile
	linux (loop)/kernels/huge.s/bzImage printk.time=0
	initrd (loop)/isolinux/initrd.img
}
```

#### SystemRescueCD

*   Initramfs framework: _RFD_
*   Live framework or installation program: _RFD_
*   Init system: _RFD_

**Note:** Replace `64` with `32` if you want to boot into a 32-bit system.

```
menuentry '[loopback]systemrescuecd-x86-4.5.2' {
	set isofile='/boot/iso/systemrescuecd-x86-4.5.2.iso'
	loopback loop $isofile
	linux (loop)/isolinux/rescue**64** isoloop=$isofile
	initrd (loop)/isolinux/initram.igz
}
```

#### Ubuntu

*   Initramfs framework: _RFD_
*   Live framework or installation program: _RFD_
*   Init system: upstart (cmdline: _RFD_)

```
menuentry '[loopback]ubuntu-14.04.1-desktop-amd64' {
	set isofile='/boot/iso/ubuntu-14.04.1-desktop-amd64.iso'
	loopback loop $isofile
	linux (loop)/casper/vmlinuz.efi boot=casper iso-scan/filename=$isofile locale=**en_US.UTF-8**
	initrd (loop)/casper/initrd.lz
}
```

#### Slitaz

*   Initramfs framework: _RFD_
*   Live framework: _RFD_
*   Init system: _RFD_

First, download slitaz iso, then extract somewhere (in this case, /live/slitaz-4.0 on /dev/sda3)

```
menuentry 'slitaz-4.0 core' {
	set dir='/live/slitaz-4.0'
	set root=(hd0,msdos3)
	set lang='pt_BR'
	set kmap='br-abnt2'
	linux ($root)/$dir/bzImage lang=$lang kmap=$kmap rw root=/dev/null vga=normal autologin
	initrd ($root)/$dir/rootfs4.gz ($root)/$dir/rootfs3.gz ($root)/$dir/rootfs2.gz ($root)/$dir/rootfs1.gz
}
```

#### Slax

*   Initramfs framework: _RFD_
*   Live framework: _RFD_
*   Init system: _RFD_

First, download Slax zip (for USB), then extract somewhere (in this case, /live/slax on /dev/sda3)

```
menuentry 'slax' {
	set dir=/live/slax
	set root=(hd0,msdos3)
	linux $dir/boot/vmlinuz from=$dir vga=normal load_ramdisk=1 prompt_ramdisk=0 printk.time=0 slax.flags=perch,xmode
	initrd $dir/boot/initrfs.img
}
```

#### Tails

*   Initramfs framework: _Unknown_
*   Live framework: _Unknown_
*   Init system: _Unknown_

Simply download and verify integrity of the Tails iso.

```
menuentry "[loopback]tails-i386-1.5.iso" {
    set isofile='/boot/iso/tails-i386-1.5.iso'
    loopback loop $isofile
    linux (loop)/live/vmlinuz2 boot=live config findiso=${isofile} live-media=removable apparmor=1 security=apparmor nopersistent noprompt timezone=Etc/UTC block.events_dfl_poll_msecs=1000 noautologin module=Tails
    initrd (loop)/live/initrd2.img
}
```

**Warning:** Emergency memory erasure does not seem to work when booting this way.

Remove the `live-media=removable` option if the iso file is not on removable media.

## Chainloading Windows

It can be very difficult to loopback a Windows install disc. One simple solution that allows you to install a variety of platforms from a USB drive with a single, unified partition is to start with a working, bootable Windows USB drive, and to replace its bootloader with GRUB.

Before installing GRUB, rename or move the Windows bootloader. It should be the default _.efi_ executable - located at `_(USB)_/efi/boot/bootx64.efi` for a 64-bit system. Install GRUB in its place, and ensure that it is now the default executable.

You can then chainload the renamed Windows bootloader from GRUB, and also configure GRUB to loopback _.iso_ files as described above.

```
menuentry '[chain]en_windows_8.1_professional_x64' {
	insmod chain
        chainloader /efi/boot/bootx64.efi.windows
}
```

## Using Syslinux and memdisk

Using the [memdisk](http://www.syslinux.org/wiki/index.php/MEMDISK) module, the ISO image is loaded into memory, and its bootloader is loaded. Make sure that the system that will boot this USB drive has sufficient amount of memory for the image file and running operating system.

### Preparation

Make sure that the USB drive is properly [partitioned](/index.php/Partitioning "Partitioning") and that there is a partition with [file system](/index.php/File_system "File system") supported by Syslinux, for example fat32 or ext4\. Then install Syslinux to this partition, see [Syslinux#Installation](/index.php/Syslinux#Installation "Syslinux").

### Install the memdisk module

The memdisk module was not installed during Syslinux installation, it has to be installed manually. Mount the partition where Syslinux is installed to `/mnt/` and copy the memdisk module to the same directory where Syslinux is installed:

```
# cp /usr/lib/syslinux/bios/memdisk /mnt/boot/syslinux/

```

### Configuration

After copying the ISO files on the USB drive, edit the [Syslinux configuration file](/index.php/Syslinux#Configuration "Syslinux") and create menu entries for the ISO images. The basic entry looks like this:

 `boot/syslinux/syslinux.cfg` 

```
LABEL _some_label_
    LINUX memdisk
    INITRD _/path/to/image.iso_
    APPEND iso

```

See [memdisk on Syslinux wiki](http://www.syslinux.org/wiki/index.php/MEMDISK) for more configuration options.

### Caveat for 32-bit systems

When booting a 32-bit system from an image larger than 128MiB, it is necessary to increase the maximum memory usage of vmalloc. This is done by adding `vmalloc=_value_M` to the kernel parameters, where `_value_` is larger than the size of the ISO image in MiB.[[22]](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

For example when booting the 32-bit system from the [Arch installation ISO](https://www.archlinux.org/download/), press the `Tab` key over the `Boot Arch Linux (i686)` entry and add `vmalloc=768M` at the end. Skipping this step will result in the following error during boot:

```
modprobe: ERROR: could not insert 'phram': Input/output error

```

## See also

*   GRUB:
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot/Examples](https://help.ubuntu.com/community/Grub2/ISOBoot/Examples)
    *   [https://help.ubuntu.com/community/Grub2/ISOBoot](https://help.ubuntu.com/community/Grub2/ISOBoot)
*   Syslinux:
    *   [Boot an ISO image](http://www.syslinux.org/wiki/index.php/Boot_an_Iso_image)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Multiboot_USB_drive&oldid=409365](https://wiki.archlinux.org/index.php?title=Multiboot_USB_drive&oldid=409365)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")
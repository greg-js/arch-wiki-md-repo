Archboot is an unofficial set of scripts to generate bootable media for CD/USB/PXE, designed for installation or rescue operation.

It only runs in RAM, without any special filesystems like squashfs, thus it is limited to the RAM which is installed in your system.

## Contents

*   [1 Installation](#Installation)
*   [2 The difference to the archiso install media](#The_difference_to_the_archiso_install_media)
*   [3 Archboot ISO Releases](#Archboot_ISO_Releases)
    *   [3.1 Burning Release](#Burning_Release)
    *   [3.2 PXE booting / Rescue system](#PXE_booting_/_Rescue_system)
    *   [3.3 Supported boot modes of Archboot media](#Supported_boot_modes_of_Archboot_media)
    *   [3.4 How to do a remote installation with ssh?](#How_to_do_a_remote_installation_with_ssh?)
    *   [3.5 Interactive setup features](#Interactive_setup_features)
    *   [3.6 FAQ, Known Issues and limitations](#FAQ,_Known_Issues_and_limitations)
    *   [3.7 History](#History)
    *   [3.8 Bugs](#Bugs)
*   [4 Archboot BETA ISO Release](#Archboot_BETA_ISO_Release)
*   [5 Links](#Links)
*   [6 Howto: Create image files](#Howto:_Create_image_files)
    *   [6.1 Requirements](#Requirements)
    *   [6.2 Create archboot chroots](#Create_archboot_chroots)
    *   [6.3 Install archboot and update to latest packages](#Install_archboot_and_update_to_latest_packages)
    *   [6.4 Generate images](#Generate_images)

## Installation

[Install](/index.php/Install "Install") the [archboot](https://www.archlinux.org/packages/?name=archboot) package.

## The difference to the archiso install media

*   It provides an additional interactive setup and quickinst script.
*   It contains [core] repository on media.
*   It runs a modified Arch Linux system in initramfs.
*   It is restricted to RAM usage, everything which is not necessary like

	man or info pages etc. is not provided.

*   It doesn't mount anything during boot process.
*   It supports remote installation through ssh.

## Archboot ISO Releases

*   Hybrid image files and torrents are provided, which include x86_64 and [core] repository,

	network labeled images don't include [core] repository.

*   Please check md5sum before using it.
*   [Download 2018.06 „2k18-R1“](https://downloads.archlinux.de/iso/archboot/2018.06) / [Changelog](ftp://ftp.archlinux.org/iso/archboot/Changelog-2018.06-1.txt) / [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=182439)

	kernel: 4.17.2-1

	pacman: 5.1.0-2

	systemd: 238.133-1

	RAM recommendations: 1500 MB

### Burning Release

Hybrid image file is a standard CD-burnable image and also a raw disk image.

*   Can be burned to CD(RW) media using most CD-burning utilities.
*   Can be raw-written to a drive using 'dd' or similar utilities. This method is intended for use with USB thumb drives.

 `'dd if=<imagefile> of=/dev/<yourdevice> bs=1M'` 

### PXE booting / Rescue system

[Download 2018.12 „2k18-R1“](https://downloads.archlinux.de/iso/archboot/2018.06/boot) needed files from the directory.

*   vmlinuz_x86_64 + initramfs_x86_64.img(x86_64)
*   intel-ucode.img (x86_64)
*   For PXE booting add the kernel and initrd to your tftp setup and you will get a running installation/rescue system.
*   For Rescue booting add an entry to your bootloader pointing to the kernel and initrd.

### Supported boot modes of Archboot media

*   It supports BIOS booting with syslinux.
*   It supports UEFI/UEFI_CD booting with [systemd-boot](/index.php/Systemd-boot "Systemd-boot") and [EFISTUB](/index.php/EFISTUB "EFISTUB").
*   It support UEFI_MIX_MODE booting with grub.
*   It supports Secure Boot with prebootloader.
*   It supports grub(2)'s iso loopback support.

	variables used (below for example):

	iso_loop_dev=PARTUUID=XXXX

	iso_loop_path=/blah/archboot.iso

```
menuentry "Archboot" --class iso {
loopback loop (hdX,X)/<archboot.iso>
linux (loop)/boot/vmlinuz_x86_64 iso_loop_dev=/dev/sdXX iso_loop_path=/<archboot.iso>
initrd (loop)/boot/initramfs_x86_64.img
}
```

*   It supports booting using syslinux's memdisk (only in BIOS mode).

```
menuentry "Archboot Memdisk" {
   linux16 /memdisk iso
   initrd16 hd(X,X)/<archboot.iso>
}
```

### How to do a remote installation with ssh?

*   During boot all network interfaces will try to obtain an IP address through dhcp.
*   root password is not set by default! If you need privacy during installation set a password.

 `'ssh root@<yourip>'` 

### Interactive setup features

*   Media and Network installation mode
*   Changing keymap and consolefont
*   Changing time and date
*   Setup network with netctl
*   Preparing storage disk, like auto-prepare, partitioning, GUID (gpt) support, 4k sector drive support etc.
*   Creation of software raid/raid partitions, lvm2 devices and luks encrypted devices
*   Supports standard linux,raid/raid_partitions,dmraid/fakeraid,lvm2 and encrypted devices
*   Filesystem support: ext2/3/4, btrfs, f2fs, nilfs2, reiserfs,xfs,jfs,ntfs-3g,vfat
*   Name scheme support: PARTUUID, PARTLABEL, FSUUID, FSLABEL and KERNEL
*   Mount support of grub(2) loopback and memdisk installation media
*   Package selection support
*   hwdetect script is used for preconfiguration
*   Auto/Preconfiguration of fstab, kms mode, ssd, mkinitcpio.conf, systemd, crypttab and mdadm.conf
*   Configuration of basic system files
*   Setting root password
*   grub(2) (BIOS and UEFI), refind-efi, systemd-boot, syslinux (BIOS and UEFI) bootloader support

### FAQ, Known Issues and limitations

*   Release specific known issues and workarounds are posted in changelog files.
*   Check also the forum threads for posted fixes and workarounds.
*   Why screen stays blank or other weird screen issues happen?

	Some hardware doesn't like the KMS activation, use radeon.modeset=0, i915.modeset=0 or nouveau.modeset=0 on boot prompt.

*   dmraid/fakeraid might be broken on some boards, support is not perfect here.

	The reason is there are so many different hardware components out there. At the moment 1.0.0rc16 is included, with latest fedora patchset, development has been stopped.

	mdadm supports some isw and ddf fakeraid chipsets, but assembling during boot is deactivated in /etc/mdadm.conf!

*   grub2 cannot detect correct bios boot order:

	It may happen that hd(x,x) entries are not correct, thus first reboot may not work.

	Reason: grub cannot detect bios boot order.

	Fix: Either change bios boot order or change menu.lst to correct entries after successful boot. This cannot be fixed it is a restriction in grub2!

*   Why is parted used in setup routine, instead of cfdisk in msdos partitiontable mode?

	parted is the only linux partition program that can handle all type of things the setup routine offers.

	cfdisk cannot handle GPT/GUID nor it can allign partitions correct with 1MB spaces for 4k sector disks.

	cfdisk is a nice tool but is too limited to be the standard partitioner anymore.

	cfdisk is still included but has to be run in another terminal.

### History

History of old releases can be found [here](ftp://ftp.archlinux.org/iso/archboot/history).

### Bugs

[Arch Linux Bugtracker](https://bugs.archlinux.org)

## Archboot BETA ISO Release

*   Hybrid image file is provided, which only supports network installation.
*   Please read the according Changelog files for RAM limitations.
*   Please check md5sum before using it.
*   No beta ISO available at the moment.

## Links

*   [GIT repository](https://projects.archlinux.org/archboot.git/)

## Howto: Create image files

(Quick regeneration of installation media with latest available core packages)

### Requirements

*   x86_64 architecture
*   ~ 3GB free space on disk

### Create archboot chroots

*   Install archboot:

```
# mkdir -p *x86_64_chroot*/var/lib/pacman
# pacman --root "*x86_64_chroot*" -Sy base --noconfirm --noprogressbar

```

*   Enter archboot x86_64 container:

```
# systemd-nspawn --capability=CAP_MKNOD --register=no -M $(uname -m) -D *x86_64_chroot*

```

### Install archboot and update to latest packages

Install [archboot](https://www.archlinux.org/packages/?name=archboot) in chroot and [update](/index.php/Pacman#Upgrading_packages "Pacman") to latest available packages.

### Generate images

```
# run in both chroots (needs quite some time ...)
archboot-allinone.sh -t
# put the generated tarballs in one directory and run (needs quite some time ...)
archboot-allinone.sh -g

```

*   Finished you get a bunch of images.
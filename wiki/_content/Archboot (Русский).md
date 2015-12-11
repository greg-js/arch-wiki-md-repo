# Archboot (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Archboot представляет собой набор скриптов для генерации загрузочного носителя для CD/USB/PXE, предназначенного для установки или восстановления системы.

Образ работает только в оперативной памяти, без каких-либо специальных файловых систем, таких как SquashFS, таким образом ограничиваясь только объёмом оперативной памяти, установленной в Вашей системе.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 The difference to the archiso install media](#The_difference_to_the_archiso_install_media)
*   [3 Archboot ISO Releases](#Archboot_ISO_Releases)
    *   [3.1 Гибридный образ](#.D0.93.D0.B8.D0.B1.D1.80.D0.B8.D0.B4.D0.BD.D1.8B.D0.B9_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7)
    *   [3.2 PXE booting / Rescue system](#PXE_booting_.2F_Rescue_system)
    *   [3.3 Поддерживаемые Archboot режимы загрузки](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_Archboot_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D1.8B_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [3.4 Как сделать удаленную установку через SSH?](#.D0.9A.D0.B0.D0.BA_.D1.81.D0.B4.D0.B5.D0.BB.D0.B0.D1.82.D1.8C_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.83.D1.8E_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D1.83_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_SSH.3F)
    *   [3.5 Возможности интерактивной настройки](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [3.6 FAQ, известные проблемы и ограничения](#FAQ.2C_.D0.B8.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B8_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.7 История](#.D0.98.D1.81.D1.82.D0.BE.D1.80.D0.B8.D1.8F)
    *   [3.8 Баги](#.D0.91.D0.B0.D0.B3.D0.B8)
*   [4 Archboot BETA ISO Release](#Archboot_BETA_ISO_Release)
*   [5 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)
*   [6 Руководство по созданию образов](#.D0.A0.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B4.D1.81.D1.82.D0.B2.D0.BE_.D0.BF.D0.BE_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D1.8E_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.B2)
    *   [6.1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [6.2 Создание archboot chroots](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_archboot_chroots)
    *   [6.3 Установка archboot и обновление пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_archboot_.D0.B8_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [6.4 Сборка образа](#.D0.A1.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)

## Установка

[Установите](/index.php/Install "Install") пакет [archboot](https://www.archlinux.org/packages/?name=archboot).

## The difference to the archiso install media

*   It provides an additional interactive setup and quickinst script.
*   It contains [core] repository on media.
*   It runs a modified Arch Linux system in initramfs.
*   It is restricted to RAM usage, everything which is not necessary like

man or info pages etc. is not provided.

*   It doesn't mount anything during boot process.
*   It supports remote installation through ssh.

## Archboot ISO Releases

*   Hybrid image files and torrents are provided, which include i686/x86_64 and [core] repository,

network labeled images don't include [core] repository.

*   Please check md5sum before using it.
*   [Download 2015.09 „2k15-R3“](https://downloads.archlinux.de/iso/archboot/2015.09) / [Changelog](ftp://ftp.archlinux.org/iso/archboot/Changelog-2015.09-1.txt) / [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=182439)

kernel: 4.2.0-3

pacman: 4.2.1-3

systemd: 226-1

RAM recommendations: 600 MB

### Гибридный образ

Файл гибридного образа можно прожечь на CD или использовать raw образ диска.

*   Can be burned to CD(RW) media using most CD-burning utilities.
*   Can be raw-written to a drive using 'dd' or similar utilities. Этот метод предназначен для записи на флэш-накопители USB.

 `'dd if=<imagefile> of=/dev/<yourdevice> bs=1M'` 

### PXE booting / Rescue system

[Download 2015.09 „2k15-R3“](https://downloads.archlinux.de/iso/archboot/2015.09/boot) needed files from the directory.

*   vmlinuz_i686 + initramfs_i686.img (i686)
*   vmlinuz_x86_64 + initramfs_x86_64.img(x86_64)
*   intel-ucode.img (x86_64/i686)
*   For PXE booting add the kernel and initrd to your tftp setup and you will get a running installation/rescue system.
*   For Rescue booting add an entry to your bootloader pointing to the kernel and initrd.

### Поддерживаемые Archboot режимы загрузки

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

### Как сделать удаленную установку через SSH?

*   Во время загрузки все сетевые интерфейсы попытаются получить IP-адрес через DHCP.
*   Пароль пользователя root по умолчанию не установлен! Для обеспечения безопасность установите пароль.

 `'ssh root@<yourip>'` 

### Возможности интерактивной настройки

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

### FAQ, известные проблемы и ограничения

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

cfdisk is still included but has to be run in an other terminal.

### История

History of old releases can be found [here](ftp://ftp.archlinux.org/iso/archboot/history).

### Баги

[Багтрекер Arch Linux](https://bugs.archlinux.org)

## Archboot BETA ISO Release

*   Hybrid image file is provided, which only supports network installation.
*   Please read the according Changelog files for RAM limitations.
*   Please check md5sum before using it.
*   No beta ISO available at the moment.

## Ссылки

*   [GIT репозитарий](https://projects.archlinux.org/archboot.git/)

## Руководство по созданию образов

(Быстрый генерация установочного носителя с последними доступными версиями базовых пакетов)

### Требования

*   Архитектура x86_64
*   ~ 3GB свободного дискового пространства

### Создание archboot chroots

*   Установка archboot:

```
# pacman -S archboot
# mkdir -p _x86_64_chroot_/var/lib/pacman
# pacman --root "_x86_64_chroot_" -Sy base --noconfirm --noprogressbar

```

*   Для контейнера i686:

```
# mkdir -p _i686_chroot_/var/lib/pacman
# linux32 pacman --root "_i686_chroot_" -Sy base --noconfirm --noprogressbar

```

*   Вход в контейнер archboot x86_64:

```
# systemd-nspawn --capability=CAP_MKNOD --register=no -M $(uname -m) -D _x86_64_chroot_

```

*   Вход в контейнер archboot i686:

```
# linux32 systemd-nspawn --capability=CAP_MKNOD --register=no -M $(uname -m) -D _i686_chroot_

```

### Установка archboot и обновление пакетов

Install in both chroots archboot:

```
# pacman -S archboot

```

Update in both chroots to latest available packages:

```
# pacman -Syu

```

### Сборка образа

```
# run in both chroots (needs quite some time ...)
archboot-allinone.sh -t
# put the generated tarballs in one directory and run (needs quite some time ...)
archboot-allinone.sh -g

```

*   Finished you get a bunch of images.

Have fun! tpowa (Archboot Developer)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Archboot_(Русский)&oldid=411478](https://wiki.archlinux.org/index.php?title=Archboot_(Русский)&oldid=411478)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [System recovery (Русский)](/index.php/Category:System_recovery_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:System recovery (Русский)")
*   [Getting and installing Arch (Русский)](/index.php/Category:Getting_and_installing_Arch_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Getting and installing Arch (Русский)")
*   [Live Arch systems (Русский)](/index.php/Category:Live_Arch_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Live Arch systems (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")
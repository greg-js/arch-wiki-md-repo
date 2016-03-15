## Contents

*   [1 WORK in progress](#WORK_in_progress)
*   [2 Wat is het?](#Wat_is_het.3F)
*   [3 De meest kale Arch Linux live media bouwen.](#De_meest_kale_Arch_Linux_live_media_bouwen.)
*   [4 Algemene (handmatig)](#Algemene_.28handmatig.29)
*   [5 Make a booteable "pendrive" that have more things than "Arch Linux"](#Make_a_booteable_.22pendrive.22_that_have_more_things_than_.22Arch_Linux.22)
*   [6 Configure our live medium](#Configure_our_live_medium)
    *   [6.1 mkinitcpio.conf](#mkinitcpio.conf)
    *   [6.2 packages.list](#packages.list)
    *   [6.3 aitab](#aitab)
        *   [6.3.1 Boot Loader](#Boot_Loader)
        *   [6.3.2 Adding a fstab](#Adding_a_fstab)
        *   [6.3.3 Finishing the root-image](#Finishing_the_root-image)
*   [7 See also](#See_also)

## WORK in progress

## Wat is het?

**Archiso** is een aantal bash scripts dat in staat is om een volledig functionerend op **Arch Linux** gebaseerde live CD/DCD en USB **images** te maken. Het is een erg basale tool en kan dus worden gebruikt voor herstell CDs, installatie CDs of live CD/DVD/USB voor een specifieke doelgroep. En wie weet wat nog meer. Simpelweg gezegd, het gaat hier over Arch op een mooie zilveren onderzetter. Hart en ziel van Archiso is **mkarchiso**. Alle opties zijn gedocumenteerd in de help output, dus direct gebruik van dit bestand zal hier niet worden besproken. Echter, deze wiki artikel zal dienen als een gids om uw eigen live media uit te rollen in een zeer korte tijd!

Door recente aanpassingen zal **Archiso** nu automatisch ISO images creeeren die ook dienen als USB images! Seperate CD/USB doelen zijn daardoor niet meer nodig.

## De meest kale Arch Linux live media bouwen.

**Note:** Werken in een schone chroot is niet nodig maar wel aangeraden

*   Installeer devtools indien nodig, mkarchroot heeft dit nodig.

```
[host] # pacman -S devtools --needed

```

*   Creëer een basis chroot om in te werken.

**Note:** prefix met linux32 als je een 32 bits omgeving wilt bouwen onder 64 bits

```
[host] # mkarchroot /tmp/chroot base

```

*   Installeer archiso onder chroot **(AUR methode)**

Halen van: [archiso-git AUR package](https://aur.archlinux.org/packages.php?ID=25996)

```
[host] # pacman -U archiso-git-YYYYMMDD-R-any.pkg.tar.xz -r /tmp/chroot

```

*   Installeer archiso **(GIT methode)**

```
[host] # pacman -S git make --needed
[host] # git clone [git://projects.archlinux.org/archiso.git](git://projects.archlinux.org/archiso.git)
[host] # make -C archiso/archiso DESTDIR=/tmp/chroot install

```

*   Chroot betreden.

**Note:** prefix met linux32 indien nodig

```
[host] # mkarchroot -r bash /tmp/chroot

```

*   Creëer een loopback device.

**Note:** mkarchroot maakt deze niet. Gebruik een ander cijfer indien niet aanwezig

```
[chroot] # mknod /dev/loop0 b 7 0

```

*   Een mirror instellen

**Note:** Verander MIRROR naar believen

```
[chroot] # echo 'Server = MIRROR/archlinux/$repo/os/$arch' >> /etc/pacman.d/mirrorlist

```

*   Installeer aditionale packages nodig voor archiso **(aleen als de GIT methode is gebruikt)**

```
[chroot] # pacman -S devtools squashfs-tools syslinux cdrkit

```

*   Bouw een basis ISO.

```
[chroot] # cp -r /usr/share/archiso/configs/baseline /tmp
[chroot] # cd /tmp/baseline
[chroot] # ./build.sh

```

*   Chroot verlaten.

```
[chroot] # exit

```

## Algemene (handmatig)

*   Een basis bestandssysteem instellen

```
mkarchiso -p "base" create work/root-image

```

*   Syslinux installeren

```
mkarchiso -p "syslinux" create work/root-image

```

*   Andere pakketten installeren (optioneel)

```
mkarchiso -p "pkg1 pkg2 pkg3 ... pkgN" create work/root-image.

```

*   Nu kunt u alles wat u wilt aanpassen aan de root-image.

```
mkarchroot -n -r bash work/root-image

```

*   Initramfs image instellen.

*   *   Create a config for mkinitcpio **mkinitcpio.conf**

```
HOOKS="base udev archiso sata filesystems"
COMPRESSION="xz"

```

*   *   Initramfs image genereren.

```
mkinitcpio -c ./mkinitcpio.conf -b work/root-image -k 2.6.39-ARCH -g work/iso/arch/boot/i686/archiso.img

```

*   Verplaats kernel naar boot/

```
mv work/root-image/boot/vmlinuz26 work/iso/arch/boot/i686

```

*   Syslinux instellen

*   *   Een werkmap ervoor aanmaken.

```
 mkdir -p work/iso/arch/boot/syslinux

```

*   *   Maak een **work/iso/arch/boot/syslinux/syslinux.cfg** bestand aan.

```
DEFAULT menu.c32
PROMPT 0
MENU TITLE Arch Linux
TIMEOUT 300

LABEL arch
MENU LABEL Arch Linux
LINUX /arch/boot/i686/vmlinuz26
INITRD /arch/boot/i686/archiso.img
APPEND archisolabel=MY_ARCH

ONTIMEOUT arch

```

*   *   Kopieëer menu.c32 die nodig is voor de vorige configuratie.

```
cp work/root-image/usr/lib/syslinux/menu.c32 work/iso/arch/boot/syslinux/

```

*   isolinux installeren (optioneel, alleen nodig voor een bootable iso)

```
mkdir work/iso/isolinux
cp work/root-image/usr/lib/syslinux/isolinux.bin work/iso/isolinux/

```

*   *   Maak een **work/iso/isolinux/isolinux.cfg** aan.

```
DEFAULT loadconfig

LABEL loadconfig
  CONFIG /arch/boot/syslinux/syslinux.cfg
  APPEND /arch/boot/syslinux/

```

*   Maak een **work/arch/aitab** bestand aan.

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>
root-image      /                     i686     xz          ext4       50%

```

*   Bouw alle bestandssysteem images die gespecificeerd zijn in aitab (.fs .fs.sfs .sfs)

```
mkarchiso prepare work

```

*   Genereer een ISO 9660 met"El Torito" boot image (optioneel)

```
mkarchiso -L "MY_ARCH" iso work "my-arch.iso"

```

## Make a booteable "pendrive" that have more things than "Arch Linux"

Copy "work/iso/arch" directory to some partition (must be booteable) that you have on the desired medium.

```
cp -r work/iso/arch /mnt/pen1

```

If partition is "vfat" run syslinux and set LABEL.

```
syslinux -i -d /mnt/pen1/arch/boot/syslinux /dev/pen1

```

**Note:** Due bug in mmove (from mtools), ldlinux.sys install fails, you can workaround with:

```
mv /mnt/pen1/arch/boot/syslinux /mnt/pen1/syslinux
syslinux -i -d /mnt/syslinux /dev/pen1
mv /mnt/pen1/ldlinux.sys /mnt/pen1/syslinux

```

```
dosfslabel /dev/pen1 MY_ARCH

```

If partition is ext2/3/4 or btrfs run extlinux and set LABEL.

```
extlinux -i /mnt/pen1/arch/boot/syslinux
e2label /dev/pen1 MY_ARCH

```

Finally install the master boot sector code.

```
cat /usr/lib/syslinux/mbr.bin > /dev/pen

```

## Configure our live medium

### mkinitcpio.conf

An *initcpio* is necessary for creating a system that is able to "wake-up" from a CD/DVD/USB.

Therefore, you should create a mkinitcpio.conf that holds a list of our hooks:

```
$ vim mkinitcpio.conf

```

A typical set of hooks for archiso looks something like this:

```
HOOKS="base udev memdisk archiso archiso_pxe_nbd archiso_loop_mnt block usb fw pcmcia filesystems usbinput"

```

This list will get you a system that can be booted off a CD/DVD or a USB device. It's worth mentioning that hardware auto-detection and things of that nature do not belong here. Only what's necessary to get the system on its feet, and out of the *initcpio* really belong here, fancier stuff can be done on the booted system anyway.

### packages.list

You'll also want to create a list of packages you want installed on your live CD system. A file full of package names, one-per-line, is the format for this. This is ***great*** for special interest live CDs, just specify packages you want and bake the image.

**Tip:** You can also create a **[custom local repository](/index.php/Custom_local_repository "Custom local repository")** for the purpose of preparing custom packages or packages from [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"). Just add your local repository at the first position (for top priority) of your build machine's **pacman.conf** and you are good to go!

### aitab

The aitab file holds information about the filesystems images that must be created by mkarchiso and mounted at initramfs stage from the archiso hook. It consists of some fields which define the behaviour of images.

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>

```

	<img>

	Image name without extension (.fs .fs.sfs .sfs).

	<mnt>

	Mount point.

	<arch>

	Architecture { i686 | x86_64 | any }.

	<sfs_comp>

	SquashFS compression type { gzip | lzo | xz }. A special value of "none" denotes no usage of SquashFS.

	<fs_type>

	Set the filesystem type of the image { ext4 | ext3 | ext2 | xfs }. A special value of "none" denotes no usage of a filesystem. In that case all files are pushed directly to SquashFS filesystem.

	<fs_size>

	An absolute value of file system image size in MiB (example: 100, 1000, 4096, etc) A relative value of file system free space [in percent] {1%..99%} (example 50%, 10%, 7%). This is an estimation, and calculated in a simple way. Space used + 10% (estimated for metadata overhead) + desired %

**Note:** Some combinations are invalid. Example both sfs_comp and fs_type are set to none

#### Boot Loader

```
DEFAULT menu.c32
PROMPT 0
MENU TITLE Arch Linux
TIMEOUT 300

LABEL arch
MENU LABEL Arch Linux
LINUX /%INSTALL_DIR%/boot/%ARCH%/vmlinuz26
INITRD /%INSTALL_DIR%/boot/%ARCH%/archiso.img
APPEND archisobasedir=%INSTALL_DIR% archisolabel=%ARCHISO_LABEL%

ONTIMEOUT arch

```

Due to the modular nature of isolinux, you are able to use lots of addons since all *.c32 files are copied and available to you. Take a look at the [official syslinux site](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) and the [archiso git repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Using said addons, it is possible to make visually attractive and complex menus. See [here](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

#### Adding a fstab

It is required to add a **fstab** file in /etc:

```
# <file system>         <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/root-image  /      auto    defaults   0       0

```

#### Finishing the root-image

Some tips that will not be covered in this article because there are other articles on this wiki that already do:

*   Adding an user.
*   Configure an *inittab* to start into X at boot time
*   Configure the *hosts* file
*   Configure *rc.conf* (no fancy modules required here)
*   Configure *sudoers*
*   Configure *rc.local*
*   Put more stuff into etc/skel
*   Put additional artworks onto the medium
*   Put arbitrary binary stuff into opt/

## See also

*   [Archiso project page](https://projects.archlinux.org/?p=archiso.git;a=summary)
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
# Asus x205ta

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Booting Arch install media](#Booting_Arch_install_media)
    *   [1.1 Creating bootia32.efi](#Creating_bootia32.efi)
    *   [1.2 Creating a bootable USB](#Creating_a_bootable_USB)
        *   [1.2.1 Adding wireless drivers to the install image](#Adding_wireless_drivers_to_the_install_image)
        *   [1.2.2 Unmount](#Unmount)
    *   [1.3 Booting the x205ta from USB](#Booting_the_x205ta_from_USB)
*   [2 Install Arch](#Install_Arch)
    *   [2.1 Enable wifi](#Enable_wifi)
    *   [2.2 Install Arch](#Install_Arch_2)
*   [3 Getting hardware working](#Getting_hardware_working)
    *   [3.1 Sound](#Sound)
    *   [3.2 Power level information (ACPI)](#Power_level_information_.28ACPI.29)
    *   [3.3 Touchpad](#Touchpad)
    *   [3.4 SD card reader](#SD_card_reader)
    *   [3.5 Special keys](#Special_keys)
    *   [3.6 Freezing](#Freezing)
    *   [3.7 Bluetooth](#Bluetooth)

## Booting Arch install media

The Asus x205ta has an exclusively 32-bit EFI bootloader. Since Arch does not include a 32-bit EFU loader in the standard install image, we need to add one. This procedure may work for other exclusively 32-bit EFI machines.

The current image (ARCH_201508) does not include the drivers for the x205ta's broadcom wireless modem, so we add those to the install image too.

### Creating bootia32.efi

Acquire the latest arch install ISO ([https://www.archlinux.org/download/](https://www.archlinux.org/download/)). Let's call this file <ISO-SOURCE>. Make note of its volume label. You can see this by running "file" on the iso file you downloaded and looking for the label in single quotes.

```
$ file <ISO-SOURCE> | sed -e "s/.*'\(.*\)'.*/\1/"

```

You'll recognise it because the convention for arch labels is: 'ARCH_<YEAR><MONTH>'.

Create a custom grub.cfg file, replacing <FS-LABEL> with the correct label for your iso.

 `grub.cfg ` 

```
insmod part_gpt
insmod part_msdos
insmod fat
insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus
insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
  insmod gfxterm
  set gfxmode="1024x768x32;auto"
  terminal_input console
  terminal_output gfxterm
fi

menuentry "Arch Linux archiso x86_64" {
  set gfxpayload=keep
  search --no-floppy --set=root --label <FS-LABEL>
  linux /arch/boot/x86_64/vmlinuz archisobasedir=arch archisolabel=<FS-LABEL> add_efi_memmap
  initrd /arch/boot/x86_64/archiso.img
}

menuentry "UEFI Shell x86_64 v2" {
  search --no-floppy --set=root --label <FS-LABEL>
  chainloader /EFI/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
  search --no-floppy --set=root --label <FS-LABEL>
  chainloader /EFI/shellx64_v1.efi
}

```

Create a grub standalone image, replacing /LOCATION/OF/ with your own path:

```
$ grub-mkstandalone -d /usr/lib/grub/i386-efi/ -O i386-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="uk" --themes="" -o "/LOCATION/OF/bootia32.efi" "boot/grub/grub.cfg=/LOCATION/OF/grub.cfg" -v

```

### Creating a bootable USB

Follow the instructions listed [here](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer#n105) under "PC-EFI (GPT) [x86_64 only]", but between steps 4 and 5, copy your custom bootia32.efi file to EFI/boot/bootia32.efi on your install medium, and add the x205ta's broadcom wifi driver to the appropriate squashfs.

In detail, that is:

Insert a usb storage device that you're happy to overwrite, noting its device node (e.g., /dev/sdb ; i.e., <DEV-TARGET>). Use gdisk to create a UFI bootable partition on the disk:

```
$ gdisk <DEV-TARGET>

```

Delete any existing partitions (repeatedly use the _d_ command until they're all gone). Add a new partition (_n_) and set its type to "ef00" when prompted. Write the changes to disk (_w_).

Update the kernel's awareness of the new partition

```
$ partprobe

```

Create a FAT32 file system on the new partition (e.g., /dev/sdb1 ; i.e., <DEV-TARGET-N>).

```
$ mkfs.vfat -F 32 -n <FS-LABEL> <DEV-TARGET-N>

```

Mount the partition (to <MNT-TARGET-N>)

```
$ mount <DEV-TARGET-N> <MNT-TARGET-N>

```

Extract the relevant parts of the arch install ISO (<ISO-SOURCE>) to your usb disk

```
$ bsdtar -x --exclude=isolinux/ --exclude=EFI/archiso/ --exclude=arch/boot/syslinux/ -f <ISO-SOURCE> -C <MNT-TARGET-N>

```

Copy your custom bootia32.efi to the usb disk

```
$ cp /LOCATION/OF/bootia32.efi <MNT-TARGET-N>/EFI/boot/bootia32.efi

```

#### Adding wireless drivers to the install image

Note, if you intend to use a wired connection during install you can skip these steps.

Get a copy of the wireless drivers and untar:

```
$ wget -qO-  [https://android.googlesource.com/platform/hardware/broadcom/wlan/+archive/master/bcmdhd/firmware/bcm43341.tar.gz](https://android.googlesource.com/platform/hardware/broadcom/wlan/+archive/master/bcmdhd/firmware/bcm43341.tar.gz) | tar xvz

```

Unsquash and mount your preferred squashfs (i386 or x64) from the arch ISO you downloaded by following the instructions these instructions: [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO").

Copy 'fw_bcm43341.bin' to '/lib/firmware/brcm/brcmfmac43340-sdio.bin' on your new bootable usb. Note the filename change.

```
$ cp /PATH/TO/fw_bcm43341.bin /PATH/TO/lib/firmware/brcm/brcmfmac43340-sdio.bin

```

Resquash the image and copy the resulting 'airootfs.sfs' to its original location on your usb install medium. Generate a new MD5 sum to sit alongside it.

#### Unmount

Unmount the usb install medium partition

```
$ umount <DEV-TARGET-N>

```

### Booting the x205ta from USB

Insert your new install medium into your x205ta.

Enter the bios by holding _F2_ while pressing the power button to turn the x205ta on. Hammering on F2 while the boot process is starting may help too. There is an alternative method to enter the bios by booting into windows and selecting the appropriate menu options ([tutorial](https://www.asus.com/support/FAQ/1008329/)), but the F2 method allows you to avoid windows entirely.

Turn off secure boot. This procedure varies between different BIOS versions. Mine was achieved by going to 'Security', and switching 'Secure Boot Control' to 'Disabled'.

Select your USB medium from the 'Boot Override' section of the 'Save & Exit' menu.

## Install Arch

### Enable wifi

The firmware for your wifi modem will not load by default. In addition to the driver we copied over, we'll need to copy over our local EFI variables:

```
$ cp /sys/firmware/efi/efivars/nvram-74b00bd9-805a-4d61-b51f-43268123d113 /lib/firmware/brcm/brcmfmac43340-sdio.txt

```

Now we can probe the wifi kernel module again to bring it up:

```
$ rmmod brcmfmac
$ modprobe brcmfmac

```

If you want to run 4.4 kernel, you must revert [this commit](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=9faac7b95ea4f9e83b7a914084cc81ef1632fd91) to get wifi working (regression in the MMC-layer)

### Install Arch

Proceed as usual.

## Getting hardware working

### Sound

There is currently no sound driver for the the x205ta's Realtek RT5648\. Keep your eye on [this](https://bugzilla.kernel.org/show_bug.cgi?id=95681) for updates. Note that while the sound does not work at the moment, it does work using an external USB audio adapter.

### Power level information (ACPI)

Before 4.2.0-1 kernel version, you must compile your own kernel with the appropriate flag ACPI_I2C_OPREGION=y (cf. [https://bugs.archlinux.org/task/44582](https://bugs.archlinux.org/task/44582))

You should have no problem with the power level information now if you obtain the latest kernel version >= 4.2.*. See [this page.](http://ifranali.blogspot.com/2015/04/installing-arch-linux-on-asus-x205ta.html)

### Touchpad

With kernel version < 4.3.* the x205ta touchpad is recognised as a mouse and so gestures (e.g., two-finger scrolling) are not recognised.

Since kernel 4.3.* a [[simpler patch](https://lkml.org/lkml/2015/8/24/647)] was merged and provides all touch/clickpad functionality out of the box.

Explicitly assigning the 'synaptics' driver to 'Elan Touchpad' in xorg.conf provides even more functionality (e.g., two-finger tap to right click, etc.)

Example:

 `/etc/X11/xorg.conf.d/elan_synaptics.conf ` 

```
Section "InputClass"
    Identifier "Elan Touchpad"
    MatchIsTouchpad "on"
    Driver "synaptics"
    Option "TapButton1" "1"
    Option "TapButton2" "3"
    Option "TapButton3" "2"
    Option "VertTwoFingerScroll" "on"
    Option "HorizTwoFingerScroll" "on"
EndSection

```

### SD card reader

The micro SD card reader will probably not work out of the box. [This page](https://wiki.debian.org/InstallingDebianOn/Asus/X205TA) contains a simple fix. First, create the file as follows:

 `/etc/modprobe.d/sdhci.conf ` 

```
# Adjustment to make micro SD card reader work
options sdhci debug_quirks=0x8000

```

Then you will have to run [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Make sure you have root privileges:

```
$ mkinitcpio -v -g /boot/initramfs-linux.img

```

This will update your initramfs file and load the new configuration you made in "sdhci.conf". You should be able to view your Micro SD card after a reboot.

With [this patch](https://lkml.org/lkml/2015/9/15/394) the card reader should work out of the box.

### Special keys

Out of the box, the only keysyms correctly sent are the audio volume keys (F10-F12). Ironic, since the sound card doesn't work. Can be conveniently remapped to control screen brightness (e.g., by calling xbacklight).

### Freezing

Some users experience regular freezes, where their x205ta can only be restarted by holding down the power button for several seconds. Some users have reported that so far kernel version 4.1.6 seems to experience fewest freezes. Freezes seem to occur less regular with the current(2015-11-02) 4.3-mainline vanilla kernel.

Setting kernel argument "intel_idle.max_cstate=1" solve the problem without affecting performance. The [kernel_parameters](/index.php/Kernel_parameters "Kernel parameters") page may help with adding to the kernel parameters.

### Bluetooth

Does not work yet.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Asus_x205ta&oldid=415290](https://wiki.archlinux.org/index.php?title=Asus_x205ta&oldid=415290)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")
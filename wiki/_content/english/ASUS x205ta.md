## Contents

*   [1 Booting Arch install media](#Booting_Arch_install_media)
    *   [1.1 Proper way of generating a bootia32.efi with grub.cfg included](#Proper_way_of_generating_a_bootia32.efi_with_grub.cfg_included)
        *   [1.1.1 Creating bootia32.efi](#Creating_bootia32.efi)
        *   [1.1.2 Creating a bootable USB](#Creating_a_bootable_USB)
            *   [1.1.2.1 Unmount](#Unmount)
    *   [1.2 OS indipendent method](#OS_indipendent_method)
    *   [1.3 Booting the x205ta from USB](#Booting_the_x205ta_from_USB)
*   [2 Install Arch](#Install_Arch)
    *   [2.1 Enable wifi](#Enable_wifi)
    *   [2.2 Install Arch](#Install_Arch_2)
*   [3 Getting hardware working on up-to-date kernels](#Getting_hardware_working_on_up-to-date_kernels)
    *   [3.1 Kernel patches](#Kernel_patches)
        *   [3.1.1 Patch history](#Patch_history)
        *   [3.1.2 AUR package with patched kernel](#AUR_package_with_patched_kernel)
    *   [3.2 Additional config](#Additional_config)
        *   [3.2.1 Freezing](#Freezing)
        *   [3.2.2 Sound](#Sound)
        *   [3.2.3 Bluetooth](#Bluetooth)
        *   [3.2.4 WIFI Breaks after resume from hibernating](#WIFI_Breaks_after_resume_from_hibernating)
*   [4 On older kernels](#On_older_kernels)
    *   [4.1 Sound](#Sound_2)
    *   [4.2 Power level information (ACPI)](#Power_level_information_.28ACPI.29)
    *   [4.3 Touchpad](#Touchpad)
    *   [4.4 SD card reader](#SD_card_reader)
        *   [4.4.1 Device support](#Device_support)
        *   [4.4.2 RPMB Partition](#RPMB_Partition)
    *   [4.5 Special keys](#Special_keys)
*   [5 See also](#See_also)

## Booting Arch install media

The Asus x205TA and x206HA have an exclusively 32-bit EFI bootloader. Since Arch does not include a 32-bit EFI loader in the standard install image, we need to add one. This procedure may work for other exclusively 32-bit EFI machines.

The current image (ARCH_201801) does include the drivers for the x205TA's broadcom wireless modem, so we need to copy efivars during boot as explained below. Adding drivers to the image is not required anymore. Booting archlinux on the x205TA can be achieved in 2 (possibly more) ways: by creating a bootia32.efi loader and modifying an existing iso, or by adding a precompiled bootia32.efi and manually starting archlinux iso from there.

### Proper way of generating a bootia32.efi with grub.cfg included

#### Creating bootia32.efi

Acquire the latest arch install ISO ([https://www.archlinux.org/download/](https://www.archlinux.org/download/)). Let us call this file <ISO-SOURCE>. Make note of its volume label. You can see this by running "file" on the iso file you downloaded and looking for the label in single quotes.

```
$ file <ISO-SOURCE> | sed -e "s/.*'\(.*\)'.*/\1/"

```

You will recognise it because the convention for arch labels is: 'ARCH_<YEAR><MONTH>'.

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

#### Creating a bootable USB

Follow the instructions listed [here](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer#n105) under "PC-EFI (GPT) [x86_64 only]", but between steps 4 and 5, copy your custom bootia32.efi file to EFI/boot/bootia32.efi on your install medium, and add the x205ta's broadcom wifi driver to the appropriate squashfs.

In detail, that is:

Insert a usb storage device that you are happy to overwrite, noting its device node (e.g., /dev/sdb ; i.e., <DEV-TARGET>). Use gdisk to create a UFI bootable partition on the disk:

```
$ gdisk <DEV-TARGET>

```

Delete any existing partitions (repeatedly use the *d* command until they are all gone). Add a new partition (*n*) and set its type to "ef00" when prompted. Write the changes to disk (*w*).

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

##### Unmount

Unmount the usb install medium partition

```
$ umount <DEV-TARGET-N>

```

### OS indipendent method

This method is not canonical and should not be used unless you are having trouble with the proper method. On the other had this procedure can be followed without compiling bootia32.efi and it might be useful to be used under Windows or any other operating system when no linux systems are around. Create a bootable usb using standard methods (es.Rufus on windows). Download a prebuilt bootia32.efi from any source you trust (es [https://github.com/jfwells/linux-asus-t100ta/blob/master/boot/bootia32.efi](https://github.com/jfwells/linux-asus-t100ta/blob/master/boot/bootia32.efi)) and copy it to /EFI/boot folder on the usb. Create a custom grub.cfg file, replacing <FS-LABEL> with the correct label for your iso as mentioned above. Copy the custom grub.cfg file to the root folder of the usb. Once booted the x205TA from the (as mentioned above) type the following command in the grub console

```
$ configfile /grub.cfg

```

Proceed to arch installation as usual.

### Booting the x205ta from USB

Insert your new install medium into your x205ta.

Enter the bios by holding *F2* while pressing the power button to turn the x205ta on. Hammering on F2 while the boot process is starting may help too. There is an alternative method to enter the bios by booting into windows and selecting the appropriate menu options ([tutorial](https://www.asus.com/support/FAQ/1008329/)), but the F2 method allows you to avoid windows entirely.

Turn off secure boot. This procedure varies between different BIOS versions. Mine was achieved by going to 'Security', and switching 'Secure Boot Control' to 'Disabled'.

Select your USB medium from the 'Boot Override' section of the 'Save & Exit' menu.

## Install Arch

### Enable wifi

The firmware for your wifi modem will not load by default. In addition to the driver we copied over, we will need to copy over our local EFI variables:

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

## Getting hardware working on up-to-date kernels

With some kernel patches on newer kernels the x205ta works. The built-in microphone does not work. (Refer to "Sound".) The Intel Baytrail CPU should be able to consume less power than it does. There are still occasional freezes possible due to the CPU power states not being properly supported. (Refer to "Freezes".)

### Kernel patches

#### Patch history

Three very elaborate threads contain the history of patches for the kernel for the x205ta: [kernel bug for baytrail power states](https://bugzilla.kernel.org/show_bug.cgi?id=109051), [kernel bug for chtrt5645](https://bugzilla.kernel.org/show_bug.cgi?id=95681) and most important [a Ubuntu forum thread](https://ubuntuforums.org/showthread.php?t=2254322) with [a patched kernel provided by harryharryharry](https://ubuntuforums.org/showthread.php?t=2254322&page=158&p=13625163#post13625163).

#### AUR package with patched kernel

AUR package [linux-x205ta](https://aur.archlinux.org/packages/linux-x205ta/) applies the patches proposed in the threads above to the standard arch kernel. Sources and references for each patch are in the PKGBUILD file. The package also downloads efivars for the wifi firmware which enables 5 GHz wifi.

Compiling the kernel with the provided config takes about one hour.

The x205ta has a limited amount of RAM, so do not extract and build the kernel in tmpfs.

Manual interventions and patches are needed on older kernels as a lot of patches came in over time. Refer to "On older kernels" below for instructions for older kernels.

### Additional config

#### Freezing

Depending on kernel versions, on an unpatched kernel, the x205ta regularly freezes, where the x205ta can only be restarted by holding down the power button for several seconds. Freezes are due to poor support for the baytrail power functions. Refer to the [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) for more info. AUR package [linux-x205ta](https://aur.archlinux.org/packages/linux-x205ta/) applies what seems to be the most effective patch.

Setting kernel argument `intel_idle.max_cstate=1` solves the problem on a patched kernel without affecting performance. Power saving functionalities should in theory be impeded using this patch and kernel parameter, but the laptop's battery life remains impressive and freezes are not frequent. The [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") page may help with adding to the kernel parameters.

#### Sound

There has recently been some success in getting the x205ta's Realtek RT5648 sound card working. The relevant patches are in Linux release 4.11 and later. Updated Alsa-lib's UCM files are available in [alsa-lib-x205ta](https://aur.archlinux.org/packages/alsa-lib-x205ta/).

In order to have working headphone jack (as of kernel 4.14) is it required to add an "options" line in any modprobe file

 `/etc/modprobe/50-x205ta.conf` 
```
options snd_soc_rt5645 quirk=0x31

```

To select headphones over speakers (which cannot be done automatically as of kernel 4.14) consider using [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

#### Bluetooth

Install a correct firmware file (e.g. `BCM43341B0_002.001.014.0122.0176.hcd` from Windows 10 driver) as `/lib/firmware/brcm/BCM43341B0.hcd`. See [this page](https://ubuntuforums.org/showthread.php?t=2254322&page=97) for more information on the hcd file.

In order to get bluetooth working create a systemd unit

 `/etc/systemd/system/btattach.service` 
```
[Unit]
Description=Btattach

[Service]
Type=simple
ExecStart=/usr/bin/btattach --bredr /dev/ttyS1 -P bcm
ExecStop=/usr/bin/killall btattach

[Install]
WantedBy=multi-user.target

```

and [enable](/index.php/Enable "Enable") the service.

Next, follow the normal steps to activate [bluetooth](/index.php/Bluetooth "Bluetooth").

#### WIFI Breaks after resume from hibernating

 `/usr/lib/systemd/system-sleep/hibernate.sh` 
```
#!/usr/bin/env bash

case $1 in
    pre)
        rmmod brcmfmac
        ;;
    post)
        modprobe brcmfmac
        ;;
esac

exit 0

```

and make the script executable.

## On older kernels

Patches came in over time. Try to use a new kernel!

### Sound

See [for a step-by-step description of how to compile Pierre Bossart's patches](https://ubuntuforums.org/showthread.php?t=2254322&page=126&p=13592053#post13592053) for sound card support. Not needed as of v4.11.

### Power level information (ACPI)

Before 4.2.0-1 kernel version, you must compile your own kernel with the appropriate flag ACPI_I2C_OPREGION=y (cf. [FS#44582)](https://bugs.archlinux.org/task/44582))

You should have no problem with the power level information now if you obtain the latest kernel version >= 4.2.*. See [this page.](http://ifranali.blogspot.com/2015/04/installing-arch-linux-on-asus-x205ta.html)

### Touchpad

With kernel version < 4.3.* the x205ta touchpad is recognised as a mouse and so gestures (e.g., two-finger scrolling) are not recognised.

Since kernel 4.3.* a [simpler patch](https://lkml.org/lkml/2015/8/24/647) was merged and provides all touch/clickpad functionality out of the box.

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

#### Device support

For older kernel versions < v4.4-rc1 the micro SD card reader will probably not work out of the box. [This page](https://wiki.debian.org/InstallingDebianOn/Asus/X205TA) contains a simple fix. First, create the file as follows:

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

#### RPMB Partition

For kernel versions < v4.15-rc1 there can be timeouts when probing the Replay Protected Memory Block partition. Refer to this page for more info and a kernel patch disabling the RPMB partition should you never need the RPMB partition. This is [fixed in a patch](https://github.com/torvalds/linux/commit/97548575bef38abd06690a5a6f6816200c7e77f7) as of v4.15-rc1.

### Special keys

On older kernel versions, out of the box, the only keysyms correctly sent are the audio volume keys (F10-F12). Ironic, since the sound card does not work. Can be conveniently remapped to control screen brightness (e.g., by calling xbacklight). On current kernel versions the sleep button, brightness buttons, display button and volume buttons all work in XFCE.

## See also

[Distro-Agnostic Installation Guide for the X205TA](http://ubuntuforums.org/showthread.php?t=2254322&p=13414345#post13414345)

[Ifran's ASUS x205ta Installation Guide](https://ifranali.blogspot.com/2015/04/installing-arch-linux-on-asus-x205ta.html)
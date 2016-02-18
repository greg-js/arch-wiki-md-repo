## Contents

*   [1 Disambiguation](#Disambiguation)
*   [2 Installation](#Installation)
    *   [2.1 Booting the install media](#Booting_the_install_media)
        *   [2.1.1 BIOS and USB drives](#BIOS_and_USB_drives)
        *   [2.1.2 Screen corruption](#Screen_corruption)
    *   [2.2 Partitioning](#Partitioning)
*   [3 Post-installation](#Post-installation)
    *   [3.1 No sound from headphone out](#No_sound_from_headphone_out)
    *   [3.2 No sound from built-in speakers](#No_sound_from_built-in_speakers)
    *   [3.3 Turn off beep sound](#Turn_off_beep_sound)
*   [4 Trackpad](#Trackpad)

## Disambiguation

This page refers to the 2013 model XPS 13\. For the 2015 model, see [Dell XPS 13 (2015)](/index.php/Dell_XPS_13_(2015) "Dell XPS 13 (2015)").

## Installation

Installation largely runs smoothly. See below for potential problems.

### Booting the install media

#### BIOS and USB drives

It is possible to boot a EFI Arch image. However the XPS' BIOS (tested with BIOS version A04 / XPS 13 9333 circa early 2014) will print "operation system not found" [sic] when using a GPT formtated USB drive. Hence a dd-copied bit-for-bit image of the arch dual ISO will not boot. A workaround is to format the USB drive to VFAT with a bootable MBR and use a tool like [UNetbootin](/index.php?title=UNetbootin&action=edit&redlink=1 "UNetbootin (page does not exist)") to copy the image files along with the syslinux MBR bootloader to the drive. This still allows you to boot in EFI mode (just press F12 during boot - you should find that even after disabling all legacy boot options you can select the arch EFI image) and continue with the install.

You may need to use dosfslabel (install core/dosfstools) to give the USB drive FAT partition a label that is searched for on boot by the arch ISO (e.g. dosfslabel /dev/sdX1 ARCH_201408) in order for the partition to be mounted properly.

#### Screen corruption

If the screen corrupts, append *nomodeset* to the kernel parameters. There may be issues with the cord of the external optical drive, possibly specific to the device.

On Haswell editions, you may run into [EFISTUB](/index.php/EFISTUB "EFISTUB") issues on full UEFI boot as detailed in [FS #33745](https://bugs.archlinux.org/task/33745). For workarounds, see [Unified Extensible Firmware Interface#USB media gets struck with black screen](/index.php/Unified_Extensible_Firmware_Interface#USB_media_gets_struck_with_black_screen "Unified Extensible Firmware Interface"). This problem is intermittent and may also be present after installation, affecting the choice of bootloaders.

### Partitioning

On recent Haswell editions, a full new [GPT](/index.php/GPT "GPT") and ESP work correctly with no boot problems. Remember to swap the system into full EFI boot in the 'BIOS'.

On older XPS 13 models there is an MBR with all four partitions already used. Additionally, if you delete any of the partitions, **the boot process will break.** Therefore, a dual-boot with Windows is impossible on this machine, although only Arch is probably fine. One solution could be [booting from a permanent USB installation](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key"). However, this has caveats too. See the [#BIOS and USB drives](#BIOS_and_USB_drives).

## Post-installation

### No sound from headphone out

The kernel modules snd-hda-intel is loaded automatically, but the model auto-detection seems to leave the system with a non-functional headphone out - there is no sound when headphones are inserted although they are detected and the speakers work. Add this file to your modprobe.d directory and restart:

 ` /etc/modprobe.d/alsa-base.conf `  ` options snd-hda-intel model=dell-headset-multi` 

This is taken from the pre-installed Ubuntu image that comes with the XPS 13 developer edition.

### No sound from built-in speakers

The HDMI output is occasionally detected as the default soundcard on the Haswell XPS 13\. Since both use snd-hda-intel we need to specify the vid and pid of each card. To do this, run `lspci -nn | grep -i audio` - the last set of numbers in braces is the vid and pid of each card.

Add this to your alsa-base.conf file in modprobe.d:

 ` /etc/modprobe.d/alsa-base.conf ` 
```
# Intel Corporation Haswell-ULT HD Audio Controller
options snd-hda-intel index=0 model=auto vid=8086 pid=0a0c
# Intel Corporation 8 Series HD Audio Controller
options snd-hda-intel index=1 model=auto vid=8086 pid=9c20
```

### Turn off beep sound

The annoying error beep can be turned off by blacklisting its module.

Add this to your nobeep.conf file in modprobe.d:

 ` /etc/modprobe.d/nobeep.conf ` 
```
# Turn off annoying beep
blacklist pcspkr
```

## Trackpad

Issues with the trackpad were originally solved with the hardware enablement (Sputnik) kernel. As of Linux 3.9 these trackpad fixes were merged, and the hardware enablement kernel *linux-mainline-dellxps* has since been removed from the [AUR](/index.php/AUR "AUR").

The touchpad may not work correctly with the touchscreen, with different solutions depending on the kernel version. See [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1431327).
Overall this 2-in-1 [Samsung notebook](/index.php/Laptop/Samsung "Laptop/Samsung") worked very well out of the box with the July 1, 2016, release of Arch Linux. It comes with Windows 10 preinstalled.

*Branding note*: Variously branded as Samsung Notebook 7 Spin, Samsung NP740U3L-L02US|NP740U3L-L02US, or just plain 740U3L. These appear to all refer to the same or similar units. Reviews and market information is scant right now.

## Contents

*   [1 Dual Booting](#Dual_Booting)
*   [2 Network/Wifi](#Network.2FWifi)
*   [3 Sound](#Sound)
*   [4 Graphics](#Graphics)
*   [5 Webcam](#Webcam)
*   [6 Possible quirks/todo](#Possible_quirks.2Ftodo)
*   [7 External links](#External_links)

## Dual Booting

This is a UEFI laptop. Dual booting required disabling secure boot in BIOS. Hit F2 immediately when machine powers up to get into setup. Select "Boot" and make relevant changes. You may need to change some other settings too. Save your settings and shut down. You should now be able to plug in some kind of USB-based install media, go back into setup, and select it from the boot order menu.

**To keep Windows 10**: This unit has a 1TB hard drive. Windows 10 and some recovery partitions consume most of it. It was resized pretty painlessly with [gparted](/index.php/Gparted "Gparted") using a live CD distro installed on a USB drive. Shrink the Windows 10 partition to a reasonable size with a live CD, move the recovery partitions to the right side of the disk, and create your Linux partitions. You probably minimally want a system partition and a swap partition larger than your system's RAM. Here is a sample configuration that worked (gave Linux almost 700GiB):
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0   100M  0 part /boot
├─sda2   8:2    0   128M  0 part 
├─sda3   8:3    0 214.9G  0 part 
├─sda4   8:4    0   500M  0 part 
├─sda5   8:5    0  11.4G  0 part 
├─sda6   8:6    0     1G  0 part 
├─sda7   8:7    0 695.2G  0 part /
└─sda8   8:8    0   8.4G  0 part [SWAP]

```

**Warning**: no Windows 10 install media came with this unit. All recovery data is on the hard drive. *Windows still booted but did not test recovery partitions after doing the above; do this at your own risk*.

Following this example, when installing Arch Linix, /dev/sda1 became boot and /dev/sda7 became the Linux root partition. Mount /dev/sda7 in /mnt/boot/ before you do arch-chroot. You will need to do your grub-install here. UEFI configuration more or less matches that described in [Windows/Arch Linux dual boot UEFI configuration section](/index.php/Dual_boot_with_Windows#UEFI_systems "Dual boot with Windows").

Grub was configured with: *grub-mkconfig -o /boot/grub/grub.cfg*

Per [this](/index.php/GRUB#Installation_2 "GRUB"), GRUB installed with a command like: *grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub*

## Network/Wifi

This unit has no ethernet port.

Wifi worked pretty painlessly during initial setup. When rebooted, wifi-menu had the dependency 'dialog' that wasn't installed with the core system. Make sure to run *pacman -S dialog* in arch-chroot to make it possible to use 'wifi-menu'. Wifi module 'iwlwifi' loads out of the box and appears to work well.

Note: wifi-menu throws a warning or error but appears to work.

## Sound

Worked out of the box with [pulseaudio](/index.php/Pulseaudio "Pulseaudio"); have not tested extensively though.

## Graphics

Intel HD Graphics 520 works out of the box.

## Webcam

Webcam uses module [uvcvideo](/index.php/Webcam_setup#linux-uvc "Webcam setup"); works out of box, tested with guvcview

## Possible quirks/todo

Touchpad variously seems over- or under-sensitive.

Touchscreen works out of box in xfce4, but haven't done extensive testing.

Need to test laptop sleeping, resume, etc..

Bluetooth not tested, but throws some errors in boot

## External links

*   spec info [here](http://www.notebookocean.com/samsung-notebook-7-spin-np740u3l-l02us-specs/)
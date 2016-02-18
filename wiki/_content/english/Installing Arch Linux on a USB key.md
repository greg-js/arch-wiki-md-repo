This page explains how to perform a regular Arch installation onto a USB key (or "flash drive"). In contrast to having a LiveUSB as covered in [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"), the result will be a persistent installation identical to normal installation to HDD, but on a USB flash drive.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installation tweaks](#Installation_tweaks)
*   [2 Configuration](#Configuration)
    *   [2.1 GRUB legacy](#GRUB_legacy)
    *   [2.2 GRUB](#GRUB)
    *   [2.3 Syslinux](#Syslinux)
*   [3 Tips](#Tips)
    *   [3.1 Using your USB install on multiple machines](#Using_your_USB_install_on_multiple_machines)
        *   [3.1.1 Architecture](#Architecture)
        *   [3.1.2 Input drivers](#Input_drivers)
        *   [3.1.3 Video drivers](#Video_drivers)
        *   [3.1.4 Persistent block device naming](#Persistent_block_device_naming)
        *   [3.1.5 Kernel parameters](#Kernel_parameters)
        *   [3.1.6 Booting from USB 3 media](#Booting_from_USB_3_media)
    *   [3.2 Compatibility](#Compatibility)
    *   [3.3 Minimizing disk access](#Minimizing_disk_access)
*   [4 See also](#See_also)

## Installation

**Note:** At least 2 GiB of storage space is recommended. A modest set of packages will fit, leaving a little free space for storage.

There are various ways of installing Arch on a USB stick, depending on the operating system you have available:

*   If you have another Linux computer available (it need not be Arch), you can follow the instructions at [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux").
*   An Arch Linux CD/USB can be used to install Arch onto the USB key, via booting the CD/USB and following the [installation guide](/index.php/Installation_guide "Installation guide"). If booting from a Live USB, the installation will have to be made on a different USB stick.
*   If you run Windows or OS X, download VirtualBox, install VirtualBox Extensions, add the USB drive to a virtual machine running Arch (for example running from an iso), point the installation into the USB drive.

### Installation tweaks

Follow the [installation guide](/index.php/Installation_guide "Installation guide") as you normally would, with these exceptions:

*   If cfdisk fails with "Partition ends in the final partial cylinder" fatal error, the only way to proceed is to kill all partitions on the drive. Open another terminal (`Alt+F2`), type `fdisk /dev/*sdX*` (where `*sdX*` is your usb drive), print partition table (p), check that it's ok, delete it (d) and write changes (w). Now return to cfdisk.
*   It is highly recommended to review the [tips for minimizing disk reads/writes](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD") on the [SSD](/index.php/SSD "SSD") wiki article prior to selecting a filesystem. To sum up, [ext4 without a journal](http://fenidik.blogspot.com/2010/03/ext4-disable-journal.html) should be fine, which can be created with `# mkfs.ext4 -O "^has_journal" /dev/sdXX`. Recognize that flash has a limited number of writes, and a journaling file system will take some of these as the journal is updated. For this same reason, it is best to forget the swap partition. Note that this does not affect installing onto a USB hard drive.
*   Before creating the initial RAM disk `# mkinitcpio -p linux`, in `/etc/mkinitcpio.conf` add the `block` hook to the hooks array right after udev. This is necessary for appropriate module loading in early userspace.
*   If you want to be able to continue to use the UFD device as a cross-platform removable drive, this can be accomplished by creating a partition housing an appropriate file system (most likely NTFS or exFAT). Note that the data partition may need to be the first partition on the device, as Windows assumes that there can only be one partition on a removable device, and will happily automount an EFI system partition otherwise. Remember to install [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) and [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Some tools are available online that may allow you to flip the removable media bit on your UFD device. This would trick operating systems into treating your UFD device as an external hard disk and allow you to use whichever partitioning scheme you choose.

**Warning:** It is not possible to flip the removable media bit on every UFD device and attempting to use software that is incompatible with your device may damage it. Attempting to flip the removable media bit is **not** recommended.

*   Install [NetworkManager](/index.php/NetworkManager "NetworkManager") to control networks, it supports changing interface names of different hardware.

## Configuration

*   Make sure that `/etc/fstab` includes the correct partition information for `/`, and for any other partitions on the USB key. If the usb key is to be booted on several machines, it is quite likely that devices and number of available hard disks vary. So it is advised to use UUID or label:

To get the proper UUIDs for your partitions issue **blkid**

**Note:**

*   When GRUB is installed on the USB key, the key will always be `hd0,0`.
*   It seems that current versions of GRUB will automatically default to using uuid. The following directions are for GRUB legacy.

### GRUB legacy

`menu.lst`, the GRUB legacy configuration file, should be edited to (loosely) match the following: With the static `/dev/sda*X*`:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro
initrd /boot/initramfs-linux.img

```

When using label your menu.lst should look like this:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** ro
initrd /boot/initramfs-linux.img

```

And for UUID, it should be like this:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
initrd /boot/initramfs-linux.img

```

### GRUB

On GPT with UEFI installations, make sure you follow the instructions on [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") and include the --removable option as doing otherwise may break existing GRUB installations, as in the below command:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub **--removable** --recheck

```

### Syslinux

With the static `/dev/sda*X*`:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sdax ro
        INITRD ../initramfs-linux.img

```

Using your UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
        INITRD ../initramfs-linux.img

```

## Tips

### Using your USB install on multiple machines

#### Architecture

For the most versatile compatibility it is recommended that you install the i686 architecture because it will run on both 32-bit (i686) and 64-bit (x86_64) architectures.

Additionally, due to the reduced size of 32-bit binaries and the absence of (possible) multilib packages, an i686 installation typically consumes less space than an equivalent x86_64 one.

**Note:** Chrooting into a 64-bit Linux installation (eg. when using the USB key as install/rescue media) is only possible from x86_64 Arch.

#### Input drivers

For laptop use (or use with a tactile screen) you will need the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package for the touchpad/touchscreen to work.

For instructions on fine tuning or troubleshooting touchpad issues, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

#### Video drivers

**Note:** The use of proprietary video drivers is **not** recommended for this type of installation.

To support most common GPUs, install [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau).

#### Persistent block device naming

It is recommended to use [UUID](/index.php/UUID "UUID") in both [fstab](/index.php/Fstab "Fstab") and bootloader configuration. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

Alternatively, you may create udev rule to create custom symlink for your usb key. Then use this symlink in fstab and bootloader configuration. See [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev") for details.

#### Kernel parameters

You may want to disable KMS for various reasons, such as getting a blank screen or a "no signal" error from the display, when using some Intel video cards, etc. To disable KMS, add `nomodeset` as a kernel parameter. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

**Warning:** Some [Xorg](/index.php/Xorg "Xorg") drivers will not work with KMS disabled. See the wiki page on your specific driver for details. Nouveau in particular needs KMS to determine the correct display resolution. If you add `nomodeset` as a kernel parameter as a preemptive measure you may have to adjust the display resolution manually when using machines with Nvidia video cards. See [Xrandr](/index.php/Xrandr "Xrandr") for more info.

#### Booting from USB 3 media

See [[1]](http://www.wyae.de/docs/boot-usb3/).

### Compatibility

The fallback image should be used for maximum compatibility.

### Minimizing disk access

*   You may want to configure [journald](/index.php/Systemd#Journal "Systemd") to store its journals in RAM, e.g. by creating a custom configuration file:

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   To disable `fsync` and related system calls in web browsers and other applications that do not write essential data, use the *eatmydata* command from [libeatmydata](https://aur.archlinux.org/packages/libeatmydata/) to avoid such system calls:

```
$ eatmydata firefox

```

## See also

*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")
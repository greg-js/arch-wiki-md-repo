Related articles

*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [General recommendations](/index.php/General_recommendations "General recommendations")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Install Arch Linux from VirtualBox](/index.php/Install_Arch_Linux_from_VirtualBox "Install Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")

This page explains how to perform a regular Arch installation onto removable media (e.g. a USB flash drive). In contrast to having a LiveUSB as covered in [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"), the result will be a persistent installation identical to normal installation to HDD.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Installation tweaks](#Installation_tweaks)
*   [2 Configuration](#Configuration)
    *   [2.1 GRUB legacy](#GRUB_legacy)
    *   [2.2 GRUB](#GRUB)
    *   [2.3 Syslinux](#Syslinux)
*   [3 Tips](#Tips)
    *   [3.1 Using your portable install on multiple machines](#Using_your_portable_install_on_multiple_machines)
        *   [3.1.1 Input drivers](#Input_drivers)
        *   [3.1.2 Video drivers](#Video_drivers)
        *   [3.1.3 Persistent block device naming](#Persistent_block_device_naming)
        *   [3.1.4 Kernel parameters](#Kernel_parameters)
        *   [3.1.5 Booting from USB 3 medium](#Booting_from_USB_3_medium)
    *   [3.2 Compatibility](#Compatibility)
    *   [3.3 Minimizing disk access](#Minimizing_disk_access)
*   [4 See also](#See_also)

## Installation

**Note:** At least 2 GiB of storage space is recommended. A modest set of packages will fit, leaving a little free space for storage.

There are various ways of installing Arch on removable media, depending on the operating system you have available:

*   If you have another Linux computer available (it need not be Arch), you can follow the instructions at [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux").
*   An Arch Linux CD/USB can be used to install Arch onto the removable medium, via booting the CD/USB and following the [installation guide](/index.php/Installation_guide "Installation guide"). If booting from a Live USB, the installation cannot be made to the same USB stick you are booting from.
*   If you run Windows or OS X, download VirtualBox, install VirtualBox Extensions, attach your removable medium to a virtual machine running Arch (for example running from an iso), point the installation into the now attached drive while using the instructions at the [Installation guide](/index.php/Installation_guide "Installation guide").

### Installation tweaks

*   Before [creating the initial RAM disk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio"), in `/etc/mkinitcpio.conf` move the `block` and `keyboard` hooks before the `autodetect` hook. This is necessary to allow booting on multiple systems each requiring different modules in early userspace.
*   It is highly recommended to review the [Improving performance#Reduce disk reads/writes](/index.php/Improving_performance#Reduce_disk_reads/writes "Improving performance") article prior to selecting a file system. To sum up, for flash-based media such as USB flash drives or SD cards, [ext4 without a journal](http://fenidik.blogspot.com/2010/03/ext4-disable-journal.html) should be fine, which can be created with `mkfs.ext4 -O "^has_journal" /dev/sdXX`. The obvious drawback of using a file system with journaling disabled is data loss as a result of an ungraceful dismount. Recognize that flash has a limited number of writes, and a journaling file system will take some of these as the journal is updated. For this same reason, it is best to forget the swap partition. Note that this does not affect installing onto a portable hard drive.
*   If you have chosen to install Arch onto a USB mass storage device and want to be able to continue to use it as a cross-platform removable drive, this can be accomplished by creating a partition housing an appropriate file system (most likely NTFS or exFAT). Note that the data partition may need to be the first partition on the device, as Windows assumes that there can only be one partition on a removable device, and will happily automount an EFI system partition otherwise. Remember to install [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) and [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Some tools are available online that may allow you to flip the Removable Medium Bit (RMB) on your USB mass storage device. This would trick operating systems into treating your USB mass storage device as an external hard disk and allow you to use whichever partitioning scheme you choose.

**Warning:** It is not possible to flip the Removable Medium Bit (RMB) on every USB mass storage device and attempting to use software that is incompatible with your device may damage it. Attempting to flip the RMB is **not** recommended.

## Configuration

*   Make sure that `/etc/fstab` includes the correct partition information for `/`, and for any other partitions on the disk. If the drive is to be booted on several machines, it is quite likely that devices and number of available hard disks vary. So it is advised to use [UUID](/index.php/UUID "UUID") or label.

To get the proper UUIDs for your partitions use *lsblk* of *blkid*. See [Persistent block device naming#by-uuid](/index.php/Persistent_block_device_naming#by-uuid "Persistent block device naming") for more information.

**Note:**

*   When GRUB is installed on the disk, the disk will always be `hd0,0`.
*   It seems that current versions of GRUB will automatically default to using uuid. The following directions are for GRUB legacy.

### GRUB legacy

`menu.lst`, the GRUB legacy configuration file, should be edited to (loosely) match the following.

When using file system labels your `menu.lst` should look like this:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** rw
initrd /boot/initramfs-linux.img

```

And for UUID, it should be like this:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa rw
initrd /boot/initramfs-linux.img

```

### GRUB

On GPT with UEFI installations, make sure you follow the instructions on [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") and include the `--removable` option as doing otherwise may break existing GRUB installations, as in the below command:

```
# grub-install --target=x86_64-efi --efi-directory=*esp*  **--removable** --recheck

```

### Syslinux

Using your UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa rw
        INITRD ../initramfs-linux.img

```

## Tips

### Using your portable install on multiple machines

#### Input drivers

For laptop use (or use with a tactile screen) you will need the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package for the touchpad/touchscreen to work.

For instructions on fine tuning or troubleshooting touchpad issues, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

#### Video drivers

**Note:** The use of proprietary video drivers is **not** recommended for this type of installation.

To support most common GPUs, install [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu), and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau).

#### Persistent block device naming

It is recommended to use [UUID](/index.php/UUID "UUID") in both [fstab](/index.php/Fstab "Fstab") and boot loader configuration. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

Alternatively, you may create udev rule to create custom symlink for your disk. Then use this symlink in [fstab](/index.php/Fstab "Fstab") and boot loader configuration. See [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev") for details.

#### Kernel parameters

You may want to disable KMS for various reasons, such as getting a blank screen or a "no signal" error from the display, when using some Intel video cards, etc. To disable KMS, add `nomodeset` as a kernel parameter. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

**Warning:** Some [Xorg](/index.php/Xorg "Xorg") drivers will not work with KMS disabled. See the wiki page on your specific driver for details. Nouveau in particular needs KMS to determine the correct display resolution. If you add `nomodeset` as a kernel parameter as a preemptive measure you may have to adjust the display resolution manually when using machines with Nvidia video cards. See [Xrandr](/index.php/Xrandr "Xrandr") for more info.

#### Booting from USB 3 medium

See [[1]](http://www.wyae.de/docs/boot-usb3/).

### Compatibility

The fallback image should be used for maximum compatibility.

### Minimizing disk access

*   You may want to configure [systemd journal](/index.php/Systemd_journal "Systemd journal") to store its journals in RAM, e.g. by creating a custom configuration file:

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   To disable `fsync` and related system calls in web browsers and other applications that do not write essential data, use the `eatmydata` command from [libeatmydata](https://www.archlinux.org/packages/?name=libeatmydata) to avoid such system calls:

```
$ eatmydata firefox

```

## See also

*   [ALMA](https://github.com/r-darwish/alma) - A utility written in Rust to automatically create persistent Arch Linux Live USB installations.
*   [ArchLinux USB](http://valleycat.org/linux/arch-usb.html) - c-magyar's excellent writeup on creating a persistent Live USB installation.
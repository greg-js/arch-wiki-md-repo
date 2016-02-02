# USB storage devices

Related articles

*   [Mount](/index.php/Mount "Mount")

This document describes how to use the popular USB memory sticks with Linux. However, it is also valid for other devices such as digital cameras that act as if they were just a USB storage device.

If you have an up-to-date system with the standard Arch kernel and a modern [Desktop environment](/index.php/Desktop_environment "Desktop environment") your device should just show up on your desktop, with no need to open a console.

## Contents

*   [1 Auto-mounting with udisks](#Auto-mounting_with_udisks)
*   [2 Manual mounting](#Manual_mounting)
    *   [2.1 Getting a kernel that supports usb_storage](#Getting_a_kernel_that_supports_usb_storage)
    *   [2.2 Identifying device](#Identifying_device)
    *   [2.3 Mounting USB memory](#Mounting_USB_memory)
        *   [2.3.1 As root](#As_root)
        *   [2.3.2 As normal user with mount](#As_normal_user_with_mount)
        *   [2.3.3 As normal user with fstab](#As_normal_user_with_fstab)

## Auto-mounting with udisks

This is the easiest and most frequently used method. It is used by many [desktop environments](/index.php/Desktop_environments "Desktop environments"), but can be used separately too. See [Udisks](/index.php/Udisks "Udisks") for details.

## Manual mounting

**Note:** Before you decide that Arch Linux does not mount your USB device, be sure to check all available ports. Some ports might not share the same controller, preventing you from mounting the device.

### Getting a kernel that supports usb_storage

If you do not use a custom-made kernel, you are ready to go, for all Arch Linux stock kernels are properly configured. If you do use a custom-made kernel, ensure it is compiled with SCSI-Support, SCSI-Disk-Support and usb_storage. If you use the latest [udev](/index.php/Udev "Udev"), you may just plug your device in and the system will automatically load all necessary kernel modules. Older releases of udev would need hotplug installed too. Otherwise, you can do the same thing manually:

```
# modprobe usb_storage
# modprobe sd_mod      (only for non SCSI kernels)

```

**Tip:** In case of manually loading modules, you may also need to load the `sg` module (SCSI generic driver).

### Identifying device

First thing one need to access storage device is its identifier assigned by kernel. See [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab") for details.

**Tip:** To see which device is your USB device, you can compare the output of `lsblk -f` (explained in the linked article) when the USB device is connected and when it is unconnected.

### Mounting USB memory

You need to create the directory in which you are going to mount the device:

```
# mkdir /mnt/usbstick

```

#### As root

Mount the device as root with this command (do not forget to replace **device_node** by the path you found):

```
# mount **device_node** /mnt/usbstick

```

or

```
# mount -U **UUID** /mnt/usbstick

```

If `mount` does not recognize the format of the device you can try to use the `-t` argument, see `man mount` for details.

**Note:**

*   If mounting your stick does not work you can try to repartition it, see [Format a device](/index.php/Format_a_device "Format a device").
*   See [[1]](https://gist.github.com/anonymous/a69093a51f83b53d9fc5) for example mount/unmount scripts using [sudo](/index.php/Sudo "Sudo").

#### As normal user with mount

If you want non-root users to be able to write to the USB stick, you can issue the following command:

```
# mount -o gid=users,fmask=113,dmask=002 /dev/sda1 /mnt/usbstick

```

#### As normal user with fstab

If you want non-root users to be able to mount a USB memory stick via [fstab](/index.php/Fstab "Fstab"), add the following line to your `/etc/fstab` file:

```
/dev/sdXY /mnt/usbstick vfat **user**,noauto,noatime,flush 0 0

```

or better:

```
UUID=E8F1-5438 /mnt/usbstick vfat **user**,noauto,noatime,flush 0 0

```

(see description of **user** and other options in the [main article](/index.php/Fstab "Fstab"))

**Note:** Where `/dev/sdXY` is replaced with the path to your own usbstick, see [Mounting USB memory](#Mounting_USB_memory).

Now, any user can mount it with:

```
$ mount /mnt/usbstick

```

And unmount it with:

```
$ umount /mnt/usbstick

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=USB_storage_devices&oldid=408489](https://wiki.archlinux.org/index.php?title=USB_storage_devices&oldid=408489)"
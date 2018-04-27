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
        *   [2.3.2 Allow writing by regular users](#Allow_writing_by_regular_users)
        *   [2.3.3 As normal user with fstab](#As_normal_user_with_fstab)
        *   [2.3.4 Mount tools](#Mount_tools)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 No USB storage devices are acknowledged by the system](#No_USB_storage_devices_are_acknowledged_by_the_system)

## Auto-mounting with udisks

This is the easiest and most frequently used method. It is used by many [desktop environments](/index.php/Desktop_environments "Desktop environments"), but can be used separately too.

See [Udisks](/index.php/Udisks "Udisks") for detailed information, including list of mount helpers.

## Manual mounting

**Note:** Before you decide that Arch Linux does not mount your USB device, be sure to check all available ports. Some ports might not share the same controller, preventing you from mounting the device.

### Getting a kernel that supports usb_storage

If you do not use a custom-made kernel, you are ready to go, for all Arch Linux stock kernels are properly configured. If you do use a custom-made kernel, ensure it is compiled with SCSI-Support, SCSI-Disk-Support and usb_storage. If you use the latest [udev](/index.php/Udev "Udev"), you may just plug your device in and the system will automatically load all necessary kernel modules.

### Identifying device

The first thing one needs to access a storage device is its identifier assigned by kernel. See [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab") for details.

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

If `mount` does not recognize the [file system](/index.php/File_system "File system") of the device you can try to use the `-t` argument, see [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) for details. If mounting does not work, you can try to [recreate the file system](/index.php/File_systems#Create_a_file_system "File systems") or even [repartition the disk](/index.php/Partitioning "Partitioning").

**Note:** See [[1]](https://gist.github.com/anonymous/a69093a51f83b53d9fc5) for example mount/unmount scripts using [sudo](/index.php/Sudo "Sudo").

#### Allow writing by regular users

If you want non-root users to be able to write to the USB stick, you can issue the following command:

```
# mount -o gid=users,fmask=113,dmask=002 /dev/sda1 /mnt/usbstick

```

If it does not work, make sure that the [file system](/index.php/File_system "File system") is mountable and writable as root, see the previous section for details.

#### As normal user with fstab

See [FAT#Writing to FAT32 as normal user](/index.php/FAT#Writing_to_FAT32_as_normal_user "FAT") if you want normal user to do the mount/unmount action.

#### Mount tools

Multiple [mount tools](/index.php/List_of_applications#Mount_tools "List of applications") facilitate mounting as a regular user.

## Troubleshooting

### No USB storage devices are acknowledged by the system

If you have connected your USB storage device to the computer and it is not listed in `lsblk` or `dmesg`, ensure that your BIOS has both XCHI Handoff and EHCI Handoff enabled.
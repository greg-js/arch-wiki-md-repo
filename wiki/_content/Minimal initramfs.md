# Minimal initramfs

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")

This article shows how to create a slim, minimal initramfs for a system with a specific, known and static hardware configuration. The procedure is expounded from [this tutorial](http://blog.falconindy.com/articles/optmizing-bootup-with-mkinitcpio.html) by Falconindy (Dave Reisner).

## Contents

*   [1 Udev requirement](#Udev_requirement)
*   [2 Editing .preset files](#Editing_.preset_files)
*   [3 Finding needed modules](#Finding_needed_modules)
*   [4 Initial edit of mkinitcpio.conf](#Initial_edit_of_mkinitcpio.conf)
*   [5 Initial test](#Initial_test)
*   [6 Sorting out modules](#Sorting_out_modules)
    *   [6.1 Filesystem modules](#Filesystem_modules)
    *   [6.2 Storage device modules](#Storage_device_modules)
    *   [6.3 Keyboard modules](#Keyboard_modules)
*   [7 Finishing up](#Finishing_up)

## Udev requirement

The big advantage of creating your own initramfs images is that you can eliminate `udev`. This hook alone is responsible for quite a bit of size (~700-800 KiB with LZ4 and LZOP, less with other algorithms) in the initramfs image. Not only will the bigger size lead to longer boots (more data to decompress) but initializing `udev` itself will also take some extra time. **However, some things require `udev`.** This includes the assembly of LVM and mdadm devices that contain the `root` partition. If you are unsure if you need `udev`, continue with the directions on this page up until the [#Initial test](#Initial_test). If not everything works without `udev`, re-enable the hook and try again.

Also, while most keyboards (AT,PS/2,or USB) don't require the use of the `udev` hook, Logitech USB devices using the Logitech Unified Receiver do. At this point you could either include `udev` in all images or rely on a `fallback` image that does.

If you need `udev`, your minimization efforts will most likely be in vain. You may still be able to shrink the image size by ~600 KiB, but boot times will not be significantly improved. Continuing on in this scenario can still be a worthwhile learning experience.

## Editing .preset files

In Falconidy's tutorial, he edits `/etc/mkinitcpio.conf` and runs `mkinitcpio -g` to create the test initramfs image, leaving the known-good initramfs images on the system untouched. However, if you blindy run `mkinitcpio -P` afterwards, even the `fallback` image will be stripped down.

A safer way to prepare for taking the creation of the initramfs files into your own hands is to modify the `.preset` files in `/etc/mkinitcpio.d`. The following example configuration will supplant `default` with the minimal initfamfs image and create a new `normal` image that is built The Arch Way. If things go wrong, you can rely on the `normal` or `fallback` images. When you are finished, you can drop the `normal_*` lines from the config and remove the `initramfs-linux*-normal.img` files.

```
...

PRESETS=('default' 'normal' 'fallback')
...

default_options="-S udev,block,mdadm_udev,filesystems,keyboard,fsck,consolefont"
...

#normal_config="/etc/mkinitcpio.conf"
normal_image="/boot/initramfs-linux-normal.img"
#normal_options=""
...

```

**Note:** The `mdadm_udev` and `consolefont` hooks are not present in the default Arch configuration. Having extraneous hooks in the `-S` parameter in the `*_options` line will not result in an error.

## Finding needed modules

The quickest way to find out what modules you need is to reboot your system with the `fallback` initramfs image and add `break=postmount` to the kernel parameters in your boot loader so you get dropped to the command line once the root filesystem is mounted.

Once your system reboots, run the following command to see what modules you need:

```
lsmod | grep -v ' [a-z]'

```

**Note:** The `grep` command is used to filter out modules that were loaded as dependencies of other modules. Arch's `mkinitcpio` takes care of bringing in module dependecies.

Write down the modules that were loaded and type `exit` to continue booting.

## Initial edit of mkinitcpio.conf

Edit `/etc/mkinitcpio.conf` and modify the `MODULES=` line. A worthwhile note is that `/etc/mkinitcpio.conf` is sourced, so you can build the MODULES line like a variable in a bash script.

```
MODULES=""   # filesystems
MODULES+=""  # storage
MODULES+=""  # keyboard
MODULES+=""  # miscellaneous

```

Add all your modules to the last `miscellaneous` line. As you sort through your modules, you can place them in the appropriate line.

You will also need the binaries to do filesystem checks on the `root` device **and any other mount points** in `/etc/fstab` that have been set to do so.

*   For ext[2|3|4] devices:

```
BINARIES="fsck fsck.ext[2|3|4] e2fsck"

```

*   For xfs devices

```
BINARIES="fsck fsck.xfs xfs_repair"

```

**Note:** The third option in each of these example are optional, but their exclusion will prevent you from repairing a damaged filesystem, necessitating a boot from another initramfs.

**Note:** Users are encouraged to add entries pertaining to other filesystems.

## Initial test

Edit `/etc/mkinitcpio.conf` and run `mkinitcpio -P` to rebuild all of your initramfs images. Then reboot.

Your first boot should be successful **if you don't need `udev`**. If something doesn't work (eg, Arch can't find your root partition or your keyboard doesn't work) then you will need to go back and remove `udev` from the `-S` parameter in the `default_options` line and try again. If you need `udev`, keep in mind that you won't see a significant improvement in boot time and continuing on is only good for a learning experience.

## Sorting out modules

Now that you have a known-good bootable initramfs, it's time to slim down the initramfs even further. The normal method is to remove a few modules at a time, rebuild the initramfs images, and reboot to see if everything is still OK. If you find out that everything is not OK, reboot with the `fallback` initramfs image and re-add the deleted modules until everything is OK again. Rinse and repeat until you have only the modules you need. As this can be a tedious experience, the following lists are provided to give people a head-start in the elimination process.

**Note:** The following are examples and are not meant to be definitive.

### Filesystem modules

**Note:** You will need the filesystem modules for the `root` device and any other device in `/etc/fstab` that will have its filesystem checked on boot.

*   `ext[2,3,4]`
*   `xfs`
*   `jfs`
*   `reiserfs`

### Storage device modules

*   `sd_mod` for all SCSI, SATA, and PATA (IDE) devices
*   `ahci` for SATA devices on modern AHCI controllers
*   `sata_*` for SATA devices on IDE-mode controllers
*   `pata_*` for PATA (IDE) devices
*   `ehci_pci` and `usb_storage` for USB storage devices
*   `virtio_blk` and `virtio_pci` for QEMU/KVM VMs using VirtIO for storage

### Keyboard modules

*   `atkbd` for AT and PS/2 keyboards, and the emulated keyboard in QEMU/KVM.
*   `hid_generic`, `ohci_pci`, and `usbhid` for normal USB keyboards.
*   `hid_logitech_dj`, `uhci_hcd`, and `usbhid` for Logitech USB keyboards using the Logitech Unified Receiver. **(Requires the `udev` hook).**

## Finishing up

Once you've slimmed your initramfs as far as it will go, remove (or comment-out) the `normal_*` lines from your `.preset` files and remove the `initramfs-linux*-normal.img` files from `/boot`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Minimal_initramfs&oldid=382385](https://wiki.archlinux.org/index.php?title=Minimal_initramfs&oldid=382385)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")
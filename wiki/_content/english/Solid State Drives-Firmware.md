## Contents

*   [1 ADATA](#ADATA)
*   [2 Crucial](#Crucial)
*   [3 Intel](#Intel)
*   [4 Kingston](#Kingston)
*   [5 Mushkin](#Mushkin)
*   [6 OCZ](#OCZ)
*   [7 Samsung](#Samsung)
    *   [7.1 Native upgrade](#Native_upgrade)
*   [8 SanDisk](#SanDisk)

## ADATA

ADATA has a utility available for Linux (i686) on their support page [here](http://www.adata.com.tw/index.php?action=ss_main&page=ss_content_driver&lan=en). The link to latest firmware will appear after selecting the model. The latest Linux update utility is packed with firmware and needs to be run as root. One may need to set correct permissions for binary file first.

## Crucial

Crucial provides an option for updating the firmware with an ISO image. These images can be found after selecting the product [here](http://www.crucial.com/usa/en/support-ssd) and downloading the "Manual Boot File." Owners of an M4 Crucial model, may check if a firmware upgrade is needed with `smartctl`.

 `$ smartctl --all /dev/sd**X**` 
```
==> WARNING: This drive may hang after 5184 hours of power-on time:
[http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html](http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html)
See the following web pages for firmware updates:
[http://www.crucial.com/support/firmware.aspx](http://www.crucial.com/support/firmware.aspx)
[http://www.micron.com/products/solid-state-storage/client-ssd#software](http://www.micron.com/products/solid-state-storage/client-ssd#software)

```

Users seeing this warning are advised to backup all sensible data and **consider upgrading immediately**.

## Intel

Intel has a Linux live system based [Firmware Update Tool](https://downloadcenter.intel.com/download/18363) for operating systems that are not compatible with its [Intel® Solid-State Drive Toolbox](https://downloadcenter.intel.com/download/18455) software.

## Kingston

Kingston has a Linux utility to update the firmware of Sandforce controller based drives: [SSD support page](http://www.kingston.com/en/ssd). Click the images on the page to go to a support page for your SSD model. Support specifically for, e.g. the SH100S3 SSD, can be found here: [support page](http://www.kingston.com/en/support/technical/downloads?product=sh100s3&filename=sh100_503fw_win).

## Mushkin

The lesser known Mushkin brand Solid State drives also use Sandforce controllers, and have a Linux utility (nearly identical to Kingston's) to update the firmware.

## OCZ

OCZ has a command line utility available for Linux (i686 and x86_64) on their forum [here](http://www.ocztechnology.com/ssd_tools/).

## Samsung

Samsung notes that update methods other than using their Magician Software are "not supported," but it is possible. The Magician Software can be used to make a USB drive bootable with the firmware update. Samsung provides pre-made [bootable ISO images](http://www.samsung.com/global/business/semiconductor/samsungssd/downloads.html) that can be used to update the firmware. Another option is to use Samsung's [samsung_magician](https://aur.archlinux.org/packages/samsung_magician/), which is available in the AUR. Magician only supports Samsung-branded SSDs; those manufactured by Samsung for OEMs (e.g., Lenovo) are not supported.

**Note:** Samsung does not make it obvious at all that they actually provide these. They seem to have 4 different firmware update pages, and each references different ways of doing things.

Users preferring to run the firmware update from a live USB created under Linux (without using Samsung's "Magician" software under Microsoft Windows) can refer to [this post](http://fomori.org/blog/?p=933) for reference.

### Native upgrade

Alternatively, the firmware can be upgraded natively, without making a bootable USB stick, as shown below.

First visit the [Samsung downloads page](http://www.samsung.com/global/business/semiconductor/minisite/SSD/global/html/support/downloads.html) and download the latest firmware for Windows, which is available as a disk image. In the following, `Samsung_SSD_840_EVO_EXT0DB6Q.iso` is used as an example file name, adjust it accordingly.

Setup the disk image:

```
$ udisksctl loop-setup -r -f Samsung_SSD_840_EVO_EXT0DB6Q.iso

```

This will make the ISO available as a loop device, and display the device path. Assuming it was `/dev/loop0`:

```
$ udisksctl mount -b /dev/loop0

```

Get the contents of the disk:

```
$ mkdir Samsung_SSD_840_EVO_EXT0DB6Q
$ cp -r /run/media/$USER/CDROM/isolinux/ Samsung_SSD_840_EVO_EXT0DB6Q

```

Unmount the iso:

```
$ udisksctl unmount -b /dev/loop0
$ cd Samsung_SSD_840_EVO_EXT0DB6Q/isolinux

```

There is a FreeDOS image here that contains the firmware. Mount the image as before:

```
$ udisksctl loop-setup -r -f btdsk.img
$ udisksctl mount -b /dev/loop1
$ cp -r /run/media/$USER/C04D-1342/ Samsung_SSD_840_EVO_EXT0DB6Q
$ cd Samsung_SSD_840_EVO_EXT0DB6Q/C04D-1342/samsung

```

Get the disk number from magician:

```
# magician -L

```

Assuming it was 0:

```
# magician --disk 0 -F -p DSRD

```

Verify that the latest firmware has been installed:

```
# magician -L

```

Finally reboot.

## SanDisk

SanDisk makes **ISO firmware images** to allow SSD firmware update on operating systems that are unsupported by their SanDisk SSD Toolkit. One must choose the firmware for the right *SSD model*, as well as for the *capacity* that it has (e.g. 60GB, **or** 256GB). After burning the adequate ISO firmware image, simply restart the PC to boot with the newly created CD/DVD boot disk (may work from a USB stick).

The iso images just contain a linux kernel and an initrd. Extract them to `/boot` partition and boot them with [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") to update the firmware.

See also:

SanDisk Extreme SSD [Firmware Release notes](http://kb.sandisk.com/app/answers/detail/a_id/10127) and [Manual Firmware update version R211](http://kb.sandisk.com/app/answers/detail/a_id/10476)

SanDisk Ultra SSD [Firmware release notes](http://kb.sandisk.com/app/answers/detail/a_id/10192) and [Manual Firmware update version 365A13F0](http://kb.sandisk.com/app/answers/detail/a_id/10477)
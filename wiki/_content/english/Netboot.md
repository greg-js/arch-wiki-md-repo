Netboot images are small (< 1 MiB) images that can be used to download the latest Arch Linux release on the fly upon system boot. It is unnecessary to update the netboot image, the newest release will be available automatically. Netboot images can be downloaded from the [Arch Linux website](https://www.archlinux.org/releng/netboot/).

**Note:** You need sufficient memory (probably 1.5GiB or even more) to store and run the live system, otherwise you may get kernel panic on boot.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Using ipxe.lkrn](#Using_ipxe.lkrn)
    *   [1.2 Using ipxe.pxe](#Using_ipxe.pxe)
*   [2 UEFI](#UEFI)
    *   [2.1 Installation with efibootmgr](#Installation_with_efibootmgr)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error 410de13c](#Error_410de13c)

## BIOS

To use netboot on a BIOS-based computer, you need either the `ipxe.lkrn` or `ipxe.pxe` image.

### Using ipxe.lkrn

The `ipxe.lkrn` image can be booted like a Linux kernel. Any Linux [boot loader](/index.php/Boot_loader "Boot loader") (like [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux")) can be used to load it from your hard drive, a CD or a USB drive. For example, the Syslinux wiki gives instructions to install[[1]](https://wiki.syslinux.org/wiki/index.php?title=Install) and configure[[2]](https://wiki.syslinux.org/wiki/index.php?title=Config) Syslinux on a bootable medium.

You can make flash drive that boots `ipxe.lkrn` with the following steps:

*   Find out your device path using [lsblk](/index.php/Lsblk "Lsblk"). Let us assume it is `/dev/sdc`.
*   Create MBR partition table on the device.
*   Create a primary partition with [FAT32](/index.php/FAT32 "FAT32") file system and flag it as active.
*   Mount partition, create `boot/syslinux` directory there and copy `ipxe.lkrn` to the `boot` directory.

```
# mount /dev/sdc /mnt
# mkdir -p /mnt/boot/syslinux
# cp ipxe.lkrn /mnt/boot

```

*   Create config for syslinux

 `/mnt/boot/syslinux/syslinux.cfg` 
```
DEFAULT arch_netboot
   SAY Booting Arch over the network.
LABEL arch_netboot
   KERNEL /boot/ipxe.lkrn
```

*   Unmount partition

```
# umount /mnt

```

*   Install Syslinux MBR and Syslinux itself

```
# dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/bios/mbr.bin of=/dev/sdc
# syslinux --directory /boot/syslinux/ --install /dev/sdc1

```

*   Now you should be able to boot your usb stick with ipxe.lkrn.

Alternatively, you can also try the image with [QEMU](/index.php/QEMU "QEMU") by running the following command:

```
$ qemu-system-x86_64 -enable-kvm -m 2G -kernel ipxe.lkrn

```

### Using ipxe.pxe

The `ipxe.pxe` image is a PXE image. It can be chainloaded from an existing PXE environment. This allows configuring a DHCP server such that booting from the network will always boot into Arch Linux netboot.

Alternatively, you can also chainload it from existing pxe loader such as pxelinux. This is a menu entry example:

```
LABEL arch_netboot_chain
  COM32 pxechn.c32
  APPEND ipxe.a56af4e6a9a9.pxe

```

For this example to work you must have pxechn.c32 copied to the directory where your pxelinux.0 resides.

## UEFI

The `ipxe.efi` image can be used to launch Arch Linux netboot in UEFI mode. Only 64-bit UEFI is supported. The `ipxe.efi` image can be added as a boot option via [efibootmgr](/index.php/Efibootmgr "Efibootmgr"), launched from a [boot manager](/index.php/Boot_manager "Boot manager"), like [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or [rEFInd](/index.php/REFInd "REFInd"), or directly from the [UEFI shell](/index.php/UEFI_shell "UEFI shell").

### Installation with efibootmgr

First install the [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) package, then download the [UEFI netboot image](https://www.archlinux.org/releng/netboot/).

Assuming your [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) is mounted under `*esp*`, you should move it as follows - let us also give it a more friendly name:

```
# mkdir *esp*/EFI/arch_netboot
# mv ipxe.*.efi *esp*/EFI/arch_netboot/arch_netboot.efi

```

Then you can create a boot entry as follows:

```
# efibootmgr --create --disk /dev/sda --part 1 --loader /EFI/arch_netboot/arch_netboot.efi --label "Arch Linux Netboot" --verbose

```

## Troubleshooting

### Error 410de13c

When loading ipxe.08268867b45a.lkrn or ipxe.d63edd60ae06.efi you get such error:

```
[https://www.archlinux.org/releng/netboot/archlinux.ipxe](https://www.archlinux.org/releng/netboot/archlinux.ipxe)... Operation not permitted ([http://ipxe.org/410de13c](http://ipxe.org/410de13c))

```

This is a bug related to https (see [FS#58470](https://bugs.archlinux.org/task/58470)).

As a workaround, download this file ([https://www.archlinux.org/releng/netboot/archlinux.ipxe](https://www.archlinux.org/releng/netboot/archlinux.ipxe)) and place it to your own http server. Then run in iPXE shell:

```
iPXE> chain http://*yourdomain.com*/path/to/file/archlinux.ipxe

```

replacing *yourdomain.com* and path.
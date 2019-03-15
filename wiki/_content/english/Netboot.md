Netboot images are small (<1MB) images that can be used to download the latest Arch Linux release on the fly upon system boot. It is unnecessary to update the netboot image, the newest release will be available automatically. Netboot images can be downloaded from the [Arch Linux website](https://www.archlinux.org/releng/netboot/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Using ipxe.lkrn](#Using_ipxe.lkrn)
    *   [1.2 Using ipxe.pxe](#Using_ipxe.pxe)
*   [2 UEFI](#UEFI)
    *   [2.1 Installation with efibootmgr](#Installation_with_efibootmgr)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error 022fe2](#Error_022fe2)

## BIOS

To use netboot on a BIOS-based computer, you need either the ipxe.lkrn or ipxe.pxe image.

### Using ipxe.lkrn

The ipxe.lkrn image can be booted like a Linux kernel. Any Linux bootloader (like Grub or syslinux) can be used to load it from your hard drive, a CD or a USB drive. For example, the Syslinux wiki gives instructions to install[[1]](https://wiki.syslinux.org/wiki/index.php?title=Install) and configure[[2]](https://wiki.syslinux.org/wiki/index.php?title=Config) Syslinux on a bootable medium.

You can make flash drive that boots ipxe.lkrn with the following steps:

*   Find out your device path using [lsblk](/index.php/Lsblk "Lsblk"). Let's assume it is /dev/sdc.
*   Create ms-dos partition table on the device.
*   Create a primary partition with FAT32 file system and flag it as active.
*   Mount partition, create ./boot/syslinux directory there and copy ipxe.lkrn to boot directory

```
# mount /dev/sdc /mnt
# mkdir -p /mnt/boot/syslinux
# cp ipxe.lkrn /mnt/boot

```

*   Create config for syslinux

 `/mnt/boot/syslinux/syslinux.cfg ` 
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

*   Install syslinux mbr and syslinux itself

```
# ms-sys --mbrsyslinux /dev/sdc
# syslinux --directory /boot/syslinux/ --install /dev/sdc1

```

*   Now you should be able to boot your usb stick with ipxe.lkrn.

Alternatively, you can also try the image with qemu by running the following command:

```
   qemu-system-x86_64 -enable-kvm -m 1G -kernel ipxe.lkrn

```

### Using ipxe.pxe

The ipxe.pxe image is a PXE image. It can be chainloaded from an existing PXE environment. This allows configuring a DHCP server such that booting from the network will always boot into Arch Linux netboot.

## UEFI

The ipxe.efi image can be used to launch Arch Linux netboot in UEFI mode. Only 64 Bit UEFI is supported. The ipxe.efi image can be added as a boot option via efibootmgr, chainloaded from a boot manager like [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or launched directly from the UEFI shell.

### Installation with efibootmgr

First install the [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) package, then download the [UEFI netboot image](https://www.archlinux.org/releng/netboot/).

Assuming your [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) is mounted under `*esp*`, you should move it as follows - let's also give it a more friendly name:

```
# mkdir *esp*/EFI/arch_netboot
# mv ipxe.*.efi *esp*/EFI/arch_netboot/arch_netboot.efi

```

Then you can create a boot entry as follows:

```
# efibootmgr --create --disk /dev/sda --part 1 --loader /EFI/arch_netboot/arch_netboot.efi --label "Arch Linux Netboot"

```

## Troubleshooting

### Error 022fe2

When loading ipxe.1e77e6bfd61e.efi you get such error:

```
[https://www.archlinux.org/releng/netboot/archlinux.ipxe](https://www.archlinux.org/releng/netboot/archlinux.ipxe)... Permission denied ([http://ipxe.org/022fe28f](http://ipxe.org/022fe28f))

```

When loading ipxe.8da38b4a9310.pxe you get such error:

```
[https://www.archlinux.org/releng/netboot/archlinux.ipxe](https://www.archlinux.org/releng/netboot/archlinux.ipxe)... Permission denied ([http://ipxe.org/022fe23c](http://ipxe.org/022fe23c))

```

This is a bug related to https/ocsp/certificates (see [FS#58470](https://bugs.archlinux.org/task/58470)).

As a workaround, download this file ([https://www.archlinux.org/releng/netboot/archlinux.ipxe](https://www.archlinux.org/releng/netboot/archlinux.ipxe)) and place it to your own http server. Then run in iPXE shell:

```
iPXE> chain http://*yourdomain.com*/path/to/file/archlinux.ipxe

```

replacing *yourdomain.com* and path.
Netboot images are small (<1MB) images that can be used to download the latest Arch Linux release on the fly upon system boot. It is unnecessary to update the netboot image, the newest release will be available automatically. Netboot images can be downloaded from the [Arch Linux website](https://www.archlinux.org/releng/netboot/).

## Contents

*   [1 BIOS](#BIOS)
    *   [1.1 Using ipxe.lkrn](#Using_ipxe.lkrn)
    *   [1.2 Using ipxe.pxe](#Using_ipxe.pxe)
*   [2 UEFI](#UEFI)
    *   [2.1 Installation with efibootmgr](#Installation_with_efibootmgr)

## BIOS

To use netboot on a BIOS-based computer, you need either the ipxe.lkrn or ipxe.pxe image.

### Using ipxe.lkrn

The ipxe.lkrn image can be booted like a Linux kernel. Any Linux bootloader (like Grub or syslinux) can be used to load it from your hard drive, a CD or a USB drive.

You can try the image with qemu by running the following command:

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
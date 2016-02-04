# Boot loaders

The boot loader is the first piece of software started by the [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or [UEFI](/index.php/UEFI "UEFI"). It is responsible for loading the kernel with the wanted [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and [initial RAM disk](/index.php/Mkinitcpio "Mkinitcpio") before initiating the [boot process](/index.php/Boot_process "Boot process"). You can use [different kinds](/index.php/Category:Boot_loaders "Category:Boot loaders") of bootloaders in Arch, such as [GRUB](/index.php/GRUB "GRUB") and [Syslinux](/index.php/Syslinux "Syslinux"). Some bootloaders only support BIOS or UEFI and some support both.

This page contains a short introduction about bootloaders available in Arch. For detailed information see the corresponding pages of each bootloader.

**Note:** Loading [Microcode](/index.php/Microcode "Microcode") updates requires adjustments in boot loader configuration. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

## Contents

*   [1 Both BIOS and UEFI boot loaders](#Both_BIOS_and_UEFI_boot_loaders)
    *   [1.1 GRUB](#GRUB)
    *   [1.2 Syslinux](#Syslinux)
*   [2 UEFI-only boot loaders](#UEFI-only_boot_loaders)
    *   [2.1 Linux Kernel EFISTUB](#Linux_Kernel_EFISTUB)
        *   [2.1.1 systemd-boot](#systemd-boot)
        *   [2.1.2 rEFInd](#rEFInd)
        *   [2.1.3 Clover](#Clover)
    *   [2.2 ELILO](#ELILO)
*   [3 BIOS-only boot loaders](#BIOS-only_boot_loaders)
    *   [3.1 GRUB Legacy](#GRUB_Legacy)
    *   [3.2 LILO](#LILO)
    *   [3.3 NeoGRUB](#NeoGRUB)
*   [4 See also](#See_also)

## Both BIOS and UEFI boot loaders

### GRUB

[GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, and can be automatically generated.

### Syslinux

[Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. An example configuration can be found in [Syslinux#Examples](/index.php/Syslinux#Examples "Syslinux").

## UEFI-only boot loaders

### Linux Kernel EFISTUB

The Linux kernel can be booted directly using the built-in EFI stub loader. See [EFISTUB](/index.php/EFISTUB "EFISTUB").

#### systemd-boot

systemd includes an EFI bootloader which provides a text menu for booting EFISTUB kernels. See [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

#### rEFInd

rEFInd is a UEFI Boot Manager which provides a graphical menu for booting EFISTUB kernels. See [rEFInd](/index.php/REFInd "REFInd").

#### Clover

Clover is a UEFI Boot Manager which provides native resolution GUI for booting EFISTUB kernels. See [Clover](/index.php/Clover "Clover").

### ELILO

**Warning:** ELILO upstream has clarified that it is no longer in active development, meaning no new features will be added and only bug-fixes are released. See [https://sourceforge.net/mailarchive/message.php?msg_id=31524008](https://sourceforge.net/mailarchive/message.php?msg_id=31524008) for more information. ELILO is not officially supported by Arch developers.

ELILO is the UEFI version of the BIOS-only [LILO](/index.php/LILO "LILO"). Its config file `elilo.conf` is similar to [LILO](/index.php/LILO "LILO")'s config file. Upstream provided compiled binaries are available at [http://sourceforge.net/projects/elilo/](http://sourceforge.net/projects/elilo/) and an AUR package at [elilo-efi](https://aur.archlinux.org/packages/elilo-efi/).

## BIOS-only boot loaders

**Warning:** None of the options presented here are officialy supported in Arch Linux.

### GRUB Legacy

GRUB Legacy (also known as grub-0.97), is the legacy, BIOS-only branch of [GRUB](/index.php/GRUB "GRUB"). See [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

### LILO

See [LILO](/index.php/LILO "LILO").

### NeoGRUB

NeoGRUB provides a means to boot Arch from the Windows boot loader without installing an additional boot loader. See [NeoGRUB](/index.php/NeoGRUB "NeoGRUB").

Booting Arch from NeoGRUB has not been tested yet from Windows 8 and/or UEFI systems.

## See also

*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Rod Smith - rEFInd, a fork or rEFIt](http://www.rodsbooks.com/refind/)
*   [Linux Kernel Documentation on EFISTUB](https://www.kernel.org/doc/Documentation/efi-stub.txt)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)
*   [rEFInd Documentation for booting EFISTUB Kernels](http://www.rodsbooks.com/refind/linux.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Boot_loaders&oldid=397545](https://wiki.archlinux.org/index.php?title=Boot_loaders&oldid=397545)"
Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

The Linux Kernel ([linux](https://www.archlinux.org/packages/?name=linux)>=3.3) supports EFISTUB (EFI BOOT STUB) booting. This feature allows EFI firmware to load the kernel as an EFI executable. The option is enabled by default on Arch Linux kernels or can be activated by setting `CONFIG_EFI_STUB=y` in the Kernel configuration (see [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) for more information).

An EFISTUB kernel can be booted directly by a UEFI motherboard or indirectly using a [boot loader](/index.php/Boot_loader "Boot loader"). The latter is recommended if you have multiple kernel/initramfs pairs and your motherboard's UEFI boot menu is not easy to use.

## Contents

*   [1 Setting up EFISTUB](#Setting_up_EFISTUB)
*   [2 Booting EFISTUB](#Booting_EFISTUB)
    *   [2.1 Using a boot manager](#Using_a_boot_manager)
    *   [2.2 Using UEFI Shell](#Using_UEFI_Shell)
    *   [2.3 Using UEFI directly](#Using_UEFI_directly)
        *   [2.3.1 efibootmgr](#efibootmgr)
        *   [2.3.2 efibootmgr with .efi file](#efibootmgr_with_.efi_file)
        *   [2.3.3 UEFI Shell](#UEFI_Shell)
        *   [2.3.4 Using a startup.nsh script](#Using_a_startup.nsh_script)

## Setting up EFISTUB

After creating the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition"), you must choose how it will be mounted. The simplest option is to mount it at `/boot` since this allows pacman to directly update the kernel that the EFI firmware will read. If you elect for this option, continue to [#Booting EFISTUB](#Booting_EFISTUB). See [EFI System Partition#Mount the partition](/index.php/EFI_System_Partition#Mount_the_partition "EFI System Partition") for all available ESP mounting options options.

**Tip:** You can keep kernel and initramfs out of ESP if you use a boot manager which has a file system driver for the partition where they reside, e.g. [rEFInd](/index.php/REFInd "REFInd").

## Booting EFISTUB

**Note:** Linux Kernel EFISTUB initramfs path should be relative to the EFI System Partition's root. For example, if the initramfs is located in `*esp*/EFI/arch/initramfs-linux.img`, the corresponding UEFI formatted line should be `initrd=/EFI/arch/initramfs-linux.img` or `initrd=\EFI\arch\initramfs-linux.img`. In the following examples we will assume that everything is in `*esp*/`.

### Using a boot manager

There are several UEFI boot managers which can provide additional options or simplify the process of UEFI booting - especially if you have multiple kernels/operating systems. See [Boot loaders](/index.php/Boot_loaders "Boot loaders") for more information.

### Using UEFI Shell

It is possible to launch an EFISTUB kernel from UEFI Shell as if it is a normal UEFI application. In this case the kernel parameters are passed as normal parameters to the launched EFISTUB kernel file.

```
> fs0:
> \vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rw initrd=/initramfs-linux.img

```

To avoid needing to remember all of your kernel parameters every time, you can save the executable command to a shell script such as `archlinux.nsh` on your UEFI System Partition, then run it with:

```
> fs0:
> archlinux

```

### Using UEFI directly

UEFI is designed to remove the need for an intermediate bootloader such as [GRUB](/index.php/GRUB "GRUB"). If your motherboard has a good UEFI implementation, it is possible to embed the kernel parameters within a UEFI boot entry and for the motherboard to boot Arch directly. You can use [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) or UEFI Shell v2 to modify your motherboard's boot entries.

#### efibootmgr

The command looks like

```
# efibootmgr --disk */dev/sdX* --part *Y* --create --gpt --label "Arch Linux" --loader /vmlinuz-linux --unicode "root=*/dev/sdBZ* rw initrd=/initramfs-linux.img"

```

Where `*/dev/sdX*` and `*Y*` are the disk and partition where the ESP is located. Change the `root=` parameter to reflect your Linux root (disk [UUIDs](/index.php/UUID "UUID") can also be used). Note that the `-u`/`--unicode` argument in double quotes is just the list of [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), so you may need to add additional parameters e.g. for [suspend to disk](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate") or [microcode](/index.php/Microcode "Microcode").

It is a good idea to then run

```
# efibootmgr --verbose

```

to verify that the resulting entry is correct.

**Note:** Some kernel and `efibootmgr` version combinations might refuse to create new boot entries. This could be due to lack of free space in the NVRAM. You can try deleting any EFI dump files
```
# rm /sys/firmware/efi/efivars/dump-*

```

Or, as a last resort, boot with the `efi_no_storage_paranoia` kernel parameter. You can also try to downgrade your efibootmgr install to version 0.11.0 if you have it available in your cache. This version works with Linux version 4.0.6\. See the bug discussion [FS#34641](https://bugs.archlinux.org/task/34641) for more information.

To set the boot order, run:

```
# efibootmgr --bootorder *XXXX*,*XXXX*

```

where *XXXX* is the number that appears in the output of `efibootmgr` command against each entry.

**Tip:** Save the command for creating your boot entry in a shell script somewhere, which makes it easier to modify (when changing kernel parameters, for example).

More info about efibootmgr at [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI"). Forum post [https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) .

#### efibootmgr with .efi file

If using [cryptboot](https://aur.archlinux.org/packages/cryptboot/) and [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/) to generate your own keys for [Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot") and sign the initramfs and kernel then create a bootable .efi image, [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) can be used directly to boot the .efi file:

 `efibootmgr -c -d /dev/sdX -p 1 -L "Arch Linux Signed" -l "EFI\Arch\linux-signed.efi"` 

-c create, -d disk, -p partition number (change it if it is not 1), -L label, and -l boot loader

#### UEFI Shell

Some UEFI implementations make it difficult to modify the NVRAM successfully using efibootmgr. If efibootmgr cannot successfully create an entry, you can use the [bcfg](/index.php/UEFI#bcfg "UEFI") command in UEFI Shell v2.

To add an entry for your kernel, use:

```
Shell> bcfg boot add **N** fs**V**:\vmlinuz-linux "Arch Linux"

```

where `N` is the priority (0 is top priority) and `V` is the volume number representing your EFI partition. If you don't know which volume number you should use, use the map command to list file systems, and the ls command to list their contents:

```
Shell> map
Shell> ls fs0:

```

To add the bare minimum necessary kernel options, use:

```
Shell> bcfg boot -opt **N** "root=**/dev/sdX#** rw initrd=\initramfs-linux.img"

```

where `N` is the priority number you selected in the first step, and `/dev/sdX#` represents your root partition.

#### Using a startup.nsh script

Some UEFI implementations do not retain EFI variables between cold boots (e.g. [VirtualBox](/index.php/VirtualBox "VirtualBox")) and anything set through the UEFI firmware interface is lost on poweroff.

The [UEFI Shell Specification 2.0](http://www.uefi.org/sites/default/files/resources/UEFI_Shell_Spec_2_0.pdf) establishes that a script called `startup.nsh` at the root of the ESP partition will always be interpreted and can contain arbitrary instructions; among those you can set a bootloading line. Make sure you mount the ESP partition on `/boot` and create a `startup.nsh` script that contains a kernel bootloading line. For example:

```
vmlinuz-linux rw root=/dev/sdX [rootfs=myfs] [rootflags=myrootflags] \
 [kernel.flag=foo] [mymodule.flag=bar] \
 [initrd=\intel-ucode.img] initrd=\initramfs-linux.img

```

This method will work with almost all UEFI firmware versions you may encounter in real hardware, you can use it as last resort. **The script must be a single long line.** Sections in brackets are optional and given only as a guide. Shell style linebreaks are for visual clarification only. FAT filesystems use the backslash as path separator and in this case, the backslash declares the initramfs is located in the root of the ESP partition. Only Intel microcode is loaded in the booting parameters line; AMD microcode is read from disk later during the boot process; this is done automatically by the kernel.
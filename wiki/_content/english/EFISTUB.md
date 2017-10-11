Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

The Linux Kernel ([linux](https://www.archlinux.org/packages/?name=linux)>=3.3) supports EFISTUB (EFI BOOT STUB) booting. This feature allows EFI firmware to load the kernel as an EFI executable. The option is enabled by default on Arch Linux kernels or can be activated by setting `CONFIG_EFI_STUB=y` in the Kernel configuration (see [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) for more information).

An EFISTUB kernel can be booted directly by a UEFI motherboard or indirectly using a [boot loader](/index.php/Boot_loader "Boot loader"). The latter is recommended if you have multiple kernel/initramfs pairs and your motherboard's UEFI boot menu is not easy to use.

## Contents

*   [1 Setting up EFISTUB](#Setting_up_EFISTUB)
    *   [1.1 Alternative ESP Mount Points](#Alternative_ESP_Mount_Points)
        *   [1.1.1 Using systemd](#Using_systemd)
        *   [1.1.2 Using incron](#Using_incron)
        *   [1.1.3 Using mkinitcpio hook](#Using_mkinitcpio_hook)
        *   [1.1.4 Using mkinitcpio hook (2)](#Using_mkinitcpio_hook_.282.29)
*   [2 Booting EFISTUB](#Booting_EFISTUB)
    *   [2.1 Using a boot manager](#Using_a_boot_manager)
    *   [2.2 Using UEFI Shell](#Using_UEFI_Shell)
    *   [2.3 Using UEFI directly](#Using_UEFI_directly)
        *   [2.3.1 efibootmgr](#efibootmgr)
        *   [2.3.2 UEFI Shell](#UEFI_Shell)
        *   [2.3.3 Using a startup.nsh script](#Using_a_startup.nsh_script)

## Setting up EFISTUB

After creating the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition"), you must choose how it will be mounted. The simplest option is to mount it at `/boot` or [bind mount](/index.php/EFI_System_Partition#Using_bind_mount "EFI System Partition") it to `/boot` since this allows pacman to directly update the kernel that the EFI firmware will read. If you elect for this option, continue to [#Booting EFISTUB](#Booting_EFISTUB).

**Note:** You can keep kernel and initramfs out of ESP if you use a boot manager which has a file system driver for the partition where they reside, e.g. [rEFInd](/index.php/REFInd "REFInd").

### Alternative ESP Mount Points

If you do not mount the EFI System Partition to `/boot`, you will need to copy your boot files to its location (referred to hereafter as `*esp*`).

```
# mkdir -p *esp*/EFI/arch
# cp /boot/vmlinuz-linux *esp*/EFI/arch/vmlinuz-linux
# cp /boot/initramfs-linux.img *esp*/EFI/arch/initramfs-linux.img
# cp /boot/initramfs-linux-fallback.img *esp*/EFI/arch/initramfs-linux-fallback.img

```

**Note:** When using an Intel CPU, you may need to copy the [Microcode](/index.php/Microcode "Microcode") to the boot-entry location.

Furthermore, you will need to keep the files on the ESP up-to-date with later kernel updates. Failure to do so could result in an unbootable system. The following sections discuss several mechanisms for automating it.

#### Using systemd

[Systemd](/index.php/Systemd "Systemd") features event triggered tasks. In this particular case, the ability to detect a change in path is used to sync the EFISTUB kernel and initramfs files when they are updated in `/boot`.

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI System Partition

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target
WantedBy=system-update.target
```

**Note:** This watches for changes to `initramfs-linux-fallback.img` since this is the last file built by mkinitcpio. This is to avoid a potential race condition where systemd could copy older files before they are all done being built.
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI System Partition

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -f /boot/vmlinuz-linux *esp*/EFI/arch/vmlinuz-linux
ExecStart=/usr/bin/cp -f /boot/initramfs-linux.img *esp*/EFI/arch/initramfs-linux.img
ExecStart=/usr/bin/cp -f /boot/initramfs-linux-fallback.img *esp*/EFI/arch/initramfs-linux-fallback.img
```

**Tip:** For [Secure Boot](/index.php/Secure_Boot "Secure Boot") (with your own keys), you can set up the service to also sign the image (using [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools)): `ExecStart=/usr/bin/sbsign --key */path/to/db.key* --cert */path/to/db.crt* --output *esp*/EFI/arch/vmlinuz-linux *esp*/EFI/arch/vmlinuz_linux` 

Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `efistub-update.path`.

#### Using incron

[incron](https://www.archlinux.org/packages/?name=incron) can be used to run a script syncing the EFISTUB Kernel after kernel updates.

 `/usr/local/bin/efistub-update.sh` 
```
#!/usr/bin/env bash
/usr/bin/cp -f /boot/vmlinuz-linux *esp*/EFI/arch/vmlinuz-linux
/usr/bin/cp -f /boot/initramfs-linux.img *esp*/EFI/arch/initramfs-linux.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img *esp*/EFI/arch/initramfs-linux-fallback.img

```

**Note:** The first parameter `/boot/initramfs-linux-fallback.img` is the file to watch. The second parameter `IN_CLOSE_WRITE` is the action to watch for. The third parameter `/usr/local/bin/efistub-update.sh` is the script to execute.
 `/etc/incron.d/efistub-update.conf` 
```
/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update.sh

```

In order to use this method, [enable](/index.php/Enable "Enable") the `incrond.service`.

#### Using mkinitcpio hook

Mkinitcpio can generate a hook that does not need a system level daemon to function. It spawns a background process which waits for the generation of `vm-linuz`, `initramfs-linux.img`, and `initramfs-linux-fallback.img` before copying the files.

Add `efistub-update` to the list of hooks in `/etc/mkinitcpio.conf`.

 `/usr/lib/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/root/watch.sh &
}

help() {
	cat <<HELPEOF
This hook waits for mkinitcpio to finish and copies the finished ramdisk and kernel to the ESP
HELPEOF
}

```
 `/root/watch.sh` 
```
#!/usr/bin/env bash

while [[ -d "/proc/$PPID" ]]; do
	sleep 1
done

/usr/bin/cp -f /boot/vmlinuz-linux *esp*/EFI/arch/vmlinuz-linux
/usr/bin/cp -f /boot/initramfs-linux.img *esp*/EFI/arch/initramfs-linux.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img *esp*/EFI/arch/initramfs-linux-fallback.img

echo "Synced kernel with ESP"

```

#### Using mkinitcpio hook (2)

Another **alternative** to the above solutions, that is potentially cleaner because there are less copies and does not need a system level daemon to function. The logic is reversed, the initramfs is directly stored in the EFI partition, not copied in /boot. Then the kernel and any other additional files are copied to the ESP partition, thanks to a mkinitcpio hook.

Edit the file `/etc/mkinitcpio.d/linux.preset` :

 `/etc/mkinitcpio.d/linux.preset` 
```
# mkinitcpio preset file for the 'linux' package

# Directory to copy the kernel, the initramfs...
ESP_DIR="/boot/efi/EFI/arch"

ALL_config="/etc/mkinitcpio.conf"
ALL_kver="/boot/vmlinuz-linux"

PRESETS=('default' 'fallback')

#default_config="/etc/mkinitcpio.conf"
default_image="${ESP_DIR}/initramfs-linux.img"
default_options="-A esp-update-linux"

#fallback_config="/etc/mkinitcpio.conf"
fallback_image="${ESP_DIR}/initramfs-linux-fallback.img"
fallback_options="-S autodetect"

```

Then create the file `/usr/lib/initcpio/install/esp-update-linux` which need to be executable :

 `/usr/lib/initcpio/install/esp-update-linux` 
```
# Directory to copy the kernel, the initramfs...
ESP_DIR="/boot/efi/EFI/arch"

build() {
	cp /boot/vmlinuz-linux "${ESP_DIR}/vmlinuz-linux.efi"
	# If ucode is used uncomment this line
	#cp /boot/intel-ucode.img "${ESP_DIR}/"
}

help() {
	cat <<HELPEOF
This hook copies the kernel to the ESP partition
HELPEOF
}

```

To test that, just run:

```
rm /boot/initramfs-linux-fallback.img
rm /boot/initramfs-linux.img
mkinitcpio -p linux

```

## Booting EFISTUB

**Warning:** Linux Kernel EFISTUB initramfs path should be relative to the EFI System Partition's root. For example, if the initramfs is located in `*esp*/EFI/arch/initramfs-linux.img`, the corresponding UEFI formatted line should be `initrd=/EFI/arch/initramfs-linux.img` or `initrd=\EFI\arch\initramfs-linux.img`. In the following examples we will assume that everything is in `*esp*/`.

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
# efibootmgr -d */dev/sdX* -p *Y* -c -g -L "Arch Linux" -l /vmlinuz-linux -u "root=*/dev/sdBZ* rw initrd=/initramfs-linux.img"

```

Where `*/dev/sdX*` and `*Y*` are the disk and partition where the ESP is located. Change the `root=` parameter to reflect your Linux root (disk UUIDs can also be used). Note that the `-u` argument in double quotes is just the list of [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), so you may need to add additional parameters e.g. for [suspend to disk](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate") or [microcode](/index.php/Microcode "Microcode").

It is a good idea to then run

```
# efibootmgr -v

```

to verify that the resulting entry is correct.

**Warning:** Some kernel and `efibootmgr` version combinations might refuse to create new boot entries. This could be due to lack of free space in the NVRAM. You can try deleting any EFI dump files
```
# rm /sys/firmware/efi/efivars/dump-*

```
Or, as a last resort, boot with the `efi_no_storage_paranoia` kernel parameter. You can also try to downgrade your efibootmgr install to version 0.11.0 if you have it available in your cache. This version works with Linux version 4.0.6\. See the bug discussion [FS#34641](https://bugs.archlinux.org/task/34641) for more information.

To set the boot order, run:

```
# efibootmgr -o XXXX,XXXX

```

where XXXX is the number that appears in the output of `efibootmgr` command against each entry.

**Tip:** Save the command for creating your boot entry in a shell script somewhere, which makes it easier to modify (when changing kernel parameters, for example).

More info about efibootmgr at [UEFI#efibootmgr](/index.php/UEFI#efibootmgr "UEFI"). Forum post [https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) .

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
rEFInd is a [UEFI](/index.php/UEFI "UEFI") boot manager. It is a fork of the no-longer-maintained [rEFIt](http://refit.sourceforge.net/) and fixes many issues with respect to non-Mac UEFI booting. It is designed to be platform-neutral and to simplify booting multiple OSes.

**Note:** In the entire article `$esp` denotes the mountpoint of the [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI") aka ESP.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Scripted installation](#Scripted_installation)
    *   [1.2 Manual installation](#Manual_installation)
    *   [1.3 Upgrading](#Upgrading)
        *   [1.3.1 Systemd automation](#Systemd_automation)
*   [2 Configuration](#Configuration)
    *   [2.1 Passing kernel parameters](#Passing_kernel_parameters)
        *   [2.1.1 For kernels automatically detected by rEFInd](#For_kernels_automatically_detected_by_rEFInd)
        *   [2.1.2 Manual boot stanzas](#Manual_boot_stanzas)
*   [3 Using rEFInd with an existing UEFI Windows installation](#Using_rEFInd_with_an_existing_UEFI_Windows_installation)
*   [4 Tools](#Tools)
    *   [4.1 UEFI shell](#UEFI_shell)
    *   [4.2 Memtest86](#Memtest86)
    *   [4.3 GPT fdisk (gdisk)](#GPT_fdisk_.28gdisk.29)
    *   [4.4 iPXE](#iPXE)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Using drivers in UEFI shell](#Using_drivers_in_UEFI_shell)
    *   [5.2 btrfs subvolume root support](#btrfs_subvolume_root_support)
    *   [5.3 Apple Macs](#Apple_Macs)
    *   [5.4 VirtualBox](#VirtualBox)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) from the [Official repositories](/index.php/Official_repositories "Official repositories").

**Warning:** Your kernel and initramfs need to reside on a file system which rEFInd can read.

rEFInd has **read-only** drivers for ReiserFS, Ext2, Ext4, Btrfs, ISO-9660, HFS+, and NTFS. Additionally rEFInd can use drivers from the UEFI firmware i.e. FAT (or HFS+ on Macs or ISO-9660 on some systems).

To find additional drivers see [The rEFInd Boot Manager: Using EFI Drivers: Finding Additional EFI Drivers](http://www.rodsbooks.com/refind/drivers.html#finding).

### Scripted installation

The rEFInd package includes the `/usr/bin/refind-install` script to simplify the process of setting rEFInd as your default EFI boot entry. The script has several options for handling differing setups and UEFI implementations, but for many systems it should be sufficient to simply run

```
# refind-install

```

This will attempt to find and mount your [ESP](/index.php/UEFI#EFI_System_Partition "UEFI"), copy rEFInd's files to `/EFI/refind/` on the ESP, and use `efibootmgr` to make rEFInd the default EFI boot application.

Alternatively you can install rEFInd to the default/fallback boot path `/EFI/BOOT/BOOT*.EFI`. This is helpful for bootable USB flash drives or on systems that have issues with the NVRAM changes made by efibootmgr:

```
# refind-install --usedefault **/dev/sdXY**

```

Where **/dev/sdXY** is the partition of your ESP.

You can read the comments in the install script for explanations of the various installation options.

**Note:** By default `refind-install` installs only the driver for the file system on which kernel resides. Additional file systems need to be installed manually or you can install all drivers with the `--alldrivers` option. This is useful for bootable USB flash drives e.g.
```
# refind-install --usedefault /dev/sdXY --alldrivers

```

After installing rEFInd's files to the ESP, verify that rEFInd has created `refind_linux.conf` containing the required [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") (e.g. `root=`) in the same directory as your kernel. If it has not created this file, you will need to set up [#Passing kernel parameters](#Passing_kernel_parameters) manually or you will most likely get a kernel panic on your next boot.

By default, rEFInd will scan all of your drives (that it has drivers for) and add a boot entry for each EFI bootloader it finds, which should include your kernel (since Arch enables [EFISTUB](/index.php/EFISTUB "EFISTUB") by default). So you may have a bootable system at this point.

**Tip:** It is always a good idea to edit the default config `/EFI/refind/refind.conf` on the ESP to ensure that the default options work for you.

### Manual installation

**Tip:** rEFInd can boot Linux in many ways. See [The rEFInd Boot Manager: Methods of Booting Linux](http://www.rodsbooks.com/refind/linux.html) for coverage of the various approaches.

**Note:** For 32-bit EFI, replace **x64** with **ia32** in the commands below.

If the `refind-install` script does not work for you, rEFInd can be set up manually.

First, copy the executable to the ESP:

```
# cp /usr/share/refind/refind_x64.efi $esp/EFI/refind/

```

Then use [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") to create a boot entry in the UEFI NVRAM (change X and Y to match the device and partition of your ESP). If you are installing rEFInd to the default UEFI path `/EFI/BOOT/BOOTX64.EFI`, you can probably skip this step.

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd Boot Manager"

```

At this point, you should be able to reboot into rEFInd but it will not be able to boot your kernel. If your kernel does not reside on your ESP, rEFInd can mount your partitions to find it - provided it has the right drivers:

```
# mkdir $esp/EFI/refind/drivers_x64
# cp /usr/share/refind/drivers_x64/**drivername**_x64.efi $esp/EFI/refind/drivers_x64/

```

rEFInd automatically loads all drivers from the subdirectories `drivers` and `drivers_*arch*` (e.g. `drivers_x64`) in its install directory.

```
# cp /usr/share/refind/drivers_x64/**drivername**_x64.efi $esp/EFI/refind/drivers_x64/

```

Now rEFInd should have a boot entry for your kernel, but it will not pass the correct kernel parameters. Set up [#Passing kernel parameters](#Passing_kernel_parameters). You should now be able to boot your kernel using rEFInd. If you are still unable to boot or if you want to tweak rEFInd's settings, many options can be changed with a config file:

```
# cp /usr/share/refind/refind.conf-sample $esp/EFI/refind/refind.conf

```

The sample config is well commented and self-explanatory.

Unless you have set `textonly` in the config file, you should copy rEFInd's icons to get rid of the ugly placeholders:

```
# cp -r /usr/share/refind/icons $esp/EFI/refind/

```

You can try out different fonts by copying them and changing the `font` setting in `refind.conf`:

```
# cp -r /usr/share/refind/fonts $esp/EFI/refind/

```

**Tip:** Pressing F10 in rEFInd will save a screenshot to the top level directory of the ESP.

### Upgrading

Pacman updates the rEFInd files in `/usr/share/refind` and will not copy new files to the ESP for you. If `refind-install` worked for your original installation of rEFInd, you can rerun it to copy the updated files. The new config file will be copied as `refind.conf-sample` so that you can integrate changes into your config file using a diff tool. If your rEFInd required [#Manual installation](#Manual_installation), you will need to copy the new files yourself.

#### Systemd automation

To automate this process, you need a .path file for watching for rEFInd updates and a .service file for copying the new files and updating the nvram.

 `/etc/systemd/system/refind_update.path` 
```
[Unit]
Description=path monitor for rEFInd updates

[Path]
PathChanged=/usr/share/refind

[Install]
WantedBy=multi-user.target

```
 `/etc/systemd/system/refind_update.service` 
```
[Unit]
Description=rEFInd boot manager update

[Service]
Type=oneshot
ExecStart=/usr/bin/refind-install

```

Then [enable](/index.php/Enable "Enable") `refind_update.path`.

## Configuration

The rEFInd configuration `refind.conf` is located in the same directory as the rEFInd EFI application (usually `$esp/EFI/refind` or `$esp/EFI/BOOT`). The default config contains extensive comments explaining all its options.

### Passing kernel parameters

There are two methods for setting the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") that rEFInd will pass to the kernel.

#### For kernels automatically detected by rEFInd

If rEFInd automatically detects your kernel, you can place a `refind_linux.conf` file containing the kernel parameters in the same directory as your kernel. You can use `/usr/share/refind/refind_linux.conf-sample` as a starting point. The first uncommented line of `refind_linux.conf` will be the default parameters for the kernel. Subsequent lines will create entries in a submenu accessible using `+`, `F2`, or `Insert`.

 `/boot/refind_linux.conf` 
```
"Boot using default options"     "root=PARTUUID=XXXXXXXX rw add_efi_memmap"
"Boot to terminal"               "root=PARTUUID=XXXXXXXX rw add_efi_memmap systemd.unit=multi-user.target"
"Boot using fallback initramfs"  "root=PARTUUID=XXXXXXXX rw add_efi_memmap initrd=initramfs-linux-fallback.img"

```

Alternatively, try running:

```
# refind-mkrlconf

```

Which will attempt to find your kernel in `/boot` and automatically generate `refind_linux.conf`. The script will only set up the most basic kernel parameters, so be sure to check the file it created for correctness.

If you do not specify an `initrd=` parameter, rEFInd will automatically add it by searching for common RAM disk filenames in the same directory as the kernel. If you need multiple `initrd=` parameters (e.g. for [Microcode](/index.php/Microcode "Microcode")) you must specify them manually in `refind_linux.conf`.

#### Manual boot stanzas

If your kernel is not autodetected, or if you simply want more control over the options for a menu entry, you can manually create boot entries using stanzas in `refind.conf`. Ensure that `scanfor` includes `manual` or these entries will not appear in rEFInd's menu. Kernel parameters are set with the `options` keyword. rEFInd will append the `initrd=` parameter using the file specified by the `initrd` keyword in the stanza. If you need additional initrds (e.g. for [Microcode](/index.php/Microcode "Microcode")), you can specify them in `options` (and the one specified by the `initrd` keyword will be added to the end).

 `$esp/EFI/refind/refind.conf` 
```
...

menuentry "Arch Linux" {
	icon     /EFI/refind/icons/os_arch.png
	volume   "Arch Linux"
	loader   /boot/vmlinuz-linux
	initrd   /boot/initramfs-linux.img
	options  "root=PARTUUID=XXXXXXXX rw add_efi_memmap"
	submenuentry "Boot using fallback initramfs" {
		initrd /boot/initramfs-linux-fallback.img
	}
	submenuentry "Boot to terminal" {
		add_options "systemd.unit=multi-user.target"

}

```

It is likely that you will need to change `volume` to match either a filesystem's LABEL, a PARTLABEL, or a PARTUUID of the partition where the kernel image resides. See [Ext3#Assigning a label](/index.php/Ext3#Assigning_a_label "Ext3") as an example of assigning a volume label.

## Using rEFInd with an existing UEFI Windows installation

**Note:** The usual caveats of [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") apply.

rEFInd is compatible with the EFI system partition created by a UEFI Windows installation, so there is no need to create or format another FAT32 partition when installing Arch alongside Windows. Simply mount the existing ESP and install rEFInd as usual. By default, rEFInd's autodetection feature should recognize any existing Windows/recovery bootloaders.

## Tools

rEFInd supports running various 3rd-party tools. Tools need to be installed separately. Edit `showtools` in `refind.conf` to choose which ones to show.

 `$esp/EFI/refind/refind.conf` 
```
...
showtools **shell**, **memtest**, **gdisk**, **netboot**, ...
...

```

### UEFI shell

See [UEFI shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface").

Copy `shellx64.efi` to the root of the [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")

### Memtest86

Install [memtest86-efi](https://aur.archlinux.org/packages/memtest86-efi/) and copy it to `$esp/EFI/tools/`.

```
# cp /usr/share/memtest86-efi/bootx64.efi $esp/EFI/tools/memtest86.efi

```

### GPT fdisk (gdisk)

There is no package for the EFI version of gdisk, but you can download a binary from gdisk's author.

Download `gdisk-efi-*.zip` from [SourceForge](http://sourceforge.net/projects/gptfdisk/files/gptfdisk/), extract the archive, and copy `gdisk_x64.efi` to `$esp/EFI/tools`.

### iPXE

**Note:** PXE support in rEFInd is **experimental**.

[refind-efi](https://www.archlinux.org/packages/?name=refind-efi) contains the iPXE UEFI binaries, you just need to copy them to `$esp/EFI/tools/`.

```
# cp /usr/share/refind/tools_x64/ipxe_discovery_x64.efi $esp/EFI/tools/ipxe_discovery.efi
# cp /usr/share/refind/tools_x64/ipxe_x64.efi $esp/EFI/tools/ipxe.efi

```

## Troubleshooting

### Using drivers in UEFI shell

To use rEFInd's drivers in UEFI shell load them using command `load` and refresh mapped drives with `map -r`.

```
# load FS0:\EFI\refind\drivers\ext4_x64.efi
# map -r

```

Now you can access your file system from UEFI shell.

### btrfs subvolume root support

If booting a [btrfs](/index.php/Btrfs "Btrfs") subvolume as root, amend the `options` line with `rootflags=subvol=<root subvolume>`. In the example below, root has been mounted as a btrfs subvolume called 'ROOT' (e.g. `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `$esp/EFI/refind/refind.conf` 
```
...

menuentry "Arch Linux" {
        icon     /EFI/refind/icons/os_arch.png
        volume   Boot
        loader   /boot/vmlinuz-linux
        initrd   /boot/initramfs-linux.img
        options  "root=PARTUUID=XXXXXXXX rw rootflags=subvol=ROOT"

...
        }

```

A failure to do so will otherwise result in the following error message: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

### Apple Macs

[mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) is an experimental "bless" utility for Linux. If that does not work, use "bless" from within OSX to set rEFInd as the default boot entry. Assuming your UEFISYS partition is mounted at `/mnt/efi` within OSX, do:

```
# bless --setBoot --folder /mnt/efi/EFI/refind --file /mnt/efi/EFI/refind/refind_x64.efi

```

### VirtualBox

Currently, VirtualBox will only boot the default `/EFI/BOOT/BOOT*.EFI` path, so `refind-install` needs to be used with at least the `--usedefault` option. See [VirtualBox#Installation in EFI mode](/index.php/VirtualBox#Installation_in_EFI_mode "VirtualBox") for more information.

## See also

*   [The rEFInd Boot Manager](http://www.rodsbooks.com/refind/) by Roderick W. Smith.
*   `/usr/share/refind/docs/README.txt`
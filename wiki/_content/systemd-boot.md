# systemd-boot

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**systemd-boot** (previously called **gummiboot**), is a simple UEFI boot manager which executes configured EFI images. The default entry is selected by a configured pattern (glob) or an on-screen menu. It is included with systemd since [systemd](https://www.archlinux.org/packages/?name=systemd) 220-2.

It is simple to configure, but can only start EFI executables, such as the Linux kernel [EFISTUB](/index.php/EFISTUB "EFISTUB"), UEFI Shell, GRUB, the Windows Boot Manager, and such.

**Warning:** systemd-boot simply provides a boot menu for EFISTUB kernels. In case you have issues booting EFISTUB kernels like in [FS#33745](https://bugs.archlinux.org/task/33745), you should use a boot loader which does not use EFISTUB, like [GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") or [ELILO](/index.php/Boot_loaders#ELILO "Boot loaders").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 EFI boot](#EFI_boot)
    *   [1.2 Legacy boot](#Legacy_boot)
    *   [1.3 Updating](#Updating)
*   [2 Configuration](#Configuration)
    *   [2.1 Basic configuration](#Basic_configuration)
    *   [2.2 Adding boot entries](#Adding_boot_entries)
        *   [2.2.1 Standard root installations](#Standard_root_installations)
        *   [2.2.2 LVM root installations](#LVM_root_installations)
        *   [2.2.3 Encrypted Root Installations](#Encrypted_Root_Installations)
        *   [2.2.4 btrfs subvolume root installations](#btrfs_subvolume_root_installations)
        *   [2.2.5 EFI Shells or other EFI apps](#EFI_Shells_or_other_EFI_apps)
    *   [2.3 Support hibernation](#Support_hibernation)
*   [3 Keys inside the boot menu](#Keys_inside_the_boot_menu)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Manual entry using efibootmgr](#Manual_entry_using_efibootmgr)
    *   [4.2 Menu does not appear after Windows upgrade](#Menu_does_not_appear_after_Windows_upgrade)
*   [5 See also](#See_also)

## Installation

### EFI boot

1.  Make sure you are booted in UEFI mode.
2.  Verify [your EFI variables are accessible](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Mount your [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")(ESP) properly. `$esp` is used to denotes the mountpoint in this article.

    **Note:** systemd-boot cannot load EFI binaries from other partitions. It is therefore recommended to mount your ESP to `/boot`. See [#Updating](#Updating) for more information and work-around, in case you want to separate `/boot` from the ESP.

4.  Copy your kernel and initramfs onto that ESP.
5.  Finally, Type the following command to install systemd-boot: `# bootctl --path=_$esp_ install` It will copy the systemd-boot binary to your EFI System Partition (`$esp/EFI/boot/systemd-bootx64.efi` on x64 systems) and add systemd-boot itself as the default EFI application (default boot entry) loaded by the EFI Boot Manager.

### Legacy boot

**Warning:** This is not the recommended process

You can also successfully install systemd-boot if booted with a legacy OS. However, this requires that you later on tell your firmware to launch systemd-boot's EFI file on boot:

*   you either have a working EFI shell somewhere;
*   or your firmware interface provides you with a way of properly setting the EFI file that will be loaded at boot time.

**Note:** E.g. on Dell's Latitude series, the firmware interface provides everything you need to setup EFI boot, and the EFI Shell won't be able to write to the computer's ROM.

If you can do so, the installation is easier: go into your EFI shell or your firmware configuration interface, and change your machine's default EFI file to `/$esp/EFI/boot/systemd-bootx64.efi` (`systemd-bootia32.efi` on i686 systems).

### Updating

systemd-boot (bootctl(1), systemd-efi-boot-generator(8)) assumes that your EFI System Partition is mounted on `/boot`. Unlike the previous separate _gummiboot_ package, which updated automatically on a new package release with a `post_install` script, updates of new systemd-boot versions are now handled manually by the user:

```
# bootctl update  

```

If the ESP is not mounted on `/boot`, the `--path=` option can pass it. For example:

```
# bootctl --path=/boot/$esp update

```

## Configuration

### Basic configuration

The basic configuration is kept in `$esp/loader/loader.conf`, with three possible configuration options:

*   `default` – default entry to select (without the `.conf` suffix); can be a wildcard like `arch-*`

*   `timeout` – menu timeout in seconds. If this is not set, the menu will only be shown when you hold the space key while booting.

*   `editor` - whether to enable the kernel parameters editor or not. `1` (default) is to enable, `0` is to disable. Since the user can add `init=/bin/bash` to bypass root password and gain root access, it's strongly recommended to set this option to `0`.

Example:

 `$esp/loader/loader.conf` 

```
default  arch
timeout  4
editor   0

```

Note that the first 2 options can be changed in the boot menu itself, which will store them as EFI variables.

### Adding boot entries

**Note:** bootctl will automatically check for "**Windows Boot Manager**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) and "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`). Where detected, entries will also automatically be generated for them as well. However, it does not auto-detect other EFI applications (unlike [rEFInd](/index.php/REFInd "REFInd")), so for booting the kernel, manual configuration entries must be created. If you dual-boot Windows, it is strongly recommended to disable its default [Fast Start-Up](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") option.

**Tip:** You can find the PARTUUID for your Root partition with the command `blkid -s PARTUUID -o value /dev/sdxY`, where 'x' is the device letter and 'Y' is the partition number. This is required only for your Root partition, not $esp.

bootctl searches for boot menu items in `$esp/loader/entries/*.conf` – each file found must contain exactly one boot entry. The possible options are:

*   `title` – operating system name. **Required.**

*   `version` – kernel version, shown only when multiple entries with same title exist. Optional.

*   `machine-id` – machine identifier from `/etc/machine-id`, shown only when multiple entries with same title and version exist. Optional.

*   `efi` – EFI program to start, relative to your ESP (`$esp`); e.g. `/vmlinuz-linux`. Either this or `linux` (see below) is **required.**

*   `options` – command line options to pass to the EFI program. Optional, but you will need at least `initrd=_efipath_` and `root=_dev_` if booting Linux.

For Linux, you can specify `linux _path-to-vmlinuz_` and `initrd _path-to-initramfs_`; this will be automatically translated to `efi _path_` and `options initrd=_path_` – this syntax is only supported for convenience and has no differences in function.

#### Standard root installations

Here is an example entry for a root partition without LVM or LUKS:

 `$esp/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Please note in the example above that PARTUUID/PARTLABEL identifies a GPT partition, and differs from UUID/LABEL, which identifies a filesystem. Using the PARTUUID/PARTLABEL is advantageous because it is invariant (i.e. unchanging) if you reformat the partition with another filesystem, or if the /dev/sd* mapping changed for some reason. It is also useful if you do not have a filesystem on the partition (or use LUKS, which does not support LABELs).

#### LVM root installations

**Warning:** Systemd-boot cannot be used without a separate `/boot` filesystem outside of LVM.

Here is an example for a root partition using [Logical Volume Management](/index.php/LVM "LVM"):

 `$esp/loader/entries/arch-lvm.conf` 

```
title          Arch Linux (LVM)
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=/dev/mapper/<VolumeGroup-LogicalVolume> rw
```

Replace `<VolumeGroup-LogicalVolume>` with the actual VG and LV names (e.g. `root=/dev/mapper/volgroup00-lvolroot`). Alternatively, it is also possible to use a UUID instead:

```
....
options  root=UUID=<UUID identifier> rw

```

Note that `root=**UUID**=` is used instead of `root=**PARTUUID**=`, which is used for Root partitions without LVM or LUKS.

#### Encrypted Root Installations

Here is an example configuration file for an encrypted root partition ([DM-Crypt / LUKS](/index.php/Dm-crypt "Dm-crypt")):

 `$esp/loader/entries/arch-encrypted.conf` 

```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<mapped-name> root=/dev/mapper/<mapped-name> quiet rw
```

UUID is used in this example; PARTUUID should be able to replace the UUID, if so desired. You may also replace the /dev path with a regular UUID. See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

You can also add other EFI programs such as `\EFI\arch\grub.efi`.

#### btrfs subvolume root installations

If booting a [btrfs](/index.php/Btrfs "Btrfs") subvolume as root, amend the `options` line with `rootflags=subvol=<root subvolume>`. In the example below, root has been mounted as a btrfs subvolume called 'ROOT' (e.g. `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `$esp/loader/entries/arch-btrfs-subvol.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

A failure to do so will otherwise result in the following error message: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### EFI Shells or other EFI apps

In case you installed EFI shells and other EFI application into the ESP, you can use the following snippets:

 `$esp/loader/entries/uefi-shell-v1-x86_64.conf` 

```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```

 `$esp/loader/entries/uefi-shell-v2-x86_64.conf` 

```
title  UEFI Shell x86_64 v2
efi    /EFI/shellx64_v2.efi
```

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Add example on how to boot into EFI firmware setup. (Discuss in [Talk:Systemd-boot#](https://wiki.archlinux.org/index.php/Talk:Systemd-boot))

### Support hibernation

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Keys inside the boot menu

The following keys are used inside the menu:

*   `Up/Down` - select entry
*   `Enter` - boot the selected entry
*   `d` - select the default entry to boot (stored in a non-volatile EFI variable)
*   `-/T` - decrease the timeout (stored in a non-volatile EFI variable)
*   `+/t` - increase the timeout (stored in a non-volatile EFI variable)
*   `e` - edit the kernel command line. has no effect if the `editor` config option is set to `0`.
*   `v` - show the gummiboot and UEFI version
*   `Q` - quit
*   `P` - print the current configuration
*   `h/?` - help

These hotkeys will, when pressed inside the menu or during bootup, directly boot a specific entry:

*   `l` - Linux
*   `w` - Windows
*   `a` - OS X
*   `s` - EFI Shell
*   `1-9` - number of entry

## Troubleshooting

### Manual entry using efibootmgr

If `bootctl install` command failed, you can create a EFI boot entry manually using [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr):

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/systemd/systemd-bootx64.efi -L "Linux Boot Manager"

```

where `/dev/sdXY` is the [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI").

### Menu does not appear after Windows upgrade

For example, if you upgraded from Windows 8 to Windows 8.1, and you no longer see a boot menu after the upgrade (i.e., Windows boots immediately):

*   Make sure Secure Boot (UEFI setting) and [Fast Startup](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") (Windows power option setting) are both disabled.
*   Make sure your UEFI prefers Linux Boot Manager over Windows Boot Manager (UEFI setting like Hard Drive Disk Priority).

**Note:** Windows 8.x+, including Windows 10, will overwrite any UEFI choices you make and install itself as the priority boot choice after every boot. Changing the boot order in the UEFI firmware will only last until the next Windows 10 boot. Know what the _Change Boot Option_ key is for your motherboard.

To make Windows 8.X and above respect your boot order, you must enter a Windows group policy and have it execute a batch (_.bat_) file on startup. In Windows:

1.  Open a command prompt with admin privlages. Type in `bcdedit /enum firmware`
2.  Find the Firmware Application that has "Linux" in the description, e.g. "Linux Boot Manager"
3.  Copy the Identifier, including the brackets, e.g. `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`
4.  Open _gpedit_ and under _Local Computer Policy > Computer Configuration > Windows Settings > Scripts(Startup/Shutdown)_, choose _Startup_. That should open a window named _Startup Properties_.
5.  Under the _Scripts_ tab, choose the _Add_ button
6.  Give your script a name, e.g. `bootorder.bat`.
7.  Under _Script Parameters_, type `bcdedit /set {fwbootmgr} DEFAULT {_identifier_copied_in_step_3_}` (e.g. `bcdedit /set {fwbootmgr} DEFAULT {31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`).

If this does not work, create a batch file somewhere on your Windows system with the `bcdedit /set {fwbootmgr} DEFAULT {_identifier_copied_in_step_3_}` line in it and go back to step 6 and _Browse_ for that file.

Alternatively, you can make the default Windows boot loader load systemd-boot instead. In an administrator command prompt in Windows, one can change this entry as follows:

```
bcdedit /set {bootmgr} path \EFI\systemd\systemd-bootx64.efi

```

## See also

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd-boot&oldid=411004](https://wiki.archlinux.org/index.php?title=Systemd-boot&oldid=411004)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders")
Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**systemd-boot**, previously called **gummiboot**, is a simple UEFI boot manager which executes configured EFI images. The default entry is selected by a configured pattern (glob) or an on-screen menu. It is included with [systemd](https://www.archlinux.org/packages/?name=systemd), which is installed on Arch system by default.

It is simple to configure but it can only start EFI executables such as the Linux kernel [EFISTUB](/index.php/EFISTUB "EFISTUB"), UEFI Shell, GRUB, the Windows Boot Manager.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 EFI boot](#EFI_boot)
    *   [1.2 BIOS boot](#BIOS_boot)
    *   [1.3 Updating](#Updating)
        *   [1.3.1 Manually](#Manually)
        *   [1.3.2 Automatically](#Automatically)
*   [2 Configuration](#Configuration)
    *   [2.1 Basic configuration](#Basic_configuration)
    *   [2.2 Adding boot entries](#Adding_boot_entries)
        *   [2.2.1 Standard root installations](#Standard_root_installations)
        *   [2.2.2 LVM root installations](#LVM_root_installations)
        *   [2.2.3 Encrypted Root Installations](#Encrypted_Root_Installations)
        *   [2.2.4 btrfs subvolume root installations](#btrfs_subvolume_root_installations)
        *   [2.2.5 ZFS root installations](#ZFS_root_installations)
        *   [2.2.6 EFI Shells or other EFI apps](#EFI_Shells_or_other_EFI_apps)
    *   [2.3 Preparing kernels for EFI\Linux](#Preparing_kernels_for_EFI.5CLinux)
    *   [2.4 Support hibernation](#Support_hibernation)
    *   [2.5 Kernel parameters editor with password protection](#Kernel_parameters_editor_with_password_protection)
*   [3 Keys inside the boot menu](#Keys_inside_the_boot_menu)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Manual entry using efibootmgr](#Manual_entry_using_efibootmgr)
    *   [4.2 Menu does not appear after Windows upgrade](#Menu_does_not_appear_after_Windows_upgrade)
*   [5 See also](#See_also)

## Installation

### EFI boot

1.  Make sure you are booted in UEFI mode.
2.  Verify [your EFI variables are accessible](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Mount your [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") (ESP) properly. `*esp*` is used to denote the mountpoint in this article.
    **Note:** *systemd-boot* cannot load EFI binaries from other partitions. It is therefore recommended to mount your ESP to `/boot`. In case you want to separate `/boot` from the ESP see [#Manually](#Manually) for more information.

4.  If the ESP is **not** mounted at `/boot`, then copy your kernel and initramfs onto that ESP.
    **Note:** For a way to automatically keep the kernel updated on the ESP, have a look at [EFISTUB#Using systemd](/index.php/EFISTUB#Using_systemd "EFISTUB") for some systemd units that can be adapted. If your EFI System Partition is using automount, you may need to add `vfat` to a file in `/etc/modules-load.d/` to ensure the current running kernel has the `vfat` module loaded at boot, before any kernel update happens that could replace the module for the currently running version making the mounting of `/boot/efi` impossible until reboot.

5.  Type the following command to install *systemd-boot*: `# bootctl --path=*esp* install` It will copy the *systemd-boot* binary to your EFI System Partition (`*esp*/EFI/systemd/systemd-bootx64.efi` and `*esp*/EFI/Boot/BOOTX64.EFI` – both of which are identical – on x86-64 systems) and add *systemd-boot* itself as the default EFI application (default boot entry) loaded by the EFI Boot Manager.
6.  Finally you must [configure](#Configuration) the boot loader to function properly.

### BIOS boot

**Warning:** This is not recommended.

You can successfully install *systemd-boot* if booted with in BIOS mode. However, this process requires you to tell firmware to launch *systemd-boot'*s EFI file at boot, usually via two ways:

*   you have a working EFI Shell somewhere else.

*   your firmware interface provides a way of properly setting the EFI file that needs to be loaded at boot time.

If you can do it, the installation is easier: go into your EFI Shell or your firmware configuration interface and change your machine's default EFI file to `*esp*/EFI/systemd/systemd-bootx64.efi` ( or `systemd-bootia32.efi` depending if your system firmware is 32 bit).

**Note:** the firmware interface of Dell Latitude series provides everything you need to setup EFI boot but the EFI Shell won't be able to write to the computer's ROM.

### Updating

Unlike the previous separate *gummiboot* package, which updated automatically on a new package release with a `post_install` script, updates of new *systemd-boot* versions must now be done manually by the user. However the procedure can be automated using pacman hooks.

#### Manually

*systemd-boot* ([bootctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/bootctl.1)) assumes that your EFI System Partition is mounted on `/boot`.

```
# bootctl update

```

If the ESP is not mounted on `/boot`, the `--path=` option can pass it. For example:

```
# bootctl --path=*esp* update

```

**Note:** This is also the command to use when migrating from *gummiboot*, before removing that package. If that package has already been removed, however, run `bootctl --path=*esp* install`.

#### Automatically

The [AUR](/index.php/AUR "AUR") package [systemd-boot-pacman-hook](https://aur.archlinux.org/packages/systemd-boot-pacman-hook/) provides a [Pacman hook](/index.php/Pacman#Hooks "Pacman") to automate the update process. [Installing](/index.php/Install "Install") the package will add a hook which will be executed every time the [systemd](https://www.archlinux.org/packages/?name=systemd) package is upgraded.

Alternatively, place the following pacman hook in the `/etc/pacman.d/hooks/` directory:

 `/etc/pacman.d/hooks/systemd-boot.hook` 
```
[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Updating systemd-boot...
When = PostTransaction
Exec = /usr/bin/bootctl update
```

## Configuration

### Basic configuration

The basic configuration is stored in `*esp*/loader/loader.conf` file and it is composed by three options:

*   `default` – default entry to select (without the `.conf` suffix); can be a wildcard like `arch-*`.

*   `timeout` – menu timeout in seconds. If this is not set, the menu will only be shown on `Space` press during boot.

*   `editor` – whether to enable the kernel parameters editor or not. `1` (default) is enabled, `0` is disabled; since the user can add `init=/bin/bash` to bypass root password and gain root access, it is strongly recommended to set this option to `0`.

Example:

 `*esp*/loader/loader.conf` 
```
default  arch
timeout  4
editor   0

```

**Note:** The first 2 options can be changed in the boot menu itself and changes will be stored as EFI variables.

**Tip:** A basic configuration file example is located at `/usr/share/systemd/bootctl/loader.conf`.

### Adding boot entries

**Note:**

*   *bootctl* will automatically check for "**Windows Boot Manager**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) and "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`) at boot time, as well as specially prepared kernel files found in `\EFI\Linux`. When detected, corresponding entries with titles `auto-windows`, `auto-efi-shell` and `auto-efi-default`, respectively, will be automatically generated. These entries do not require manual loader configuration. However, it does not auto-detect other EFI applications (unlike [rEFInd](/index.php/REFInd "REFInd")), so for booting the Linux kernel, manual configuration entries must be created.

*   If you dual-boot Windows, it is strongly recommended to disable its default [Fast Start-Up](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") option.
*   Remember to load the intel [microcode](/index.php/Microcode "Microcode") with `initrd` if applicable.
*   You can find the `PARTUUID` for your root partition with the command `blkid -s PARTUUID -o value /dev/sd*xY*`, where `*x*` is the device letter and `*Y*` is the partition number. This is required only for your root partition, not `*esp*`.

*bootctl* searches for boot menu items in `*esp*/loader/entries/*.conf` – each file found must contain exactly one boot entry. The possible options are:

*   `title` – operating system name. **Required.**

*   `version` – kernel version, shown only when multiple entries with same title exist. Optional.

*   `machine-id` – machine identifier from `/etc/machine-id`, shown only when multiple entries with same title and version exist. Optional.

*   `efi` – EFI program to start, relative to your ESP (`*esp*`); e.g. `/vmlinuz-linux`. Either this or `linux` (see below) is **required.**

*   `options` – command line options to pass to the EFI program or kernel boot parameters. Optional, but you will need at least `initrd=*efipath*` and `root=*dev*` if booting Linux.

For Linux, you can specify `linux *path-to-vmlinuz*` and `initrd *path-to-initramfs*`; this will be automatically translated to `efi *path*` and `options initrd=*path*` – this syntax is only supported for convenience and has no differences in function.

#### Standard root installations

Here is an example entry for a root partition without LVM or LUKS:

 `*esp*/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Please note in the example above that `PARTUUID`/`PARTLABEL` identifies a GPT partition, and differs from `UUID`/`LABEL`, which identifies a filesystem. Using the `PARTUUID`/`PARTLABEL` is advantageous because it is invariant (i.e. unchanging) if you reformat the partition with another filesystem, or if the `/dev/sd*` mapping changed for some reason. It is also useful if you do not have a filesystem on the partition (or use LUKS, which does not support `LABEL`s).

**Tip:** An example entry file is located at `/usr/share/systemd/bootctl`.

#### LVM root installations

**Warning:** *systemd-boot* cannot be used without a separate `/boot` filesystem outside of LVM.

Here is an example for a root partition using [Logical Volume Management](/index.php/LVM "LVM"):

 `*esp*/loader/entries/arch-lvm.conf` 
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

Here is an example configuration file for an encrypted root partition ([DM-Crypt / LUKS](/index.php/Dm-crypt "Dm-crypt")) using the `encrypt` [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook:

 `*esp*/loader/entries/arch-encrypted.conf` 
```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<mapped-name> root=/dev/mapper/<mapped-name> quiet rw
```

UUID is used in this example; `PARTUUID` should be able to replace the UUID, if so desired. You may also replace the `/dev` path with a regular UUID. `mapped-name` is whatever you want it to be called. See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

If you are using LVM, your cryptdevice line will look like this:

 `*esp*/loader/entries/arch-encrypted-lvm.conf` 
```
title Arch Linux Encrypted LVM
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:MyVolGroup root=/dev/mapper/MyVolGroup-MyVolRoot quiet rw
```

You can also add other EFI programs such as `\EFI\arch\grub.efi`.

#### btrfs subvolume root installations

If booting a [btrfs](/index.php/Btrfs "Btrfs") subvolume as root, amend the `options` line with `rootflags=subvol=<root subvolume>`. In the example below, root has been mounted as a btrfs subvolume called 'ROOT' (e.g. `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `*esp*/loader/entries/arch-btrfs-subvol.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

A failure to do so will otherwise result in the following error message: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### ZFS root installations

When booting from a [ZFS](/index.php/ZFS "ZFS") dataset, add `zfs=<root dataset>` to the `options` line. Here the root dataset has been set to 'zroot/ROOT/default':

 `*esp*/loader/entries/arch-zfs.conf` 
```
title          Arch Linux ZFS
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        zfs=zroot/ROOT/default rw
```

When booting off of a ZFS dataset ensure that it has had the `bootfs` property set with `zpool set bootfs=<root dataset> <zpool>`.

#### EFI Shells or other EFI apps

In case you installed EFI shells and other EFI application into the ESP, you can use the following snippets:

 `*esp*/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```
 `*esp*/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title  UEFI Shell x86_64 v2
efi    /EFI/shellx64_v2.efi
```

### Preparing kernels for EFI\Linux

*EFI\Linux* is searched for specially prepared kernel files, which bundle the kernel, the initrd, the kernel command line and /etc/os-release into one file. This file can be easily signed for secure boot.

Create the bundle file like this:

 `Kernel packaging command:` 
```
objcopy \
    --add-section .osrel="/usr/lib/os-release" --change-section-vma .osrel=0x20000 \
    --add-section .cmdline="kernel command line" --change-section-vma .cmdline=0x30000 \
    --add-section .linux="vmlinuz-file" --change-section-vma .linux=0x40000 \
    --add-section .initrd="initrd-file" --change-section-vma .initrd=0x3000000 \
    "/usr/lib/systemd/boot/efi/linuxx64.efi.stub" "linux.efi"
```

Optionally sign *linux.efi* now (e.g. using *sbsigntools* from AUR).

Copying *linux.efi* into `esp*\EFI\Linux*`.

### Support hibernation

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

### Kernel parameters editor with password protection

Alternatively you can install [systemd-boot-password](https://aur.archlinux.org/packages/systemd-boot-password/) which supports `password` basic configuration option. Use `sbpctl generate` to generate a value for this option.

Install *systemd-boot-password* with the following command:

 `# sbpctl install *esp*` 

With enabled editor you will be prompted for your password before you can edit kernel parameters.

## Keys inside the boot menu

The following keys are used inside the menu:

*   `Up/Down` - select entry
*   `Enter` - boot the selected entry
*   `d` - select the default entry to boot (stored in a non-volatile EFI variable)
*   `-/T` - decrease the timeout (stored in a non-volatile EFI variable)
*   `+/t` - increase the timeout (stored in a non-volatile EFI variable)
*   `e` - edit the kernel command line. It has no effect if the `editor` config option is set to `0`.
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

where `/dev/sdXY` is the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

### Menu does not appear after Windows upgrade

See [UEFI#Windows changes boot order](/index.php/UEFI#Windows_changes_boot_order "UEFI").

## See also

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)
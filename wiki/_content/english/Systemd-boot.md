Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**systemd-boot**, previously called **gummiboot**, is a simple UEFI boot manager which executes configured EFI images. The default entry is selected by a configured pattern (glob) or an on-screen menu. It is included with [systemd](https://www.archlinux.org/packages/?name=systemd), which is installed on Arch system by default.

It is simple to configure but it can only start EFI executables such as the Linux kernel [EFISTUB](/index.php/EFISTUB "EFISTUB"), UEFI Shell, GRUB, the Windows Boot Manager.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing the EFI boot manager](#Installing_the_EFI_boot_manager)
    *   [1.2 Updating the EFI boot manager](#Updating_the_EFI_boot_manager)
        *   [1.2.1 Manual update](#Manual_update)
        *   [1.2.2 Automatic update](#Automatic_update)
*   [2 Configuration](#Configuration)
    *   [2.1 Loader configuration](#Loader_configuration)
    *   [2.2 Adding loaders](#Adding_loaders)
        *   [2.2.1 EFI Shells or other EFI apps](#EFI_Shells_or_other_EFI_apps)
    *   [2.3 Booting into EFI Firmware Setup](#Booting_into_EFI_Firmware_Setup)
    *   [2.4 Preparing kernels for /EFI/Linux](#Preparing_kernels_for_.2FEFI.2FLinux)
    *   [2.5 Support hibernation](#Support_hibernation)
    *   [2.6 Kernel parameters editor with password protection](#Kernel_parameters_editor_with_password_protection)
*   [3 Keys inside the boot menu](#Keys_inside_the_boot_menu)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Installing after booting in BIOS mode](#Installing_after_booting_in_BIOS_mode)
    *   [4.2 Manual entry using efibootmgr](#Manual_entry_using_efibootmgr)
    *   [4.3 Menu does not appear after Windows upgrade](#Menu_does_not_appear_after_Windows_upgrade)
*   [5 See also](#See_also)

## Installation

### Installing the EFI boot manager

To install the *systemd-boot* EFI boot manager, first make sure the system has booted in UEFI mode and that [UEFI variables](/index.php/Unified_Extensible_Firmware_Interface#UEFI_variables "Unified Extensible Firmware Interface") are accessible. This can be checked by running the command `efivar --list`.

It should be noted that *systemd-boot* is only able to load the [EFISTUB](/index.php/EFISTUB "EFISTUB") kernel from the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP). To keep the kernel updated, it is simpler and therefore **recommended** to mount the ESP to `/boot`. If the ESP is **not** mounted to `/boot`, the kernel and initramfs files must be copied onto that ESP. See [EFI system partition#Alternative mount points](/index.php/EFI_system_partition#Alternative_mount_points "EFI system partition") for details.

`*esp*` will be used throughout this page to denote the ESP mountpoint, i.e. `/boot`.

With the ESP mounted to `*esp*`, use [bootctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bootctl.1) to install *systemd-boot* into the EFI system partition by running:

```
# bootctl --path=*esp* install

```

This will copy the *systemd-boot* boot loader to the EFI partition: on a x64 architecture system the two identical binaries `*esp*/EFI/systemd/systemd-bootx64.efi` and `*esp*/EFI/Boot/BOOTX64.EFI` will be transferred to the ESP. It will then set *systemd-boot* as the default EFI application (default boot entry) loaded by the EFI Boot Manager.

Then, go to the [#Configuration](#Configuration) section to add boot loaders to make *systemd-boot* to function properly at boot time.

### Updating the EFI boot manager

Whenever there is a new version of *systemd-boot*, the boot manager must be updated by the user. This can be performed manually or the update can be automatically triggered using pacman hooks. The two approaches are described thereafter.

#### Manual update

*bootctl* must be used to update *systemd-boot*. If the `path` parameter is not specified, `/efi`, `/boot`, and `/boot/efi` are checked in turn.

```
# bootctl update

```

If the ESP is mounted on a different location, the `path` option can be passed as follows:

```
# bootctl --path=*esp* update

```

**Note:** This is also the command to use when migrating from *gummiboot*, before removing that package. If that package has already been removed, however, run `bootctl --path=*esp* install`.

#### Automatic update

The package [systemd-boot-pacman-hook](https://aur.archlinux.org/packages/systemd-boot-pacman-hook/) provides a [Pacman hook](/index.php/Pacman_hook "Pacman hook") to automate the update process. [Installing](/index.php/Install "Install") the package will add a hook which will be executed every time the [systemd](https://www.archlinux.org/packages/?name=systemd) package is upgraded. Alternatively, to replicate what the *systemd-boot-pacman-hook* package does without installing it, place the following pacman hook in the `/etc/pacman.d/hooks/` directory:

 `/etc/pacman.d/hooks/systemd-boot.hook` 
```
[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Updating systemd-boot
When = PostTransaction
Exec = /usr/bin/bootctl update
```

## Configuration

### Loader configuration

The loader configuration is stored in the file `*esp*/loader/loader.conf` and it is composed of the following options:

*   `default` – default entry to select as defined in [#Adding loaders](#Adding_loaders); it is given without the *.conf* suffix and it can be a wildcard like `arch-*`.
*   `timeout` – menu timeout in seconds before the default entry is booted. If this is not set, the menu will only be shown on `Space` key (or most other keys actually work too) press during boot.
*   `editor` – whether to enable the kernel parameters editor or not. `yes` (default) is enabled, `no` is disabled; since the user can add `init=/bin/bash` to bypass root password and gain root access, it is strongly recommended to set this option to `no`.
*   `auto-entries` – shows automatic entries for Windows, EFI Shell, and Default Loader if set to `1` (default), `0` to hide;
*   `auto-firmware` – shows entry for rebooting into UEFI firmware settings if set to `1` (default), `0` to hide;
*   `console-mode` – changes UEFI console mode: `0` for 80x25, `1` for 80x50, `2` and above for non-standard modes provided by the device firmware, if any, `auto` picks a suitable mode automatically, `max` for highest available mode, `keep` (default) for the firmware selected mode.

See [loader.conf manual](https://www.freedesktop.org/software/systemd/man/loader.conf.html) for the full list of options.

Example:

 `*esp*/loader/loader.conf` 
```
default  arch
timeout  4
editor   no

```

**Tip:**

*   `default` and `timeout` can be changed in the boot menu itself and changes will be stored as EFI variables, overriding these options.
*   A basic loader configuration file is located at `/usr/share/systemd/bootctl/loader.conf`.

### Adding loaders

*bootctl* searches for boot menu items in `*esp*/loader/entries/*.conf` – each file found must contain exactly one loader. The possible options are:

*   `title` – operating system name. **Required.**
*   `version` – kernel version, shown only when multiple entries with same title exist. Optional.
*   `machine-id` – machine identifier from `/etc/machine-id`, shown only when multiple entries with same title and version exist. Optional.
*   `efi` – EFI program to start, relative to your ESP (`*esp*`); e.g. `/vmlinuz-linux`. **Either** this parameter or `linux` (see below) is **required**.
*   `options` – command line options to pass to the EFI program or [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Optional, but you will need at least `initrd=*efipath*` and `root=*dev*` if booting Linux.

For Linux boot, you can also use instead of `efi` and `options` the following syntax:

*   `linux` and `initrd` followed by the relative path of the corresponding files in the ESP; e.g. `/vmlinuz-linux`; this will be automatically translated into `efi *path*` and `options initrd=*path*` – this syntax is only supported for convenience and has no differences in function.

An example of a loader file to launch Arch from a partition with the label *arch_os* and loading the Intel CPU [microcode](/index.php/Microcode "Microcode") is:

 `*esp*/loader/entries/arch.conf` 
```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options root=LABEL=*arch_os* rw
```

*bootctl* will automatically check at boot time for **Windows Boot Manager** at the location `/EFI/Microsoft/Boot/Bootmgfw.efi`, **EFI Shell** `/shellx64.efi` and **EFI Default Loader** `/EFI/BOOT/bootx64.efi`, as well as specially prepared kernel files found in `/EFI/Linux`. When detected, corresponding entries with titles `auto-windows`, `auto-efi-shell` and `auto-efi-default`, respectively, will be generated. These entries do not require manual loader configuration. However, it does not auto-detect other EFI applications (unlike [rEFInd](/index.php/REFInd "REFInd")), so for booting the Linux kernel, manual configuration entries must be created.

**Note:**

*   If you dual-boot Windows, it is strongly recommended to disable its default [Fast Start-Up](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") option.
*   Remember to load the Intel *microcode* with `initrd` if applicable, an example is provided in [Microcode#systemd-boot](/index.php/Microcode#systemd-boot "Microcode").
*   The root partition can be identified with its `LABEL` or its `PARTUUID`. The latter can be found with the command `blkid -s PARTUUID -o value /dev/sd*xY*`, where `*x*` is the device letter and `*Y*` is the partition number. This is required only to identify the root partition, not the `*esp*`.

**Tip:**

*   The available boot entries which have been configured can be listed with the command `bootctl list`.
*   An example entry file is located at `/usr/share/systemd/bootctl/arch.conf`.
*   The [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for scenarios such as [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/LUKS "LUKS") or [dm-crypt](/index.php/Dm-crypt "Dm-crypt") can be found on the relevant pages.

#### EFI Shells or other EFI apps

In case you installed EFI shells and other EFI application into the ESP, you can use the following snippets.

**Note:** The file path parameter for the `efi` line is relative to your *esp* mount point. If you are mounted on `/boot` and your EFI binaries reside at `/boot/EFI/xx.efi` and `/boot/yy.efi`, then you would specify the parameters as `efi /EFI/xx.efi` and `efi /yy.efi` respectfully.

Examples of loading custom UEFI Shell loaders:

 `*esp*/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title   UEFI Shell x86_64 v1
efi     /EFI/shellx64_v1.efi
```
 `*esp*/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title   UEFI Shell x86_64 v2
efi     /EFI/shellx64_v2.efi
```

### Booting into EFI Firmware Setup

Most system firmware configured for EFI booting will add its own [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface") entries to boot into UEFI Firmware Setup.

### Preparing kernels for /EFI/Linux

*/EFI/Linux* is searched for specially prepared kernel files, which bundle the kernel, the init RAM disk (initrd), the kernel command line and `/etc/os-release` into one single file. This file can be easily signed for secure boot.

**Note:** `systemd-boot` requires that the `os-release` file contain either `VERSION_ID` or `BUILD_ID` to generate an ID and automatically add the entry, which the Arch `os-release` does not. Either maintain your own copy with one of them, or make your bundling script generate it automatically.

Put the kernel command line you want to use in a file, and create the bundle file like this:

 `Kernel packaging command:` 
```
objcopy \
    --add-section .osrel="/usr/lib/os-release" --change-section-vma .osrel=0x20000 \
    --add-section .cmdline="kernel-command-line.txt" --change-section-vma .cmdline=0x30000 \
    --add-section .linux="vmlinuz-file" --change-section-vma .linux=0x40000 \
    --add-section .initrd="initrd-file" --change-section-vma .initrd=0x3000000 \
    "/usr/lib/systemd/boot/efi/linuxx64.efi.stub" "*linux*.efi"
```

Optionally sign the `*linux*.efi` file produced above.

Copy `*linux*.efi` into `*esp*/EFI/Linux`.

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
*   `v` - show the systemd-boot and UEFI version
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

### Installing after booting in BIOS mode

**Warning:** This is not recommended.

If booted in BIOS mode, you can still install *systemd-boot*, however this process requires you to tell firmware to launch *systemd-boot'*s EFI file at boot, usually via two ways:

*   you have a working EFI Shell somewhere else.
*   your firmware interface provides a way of properly setting the EFI file that needs to be loaded at boot time.

If you can do it, the installation is easier: go into your EFI Shell or your firmware configuration interface and change your machine's default EFI file to `*esp*/EFI/systemd/systemd-bootx64.efi` ( or `systemd-bootia32.efi` depending if your system firmware is 32 bit).

**Note:** The firmware interface of Dell Latitude series provides everything you need to setup EFI boot but the EFI Shell won't be able to write to the computer's ROM.

### Manual entry using efibootmgr

If the `bootctl install` command failed, you can create a EFI boot entry manually using [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr):

```
# efibootmgr -c -d /dev/sdX -p Y -l "\EFI\systemd\systemd-bootx64.efi" -L "Linux Boot Manager"

```

where `/dev/sdXY` is the [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

**Note:** The path to the EFI image must use the backslash (`\`) as the separator

### Menu does not appear after Windows upgrade

See [UEFI#Windows changes boot order](/index.php/UEFI#Windows_changes_boot_order "UEFI").

## See also

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)
*   [https://github.com/systemd/systemd/tree/master/src/boot/efi](https://github.com/systemd/systemd/tree/master/src/boot/efi)
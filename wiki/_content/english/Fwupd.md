Related articles

*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**fwupd** is a simple daemon allowing to update some devices firmware, including UEFI BIOS for several machines thanks to **fwupdate**.

Supported devices are listed [here](https://fwupd.org/lvfs/devicelist) and [more are to come](https://fwupd.org/vendorlist).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Setup for UEFI BIOS upgrade](#Setup_for_UEFI_BIOS_upgrade)
    *   [3.1 Verifying leftovers from previous installations](#Verifying_leftovers_from_previous_installations)
    *   [3.2 Installing and updating fwupdate](#Installing_and_updating_fwupdate)
        *   [3.2.1 Manually](#Manually)
        *   [3.2.2 Automatically](#Automatically)
    *   [3.3 Running fwupd](#Running_fwupd)

## Installation

[Install](/index.php/Install "Install") [fwupd](https://www.archlinux.org/packages/?name=fwupd), this will also install [fwupdate](https://www.archlinux.org/packages/?name=fwupdate) as a required dependency.

See [#Setup for UEFI BIOS upgrade](#Setup_for_UEFI_BIOS_upgrade) if you intend such an use.

## Usage

You can get available devices by running:

```
$ fwupdmgr get-devices

```

**Note:** Some returned devices might not be updatable through fwupd, *e.g.* Intel integrated graphics.

To refresh metadata on available updates:

```
$ fwupdmgr refresh

```

To check which devices have updates:

```
$ fwupdmgr get-updates

```

To install updates:

```
$ fwupdmgr update

```

**Note:** Some updates might require root rights.

## Setup for UEFI BIOS upgrade

1.  Make sure you are booted in UEFI mode.
2.  Verify [your EFI variables are accessible](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Mount your [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) properly. `*esp*` is used to denote the mountpoint in this article.

### Verifying leftovers from previous installations

If you had previously installed fwupdate on any other Linux installation, make sure to remove their leftovers in efivars. You can find then by issuing this command:

```
$ ls /sys/firmware/efi/efivars/fwupdate-*-0abba7dc-e516-4167-bbf5-4d9d1c739416

```

If they are any results, remove them this way:

```
# chattr -i /sys/firmware/efi/efivars/fwupdate-*-0abba7dc-e516-4167-bbf5-4d9d1c739416
# rm -f /sys/firmware/efi/efivars/fwupdate-*-0abba7dc-e516-4167-bbf5-4d9d1c739416

```

### Installing and updating fwupdate

Installation and updates to new *fwupdate* versions requires user intervention. However the update procedure can be automated using pacman hooks (but the manual procedure must be run at least once upon install).

#### Manually

Copy the `/usr/lib/fwupdate/EFI` folder to your ESP:

```
# cp -r /usr/lib/fwupdate/EFI *esp*

```

#### Automatically

Pacman hooks are provided in the [fwupdate](https://www.archlinux.org/packages/?name=fwupdate) for system with ESP at `/boot` or `/boot/efi`. If this is your case you can just symlink the relevant file so that it is taken into account:

*   for system with `*esp*` as `/boot`:

```
# ln -s /usr/share/doc/fwupdate/esp-as-boot.hook /etc/pacman.d/hooks/fwupdate-efi-copy.hook

```

*   for system with `*esp*` as `/boot/efi`

```
# ln -s /usr/share/doc/fwupdate/esp-as-boot-efi.hook /etc/pacman.d/hooks/fwupdate-efi-copy.hook

```

Else, adapt the snippet below to suit your `*esp*` mountpoint:

 `/etc/pacman.d/hooks/fwupdate-efi-copy.hook` 
```
[Trigger]
Type = Package
Operation = Install
Operation = Upgrade
Target = fwupdate

[Action]
Description = Copying fwupdate to EFI directory...
When = PostTransaction
Exec = /usr/bin/cp -r /usr/lib/fwupdate/EFI *esp*

```

### Running fwupd

Follow [#Usage](#Usage), but take care of the two following points.

**Note:** If you don’t see an UEFI entry but are in UEFI mode, check BIOS setup for an option to turn on UEFI capsule updates.

**Warning:** If your ESP is not mounted at `/boot/efi` (e.g. at `/boot`), you specify your *esp* mount point as follow: `/etc/fwupd/uefi.conf` 
```
[uefi]

# For fwupdate 10+ allow overriding
# the compiled EFI system partition path
OverrideESPMountPoint=*esp*

```
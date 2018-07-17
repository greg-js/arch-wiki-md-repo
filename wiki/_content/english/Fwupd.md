Related articles

*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**fwupd** is a simple daemon allowing to update some devices firmware, including UEFI BIOS for several machines.

Supported devices are listed [here](https://fwupd.org/lvfs/devicelist) and [more are to come](https://fwupd.org/vendorlist).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Setup for UEFI BIOS upgrade](#Setup_for_UEFI_BIOS_upgrade)
    *   [3.1 Secure Boot](#Secure_Boot)

## Installation

[Install](/index.php/Install "Install") [fwupd](https://www.archlinux.org/packages/?name=fwupd).

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

### Secure Boot

If you use Secure Boot, you have to sign the UEFI executable used to perform upgrades.
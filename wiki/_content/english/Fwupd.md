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
        *   [3.1.1 Using your own keys](#Using_your_own_keys)

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

Currently, fwupd relies on [shim](/index.php/Secure_Boot#shim "Secure Boot") to chainload the fwupd EFI binary on systems with [Secure Boot](/index.php/Secure_Boot "Secure Boot") enabled. For this to work, shim has to be installed correctly.

#### Using your own keys

**Note:** The following description is based on a future version of fwupd that is not yet released. See [[1]](https://github.com/hughsie/fwupd/issues/669).

Alternatively, you have to manually sign the UEFI executable used to perform upgrades, which is located in `/usr/lib/fwupd/efi/fwupdx64.efi`. The signed UEFI executable is expected in `/usr/lib/fwupd/efi/fwupdx64.efi.signed`. Using [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools), this can be achieved by running:

```
# sbsign --key <keyfile> --cert <certfile> /usr/lib/fwupd/efi/fwupdx64.efi

```

To automatically sign this file when installed or upgraded, a [Pacman hook](/index.php/Pacman#Hooks "Pacman") can be used:

 `/etc/pacman.d/hooks/sign-fwupd-secureboot.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = File
Target = usr/lib/fwupd/efi/fwupdx64.efi

[Action]
When = PostTransaction
Exec = /usr/bin/sbsign --key <keyfile> --cert <certfile> /usr/lib/fwupd/efi/fwupdx64.efi
Depends = sbsigntools
```

Make sure to replace `<keyfile>` and `<certfile>` with the corresponding paths of your keys.

Finally, you have to change the line containing `RequireShimForSecureBoot` in `/etc/fwupd/uefi.conf` to `RequireShimForSecureBoot=false`.
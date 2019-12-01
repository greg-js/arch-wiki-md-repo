Related articles

*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**fwupd** is a simple daemon allowing to update some devices firmware, including UEFI BIOS for several machines.

Supported devices are listed [here](https://fwupd.org/lvfs/devicelist) and [more are to come](https://fwupd.org/vendorlist).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Graphical front-ends](#Graphical_front-ends)
*   [2 Usage](#Usage)
*   [3 Setup for UEFI BIOS upgrade](#Setup_for_UEFI_BIOS_upgrade)
    *   [3.1 Prepare ESP](#Prepare_ESP)
    *   [3.2 Secure Boot](#Secure_Boot)
        *   [3.2.1 Using your own keys](#Using_your_own_keys)

## Installation

[Install](/index.php/Install "Install") [fwupd](https://www.archlinux.org/packages/?name=fwupd).

See [#Setup for UEFI BIOS upgrade](#Setup_for_UEFI_BIOS_upgrade) if you intend such an use.

### Graphical front-ends

Certain [desktop environments](/index.php/Desktop_environments "Desktop environments") front-end solutions have built-in fwupd support:

*   **GNOME Software** — Will check for updates periodically and automatically download firmwares in the background on [GNOME](/index.php/GNOME "GNOME"). After a firmware has been downloaded a popup will be displayed in Gnome Software to perform the update.

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **KDE Discover** — Software center used with [Plasma](/index.php/Plasma "Plasma"). With the release of KDE Plasma 5.14, a new fwupd backend has been implemented in KDE Discover for firmware updates. These firmware updates are shown with other system updates.

	[https://userbase.kde.org/Discover](https://userbase.kde.org/Discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME Firmware** — Application to upgrade, downgrade and reinstall firmware on devices supported by fwupd. It can unlock locked fwupd devices, verify firmware on supported devices and display all releases for a fwupd device.

	[https://gitlab.gnome.org/hughsie/gnome-firmware-updater](https://gitlab.gnome.org/hughsie/gnome-firmware-updater) || [gnome-firmware](https://aur.archlinux.org/packages/gnome-firmware/)

## Usage

To display all devices detected by fwupd:

```
$ fwupdmgr get-devices

```

**Note:** Listed devices may not be updatable through fwupd (*e.g.* Intel integrated graphics). Alternative vendor solutions may be provided instead.

To download the latest metadata from LVFS:

```
$ fwupdmgr refresh

```

To list updates available for any devices on the system:

```
$ fwupdmgr get-updates

```

To install updates:

```
$ fwupdmgr update

```

**Note:**

*   Updates that can be applied live will be done immediately.
*   Updates that run at bootup will be staged for the next reboot.
*   The [root user](/index.php/Root_user "Root user") may be required to perform certain device updates.

## Setup for UEFI BIOS upgrade

**Warning:** An update to your UEFI firmware may discard the current [bootloader](/index.php/Bootloader "Bootloader") installation. It may be necessary to recreate the NVRAM entry (for example using [efibootmgr](/index.php/Efibootmgr "Efibootmgr")) after the firmware update has been installed successfully.

The following requirements should be met:

1.  Make sure you are booted in [UEFI](/index.php/UEFI "UEFI") mode, it will not work in legacy boot mode.
2.  Verify [your EFI variables are accessible](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Mount your [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) properly. `*esp*` is used to denote the mountpoint in this section.

### Prepare ESP

fwupd will copy all the necessary files over to the *esp* but for this to work, a basic folder layout must be present on your *esp*.

**Note:** Depending on the boot loader you have in use or the presence of other operating systems, this directory may already exist.

This constitutes the creation of an 'EFI' directory on your *esp*.

 `mkdir *esp*/EFI/` 
**Warning:** The 'EFI' directory **MUST** be in all upper-case. If you used lower-case, fwupd may detect the *esp* as *esp*/efi/ instead and would start looking for *esp*/efi/EFI/

After creation, you'll have to restart the fwupd service.

 `systemctl restart fwupd.service` 

You can now `$ fwupd refresh` and `$ fwupd update`. It will ask to reboot and should now automatically reboot into the firmware updater.

### Secure Boot

Currently, fwupd relies on [shim](/index.php/Secure_Boot#shim "Secure Boot") to chainload the fwupd EFI binary on systems with [Secure Boot](/index.php/Secure_Boot "Secure Boot") enabled. For this to work, shim has to be installed correctly.

#### Using your own keys

Alternatively, you have to manually sign the UEFI executable used to perform upgrades, which is located in `/usr/lib/fwupd/efi/fwupdx64.efi`. The signed UEFI executable is expected in `/usr/lib/fwupd/efi/fwupdx64.efi.signed`. Using [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools), this can be achieved by running:

```
# sbsign --key <keyfile> --cert <certfile> /usr/lib/fwupd/efi/fwupdx64.efi

```

To automatically sign this file when installed or upgraded, a [Pacman hook](/index.php/Pacman_hook "Pacman hook") can be used:

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

Check out [[1]](https://github.com/hughsie/fwupd/issues/669) for more information discussing this.
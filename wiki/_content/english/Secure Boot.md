For an overview about Secure Boot in Linux see [Rodsbooks' Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html) article. This article focuses on how to set up Secure Boot in Arch Linux.

## Contents

*   [1 Using a signed boot loader](#Using_a_signed_boot_loader)
    *   [1.1 Booting archiso](#Booting_archiso)
    *   [1.2 Set up PreLoader](#Set_up_PreLoader)
        *   [1.2.1 Fallback](#Fallback)
    *   [1.3 Remove PreLoader](#Remove_PreLoader)
*   [2 Using your own keys](#Using_your_own_keys)
    *   [2.1 Creating keys](#Creating_keys)
    *   [2.2 Signing bootloader and kernel](#Signing_bootloader_and_kernel)
    *   [2.3 Put firmware in "Setup Mode"](#Put_firmware_in_.22Setup_Mode.22)
    *   [2.4 Enrol keys in firmware](#Enrol_keys_in_firmware)
        *   [2.4.1 Using firmware setup utility](#Using_firmware_setup_utility)
        *   [2.4.2 Using KeyTool](#Using_KeyTool)
*   [3 Disable Secure Boot](#Disable_Secure_Boot)

## Using a signed boot loader

### Booting archiso

Booting the archiso with Secure Boot enabled is possible since the EFI applications `PreLoader.efi` and `HashTool.efi` have been added to it. A message will show up that says *Failed to Start loader... I will now execute HashTool.* To use HashTool for enrolling the hash of `loader.efi` and `vmlinuz.efi`, follow these steps.

*   Select `OK`
*   In the HashTool main menu, select `Enroll Hash`, choose `\loader.efi` and confirm with `Yes`. Again, select `Enroll Hash` and `archiso` to enter the archiso directory, then select `vmlinuz.efi` and confirm with `Yes`. Then choose `Exit` to return to the boot device selection menu.
*   In the boot device selection menu choose `Arch Linux archiso x86_64 UEFI CD`

The archiso boots, and you are presented with a shell prompt, automatically logged in as root. To check if the archiso was booted with Secure Boot, use this command:

```
$ od -An -t u1 /sys/firmware/efi/efivars/SecureBoot-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX

```

The characters denoted by `XXXX` differ from machine to machine. To help with this, you can use tab completion or list the EFI variables.

If a Secure Boot is enabled, this command returns `1` as the final integer in a list of five, for example:

```
6  0  0  0  1

```

For a verbose status, another way is to execute:

```
# bootctl status

```

### Set up PreLoader

**Warning:** `PreLoader.efi` and `HashTool.efi` in [efitools](https://www.archlinux.org/packages/?name=efitools) package are not signed, so their usefulness is limited. You can get a signed `PreLoader.efi` and `HashTool.efi` from [[1]](http://blog.hansenpartnership.com/linux-foundation-secure-boot-system-released/).

Acquire signed `PreLoader.efi` and `HashTool.efi` and copy them to the [boot loader](/index.php/Boot_loader "Boot loader") directory; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp {PreLoader,HashTool}.efi *esp*/EFI/systemd

```

Now copy over the boot loader binary and rename it to `loader.efi`; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp *esp*/EFI/systemd/systemd-bootx64.efi *esp*/EFI/systemd/loader.efi

```

Finally, create a new NVRAM entry to boot `PreLoader.efi`:

```
# efibootmgr --disk /dev/sd**X** --part **Y** --create --label "PreLoader" --loader /EFI/systemd/PreLoader.efi

```

Replace `X` with the drive letter and replace `Y` with the partition number of the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

This entry should be added to the list as the first to boot; check with the `efibootmgr` command and adjust the boot-order if necessary.

#### Fallback

If there are problems booting the custom NVRAM entry, copy `HashTool.efi` & `loader.efi` to the default loader location booted automatically by UEFI systems:

```
# cp HashTool.efi *esp*/EFI/Boot
# cp *esp*/EFI/systemd/systemd-bootx64.efi *esp*/EFI/Boot/loader.efi

```

Copy over `PreLoader.efi` and rename it:

```
# cp PreLoader.efi *esp*/EFI/Boot/bootx64.efi

```

For particularly intransigent UEFI implementations, copy `PreLoader.efi` to the default loader location used by Windows systems:

```
# mkdir -p *esp*/EFI/Microsoft/Boot
# cp PreLoader.efi *esp*/EFI/Microsoft/Boot/bootmgfw.efi

```

**Note:** If dual-booting with Windows, backup the original `bootmgfw.efi` first as replacing it may cause problems with Windows updates.

As before, copy `HashTool.efi` & `loader.efi` to `*esp*/EFI/Microsoft/Boot`

When the system starts with Secure Boot enabled, follow the steps above to enrol `loader.efi` and `/vmlinuz-linux` (or whichever kernel image is being used).

### Remove PreLoader

**Note:** Since you are going to remove stuff, is a good idea to backup it.

Simply [remove](/index.php/Remove "Remove") the copied files and revert configuration; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# rm *esp*/EFI/systemd/{PreLoader,HashTool}.efi
# rm *esp*/EFI/systemd/loader.efi
# efibootmgr -b N -B
# bootctl update

```

Where `N` is the NVRAM boot entry created for booting `PreLoader.efi`. Check with the *efibootmgr* command and adjust the boot-order if necessary.

**Note:** The above commands cover the easiest case; if you have created, copied, renamed or edited further files probably you have to handle with them, too. If PreLoader was your operational boot entry, you obviously also need to [#Disable Secure Boot](#Disable_Secure_Boot).

## Using your own keys

**Tip:** It is advised to read [Rod Smith's Controlling Secure Boot](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html).

Secure Boot implementations use these keys:

	Platform Key (PK)

	Top-level key

	Key Exchange Key (KEK)

	Key used to sign signature databases or EFI binaries

	Signature Database (db)

	Contains keys and/or hashes used to sign EFI binaries

	Forbidden Signatures Database (dbx)

	Contains keys and/or hashes used to blacklist EFI binaries

To use Secure Boot you need at least **PK**, **KEK** and **db** keys.

### Creating keys

To generate keys, [install](/index.php/Install "Install") [efitools](https://www.archlinux.org/packages/?name=efitools).

You will need keys and certificates in multiple formats:

1.  Create keys and **PEM** format certificates for `sbsign`
2.  Convert certificates to **DER** format for firmware
3.  Convert certificates to **EFI Signature List** for `KeyTool`

Create a [GUID](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") for owner identification:

```
$ uuidgen --random

```

Platform key:

```
$ openssl req -new -x509 -newkey rsa:2048 -subj "/CN=*my PK*/" -keyout PK.key -out PK.crt -days *3650* -nodes -sha256
$ openssl x509 -outform DER -in PK.crt -out PK.cer
$ cert-to-efi-sig-list -g *GUID* PK.crt PK.esl
$ sign-efi-sig-list -g *GUID* -k PK.key -c PK.crt PK PK.esl PK.auth

```

Create an empty file `null.esl` and sign it to allow deleting Platform Key:

```
$ sign-efi-sig-list -g *GUID* -c PK.crt -k PK.key PK *null.esl* rm_PK.auth

```

Key Exchange Key:

```
$ openssl req -new -x509 -newkey rsa:2048 -subj "/CN=*my KEK*/" -keyout KEK.key -out KEK.crt -days *3650* -nodes -sha256
$ openssl x509 -outform DER -in KEK.crt -out KEK.cer
$ cert-to-efi-sig-list -g *GUID* KEK.crt KEK.esl

```

Signature Database:

```
$ openssl req -new -x509 -newkey rsa:2048 -subj "/CN=*my db*/" -keyout db.key -out db.crt -days *3650* -nodes -sha256
$ openssl x509 -outform DER -in db.crt -out db.cer
$ cert-to-efi-sig-list -g *GUID* db.crt db.esl

```

### Signing bootloader and kernel

When Secure Boot is active (i.e. in "User Mode") you will only be able to launch signed binaries, so you need to sign your kernel and [boot loader](/index.php/Boot_loader "Boot loader").

Install [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools).

**Note:** If running *sbsign* without `--output` the resulting file will be `*filename*.signed`.

```
# sbsign --key db.key --cert db.crt --output /boot/vmlinuz-linux /boot/vmlinuz-linux
# sbsign --key db.key --cert db.crt --output *esp*/EFI/BOOT/BOOTX64.EFI *esp*/EFI/BOOT/BOOTX64.EFI

```

**Tip:** To check if a binary is signed and list its signatures use
```
$ sbverify --list */path/to/binary*

```

### Put firmware in "Setup Mode"

Secure Boot is in Setup Mode when the Platform Key is removed. To put firmware in Setup Mode, enter firmware setup utility and find an option to delete or clear certificates.

### Enrol keys in firmware

Copy all `*.cer`, `*.esl`, `*.auth` to a FAT formatted file system (you can use [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition")).

Launch firmware setup utility or KeyTool and enrol **db**, **KEK** and **PK** certificates.

If the used tool supports it prefer using `.auth` and `.esl` over `.cer`.

**Warning:** Enrolling Platform Key sets Secure Boot in "User Mode", so it needs to be enrolled last.

#### Using firmware setup utility

Firmwares have various different interfaces, see [Replacing Keys Using Your Firmware's Setup Utility](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html#setuputil) for example how to enrol keys.

#### Using KeyTool

`KeyTool.efi` is in [efitools](https://www.archlinux.org/packages/?name=efitools) package, copy it to ESP. To use it after enrolling keys, sign it with `sbsign`.

```
# sbsign --key db.key --cert db.crt --output *esp*/EFI/KeyTool-signed.efi /usr/share/efitools/efi/KeyTool.efi

```

Launch `KeyTool-signed.efi` using firmware setup utility, boot loader or [UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") and enrol keys.

See [Replacing Keys Using KeyTool](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html#keytool) for explanation of KeyTool menu options.

## Disable Secure Boot

The Secure Boot feature can be disabled via the UEFI firmware interface. You may access the firmware configuration by pressing a special key during the boot process. The key to use depends on the firmware. It is usually one of `Esc`, `F2`, `Del` or possibly another `F*n*` key.

If using a hotkey did not work and you can boot Windows, you can force a reboot into the firmware configuration in the following way (for Windows 10): *Settings > Update & Security > Recovery > Advanced startup (Restart now) > Troubleshoot > Advanced options > UEFI Firmware settings > restart*.

Note that some motherboards (this is the case in a Packard Bell laptop) only allow to disable secure boot if you have set an administrator password (that can be removed afterwards). See also [Rod Smith's Disabling Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html#disable).
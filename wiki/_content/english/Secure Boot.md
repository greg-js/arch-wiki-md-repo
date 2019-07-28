Related articles

*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

For an overview about Secure Boot in Linux see [Rodsbooks' Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html) article. This article focuses on how to set up Secure Boot in Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Secure Boot status](#Secure_Boot_status)
    *   [1.1 Check the status](#Check_the_status)
        *   [1.1.1 Before booting the OS](#Before_booting_the_OS)
        *   [1.1.2 After booting the OS](#After_booting_the_OS)
    *   [1.2 Change the status](#Change_the_status)
*   [2 Using a signed boot loader](#Using_a_signed_boot_loader)
    *   [2.1 PreLoader](#PreLoader)
        *   [2.1.1 Set up PreLoader](#Set_up_PreLoader)
            *   [2.1.1.1 Fallback](#Fallback)
        *   [2.1.2 How to use while booting?](#How_to_use_while_booting?)
        *   [2.1.3 Remove PreLoader](#Remove_PreLoader)
    *   [2.2 shim](#shim)
        *   [2.2.1 Set up shim](#Set_up_shim)
            *   [2.2.1.1 shim with hash](#shim_with_hash)
            *   [2.2.1.2 shim with key](#shim_with_key)
        *   [2.2.2 Remove shim](#Remove_shim)
*   [3 Using your own keys](#Using_your_own_keys)
    *   [3.1 Custom keys](#Custom_keys)
        *   [3.1.1 Creating keys](#Creating_keys)
        *   [3.1.2 Updating keys](#Updating_keys)
    *   [3.2 Signing bootloader and kernel](#Signing_bootloader_and_kernel)
        *   [3.2.1 Signing kernel with pacman hook](#Signing_kernel_with_pacman_hook)
    *   [3.3 Put firmware in "Setup Mode"](#Put_firmware_in_"Setup_Mode")
    *   [3.4 Enroll keys in firmware](#Enroll_keys_in_firmware)
        *   [3.4.1 Using firmware setup utility](#Using_firmware_setup_utility)
        *   [3.4.2 Using KeyTool](#Using_KeyTool)
    *   [3.5 Dual booting with other operating systems](#Dual_booting_with_other_operating_systems)
        *   [3.5.1 Microsoft Windows](#Microsoft_Windows)
*   [4 Disable Secure Boot](#Disable_Secure_Boot)
*   [5 Booting an install media](#Booting_an_install_media)
*   [6 See also](#See_also)

## Secure Boot status

### Check the status

#### Before booting the OS

At this point, one has to look at the firmware setup. If the machine was booted and is running, in most cases it will have to be rebooted.

You may access the firmware configuration by pressing a special key during the boot process. The key to use depends on the firmware. It is usually one of `Esc`, `F2`, `Del` or possibly another `F*n*` key. Sometimes the right key is displayed for a short while at the beginning of the boot process. The motherboard manual usually records it. You might want to press the key, and keep pressing it, immediately following powering on the machine, even before the screen actually displays anything.

After entering the firmware setup, be careful not to change any settings without prior intention. Usually there are navigation instructions, and short help for the settings, at the bottom of each setup screen. The setup itself might be composed of several pages. You will have to navigate to the correct place. The interesting setting might be simply denoted by secure boot, which can be set on or off.

#### After booting the OS

To check if the machine was booted with Secure Boot, use this command:

```
$ od --address-radix=n --format=u1 /sys/firmware/efi/efivars/SecureBoot-*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*

```

The characters denoted by `*XXXX*` differ from machine to machine. To help with this, you can use [tab completion](/index.php/Bash#Tab_completion "Bash") or list the EFI variables.

If Secure Boot is enabled, this command returns `1` as the final integer in a list of five, for example:

```
6  0  0  0  1

```

For a verbose status, another way is to execute:

```
$ bootctl status

```

### Change the status

## Using a signed boot loader

Using a signed boot loader means using a boot loader signed with Microsoft's key. There are two known signed boot loaders PreLoader and shim, their purpose is to chainload other EFI binaries (usually [boot loaders](/index.php/Boot_loader "Boot loader")). Since Microsoft would never sign a boot loader that automatically launches any unsigned binary, PreLoader and shim use a whitelist called Machine Owner Key list, abbreviated MokList. If the SHA256 hash of the binary (Preloader and shim) or key the binary is signed with (shim) is in the MokList they execute it, if not they launch a key management utility which allows enrolling the hash or key.

### PreLoader

When run, PreLoader tries to launch `loader.efi`. If the hash of `loader.efi` is not in MokList, PreLoader will launch `HashTool.efi`. In HashTool you must enroll the hash of the EFI binaries you want to launch, that means your [boot loader](/index.php/Boot_loader "Boot loader") (`loader.efi`) and kernel.

**Note:** Each time you update any of the binaries (e.g. boot loader or kernel) you will need to enroll their new hash.

**Tip:** The [rEFInd](/index.php/REFInd "REFInd") boot manager's `refind-install` script can copy the rEFInd and PreLoader EFI binaries to the ESP. See [rEFInd#Using PreLoader](/index.php/REFInd#Using_PreLoader "REFInd") for instructions.

#### Set up PreLoader

**Note:** `PreLoader.efi` and `HashTool.efi` in [efitools](https://www.archlinux.org/packages/?name=efitools) package are not signed, so their usefulness is limited. You can get a signed `PreLoader.efi` and `HashTool.efi` from [preloader-signed](https://aur.archlinux.org/packages/preloader-signed/) or [download them manually](https://blog.hansenpartnership.com/linux-foundation-secure-boot-system-released/).

[Install](/index.php/Install "Install") [preloader-signed](https://aur.archlinux.org/packages/preloader-signed/) and copy `PreLoader.efi` and `HashTool.efi` to the [boot loader](/index.php/Boot_loader "Boot loader") directory; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp /usr/share/preloader-signed/{PreLoader,HashTool}.efi *esp*/EFI/systemd

```

Now copy over the boot loader binary and rename it to `loader.efi`; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp *esp*/EFI/systemd/systemd-bootx64.efi *esp*/EFI/systemd/loader.efi

```

Finally, create a new NVRAM entry to boot `PreLoader.efi`:

```
# efibootmgr --verbose --disk /dev/sd***X*** --part ***Y*** --create --label "PreLoader" --loader /EFI/systemd/PreLoader.efi

```

Replace `*X*` with the drive letter and replace `*Y*` with the partition number of the [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

This entry should be added to the list as the first to boot; check with the `efibootmgr` command and adjust the boot-order if necessary.

##### Fallback

If there are problems booting the custom NVRAM entry, copy `HashTool.efi` and `loader.efi` to the default loader location booted automatically by UEFI systems:

```
# cp /usr/share/preloader-signed/HashTool.efi *esp*/EFI/Boot
# cp *esp*/EFI/systemd/systemd-bootx64.efi *esp*/EFI/Boot/loader.efi

```

Copy over `PreLoader.efi` and rename it:

```
# cp /usr/share/preloader-signed/PreLoader.efi *esp*/EFI/Boot/bootx64.efi

```

For particularly intransigent UEFI implementations, copy `PreLoader.efi` to the default loader location used by Windows systems:

```
# mkdir -p *esp*/EFI/Microsoft/Boot
# cp /usr/share/preloader-signed/PreLoader.efi *esp*/EFI/Microsoft/Boot/bootmgfw.efi

```

**Note:** If dual-booting with Windows, backup the original `bootmgfw.efi` first as replacing it may cause problems with Windows updates.

As before, copy `HashTool.efi` and `loader.efi` to `*esp*/EFI/Microsoft/Boot/`.

When the system starts with Secure Boot enabled, follow the steps above to enroll `loader.efi` and `/vmlinuz-linux` (or whichever kernel image is being used).

#### How to use while booting?

A message will show up that says `Failed to Start loader... I will now execute HashTool.` To use HashTool for enrolling the hash of `loader.efi` and `vmlinuz.efi`, follow these steps. These steps assume titles for a remastered archiso installation media. The exact titles you will get depends on your boot loader setup.

*   Select *OK*
*   In the HashTool main menu, select *Enroll Hash*, choose `\loader.efi` and confirm with *Yes*. Again, select *Enroll Hash* and `archiso` to enter the archiso directory, then select `vmlinuz.efi` and confirm with *Yes*. Then choose *Exit* to return to the boot device selection menu.
*   In the boot device selection menu choose *Arch Linux archiso x86_64 UEFI CD*

#### Remove PreLoader

**Note:** Since you are going to remove stuff, is a good idea to backup it.

[Uninstall](/index.php/Uninstall "Uninstall") [preloader-signed](https://aur.archlinux.org/packages/preloader-signed/) and simply remove the copied files and revert configuration; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# rm *esp*/EFI/systemd/{PreLoader,HashTool}.efi
# rm *esp*/EFI/systemd/loader.efi
# efibootmgr --verbose --bootnum *N* --delete-bootnum
# bootctl update

```

Where `*N*` is the NVRAM boot entry created for booting `PreLoader.efi`. Check with the *efibootmgr* command and adjust the boot-order if necessary.

**Note:** The above commands cover the easiest case; if you have created, copied, renamed or edited further files probably you have to handle with them, too. If PreLoader was your operational boot entry, you obviously also need to [#Disable Secure Boot](#Disable_Secure_Boot).

### shim

When run, shim tries to launch `grubx64.efi`. If MokList does not contain the hash of `grubx64.efi` or the key it is signed with, shim will launch MokManager (`mmx64.efi`). In MokManager you must enroll the hash of the EFI binaries you want to launch (your [boot loader](/index.php/Boot_loader "Boot loader") (`grubx64.efi`) and kernel) or enroll the key they are signed with.

**Note:** If you use [#shim with hash](#shim_with_hash), each time you update any of the binaries (e.g. boot loader or kernel) you will need to enroll their new hash.

#### Set up shim

**Tip:** The [rEFInd](/index.php/REFInd "REFInd") boot manager's `refind-install` script can sign rEFInd EFI binaries and copy them along with shim and the MOK certificates to the ESP. See [rEFInd#Using shim](/index.php/REFInd#Using_shim "REFInd") for instructions.

[Install](/index.php/Install "Install") [shim-signed](https://aur.archlinux.org/packages/shim-signed/).

Rename your current [boot loader](/index.php/Boot_loader "Boot loader") to `grubx64.efi`

```
# mv *esp*/EFI/BOOT/BOOTX64.efi *esp*/EFI/BOOT/grubx64.efi

```

Copy *shim* and *MokManager* to your boot loader directory on ESP; use previous filename of your boot loader as as the filename for `shimx64.efi`:

```
# cp /usr/share/shim-signed/shimx64.efi *esp*/EFI/BOOT/BOOTX64.efi
# cp /usr/share/shim-signed/mmx64.efi *esp*/EFI/BOOT/

```

*shim* can authenticate binaries by Machine Owner Key or hash stored in MokList.

	Machine Owner Key (MOK)

	A key that a user generates and uses to sign EFI binaries.

	hash

	A SHA256 hash of an EFI binary.

Using hash is simpler, but each time you update your boot loader or kernel you will need to add their hashes in MokManager. With MOK you only need to add the key once, but you will have to sign the boot loader and kernel each time it updates.

##### shim with hash

If *shim* does not find the SHA256 hash of `grubx64.efi` in MokList it will launch MokManager (`mmx64.efi`).

In *MokManager* select *Enroll hash from disk*, find `grubx64.efi` and add it to MokList. Repeat the steps and add your kernel `vmlinuz-linux`. When done select *Continue boot* and your boot loader will launch and it will be capable launching the kernel.

##### shim with key

Install [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools).

You will need:

	*.key*

	PEM format **private** key for EFI binary signing.

	*.crt*

	PEM format certificate for *sbsign*.

	*.cer*

	DER format certificate for *MokManager*.

Create a Machine Owner Key:

```
$ openssl req -newkey rsa:4096 -nodes -keyout MOK.key -new -x509 -sha256 -days *3650* -subj "/CN=*my Machine Owner Key*/" -out MOK.crt
$ openssl x509 -outform DER -in MOK.crt -out MOK.cer

```

Sign your boot loader (named `grubx64.efi`) and kernel:

```
# sbsign --key MOK.key --cert MOK.crt --output /boot/vmlinuz-linux /boot/vmlinuz-linux
# sbsign --key MOK.key --cert MOK.crt --output *esp*/EFI/BOOT/grubx64.efi *esp*/EFI/BOOT/grubx64.efi

```

You will need to do this each time they are updated. You can automate the kernel signing with a [pacman hook](/index.php/Pacman_hook "Pacman hook"), e.g.:

 `/etc/pacman.d/hooks/999-sign_kernel_for_secureboot.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = linux

[Action]
Description = Signing kernel with Machine Owner Key for Secure Boot
When = PostTransaction
Exec = /usr/bin/find /boot/ -maxdepth 1 -name 'vmlinuz-*' -exec /usr/bin/sh -c 'if ! /usr/bin/sbverify --list {} 2>/dev/null | /usr/bin/grep -q "signature certificates"; then /usr/bin/sbsign --key MOK.key --cert MOK.crt --output {} {}; fi' ;
Depends = sbsigntools
Depends = findutils
Depends = grep
```

Copy `MOK.cer` to a [FAT](/index.php/FAT "FAT") formatted file system (you can use [EFI system partition](/index.php/EFI_system_partition "EFI system partition")).

Reboot and enable Secure Boot. If *shim* does not find the certificate `grubx64.efi` is signed with in MokList it will launch MokManager (`mmx64.efi`).

In *MokManager* select *Enroll key from disk*, find `MOK.cer` and add it to MokList. When done select *Continue boot* and your boot loader will launch and it will be capable launching any binary signed with your Machine Owner Key.

#### Remove shim

[Uninstall](/index.php/Uninstall "Uninstall") [shim-signed](https://aur.archlinux.org/packages/shim-signed/), remove the copied *shim* and *MokManager* files and rename back your boot loader.

## Using your own keys

**Tip:**

*   It is advised to read [Rod Smith's Controlling Secure Boot](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html).
*   You can use `cryptboot-efikeys` script from [cryptboot](https://aur.archlinux.org/packages/cryptboot/) package for simplified creating keys, enrolling keys, signing bootloader and verifying signatures.
    *   Note that [cryptboot](https://aur.archlinux.org/packages/cryptboot/) requires the encrypted `/boot` partition to be specified in `/etc/crypttab` before it runs, and if you are using it in combination with [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), *sbupdate* expects the `/boot/efikeys/db.*` files created by *cryptboot* to be capitalized like `DB.*` unless otherwise configured in `/etc/sbupdate.conf`. Users who do not use systemd to handle encryption may not have anything in their `/etc/crypttab` file and would need to create an entry.

Secure Boot implementations use these keys:

	Platform Key (PK)

	Top-level key.

	Key Exchange Key (KEK)

	Keys used to sign Signatures Database and Forbidden Signatures Database updates.

	Signature Database (db)

	Contains keys and/or hashes of allowed EFI binaries.

	Forbidden Signatures Database (dbx)

	Contains keys and/or hashes of blacklisted EFI binaries.

See [The Meaning of all the UEFI Keys](https://blog.hansenpartnership.com/the-meaning-of-all-the-uefi-keys/) for a more detailed explanation.

### Custom keys

To use Secure Boot you need at least **PK**, **KEK** and **db** keys. While you can add multiple KEK, db and dbx certificates, only one Platform Key is allowed.

Once Secure Boot is in "User Mode" keys can only be updated by signing the update (using *sign-efi-sig-list*) with a higher level key. Platform key can be signed by itself.

#### Creating keys

To generate keys, [install](/index.php/Install "Install") [efitools](https://www.archlinux.org/packages/?name=efitools).

You will need private keys and certificates in multiple formats:

	*.key*

	PEM format **private** keys for EFI binary and EFI signature list signing.

	*.crt*

	PEM format certificates for *sbsign*.

	*.cer*

	DER format certificates for firmware.

	*.esl*

	Certificates in EFI Signature List for *KeyTool* and/or firmware.

	*.auth*

	Certificates in EFI Signature List with authentication header (i.e. a signed certificate update file) for *KeyTool* and/or firmware.

Create a [GUID](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") for owner identification:

```
$ uuidgen --random > GUID.txt

```

Platform key:

```
$ openssl req -newkey rsa:4096 -nodes -keyout PK.key -new -x509 -sha256 -days *3650* -subj "/CN=*my Platform Key*/" -out PK.crt
$ openssl x509 -outform DER -in PK.crt -out PK.cer
$ cert-to-efi-sig-list -g "$(< GUID.txt)" PK.crt PK.esl
$ sign-efi-sig-list -g "$(< GUID.txt)" -k PK.key -c PK.crt PK PK.esl PK.auth

```

Sign an empty file to allow removing Platform Key when in "User Mode":

```
$ sign-efi-sig-list -g "$(< GUID.txt)" -c PK.crt -k PK.key PK /dev/null rm_PK.auth

```

Key Exchange Key:

```
$ openssl req -newkey rsa:4096 -nodes -keyout KEK.key -new -x509 -sha256 -days *3650* -subj "/CN=*my Key Exchange Key*/" -out KEK.crt
$ openssl x509 -outform DER -in KEK.crt -out KEK.cer
$ cert-to-efi-sig-list -g "$(< GUID.txt)" KEK.crt KEK.esl
$ sign-efi-sig-list -g "$(< GUID.txt)" -k PK.key -c PK.crt KEK KEK.esl KEK.auth

```

Signature Database key:

```
$ openssl req -newkey rsa:4096 -nodes -keyout db.key -new -x509 -sha256 -days *3650* -subj "/CN=*my Signature Database key*/" -out db.crt
$ openssl x509 -outform DER -in db.crt -out db.cer
$ cert-to-efi-sig-list -g "$(< GUID.txt)" db.crt db.esl
$ sign-efi-sig-list -g "$(< GUID.txt)" -k KEK.key -c KEK.crt db db.esl db.auth

```

#### Updating keys

Once Secure Boot is in "User Mode" any changes to KEK, db and dbx need to be signed with a higher level key.

For example, if you wanted to replace your db key with a new one:

1.  [Create the new key](#Creating_keys),
2.  Convert it to EFI Signature List,
3.  Sign the EFI Signature List,
4.  Enroll the signed certificate update file.

```
$ cert-to-efi-sig-list -g "$(< GUID.txt)" *new_db*.crt *new_db*.esl
$ sign-efi-sig-list -g "$(< GUID.txt)" -k KEK.key -c KEK.crt db *new_db*.esl *new_db*.auth

```

If instead of replacing your db key, you want to **add** another one to the Signature Database, you need to use the option `-a` (see [sign-efi-sig-list(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sign-efi-sig-list.1)):

```
$ sign-efi-sig-list **-a** -g "$(< GUID.txt)" -k KEK.key -c KEK.crt db *new_db*.esl *new_db*.auth

```

When `*new_db*.auth` is created, [enroll it](#Enroll_keys_in_firmware).

### Signing bootloader and kernel

**Tip:** The [rEFInd](/index.php/REFInd "REFInd") boot manager's `refind-install` script can sign rEFInd EFI binaries and copy them together with the db certificates to the ESP. See [rEFInd#Using your own keys](/index.php/REFInd#Using_your_own_keys "REFInd") for instructions.

When Secure Boot is active (i.e. in "User Mode") you will only be able to launch signed binaries, so you need to sign your kernel and [boot loader](/index.php/Boot_loader "Boot loader").

Install [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools).

**Note:** If running *sbsign* without `--output` the resulting file will be `*filename*.signed`. See [sbsign(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sbsign.1) for more information.

```
# sbsign --key db.key --cert db.crt --output /boot/vmlinuz-linux /boot/vmlinuz-linux
# sbsign --key db.key --cert db.crt --output *esp*/EFI/BOOT/BOOTX64.EFI *esp*/EFI/BOOT/BOOTX64.EFI

```

**Tip:**

*   To check if a binary is signed and list its signatures use `sbverify --list */path/to/binary*`.
*   You can use [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/) to automatically sign your kernels on update. This will also take care of embedding the otherwise unprotected initramfs and kernel command line into the signed UEFI image.
    *   When using [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), `CMDLINE_DEFAULT` must be set in `/etc/sbupdate.conf` in order for the *.efi* image to be bootable.
    *   You may want to consider using [Direct UEFI boot](/index.php/EFISTUB#efibootmgr_with_.efi_file "EFISTUB") with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) after generating the signed *.efi* file.

#### Signing kernel with pacman hook

You can also create your own pacman hook to sign kernel on install and updates.

 `/etc/pacman.d/hooks/99-secureboot.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = linux

[Action]
Description = Signing Kernel for SecureBoot
When = PostTransaction
Exec = /usr/bin/find /boot/ -maxdepth 1 -name 'vmlinuz-*' -exec /usr/bin/sh -c 'if ! /usr/bin/sbverify --list {} 2>/dev/null | /usr/bin/grep -q "signature certificates"; then /usr/bin/sbsign --key db.key --cert db.crt --output {} {}; fi' \ ;
Depends = sbsigntools
Depends = findutils
Depends = grep
```

Since your boot loader or boot manager will also need to be signed, you might want to trigger the hook when the former is updated. Here is an example with systemd-boot:

 `/etc/pacman.d/hooks/99-secureboot.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = linux
Target = systemd

[Action]
Description = Signing Kernel for SecureBoot
When = PostTransaction
Exec = /usr/bin/sh -c "/usr/bin/find /boot/ -type f \( -name 'vmlinuz-*' -o -name 'systemd*' \) -exec /usr/bin/sh -c 'if ! /usr/bin/sbverify --list {} 2>/dev/null
```

The `Target` needs to be duplicated each time you want to add a new package. Wrt. the `find` statement, since we had a condition with the filenames and APLM hooks are being split on spaces, we had to surround the whole statement by quotes in order for the hook to be parsed properly. Since systemd-boot is located in sub-folders, the depth needed to be adjusted as well so that we removed the `-maxdepth` argument. In order to avoid hassle, if you are unsure, try to reinstall the package you want to test to see if the hook and signing part are processed successfully. See [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman") or [alpm-hooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/alpm-hooks.5) for more info.

### Put firmware in "Setup Mode"

Secure Boot is in Setup Mode when the Platform Key is removed. To put firmware in Setup Mode, enter firmware setup utility and find an option to delete or clear certificates. How to enter the setup utility is described in [#Before booting the OS](#Before_booting_the_OS).

### Enroll keys in firmware

Copy all `*.cer`, `*.esl`, `*.auth` to a [FAT](/index.php/FAT "FAT") formatted file system (you can use [EFI system partition](/index.php/EFI_system_partition "EFI system partition")).

Launch firmware setup utility or KeyTool and enroll **db**, **KEK** and **PK** certificates.

If the used tool supports it prefer using *.auth* and *.esl* over *.cer*.

**Warning:** Enrolling Platform Key sets Secure Boot in "User Mode", leaving "Setup Mode", so it should be enrolled last in sequence.

#### Using firmware setup utility

Firmwares have various different interfaces, see [Replacing Keys Using Your Firmware's Setup Utility](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html#setuputil) for example how to enroll keys.

#### Using KeyTool

`KeyTool.efi` is in [efitools](https://www.archlinux.org/packages/?name=efitools) package, copy it to ESP. To use it after enrolling keys, sign it with `sbsign`.

```
# sbsign --key db.key --cert db.crt --output *esp*/KeyTool-signed.efi /usr/share/efitools/efi/KeyTool.efi

```

Launch `KeyTool-signed.efi` using firmware setup utility, boot loader or [UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") and enroll keys.

See [Replacing Keys Using KeyTool](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html#keytool) for explanation of KeyTool menu options.

### Dual booting with other operating systems

#### Microsoft Windows

To [dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows"), you would need to add Microsoft's certificates to the Signature Database. Microsoft has two db certificates:

*   [Microsoft Windows Production PCA 2011](https://www.microsoft.com/pkiops/certs/MicWinProPCA2011_2011-10-19.crt) for Windows
*   [Microsoft Corporation UEFI CA 2011](https://www.microsoft.com/pkiops/certs/MicCorUEFCA2011_2011-06-27.crt) for third-party binaries like UEFI drivers, option ROMs etc.

Microsoft's certificates are in DER format, convert them to PEM format with *openssl*:

```
$ openssl x509 -inform DER -outform PEM -in MicWinProPCA2011_2011-10-19.crt -out MicWinProPCA2011_2011-10-19.crt.pem
$ openssl x509 -inform DER -outform PEM -in MicCorUEFCA2011_2011-06-27.crt -out MicCorUEFCA2011_2011-06-27.crt.pem

```

Create EFI Signature Lists with Microsoft's GUID (`77fa9abd-0359-4d32-bd60-28f4e78f784b`) and combine them in one file for simplicity:

```
$ cert-to-efi-sig-list -g 77fa9abd-0359-4d32-bd60-28f4e78f784b MicWinProPCA2011_2011-10-19.crt.pem MS_Win_db.esl
$ cert-to-efi-sig-list -g 77fa9abd-0359-4d32-bd60-28f4e78f784b MicCorUEFCA2011_2011-06-27.crt.pem MS_UEFI_db.esl
$ cat MS_Win_db.esl MS_UEFI_db.esl > MS_db.esl

```

Sign a db update with your KEK. Use `sign-efi-sig-list` with option `-a` to **add** not replace a db certificate:

```
$ sign-efi-sig-list -a -g 77fa9abd-0359-4d32-bd60-28f4e78f784b -k KEK.key -c KEK.crt db MS_db.esl add_MS_db.auth

```

Follow [#Enroll keys in firmware](#Enroll_keys_in_firmware) to add `add_MS_db.auth` to Signature Database.

## Disable Secure Boot

The Secure Boot feature can be disabled via the UEFI firmware interface. How to access the firmware configuration is described in [#Before booting the OS](#Before_booting_the_OS).

If using a hotkey did not work and you can boot Windows, you can force a reboot into the firmware configuration in the following way (for Windows 10): *Settings > Update & Security > Recovery > Advanced startup (Restart now) > Troubleshoot > Advanced options > UEFI Firmware settings > restart*.

Note that some motherboards (this is the case in a Packard Bell laptop) only allow to disable secure boot if you have set an administrator password (that can be removed afterwards). See also [Rod Smith's Disabling Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html#disable).

## Booting an install media

**Note:** The official installation image does not support Secure Boot ([FS#53864](https://bugs.archlinux.org/task/53864)). To successfully boot the installation medium you will need to [disable Secure Boot](#Disable_Secure_Boot).

Secure Boot support was removed starting with `archlinux-2016.06.01-dual.iso`. At that time *prebootloader* was replaced with [efitools](https://www.archlinux.org/packages/?name=efitools), even though the later uses unsigned EFI binaries. One might want to [remaster the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO") in a way described by previous topics of this article. For example, the signed EFI applications `PreLoader.efi` and `HashTool.efi` from [#PreLoader](#PreLoader) can be adopted to here. Note that up to this point, the article assumed one can access the [ESP](/index.php/ESP "ESP") of the machine. But when installing a machine that never had an OS before, there is no ESP present. You should explore other articles, for example [Unified Extensible Firmware Interface#Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface"), to learn how this situation should be handled.

## See also

*   [Wikipedia:Unified Extensible Firmware Interface#Secure boot](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#Secure_boot "wikipedia:Unified Extensible Firmware Interface")
*   [Dealing with Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html) by Rod Smith
*   [Controlling Secure Boot](http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html) by Rod Smith
*   [UEFI secure booting (part 2)](https://mjg59.dreamwidth.org/5850.html) by Matthew Garrett
*   [UEFI Secure Boot](https://blog.hansenpartnership.com/uefi-secure-boot/) by James Bottomley
*   [efitools README](https://git.kernel.org/cgit/linux/kernel/git/jejb/efitools.git/tree/README)
*   [Will your computer's "Secure Boot" turn out to be "Restricted Boot"?](https://www.fsf.org/campaigns/secure-boot-vs-restricted-boot) — Free Software Foundation
*   [Free Software Foundation recommendations for free operating system distributions considering Secure Boot](https://www.fsf.org/campaigns/secure-boot-vs-restricted-boot/statement/campaigns/secure-boot-vs-restricted-boot/whitepaper-web)
*   [Intel's UEFI Secure Boot Tutorial](https://firmware.intel.com/messages/219)
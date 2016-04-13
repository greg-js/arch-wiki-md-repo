For an overview about Secure Boot in Linux see [Rodsbooks' Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html) article. This section focuses on how to set up Secure Boot in Arch Linux.

## Secure boot archiso

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

## Secure Boot in the installed system

[Install](/index.php/Install "Install") the [prebootloader](https://www.archlinux.org/packages/?name=prebootloader) package and copy `PreLoader.efi` and `HashTool.efi` to the boot{loader,manager} directory; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp /usr/lib/prebootloader/{PreLoader,HashTool}.efi $ESP/EFI/systemd

```

Now copy over the boot{loader,manager} binary and rename it to "loader.efi"; for [systemd-boot](/index.php/Systemd-boot "Systemd-boot") use:

```
# cp $ESP/EFI/systemd/systemd-bootx64.efi $ESP/EFI/systemd/loader.efi

```

Finally, create a new NVRAM entry to boot `PreLoader.efi`:

```
# efibootmgr -d /dev/sd**X** -p **Y** -c -L "PreLoader" -l /EFI/systemd/PreLoader.efi

```

Replace `X` with the drive letter and replace `Y` with the partition number of the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

This entry should be added to the list as the first to boot; check with the `efibootmgr` command and adjust the bootorder if necessary.

If there are problems booting the custom NVRAM entry, copy `HashTool.efi` & `loader.efi` to the default loader location booted automatically by UEFI systems:

```
# cp /usr/lib/prebootloader/HashTool.efi $ESP/EFI/Boot
# cp $ESP/EFI/systemd/systemd-bootx64.efi $ESP/EFI/Boot/loader.efi

```

Copy over `PreLoader.efi` and rename it:

```
# cp /usr/lib/prebootloader/PreLoader.efi $ESP/EFI/Boot/bootx64.efi

```

For particularly intransigent UEFI implementations, copy `PreLoader.efi` to the default loader location used by Windows systems:

```
# mkdir -p $ESP/EFI/Microsoft/Boot
# cp /usr/lib/prebootloader/PreLoader.efi $ESP/EFI/Microsoft/Boot/bootmgfw.efi

```

**Note:** If dual-booting with Windows, backup the original `bootmgfw.efi` first as replacing it may cause problems with Windows updates.

As before, copy `HashTool.efi` & `loader.efi` to `$ESP/EFI/Microsoft/Boot`

When the system starts with Secure Boot enabled, follow the steps above to enrol `loader.efi` and `/vmlinuz-linux` (or whichever kernel image is being used).
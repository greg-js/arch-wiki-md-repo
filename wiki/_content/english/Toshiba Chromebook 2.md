Related articles

*   [Chromebook](/index.php/Chromebook "Chromebook")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

To install Arch Linux on this model of Chromebook, you have to run these commands to install a Seabios boot stub:

```
$ cd; rm -f flash_chromebook_rom.sh; curl -k -L -O [https://johnlewis.ie/flash_chromebook_rom.sh](https://johnlewis.ie/flash_chromebook_rom.sh); sudo -E bash flash_chromebook_rom.sh

```

For a faster boot time you can use a UEFI bootloader ([coreboot](https://www.coreboot.org/)), even remove all the google components. As shown by reddit user coolstarorg in /r/chrultrabook [subreddit](https://www.reddit.com/r/chrultrabook/comments/4t28v1/uefi_firmware_available_for_all_broadwell/?ref=share&ref_source=link).

```
$ cd ~; curl -L -O [https://coolstar.org/chromebook/setup-firmware.sh](https://coolstar.org/chromebook/setup-firmware.sh); sudo bash setup-firmware.sh

```

From here, you will be able to follow the [Beginner's Guide](/index.php/Beginner%27s_Guide "Beginner's Guide") to install Arch Linux.

## Known Issues

*   Sound doesn't work without the appropriate asound.state file (James Fu's backup can be found here: [https://www.dropbox.com/s/gb9mhd0z4356n81/asound.state?dl=0](https://www.dropbox.com/s/gb9mhd0z4356n81/asound.state?dl=0) )

*   Newer Arch kernels don't support the Bay Trail MAX98090 soc audio drivers. A regression introduced by 4.5.0 broke it so if you desire a newer kernel then you can install [linux-max98090](https://aur.archlinux.org/packages/linux-max98090/).
*   Support for the keyboard layout may be found in the xkeyboard-config-chromebook package in the AUR

## See also

*   [https://www.reddit.com/r/chrultrabook/](https://www.reddit.com/r/chrultrabook/)
*   [https://johnlewis.ie/custom-chromebook-firmware/rom-download/](https://johnlewis.ie/custom-chromebook-firmware/rom-download/)
*   [https://plus.google.com/communities/112479827373921524726](https://plus.google.com/communities/112479827373921524726)
*   [https://plus.google.com/+JamesFuBEEFCAKE/posts/Tf4Pc5Z8reH](https://plus.google.com/+JamesFuBEEFCAKE/posts/Tf4Pc5Z8reH)
*   [https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html](https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html)
*   [https://lkml.org/lkml/2016/8/12/180](https://lkml.org/lkml/2016/8/12/180)
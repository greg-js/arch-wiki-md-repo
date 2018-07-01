Related articles

*   [Chromebook](/index.php/Chromebook "Chromebook")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

To install Arch Linux on this model of Chromebook, you have to run these commands to install a Seabios boot stub:

```
$ cd; rm -f flash_chromebook_rom.sh; curl -k -L -O [https://johnlewis.ie/flash_chromebook_rom.sh](https://johnlewis.ie/flash_chromebook_rom.sh); sudo -E bash flash_chromebook_rom.sh

```

For a faster boot time you can use a UEFI bootloader ([coreboot](https://www.coreboot.org/)), even remove all the google components.

From here, you will be able to follow the [Beginner's Guide](/index.php/Beginner%27s_Guide "Beginner's Guide") to install Arch Linux.

## Known Issues

*   Support for the keyboard layout may be found in the [xkeyboard-config-chromebook](https://aur.archlinux.org/packages/xkeyboard-config-chromebook/) package

## See also

*   [https://www.reddit.com/r/chrultrabook/](https://www.reddit.com/r/chrultrabook/)
*   [https://johnlewis.ie/custom-chromebook-firmware/rom-download/](https://johnlewis.ie/custom-chromebook-firmware/rom-download/)
*   [https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html](https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html)
*   [https://lkml.org/lkml/2016/8/12/180](https://lkml.org/lkml/2016/8/12/180)
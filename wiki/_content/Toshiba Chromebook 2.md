# Toshiba Chromebook 2

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Chromebook](/index.php/Chromebook "Chromebook")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

To install Arch Linux on this model of Chromebook, you have to run this script to install a Seabios boot stub:

cd; rm -f flash_chromebook_rom.sh; curl -k -L -O [https://johnlewis.ie/flash_chromebook_rom.sh](https://johnlewis.ie/flash_chromebook_rom.sh); sudo -E bash flash_chromebook_rom.sh  
From here, you will be able to follow the Beginner's Guide to install Arch Linux

## Known Issues

-Sound doesn't work without the appropriate asound.state file (James Fu's backup can be found here: [https://www.dropbox.com/s/gb9mhd0z4356n81/asound.state?dl=0](https://www.dropbox.com/s/gb9mhd0z4356n81/asound.state?dl=0) )  
-Support for the keyboard layout may be found in the xkeyboard-config-chromebook package in the AUR

## See also

*   [https://johnlewis.ie/custom-chromebook-firmware/rom-download/](https://johnlewis.ie/custom-chromebook-firmware/rom-download/)
*   [https://plus.google.com/communities/112479827373921524726](https://plus.google.com/communities/112479827373921524726)
*   [https://plus.google.com/+JamesFuBEEFCAKE/posts/Tf4Pc5Z8reH](https://plus.google.com/+JamesFuBEEFCAKE/posts/Tf4Pc5Z8reH)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Chromebook_2&oldid=408208](https://wiki.archlinux.org/index.php?title=Toshiba_Chromebook_2&oldid=408208)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Toshiba](/index.php/Category:Toshiba "Category:Toshiba")
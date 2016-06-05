### Specs

* * *

*   i5 4210U
*   Nvidia 840M
*   SATA III storage @5400RPM. Easy to swap with an SSD.
*   8GB DDR3 RAM (The first 4GB are soldered onto the motheboard).
*   15" 720p LED.
*   Broadcom BCM43142 WLAN + Bluetooth module.

### Things that needed some tinkering to make work and are functional as of May, 2016.

*   WLAN ―requires [Broadcom Classic Firmware from the AUR](https://aur.archlinux.org/packages/b43-firmware-classic/) to be installed and modprobed, as well as any other WLAN drivers to be blacklisted.
*   [FN] F5 and F6 keys for internal display brightness ―special thanks to [Erkexzcx](/index.php/User:Erkexzcx "User:Erkexzcx") who advised me of his [page for the Asus N550JV](/index.php/ASUS_N550JV "ASUS N550JV"). Edit /edit/default/grub so that the line

> GRUB_CMDLINE_LINUX_DEFAULT="quiet"

becomes

> GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi= "

Yes, there is a blank space in "acpi_osi= ". Next, rebuild your grub:

> sudo grub-mkconfig -o /boot/grub/grub.cfg

and reboot.

### Things pending to fix

*   FN + F8, swaps display output.
*   FN + F10/F11/F12, volume controls.
*   FN + arow keys, multimedia controls.
*   Bluetooth support. I have no use for it lately, so it's not a priority.
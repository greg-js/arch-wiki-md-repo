# Laptop/Samsung

| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - **Samsung** - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| R65-Pro T5500 Boteez | 2008.06 overlord | GeForce 7600 Go | hda-intel | BCM4401B0 100BaseTX | Intel 3945ABG | N/A | Suspend to RAM: N/A
Disk: N/A
Battery: No
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | N/A | N/A |
| Q45 T5750 | 2009.02 | Intel GMA X3100 | hda-intel | Marvel 88E8039 (sky2) | Intel 3945ABG (iwl-3945) | N/A | Suspend to RAM: OK
Disk: OK
Dimming of display: Yes (with some tricks)
CPU frequency scaling: Yes | N/A | 3G+ modem option GTM378 (hso)
Web cam (uvcvideo) | N/A |
| NC110 | 2011.08.19 | 3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.19, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.12 (1024x600), external screens work fine | Intel HD Audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes; rfkill soft block also works | Recognized; not tested | Suspend to RAM: OK
Disk: Not tested
Dimming of display: Yes (with `acpi_backlight=vendor`)
CPU frequency scaling: Yes | N/A | Web cam works, card reader works, two-fingered scrolling works, only half of the function buttons work out-of-the-box ([samsung-tools](https://aur.archlinux.org/packages/samsung-tools/)<sup><small>AUR</small></sup> needed for rest) | N/A |
| QX411 W02UB | 2011.08.19 | Intel HD Graphics 3000 - i915 same packages as above model (1366x768) | Intel HD Audio with ALSA | Realtek Gigabit Ethernet controller (rev 06 | Centrino Wireless-N + WiMAX 6150 (rev 67) | N/A | Suspend to RAM: OK
Disk: OK
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | Web cam (uvcvideo) | No tricky hardware. Fully functional. |
| NP730U3E (Series 7 Ultra) | 2013.06.01 | Intel HD Graphics 4000 @ 1920x1080_60 - works fine (i915 w/KMS and [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel));
AMD Radeon 8570M (muxless hybrid) - Seems to work with PRIME (Linux 3.11);
external screens not tested. | Intel HDA + ALSA | Realtek Gigabit Ethernet, r8169 driver | Intel Centrino Advanced-N 6235 (rev 24), _iwlwifi_ driver;
rfkill works with _samsung-laptop_ module | Not tested | Suspend to RAM: OK
Disk: Not tested
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | Web cam - _uvcvideo_, works ok;
Card reader Realtek RTS5139 - staging driver, works as of Linux 3.11;
Fn keys - only brightness and sound out-of-the-box;
Elan Touchpad works perfectly (Linux 3.11);
Cannot wake up on lid open; | Somewhat tricky, needs work. |

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Samsung&oldid=375511](https://wiki.archlinux.org/index.php?title=Laptop/Samsung&oldid=375511)"
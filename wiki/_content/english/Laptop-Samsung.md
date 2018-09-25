[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – <a class="mw-selflink selflink">Samsung</a> – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
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
CPU frequency scaling: Yes | N/A | Web cam works, card reader works, two-fingered scrolling works, only half of the function buttons work out-of-the-box ([samsung-tools](https://aur.archlinux.org/packages/samsung-tools/) needed for rest) | N/A |
| QX411 W02UB | 2011.08.19 | Intel HD Graphics 3000 - i915 same packages as above model (1366x768) | Intel HD Audio with ALSA | Realtek Gigabit Ethernet controller (rev 06 | Centrino Wireless-N + WiMAX 6150 (rev 67) | N/A | Suspend to RAM: OK
Disk: OK
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | Web cam (uvcvideo) | No tricky hardware. Fully functional. |
| NP730U3E (Series 7 Ultra) | 2013.06.01 | Intel HD Graphics 4000 @ 1920x1080_60 - works fine (i915 w/KMS and [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel));
AMD Radeon 8570M (muxless hybrid) - Seems to work with PRIME (Linux 3.11);
external screens not tested. | Intel HDA + ALSA | Realtek Gigabit Ethernet, r8169 driver | Intel Centrino Advanced-N 6235 (rev 24), *iwlwifi* driver;
rfkill works with *samsung-laptop* module | Not tested | Suspend to RAM: OK
Disk: Not tested
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | Web cam - *uvcvideo*, works ok;
Card reader Realtek RTS5139 - staging driver, works as of Linux 3.11;
Fn keys - only brightness and sound out-of-the-box;
Elan Touchpad works perfectly (Linux 3.11);
Cannot wake up on lid open; | Somewhat tricky, needs work. |
| NP535U3C (Series 5) | 2016.03.01 | Radeon HD 7300G @ 1366x768_60 - works fine with [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)
HDMI works fine. | Generic AMD Audio;
Works fine with [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) | Realtek Gigabit Ethernet, r8169 driver | Qualcomm Atheros AR9462 ath9k driver | AR3012 Bluetooth 4.0, works fine | Suspend to RAM: OK
Disk: Not tested
Dimming of display: Yes
CPU frequency scaling: Yes | N/A | Web-Cam: OK;
Card reader: Untested;
Fn keys - All Out-of-Box;
Elan Touchpad works perfectly | N/A |
| Samsung Notebook 7 Spin [NP740U3L-L02US](/index.php/Samsung_NP740U3L-L02US "Samsung NP740U3L-L02US") | 2016.07.01 | Intel HD Graphics 520 | works | N/A | *iwlwifi* driver | Not tested | ? | N/A | Need to work on touchpad sensitivity

Dual booting required shutting off secure boot | Very recent (as of July 4, 2016) 2-in-1 laptop model with pretty generic hardware (spec info [here](http://www.notebookocean.com/samsung-notebook-7-spin-np740u3l-l02us-specs/)); so far seems very usable |
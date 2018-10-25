[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – <a class="mw-selflink selflink">Fujitsu</a> – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Lifebook T902 | 2017.08.01 | mesa works great (Intel) | Works (Intel) | Works (Intel) | Works (wifi-menu and networkmanager) (Intel) | Works | [TLP](/index.php/TLP "TLP") works | untested | Touchscreen / pen works with [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom), but the [driver needs to be manually removed and readded after suspend](https://github.com/link07/Arch-Makepkgs-not-in-AUR/tree/master/wacom-touchscreen-fix).

Fingerprint scanner works with [fprint](/index.php/Fprint "Fprint").

 | Haven't found a way to program the button panel by the power button yet. Sound buttons work, super key button works (in kde at least) but rotation lock, A and B buttons do nothing.

Also haven't found a way to rotate screen and disable the keyboard / touchpad automatically when switching to tablet mode, making tablet mode essentially unusable.

 |
| Lifebook T904 | circa 2014 | ?? | ?? | ?? | Works (Intel) | ?? | ?? | ?? | According to the [Fprint wiki](/index.php/Fprint "Fprint"), the reader does not appear to be a [supported model](http://www.freedesktop.org/wiki/Software/fprint/libfprint/Supported_devices/).

If the reader is unused, it is recommended that the device be physically disabled in the bios.

 | Fan noise was an issue on initial BIOS revisions.

The change log for BIOS version 1.08 noted a fan settings update which has since resolved the fan noise issue.

User confirmations of the fix may be found after post #540 [[1]](http://forum.tabletpcreview.com/fujitsu/61570-official-t904-thread-54.html#post391747)

 |
| Amilo Se 1520 | circa 2007 | Works | Works poorly with [ALSA](/index.php/ALSA "ALSA"). Both SPDIF and the external microphone do not work. The internal microphone above the LCD works, however the volume can't be changed or the microphone disabled. | ?? | Works (ipw3945 chipset, see [Wireless network configuration#iwlegacy](/index.php/Wireless_network_configuration#iwlegacy "Wireless network configuration")) | ?? | Works | ?? | Touchpad works with [Synaptics](/index.php/Synaptics "Synaptics") | `Alt`+`Function` key commands work, but the special buttons on the left side of the keyboard do not work out of the box. |
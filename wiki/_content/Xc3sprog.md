# Xc3sprog

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

xc3sprog is a suite of utilities for programming Xilinx FPGAs, CPLDs, and EEPROMs with the Xilinx Parallel Cable and other JTAG adapters

## Installation

Install [xc3sprog-svn](https://aur.archlinux.org/packages/xc3sprog-svn/) from AUR.

## Devices

### Xilinx USB JTAG

Initially has USBID=03fd:000f, after proper initialization becomes 03fd:0008.

*   install [fxload](https://aur.archlinux.org/packages/fxload/) from AUR.
*   extract xusb_xlp.hex from [Xilinx ISE](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")
*   create file /etc/udev/rules.d/99-xilinx.rules

```
 SUBSYSTEM=="usb", ACTION=="add", ATTR{idVendor}=="03fd", ATTR{idProduct}=="000f", RUN+="/usr/bin/fxload -v -t fx2 -I /path/to/xusb_xlp.hex -D $tempnode"

```

*   reload udev rules with "udevadm control --reload" and replug JTAG
*   test connection with "xc3sprog -c xpc -j"

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xc3sprog&oldid=373691](https://wiki.archlinux.org/index.php?title=Xc3sprog&oldid=373691)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
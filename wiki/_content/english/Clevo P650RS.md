The P650RS is a device by the taiwanese OEM manufacturer Clevo. It is also sold as Sager NP8153-S. The hardware is configurable and includes an Intel Skylake Core i7, NVidia 1070M graphics, USB-C connectors, a fingerprint reader, mini DisplayPort as well as HDMI connections, and more.

## Installation

Installing Archlinux requires kernel parameters `nomodeset` and `nouveau.modeset=0` and most of the hardware works out of the box. It is recommended to use UEFI boot at this time.

## Webcam

As with the [Clevo W840SU](/index.php/Clevo_W840SU "Clevo W840SU") the webcam must be activated with Fn-F10 before it will show up in the device list.

## Display

Using the Nvidia proprietary driver (testing with 375.20) the backlight may not come back on after the display has gone to sleep. A workaround is to drop to console (e.g. Ctrl-Alt-F2) and then back to X.
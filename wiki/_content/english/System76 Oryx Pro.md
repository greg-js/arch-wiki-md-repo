<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Drivers](#Drivers)
*   [3 Graphical](#Graphical)
*   [4 Audio](#Audio)
*   [5 Suspend/Hibernate](#Suspend/Hibernate)

## Installation

The System76 Oryx Pro comes with two NVMe M.2 slots, as well as space for a 2.5" SSD/HDD. Booting from NVMe requires the use of EFI, while booting over SATA/AHCI does not. Typically EFI would be a safe-to-use method for this laptop overall.

## Drivers

The System76 Oryx Pro has customized utilities and daemons that assist with running the Oryx Pro nicely under Linux. This includes driver (graphical, io, fan) configuration, firmware updates, and LED control.

System76 produces a distribution called Pop OS! which they install on their machines. This guide is meant to align drivers and graphical configurations with the style that Pop OS! chooses, which seems to be best for these configurations.

The collection of drivers can be found in the AUR.

[system76-driver](https://aur.archlinux.org/packages/system76-driver/)

[system76-dkms](https://aur.archlinux.org/packages/system76-dkms/)

[system76-io-dkms](https://aur.archlinux.org/packages/system76-io-dkms/)

[system76-firmware-daemon](https://aur.archlinux.org/packages/system76-firmware-daemon/)

[system76-power](https://aur.archlinux.org/packages/system76-power/)

There are also -git versions of many of these packages, if you wish to stay bleeding edge.

## Graphical

This system comes complete with an integrated (intel) and discrete (nvidia) graphics card. The external ports (DP over Mini-DP, DP over USB-C, HDMI) are tied to the discrete nvidia card. Some users have reported getting this to work right with Bumblebee.

When in doubt, remove bumblebee and install nvidia proprietary drivers.

Your mileage may vary if you are using a more complete DE like Gnome; this has only been tested with i3-wm.

## Audio

Audio seems to work out of the box with a USB headset, however, it does not relay audio to the onboard speaker. This section needs to be feature complete with workarounds for any issues.

## Suspend/Hibernate

Out of the box, Arch Linux does not resume a previously suspended or hibernated session. This section needs to be feature complete with workarounds for any issues.
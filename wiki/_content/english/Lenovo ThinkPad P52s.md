Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Xorg](#Xorg)
*   [4 Bumblebee](#Bumblebee)
*   [5 Prime](#Prime)
*   [6 Nvidia-xrun](#Nvidia-xrun)
*   [7 Smartcard reader](#Smartcard_reader)

## Installation

Use the [Installation guide](/index.php/Installation_guide "Installation guide"). Make sure that Secure Boot is disabled in the BIOS. For video output on Xorg see the [Xorg configuration section](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_P52s#Xorg).

## Configuration

## Xorg

The Intel device needs to be specified in the Xorg config. Add the following section to your Xorg configuration (`/etc/X11/xorg.conf`).

```
Section "Device"
   Identifier "intel"
   Driver "intel"
   BusID "PCI:0:2:0"
   Option "TearFree" # Not required but helpful
EndSection

```

## Bumblebee

Bumblebee seems to work fine with the proprietary [NVIDIA](http://www.nvidia.com) drivers. Follow the [Bumblebee instalation guide](/index.php/Bumblebee#Installation "Bumblebee"). You might need to set the PCI bus (showed in `lspci`) in `/etc/bumblebee/xorg.conf.nvidia`.

## Prime

[PRIME](/index.php/PRIME "PRIME") doesn't seem to be working properly. The 3D device shows use as the Quadro P500 but performance is the same as the Intel GPU. Not sure what's going on there.

## Nvidia-xrun

[Nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun") seems to be working properly, even with Bumblebee set up. To use it you just need go to other tty and run `nvivia-xrun`.

## Smartcard reader

For the smartcard reader to work you need to install [pcsclite](https://www.archlinux.org/packages/?name=pcsclite). You can test it with `sudo pcsc_scan` (you need [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) installed).
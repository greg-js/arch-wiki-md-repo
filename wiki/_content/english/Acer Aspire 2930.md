## Contents

*   [1 Hardware](#Hardware)
*   [2 Ethernet](#Ethernet)
*   [3 Wireless](#Wireless)
*   [4 Xorg](#Xorg)
*   [5 Sound](#Sound)
*   [6 Card Reader](#Card_Reader)
*   [7 Webcam](#Webcam)
*   [8 ACPI](#ACPI)
*   [9 Touchpad](#Touchpad)

## Hardware

**Processor:** Intel Core 2 Duo T5800 _This can vary based on exact model_

**Video:** Intel Corporation GM45 Chipset

**Audio:** Intel Coporation 82801I HD Audio Controller

**Wired NIC:** Realtek RTL8111/8168B

**Wireless NIC:** Intel Corporation Wireless Wifi Link 5100

## Ethernet

Should work out of the box

## Wireless

See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration").

## Xorg

See [Xorg](/index.php/Xorg "Xorg") and [Intel graphics](/index.php/Intel_graphics "Intel graphics").

## Sound

[PulseAudio](/index.php/PulseAudio "PulseAudio") did the job admirably for me getting the sound working.

External speakers will work after configuration, however headphone and microphone jacks need one additional fix

 `/etc/modprobe.d/modprobe.conf`  `options snd-hda-intel model=acer position_fix=1 enable=yes` 

## Card Reader

Seemed to work with no additional configuration.

## Webcam

Worked with no additional configuration.

## ACPI

Worked with no additional configuration

## Touchpad

Works after [synaptics](/index.php/Synaptics "Synaptics") is installed. For touchpad taps follow configuration instructions copying /usr/share/X11/xorg.conf.d/50-synaptics.conf to /etc/X11/xorg.conf.d/
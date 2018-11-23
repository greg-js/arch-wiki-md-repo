The HP Envy X360 15-bq102ng was released in 2017\. It has a Ryzen Mobile 5 2500u with an integrated Vega 8 GPU and 8GB of DDR4 RAM.

| **Device** | **Model** | **Status** | **Modules** |
| GPU | AMD Vega 8 IGPU | **Working** | xf86-video-amdgpu; Backlight works |
| Wifi | Realtek RTL8822BE | **Working** | r8822be |
| Bluetooth | Realtek RTL8822BE | **Working** | btusb |
| Audio | **Working** | snd_hda_intel |
| Touchpad | Synaptics | **Working** | synaptics |
| Camera | Normal 1080p + IR 336x340 | **Working** | uvcvideo |
| Card Reader | RTS522A | **Working** | rtsx_pci |
| Sensors | STM Sensor hub | **Working** | Use [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) to use autorotate |
| USB C | AMD xHCI Host Controller | **Working** | Data and DP working |

## Contents

*   [1 Installing Arch](#Installing_Arch)
*   [2 Battery and Power Management](#Battery_and_Power_Management)
*   [3 Display, Video Card](#Display,_Video_Card)
*   [4 Touchscreen and Stylus](#Touchscreen_and_Stylus)
*   [5 Orientation Sensor](#Orientation_Sensor)
*   [6 Wireless Networking](#Wireless_Networking)
*   [7 Bluetooth](#Bluetooth)
*   [8 Hard Drive](#Hard_Drive)
*   [9 Dual Boot](#Dual_Boot)

## Installing Arch

This laptop has secure boot enabled by default. To start the installer you need to disable it in the UEFI. Then you can just boot the installer in UEFI mode and just install like a normal UEFI system.

## Battery and Power Management

On Linux 4.17 I get about 5 hours on light load, like watching youtube. Installing [tlp](https://www.archlinux.org/packages/?name=tlp) is a good idea. Suspend and Hibernate works.

## Display, Video Card

The integrated Vega GPU works with the AMDGPU drivers. Apparently the display panel is freesync capable.

## Touchscreen and Stylus

At the moment (22.11.2018) you need to build a Kernel with custom patches to get the touchscreen working. [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=198715) An effort to upstream this work is in progress, which will make it possible to use the touchscreen with the stock Arch kernel.

## Orientation Sensor

You currently need to install [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) and reboot to make the orientation sensor work. This will disable the keyboard and touchpad, and invert the side volume buttons when the screen is held at the right orientation or is folded. The Gnome desktop environment does support the rotation natively. Other desktop enviroments may need extra software. You could compile and use this daemon [[2]](https://github.com/mrquincle/yoga-900-auto-rotate) written in C.

## Wireless Networking

Works out of the box.

## Bluetooth

Works, but to use an BT audio device with GNOME you have to install [pulseaudio-bluetooth-a2dp-gdm-fix](https://aur.archlinux.org/packages/pulseaudio-bluetooth-a2dp-gdm-fix/).

## Hard Drive

Built-in NVME drive works with advertised speed. Blockdevices are loacated at /dev/nvme0n1p*. There is an empty bay for an additional SATA 2.5 inch drive, but you have to buy a proprietary cable.

## Dual Boot

Not tested, but there shouldn't any difficulties.
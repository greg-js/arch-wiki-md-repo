The HP Envy X360 13z-ag000 was released in 2018\. It has variable processors/ram and displays, from a Ryzen Mobile 2300U to a 2700U, from 4GB RAM to 16GB RAM, and a 1080p display to a 4K display.

The specs of my particular model are:

*   2500U with 16GB RAM
*   4K display
*   Realtek RTL8822BE wireless chip

| **Device** | **Model** | **Status** | **Modules** |
| GPU | AMD Vega IGPU | **Working** | xf86-video-amdgpu; Backlight works |
| Wifi | Realtek RTL8822BE | **Working** | r8822be |
| Bluetooth | Realtek RTL8822BE | **Working** | btusb |
| Audio | **Working** | snd_hda_intel |
| Touchpad | Synaptics | **Working** | synaptics |
| Camera | Normal 1080p + IR 336x340 | **Working** | uvcvideo |
| Sensors | STM Sensor hub | **Not Working** | On Windows used for orientation sensing and hard drive drop protection |
| USB C | AMD xHCI Host Controller | **Not Working** | Data and DP working |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

There appears to be an option to use your own Secureboot keys. I've not yet investigated that.

## Battery and Power Management

a 4 hour battery life because of the 4K display. Currently I'm running a patched 4.17 kernel; 4.18 might improve battery life somewhat.

## Display, Video Card

The integrated Vega GPU works with the AMDGPU drivers. `GDK_SCALE=2` is somewhat necessary for most applications.

## Touchscreen and Stylus

Kernel 4.19.5 or greater is needed. [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=198715#c14) [[2]](https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.19.5)

## Orientation Sensor

No `iio` sensors are enumerated as of 4.18-rc7, with all possible iio modules compiled. `iio-sensor-proxy` returns no sensors detected.

## Wireless Networking

Works out of the box. `aspm=0` seems to prevent the card from dropping offline as much, but also worsens battery life.

## Bluetooth

Works out of the box with Motorola Pulse Escape on kernel 4.19.5.

## Hard Drive

Built-in NVME drive works with advertised speed. Blockdevices are loacated at /dev/nvme0n1p*.

## Dual Boot

Untested, but there shouldn't any difficulties.
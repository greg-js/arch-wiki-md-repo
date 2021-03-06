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
*   [4 Audio](#Audio)
*   [5 Touchscreen and Stylus](#Touchscreen_and_Stylus)
*   [6 Orientation Sensor](#Orientation_Sensor)
*   [7 Wireless Networking](#Wireless_Networking)
*   [8 Bluetooth](#Bluetooth)
*   [9 Hard Drive](#Hard_Drive)
*   [10 Dual Boot](#Dual_Boot)

## Installing Arch

This laptop has secure boot enabled by default. To start the installer you need to disable it in the UEFI. Then you can just boot the installer in UEFI mode and just install like a normal UEFI system.

There appears to be an option to use your own Secureboot keys. I've not yet investigated that.

## Battery and Power Management

a 4 hour battery life because of the 4K display. Currently I'm running a patched 4.17 kernel; 4.18 might improve battery life somewhat.

## Display, Video Card

The integrated Vega GPU works with the AMDGPU drivers. `GDK_SCALE=2` is somewhat necessary for most applications.

## Audio

The"Bang & Olufsen" top-soundbar is by default disabled. You can activate it by using the "hdajackretask" utility provided by alsa-tools. More information can be found in this thread: [https://bugzilla.kernel.org/show_bug.cgi?id=189331](https://bugzilla.kernel.org/show_bug.cgi?id=189331)

The exact pinout can be found in this attachment: [https://bugzilla.kernel.org/attachment.cgi?id=282109&action=edit](https://bugzilla.kernel.org/attachment.cgi?id=282109&action=edit)

`
```
   Options : [x] Show unconnected
             [ ] Set model  =  auto
             [X] Advanced ovveride
             [ ] Parser hints

```
``
```
   Pin ID; 0x14 
   [x] Override
   Connectivity : Jack; Location : Internal; Device : Speaker; Jack : Other Analog
   Color : Unknown; Jack detection : Not present; Channel group : 5; Channel : Front

```
``
```
   Pin ID: 0x17
   [X] Override
   Connectivity : Jack; Location : Internal; Device : Speaker; Jack : Other
   Color : Unknown; Jack detection : Not present; Channel group : 5; Channel : Back

```
`
**Note:** that the top-soundbar only fires when using close to the max volume.

## Touchscreen and Stylus

Kernel 4.19.5 or greater is needed. [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=198715#c14) [[2]](https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.19.5)

The built in ELAN digitizer doesn't use the wacom driver by default, but it can be configured to do so. Switching to the wacom driver allows easier configuration of the digitizer and pen through tools like xsetwacom. This can be achieved with the following xorg configuration file:

 `/etc/X11/xorg.conf.d/99-ELAN-stylus.conf` 
```
Section "InputClass"
    Identifier "Elan driver override"
    MatchUSBID "04f3:*"
    MatchDevicePath "/dev/input/event*"
    MatchIsTablet "true"
    Driver "wacom"
EndSection

```

After a reboot xsetwacom should now correctly register the device.

 `xsetwacom --list devices` 
```
ELAN0732:00 04F3:262A stylus    	id: 13	type: STYLUS    
ELAN0732:00 04F3:262A eraser    	id: 18	type: ERASER

```

You can use xinput to probe the different devices and find out what actions get triggered by which buttons. For instance the "wacom bamboo ink" pen triggers the eraser device while touching the screen while maintaining the second side button pressed.

```
xinput test $deviceID

```

The following simple example script will bind rightclick to the eraser device.

```
device=$(xsetwacom --list | grep -i "eraser" |  awk '{print $(NF-2)}') 
xsetwacom --set "$device" button 1 3

```

## Orientation Sensor

No `iio` sensors are enumerated as of 4.18-rc7, with all possible iio modules compiled. `iio-sensor-proxy` returns no sensors detected.

## Wireless Networking

Works out of the box. `aspm=0` seems to prevent the card from dropping offline as much, but also worsens battery life.

## Bluetooth

Works out of the box with Motorola Pulse Escape on kernel 4.19.5.

## Hard Drive

Built-in NVME drive works with advertised speed. Blockdevices are located at /dev/nvme0n1p*.

## Dual Boot

Untested, but there shouldn't any difficulties.
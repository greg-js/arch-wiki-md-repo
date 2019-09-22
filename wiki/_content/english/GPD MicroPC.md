Notes for the [GPD MicroPC](https://www.gpd.hk/gpdmicropc).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Specs](#Specs)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 kernel modules](#kernel_modules)
    *   [3.2 screen rotation during boot](#screen_rotation_during_boot)
    *   [3.3 wayland](#wayland)

## Specs

*   Display: 6inch 720x1280 (yes, rotated)
*   CPU: Intel Gemini Lake N4100 4x 1.10GHz
*   RAM: 8GB LPDDR4-2133
*   Storage: 128GB M2-2242 SATA SSD (replacable)
*   Battery: 6200mAh
*   WiFi: Intel Dual Band Wireless-AC 3165
*   LAN: Realtek RTL8168
*   Audio: Intel 8086:3198
*   Input Devices: QWERTY Keyboard, 3 Mouse Bottons, Touchpad, Power Buttom, physical CPU-Fan Switch, reset Switch
*   Ports: 3 x USB 3 type A, 1 x HDMI, 1 x USB 3 type C, 1 x microSDXC, 1 x RJ45, 1 x DB9 (RS232), 1 x 3.5mm Headphone Jack

USB-C Port is used for charging, it supports PD 2.0 but is also compatible with 5V USB Chargers

## Installation

Please be sure to have at least an installation Image with linux 5.1 Kernel.

## Configuration

### kernel modules

For an working keyboard during boot, add battery to the preloaded modules:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(battery)
...

```

### screen rotation during boot

For correct screen rotation during boot, add fbcon=rotate:1 to your bootloader config:

 `/boot/loader/entries/arch.conf` 
```
...
options root=/dev/mapper/crypt cryptdevice=UUID=000ccc23-4223-0ccc-4223-deadbeaf2342:btrfs rw fbcon=rotate:1
...

```

### wayland

The screen is on DSI-1 and 90° rotated, so you need to configure this:

 `~/.config/sway/config` 
```
...
# configure display
# get the names of your outputs by: swaymsg -t get_outputs
output DSI-1 resolution 720x1280 transform 90
...

```
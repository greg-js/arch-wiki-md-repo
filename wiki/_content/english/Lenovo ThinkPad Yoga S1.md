## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Battery](#Battery)
    *   [3.2 Graphics](#Graphics)
    *   [3.3 Touchscreen and Stylus](#Touchscreen_and_Stylus)
    *   [3.4 Sensor hub](#Sensor_hub)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Wakeup after suspend](#Wakeup_after_suspend)

## Overview

This Page is a work in progress

Hardware info can be found [here](https://www.thinkwiki.org/wiki/Category:Yoga_S1)

The hardware and firmware supports both [UEFI](/index.php/UEFI "UEFI") and BIOS (mentioned as "Legacy" in firmware). It comes preinstalled with Windows in UEFI mode, so the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") is already there. By default the HDD/SSD should be using [GPT](/index.php/GPT "GPT").

## Installation

All you need is to disable Secure Boot and install ArchLinux as usual, Legacy install is also possible

## Configuration

### Battery

Battery functions like charging thresholds can be controlled using the script [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) together with the kernel module [acpi_call](https://www.archlinux.org/packages/?name=acpi_call). The [TLP](/index.php/TLP "TLP") power saving tool supports using acpi_call as backend for setting the thresholds as well.

### Graphics

The graphics driver is provided by the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package from the [Official repositories](/index.php/Official_repositories "Official repositories"). Unfortunately screen is very PWMed, so you might need to [fix](/index.php/Backlight#Backlight_PWM_modulation_frequency_.28Intel_i915_only.29 "Backlight") it. Also [TearFree video](/index.php/Intel_graphics#Tearing "Intel graphics") works great

### Touchscreen and Stylus

Touchscreen works with the Wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)). [thinkpad-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-yoga-scripts-git/) provides useful services such as disabling touchscreen while pen is near the screen.

**Note:** See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for more info on optimizing the touchscreen experience.

### Sensor hub

Laptop has STM Micro HID Sensor HUB with such sensors as

*   accelerometer sensor
*   rotation sensor
*   magnetometer sensor
*   angular velocity sensor (aka gyroscope)
*   inclination sensor
*   ambient light sensor

To work with sensors you need [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy). [thinkpad-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-yoga-scripts-git/) also provides service for ambient light sensor. With [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) while turning into tablet mode touchpad and keyboard are automatically disabled on KDE Plasma 5.13.3, not sure about other DEs

## Troubleshooting

### Wakeup after suspend

After installing [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) my Yoga is immediately waking after suspending. The soloution is to disable XHC in wake events

```
echo XHC | sudo tee /proc/acpi/wakeup

```
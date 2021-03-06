| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working |
| Battery Status | Working |
| Camera | Partially |
| Bluetooth | Working |
| MicroSD Reader | Working |
| Power Management | Working |
| Accelerometer | Not tested yet |
| Luxsensor | Partially |
| Gyroscope | Partially |
| Hardware Buttons | Working |

The [Acer Switch Alpha 12](https://www.acer.com/ac/en/US/content/series/switchalpha12) is a two 2 in 1 [Tablet PC](/index.php/Tablet_PC "Tablet PC") device, equipped with a 12 inch display that supports for 2160 x 1440 pixels. This installation was done on the version SA5-271-38U0 which is a version with an i3-6100 CPU and 4GB of RAM. Please note I was not using Arch-Linux directly, but used the derivate Antergos for the installation.

## Contents

*   [1 Installation](#Installation)
*   [2 Camera](#Camera)
*   [3 Power Management](#Power_Management)
*   [4 Sensors](#Sensors)

## Installation

You need to disable Secure Boot in BIOS first, which requires you to set a Supervisor Password. I also recommend to enable "F12 Boot Menue". To go into the BIOS, press "Volume Up" while powering up the device.

The remaining part of the installation should be the same as on every other x86 System.

## Camera

Front Camera is detected properly and working fine. Camera on the back is not detected as of May 2018.

## Power Management

[tlp](https://www.archlinux.org/packages/?name=tlp) is working fine. You may want to exclude the detachable keyboard from USB auto-suspend, otherwise it misbehaves.

## Sensors

Luxsensor and Gyroscope are working well under [GNOME](/index.php/GNOME "GNOME") with [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) installed.
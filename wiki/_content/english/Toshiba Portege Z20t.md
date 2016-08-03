The power of an enterprise-class laptop. The freedom and convenience of a tablet. Why choose when you can get the best of both? The Toshiba Portégé® Z20t Ultrabook® offers innovative 2-in-1 versatility in a supremely crafted chassis, along with outstanding battery life and an exceptional handwriting experience.

## Contents

*   [1 Specifications](#Specifications)
*   [2 Installation and configuration](#Installation_and_configuration)
    *   [2.1 CPU & Graphics](#CPU_.26_Graphics)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Wifi](#Wifi)
    *   [2.5 Smart Card Reader](#Smart_Card_Reader)
    *   [2.6 Display Backlight Control](#Display_Backlight_Control)
    *   [2.7 Keyboard Backlight control](#Keyboard_Backlight_control)

## Specifications

| Name | Series Toshiba Portege Z20t |
| Processor | Intel Core M-5Y71 |
| Screen | 12.5" Touchscreen |
| RAM | 4-8-16GB |
| HDD | Toshiba SDD (256 [MZNTE256HMHP], 256, 512 GB) |
| Optical Drive | none |
| Graphics | Intel® HD Graphics 5300 (Broadwell GT2) |
| Network | Ethernet - Intel I218-LM, Wifi - Intel Wireless 7265 |
| Touchpad | ALPS (Trackstick+Mousepad) |
| Fingerprint reader | none |
| Smart Card Reader | Realtec (Micro SD card reader) |
| Webcam | Toshiba Web Camera (Front and Back) |

## Installation and configuration

### CPU & Graphics

Works fine after installation, the video have some issues with lightdm locker when locking the session or after resume, if that's the case the configuration recommended for Intel works [Intel Arch](/index.php/Intel_graphics#Configuration "Intel graphics")
Touchscreen works fine tested in gnome.

### Touchpad

It Works without any modification including gestures.

### Bluetooth

Works

### Wifi

Works

### Smart Card Reader

Works fine, it is a mini SD card reader not a regular SD Card.

### Display Backlight Control

It works out of the box, even after resume, no additional package has been installed

### Keyboard Backlight control

Works

For instructions on Keyboard backlight toggle see [Toshiba Portege Z30-A#Installation and configuration](/index.php/Toshiba_Portege_Z30-A#Installation_and_configuration "Toshiba Portege Z30-A").

Since changing sys values requires root, one can either write a wrapper for bash scripts for setuid, which is generally considered insecure. Here is a simple toggle switch written in C: [https://github.com/Exel232/Configurations/tree/highcontrast/Toshiba](https://github.com/Exel232/Configurations/tree/highcontrast/Toshiba)
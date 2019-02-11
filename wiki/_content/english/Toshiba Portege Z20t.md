The power of an enterprise-class laptop. The freedom and convenience of a tablet. Why choose when you can get the best of both? The Toshiba Portégé® Z20t Ultrabook® offers innovative 2-in-1 versatility in a supremely crafted chassis, along with outstanding battery life and an exceptional handwriting experience.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Specifications](#Specifications)
*   [2 Installation and configuration](#Installation_and_configuration)
    *   [2.1 CPU & Graphics](#CPU_&_Graphics)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Wifi](#Wifi)
    *   [2.5 LTE/3G](#LTE/3G)
    *   [2.6 Smart Card Reader](#Smart_Card_Reader)
    *   [2.7 Display Backlight Control](#Display_Backlight_Control)
    *   [2.8 Keyboard Backlight control](#Keyboard_Backlight_control)
    *   [2.9 Fn-F9 Touchpad Toggle](#Fn-F9_Touchpad_Toggle)
*   [3 Issues](#Issues)
    *   [3.1 No speaker sound when resuming from suspend to RAM](#No_speaker_sound_when_resuming_from_suspend_to_RAM)

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

### LTE/3G

Works in some situations. Some providers might not connect with the default configuration.

The built-in Sierra EM7305 is operating in mbim-mode, which is the default configuration on Windows 8/10 Systems. mbim is still not well supported in Linux. Switching to QMI-Mode can solve some problems. [Source](http://www.0xf8.org/2015/07/dell-wireless-5809e-support-in-linux-a-followup/#more-1258)

 `99-em7305.rules` 
```
ACTION!="add|change", GOTO="mbim_to_qmi_rules_end"
SUBSYSTEM!="usb|drivers", GOTO="mbim_to_qmi_rules_end"

# force Sierra EM7305 to configuration #1
SUBSYSTEM=="usb", \
        ATTR{idVendor}=="1199", ATTR{idProduct}=="9063", \
        ATTR{bConfigurationValue}="1"

# load qcserial module
SUBSYSTEM=="usb", \
        ATTR{idVendor}=="1199", ATTR{idProduct}=="9063", \
        RUN+="/sbin/modprobe -b qcserial"

# add the new id in the qcserial driver
SUBSYSTEM=="drivers", \
        ENV{DEVPATH}=="/bus/usb-serial/drivers/qcserial", \
        ATTR{new_id}="1199 9063"

# load qmi_wwan module
SUBSYSTEM=="usb", \
        ATTR{idVendor}=="1199", ATTR{idProduct}=="9063", \
        RUN+="/sbin/modprobe -b qmi_wwan"

# add the new id in the qmi_wwan driver
SUBSYSTEM=="drivers", \
        ENV{DEVPATH}=="/bus/usb/drivers/qmi_wwan", \
        ATTR{new_id}="1199 9063"

LABEL="mbim_to_qmi_rules_end"

```

### Smart Card Reader

Works fine, it is a mini SD card reader not a regular SD Card.

### Display Backlight Control

It works out of the box, even after resume, no additional package has been installed

### Keyboard Backlight control

Works

For instructions on Keyboard backlight toggle see [Toshiba Portege Z30-A#Installation and configuration](/index.php/Toshiba_Portege_Z30-A#Installation_and_configuration "Toshiba Portege Z30-A").

Since changing sys values requires root, one can either write a wrapper for bash scripts for setuid, which is generally considered insecure. Here is a simple toggle switch: [KbdBacklightToggle in C](https://github.com/Exel232/Configurations/raw/master/Toshiba/kbdback.c)

### Fn-F9 Touchpad Toggle

Needs custom hwdb to work. See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys"). Example hwdb provided here, but you might want to choose a different keycode: [HWDB Config](https://github.com/Exel232/Configurations/raw/master/Toshiba/60-toshiba-input.hwdb)

## Issues

### No speaker sound when resuming from suspend to RAM

See [https://bbs.archlinux.org/viewtopic.php?id=213720](https://bbs.archlinux.org/viewtopic.php?id=213720)
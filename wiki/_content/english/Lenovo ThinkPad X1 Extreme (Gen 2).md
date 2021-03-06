Related articles

*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")
*   [Lenovo ThinkPad X1 Extreme](/index.php/Lenovo_ThinkPad_X1_Extreme "Lenovo ThinkPad X1 Extreme")

| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i915 |
| NVIDIA GeForce GTX 1650 | Working | nvidia |
| Intel AX200 Wifi | Working | iwlwifi |
| Intel HDA | Working | snd_hda_intel |
| Synaptics touchpad | Working | libinput |
| Chicony Electronics | Working | uvcvideo |
| Card reader | Working | xhci_hcd |
| Intel AX200 Bluetooth | Working | btusb |
| Intel Thunderbolt | Working | thunderbolt |
| Synaptics fingerprint reader | Initial Support Complete |

The [Thinkpad X1E Gen 2](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/X1-Extreme-Gen-2/p/22TP2TXX1E2) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2019 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
    *   [1.1 Thunderbolt 3](#Thunderbolt_3)
    *   [1.2 Battery](#Battery)
        *   [1.2.1 Invalid stats workaround](#Invalid_stats_workaround)
        *   [1.2.2 Battery life and graphics](#Battery_life_and_graphics)
    *   [1.3 Graphics](#Graphics)
        *   [1.3.1 Nouveau](#Nouveau)
        *   [1.3.2 NVIDIA](#NVIDIA)
            *   [1.3.2.1 Prime features](#Prime_features)
            *   [1.3.2.2 Power Management](#Power_Management)
            *   [1.3.2.3 Optimus manager](#Optimus_manager)
    *   [1.4 OLED Display](#OLED_Display)
        *   [1.4.1 Brightness control](#Brightness_control)
    *   [1.5 Audio](#Audio)
        *   [1.5.1 Audio pop on shutdown and startup](#Audio_pop_on_shutdown_and_startup)
    *   [1.6 Fingerprint](#Fingerprint)
    *   [1.7 Card reader](#Card_reader)
        *   [1.7.1 Installation](#Installation)
        *   [1.7.2 Testing](#Testing)
    *   [1.8 Webcam](#Webcam)
    *   [1.9 Keyboard](#Keyboard)
        *   [1.9.1 Backlight](#Backlight)
    *   [1.10 Touchpad](#Touchpad)
        *   [1.10.1 Acceleration](#Acceleration)
        *   [1.10.2 Two-Finger Right Click](#Two-Finger_Right_Click)
        *   [1.10.3 Tap Clicking](#Tap_Clicking)
*   [2 Firmware](#Firmware)
*   [3 Software](#Software)
    *   [3.1 Throttling fix](#Throttling_fix)
    *   [3.2 CPU undervolting](#CPU_undervolting)

## Hardware

### Thunderbolt 3

To use Thunderbolt 3, ensure you are on the latest BIOS firmware (doing the following steps on older BIOSes may brick your device):

1\. Go into BIOS

2\. Enable BIOS Assist mode: (Thunderbolt 3 -> Enable BIOS assist mode) *Ensure you're on the latest BIOS!*

### Battery

#### Invalid stats workaround

As of writing, [a bug exists](https://bbs.archlinux.org/viewtopic.php?pid=1859876) where the battery data can appear corrupt, wildly incorrect, or seem to change drastically from boot to boot. To workaround this bug you should add battery to the `/etc/mkinitcpio.conf`.

```
MODULES=(**battery**)

```

Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") for these changes to take effect.

**Note:** You can also build the battery module into your kernel.

#### Battery life and graphics

[bbswitch does not work](https://bbs.archlinux.org/viewtopic.php?id=238389) on this laptop to disable the NVIDIA card when not in use. To disable the NVIDIA card you can run:

```
# tee /sys/bus/pci/devices/0000\:01\:00.1/remove <<<1
# tee /sys/bus/pci/devices/0000\:01\:00.0/remove <<<1

```

**Note:** It may be much easier to just use optimus manager with the necessary power options described in [#Graphics](#Graphics)

### Graphics

#### Nouveau

Currently (5.2.9-arch1), the Nouveau driver can cause quite a lot of kernel panics when using the webcamera. You should blacklist this driver to prevent it from being loaded.

#### NVIDIA

##### Prime features

The NVIDIA driver now supports PRIME Offloading. [Following this guide](http://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/primerenderoffload.html) you can try out this new mode. However, [external display ports will not work with only this method](https://forum.manjaro.org/t/nvidia-render-offloading-help-getting-external-monitor-working/99430/22).

##### Power Management

To get the best power options the graphics card may be configured to use low power mode by [following the guide here](http://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/dynamicpowermanagement.html)

##### Optimus manager

Currently, one of the easiest solutions for this laptop is to use [optimus-manager](https://github.com/Askannz/optimus-manager) with the hybrid backend. This requires the most up to date nvidia and xorg-server packages.

This allows easy switching between the PRIME offloading feature above, and a mode where external display ports (HDMI and USB-C) work.

### OLED Display

#### Brightness control

OLED screens have no backlight, brightness cannot be controlled by changing backlight power in the traditional way. Instead, it can be controlled using PWM by enabling following option:

```
echo "options i915 enable_dpcd_backlight=1" >> /etc/modprobe.d/i915.conf

```

Alternatively, you can add a kernel parameter. For example, if you are using GRUB, edit /etc/default/grub with

```
GRUB_CMDLINE_LINUX_DEFAULT="i915.enable_dpcd_backlight=1"

```

Don't forget to [update the grub configuration](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") to apply the changes.

**Note:** As of January 2020, setting the brightness is not flawless due to [this bug](https://gitlab.freedesktop.org/drm/intel/issues/510). Nevertheless, you still have some control.

### Audio

#### Audio pop on shutdown and startup

To work around the loud audio artifacts on startup/shutdown follow the guide for enabling the audio powersave: [Power management#Audio](/index.php/Power_management#Audio "Power management").

### Fingerprint

The 2.0 version of fprint [supports this device](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) after a firmware update.

To get fingerprint working right now:

**Note:** The Firmware for this is still in the testing phase at LVFS. Proceed with caution.

Install the following packages available on the [AUR](/index.php/AUR "AUR") :

*   [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/)
*   [fprintd-libfprint2](https://aur.archlinux.org/packages/fprintd-libfprint2/)

And setup [fwupd](/index.php/Fwupd "Fwupd")

The firmware updates currently require the newest version of fwupd and you must manually download the updates:

*   [https://fwupd.org/lvfs/devices/com.synaptics.prometheus.firmware](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.firmware)
*   [https://fwupd.org/lvfs/devices/com.synaptics.prometheus.config](https://fwupd.org/lvfs/devices/com.synaptics.prometheus.config)

using the latest version of the fwupd tool you should be able to run:

```
fwupdmgr get-devices

```

and see a "Prometheus" device in the list.

Install the firmware by running

```
fwupdmgr install *.cab

```

on each downloaded .cab file

**Note:** At this point, a reboot may be required

You should then be able to enroll your fingerprints with [Fprint#Configuration](/index.php/Fprint#Configuration "Fprint")

**Note:** For some reason, [the fprint.service can take some time to start. if fprint reports no devices, wait until fprint.service has completely stopped (it should become inactive in systemctl) To fix this, reset the fingerprint data in your bios settings](https://gitlab.freedesktop.org/libfprint/libfprint/issues/207)

### Card reader

The optional card reader that the Lenovo can install in your laptop is a Alcor Micro AU9560\. There are some tools you can use to test your card reader.

#### Installation

Install [ccid](https://www.archlinux.org/packages/?name=ccid) and [opensc](https://www.archlinux.org/packages/?name=opensc) from [official repositories](/index.php/Official_repositories "Official repositories"). Then, [Start](/index.php/Start "Start") and enable `pcscd.socket`.

```
pacman -S ccid opensc

systemctl enable pcscd
systemctl start pcscd

```

#### Testing

First, verify that your card reader can be found by pcsc:

```
opensc-tool --list-readers

```

Now, insert a smart card and run the following to verify that pcsc is able to read your card:

```
pcsc_scan

```

### Webcam

The webcam in this laptop is capable of "Windows Hello" which has a Linux version called [Howdy](/index.php/Howdy "Howdy"). The device you should use to configure howdy on this laptop is `/dev/video0`.

### Keyboard

#### Backlight

If you would like to enable the keyboard backlight, run:

```
echo 2 | tee /sys/class/leds/tpacpi::kbd_backlight/brightness

```

The "2" represents the brightness and can be any value between 0 and 2 (inclusive) for the laptop. For example, to turn off the keyboard backlight, you would run:

```
echo 0 | tee /sys/class/leds/tpacpi::kbd_backlight/brightness

```

### Touchpad

The touchpad works out-of-the-box with libinput. However, it will be very insensitive.

#### Acceleration

You can adjust acceleration using the command:

```
xinput set-prop 'SynPS/2 Synaptics TouchPad' 'libinput Accel Speed' 0.5

```

#### Two-Finger Right Click

Additionally, if you wish to disable right-clicking so that you use two finger click as your right click, run:

```
xinput set-prop 'SynPS/2 Synaptics TouchPad' 'libinput Click Method Enabled' 0 1    

```

#### Tap Clicking

If you would like for a tap on the touchpad to be registered as a click, use:

```
xinput set-prop 'SynPS/2 Synaptics TouchPad' 'libinput Tapping Enabled' 1

```

## Firmware

BIOS and firmware updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme-gen-2/downloads).

The latest BIOS version, v1.26, is highly recommended. All information on this page generally assumes the latest BIOS unless explicitly stated.

## Software

### Throttling fix

You will see a dmesg error that talks about CPU throttling. To fix this install [throttled](https://www.archlinux.org/packages/?name=throttled), then run

```
systemctl enable --now lenovo_fix.service

```

### CPU undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU").
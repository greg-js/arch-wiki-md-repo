Models covered: Lenovo IdeaPad Yoga 13

Sub-models options :

| Diffefenses | Value |
| CPU | Intel i3, i5, i7 |
| RAM | 4GB, 8GB |
| SSD | 128 GB, 256 GB |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overall Status](#Overall_Status)
*   [2 Display](#Display)
    *   [2.1 Backlight](#Backlight)
    *   [2.2 Touch Screen](#Touch_Screen)
*   [3 Keyboard](#Keyboard)
*   [4 Configaration](#Configaration)
    *   [4.1 Wireless](#Wireless)
    *   [4.2 Bluetooth](#Bluetooth)
*   [5 Hardware](#Hardware)
    *   [5.1 PCI devices](#PCI_devices)
*   [6 See also](#See_also)

## Overall Status

| Feature | Status |
| Boot Standard Kernel | OK |
| Detect SSD | OK |
| CPU Frequency Scaling | not tested |
| Hibernation | not tested |
| Sleep / Suspend | OK |
| Switch to External Screen | OK |
| Wireless/Bluetooth | with troubles |
| Wireless/Wifi | with troubles |
| Keyboard's Hotkeys | not all |
| Touch screen | works, but multitouch is a problem |
| Card reader | OK |

## Display

Works out of the box. Intel HD 4000

### Backlight

Control of brightness only works after suspend. After wake up, you can control brightness via f11 (less bright) and f12 (more bright). However, it is not brightnes problem, but keyboard buttons' problem. To control brightness while loaded from scratch, you can do the following command:

```
# cat 4882 > /sys/class/backlight/intel_backlight/brightness

```

This will change brightness value to 4882\. It is maximum brightness level. You can choose some other value, of course.

### Touch Screen

One touch works out of the box. But it works like a mouse.

## Keyboard

In addition to the keyboard, there are some extra Lenovo keys:

*   Volume + and - work as intended
*   Recovery button has no effect while computer is running
*   Screen rotation lock button simulates pressing Super + o
*   Windows button under the screen simulates pressing Super. Also gives haptic feedback, currently not controllable by software.

Most media buttons work out of the box:

*   Mute on F1 works
*   Vol- on F2 works
*   Vol+ on F3 works
*   Close on F4 works
*   Refresh on F5 works
*   Disable touchpad on F6 works, but also types the ± symbol
*   Airplane mode on F7 does not work
*   Choose application on F8 simulates pressing ctrl+alt+tab. The keys are pressed and instantly released, which (depending on your DE) may not have the intended effect.
*   Disable display on F9 works
*   Change video output on F10 simulates pressing ctrl+p
*   Brightness- on F11 works
*   Brightness+ on F12 works

## Configaration

### Wireless

See [Wireless network configuration#rtl8xxxu](/index.php/Wireless_network_configuration#rtl8xxxu "Wireless network configuration").

### Bluetooth

???

## Hardware

### PCI devices

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:04.0 Signal processing controller: Intel Corporation 3rd Gen Core Processor Thermal Subsystem (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation QS77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
00:1f.6 Signal processing controller: Intel Corporation 7 Series/C210 Series Chipset Family Thermal Management Controller (rev 04)

```

## See also

*   [https://wiki.debian.org/InstallingDebianOn/Lenovo/IdeaPad_Yoga_13_(Wheezy)](https://wiki.debian.org/InstallingDebianOn/Lenovo/IdeaPad_Yoga_13_(Wheezy))
*   [Lenovo IdeaPad Yoga 13](https://en.wikipedia.org/wiki/Lenovo_IdeaPad_Yoga_13 "wikipedia:Lenovo IdeaPad Yoga 13")
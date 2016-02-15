## Contents

*   [1 System Configuration](#System_Configuration)
    *   [1.1 Wifi](#Wifi)
    *   [1.2 Hybrid Graphics](#Hybrid_Graphics)
    *   [1.3 ClickPad](#ClickPad)
    *   [1.4 Suspend to ram](#Suspend_to_ram)
    *   [1.5 Keyboard](#Keyboard)
*   [2 Known issues](#Known_issues)
    *   [2.1 Clickpad](#Clickpad_2)
    *   [2.2 Audio](#Audio)

## System Configuration

### Wifi

The current driver for RTL8723BE PCIe Wireless Network Adapter can drop signals due to a power saving bug. This can be fixed with a quick command.

```
# iwconfig wlp3s0 rate 54M

```

### Hybrid Graphics

Out of the box, the integrated card is used while the radeon driver dynamically powers off the discrete card. For use of discrete card, see [PRIME](/index.php/PRIME "PRIME").

### ClickPad

The clickpad that is used is from Alps. Specifically, it uses Alps protocol 8 which has initial support in kernel 4.1\. While basic functionality works with kernels less than 4.1, there may be issues that occur with use in kernel less than 4.1.

For more advance features such as Vertical Edge Scrolling, see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). An interesting quirk that occurs is that in order to be able to use Vertical, or Horizontal, Edge Scrolling you have to enable Two Finger Scrolling. Setting only the Edge Scrolling option in xorg doesn't enable it.

### Suspend to ram

Works out of the box.

### Keyboard

**Fn and Ctrl keys** can be swapped in BIOS.

**Fn key** lock can be switched with **Fn + Esc**.

## Known issues

### Clickpad

**Issue (kernel < 4.1):**

After a certain amount of time used, the clickpad interrupts cease to be processed.

**Work-Around (Non-Permanent):**

Reload the "psmouse" kernel module when functionality ceases. Eventually it will cease up again requiring another reload.

```
# modprobe -r psmouse
# modprobe psmouse
```

### Audio

The audio won't work with Alsamixer alone, but it will with puleaudio-alsa.
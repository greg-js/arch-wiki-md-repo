The [ASUS Eee PC 1001P](https://www.asus.com/Laptops/Eee_PC_1001P_Seashell/) is a 10.1" laptop with an Intel Atom N450 processor.

## Contents

*   [1 Issues](#Issues)
    *   [1.1 ACPI and Intel KMS](#ACPI_and_Intel_KMS)
    *   [1.2 LCD Brightness](#LCD_Brightness)
    *   [1.3 Network Adapter](#Network_Adapter)
    *   [1.4 Touchpad](#Touchpad)

## Issues

### ACPI and Intel KMS

Screen goes black when [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") and ACPI is on. Brightness controls are not working.

**Solution**: Add the following to your kernel parameter list:

```
 acpi_osi=Linux acpi_backlight=vendor

```

**Alternate solution** (as those parameters break some fn keys):

*   With `acpi_osi=Linux` or both - mute, wireless and sleep keys do not work.
*   With `acpi_backlight=vendor`, brightness is not shifted, but control is totally disabled and brightness does not restore to max when AC power is restored.

So instead (as seen [here](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/631323/comments/2)):

```
# setpci -s 00:02.0 f4.b=ff

```

Where "00:02.0" is PCI address of video card (as reported by `lspci`). This shifts up min and max brightness levels on hardware level, without affecting anything in `/sys/class/backlight/...` or `/proc/acpi/video/VGA/LCDD/...`

Using `acpi_backlight=vendor` and changing `f4.b` register simultaneously will result in **even brighter**, blinding maximum backlight, while used separately the effect is roughly equal.

### LCD Brightness

See [Backlight](/index.php/Backlight "Backlight").

If brightness levels are erratic, download the latest BIOS from [Asus](http://support.asus.com)

If maximum brightness seems lower than it should be, see setpci solution above.

### Network Adapter

**Problem**: The network adapter for wired LAN does not or rarely get recognized (`lspci` and `ip addr` do not list it).

**Solution**: Add the following to your kernel parameter list:

```
 eeepc_laptop.hotplug_disabled=1

```

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

Two-Finger scrolling works with a `/etc/X11/xorg.conf` like this:

```
 Section "InputDevice"
  Identifier  "SynapticsTouchpad"
  Driver      "synaptics"
  Option      "AlwaysCore"        "true"  # send events to CorePointer
  #Option      "Device"            "/dev/input/mice"
  Option      "Device"            "/dev/psaux"
  Option      "Protocol"          "auto-dev"
  Option      "SHMConfig"         "false" # configurable at runtime? security risk
  Option      "LeftEdge"          "1700"  # x coord left
  Option      "RightEdge"         "5300"  # x coord right
  Option      "TopEdge"           "1700"  # y coord top
  Option      "BottomEdge"        "4200"  # y coord bottom
  Option      "FingerLow"         "25"    # pressure below this level triggers release
  Option      "FingerHigh"        "30"    # pressure above this level triggers touch
  Option      "MaxTapTime"        "180"   # max time in ms for detecting tap
  Option      "VertEdgeScroll"    "true"  # enable vertical scroll zone
  Option      "HorizEdgeScroll"   "true"  # enable horizontal scroll zone
  Option      "CornerCoasting"    "true"  # enable continuous scroll with finger in corner
  Option      "CoastingSpeed"     "0.30"  # corner coasting speed
  Option      "VertScrollDelta"   "100"   # edge-to-edge scroll distance of the vertical scroll
  Option      "HorizScrollDelta"  "100"   # edge-to-edge scroll distance of the horizontal scroll
  Option      "MinSpeed"          "0.10"  # speed factor for low pointer movement
  Option      "MaxSpeed"          "0.60"  # maximum speed factor for fast pointer movement
  Option      "AccelFactor"       "0.0020"    # acceleration factor for normal pointer movements
  Option      "VertTwoFingerScroll"   "true"  # vertical scroll anywhere with two fingers
  Option      "HorizTwoFingerScroll"  "true"  # horizontal scroll anywhere with two fingers
  Option      "TapButton1" "1"
  Option      "TapButton2" "2"
  Option      "TapButton3" "3"
 EndSection

```
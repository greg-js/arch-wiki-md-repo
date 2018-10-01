Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Backlight](#Backlight)
    *   [2.2 Fn Keys](#Fn_Keys)
    *   [2.3 Suspend](#Suspend)
    *   [2.4 Video Drivers](#Video_Drivers)
*   [3 Issues](#Issues)
    *   [3.1 DisplayPort Extenders](#DisplayPort_Extenders)
    *   [3.2 USB](#USB)

## Installation

Use the [Installation guide](/index.php/Installation_guide "Installation guide").

## Configuration

### Backlight

The following kernel options are needed for [ACPI/Backlight](/index.php/Backlight#Kernel_command-line_options "Backlight"):

```
acpi_osi=Linux acpi_backlight=vendor video.use_native_backlight=1

```

### Fn Keys

Function/Fn keys do not work without the FnLock on. To enable the FnLock, press `Fn+Esc`. The green light on the `Fn` key should turn on. Now you can use the `Fn` key like normal (*i.e.*, with FnLock on `Fn+F1` would equate to a `XF86AudioMute` to be handled by X/WM/whathaveyou).

### Suspend

Add the following kernel parameter in order to combat freeze/panic after suspend-to-ram:

```
i915.enable_rc6=0

```

### Video Drivers

Follow [Intel graphics](/index.php/Intel_graphics "Intel graphics") for installing the GPU driver. The T550 suffers from [Intel graphics#Loss of horizontal sync when switching TTYs](/index.php/Intel_graphics#Loss_of_horizontal_sync_when_switching_TTYs "Intel graphics"), but changing the [Graphics Acceleration to UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics") fixes it.

## Issues

### DisplayPort Extenders

The T550 is only able to drive three displays at once. If you are using a one-to-three DisplayPort adapter, you will need to disable the laptop display (`xrandr --output eDP1 --off`) in order to use three external displays. Expect a heavy delay (1-2 seconds) while adjusting displays via DisplayPort with `xrandr`.

### USB

Enabling "Always-On USB" in the BIOS seems to make the forward-most USB port on the right side of the laptop (the 'Charging Port') unusable in Linux - disabling this feature in BIOS re-enables the port.
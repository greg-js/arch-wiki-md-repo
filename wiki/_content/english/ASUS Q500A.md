<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Booting](#Booting)
    *   [1.1 Booting without Secure Boot](#Booting_without_Secure_Boot)
    *   [1.2 Booting with Secure Boot](#Booting_with_Secure_Boot)
*   [2 Display](#Display)
    *   [2.1 1920x1080 Models](#1920x1080_Models)
    *   [2.2 1366x768 Models](#1366x768_Models)
*   [3 See Also](#See_Also)

## Booting

Press Esc to get to the boot menu.

You are able to use [efibootmgr](/index.php/EFISTUB#efibootmgr "EFISTUB") for adding bootloaders or even [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels.

### Booting without Secure Boot

You are able to disable Secure Boot using the firmware setup menu.

### Booting with Secure Boot

**Warning:** Clearing the provided firmware keys will disable your ability to securely boot into Windows.

**Note:** For security reasons, you are unable to change the firmware keys using [EFI utilities](/index.php/Unified_Extensible_Firmware_Interface#Userspace_tools "Unified Extensible Firmware Interface"), even when Secure Boot is disabled.

Read [Secure Boot](/index.php/Secure_Boot "Secure Boot") for more information on how to generate firmware keys.

In order to change the firmware keys, you must enter the [UEFI](/index.php/UEFI "UEFI") firmware setup menu. Enable the Secure Boot option. There should be an option below the Secure Boot toggle for changing UEFI firmware keys.

The UEFI firmware will accept user-generated .auth keys.

## Display

Backlight is supported through [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight). Make sure you bind `Fn+F5` and `Fn+F6` to use `xbacklight`.

### 1920x1080 Models

DPI is not automatically detected on the 1920x1080 15.6 inch display. This might cause readability issues. The display is approximately 144 DPI.

An example [Xorg configuration file](/index.php/Xorg#Display_size_and_DPI "Xorg"):

 `/etc/X11/xorg.conf.d/90-monitor.conf` 
```
Section "Monitor"
        Identifier      "Monitor0"
        DisplaySize     338 190
EndSection

Section "Screen"
        Identifier      "Screen0"
        Monitor         "Monitor0"
EndSection
```

**Tip:** It is also a good idea to set the [xterm](/index.php/Xterm "Xterm") font size to 14-15 or higher if you are not going to use multiple displays.

### 1366x768 Models

The DPI is approximately 96 DPI which is the default Xorg setting.

## See Also

*   [Laptop](/index.php/Laptop "Laptop")
*   [Keyboard backlight#Asus](/index.php/Keyboard_backlight#Asus "Keyboard backlight")
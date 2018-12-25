This article assumes you have read [Keyboard input](/index.php/Keyboard_input "Keyboard input").

Many keyboards include some *special keys* (also called *hotkeys* or *multimedia keys*), which are supposed to execute an application or print special characters (not included in the standard national keymaps). [udev](/index.php/Udev "Udev") contains a large database of mappings specific to individual keyboards, so common keyboards usually work out of the box. If you have very recent or uncommon piece of hardware, you may need to adjust the mapping manually.

## Contents

*   [1 Laptops](#Laptops)
    *   [1.1 Apple MacBooks](#Apple_MacBooks)
    *   [1.2 Asus M series](#Asus_M_series)
    *   [1.3 Asus N56VJ (or possibly others)](#Asus_N56VJ_(or_possibly_others))
    *   [1.4 Lenovo T460p (or possibly others)](#Lenovo_T460p_(or_possibly_others))
*   [2 Gaming Keyboards](#Gaming_Keyboards)
    *   [2.1 Cooler Master CM Storm QuickFire TK](#Cooler_Master_CM_Storm_QuickFire_TK)
    *   [2.2 Corsair K series keyboards](#Corsair_K_series_keyboards)
    *   [2.3 Logitech G series G710 and 710+](#Logitech_G_series_G710_and_710+)
*   [3 See also](#See_also)

## Laptops

### Apple MacBooks

All the required information is available on the [Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard") dedicated article.

### Asus M series

In order to have control over the light sensor and the multimedia keys on your Asus machine, you should use the following command:

```
# echo 1 > /sys/devices/platform/asus_laptop/ls_switch

```

To have it run on boot create a [Systemd tmpfile](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/devices/platform/asus_laptop/ls_switch - - - - 1

```

**Note:** This may work also for other Asus notebook models.

### Asus N56VJ (or possibly others)

If most of your special keys do not work, try loading the asus-nb-wmi kernel module with

```
# modprobe asus-nb-wmi

```

then check xev again. If you combine this with the acpi_osi="!Windows 2012" boot option, you may get weird results in xev, so try not using it. If this did fix things, make sure to make the module load at boot with methods described in [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules").

### Lenovo T460p (or possibly others)

Out of the box, the backlight keys (on F5, F6) might not be available, even via the `/dev/input` interface. To fix this, follow [Backlight#Kernel command-line options](/index.php/Backlight#Kernel_command-line_options "Backlight").

## Gaming Keyboards

Gaming keyboards have some special features which may cause them to "misbehave" in Linux.

### Cooler Master CM Storm QuickFire TK

This keyboard has two features that could cause confusion in Linux: N-Key Rollover and the Win-Lock Key.

N-Key Rollover can [cause problems with the Function keys](https://bbs.archlinux.org/viewtopic.php?id=170877). To disable N-key rollover, hold down the FN lock key (next to right-ctrl) until it lights up, then hold Escape and press 6 to switch to 6-key rollover. Hold down the FN lock key to disable the Fn lock.

The Win-Lock Key completely disables the Super (Windows) keys. Simply press the FN lock key and F12 together to toggle Win-Lock on and off.

### Corsair K series keyboards

There is a winlock button on these keyboards that can disable the use of the Super (Windows) keys. This button is located at the top right of the keyboard next to the num and capslock buttons. CKB can be used to disable this functionality entirely preventing further locking. However, in a default state, simply pressing the button would enable the Super (Windows) keys again.

### Logitech G series G710 and 710+

This keyboard has a row of 6 programmable G keys. In order to use them as intended by Logitech, you need to install [sidewinderd](https://aur.archlinux.org/packages/sidewinderd/) and [start](/index.php/Start "Start") `sidewinderd.service`.

## See also

*   [Enabling Keyboard Multimedia Keys](http://wiki.linuxquestions.org/wiki/Configuring_keyboards#Enabling_Keyboard_Multimedia_Keys) - guide on LinuxQuestions wiki
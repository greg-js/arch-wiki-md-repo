## Contents

*   [1 Specs](#Specs)
*   [2 Install/Configuration](#Install.2FConfiguration)
    *   [2.1 Kernel](#Kernel)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Audio](#Audio)
    *   [2.4 Video](#Video)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Hotkeys](#Hotkeys)
    *   [2.8 Bluetooth](#Bluetooth)
    *   [2.9 Card reader](#Card_reader)
*   [3 See Also](#See_Also)

## Specs

| Model | HP Mini 210-1040BR |
| CPU | Intel Atom N450 (1.66 GHz, 512 KB L2 cache, 667 MHz FSB) [(Intel Atom in Wikipedia)](https://en.wikipedia.org/wiki/List_of_Intel_Atom_microprocessors#.22Pineview.22_.2845_nm.29 "wikipedia:List of Intel Atom microprocessors") |
| Architecture | x86_64 |
| Display | LED HD 10.1" (1024x600) |
| RAM | 2GB 667 |
| HDD | 250GB 7200RPM HDD (Seagate SATA II) [(Seagate)](http://www.seagate.com/ww/v/index.jsp?name=st9250410as-momentus-7200.4-sata-250-gb-hd&vgnextoid=e9f188b2ea9dd110VgnVCM100000f5ee0a0aRCRD&locale=en-US) |
| Battery | 6 cells, lasts about 6 hours with wireless NIC on |
| Optical drive | None |
| Graphics | Intel Graphics Media Accelerator HD (3150) (Embedded) [(Intel GMA in Wikipedia)](https://en.wikipedia.org/wiki/Intel_GMA#Specifications "wikipedia:Intel GMA") |
| LAN | Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E |
| Wireless/Bluetooth | Broadcom Corporation BCM4312 802.11b/g |
| Webcam | 0.3 Megapixel |
| Card reader | Secure Digital, MultiMedia, Memory Stick, Memory Stick Pro, or xD-Picture cards |
| Connections | 3 USB 2.0, 1 VGA, 1 Ethernet port |

## Install/Configuration

**ISO**: 2010-05 (64-bit) netinstall.

### Kernel

Arch stock kernel (x86_64), no issues in boot time, no need for additional parameters.

### Wireless

Follow the instructions in [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"), requiring to have [installed](/index.php/Install "Install") the packages [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) and [b43-fwcutter](https://www.archlinux.org/packages/?name=b43-fwcutter), or the proprietary driver [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl).

With it, your keyboard key for wireless network will work normally.

### Audio

[Install](/index.php/Install "Install") [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and run *alsaconf*. Then, launch *alsamixer* and mute the *Beep*, otherwise a weird beep when powering on and off. Save the configurations with `alsactl store`.

### Video

Work fine with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (did not test others) without additional configs. VGA output not tested.

### Touchpad

Working, 3 buttons. Upper right corner (middle-button), bottom right (right-button), vertical scroll (right edge) e horizontal scroll (bottom edge). [Install](/index.php/Install "Install") [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) for synaptics driver.

Configurations for the `/etc/X11/xorg.conf.d/10-synaptics.conf` file:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad catchall"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
        Option "RBCornerButton" "3"
        Option "RTCornerButton" "2"
EndSection

```

Comment/erase the touchpad section for the file `/etc/X11/xorg.conf.d/10-evdev.conf`. For more configurations, see [synaptics(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/synaptics.4)

### Webcam

Works, no additional configurations are necessary. Tested only in [cheese](https://www.archlinux.org/packages/?name=cheese) from [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

### Hotkeys

If you want to change the default configuration of "fn" key to enable the keys F1, F2, etc, simply change in BIOS and the second function will be the hotkeys of volume etc.

All works, except for:

*   F12/Wireless (does not turn off, except when using b43 driver), requiring *rfkill* from [util-linux](https://www.archlinux.org/packages/?name=util-linux) to turn it on.

To list network interfaces:

```
$ rfkill list

```

Disable wireless

```
# rfkill ublock 0
# rfkill ublock 2

```

Now you will be able to use wireless/Bluetooh again.

*   F4 switch mode between notebook display and VGA output. *Doesn't work.*

### Bluetooth

Working with [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl). See [Bluetooth](/index.php/Bluetooth "Bluetooth") for configurations, GUIs e etc.

### Card reader

*Not tested.*

## See Also

*   [HP Mini 210-1040BR support page in HP website](https://support.hp.com/br-pt/product/HP-Mini-210-PC-series/4075896/model/4126174)
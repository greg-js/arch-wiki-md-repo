# ASUS M51SN

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 CPU](#CPU)
    *   [1.2 Video](#Video)
        *   [1.2.1 Xorg](#Xorg)
    *   [1.3 Audio](#Audio)
    *   [1.4 Wi-Fi](#Wi-Fi)
    *   [1.5 Webcam](#Webcam)
    *   [1.6 Bluetooth](#Bluetooth)
    *   [1.7 Pointer](#Pointer)

## Configuration

### CPU

Works out of the box.

Follow this [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") guide to enable speed-stepping.

### Video

Video out works out of the box, and nvidia-settings detects the TV I used with it.

#### Xorg

Works out of the box.

Follow this guide: [NVIDIA](/index.php/NVIDIA "NVIDIA")

### Audio

Follow the official documentation: [ALSA](/index.php/ALSA "ALSA")

Need to tweak the options for the snd-hda-intel driver a little bit before it will work:

Add the following to /etc/modprobe.d/modprobe.conf [from here](http://gentoo-wiki.com/HARDWARE_Asus_M51Sn):

```
 options snd-hda-intel model=lenovo

```

### Wi-Fi

Use the included iwl4965 driver.

To enable wireless follow the official guide: [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

### Webcam

Works out of the box with the v4l2 driver.

### Bluetooth

Works out of the box.

### Pointer

Works out of the box.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_M51SN&oldid=297833](https://wiki.archlinux.org/index.php?title=ASUS_M51SN&oldid=297833)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")
# HP Mini 2140

The HP Mini 2140 is a 10.2" Netbook PC released in early 2009.

## Contents

*   [1 Hardware Compatibility](#Hardware_Compatibility)
    *   [1.1 Video](#Video)
    *   [1.2 Touchpad](#Touchpad)
    *   [1.3 Wireless](#Wireless)
    *   [1.4 Ethernet](#Ethernet)
    *   [1.5 Bluetooth](#Bluetooth)
    *   [1.6 CPU Scaling](#CPU_Scaling)
    *   [1.7 Webcam](#Webcam)
    *   [1.8 Sound](#Sound)
    *   [1.9 Suspend](#Suspend)
*   [2 See also](#See_also)

## Hardware Compatibility

### Video

Video is supported with "intel" driver, replace "vesa" in your xorg.conf with "intel". Kernel Mode-Setting is also possible.

### Touchpad

Works, you need to add "synaptics" support to your xorg.conf

### Wireless

This netbook uses the Broadcom BCM4312 wireless modem. This modem is not supported by either the b43 or STA drivers included as part of the Linux kernel. In order to be able to use wifi, the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") needs to be installed. Instructions for using [makepkg](/index.php/Makepkg "Makepkg") and [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") can be found on their respective wiki pages. Further information about [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") modem issues is covered in it's own wiki page.

After installing the driver, you need to have it loaded during boot, usually achieved by making the following edits to [/etc/rc.conf](/index.php//etc/rc.conf "/etc/rc.conf"):

 `rc.conf` 

```
...

MODULES=(lib80211 wl !b43 !ssb)

...

```

Any other modules listed to be loaded should remain as is and the above mentioned modules added to the list. The following may also work, but if not, use the above:

 `rc.conf` 

```
...

MODULES=(wl)

...

```

### Ethernet

Marvell Gigabit Ethernet - Use sky2 module.

### Bluetooth

Bluetooth - Works

### CPU Scaling

Works (acpi_cpufreq module)

### Webcam

Works (uvcvideo module)

### Sound

This netbook uses an Intel High Definition Audio AD1984A sound card. For general information on setting up sound see [Sound](/index.php/Sound "Sound") and [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"). To activate the sound card, follow the steps detailed on the ALSA page. Before running "_speaker-test -c 2_" as instructed, create a file `/etc/modprobe.d/alsa.conf` and enter the following into it:

 `alsa.conf` 

```
options snd-hda-intel model=laptop

```

Now reboot and you should hear sound when running "_speaker-test -c 2_". As per the ALSA page, save your mixer settings so that they are loaded with each boot.

### Suspend

*   Suspend To RAM - works via uswsusp
*   Suspend To Disk - works via uswsusp

## See also

*   [Wikipedia:HP Mini 2140](https://en.wikipedia.org/wiki/HP_Mini_2140 "wikipedia:HP Mini 2140")

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Mini_2140&oldid=376804](https://wiki.archlinux.org/index.php?title=HP_Mini_2140&oldid=376804)"
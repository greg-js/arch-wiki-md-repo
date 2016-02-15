| **Device** | **Status** | **Modules** |
| Video | Working | radeon |
| Wireless | Works after installing firmware | b43legacy/ipw2200 |
| Ethernet | Working | tg3 |
| Audio | Working | snd_ac97_codec |
| Trackpad | Working | xf86-input-synaptics |
| PCMCIA | Working | pcmcia-cs |
| Modem | Untested, probably works | hsfmodem |
| IRDA | Untested |  ? |

The Dell Latitude D600 was released on 3/12/2003\. Despite its age, it can prove to be quite a capable machine. With a couple exceptions, Linux support for the D600 is outstanding. Most of its components work automatically with Arch.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Video](#Video)
    *   [1.2 WiFi](#WiFi)
        *   [1.2.1 Intel PRO Wireless 2200](#Intel_PRO_Wireless_2200)
        *   [1.2.2 Broadcom BCM4306 rev.2](#Broadcom_BCM4306_rev.2)
    *   [1.3 Trackpad](#Trackpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 CPU powersaving](#CPU_powersaving)
    *   [2.2 Resuming from sleep](#Resuming_from_sleep)
*   [3 See also](#See_also)

## Configuration

### Video

Use the open source [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) driver. ATI dropped support for the Mobility Radeon 9000 in their proprietary Catalyst driver after version 8.28.8.

### WiFi

The D600 comes with either an Intel Pro Wireless 2200 or a Broadcom BCM4306 rev 2\. Both are supported natively.

#### Intel PRO Wireless 2200

The driver, ipw2200, is included in the kernel, so just install the [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw) package and it should work.

#### Broadcom BCM4306 rev.2

The b43legacy driver is included in the kernel, but unlike with the Intel card, the firmware license is not as permissive, so this process is a little more involved.

You'll need to download the following two firmware files:

*   [http://mirror2.openwrt.org/sources/broadcom-wl-4.150.10.5.tar.bz2](http://mirror2.openwrt.org/sources/broadcom-wl-4.150.10.5.tar.bz2)

*   [http://downloads.openwrt.org/sources/wl_apsta-3.130.20.0.o](http://downloads.openwrt.org/sources/wl_apsta-3.130.20.0.o)

And use [b43-fwcutter](https://www.archlinux.org/packages/?name=b43-fwcutter) to install the firmware files:

```
 $ tar xfvj broadcom-wl-4.150.10.5.tar.bz2
 # b43-fwcutter -w /lib/firmware wl_apsta-3.130.20.0.o
 # b43-fwcutter --unsupported -w /lib/firmware broadcom-wl-4.150.10.5/driver/wl_apsta_mimo.o

```

It would be bad if udev were to load the b43 driver, as it would conflict with b43legacy, so we'll need to blacklist it:

```
 # modprobe -r b43
 # echo "blacklist b43" >> /etc/modprobe.d/modprobe.conf

```

Finally, load the b43legacy driver:

```
 # modprobe b43legacy

```

### Trackpad

**Note:** This configuration may not be necessary on a modern system. Only follow these instructions if you find the trackpad is not working properly.

The trackpad and pointing stick are supported out-of-the-box, but to enable certain features, such as tap-to-click or edge scrolling, you'll need to write some Xorg configuration files.

Open `/etc/X11/xorg.conf.d/10-evdev.conf` and comment out every line in the section referring to touchpads. It should look like this when you're done:

```
 #Section "InputClass"
 #        Identifier "evdev touchpad catchall"
 #        MatchIsTouchpad "on"
 #        MatchDevicePath "/dev/input/event*"
 #        Driver "evdev"
 #EndSection

```

Next, you'll want to create a configuration file for your trackpad. The following is a good starting point.

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 

```
Section "InputClass"
   Driver      "synaptics"
   Identifier  "touchpad catchall"
   MatchDevicePath      "/dev/input/event*"
   MatchIsTouchpad      "on"
   Option "VertEdgeScroll" "on"
   Option "HorizEdgeScroll" "on"
   Option "TapButton1"  "1"
EndSection
```

After saving, reboot or restart X to apply the changes.

## Troubleshooting

### CPU powersaving

Some BIOS revisions don't work properly with acpi-cpufreq, likely due to the driver being buggy or incorrect DSDT tables. If you're experiencing problems, flash your BIOS to A16 (the latest version.)

If your D600 lacks a battery, the BIOS will forcibly downclock the CPU to 600MHz. To override this behavior, add `processor.ignore_ppc=1` to your kernel command-line.

### Resuming from sleep

There is a serious problem with KMS in the radeon driver that prevents normal resume from sleep mode with this laptop. [[1]](https://bugzilla.redhat.com/show_bug.cgi?id=531825) A quirk was [included in Linux 3.7](https://github.com/torvalds/linux/commit/45171002b01b2e2ec4f991eca81ffd8430fd0aec) that works around this issue automatically. If you're using an older kernel, either add `AGPMode=1` to your kernel command-line or set a primary password in the BIOS.

## See also

*   [Dell specifications brochure](http://www.dell.com/downloads/us/products/latit/d600_spec.pdf) (PDF)
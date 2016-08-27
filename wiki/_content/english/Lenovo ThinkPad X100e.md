## Contents

*   [1 Configuration Notes](#Configuration_Notes)
*   [2 Known Issues](#Known_Issues)
*   [3 Pre-install](#Pre-install)
*   [4 Wireless network device](#Wireless_network_device)

## Configuration Notes

This writeup was done based around a single x100e unit in two specific configurations (two different wifi cards, noted below):

*   2GB RAM
*   40GB SSD (Intel X25-V)
*   no WWAN card
*   First wifi card: Realtek 8172 (working on 2.4GHz b/g/n)
*   Second wifi card: Intel 5100 agn (working on 2.4GHz and 5Ghz b/g/n but ‘n’ connections drop after 5 minutes at time of this writeup - Sept. 2010 - Intel is working on a fix and there is a stopgap workaround to turn off ‘n’ functionality)

## Known Issues

Prior to kernel 2.6.35 there were several issues that plagued Linux installation on the x100e, including audio jack issues, wifi driver problems, display issues.

Some of these remain but for the most part a straight Arch install with kernel 2.6.35 or later on the x100e gets most things working almost immediately. Wifi continues to need love and care to bring up successfully, but once configured seems relatively reliable on both the Realtek wifi card.

Thinkwiki reports that wifi should work out of the box on kernels 2.6.32-22.33 but this did not seem to be the case as of 2.6.35\. Others may have better success with out of the box support and if so please note here.

If using the Intel 5100 agn wifi card (**must** be the lenovo part, FRU 43Y6517, as the BIOS detects non lenovo cards and will fail to boot) the card will work out of the box 2.6.35 or later (possibly eariler kernels as well, but those weren’t tested in this writeup).

Poweroff stalls unless clocksource-jiffies kernel parameter is set. There may be other work arounds or kernel parameters that would address this. noalpic-timer parameter also works but results in failure to bring CPUs up to high res mode (though I assume jiffies prevents high res mode too... out of my depth here and will be researching more).

Upon resume from suspend to ram, there are rare incidents of the filesystem not mounting properly and being set to a read-only state due to a journaling failure at the time of suspend. This seems to be addressed in a patch submitted for inclusion in kernel 2.6.36-rc4\. It is unclear whether this is related to the x100e alone, the Intel X25-V alone, or the specific combination of unit/drive. It is rare enough in the installation described here that no steps have been taken to patch ahead of expected availabilty of kernel 2.6.36.

## Pre-install

For this successful installation, the net install ISO (2010.05, current at time of initial writeup) was used. Many of the issues that the x100e faced with 2.6 kernels have been addressed as of kernel 2.6.35. There is no optical drive in the x100e so you’ll need to use a USB key or network boot. See [Putting installation media on a USB key](/index.php/Putting_installation_media_on_a_USB_key "Putting installation media on a USB key") for more details on booting off a USB key.

## Wireless network device

If you find that you can't make use of your wireless interface due to the following error:

```
# ip link set dev eth0 up
SIOCSIFFLAGS: Operation not possible due to RF-kill

```

And you see the interface as "Hard blocked" by rfkill:

```
# rfkill list
0: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: yes

```

Try these steps:

1.  Reboot.
2.  When the ThinkPad splash appears, press Enter, then F1 to access the BIOS configuration interface.
3.  Go to Config > Network.
4.  Enable "Wireless LAN and WiMAX Radios".
5.  Press F10 and save changes.

**Note:** remainder ot content to be added asap after I complete testing, formatting

Currently able to get power usage to under 12W with wifi *on*: [[1]](http://lh6.ggpht.com/_6-8K9TAVt1M/TMoagwDkKuI/AAAAAAAAAGk/q4EWZtotYUQ/s800/2010-10-28-175113_1366x768_scrot.png)
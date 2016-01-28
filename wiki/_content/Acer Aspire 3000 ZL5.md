# Acer Aspire 3000 ZL5

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Acer Aspire 3000 ZL5#](https://wiki.archlinux.org/index.php/Talk:Acer_Aspire_3000_ZL5))

This page provides a variety of configurations and optimizations for getting the Acer Aspire 3000 Series of Laptops running fast and smooth. Specifically for the **Acer Aspire 3000 ZL5** and based off the article for the [Acer Aspire 3003 WLMi](/index.php/Acer_Aspire_3003_WLMi "Acer Aspire 3003 WLMi")

## Contents

*   [1 Drivers](#Drivers)
*   [2 Internet](#Internet)
*   [3 Sound](#Sound)
*   [4 Xorg](#Xorg)
    *   [4.1 /home/user/.xinitrc](#.2Fhome.2Fuser.2F.xinitrc)
    *   [4.2 /etc/rc.local](#.2Fetc.2Frc.local)
*   [5 Kernel](#Kernel)
    *   [5.1 sisfb](#sisfb)
*   [6 Hardware](#Hardware)
    *   [6.1 lspci](#lspci)
    *   [6.2 lsusb](#lsusb)
*   [7 Related articles](#Related_articles)

## Drivers

Note that you need to install some drivers like [SiS](/index.php/SiS "SiS") manually by pacman and b43 module (Broadcom Wi-Fi driver) needs you to manually download and extract latest firmware using [b43fwcutter](/index.php/Wireless_network_configuration#b43 "Wireless network configuration").

## Internet

To get the wireless working you need the b43-fwcutter tool and firmware module: [Wireless network configuration#b43](/index.php/Wireless_network_configuration#b43 "Wireless network configuration")

What I did was download all the broadcom tarballs, extract them, and then ran this:

```
 $ find . -name '*.o' -type f | xargs -P1 -I{} sh -c 'echo "CUT {}";b43-fwcutter {}||echo "{} FAILED"'

```

See [here](/index.php/Wireless_network_configuration#Systemd_with_wpa_supplicant_and_static_IP "Wireless network configuration") for wireless configuration.

## Sound

Add this to `/etc/modprobe.d/modprobe.conf`

```
options snd-intel8x0 index=0

```

Add the packages [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss).

Unmute settings, then save.

```
 sudo amixer set Master 90% unmute
 sudo amixer set PCM 90% unmute
 sudo alsactl store

```

## Xorg

I use ratpoison because its lightning fast on my acer, and because I am a poweruser. If you have to use a GUI, go with xfce4\. KDE and gnome are outrageously slow on the acer.

### /home/user/.xinitrc

This is what the

```
 $ startx 

```

command uses.

```
xsetroot -solid black
#exec startxfce4
exec ratpoison

```

### /etc/rc.local

```
fbset -a -depth 32

```

## Kernel

If you want to compile a custom kernel that contains the modules used by your acer 3000 ZL5 for faster boots (among other benefits), see [Kernels#Compilation](/index.php/Kernels#Compilation "Kernels").

Here is the list of modules:

```
MODULES="sisfb ac battery button processor thermal cdrom agpgart amd64-agp sis-agp tpm_bios tpm tpm_tis k8temp i2c-sis96x i2c-core evdev pcspkr psmouse serio_raw mmc_core pci_hotplug shpchp rtc-cmos rtc-core rtc-lib ssb ac97_bus snd-mixer-oss snd-pcm-oss snd snd-page-alloc snd-pcm snd-timer snd-ac97-codec snd-intel8x0 snd-intel8x0m soundcore pata_sis scsi_mod mii sis900 pcmcia_core pcmcia rsrc_nonstatic yenta_socket usb-storage usbcore ehci-hcd ohci-hcd option usbserial sd_mod sr_mod st b43"

```

### sisfb

If you want to specify your own resolution using custom video driver, then you have to set _video_ option in [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). For example if you want to user resolution 1280x800 with 32-bit color depth at 76Hz (which is recommended for [Acer Aspire 3000](/index.php/Acer_Aspire_3000 "Acer Aspire 3000")) then you can use this option:

```
video=sisfb:mode:1280x800x32,rate:76

```

You can also play with memory consumption like this, but its not needed and it can cause some problems, if you do not know what are you doing:

```
video=sisfb:mode:1280x800x24,mem:12288,rate:76

```

## Hardware

The hardware of this laptop. Note that because the single hard-drive is so terrible compared to modern drives, I bought a PNY 4GB usb drive that I use for swap and tmp.

### lspci

```
00:00.0 Host bridge: Silicon Integrated Systems [SiS] 760/M760 Host (rev 03)
00:01.0 PCI bridge: Silicon Integrated Systems [SiS] SG86C202
00:02.0 ISA bridge: Silicon Integrated Systems [SiS] SiS963 [MuTIOL Media IO] (rev 25)
00:02.1 SMBus: Silicon Integrated Systems [SiS] SiS961/2 SMBus Controller
00:02.5 IDE interface: Silicon Integrated Systems [SiS] 5513 [IDE]
00:02.6 Modem: Silicon Integrated Systems [SiS] AC'97 Modem Controller (rev a0)
00:02.7 Multimedia audio controller: Silicon Integrated Systems [SiS] AC'97 Sound Controller (rev a0)
00:03.0 USB Controller: Silicon Integrated Systems [SiS] USB 1.1 Controller (rev 0f)
00:03.1 USB Controller: Silicon Integrated Systems [SiS] USB 1.1 Controller (rev 0f)
00:03.2 USB Controller: Silicon Integrated Systems [SiS] USB 2.0 Controller
00:04.0 Ethernet controller: Silicon Integrated Systems [SiS] SiS900 PCI Fast Ethernet (rev 91)
00:06.0 CardBus bridge: Texas Instruments PCI1410 PC card Cardbus Controller (rev 02)
00:0b.0 Network controller: Broadcom Corporation BCM4318 [AirForce One 54g] 802.11g Wireless LAN Controller (rev 02)
00:18.0 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] HyperTransport Technology Configuration
00:18.1 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Address Map
00:18.2 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] DRAM Controller
00:18.3 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Miscellaneous Control
01:00.0 VGA compatible controller: Silicon Integrated Systems [SiS] 661/741/760 PCI/AGP or 662/761Gx PCIE VGA Display Adapter

```

### lsusb

```
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 002: ID 154b:6545 PNY 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Related articles

*   [xf86-video-sis](/index.php/Xf86-video-sis "Xf86-video-sis")
*   [Wireless network configuration#b43](/index.php/Wireless_network_configuration#b43 "Wireless network configuration")
*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   Misc.
    *   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
    *   [Pm-utils](/index.php/Pm-utils "Pm-utils")
    *   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
    *   [Wacom Tablet](/index.php/Wacom_Tablet "Wacom Tablet")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_3000_ZL5&oldid=375952](https://wiki.archlinux.org/index.php?title=Acer_Aspire_3000_ZL5&oldid=375952)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")
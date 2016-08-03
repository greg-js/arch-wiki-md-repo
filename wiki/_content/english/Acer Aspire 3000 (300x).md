This page was created using knowledge collected while playing with Acer Aspire 3003 WLMi, but it will be probably compatible with other 300x Aspires. You can add your laptops to the compatibility list.

## Contents

*   [1 Compatibility list](#Compatibility_list)
*   [2 lspci](#lspci)
*   [3 /etc/X11/xorg.conf](#.2Fetc.2FX11.2Fxorg.conf)
*   [4 FBDev (SiSFB FrameBuffer)](#FBDev_.28SiSFB_FrameBuffer.29)
    *   [4.1 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
        *   [4.1.1 sisfb](#sisfb)
        *   [4.1.2 vga](#vga)
*   [5 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
*   [6 Related articles](#Related_articles)

## Compatibility list

*   [Acer Aspire 3003 WLMi](/index.php/Acer_Aspire_3003_WLMi "Acer Aspire 3003 WLMi")
*   [Acer Aspire 3000 ZL5](/index.php/Acer_Aspire_3000_ZL5 "Acer Aspire 3000 ZL5")

## lspci

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

## /etc/X11/xorg.conf

Before editing xorg.conf, you will need to install few drivers:

```
xf86-input-synaptics 0.99.3-1
   synaptics driver for notebook touchpads
xf86-video-sis 0.10.1-1 (xorg-video-drivers)
   X.org SiS video driver

```

You can use this xorg.conf to get your [Synaptics](/index.php/Synaptics "Synaptics") touchpad, USB mouse (or optionally [wacom](/index.php/Wacom "Wacom") tablet) and SiS graphical adapter with [sisctrl](/index.php/Sisctrl "Sisctrl") support working.

## FBDev (SiSFB FrameBuffer)

The `sisfb` module is no longer available as of [linux](https://www.archlinux.org/packages/?name=linux) 3.16, an alternative is to use [uvesafb](/index.php/Uvesafb "Uvesafb").

### /boot/grub/menu.lst

If you want have nicer screen resolutin in [framebuffer](/index.php/Framebuffer "Framebuffer") (textmode), then you have to add this configuration in [/boot/grub/menu.lst](/index.php/GRUB_Legacy "GRUB Legacy").

#### sisfb

If you want to specify your own resolution using custom video driver, then you have to replace *vga* option with *video* option. For example if you want to user resolution 1280x800 with 32-bit color depth at 76Hz (which is recommended for [Acer Aspire 3000](/index.php/Acer_Aspire_3000 "Acer Aspire 3000")) then you can use this option:

```
video=sisfb:mode:1280x800x32,rate:76

```

You can also play with memory consumption like this, but its not needed and it can cause some problems, if you do not know what are you doing:

```
video=sisfb:mode:1280x800x24,mem:12288,rate:76

```

#### vga

Basically you can append this option to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). This should work on any VGA compliant graphical adapter if it will have enough resources. But it will look ugly on widescreens, LCDs and similar, if they do not match the exact VGA resolution and it is better to use *video=...* option.

```
vga=791

```

If you do not like 791 mode, then you can use this:

```
vga=ask

```

And you will be informed about all modes compatible with your system configuration after reboot.

## /etc/mkinitcpio.conf

You can also add sisfb module to [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") by adding it to the /etc/mkinitcpio.conf and regenerating mkinitcpio. This will allow sisfb get loaded before filesystems are mounted, so you will get nice screen resolution much earlier than without it.

```
MODULES="pata_acpi pata_sis ata_generic scsi_mod **sisfb** ..."

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
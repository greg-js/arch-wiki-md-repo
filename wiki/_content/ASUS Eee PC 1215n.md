# ASUS Eee PC 1215n

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** This article mentions acpi_call and legacy Bumblebee (Discuss in [Talk:ASUS Eee PC 1215n#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_1215n))

**Notice: Kernel Panic Issue**

Kernels 3.10.6 - 3.10.10 cause kernel panics with the brcmsmac WiFi driver.

If you need one of these kernels, see [section](https://wiki.archlinux.org/index.php/ASUS_Eee_PC_1215n#brcmsmac_WiFi_driver_kernel_panic) below for work-around. Otherwise, update kernel to 3.11.1+

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Module**</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>atl1c [[1]](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx)</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>[brcmsmac](https://wiki.archlinux.org/index.php/Broadcom_wireless#brcmsmac.2Fbrcmfmac); [broadcom-wl](https://wiki.archlinux.org/index.php/Broadcom_wireless#broadcom-wl)</td>

</tr>

<tr>

<td>Video</td>

<td style="color:green">**Working**</td>

<td>[i915](https://www.archlinux.org/packages/extra/x86_64/xf86-video-intel/); [nvidia](https://wiki.archlinux.org/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA); [noveau](https://wiki.archlinux.org/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNouveau)</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>[snd-hda-intel](https://wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture)</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>[uvcvideo](https://wiki.archlinux.org/index.php/Webcam_Setup#linux-uvc)</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

<td>[usb-storage](https://wiki.archlinux.org/index.php/USB_Storage_Devices#Getting_a_kernel_that_supports_usb_storage)</td>

</tr>

<tr>

<td>Function Keys</td>

<td style="color:darkorange">**Partial**</td>

<td>eeepc-wmi [[2]](http://acpi4asus.sourceforge.net/)</td>

</tr>

</tbody>

</table>

This page includes general information regarding Asus EEE PC 1215n and related notes on installing/using Arch Linux on it.

## Contents

*   [1 System Specs](#System_Specs)
*   [2 Configuration](#Configuration)
    *   [2.1 Wireless and Bluetooth](#Wireless_and_Bluetooth)
    *   [2.2 Media- and FN-keys](#Media-_and_FN-keys)
    *   [2.3 nVidia ION 2 with Optimus](#nVidia_ION_2_with_Optimus)
    *   [2.4 Bumblebee Installation](#Bumblebee_Installation)
    *   [2.5 Relevant links](#Relevant_links)
*   [3 Problems](#Problems)
    *   [3.1 Nvidia graphic card](#Nvidia_graphic_card)
    *   [3.2 Bluetooth](#Bluetooth)
    *   [3.3 CPU power consumption](#CPU_power_consumption)
    *   [3.4 brcmsmac WiFi driver kernel panic](#brcmsmac_WiFi_driver_kernel_panic)

# System Specs

**CPU:** [Intel Atom D525](http://ark.intel.com/products/49490) (Dual Core; 1.8GHz; Codename [Pineview](https://en.wikipedia.org/wiki/List_of_Intel_Atom_microprocessors#.22Pineview.22_.2845_nm.29_2))

**RAM:** 1-2 x 1GB DDR3 SO-DIMM; 800 MHz (Maximum 4 GB)

**HDD:** 2.5" SATA2 250GB/320GB HDD; 5400 RPM (SATA2)

**GPU:** [nVidia ION2](http://www.nvidia.com/object/sff_ion.html) (GT218; 16 CUDA cores; 475 MHz; 256 MB DDR3) [[3]](https://en.wikipedia.org/wiki/Nvidia_Ion#Ion_2_.28next-generation_Nvidia_Ion.29) / Intel Graphics Media Accelerator on CPU die ([Intel GMA 3150](https://en.wikipedia.org/wiki/GMA_3150#GMA_3150); 400 MHz; 256 MB Max Shared Memory [[4]](http://www.intel.com/support/graphics/sb/CS-031160.htm?wapkw=gma+3150))

**North Bridge:** [NM10](http://ark.intel.com/products/47610/Intel-CG82NM10-PCH?q=nm10Intel) [[5]](http://www.intel.com/content/www/us/en/chipsets/internet-devices-chipsets/nm10-chipset.html)

**South Bridge:** [Intel ICH7-M](http://ark.intel.com/products/27680/Intel-82801GBM-IO-Controller) [[6]](https://en.wikipedia.org/wiki/List_of_Intel_chipsets#Southbridge_9xx_and_3.2F4_Series_chipsets)

**Audio:** [Intel High Definition Audio Controller](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio)

**Display:** 12.1" 1366x768 LED display

**Wireless:** [Broadcom BCM4313](http://www.broadcom.com/products/Wireless-LAN/802.11-Wireless-LAN-Solutions/BCM4313) 802.11b/g/n

**Ethernet:** [Qualcomm Atheros AR8152 v2.0](https://www.qca.qualcomm.com/media/product/product_98_file1.pdf) 10/100 Mb

**Bluetooth:** [BCM4313](http://www.broadcom.com/products/Wireless-LAN/802.11-Wireless-LAN-Solutions/BCM4313Broadcom) [Bluetooth v3.0 + HS](https://en.wikipedia.org/wiki/Bluetooth#Bluetooth_v3.0_.2B_HS)

**Webcam:** [Azurewave 0.3 MP (VGA)](http://www.azurewave.com/product_AM-VB002_1.asp)

**Expansion / Connectivity:** USB (3 x USB 2.0); Video Ports (VGA, HDMI); Audio Ports (Out 3.5 mm, In 3.5 mm); Card Reader (SD/ SDHC/ SDXC/ MMC)

**Extras:** Two USB 3.0 ports (optional)

# Configuration

## Wireless and Bluetooth

With the Kernel 3.0 and after, there is no need for any of the procedure below, because Wireless and Bluetooth work out of box.

## Media- and FN-keys

example ~/.[xbindkeysrc](/index.php/Xbindkeys "Xbindkeys") configuration

```
#Muter/UnMute
"amixer set "Master" toggle"
    m:0x0 + c:121
    XF86AudioMute 
#Volume up
"amixer set "Master" 5%+"
    m:0x0 + c:123
    XF86AudioRaiseVolume 
#Volume down
"amixer set "Master" 5%-"
    m:0x0 + c:122
    XF86AudioLowerVolume 
#MPD next song
"mpc next"
    m:0x0 + c:171
    XF86AudioNext 
#MPD stop playing
"mpc stop"
    m:0x0 + c:174
    XF86AudioStop 
#MPD prev song
"mpc prev"
    m:0x0 + c:173
    XF86AudioPrev 
#MPD pase/unpause
"mpc toggle"
    m:0x0 + c:172
    XF86AudioPlay 

```

## nVidia ION 2 with Optimus

nVidia Optimus is basically a software configuration that utilizes an Intel IGP + an nVidia GPU that writes to the Intel IGP's framebuffer. This is all done on the software side. The nVidia GPU is not wired to the outputs (VGA, HDMI etc.) At the time of this writing (September 27, 2010) Optimus on Linux sucks (i.e. doesn't work at all). You can still use the Intel IGP, but there is no way to access the discrete GPU. **DO NOT** try to install the nVidia binary driver, you have been warned.

Things are not that bad however. There is a kernel module called "acpi_call" which enables you to power off the nVidia GPU, hence you can significantly improve battery life.

David Airlie seems to be working on PRIME support (google it). You can also try "bumblebee-git" from the aur, which is the first working soloution to get the nvidia-card besides the intel gpu working.

Module auto-detection may load the nouveau module, but this sometimes seems to cause X to crash after boot-up, so try blacklisting this module if you encounter this problem.

There is a new project, called [Bumblebee](/index.php/Bumblebee "Bumblebee") (Transformers reference) that allows you to use the Nvidia Optimus ION2, but not natively, you have to instale it, and then call each program on the terminal with a command.

## Bumblebee Installation

Recently tested Bumblebee installation with kernel 3.1.8 and nvidia driver 290.10, which is installed as part of bumblebee package.

Install Bumblebee from AUR and follow instructions [here](https://wiki.archlinux.org/index.php/Bumblebee)

**Output from Optirun Test**

After installation, use

```
# glxgears 

```

and

```
# optirun glxgears

```

for comparison of integrated and dedicated GPU rendering (integrated GPU ~60 FPS)

The default compression method for the dedicated GPU is "proxy" (lower compression).

By changing the compression method while using Nvidia Optimus, the FPS can be increased or decreased, some results (by compression method and approx. FPS, respectively):

_proxy_ 220, _jpeg_ 340, _rgb_ 280, _yuv_ 330.

**Power Management**

On the wiki page, there are warnings about using power management with Bumblebee, essentially turning the card on and off using "acpi_call" module. Testing so far hasn't produced any problems....

The two files, cardon and cardoff, containing the commands used to control Nvidia Optimus need to be created in "/etc/bumblebee" for the 1215n with the following commands:

"/etc/bumblebee/cardon"

```
\_SB.PCI0.P0P4.GFX0._PS0

```

"/etc/bumblebee/cardoff"

```
\_SB.PCI0.P0P4.GFX0._DSM  {0xF8,0xD8,0x86,0xA4,0xDA,0x0B,0x1B,0x47,0xA7,0x2B,0x60,0x42,0xA6,0xB5,0xBE,0xE0} 0x100 0x1A {0x1,0x0,0x0,0x3}
\_SB.PCI0.P0P4.GFX0._PS3

```

## Relevant links

[http://airlied.livejournal.com/71734.html](http://airlied.livejournal.com/71734.html)

[https://launchpad.net/~hybrid-graphics-linux](https://launchpad.net/~hybrid-graphics-linux)

[http://linux-hybrid-graphics.blogspot.com/2010/02/howto-install-vgaswitcheroo-for-linux.html](http://linux-hybrid-graphics.blogspot.com/2010/02/howto-install-vgaswitcheroo-for-linux.html)

[https://aur.archlinux.org/packages.php?ID=48866](https://aur.archlinux.org/packages.php?ID=48866) (AUR for Bumblebee)

[https://github.com/MrMEEE/bumblebee/](https://github.com/MrMEEE/bumblebee/) (Bumblebee Project Git)

# Problems

## Nvidia graphic card

On the default kernel (2.6.36 branch) you cannot suspend system after disabling nvidia card with "acpi_call" module (nor after turning it on once you disabed it). This bug affects also turning off laptop (you'll have to manually power off laptop with power button). Using LTS 2.6.32 kernel ("kernel26-lts" package) allows you to safely power off/suspend netbook with disabled nvidia card (but with older kernel you won't be able to use some eee Fn hotkeys: disabling LCD/external output, volume controls, playback controls).

**Update (after a little testing):**

With the latest kernel running (3.0) and the "acpi_call" module installed from [AUR](https://aur.archlinux.org/packages.php?O=0&K=acpi_call&do_Search=Go), the suspend and hibernate scripts used by [pm-utils](https://wiki.archlinux.org/index.php/Pm-utils) will work (from commandline and in Gnome 3) as long as the acpi_call module is added to the suspend modules list used by the scripts.

Create a file `modules` in `/etc/pm/config.d` and paste in the line below.

```
 SUSPEND_MODULES="acpi_call"

```

## Bluetooth

Turning on bluetooth freezes the system. Need to do hard reset. No more info about this atm.

## CPU power consumption

There is a kernel parameter which must be added in linux 3.0 kernel to use energy saving feature of the intel driver: `pcie_aspm=force i915.i915_enable_rc6=1`, see [this thread](https://bbs.archlinux.org/viewtopic.php?id=125954).

## brcmsmac WiFi driver kernel panic

After connecting to an access point, the system's kernel will panic. To stop the connection, press your WiFi toggle button while booting Arch to temporarily disable your wireless. Your kernel can be patched to correct the issue until the kernel is officially updated. Use 'sudo pacman -U /path/to/kernel/patch.pkg.tar.xz' to install. [Patch](https://bbs.archlinux.org/viewtopic.php?pid=1314588#p1314588).

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1215n&oldid=383288](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1215n&oldid=383288)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")
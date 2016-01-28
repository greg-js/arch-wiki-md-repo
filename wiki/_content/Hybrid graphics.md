# Hybrid graphics

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_Hybrid-graphics is a concept involving two graphics cards on same computer, it was first designed to control power consumption in laptops and is extending to desktop computers as well_.

## Contents

*   [1 About Hybrid-graphics Technologies](#About_Hybrid-graphics_Technologies)
*   [2 The "Old" Hybrid Model (Basic Switching)](#The_.22Old.22_Hybrid_Model_.28Basic_Switching.29)
*   [3 The New Dynamic Switching Model](#The_New_Dynamic_Switching_Model)
    *   [3.1 Nvidia Optimus](#Nvidia_Optimus)
        *   [3.1.1 Current Problems](#Current_Problems)
        *   [3.1.2 Software Solutions So Far](#Software_Solutions_So_Far)
    *   [3.2 ATI Dynamic Switchable Graphics](#ATI_Dynamic_Switchable_Graphics)
        *   [3.2.1 Current Problems](#Current_Problems_2)
    *   [3.3 Fully Power Down Discrete GPU](#Fully_Power_Down_Discrete_GPU)
*   [4 See Also](#See_Also)

## About Hybrid-graphics Technologies

The laptop manufacturers developed new technologies involving two graphic cards in an single computer, enabling both high performance and power saving usages. This technology is well supported on Windows but it's still quite experimental with Linux distributions.

We call hybrid graphics a set of two graphic cards with different abilities and power consumptions. There are a variety of technologies and each manufacturer developed its own solution to this problem. Here we try to explain a little about each approach and models and some community solutions to the lack of GNU/Linux systems support.

## The "Old" Hybrid Model (Basic Switching)

This approach involves a two graphic card setup with a hardware multiplexer ([MUX](https://en.wikipedia.org/wiki/Multiplexer "wikipedia:Multiplexer")). It allows power save and low-end 3D rendering by using an Integrated Graphics Processor (IGP); or a major power consumption with 3D rendering performance using a Dedicated/Discrete Graphics Processor (DGP). This model makes the user choose (at boot time or at login time) within the two power/graphics profiles and is almost fixed through all the user session. The switch is done by a similar workflow:

*   Turn off the display
*   Turn on the DGP
*   Switch the multiplexer
*   Turn off the IGP
*   Turn on again the display

This switch is somewhat rough and adds some blinks and black screens in laptops that could do it "on the fly". Later approaches made the transition a little more user-friendly.

## The New Dynamic Switching Model

Most of the new Hybrid-graphics technologies involves two graphic cards as the basic switching but now the DGP and IGP are plugged to a framebuffer and there is no hardware multiplexer. The IGP is always on and the DGP is switched on/off when there is a need in power-save or performance-rendering. In most cases there is no way to use _only_ the DGP and all the switching and rendering is controlled by software. At startup, the Linux kernel starts using a video mode and setting up low-level graphic drivers which will be used by the applications. Most of the Linux distributions then use X.org to create a graphical environment. Finally, a few other softwares are launched, first a login manager and then a window manager, and so on. This hierarchical system has been designed to be used in most of cases on a single graphic card.

### Nvidia Optimus

[Nvidia Optimus Whitepaper](http://www.nvidia.com/object/LO_optimus_whitepapers.html)

#### Current Problems

*   Switching between cards when possible.
*   Switching on/off the discrete card.
*   Be able to use the discrete card for 3D render.
*   Be able to use both cards for 3D render (problem arised in [this post](https://bbs.archlinux.org/viewtopic.php?id=120994)).

#### Software Solutions So Far

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** missing links (Discuss in [Talk:Hybrid graphics#](https://wiki.archlinux.org/index.php/Talk:Hybrid_graphics))

*   asus_switcheroo -- a solution for Intel/Nvidia switching on ASUS and other laptops with a similar hardware mux -- by Alex Williamson
*   byo_switcheroo -- a solution to build your own handler (like acpi_call) to switch between cards with vga_switcheroo -- by Alex Williamson
*   [vga_switcheroo](https://wiki.gentoo.org/wiki/Hprofile#VGA) -- the original GPU switching solution primarily for Intel/ATI notebooks -- by David Airlie
*   acpi_call -- allows you to switch off discrete graphics card to improve battery life -- by Michal Kottman
*   [PRIME](/index.php/PRIME "PRIME") -- long-term Optimus solution in progress -- by David Airlie
*   [Bumblebee](/index.php/Bumblebee "Bumblebee") -- allows you to run specific programs on the discrete graphic card, inside of an X session using the integrated graphic card. Works on Nvidia Optimus cards -- by Martin Juhl
*   hybrid-windump -- dump window using Nvidia onto Intel display -- by Florian Berger and Joakim Gebart
*   [gpu-switch](https://aur.archlinux.org/packages/gpu-switch/)<sup><small>AUR</small></sup> -- gpu-switch is an application to switch between the integrated and dedicated GPU of dual-GPU MacBook Pro models for the next reboot
*   [systemd-vgaswitcheroo-units](https://aur.archlinux.org/packages/systemd-vgaswitcheroo-units/)<sup><small>AUR</small></sup> -- Disable discrete GPU at boot for AMD/NVIDIA & Intel dual GPU setups.

### ATI Dynamic Switchable Graphics

This is a new technology similar to the one of Nvidia as it uses no hardware multiplexer.

#### Current Problems

The Dynamic Switch needs Xorg support for the discrete videocard assigned for rendering to work [[1]](http://www.x.org/wiki/RadeonFeature#fnref-e188f8b793017f6c1c15025dc3d042a1e560915e). So, rendering on the discrete gpu will not work until the Xorg team adds support for it.

This means that with a muxless intel+ati design, you cannot use your discrete card by simply modprobing the radeon module.

As of now, there are 3 choices:

- Test and improve some virtualGL based program to make the switch, like the common-amd branch of bumblebee project. Check the [project repository](https://github.com/Bumblebee-Project/Bumblebee/issues/52) and [this](http://forums.gentoo.org/viewtopic-t-909802.html) useful post.

- Use the proprietary driver with powerxpress (a.k.a. pxp) support maintained by [Vi0l0](/index.php/AMD_Catalyst#Installing_from_the_AUR "AMD Catalyst") (remember to check for xorg compatibility).

### Fully Power Down Discrete GPU

You may want to turn off the high-performance graphics processor to save battery power, this can be done by installing the the [acpi_call-git](https://aur.archlinux.org/packages/acpi_call-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/acpi_call-git)]</sup> or [acpi_call-git-dkms](https://aur.archlinux.org/packages/acpi_call-git-dkms/)<sup><small>AUR</small></sup> package from the AUR.

Once installed load the kernel module:

```
modprobe acpi_call

```

With the kernel module loaded run the following (requires root):

```
turn_off_gpu.sh

```

This script will go through all the known data buses and attempt to turn them off. You will get an output similar to the following:

```
Trying \_SB.PCI0.P0P1.VGA._OFF: failed
Trying \_SB.PCI0.P0P2.VGA._OFF: failed
Trying \_SB_.PCI0.OVGA.ATPX: failed
Trying \_SB_.PCI0.OVGA.XTPX: failed
Trying \_SB.PCI0.P0P3.PEGP._OFF: failed
Trying \_SB.PCI0.P0P2.PEGP._OFF: failed
Trying \_SB.PCI0.P0P1.PEGP._OFF: failed
Trying \_SB.PCI0.MXR0.MXM0._OFF: failed
Trying \_SB.PCI0.PEG1.GFX0._OFF: failed
Trying \_SB.PCI0.PEG0.GFX0.DOFF: failed
Trying \_SB.PCI0.PEG1.GFX0.DOFF: failed
**Trying \_SB.PCI0.PEG0.PEGP._OFF: works!**
Trying \_SB.PCI0.XVR0.Z01I.DGOF: failed
Trying \_SB.PCI0.PEGR.GFX0._OFF: failed
Trying \_SB.PCI0.PEG.VID._OFF: failed
Trying \_SB.PCI0.PEG0.VID._OFF: failed
Trying \_SB.PCI0.P0P2.DGPU._OFF: failed
Trying \_SB.PCI0.P0P4.DGPU.DOFF: failed
Trying \_SB.PCI0.IXVE.IGPU.DGOF: failed
Trying \_SB.PCI0.RP00.VGA._PS3: failed
Trying \_SB.PCI0.RP00.VGA.P3MO: failed
Trying \_SB.PCI0.GFX0.DSM._T_0: failed
Trying \_SB.PCI0.LPC.EC.PUBS._OFF: failed
Trying \_SB.PCI0.P0P2.NVID._OFF: failed
Trying \_SB.PCI0.P0P2.VGA.PX02: failed
Trying \_SB_.PCI0.PEGP.DGFX._OFF: failed
Trying \_SB_.PCI0.VGA.PX02: failed

```

See the "works"? This means the script found a bus which your GPU sits on and it has now turned off the chip. To confirm this, your battery time remaining should have increased. Currently, the chip will turn back on with the next reboot to get around this we do the following:

**Note:** To turn the GPU back on just reboot.

Add the kernel module to the array of modules to load at boot:

 `/etc/modules-load.d/acpi_call.conf` 

```
#Load 'acpi_call.ko' at boot.

acpi_call
```

To turn off the GPU at boot we could just run the above script but honestly that is not very elegant so instead lets make use of systemd's tmpfiles.

 `/etc/tmpfiles.d/acpi_call.conf` 

```

w /proc/acpi/call - - - - \\_SB.PCI0.PEG0.PEGP._OFF
```

The above config will be loaded at boot by systemd. What it does is write the specific OFF signal to the `/proc/acpi/call` file. Obviously, replace the `\_SB.PCI0.PEG0.PEGP._OFF` with the one which works on your system (please note that you need to escape the backslash).

**Tip:** To prevent manual reinstalling the [acpi_call-git](https://aur.archlinux.org/packages/acpi_call-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/acpi_call-git)]</sup> package after each kernel upgrade, you can use the [acpi_call-git-dkms](https://aur.archlinux.org/packages/acpi_call-git-dkms/)<sup><small>AUR</small></sup> package.

## See Also

*   [Linux Hybrid-Graphics Blog](http://linux-hybrid-graphics.blogspot.com)
*   [Hybrid graphics on Linux Wiki](http://hybrid-graphics-linux.tuxfamily.org/index.php)
*   [Nvidia Optimus commercial presentation](http://www.nvidia.com/object/optimus_technology.html)
*   [ATI commercial presentation](http://www.amd.com/us/products/technologies/switchable-graphics/Pages/dynamic-switchable-graphics.aspx)
*   [Bumblebee](/index.php/Bumblebee "Bumblebee")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hybrid_graphics&oldid=412951](https://wiki.archlinux.org/index.php?title=Hybrid_graphics&oldid=412951)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Graphics](/index.php/Category:Graphics "Category:Graphics")

Hidden categories:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
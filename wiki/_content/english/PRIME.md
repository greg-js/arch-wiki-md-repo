PRIME is a technology used to manage hybrid graphics found on recent laptops ([Optimus for NVIDIA](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), AMD Dynamic Switchable Graphics for Radeon). **PRIME GPU offloading** and **Reverse PRIME** is an attempt to support muxless hybrid graphics in the Linux kernel.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Open Source Drivers](#Open_Source_Drivers)
    *   [1.2 Closed Source Drivers](#Closed_Source_Drivers)
*   [2 PRIME GPU offloading](#PRIME_GPU_offloading)
*   [3 Reverse PRIME](#Reverse_PRIME)
    *   [3.1 Discrete Card as Primary GPU](#Discrete_Card_as_Primary_GPU)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 XRandR specifies only 1 output provider](#XRandR_specifies_only_1_output_provider)
    *   [4.2 When an application is rendered with the discrete card, it only renders a black screen](#When_an_application_is_rendered_with_the_discrete_card.2C_it_only_renders_a_black_screen)
        *   [4.2.1 Black screen with GL-based compositors](#Black_screen_with_GL-based_compositors)
    *   [4.3 Kernel crash/oops when using PRIME and switching windows/workspaces](#Kernel_crash.2Foops_when_using_PRIME_and_switching_windows.2Fworkspaces)
    *   [4.4 Glitches/Ghosting synchronization problem on second monitor when using reverse PRIME](#Glitches.2FGhosting_synchronization_problem_on_second_monitor_when_using_reverse_PRIME)
*   [5 See also](#See_also)

## Installation

### Open Source Drivers

Remove any closed-source graphic drivers and replace them with the open source equivalent:

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)
*   [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)

Reboot and check the list of attached graphic drivers:

 `$ xrandr --listproviders` 
```
Providers: number : 2
Provider 0: id: 0x7d cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 3 outputs: 4 associated providers: 1 name:Intel
Provider 1: id: 0x56 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 6 outputs: 1 associated providers: 1 name:radeon

```

We can see that there are two graphic cards: Intel, the integrated card (id 0x7d), and Radeon, the discrete card (id 0x56), which should be used for GPU-intensive applications.

By default the Intel card is always used:

 `$ glxinfo | grep "OpenGL renderer"` 
```
OpenGL renderer string: Mesa DRI Intel(R) Ivybridge Mobile

```

### Closed Source Drivers

[Nvidia's documentation for their 364.15 Linux driver](http://us.download.nvidia.com/XFree86/Linux-x86/364.15/README/randr14.html) gives similar information to the [#Discrete Card as Primary GPU](#Discrete_Card_as_Primary_GPU) section of this article.

## PRIME GPU offloading

GPU-intensive applications should be rendered on the more powerful discrete card. The command `xrandr --setprovideroffloadsink provider sink` can be used to make a render offload provider send its output to the sink provider (the provider which has a display connected). The provider and sink identifiers can be numeric (0x7d, 0x56) or a case-sensitive name (Intel, radeon).

Example:

```
$ xrandr --setprovideroffloadsink radeon Intel

```

Now, you can use your discrete card for the applications who need it the most (for example games, 3D modellers...) by prepending the `DRI_PRIME=1` environment variable:

 `$ DRI_PRIME=1 glxinfo | grep "OpenGL renderer"` 
```
OpenGL renderer string: Gallium 0.4 on AMD TURKS

```

Other applications will still use the less power-hungry integrated card. These settings are lost once the X server restarts, you may want to make a script and auto-run it at the startup of your desktop environment (alternatively, put it in `/etc/X11/xinit/xinitrc.d/`). This may reduce your battery life and increase heat though.

## Reverse PRIME

If the second GPU has outputs that are not accessible by the primary GPU, you can use **Reverse PRIME** to make use of them. This will involve using the primary GPU to render the images, and then pass them off to the secondary GPU.

In the scenario above, you would do

```
$ xrandr --setprovideroutputsource radeon Intel

```

When this is done, the discrete card's outputs should be available in xrandr, and you could do something like:

```
$ xrandr --output HDMI-1 --auto --above LVDS1

```

### Discrete Card as Primary GPU

Imagine following scenario: The LVDS1 (internal laptop screen) and VGA outputs are both only accessible through the integrated Intel GPU. The HDMI and Display Port outputs are attached to the discrete NVIDIA card. It is possible to use all four outputs by making use of the **Reverse PRIME** technology as described above. However the performance might be slow, because all the rendering for all outputs is done by the integrated Intel card. To improve this situation it is possible to do the rendering by the discrete NVIDIA card, which then copies the framebuffers for the LVDS1 and VGA outputs to the Intel card.

Create the following Xorg configuration:

 `/etc/X11/xorg.conf.d/10-gpu.conf` 
```
# Discrete Card as Primary GPU

Section "ServerLayout"
    Identifier "layout"
    Screen 0 "nouveau"
    Inactive "intel"
EndSection

Section "Device"
    Identifier  "nouveau"
    Driver      "nouveau"
    BusID       "PCI:x:x:x" # Sample: "PCI:1:0:0"
EndSection

Section "Screen"
    Identifier "nouveau"
    Device "nouveau"
EndSection

Section "Device"
    Identifier  "intel"
    Driver      "intel"
    BusID       "PCI:x:x:x"  # Sample: "PCI:0:2:0"
EndSection

Section "Screen"
    Identifier "intel"
    Device "intel"
EndSection

```

Restart Xorg. The discrete NVIDIA card should be used now. The HDMI and Display Port outputs are the main outputs. The LVDS1 and VGA outputs are off. To enable them run:

```
$ xrandr --setprovideroutputsource Intel nouveau

```

The discrete card's outputs should be available now in xrandr.

## Troubleshooting

### XRandR specifies only 1 output provider

Delete/move /etc/X11/xorg.conf file and any other files relating to GPUs in /etc/X11/xorg.conf.d/. Restart the X server after this change.

If the video driver is blacklisted in `/etc/modprobe.d/`, load the module and restart X. This may be the case if you use the bbswitch module for Nvidia GPUs.

Since kernel version 3.19.0 the nouveau kernel module cannot be loaded under certain circumstances. Dmesg will throw an error with `invalid rom content`. The bug as has been patched, but hasnt yet reached mainline. [Freedesktop Bug Thread](https://bugs.freedesktop.org/show_bug.cgi?id=89047) In the meantime, applying the patches to a custom kernel before compiling seems to be the only fix.

### When an application is rendered with the discrete card, it only renders a black screen

In some cases PRIME needs a composition manager to properly work. If your window manager doesn’t do compositing, you can use [xcompmgr](/index.php/Xcompmgr "Xcompmgr") on top of it.

If you use Xfce, you can go to Menu->Settings->Window Manager Tweaks->Compositor and enable compositing, then try again your application.

#### Black screen with GL-based compositors

Currently there are issues with GL-based compositors and PRIME offloading. While Xrender-based compositors (xcompmgr, xfwm, compton's default backend, cairo-compmgr, and a few others) will work without issue, GL-based compositors (Mutter/muffin, Compiz, compton with GLX backend, Kwin's OpenGL backend, etc) will initially show a black screen, as if there was no compositor running. While you can force an image to appear by resizing the offloaded window, this is not a practical solution as it will not work for things such as full screen Wine applications. This means that desktop environments such as GNOME3 and Cinnamon have issues with using PRIME offloading.

Additionally if you are using an Intel IGP you might be able to fix the GL Compositing issue by running the IGP as UXA instead of SNA, however this may cause issues with the offloading process (ie, xrandr --listproviders may not list the discrete GPU).

For details see [FDO Bug #69101.](https://bugs.freedesktop.org/show_bug.cgi?id=69101)

### Kernel crash/oops when using PRIME and switching windows/workspaces

Note: this has been tested on a system with Intel+AMD

Using DRI3 WITH a config file for the integrated card seems to fix this issue.

To enable DRI3, you need to recompile mesa with --enable-dri3 in the configure flags[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1494777#p1494777) and create a config for the integrated card adding the DRI3 option:

```
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
    Option "DRI" "3"
EndSection

```

After this you can use DRI_PRIME=1 WITHOUT having to run `xrandr --setprovideroffloadsink radeon Intel` as DRI3 will take care of the offloading.

### Glitches/Ghosting synchronization problem on second monitor when using reverse PRIME

This problem users when not using a [composite manager](/index.php/Composite_manager "Composite manager"), such as with [i3](/index.php/I3 "I3"). [[2]](https://bugs.freedesktop.org/show_bug.cgi?id=75579)

If you experience this problem under Gnome, then a possible fix is to set some environment variables in `/etc/environment` [[3]](https://bbs.archlinux.org/viewtopic.php?id=177925)

```
CLUTTER_PAINT=disable-clipped-redraws:disable-culling
CLUTTER_VBLANK=True

```

## See also

*   [Nouveau Optimus](https://wiki.freedesktop.org/nouveau/Optimus/)
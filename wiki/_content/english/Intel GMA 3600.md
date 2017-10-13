Related articles

*   [Intel graphics](/index.php/Intel_graphics "Intel graphics")
*   [Xorg](/index.php/Xorg "Xorg")

The **Intel GMA 3600** series is a family of integrated video adapters based on the PowerVR SGX 545 graphics core. It is used in the Atom N2600, N2800 and D2550.

The Linux kernel has support since version 3.5.

## Contents

*   [1 Xorg driver](#Xorg_driver)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Blank screen after resume](#Blank_screen_after_resume)
    *   [2.2 Playing video](#Playing_video)
*   [3 See also](#See_also)

## Xorg driver

At the moment there is no accelerated driver for Xorg Server, but some support is available using the Xorg modesetting driver provided by package [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

 `/etc/X11/xorg.conf.d/20-gpudriver.conf` 
```
Section "Device"
    Identifier "Intel GMA3600"
    Driver     "modesetting"
EndSection

```

The modesetting driver allows disabling/enabling LVDS, VGA, etc. ports and changing resolution using xrandr.

The following can be used to disable LVDS and force enable VGA if needed.

 `/etc/X11/xorg.conf.d/20-gpudriver.conf` 
```
Section "Device"
    Identifier "Intel GMA3600"
    Driver     "modesetting"
    Option     "Monitor-LVDS-0" "Ignore"
    Option     "Monitor-VGA-0" "Monitor"
EndSection

Section "Monitor"
    Identifier "Ignore"
    Option     "Ignore"
EndSection

Section "Monitor"
    Identifier "Monitor"
    Option     "Enable"
EndSection

```

## Troubleshooting

### Blank screen after resume

If after resume you got a blank screen try the following

```
# touch /etc/pm/sleep.d/99video

```

### Playing video

It is unable to utilize whole chip power and play fullHD movies using graphics acceleration. As workaround you could utilize the maximum power of your Atom CPU to decode video:

```
mplayer -lavdopts threads=4 -fs myvideo.avi

```

## See also

*   [https://www.change.org/en-GB/petitions/intel-listen-to-the-community-and-develop-gma3600-drivers-for-linux](https://www.change.org/en-GB/petitions/intel-listen-to-the-community-and-develop-gma3600-drivers-for-linux)
*   [http://ubuntuforums.org/showthread.php?t=1953734](http://ubuntuforums.org/showthread.php?t=1953734)
*   [http://communities.intel.com/message/158477](http://communities.intel.com/message/158477)
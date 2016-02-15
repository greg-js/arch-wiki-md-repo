Another work in Progress - by PhrakTure I am currently running Arch on this laptop, 98% problem free... and no I have not yet configured the media card reader, as I have no use for it. If anyone really has a problem, let me know (PM from forums).

## Contents

*   [1 Modules](#Modules)
*   [2 Other](#Other)
*   [3 Unusual settings](#Unusual_settings)
*   [4 See also](#See_also)

## Modules

*   Ethernet: 8139too
*   Wireless: ndiswrapper using BCMWL5A [[pkg](http://phrakture.freelinuxhost.com/ndiswrapper-bcmwl5a-0.2-1.pkg.tar.gz)] [[PKGBUILD](http://phrakture.freelinuxhost.com/pkgbuilds/PKGBUILD.ndiswrapper-bcmwl5a)]
*   Audio: snd-intel-8x0 / snd-pcm-oss
*   Video: nvidia [[1]](http://www.nvidia.com)

## Other

*   Composite: works, but gets goofy with flash animations in Firefox

## Unusual settings

*   Video mode detected wrong

	Add the following to the device (nvidia driver) section in xorg.conf

	 `Option "IgnoreEDID" "True"` 

*   And the following line to the "Monitor" section
     `Modeline "1440x900"  106.47  1440 1520 1672 1904  900 901 904 932  -hsync +vsync` 

The following Display Subsection (in the Screen Section) will allow you to use the display's native viewing mode.

```
Subsection "Display"
  Depth       24
  Modes "1440x900"
  Virtual 1440 900
EndSubsection

```

## See also

*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: Hewlett-Packard - HP](http://tuxmobil.org/hp.html).
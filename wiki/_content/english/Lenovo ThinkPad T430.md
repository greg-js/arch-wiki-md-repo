The Lenovo ThinkPad T430 is a durable, business-style laptop that was made in 2012 with a mobile Intel i3, i5, or i7 CPU, and Intel Graphics. Some models have an NVIDIA NVS 5400M GPU w/[NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")™ Technology. You can view more information about the laptop at [ThinkWiki](https://www.thinkwiki.org/wiki/Category:T430).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Power Management](#Power_Management)
    *   [1.1 Method 1 (TLP only)](#Method_1_(TLP_only))
    *   [1.2 Method 1 (powertop & TLP)](#Method_1_(powertop_&_TLP))
*   [2 HiDPI Displays](#HiDPI_Displays)
*   [3 Adjust trackpoint drift](#Adjust_trackpoint_drift)

## Power Management

### Method 1 (TLP only)

[Install](/index.php/Install "Install") and enable the [tlp](https://www.archlinux.org/packages/?name=tlp) package. Installing the optional dependencies may help provide additional power saving.

Refer to [Wiki:TLP](https://wiki.archlinux.org/index.php/TLP#rdw) for details for configuration and optimization.

### Method 1 (powertop & TLP)

[Install](/index.php/Install "Install") the [powertop](https://www.archlinux.org/packages/?name=powertop) package.

Refer to [Wiki:powertop](https://wiki.archlinux.org/index.php/Powertop#rdw) for details on configuration and optimization.

## HiDPI Displays

HiDPI (High Dots Per Inch) displays, also known by Apple's "Retina Display" marketing name, are screens with a high resolution in a relatively small format. They are mostly found in high-end laptops and monitors. Not all software behaves well in high-resolution mode yet. Here are listed most common tweaks which make work on a HiDPI screen more pleasant. For configuration and usage with HiDPI displays, refer to the [HiDPI configuration](https://wiki.archlinux.org/index.php/HiDPI#Applications#rdw)

## Adjust trackpoint drift

When the trackpoint does not move for 0.5 seconds, it re-calibrates that point as zero. Hence, if you hold the trackpoint in the same place for more than 0.5 seconds (for instance while scrolling), the trackpoint re-calibrates that position as zero. When you leave the trackpoint, it re-calibrates again, leading to the infamous trackpoint drift.

On Linux, this value can be changed from 0.5 seconds to anything you like. For instance, to set it to 2.5 seconds: `echo 25 >/sys/devices/platform/i8042/serio1/serio2/drift_time`
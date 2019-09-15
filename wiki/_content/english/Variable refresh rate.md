Related articles

*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Xorg](/index.php/Xorg "Xorg")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [AMDGPU](/index.php/AMDGPU "AMDGPU")

[Variable refresh rate](https://en.wikipedia.org/wiki/Variable_refresh_rate "wikipedia:Variable refresh rate") (VRR), also referred to as adaptive sync, allows the monitor to adjust its refresh rate to the output signal. This allows for games to eliminate screen tearing with less of the usual downsides of Vsync (such as stuttering). For a comprehensive look at VRR see [PC Gaming Wiki](https://pcgamingwiki.com/wiki/Glossary:Variable_refresh_rate_(VRR)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Configuration](#Configuration)
    *   [2.1 Enable on AMDGPU](#Enable_on_AMDGPU)
        *   [2.1.1 Using a Xorg conf file](#Using_a_Xorg_conf_file)
    *   [2.2 Enable on NVIDIA](#Enable_on_NVIDIA)
        *   [2.2.1 Using a Xorg conf file](#Using_a_Xorg_conf_file_2)
        *   [2.2.2 Via nvidia-settings](#Via_nvidia-settings)
*   [3 Change Freesync Range of Monitor](#Change_Freesync_Range_of_Monitor)
    *   [3.1 Editing the EDID File](#Editing_the_EDID_File)
*   [4 Tips and Tricks](#Tips_and_Tricks)
    *   [4.1 Remove applications from Blacklist](#Remove_applications_from_Blacklist)
*   [5 Limitations](#Limitations)

## Overview

There are multiple implementations of VRR:

*   FreeSync is AMD's implementation of VESA's VRR standard, and the phrases are often used interchangeably. FreeSync branded monitors should be compatible with all VESA compatible drivers.

*   Gsync is NVIDIA's proprietary hardware and software implementation of VRR.

*   Intel plans on implementing VESA's standard in their upcoming 10th Gen. [[1]](https://techreport.com/news/34053/intel-reiterates-plans-to-support-vesa-adaptive-sync-in-its-gpus/)

**VRR compatibility and implimentations**

| Driver | VESA | Gsync |
| [AMDGPU](/index.php/AMDGPU "AMDGPU") | FreeSync | No |
| [Intel](/index.php/Intel "Intel") | Planned | No |
| [Nouveau](/index.php/Nouveau "Nouveau") | Not Supported | Not Supported |
| [NVIDIA](/index.php/NVIDIA "NVIDIA") | Gsync Compatible | Gsync |

**Note:** Nvidia GPUs older than their 10 series do not support "Gsync Compatible" monitors.

## Configuration

### Enable on AMDGPU

#### Using a Xorg conf file

Add the line to your [.conf](/index.php/Xorg#Using_.conf_files "Xorg") file.

```
Option "VariableRefresh" "true"

```

For more information on Xorg configuration see the [AMDGPU](/index.php/AMDGPU#Xorg_configuration "AMDGPU") page.

Verify *vrr_capable* is set to *1* using [xrandr](/index.php/Xrandr "Xrandr"):

 `$ xrandr --props` 
```
vrr_capable: 1
        range: (0, 1)

```

### Enable on NVIDIA

#### Using a Xorg conf file

**Note:** This section needs info.

#### Via nvidia-settings

Gsync monitors should automatically be enabled. To enable Gsync compatible monitors do the following:

*   In [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) go to the "X Server Display Configuration" page, then under the Advanced button is the option to "Allow G-SYNC on monitor not validated as G-SYNC Compatible". Then click apply.
*   Now, under OpenGL settings, check "Allow Gsync/Gsync Compatible."

**Tip:** In the same menu, you can check the "show Gsync indicator" option to display an indicator that Gsync is working in the top right corner.

## Change Freesync Range of Monitor

Freesync monitors usually have a limited range for VRR that are much lower than their max refresh rate. It should be possible to overclock the monitor to change the Freesync range.

**Warning:** Overclocking your monitor may cause it to run hot and possibly cause harm. Proceed at your own risk.

#### Editing the EDID File

External Display Identification Data (EDID) stores driver information about your monitor. By default, this file is sent by your monitor and read on connect. You will need to extract this file using something like [read-edid](https://www.archlinux.org/packages/?name=read-edid) or [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings).

You can edit this file with [wxedid](https://aur.archlinux.org/packages/wxedid/)

You may follow one of the guides of people changing the freesync range on Windows: [[2]](https://www.reddit.com/r/Amd/comments/5iux1q/updated_tutorial_on_increasing_and_decreasing/)[[3]](https://wccftech.com/amd-freesync-hack-expands-refresh-rate-range/)

Process of overclocking on Linux: [[4]](https://forum.level1techs.com/t/overclock-your-monitor-with-nvidia-windows-and-linux/109323)

Make a Xorg [.conf](/index.php/Xorg#Using_.conf_files "Xorg") file for your monitor and add a path to the custom EDID file you have edited. See [xrandr](/index.php/Xrandr "Xrandr") to find find out the other information about your monitor.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Screen"
    Identifier "Screen0"
    Device "nvidia" # e.g. Radeon, nvidia
    Monitor "DP1"
    Option “CustomEDID” “MONITOR:/home/USER/Desktop/modified-edid.bin”
EndSection
```

**Note:** Edit “MONITOR” in the fileto be the correct display ID. You can get the display ID with the `xrandr –query` command.

## Tips and Tricks

### Remove applications from Blacklist

Mesa has a list of blacklisted applications to avoid unexpected behavior, you can edit this blacklist here:

```
/usr/share/drirc.d/00-mesa-defaults.conf

```

## Limitations

*   For Gsync, the monitor must be plugged in via display port. For Freesync, some monitors with the HDMI 2.1 specification is supported otherwise display port will be needed.
*   Only one monitor may be used at a time with Gsync and possibly Freesync.
*   Some compositors may need to be disabled before the OpenGl/Vulkan program is started.
*   Mesa [blacklists](#Remove_applications_from_Blacklist) many applications including video players.
*   Although tearing is much less of an issue at higher refresh rates, most Freesync monitors only have a range up to 90Hz see [Change Freesync range of Monitor](#Change_Freesync_Range_of_Monitor)
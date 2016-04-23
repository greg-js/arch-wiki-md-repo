Owners of **AMD** (previously **ATI**) video cards have a choice between [proprietary driver](/index.php/AMD_Catalyst "AMD Catalyst") ([catalyst](https://aur.archlinux.org/packages/catalyst/)) and the open source drivers (**ATI** for older or [AMDGPU](/index.php/AMDGPU "AMDGPU") for newer cards). This article covers the **ATI**/[Radeon](https://wiki.freedesktop.org/xorg/radeon/) open source driver for older cards.

The open source driver is *on par* performance-wise with the proprietary driver for many cards. (See this [benchmark](http://www.phoronix.com/scan.php?page=article&item=radeonsi-cat-wow&num=1).) It also has good dual-head support but worse TV-out support. Newer cards support might be lagging behind Catalyst.

If unsure, try the open source driver first, it will suit most needs and is generally less problematic. (See the [feature matrix](http://www.x.org/wiki/RadeonFeature) to know what is supported for the GPU.)

## Contents

*   [1 Naming conventions](#Naming_conventions)
*   [2 Overview](#Overview)
*   [3 Installation](#Installation)
*   [4 Configuration](#Configuration)
*   [5 Loading](#Loading)
    *   [5.1 Enable early KMS](#Enable_early_KMS)
*   [6 Performance tuning](#Performance_tuning)
    *   [6.1 Enabling video acceleration](#Enabling_video_acceleration)
    *   [6.2 Driver options](#Driver_options)
    *   [6.3 Kernel parameters](#Kernel_parameters)
        *   [6.3.1 Deactivating PCI-E 2.0](#Deactivating_PCI-E_2.0)
    *   [6.4 Gallium Heads-Up Display](#Gallium_Heads-Up_Display)
*   [7 Hybrid graphics/AMD Dynamic Switchable Graphics](#Hybrid_graphics.2FAMD_Dynamic_Switchable_Graphics)
*   [8 Powersaving](#Powersaving)
    *   [8.1 Dynamic power management](#Dynamic_power_management)
    *   [8.2 Old methods](#Old_methods)
        *   [8.2.1 Dynamic frequency switching](#Dynamic_frequency_switching)
        *   [8.2.2 Profile-based frequency switching](#Profile-based_frequency_switching)
        *   [8.2.3 Persistent configuration](#Persistent_configuration)
        *   [8.2.4 Graphical tools](#Graphical_tools)
    *   [8.3 Other notes](#Other_notes)
*   [9 Fan Speed](#Fan_Speed)
*   [10 TV out](#TV_out)
    *   [10.1 Force TV-out in KMS](#Force_TV-out_in_KMS)
*   [11 HDMI audio](#HDMI_audio)
*   [12 Multihead setup](#Multihead_setup)
    *   [12.1 Using the RandR extension](#Using_the_RandR_extension)
    *   [12.2 Independent X screens](#Independent_X_screens)
*   [13 Turn vsync off](#Turn_vsync_off)
*   [14 Troubleshooting](#Troubleshooting)
    *   [14.1 Artifacts upon logging in](#Artifacts_upon_logging_in)
    *   [14.2 Adding undetected resolutions](#Adding_undetected_resolutions)
    *   [14.3 AGP is disabled (with KMS)](#AGP_is_disabled_.28with_KMS.29)
    *   [14.4 TV showing a black border around the screen](#TV_showing_a_black_border_around_the_screen)
    *   [14.5 Black screen with mouse cursor on resume from suspend in X](#Black_screen_with_mouse_cursor_on_resume_from_suspend_in_X)
    *   [14.6 No desktop effects in KDE4 with X1300 and Radeon driver](#No_desktop_effects_in_KDE4_with_X1300_and_Radeon_driver)
    *   [14.7 Black screen and no console, but X works in KMS](#Black_screen_and_no_console.2C_but_X_works_in_KMS)
    *   [14.8 2D performance (e.g. scrolling) is slow](#2D_performance_.28e.g._scrolling.29_is_slow)
    *   [14.9 Monitor rotation works for cursor but not windows/content](#Monitor_rotation_works_for_cursor_but_not_windows.2Fcontent)
    *   [14.10 ATI X1600 (RV530 series) 3D application show black windows](#ATI_X1600_.28RV530_series.29_3D_application_show_black_windows)
    *   [14.11 Cursor corruption after coming out of sleep](#Cursor_corruption_after_coming_out_of_sleep)
    *   [14.12 DisplayPort stays black on multimonitor mode](#DisplayPort_stays_black_on_multimonitor_mode)
    *   [14.13 Low 2D performance in console and X](#Low_2D_performance_in_console_and_X)

## Naming conventions

The [Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon") brand follows a naming scheme that relates each product to a market segment. Within this article, readers will see both *product* names (e.g. HD 4850, X1900) and *code* or *core* names (e.g. RV770, R580). Traditionally, a *product series* will correspond to a *core series* (e.g. the "X1000" product series includes the X1300, X1600, X1800, and X1900 products which utilize the "R500" core series – including the RV515, RV530, R520, and R580 cores).

For a table of core and product series, see [Wikipedia:Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon") and [Wikipedia:List of AMD graphics processing units](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units "wikipedia:List of AMD graphics processing units").

## Overview

*   For the latest Fiji and Tonga based graphics cards (Volcanic Islands/GCN 1.2), see the [AMDGPU](/index.php/AMDGPU "AMDGPU") page.
*   Radeons in the Rx 200 and Rx 300 (except for Radeon R9 285, R9 380, Radeon R9 Fury, Radeon R9 Nano) series (Sea/Southern Islands or GCN 1.1/1.0) have almost complete feature coverage and offer best performance.
*   Radeons up to the HD 8xxx series have full 2D and 3D acceleration, but might not support all the features that the proprietary driver provides. Performance varies from medicore for some cards to excellent for others.
*   Support of DRI1, RandR 1.2/1.3/1.4, Glamor, EXA acceleration and [kernel mode-setting](/index.php/KMS "KMS")/DRI2.

Check the [feature matrix](http://www.x.org/wiki/RadeonFeature) for more details.

Generally, **xf86-video-ati** should be your first choice, no matter which AMD/ATI card you own. In case you need to use a driver for newer AMD cards, you should consider the proprietary **catalyst** driver.

**Note:** **xf86-video-ati** is specified as ***radeon*** for the kernel and in `xorg.conf`.

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) package. It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.

To enable OpenGL support, also install [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). If you are on x86_64 and need 32-bit support, also install [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) from the [multilib](/index.php/Multilib "Multilib") repository.

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages.

## Configuration

Xorg will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-radeon.conf`, and add the following:

```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
EndSection

```

Using this section, you can enable features and tweak the driver settings.

## Loading

The radeon kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since radeon requires kernel mode-setting.
*   Also, check that you have not disabled radeon by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

### Enable early KMS

**Tip:** If you have problems with the resolution, [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") may help.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the radeon driver and is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `radeon` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="... radeon ..."

```

Now, regenerate the initramfs:

```
# mkinitcpio -p linux

```

The change takes effect at the next reboot.

## Performance tuning

### Enabling video acceleration

[VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") can be installed to provide hardware accelerated video encoding and decoding.

### Driver options

The following options apply to `/etc/X11/xorg.conf.d/**20-radeon.conf**`.

Please read `man radeon` and [RadeonFeature](http://www.x.org/wiki/RadeonFeature/#index4h2) first before applying driver options.

**ColorTiling** and **ColorTiling2D** is completely safe to enable and supposedly is enabled by default. Most users will notice increased performance but it is not yet supported on R200 and earlier cards. Can be enabled on earlier cards, but the workload is transferred to the CPU:

```
Option "ColorTiling" "on"
Option "ColorTiling2D" "on"

```

**DRI3** support can be enabled, instead of using the default **DRI2**. You may want to read the following benchmark by [Phoronix](http://www.phoronix.com/scan.php?page=article&item=radeon-dri3-perf&num=1) to give you an idea of the performance of DRI2 vs DRI3:

```
Option "DRI" "3"

```

**TearFree** is a tearing prevention using the hardware page flipping mechanism. Enabling this option currently disables Option "EnablePageFlip":

```
Option "TearFree" "on"

```

**Acceleration architecture**; Glamor is available as 2D acceleration method implement through OpenGL, and it should work with graphic cards whose drivers are newer or equal to R300. Since xf86-video-ati driver-1:7.2.0-1, it is automatically enabled with radeonsi drivers (Southern Islands and superior GFX cards); on other graphic cards the method can be forced by adding AccelMethod **glamor** to the configuration file:

```
Option "AccelMethod" "glamor"

```

When using Glamor as acceleration architecture it is possible to enable the option **ShadowPrimary**, enables a so-called "shadow primary" buffer for fast CPU access to pixel data, and separate scanout buf‐fers for each display controller (CRTC). This may improve performance for some 2D workloads, potentially at the expense of other (e.g. 3D, video) workloads. Note that enabling this option currently disables Option "EnablePageFlip":

```
Option "ShadowPrimary" "on"

```

**EXAVSync** is only available when using EXA and can be enabled to avoid tearing by stalling the engine until the display controller has passed the destination region. It reduces tearing at the cost of performance and has been know to cause instability on some chips:

```
Option "EXAVSync" "yes"

```

Below is a sample configuration file of `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
	Identifier  "Radeon"
	Driver "radeon"
	Option "AccelMethod" "glamor"
        Option "DRI" "3"
        Option "TearFree" "on"
EndSection

```

**Tip:** [driconf](https://www.archlinux.org/packages/?name=driconf) is a tool that allows to modify several settings: vsync, anisotropic filtering, texture compression, etc. Using this tool it is also possible to "disable Low Impact fallback" needed by some programs (e.g. Google Earth).

### Kernel parameters

**Tip:** You may want to debug the newly parameters with `systool` as stated in [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules").

Useful [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") may be `radeon.bapm=1` [[1]](https://www.phoronix.com/scan.php?page=news_item&px=MTczMzI), `radeon.disp_priority=2` [[2]](http://lists.freedesktop.org/pipermail/xorg/2013-February/055477.html), `radeon.hw_i2c=1` [[3]](https://superuser.com/questions/723760/does-radeon-hw-i2c-1-has-any-thing-to-do-with-temperature-readings), `radeon.mst=1` [[4]](https://www.phoronix.com/scan.php?page=news_item&px=Linux-4.1-Radeon-DP-MST), `radeon.msi=1` (force-enable MSI-support), `radeon.audio=0` (force-disable GPU audio) and/or `radeon.tv=0` (disable TV-out).

Defining the **gartsize**, if not autodetected, can be done by adding `radeon.gartsize=32` into [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Note:** Setting this parameter should not be needed anymore with modern AMD videocards:
```
[drm] Detected VRAM RAM=2048M, BAR=256M
[drm] radeon: 2048M of VRAM memory ready
[drm] radeon: 2048M of GTT memory ready.

```

The changes take effect at the next reboot.

#### Deactivating PCI-E 2.0

Since kernel 3.6, PCI-E v2.0 in **radeon** is turned on by default.

It may be unstable with some motherboards, deactivation can be done by adding `radeon.pcie_gen2=0` as a [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

See [Phoronix article](http://www.phoronix.com/scan.php?page=article&item=amd_pcie_gen2&num=1) for more information.

### Gallium Heads-Up Display

The radeonsi driver supports activating a heads up display which can draw transparent graphs and text on top of applications that are rendering such as games. These can show such values as the current frame rate or the CPU load for each CPU core or an average of all of them. The HUD is controlled by the GALLIUM_HUD environment variable, and can be passed the following list of parameters among others:

*   "fps" - displays current frames per second
*   "cpu" - displays the average CPU load
*   "cpu0" - displays the CPU load for the first CPU core
*   "cpu0+cpu1" - displays the CPU load for the first two CPU cores
*   "draw-calls" - displays how many times each material in an object is drawn to the screen
*   "requested-VRAM" - displayed how much VRAM is being used on the GPU
*   "pixels-rendered" - displays how many pixels are being displayed

To see a full list of parameters as well as some notes on operating GALLIUM_HUD you can also pass the "help" parameter to a simple application such as glxgears and see the corresponding terminal output:

 `# GALLIUM_HUD="help" glxgears` 

More information can be found from this [mailing list post](http://lists.freedesktop.org/archives/mesa-dev/2013-March/036586.html) or [this blog post](https://kparal.wordpress.com/2014/03/03/fraps-like-fps-overlay-for-linux/).

## Hybrid graphics/AMD Dynamic Switchable Graphics

It is the technology used on recent laptops equiped with two GPUs, one power-efficent (generally Intel integrated card) and one more powerful and more power-hungry (generally Radeon or Nvidia). There are two ways to get it work:

*   If it is not required to run 'GPU-hungry' applications, it is possible to disable the discrete card (see [Ubuntu wiki](https://help.ubuntu.com/community/HybridGraphics#Using_vga_switcheroo)): `echo OFF > /sys/kernel/debug/vgaswitcheroo/switch`.
*   [PRIME](/index.php/PRIME "PRIME"): Is a proper way to use hybrid graphics on Linux, but still requires a bit of manual intervention from the user.

## Powersaving

**Note:** Power management is supported on all chips that include the appropriate power state tables in the vbios (R1xx and newer). "dpm" is only supported on R6xx and newer chips.

With the radeon driver, power saving is disabled by default and has to be enabled manually if desired.

You can choose between three different methods:

1.  [dpm](#Dynamic_power_management) (enabled by default since kernel 3.13)
2.  [dynpm](#Dynamic_frequency_switching)
3.  [profile](#Profile-based_frequency_switching)

**It is hard to say which is the best for you, so you have to try it yourself!**

See [http://www.x.org/wiki/RadeonFeature/#index3h2](http://www.x.org/wiki/RadeonFeature/#index3h2) for more details.

### Dynamic power management

Since kernel 3.13, DPM is enabled by default for [lots of AMD Radeon hardware](http://kernelnewbies.org/Linux_3.13#head-f95c198f6fdc7defe36f470dc8369cf0e16898df). If you want to disable it, add the parameter `radeon.dpm=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Unlike [dynpm](#Dynamic_frequency_switching), the "dpm" method uses hardware on the GPU to dynamically change the clocks and voltage based on GPU load. It also enables clock and power gating.

There are 3 operation modes to choose from:

*   `battery` lowest power consumption
*   `balanced` sane default
*   `performance` highest performance

They can be changed via sysfs

```
# echo battery > /sys/class/drm/card0/device/power_dpm_state

```

For testing or debugging purposes, you can force the card to run in a set performance mode:

*   `auto` default; uses all levels in the power state
*   `low` enforces the lowest performance level
*   `high` enforces the highest performance level

```
# echo low > /sys/class/drm/card0/device/power_dpm_force_performance_level

```

### Old methods

#### Dynamic frequency switching

This method dynamically changes the frequency depending on GPU load, so performance is ramped up when running GPU intensive apps, and ramped down when the GPU is idle. The re-clocking is attempted during vertical blanking periods, but due to the timing of the re-clocking functions, does not always complete in the blanking period, which can lead to flicker in the display. Due to this, dynpm only works when a single head is active.

It can be activated by simply running the following command:

```
# echo dynpm > /sys/class/drm/card0/device/power_method

```

#### Profile-based frequency switching

This method will allow you to select one of the five profiles (described below). Different profiles, for the most part, end up changing the frequency/voltage of the GPU. This method is not as aggressive, but is more stable and flicker free and works with multiple heads active.

To activate the method, run the following command:

```
# echo profile > /sys/class/drm/card0/device/power_method

```

Select one of the available profiles:

*   `default` uses the default clocks and does not change the power state. This is the default behaviour.
*   `auto` selects between `mid` and `high` power states based on the whether the system is on battery power or not.
*   `low` forces the gpu to be in the `low` power state all the time. Note that `low` can cause display problems on some laptops, which is why `auto` only uses `low` when monitors are off. Selected on other profiles when the monitors are in the [DPMS](/index.php/DPMS "DPMS")-off state.
*   `mid` forces the gpu to be in the `mid` power state all the time.
*   `high` forces the gpu to be in the `high` power state all the time.

As an example, we will activate the `low` profile (replace `low` with any of the aforementioned profiles as necessary):

```
# echo low > /sys/class/drm/card0/device/power_profile

```

#### Persistent configuration

The activation described above is not persistent, it will not last when the computer is rebooted. To make it persistent, you can use [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd") (example for [#Dynamic frequency switching](#Dynamic_frequency_switching)):

 `/etc/tmpfiles.d/radeon-pm.conf` 
```
w /sys/class/drm/card0/device/power_method - - - - dynpm

```

Alternatively, you may use this [udev](/index.php/Udev "Udev") rule instead (example for [#Profile-based frequency switching](#Profile-based_frequency_switching)):

 `/etc/udev/rules.d/30-radeon-pm.rules` 
```
KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile", ATTR{device/power_profile}="low"

```

**Note:** If the above rule is failing, try removing the `dri/` prefix.

#### Graphical tools

*   **Radeon-tray** — A small program to control the power profiles of your Radeon card via systray icon. It is written in PyQt4 and is suitable for non-Gnome users.

	[https://github.com/StuntsPT/Radeon-tray](https://github.com/StuntsPT/Radeon-tray) || [radeon-tray](https://aur.archlinux.org/packages/radeon-tray/)

*   **power-play-switcher** — A gui for changing powerplay setting of the open source driver for ati radeon video cards.

	[https://code.google.com/p/power-play-switcher/](https://code.google.com/p/power-play-switcher/) || [power-play-switcher](https://aur.archlinux.org/packages/power-play-switcher/)

*   **Gnome-shell-extension-Radeon-Power-Profile-Manager** — A small extension for Gnome-shell that will allow you to change the power profile of your radeon card when using the open source drivers.

	[https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager](https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager) || [gnome-shell-extension-radeon-ppm](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-ppm/) [gnome-shell-extension-radeon-power-profile-manager-git](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-power-profile-manager-git/)

### Other notes

To view the speed that the GPU is running at, perform the following command and you will get something like this output:

 `# cat /sys/kernel/debug/dri/0/radeon_pm_info` 
```
  state: PM_STATE_ENABLED
  default engine clock: 300000 kHz
  current engine clock: 300720 kHz
  default memory clock: 200000 kHz

```

It depends on which GPU line yours is, however. Along with the radeon driver versions, kernel versions, etc. So it may not have much/any voltage regulation at all.

Thermal sensors are implemented via external i2c chips or via the internal thermal sensor (rv6xx-evergreen only). To get the temperature on asics that use i2c chips, you need to load the appropriate hwmon driver for the sensor used on your board (lm63, lm64, etc.). The drm will attempt to load the appropriate hwmon driver. On boards that use the internal thermal sensor, the drm will set up the hwmon interface automatically. When the appropriate driver is loaded, the temperatures can be accessed via [lm_sensors](/index.php/Lm_sensors "Lm sensors") tools or via sysfs in `/sys/class/hwmon`.

## Fan Speed

While the power saving features above should handle fan speeds quite well, some cards may still be too noisy in their idle state. In this case, and when your card supports it, you can change the fan speed manually.

**Note:**

*   Keep in mind that the following method sets the fan speed to a fixed value, hence it will not adjust with the stress of your gpu, which can lead to overheating under heavy load.
*   Better check your gpu temperature when applying lower than standard values.

First, issue the following command to enable the manual adjustment of the fan speed of your graphics card (or your first gpu in case of a multi gpu setup).

```
# echo 1 > /sys/class/drm/card0/device/hwmon/hwmon2/pwm1_enable

```

Then set your desired fan speed from 0 to 255, which corresponds to 0-100% fan speed (The following command sets it to roughly 20%).

```
# echo 55 > /sys/class/drm/card0/device/hwmon/hwmon2/pwm1

```

For persistence, use [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd") as shown above by the example with power profiles.

If a fixed value isn't desired, there are possibilities to define a custom fan curve manually by, for example, writing a script in which fan speeds are set depending on the current temperature (current value in /sys/class/drm/card0/device/hwmon/hwmon2/temp1_input), preferably with hystereses. There is also a gui solution: [http://github.com/marazmista/radeon-profile](http://github.com/marazmista/radeon-profile)[radeon-profile-git](https://aur.archlinux.org/packages/radeon-profile-git/).

## TV out

First, check that you have an S-video output: `xrandr` should give you something like

```
Screen 0: minimum 320x200, current 1024x768, maximum 1280x1200
...
S-video disconnected (normal left inverted right x axis y axis)

```

Now we should tell Xorg that it is actually connected (it *is*, right?)

```
xrandr --output S-video --set "load detection" 1

```

Setting TV standard to use:

```
xrandr --output S-video --set "tv standard" ntsc

```

Adding a mode for it (currently supports only 800x600):

```
xrandr --addmode S-video 800x600

```

Clone mode:

```
xrandr --output S-video --same-as VGA-0

```

Now let us try to see what we have:

```
xrandr --output S-video --mode 800x600

```

At this point you should see a 800x600 version of your desktop on your TV.

To disable the output, do

```
xrandr --output S-video --off

```

Also you may notice that the video is being played on monitor only and not on the TV. Where the Xv overlay is sent is controlled by XV_CRTC attribute.

To send the output to the TV, do:

```
xvattr -a XV_CRTC -v 1

```

**Note:** you need to install [xvattr](https://aur.archlinux.org/packages/xvattr/) to execute this command.

To switch back to the monitor, I change this to `0`. `-1` is used for automatic switching in dualhead setups.

Please see [Enabling TV-Out Statically](http://www.x.org/wiki/radeonTV) for how to enable TV-out in your xorg configuration file.

### Force TV-out in KMS

The kernel can recognize `video=` parameter in following form (see [KMS](/index.php/KMS "KMS") for more details):

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

For example:

```
video=DVI-I-1:1280x1024-24@60e

```

Parameters with whitespaces must be quoted:

```
"video=9-pin DIN-1:1024x768-24@60e"

```

Current mkinitcpio implementation also requires `#` in front. For example:

```
root=/dev/disk/by-uuid/d950a14f-fc0c-451d-b0d4-f95c2adefee3 ro quiet radeon.modeset=1 security=none # video=DVI-I-1:1280x1024-24@60e "video=9-pin DIN-1:1024x768-24@60e"

```

*   Grub can pass such command line as is.
*   Lilo needs backslashes for doublequotes (append `# \"video=9-pin DIN-1:1024x768-24@60e\"`)
*   Grub2: TODO

You can get list of your video outputs with following command:

 `$ ls -1 /sys/class/drm/ | grep -E '^card[[:digit:]]+-' | cut -d- -f2-` 

## HDMI audio

HDMI audio is supported in the [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) video driver. By default HDMI audio is disabled in the driver kernel versions >=3.0 because it can be problematic. To enable HDMI audio add `radeon.audio=1` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

If there is no video after boot up, the driver option has to be disabled.

**Note:**

*   If HDMI audio does not work after installing the driver, test your setup with the procedure at [Advanced Linux Sound Architecture/Troubleshooting#HDMI Output does not work](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#HDMI_Output_does_not_work "Advanced Linux Sound Architecture/Troubleshooting").
*   If the sound is distorted in PulseAudio try setting `tsched=0` as described in [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches.2C_skips_or_crackling "PulseAudio/Troubleshooting") and make sure `rtkit` daemon is running.
*   Your sound card might use the same module, since HDA compliant hardware is pretty common. [Change the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture") using one of the suggested methods, which include using the `defaults` node in alsa configuration.

## Multihead setup

### Using the RandR extension

See [Multihead#RandR](/index.php/Multihead#RandR "Multihead") how to setup multiple monitors by using [RandR](https://en.wikipedia.org/wiki/RandR "wikipedia:RandR").

### Independent X screens

Independent dual-headed setups can be configured the usual way. However you might want to know that the radeon driver has a `"ZaphodHeads"` option which allows you to bind a specific device section to an output of your choice:

 `/etc/X11/xorg.conf.d/20-radeon.conf` 
```
Section "Device"
  Identifier "Device0"
  Driver "radeon"
  Option "ZaphodHeads" "VGA-0"
  VendorName "ATI"
  BusID "PCI:1:0:0"
  Screen 0
EndSection

```

This can be a life-saver, when using videocards that have more than two outputs. For instance one HDMI out, one DVI, one VGA, will only select and use HDMI+DVI outputs for the dual-head setup, unless you explicitly specify `"ZaphodHeads" "VGA-0"`.

## Turn vsync off

The radeon driver will enable vsync by default, which is perfectly fine except for benchmarking. To turn it off, create `~/.drirc` (or edit it if it already exists) and add the following section:

 `~/.drirc` 
```
<driconf>
    <device screen="0" driver="dri2">
        <application name="Default">
            <option name="vblank_mode" value="0" />
        </application>
    </device>
    <!-- Other devices ... -->
</driconf>

```

Make sure the driver is **dri2**, not your video card code (like r600).

If vsync is still enabled, you can try to disable it by editing the xf86-video-ati configuration :

 `/etc/X11/xorg.conf.d/20-radeon.con` 
```
Section "Device"
	Identifier  "My Graphics Card"
	Driver	"radeon"
	Option	"EXAVSync" "off"
	Option "SwapbuffersWait" "false" 
EndSection

```

## Troubleshooting

### Artifacts upon logging in

If encountering artifacts, first try starting X without `/etc/X11/xorg.conf`. Recent versions of Xorg are capable of reliable auto-detection and auto-configuration for most use cases. Outdated or improperly configured `xorg.conf` files are known to cause trouble.

In order to run without a configuration tile, it is recommended that the `xorg-input-drivers` package group be installed.

You may as well try disabling `EXAPixmaps` in `/etc/X11/xorg.conf.d/20-radeon.conf`:

```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
    Option "EXAPixmaps" "off"
EndSection

```

### Adding undetected resolutions

Please see the [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### AGP is disabled (with KMS)

If you experience poor performance and dmesg shows something like this

```
[drm:radeon_agp_init] *ERROR* Unable to acquire AGP: -19

```

then check if the agp driver for your motherboard (e.g., `via_agp`, `intel_agp` etc.) is loaded before the `radeon` module, see [Enabling KMS](#Enabling_KMS).

### TV showing a black border around the screen

When I connected my TV to my Radeon HD 5770 using the HDMI port, the TV showed a blurry picture with a 2-3cm border around it. This is not the case when using the proprietary driver. However, this protection against overscanning (see [Wikipedia:Overscan](https://en.wikipedia.org/wiki/Overscan "wikipedia:Overscan")) can be turned off using xrandr:

```
xrandr --output HDMI-0 --set underscan off

```

### Black screen with mouse cursor on resume from suspend in X

Waking from suspend on cards with 32MB or less can result in a black screen with a mouse pointer in X. Some parts of the screen may be redrawn when under the mouse cursor. Forcing `EXAPixmaps` to `"enabled"` in `/etc/X11/xorg.conf.d/20-radeon.conf` may fix the problem. See [performance tuning](#Performance_tuning) for more information.

### No desktop effects in KDE4 with X1300 and Radeon driver

A bug in KDE4 may prevent an accurate video hardware check, thereby deactivating desktop effects despite the X1300 having more than sufficient GPU power. A workaround may be to manually override such checks in KDE4 configuration files `/usr/share/kde-settings/kde-profile/default/share/config/kwinrc` and/or `.kde/share/config/kwinrc`.

Add:

```
DisableChecks=true

```

To the [Compositing] section. Ensure that compositing is enabled with:

```
Enabled=true

```

### Black screen and no console, but X works in KMS

This is a solution to no-console problem that might come up, when using two or more ATI cards on the same PC. Fujitsu Siemens Amilo PA 3553 laptop for example has this problem. This is due to fbcon console driver mapping itself to wrong framebuffer device that exist on the wrong card. This can be fixed by adding a this to the kernel boot line:

```
fbcon=map:1

```

This will tell the fbcon to map itself to the `/dev/fb1` framebuffer dev and not the `/dev/fb0`, that in our case exist on the wrong graphics card. If that does not fix your problem, try booting with

```
fbcon=map:0

```

instead.

### 2D performance (e.g. scrolling) is slow

If you have problem with 2D performance, like scrolling in terminal or browser, you might need to add `Option "MigrationHeuristic" "greedy"` into the `"Device"` section of your `xorg.conf` file.

**Note:** This only applies to EXA.

Below is a sample configuration file `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
        Identifier  "My Graphics Card"
        Driver  "radeon"
        Option  "MigrationHeuristic"  "greedy"
EndSection

```

### Monitor rotation works for cursor but not windows/content

Users with newer graphics boards who have enabled EXA instead of glamor may find that rotating their monitor with xrandr causes the cursor and monitor dimensions to rotate, but windows and other content stay in their normal orientation. Additionally, the cursor moves according to normal rotation when the user moves the mouse. Look for the following line in your `/var/log/Xorg.0.log` when you issue the xrandr rotate command:

```
(EE) RADEON(0): Rotation requires acceleration!

```

Acceleration is disabled when using EXA on newer graphics cards (source: [comment 17](https://bugs.freedesktop.org/show_bug.cgi?id=73420#c17)). You must choose between enabling EXA ([detailed above in the glamor section](#Glamor)) and the ability to rotate.

### ATI X1600 (RV530 series) 3D application show black windows

There are three possible solutions:

*   Try add `pci=nomsi` to your boot loader [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
*   If this does not work, you can try adding `noapic` instead of `pci=nomsi`.
*   If none of the above work, then you can try running `vblank_mode=0 glxgears` or `vblank_mode=1 glxgears` to see which one works for you, then install [driconf](https://www.archlinux.org/packages/?name=driconf) and set that option in `~/.drirc`.

### Cursor corruption after coming out of sleep

If the cursor becomes corrupted like it's repeating itself vertically after the monitor(s) comes out of sleep, set `"SWCursor" "True"` in the `"Device"` section of the `20-radeon.conf` configuration file.

### DisplayPort stays black on multimonitor mode

Try booting with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `radeon.audio=0`.

### Low 2D performance in console and X

Since kernel 4.1.4, [dpm](#Dynamic_power_management) is broken on certain R9 270X cards (chip device number 6810, subsystem 174b:e271, shown as Curacao XT, PC Partner Limited / Sapphire Technology Device e271 in lspci). The regression is caused by a [fix](https://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/commit/?id=ea039f927524e36c15b5905b4c9469d788591932) for cards with the same PCI ids. Disabling dpm (add `radeon.dpm=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters")) solves the problem.
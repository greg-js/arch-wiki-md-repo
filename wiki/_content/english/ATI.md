Related articles

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")
*   [AMDGPU](/index.php/AMDGPU "AMDGPU")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")

This article covers the [radeon](https://wiki.freedesktop.org/xorg/radeon/) open source driver which supports the majority of AMD (previously ATI) GPUs.

## Contents

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Xorg configuration](#Xorg_configuration)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 Enabling video acceleration](#Enabling_video_acceleration)
    *   [5.2 Driver options](#Driver_options)
    *   [5.3 Kernel parameters](#Kernel_parameters)
        *   [5.3.1 Deactivating PCIe 2.0](#Deactivating_PCIe_2.0)
    *   [5.4 Gallium Heads-Up Display](#Gallium_Heads-Up_Display)
*   [6 Hybrid graphics/AMD Dynamic Switchable Graphics](#Hybrid_graphics/AMD_Dynamic_Switchable_Graphics)
*   [7 Powersaving](#Powersaving)
    *   [7.1 Dynamic power management](#Dynamic_power_management)
        *   [7.1.1 Commandline Tools](#Commandline_Tools)
    *   [7.2 Old methods](#Old_methods)
        *   [7.2.1 Dynamic frequency switching](#Dynamic_frequency_switching)
        *   [7.2.2 Profile-based frequency switching](#Profile-based_frequency_switching)
    *   [7.3 Persistent configuration](#Persistent_configuration)
    *   [7.4 Graphical tools](#Graphical_tools)
    *   [7.5 Other notes](#Other_notes)
*   [8 Fan Speed](#Fan_Speed)
*   [9 TV out](#TV_out)
    *   [9.1 Force TV-out in KMS](#Force_TV-out_in_KMS)
*   [10 HDMI audio](#HDMI_audio)
*   [11 Multihead setup](#Multihead_setup)
    *   [11.1 Using the RandR extension](#Using_the_RandR_extension)
    *   [11.2 Independent X screens](#Independent_X_screens)
*   [12 Turn vsync off](#Turn_vsync_off)
*   [13 Troubleshooting](#Troubleshooting)
    *   [13.1 Performance and/or artifacts issues when using EXA](#Performance_and/or_artifacts_issues_when_using_EXA)
    *   [13.2 Adding undetected/unsupported resolutions](#Adding_undetected/unsupported_resolutions)
    *   [13.3 TV showing a black border around the screen](#TV_showing_a_black_border_around_the_screen)
    *   [13.4 Black screen and no console, but X works in KMS](#Black_screen_and_no_console,_but_X_works_in_KMS)
    *   [13.5 ATI X1600 (RV530 series) 3D application show black windows](#ATI_X1600_(RV530_series)_3D_application_show_black_windows)
    *   [13.6 Cursor corruption after coming out of sleep](#Cursor_corruption_after_coming_out_of_sleep)
    *   [13.7 DisplayPort stays black on multimonitor mode](#DisplayPort_stays_black_on_multimonitor_mode)
    *   [13.8 R9-390 Poor Performance and/or Instability](#R9-390_Poor_Performance_and/or_Instability)
    *   [13.9 QHD / UHD / 4k support over HDMI for older Radeon cards](#QHD_/_UHD_/_4k_support_over_HDMI_for_older_Radeon_cards)
*   [14 See also](#See_also)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). This page has instructions for **ATI**.

If unsure, try this open source driver first, it will suit most needs and is generally less problematic. See the [feature matrix](https://www.x.org/wiki/RadeonFeature) to know what is supported and the [decoder ring](https://www.x.org/wiki/RadeonFeature/#index5h2) to translate marketing names (e.g. Radeon HD4330) to chip names (e.g. R700).

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package, which provides the DRI driver for 3D acceleration.

*   For 32-bit application support, also install the [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) package from the [multilib](/index.php/Multilib "Multilib") repostory.
*   For the DDX driver (which provides 2D acceleration in [Xorg](/index.php/Xorg "Xorg")), install the [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) package.

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages.

## Loading

The radeon kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since radeon requires [KMS](/index.php/KMS "KMS").
*   Also, check that you have not disabled radeon by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

### Enable early KMS

**Tip:** If you have problems with the resolution, [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") may help.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the radeon driver and is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `radeon` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="... radeon ..."

```

Now, [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

The change takes effect at the next reboot.

## Xorg configuration

Xorg will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-radeon.conf`, and add the following:

```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
EndSection

```

Using this section, you can enable features and tweak the driver settings.

## Performance tuning

### Enabling video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

### Driver options

The following options apply to `/etc/X11/xorg.conf.d/**20-radeon.conf**`.

Please read [radeon(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/radeon.4) and [RadeonFeature](https://www.x.org/wiki/RadeonFeature/#index4h2) first before applying driver options.

**Acceleration architecture**; Glamor is available as a 2D acceleration method implemented through OpenGL, and it [is the default](https://cgit.freedesktop.org/xorg/driver/xf86-video-ati/commit/?id=f11531c99fcd6473f58b4d10efaf3efd84304d8e) for R600 (Radeon HD2000 series) and newer graphic cards. Older cards use EXA.

```
Option "AccelMethod" "glamor"

```

**DRI3** is enabled by default [since xf86-video-ati 7.8.0](https://www.phoronix.com/scan.php?page=news_item&px=Radeon-AMDGPU-1.19-Updates). For older drivers, which use DRI2 by default, switch to DRI3 with the following option:

```
Option "DRI" "3"

```

**TearFree** is a tearing prevention option which prevents tearing by using the hardware page flipping mechanism:

```
Option "TearFree" "on"

```

**ColorTiling** and **ColorTiling2D** are supposed to be enabled by default. Tiled mode can provide significant performance benefits with 3D applications. It is disabled if the DRM module is too old or if the current display configuration does not support it. KMS ColorTiling2D is only supported on R600 (Radeon HD2000 series) and newer chips:

```
Option "ColorTiling" "on"
Option "ColorTiling2D" "on"

```

When using Glamor as acceleration architecture, it is possible to enable the **ShadowPrimary** option, which enables a so-called "shadow primary" buffer for fast CPU access to pixel data, and separate scanout buffers for each display controller (CRTC). This may improve performance for some 2D workloads, potentially at the expense of other (e.g. 3D, video) workloads. Note that enabling this option currently disables Option "EnablePageFlip":

```
Option "ShadowPrimary" "on"

```

**EXAVSync** is only available when using EXA and can be enabled to avoid tearing by stalling the engine until the display controller has passed the destination region. It reduces tearing at the cost of performance and has been known to cause instability on some chips:

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
        Option "ColorTiling" "on"
        Option "ColorTiling2D" "on"
EndSection

```

**Tip:** [driconf](https://www.archlinux.org/packages/?name=driconf) is a tool which allows several settings to be modified: vsync, anisotropic filtering, texture compression, etc. Using this tool it is also possible to "disable Low Impact fallback" needed by some programs (e.g. Google Earth).

### Kernel parameters

**Tip:** You may want to debug the new parameters with `systool` as stated in [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules").

Defining the **gartsize**, if not autodetected, can be done by adding `radeon.gartsize=32` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

**Note:** Setting this parameter should not be needed anymore with modern AMD video cards:
```
[drm] Detected VRAM RAM=2048M, BAR=256M
[drm] radeon: 2048M of VRAM memory ready
[drm] radeon: 2048M of GTT memory ready.

```

The changes take effect at the next reboot.

#### Deactivating PCIe 2.0

Since kernel 3.6, PCI Express 2.0 in **radeon** is turned on by default.

It may be unstable with some motherboards. It can be deactivated by adding `radeon.pcie_gen2=0` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

See [Phoronix article](https://www.phoronix.com/scan.php?page=article&item=amd_pcie_gen2&num=1) for more information.

### Gallium Heads-Up Display

The radeon driver supports the activation of a heads-up display (HUD) which can draw transparent graphs and text on top of applications that are rendering, such as games. These can show values such as the current frame rate or the CPU load for each CPU core or an average of all of them. The HUD is controlled by the GALLIUM_HUD environment variable, and can be passed the following list of parameters among others:

*   "fps" - displays current frames per second
*   "cpu" - displays the average CPU load
*   "cpu0" - displays the CPU load for the first CPU core
*   "cpu0+cpu1" - displays the CPU load for the first two CPU cores
*   "draw-calls" - displays how many times each material in an object is drawn to the screen
*   "requested-VRAM" - displays how much VRAM is being used on the GPU
*   "pixels-rendered" - displays how many pixels are being displayed

To see a full list of parameters, as well as some notes on operating GALLIUM_HUD, you can also pass the "help" parameter to a simple application such as glxgears and see the corresponding terminal output:

 `# GALLIUM_HUD="help" glxgears` 

More information can be found from this [mailing list post](https://lists.freedesktop.org/archives/mesa-dev/2013-March/036586.html) or [this blog post](https://kparal.wordpress.com/2014/03/03/fraps-like-fps-overlay-for-linux/).

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

See [https://www.x.org/wiki/RadeonFeature/#index3h2](https://www.x.org/wiki/RadeonFeature/#index3h2) for more details.

### Dynamic power management

Since kernel 3.13, DPM is enabled by default for [lots of AMD Radeon hardware](https://kernelnewbies.org/Linux_3.13#head-f95c198f6fdc7defe36f470dc8369cf0e16898df). If you want to disable it, add the parameter `radeon.dpm=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Tip:** DPM works on R6xx gpus, but is not enabled by default in the kernel (only R7xx and up). Setting the `radeon.dpm=1` kernel parameter will enable dpm.

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

#### Commandline Tools

*   [radcard](https://github.com/superjamie/snippets/blob/master/radcard) - A script to get and set DPM power states and levels

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

### Persistent configuration

The methods described above are not persistent. To make them persistent, you may create a [udev](/index.php/Udev "Udev") rule (example for [#Profile-based frequency switching](#Profile-based_frequency_switching)):

 `/etc/udev/rules.d/30-radeon-pm.rules` 
```
KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile", ATTR{device/power_profile}="low"

```

As another example, [dynamic power management](#Dynamic_power_management) can be permanently forced to a certain performance level:

 `/etc/udev/rules.d/30-radeon-pm.rules` 
```
KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_dpm_force_performance_level}="high"

```

**Note:** If the above rules are failing, try removing the `dri/` prefix.

### Graphical tools

*   **Radeon-tray** — A small program to control the power profiles of your Radeon card via systray icon. It is written in PyQt4 and is suitable for non-Gnome users.

	[https://github.com/StuntsPT/Radeon-tray](https://github.com/StuntsPT/Radeon-tray) || [radeon-tray](https://aur.archlinux.org/packages/radeon-tray/)

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

**Warning:**

*   Keep in mind that the following method sets the fan speed to a fixed value, hence it will not adjust with the stress of the GPU, which can lead to overheating under heavy load.
*   Check GPU temperature when applying lower than standard values.

To control the GPU fan, see [Fan speed control#AMDGPU sysfs fan control](/index.php/Fan_speed_control#AMDGPU_sysfs_fan_control "Fan speed control") (amdgpu and radeon share the same controls for this).

For persistence, see the example in [#Persistent configuration](#Persistent_configuration).

If a fixed value is not desired, there are possibilities to define a custom fan curve manually by, for example, writing a script in which fan speeds are set depending on the current temperature (current value in `/sys/class/drm/card0/device/hwmon/hwmon0/temp1_input`).

A GUI solution is available by installing [radeon-profile-git](https://aur.archlinux.org/packages/radeon-profile-git/).

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

*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") can pass such command line as is.
*   [LILO](/index.php/LILO "LILO") needs backslashes for doublequotes (append `# \"video=9-pin DIN-1:1024x768-24@60e\"`)

You can get list of your video outputs with following command:

 `$ ls -1 /sys/class/drm/ | grep -E '^card[[:digit:]]+-' | cut -d- -f2-` 

## HDMI audio

HDMI audio is supported in the [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) video driver. To disable HDMI audio add `radeon.audio=0` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

If there is no video after boot up, the driver option has to be disabled.

**Note:**

*   If HDMI audio does not work after installing the driver, test your setup with the procedure at [Advanced Linux Sound Architecture/Troubleshooting#HDMI Output does not work](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting#HDMI_Output_does_not_work "Advanced Linux Sound Architecture/Troubleshooting").
*   If the sound is distorted in PulseAudio try setting `tsched=0` as described in [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches,_skips_or_crackling "PulseAudio/Troubleshooting") and make sure `rtkit` daemon is running.
*   Your sound card might use the same module, since HDA compliant hardware is pretty common. [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture") using one of the suggested methods, which include using the `defaults` node in alsa configuration.

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

The radeon driver will probably enable vsync by default, which is perfectly fine except for benchmarking. To turn it off try the `vblank_mode=0` [environment variable](/index.php/Environment_variable "Environment variable") or create `~/.drirc` (edit it if it already exists) and add the following:

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

**Note:** Make sure the driver is **dri2**, not your video card code (like r600).

If vsync is still enabled, you can disable it by editing `/etc/X11/xorg.conf.d/20-radeon.conf`. See [#Driver options](#Driver_options).

## Troubleshooting

### Performance and/or artifacts issues when using EXA

**Note:** This only applies to cards older than R600 (Radeon X1000 series and older). Newer cards you should use Glamor instead of EXA.

If having 2D performance issues, like slow scrolling in a terminal or webbrowser, adding `Option "MigrationHeuristic" "greedy"` as device option may solve the issue.

In addition disabling EXAPixmaps may solve artifacts issues, although this is generally not recommended and may cause other issues.

 `/etc/X11/xorg.conf.d/20-radeon.conf` 
```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
    Option "AccelMethod" "exa"
    Option "MigrationHeuristic" "greedy"
    #Option "EXAPixmaps" "off"
EndSection

```

### Adding undetected/unsupported resolutions

See [Xrandr#Adding undetected resolutions](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### TV showing a black border around the screen

**Note:** Make sure the tv has been setup correctly (see manual) before attempting the following solution.

When connecting a TV using the HDMI port, the TV may show a blurry picture with a 2-3cm border around it. This protects against overscanning (see [Wikipedia:Overscan](https://en.wikipedia.org/wiki/Overscan "wikipedia:Overscan")), but can be turned off using xrandr:

```
xrandr --output HDMI-0 --set underscan off

```

### Black screen and no console, but X works in KMS

This is a solution to the no-console problem that might come up, when using two or more ATI cards on the same PC. Fujitsu Siemens Amilo PA 3553 laptop for example has this problem. This is due to fbcon console driver mapping itself to the wrong framebuffer device that exists on the wrong card. This can be fixed by adding this to the kernel boot line:

```
fbcon=map:1

```

This will tell the fbcon to map itself to the `/dev/fb1` framebuffer dev and not the `/dev/fb0`, that in our case exists on the wrong graphics card. If that does not fix your problem, try booting with

```
fbcon=map:0

```

instead.

### ATI X1600 (RV530 series) 3D application show black windows

There are three possible solutions:

*   Try adding `pci=nomsi` to your boot loader [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
*   If this does not work, you can try adding `noapic` instead of `pci=nomsi`.
*   If none of the above work, then you can try running `vblank_mode=0 glxgears` or `vblank_mode=1 glxgears` to see which one works for you, then install [driconf](https://www.archlinux.org/packages/?name=driconf) and set that option in `~/.drirc`.

### Cursor corruption after coming out of sleep

If the cursor becomes corrupted like it's repeating itself vertically after the monitor(s) comes out of sleep, set `"SWCursor" "True"` in the `"Device"` section of the `/etc/X11/xorg.conf.d/20-radeon.conf` configuration file.

### DisplayPort stays black on multimonitor mode

Try booting with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `radeon.audio=0`.

### R9-390 Poor Performance and/or Instability

Firmware issues with R9-390 series cards include poor performance and crashes (frequently caused by gaming or using Google Maps) possibly related DPM. Comment 115 of this bug [report](https://bugs.freedesktop.org/show_bug.cgi?id=91880) includes instructions for a fix.

### QHD / UHD / 4k support over HDMI for older Radeon cards

Older cards have their pixel clock limited to 165MHz for HDMI. Hence, they do not support QHD or 4k only via dual-link DVI but not over HDMI.

One possibility to work around this is to use [custom modes with lower refresh rate](https://www.elstel.org/software/hunt-for-4K-UHD-2160p.html.en), e.g. 30Hz.

Another one is a kernel patch removing the pixel clock limit, but this may damage the card!

Official kernel bug ticket with patch for 4.8: [https://bugzilla.kernel.org/show_bug.cgi?id=172421](https://bugzilla.kernel.org/show_bug.cgi?id=172421)

The patch introduces a new kernel parameter `radeon.hdmimhz` which alters the pixel clock limit.

Be sure to use a high speed HDMI cable for this.

## See also

[Benchmark](https://www.phoronix.com/scan.php?page=article&item=radeonsi-cat-wow&num=1) showing the open source driver is on par performance-wise with the proprietary driver for many cards.
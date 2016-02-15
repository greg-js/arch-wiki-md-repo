Since Intel provides and supports open source drivers, Intel graphics are now essentially plug-and-play.

For a comprehensive list of Intel GPU models and corresponding chipsets and CPUs, see [this comparison on Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Note:** PowerVR-based graphics ([GMA 500](/index.php/GMA_500 "GMA 500") and [GMA 3600](/index.php/Intel_GMA3600 "Intel GMA3600") series) are not supported by open source drivers.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Module-based Powersaving Options](#Module-based_Powersaving_Options)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Enable Glamor Acceleration Method](#Enable_Glamor_Acceleration_Method)
    *   [5.2 Direct Rendering Infrastructure 3 (DRI3)](#Direct_Rendering_Infrastructure_3_.28DRI3.29)
    *   [5.3 Tear-free video](#Tear-free_video)
    *   [5.4 Disable Vertical Synchronization (VSYNC)](#Disable_Vertical_Synchronization_.28VSYNC.29)
    *   [5.5 Setting scaling mode](#Setting_scaling_mode)
    *   [5.6 KMS Issue: console is limited to small area](#KMS_Issue:_console_is_limited_to_small_area)
    *   [5.7 H.264 decoding on GMA 4500](#H.264_decoding_on_GMA_4500)
    *   [5.8 Setting brightness and gamma](#Setting_brightness_and_gamma)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 SNA issues](#SNA_issues)
    *   [6.2 Blank screen during boot, when "Loading modules"](#Blank_screen_during_boot.2C_when_.22Loading_modules.22)
    *   [6.3 X freeze/crash with intel driver](#X_freeze.2Fcrash_with_intel_driver)
    *   [6.4 Adding undetected resolutions](#Adding_undetected_resolutions)
    *   [6.5 Weathered colors (color range problem)](#Weathered_colors_.28color_range_problem.29)
    *   [6.6 Backlight is not adjustable](#Backlight_is_not_adjustable)
    *   [6.7 Disabling frame buffer compression](#Disabling_frame_buffer_compression)
    *   [6.8 Corruption/Unresponsiveness in Chromium and Firefox](#Corruption.2FUnresponsiveness_in_Chromium_and_Firefox)
    *   [6.9 Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips](#Kernel_crashing_w.2Fkernels_4.0.2B_on_Broadwell.2FCore-M_chips)
    *   [6.10 Skylake Support](#Skylake_Support)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.

To enable OpenGL support, also install [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). If you are on x86_64 and need 32-bit support, also install [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) from the [multilib](/index.php/Multilib "Multilib") repository.

Follow [VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") for hardware-accelerated video processing; on older GPUs, this is provided instead by the [XvMC](/index.php/XvMC "XvMC") driver, which is included with the DDX driver.

## Configuration

There is no need for any configuration to run [Xorg](/index.php/Xorg "Xorg").

**Note:** The latest generation of integrated GPUs (Skylake/HD 530 for instance) may require additional configuration, see [#Skylake_Support](#Skylake_Support)

However, to take advantage of some driver options, you will need to create a Xorg configuration file similar to the one below:

 `/etc/X11/xorg.conf.d/20-intel.conf` 

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
EndSection
```

Additional options are added by the user on new lines below `Driver`.

**Note:**

*   You may need to indicate `AccelMethod` when creating a configuration file, even just to set it to the default method (currently `"sna"`); otherwise, X may crash.
*   You might need to add more device sections than the one listed above. This will be indicated where necessary.

For the full list of options, see the [man page](/index.php/Man_page "Man page") for `intel`.

## Loading

The Intel kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since Intel requires kernel mode-setting.
*   Also, check that you have not disabled Intel by using any modprobe blacklisting within `/etc/modprobe.d/` or `/usr/lib/modprobe.d/`.

### Enable early KMS

**Tip:** If you have problems with the resolution, you can check whether [enforcing the mode](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") helps.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by Intel chipsets that use the i915 DRM driver and is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `i915` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="... i915 ..."

```

**Tip:** Users might need to add `intel_agp` before `i915` to suppress the ACPI errors. The order matters because the modules are activated in sequence. This might be required for resuming from hibernation to work with changed display configuration!

If you are using a custom [EDID](https://en.wikipedia.org/wiki/Extended_display_identification_data "wikipedia:Extended display identification data") file, you should embed it into initramfs as well:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Now, regenerate the initramfs:

```
# mkinitcpio -p linux

```

The change takes effect at the next reboot.

## Module-based Powersaving Options

The `i915` kernel module allows for configuration via [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Some of the module options impact power saving.

A list of all options along with short descriptions and default values can be generated with the following command:

```
$ modinfo -p i915

```

To check which options are currently enabled, run

```
# systool -m i915 -av

```

You will note that the `i915.powersave` option which "enable[s] powersavings, fbc, downclocking, etc." is enabled by default, resulting in per-chip powersaving defaults. It is however possible to configure more aggressive powersaving by using [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules").

**Warning:** Diverting from the defaults will mark the kernel as [tainted](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=fc9740cebc3ab7c65f3c5f6ce0caf3e4969013ca) from Linux 3.18 onwards. This basically implies using other options than the per-chip defaults is considered experimental and not supported by the developers.

The following set of options should be generally safe to enable:

 `/etc/modprobe.d/i915.conf` 

```
options i915 enable_rc6=1 enable_fbc=1 lvds_downclock=1 semaphores=1

```

You can experiment with higher values for `enable_rc6`, but your GPU may not support them or the activation of the other options [[1]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

Framebuffer compression, for example, may be unreliable or unavailable on Intel GPU generations before Sandy Bridge (generation 6). This results in messages logged to the system journal similar to this one:

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## Tips and tricks

### Enable Glamor Acceleration Method

[Glamor](https://wiki.freedesktop.org/www/Software/Glamor/) is Intel's experimental OpenGL 2D acceleration method and is not documented in the manpages. To use it, add the following line to your [configuration file](#Configuration):

```
Option      "AccelMethod"  "glamor"

```

**Note:** This acceleration method is experimental and may not be stable for your system.

### Direct Rendering Infrastructure 3 (DRI3)

By default Direct Rendering Infrastructure 2 (DRI2) is used. To enable the next generation of DRI, [DRI3](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure#DRI3 "wikipedia:Direct Rendering Infrastructure"), which contains several improvements, add the following line to your [configuration file](#Configuration):

```
Option      "DRI"    "3"

```

To verify that DRI3 is enabled you can check the [Xorg](/index.php/Xorg "Xorg") log files after restarting.

### Tear-free video

The SNA acceleration method causes tearing for some people. To fix this, enable the `"TearFree"` option in the driver by adding the following line to your [configuration file](#Configuration):

```
Option      "TearFree"    "true"

```

See the [original bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) for more info.

**Note:**

*   This option may not work when `SwapbuffersWait` is `false`.
*   This option is problematic for applications that are very picky about vsync timing, like [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy").
*   This option does not work with UXA acceleration method, only with SNA.

### Disable Vertical Synchronization (VSYNC)

The intel-driver uses [Triple Buffering](http://www.intel.com/support/graphics/sb/CS-004527.htm) for vertical synchronization, this allows for full performance and avoids tearing. To turn vertical synchronization off (e.g. for benchmarking) use this `.drirc` in your home directory:

 `~/.drirc` 

```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

**Warning:** Do not use [driconf](https://www.archlinux.org/packages/?name=driconf) to create this file, it is buggy and will set the wrong driver.

### Setting scaling mode

This can be useful for some full screen applications:

```
$ xrandr --output LVDS1 --set PANEL_FITTING param

```

where `param` can be:

*   `center`: resolution will be kept exactly as defined, no scaling will be made,
*   `full`: scale the resolution so it uses the entire screen or
*   `full_aspect`: scale the resolution to the maximum possible but keep the aspect ratio.

If it does not work, try:

```
$ xrandr --output LVDS1 --set "scaling mode" param

```

where `param` is one of `"Full"`, `"Center"` or `"Full aspect"`.

### KMS Issue: console is limited to small area

One of the low-resolution video ports may be enabled on boot which is causing the terminal to utilize a small area of the screen. To fix, explicitly disable the port with an i915 module setting with `video=SVIDEO-1:d` in the kernel command line parameter in the bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

If that does not work, try disabling TV1 or VGA1 instead of SVIDEO-1.

### H.264 decoding on GMA 4500

The [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) package provides MPEG-2 decoding only for GMA 4500 series GPUs. The H.264 decoding support is maintained in a separated g45-h264 branch, which can be used by installing [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) package. Note however that this support is experimental and its development has been abandoned. Using the VA-API with this driver on a GMA 4500 series GPU will offload the CPU but may not result in as smooth a playback as non-accelerated playback. Tests using mplayer showed that using vaapi to play back an H.264 encoded 1080p video halved the CPU load (compared to the XV overlay) but resulted in very choppy playback, while 720p worked reasonably well [[2]](https://bbs.archlinux.org/viewtopic.php?id=150550). This is echoed by other experiences [[3]](http://www.emmolution.org/?p=192&cpage=1#comment-12292).

### Setting brightness and gamma

See [Backlight](/index.php/Backlight "Backlight").

## Troubleshooting

### SNA issues

From `man 4 intel`:

	_There are a couple of backends available for accelerating the DDX. "UXA" (Unified Acceleration Architecture) is the mature backend that was introduced to support the GEM driver model. It is in the process of being superseded by "SNA" (Sandybridge's New Acceleration). Until that process is complete, the ability to choose which backend to use remains for backwards compatibility._

_SNA_ is the default acceleration method in [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). If you are experience issues with _SNA_ (e.g. pixelated graphics, corrupt text, etc.), try using _UXA_ instead, which can be done by adding the following line to your [configuration file](#Configuration):

```
Option      "AccelMethod"  "uxa"

```

### Blank screen during boot, when "Loading modules"

If using "late start" KMS and the screen goes blank when "Loading modules", it may help to add `i915` and `intel_agp` to the initramfs. See [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") section.

Alternatively, appending the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") seems to work as well:

```
video=SVIDEO-1:d

```

If you need to output to VGA then try this:

```
video=VGA-1:1280x800

```

### X freeze/crash with intel driver

Some issues with X crashing, GPU hanging, or problems with X freezing, can be fixed by disabling the GPU usage with the `NoAccel` option - add the following lines to your [configuration file](#Configuration):

```
  Option "NoAccel" "True"

```

Alternatively, try to disable the 3D acceleration only with the `DRI` option:

```
  Option "DRI" "False"

```

If you experience crashes and have

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

in your configuration file, in most cases these can be fixed by adding

```
i915.semaphores=1

```

to your boot parameters.

If you are using kernel 4.0.X or above on Baytrail architecture and frequently encounter complete system freezes (especially when watching video or using GFX intensivelly), you should try adding the following kernel option as a workaround, until [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) will be fixed permanently.

```
 intel_idle.max_cstate=1

```

### Adding undetected resolutions

This issue is covered on the [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Weathered colors (color range problem)

**Note:** This problem is related to the [changes](http://lists.freedesktop.org/archives/dri-devel/2013-January/033576.html) in the kernel 3.9\. This problem still remains in kernel 4.1.

Kernel 3.9 contains a new default "Automatic" mode for the "Broadcast RGB" property in the Intel driver. It is almost equivalent to "Limited 16:235" (instead of the old default "Full") whenever an HDMI/DP output is in a [CEA mode](http://raspberrypi.stackexchange.com/questions/7332/what-is-the-difference-between-cea-and-dmt). If a monitor does not support signal in limited color range, it will cause weathered colors.

**Note:** Some monitors/TVs support both color range. In that case an option often known as _Black Level_ may need to be adjusted to make them handle the signal correctly.

One can force mode e.g. `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (replace `<HDMI>` with the appropriate output device, verify by running `xrandr`). You can add it into your `.xprofile`, make it executable to run the command before it will start the graphical mode.

**Note:** Some TVs can handle signal in limited range only. Setting Broadcast RGB to "Full" will cause color clipping. You may need to set it to "Limited 16:235" manually to avoid the clipping.

Also there are other related problems which can be fixed editing GPU registers. More information can be found [[4]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) and [[5]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

Unfortunately, the Intel driver does not support setting the color range through an `xorg.conf.d` configuration file.

A [bug report](https://bugzilla.kernel.org/show_bug.cgi?id=94921) is filed and a patch can be found in the attachment.

### Backlight is not adjustable

If after resuming from suspend, the hotkeys for changing the screen brightness do not take effect, check your configuration against the [Backlight](/index.php/Backlight "Backlight") article.

If the problem persists, try one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_osi=Linux
acpi_osi="!Windows 2012"
acpi_osi=

```

### Disabling frame buffer compression

Enabling frame buffer compression on pre-Sandy Bridge CPUs results in endless error messages:

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

The solution is to disable frame buffer compression which will slightly increase power consumption. In order to disable it add `i915.enable_fbc=0` to the kernel line parameters. More information on the results of disabled compression can be found [here](http://zinc.canonical.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/results.txt).

### Corruption/Unresponsiveness in Chromium and Firefox

If you experience corruption or unresponsiveness in Chromium and/or Firefox [set the AccelMethod to "uxa"](#SNA_issues).

### Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips

A few seconds after X/Wayland loads the machine will freeze and journalctl will log a kernel crash referencing the Intel graphics as below:

```
Jun 16 17:54:03 hostname kernel: BUG: unable to handle kernel NULL pointer dereference at           (null)
Jun 16 17:54:03 hostname kernel: IP: [<          (null)>]           (null)
...
Jun 16 17:54:03 hostname kernel: CPU: 0 PID: 733 Comm: gnome-shell Tainted: G     U     O    4.0.5-1-ARCH #1
...
Jun 16 17:54:03 hostname kernel: Call Trace:
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055cc27>] ? i915_gem_object_sync+0xe7/0x190 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0579634>] intel_execlists_submission+0x294/0x4c0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa05539fc>] i915_gem_do_execbuffer.isra.12+0xabc/0x1230 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055d349>] ? i915_gem_object_set_to_cpu_domain+0xa9/0x1f0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ba2ae>] ? __kmalloc+0x2e/0x2a0
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555471>] i915_gem_execbuffer2+0x141/0x2b0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa042fcab>] drm_ioctl+0x1db/0x640 [drm]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555330>] ? i915_gem_execbuffer+0x450/0x450 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff8122339b>] ? eventfd_ctx_read+0x16b/0x200
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebc36>] do_vfs_ioctl+0x2c6/0x4d0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811f6452>] ? __fget+0x72/0xb0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebec1>] SyS_ioctl+0x81/0xa0
Jun 16 17:54:03 hostname kernel:  [<ffffffff8157a589>] system_call_fastpath+0x12/0x17
Jun 16 17:54:03 hostname kernel: Code:  Bad RIP value.
Jun 16 17:54:03 hostname kernel: RIP  [<          (null)>]           (null)

```

This can be fixed by disabling execlist support which was changed to default on with kernel 4.0\. Add the following kernel parameter:

```
i915.enable_execlists=0

```

This is known to be broken to at least kernel 4.0.5.

### Skylake Support

For linux kernels older than 4.3.x, `i915.preliminary_hw_support=1` must be added to your boot parameters for the driver to work on the new Intel Skylake (6th gen.) GPUs. On a fully updated system running kernel 4.3.x and up, this step is unneccesary.

The i915 DRM driver is known to cause various GPU hangs, crashes and even full system freezes. It might be neccesary to disable hardware acceleration to workaround these issues. One solution is to use the following Xorg configuration.

 `/etc/X11/xorg.conf.d/20-intel.conf` 

```
Section "Device"
	Identifier  "Intel Graphics"
	Driver      "intel"
	Option	    "DRI"	"false"
EndSection

```

Otherwise, specific applications such as Chromium and Firefox browsers can be instructed to disable hardware rendering directly.

Another option that seems to work for some users is to add the `i915.enable_rc6=0` kernel boot parameter, which will cause the CPU/GPU to remain in high-power modes, but seems to resolve most cases of GPU hangs and system freezes.

## See also

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (includes a list of supported hardware)
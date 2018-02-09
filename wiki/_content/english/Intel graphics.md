Related articles

*   [Intel GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")
*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Vulkan](/index.php/Vulkan "Vulkan")

Since Intel provides and supports open source drivers, Intel graphics are essentially plug-and-play.

For a comprehensive list of Intel GPU models and corresponding chipsets and CPUs, see [this comparison on Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Note:** PowerVR-based graphics ([GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600") series) are not supported by open source drivers.

## Contents

*   [1 Installation](#Installation)
*   [2 Loading](#Loading)
    *   [2.1 Enable early KMS](#Enable_early_KMS)
    *   [2.2 Enable GuC / HuC firmware loading](#Enable_GuC_.2F_HuC_firmware_loading)
*   [3 Xorg configuration](#Xorg_configuration)
*   [4 Module-based Powersaving Options](#Module-based_Powersaving_Options)
    *   [4.1 RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_.28enable_rc6.29)
    *   [4.2 Framebuffer compression (enable_fbc)](#Framebuffer_compression_.28enable_fbc.29)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Tear-free video](#Tear-free_video)
    *   [5.2 Disable Vertical Synchronization (VSYNC)](#Disable_Vertical_Synchronization_.28VSYNC.29)
    *   [5.3 Setting scaling mode](#Setting_scaling_mode)
    *   [5.4 KMS Issue: console is limited to small area](#KMS_Issue:_console_is_limited_to_small_area)
    *   [5.5 H.264 decoding on GMA 4500](#H.264_decoding_on_GMA_4500)
    *   [5.6 Setting brightness and gamma](#Setting_brightness_and_gamma)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 SNA issues](#SNA_issues)
    *   [6.2 DRI3 issues](#DRI3_issues)
    *   [6.3 Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)](#Font_and_screen_corruption_in_GTK.2B_applications_.28missing_glyphs_after_suspend.2Fresume.29)
    *   [6.4 Blank screen during boot, when "Loading modules"](#Blank_screen_during_boot.2C_when_.22Loading_modules.22)
    *   [6.5 X freeze/crash with intel driver](#X_freeze.2Fcrash_with_intel_driver)
    *   [6.6 Baytrail complete freeze](#Baytrail_complete_freeze)
    *   [6.7 Adding undetected resolutions](#Adding_undetected_resolutions)
    *   [6.8 Weathered colors (color range problem)](#Weathered_colors_.28color_range_problem.29)
    *   [6.9 Backlight is not adjustable](#Backlight_is_not_adjustable)
    *   [6.10 Disabling frame buffer compression](#Disabling_frame_buffer_compression)
    *   [6.11 Corruption/Unresponsiveness in Chromium and Firefox](#Corruption.2FUnresponsiveness_in_Chromium_and_Firefox)
    *   [6.12 Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips](#Kernel_crashing_w.2Fkernels_4.0.2B_on_Broadwell.2FCore-M_chips)
    *   [6.13 Skylake support](#Skylake_support)
    *   [6.14 Lag in Windows guests](#Lag_in_Windows_guests)
    *   [6.15 Screen flickering](#Screen_flickering)
    *   [6.16 OpenGL 2.1 with i915 driver](#OpenGL_2.1_with_i915_driver)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package, which provides the DRI driver for 3D acceleration.

*   For 32-bit application support, also install the [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) package from the [multilib](/index.php/Multilib "Multilib") repository.
*   For the DDX driver (which provides 2D acceleration in [Xorg](/index.php/Xorg "Xorg")), [install](/index.php/Install "Install") the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. (Often not recommended, see note below.)
*   For [Vulkan](/index.php/Vulkan "Vulkan") support (*Ivy Bridge* and newer), install the [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel) package.

Also see [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

**Note:** Some ([Debian & Ubuntu](http://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-Debian-Abandon-Intel-DDX), [Fedora](http://www.phoronix.com/scan.php?page=news_item&px=Fedora-Xorg-Intel-DDX-Switch), [KDE](https://community.kde.org/Plasma/5.9_Errata#Intel_GPUs)) recommend not installing the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver, and instead falling back on the modesetting driver for fourth generation and newer GPUs. See [[1]](https://www.reddit.com/r/archlinux/comments/4cojj9/it_is_probably_time_to_ditch_xf86videointel/), [[2]](http://www.phoronix.com/scan.php?page=article&item=intel-modesetting-2017&num=1), [Xorg#Installation](/index.php/Xorg#Installation "Xorg"), and [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4). However, the modesetting driver can cause problems such as [Chromium Issue 370022](https://bugs.chromium.org/p/chromium/issues/detail?id=370022).

## Loading

The Intel kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since Intel requires kernel mode-setting.
*   Also, check that you have not disabled Intel by using any modprobe blacklisting within `/etc/modprobe.d/` or `/usr/lib/modprobe.d/`.

### Enable early KMS

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by Intel chipsets that use the i915 DRM driver and is mandatory and enabled by default.

Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for instuctions on how to enable KMS as soon as possible at the boot process.

### Enable GuC / HuC firmware loading

For Skylake and newer processors, some video features (e.g. CBR rate control on SKL low-power encoding mode) may require the use of an updated GPU firmware, which is currently (as of 4.14) not enabled by default.

It is necessary to add `i915.enable_guc_loading=1 i915.enable_guc_submission=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to enable it.

You can verify that it's enabled by checking *dmesg*:

```
[    2.142029] [drm] GuC loaded (firmware i915/skl_guc_ver6_1.bin [version 6.1])

```

Alternatively, check:

```
# cat /sys/kernel/debug/dri/0/i915_huc_load_status
# cat /sys/kernel/debug/dri/0/i915_guc_load_status

```

## Xorg configuration

There is no need for any configuration to run [Xorg](/index.php/Xorg "Xorg").

**Note:** The latest generation of integrated GPUs (Skylake/HD 530 for instance) may require additional configuration, see [#Skylake support](#Skylake_support)

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

*   You may need to indicate `Option "AccelMethod"` when creating a configuration file, even just to set it to the default method (currently `"sna"`); otherwise, X may crash.
*   You might need to add more device sections than the one listed above. This will be indicated where necessary.

For the full list of options, see the [intel(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4) man page.

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

You will note that many options default to -1, resulting in per-chip powersaving defaults. It is however possible to configure more aggressive powersaving by using [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules").

**Warning:** Diverting from the defaults will mark the kernel as [tainted](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=fc9740cebc3ab7c65f3c5f6ce0caf3e4969013ca) from Linux 3.18 onwards. This basically implies using other options than the per-chip defaults is considered experimental and not supported by the developers.

The following set of options should be generally safe to enable:

 `/etc/modprobe.d/i915.conf` 
```
options i915 enable_rc6=1 enable_fbc=1 semaphores=1

```

### RC6 sleep modes (enable_rc6)

You can experiment with higher values for `enable_rc6`, but your GPU may not support them or the activation of the other options [[3]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

The available `enable_rc6` values are a bitmask with bit values RC6=1, RC6p=2, RC6pp=4[[4]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/intel_pm.c#n34) - where "RC6p" and "RC6pp" are lower power states.

To confirm the current running RC6 level, you can look in sysfs:

```
# cat /sys/class/drm/card0/power/rc6_enable

```

... if the value read is a lower number than expected, the other RC6 level are probably not supported. Passing `drm.debug=0xe` will add DRM debugging information to the kernel log - possibly including a line like this:

```
[drm:sanitize_rc6_option] Adjusting RC6 mask to 1 (requested 7, valid 1)

```

### Framebuffer compression (enable_fbc)

Framebuffer compression may be unreliable or unavailable on Intel GPU generations before Sandy Bridge (generation 6). This results in messages logged to the system journal similar to this one:

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## Tips and tricks

### Tear-free video

The SNA acceleration method causes tearing for some people. To fix this, enable the `"TearFree"` option in the driver by adding the following line to your [configuration file](#Xorg_configuration):

```
Option "TearFree" "true"

```

See the [original bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) for more info.

**Note:**

*   This option may not work when `SwapbuffersWait` is `false`.
*   This option may increases memory allocation considerably and reduce performance. [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)
*   This option is problematic for applications that are very picky about vsync timing, like [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy").
*   This option does not work with UXA acceleration method, only with SNA.

### Disable Vertical Synchronization (VSYNC)

Useful when:

*   Chomium/Chrome has lags and slow performance due to GPU and runs smoothly with --disable-gpu switch
*   glxgears test does not show desired performance

The intel-driver uses [Triple Buffering](http://www.intel.com/support/graphics/sb/CS-004527.htm) for vertical synchronization, this allows for full performance and avoids tearing. To turn vertical synchronization off (e.g. for benchmarking) use this `.drirc` in your home directory:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

**Warning:** Do not use [driconf](https://www.archlinux.org/packages/?name=driconf) to create this file. It is buggy and will set the wrong driver.

### Setting scaling mode

This can be useful for some full screen applications:

```
$ xrandr --output LVDS1 --set PANEL_FITTING *param*

```

where `*param*` can be:

*   `center`: resolution will be kept exactly as defined, no scaling will be made,
*   `full`: scale the resolution so it uses the entire screen or
*   `full_aspect`: scale the resolution to the maximum possible but keep the aspect ratio.

If it does not work, try:

```
$ xrandr --output LVDS1 --set "scaling mode" *param*

```

where `*param*` is one of `"Full"`, `"Center"` or `"Full aspect"`.

**Note:** This option currently does not work for external displays (e.g. VGA, DVI, HDMI, DP). [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=90989)

### KMS Issue: console is limited to small area

One of the low-resolution video ports may be enabled on boot which is causing the terminal to utilize a small area of the screen. To fix, explicitly disable the port with an i915 module setting with `video=SVIDEO-1:d` in the kernel command line parameter in the bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

If that does not work, try disabling TV1 or VGA1 instead of SVIDEO-1\. Video port names can be listed with [xrandr](/index.php/Xrandr "Xrandr").

### H.264 decoding on GMA 4500

The [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) package provides MPEG-2 decoding only for GMA 4500 series GPUs. The H.264 decoding support is maintained in a separated g45-h264 branch, which can be used by installing [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) package. Note however that this support is experimental and its development has been abandoned. Using the VA-API with this driver on a GMA 4500 series GPU will offload the CPU but may not result in as smooth a playback as non-accelerated playback. Tests using mplayer showed that using vaapi to play back an H.264 encoded 1080p video halved the CPU load (compared to the XV overlay) but resulted in very choppy playback, while 720p worked reasonably well [[7]](https://bbs.archlinux.org/viewtopic.php?id=150550). This is echoed by other experiences [[8]](http://www.emmolution.org/?p=192&cpage=1#comment-12292). Setting the preallocated video ram size higher in bios results in much better hardware decoded playback. Even 1080p h264 works well if this is done. Smooth playback (1080p/720p) works also with [mpv-git](https://aur.archlinux.org/packages/mpv-git/) in combination with [ffmpeg-git](https://aur.archlinux.org/packages/ffmpeg-git/) and [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). With MPV and the Firefox plugin "Watch with MPV"[[9]](https://addons.mozilla.org/de/firefox/addon/watch-with-mpv/) it is possible to watch hardware accelerated YouTube videos.

### Setting brightness and gamma

See [Backlight](/index.php/Backlight "Backlight").

## Troubleshooting

### SNA issues

*SNA* is the default acceleration method in [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). If you experience issues with *SNA* (e.g. pixelated graphics, corrupt text, etc.), try using *UXA* instead, which can be done by adding the following line to your [configuration file](#Xorg_configuration):

```
Option      "AccelMethod"  "uxa"

```

See [intel(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4) under `Option "AccelMethod"`.

### DRI3 issues

*DRI3* is the default DRI version in [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). On some systems this can cause issues such as [this](https://bugs.chromium.org/p/chromium/issues/detail?id=370022). To switch back to *DRI2* add the following line to your [configuration file](#Xorg_configuration):

```
Option "DRI" "2"

```

For the `modesetting` driver, this method of disabling DRI3 does not work. Instead, one can set the environment variable `LIBGL_DRI3_DISABLE=1`.

### Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)

Should you experience missing font glyphs in GTK+ applications, the following workaround might help. [Edit](/index.php/Textedit "Textedit") `/etc/environment` to add the following line:

 `/etc/environment`  `COGL_ATLAS_DEFAULT_BLIT_MODE=framebuffer` 

See also [FreeDesktop bug 88584](https://bugs.freedesktop.org/show_bug.cgi?id=88584).

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

Some issues with X crashing, GPU hanging, or problems with X freezing, can be fixed by disabling the GPU usage with the `NoAccel` option - add the following lines to your [configuration file](#Xorg_configuration):

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

### Baytrail complete freeze

If you are using kernel > 3.16 on Baytrail architecture and randomly encounter total system freezes, the following kernel option is a workaround until [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) is fixed in the linux kernel.

```
intel_idle.max_cstate=1

```

This is originally an Intel CPU bug that can be triggered by certain c-state transitions. It can also happen with Linux kernel 3.16 or Windows, though apparently much more rarely. The kernel option will prevent the freeze by avoiding c-state transitions but will also increase power consumption.

### Adding undetected resolutions

This issue is covered on the [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Weathered colors (color range problem)

Kernel 3.9 [contains](http://lists.freedesktop.org/archives/dri-devel/2013-January/033576.html) a new default "Automatic" mode for the "Broadcast RGB" property in the Intel driver. It is almost equivalent to "Limited 16:235" (instead of the old default "Full") whenever an HDMI/DP output is in a [CEA mode](http://raspberrypi.stackexchange.com/questions/7332/what-is-the-difference-between-cea-and-dmt). If a monitor does not support signal in limited color range, it will cause weathered colors.

**Note:** Some monitors/TVs support both color range. In that case an option often known as *Black Level* may need to be adjusted to make them handle the signal correctly. Some TVs can handle signal in limited range only. Setting Broadcast RGB to "Full" will cause color clipping. You may need to set it to "Limited 16:235" manually to avoid the clipping.

One can force mode e.g. `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (replace `<HDMI>` with the appropriate output device, verify by running `xrandr`).

Unfortunately, the Intel driver does not support setting the color range through an `xorg.conf.d` configuration file.

A [bug report](https://bugzilla.kernel.org/show_bug.cgi?id=94921) is filed and a patch can be found in the attachment.

Also there are other related problems which can be fixed editing GPU registers. More information can be found [[10]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) and [[11]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

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

The solution is to disable frame buffer compression which will imperceptibly increase power consumption (around 0.06 W). In order to disable it add `i915.enable_fbc=0` to the kernel line parameters. More information on the results of disabled compression can be found [here](http://kernel.ubuntu.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/).

### Corruption/Unresponsiveness in Chromium and Firefox

If you experience corruption, unresponsiveness, lags or slow performance in Chromium and/or Firefox:

*   [Set the AccelMethod to "uxa"](#SNA_issues)
*   [Disable VSYNC](#Disable_Vertical_Synchronization_.28VSYNC.29)

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

This can be fixed by disabling execlist support which was changed to default on with kernel 4.0\. Add the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
i915.enable_execlists=0

```

This is known to be broken to at least kernel 4.0.5.

### Skylake support

The i915 DRM driver is known to cause various GPU hangs, crashes and even full system freezes. It might be necessary to disable hardware acceleration to workaround these issues. One solution is to use the following Xorg configuration.

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

**Note:** If the system appears to hang after "Loading Initial Ramdisk", make sure that the IGD aperture size in BIOS is less than 4GB.

### Lag in Windows guests

The video output of a Windows guest in VirtualBox sometimes hangs until the host forces a screen update (e.g. by moving the mouse cursor). Removing the `enable_fbc=1` option fixes this issue.

### Screen flickering

The following power saving features used by intel iGPUs are known to cause flickering in some instances. A temporary solution is to disable one of them using the appropriate [kernel boot parameter](/index.php/Kernel_parameters "Kernel parameters") option:

*   Rc6 sleep modes (see [#RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_.28enable_rc6.29)), can be disabled with `i915.enable_rc6=0`.

*   Panel Self Refresh (PSR) [FS#49628](https://bugs.archlinux.org/task/49628) [FS#49371](https://bugs.archlinux.org/task/49371) [FS#50605](https://bugs.archlinux.org/task/50605), enabled by default since kernel mainline 4.6\. To disable this feature use the option `i915.enable_psr=0`.

### OpenGL 2.1 with i915 driver

The update of [mesa](https://www.archlinux.org/packages/?name=mesa) from version 13.x to 17 may break support for OpenGL 2.1 on third gen Intel GPUs (GMA3100, see [here](https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units#Third_generation "wikipedia:List of Intel graphics processing units")), as described in this [article](http://www.phoronix.com/scan.php?page=news_item&px=Mesa-i915-OpenGL-2-Drop), reverting it back to OpenGL 1.4\. However this could be restored manually by setting `/etc/drirc` or `~/.drirc` options like :

 `/etc/drirc` 
```
<driconf>
...
    <device driver="i915">
        <application name="Default">
            <option name="**stub_occlusion_query**" value="**true**" />
            <option name="**fragment_shader**" value="**true**" />
        </application>
    </device>
...
</driconf>
```

**Note:** the reason of this step back was Chromium and other apps bad experience. If needed, you might edit the drirc file in a "app-specific" style, see [here](https://dri.freedesktop.org/wiki/ConfigurationInfrastructure/), to disable gl2.1 on executable chromium for instance.

## See also

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (includes a list of supported hardware)
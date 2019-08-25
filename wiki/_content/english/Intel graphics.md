Related articles

*   [Intel GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")
*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Vulkan](/index.php/Vulkan "Vulkan")

Since Intel provides and supports open source drivers, Intel graphics are essentially plug-and-play.

For a comprehensive list of Intel GPU models and corresponding chipsets and CPUs, see [Wikipedia:List of Intel graphics processing units](https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units "wikipedia:List of Intel graphics processing units").

**Note:** PowerVR-based graphics ([GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600") series) are not supported by open source drivers.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Loading](#Loading)
    *   [2.1 Enable early KMS](#Enable_early_KMS)
    *   [2.2 Enable GuC / HuC firmware loading](#Enable_GuC_/_HuC_firmware_loading)
*   [3 Xorg configuration](#Xorg_configuration)
*   [4 Module-based options](#Module-based_options)
    *   [4.1 Framebuffer compression (enable_fbc)](#Framebuffer_compression_(enable_fbc))
    *   [4.2 Fastboot](#Fastboot)
    *   [4.3 Intel GVT-g graphics virtualization support](#Intel_GVT-g_graphics_virtualization_support)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Setting scaling mode](#Setting_scaling_mode)
    *   [5.2 Hardware accelerated H.264 decoding on GMA 4500](#Hardware_accelerated_H.264_decoding_on_GMA_4500)
    *   [5.3 Setting brightness and gamma](#Setting_brightness_and_gamma)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Tearing](#Tearing)
    *   [6.2 Disable Vertical Synchronization (VSYNC)](#Disable_Vertical_Synchronization_(VSYNC))
    *   [6.3 SNA issues](#SNA_issues)
    *   [6.4 DRI3 issues](#DRI3_issues)
    *   [6.5 Font and screen corruption in GTK applications (missing glyphs after suspend/resume)](#Font_and_screen_corruption_in_GTK_applications_(missing_glyphs_after_suspend/resume))
    *   [6.6 Blank screen during boot, when "Loading modules"](#Blank_screen_during_boot,_when_"Loading_modules")
    *   [6.7 X freeze/crash with intel driver](#X_freeze/crash_with_intel_driver)
    *   [6.8 Baytrail complete freeze](#Baytrail_complete_freeze)
    *   [6.9 Adding undetected resolutions](#Adding_undetected_resolutions)
    *   [6.10 Backlight is not adjustable](#Backlight_is_not_adjustable)
    *   [6.11 Corruption/Unresponsiveness in Chromium and Firefox](#Corruption/Unresponsiveness_in_Chromium_and_Firefox)
    *   [6.12 Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips](#Kernel_crashing_w/kernels_4.0+_on_Broadwell/Core-M_chips)
    *   [6.13 Lag in Windows guests](#Lag_in_Windows_guests)
    *   [6.14 Screen flickering](#Screen_flickering)
    *   [6.15 OpenGL 2.1 with i915 driver](#OpenGL_2.1_with_i915_driver)
    *   [6.16 KMS Issue: console is limited to small area](#KMS_Issue:_console_is_limited_to_small_area)
    *   [6.17 Weathered colors (color range problems)](#Weathered_colors_(color_range_problems))
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package, which provides the [DRI](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure "wikipedia:Direct Rendering Infrastructure") driver for 3D acceleration.

*   For 32-bit application support, also install the [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) package from the [multilib](/index.php/Multilib "Multilib") repository.
*   For the [DDX](https://en.wikipedia.org/wiki/X.Org_Server#DDX "wikipedia:X.Org Server") driver (which provides 2D acceleration in [Xorg](/index.php/Xorg "Xorg")), [install](/index.php/Install "Install") the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. (Often not recommended, see note below.)
*   For [Vulkan](/index.php/Vulkan "Vulkan") support (*Ivy Bridge* and newer), install the [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel) package.

Also see [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

**Note:** Some ([Debian & Ubuntu](http://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-Debian-Abandon-Intel-DDX), [Fedora](http://www.phoronix.com/scan.php?page=news_item&px=Fedora-Xorg-Intel-DDX-Switch), [KDE](https://community.kde.org/Plasma/5.9_Errata#Intel_GPUs)) recommend not installing the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver, and instead falling back on the modesetting driver for fourth generation and newer GPUs. See [[1]](https://www.reddit.com/r/archlinux/comments/4cojj9/it_is_probably_time_to_ditch_xf86videointel/), [[2]](http://www.phoronix.com/scan.php?page=article&item=intel-modesetting-2017&num=1), [Xorg#Installation](/index.php/Xorg#Installation "Xorg"), and [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4). However, the modesetting driver can cause problems such as [Chromium Issue 370022](https://bugs.chromium.org/p/chromium/issues/detail?id=370022). Also, the modesetting driver will not be benefited by Intel GuC/HuC/DMC firmware.

## Loading

The Intel kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since Intel requires kernel mode-setting.
*   Also, check that you have not disabled Intel by using any modprobe blacklisting within `/etc/modprobe.d/` or `/usr/lib/modprobe.d/`.

### Enable early KMS

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by Intel chipsets that use the i915 DRM driver and is mandatory and enabled by default.

Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for instructions on how to enable KMS as soon as possible at the boot process.

### Enable GuC / HuC firmware loading

For Skylake and newer processors, some video features (e.g. CBR rate control on SKL low-power encoding mode) may require the use of an updated GPU firmware, which is currently (as of 4.16) not enabled by default. Enabling GuC/HuC firmware loading can cause issues on some systems; disable it if you experience freezing (for example, after resuming from hibernation).

**Note:** See [Gentoo:Intel#Feature support](https://wiki.gentoo.org/wiki/Intel#Feature_support "gentoo:Intel") for an overview of Intel processor generations.

For those processors it is necessary to add `i915.enable_guc=2` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to enable both GuC and HuC firmware loading. Alternatively, if the [initramfs](/index.php/Initramfs "Initramfs") already includes the `i915` module (see [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting")), you can set these options through a file in `/etc/modprobe.d/`, e.g.:

 `/etc/modprobe.d/i915.conf`  `options i915 enable_guc=2` 
**Note:** It is possible to enable both GuC/HuC firmware loading and GuC submission by using the `enable_guc=3` module parameter, although this is generally discouraged and may even negatively affect your system stability.

You can verify both are enabled by using [dmesg](/index.php/Dmesg "Dmesg"):

 `$ dmesg` 
```
[drm] HuC: Loaded firmware i915/kbl_huc_ver02_00_1810.bin (version 2.0)
[drm] GuC: Loaded firmware i915/kbl_guc_ver9_39.bin (version 9.39)
i915 0000:00:02.0: GuC firmware version 9.39
i915 0000:00:02.0: GuC submission enabled
i915 0000:00:02.0: HuC enabled
```

Alternatively, check using:

```
# cat /sys/kernel/debug/dri/0/i915_huc_load_status
# cat /sys/kernel/debug/dri/0/i915_guc_load_status

```

**Warning:** Using [GVT-g graphics virtualization](/index.php/Intel_GVT-g "Intel GVT-g") by setting `enable_gvt=1` is not supported as of linux 4.20.11 when GuC/HuC is also enabled. The i915 module would fail to initialize as shown in system journal. `$ journalctl` 
```
... kernel: [drm:intel_gvt_init [i915]] *ERROR* i915 GVT-g loading failed due to Graphics virtualization is not yet supported with GuC submission
... kernel: i915 0000:00:02.0: [drm:i915_driver_load [i915]] Device initialization failed (-5)
... kernel: i915: probe of 0000:00:02.0 failed with error -5
... kernel: snd_hda_intel 0000:00:1f.3: failed to add i915 component master (-19)

```

## Xorg configuration

There may be no need for any configuration to run [Xorg](/index.php/Xorg "Xorg").

However, if [Xorg](/index.php/Xorg "Xorg") does not start, and to take advantage of some driver options, you can create an Xorg configuration file similar to the one below:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "OutputClass"
  Identifier "Intel Graphics"
  MatchDriver "i915"
  Driver "intel"
EndSection
```

Additional options are added by the user on new lines below `Driver`. For the full list of options, see the [intel(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4) man page.

**Note:**

*   You may need to indicate `Option "AccelMethod"` when creating a configuration file, even just to set it to the default method (currently `"sna"`); otherwise, X may crash.
*   You might need to add more device sections than the one listed above. This will be indicated where necessary.

## Module-based options

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

### Framebuffer compression (enable_fbc)

Making use of Framebuffer compression (FBC) can reduce power consumption while reducing memory bandwidth needed for screen refreshes.

To enable FBC, use `i915.enable_fbc=1` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or set in `/etc/modprobe.d/i915.conf`:

 `/etc/modprobe.d/i915.conf`  `options i915 enable_fbc=1` 
**Note:** Framebuffer compression may be unreliable or unavailable on Intel GPU generations before Sandy Bridge (generation 6). This results in messages logged to the system journal similar to this one:
```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

Enabling frame buffer compression on pre-Sandy Bridge CPUs results in endless error messages:

 `$ dmesg` 
```
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```
The solution is to disable frame buffer compression which will imperceptibly increase power consumption (around 0.06 W). In order to disable it add `i915.enable_fbc=0` to the kernel line parameters. More information on the results of disabled compression can be found [here](http://kernel.ubuntu.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/).

### Fastboot

The goal of Intel Fastboot is to preserve the frame-buffer as setup by the BIOS or [bootloader](/index.php/Bootloader "Bootloader") to avoid any flickering until [Xorg](/index.php/Xorg "Xorg") has started [[3]](https://www.phoronix.com/scan.php?page=news_item&px=MTEwNzc).

To enable fastboot, set `i915.fastboot=1` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or set in `/etc/modprobe.d/i915.conf`:

 `/etc/modprobe.d/i915.conf`  `options i915 fastboot=1` 
**Warning:** This parameter is not enabled by default and may cause issues on some older (pre-Skylake) systems.[[4]](https://www.phoronix.com/scan.php?page=news_item&px=Intel-Fastboot-Default-2019-Try)

### Intel GVT-g graphics virtualization support

See [Intel GVT-g](/index.php/Intel_GVT-g "Intel GVT-g") for details.

## Tips and tricks

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

**Note:** This option currently does not work for external displays (e.g. VGA, DVI, HDMI, DP). [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=90989)

### Hardware accelerated H.264 decoding on GMA 4500

The [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) package only provides hardware accelerated MPEG-2 decoding for GMA 4500 series GPUs. The H.264 decoding support is maintained in a separated g45-h264 branch, which can be used by installing [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/) package. Note however that this support is experimental and its development has been abandoned. Using the VA-API with this driver on a GMA 4500 series GPU will offload the CPU but may not result in as smooth a playback as non-accelerated playback. Tests using mplayer showed that using vaapi to play back an H.264 encoded 1080p video halved the CPU load (compared to the XV overlay) but resulted in very choppy playback, while 720p worked reasonably well [[6]](https://bbs.archlinux.org/viewtopic.php?id=150550). This is echoed by other experiences [[7]](http://www.emmolution.org/?p=192&cpage=1#comment-12292). Setting the preallocated video ram size higher in bios results in much better hardware decoded playback. Even 1080p h264 works well if this is done. Smooth playback (1080p/720p) works also with [mpv-git](https://aur.archlinux.org/packages/mpv-git/) in combination with [ffmpeg-git](https://aur.archlinux.org/packages/ffmpeg-git/) and [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). With MPV and the Firefox plugin "Watch with MPV"[[8]](https://addons.mozilla.org/de/firefox/addon/watch-with-mpv/) it is possible to watch hardware accelerated YouTube videos.

### Setting brightness and gamma

See [Backlight](/index.php/Backlight "Backlight").

## Troubleshooting

### Tearing

The SNA acceleration method causes tearing on some machines. To fix this, enable the `"TearFree"` option in the driver by adding the following line to your [configuration file](#Xorg_configuration):

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "OutputClass"
  Identifier "Intel Graphics"
  MatchDriver "i915"
  Driver "intel"
  Option "TearFree" "true"
EndSection
```

See the [original bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) for more info.

**Note:**

*   This option may not work when `SwapbuffersWait` is `false`.
*   This option may increases memory allocation considerably and reduce performance. [[9]](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)
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

**Note:** Do not use [driconf](https://aur.archlinux.org/packages/driconf/) to create this file. It is buggy and will set the wrong driver.

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

### Font and screen corruption in GTK applications (missing glyphs after suspend/resume)

Should you experience missing font glyphs in GTK applications, the following workaround might help. [Edit](/index.php/Textedit "Textedit") `/etc/environment` to add the following line:

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

### Baytrail complete freeze

If you are using kernel > 3.16 on Baytrail architecture and randomly encounter total system freezes, the following kernel option is a workaround until [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) is fixed in the linux kernel.

```
intel_idle.max_cstate=1

```

This is originally an Intel CPU bug that can be triggered by certain c-state transitions. It can also happen with Linux kernel 3.16 or Windows, though apparently much more rarely. The kernel option will prevent the freeze by avoiding c-state transitions but will also increase power consumption.

### Adding undetected resolutions

This issue is covered on the [Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Backlight is not adjustable

If after resuming from suspend, the hotkeys for changing the screen brightness do not take effect, check your configuration against the [Backlight](/index.php/Backlight "Backlight") article.

If the problem persists, try one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_osi=Linux
acpi_osi="!Windows 2012"
acpi_osi=

```

Also make sure you are not using fastboot mode (i915.fastboot kernel parameter), it is [known](https://www.phoronix.com/forums/forum/software/mobile-linux/1066447-arch-linux-users-with-intel-graphics-can-begin-enjoying-a-flicker-free-boot) for breaking backlight controls.

### Corruption/Unresponsiveness in Chromium and Firefox

If you experience corruption, unresponsiveness, lags or slow performance in Chromium and/or Firefox:

*   [Set the AccelMethod to "uxa"](#SNA_issues)
*   [Disable VSYNC](#Disable_Vertical_Synchronization_(VSYNC))

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

### Lag in Windows guests

The video output of a Windows guest in VirtualBox sometimes hangs until the host forces a screen update (e.g. by moving the mouse cursor). Removing the `enable_fbc=1` option fixes this issue.

### Screen flickering

Panel Self Refresh (PSR), a power saving feature used by Intel iGPUs is known to cause flickering in some instances [FS#49628](https://bugs.archlinux.org/task/49628) [FS#49371](https://bugs.archlinux.org/task/49371) [FS#50605](https://bugs.archlinux.org/task/50605). A temporary solution is to disable this feature using the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `i915.enable_psr=0`.

### OpenGL 2.1 with i915 driver

The update of [mesa](https://www.archlinux.org/packages/?name=mesa) from version 13.x to 17 may break support for OpenGL 2.1 on third gen Intel GPUs (GMA3100, see [here](https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units#Third_generation "wikipedia:List of Intel graphics processing units")), as described in this [article](http://www.phoronix.com/scan.php?page=news_item&px=Mesa-i915-OpenGL-2-Drop), reverting it back to OpenGL 1.4\. However this could be restored manually by setting `/etc/drirc` or `~/.drirc` options like:

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

### KMS Issue: console is limited to small area

One of the low-resolution video ports may be enabled on boot which is causing the terminal to utilize a small area of the screen. To fix, explicitly disable the port with an i915 module setting with `video=SVIDEO-1:d` in the kernel command line parameter in the bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

If that does not work, try disabling TV1 or VGA1 instead of SVIDEO-1\. Video port names can be listed with [xrandr](/index.php/Xrandr "Xrandr").

### Weathered colors (color range problems)

The "Broadcast RGB" property in the Intel driver defines the color range which can be used by the display - either "Limited 16:235" (which limits the color range for some displays that can't properly display all colors) and "Full". Since kernel 3.9, the new default property "Automatic" tries to determine whenever the display supports the full color range, and if it doesn't/detection fails, color range falls back to "Limited 16:235". This results in weathered colors and grey blacks. On some displays/connectors, despite the full color range being supported properly, automatic detection fails and falls back to the limited color range ([upstream bug report, kernels 4.18-4.20](https://bugs.freedesktop.org/show_bug.cgi?id=108821)).

You can forcefully set the desired color range by running `xrandr --output <OUT> --set "Broadcast RGB" "Full"` (replace `<OUT>` with the appropriate output device, listed by running `xrandr`). There is no way to persist this setting in `xorg.conf`.

## See also

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (includes a list of supported hardware)
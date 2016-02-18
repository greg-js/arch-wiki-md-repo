Kernel [Mode Setting](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting") (KMS) is a method for setting display resolution and depth in the kernel space rather than user space.

The Linux kernel's implementation of KMS enables native resolution in the framebuffer and allows for instant console (tty) switching. KMS also enables newer technologies (such as DRI2) which will help reduce artifacts and increase 3D performance, even kernel space power-saving.

**Note:** The proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") and [catalyst](/index.php/Catalyst "Catalyst") drivers also implement kernel mode-setting, but as they do not use the built-in kernel implementation, they lack an fbdev driver for the high-resolution console.

## Contents

*   [1 Background](#Background)
*   [2 Installation](#Installation)
    *   [2.1 Late KMS start](#Late_KMS_start)
    *   [2.2 Early KMS start](#Early_KMS_start)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 My fonts are too tiny](#My_fonts_are_too_tiny)
    *   [3.2 Problem upon bootloading and dmesg](#Problem_upon_bootloading_and_dmesg)
*   [4 Forcing modes and EDID](#Forcing_modes_and_EDID)
*   [5 Disabling modesetting](#Disabling_modesetting)

## Background

Previously, setting up the video card was the job of the X server. Because of this, it was not easily possible to have fancy graphics in virtual consoles. Also, each time a switch from X to a virtual console was made (`Ctrl+Alt+F1`), the server had to give control over the video card to the kernel, which was slow and caused flickering. The same "painful" process happened when the control was given back to the X server (`Ctrl+Alt+F7`).

With Kernel Mode Setting (KMS), the kernel is now able to set the mode of the video card. This makes fancy graphics during bootup, virtual console and X fast switching possible, among other things.

## Installation

At first, note that for *any* method you use, you should *always* disable:

*   Any `vga=` options in your bootloader as these will conflict with the native resolution enabled by KMS.
*   Any `video=` lines that enable a framebuffer that conflicts with the driver.
*   Any other framebuffer drivers (such as [uvesafb](/index.php/Uvesafb "Uvesafb")).

### Late KMS start

[Intel](/index.php/Intel "Intel"), [Nouveau](/index.php/Nouveau "Nouveau"), [ATI](/index.php/ATI "ATI") and [AMDGPU](/index.php/AMDGPU "AMDGPU") drivers already enable KMS automatically for all chipsets, so you need not install it manually.

The proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") and [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") drivers do not support KMS. In order to use KMS you should replace them with open source drivers.

### Early KMS start

To load KMS as early as possible in boot process, add the module `radeon`/`amdgpu` (for ATI/AMD cards), `i915` (for Intel integrated graphics) or `nouveau` (for Nvidia cards) to the `MODULES` line in `/etc/mkinitcpio.conf`. For example:

 `/etc/mkinitcpio.conf`  `MODULES="... i915 ..."` 
**Note:** Intel users might need to add `intel_agp` before `i915` to suppress the ACPI errors.

If you are using a custom EDID file (not applicable for the built-in resolutions), you should embed it into initramfs as well:

 `/etc/mkinitcpio.conf`  `FILES="/usr/lib/firmware/edid/your_edid.bin"` 

Rebuild your kernel image (refer to the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") article for more info):

```
# mkinitcpio -p <name of your kernel preset; e.g. *linux*>

```

## Troubleshooting

### My fonts are too tiny

See [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") for how to change your console font to a large font. The Terminus font ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)) is available in many sizes, including larger sizes.

### Problem upon bootloading and dmesg

Polling for connected display devices on older systems can be quite expensive. Poll will happen periodically and can in worst cases take several hundred milliseconds, depending on the hardware. This will cause visible stalls, for example in video playback. These stalls might happen even when your video is on HDP output but you have other non HDP outputs in your hw configuration. If you experience stalls in display output occurring every 10 seconds, disabling polling might help.

If you see an error code of `0x00000010 (2)` while booting up, (you will get about 10 lines of text, the last part denoting that error code), use:

 `/etc/modprobe.d/modprobe.conf`  `options drm_kms_helper poll=0` 

## Forcing modes and EDID

In case that your monitor/TV is not sending the appropriate [EDID](https://en.wikipedia.org/wiki/EDID "wikipedia:EDID") or similar problems, you will notice that the native resolution is not automatically configured or no display at all. The kernel has a provision to load the binary EDID data, and provides as well data to set four of the most typical resolutions.

If you have the EDID file for your monitor the process is easy. If you do not have, you can either use one of the built-in resolution-EDID binaries (or generate one during kernel compilation, [more info here](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/EDID/HOWTO.txt)) or build your own EDID.

In case you have an EDID file (e.g. extracted from Windows drivers for your monitor or using `get-edid` command from [read-edid](https://www.archlinux.org/packages/?name=read-edid)), create a dir `edid` under `/usr/lib/firmware`:

```
# mkdir /usr/lib/firmware/edid

```

and then copy your binary into the `/usr/lib/firmware/edid` directory.

To load it at boot, specify the following in the [kernel command line](/index.php/Kernel_command_line "Kernel command line"):

```
drm_kms_helper.edid_firmware=edid/your_edid.bin

```

You can also specify it only for a specified connection:

```
drm_kms_helper.edid_firmware=VGA-1:edid/your_edid.bin

```

For the four built-in resolutions, see table below for the name to specify:

| **Resolution** | **Name to specify** |
| 1024x768 | edid/1024x768.bin |
| 1280x1024 | edid/1280x1024.bin |
| 1600x1200 (kernel 3.10 or higher) | edid/1600x1200.bin |
| 1680x1050 | edid/1680x1050.bin |
| 1920x1080 | edid/1920x1080.bin |

If you are doing early KMS, you must include the custom EDID file in the [initramfs](#Early_KMS_start) or you will run into problems.

You can also construct your own EDID with the makefile included in the `Documentation/EDID` sources of the kernel. The full information can be read [here](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/EDID/HOWTO.txt) and [there](https://www.osadl.org/Single-View.111+M591850c02b5.0.html).

**Warning:** The method described below is somehow incomplete because e.g. Xorg does not take into account the resolution specified, so users are encouraged to use the method described above; however, specifying resolution with `video=` command line may be useful in some scenarios

From [the nouveau wiki](http://nouveau.freedesktop.org/wiki/KernelModeSetting):

A mode can be forced on the kernel command line. Unfortunately, the command line option video is poorly documented in the DRM case. Bits and pieces on how to use it can be found in

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

The format is:

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

*   <conn>: Connector, e.g. DVI-I-1, see `/sys/class/drm/` for available connectors
*   <xres> x <yres>: resolution
*   M: compute a CVT mode?
*   R: reduced blanking?
*   -<bpp>: color depth
*   @<refresh>: refresh rate
*   i: interlaced (non-CVT mode)
*   m: margins?
*   e: output forced to on
*   d: output forced to off
*   D: digital output forced to on (e.g. DVI-I connector)

You can override the modes of several outputs using "video" several times, for instance, to force DVI to 1024x768 at 85 Hz and TV-out off:

```
video=DVI-I-1:1024x768@85 video=TV-1:d

```

To get the name and current status of connectors, you can use the following shell oneliner:

 `$ for p in /sys/class/drm/*/status; do con=${p%/status}; echo -n "${con#*/card?-}: "; cat $p; done` 
```

DVI-I-1: connected
HDMI-A-1: disconnected
VGA-1: disconnected

```

## Disabling modesetting

You may want to disable KMS for various reasons, such as getting a blank screen or a "no signal" error from the display, when using the Catalyst driver, etc. To disable KMS add `nomodeset` as a kernel parameter. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

Along with `nomodeset` kernel parameter, for Intel graphics card you need to add `i915.modeset=0` and for Nvidia graphics card you need to add `nouveau.modeset=0`. For Nvidia Optimus dual-graphics system, you need to add all the three kernel parameters (i.e. `"nomodeset i915.modeset=0 nouveau.modeset=0"`).

**Note:** Some [Xorg](/index.php/Xorg "Xorg") drivers will not work with KMS disabled. See the wiki page on your specific driver for details.
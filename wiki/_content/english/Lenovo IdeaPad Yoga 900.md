| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Wireless | Working | iwlwifi |
| Audio | Working |
| Touchpad | Working | xf86-input-libinput |
| Touchscreen | Working | xf86-input-libinput |
| Camera | Working |
| Card Reader | Working |
| Bluetooth | Working | btusb |

The [Lenovo Yoga 900](http://shop.lenovo.com/us/en/laptops/yoga/900-series/yoga-900-13/#tab-tech_specs) is a 2 in 1 laptop with a QHD+ display.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 Font Size](#Font_Size)
    *   [1.3 Wifi](#Wifi)
*   [2 Configuration](#Configuration)
    *   [2.1 Keyboard](#Keyboard)
    *   [2.2 KVM](#KVM)
    *   [2.3 HiDPI](#HiDPI)
    *   [2.4 Sensors](#Sensors)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Card Reader](#Card_Reader)
    *   [3.2 External Monitor](#External_Monitor)
    *   [3.3 Networking =](#Networking_.3D)
    *   [3.4 Toggle Trackpad](#Toggle_Trackpad)
    *   [3.5 Screen Rotation](#Screen_Rotation)
    *   [3.6 Light Sensor](#Light_Sensor)

## Installation

### BIOS

Lenovo does not currently offer a BIOS update ISO image. This means you can only upgrade the BIOS from Windows 10.

### Font Size

The console text is hard to read during install with this high resolution screen. You can temporarily use a default larger font like sun12x22.

 `setfont sun12x22` 

Consider installing the [Terminus](https://www.archlinux.org/packages/community/any/terminus-font/) font package for access to even larger fonts and making it permanent with vconsole.conf ([Fonts#Persistent configuration](/index.php/Fonts#Persistent_configuration "Fonts")).

### Wifi

During install the wifi-menu may show no networks. This is caused by a soft-block. Using rfkill should fix the issue.

 `rfkill unblock all` 

## Configuration

### Keyboard

**Note:**

*   BIOS has a setting to flip the behavior of the FN key.
*   The status below is based on Gnome

| Keys | Function | Status |
| `Fn+F1` | Audio mute/unmute | Working |
| `Fn+F2` | Audio volume down | Working |
| `Fn+F3` | Audio volume up | Working |
| `Fn+F4` | Close application | Working |
| `Fn+F5` | Refresh page | Working |
| `Fn+F6` | Disable Touchpad | Not Working |
| `Fn+F7` | Airplane mode | Working |
| `Fn+F8` | Display active apps | Not Working |
| `Fn+F9` | Turn off LCD | Working |
| `Fn+F10` | Toggle display | Working |
| `Fn+F11` | Dim LCD backlight | Working |
| `Fn+F12` | Brighten LCD backlight | Working |
| `Fn+Space` | Toggle keyboard backlight | Working |

### KVM

KVM can be enabled in the BIOS via the *Intel Virtual Technology* option.

### HiDPI

See [HiDPI](/index.php/HiDPI "HiDPI").

### Sensors

Install the [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) to get the accelerometer and light sensor working

## Troubleshooting

### Card Reader

Initial testing shows the card read working fine out of the box. There are a few errors on boot that need more research.

Boot message:

 `kernel: mmc0: Unknown controller version (3). You may experience problems.` 

Insert of card message:

```
kernel: sdhci: Timeout waiting for Buffer Read Ready interrupt during tuning procedure, falling back to fixed sampling clock
kernel: mmc0: tuning execution failed
kernel: mmc0: ddr50 tuning failed
```

### External Monitor

**Note:** Updating to the latest [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) and [linux](https://www.archlinux.org/packages/?name=linux) kernel has fixed some of the external display issues with VGA and HDMI dongles.

Several issues occur when trying to display on an external monitor. This laptop only has a display port over USBC-C, which requires dongles to connect to most monitors. Testing to a monitor with a display port connection has yielded the best result. Testing with HDMI and VGA dongles have revealed several issues. Often xrandr does not show a display connected. Rebooting with the monitor attached does not fix the issue. Sometimes running xrandr several times will show a connection.

If you try to force xrandr to display with the following:

 `xrandr --output eDP1 --auto --output DP1 --auto --right-of eDP1` 

Sometimes you will see the following kernel message:

```
 kernel: ------------[ cut here ]------------
 kernel: WARNING: CPU: 1 PID: 1253 at drivers/gpu/drm/i915/intel_pm.c:3553 skl_update_other_pipe_wm+0x177/0x180 [i915]()
 kernel: WARN_ON(!wm_changed)
 kernel: Modules linked in:
 kernel:  ccm snd_hda_codec_hdmi deflate ctr twofish_generic twofish_avx_x86_64 twofish_x86_64_3way twofish_x86_64 twofish_
 kernel:  hid_rmi ax88179_178a usbnet mii iwlmvm mac80211 snd_soc_skl snd_soc_skl_ipc i2c_designware_platform i2c_designwar
 kernel:  fan i2c_hid thermal wmi battery bluetooth intel_hid int3400_thermal rfkill pinctrl_sunrisepoint pinctrl_intel int
 kernel: 
 kernel: CPU: 1 PID: 1253 Comm: Xorg Tainted: G     U  W  O    4.5.2-1-ARCH #1
 kernel: Hardware name: LENOVO 80MK/VIUU4, BIOS C6CN35WW 12/17/2015
 kernel:  0000000000000286 000000000f1007b6 ffff88044bf4f918 ffffffff812dad91
 kernel:  ffff88044bf4f960 ffffffffa01b8d20 ffff88044bf4f950 ffffffff81078e52
 kernel:  ffff8804604ec000 ffff88044bf4f9dc ffff88045d629bd4 ffff8804604eb000
 kernel: Call Trace:
 kernel:  [<ffffffff812dad91>] dump_stack+0x63/0x82
 kernel:  [<ffffffff81078e52>] warn_slowpath_common+0x82/0xc0
 kernel:  [<ffffffff81078eec>] warn_slowpath_fmt+0x5c/0x80
 kernel:  [<ffffffffa00e77c7>] skl_update_other_pipe_wm+0x177/0x180 [i915]
 kernel:  [<ffffffffa00e795e>] skl_update_wm+0x18e/0x5f0 [i915]
 kernel:  [<ffffffffa01725ff>] ? intel_ddi_enable_transcoder_func+0x17f/0x260 [i915]
 kernel:  [<ffffffffa00eb06e>] intel_update_watermarks+0x1e/0x30 [i915]
 kernel:  [<ffffffffa0155e61>] haswell_crtc_enable+0x321/0x8c0 [i915]
 kernel:  [<ffffffffa0151777>] intel_atomic_commit+0x737/0x1870 [i915]
 kernel:  [<ffffffffa0020581>] ? drm_atomic_check_only+0x181/0x600 [drm]
 kernel:  [<ffffffffa0020a37>] drm_atomic_commit+0x37/0x60 [drm]
 kernel:  [<ffffffffa00908b6>] drm_atomic_helper_set_config+0x76/0xb0 [drm_kms_helper]
 kernel:  [<ffffffffa000f1b2>] drm_mode_set_config_internal+0x62/0x100 [drm]
 kernel:  [<ffffffffa00142c0>] drm_mode_setcrtc+0x3e0/0x500 [drm]
 kernel:  [<ffffffffa0005892>] drm_ioctl+0x152/0x540 [drm]
 kernel:  [<ffffffffa0013ee0>] ? drm_mode_setplane+0x1b0/0x1b0 [drm]
 kernel:  [<ffffffff811ece7c>] ? __vfs_write+0xcc/0x100
 kernel:  [<ffffffff811ffdd1>] do_vfs_ioctl+0xa1/0x5b0
 kernel:  [<ffffffff81084df1>] ? __set_task_blocked+0x41/0xa0
 kernel:  [<ffffffff8120a1f7>] ? __fget+0x77/0xb0
 kernel:  [<ffffffff81200359>] SyS_ioctl+0x79/0x90
 kernel:  [<ffffffff8108793e>] ? SyS_rt_sigprocmask+0x8e/0xc0
 kernel:  [<ffffffff815b0b6e>] entry_SYSCALL_64_fastpath+0x12/0x6d
 kernel: ---[ end trace 4d86447ef15dd94e ]---

```

### Networking =

### Toggle Trackpad

**Note:** This fix has an unintended consequence that needs more research. The mapping will work and it disables the trackpad when you go into tablet mode. The issue is the trackpad will be automatically disabled if you close the laptop lid and re-open it. This requires you to hit F6 to re-enable it. Not mapping this key will leave the trackpad enabled in tablet mode, but otherwise all other operations are normal.

The trackpad key (F6) is not mapped correctly to toggle the trackpad. Using UDEV to [Map_scancodes_to_keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes") will restore this function. This is a custom hwdb file to restore the feature.

```
# Lenovo YOGA 900-13ISK
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*:pvrLenovoYOGA900*
 KEYBOARD_KEY_bf=f21                                   # Fn+F6 Disable Touchpad

```

### Screen Rotation

When you first boot the screen rotation may not work. A bug currently requires you to suspend and resume the laptop before the screen will rotate using the [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) package.

### Light Sensor

When you first boot the light sensor for automatic screen brightness may not work. A bug currently requires you to suspend and resume the laptop before the light sensor will work using the [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) package.
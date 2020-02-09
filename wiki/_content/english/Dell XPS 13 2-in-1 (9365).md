Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")

The Dell XPS 13 2-in-1 (9365) is the early 2017 model. It can be used like a tablet when folding the display on the back. The touchscreen works out of the box.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 BIOS configuration](#BIOS_configuration)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Suspend issues](#Suspend_issues)
    *   [2.2 Screen not rotating](#Screen_not_rotating)
    *   [2.3 Fingerprint sensor](#Fingerprint_sensor)
    *   [2.4 Soundcard turning off and coil whine](#Soundcard_turning_off_and_coil_whine)
    *   [2.5 Turbo Boost not working](#Turbo_Boost_not_working)
    *   [2.6 Reduce throttling](#Reduce_throttling)

## Installation

### BIOS configuration

Bios can be accessed with F2 or F12 on DELL logo boot screen.

With Bios version 1.1.0 or 1.3.1 to 2.1.2 you have to set sata operation to AHCI first and then uncheck in Advanced Boot options -> Legacy ROM.[[1]](http://en.community.dell.com/support-forums/laptop/f/3518/t/20004529?pi41097=1)

**Note:**

*   In RAID mode the BIOS/UEFI is able to see the internal drive and is able to boot from it. It is possible to boot Archiso in RAID mode, but it can't see the internal drive.
*   In AHCI mode the BIOS/UEFI with Legacy ROM activated is not able to see the internal drive. If you try to boot it will fail and display an error that no harddrive is installed.
*   In AHCI mode the BIOS/UEFI with Legacy ROM deactivated is able to see the internal drive and therefore boot from it and Archiso is able to see the drive too. With these settings you can install and boot arch.

It is also needed to set the following settings [[2]](https://www.dell.com/community/General/Dell-XPS-13-9365-Won-t-boot-USB-in-SATA-Mode-AHCI-Trying-to/m-p/5119127/highlight/true#M918191) :

*   UEFI network stack - disabled
*   Secure Boot - disabled
*   SATA operations - AHCI
*   Legacy ROM - disabled
*   POST Behaviour : Fastboot - *minimal* (if not, BIOS is really slow, and cannot boot to any mediums)

**Note:**

*   Some changes in BIOS might reset other settings. Check your BIOS settings twice.
*   Those settings are working as of 2018/11/28

## Troubleshooting

### Suspend issues

This model only supports the S0 (s2idle) sleep mode. [[3]](https://patchwork.kernel.org/patch/9758513/) Change the suspend mode to `s2idle` by adding the `mem_sleep_default=s2idle` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). **Note:** As of 2018/11/18, this does not seem required anymore: the kernel automatically sets it correctly.

### Screen not rotating

You need to install [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) for automatic screen rotation to work.

### Fingerprint sensor

The fingerprint sensor on this computer is not yet supported. [[4]](https://www.dell.com/community/Linux-Developer-Systems/XPS-13-Fingerprint-reader-Linux-support/td-p/5090723) . There is an open [fprint](/index.php/Fprint "Fprint") bug opened to track progress on this issue [[5]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/52)

### Soundcard turning off and coil whine

By default, the soundcard automatically turns of which leads to delays when there is a song to play (or distortion). This can also cause coil whine especially while scrolling with headphones plugged and sound muted. To solve this, you can force the soundcard to always stay awake :

 `/etc/modprobe.d/audio_no_powersave.conf`  `options snd_hda_intel power_save=0` 

### Turbo Boost not working

If the CPU is not reaching turbo boost clock speeds a possible solution can be to set activate HWP dynamic boost. Try

```
 $ echo 1 > /sys/devices/system/cpu/intel_pstate/hwp_dynamic_boost

```

If that works you can make the change permanent.

 `/etc/tmpfiles.d/hwp.conf`  `w /sys/devices/system/cpu/intel_pstate/hwp_dynamic_boost - - - - 1` 

### Reduce throttling

The CPU seems to throttle already at around 50 to 60°C. You can install [throttled](https://www.archlinux.org/packages/?name=throttled) to raise this limit. It also has the option to change the short and long term power limit and allows undervolting. It raises the temperature limit by default to 90°C. Intel's product page lists 100°C as the temperature limit. [[6]](https://ark.intel.com/content/www/de/de/ark/products/95452/intel-core-i5-7y54-processor-4m-cache-up-to-3-20-ghz.html) Though it is not recommenced to run it at such a high temperature. You can change these settings at

```
/etc/lenovo_fix.conf

```

After installation you need enable the systemd service with

```
$ sudo systemctl enable --now lenovo_fix.service

```

Beware that a higher temperature might reduce the longevity of your device. The battery in the device is rated for a maximum temperature of 65°C.
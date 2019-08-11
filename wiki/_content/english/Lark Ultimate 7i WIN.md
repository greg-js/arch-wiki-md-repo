| **Device** | **Status** | **Modules** |
| Display | Working, including backlight | xf86-video-intel |
| Touchscreen | Working, but needs copying firmware and calibration, Windows button not working by default | silead |
| Wireless | Working |
| Audio | Working (speaker, 3.5 mm jack, HDMI) | snd_soc_rt5640 |
| Battery Status | Working | battery |
| Camera (front) | Not working on stock Arch kernel (as of 5.3), driver removed in 4.18 | gc0310 |
| Camera (back) | Not working on stock Arch kernel (as of 5.3) | ov2680 |
| Bluetooth | Working |
| MicroSD Reader | Working, tested with 64GB microSD | sdhci |
| Power Management | Sleep seems to work fine, hibernate may need further testing |
| Accelerometer | Working | bmc150_accel_* |
| Hardware Buttons | Working | soc_button_array gpio_keys |

[Lark Ultimate 7i WIN](http://www.lark.com.pl/produkt/155_ultimate-7i-win.html) is a budget 7" tablet shipping with Windows 8, 8.1 or 10\. Android versions are known to exist but were not as popular and less featured than the Windows (WIN) counterparts. There also exist 8", 10" and 11" versions of these tables and versions with 3G modem, featuring different interiors.

Lark Ultimate 7i WIN has Intel Atom Z3735G BayTrail processor with integrated graphics and 1 GB of integrated DDR3L RAM, 16 GB eMMC, 1024 x 600 pixel screen with 10-point touchscreen of unknown resolution and "Windows" button, three hardware buttons (volume up, down and power), basic accelerometer, two cameras (VGA in front, 2 Mpix in the back), microphone, mono speaker, 3.5 mm jack slot, microSD slot, miniHDMI port and one microUSB port (for data and charging). It features InsydeH20 32-bit UEFI BIOS.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Installation](#Installation)
    *   [1.2 Touchscreen](#Touchscreen)
    *   [1.3 Accelerometer](#Accelerometer)
*   [2 Broken devices](#Broken_devices)
    *   [2.1 Camera](#Camera)
*   [3 Device info](#Device_info)
    *   [3.1 Devices on i2c bus](#Devices_on_i2c_bus)

## Configuration

### Installation

This tablet uses 32-bit UEFI despite having 64-bit processor. To install 64-bit system on it, see [Unified Extensible Firmware Interface#Booting 64-bit kernel on 32-bit UEFI](/index.php/Unified_Extensible_Firmware_Interface#Booting_64-bit_kernel_on_32-bit_UEFI "Unified Extensible Firmware Interface").

For installation, you will most likely need some kind of USB hub, as you need to have mouse and boot media connected. Booting from microSD was not tested. Wireless should work with recent Arch boot media.

**Warning:** Be careful not to turn off USB in BIOS, doing so will require disassembly of the device to reset CMOS to default values.

### Touchscreen

For touchscreen to work, firmware is needed. For `silead` (recommended) driver, copy [mssl1680.fw](https://github.com/onitake/gsl-firmware/blob/master/firmware/lark/ulti7iwin/mssl1680.fw) file that was extracted from Windows drivers to `/usr/lib/firmware/silead/` directory. Then, [Calibrating Touchscreen](/index.php/Calibrating_Touchscreen "Calibrating Touchscreen") will be needed. Until a better solution is found, this entry can be added at the bottom of `.xinitrc` file for relatively usable touchpad:

 `~/.xinitrc`  `xinput set-prop "silead_ts' --type=float "Coordinate Transformation Matrix" 4.75 0 -0.02 0 6.7 -0.02 0 0 1` 

See [https://github.com/onitake/gsl-firmware/tree/master/firmware/lark/ulti7iwin](https://github.com/onitake/gsl-firmware/tree/master/firmware/lark/ulti7iwin) and [https://github.com/onitake/gsl-firmware/blob/master/README.md](https://github.com/onitake/gsl-firmware/blob/master/README.md) for more info.

### Accelerometer

`/sys/bus/i2c/devices` lists a BMA250E device. To see how it works, see

```
$ cd /sys/bus/i2c/devices/i2c-BMA250E\:00/iio\:device0/
$ watch cat in_accel_*_raw

```

## Broken devices

### Camera

According to `/sys/bus/i2c/devices`, there is an INT0310 device (GalaxyCore GC0310 - Front Camera) and OVTI2680 device (OmniVision OV2680 - Back Camera). Both had a short-lived driver implementation as a part of Linux kernels 4.12–4.17 staging `atomisp` driver [[1]](https://github.com/torvalds/linux/tree/v4.17/drivers/staging/media/atomisp), which was later removed. OV2680 is implemented as a standalone driver, but it's not enabled on stock Arch kernel.

## Device info

### Devices on i2c bus

/sys/bus/i2c/devices

| i2c-10EC5640:00 | snd_soc_rt5640 | Realtek RT5640 - Sound Card |
| i2c-BMA250E:00 | bmc150_accel_* | Bosch BMC150 - Accelerometer |
| i2c-INT0310:00 | gc0310 | GalaxyCore GC0310 - Front Camera |
| i2c-INT33F4:00 | intel_soc_pmic_i2c | Intel I2C Interface |
| i2c-MSSL1680:00 | silead | GSL1680 - Silead touchescreen |
| i2c-OVTI2680:00 | ov2680 | OmniVision OV2680 - Back Camera |
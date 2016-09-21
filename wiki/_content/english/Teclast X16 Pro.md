| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working | goodix |
| Wireless | Working, with kernel patches | rt8723bs |
| Audio | Working | snd_soc_rt5640 |
| Touchpad | Working |
| Battery Status | Working | battery_BATC |
| Camera | Not working |
| Bluetooth | Working, with kernel patches | rtl8723bs_bt |
| MicroSD Reader | Partially Working | sdhci |
| Power Management | Not working |
| Accelerometer | Working, with external kernel module | bmc150_accel_i2c |

The Teclast X16 [Pro](http://www.teclast.com/en/zt/X16Pro/) and [Power](http://www.teclast.com/en/zt/X16Power/) are two 2 in 1 [Tablet PC](/index.php/Tablet_PC "Tablet PC") devices, equipped with a 11.6 inch display that supports for 1920 x 1080 pixels. Besides, the Teclast X16 Pro and Power support dual OS that allows users to take advantage of both Windows 10 and Android 5.1 operating systems on the device. They are powered by fifth-generation Intel Atom Z8500 (Pro) and Intel Atom Z8700 (Power) CPUs, aka Cherry Trail-Braswell, and by eighth-generation Intel HD graphics (12EUs Pro, 16EUs Power), coupled with 4GB of RAM (Pro) or 8GB of RAM (Power), both DDR3-1066 (due to a BIOS bug).

With kernel 4.7.2 and newer surprisingly much is working or there is a way to get it to work. If you have the time to go through all the steps you can get a pretty good useable linux tab.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Booting with UEFI bios (systemd-boot)](#Booting_with_UEFI_bios_.28systemd-boot.29)
    *   [1.2 Display](#Display)
    *   [1.3 Sound card](#Sound_card)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 WiFi](#WiFi)
    *   [2.2 Bluetooth](#Bluetooth)
    *   [2.3 Touchpad (Cover)](#Touchpad_.28Cover.29)
    *   [2.4 Accelerometer](#Accelerometer)
*   [3 Partially broken devices](#Partially_broken_devices)
    *   [3.1 microSD Reader](#microSD_Reader)
*   [4 Broken devices](#Broken_devices)
    *   [4.1 Micro-USB OTG port](#Micro-USB_OTG_port)
    *   [4.2 Power Management](#Power_Management)
    *   [4.3 Camera](#Camera)
*   [5 Device Info](#Device_Info)
    *   [5.1 Devices on i2c bus](#Devices_on_i2c_bus)
*   [6 Tips and ticks](#Tips_and_ticks)
    *   [6.1 On-Screen Keyboard](#On-Screen_Keyboard)

## Configuration

### Booting with UEFI bios (systemd-boot)

Use an usb hub, a cheap usb wifi, an usb flash drive and an usb keyboard (or the keyboard cover) to install arch linux. You can enter the bios by pressing del several times and overrule the boot device. There isn't anything special to do, just prepare the flash drive and boot from it.

### Display

Changing display brightness works, however you have to alter the keybindings yourself because of non-standard keycodes for display brightness; see [Backlight](/index.php/Backlight "Backlight"), [Touchscreen](/index.php/Touchscreen "Touchscreen").

Automatic rotation does not work because of the missing support for the accelerometer.

### Sound card

Install alsamixer and set the following of about 50 volume controls have to be set to 30-50%, too much gain results in clicking noise.

*   media1_in Gain 0
*   codec_out1 Gain 0
*   pcm0_in Gain 0
*   Mono DAC
*   Speaker ClassD
*   Speaker

This is remembered during a reboot. Global shortcuts to change sound volume work.

## Troubleshooting

### WiFi

this step will take quite long, you can stop here and use the tab with an USB Wi-Fi Dongle

Compiling an Arch Linux kernel, see [Kernels/Traditional_compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation")

1) apply the pm_set/get-revertes + rfkill patches **NOT** the sound patches from Laszlo-Fiat see: [http://github.com/hadess/rtl8723bs/issues/76](http://github.com/hadess/rtl8723bs/issues/76) (0001-My-changes-for-4.7.0-rc7-for-Baytrail-T.patch.txt)

2) compile kernel (takes many hours), create new vmlinuz/initrd, create syslinux entries

check out the sources from [http://github.com/hadess/rtl8723bs](http://github.com/hadess/rtl8723bs) + make install

### Bluetooth

This device needs the rfkill patch from the step above.

see [http://github.com/lwfinger/rtl8723bs_bt](http://github.com/lwfinger/rtl8723bs_bt) not much to do, file-transfer works.

### Touchpad (Cover)

This is recognized as a generic pointing device, not as [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

### Accelerometer

/sys/bus/i2c/devices lists a BMA250E device

```
cd /sys/bus/i2c/devices/i2c-BMA250E:00/iio:device0
watch cat in_accel_x_raw in_accel_y_raw in_accel_z_raw

```

Tip: this kernel module has to be compiled by yourself, search for bmc150 below modules/industrialio

## Partially broken devices

### microSD Reader

Working fine with SDHC and lower cards, crashing with SDXC UHS-I and higher ones, (Timeout for Hardware Interrupt issue)

## Broken devices

### Micro-USB OTG port

Nothing happens if a USB Stick, or any other device, is plugged in.

### Power Management

Hibernate and pm-suspend crashes. To avoid any kind of instability, add this "intel_idle.max_cstate=1" to the CMDLINE.

### Camera

According to /sys/bus/i2c/devices, there is an OVTI2680 device (OmniVision OV2680 - Front Camera) and INT5648 device (OmniVision OV5648 - Rear Camera)

## Device Info

### Devices on i2c bus

/sys/bus/i2c/devices

| i2c-10EC5645:00 | rt5645 | Realtek RT5645 - Sound Card |
| i2c-BMA250E:00 | bmc150_accel_i2c | Bosch BMC150 - Accelerometer |
| i2c-FGCW2015:00 | CW2015 Fuel-Gauge IC? ([http://www.lean-chip.com/mc-download.html?id=154](http://www.lean-chip.com/mc-download.html?id=154)) |
| i2c-GDIX1001:00 | goodix | Goodix GT9110P - Touchscreen |
| i2c-INT33FD:00 | intel_soc_pmic_i2c | Intel I2C Interface |
| i2c-INT5648:00 | OmniVision OV5648 - Rear Camera |
| i2c-LNXVIDEO:00 | Video Extension - ACPI_VIDEO |
| i2c-OVTI2680:00 | OmniVision OV2680 - Front Camera |
| i2c-TBQ24297:00 | TI BQ24297 - Charging Controller ([http://www.ti.com/product/bq24297/description](http://www.ti.com/product/bq24297/description)) |
| i2c-XXVM149C:00 | VM149C Voice-Coil-Motor IC? ([http://www.siti.com.tw/product/spec/Motor/SP-VM149C-A.002.pdf](http://www.siti.com.tw/product/spec/Motor/SP-VM149C-A.002.pdf)) |

## Tips and ticks

### On-Screen Keyboard

Depending on your preferred window manager, install kvkbd for [KDE](/index.php/KDE "KDE") or CellWriter for [Gnome](/index.php/Gnome "Gnome"), see [Tablet_PC](/index.php/Tablet_PC "Tablet PC")
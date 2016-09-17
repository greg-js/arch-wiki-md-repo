| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working | goodix |
| Wireless | Working, with kernel patches | r8723bs |
| Audio | Working | snd_soc_rt5640 |
| Touchpad | Working | buggy two finger scroll. |
| Battery status | Working |
| Camera | Not working |
| Bluetooth | Working, with kernel patches | rtl8723bs_bt |
| Accelerometer | Working | bmc150_accel_i2c, see below |

[Teclast X16 Pro](http://www.teclast.com/en/zt/X16Pro/) is a 2 in 1 [Tablet PC](/index.php/Tablet_PC "Tablet PC") device, equipped with a 11.6 inch display that supports for 1920 x 1080 pixels. Besides, the Teclast X16 Pro is a dual OS supporting device that allows users to take advantage of both Windows 10 and Android 5.1 operating systems on the device. It is powered by fifth-generation Intel Atom Z8500 graphics and eighth-generation Intel HD graphics, coupled with 4GB of RAM.

With kernel 4.7.2 (20160902) surprisingly much is working or there is a way to get it to work. If you have the time to go through all the steps you can get a pretty good useable linux tab.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Booting with uefi bios (systemd-boot)](#Booting_with_uefi_bios_.28systemd-boot.29)
    *   [1.2 Display](#Display)
    *   [1.3 Sound card](#Sound_card)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 WiFi](#WiFi)
    *   [2.2 Bluetooth](#Bluetooth)
    *   [2.3 Keyboard cover touchpad](#Keyboard_cover_touchpad)
    *   [2.4 Acceleration sensor](#Acceleration_sensor)
*   [3 Broken devices](#Broken_devices)
    *   [3.1 OTG port](#OTG_port)
    *   [3.2 Hardware buttons](#Hardware_buttons)
    *   [3.3 Power management](#Power_management)
    *   [3.4 Camera](#Camera)
    *   [3.5 Devices on i2c bus](#Devices_on_i2c_bus)
*   [4 Tips and ticks](#Tips_and_ticks)
    *   [4.1 on-screen keyboard](#on-screen_keyboard)

## Configuration

### Booting with uefi bios (systemd-boot)

Use an usb hub, a cheap usb wifi, an usb flash drive and an usb keyboard (or the keyboard cover) to install arch linux. You can enter the bios by pressing del several times and overrule the boot device. There isn't anything special to do, just prepare the flash drive and boot from it.

### Display

Changing display brightness works, however you have to alter the keybindings yourself because of non-standard keycodes for display brightness; see [Backlight](/index.php/Backlight "Backlight"), [Touchscreen](/index.php/Touchscreen "Touchscreen"). Automatic rotation does not work because of the missing support for the accelerometer.

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

this step will take quite long, you can stop here and use the tab with the usb wifi dongle

Compiling an arch linux kernel, see [Kernels/Traditional_compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation")

apply the pm_set/get-revertes + rfkill patches **NOT** the sound patches from Laszlo-Fiat see: [http://github.com/hadess/rtl8723bs/issues/76](http://github.com/hadess/rtl8723bs/issues/76) (0001-My-changes-for-4.7.0-rc7-for-Baytrail-T.patch.txt)

compile kernel (takes many hours), create new vmlinuz/initrd, create syslinux entries

check out the sources from [http://github.com/hadess/rtl8723bs](http://github.com/hadess/rtl8723bs) + make install

### Bluetooth

This device needs the rfkill patch from the step above.

see [http://github.com/lwfinger/rtl8723bs_bt](http://github.com/lwfinger/rtl8723bs_bt) not much to do, filetransfer works.

### Keyboard cover touchpad

This is recognized as pointing device, not as [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

### Acceleration sensor

/sys/bus/i2c/devices lists a BMA250E

```
cd /sys/bus/i2c/devices/i2c-BMA250E:00/iio:device0
watch cat in_accel_x_raw in_accel_y_raw in_accel_z_raw

```

Tip: this kernel module has to be compiled by yourself, search for bmc150 below modules/industrialio

## Broken devices

### OTG port

Nothing happens if usb stick is plugged in or used as device.

### Hardware buttons

Home/windows-button, sound volume and power button are dead. However the power button is recognized during boot by [ACPI](/index.php/Acpid "Acpid")

Sound volume keys work in systemd-boot to choose an entry.

### Power management

Hibernate and pm-suspend crashes.

### Camera

According to /sys/bus/i2c/devices there is an OVTI2680 (OV2680) and INT5648 (this might be an OV5648)

### Devices on i2c bus

/sys/bus/i2c/devices

| i2c-10EC5645:00 | rt5645 | sound card |
| i2c-BMA250E:00 | bmc150_accel_i2c | acceleration sensor |
| i2c-FGCW2015:00 | unknown |
| i2c-GDIX1001:00 | Goodix-TS | touchscreen |
| i2c-INT33FD:00 | intel_soc_pmic_i2c |
| i2c-INT5648:00 | unknown, might be camera |
| i2c-LNXVIDEO:00 |
| i2c-OVTI2680:00 | unknown, might be ov2680 camera |
| i2c-TBQ24297:00 | unknown |
| i2c-XXVM149C:00 | unknown |

## Tips and ticks

### on-screen keyboard

Depending on your window manager install kvkbd for [KDE](/index.php/KDE "KDE") or CellWriter for [Gnome](/index.php/Gnome "Gnome"), see [Tablet_PC](/index.php/Tablet_PC "Tablet PC")
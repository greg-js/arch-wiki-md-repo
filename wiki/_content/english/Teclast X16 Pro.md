| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working |
| Wireless | Working, with kernel patches | r8723bs |
| Audio | Working | snd_soc_rt5640 |
| Touchpad | Working | buggy two finger scroll. |
| Battery status | Working |
| Camera | Not working |
| Bluetooth | Working, with kernel patches | rtl8723bs_bt |

[Teclast X16 Pro](http://www.teclast.com/en/zt/X16Pro/) is a 2 in 1 tablet PC device, equipped with a 11.6 inch display that supports for 1920 x 1080 pixels. Besides, the Teclast X16 Pro is a dual OS supporting device that allows users to take advantage of both Windows 10 and Android 5.1 operating systems on the device. It is powered by fifth-generation Intel Atom Z8500 graphics and eighth-generation Intel HD graphics, coupled with 4GB of RAM.

With kernel 4.7.2 (20160902) surprisingly much is working or there is a way to get it to work. If you have the time to go through all the steps you can get a pretty good useable linux tab.

## Contents

*   [1 Booting with uefi bios (systemd-boot)](#Booting_with_uefi_bios_.28systemd-boot.29)
*   [2 Display](#Display)
*   [3 Sound card](#Sound_card)
*   [4 WiFi](#WiFi)
*   [5 Bluetooth](#Bluetooth)
*   [6 OTG port](#OTG_port)
*   [7 Hardware buttons](#Hardware_buttons)
*   [8 Power management](#Power_management)

## Booting with uefi bios (systemd-boot)

Use an usb hub and cheap usb wifi stick to install arch linux. You can enter the bios by pressing del several times and overrule the boot device. There isn't anything special to do, just prepare an usb stick and boot from it.

## Display

Changing display brightness works, however you have to alter the keybindings yourself because of non-standard keycodes for display brightness; see [Backlight](/index.php/Backlight "Backlight").

## Sound card

The following of about 50 volume controls have to be set to 30-50%, too much gain results in clicking noise.

media1_in Gain 0 codec_out1 Gain 0 pcm0_in Gain 0 Mono DAC Speaker ClassD Speaker

This is remembered during a reboot. Global shortcuts to change sound volume work.

## WiFi

this step will take quite long, you can stop here and use the tab with the usb wifi dongle

Compiling an arch linux kernel, see [Kernels/Traditional_compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation")

apply the pm_set/get-revertes + rfkill patches **NOT** the sound patches from Laszlo-Fiat see: [http://github.com/hadess/rtl8723bs/issues/76](http://github.com/hadess/rtl8723bs/issues/76) (0001-My-changes-for-4.7.0-rc7-for-Baytrail-T.patch.txt)

compile kernel (takes many hours), create new vmlinuz/initrd, create syslinux entries

check out the sources from [http://github.com/hadess/rtl8723bs](http://github.com/hadess/rtl8723bs) + make install

## Bluetooth

this needs one patch from the step above.

see [http://github.com/lwfinger/rtl8723bs_bt](http://github.com/lwfinger/rtl8723bs_bt) not much to do, filetransfer works.

## OTG port

nothing happens if usb stick is plugged in or used as device

## Hardware buttons

home/windows-button, sound volume and power button does nothing

## Power management

hibernate and pm-suspend crashes
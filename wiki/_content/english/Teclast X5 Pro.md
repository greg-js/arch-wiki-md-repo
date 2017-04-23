| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Touchscreen | Working,with firmware [mssl1680-firmware](https://aur.archlinux.org/packages/mssl1680-firmware/) | silead_ts |
| Wireless | Working | iwlwifi |
| Audio | Working | alc269 |
| Touchpad | Working |
| Battery Status | Working |
| Camera | Not working |
| Bluetooth | Working | btintel |
| MicroSD Reader | Working |
| Power Management | Seems work fine |
| Accelerometer | No driver found |
| Hardware Buttons | Working |

The [Teclast X5 Pro](http://www.teclast.com/zt/Tbook/X5Pro/) is a two 2 in 1 [Tablet PC](/index.php/Tablet_PC "Tablet PC") devices, equipped with a 12.2 inch display that supports for 1920 x 1200 pixels.It is powered by seventh-generatipn Intel CoreM 7Y30, aka Kabe-Lake, and by nineth-generation Intel HD graphics, coupled with 8GB of RAM , both DDR3L, 240G SSD or 256G SSD (Optional).

With kernel >= 4.9.0, seems the newest silead_ts driver has added support for silead mssl1680 touch screen (firmware needed [mssl1680-firmware](https://aur.archlinux.org/packages/mssl1680-firmware/)).

## Installation

Just Install Arch Linux in a normal way, however, for [SSD](/index.php/SSD "SSD") you should better refer [ArchWiki Solid_State_Drives](/index.php/Solid_State_Drives "Solid State Drives").

## [Calibrating Touch Screen](/index.php/Calibrating_Touchscreen#Your_screen "Calibrating Touchscreen")

Unfortunately there is no solution found for [Wayland](/index.php/Wayland "Wayland") :( (so if you are using GNOME with gdm, disable Wayland in "/etc/gdm/custom.conf" which is enabled by dafault and login with the option "Gnome on Xorg". )

Then create "/etc/X11/xorg.conf.d/99-calibration.conf"

 `/etc/X11/xorg.conf.d/99-calibration.conf` 
```
Section "InputClass"
	Identifier	"calibration"
	MatchProduct	"silead_ts"
	Option	"CalibrationMatrix"	"2.074595 0 0 0 2.688341 0 0 0 1"
	Driver	"libinput"
EndSection

```

Reboot and touchscreen will work fine. If not, make sure you have [mssl1680-firmware](https://aur.archlinux.org/packages/mssl1680-firmware/) installed.

## On-Screen Keyboard

Depending on your preferred window manager, install kvkbd for [KDE](/index.php/KDE "KDE") or CellWriter for [GNOME](/index.php/GNOME "GNOME"), see [Tablet PC](/index.php/Tablet_PC "Tablet PC")
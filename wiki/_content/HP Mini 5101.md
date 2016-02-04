# HP Mini 5101

## Contents

*   [1 Video](#Video)
*   [2 Audio](#Audio)
*   [3 Network](#Network)
    *   [3.1 Wireless Driver (Broadcom)](#Wireless_Driver_.28Broadcom.29)
        *   [3.1.1 Driver Overview](#Driver_Overview)
*   [4 Bluetooth](#Bluetooth)
*   [5 Touchpad](#Touchpad)
*   [6 Webcam](#Webcam)
*   [7 ACPI](#ACPI)
    *   [7.1 Suspend on Lid](#Suspend_on_Lid)
    *   [7.2 Power Button](#Power_Button)
    *   [7.3 Hotkeys](#Hotkeys)
        *   [7.3.1 Display toggle](#Display_toggle)
        *   [7.3.2 Mute, browser button, volume down, etc...](#Mute.2C_browser_button.2C_volume_down.2C_etc...)
*   [8 Hard disk shock protection](#Hard_disk_shock_protection)

## Video

Install xf86-video-intel or xf86-video-intel-newest. Make sure to configure [KMS](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel") correctly.

## Audio

Typical Intel HD Audio. Just follow [ALSA](/index.php/ALSA "ALSA").

Make sure you have the latest version of alsa-utils, alsa-lib and alsa-firmware.

## Network

Swapping eth0/eth1 can confuse [Wicd](/index.php/Wicd "Wicd"), assigning [static names](/index.php/Udev#Mixed_Up_Devices.2C_Sound.2FNetwork_Cards_Changing_Order_Each_Boot "Udev") helps.

### Wireless Driver (Broadcom)

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for driver setup.

It may be necessary to load the driver (wl as an axample here) manually:

 `/etc/rc.conf `  `MODULES=(... wl ...)` 

Problem with reconnecting after suspending might be solved by:

 `/etc/pm/config.d/01-modules `  `SUSPEND_MODULES="wl"` 

#### Driver Overview

1.  brcmsmac: Works best but the red/blue led isn't working.
2.  broadcom-wl: Needs to be compiled newly from the AUR ([broadcom-wifi-builder](https://aur.archlinux.org/packages/broadcom-wifi-builder/) or [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)) after each kernel upgrade. LED works but reconnecting problem after suspending.
3.  b43: Alternatively your network chip may be supported by [b43](/index.php/Broadcom_wireless#b43.2Fb43legacy "Broadcom wireless") (kernel > 2.6.32).

## Bluetooth

See: [Bluetooth](/index.php/Bluetooth "Bluetooth")

## Touchpad

Works out of the box.

## Webcam

Works out of the box.

## ACPI

### Suspend on Lid

This here works quite fine: [Suspend to RAM#Automatic Suspend, the Hard Way](/index.php/Suspend_to_RAM#Automatic_Suspend.2C_the_Hard_Way "Suspend to RAM")

It might be necessary to use "/etc/acpi/events/lm_lid" instead of "/etc/acpi/events/lid". (laptop-mode?)

Just change the "LID" to it's actual value. For me it was C1D0.

 `/etc/acpi/actions/lid_handler.sh`  `if grep closed /proc/acpi/button/lid/**C1D0**/state >/dev/null ; then ` 

### Power Button

[Shutting system down by pressing the power button](/index.php/Shutting_system_down_by_pressing_the_power_button "Shutting system down by pressing the power button")

### Hotkeys

#### Display toggle

[ACPI hotkeys](/index.php/ACPI_hotkeys "ACPI hotkeys")

```
# acpi_listen
(Press fn+f2)
video C088 00000080 00000000

```

So we have to edit

```
/etc/acpi/handler.sh

```

like this

 `/etc/acpi/handler.sh ` 

```
case "$1" in
    .
    .
    .
    video)
        arandr #or path to your shell script for switching display mode
        ;;
    .
    .
    .
esac

```

#### Mute, browser button, volume down, etc...

[Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

## Hard disk shock protection

Install [hpfall](https://aur.archlinux.org/packages.php?ID=45093) from AUR and add it to rc.conf:

 `/etc/rc.conf `  `DAEMONS=(... hpfall ...)` 

See also [Shock protection for HP/Compaq laptops](/index.php/Laptop#Hard_disk_shock_protection "Laptop").

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Mini_5101&oldid=392219](https://wiki.archlinux.org/index.php?title=HP_Mini_5101&oldid=392219)"
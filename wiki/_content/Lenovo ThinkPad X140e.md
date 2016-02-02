# Lenovo ThinkPad X140e

Installation instructions for the Lenovo ThinkPad X140e. Should work for E145 as well.

## Contents

*   [1 Video drivers](#Video_drivers)
*   [2 Wireless](#Wireless)
*   [3 Input](#Input)
    *   [3.1 TrackPoint scrolling (wheel emulation)](#TrackPoint_scrolling_.28wheel_emulation.29)
    *   [3.2 TrackPad](#TrackPad)
    *   [3.3 TrackPoint speed and sensitivity](#TrackPoint_speed_and_sensitivity)
*   [4 Power saving](#Power_saving)
    *   [4.1 Disable Bluetooth](#Disable_Bluetooth)
    *   [4.2 ATI video card powersaving](#ATI_video_card_powersaving)

## Video drivers

Users have the choice between the open source [ATI](/index.php/ATI "ATI") video driver or the closed source [Catalyst](/index.php/Catalyst "Catalyst") video driver.

As of 3.15 kernel, the open source drivers are very suitable for this chips' GPU. 3.16 is a mild improvement over that.

## Wireless

The Thinkpad x140e is available from Lenovo with one of two wireless cards:

*   A BGN solution of unknown chipset.
*   A Broadcom ABGN Wifi / BT4.0 card which is currently not supported by the `b43` driver. Ideally, use driver `broadcom-wl`. See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for details.

As of BIOS 2.05, the X140e supports Lenovo branded mPCIe Intel 802.11 ac/a/b/g/n. However no X140e is currently sold with this wifi option. This card is supported out of the box by Arch. The only tested and confirmed FRU is 04W3814.

## Input

### TrackPoint scrolling (wheel emulation)

See [Lenovo ThinkPad X120e#TrackPoint scrolling (wheel emulation)](/index.php/Lenovo_ThinkPad_X120e#TrackPoint_scrolling_.28wheel_emulation.29 "Lenovo ThinkPad X120e").

### TrackPad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### TrackPoint speed and sensitivity

See [Lenovo ThinkPad X120e#TrackPoint speed and sensitivity](/index.php/Lenovo_ThinkPad_X120e#TrackPoint_speed_and_sensitivity "Lenovo ThinkPad X120e").

## Power saving

Use TLP. Should average 9~ hours.

See [power saving](/index.php/Power_saving "Power saving").

### Disable Bluetooth

See [Power saving#Bluetooth](/index.php/Power_saving#Bluetooth "Power saving").

### ATI video card powersaving

For the open-source driver, follow the information in [ATI#Powersaving](/index.php/ATI#Powersaving "ATI").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X140e&oldid=412579](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X140e&oldid=412579)"
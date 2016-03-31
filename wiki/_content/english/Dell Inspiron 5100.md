This is based on my experience with arch on my Dell Inspiron 5100 laptop. Most of this information should apply to other 5xxx series Inspiron laptops and similar generation laptops in general.

## Contents

*   [1 Hardware](#Hardware)
*   [2 Kernel](#Kernel)
*   [3 Networking](#Networking)
    *   [3.1 Wired](#Wired)
    *   [3.2 Wireless](#Wireless)
    *   [3.3 Modem](#Modem)
*   [4 Power Management](#Power_Management)
*   [5 Xorg](#Xorg)
*   [6 See also](#See_also)

## Hardware

Audio: Intel 82801DB AC'97 Audio

Video: ATi Radeon Mobility M7

Modem: Broadcom BCM v.92 56k WinModem

Wired NIC: Broadcom BCM4401

Wireless NIC: Intel IPW 2200 (*note most of these laptops came with a Dell Truemobile 1300 card. aka Broadcom 4320.)

## Kernel

The stock arch kernel contains everything you need to get this laptop running.

## Networking

### Wired

Works fine using the b44 module.

### Wireless

My ipw2200 card works fine with the ipw2200 module.

The Truemobile 1300 card requires ndiswrapper I believe.

### Modem

The modem is believed to be a Broadcom BCM v.92 56k WinModem. The FCC sticker on the bottom of my laptop labels is as a BCM9415M. Its a winmodem and is on an intel AC'97 AMR interface. I do not use is and I do not plan to. A quick google search says the best way to get this modem working is buy a different one.

## Power Management

See the main [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") article.

## Xorg

hwd does a pretty good job of generating the xorg.conf for you. You should be able to use its config to start up X and get going but there are a few things you can do to optimize it.

The laptop has an ati radeon card (I believe some of the more optioned up versions have an nvidia card) but its a mobility m7 and is not supported by the radeon package in community so you need to stick with the driver that ships with the kernel.

The big changes you'll need to make are for the synaptics touchpad. Yes the touchpad will work fine if you just leave it as a generic ps/2 mouse but with the synaptics driver in extra there is no reason not to unlock all of its features. Personally the tap click feature drives me crazy so I have it disabled in my config, but you can probably figure out what the different parameters do and change them to suit your taste

```
Section "Input Device"
       Identifier  "Synaptics Mouse"
       Driver      "synaptics"
       Option      "Device"              "/dev/psaux"
       Option      "Protocol"            "auto-dev"
       Option      "LeftEdge"            "1700"
       Option      "RightEdge"           "5300"
       Option      "TopEdge"             "1700"
       Option      "BottomEdge"          "4200"
       Option      "FingerLow"           "25"
       Option      "FingerHigh"          "30"
       Option      "MaxTapTime"          "0"
       Option      "MaxTapMove"          "220"
       Option      "MaxDoubleTapTime"    "0"
       Option      "FastTaps"            "on"
       Option      "VertScrollDelta"     "100"
       Option      "HorizScrollDelta"    "100"
       Option      "MinSpeed"            "0.09"
       Option      "MaxSpeed"            "0.18"
       Option      "AccelFactor"         "0.0015"
       Option      "EmulateMidButtonTime""100"
       Option      "EdgeMotionMinZ"      "30"
       Option      "EdgeMotionMaxZ"      "35"
       Option      "EdgeMotionMinSpeed"  "0"
       Option      "EdgeMotionMaxSpeed"  "0"
       Option      "EdgeMotionUseAlways" "off"
       Option      "TapButton1"          "1"
       Option      "RBCornerButton"      "3"
       Option      "LBCornerButton"      "2"
       Option      "CoastingSpeed"       "0.1"
       Option      "SHMConfig"           "on"
EndSection

```

To use this you'll need to add an InputDevice line in your server layout section to use the synaptics mouse.

```
InputDevice    "Synaptics Mouse" "CorePointer"

```

Remember you can only have one CorePointer so if you already have a configured mouse with the "CorePointer" value, set one to "SendCoreEvents", e.g.

```
InputDevice    "Mouse1"          "CorePointer"
InputDevice    "Synaptics Mouse" "SendCoreEvents"

```

## See also

*   This report has been listed in the [Linux Laptop and Notebook Installation Survey: DELL](http://tuxmobil.org/dell.html).
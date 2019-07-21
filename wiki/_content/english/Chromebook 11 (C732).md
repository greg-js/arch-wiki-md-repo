| Device | Status |
| LTE | Works |
| Wireless | Works |
| Bluetooth | Not tested |
| Sound | Not working |
| Touchpad | Works |
| Touchscreen | Not working |
| Webcam | Not tested |

## Firmware

*   disable hardware write-protection by booting without battery
*   only SeaBIOS (no CoreBoot with UEFI) by [https://mrchromebox.tech/#devices](https://mrchromebox.tech/#devices)

## Touchscreem

Maybe it works with the lates `xf86-input-cmt` the AUR packages are outdated ;(

## System Settings

```
cat /proc/bus/input/devices
---
I: Bus=0019 Vendor=0000 Product=0005 Version=0000
N: Name="Lid Switch"
P: Phys=PNP0C0D/button/input0
S: Sysfs=/devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A08:00/device:14/PNP0C09:00/PNP0C0D:00/input/input0
U: Uniq=
H: Handlers=event0 
B: PROP=0
B: EV=21
B: SW=1

I: Bus=0019 Vendor=0000 Product=0001 Version=0000
N: Name="Power Button"
P: Phys=PNP0C0C/button/input0
S: Sysfs=/devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0C:00/input/input1
U: Uniq=
H: Handlers=kbd event1 
B: PROP=0
B: EV=3
B: KEY=10000000000000 0

I: Bus=0019 Vendor=0000 Product=0003 Version=0000
N: Name="Sleep Button"
P: Phys=PNP0C0E/button/input0
S: Sysfs=/devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0E:00/input/input2
U: Uniq=
H: Handlers=kbd event2 
B: PROP=0
B: EV=3
B: KEY=4000 0 0

I: Bus=0019 Vendor=0000 Product=0001 Version=0000
N: Name="Power Button"
P: Phys=LNXPWRBN/button/input0
S: Sysfs=/devices/LNXSYSTM:00/LNXPWRBN:00/input/input3
U: Uniq=
H: Handlers=kbd event3 
B: PROP=0
B: EV=3
B: KEY=10000000000000 0

I: Bus=0011 Vendor=0001 Product=0001 Version=ab83
N: Name="AT Translated Set 2 keyboard"
P: Phys=isa0060/serio0/input0
S: Sysfs=/devices/platform/i8042/serio0/input/input4
U: Uniq=
H: Handlers=sysrq kbd event4 leds 
B: PROP=0
B: EV=120013
B: KEY=402000000 3803078f800d001 feffffdfffefffff fffffffffffffffe
B: MSC=10
B: LED=7

I: Bus=0019 Vendor=0000 Product=0000 Version=0001
N: Name="Tablet Mode Switch"
P: Phys=GOOG0006
S: Sysfs=/devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A08:00/device:14/PNP0C09:00/GOOG0006:00/input/input5
U: Uniq=
H: Handlers=event5 
B: PROP=0
B: EV=21
B: SW=2

I: Bus=0010 Vendor=001f Product=0001 Version=0100
N: Name="PC Speaker"
P: Phys=isa0061/input0
S: Sysfs=/devices/platform/pcspkr/input/input6
U: Uniq=
H: Handlers=kbd event6 
B: PROP=0
B: EV=40001
B: SND=6

I: Bus=0003 Vendor=0bda Product=57f0 Version=0005
N: Name="HD WebCam: HD WebCam"
P: Phys=usb-0000:00:15.0-5/button
S: Sysfs=/devices/pci0000:00/0000:00:15.0/usb1/1-5/1-5:1.0/input/input7
U: Uniq=
H: Handlers=kbd event7 
B: PROP=0
B: EV=3
B: KEY=100000 0 0 0

I: Bus=0018 Vendor=04f3 Product=009a Version=0000
N: Name="Elan Touchpad"
P: Phys=
S: Sysfs=/devices/pci0000:00/0000:00:17.0/i2c_designware.4/i2c-4/i2c-ELAN0000:00/input/input8
U: Uniq=
H: Handlers=event8 mouse0 
B: PROP=5
B: EV=b
B: KEY=e520 10000 0 0 0 0
B: ABS=663800013000003

I: Bus=0018 Vendor=0000 Product=0000 Version=0000
N: Name="Elan Touchscreen"
P: Phys=
S: Sysfs=/devices/pci0000:00/0000:00:16.3/i2c_designware.3/i2c-3/i2c-ELAN0001:00/input/input9
U: Uniq=
H: Handlers=event9 mouse1 
B: PROP=2
B: EV=b
B: KEY=400 0 0 0 0 0
B: ABS=661800001000003 

I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="HDA Intel PCH HDMI/DP,pcm=3"
P: Phys=ALSA
S: Sysfs=/devices/pci0000:00/0000:00:0e.0/sound/card0/input10
U: Uniq=
H: Handlers=event10 
B: PROP=0
B: EV=21
B: SW=140

I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="HDA Intel PCH HDMI/DP,pcm=7"
P: Phys=ALSA
S: Sysfs=/devices/pci0000:00/0000:00:0e.0/sound/card0/input11
U: Uniq=
H: Handlers=event11 
B: PROP=0
B: EV=21
B: SW=140

I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="HDA Intel PCH HDMI/DP,pcm=8"
P: Phys=ALSA
S: Sysfs=/devices/pci0000:00/0000:00:0e.0/sound/card0/input12
U: Uniq=
H: Handlers=event12 
B: PROP=0
B: EV=21
B: SW=140

I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="HDA Intel PCH HDMI/DP,pcm=9"
P: Phys=ALSA
S: Sysfs=/devices/pci0000:00/0000:00:0e.0/sound/card0/input13
U: Uniq=
H: Handlers=event13 
B: PROP=0
B: EV=21
B: SW=140

I: Bus=0000 Vendor=0000 Product=0000 Version=0000
N: Name="HDA Intel PCH HDMI/DP,pcm=10"
P: Phys=ALSA
S: Sysfs=/devices/pci0000:00/0000:00:0e.0/sound/card0/input14
U: Uniq=
H: Handlers=event14 
B: PROP=0
B: EV=21
B: SW=140

```
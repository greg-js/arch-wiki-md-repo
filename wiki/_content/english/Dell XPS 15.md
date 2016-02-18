This page is a work in progress! More info coming soon.

| Device | Status |
| Network | Works |
| Wireless | Works |
| Sound | Works |
| Bluetooth | Works |
| Touchpad | Works |
| Graphics | Modify |
| USB 3.0 | Works |
| Webcam | Works |
| System info | Not tested |
| Power management | Buggy |
| WiDi | Not working |
| Touchpad gestures | Not working |

*   Works - Works out-of-the-box
*   Modify - Works with modifications
*   Not tested
*   Not working

## Contents

*   [1 System Settings](#System_Settings)
*   [2 System Setup](#System_Setup)
    *   [2.1 Power Management](#Power_Management)
    *   [2.2 Graphics](#Graphics)
        *   [2.2.1 Intel only](#Intel_only)
            *   [2.2.1.1 acpi_call usage](#acpi_call_usage)
        *   [2.2.2 Intel with Nvidia](#Intel_with_Nvidia)
    *   [2.3 Screen](#Screen)
    *   [2.4 External Display](#External_Display)
        *   [2.4.1 Multihead](#Multihead)
    *   [2.5 WLAN](#WLAN)
        *   [2.5.1 Note](#Note)
    *   [2.6 Bluetooth](#Bluetooth)
    *   [2.7 Webcam](#Webcam)
    *   [2.8 Power management](#Power_management_2)
    *   [2.9 Special Touch Keys](#Special_Touch_Keys)
        *   [2.9.1 Alternative method](#Alternative_method)
    *   [2.10 Hidden Keyboard Keys](#Hidden_Keyboard_Keys)
    *   [2.11 Notes](#Notes)
*   [3 Howtos](#Howtos)

## System Settings

Hardware settings om January 2011 model

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 18)
00:01.0 PCI bridge: Intel Corporation Core Processor PCI Express x16 Root Port (rev 18)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 18)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 06)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 06)
00:1c.1 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 2 (rev 06)
00:1c.3 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 4 (rev 06)
00:1c.4 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 5 (rev 06)
00:1c.5 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 (rev 06)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a6)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 06)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 6 port SATA AHCI Controller (rev 06)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 06)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 06)
02:00.0 VGA compatible controller: nVidia Corporation Device 0df1 (rev a1)
02:00.1 Audio device: nVidia Corporation GF108 High Definition Audio Controller (rev a1)
04:00.0 Network controller: Intel Corporation Centrino Wireless-N 1000
05:00.0 USB Controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 03)
09:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)
ff:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 05)
ff:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 05)
ff:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 05)
ff:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 05)
ff:02.2 Host bridge: Intel Corporation Core Processor Reserved (rev 05)
ff:02.3 Host bridge: Intel Corporation Core Processor Reserved (rev 05)

```

For Sandy Bridge model (L502X)

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation 2nd Generation Core Processor Family PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 6 Series Chipset Family High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 1 (rev b5)
00:1c.1 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 2 (rev b5)
00:1c.3 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 4 (rev b5)
00:1c.4 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 5 (rev b5)
00:1c.5 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 6 (rev b5)
00:1d.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM67 Express Chipset Family LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 6 Series Chipset Family 6 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 6 Series Chipset Family SMBus Controller (rev 05)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 1030 (rev 34)
04:00.0 USB Controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 04)
06:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)

```

For 2012 Model (L521X)

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GT 640M] (rev ff)
07:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168 PCI Express Gigabit Ethernet controller (rev 07)
08:00.0 Network controller: Atheros Communications Inc. AR9462 Wireless Network Adapter (rev 01)
09:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)
09:00.1 SD Host controller: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)

```

For 2013 Model (9350)

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06) 
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller (rev 06)
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
00:04.0 Signal processing controller: Intel Corporation Device 0c03 (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 05)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d5)
00:1c.2 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d5)
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d5)
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM87 Express LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 05)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 05)
00:1f.6 Signal processing controller: Intel Corporation 8 Series Chipset Family Thermal Management Controller (rev 05)
02:00.0 3D controller: NVIDIA Corporation GK107M [GeForce GT 750M] (rev ff)
06:00.0 Network controller: Intel Corporation Wireless 7260 (rev 6b)
07:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 5249 (rev 01)

```

lspci for model 9550 (variant with touchscreen & PCIe m.2 ssd):

```
00:00.0 Host bridge: Intel Corporation Sky Lake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Sky Lake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 191b (rev 06)
00:04.0 Signal processing controller: Intel Corporation Device 1903 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H LPSS I2C Controller #0 (rev 31)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-H LPSS I2C Controller #1 (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.1 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #2 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #13 (rev f1)
00:1d.6 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #15 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 960M] (rev a2)
02:00.0 Network controller: Broadcom Corporation BCM43602 802.11ac Wireless LAN SoC (rev 01)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 525a (rev 01)
04:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a802 (rev 01)

```

lsusb for model 9550 (variant with touchscreen & PCIe m.2 ssd):

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 04f3:21d5 Elan Microelectronics Corp. 
Bus 001 Device 003: ID 0a5c:6410 Broadcom Corp. 
Bus 001 Device 005: ID 1bcf:2b95 Sunplus Innovation Technology Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## System Setup

### Power Management

For the Sandy Bridge model (L502X): Suspend works; hibernation does not (it gets hung on a flashing cursor in text mode and does not even switch video modes).

### Graphics

By default, both Intel and NVidia cards are active, which can consume a lot of power. Using the Intel-only setup below, you can reduce your battery usage due to disabling the Nvidia card. The Intel and Nvidia setup describes how to utilize both cards and save power using [Bumblebee](/index.php/Bumblebee "Bumblebee").

#### Intel only

Install the Intel video driver using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.

To make sure nvidia module will not load into your system:

*   Remove nouveau and/or nvidia drivers
*   Use acpi_call (compile [acpi_call](http://github.com/mkottman/acpi_call) or use the [AUR package](https://aur.archlinux.org/packages.php?ID=39470) ) to disable the nvidia card

##### acpi_call usage

```
modprobe acpi_call
test_off.sh

```

If you have a positive value then do:

```
echo '\_SB.<YOUR>.<POSITIVE>.<VALUE>._OFF' > /proc/acpi/call

```

Else your can test the other script m11xr2.sh (it worked for me):

```
/usr/share/acpi_call/m11xr2.sh off

```

You can use this command *before* and *after* to see how the battery consumption change (you need to disconnect sector first):

```
grep rate /proc/acpi/battery/BAT1/state

```

To make this permanent, just add your working command in `/etc/rc.local`. Example:

```
modprobe acpi_call
/usr/share/acpi_call/m11xr2.sh off

```

#### Intel with Nvidia

The [Optimus](/index.php/Optimus "Optimus") setup consists of the integrated Intel chip connected to the laptop screen and the Nvidia card runs through this. As such, the Nvidia chip cannot be used without the Intel chip (some other laptops have the option in BIOS to turn Intel off and use just Nvidia, but not this laptop).

See the [Bumblebee](/index.php/Bumblebee "Bumblebee") page [set of instructions](/index.php/Bumblebee#Installation "Bumblebee"), particularly the Intel/Nvidia section which has been tested. The main thing to note is that installing both the Intel and Nvidia packages at once tends to avoid dependency issues.

### Screen

### External Display

Since the Display Port is controlled by the Intel driver, it tends to work quite well and will usually mirror the laptop display without configuration. Getting both the HDMI and DP adapters to display separate requires additional setup.

#### Multihead

The following instructions should help configure the laptop to display separate output on two external monitors. These instructions are similar in nature to the [instructions](/index.php/Bumblebee#xf86-video-intel-virtual-crtc_and_hybrid-screenclone "Bumblebee") on the [Bumblebee](/index.php/Bumblebee "Bumblebee") page, though recent advancements in virtual displays on Intel reduce the number of steps and packages needed.

*   First, follow the instructions in the previous section to install drivers for both Intel and Nvidia with Bumblebee.
*   Run `Xorg -configure` to generate a `xorg.conf` file. It may have a different filename, so watch the output and regardless of where it generates it, copy it to `/etc/X11/xorg.conf`. This should generate something like the following (for two external monitors):

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
	Identifier     "X.org Configured"
	Screen      0  "Screen0" 0 0
	Screen      1  "Screen1" RightOf "Screen0"
	InputDevice    "Mouse0" "CorePointer"
	InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
	ModulePath   "/usr/lib/xorg/modules"
	FontPath     "/usr/share/fonts/misc/"
	FontPath     "/usr/share/fonts/TTF/"
	FontPath     "/usr/share/fonts/OTF/"
	FontPath     "/usr/share/fonts/Type1/"
	FontPath     "/usr/share/fonts/100dpi/"
	FontPath     "/usr/share/fonts/75dpi/"
EndSection

Section "Module"
	Load  "glx"
EndSection

Section "InputDevice"
	Identifier  "Keyboard0"
	Driver      "kbd"
EndSection

Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "auto"
	Option	    "Device" "/dev/input/mice"
	Option	    "ZAxisMapping" "4 5 6 7"
EndSection

Section "Monitor"
	Identifier   "Monitor0"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Monitor"
	Identifier   "Monitor1"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Device"
	Identifier  "Card0"
	Driver      "nvidia"
	BusID       "PCI:1:0:0"
EndSection

Section "Device"
	Identifier  "Card1"
	Driver      "intel"
	BusID       "PCI:0:2:0"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0"
	Monitor    "Monitor0"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

Section "Screen"
	Identifier "Screen1"
	Device     "Card1"
	Monitor    "Monitor1"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection
```

*   Change the `bumblebee.conf` file to the following settings (these are scattered throughout the conf file):

 `/etc/bumblebee/bumblebee.conf` 
```
KeepUnusedXServer=true
Driver=nvidia
# In the [driver-nvidia] section,
XorgConfFile=/etc/X11/xorg.conf
```

*   Add the following to your `.xinitrc` file.

 `~/.xinitrc` 
```
# Start Bumblebee, create VIRTUAL display, and configure monitors.
optirun true
intel-virtual-output
xrandr --output VIRTUAL2 --left-of HDMI1 --mode 1920x1080 --auto

# Turn off the laptop display (optional of course, leave out if you want triple display).
xrandr --output LVDS1 --off

# Execute a window manager or desktop environment here.
# ex: exec awesome
```

*   Run `startx` and check that your displays are working.

The modifications to `.xinitrc` automate the configuration of the displays. First, `optirun` is launched to run [Bumblebee](/index.php/Bumblebee "Bumblebee"). Then, the `intel-virtual-output` utility (included with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) versions 2.99+) creates a few `VIRTUAL` displays; `VIRTUAL2` was the display mapping to my HDMI port, run `xrandr` to double check this for yourself. The remaining commands may vary for your configuration, note that `LVDS1` is the laptop screen and `HDMI1` is actually the Display Port.

### WLAN

Some users will need to install the [rfkill](https://www.archlinux.org/packages/?name=rfkill) package in order to switch on the wireless adapter with the fn+F2 key. Remember that [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) will be needed for using a network manager such as [NetworkManager](/index.php/NetworkManager "NetworkManager"), see [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") for more information.

#### Note

It seems that [rfkill](https://www.archlinux.org/packages/?name=rfkill) used in conjunction with [NetworkManager](/index.php/NetworkManager "NetworkManager") will cause a normal shutdown to result in reboot when Wlan is powered off. To avoid this DO NOT install both together.

### Bluetooth

Some users may need to run

```
hciconfig hci0 reset

```

to get blueman working

### Webcam

If the camera seems that it does not work (black image), try to enable/disable auto-exposure (for example in Skype, the option is in the Video Settings and in guc). In reality, the camera tries to record at 0.5 fps and this is why it seems not to work, even if everything seems normal.

### Power management

### Special Touch Keys

The special touch keys are strangely mapped by default. One changes brightness, one does next track. They seem to be linked to the same key sequences as the Fn+F# keys that do the same job. To fix this, make this new file:

 `/opt/dell_touchkeys_keymap` 
```
0x90 previoussong # Previous song
0xA2 playpause # Play/Pause
0x99 nextsong # Next song
0xDB computer # First touch key, Dell apparently uses a key sequence here where 0xDB is a modifer, 0x2D stands for the touch key and 0x19 for the monitor toggle
0x85 prog1 # Second touch key
0x84 media # Third touch key

```

and add this to /etc/rc.local:

 `/etc/rc.local` 
```
…
# Fix touch keys
/usr/lib/udev/keymap input/event0 /opt/dell_touchkeys_keymap

```

[Source](https://bbs.archlinux.org/viewtopic.php?id=131886)

#### Alternative method

For L502x model the above method can be improved:

1.  No need to remap Play/Pause, Previous song, Next song keys as they are mapped correctly by default.
2.  For the first (leftmost) touch key: it's wired in a weird way on the hardware level. It seems to be wired to both Super_L and x. Your best bet would be to remap this using your DE or something like xbindkeys. You may want to double-check with `xev` or `xbindkeys -mk` to see exactly what keys it is producing.

Thus the keymap file should be (I prefer standard location):

 `/usr/lib/udev/keymaps/dell-xps-l502x` 
```
0x85 prog1 # Second touch key
0x84 media # Third touch key

```

and add this to /etc/rc.local:

 `/etc/rc.local` 
```
…
# Fix touch keys
/usr/lib/udev/keymap input/event0 /usr/lib/udev/keymaps/dell-xps-l502x

```

OR make a udev rule (the former remaps keys on boot, this lets udev take care of the remapping):

 `/etc/udev/rules.d/99-local.rules` 
```
…
# Keymap Dell Touch keys
SUBSYSTEM=="input", KERNEL=="event0", RUN+="keymap $name dell-xps-l502x"

```

### Hidden Keyboard Keys

For L502X model: there are additional Fn+<Key> (sequences) that are not marked at all on the keyboard but underlying hardware generates them anyway. Here they are (if you find more add them to the table below):

<caption>Hidden Fn Keys</caption>
| Fn+<Key> | Resulting key (sequence) |
| Fn+Esc | Sleep |
| Fn+Super_L | Super_R |
| Fn+Ins | Pause/Break |
| Fn+Del | Ctrl + Pause/Break |
| Fn+PrntScr | Alt + PrtSc/SysRq |

### Notes

*   Remember to turn on Wi-Fi and Bluetooth by pressing the F2 button.
*   Touchpad can handle multitouch. Read [Synaptics](/index.php/Synaptics "Synaptics") to get that working.
*   Card reader is finnicky. Try booting with a card inserted or inserting a card after it is booted and running `sudo echo 1 > /sys/bus/pci/rescan`. Otherwise, card reader will not be detected. It seems that a certain kernel update results in the workaround not working as well. More info needed.

## Howtos

*   [A fairly comprehensive writeup of running Arch Linux on an XPS 15.](http://drwho.virtadpt.net/archive/2015/01/05/linux-on-the-dell-xps-15-9530)
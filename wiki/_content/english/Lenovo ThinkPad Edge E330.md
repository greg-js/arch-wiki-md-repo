This article covers the Arch Linux support for the Lenovo ThinkPad Edge E330s laptop.

## Contents

*   [1 Review](#Review)
*   [2 Hardware](#Hardware)
    *   [2.1 lspci](#lspci)
*   [3 Configuration](#Configuration)
    *   [3.1 Clickpad](#Clickpad)
    *   [3.2 Jumping cursor on touchpad release](#Jumping_cursor_on_touchpad_release)
    *   [3.3 Video](#Video)
    *   [3.4 Wireless](#Wireless)
        *   [3.4.1 Intel Centrino Wireless-N 2230 (rev c4)](#Intel_Centrino_Wireless-N_2230_.28rev_c4.29)
    *   [3.5 Sound](#Sound)
    *   [3.6 Webcam](#Webcam)
    *   [3.7 Power](#Power)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Brightness control](#Brightness_control)
    *   [4.2 USB 2.0 not working or giving kernel traces](#USB_2.0_not_working_or_giving_kernel_traces)

## Review

Check this [http://www.notebookcheck.net/Review-Lenovo-Thinkpad-Edge-E330-Notebook.83754.0.html](http://www.notebookcheck.net/Review-Lenovo-Thinkpad-Edge-E330-Notebook.83754.0.html) for a hardware review.

## Hardware

My notebook is a Lenovo 3354ALG/3354ALG, BIOS H3ET65WW(1.02) 09/12/2012 with a Core i3-3110M CPU, memory upgraded to 2x4GB and I've instantly replaced the 320GB hdd with a 64GB Crucial m4 slim(!) SSD.

Using **kernel 3.7.2**

| Device | Works |
| Video | Yes |
| Ethernet | Yes |
| Wireless (Intel Centrino Wireless-N 2230 (rev c4) | Yes (but a bit slower than expected, not above 150 MBit/s) |
| Bluetooth | Yes |
| Audio | Yes |
| Camera | Yes |
| Card Reader | Yes |
| USB 2.0 | Yes - see below |
| USB 3.0 | Yes |

### lspci

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
02:00.0 Network controller: Intel Corporation Centrino Wireless-N 2230 (rev c4)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)
08:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 07)

```

## Configuration

### Clickpad

worked out of the box for my with xf86-input-synaptics 1.6.2-4

In some cases it is necessary to add the following to /etc/X11/xorg.conf.d/50-touchpad.conf

```
Section "InputClass"
        Identifier "touchpad"
        MatchProduct "SynPS/2 Synaptics TouchPad"
        Driver "synaptics"
        # fix touchpad resolution
        Option "VertResolution" "100"
        Option "HorizResolution" "65"
        # disable synaptics driver pointer acceleration
        Option "MinSpeed" "1"
        Option "MaxSpeed" "1"
        # tweak the X-server pointer acceleration
        Option "AccelerationProfile" "2"
        Option "AdaptiveDeceleration" "16"
        Option "ConstantDeceleration" "16"
        Option "VelocityScale" "32"
EndSection

```

Also see: [http://forums.lenovo.com/t5/Linux-Discussion/lenovo-e330-touchpad-problem-on-ubuntu-12-04-LTS-32-bit/td-p/1053541](http://forums.lenovo.com/t5/Linux-Discussion/lenovo-e330-touchpad-problem-on-ubuntu-12-04-LTS-32-bit/td-p/1053541)

### Jumping cursor on touchpad release

I struggled with jumping cursor when releasing the finger, making it impossible to hit small objects. It was solved with synclient FingerHigh/Low:

```
synclient FingerHigh=40
synclient FingerLow=40
```

### Video

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Wireless

#### Intel Centrino Wireless-N 2230 (rev c4)

Works out of the box. Module: **iwldvm**

### Sound

Works out of the box. Kernel module: `snd_hda_intel`

### Webcam

Works out of the box (tested using [cheese](https://www.archlinux.org/packages/?name=cheese))

### Power

Suspend works out of the box. Hibernate works using pm-utils (see [Suspend and hibernate#Kernel](/index.php/Suspend_and_hibernate#Kernel "Suspend and hibernate")). [Uswsusp](/index.php/Uswsusp "Uswsusp") was not tested

## Troubleshooting

### Brightness control

Brightness can only be switched between darkest and brightest values using OS method. The fix is to make the `thinkpad-acpi` kernel module control it: append `thinkpad-acpi.brightness_enable=1 acpi.brightness_switch_enabled=0` to the kernel line in the bootloader.

### USB 2.0 not working or giving kernel traces

Not sure if this was solved by using `acpi_backlight=vendor` or by blacklisting these modules I do not use:

```
cat /etc/modprobe.d/modprobe.conf 
blacklist joydev
blacklist pcspkr
blacklist iTCO_vendor_support
blacklist iTCO_wdt

blacklist thinkpad_acpi # it not used by this model and gives warnings about unknown events to the logfiles when loaded.

```
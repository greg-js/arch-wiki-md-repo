| **Device** | **Status** | **Modules** |
| Graphics | **Working** | xf86-video-intel and fglrx (Catalyst) |
| Bluetooth | **Working** | bluetooth |
| Ethernet | **Working** | r8169 |
| Wireless | **Working** | ath9k |
| Audio | **Working** | snd_hda_intel |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** | sdhci/sdhci_pci, jmb38x_ms |
| Touchpad | **Working** | xf86-input-synaptics-led |
| Function Keys | **Working** | hp_wmi |

## Contents

*   [1 Device information](#Device_information)
    *   [1.1 lspci](#lspci)
*   [2 Configuration](#Configuration)
    *   [2.1 Network](#Network)
    *   [2.2 Bluetooth](#Bluetooth)
        *   [2.2.1 hciconfig -a](#hciconfig_-a)
    *   [2.3 Graphics](#Graphics)
        *   [2.3.1 Brightness](#Brightness)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Miscellaneous hardware](#Miscellaneous_hardware)
        *   [2.5.1 Card reader](#Card_reader)
        *   [2.5.2 Function keys](#Function_keys)
        *   [2.5.3 Camera](#Camera)
        *   [2.5.4 HP DriveGuard](#HP_DriveGuard)
    *   [2.6 Power](#Power)
    *   [2.7 Suspend and hibernation](#Suspend_and_hibernation)
        *   [2.7.1 Sensors](#Sensors)

## Device information

This model has many hardware configurations. Mine has an i3 processor, Intel HD Graphics 3000 video card, and an Atheros AR9285 Wi-Fi card.

### lspci

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series/C200 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 6 Series/C200 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 1 (rev b4)
00:1c.1 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 2 (rev b4)
00:1c.2 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 3 (rev b4)
00:1c.3 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 4 (rev b4)
00:1c.5 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 6 (rev b4)
00:1c.7 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 8 (rev b4)
00:1d.0 USB controller: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM65 Express Chipset Family LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 6 Series/C200 Series Chipset Family 6 port SATA AHCI Controller (rev 04)
23:00.0 System peripheral: JMicron Technology Corp. SD/MMC Host Controller (rev 30)
23:00.2 SD Host controller: JMicron Technology Corp. Standard SD Host Controller (rev 30)
23:00.3 System peripheral: JMicron Technology Corp. MS Host Controller (rev 30)
24:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
25:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)
26:00.0 USB controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 04)
```

## Configuration

### Network

Both the wired and wireless network cards works out-of-the-box. The Atheros card requires the **ath9k** module, and the Realtek Ethernet card requires the **r8169** module. More information can be found at [Wireless network configuration#ath9k](/index.php/Wireless_network_configuration#ath9k "Wireless network configuration")

**Note:** With some revisions of this Realtek Ethernet card, better performance may be obtained with the Realtek provided [r8168](https://www.archlinux.org/packages/?name=r8168) module, available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Bluetooth

Sending/receiving files and switching Bluetooth on/off works. The **ath3k** module is required.

#### hciconfig -a

```
hci0:	Type: BR/EDR  Bus: USB
	BD Address: D0:DF:9A:91:B2:51  ACL MTU: 1022:8  SCO MTU: 121:3
	UP RUNNING PSCAN ISCAN 
	RX bytes:1823103 acl:11471 sco:0 events:10296 errors:0
	TX bytes:334040 acl:9846 sco:0 commands:259 errors:0
	Features: 0xff 0xfe 0x0d 0xfe 0x98 0x7f 0x79 0x87
	Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
	Link policy: RSWITCH HOLD SNIFF 
	Link mode: SLAVE ACCEPT 
	Name: '4530s'
	Class: 0x580100
	Service Classes: Capturing, Object Transfer, Telephony
	Device Class: Computer, Uncategorized
	HCI Version: 3.0 (0x5)  Revision: 0x9999
	LMP Version: 3.0 (0x5)  Subversion: 0x9999
	Manufacturer: Atheros Communications, Inc. (69)

```

### Graphics

Intel HD Graphics 3000 is supported by the open-source [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. Dual-head with HDMI works. If using hybrid graphics in conjunction with AMD, [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") works well regarding GPU power management. Switching, however, requires a system reboot or Xorg restart. AMD Catalyst should be installed along with xf86-video-intel to support hybrid (Intel) GPU.

#### Brightness

Controlling screen brightness with the keystrokes `Fn+F2` and `Fn+F3` works in Gnome 3, KDE and MATE and has not been tested in other desktop environments.

### Touchpad

Touchpad function works with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package. Disabling touchpad using the top-left corner double tap works with [xf86-input-synaptics-led](https://aur.archlinux.org/packages/xf86-input-synaptics-led/) and [synaptics-led](https://aur.archlinux.org/packages/synaptics-led/) packages.

### Miscellaneous hardware

#### Card reader

```
23:00.0 System peripheral: JMicron Technology Corp. SD/MMC Host Controller (rev 30)
23:00.2 SD Host controller: JMicron Technology Corp. Standard SD Host Controller (rev 30)
23:00.3 System peripheral: JMicron Technology Corp. MS Host Controller (rev 30)

```

SD cards tested and working. ~~Memory Stick cards do not work, despite having module **jmb38x_ms** loaded. Dmesg does not show any info about Memory Stick card being inserted.~~ With 3.4.7 kernel, Memory Stick card works as intended.

#### Function keys

Module **hp-wmi** is likely to be required for the keys to work. In Gnome 3 and MATE every `Fn+F*` key works. `Fn-F6` key requires gnome-power-manager installed. Keys above numeric keypad are also recognized. The Web key has a XF86HomePage symbol (opens home page) and Wi-Fi key has NoSymbol and does nothing.

#### Camera

Works with **uvcvideo** module.

#### HP DriveGuard

Works with [hpfall-git](https://aur.archlinux.org/packages/hpfall-git/) package.

### Power

Module **acpi-cpufreq** and at least one of CPU governors (**cpufreq_ondemand**, **cpufreq_conservative**, etc.) are required. More informations on [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

**Note:** ~~i915 module parameter i915_enable_rc6 can give up to 2 hours of additional battery life. However it is considered unstable and might cause crashes and graphical glitches. Add **i915.i915_enable_rc6=1** to the kernel command line of your bootloader to try it.~~

*   With laptop-mode-tools, tune from powertop2 and i915_enable_rc6 parameter I was able to get about 5:30h of estimated battery life.
*   Keep in mind that the powertop "good/bad" parameters will not survive a reboot. [As of 3.4.x](http://intellinuxgraphics.org/2012.07.html) rc6 is enabled by default for Ivy Bridge and Sandy Bridge processors. The default (marked -1) is equivalent of i915_enable_rc6=3 which enables rc6 and rc6p. An additional, lower power state can also be enabled by using i915_enable_rc6=7, though this has been reported to sometimes come at the cost of stability. Also, as of [2011Q4](http://intellinuxgraphics.org/2011Q4.html) the i915 module in Sandy Bridge and Ivy Bridge also have framebuffer compression enabled by default.

### Suspend and hibernation

Both suspend and hibernation work with pm-utils and kernel backend.

#### Sensors

[lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) shows one acpitz-virtual device with 4 working temperature readings and coretemp-isa device which has one sensor for each CPU core. It does not show any info about fans RPMs.

```
acpitz-virtual-0
Adapter: Virtual device
temp1:        +51.0°C  (crit = +128.0°C)
temp2:         +0.0°C  (crit = +128.0°C)
temp3:        +38.0°C  (crit = +128.0°C)
temp4:        +50.0°C  (crit = +128.0°C)
temp5:        +26.0°C  (crit = +128.0°C)
temp6:         +0.0°C  (crit = +128.0°C)
temp7:         +0.0°C  (crit = +128.0°C)
temp8:         +0.0°C  (crit = +128.0°C)

coretemp-isa-0000
Adapter: ISA adapter
Physical id 0:  +53.0°C  (high = +80.0°C, crit = +85.0°C)
Core 0:         +49.0°C  (high = +80.0°C, crit = +85.0°C)
Core 1:         +50.0°C  (high = +80.0°C, crit = +85.0°C)
```
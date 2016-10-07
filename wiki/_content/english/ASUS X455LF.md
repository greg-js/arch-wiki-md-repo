## Contents

*   [1 Hardware Information](#Hardware_Information)
    *   [1.1 lspci](#lspci)
    *   [1.2 lsusb](#lsusb)
    *   [1.3 Wired and Wireless Networking](#Wired_and_Wireless_Networking)
    *   [1.4 Bluetooth](#Bluetooth)
    *   [1.5 CPU](#CPU)
    *   [1.6 HDMI Out](#HDMI_Out)
    *   [1.7 Input Devices](#Input_Devices)
    *   [1.8 Graphics](#Graphics)
    *   [1.9 Webcam](#Webcam)
    *   [1.10 Storage](#Storage)
    *   [1.11 RAM](#RAM)
    *   [1.12 BIOS](#BIOS)
    *   [1.13 Battery](#Battery)
    *   [1.14 Thermal](#Thermal)
*   [2 Software Information](#Software_Information)

## Hardware Information

The laptop's model is X455LF-WX031DC

### lspci

```

00:00.0 Host bridge: Intel Corporation Haswell-ULT DRAM Controller (rev 0b)
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)
00:03.0 Audio device: Intel Corporation Haswell-ULT HD Audio Controller (rev 0b)
00:04.0 Signal processing controller: Intel Corporation Device 0a03 (rev 0b)
00:14.0 USB controller: Intel Corporation 8 Series USB xHCI HC (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series HECI #0 (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series HD Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 1 (rev e4)
00:1c.2 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 3 (rev e4)
00:1c.3 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 4 (rev e4)
00:1c.4 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 5 (rev e4)
00:1f.0 ISA bridge: Intel Corporation 8 Series LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series SMBus Controller (rev 04)
00:1f.6 Signal processing controller: Intel Corporation 8 Series Thermal (rev 04)
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
03:00.0 Network controller: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter (rev 01)
04:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 930M] (rev ff)

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 04f2:b483 Chicony Electronics Co., Ltd 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Wired and Wireless Networking

Wireless is working out of the box. Wired networking has not been tested.

### Bluetooth

Detectable by other devices, has not been tested.

### CPU

Intel® Core™ i3-4005U CPU @ 1.70GHz × 4 ( 2 physical, 2 logical cores)

### HDMI Out

Works out of the box, tested with Nvidia binnary driver (364) and intel on board.

### Input Devices

```
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ ETPS/2 Elantech Touchpad                	id=14	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=9	[slave  keyboard (3)]
    ↳ Asus WMI hotkeys                        	id=12	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=13	[slave  keyboard (3)]

```

No touchscreen. Fn + Brightness combination doesn't work. Fn + Volume and media control buttons do work. Fn + Screen On/Off works. Fn + Airplane mode doesn't work. On hibernation touchpad becomes unresponsive. Some say boot some parameters fix it. It didn't in my laptop.

### Graphics

One can Install Nvidia binary drivers to use the Nvidia card. Tested with nvidia-367\. Works as intended. One can use the binary driver's PRIME function to use either Nvidia (High drain, high performance, no hardware video (h264) acceleration meaning vdpau is not accesible? [[1]](https://devtalk.nvidia.com/default/topic/794999/linux/can-t-get-to-work-vdpau-on-optimus-notebook-but-everything-else-works-fine/post/4964577/#4964577) ) or Intel (low drain, hardware video acceleration(h264).

### Webcam

Works out of the box.

### Storage

```
        *-cdrom
             description: DVD-RAM writer
             product: DVDRAM GUE1N
             vendor: HL-DT-ST
             physical id: 0.0.0
             bus info: scsi@1:0.0.0
             logical name: /dev/cdrom
             logical name: /dev/cdrw
             logical name: /dev/dvd
             logical name: /dev/dvdrw
             logical name: /dev/sr0
             version: AS00
             capabilities: removable audio cd-r cd-rw dvd dvd-r dvd-ram
             configuration: ansiversion=5 status=nodisc

```

```
        *-disk
             description: ATA Disk
             product: TOSHIBA MQ01ABF0
             vendor: Toshiba
             physical id: 0.0.0
             bus info: scsi@0:0.0.0
             logical name: /dev/sda
             version: 1J
             serial: SerialNumber
             size: 465GiB (500GB)

```

### RAM

Slot 1 is soldered:

```
description: SODIMM DDR3 Synchronous 1600 MHz (0,6 ns)
product: M471B5173EB0-YK0
vendor: Samsung
physical id: 1
serial: 00000000
slot: ChannelB-DIMM0
size: 4GiB
width: 64 bits
clock: 1600MHz (0.6ns)

```

It has got one free ram slot that is easily accessible using the RAM bay.

### BIOS

User can disable Secure Boot. User can't disable Intel HT There is a choice of compatibility mode, it was accessible at first boot. I set it do enabled some time and disabled later. Now it is grayed out(?). User can disable AES-NI User can disable Intel Virtualization.

### Battery

Design ~37Wh, Usable ~35Wh ASUS Battery

### Thermal

There is a fan that can turn itself off. Sample sensors output while on batter doing light web surfing.

```
acpitz-virtual-0
Adapter: Virtual device
temp1:        +49.0°C  (crit = +103.0°C)
temp2:        +27.8°C  (crit = +105.0°C)
temp3:        +29.8°C  (crit = +105.0°C)

coretemp-isa-0000
Adapter: ISA adapter
Physical id 0:  +50.0°C  (high = +100.0°C, crit = +100.0°C)
Core 0:         +47.0°C  (high = +100.0°C, crit = +100.0°C)
Core 1:         +50.0°C  (high = +100.0°C, crit = +100.0°C)

asus-isa-0000
Adapter: ISA adapter
cpu_fan:        0 RPM
temp1:        +49.0°C  

```

## Software Information

Comes with FreeDos. Tested with Ubuntu 16.04 (Linux 4.4.0-38-generic)
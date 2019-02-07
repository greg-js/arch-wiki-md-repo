This is an install and configuration guide for the Dell Inspiron 13 7000 Series (Model 7375) laptop, Ryzen 7 2700U with Vega Mobile graphics.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Tunning](#Tunning)
    *   [2.1 lm_sensors](#lm_sensors)
    *   [2.2 Disable C6 State](#Disable_C6_State)
    *   [2.3 Grub parameters](#Grub_parameters)
    *   [2.4 Power Saving Modes](#Power_Saving_Modes)
        *   [2.4.1 plugged](#plugged)
        *   [2.4.2 On battery](#On_battery)
        *   [2.4.3 Fan Control](#Fan_Control)
*   [3 Others](#Others)

## Hardware Details

lspci output:

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15d0
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Device 15d1
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:01.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15db
00:08.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15dc
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e8
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e9
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ea
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15eb
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ec
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ed
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ee
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ef
01:00.0 Network controller: Qualcomm Atheros QCA9377 802.11ac Wireless Network Adapter (rev 31)
02:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Raven Ridge [Radeon Vega Series / Radeon Vega Mobile Series] (rev c3)
02:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Device 15de
02:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 15df
02:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e0
02:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e1
02:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Device 15e3
03:00.0 SATA controller: Advanced Micro Devices, Inc. [AMD] FCH SATA Controller [AHCI mode] (rev 61)

```

lsusb output:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 005: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 003 Device 004: ID 0cf3:e009 Qualcomm Atheros Communications 
Bus 003 Device 003: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 003 Device 002: ID 04f3:2494 Elan Microelectronics Corp. 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0bda:58f3 Realtek Semiconductor Corp. 
Bus 001 Device 002: ID 0483:91d1 STMicroelectronics Sensor Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Tunning

### lm_sensors

work as expected, using

```
sensors

```

in order to get temperatures

### Disable C6 State

This will save you freezez, use only if you get them, because it will get hotter.

install [zenstates](https://aur.archlinux.org/packages/zenstates-git/) from aur

```
yay -S zenstates-git

```

Then place create a service that disables C6 on the following path: /lib/systemd/system/disable-c6.service with the following code:

```
[Unit]
Description=Disables C6 state

[Service]
ExecStart=/usr/bin/zenstates --disable-c6

[Install]
WantedBy=multi-user.target

```

Fnally enable de process and reboot

```
sudo systemctl enable disable-c6.service
sudo reboot

```

### Grub parameters

```
quiet radeon.dpm=1 acpi_osi=Linux acpi_backlight=vendor

```

if you get freezez add (but will get hotter):

```
idle=nomwait

```

### Power Saving Modes

#### plugged

```
sudo cpupower frequency-set -g schedutil
echo auto | sudo tee /sys/class/drm/card0/device/power_dpm_force_performance_level

```

schedutil proces less heat than ondemand here

#### On battery

```
sudo cpupower frequency-set -g powersave
echo low | sudo tee /sys/class/drm/card0/device/power_dpm_force_performance_level

```

#### Fan Control

I'm having good results tuning with [nbfc](https://aur.archlinux.org/packages/nbfc/) I made a config based on Dell Inspiron 7348 avivable on [my nbfc fork](https://github.com/danielfm123/nbfc/blob/master/Configs/Dell%20Inspiron%207375.xml) witch has more than the default 2 levels of speed in bios.

Ill pull request upon more testing

## Others

this is wip, please wait
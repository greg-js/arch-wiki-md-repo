This is an install and configuration guide for the Dell Inspiron 13 7000 Series (Model 7375) laptop, Ryzen 7 2700U with Vega Mobile graphics.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Information](#Hardware_Information)
    *   [1.1 Temperatures](#Temperatures)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Screen goes blank](#Screen_goes_blank)
*   [3 Tunning](#Tunning)
    *   [3.1 lm_sensors](#lm_sensors)
    *   [3.2 Kernel and Grub Parameters](#Kernel_and_Grub_Parameters)
    *   [3.3 Power Saving Modes](#Power_Saving_Modes)
        *   [3.3.1 plugged](#plugged)
        *   [3.3.2 On battery](#On_battery)
    *   [3.4 Fan Control](#Fan_Control)
    *   [3.5 Wifi](#Wifi)
    *   [3.6 Blacklisting unused module](#Blacklisting_unused_module)
    *   [3.7 Disable Time Throttling STAPM](#Disable_Time_Throttling_STAPM)
*   [4 Improve Cooling](#Improve_Cooling)

## Hardware Information

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

### Temperatures

The following script will provide all temperatures.

```
#!/bin/bash
echo Sensors
sensors dell_smm-virtual-0
echo CPU real speed
cat /proc/cpuinfo | grep  MHz
echo GPU real speed
sudo cat /sys/kernel/debug/dri/0/amdgpu_pm_info | grep MHz
echo SSD Temp
sudo smartctl -a /dev/sda | grep Temperature

```

you will need smartools and lmsensors

## Troubleshooting

#### Screen goes blank

The boot process normally gets stuck at certain point of the boot process and the scren goes blank. You can check if the caps lock LED still works. If that's the case, it means that **only** the amdgpu driver is gone. The rest of the system will be functional, meaning:

*   You can ssh to that machine
*   You can perform login and some debugging commands in blind mode, dumping their output into some files in the hard disk for posterior checks.

The solution is to disable Legacy Boot in the BIOS, so the UEFI mode will be the one used to boot. Tested with Secure Boot turned **off**

## Tunning

### lm_sensors

work as expected, using

```
sensors

```

in order to get temperatures

### Kernel and Grub Parameters

System will be unstable with kernel bellow 4.20, while you have older kernel add this parameters to grub

```
quiet radeon.dpm=1 acpi_osi=Linux acpi_backlight=vendor amd_iommu=on ivrs_ioapic[4]=00:14.0 ivrs_ioapic[5]=00:00.2 idle=nomwait

```

you can use grub-customizer to make it easier

The upgrade to kernel 4.20 since raven support if there is problem try [linux-amd-raven](https://aur.archlinux.org/packages/linux-amd-raven/) and may be you will want to install after [linux-amd-raven-headers](https://aur.archlinux.org/packages/linux-amd-raven-headers/) in order to build DKMS modules.

If you want bleeding edge features and power saving try [linux-amd-staging-drm-next-git](https://aur.archlinux.org/packages/linux-amd-staging-drm-next-git/) with [linux-amd-staging-drm-next-git-headers](https://aur.archlinux.org/packages/linux-amd-staging-drm-next-git-headers/), but keep idle=nomwait since still causes hangups.

You can also use kernel 5.1 without kernel parameters without hangups or bugs, you will just have to ignore the startup warning messages.

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

once you have kernel 4.20, this setup plus tlp will give you the same battery time as windows.

### Fan Control

I'm having good results tuning with [nbfc](https://aur.archlinux.org/packages/nbfc/) I made a config based on Dell Inspiron 7348 avivable on [my nbfc fork](https://github.com/danielfm123/nbfc/blob/master/Configs/Dell%20Inspiron%207375.xml) witch has more than the default 2 levels of speed in bios.

Ill pull request upon more testing

### Wifi

Broadcom wifi works.... sometimes.... you will need linux firmware package.(if someone can write a tutorial, please help i was using manjaro) I switched for an intel ac 8260 and now works perfect, as a reference, [amazon link](https://www.amazon.com/gp/product/B0197W86IE/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) to the product.

### Blacklisting unused module

There is no support for IPMI in this laptop so we can disable sp5100_tco in `/etc/modprobe.d/sp5100_tco.conf`:

```
blacklist sp5100_tco

```

This will prevent some warnings while booting.

### Disable Time Throttling STAPM

Is you only want CPU/GPU temperature based throttling install [ryzenadj-git](https://aur.archlinux.org/packages/ryzenadj-git/) and run:

```
sudo ryzenadj --slow-time=0xffffffff --stapm-time=0xffffffff

```

You must run the code before running the high demand task, this setting bill be disabled after suspension.

Please improve cooling before doing it.

## Improve Cooling

This laptop gets super hot, in order to decrease temperature and perform long intensive tasks, you can perform the following hardware hacks (witch might void guarantee and i will not take any responsibility for breaking the laptop)

1.- Change Dissipation Paste on the CPU, the included one is not very good

2.- Give fresh air by making holes on the bottom like the ones on the link: [here](https://s3.us-east-2.amazonaws.com/danielfm123-public/proyects/dell+7375/dell+7375+results.jpeg), the holes were performed using 1.5 mm drill (1.0mm is fine too) and this [grid](https://s3.us-east-2.amazonaws.com/danielfm123-public/proyects/dell+7375/grid.pdf)

In order to perform the holes, take the bottom cover out and fir with tape the grid to the inside side of the plate, then drill from inside to outside side of the plate where the lines cross on the grid. After finishing clean very well all the metal residuals.

If you don't have a vertical drill, stick the grid into a 0.5cm wood, and put the wood on top of the plate. It will give you more control.

3.- After doing 1 and 2 you can add a cooling base with a fan in the bottom and you should be able to play games with out burning the laptop.

4.- If you made the holes you can make the laptop more quiet with [this NBFC settings](https://s3.us-east-2.amazonaws.com/danielfm123-public/proyects/dell+7375/Dell+Inspiron+7375+custom.xml)

5.- Add thermal pads (same ones as most GPU RAM have) between CPU and case (not much).
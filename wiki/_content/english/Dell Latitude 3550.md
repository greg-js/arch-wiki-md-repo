Intel Core i7-5500U Processor, NVIDIA GeForce 830M 2GB Graphics 15.6" FHD (1920x1080) Wide View Anti-Glare LED-backlit 8GB1 DDR3L at 1600MHz

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 Graphic](#Graphic)
    *   [2.2 Ethernet](#Ethernet)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Keyboard](#Keyboard)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Cpu frequency scaling](#Cpu_frequency_scaling)

## Installation

You can follow the [Installation guide](/index.php/Installation_guide "Installation guide") to get yourself up and running
booting: uefi boot works with [Systemd-boot](/index.php/Systemd-boot "Systemd-boot")
I try witch efibootmgr but have kernel panic

## Hardware

lspci output:

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation Broadwell-U Host Bridge -OPI (rev 09)
00:02.0 VGA compatible controller: Intel Corporation Broadwell-U Integrated Graphics (rev 09)
00:03.0 Audio device: Intel Corporation Broadwell-U Audio Controller (rev 09)
00:14.0 USB controller: Intel Corporation Wildcat Point-LP USB xHCI Controller (rev 03)
00:16.0 Communication controller: Intel Corporation Wildcat Point-LP MEI Controller #1 (rev 03)
00:1b.0 Audio device: Intel Corporation Wildcat Point-LP High Definition Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #1 (rev e3)
00:1c.2 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #3 (rev e3)
00:1c.3 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #4 (rev e3)
00:1c.4 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #5 (rev e3)
00:1d.0 USB controller: Intel Corporation Wildcat Point-LP USB EHCI Controller (rev 03)
00:1f.0 ISA bridge: Intel Corporation Wildcat Point-LP LPC Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation Wildcat Point-LP SATA Controller [AHCI Mode] (rev 03)
00:1f.3 SMBus: Intel Corporation Wildcat Point-LP SMBus Controller (rev 03)
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
03:00.0 Network controller: Intel Corporation Wireless 7265 (rev 3b)
04:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 830M] (rev ff)

```

Detected modules

 `hwdetect --show-modules` 
```
 AGP      : intel-gtt 
 ACPI     : ac acpi_pad battery button fan processor thermal video 
 BLOCK    : scsi_mod sd_mod ahci libahci libata uvcvideo usb-common usbcore ehci-hcd ehci-pci xhci-hcd xhci-pci 
 CPUFREQ  : acpi-cpufreq pcc-cpufreq 
 CRYPTO   : aesni-intel aes-x86_64 crc32c-intel crc32-pclmul crct10dif-pclmul ghash-clmulni-intel glue_helper ablk_helper cryptd gf128mul lrw 
 DRM      : drm_kms_helper drm i915 
 HWMON    : coretemp hwmon 
 I2C      : i2c-algo-bit i2c-designware-core i2c-designware-platform i2c-i801 i2c-core 
 INPUT    : evdev joydev atkbd mousedev psmouse i8042 libps2 serio serio_raw sparse-keymap hid i2c-hid 
 KVM      : kvm-intel kvm 
 MEDIA    : media uvcvideo v4l2-common videobuf2-core videobuf2-memops videobuf2-vmalloc videodev 
 NET      : r8169 mii iwlwifi rfkill cfg80211 
 SOUND    : pcspkr snd-hwdep snd snd-pcm snd-timer snd-hda-codec snd-hda-controller snd-hda-intel soundcore 
 WATCHDOG : iTCO_vendor_support iTCO_wdt 
 OTHER    : iosf_mbi i8k dw_dmac_core dw_dmac dcdbas gpio-lynxpoint led-class mac_hid lpc_ich mei mei-me mmc_core sdhci-acpi sdhci shpchp dell-laptop dell-wmi mxm-wmi wmi intel_rapl spi-pxa2xx-platform intel_powerclamp x86_pkg_temp_thermal 8250_dw 

```

### Graphic

Install [Bumblebee](/index.php/Bumblebee "Bumblebee")
add following lines in `/etc/bumblebee/xorg.conf.nvidia` :

```
Section "Screen"
    Identifier "Default Screen"
    Device "DiscreteNvidia"
EndSection

```

### Ethernet

Not tested

### Bluetooth

Not tested

### Keyboard

keyboard [issue](http://en.community.dell.com/support-forums/laptop/f/3518/t/19593360?pi239031352=1)
bios version [A5](http://downloads.dell.com/FOLDER02951247M/1/3550A05.exe) : fix keyboard issue

### Touchpad

works with [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

### Cpu frequency scaling

install from aur [thermald](https://aur.archlinux.org/packages/thermald/) or [pstate-frequency](https://aur.archlinux.org/packages/pstate-frequency/)
## Contents

*   [1 Specifications](#Specifications)
*   [2 Hardware](#Hardware)
    *   [2.1 Wi-Fi](#Wi-Fi)
    *   [2.2 Ethernet](#Ethernet)
    *   [2.3 Touchpad](#Touchpad)
    *   [2.4 Webcam](#Webcam)
    *   [2.5 Card reader](#Card_reader)
    *   [2.6 Video](#Video)
    *   [2.7 Sound](#Sound)
    *   [2.8 Multimedia keys](#Multimedia_keys)
    *   [2.9 Fingerprint Reader](#Fingerprint_Reader)
*   [3 Actions](#Actions)
    *   [3.1 Brightness adjustment](#Brightness_adjustment)
    *   [3.2 Hibernation](#Hibernation)
    *   [3.3 Suspend to RAM](#Suspend_to_RAM)

## Specifications

On manufacturer site: [[1]](http://www.dell.com/ru/business/p/vostro-3360/pd)

lspci output:

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.4 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 5 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 Network controller: Atheros Communications Inc. AR9485 Wireless Network Adapter (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8161 Gigabit Ethernet (rev 10)

```

lsusb output:

```
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 138a:0011 Validity Sensors, Inc. VFS5011 Fingerprint Reader
Bus 001 Device 004: ID 0bda:0129 Realtek Semiconductor Corp. 
Bus 001 Device 005: ID 0c45:648b Microdia 
Bus 002 Device 004: ID 0cf3:e004 Atheros Communications, Inc.

```

## Hardware

### Wi-Fi

Works out-of-the-box.

### Ethernet

Works out-of-the-box.

### Touchpad

Touchpad works out-of-the-box.

To turn the touchpad LED on:

```
echo 255 >/sys/class/leds/dell-laptop::touchpad/brightness

```

and off:

```
echo 0 >/sys/class/leds/dell-laptop::touchpad/brightness

```

### Webcam

Works out-of-the-box. You don't need GSPCA for that.

### Card reader

Works out-of-the-box. Notice that rts5139 driver is in staging, so be ready to complain on bugs.

### Video

Intel HD4000 works out-of-the-box.

### Sound

Works out-of-the-box:

```
CONFIG_SND_HDA_INTEL=m
CONFIG_SND_HDA_PREALLOC_SIZE=4096
CONFIG_SND_HDA_HWDEP=y
CONFIG_SND_HDA_RECONFIG=y
CONFIG_SND_HDA_INPUT_BEEP=y
CONFIG_SND_HDA_INPUT_BEEP_MODE=1
CONFIG_SND_HDA_INPUT_JACK=y
CONFIG_SND_HDA_PATCH_LOADER=y
CONFIG_SND_HDA_CODEC_HDMI=y
CONFIG_SND_HDA_CODEC_CIRRUS=y
CONFIG_SND_HDA_GENERIC=y
CONFIG_SND_HDA_POWER_SAVE_DEFAULT=0

```

Other HDA codecs are unnecessary.

Note that full sound support including internal mic support appeared in 3.9 kernel, do consider using it. PulseAudio works OK as well.

### Multimedia keys

No way to make hardware ones work. Brightness, volume and mediaplayer keys work OK. For touchpad toggling consider using my desktop-scripts: [[2]](https://github.com/pfactum/desktop-scripts)

### Fingerprint Reader

Test libfprintd version with VFS5011 Fingerprint Reader support is available here: [[3]](https://github.com/ars3niy/fprint_vfs5011). Work OK.

## Actions

### Brightness adjustment

It's OK to pass the following options to kernel via bootloader:

```
acpi_osi=Linux acpi_backlight=vendor

```

to use native brightness control module. Otherwise it's level won't be stored. But if you use KDE, remove this one:

```
acpi_backlight=vendor

```

otherwise KDE won't be able to adjust brightness.

### Hibernation

It works, but requires several tricks to take bugs away. Create tricks.sh file in /usr/lib/systemd/system-sleep/ folder with the following content:

```
#!/bin/sh

case $1/$2 in
pre/hibernate)
        echo never >/sys/kernel/mm/transparent_hugepage/enabled
        echo 1 >/sys/power/tuxonice/replace_swsusp
        echo 1 >/sys/power/tuxonice/compression/enabled
        echo 1 >/sys/power/tuxonice/user_interface/enable_escape
        echo 1 >/sys/power/tuxonice/user_interface/default_console_level
        echo lzo >/sys/power/tuxonice/compression/algorithm
        echo shutdown >/sys/power/disk
        ifconfig wlan0 down
        uksmctl -d
        sync
        ;;
post/hibernate)
        hdparm -B 253 /dev/sda
        uksmctl -a
        echo madvise >/sys/kernel/mm/transparent_hugepage/enabled
        ;;
pre/suspend)
        uksmctl -d
        sync
        ;;
post/suspend)
        hdparm -B 253 /dev/sda
        uksmctl -a
        ;;
esac

```

and make it executable. It you don't use pf-kernel, remove all strings related to TuxOnIce, UKSM and Transparent Hugepages.

Also it's nice to pass the following option to kernel via bootloader:

```
i8042.nopnp

```

otherwise errors during hibernation may occur. They do not interrupt hibernation, just pollute the screen. Everything works without this option.

### Suspend to RAM

Works out-of-the-box.
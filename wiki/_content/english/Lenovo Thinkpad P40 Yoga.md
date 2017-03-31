| **Device** | **Status** | **Modules** |
| Intel | Working | [i915](/index.php/I915 "I915") |
| Nvidia | Working | [nouveau *or* nvidia](/index.php/NVIDIA_Optimus "NVIDIA Optimus") |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | [xf86-input-synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") |
| Stylus | Working | [wacom](/index.php/Wacom "Wacom") |
| Touchscreen | Working | [wacom](/index.php/Wacom "Wacom") |
| Camera | Working | [uvcvideo](/index.php/Webcam_setup#linux-uvc "Webcam setup") |
| Card Reader | Not tested |
| Bluetooth | Working | btusb |
| Accelerometer | Working | hid_sensor_hub |

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Automatic rotation](#Automatic_rotation)
*   [2 Hardware Overview](#Hardware_Overview)
*   [3 See also](#See_also)

## Configuration

### Automatic rotation

Install [iio-sensor-proxy-git](https://aur.archlinux.org/packages/iio-sensor-proxy-git/). Under [GNOME](/index.php/GNOME "GNOME"), rotation will happen automatically. Under [i3](/index.php/I3 "I3"), you can use this script in the background:

```
#!/bin/sh
# Requires [https://github.com/hadess/iio-sensor-proxy](https://github.com/hadess/iio-sensor-proxy)

dbus-monitor --system interface=org.freedesktop.DBus.Properties,member=PropertiesChanged,path=/net/hadess/SensorProxy 2> /dev/null |
        sed -n -u -e '/string "AccelerometerOrientation"/ {n ; s/\s*variant\s*string\s*"\(.*\)"/\1/p}' |
        while read -r line ; do
                case $line in
                        right-up )
                                xrandr -o right &> /dev/null
                                ;;
                        left-up )
                                xrandr -o left &> /dev/null 
                                ;;
                        bottom-up )
                                xrandr -o inverted &> /dev/null
                                ;;
                        normal | * )
                                xrandr -o normal &> /dev/null
                                ;;
                 esac
        done

```

In order to have your touchpad, Trackpoint, touchscreen and stylus also change orientation, install [xrandr-align](https://github.com/wolneykien/xrandr-align) and run the following script at startup:

```
#!/bin/sh
# Requires [https://github.com/wolneykien/xrandr-align](https://github.com/wolneykien/xrandr-align)

for input in \
        "Wacom Co.,Ltd. Pen and multitouch sensor Finger touch" \
        "Wacom Co.,Ltd. Pen and multitouch sensor Pen stylus" \
        "ETPS/2 Elantech Touchpad" \
        "ETPS/2 Elantech TrackPoint" \
        "Wacom Co.,Ltd. Pen and multitouch sensor Pen eraser" ; do
        xrandr-align monitor --input="$input" &
done

```

## Hardware Overview

 `sudo dmidecode | grep -A3 '^System Information'` 
```
 System Information
         Manufacturer: LENOVO
         Product Name: 20GQCTO1WW
         Version: ThinkPad P40 Yoga

```
 `lspci -nn` 
```
 00:00.0 Host bridge [0600]: Intel Corporation Skylake Host Bridge/DRAM Registers [8086:1904] (rev 08)
 00:02.0 VGA compatible controller [0300]: Intel Corporation HD Graphics 520 [8086:1916] (rev 07)
 00:08.0 System peripheral [0880]: Intel Corporation Skylake Gaussian Mixture Model [8086:1911]
 00:13.0 Non-VGA unclassified device [0000]: Intel Corporation Device [8086:9d35] (rev 21)
 00:14.0 USB controller [0c03]: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller [8086:9d2f] (rev 21)
 00:14.2 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Thermal subsystem [8086:9d31] (rev 21)
 00:16.0 Communication controller [0780]: Intel Corporation Sunrise Point-LP CSME HECI #1 [8086:9d3a] (rev 21)
 00:16.3 Serial controller [0700]: Intel Corporation Device [8086:9d3d] (rev 21)
 00:17.0 SATA controller [0106]: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] [8086:9d03] (rev 21)
 00:1c.0 PCI bridge [0604]: Intel Corporation Device [8086:9d13] (rev f1)
 00:1c.5 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 [8086:9d15] (rev f1)
 00:1d.0 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 [8086:9d18] (rev f1)
 00:1e.0 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Serial IO UART Controller #0 [8086:9d27] (rev 21)
 00:1f.0 ISA bridge [0601]: Intel Corporation Sunrise Point-LP LPC Controller [8086:9d48] (rev 21)
 00:1f.2 Memory controller [0580]: Intel Corporation Sunrise Point-LP PMC [8086:9d21] (rev 21)
 00:1f.3 Audio device [0403]: Intel Corporation Sunrise Point-LP HD Audio [8086:9d70] (rev 21)
 00:1f.4 SMBus [0c05]: Intel Corporation Sunrise Point-LP SMBus [8086:9d23] (rev 21)
 00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection I219-LM [8086:156f] (rev 21)
 02:00.0 SD Host controller [0805]: O2 Micro, Inc. SD/MMC Card Reader Controller [1217:8520] (rev 01)
 03:00.0 Network controller [0280]: Intel Corporation Wireless 8260 [8086:24f3] (rev 3a)
 06:00.0 3D controller [0302]: NVIDIA Corporation GM108GLM [Quadro K620M / Quadro M500M] [10de:137a] (rev ff)

```
 `lsusb` 
```
 Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
 Bus 001 Device 005: ID 138a:0017 Validity Sensors, Inc. Fingerprint Reader
 Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
 Bus 001 Device 003: ID 13d3:5248 IMC Networks 
 Bus 001 Device 002: ID 056a:504a Wacom Co., Ltd 
 Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## See also

[Official Support page](http://support.lenovo.com/ch/en/products/Laptops-and-netbooks/ThinkPad-P-Series-laptops/ThinkPad-P40-Yoga/20GQ?LinkTrack=Solr&beta=false)

[ThinkPad P40 Yoga Platform Specifications](http://psref.lenovo.com/syspool%5CSys/PDF/Think%20Tablets%20_%20Convertibles/ThinkPad%20P40%20Yoga/ThinkPad_P40_Yoga_specs.pdf)
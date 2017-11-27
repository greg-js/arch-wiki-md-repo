| **Device** | **Status** | **Module** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | nvidia (Optimus) |
| Ethernet | Working | r8169 |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel or via HDMI |
| Touchpad | Working | Elantech |
| Camera | Working | uvcvideo |
| Card Reader | Working | rtsx_usb? |
| Bluetooth | Not Tested | bluetooth? |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 Keyboard](#Keyboard)
    *   [2.4 Touchpad](#Touchpad)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 nouveau problems](#nouveau_problems)

# Hardware

This article covers hardware specific configuration for [ASUS N551VW](https://www.asus.com/Laptops/N551VW/specifications/) laptop.

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)                                                                                                                                                           
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #0 (rev 31)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #1 (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #3 (rev f1)
00:1c.3 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #4 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 960M] (rev a2)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTL8411B PCI Express Card Reader (rev 01)
03:00.1 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 12)
```

# Configuration

## Video

Laptop comes with two GPU's (main [INTEL](/index.php/Intel_graphics "Intel graphics") and dedicated [NVIDIA](/index.php/NVIDIA "NVIDIA")):

```
$ lspci | grep "VGA|3D"

```

```
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 960M] (rev a2)
```

NVIDIA Optimus technology can be implemented and controlled using [Bumblebee](/index.php/Bumblebee "Bumblebee") software.

Setting up laptop's screen resolution if the resolution is incorrect:

```
xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync                                                                                                                                                                      
xrandr --addmode eDP-1-1 "1920x1080_60.00"                                                                                                                                                                                                                              
xrandr --output eDP-1-1 --mode 1920x1080_60.00
```

## Audio

Works over regular jack and also over HDMI. For regular jack to work please select Analog Stereo Output in PulseAudio Volume Control. External ASUS subwoofer does not work though (I believe it requires a MS Windows based driver)

## Keyboard

No problems with keyboard keys, function keys not tested. TBC

## Touchpad

This is Elantech touchpad. Please follow instructions from here: [Elantech touchpads](/index.php/Touchpad_Synaptics#Elantech_touchpads "Touchpad Synaptics")

# Troubleshooting

## nouveau problems

disable *nouveau* module:

 `/etc/modprobe.d/blacklist-nouveau.conf`  `blacklist nouveau`
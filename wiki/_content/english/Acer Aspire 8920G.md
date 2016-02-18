This is my 1st ever wiki and I hope that by writing this it can benefit another user out there to setup archlinux on their laptop like me. I should also like to explain that I am a novice in the World of Linux and so I shall try and pass on as much knowledge as I possibly can. These are the settings that apply to my machine and my network setup so you must remember that what works for me will not necessarily work ok for you. This machine is running 2.6.31-ARCH and all the hardware is ok other than having to load the wireless driver iwl4965 and nvidia everything else just worked from the core install.

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Standard Hardware](#Standard_Hardware)
*   [2 System Files and Command Outputs](#System_Files_and_Command_Outputs)
    *   [2.1 Command Outputs](#Command_Outputs)
        *   [2.1.1 lsusb](#lsusb)
        *   [2.1.2 lspci](#lspci)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Wireless](#Wireless)
    *   [3.2 Nvidia Graphics](#Nvidia_Graphics)
*   [4 Power saving](#Power_saving)

## Hardware

### Standard Hardware

| Hardware | Description |
| Processor | Intel(R) Core(TM)2 DuoCPU T8300 @ 2.40GHz |
| System Memory | 4GB DDR2 667 MHz |
| Graphic Card | NVIDIA® GeForce® 9500M GS with up to 1280 MB of TurboCache™ (512 MB of dedicated GDDR2 VRAM, up to 768 MB of shared system memory |
| Display | 18.4” Full HD 1920 x 1080 resolution, high-brightness (300- cd/m2) Acer CineCrystal™ TFT LCD, two lamps, 8 ms high-def response time, 16:9 aspect ratio |
| Sound Card | Intel High Definition Audio Controller |
| CD/DVD | 2X Blu-ray Disc™ Super Multi double-layer drive |
| Lan | Attansic Technology Corp. Atheros AR8121/AR8113/AR8114 PCI-E Ethernet Controller |
| WLan | Intel® Wireless WiFi Link 4965AGN (dual-band quad-mode 802.11a/b/g/Draft-N) |
| WPan | Bluetooth® 2.0+EDR (Enhanced Data Rate) |
| Webcam | Acer OrbiCam integrated 1.3 megapixel |
| Touchpad | Synaptics PS/2 Port Touchpad |
| I/O Interface | 

*   1 x ExpressCard™/54 slot
*   1 x 5-in-one card reader: SD™ Card, MultiMediaCard, Memory Stick®, Memory Stick PRO™ or xD-Picture Card™
*   4 x USB 2.0 Ports
*   1 x HDMI™ port with HDCP support
*   1 x Consumer infrared (CIR) port
*   1 x External display (VGA) port
*   1 x RF-in jack
*   1 x Headphone/speaker/line-out jack with S/PDIF support
*   1 x Microphone-in jack, Line-in jack
*   1 x Acer Bio-Protection fingerprint solution
*   1 x Modem: 56K ITU V.92
*   1 x RF-in jack
*   1 x Acer CineDash media console capacitive human interface device
*   1 x 105-/106-key keyboard English

 |
| Printer | HP Color OfficeJet 6300 |
| NAS | Buffalo Linkstation Pro 1.5Tb |

## System Files and Command Outputs

### Command Outputs

#### lsusb

 `$ lsusb` 
```
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 002: ID 138a:0001 DigitalPersona, Inc Fingeprint Reader
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 003: ID 064e:a103 Suyin Corp. 
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

#### lspci

 `$ lspci` 
```
00:00.0 Host bridge: Intel Corporation Mobile PM965/GM965/GL960 Memory Controller Hub (rev 03)
00:01.0 PCI bridge: Intel Corporation Mobile PM965/GM965/GL960 PCI Express Root Port (rev 03)
00:1a.0 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #4 (rev 03)
00:1a.1 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #5 (rev 03)
00:1a.7 USB Controller: Intel Corporation 82801H (ICH8 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801H (ICH8 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 1 (rev 03)
00:1c.1 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 2 (rev 03)
00:1c.2 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 3 (rev 03)
00:1c.3 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 4 (rev 03)
00:1c.4 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 5 (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB Controller: Intel Corporation 82801H (ICH8 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev f3)
00:1f.0 ISA bridge: Intel Corporation 82801HEM (ICH8M) LPC Interface Controller (rev 03)
00:1f.1 IDE interface: Intel Corporation 82801HBM/HEM (ICH8M/ICH8M-E) IDE Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation 82801HBM/HEM (ICH8M/ICH8M-E) SATA AHCI Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801H (ICH8 Family) SMBus Controller (rev 03)
01:00.0 VGA compatible controller: nVidia Corporation G84 [GeForce 9500M GS] (rev a1)
02:00.0 Ethernet controller: Attansic Technology Corp. Atheros AR8121/AR8113/AR8114 PCI-E Ethernet Controller (rev b0)
08:00.0 Network controller: Intel Corporation PRO/Wireless 4965 AG or AGN [Kedron] Network Connection (rev 61)

```

## Troubleshooting

These are some of the things I needed to download and the configuration files that needed modifying in order to configure the machine to behave as a laptop should... be wireless and consume less power! I assume by this point that you have already got to the stage of a working desktop and just need to dot the i's and cross the t's to polish things off.

### Wireless

Works out of the box. See [Network configuration](/index.php/Network_configuration "Network configuration").

### Nvidia Graphics

I assume by now that you have a working desktop and just need to "tweak" the system for 3-D apps and power management so this is what I changed in my system.

In the /etc/X11/xorg.conf file I made the following changes to allow compiz eye candy and power management. The PowerMizer options are set to lowest performance on battery, with the option of increasing speed if needed and the system will run at full speed when the mains are plugged in.

Make these changes to the Device section

```
Section "Device"
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
   **Option         "AddARGBGLXVisuals" "True"**
   **Option         "NoLogo" "True"**
   **Option         "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefault=0x3; PowerMizerDefaultAC=0x1"**
EndSection

```

## Power saving

See [Power management](/index.php/Power_management "Power management").
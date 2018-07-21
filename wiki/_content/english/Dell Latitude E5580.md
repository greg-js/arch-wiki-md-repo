This is an install and configuration guide for the Dell Lattitude 5580 laptop, testing with Current Release: 2018.07.01, Included Kernel: 4.17.3

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Keyboard](#Keyboard)
    *   [2.3 Touchpad](#Touchpad)
    *   [2.4 Wireless](#Wireless)
    *   [2.5 Ethernet](#Ethernet)
    *   [2.6 USB, SD card slot, ethernet, firewire, HDMI, webcam and mediakeys](#USB.2C_SD_card_slot.2C_ethernet.2C_firewire.2C_HDMI.2C_webcam_and_mediakeys)
    *   [2.7 LSPCI Output](#LSPCI_Output)
    *   [2.8 optirun nvidia-smi Output](#optirun_nvidia-smi_Output)
    *   [2.9 Dell WD15 Displayport/USB-C Dock](#Dell_WD15_Displayport.2FUSB-C_Dock)
    *   [2.10 Dell TB16 Thunderbolt 3 Dock](#Dell_TB16_Thunderbolt_3_Dock)

## Installation

Installation proceeds as normal after altering the kernel boot parameters to blacklist nouveau (modprobe.blacklist=nouveau)

AUR was not needed for any part of hardware installation/compatibility and is entirely optional.

## Configuration

All other hardware works adequately with the exclustion of the nouveau driver, Tested with nmcli and NetworkManager for wifi and ethernet

### Video

Tested model comes with an optimus enabled Intel HD Graphics 630 and Nvidia MX940\. In order to boot you will need to blacklist the nouveau driver during installation, and later during installation. However the arch provided nvidia drivers work well. Also suggest installing the related arch provided intel drivers. Additionally I needed to install the bumblebee drivers in order to gain smooth use of both GPU's but it did also fully support multiple monitors gracefully.

### Keyboard

Keyboard worked with full function key and backlight support.

### Touchpad

Touchpad worked added the synamptics drivers in order to enable extra features.

### Wireless

Intel Corporation Wireless 8265 / 8275 (rev 78) works without complaint.

### Ethernet

Intel Corporation Ethernet Connection (5) I219-LM (rev 31) works without complaint

### USB, SD card slot, ethernet, firewire, HDMI, webcam and mediakeys

All work without complaint

### LSPCI Output

	00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 05)

	00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 05)

	00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)

	00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 05)

	00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)

	00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)

	00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #0 (rev 31)

	00:15.1 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #1 (rev 31)

	00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)

	00:16.3 Serial controller: Intel Corporation Sunrise Point-H KT Redirection (rev 31)

	00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA controller [AHCI mode] (rev 31)

	00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #2 (rev f1)

	00:1c.2 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #3 (rev f1)

	00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)

	00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)

	00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)

	00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)

	00:1f.3 Audio device: Intel Corporation CM238 HD Audio Controller (rev 31)

	00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)

	00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (5) I219-LM (rev 31)

	01:00.0 3D controller: NVIDIA Corporation Device 179c (rev a2)

	02:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)

	03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

	3d:00.0 Non-Volatile memory controller: Kingston Technology Company, Inc. Device 5008 (rev 01)

### optirun nvidia-smi Output

NVIDIA-SMI 396.24 Driver Version: 396.24 GPU Name: GeForce 940MX Bus-Id 00000000:01:00.0

### Dell WD15 Displayport/USB-C Dock

Works with all ports and hotplug Ethernet detects as realtek USB Ethernet device

### Dell TB16 Thunderbolt 3 Dock

Works with all ports and hotplug Ethernet detects as realtek USB Ethernet device
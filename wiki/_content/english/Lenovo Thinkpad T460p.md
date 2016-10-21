## Contents

*   [1 Overview](#Overview)
*   [2 Firmware](#Firmware)
*   [3 Hardware information](#Hardware_information)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 Failure to load 3rd party kernel modules](#Failure_to_load_3rd_party_kernel_modules)

## Overview

The **Lenovo ThinkPad T460p** is a high-performance laptop with very good Linux support out of the box.

## Firmware

It is recommended that you peruse all the available options and features in the BIOS as there are many of them and in some cases you will get unexpected behaviours, e.g. swapping the Fn and Ctrl keys, enabling topmost keyboard row F1-F12 functionality as the default, etc. To access the BIOS, press ENTER key on boot-up. Enable Diagnostics mode bootup instead of Quick mode to make it easier to enter the BIOS.

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:01.2 PCI bridge: Intel Corporation Skylake PCIe Controller (x4) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (2) I219-LM (rev 31)
02:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)
03:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)

```

The output of *lsusb* is

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 138a:0090 Validity Sensors, Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Troubleshooting

## Failure to load 3rd party kernel modules

In laptops with [Secure Boot](/index.php/Secure_Boot "Secure Boot") enabled, if you install a kernel module provided by a 3rd party or compiled by yourself, *modprobe* will not load it and will throw an error similar to this:

```
modprobe: ERROR: could not insert 'vboxdrv': Required key not available

```

Secure Boot will prevent this module from running until you provide a valid signature for it. Therefore, you can either [try to sign it yourself](https://flavioprimo.xyz/linux/how-to-install-virtualbox-on-ubuntu-having-uefi-secure-boot-enabled/) or disable Secure Boot altogether. Unfortunately, the current Secure Boot firmware (v2.11 2016/09/26) installed in the ThinkPad T460 series BIOS [is unable to complete the signing process](https://github.com/rhinstaller/shim/issues/55), thus it is recommended to disable it in the BIOS configuration until this issue is resolved.

See also: [http://askubuntu.com/questions/802668/virtualbox-installation-gives-message-modprobe-vboxdrv-failed](http://askubuntu.com/questions/802668/virtualbox-installation-gives-message-modprobe-vboxdrv-failed)
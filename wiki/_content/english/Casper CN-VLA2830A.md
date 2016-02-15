## Contents

*   [1 Hardware Information](#Hardware_Information)
    *   [1.1 lspci](#lspci)
    *   [1.2 lsusb](#lsusb)
    *   [1.3 Wired and Wireless Networking](#Wired_and_Wireless_Networking)
    *   [1.4 Bluetooth](#Bluetooth)
    *   [1.5 CPU](#CPU)
    *   [1.6 TouchPad](#TouchPad)
    *   [1.7 Webcam](#Webcam)
    *   [1.8 Input Devices](#Input_Devices)
    *   [1.9 Storage](#Storage)
    *   [1.10 RAM](#RAM)
    *   [1.11 Manufacturer](#Manufacturer)
*   [2 Software Information](#Software_Information)
    *   [2.1 BIOS](#BIOS)

## Hardware Information

### lspci

```

00:00.0 Host bridge: Intel Corporation ValleyView SSA-CUnit (rev 0e)
00:02.0 VGA compatible controller: Intel Corporation ValleyView Gen7 (rev 0e)
00:13.0 SATA controller: Intel Corporation ValleyView 6-Port SATA AHCI Controller (rev 0e)
00:14.0 USB controller: Intel Corporation ValleyView USB xHCI Host Controller (rev 0e)
00:1a.0 Encryption controller: Intel Corporation ValleyView SEC (rev 0e)
00:1b.0 Audio device: Intel Corporation ValleyView High Definition Audio Controller (rev 0e)
00:1c.0 PCI bridge: Intel Corporation ValleyView PCI Express Root Port (rev 0e)
00:1c.1 PCI bridge: Intel Corporation ValleyView PCI Express Root Port (rev 0e)
00:1f.0 ISA bridge: Intel Corporation ValleyView Power Control Unit (rev 0e)
00:1f.3 SMBus: Intel Corporation ValleyView SMBus Controller (rev 0e)
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 07)
RTL8723BE

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 05e3:0745 Genesys Logic, Inc. 
Bus 001 Device 002: ID 05e3:0608 Genesys Logic, Inc. USB-2.0 4-Port HUB
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Wired and Wireless Networking

Wired works out of the box.

Wireless works out of the box with kernel 4 and up, but It has issues. WiFi NIC is accessible with the removal of the entire under cover of laptop, replacing it is easy.

### Bluetooth

Works out of the box

### CPU

Intel(R) Celeron(R) CPU N2830 @ 2.16GHz

You can't shut the laptop down sometimes. A user reported there is need for a microcode to shutdown [[1]](https://communities.intel.com/thread/54149) and [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1341925) . You can get the related microcode here: [[3]](https://chromium.googlesource.com/chromiumos/third_party/coreboot/+/379bf9beb361d392dc5d4b52220b3a3b274cdf01/src/soc/intel/baytrail/microcode/M0C30678_00000829.h) but it does not fix the issue, it just makes it happen less often.

### TouchPad

Use Kernel 4 and up, and put this "i8042.kbdreset=1" in GRUB_CMDLINE_LINUX_DEFAULT for touchpad to work after a restart. Bug here [[4]](https://bugzilla.kernel.org/show_bug.cgi?id=81331)

### Webcam

Works out of the box.

### Input Devices

```
Input Devices
Lid Switch	
Power Button	
Sleep Button	
Power Button	
AT Translated Set 2 keyboard	
Video Bus	
ETPS/2 Elantech Touchpad	
HDA Intel PCH Mic	
HDA Intel PCH Headphone	
HDA Intel PCH HDMI/DP,pcm

```

### Storage

```
TSSTcorp CDDVDW SU-208DB	
ATA WDC WD5000LPVX-2	
Generic STORAGE DEVICE	#Card Reader

```

### RAM

Has Single Slot

Elixir m2s4g64cc88b4n #4GB, Datasheet [[5]](http://www.elixir-memory.com/products/file/B3070-144004(4GB_8GB_DDR3_B_Die_Elixir-SODIMM_Datasheet).pdf)

### Manufacturer

It is probably made by Lengda, since battery info says Lengda. Very similar to this [[6]](http://www.lengdatek.com/detail.asp?ThisproductID=85&TengsoID=2039)

## Software Information

It comes with Windows 8.1\. Key embedded in bios. It is not "Bing Edition"

### BIOS

User can disable secure boot.

UEFI or Legacy mode. Legacy mode is not tested.

Tested with Ubuntu 14.04 for now.
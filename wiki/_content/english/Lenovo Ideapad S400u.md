This article covers the Arch Linux support for the [Lenovo Ideapad S400u ultrabook](http://mobilesupport.lenovo.com/us/en/documents/pd026502).

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 inxi](#inxi)
    *   [1.2 lspci](#lspci)
*   [2 Configuration](#Configuration)
    *   [2.1 Jumping cursor on touchpad release](#Jumping_cursor_on_touchpad_release)
    *   [2.2 Video](#Video)
    *   [2.3 Brightness Control](#Brightness_Control)

## Hardware

This model has a 32 GB SSD. It comes with Windows 8 pre-installed.

Using **kernel 3.14.4-1-ARCH**.

### inxi

Version: 2.1.28.

 `inxi -F -M` 
```
System:    Host: arch Kernel: 3.14.4-1-ARCH x86_64 (64 bit) Desktop: i3 4.7.2-177-gf41e81b Distro: Arch Linux 
Machine:   System: LENOVO product: VIUS3 v: Lenovo IdeaPad S400U
           Mobo: LENOVO model: INVALID v: 31900004WIN8 STD SGL Bios: LENOVO v: 6DCN92WW(V8.06) date: 02/21/2013
CPU:       Dual core Intel Core i5-3317U (-HT-MCP-) cache: 3072 KB 
           Clock Speeds: 1: 946 MHz 2: 999 MHz 3: 813 MHz 4: 840 MHz
Graphics:  Card: Intel 3rd Gen Core processor Graphics Controller
           Display Server: X.Org 1.15.1 driver: intel Resolution: 1366x768@60.01hz
           GLX Renderer: Mesa DRI Intel Ivybridge Mobile GLX Version: 3.0 Mesa 10.1.4
Audio:     Card Intel 7 Series/C210 Series Family High Definition Audio Controller driver: snd_hda_intel 
           Sound: Advanced Linux Sound Architecture v: k3.14.4-1-ARCH
Network:   Card-1: Qualcomm Atheros AR9285 Wireless Network Adapter (PCI-Express) driver: ath9k
           IF: wlp2s0 state: up mac: 1c:3e:84:da:7f:f5
           Card-2: Realtek RTL8101E/RTL8102E PCI Express Fast Ethernet controller driver: r8169
           IF: enp1s0 state: down mac: 64:1c:67:5e:aa:1c
Drives:    HDD Total Size: 533.6GB (35.4% used) ID-1: /dev/sdb model: WDC_WD5000LPVT size: 500.1GB
           ID-2: /dev/sda model: MZMPC032HBCD size: 32.0GB ID-3: USB /dev/sdd model: Internal_Storage size: 1.4GB
Partition: ID-1: / size: 30G used: 13G (46%) fs: ext4 dev: /dev/sda1 
           ID-2: /home size: 306G used: 149G (52%) fs: ext4 dev: /dev/sdb7 
           ID-3: swap-1 size: 4.00GB used: 0.02GB (1%) fs: swap dev: /dev/sdb5 
Sensors:   System Temperatures: cpu: 53.0C mobo: N/A 
           Fan Speeds (in rpm): cpu: 0
Info:      Processes: 178 Uptime: 10:04 Memory: 2089.3/3826.2MB Client: Shell (zsh) inxi: 2.1.28 

```

### lspci

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E PCI Express Fast Ethernet controller (rev 05)
02:00.0 Network controller: Qualcomm Atheros AR9285 Wireless Network Adapter (PCI-Express) (rev 01)

```

## Configuration

### Jumping cursor on touchpad release

It might be solved with synclient FingerHigh and FingerLow:

```
synclient FingerHigh=40
synclient FingerLow=40
```

### Video

Drivers: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) and [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver).

### Brightness Control

Works okay with the corresponding Fn keys.
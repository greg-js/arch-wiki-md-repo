# ASUS K52J

**The parameters depend on the submodel...**

## Contents

*   [1 Model K52JT-SX011V:](#Model_K52JT-SX011V:)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 Graphics](#Graphics)
        *   [1.2.1 Setting resolution](#Setting_resolution)
        *   [1.2.2 Setting Brightness](#Setting_Brightness)
        *   [1.2.3 Hibernate and Suspend](#Hibernate_and_Suspend)
    *   [1.3 Touchpad](#Touchpad)
    *   [1.4 DVD](#DVD)
    *   [1.5 Sound](#Sound)
    *   [1.6 Webcam](#Webcam)
    *   [1.7 Networking](#Networking)
        *   [1.7.1 LAN](#LAN)
        *   [1.7.2 sd-cardreader](#sd-cardreader)
        *   [1.7.3 WLAN](#WLAN)
        *   [1.7.4 bluetooth](#bluetooth)
    *   [1.8 Untested](#Untested)
    *   [1.9 lspci](#lspci)

# Model K52JT-SX011V:

## Hardware

*   **Processor:** Intel Core i7 740QM 1.73 GHz (Turbo up to 2.93GHz)
*   **Display:** - 15.6" (HD, Glare Type) / ATI HD6370 1G GDDR3 VRAM
*   **HDD:**
*   **Card Reader:** SD-card, Memory Stick, MultiMediaCard
*   **DVD:**
*   **Webcam:**
*   **WLAN:** - Gbe - WLAN 802.11bgn
*   **LAN:**
*   **Bluetooth**

## Graphics

See [ATI](/index.php/ATI "ATI").

### Setting resolution

See [xrandr](/index.php/Xrandr "Xrandr").

### Setting Brightness

Strangely enough the keyboard buttons works out of the box: `Fn+F5` and `Fn+F6`.

### Hibernate and Suspend

The USB unbind hook is no longer necessary as of [Linux 3.5](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=dbf0e4c7257f8d684ec1a3c919853464293de66e).

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## DVD

Works fine with no configuration required.

## Sound

Works.

## Webcam

Works fine, a little strange but ok. Cheese works fine out of the box.

## Networking

### LAN

Works fine with no configuration required.

### sd-cardreader

Works fine with no configuration required.

### WLAN

Works fine with no configuration required.

### bluetooth

Works fine with no configuration required.

## Untested

*   VGA port

## lspci

```
00:00.0 Host bridge: Intel Corporation Core Processor DMI (rev 11)
00:03.0 PCI bridge: Intel Corporation Core Processor PCI Express Root Port 1 (rev 11)
00:08.0 System peripheral: Intel Corporation Core Processor System Management Registers (rev 11)
00:08.1 System peripheral: Intel Corporation Core Processor Semaphore and Scratchpad Registers (rev 11)
00:08.2 System peripheral: Intel Corporation Core Processor System Control and Status Registers (rev 11)
00:08.3 System peripheral: Intel Corporation Core Processor Miscellaneous Registers (rev 11)
00:10.0 System peripheral: Intel Corporation Core Processor QPI Link (rev 11)
00:10.1 System peripheral: Intel Corporation Core Processor QPI Routing and Protocol Registers (rev 11)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 06)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 06)
00:1c.1 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 2 (rev 06)
00:1c.2 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 3 (rev 06)
00:1c.5 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 (rev 06)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a6)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 06)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 4 port SATA AHCI Controller (rev 06)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 06)
01:00.0 VGA compatible controller: ATI Technologies Inc Robson CE [AMD Radeon HD 6300 Series]
01:00.1 Audio device: ATI Technologies Inc Manhattan HDMI Audio [Mobility Radeon HD 5000 Series]
03:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
05:00.0 System peripheral: JMicron Technology Corp. SD/MMC Host Controller (rev 80)
05:00.2 SD Host controller: JMicron Technology Corp. Standard SD Host Controller (rev 80)
05:00.3 System peripheral: JMicron Technology Corp. MS Host Controller (rev 80)
05:00.4 System peripheral: JMicron Technology Corp. xD Host Controller (rev 80)
05:00.5 Ethernet controller: JMicron Technology Corp. JMC250 PCI Express Gigabit Ethernet Controller (rev 03)
ff:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-Core Registers (rev 04)
ff:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 04)
ff:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 04)
ff:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 04)
ff:03.0 Host bridge: Intel Corporation Core Processor Integrated Memory Controller (rev 04)
ff:03.1 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Target Address Decoder (rev 04)
ff:03.4 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Test Registers (rev 04)
ff:04.0 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 0 Control Registers (rev 04)
ff:04.1 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 0 Address Registers (rev 04)
ff:04.2 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 0 Rank Registers (rev 04)
ff:04.3 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 0 Thermal Control Registers (reva 04)
ff:05.0 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 1 Control Registers (rev 04)
ff:05.1 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 1 Address Registers (rev 04)
ff:05.2 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 1 Rank Registers (rev 04)
ff:05.3 Host bridge: Intel Corporation Core Processor Integrated Memory Controller Channel 1 Thermal Control Registers (rev 04)

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_K52J&oldid=377654](https://wiki.archlinux.org/index.php?title=ASUS_K52J&oldid=377654)"
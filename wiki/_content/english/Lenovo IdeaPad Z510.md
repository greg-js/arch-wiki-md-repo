## Contents

*   [1 System Specification](#System_Specification)
*   [2 BIOS](#BIOS)
*   [3 Networking](#Networking)
    *   [3.1 Wired Ethernet](#Wired_Ethernet)
    *   [3.2 Wireless](#Wireless)
        *   [3.2.1 Atheros](#Atheros)
        *   [3.2.2 Broadcom](#Broadcom)
*   [4 Graphics](#Graphics)
    *   [4.1 Intel HD](#Intel_HD)
    *   [4.2 nVidia GeForce](#nVidia_GeForce)
*   [5 Sound](#Sound)
    *   [5.1 Via Kernel: snd_pcm_intel parameters](#Via_Kernel:_snd_pcm_intel_parameters)
*   [6 Trackpad](#Trackpad)
*   [7 Suspend/Hibernate](#Suspend.2FHibernate)

## System Specification

**Note:** Specifications might differ.

*   Processor: 4th Generation Intel Core i5-4200M OR i7-4702MQ Processor
*   Memory: 4/8GB PC3-12800 DDR3L SDRAM 1600 MHz
*   WiFi: Qualcomm Atheros AR9485 OR Broadcom BCM43142 802.11b/g/n Wireless Network Adapter
*   Hard-Drive: 1TB 5400 rpm
*   Optical Drive: DVD Recordable (Dual Layer)
*   Integrated Graphics: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller
*   Accelerated Graphics: NVIDIA GeForce GT 740M 1GB (optional)
*   Sound: Intel HDA
*   Screen: 15.6 *1366x768 (or higher) "AntiGlare" (Matte)*
*   SD Card Reader
*   Ethernet: Fast-Ethernet

## BIOS

**Warning:** Updating the BIOS is risky, be sure about what your are doing! Also remember this is at your own risk and you may get no support when flashing goes wrong.

**Note:** At the moment it is only possible to flash on Microsoft Windows 8 (64-bit), no Linux method hasn't been released (yet).

Lenovo released [a new BIOS](http://mobilesupport.lenovo.com/us/en/products/laptops-and-netbooks/ideapad-z-series-laptops/ideapad-z510-notebook/downloads/DS100474) rom that fixes some issues. The V39 version should fix the following:

*   Phase in V39 BIOS into Zx10 for solving CPU 0.77GHz issue
*   Solve Windows 7 SLP2.0 function issue

Although it fixes Microsoft Windows issues, it could also effect (Arch) Linux.

## Networking

### Wired Ethernet

Works without any issues. Remember it only features Fast Ethernet.

### Wireless

#### Atheros

Works out-of-the-box. Remember to press the airplane mode button to turn on the wireless card or use the following command:

```
# iwconfig wlp2s0 txpower on

```

#### Broadcom

Install the Broadcom-driver as provided in [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) AUR.

## Graphics

### Intel HD

Follow the [Intel](/index.php/Intel "Intel") Graphics Wiki to install. VGA-video output is working.

### nVidia GeForce

[Bumblebee](/index.php/Bumblebee "Bumblebee") provides support for the dedicated [NVIDIA](/index.php/NVIDIA "NVIDIA") video-card.

## Sound

Works out of the box with [ALSA](/index.php/ALSA "ALSA") and [PulseAudio](/index.php/PulseAudio "PulseAudio"). Arch Linux detects the HDMI as the first sound card and PCH (jack plug) as the second one. This might be undesirable on most applications, which will try, by default, to send sound through the HDMI port. You can either solve this by changing the order in which the kernel detects the cards, effectively making PCH as the card 0\. Another option is by configuring "asoundrc" to use the second card (number 1). either in your home directory or system-wide (on etc). The latter option has the problem of you manually having to reconfigure that on pulseaudio or other applications that override that setting. **Don't use the two options at the same time**, as they'll reverse each others effect: choose the one that most fits your needs.

### Via Kernel: snd_pcm_intel parameters

Simply create a file, /etc/modprobe.d/alsa-card-reordering.conf containing the following line:

 `options snd-hda-intel index=1,0` 

This solution is adapted from [here](http://alsa.opensrc.org/MultipleCards#Reordering_the_driver_for_a_particular_card).

## Trackpad

As of Kernel 3.15.2-1, the trackpad - including two-finger scroll - should work out of the box.

## Suspend/Hibernate

Suspend and Hibernate doesn't work out of the box because of hybrid graphics. Adding `acpi_osi=! acpi_osi="Windows 2009"` to [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") fixes the issue. [[1]](https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29)
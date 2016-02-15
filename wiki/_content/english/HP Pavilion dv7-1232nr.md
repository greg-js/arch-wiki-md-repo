## Contents

*   [1 Hardware Specifications](#Hardware_Specifications)
*   [2 Configuration](#Configuration)
    *   [2.1 Processor](#Processor)
    *   [2.2 Video](#Video)
    *   [2.3 Audio](#Audio)
    *   [2.4 LAN](#LAN)
    *   [2.5 WLAN](#WLAN)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Card Reader](#Card_Reader)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 QuickPlay buttons](#QuickPlay_buttons)

## Hardware Specifications

*   AMD Turion X2 Dual-Core Mobile Processor RM-74 (2.2 GHz, 1MB L2 Cache)
*   17.0" Diagonal WXGA+ High-Definition BrightView Widescreen Display (1440 x 900)
*   4GB DDR2 SDRAM (2 DIMM)
*   ATI Radeon HD 3200 Graphics (256 MB)
*   320GB 5400RPM SATA Hard Drive
*   Realtek RTL8101E/RTL8102E LAN
*   Atheros AR5001 802.11b/g WLAN
*   SuperMulti 8x DVD+/-R/RW drive with Double Layer Support
*   Webcam
*   JMicron SD,MS/Pro,MMC,XD Card Reader
*   3 USB 2.0, HDMI, eSATA ports

## Configuration

### Processor

Frequency scaling works with [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") using the "**powernow-k8**" module. Available frequencies are 2.20 GHz, 1.10 GHz, and 550 MHz

### Video

Using "xf86-video-ati" driver for the ATI card. No xorg.conf file needed. Seems to function properly with and without KMS enabled. Display supports 1440x900 @ 60 Hz. HDMI output not tested.

### Audio

All necessary modules are automatically loaded.

### LAN

All necessary modules are automatically loaded. Requires the "**r8169**" module

### WLAN

All necessary modules are automatically loaded. Requires the "**ath5k**" module

### Webcam

All necessary modules are automatically loaded. Tested with Cheese (GNOME webcam app)

### Card Reader

All necessary modules are automatically loaded.

## Troubleshooting

### QuickPlay buttons

*   Mute button works as expected
*   Volume control works as expected
*   Rewind, play, fast forward and stop buttons not tested
*   Wireless button does not appear to enable/disable wireless, further setup may be needed for this
## Contents

*   [1 Hardware Specifications](#Hardware_Specifications)
*   [2 Configuration](#Configuration)
    *   [2.1 Processor](#Processor)
    *   [2.2 Video](#Video)
    *   [2.3 Audio](#Audio)
    *   [2.4 LAN](#LAN)
    *   [2.5 WLAN](#WLAN)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Touchpad](#Touchpad)
    *   [2.8 Card Reader](#Card_Reader)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 QuickPlay buttons](#QuickPlay_buttons)
    *   [3.2 Untested Peripherals](#Untested_Peripherals)

## Hardware Specifications

*   AMD Turion X2 Dual-Core Mobile Processor ZM-82 (2.2 GHz, 1MB L2 Cache)
*   17.3" Diagonal WXGA+ High-Definition BrightView Widescreen Display (1440 x 900)
*   4GB DDR2 SDRAM (2 DIMM)
*   ATI Mobility Radeon HD 4530 (512 MB)
*   500GB 5400RPM SATA Hard Drive
*   Realtek RTL8111/8168B Gigabit LAN
*   Atheros AR9285 WLAN
*   DVD+/-R/RW SuperMulti (Lightscribe burner)
*   Webcam
*   JMicron SD,MS/Pro,MMC,XD Card Reader
*   4 USB 2.0, HDMI, eSATA ports

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

All necessary modules are automatically loaded. Requires the "**ath9k**" module

### Webcam

All necessary modules are automatically loaded. Tested with Cheese (GNOME webcam app)

### Touchpad

Works with "**xf86-input-synaptics**" driver.

### Card Reader

JMicron card reader not working. Further setup needed for this.

## Troubleshooting

### QuickPlay buttons

*   Mute button not working
*   Volume control not working
*   Rewind, play, fast forward and stop buttons not tested
*   Wireless button not tested

### Untested Peripherals

*   LightScribe
*   FireWire
*   PCMCIA Socket
*   eSATA Port
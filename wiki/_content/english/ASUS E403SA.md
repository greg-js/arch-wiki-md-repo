| **Device** | **Status** | **Modules** |
| Graphics | Working | xf86-video-intel |
| Wireless | Working | ath9k |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Webcam | Working | uvcvideo |
| Suspend | Working | systemd-suspend |
| Function keys | Working |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
    *   [1.1 E403SA-WX0026T](#E403SA-WX0026T)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
    *   [2.3 Touchpad](#Touchpad)

## Hardware

### E403SA-WX0026T

*   **Processor:** Intel Pentium N3700 1.60 GHz (2.4 GHz max)
*   **Display:** 14.0", 1366x768
*   **Graphics:** Integrated Intel HD Graphics 400 (Braswell)
*   **SSD:** 128GB eMMC
*   **Memory:** 4 GiB Hynix DIMM DDR3 1600 MHz
*   **Card Reader:** Realtek RTS5129 (SD)
*   **Webcam:** 640x480
*   **WLAN:** Qualcomm Atheros AR9462
*   **Bluetooth:** IMC Networks Atheros AR3012
*   **Touchpad:** Elantech

## Configuration

### CPU

Read [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") about managing frequency.

### Video

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), read [Intel graphics](/index.php/Intel_graphics "Intel graphics") for graphics driver setup. Both SNA and UXA acceleration works well.

### Touchpad

The touch works out of the box, read the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") page for driver install and configuration.
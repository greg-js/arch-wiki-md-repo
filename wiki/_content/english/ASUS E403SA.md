| **Device** | **Status** | **Modules** |
| Graphics | Working | xf86-video-intel |
| Wireless | Working | ath9k |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Webcam | Working | uvcvideo |
| Suspend | Working | systemd-suspend |
| Function keys | Partially working |

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 E403SA-WX0026T](#E403SA-WX0026T)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
    *   [2.3 Touchpad](#Touchpad)
    *   [2.4 Wi-Fi](#Wi-Fi)
*   [3 Problems](#Problems)
    *   [3.1 ACPI](#ACPI)

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

### Wi-Fi

Connecting wirelessly works out of the box with the `ath9k` driver, but times out sometimes during the DHCP lease process. Configuration can be done by editing the `/etc/modprobe.d/ath9k.conf` file. For example:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k ps_enable=0 bt_ant_diversity=1 nohwcrypt=1` 

The `ps_enable=0` option disables power saving mode. `bt_ant_diversity=1` enables [antenna diversity](https://wireless.wiki.kernel.org/en/users/drivers/ath9k/antennadiversity). `nohwcrypt=1` disables encryption and decryption with hardware which may solve some connection issues.

## Problems

### ACPI

ACPI functions such as the lid switch and `fn` keys do not work properly. Closing the lid will not suspend the laptop and pressing `fn`+`F6` will not increase the screen backlight. Suspending with the power key and resuming from suspend by opening the lid does work. `acpi_listen` only detects mute, volume up, volume down keys. However, when removing "Windows 2012" from the ACPI strings by setting `acpi_osi="!Windows 2012"` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), the lid switch and all `fn` keys work perfectly but the the touchpad gets disabled.
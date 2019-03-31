**Note:** This page is far from completed. Some not mentioned items could be the same as [XPS 15 9560](/index.php/XPS_15_9560 "XPS 15 9560") and [Dell XPS 15 9570](/index.php/Dell_XPS_15_9570 "Dell XPS 15 9570")

This page is about the Dell XPS 15 9575, also known as the Dell XPS 15 2-in-1.

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Intel HD Graphics 630](#Graphics) | Working |
| [Discrete Radeon RX Vega M GL Graphics](#Graphics) | Working |
| [Wifi](#Wifi_and_Bluetooth) | Working |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Untested |
| Audio | Working |
| [Touchpad](#Touchpad) | Working |
| Webcam | Working |
| Card Reader | Untested |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Management) | Working |
| [EFI Firmware Updates](#EFI_Firmware_Updates) | Working |
| [Fingerprint Reader](#Fingerprint_Reader) | Not working |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Suspend](#Suspend)
*   [2 Hibernate](#Hibernate)
*   [3 Graphics](#Graphics)
*   [4 Wifi and Bluetooth](#Wifi_and_Bluetooth)
*   [5 Audio](#Audio)
*   [6 Power Management](#Power_Management)
*   [7 EFI Firmware Updates](#EFI_Firmware_Updates)
*   [8 Fingerprint Reader](#Fingerprint_Reader)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Overheating](#Overheating)

## Suspend

## Hibernate

## Graphics

## Wifi and Bluetooth

## Audio

## Power Management

## EFI Firmware Updates

## Fingerprint Reader

## Troubleshooting

### Overheating

When using the GPU or CPU extensively, you may see overheating messages from dmesg. Disabling Intel Turbo Boost resolves this problem. This can be done in the BIOS, or by echoing `1` to `/sys/devices/system/cpu/intel_pstate/no_turbo`.
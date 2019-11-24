**Note:** This page is far from completed. Some not mentioned items could be the same as [XPS 15 9560](/index.php/XPS_15_9560 "XPS 15 9560") and [Dell XPS 15 9570](/index.php/Dell_XPS_15_9570 "Dell XPS 15 9570")

This page is about the Dell XPS 15 9575, also known as the Dell XPS 15 2-in-1.

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Intel HD Graphics 630](#Graphics) | Working |
| [Discrete Radeon RX Vega M GL Graphics](#Graphics) | Working |
| [Wifi](#Wifi_and_Bluetooth) | Working |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Working |
| Audio | Working |
| [Touchpad](#Touchpad) | Working |
| Webcam | Working |
| Card Reader | Working |
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
        *   [9.1.1 Disabling Turbo Boost](#Disabling_Turbo_Boost)
        *   [9.1.2 Using smbios-thermal-ctl](#Using_smbios-thermal-ctl)

## Suspend

## Hibernate

## Graphics

The AMD Vega M is compeltely functionnal and is usable OOB by using DRI_PRIME=1 [command].

See [PRIME](/index.php/PRIME "PRIME") to get more information.

## Wifi and Bluetooth

## Audio

## Power Management

## EFI Firmware Updates

## Fingerprint Reader

As of writing, the fingerprint reader isn't currently supported. There is a collaborative effort on a reverse-engineered open-source driver [here](https://github.com/IDerr/Goodix92/). Also see this [room](https://gitter.im/Goodix92) if you're interested in helping.

## Troubleshooting

### Overheating

When using the GPU and/or CPU extensively, you may see overheating messages from dmesg:

```
[ 4233.376972] mce: CPU3: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376974] mce: CPU6: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376975] mce: CPU2: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376976] mce: CPU7: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376977] mce: CPU5: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376979] mce: CPU4: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376980] mce: CPU0: Package temperature above threshold, cpu clock throttled (total events = 20006)
[ 4233.376981] mce: CPU1: Package temperature above threshold, cpu clock throttled (total events = 20006)

```

It is important to mitigate overheating as it can damage your system and eventually lead to system failure. There are two solutions:

#### Disabling Turbo Boost

Disabling Intel Turbo Boost resolves this problem. This can be done in the BIOS, or temporarily by echoing `1` to `/sys/devices/system/cpu/intel_pstate/no_turbo`.

#### Using `smbios-thermal-ctl`

Alternatively, you can control thermal parameters using the SMBIOS interface. To do this, you must have `libsmbios` installed. You can then set the thermal mode to `cool-bottom` by running `sudo smbios-thermal-ctl --set-thermal-mode THERMAL_MODE`. If this doesn't lower temperatures enough, try `quiet`. You can also run `sudo smbios-thermal-ctl -i` to see all supported thermal modes. To see the current status, run `sudo smbios-thermal-ctl -g`.
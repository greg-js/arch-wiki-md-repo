**Note:** This page far from completed. Some not mentioned items could be same as [XPS 15 9560](/index.php/XPS_15_9560 "XPS 15 9560")

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Suspend_and_Hibernate) | Not tested |
| [Integrated Graphics](#Graphics) | Working |
| [Discrete Nvidia Graphics](#Graphics) | Modify |
| [Wifi](#Wifi_and_Bluetooth) | Working |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Working |
| Audio | Working |
| [Touchpad](#Touchpad) | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Saving) | Buggy |
| [EFI firmware updates](#EFI_firmware_updates) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

## Contents

*   [1 Suspend](#Suspend)
*   [2 Graphics](#Graphics)
    *   [2.1 Optimus Nvidia](#Optimus_Nvidia)
    *   [2.2 bbswitch](#bbswitch)
*   [3 EFI firmware updates](#EFI_firmware_updates)

## Suspend

By default, the very inefficient s2idle suspend variant is incorrectly selected. This is probably due to the BIOS. The much more efficient deep variant should be selected instead:

```
 $ cat /sys/power/mem_sleep 
 [s2idle] deep
 $ echo deep|sudo tee /sys/power/mem_sleep
 $ cat /sys/power/mem_sleep 
 s2idle [deep]

```

To make the change permanent add `mem_sleep_default=deep` to your kernel parameters.

Read more regarding the sleep variants on the kernel documentation [[1]](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html).

## Graphics

Integrated graphics works well out of the box.

### Optimus Nvidia

Works but additional configuration is needed. (see *[[2]](https://github.com/Bumblebee-Project/bbswitch/issues/140#issuecomment-394180574))

*   Add pcie_port_pm=on to kernel options
*   If tlp is installed, add the graphic card to **RUNTIME_PM_BLACKLIST**
*   Uninstall or disable bbswitch
*   Install bumblebee and set **PMMethod=none** in nvidia section
*   Install nvidia driver
*   Reboot

Note: This is just one configuration that worked. There are more configurations that might work just as well or even better. Sometimes nvidia driver can not be unloaded because some process is still using it. However even if the driver is loaded power saving still works.

### bbswitch

Discrete (GeForce GTX 1050 Ti) graphics card do not work well with bbswich. It won't power on/off (see *[[3]](https://bbs.archlinux.org/viewtopic.php?id=238389))

## EFI firmware updates

This device is supported by [Fwupd](/index.php/Fwupd "Fwupd").
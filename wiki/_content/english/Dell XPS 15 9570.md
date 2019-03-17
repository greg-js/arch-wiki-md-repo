**Note:** This page far from completed. Some not mentioned items could be same as [XPS 15 9560](/index.php/XPS_15_9560 "XPS 15 9560"). Most of it also applies to the Precision 5530

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Graphics](#Graphics) | Working |
| [Discrete Nvidia Graphics](#Graphics) | Modify |
| [Wifi](#Wifi_and_Bluetooth) | Working |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Working |
| Audio | Working |
| [Touchpad](#Touchpad_and_Touchscreen) | Working |
| [Touchscreen](#Touchpad_and_Touchscreen) | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Saving) | Buggy |
| [EFI firmware updates](#EFI_firmware_updates) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Suspend](#Suspend)
*   [2 Hibernate](#Hibernate)
*   [3 Graphics](#Graphics)
    *   [3.1 Optimus Nvidia](#Optimus_Nvidia)
    *   [3.2 bbswitch](#bbswitch)
    *   [3.3 nvidia-xrun](#nvidia-xrun)
    *   [3.4 Troubleshoot](#Troubleshoot)
        *   [3.4.1 NVRM: Failed to enable MSI; falling back to PCIe virtual-wire interrupts](#NVRM:_Failed_to_enable_MSI;_falling_back_to_PCIe_virtual-wire_interrupts)
        *   [3.4.2 Built-in screen flickers after Linux 5.0.x upgrade](#Built-in_screen_flickers_after_Linux_5.0.x_upgrade)
*   [4 Touchpad and Touchscreen](#Touchpad_and_Touchscreen)
*   [5 Thunderbolt docks](#Thunderbolt_docks)
    *   [5.1 TB16](#TB16)
*   [6 EFI firmware updates](#EFI_firmware_updates)
*   [7 Tips and Tricks](#Tips_and_Tricks)
    *   [7.1 Systemd doesn't wait for Network](#Systemd_doesn't_wait_for_Network)

## Suspend

By default, the very inefficient s2idle suspend variant is incorrectly selected. This is probably due to the BIOS. The much more efficient deep variant should be selected instead:

```
 $ cat /sys/power/mem_sleep 
 [s2idle] deep
 $ echo deep|sudo tee /sys/power/mem_sleep
 $ cat /sys/power/mem_sleep 
 s2idle [deep]

```

To make the change permanent add `mem_sleep_default=deep` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Read more regarding the sleep variants on the kernel documentation [[1]](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html).

**Warning:** Some users have reported a problem where the CPUs get stuck in a high power state after resuming from S3 (deep) suspension [[2]](https://www.reddit.com/r/Dell/comments/91313h/xps_15_9570_c_state_bug_after_s3_sleep_and_modern/).

## Hibernate

Works out of the Box see [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")

## Graphics

The nouveau module is known to cause kernel panics and freezes on this model. One way to mitigate this is by adding `nomodeset` to the kernel options, however it's best if you completely disable it.

 `/etc/modprobe.d/blacklist.conf` 
```
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
blacklist nv
```

And make sure the discrete GPU powers off by default on boot.

 `/etc/tmpfiles.d/nvidia_pm.conf`  `w /sys/bus/pci/devices/0000:01:00.0/power/control - - - - auto` 

Integrated graphics works well out of the box.

### Optimus Nvidia

Works but additional configuration is needed. (see *[[3]](https://github.com/Bumblebee-Project/bbswitch/issues/140#issuecomment-394180574))

*   Disable runtime PM:
    *   If [TLP](/index.php/TLP "TLP") is installed, add the graphic card to **RUNTIME_PM_BLACKLIST**
    *   If [laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools") is installed, add the graphic card to **AUTOSUSPEND_RUNTIME_DEVID_BLACKLIST** in **/etc/laptop-mode/conf.d/runtime-pm.conf**
*   Uninstall or disable bbswitch
*   Install bumblebee and set **PMMethod=none** in nvidia section
*   Install [NVIDIA](/index.php/NVIDIA "NVIDIA") driver
*   Reboot

Note: This is just one configuration that worked. There are more configurations that might work just as well or even better. Sometimes nvidia driver can not be unloaded because some process is still using it.

### bbswitch

Discrete (GeForce GTX 1050 Ti) graphics card do not work well with bbswich. It won't power on/off (see *[[4]](https://bbs.archlinux.org/viewtopic.php?id=238389)).

### nvidia-xrun

The [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/) package will not work because it relies on bbswitch, that is broken. The [nvidia-xrun-pm](https://aur.archlinux.org/packages/nvidia-xrun-pm/) package provides an alternative version that works with this card. After installing the package a service can be enabled to automatically bring the card down during boot:

```
 systemctl enable nvidia-xrun-pm

```

### Troubleshoot

#### NVRM: Failed to enable MSI; falling back to PCIe virtual-wire interrupts

Sometimes it happens after suspend/resume. GPU could work fine without MSI. [[5]](http://us.download.nvidia.com/XFree86/Linux-x86/325.15/README/knownissues.html#msi_interrupts). You could disable MSI by adding the following in **/etc/modprobe.d/nvidia.conf**:

```
 options nvidia NVreg_EnableMSI=0

```

#### Built-in screen flickers after Linux 5.0.x upgrade

Some users reported that upgrading to Linux 5.0.x can cause the screen to flicker when booting up, making the built-in display unusable (see *[[6]](https://bugs.archlinux.org/task/61964))

Currently, it seems that there are two possible workarounds :

*   [Downgrade](/index.php/Downgrading_packages "Downgrading packages") to Linux 4.20.13.
*   Apply [Albert Astals Cid's patch](https://invent.kde.org/snippets/44) on Linux kernel 5.0.x (see [kernel Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")).

## Touchpad and Touchscreen

Wacom touchscreen and Synaptics touchpad:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ SYNA2393:00 06CB:7A13 Touchpad            id=16   [slave  pointer  (2)]
⎜   ↳ Wacom HID 488F Finger                     id=15   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
[truncated]
```

Both are i2c devices:

 `$ udevadm info /dev/input/mouse3 # touchscreen` 
```
P: /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-10/i2c-WCOM488F:00/0018:056A:488F.0006/input/input47/mouse3
N: input/mouse3
L: 0
E: DEVPATH=/devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-10/i2c-WCOM488F:00/0018:056A:488F.0006/input/input47/mouse3
E: DEVNAME=/dev/input/mouse3
E: MAJOR=13
E: MINOR=35
E: SUBSYSTEM=input
E: USEC_INITIALIZED=5501073
E: ID_INPUT=1
E: ID_INPUT_TOUCHSCREEN=1
E: ID_PATH=pci-0000:00:15.0-platform-i2c_designware.0
E: ID_PATH_TAG=pci-0000_00_15_0-platform-i2c_designware_0
```
 `$ udevadm info /dev/input/mouse6 # touchpad` 
```
P: /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-11/i2c-SYNA2393:00/0018:06CB:7A13.0007/input/input38/mouse6
N: input/mouse6
L: 0
S: input/by-path/pci-0000:00:15.1-platform-i2c_designware.1-mouse
E: DEVPATH=/devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-11/i2c-SYNA2393:00/0018:06CB:7A13.0007/input/input38/mouse6
E: DEVNAME=/dev/input/mouse6
E: MAJOR=13
E: MINOR=38
E: SUBSYSTEM=input
E: USEC_INITIALIZED=4683741
E: ID_INPUT=1
E: ID_INPUT_TOUCHPAD=1
E: ID_SERIAL=noserial
E: ID_PATH=pci-0000:00:15.1-platform-i2c_designware.1
E: ID_PATH_TAG=pci-0000_00_15_1-platform-i2c_designware_1
E: DEVLINKS=/dev/input/by-path/pci-0000:00:15.1-platform-i2c_designware.1-mouse
```

## Thunderbolt docks

### TB16

TB16 works fine if either Thunderbolt security is disabled in the BIOS or using [bolt](https://www.archlinux.org/packages/?name=bolt) to temporarily authorize or permanently enroll Thunderbolt devices with Thunderbolt security activated. Various quirks are detailed on the [Dell TB16](/index.php/Dell_TB16 "Dell TB16") page.

## EFI firmware updates

This device is supported by [Fwupd](/index.php/Fwupd "Fwupd").

## Tips and Tricks

### Systemd doesn't wait for Network

Few months ago systemd added "after= .. .. network.target" in /usr/lib/systemd/system/systemd-user-sessions.service

This causes systemd to wait for network connection at boot, you can modify this file to remove network.target but it will be overwritten on systemd update. A better workaround is to add /etc/systemd/system/systemd-user-sessions.service with network.target removed.

 `/etc/systemd/system/systemd-user-sessions.service` 
```
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

[Unit]
Description=Permit User Sessions
Documentation=man:systemd-user-sessions.service(8)
After=remote-fs.target nss-user-lookup.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-user-sessions start
ExecStop=/usr/lib/systemd/systemd-user-sessions stop
```
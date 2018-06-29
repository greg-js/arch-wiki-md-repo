**Note:** This page refers to the 9560 revision of the XPS 15\. Most of it also applies to the Precision 5520 and the XPS 15 9570

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend_and_Hibernate) | Buggy |
| [Hibernate](#Suspend_and_Hibernate) | Working |
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
| [Power Management](#Power_Saving) | Modify |
| [EFI firmware updates](#UEFI) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

This page contains recommendations for running Arch Linux on the Dell XPS 15 9560 (late 2016). With some configuration almost all the hardware is well supported. Exceptions are the fingerprint reader, occasional locks on resuming from suspend experienced by some users, and the lack of support for PRIME render offload to the discrete GPU in the Nvidia proprietary driver.

## Contents

*   [1 UEFI](#UEFI)
*   [2 Power Management](#Power_Management)
    *   [2.1 Suspend and Hibernate](#Suspend_and_Hibernate)
    *   [2.2 Fan and temperature monitoring and control](#Fan_and_temperature_monitoring_and_control)
*   [3 Power Saving](#Power_Saving)
    *   [3.1 Disable discrete GPU](#Disable_discrete_GPU)
        *   [3.1.1 bbswitch method](#bbswitch_method)
        *   [3.1.2 acpi_call method](#acpi_call_method)
    *   [3.2 Standard power saving configuration](#Standard_power_saving_configuration)
    *   [3.3 Disable/autosuspend of touchscreen](#Disable.2Fautosuspend_of_touchscreen)
    *   [3.4 Enable NVME APST](#Enable_NVME_APST)
    *   [3.5 Enable power saving features for the i915 kernel module](#Enable_power_saving_features_for_the_i915_kernel_module)
    *   [3.6 Wifi and Bluetooth](#Wifi_and_Bluetooth)
*   [4 Graphics](#Graphics)
    *   [4.1 Intel card only](#Intel_card_only)
    *   [4.2 Open source driver with PRIME render offloading](#Open_source_driver_with_PRIME_render_offloading)
    *   [4.3 Proprietary driver with bumblebee](#Proprietary_driver_with_bumblebee)
    *   [4.4 Proprietary driver with PRIME output offloading](#Proprietary_driver_with_PRIME_output_offloading)
*   [5 Touchpad](#Touchpad)
    *   [5.1 libinput Driver Configuration](#libinput_Driver_Configuration)
    *   [5.2 Synaptics Driver Configuration](#Synaptics_Driver_Configuration)
        *   [5.2.1 Configure middle button](#Configure_middle_button)
*   [6 Thunderbolt docks](#Thunderbolt_docks)
    *   [6.1 TB16](#TB16)
    *   [6.2 Dell Docks](#Dell_Docks)
*   [7 Firmware updates](#Firmware_updates)
*   [8 Fingerprint reader](#Fingerprint_reader)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 xorg freezes at startup](#xorg_freezes_at_startup)
    *   [9.2 PCIe Bus Error in system logs](#PCIe_Bus_Error_in_system_logs)
    *   [9.3 lspci causes CPU lockups](#lspci_causes_CPU_lockups)
*   [10 Notes](#Notes)
*   [11 External links](#External_links)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the change but [this can be fixed without a reinstallation](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/).
*   Change Fastboot to "Thorough" in "POST Behaviour". This prevents intermittent boot failures.
*   Disable secure boot to allow Linux to boot.

Installation of Arch Linux can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more information.

## Power Management

### Suspend and Hibernate

Suspend and Hibernate work out of the box, although some users have reported [occasional system hangs on resuming from suspend](https://bbs.archlinux.org/viewtopic.php?id=223056), more commonly on kernels since 4.10.

### Fan and temperature monitoring and control

Many of the thermometers can be read with [lm_sensors](/index.php/Lm_sensors "Lm sensors").

Fan speeds can be monitored with `i8kctl` from [i8kutils-git](https://aur.archlinux.org/packages/i8kutils-git/). This laptop is not in the supported list so it is necessary to load the `i8k` kernel module with the `force=1` module option. See [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). It is also possible to manually control fan speeds (at your own risk) however with manual control only a subset of the possible speeds are available (0rpm, 2500rpm, 4800rpm) instead of (0rpm, 2500rpm, 3200rpm, 3700rpm, 4800rpm, and 5100rpm) in the firmware's automatic control. See [Fan speed control#Disable BIOS fan speed control](/index.php/Fan_speed_control#Disable_BIOS_fan_speed_control "Fan speed control").

The thermometer on the discrete Nvidia GPU can be monitored with the `nvidia-smi` utility, which is part of [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils).

## Power Saving

### Disable discrete GPU

#### `bbswitch` method

The discrete Nvidia GTX 1050 GPU is on by default and cannot be disabled in the UEFI settings. Even when idle, it uses a significant amount of power (about 7W). To disable it when not in use it is necessary to install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) and [bumblebee](https://www.archlinux.org/packages/?name=bumblebee), add `acpi_rev_override=1` to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), [enable](/index.php/Enable "Enable") `bumblebeed.service`, and reboot (you may need to reboot twice for the firmware to notice `acpi_rev_override`).

```
$ cat /proc/acpi/bbswitch

```

should now print

```
$ OFF

```

and

```
$ dmesg | grep bbswitch

```

should print something like

```
$ [    4.253642] bbswitch: loading out-of-tree module taints kernel.
$ [    4.253833] bbswitch: version 0.8
$ [    4.254093] bbswitch: Found integrated VGA device 0000:00:02.0: \_SB_.PCI0.GFX0
$ [    4.254163] bbswitch: Found discrete VGA device 0000:01:00.0: \_SB_.PCI0.PEG0.PEGP
$ [    4.254225] bbswitch: detected an Optimus _DSM function
$ [    4.254282] bbswitch: Succesfully loaded. Discrete card 0000:01:00.0 is on
$ [    4.256651] bbswitch: disabling discrete graphics

```

#### `acpi_call` method

An alternative set of steps, not requiring [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) or [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) is as follows:

*   Install the Intel video driver using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.
*   Blacklist the `nvidia` & `nouveau` modules [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")
*   Power down the GPU [with an ACPI command](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics")

### Standard power saving configuration

It is a good idea to install a tool to tune common settings to save power. See [Power management#Userspace tools](/index.php/Power_management#Userspace_tools "Power management").

### Disable/autosuspend of touchscreen

Disabling the touchscreen can be done in the UEFI settings and results in significant power savings. If touchscreen is required it can be placed into autosuspend by [TLP](/index.php/TLP "TLP") by adding `04f3:24a1` to `USB_WHITELIST` in tlp config file. This will leave touchscreen enabled for usage and will consume much less battery.

### Enable NVME APST

Before Kernel 4.11 Linux does not support NVME APST, so the NVME SSD is in its highest power state all the time. Significant power savings can be achieved by running a Kernel with patches and appropriate parameters to enable APST. See [Solid State Drives/NVMe#Power Saving APST](/index.php/Solid_State_Drives/NVMe#Power_Saving_APST "Solid State Drives/NVMe"). Even when running such a kernel, it may be necessary to adjust the `default_ps_max_latency_us` parameter to the `nvme_core` module in order to make ASPT work.

### Enable power saving features for the i915 kernel module

Passing the following options to the i915 kernel module results in significant power savings: `enable_fbc=1 enable_psr=1 disable_power_well=0`. Some users with the HD matte screen have reported that these parameters cause screen flickering. Frame buffer compression (`enable_fbc=1`) is enabled by default starting from kernel 4.11.

### Wifi and Bluetooth

For the Precision 5520 which has an Intel 8265 wifi card, the `power_save` option for the `iwlwifi` kernel module can be set from 1 to 5 with potential power savings. See [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Bluetooth and Wifi can seperately be disabled with rfkill. See [Wireless network configuration#Rfkill caveat](/index.php/Wireless_network_configuration#Rfkill_caveat "Wireless network configuration").

## Graphics

The integrated Intel HD 630 GPU works well out of the box. Optionally you may install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) but this is no longer recommended, since the built in kernel modesetting driver is more reliable. If you do not want to use the discrete Nvidia GPU, no extra setup is necessary. Otherwise there are a few options. All of the display outputs are connected to the integrated GPU so there is no need to set up output from the discrete GPU. It may be necessary to compile a custom kernel as described in [#Power Saving](#Power_Saving).

### Intel card only

See [#Disable discrete GPU](#Disable_discrete_GPU) above.

### Open source driver with PRIME render offloading

With this setup it is possible to use the integrated GPU by default and to offload GPU intensive applications to the discrete GPU by the use of the `DRI_PRIME` environment variable. See [PRIME](/index.php/PRIME "PRIME") for details. Note that the open source Nvidia driver [Nouveau](/index.php/Nouveau "Nouveau") currently [does not support](https://nouveau.freedesktop.org/wiki/CodeNames/#NV130) power management on Pascal GPUs such as the GTX 1050, so performance is very poor with this driver. See [Nouveau#Power management](/index.php/Nouveau#Power_management "Nouveau").

### Proprietary driver with bumblebee

With this setup the integrated GPU is used by default but some applications can be rendered on the discrete GPU with the `optirun` or `primusrun` launchers. See [Bumblebee](/index.php/Bumblebee "Bumblebee") for detailed instructions. The lack of proper v-sync support means that with this method applications rendered on the discrete GPU exhibit tearing. There is also some overhead introduced as a result of moving data inefficiently between the discrete and integrated GPUs, but the Nvidia GPU performs much better than it does with Nouveau. The current stable [NVIDIA](/index.php/NVIDIA "NVIDIA") release (378.13) does not work (rmInitAdapterFailed in dmesg), however the latest beta drivers [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/), [nvidia-utils-beta](https://aur.archlinux.org/packages/nvidia-utils-beta/), and [lib32-nvidia-utils-beta](https://aur.archlinux.org/packages/lib32-nvidia-utils-beta/) are working. To use them with a custom kernel it is necessary to use the [DKMS](/index.php/DKMS "DKMS") version [nvidia-beta-dkms](https://aur.archlinux.org/packages/nvidia-beta-dkms/) and to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") to update it to the same version as the utils package. Alternatively the current long lived branch release (375.66) works too ([nvidia-llb-dkms](https://aur.archlinux.org/packages/nvidia-llb-dkms/), [nvidia-utils-llb](https://aur.archlinux.org/packages/nvidia-utils-llb/), [lib32-nvidia-utils-llb](https://aur.archlinux.org/packages/lib32-nvidia-utils-llb/)).

### Proprietary driver with PRIME output offloading

With this setup the discrete GPU is used for all rendering and the integrated GPU is used only to display the rendered output. Power consumption is much higher during light usage because the discrete GPU cannot be disabled. Performance for graphics intensive applications is significantly better than with Bumblebee, and v-sync works due to [PRIME Synchronization](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/1) so tearing is eliminated. Remove [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) and follow the instructions in [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), [Nvidia README](http://us.download.nvidia.com/XFree86/Linux-x86_64/375.66/README/randr14.html), or [PRIME Synchronization thread](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/1) using `PCI:1:0:0` as the BusID. Add the `modeset=1` parameter to the `nvidia_drm` kernel module (on boot, not with modprobe) to enable PRIME synchronization and remove tearing (see [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")). It is necessary to use the long lived branch of the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver ([nvidia-llb-dkms](https://aur.archlinux.org/packages/nvidia-llb-dkms/), [nvidia-utils-llb](https://aur.archlinux.org/packages/nvidia-utils-llb/), [lib32-nvidia-utils-llb](https://aur.archlinux.org/packages/lib32-nvidia-utils-llb/)) since the latest version (375.66) contains [bugfixes](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/post/5141480/#5141480) making PRIME Synchronization usable on the GTX 1050, which are not present in the latest stable (378.13) and beta (381.09) releases.

## Touchpad

The Synaptics Touchpad's basic functionality works out of the box. Some [desktop environments](/index.php/Desktop_environment "Desktop environment") ship with [libinput](/index.php/Libinput "Libinput") and others with the [xf86-input-synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") driver. You can see which package is installed by running:

```
pacman -Qn libinput xf86-input-synaptics

```

Depending on which package handles your touchpad input, the methods to extend the functionality varies.

### libinput Driver Configuration

The full documentation for [libinput](/index.php/Libinput "Libinput") seemed to work quite well for this touchpad. While the driver already contains logic to process advanced multi-touch events like swipe and pinch gestures, the desktop environment or window manager might not have implemented actions for all of them yet.

To get some three and four-touch gestures to work you may need to use the documentation at [libinput-gestures](https://github.com/bulletmark/libinput-gestures) and install the [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/) package.

### Synaptics Driver Configuration

You can use `synclient` to list the touchpad's capabilities and change them for the session.

#### Configure middle button

The touchpad has a big click zone in the bottom that can be disabled or configured for 1, 2 or 3 buttons. For example, to have most of the touchpad seen as "button 1" but the middle lower zone (middle button) and the right lower zone (right button), create `/etc/X11/xorg.conf.d/50-synaptics.conf` with content:

```
Section "InputClass"
   Identifier "touchpad catchall"
   Driver "synaptics"
   MatchIsTouchpad "on"
   # enable clik zone and configure 3 buttons on bottom
   Option "ClickPad" "1"
   Option "SoftButtonAreas" "60% 0 82% 0 40% 60% 82% 0"
   # other commons options than you may want to configure
   # scroll with two fingers (enabled vertically, disabled horizontally)
   Option "VertTwoFingerScroll" "1"
   Option "HorizTwoFingerScroll" "0"
   # enable tap as click: 1 finger -> left button, 2 fingers -> right, 3 fingers -> middle
   Option "TapButton1" "1"
   Option "TapButton2" "3"
   Option "TapButton3" "2"
   # idem but for click with 1,2,3 fingers. Use "0" to disable. 
   Option "ClickFinger1" "1"
   Option "ClickFinger2" "3"
   Option "ClickFinger3" "2"
   # palm detection. These parameters somehow works, YMMV. 
   Option "PalmDetect" "1"
   Option "PalmMinWidth" "10"
   Option "PalmMinZ" "200"
EndSection

```

With the recent deprecation of synaptics, it is possible to use existing GUI (for instance, GNOME Tweak Tool) to change the behavior. Using gnome-tweaks, under Keyboard & Mouse section, Mouse Click Emulation is set by default to "Fingers". Changing it to the "Area" option, which uses the bottom right of the touchpad for a right click, fixes the problem.

## Thunderbolt docks

### TB16

TB16 works fine if either Thunderbolt security is disabled in the BIOS or using [bolt](https://aur.archlinux.org/packages/bolt/) to temporarily authorize or permanently enroll Thunderbolt devices with Thunderbolt security activated.

### Dell Docks

Some Dell docks (tested with the D6000) experience behavior whereby the displays periodically disconnect. Unplugging and plugging the dock back in again causes the displays to come back to life, but the displays will disconnect again. The more permanent fix for this is to edit the /etc/pulse/default.pa file, and comment out the following line:

```
### Automatically suspend sinks/sources that become idle for too long
load-module module-suspend-on-idle

```

A discussion around this issue can be found [here](https://www.displaylink.org/forum/showthread.php?t=65476&page=2), including the discussion around fixes.

## Firmware updates

Firmware updates are provided by Dell and can be installed with [fwupdate](https://www.archlinux.org/packages/?name=fwupdate) or [fwupd](https://www.archlinux.org/packages/?name=fwupd). Available firmware versions can be seen [here](https://secure-lvfs.rhcloud.com/lvfs/device/34578c72-11dc-4378-bc7f-b643866f598c).

Alternatively, firmware updates can be installed by copying the MS-DOS executable firmware file to a FAT32-formatted USB key (or directly to your EFI boot partition) and booting into "BIOS Flash Update" from the Boot Menu.

## Fingerprint reader

The fingerprint reader is a Validity/Synaptics model with USB id `138a:0091`. There is currently a working prototype of a driver capable of capturing prints, however direct integration with libfprint is unlikely due to the manner in which the matching algorithm is implemented. [[1]](https://github.com/hmaarrfk/Validity91).

There is also some people working on drivers for various other related readers. According to them it should be fairly easy to implement a driver for this model as none of the traffic to or from the device appears to be encrypted. Nevertheless, `138a:0091` is out of the scope of the project. [[2]](https://github.com/nmikhailov/Validity90)

## Troubleshooting

### xorg freezes at startup

If Xorg freezes as soon as it starts, even before printing any logs, and you are trying to use the Intel card with the nvidia one disabled, you need to add kernel parameter `acpi_rev_override=1` as explained in [#Disable discrete GPU](#Disable_discrete_GPU) above.

### PCIe Bus Error in system logs

If you have an NVMe disk and depending of your BIOS version (but even with 1.5.0 from october 2017), you may have a lot of system error logs like:

```
Nov 25 22:36:08 xxxxx kernel: pcieport 0000:00:1c.0: PCIe Bus Error: severity=Corrected, type=Data Link Layer, id=00e0(Transmitter ID)
Nov 25 22:36:08 xxxxx kernel: pcieport 0000:00:1c.0:   device [8086:a110] error status/mask=00001000/00002000
Nov 25 22:36:08 xxxxx kernel: pcieport 0000:00:1c.0:    [12] Replay Timer Timeout

```

This can be corrected with the kernel boot option `pcie_aspm=off` which appears to have minimal to no affect on power consumption. If that does not work, try `pci=nommconf` (see [here](https://unix.stackexchange.com/questions/327730/what-causes-this-pcieport-00000003-0-pcie-bus-error-aer-bad-tlp) for explanation).

### `lspci` causes CPU lockups

The NVidia/nouveau driver may cause any runs of `lspci`, starting an X server, or otherwise poking the graphics card to cause at least one CPU core to lock up, as well as seeming to completely lock up PCIe access, for instance to the NVMe SSD. The kernel parameter `nouveau.modeset=0` may fix this. This is also related to the X freezes on startup (some machines may require lspci/startx to be run twice so they freeze after nouveau is taken care of); the solution in that case is to also set `acpi_rev_override=1`. [[3]](https://cnly.github.io/2017/08/25/fix-system-hangs-xps-15-9560.html)

## Notes

The suspend function key is not printed on the keyboard, but it's actually mapped to `Fn`+`Insert`.

## External links

*   [Dell XPS 15 9560 (Early 2017) Thread on the Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=223056)
*   [Optimizing Dell XPS](https://www.reddit.com/r/Dell/comments/6s2e3w/optimizing_dell_xps_for_linux/)
*   [Tutorial about how to change CPU thermal paste on XPS15 to avoid throttling](https://www.ultrabookreview.com/14875-fix-throttling-xps-15/)
*   [[4]](https://www.displaylink.org/forum/showthread.php?t=65476&page=2)
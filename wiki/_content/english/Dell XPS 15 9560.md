**Note:** This page refers to the 9560 revision of the XPS 15\. Most of it also applies to the Precision 5520

| **Device/Functionality** | **Status** |
| Suspend | Buggy |
| Hibernate | Working |
| Integrated Graphics | Working |
| Discrete Nvidia Graphics | Modify |
| Wifi | Working |
| Bluetooth | Working |
| rfkill | Working |
| Audio | Working |
| Touchpad | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| Power Management | Modify |
| EFI firmware updates | Working |
| Fingerprint reader | Not working |

This page contains recommendations for running Arch Linux on the Dell XPS 15 9650 (late 2016). With some configuration almost all the hardware is well supported. Exceptions are the fingerprint reader, occasional locks on resuming from suspend experienced by some users, and the lack of support for PRIME render offload to the discrete GPU in the Nvidia proprietary driver.

## Contents

*   [1 UEFI](#UEFI)
*   [2 Power Management](#Power_Management)
    *   [2.1 Suspend and Hibernate](#Suspend_and_Hibernate)
    *   [2.2 Fan and temperature monitoring and control](#Fan_and_temperature_monitoring_and_control)
*   [3 Power Saving](#Power_Saving)
    *   [3.1 Disable discrete GPU](#Disable_discrete_GPU)
    *   [3.2 Standard power saving configuration](#Standard_power_saving_configuration)
    *   [3.3 Disable touchscreen](#Disable_touchscreen)
    *   [3.4 Enable NVME APST](#Enable_NVME_APST)
    *   [3.5 Enable power saving features for the i915 kernel module](#Enable_power_saving_features_for_the_i915_kernel_module)
    *   [3.6 Wifi and Bluetooth](#Wifi_and_Bluetooth)
*   [4 Graphics](#Graphics)
    *   [4.1 Open source driver with PRIME render offloading](#Open_source_driver_with_PRIME_render_offloading)
    *   [4.2 Proprietary driver with bumblebee](#Proprietary_driver_with_bumblebee)
    *   [4.3 Proprietary driver with PRIME output offloading](#Proprietary_driver_with_PRIME_output_offloading)
*   [5 Firmware updates](#Firmware_updates)
*   [6 Fingerprint reader](#Fingerprint_reader)
*   [7 External links](#External_links)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the change but this can be fixed without a reinstallation.
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

The discrete Nvidia GTX 1050 GPU is on by default and cannot be disabled in the UEFI settings. Even when idle, it uses a significant amount of power (about 7W). To disable it when not in use it is necessary to build a custom kernel with the `CONFIG_ACPI_REV_OVERRIDE_POSSIBLE` flag set. See [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). When running such a kernel, install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) and [bumblebee](https://www.archlinux.org/packages/?name=bumblebee), add `acpi_rev_override=1` to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), [enable](/index.php/Enable "Enable") `bumblebeed.service`, and reboot.

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

### Standard power saving configuration

It is a good idea to install a tool to tune common settings to save power. See [Power management#Userspace tools](/index.php/Power_management#Userspace_tools "Power management"). One caveat is that enabling PCIE runtime power management results in [bbswitch not working](https://github.com/Bumblebee-Project/bbswitch/issues/140). A workaround is to disable PCIE runtime power management for the Nvidia GPU. For example for [TLP](/index.php/TLP "TLP"), edit `/etc/default/tlp` to have `RUNTIME_PM_BLACKLIST="01:00.0"`. This is done by default in later versions of tlp, such as [tlp-git](https://aur.archlinux.org/packages/tlp-git/). Alternatively, PCIE runtime power management can be disabled for all devices using the kernel parameter `pcie_port_pm=off`.

### Disable touchscreen

Disabling the touchscreen can be done in the UEFI settings and results in significant power savings.

### Enable NVME APST

Before Kernel 4.11 Linux does not support NVME APST, so the NVME SSD is in its highest power state all the time. Significant power savings can be achieved by running a Kernel with patches and appropriate parameters to enable APST. See [Solid State Drives/NVMe#Power Saving APST](/index.php/Solid_State_Drives/NVMe#Power_Saving_APST "Solid State Drives/NVMe"). Even when running such a kernel, it may be necessary to adjust the `default_ps_max_latency_us` parameter to the `nvme_core` module in order to make ASPT work.

### Enable power saving features for the i915 kernel module

Passing the following options to the i915 kernel module results in significant power savings: `enable_fbc=1 enable_psr=1 disable_power_well=0`.

### Wifi and Bluetooth

For the Precision 5520 which has an Intel 8265 wifi card, the `power_save` option for the `iwlwifi` kernel module can be set from 1 to 5 with potential power savings. See [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Bluetooth and Wifi can seperately be disabled with rfkill. See [Wireless network configuration#Rfkill caveat](/index.php/Wireless_network_configuration#Rfkill_caveat "Wireless network configuration").

## Graphics

The integrated Intel HD 630 GPU works well out of the box. Optionally you may install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) but this is no longer recommended, since the built in kernel modesetting driver is more reliable. If you do not want to use the discrete Nvidia GPU, no extra setup is necessary. Otherwise there are a few options. All of the display outputs are connected to the integrated GPU so there is no need to set up output from the discrete GPU. It may be necessary to compile a custom kernel as described in [#Power Saving](#Power_Saving).

### Open source driver with PRIME render offloading

With this setup it is possible to use the integrated GPU by default and to offload GPU intensive applications to the discrete GPU by the use of the `DRI_PRIME` environment variable. See [PRIME](/index.php/PRIME "PRIME") for details. Note that the open source Nvidia driver [Nouveau](/index.php/Nouveau "Nouveau") currently [does not support](https://nouveau.freedesktop.org/wiki/CodeNames/#NV130) power management on Pascal GPUs such as the GTX 1050, so performance is very poor with this driver. See [Nouveau#Power management](/index.php/Nouveau#Power_management "Nouveau").

### Proprietary driver with bumblebee

With this setup the integrated GPU is used by default but some applications can be rendered on the discrete GPU with the `optirun` or `primusrun` launchers. See [Bumblebee](/index.php/Bumblebee "Bumblebee") for detailed instructions. The lack of proper v-sync support means that with this method applications rendered on the discrete GPU exhibit tearing. There is also some overhead introduced as a result of moving data inefficiently between the discrete and integrated GPUs, but the Nvidia GPU performs much better than it does with Nouveau. The current stable [NVIDIA](/index.php/NVIDIA "NVIDIA") release (378.13) does not work (rmInitAdapterFailed in dmesg), however the latest beta drivers [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/), [nvidia-utils-beta](https://aur.archlinux.org/packages/nvidia-utils-beta/), and [lib32-nvidia-utils-beta](https://aur.archlinux.org/packages/lib32-nvidia-utils-beta/) are working. To use them with a custom kernel it is necessary to use the [DKMS](/index.php/DKMS "DKMS") version [nvidia-beta-dkms](https://aur.archlinux.org/packages/nvidia-beta-dkms/) and to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") to update it to the same version as the utils package. Alternatively the current long lived branch release (375.66) works too ([nvidia-llb-dkms](https://aur.archlinux.org/packages/nvidia-llb-dkms/), [nvidia-utils-llb](https://aur.archlinux.org/packages/nvidia-utils-llb/), [lib32-nvidia-utils-llb](https://aur.archlinux.org/packages/lib32-nvidia-utils-llb/)).

### Proprietary driver with PRIME output offloading

With this setup the discrete GPU is used for all rendering and the integrated GPU is used only to display the rendered output. Power consumption is much higher during light usage because the discrete GPU cannot be disabled. Performance for graphics intensive applications is significantly better than with Bumblebee, and v-sync works due to [PRIME Synchronization](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/1) so tearing is eliminated. Remove [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) and follow the instructions in [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), [Nvidia README](http://us.download.nvidia.com/XFree86/Linux-x86_64/375.66/README/randr14.html), or [PRIME Synchronization thread](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/1) using `PCI:1:0:0` as the BusID. Add the `modeset=1` parameter to the `nvidia_drm` kernel module (on boot, not with modprobe) to enable PRIME synchronization and remove tearing (see [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")). It is necessary to use the long lived branch of the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver ([nvidia-llb-dkms](https://aur.archlinux.org/packages/nvidia-llb-dkms/), [nvidia-utils-llb](https://aur.archlinux.org/packages/nvidia-utils-llb/), [lib32-nvidia-utils-llb](https://aur.archlinux.org/packages/lib32-nvidia-utils-llb/)) since the latest version (375.66) contains [bugfixes](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/post/5141480/#5141480) making PRIME Synchronization usable on the GTX 1050, which are not present in the latest stable (378.13) and beta (381.09) releases.

## Firmware updates

Firwmare updates are provided by Dell and can be installed with [fwupdate](https://aur.archlinux.org/packages/fwupdate/). Available firmware versions can also be seen [here](https://secure-lvfs.rhcloud.com/lvfs/device/34578c72-11dc-4378-bc7f-b643866f598c).

## Fingerprint reader

The fingerprint reader is a Validity/Synaptics model with USB id `138a:0090`. There currently is no Linux driver but an open source Linux driver is being developed by reverse engineering the Windows driver. [[1]](https://github.com/nmikhailov/Validity90)

## External links

*   [Dell XPS 15 9560 (Early 2017) Thread on the Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=223056)
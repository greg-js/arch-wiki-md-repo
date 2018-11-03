Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")

From the [project page](http://linrunner.de/en/tlp/tlp.html):

	TLP brings you the benefits of advanced power management for Linux without the need to understand every technical detail. TLP comes with a default configuration already optimized for battery life, so you may just install and forget it. Nevertheless TLP is highly customizable to fulfill your specific requirements.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 ThinkPads only](#ThinkPads_only)
    *   [1.2 Front end](#Front_end)
*   [2 Configuration](#Configuration)
    *   [2.1 Force battery (BAT) configuration](#Force_battery_.28BAT.29_configuration)
    *   [2.2 Btrfs](#Btrfs)
    *   [2.3 Bumblebee with NVIDIA driver](#Bumblebee_with_NVIDIA_driver)
    *   [2.4 Radio Device Wizard](#Radio_Device_Wizard)
    *   [2.5 Command line](#Command_line)
*   [3 Debugging](#Debugging)
*   [4 Features intentionally excluded](#Features_intentionally_excluded)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tlp](https://www.archlinux.org/packages/?name=tlp) package. Note its optional dependencies may help provide additional power saving.

To complete TLP's install, you must [enable](/index.php/Enable "Enable") the systemd services `tlp.service` and `tlp-sleep.service`. You should also [mask](/index.php/Mask "Mask") the systemd service `systemd-rfkill.service` and socket `systemd-rfkill.socket` to avoid conflicts and assure proper operation of TLP's radio device switching options.

**Note:** `tlp.service` starts `NetworkManager.service` if it is available: [FS#43733](https://bugs.archlinux.org/task/43733). If you use a different [network manager](/index.php/List_of_applications#Network_managers "List of applications"), [mask](/index.php/Mask "Mask") `NetworkManager.service` or [edit](/index.php/Edit "Edit") `tlp.service` and remove the service out of line `Wants=`.

### ThinkPads only

For advanced battery functions, i.e. charge thresholds and recalibration, install the following package(s):

*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) – tp-smapi is needed for battery charge thresholds, recalibration and specific status output of tlp-stat
*   [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) – acpi-call is needed for battery charge thresholds and recalibration on Sandy Bridge and newer models (X220/T420, X230/T430 et al.)

See the TLP FAQ, section ["Which kernel module?"](http://linrunner.de/en/tlp/docs/tlp-faq.html#kernmod), for details.

Controlling the charge thresholds using D-Bus without root privileges is possible using [threshy](https://aur.archlinux.org/packages/threshy/) and it's example Qt user interface [threshy-gui](https://aur.archlinux.org/packages/threshy-gui/).

### Front end

[tlpui-git](https://aur.archlinux.org/packages/tlpui-git/) is a [GTK](/index.php/GTK "GTK") user interface for TLP written in Python. As of October 2018, the software is still in beta.

## Configuration

The configuration file is located at `/etc/default/tlp` and provides a "largely" optimized power saving by default. For a full explanation of options see: [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html).

### Force battery (BAT) configuration

When no power supply can be detected, the setting for AC will be used (e.g. on desktops and embedded hardware).

You may want to force the battery (BAT) settings when using TLP on these devices to enable more power saving:

 `/etc/default/tlp` 
```
# Operation mode when no power supply can be detected: AC, BAT.
TLP_DEFAULT_MODE=BAT

# Operation mode select: 0=depend on power source, 1=always use TLP_DEFAULT_MODE
TLP_PERSISTENT_DEFAULT=1
```

### Btrfs

To avoid filesystem corruption on btrfs formatted partitions, set:

```
SATA_LINKPWR_ON_BAT=max_performance

```

See also these links for discussion on this topic: [Github bug report](https://github.com/linrunner/TLP/issues/128), [Reddit follow-up discussion](https://www.reddit.com/r/archlinux/comments/4f5xvh/saving_power_is_the_btrfs_dataloss_warning_still/).

### Bumblebee with NVIDIA driver

If you're running [Bumblebee](/index.php/Bumblebee "Bumblebee") with NVIDIA driver, you need to disable power management for the GPU in TLP in order to make Bumblebee control the power of the GPU.

Run `lspci` to determine the address of the GPU (such as 01:00.0), then set the value:

```
 RUNTIME_PM_BLACKLIST="01:00.0"

```

### Radio Device Wizard

The Radio Device Wizard allows a more sophisticated management of radio devices depending on network connect/disconnect events. It requires [NetworkManager](/index.php/NetworkManager "NetworkManager"), [tlp-rdw](https://www.archlinux.org/packages/?name=tlp-rdw) and [enabling](/index.php/Enabling "Enabling") `NetworkManager-dispatcher.service`.

See [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html#rdw) for details.

### Command line

TLP provides several command line tools. See [TLP commands](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#commands).

## Debugging

You can display information about the currently used Mode(AC/BAT) and applied configurations:

```
 # tlp-stat

```

## Features intentionally excluded

*   Fan control. See [Fan speed control](/index.php/Fan_speed_control "Fan speed control")

*   Backlight brightness. See [Backlight](/index.php/Backlight "Backlight")

## See also

*   [TLP - Linux Advanced Power Management](http://linrunner.de/tlp) - Project homepage & documentation.
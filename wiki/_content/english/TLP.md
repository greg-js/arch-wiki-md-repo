From the [project page](http://linrunner.de/en/tlp/tlp.html):

	TLP brings you the benefits of advanced power management for Linux without the need to understand every technical detail. TLP comes with a default configuration already optimized for battery life, so you may just install and forget it. Nevertheless TLP is highly customizable to fulfill your specific requirements.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 ThinkPads only](#ThinkPads_only)
*   [2 Start](#Start)
*   [3 Configuration](#Configuration)
    *   [3.1 Btrfs](#Btrfs)
    *   [3.2 Bumblebee with NVIDIA driver](#Bumblebee_with_NVIDIA_driver)
    *   [3.3 Radio Device Wizard](#Radio_Device_Wizard)
    *   [3.4 Command line](#Command_line)
*   [4 Debugging](#Debugging)
*   [5 Features intentionally excluded](#Features_intentionally_excluded)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [tlp](https://www.archlinux.org/packages/?name=tlp) from the [official repositories](/index.php/Official_repositories "Official repositories") - pay attention to its optional dependencies that may help provide additional power saving.

To complete TLP's install, you must [enable](/index.php/Enable "Enable") the systemd services `tlp.service` and `tlp-sleep.service`. You should also [mask](/index.php/Mask "Mask") the systemd service `systemd-rfkill.service` and socket `systemd-rfkill.socket` to avoid conflicts and assure proper operation of TLP's radio device switching options.

**Note:** `tlp.service` starts `NetworkManager.service` if it is available: [FS#43733](https://bugs.archlinux.org/task/43733). If you use a different [network manager](/index.php/List_of_applications#Network_managers "List of applications"), [edit](/index.php/Edit "Edit") `tlp.service`in order to remove the service (line `Wants=`) or [mask](/index.php/Mask "Mask") it.

### ThinkPads only

For advanced battery functions, i.e. charge thresholds and recalibration, install the following package(s):

*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) – tp-smapi is needed for battery charge thresholds, recalibration and specific status output of tlp-stat
*   [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) – acpi-call is needed for battery charge thresholds and recalibration on Sandy Bridge and newer models (X220/T420, X230/T430 et al.)

See the TLP FAQ, section ["Which kernel module?"](http://linrunner.de/en/tlp/docs/tlp-faq.html#kernmod), for details.

## Start

After installation TLP will be automatically activated upon system start. To start it immediately without reboot or to apply changed settings, use:

```
# tlp start

```

## Configuration

The configuration file is located at `/etc/default/tlp` and provides a "largely" optimized power saving by default. For a full explanation of options see: [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html).

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

You can display informations about the currently used Mode(AC/BAT) and applied configurations:

```
 # tlp-stat

```

## Features intentionally excluded

*   Fan control. See [Fan speed control](/index.php/Fan_speed_control "Fan speed control") and [Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control")

*   Backlight brightness. See [Backlight](/index.php/Backlight "Backlight")

## See also

*   [TLP - Linux Advanced Power Management](http://linrunner.de/tlp) - Project homepage & documentation.
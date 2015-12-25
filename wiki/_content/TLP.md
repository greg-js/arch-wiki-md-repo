# TLP

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")

From the [project page](http://linrunner.de/en/tlp/tlp.html):

TLP brings you the benefits of advanced power management for Linux without the need to understand every technical detail. TLP comes with a default configuration already optimized for battery life, so you may just install and forget it. Nevertheless TLP is highly customizable to fulfill your specific requirements.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 ThinkPads only](#ThinkPads_only)
*   [2 Start](#Start)
*   [3 Configuration](#Configuration)
    *   [3.1 btrfs](#btrfs)
    *   [3.2 Radio Device Wizard](#Radio_Device_Wizard)
    *   [3.3 Command line](#Command_line)
*   [4 Features intentionally excluded](#Features_intentionally_excluded)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [tlp](https://www.archlinux.org/packages/?name=tlp) from the [official repositories](/index.php/Official_repositories "Official repositories") - pay attention to its optional dependencies that may help provide additional power saving.

To complete TLP's install, you must [enable](/index.php/Enable "Enable") the systemd services `tlp.service` and `tlp-sleep.service`. You should also [disable](/index.php/Disable "Disable") the systemd service `systemd-rfkill.service` to avoid conflicts and assure proper operation of TLP's radio device switching options.

**Note:** `tlp.service` starts `NetworkManager.service` if it is available: [FS#43733](https://bugs.archlinux.org/task/43733). Should you use a different [network manager](/index.php/List_of_applications#Network_managers "List of applications"), [edit](/index.php/Systemd#Editing_provided_units "Systemd") `tlp.service` to remove the service from `Wants=`, or [mask](/index.php/Mask "Mask") it.

### ThinkPads only

For advanced battery functions, i.e. charge thresholds and recalibration, install the following package(s):

*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) – needed for X220, T420 and older models
*   [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) – needed for X220, T420 and newer models

## Start

After installation TLP will be automatically activated upon system start. To start it immediately without reboot or to apply changed settings, use:

```
# tlp start

```

## Configuration

The configuration file is located at `/etc/default/tlp` and provides a "largely" optimized power saving by default. For a full explanation of options see: [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html).

### btrfs

To avoid filesystem corruption on btrfs formatted partitions, set:

```
SATA_LINKPWR_ON_BAT=max_performance 

```

### Radio Device Wizard

The Radio Device Wizard allows a more sophisticated management of radio devices depending on network connect/disconnect events. It requires [NetworkManager](/index.php/NetworkManager "NetworkManager"), [tlp-rdw](https://www.archlinux.org/packages/?name=tlp-rdw) and [enabling](/index.php/Enabling "Enabling") `NetworkManager-dispatcher.service`.

See [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html#rdw) for details.

### Command line

TLP provides several command line tools. See [TLP commands](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#commands).

## Features intentionally excluded

*   Fan control. See [Fan speed control](/index.php/Fan_speed_control "Fan speed control") and [Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control")

*   Backlight brightness. See [Backlight](/index.php/Backlight "Backlight")

## See also

*   [TLP - Linux Advanced Power Management](http://linrunner.de/tlp) - Project homepage & documentation.

Retrieved from "[https://wiki.archlinux.org/index.php?title=TLP&oldid=413400](https://wiki.archlinux.org/index.php?title=TLP&oldid=413400)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Power management](/index.php/Category:Power_management "Category:Power management")
Related articles

*   [Power saving](/index.php/Power_saving "Power saving")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")

**Powertop** is a tool provided by Intel to enable various powersaving modes in userspace, kernel and hardware. It is possible to monitor processes and show which of them are utilizing the CPU and wake it from its Idle-States, allowing to identify applications with particular high power demands.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Apply settings](#Apply_settings)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error: Cannot load from file](#Error:_Cannot_load_from_file)
    *   [3.2 Calibration to prevent inaccurate measurement](#Calibration_to_prevent_inaccurate_measurement)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [powertop](https://www.archlinux.org/packages/?name=powertop) package.

## Usage

Powertop suggests a few methods to reduce the power consumption further. However, in interactive mode, powertop does not display the parameters. To find out which ones are suggested, proceed as follows:

1.  If you have changed parameters (e.g. in powertop), reboot so that the system has default state of the parameters.
2.  Use powertop to produce a report on parameters: `# powertop --html=powerreport.html`
3.  Open the report in your favorite web browser. The "Tuning" tab of the report now shows the actual parameters suggested by the tool to apply to save power. You may extract the commands with `awk -F '</?td ?>' '/tune/ { print $4 }' powerreport.html`.

### Apply settings

There are two ways to automatically apply the suggested settings:

*   **Recommended:** You can apply these settings at boot by using [module parameters](/index.php/Module_parameters "Module parameters"), [udev rules](/index.php/Udev_rules "Udev rules") and [sysctl](/index.php/Sysctl "Sysctl"). For details, see the [power management](/index.php/Power_management "Power management") page.
*   You can use the `--auto-tune` feature from powertop which sets all tunable options to their GOOD setting. This can be combined with systemd service to have the tunables set on boot.

 `/etc/systemd/system/powertop.service` 
```
[Unit]
Description=Powertop tunings

[Service]
ExecStart=/usr/bin/powertop --auto-tune
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

## Troubleshooting

### Error: Cannot load from file

If you receive an error like the following when starting powertop, it's likely that powertop has not collected enough measurement data yet. To fix this, keep powertop running for a certain time connected to battery power only.

```
Loaded 39 prior measurements
Cannot load from file /var/cache/powertop/saved_parameters.powertop
Cannot load from file /var/cache/powertop/saved_parameters.powertop

```

### Calibration to prevent inaccurate measurement

If you experience inaccurate measurement, then it is likely that you need to calibrate powertop first. This can be done by running powertop with the `--calibrate` parameter.

**Note:** Calibration will toggle various functions like backlight or wifi. Thus, it may turn your screen black for some time, lose your connection, and so on. Do not touch the machine during the calibration.

```
# powertop --calibrate

```

## See also

*   [Official site](https://01.org/powertop/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Powertop "wikipedia:Powertop")
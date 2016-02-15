**PowerTOP** is a tool provided by Intel to enable various powersaving modes in userspace, kernel and hardware. It is possible to monitor processes and show which of them are utilizing the CPU and wake it from its Idle-States, allowing to identify applications with particular high power demands.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error: Cannot load from file](#Error:_Cannot_load_from_file)
    *   [3.2 Calibration to prevent inaccurate measurement](#Calibration_to_prevent_inaccurate_measurement)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") package [powertop](https://www.archlinux.org/packages/?name=powertop), available in [official repositories](/index.php/Official_repositories "Official repositories").

PowerTOP features are detailed on the release notes for each version on the [PowerTOP blog](https://01.org/powertop/blogs).

## Tips and tricks

PowerTOP suggests a few methods to reduce the power consumption further. However, in the console, PowerTOP does not display the parameters. To find out which ones are suggested, proceed as follows:

1.  If you have changed parameters (e.g. in PowerTOP), reboot so that the system has default state of the parameters.
2.  Use PowerTOP to produce a report on parameters: `# powertop --html=powerreport.html`
3.  Open the report in your favorite web browser. The "Tuning" tab of the report now shows the actual parameters suggested by the tool to apply to save power. You may extract the commands with `awk -F '</?td ?>' '/tune/ { print $4 }' powerreport.html`.
4.  They are two ways to apply those settings:
    *   **Recommended:** You can apply these settings at boot by using [module parameters](/index.php/Module_parameters "Module parameters"), [udev rules](/index.php/Udev_rules "Udev rules") and [sysctl](/index.php/Sysctl "Sysctl"). For details, see the [power management](/index.php/Power_management "Power management") page.
    *   You can use the `--auto-tune` feature from PowerTOP which sets all tunable options to their GOOD setting. This can be combined with systemd to have the tunables set on boot.

 `/etc/systemd/system/powertop.service` 

```
[Unit]
Description=Powertop tunings

[Service]
Type=oneshot
ExecStart=/usr/bin/powertop --auto-tune

[Install]
WantedBy=multi-user.target
```

## Troubleshooting

### Error: Cannot load from file

If you get an error like the following when starting powertop, you are likely to have powertop not allowed collecting enough measurement data yet. All you need to do is to keep powertop running with `--calibrate` for a certain time whilst being on battery.

```
Loaded 39 prior measurements
Cannot load from file /var/cache/powertop/saved_parameters.powertop
Cannot load from file /var/cache/powertop/saved_parameters.powertop

```

### Calibration to prevent inaccurate measurement

If you experience inaccurate measurement, then it is likely that you need to calibrate powertop first. This can be done by running powertop with the `--calibrate` parameter.

**Note:**

*   Calibration will toggle various functions like backlight or wifi. Thus, it may turn your screen black for some time, lose your connection, and so on. Do not touch the machine during the calibration.

```
# powertop --calibrate

```

## See also

*   [Official site](https://01.org/powertop/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Powertop "wikipedia:Powertop")
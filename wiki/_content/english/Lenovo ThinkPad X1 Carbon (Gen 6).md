Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Suspend-to-RAM (S3) not supported by default](#Suspend-to-RAM_.28S3.29_not_supported_by_default)
    *   [2.2 S0i3 support](#S0i3_support)
    *   [2.3 BIOS configurations](#BIOS_configurations)
*   [3 Power Management/Throttling issues](#Power_Management.2FThrottling_issues)

## Model description

Lenovo ThinkPad X1 Carbon, Gen 6.

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 6th

```

## Suspend issues

### Suspend-to-RAM (S3) not supported by default

The 6th Generation X1 Carbon supports S0i3 (also known as Windows Modern Standby) and does not support the S3 sleep state. See [https://delta-xi.net/#056](https://delta-xi.net/#056) for instructions for patching ACPI DSDT tables to add S3 support.

See [https://bbs.archlinux.org/viewtopic.php?id=234913](https://bbs.archlinux.org/viewtopic.php?id=234913) for the discussion related to this issue.

### S0i3 support

From [https://forums.lenovo.com/t5/Linux-Discussion/X1-Carbon-Gen-6-cannot-enter-deep-sleep-S3-state-aka-Suspend-to/m-p/4016317/highlight/true#M10682](https://forums.lenovo.com/t5/Linux-Discussion/X1-Carbon-Gen-6-cannot-enter-deep-sleep-S3-state-aka-Suspend-to/m-p/4016317/highlight/true#M10682), add the kernel parameter:

```
acpi.ec_no_wakeup=1

```

You might also need to disable the Realtek memory card reader (which appears to use a constant 2-3 W) either via the BIOS or via

```
echo "2-3" | sudo tee /sys/bus/usb/drivers/usb/unbind

```

### BIOS configurations

*   Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled". When disabled, on Linux, power usage appears to be significantly higher because of a substantial number of CPU wakeups during s2idle.

## Power Management/Throttling issues

Due to wrong configured power management registers the CPU may consume a lot less power than under windows and the thermal throttling occurs at 80°C (97°C when using Windows, see [https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/)).

There is a post in the official Lenovo forum ([https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489)) to inform Lenovo about this issue.
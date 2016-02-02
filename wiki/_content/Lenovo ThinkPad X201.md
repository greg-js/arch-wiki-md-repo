# Lenovo ThinkPad X201

The X201 is a 4-core subnotebook produced by Lenovo. See [Thinkwiki](http://www.thinkwiki.org/wiki/Category:X201) for specifications.

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Network](/index.php/Network "Network") | Yes |
| [Wireless](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Card reader | Yes |
| [Power management](/index.php/Power_management "Power management") | Limited |

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Prevent LID switch from waking up](#Prevent_LID_switch_from_waking_up)
    *   [1.2 Fbsplash](#Fbsplash)
    *   [1.3 Power saving](#Power_saving)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Overheating](#Overheating)
    *   [2.2 No speaker output](#No_speaker_output)
    *   [2.3 No ACPI events](#No_ACPI_events)

## Configuration

### Prevent LID switch from waking up

 `/etc/tmpfiles.d/disable-lid-wakeup.conf`  `w /proc/acpi/wakeup - - - - LID` 

### Fbsplash

To make [fbsplash](/index.php/Fbsplash "Fbsplash") work, i915 has to be added to the modules array in mkinitcpio.conf:

 `/etc/mkinitcpio.conf`  `MODULES="i915"` 

### Power saving

**Warning:** These options may cause system instabilities. Remove them if experiencing problems.

Add the `i915_enable_rc6=1` and `i915_enable_fbc=1` [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to make use of power saving mechanismens turned off by default because of reported instabilities.

## Troubleshooting

### Overheating

There are some discussions concerning overheating-related shutdowns when running under full load (video encoding, etc). [[1]](http://forums.lenovo.com/t5/X-Series-ThinkPad-Laptops/x201-random-shutdown/td-p/227471) [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/751689)

See [Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control") to install _tpfand_ as a replacement for hardware (BIOS) fan control.

**Warning:** Wrong settings may damage your machine - use with caution.

Start `tpfan-admin`, and adjust the settings by clicking on the sensor's graph. Split the graph (via context menu), and set the fan to **full-speed** when the sensor reaches, say, 65 °C. You may also edit the config file directly.

Alternatively, use the following [thinkfan](https://aur.archlinux.org/packages/thinkfan/) configuration [[3]](http://thinkpad-forum.de/threads/185587-X201-Thinkfan-Standardschaltschwellen-ermitteln):

 `/etc/thinkfan.conf` 

```
#X201 user specific
#lvl    low     up      RPM
(0,    0,      47)     # 0
(1,    42,     57)     # 2000
(2,    44,     59)     # 3300
(3,    50,     65)     # 3500
(4,    54,     70)     # 3500
(5,    60,     73)     # 3800
(6,    62,     83)     # 3800
(7,    65,     88)     # 4300
(127,  70,     32767)  # 5300

```

[cpupower](https://www.archlinux.org/packages/?name=cpupower) can be used for frequency scaling; see [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") for more information. Undervolting is not possible with the Intel core iX cpu.

### No speaker output

Try pressing the **mute button** (next to the Escape key). See [this article](http://www.stderr.nl/Blog/Hardware/Thinkpad/WeirdMuteButtonBehaviour.html) for details.

### No ACPI events

After suspension, an EC IRQ may hang in the queue causing all functions keys to stop working. [[4]](http://www.coreboot.org/Board:lenovo/x201) As a workaround, reload the _thinkpad_acpi_ module:

```
# rmmod -f thinkpad_acpi
# modprobe thinkpad_acpi

```

**Note:** `-f` is used as the module may be in use.

Other issues include the yellow USB port not being powered.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X201&oldid=410674](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X201&oldid=410674)"
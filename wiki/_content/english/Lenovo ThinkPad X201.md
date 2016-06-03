The [Lenovo X201](https://support.lenovo.com/us/en/documents/migr-75044) is a dual-core subnotebook produced by Lenovo.

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
| [Backlight](/index.php/Backlight "Backlight") | Limited |

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Modify wake events](#Modify_wake_events)
    *   [1.2 Power saving](#Power_saving)
    *   [1.3 Backlight](#Backlight)
    *   [1.4 Hibernation](#Hibernation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Overheating](#Overheating)
    *   [2.2 No speaker output](#No_speaker_output)
    *   [2.3 No ACPI events](#No_ACPI_events)
    *   [2.4 Display issues](#Display_issues)
*   [3 lspci](#lspci)
*   [4 See also](#See_also)

## Configuration

### Modify wake events

Events which cause the system to resume from [power states](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface#Power_states "w:Advanced Configuration and Power Interface") can be regulated in `/proc/acpi/wakeup`. Writing an entry from the *Device* column toggles the status from `enabled` to `disabled`, or vice-versa.

For example, to disable waking from suspend (S3) on opening the lid, run:

```
# echo LID > /proc/acpi/wakeup

```

This change can be made permament with tmpfiles.d(5):

 `/etc/tmpfiles.d/disable-lid-wakeup.conf`  `w /proc/acpi/wakeup - - - - LID` 

### Power saving

**Warning:** These options may cause system instabilities. Remove them if experiencing problems.

Add the `i915_enable_rc6=1` and `i915_enable_fbc=1` [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to make use of power saving mechanismens turned off by default because of reported instabilities.

### Backlight

As of [linux](https://www.archlinux.org/packages/?name=linux) 4.4 and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 4.1, backlight keys must be configured manually. See [Backlight](/index.php/Backlight "Backlight") for details.

### Hibernation

Hibernation works with [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 4.1\. See [Power management/Suspend and hibernate#Hibernation](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate").

## Troubleshooting

### Overheating

There are some discussions concerning overheating-related shutdowns when running under full load (video encoding, etc). [[1]](http://forums.lenovo.com/t5/X-Series-ThinkPad-Laptops/x201-random-shutdown/td-p/227471) [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/751689)

Use the following [thinkfan](https://aur.archlinux.org/packages/thinkfan/) configuration [[3]](http://thinkpad-forum.de/threads/185587-X201-Thinkfan-Standardschaltschwellen-ermitteln):

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

After suspension, an EC IRQ may hang in the queue causing all functions keys to stop working. [[5]](http://www.coreboot.org/Board:lenovo/x201)

It may help to reload the *thinkpad_acpi* module (`rmmod -f` is used as the module may be in use):

```
# rmmod -f thinkpad_acpi
# modprobe thinkpad_acpi

```

Other issues include the yellow USB port not being powered.

### Display issues

See [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

## lspci

**Note:** Model: X201, Type: 3680-WPH

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:19.0 Ethernet controller: Intel Corporation 82577LM Gigabit Network Connection (rev 06)
00:1a.0 USB controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 06)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 06)
00:1c.3 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 4 (rev 06)
00:1c.4 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 5 (rev 06)
00:1d.0 USB controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a6)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 06)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 6 port SATA AHCI Controller (rev 06)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 06)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 06)
02:00.0 Network controller: Intel Corporation Centrino Ultimate-N 6300 (rev 35)
ff:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 02)
ff:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 02)
ff:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 02)
ff:02.1 Host bridge: Intel Corporation 1st Generation Core i3/5/7 Processor QPI Physical 0 (rev 02)
ff:02.2 Host bridge: Intel Corporation 1st Generation Core i3/5/7 Processor Reserved (rev 02)
ff:02.3 Host bridge: Intel Corporation 1st Generation Core i3/5/7 Processor Reserved (rev 02)

```

## See also

*   [ThinkWiki.org](http://www.thinkwiki.org/wiki/Category:X201)
*   [ThinkWiki.de](http://thinkwiki.de/X201)
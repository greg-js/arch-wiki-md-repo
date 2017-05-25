**Note:** This page is basing on the L5H60EA#ABD version of HP Pro x2 612 G2, it should also work with the other versions.

| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| LTE/HSPA+ 4G Mobile Broadband | Not tested |  ? |
| Bluetooth | Working | bluetooth |
| Audio | Working | snd_hda_intel |
| Touchscreen | Working |  ? |
| Webcam | Not working |  ? |
| microSD Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Buggy |  ? |
| Power Management | Working | ... |
| Finger Print Scanner | Not working | libfprint |
| Smart Card Reader | Not tested |  ? |
| Ambient light sensor | Working, kernel >= 4.11 | iio-sensor-proxy |
| Acceleration sensor, Magnetometer, Gyro | Working, kernel >= 4.11 | iio-sensor-proxy |

This page covers the current status of hardware support on Arch, pre-installation system configuration tweaks, as well as post-installation recommendations to improve the usability of the system.

The installation process for Arch on the HP Pro x2 612 G2 does not differ from any other PC. For installation help please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). To set up a dual boot configuration with Windows, refer to [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Graphics Configuration](#Graphics_Configuration)
*   [3 IIO Sensors](#IIO_Sensors)
*   [4 Power Management](#Power_Management)
    *   [4.1 Suspend](#Suspend)
    *   [4.2 Battery](#Battery)
*   [5 Function keys](#Function_keys)
*   [6 Known issues](#Known_issues)
    *   [6.1 ACPI errors](#ACPI_errors)

## Pre-Installation System Settings

Prior to installation, access the system UEFI firmware by pressing F2 during boot.

*   Secure Boot: disable

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

## Graphics Configuration

The HP Pro x2 612 G2 has Intel HD Graphics 615 integrated graphics, see [Intel graphics](/index.php/Intel_graphics "Intel graphics") for details.

## IIO Sensors

[iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) is working with kernel 4.11.

[Issue on GitHub](https://github.com/hadess/iio-sensor-proxy/issues/163)

## Power Management

### Suspend

Suspend works without issues.

### Battery

Battery life can be improved by installing [powertop](https://www.archlinux.org/packages/?name=powertop) and calibrating it. See [Powertop](/index.php/Powertop "Powertop") for more info.

It's also possible to deactivate some devices and ports over the BIOS.

*   BIOS -> Advanced -> Build-In Device options (Example: WWAN)
*   BIOS -> Advanced -> Port Options (Example: Smart Card)

## Function keys

| **Function Key** | **Status** | **Comment** |
| Body - Volume down | Not working |
| Body - Volume down | Not working |
| Keyboard - Switches the screen image among display devices connected to the system (FN + F1) | Working |  ? |
| Keyboard - Decreases the screen brightness (FN + F3) | Not working | no output via xev |
| Keyboard - Increases the screen brightness (FN + F4) | Not working | no output via xev |
| Keyboard - Mute (FN + F5) | Working | mute light of the key is not working |
| Keyboard - Volume down (FN + F6) | Working |
| Keyboard - Volume up (FN + F7) | Working |
| Keyboard - Microphone mute (FN + F8) | Not working | no output via xev |
| Keyboard - Keyboard light (FN + F9) | Working |
| Keyboard - Num lock (FN + F10) | Working |
| Keyboard - calendar (FN + F12) | Not working |
| Keyboard - screen sharing | Not working |
| Keyboard - answer call | Not working |
| Keyboard - end call | Not working |

# Known issues

## ACPI errors

There are lots of acpi related error messages:

```
Apr 23 09:27:44 localhost kernel: ACPI Error: Field [CAP1] at 96 exceeds Buffer [NULL] size 64 (bits) (20160930/dsopcode-236)
Apr 23 09:27:44 localhost kernel: ACPI Error: Method parse/execution failed [\_SB._OSC] (Node ffff880226cea7f8), AE_AML_BUFFER_LIMIT (20160930/psparse-543)

Apr 23 09:27:45 localhost kernel: ACPI Exception: AE_AML_PACKAGE_LIMIT, Index (0x000000005) is beyond end of object (length 0x5) (20160930/exoparg2-427)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_TZ.GETP] (Node ffff880226cea2f8), AE_AML_PACKAGE_LIMIT (20160930/psparse-543)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_TZ.CHGZ._CRT] (Node ffff880226cebfc8), AE_AML_PACKAGE_LIMIT (20160930/psparse-543)

Apr 23 09:27:45 localhost kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88021def0750 (20160930/exresop-594)
Apr 23 09:27:45 localhost kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160930/dswexec-461)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff880226ca2d98), AE_AML_OPERAND_TYPE (20160930/psparse-543)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff880226ca22d0), AE_AML_OPERAND_TYPE (20160930/psparse-543)

Apr 23 09:27:45 localhost kernel: ACPI Error: Attempt to CreateField of length zero (20160930/dsopcode-168)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPI] (Node ffff880226ca2208), AE_AML_OPERAND_VALUE (20160930/psparse-543)
Apr 23 09:27:45 localhost kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff880226ca22d0), AE_AML_OPERAND_VALUE (20160930/psparse-543)

```

Upstream report: [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=194833) - looks like a HP Bios bug
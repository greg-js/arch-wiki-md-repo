**Note:** This page is basing on the L5H60EA#ABD version of HP Pro x2 612 G2, it should also work with the other versions. Current bios version is 1.0.5

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
| Ambient light sensor | Working, kernel = 4.11 | iio-sensor-proxy |
| Acceleration sensor, Magnetometer, Gyro | Working, kernel = 4.11 | iio-sensor-proxy |

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
        *   [6.1.1 After Bios update to 1.05](#After_Bios_update_to_1.05)

## Pre-Installation System Settings

Prior to installation, access the system UEFI firmware by pressing F2 during boot.

*   Secure Boot: disable

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

## Graphics Configuration

The HP Pro x2 612 G2 has Intel HD Graphics 615 integrated graphics, see [Intel graphics](/index.php/Intel_graphics "Intel graphics") for details.

## IIO Sensors

[iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) is working with kernel 4.11\. With kernel version 4.12 is not working

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
| Body - Volume down | Working |
| Body - Volume down | Working |
| Keyboard - Switches the screen image among display devices connected to the system (FN + F1) | Working |  ? |
| Keyboard - Decreases the screen brightness (FN + F3) | Working |
| Keyboard - Increases the screen brightness (FN + F4) | Working |
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

### After Bios update to 1.05

Errors changed a little after bios update.

```
[    0.663157] ACPI Error: Field [CAP1] at 96 exceeds Buffer [NULL] size 64 (bits) (20170303/dsopcode-236)
[    0.663173] ACPI Error: Method parse/execution failed [\_SB._OSC] (Node ffff99b426d540f0), AE_AML_BUFFER_LIMIT (20170303/psparse-543)
[    1.337558] RAS: Correctable Errors collector initialized.
[    2.506913] ACPI Exception: AE_AML_PACKAGE_LIMIT, Index (0x000000005) is beyond end of object (length 0x5) (20170303/exoparg2-427)
[    2.507031] ACPI Error: Method parse/execution failed [\_TZ.GETP] (Node ffff99b426d54a28), AE_AML_PACKAGE_LIMIT (20170303/psparse-543)
[    2.507146] ACPI Error: Method parse/execution failed [\_TZ.CHGZ._CRT] (Node ffff99b426d55fc8), AE_AML_PACKAGE_LIMIT (20170303/psparse-543)
[    2.509748] ACPI Exception: AE_AML_PACKAGE_LIMIT, Index (0x000000005) is beyond end of object (length 0x5) (20170303/exoparg2-427)
[    2.509853] ACPI Error: Method parse/execution failed [\_TZ.GETP] (Node ffff99b426d54a28), AE_AML_PACKAGE_LIMIT (20170303/psparse-543)
[    2.509966] ACPI Error: Method parse/execution failed [\_TZ.CHGZ._CRT] (Node ffff99b426d55fc8), AE_AML_PACKAGE_LIMIT (20170303/psparse-543)
[    3.680108] ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff99b423894870 (20170303/exresop-593)
[    3.680116] ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20170303/dswexec-461)
[    3.680121] ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff99b426d0c640), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.680156] ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff99b426d0cb68), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.681110] ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff99b418b25f30 (20170303/exresop-593)
[    3.681114] ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20170303/dswexec-461)
[    3.681119] ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff99b426d0c640), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.681125] ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff99b426d0cb68), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.682151] ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff99b418918168 (20170303/exresop-593)
[    3.682156] ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20170303/dswexec-461)
[    3.682161] ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff99b426d0c640), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.682167] ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff99b426d0cb68), AE_AML_OPERAND_TYPE (20170303/psparse-543)
[    3.685523] ACPI Error: Attempt to CreateField of length zero (20170303/dsopcode-168)
[    3.685540] ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPI] (Node ffff99b426d0cde8), AE_AML_OPERAND_VALUE (20170303/psparse-543)
[    3.685551] ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff99b426d0cb68), AE_AML_OPERAND_VALUE (20170303/psparse-543)

```
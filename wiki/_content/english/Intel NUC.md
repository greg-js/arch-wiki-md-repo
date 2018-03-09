[Next Unit of Computing (NUC)](https://en.wikipedia.org/wiki/Next_Unit_of_Computing "wikipedia:Next Unit of Computing") is a small-form-factor (SFF) PC designed by Intel and is based on soldered-on low-power Celeron, Pentium, i3, i5 and i7 CPUs. Its motherboard measures 4 × 4 inches (10.16 × 10.16 cm).

The barebone kits consist of the board, in a plastic case with a fan, an external power supply and VESA mounting plate. Intel does offer for sale just the NUC motherboards, which have a built-in CPU, although (as of 2013) the price of a NUC motherboard is very close to the corresponding cased kit; third-party cases for the NUC boards are also available.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 NVMe](#NVMe)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Wireless](#Wireless)
    *   [1.4 LEDs](#LEDs)
*   [2 Performance](#Performance)
    *   [2.1 Boot](#Boot)
    *   [2.2 4K](#4K)
*   [3 Power management](#Power_management)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Audio plug](#Audio_plug)
    *   [4.2 TPM](#TPM)
    *   [4.3 Poweroff](#Poweroff)
*   [5 Resources](#Resources)

## Installation

Follow usual [installation guide](/index.php/Installation_guide "Installation guide") procedures.

It is highly recommended to update the board BIOS prior to installation. See [official Intel BIOS update instructions](https://www-ssl.intel.com/content/www/us/en/support/boards-and-kits/000005636.html) for details.

**Note:** Prior to BIOS update, review the community response to the latest BIOS version compatability with the specific NUC model, as some versions are known to cause new regressions.

### NVMe

Intel NUCs support NVMe drives connected to the PCIe M.2 connector. See [Solid State Drives/NVMe](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe").

**Tip:** If supported by the NVMe and/or other devices connected to the PCIe-slot, you may want to **enable** *Native ACPI OS PCIe Support* in the *Power* section to allow power saving and possible cooling the device in idle.

### Graphics

Most NUCs use integrated [Intel graphics](/index.php/Intel_graphics "Intel graphics"). See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") to enjoy it on supported NUC models.

### Wireless

Most NUC wireless adapters should work out of the box. Make sure relevant firmware is loaded. See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for details.

### LEDs

Some NUCs have LEDs which can be controlled by software by installing the kernel driver [intel_nuc_led-dkms-git](https://aur.archlinux.org/packages/intel_nuc_led-dkms-git/) [[1]](https://github.com/milesp20/intel_nuc_led). To use this, Software Control must be enabled in the BIOS *Power* settings.

## Performance

### Boot

Fastest boot times are achieved with [UEFI](/index.php/UEFI "UEFI") boot and disabling legacy boot in the BIOS settings.

### 4K

If you want to use 4K graphic output, open the BIOS settings and set *Devices and Peripherals* -> *Video* -> *IGD Minimum Memory* to 512 MB and *IGD Aperture Size* to 1024 MB.

## Power management

It is possible to reduce power usage, see [TLP](/index.php/TLP "TLP") and [Powertop](/index.php/Powertop "Powertop").

## Troubleshooting

### Audio plug

The [PulseAudio#Switch on connect](/index.php/PulseAudio#Switch_on_connect "PulseAudio") module is buggy and in some cases might cause pulseaudio to stop playing audio when disconnecting the plug, until pulse is restarted. In this case, comment out the module:

 `/etc/pulse/default.pa` 
```
#load-module module-switch-on-port-available

```

### TPM

NUC devices have [TPM](/index.php/TPM "TPM") capabilites that are currently blocked due to a few bugs in `tpm_crb`[[2]](https://bugzilla.kernel.org/show_bug.cgi?id=98181)[[3]](https://bugzilla.kernel.org/show_bug.cgi?id=111511). 4.6 Kernel still has no solution for Haswell TPMs but a relevant patch is work in progress[[4]](https://lkml.org/lkml/2016/4/19/46).

### Poweroff

After issuing a shutdown, the NUC might remain in some state which isn't completely shut down, as indicated by a remaining blue power LED. In this case it's neccesary to power off the unit by holding the power button for a few seconds.

The workaround for this issue is to disable all wake-on-CIR (infrared sensor) options in the BIOS. In some cases it might be required to disable the CIR sensor completely to fix the issue.

## Resources

*   [Official Intel NUC Support Community](https://communities.intel.com/community/tech/nuc)
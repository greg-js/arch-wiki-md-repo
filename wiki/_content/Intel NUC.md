# Intel NUC

[Next Unit of Computing (NUC)](https://en.wikipedia.org/wiki/Next_Unit_of_Computing) is a small-form-factor (SFF) PC designed by Intel and is based on soldered-on low-power i3, i5 and i7 CPUs. Its motherboard measures 4 × 4 inches (10.16 × 10.16 cm).

The barebone kits consist of the board, in a plastic case with a fan, an external power supply and VESA mounting plate. Intel does offer for sale just the NUC motherboards, which have a built-in CPU, although (as of 2013) the price of a NUC motherboard is very close to the corresponding cased kit; third-party cases for the NUC boards are also available.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 NVMe](#NVMe)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Wireless](#Wireless)
*   [2 Performance](#Performance)
    *   [2.1 Boot](#Boot)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 NUC brick-by-suspend issue](#NUC_brick-by-suspend_issue)
    *   [3.2 TPM](#TPM)
    *   [3.3 Poweroff](#Poweroff)
*   [4 Resources](#Resources)

## Installation

Follow usual [installation guide](/index.php/Installation_guide "Installation guide") procedures.

It is highly recommended to update the board BIOS prior to installation. See [official Intel BIOS update instructions](https://www-ssl.intel.com/content/www/us/en/support/boards-and-kits/000005636.html) for details.

**Note:** Prior to BIOS update, review the community response to the latest BIOS version compatability with the specific NUC model, as some versions are known to cause new regressions.

### NVMe

Intel NUCs support NVMe drives connected to the PCIe M.2 connector. See [Solid State Drives/NVMe](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe").

**Note:** In latest BIOS version 0033, M.2 is disabled by default due to a bug.

### Graphics

Most NUCs use integrated [Intel Graphics](/index.php/Intel_Graphics "Intel Graphics"). Make sure to install [VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") to enjoy the hardware graphics acceleration on supported NUC models.

**Note:** The `i915` Intel DRM driver suffers from various bugs and will throw kernel log errors. Fixes are pending in 4.5.x kernel branch.

### Wireless

Most NUC wireless adapters should work out of the box. Make sure relevant firmware is loaded. See [Wireless_network_configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for details.

## Performance

### Boot

Fastest boot times are achieved with [UEFI](/index.php/UEFI "UEFI") boot and disabling legacy boot in the BIOS settings.

## Troubleshooting

### NUC brick-by-suspend issue

**Warning:** There is a widely reported issue [[1]](https://communities.intel.com/thread/96168)[[2]](https://communities.intel.com/thread/93211)[[3]](https://www.reddit.com/r/intelnuc/comments/408rai/intel_nucs_getting_bricked_after_linux_sleep/) where Intel NUCs running Linux can become bricked by going into [sleep, suspend and/or hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"). The source of this issue in unclear but according to some reports Arch Linux is affected as well.

The current recommended workaround is to never wake up the NUC from hibernation via the power button but only through alternative means such as [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") or wake-on-USB.

If your NUC has become bricked, it might be possible to restore it by momentarily disconnecting the CMOS battery on the bottom side of the motherboard.

### TPM

NUC devices have [TPM](/index.php/TPM "TPM") capabilites that are currently blocked due to a bug [[4]](https://bugzilla.kernel.org/show_bug.cgi?id=98181) in `tpm_crb`. A fix should be available in the 4.4.x kernel.

### Poweroff

After issuing a shutdown, the NUC might remain in some state which isn't completely shut down, as indicated by a remaining blue power LED. In this case it's neccesary to power off the unit by holding the power button for a few seconds.

The workaround for this issue is to disable all wake-on-CIR (infrared sensor) options in the BIOS. In some cases it might be required to disable the CIR sensor completely to fix the issue.

## Resources

*   [Official Intel NUC Support Community](https://communities.intel.com/community/tech/nuc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Intel_NUC&oldid=418651](https://wiki.archlinux.org/index.php?title=Intel_NUC&oldid=418651)"
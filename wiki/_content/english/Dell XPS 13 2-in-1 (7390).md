Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The New Dell XPS 13 2-in-1 (7390) is the model released in mid 2019 in most territories and is the second iteration of the Dell XPS 13 2-in-1 series, including an updated 10th generation Intel Ice Lake processor with Iris Plus integrated graphics. It can be used like a tablet when folding the display 180 degrees backwards and includes a enlarged 16:10 FHD+ or UHD touchscreen which should work out of the box.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 First Boot](#First_Boot)
    *   [2.2 Intel LPSS](#Intel_LPSS)
    *   [2.3 Wifi & Bluetooth](#Wifi_&_Bluetooth)

## Installation

Installation is similar to most other Dell XPS machines although without modifications the machine will freeze a few seconds into boot. These modifications are outlined in the troubleshooting section.

It's recommended to update the kernel to 5.3 or higher once the system is bootable.

## Troubleshooting

### First Boot

To boot fully without the boot process hanging one must blacklist the 'intel_lpss_pci' module, which can be done on a live media installation by selecting the boot option you want and pressing 'e', navigating to the end of the boot options string, and adding 'modprobe.blacklist=intel_lpss_pci'. This should allow booting into the full OS and further installation to the internal SSD.

### Intel LPSS

To fix the intel_lpss_module the patch from this paste must be applied to the kernel.

[https://pastebin.com/R7FpCefm](https://pastebin.com/R7FpCefm) (last tested on linux 5.3.12.1-1)

Remember to be cautious about running code or installing patches from third party sources if you do not know what it does.

This patch should enable the system to boot without blacklisting the module, further enabling access to the touchscreen.

NOTE: The patch is no longer required as of 5.4.2.1-1, so upgrading your kernel after installation will resolve the LPSS issue.

### Wifi & Bluetooth

WiFi and Bluetooth should require at least linux 5.3 to work, alongside the latest linux-firmware package. However, there is a bug in the *iwlwifi* driver which affects all kernel versions from 5.4 up to and, as of writing, including 5.5rc2\. This bug loads the incorrect firmware onto the Killer AX1650i, causing a *Failed to run INIT ucode* error and breaks Wifi (see [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1878902) for discussion).

Currently two options are available:

*   Select an alternate *linux-** package which still runs using the 5.3.x branch; or
*   Symlink the *c0-50* firmware to *b0-50*, which the driver will load in preference to *b0-48* (which is the current latest release of *b0* type firmware):

```
 $ cd /lib/firmware
 $ ln -s iwlwifi-Qu-{c,b}0-hr-b0-50.ucode

```

Reboot your laptop and the correct firmware should now be loaded in preference. Your WiFi should connect now as expected.
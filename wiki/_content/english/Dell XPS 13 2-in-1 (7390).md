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

It's recommended to update the kernel to 5.3 or higher once the system is bootable. This can be easily performed by installing 'linux-mainline' from the AUR.

## Troubleshooting

### First Boot

To boot fully without the boot process hanging one must blacklist the 'intel_lpss_pci' module, which can be done on a live media installation by selecting the boot option you want and pressing 'e', navigating to the end of the boot options string, and adding 'modprobe.blacklist=intel_lpss_pci'. This should allow booting into the full OS and further installation to the internal SSD.

### Intel LPSS

To fix the intel_lpss_module the patch from this paste must be applied to the kernel.

[https://pastebin.com/sqPv8ShP](https://pastebin.com/sqPv8ShP)

Remember to be cautious about running code or installing patches from third party sources if you do not know what it does.

This patch should enable the system to boot without blacklisting the module, further enabling access to the touchscreen.

### Wifi & Bluetooth

In order to get Wifi & Bluetooth working as of 12.09.2019 firmware drivers should be downloaded from [https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/) and the contents should be copied into /lib/firmware.
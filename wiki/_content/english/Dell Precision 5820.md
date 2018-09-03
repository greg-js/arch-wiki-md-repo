The **Dell Precision 5820** is a desktop tower workstation.

## System specifications

The workstation has a processor of the Intel Xeon W family (Skylake-W) with no integrated graphics, and it can mount up to two PCI express X16 Gen 3 graphics cards. The machine can have up to two M.2 NVMe PCIe SSDs that are front-accessible and hot-swappable (when [Intel VMD](https://www.intel.com/content/www/us/en/architecture-and-technology/intel-volume-management-device-overview.html) is enabled). [Officially supported operating systems](https://www.dell.com/is/business/p/precision-5820-workstation/pd) are Windows 10 Pro, RHL Enterprise 7.3 and Ubuntu 16.04.

## Installation notes

The BIOS supports both UEFI and legacy boot (with the latter disabled by default). In order to install from the official Arch image, it may be necessary to disable secure boot from the BIOS setup.

After installation on the SSD drive, the system may fail to boot, being unable to locate the partitions:

```
ERROR: device 'UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX' not found. Skipping fsck.
mount: /new_root: can't find UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.
You are now being dropped into an emergency shell.
```

In that case, setting SATA operation mode to AHCI and disabling VMD should solve the problem (even though [it seems to be possible](https://ubuntuforums.org/showthread.php?t=2381899) to boot Ubuntu with RAID and VMD enabled, despite Dell [recommends to set SATA to AHCI](https://www.dell.com/support/article/us/en/04/sln299303/loading-ubuntu-on-systems-using-pcie-m2-drives?lang=en) when installing Ubuntu on systems with PCIe M2 drives).
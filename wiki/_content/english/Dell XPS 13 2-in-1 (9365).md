The Dell XPS 13 2-in-1 (9365) is the early 2017 model. It can be used like a tablet when folding the display on the back. The touchscreen works out of the box.

## Installation

With Bios version 1.0.21 you have to set sata operation to AHCI first and then uncheck in Advanced Boot options -> Legacy ROM.[[1]](http://en.community.dell.com/support-forums/laptop/f/3518/t/20004529?pi41097=1)

**Note:**

*   In RAID mode the BIOS/UEFI is able to see the internal drive and is able to boot from it. It is possible to boot Archiso in RAID mode, but it can't see the internal drive.
*   In AHCI mode the BIOS/UEFI with Legacy ROM activated is not able to see the internal drive. If you try to boot it will fail and display an error that no harddrive is installed.
*   In AHCI mode the BIOS/UEFI with Legacy ROM deactivated is able to see the internal drive and therefore boot from it and Archiso is able to see the drive too. With these settings you can install and boot arch.

## Troubleshooting

### Not waking from suspend

This model only supports the S0 (s2idle) sleep mode. [[2]](https://patchwork.kernel.org/patch/9758513/) Change the suspend mode to `s2idle` by adding the `mem_sleep_default=s2idle` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
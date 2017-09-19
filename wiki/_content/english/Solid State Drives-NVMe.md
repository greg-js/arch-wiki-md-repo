Related articles

*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")

NVM Express (NVMe) is a specification for accessing SSDs attached through the PCI Express bus. As a logical device interface, NVM Express has been designed from the ground up, capitalizing on the low latency and parallelism of PCI Express SSDs, and mirroring the parallelism of contemporary CPUs, platforms and applications.

## Contents

*   [1 Installation](#Installation)
*   [2 Performance](#Performance)
    *   [2.1 Sector size](#Sector_size)
    *   [2.2 Discards](#Discards)
    *   [2.3 Airflow](#Airflow)
    *   [2.4 Testing](#Testing)
*   [3 Power Saving APST](#Power_Saving_APST)
    *   [3.1 NVME Power Saving Patch](#NVME_Power_Saving_Patch)
*   [4 References](#References)

## Installation

The Linux NVMe driver is natively included in the kernel since version 3.3\. NVMe devices should show up under `/dev/nvme*`.

Extra userspace NVMe tools can be found in [nvme-cli](https://aur.archlinux.org/packages/nvme-cli/) or [nvme-cli-git](https://aur.archlinux.org/packages/nvme-cli-git/).

See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for supported filesystems, maximizing performance, minimizing disk reads/writes, etc.

**Note:** It may be needed to add the **nvme** module to the [MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array within `/etc/mkinitcpio.conf` to successfully boot into the root filesystem.

## Performance

### Sector size

See [Advanced Format#How to determine if HDD employ a 4k sector](/index.php/Advanced_Format#How_to_determine_if_HDD_employ_a_4k_sector "Advanced Format").

### Discards

**Note:** Although [continuous TRIM](/index.php/Solid_State_Drives#Continuous_TRIM "Solid State Drives") is an option (albeit not recommended) for SSDs, **NVMe devices should not be issued discards**.

Discards are disabled by default on typical setups that use [ext4](/index.php/Ext4 "Ext4") and [LVM](/index.php/LVM "LVM"), but other filesystems might need discards to be disabled explicitly.

Intel, as one device manufacturer, recommends not to enable discards at the filesystem level, but suggests the [periodic TRIM](/index.php/Solid_State_Drives#Periodic_TRIM "Solid State Drives") method, or apply `fstrim` manually.[[1]](https://communities.intel.com/thread/75161?start=0&tstart=0)

### Airflow

NVMe SSDs are known to be affected by high operating temperatures and will throttle performance over certain thresholds.[[2]](http://www.legitreviews.com/samsung-ssd-950-pro-512gb-nvme-pcie-ssd-review_174096/3)

### Testing

Raw device performance tests can be run with [hdparm](https://www.archlinux.org/packages/?name=hdparm):

```
# hdparm -Tt --direct /dev/nvme0n1

```

## Power Saving APST

### NVME Power Saving Patch

Andy Lutomirski has created a patchset which fixes powersaving for NVME devices in linux. The patch has been merged into mainline kernel v4.11\. For older kernels you can use: **Linux-nvme** — Mainline linux kernel patched with Andy's patch for NVME powersaving APST.

	[https://github.com/damige/linux-nvme](https://github.com/damige/linux-nvme) || [linux-nvme](https://aur.archlinux.org/packages/linux-nvme/).

To test if NVME Power Management is working, install [nvme-cli](https://aur.archlinux.org/packages/nvme-cli/) if running an older kernel, and run `# nvme get-feature -f 0x0c -H /dev/nvme[0-9]`.

When ASPT is enabled the output should contain "Autonomous Power State Transition Enable (APSTE): Enabled" and there should be non-zero entries in the table below indicating the idle time before transitioning into each of the available states.

If ASPT is enabled but no non-zero states appear in the table, the latencies might be too high for any states to be enabled by default. The output of `# nvme id-ctrl /dev/nvme[0-9]` should show the available non-operational power states of the NVME controller. If the total latency of any state (enlat + xlat) is greater than 25000 (25ms) then to enable it you must pass a value at least that high to the `default_ps_max_latency_us` option for the `nvme_core` module in the boot parameters. This should enable ASPT and make the table in `# nvme get-feature` show the entries.

## References

*   [Intel Linux NVMe driver reference](http://www.intel.com/content/dam/support/us/en/documents/ssdc/data-center-ssds/Intel_Linux_NVMe_Guide_330602-002.pdf)
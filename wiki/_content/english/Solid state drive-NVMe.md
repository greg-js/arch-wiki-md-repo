Related articles

*   [Solid State Drive](/index.php/Solid_State_Drive "Solid State Drive")

[NVM Express](https://en.wikipedia.org/wiki/NVM_Express "wikipedia:NVM Express") (NVMe) is a specification for accessing [SSDs](/index.php/SSD "SSD") attached through the PCI Express bus. As a logical device interface, NVM Express has been designed from the ground up, capitalizing on the low latency and parallelism of PCI Express SSDs, and mirroring the parallelism of contemporary CPUs, platforms and applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Performance](#Performance)
    *   [2.1 Sector size](#Sector_size)
    *   [2.2 Discards](#Discards)
    *   [2.3 Airflow](#Airflow)
    *   [2.4 Testing](#Testing)
*   [3 Power Saving APST](#Power_Saving_APST)
    *   [3.1 NVME Power Saving Patch](#NVME_Power_Saving_Patch)
        *   [3.1.1 Samsung drive errors on Linux 4.10](#Samsung_drive_errors_on_Linux_4.10)
*   [4 References](#References)

## Installation

The Linux NVMe driver is natively included in the kernel since version 3.3\. NVMe devices should show up under `/dev/nvme*`.

Extra userspace NVMe tools can be found in [nvme-cli](https://www.archlinux.org/packages/?name=nvme-cli) or [nvme-cli-git](https://aur.archlinux.org/packages/nvme-cli-git/).

See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for supported filesystems, maximizing performance, minimizing disk reads/writes, etc.

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

Andy Lutomirski has created a patchset which fixes powersaving for NVME devices in linux. The patch has been merged into mainline kernel v4.11.

To test if NVME Power Management is working, install [nvme-cli](https://www.archlinux.org/packages/?name=nvme-cli) or [nvme-cli-git](https://aur.archlinux.org/packages/nvme-cli-git/), and run `nvme get-feature -f 0x0c -H /dev/nvme[0-9]`:

 `# nvme get-feature -f 0x0c -H /dev/nvme0` 
```
get-feature:0xc (Autonomous Power State Transition), Current value:0x000001
        Autonomous Power State Transition Enable (APSTE): Enabled
        Auto PST Entries        .................

...
```

When APST is enabled the output should contain "Autonomous Power State Transition Enable (APSTE): Enabled" and there should be non-zero entries in the table below indicating the idle time before transitioning into each of the available states.

If APST is enabled but no non-zero states appear in the table, the latencies might be too high for any states to be enabled by default. The output of `# nvme id-ctrl /dev/nvme[0-9]` should show the available non-operational power states of the NVME controller. If the total latency of any state (enlat + xlat) is greater than 25000 (25ms) you must pass a value at least that high as parameter `default_ps_max_latency_us` for the `nvme_core` [kernel module](/index.php/Kernel_module "Kernel module"). This should enable APST and make the table in `# nvme get-feature` show the entries.

#### Samsung drive errors on Linux 4.10

On Linux 4.10, drive errors can occur and causing system instability. This seems to be the result of a power saving state that the drive cannot use. Adding the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `nvme_core.default_ps_max_latency_us=5500`[[3]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1678184)[[4]](https://askubuntu.com/questions/905710/ext4-fs-error-after-ubuntu-17-04-upgrade/906105#906105) disables the lowest power saving state, preventing write errors.

## References

*   [Intel Linux NVMe driver reference](http://www.intel.com/content/dam/support/us/en/documents/ssdc/data-center-ssds/Intel_Linux_NVMe_Guide_330602-002.pdf)
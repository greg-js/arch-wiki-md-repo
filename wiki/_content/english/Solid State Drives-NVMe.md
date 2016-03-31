NVM Express (NVMe) is a specification for accessing SSDs attached through the PCI Express bus. As a logical device interface, NVM Express has been designed from the ground up, capitalizing on the low latency and parallelism of PCI Express SSDs, and mirroring the parallelism of contemporary CPUs, platforms and applications.

## Contents

*   [1 Installation](#Installation)
*   [2 Performance](#Performance)
    *   [2.1 Alignment](#Alignment)
    *   [2.2 Discards](#Discards)
    *   [2.3 Airflow](#Airflow)
    *   [2.4 Testing](#Testing)
*   [3 References](#References)

## Installation

The Linux NVMe driver is natively included in the kernel since version 3.3\. NVMe devices should show up under `/dev/nvme*`.

Extra userspace NVMe tools can be found in [nvme-cli-git](https://aur.archlinux.org/packages/nvme-cli-git/)

## Performance

### Alignment

Partitions should be aligned to 4096 bytes.

### Discards

**Note:** Contrary to recommendations for SSDs, **NVMe devices should not be issued discards**.

Discards are disabled by default on typical setups that use [ext4](/index.php/Ext4 "Ext4") and [LVM](/index.php/LVM "LVM"), but other filesystems might need discards to be disabled explicitly.

Intel, as one device manufacturer, recommends not to enable discards at the filesystem level, but suggests the [Solid State Drives#Apply periodic TRIM via fstrim](/index.php/Solid_State_Drives#Apply_periodic_TRIM_via_fstrim "Solid State Drives") method, or apply *fstrim* manually.[[1]](https://communities.intel.com/thread/75161?start=0&tstart=0)

### Airflow

NVMe SSDs are known to be affected by high operating temperatures and will throttle performance over certain thresholds.[[2]](http://www.legitreviews.com/samsung-ssd-950-pro-512gb-nvme-pcie-ssd-review_174096/3)

### Testing

Raw device performance tests can be run with [hdparm](https://www.archlinux.org/packages/?name=hdparm):

```
# hdparm -Tt --direct /dev/nvme0n1

```

## References

*   [Intel Linux NVMe driver reference](http://downloadmirror.intel.com/23929/eng/Intel_Linux_NVMe_Driver_Reference_Guide_330602-002.pdf)
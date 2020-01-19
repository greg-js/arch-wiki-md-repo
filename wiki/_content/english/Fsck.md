Related articles

*   [Ext4](/index.php/Ext4 "Ext4")
*   [Btrfs](/index.php/Btrfs "Btrfs")
*   [fstab](/index.php/Fstab "Fstab")

[fsck](https://en.wikipedia.org/wiki/Fsck "wikipedia:Fsck") stands for *"file system check"* and it is used to check and optionally repair one or more Linux file systems. Normally, the fsck program will try to handle filesystems on different physical disk drives in parallel to reduce the total amount of time needed to check all of the filesystems (see: [fsck(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.8)).

The [Arch Linux boot process](/index.php/Arch_boot_process "Arch boot process") conveniently takes care of the fsck procedure for you and will check all relevant partitions on your drive(s) automatically on every boot. Hence, there is usually no need to resort to the command-line unless necessary.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Boot time checking](#Boot_time_checking)
    *   [1.1 Mechanism](#Mechanism)
    *   [1.2 Forcing the check](#Forcing_the_check)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Attempt to repair damaged blocks](#Attempt_to_repair_damaged_blocks)
    *   [2.2 Repair damaged blocks interactively](#Repair_damaged_blocks_interactively)
    *   [2.3 Changing the check frequency](#Changing_the_check_frequency)
    *   [2.4 fstab options](#fstab_options)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Can't run fsck on a separate /usr partition](#Can't_run_fsck_on_a_separate_/usr_partition)
    *   [3.2 ext2fs : no external journal](#ext2fs_:_no_external_journal)

## Boot time checking

### Mechanism

There are two players involved:

1.  mkinitcpio offers you the option to fsck your root filesystem before mounting it via the fsck hook. If you do this, you should mount root read-write via the appropriate `rw` kernel parameter.[[1]](https://projects.archlinux.org/mkinitcpio.git/commit/?id=449b3e543c)
2.  systemd will fsck all filesystems having a fsck pass number greater than 0 (either from `/etc/fstab` or a user-supplied unit file). For the root filesystem, it also has to be mounted read-only initially with the kernel parameter `ro` and only then remounted read-write from [fstab](/index.php/Fstab "Fstab") (note that the `defaults` mount option implies `rw`).

The first option is the recommended default, and what you will end up with if you follow the [Installation guide](/index.php/Installation_guide "Installation guide"). If you want to go with option 2 instead, you should remove the fsck hook from `mkinitcpio.conf` and use `ro` on the kernel commandline. The kernel parameter `fsck.mode=skip` can be used to make sure fsck is disabled entirely for both options.

### Forcing the check

If you use the `base` [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook, you can force fsck at boot time by passing `fsck.mode=force` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). This will check every filesystem you have on the machine.

Alternatively, systemd provides [systemd-fsck@.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fsck%40.service.8), which checks all configured file systems, which were not checked in the initramfs. However, checking the root filesystem this way causes a delay in the boot process, because the file system has to be remounted.

**Note:** For those accustomed to use other GNU/Linux distributions, the old tricks consisting in writing a file with the name `forcefsck` to the root of each filesystem or using the command `shutdown` with the `-F` flag were only working for the old [SysVinit](/index.php/SysVinit "SysVinit") and early versions of [Upstart](https://en.wikipedia.org/wiki/Upstart "wikipedia:Upstart") and are not working with [systemd](/index.php/Systemd "Systemd"). The aforementioned solution is thus the only one working for Arch Linux.

## Tips and tricks

### Attempt to repair damaged blocks

To automatically repair damaged portions, run:

**Warning:** This will not ask if you want to repair it, as the answer is **Yes** when you run it.

```
# fsck -a

```

### Repair damaged blocks interactively

**Tip:** This is useful for when file on the boot partition have changed, and the journal failed to properly update. In this case, unmount the boot partition, and run the following code:

To repair damaged portions, run :

```
# fsck -r <drive>

```

### Changing the check frequency

By default, fsck checks a filesystem every 30 boots (counted individually for each partition). To change the frequency of checking, run:

```
# tune2fs -c 20 /dev/sda1

```

In this example, `20` is the number of boots between two checks.

Note that `1` would make it scan at every boot, while `0` would stop scanning altogether.

**Tip:** If you wish to see the frequency number and the current mount count for a specific partition, use:
```
# dumpe2fs -h /dev/sda1 | grep -i 'mount count'

```

### fstab options

[fstab](/index.php/Fstab "Fstab") is a system configuration file and is used to tell the Linux kernel which partitions (file systems) to mount and where on the file system tree.

A typical `/etc/fstab` entry may look like this:

```
/dev/sda1   /         ext4      defaults       0  **1**
/dev/sda2   /other    ext4      defaults       0  **2**
/dev/sda3   /win      ntfs-3g   defaults       0  **0**

```

The 6th column (in bold) is the fsck option.

*   0 = Do not check.
*   1 = First file system (partition) to check; `/` (root partition) should be set to 1.
*   2 = All other filesystems to be checked.

## Troubleshooting

### Can't run fsck on a separate /usr partition

1.  Make sure you have the required [hooks](/index.php/Mkinitcpio#.2Fusr_as_a_separate_partition "Mkinitcpio") in `/etc/mkinitcpio.conf` and that you remembered to re-generate your initramfs image after editing this file.
2.  Check your [fstab](/index.php/Fstab "Fstab")! Only the root partition needs "1" at the end, everything else should have either "2" or "0". Carefully inspect it for other typos, as well.

### ext2fs : no external journal

There are times (due to power failure) in which an ext(3/4) file system can corrupt beyond normal repair. Normally, there will be a prompt from fsck indicating that it cannot find an external journal. In this case, run the following commands:

Unmount the partition based on its directory

```
# umount <directory>

```

Write a new journal to the partition

```
# tune2fs -j /dev/<partition>

```

Run an fsck to repair the partition

```
# fsck -p /dev/<partition>

```
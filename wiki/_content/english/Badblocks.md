*badblocks* is a program to test storage devices for bad blocks.

In case of a HDD the whole sector should get retired. A sector is a subdivision of a track on a storage device and sectors that have become bad cannot be used because they have become permanently damaged (a bad sector can have adverse effects ranging from changing a letter in a text file to causing a binary program to have a segmentation fault).

[S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") (Self-Monitoring, Analysis, and Reporting Technology) is hardware-featured in almost every HDD still in use nowadays and in some cases it can automatically retire defective HDD sectors. Anyhow S.M.A.R.T. only passively waits for errors while *badblocks* writes simple patterns to every block of a device and then reads and checks them searching for damaged areas. (Just like memtest86* does with RAM.)

This can be done in a destructive write-mode that effectively [wipes](/index.php/Securely_wipe_disk "Securely wipe disk") the device (do backup!) or in non-destructive read-write (backup advisable as well!) and read-only modes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Storage device fidelity](#Storage_device_fidelity)
*   [3 Comparisons with other programs](#Comparisons_with_other_programs)
*   [4 Testing for bad sectors](#Testing_for_bad_sectors)
    *   [4.1 Read-write test (warning:destructive)](#Read-write_test_(warning:destructive))
        *   [4.1.1 Define specific test pattern](#Define_specific_test_pattern)
            *   [4.1.1.1 Random pattern](#Random_pattern)
    *   [4.2 Read-write test (non-destructive)](#Read-write_test_(non-destructive))
*   [5 Have filesystem incorporate bad sectors](#Have_filesystem_incorporate_bad_sectors)
    *   [5.1 During filesystem check](#During_filesystem_check)
    *   [5.2 Before filesystem creation](#Before_filesystem_creation)
        *   [5.2.1 Ext4](#Ext4)
        *   [5.2.2 Block size](#Block_size)
*   [6 See also](#See_also)

## Installation

The [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) package is part of the [base group](/index.php/Base_group "Base group"). See [badblocks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/badblocks.8) for the usage.

## Storage device fidelity

Although there is no firm rule, it is common thinking that a new drive should have zero bad sectors. Over time, bad sectors will develop and although they are able to be defined to the file system so that they are avoided, continual use of the drive will usually result in additional bad sectors forming and it is usually the harbinger of its eventual death. Replacing the device is recommended.

## Comparisons with other programs

Typical recommended practice for testing a storage device for bad sectors is to use the manufacturer's testing program. Most manufacturers have programs that do this. The main reasoning for this is that manufacturers usually have their standards built into the test programs that will tell you if the drive needs to be replaced or not. The caveat here being is that some manufacturers testing programs do not print full test results and allow a certain number of bad sectors saying only if they pass or not. Manufacturer programs, however, are generally quicker than *badblocks* sometimes a fair amount so.

## Testing for bad sectors

To test for bad sectors in Linux the program *badblocks* is typically used. *badblocks* has several different modes to be able to detect bad sectors.

### Read-write test (warning:destructive)

This test is primarily for testing new drives and is a read-write test. As the pattern is written to every accessible block the device effectively gets [wiped](/index.php/Securely_wipe_disk "Securely wipe disk"). Default is an extensive test with four passes using four different patterns: 0xaa (10101010), 0x55 (01010101), 0xff (11111111) and 0x00 (00000000). For some devices this will take a couple of days to complete.

 `# badblocks -wsv /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing: done
Testing with pattern **0x55**: done
Reading and comparing: done
Testing with pattern **0xff**: 22.93% done, 4:09:55 elapsed. (0/0/0 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

Options:

	`-w`: do a destructive write test

	`-s`: show progress-bar

	`-v`: be "verbose" and output bad sectors detected to stdout

Additional options you might consider:

	`-b *number*`: specify the block size of the hard disk which can significantly improve testing time. (`# tune2fs -l *partition*`)

	`-p *number*`: run through the extensive four pass test *number* of sequent iterations

	`-o */path/to/output-file*`: print bad sectors to *output-file* instead of stdout

	`-t *test_pattern*`: Specify a pattern. See below.

#### Define specific test pattern

**From the manpage:** "The *test_pattern* may either be a numeric value between 0 and ULONG_MAX-1 inclusive [...]."

##### Random pattern

*Badblocks* can be made to repeatedly write a single "random pattern" with the `-t random` option.

 `# badblocks -wsv -t random /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with **random pattern**: done                                                 
Reading and comparing: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

**Warning:** This is not secure for cryptographic purposes. A "random pattern" is a contradiction in itself. As *badblocks* does not (like [/dev/urandom](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random")) apply sophisticated procedures to reuse entropy but simply repeats one "random pattern" it should not be used where random data would be needed, e.g. for [block device encryption](/index.php/Securely_wipe_disk#Preparations_for_block_device_encryption "Securely wipe disk").

### Read-write test (non-destructive)

This test is designed for devices with data already on them. A non-destructive read-write test makes a backup of the original content of a sector before testing with a single random pattern and then restoring the content from the backup. This is a single pass test and is useful as a general maintenance test.

 `# badblocks -nsv /dev/*device*` 
```
Checking for bad blocks in non-destructive read-write mode
From block 0 to 488386583
Checking for bad blocks (non-destructive read-write test)
Testing with **random pattern**: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

The `-n` option signifies a non-destructive read-write test.

## Have filesystem incorporate bad sectors

To not use bad sectors they have to be known by the filesystem.

### During filesystem check

Incorporating bad sectors can be done using the filesystem check utility (`fsck`). `fsck` can be told to use *badblocks* during a check. To do a **read-write** (non-destructive) test and have the bad sectors made known to the filesystem run:

```
# fsck -vcck /dev/*device-PARTITION*

```

The `-cc` option tells run `fsck` in **non-destructive** test mode, the `-v` tells `fsck` to show its output, and the `-k` option preserves old bad sectors that were detected.

To do a **read-only** test (not recommended):

```
# fsck -vck /dev/*device-PARTITION*

```

### Before filesystem creation

Alternately, this can be done before filesystem creation.

If *badblocks* is run without the `-o` option bad sectors will only be printed to stdout.

Example output for read errors in the beginning of the disk:

 `# badblocks -wsv /dev/*drive*` 
```
[...]
Testing with pattern **0xff**: done                                                 
Reading and comparing:
[...]
37584
37585 0.84% done, 7:31:08 elapsed. (0/0/527405 errors)
37586
[...]
done
Testing with pattern **0x00**:
Reading and comparing:
[...]
37584
37585
[...]
done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

For comfortably passing *badblocks* error output to the filesystem it has to be written to a file.

 `# badblocks -wsv **-o** /root/*badblocks.txt* /dev/*device*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing:   6.36% done, 0:51 elapsed. (0/0/14713 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

Then (re-)create the file system with the information:

```
# mkfs.*filesystem-type* **-l** /root/*badblocks.txt* /dev/*device*

```

**Note:** The meaning of `0/0/527405` errors is *number_of_read_errors* / *number_of_write_errors* / *number_of_corruption_errors*.

#### Ext4

From the [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) manual page:

	Note that the block numbers in the bad block list must be generated using the same block size as used by *mke2fs*. As a result, the `-c` option to *mke2fs* is a much simpler and less error-prone method of checking a disk for bad blocks before formatting it.

So the recommended method is to use:

```
# mkfs.ext4 -c /dev/*device*

```

Use `-cc` to do a read-write bad block test.

#### Block size

First find the file systems **block size**. For example for ext# filesystems:

```
# dumpe2fs /dev/*device-PARTITION* | grep 'Block size'

```

Feed this to *badblocks*:

```
# badblocks -b *block size*

```

## See also

*   [My hard disk has bad sectors or is developing bad sectors over time](http://www.pcguide.com/ts/x/comp/hdd/errorsBadSectors-c.html)
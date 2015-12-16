# Benchmarking/Disk wipes

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")
*   [Frandom](/index.php/Frandom "Frandom")
*   [Benchmarking](/index.php/Benchmarking "Benchmarking")

Benchmark different methods of [disk wiping](/index.php/Securely_wipe_disk "Securely wipe disk").

## Contents

*   [1 Frequently asked questions](#Frequently_asked_questions)
    *   [1.1 How do I wipe a disk?](#How_do_I_wipe_a_disk.3F)
    *   [1.2 Are there other ways to benchmark a disk?](#Are_there_other_ways_to_benchmark_a_disk.3F)
    *   [1.3 How do I get the HDD model with hdparm?](#How_do_I_get_the_HDD_model_with_hdparm.3F)
    *   [1.4 How do I check progress of dd while running?](#How_do_I_check_progress_of_dd_while_running.3F)
    *   [1.5 Benchmarking with dcfldd](#Benchmarking_with_dcfldd)
*   [2 Data](#Data)
    *   [2.1 /dev/frandom](#.2Fdev.2Ffrandom)

## Frequently asked questions

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Benchmarking/Data storage devices](/index.php/Benchmarking/Data_storage_devices "Benchmarking/Data storage devices").**

**Notes:** Merge in case the content in [#Data](#Data) is (re)moved from here. Other possible candidates are [Benchmarking](/index.php/Benchmarking "Benchmarking") and [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk"). (Discuss in [Talk:Benchmarking/Disk wipes#](https://wiki.archlinux.org/index.php/Talk:Benchmarking/Disk_wipes))

### How do I wipe a disk?

See [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk").

### Are there other ways to benchmark a disk?

Of course. Take a look at [Hdparm](/index.php/Hdparm "Hdparm").

### How do I get the HDD model with hdparm?

```
# hdparm -i /dev/sdX | grep Model

```

### How do I check progress of dd while running?

See [Core utilities#Checking progress of dd while running](/index.php/Core_utilities#Checking_progress_of_dd_while_running "Core utilities").

### Benchmarking with dcfldd

Dcfldd doesn't print the average speed in MB/s like good old dd does but with [time](/index.php/Benchmarking#time "Benchmarking") you can work around that.

Time the run clearing the disk:

```
# time dcfldd if=/dev/zero of=/dev/sdX bs=4M
18944 blocks (75776Mb) written.dcfldd:: No space left of device
real     16m17.033s
user     0m0.377s
sys      0m51.160s

```

Calculate MB/s by dividing the output of the dcfldd command by the time in seconds. For this example: 75776Mb / (16.4 min * 60) = 77.0 MB/s.

## Data

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The community is encouraged to populate the tables in this section. Alternatively, delete this section. (Discuss in [Talk:Benchmarking/Disk wipes#](https://wiki.archlinux.org/index.php/Talk:Benchmarking/Disk_wipes))

### /dev/frandom

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Frandom](/index.php/Frandom "Frandom").**

**Notes:** The "Benchmarks" on the frandom page should get incorporated here. The frandom page should stay intact of course. Alternatively, delete this section. (Discuss in [Talk:Benchmarking/Disk wipes#](https://wiki.archlinux.org/index.php/Talk:Benchmarking/Disk_wipes))

Retrieved from "[https://wiki.archlinux.org/index.php?title=Benchmarking/Disk_wipes&oldid=412587](https://wiki.archlinux.org/index.php?title=Benchmarking/Disk_wipes&oldid=412587)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")
*   [Hardware](/index.php/Category:Hardware "Category:Hardware")
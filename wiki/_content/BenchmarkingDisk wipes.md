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
    *   [2.2 /dev/zero](#.2Fdev.2Fzero)

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

### /dev/zero

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** As the note below says, this data is not presented in a scientific, reproducible way, i.e. it is useless. Besides, do people really buy storage media based on the speed it gets wiped at with /dev/zero? There is plenty of benchmarks on the internet, and we already have [Benchmarking/Data storage devices](/index.php/Benchmarking/Data_storage_devices "Benchmarking/Data storage devices") to help people publish more on their blogs. (Discuss in [Talk:Benchmarking/Disk wipes#](https://wiki.archlinux.org/index.php/Talk:Benchmarking/Disk_wipes))

**Note:** As there has been no evident clarification in [the article this table was moved from](/index.php/Securely_wipe_disk "Securely wipe disk") it can only be assumed all wipes were done with `/dev/zero`.

<table class="wikitable sortable" style="text-align: right;">

<tbody>

<tr>

<th>Manufacture</th>

<th>Model</th>

<th>HDD Speed (RPM)</th>

<th>Interface</th>

<th>Capacity (GB)</th>

<th>Time (Hrs)</th>

<th>Throughput (MB/s)</th>

</tr>

<tr>

<td>Hitachi</td>

<td>HTS725016A9A364</td>

<td>7200</td>

<td>SATA2</td>

<td>160</td>

<td>0.72</td>

<td>63</td>

</tr>

<tr>

<td>Intel</td>

<td>SSDSA2M080G2GC</td>

<td>SSD</td>

<td>SATA2</td>

<td>80</td>

<td>0.27</td>

<td>77</td>

</tr>

<tr>

<td>Samsung</td>

<td>HD322HJ</td>

<td>7200</td>

<td>SATA2</td>

<td>320</td>

<td>1.15</td>

<td>74</td>

</tr>

<tr>

<td>Seagate</td>

<td>ST31000333AS</td>

<td>7200</td>

<td>SATA2</td>

<td>1000</td>

<td>2.92</td>

<td>90</td>

</tr>

<tr>

<td>Seagate</td>

<td>ST31500341AS</td>

<td>7200</td>

<td>SATA2</td>

<td>1500</td>

<td>4.13</td>

<td>96</td>

</tr>

<tr>

<td>Western Digital</td>

<td>WD20EARS</td>

<td>5900</td>

<td>SATA2</td>

<td>2000</td>

<td>5.91</td>

<td>94</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Benchmarking/Disk_wipes&oldid=412497](https://wiki.archlinux.org/index.php?title=Benchmarking/Disk_wipes&oldid=412497)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")
*   [Hardware](/index.php/Category:Hardware "Category:Hardware")
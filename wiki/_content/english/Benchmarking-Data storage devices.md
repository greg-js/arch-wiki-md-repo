This article covers several Linux-native apps that benchmark I/O devices such as HDDs, SSDs, USB thumb drives, etc. There is also a "database" section specific to SSDs meant to capture user-entered benchmark results.

## Contents

*   [1 Overview](#Overview)
*   [2 Using hdparm](#Using_hdparm)
*   [3 Using gnome-disks](#Using_gnome-disks)
*   [4 Using systemd-analyze](#Using_systemd-analyze)
*   [5 Using dd](#Using_dd)
*   [6 Using dcfldd](#Using_dcfldd)

## Overview

Several I/O benchmark options exist under Linux.

*   Using hdparm with the -Tt switch, one can time sequential reads. This method is **independent** of partition alignment!
*   There is a graphical benchmark called gnome-disks contained in the [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility) package that will give min/max/ave reads along with ave access time and a nice graphical display. This method is **independent** of partition alignment!
*   The dd utility can be used to measure both reads and writes. This method is **dependent** on partition alignment! In other words, if you failed to properly align your partitions, this fact will be seen here since you are writing and reading to a mounted filesystem.
*   [Bonnie++](/index.php/Benchmarking#Bonnie.2B.2B "Benchmarking") (**caution**: by default, bonnie++ write at least twice the RAM size on disk. If you want to preserve your SSD, use non default option)

## Using hdparm

```
# hdparm -Tt /dev/sdX
/dev/sdX:
Timing cached reads:   x MB in  y seconds = z MB/sec
Timing buffered disk reads:  x MB in  y seconds = z MB/sec

```

**Note:** One should run the above command 4-5 times and manually average the results for an accurate evaluation of read speed per the hdparm man page.

## Using gnome-disks

```
# gnome-disks

```

Users will need to navigate through the GUI to the benchmark button ("More actions..." => "Benchmark Volume..."). [Example](http://imgur.com/Ayv1B)

## Using systemd-analyze

```
systemd-analyze plot > boot.svg

```

Will plot a detailed graphic with the boot sequence: kernel time, userspace time, time taken by each service. [Example](http://imgur.com/4ywt1)

## Using dd

**Note:** This method requires the command to be executed from a mounted partition on the device of interest!

First, enter a directory on the SSD with at least 1.1 GB of free space (and one that obviously gives your user wrx permissions) and write a test file to measure write speeds and to give the device something to read:

```
$ cd /path/to/SSD
$ dd if=/dev/zero of=tempfile bs=1M count=1024 conv=fdatasync,notrunc
1024+0 records in
1024+0 records out
w bytes (x GB) copied, y s, z MB/s

```

**Tip:** See [dd-benchmark](https://romanrm.net/dd-benchmark) for an explanation on the requirement to `sync` and further related `dd` options.

Next, clear the buffer-cache to accurately measure read speeds directly from the device:

```
# echo 3 > /proc/sys/vm/drop_caches
$ dd if=tempfile of=/dev/null bs=1M count=1024
1024+0 records in
1024+0 records out
w bytes (x GB) copied, y s, z MB/s

```

Now that the last file is in the buffer, repeat the command to see the speed of the buffer-cache:

```
$ dd if=tempfile of=/dev/null bs=1M count=1024
1024+0 records in
1024+0 records out
w bytes (x GB) copied, y s, z GB/s

```

**Note:** One should run the above command 4-5 times and manually average the results for an accurate evaluation of the buffer read speed.

Finally, delete the temp file

```
$ rm tempfile

```

**Note:** Some SSD controllers have compression hardware, which may skew benchmark results. See [http://www.pugetsystems.com/labs/articles/SSDs-Advertised-vs-Actual-Performance-179/](http://www.pugetsystems.com/labs/articles/SSDs-Advertised-vs-Actual-Performance-179/)

See also [Core utilities#dd](/index.php/Core_utilities#dd "Core utilities").

## Using dcfldd

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
Related articles

*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Sysstat](/index.php/Sysstat "Sysstat")

所谓基准测试，就是通过一个统一的流程来测试性能，并将其结果和其它系统测到的结果或一个被广泛接受的标准相比较的行为。这种计算系统性能的统一流程可以帮助解答一些问题，比如：

*   系统是否发挥正常？
*   应该用哪个版本的驱动以达到最佳性能？
*   系统是否能够胜任某任务？

许多工具可以测试系统性能，下面列出可用的工具。

## Contents

*   [1 独立工具](#.E7.8B.AC.E7.AB.8B.E5.B7.A5.E5.85.B7)
    *   [1.1 glxgears](#glxgears)
    *   [1.2 UnixBench](#UnixBench)
    *   [1.3 interbench](#interbench)
    *   [1.4 ttcp](#ttcp)
    *   [1.5 iperf](#iperf)
    *   [1.6 time](#time)
    *   [1.7 hdparm](#hdparm)
    *   [1.8 Unigine 引擎](#Unigine_.E5.BC.95.E6.93.8E)
    *   [1.9 gnome-disks](#gnome-disks)
    *   [1.10 systemd-analyze](#systemd-analyze)
    *   [1.11 dd](#dd)
    *   [1.12 dcfldd](#dcfldd)
*   [2 软件集](#.E8.BD.AF.E4.BB.B6.E9.9B.86)
    *   [2.1 Bonnie++](#Bonnie.2B.2B)
    *   [2.2 IOzone](#IOzone)
    *   [2.3 HardInfo](#HardInfo)
    *   [2.4 Phoronix测试集](#Phoronix.E6.B5.8B.E8.AF.95.E9.9B.86)
    *   [2.5 S](#S)
*   [3 闪存介质](#.E9.97.AA.E5.AD.98.E4.BB.8B.E8.B4.A8)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 独立工具

### glxgears

glxgears是流行的OpenGL测试，渲染非常简单的齿轮，输出帧率。尽管glxgears可以测试显卡驱动直接渲染能力，但是它已经过时，不能代表GNU/Linux图形显示的现状以及OpenGL的全部能力。glxgears仅测试了一小部分OpenGL功能。在glxgears中体现的性能提升在游戏中并不能感受到。更多信息请看[这里](http://wiki.cchtml.com/index.php/Glxgears_is_not_a_Benchmark)。

可以通过[mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) 安装 64 位版本，通过 [Multilib](/index.php/Multilib "Multilib") 中的 [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos)安装 32 位版本。

### UnixBench

unixbench [unixbench](https://aur.archlinux.org/packages/unixbench/)中。 在终端中运行*ubench*跑评测。

请看：

*   [https://github.com/kdlucas/byte-unixbench](https://github.com/kdlucas/byte-unixbench)
*   [https://github.com/kdlucas/byte-unixbench/blob/master/UnixBench/USAGE](https://github.com/kdlucas/byte-unixbench/blob/master/UnixBench/USAGE)

### interbench

[interbench](https://aur.archlinux.org/packages/interbench/) 可以评测 Linux 的交互性。测试 Linux 内核设计或系统配置改变后的效果，例如 CPU、I/O调度、文件系统，以及参数的改变。使用仔细的评测，可以比较不同的硬件。

请看：

*   [Realtime process management](/index.php/Realtime_process_management "Realtime process management")
*   [Advanced traffic control](/index.php/Advanced_traffic_control "Advanced traffic control")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [Linux-pf](/index.php/Linux-pf "Linux-pf")

### ttcp

ttcp (Test TCP)测试任意网络连接的P2P带宽。需要在（被测试带宽的）网络两端都安装该程序。

可以在[AUR](/index.php/AUR "AUR")找到不同版本的ttcp。

*   [ttcp](https://aur.archlinux.org/packages/ttcp/)
*   [nuttcp](https://aur.archlinux.org/packages/nuttcp/)

### iperf

iperf是简单的P2P带宽测试工具，可以用于TCP或UDP。它的输出格式非常好，并发测试模式。

可以安装[iperf](https://www.archlinux.org/packages/?name=iperf)，或不同版本的[iperf3](https://www.archlinux.org/packages/?name=iperf3)。

### time

time统计调用某个命令到结束所花的时间。在大多数Linux系统上都有time。

```
$ time tar -zxvf archive.tar.gz

```

### hdparm

可以用[hdparm](/index.php/Hdparm "Hdparm")([hdparm](https://www.archlinux.org/packages/?name=hdparm))测试存储介质。Using hdparm with the -Tt switch, one can time sequential reads. This method is independent of partition alignment!

```
# hdparm -Tt /dev/sdX
/dev/sdX:
Timing cached reads:   x MB in  y seconds = z MB/sec
Timing buffered disk reads:  x MB in  y seconds = z MB/sec

```

**Note:** 一次测试需要执行上述命令2-3次并手动计算平均值以便评估read speed per the hdparm man page.

### Unigine 引擎

[Unigine公司](http://www.unigine.com/)基于他们的图形引擎制造了多个现代的OpenGL评测，特性如下：

*   像素动态照明
*   普通和视差映射
*   64位HDR渲染
*   容积雾和光
*   强大的粒子系统：火焰、烟、爆炸
*   可扩展着色（GLSL/HLSL）
*   后期处理：景深、折射、辉光、模糊、色彩校正等。

那些想超频系统的目前在使用Unigine评测。Unigine天堂被用来测试超频的初始稳定性。

可以在[AUR](/index.php/AUR "AUR")找到这些评测（看下面的链接）。

请看：

*   [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/)
*   [unigine-tropics](https://aur.archlinux.org/packages/unigine-tropics/)
*   [unigine-sanctuary](https://aur.archlinux.org/packages/unigine-sanctuary/)
*   [unigine-valley](https://aur.archlinux.org/packages/unigine-valley/)
*   [unigine-superposition](https://aur.archlinux.org/packages/unigine-superposition/)

### gnome-disks

There is a graphical benchmark called gnome-disks contained in the gnome-disk-utility package that will give min/max/ave reads along with average access time and a nice graphical display. This method is independent of partition alignment!

```
# gnome-disks

```

Users will need to navigate through the GUI to the benchmark button ("More actions..." => "Benchmark Volume..."). [Example](http://imgur.com/Ayv1B)

### systemd-analyze

```
systemd-analyze plot > boot.svg

```

上述命令会吧启动顺序画一个详细的图，包括：kernel用的时间，用户态时间，每个服务的时间。 [Example](http://imgur.com/4ywt1)

### dd

The dd utility can be used to measure both reads and writes. This method is dependent on partition alignment! In other words, if you failed to properly align your partitions, this fact will be seen here since you are writing and reading to a mounted filesystem.

**Note:** This method requires the command to be executed from a mounted partition on the device of interest!

First, enter a directory on the SSD with at least 1.1 GB of free space (and one that obviously gives your user wrx permissions) and write a test file to measure write speeds and to give the device something to read:

```
$ cd /path/to/SSD
$ dd if=/dev/zero of=tempfile bs=1M count=1024 conv=fdatasync,notrunc status=progress
1024+0 records in
1024+0 records out
w bytes (x GB) copied, y s, z MB/s

```

**Tip:** See [dd-benchmark](https://romanrm.net/dd-benchmark) for an explanation on the requirement to `sync` and further related `dd` options.

Next, clear the buffer-cache to accurately measure read speeds directly from the device:

```
# echo 3 > /proc/sys/vm/drop_caches
$ dd if=tempfile of=/dev/null bs=1M count=1024 status=progress
1024+0 records in
1024+0 records out
w bytes (x GB) copied, y s, z MB/s

```

Now that the last file is in the buffer, repeat the command to see the speed of the buffer-cache:

```
$ dd if=tempfile of=/dev/null bs=1M count=1024 status=progress
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

### dcfldd

Dcfldd doesn't print the average speed in MB/s like good old dd does but with [time](#time) you can work around that.

Time the run clearing the disk:

```
# time dcfldd if=/dev/zero of=/dev/sdX bs=4M
18944 blocks (75776Mb) written.dcfldd:: No space left of device
real     16m17.033s
user     0m0.377s
sys      0m51.160s

```

Calculate MB/s by dividing the output of the dcfldd command by the time in seconds. For this example: 75776Mb / (16.4 min * 60) = 77.0 MB/s.

## 软件集

### Bonnie++

[bonnie++](https://www.archlinux.org/packages/?name=bonnie%2B%2B)用C++重写了[原Bonnie](http://www.textuality.com/bonnie/)评测集，主要测试硬盘和文件系统性能。

**Warning:** By default, bonnie++ write at least twice the RAM size on disk. If you want to preserve your SSD, use non default option.

**Note:** 原Bonnie集不是以GPL或其他兼容许可证发布。

请看：

*   [作者的网站](http://www.coker.com.au/bonnie++/)
*   [Wikipedia:Bonnie++](https://en.wikipedia.org/wiki/Bonnie%2B%2B "wikipedia:Bonnie++")

### IOzone

IOzone用来测试文件系统性能。

[AUR](/index.php/AUR "AUR"): [iozone](https://aur.archlinux.org/packages/iozone/)可以安装该程序。

看看论坛帖子：[iozone评估I/O调度... 结果并不是您期望的！](https://bbs.archlinux.org/viewtopic.php?pid=969463)。

### HardInfo

[hardinfo](https://www.archlinux.org/packages/?name=hardinfo)可以收集系统硬件和操作系统信息，性能评测，生成HTML或纯文本格式的可打印的报表。hardinfo评测CPU和FPU，有清爽的Gtk界面。

请看[作者网站](http://wiki.hardinfo.org/HomePage)。

### Phoronix测试集

*[Phoronix测试集](http://www.phoronix-test-suite.com/)是最全面测试和评测平台，提供可扩展的框架，添加新的测试很方便。该软件可以有效地完成定性和定量评测，用起来很清爽、可复用、很简单。*

*Phoronix测试集基于广泛的测试，内部工具从2004年起由Phoronix.com开发，获得一线硬件和软件公司的支持。该软件开源采用GPLv3。*

*原先开发用于Linux自动化测试，后来加入了OpenSolaris、苹果 macOS、微软 Windows 和 BSD 操作系统。Phoronix 测试集由轻量的处理核心（pts-core）组成，每个评测由基于XML的总述、相关的资源脚本组成。从安装评测，到实际评测、到解析重要硬件和软件组件，都是全自动化的，完全可复用的，仅询问用户是否执行操作。*

*Phoronix测试集使用OpenBenchmarking.org接口用于存储测试结果，分享测试总述和结果，高级的分析特性，以及其他功能。Phoromatic是在多系统编排测试执行的企业组件，具有远程管理的功能。*

可以[安装](/index.php/Pacman "Pacman")[phoronix-test-suite](https://aur.archlinux.org/packages/phoronix-test-suite/)包。还有开发版[phoronix-test-suite-git](https://aur.archlinux.org/packages/phoronix-test-suite-git/)。

### S

[S](https://github.com/Algodev-github/S), an I/O Benchmark Suite, is a small collection of scripts to measure storage I/O performance.

It has been developed by [algodev](http://algogroup.unimore.it/algodev/), the team behind the BFQ scheduler.

Download or clone the project, install its dependencies and run it as root (privileges needed to change disk scheduler).

## 闪存介质

[iozone](https://aur.archlinux.org/packages/iozone/)可以定量测试性能特点。*连续的*读和写，常被用来做I/O压力测试，例如解压缩，以及系统更新写大量文件。相关指标是小文件*随机写*的速度。

该示例调用测试使用4K记录大小操作10M文件：

```
$ iozone -e -I -a -s 10M -r 4k -i 0 -i 1 -i 2
...

                                                                random   random
              kB  reclen    write  rewrite    read    reread    read     write
           10240       4      661      649     5802     5822     3892      624

```

**Note:**

*   单位是KB/s。
*   SD卡和其他闪存介质的性能图表[Tom's Hardware](http://www.tomshardware.com/charts/memory-cards,39.html)。

## 参阅

*   [Linux评测主页](http://lbs.sourceforge.net/)
*   [Phoronix.com](http://www.phoronix.com/)
*   [Interbench主页](http://users.on.net/~ckolivas/interbench/)
*   [Unigine.com](http://unigine.com/download/)
*   [普华开源社区评测](https://isoft-linux.org)
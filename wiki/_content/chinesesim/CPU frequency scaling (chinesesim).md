**翻译状态：** 本文是英文页面 [CPU_Frequency_Scaling](/index.php/CPU_Frequency_Scaling "CPU Frequency Scaling") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-04-14，点击[这里](https://wiki.archlinux.org/index.php?title=CPU_Frequency_Scaling&diff=0&oldid=362979)可以查看翻译后英文页面的改动。

[CPUfreq](http://www.kernel.org/pub/linux/utils/kernel/cpufreq/cpufreq.html) 引用了内核架构中的 CPU 频率调整部分相关功能。这项技术使得操作系统能够提高或降低CPU速度来达到省电目的。CPU 频率可以根据系统负荷自动调整，或响应 ACPI 事件而调整，或通过用户空间程序手工调整。

从 3.4 内核开始，必要的模块都会自动加载，而且推荐的调速器 [ondemand governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling") 默认启动。但是，用户空间程序，例如 [cpupower](#cpupower)，[acpid](/index.php/Acpid "Acpid")，[laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools")，或你的桌面系统对应的图形化工具，在进行高级特性配置时可能仍然需要被用到。

## Contents

*   [1 用户空间工具](#.E7.94.A8.E6.88.B7.E7.A9.BA.E9.97.B4.E5.B7.A5.E5.85.B7)
    *   [1.1 thermald](#thermald)
    *   [1.2 i7z](#i7z)
    *   [1.3 cpupower](#cpupower)
*   [2 CPU frequency driver](#CPU_frequency_driver)
    *   [2.1 设置最大和最小频率](#.E8.AE.BE.E7.BD.AE.E6.9C.80.E5.A4.A7.E5.92.8C.E6.9C.80.E5.B0.8F.E9.A2.91.E7.8E.87)
*   [3 调整调速器](#.E8.B0.83.E6.95.B4.E8.B0.83.E9.80.9F.E5.99.A8)
    *   [3.1 调节 ondemand 调速器](#.E8.B0.83.E8.8A.82_ondemand_.E8.B0.83.E9.80.9F.E5.99.A8)
        *   [3.1.1 开关阙值](#.E5.BC.80.E5.85.B3.E9.98.99.E5.80.BC)
        *   [3.1.2 采样率](#.E9.87.87.E6.A0.B7.E7.8E.87)
*   [4 与ACPI事件交互](#.E4.B8.8EACPI.E4.BA.8B.E4.BB.B6.E4.BA.A4.E4.BA.92)
*   [5 GNOME下的授权](#GNOME.E4.B8.8B.E7.9A.84.E6.8E.88.E6.9D.83)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 BIOS频率限制](#BIOS.E9.A2.91.E7.8E.87.E9.99.90.E5.88.B6)
*   [7 See also](#See_also)

## 用户空间工具

### thermald

[thermald](https://aur.archlinux.org/packages/thermald/) 是一个 Linux 守护进程，它可以防止平台过热。此进程监控平台的温度，且使用可用的办法帮助温度的降低。

By default, it monitors CPU temperature using available CPU digital temperature sensors and maintains CPU temperature under control, before HW takes aggressive correction action. If there is a skin temperature sensor in thermal sysfs, then it tries to keep skin temperature under 45C.

默认情况下，它在硬件采取激进的行为之前，利用现有的 CPU 数字温度传感器监控 CPU 温度，并保持 CPU 的温度处于可控范围。如果 sysfs 中存在表面温度传感器，那么它将让表面温度保持在 45℃ 以下。

### i7z

[i7z](https://www.archlinux.org/packages/?name=i7z) 是 Linux 下极其好用的针对 i7 CPU 的报告工具（也同样适用于 i3 和 i5 CPU）。您可以在终端下输入 `i7z` 或者使用图形化工具 `i7z-gui` 来运行它。

**注意:** [i7z](https://www.archlinux.org/packages/?name=i7z)-0.27.2 在 2012 年 9月已经释出。这里推荐安装 [i7z-git](https://aur.archlinux.org/packages/i7z-git/)，以适应更多的硬件类型。

### cpupower

[cpupower](https://www.archlinux.org/packages/?name=cpupower) is a set of userspace utilities designed to assist with CPU frequency scaling. The package is not required to use scaling, but is highly recommended because it provides useful command-line utilities and a [systemd](/index.php/Systemd "Systemd") service to change the governor at boot.

The configuration file for *cpupower* is located in `/etc/default/cpupower`. This configuration file is read by a bash script in `/usr/lib/systemd/scripts/cpupower` which is activated by *systemd* with `cpupower.service`. You may want to enable `cpupower.service` to start at boot.

[cpupower](https://www.archlinux.org/packages/?name=cpupower) 是一组为辅助 *CPU frequency scaling* 而设计的用户空间工具。这个软件包并不是必须的，但强烈建议安装，因为它提供了方便的命令行工具，且提供在启动时改变调速器的服务。

[cpupower](https://www.archlinux.org/packages/?name=cpupower) 的配置文件位于 `/etc/default/cpupower`。这个配置文件被bash脚本读取，该脚本位于 `/usr/lib/systemd/scripts/cpupower`，它又由 `systemd` 通过 `cpupower.service` 激活。为使用 [systemd](https://www.archlinux.org/packages/?name=systemd) 在启动时启用 [cpupower](https://www.archlinux.org/packages/?name=cpupower)，运行：

```
# systemctl enable cpupower.service

```

## CPU frequency driver

**注意:**

*   从 kernel 3.4 开始，原生的 CPU 模块将会自动加载。
*   从 kernel 3.9 开始，名为 `pstate` 的新的功率驱动程序将会在以下的驱动程序之前自动为现代的 Intel CPU 启用。该驱动会优先于其他的驱动程序，因为它是内置驱动，而不是作为一个模块来加载。该驱动自动作用于 Sandy Bridge 和 Ivy Bridge 这两个类型的 CPU。如果您在使用这个驱动的时候遇到问题，建议您在 Grub 的内核参数中对其禁用（即修改 /etc/default/grub 文件，在 GRUB_CMDLINE_LINUX_DEFAULT= 后添加 intel_pstate=disable）。
*   实际上，P 状态的状态功能可以通过 `/sys/devices/system/cpu/intel_pstate` 进行更改。例如：通过 `# echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo` 可以关闭 Intel Turbo Boost 来降低 CPU 的温度。
*   对于现代的 Intel CPU，[Linux Thermal Daemon](https://01.org/linux-thermal-daemon) 也提供了一些其他的控制方法（例如，AUR 中的 [thermald](https://aur.archlinux.org/packages/thermald/)），它们能够更加激进的用 P-states，T-states 或 Intel power clamp driver 对系统温度进行抑制。thermald 也可用于老式的 Intel CPUs。如果最新的驱动不可用，守护进程将会恢复到 x86 model specific registers 而用 Linux ‘cpufreq subsystem’ 来抱持系统的清凉。

*cpupower* 需要模块才能知道本地的 CPU 限制信息：

| 模块 | 描述 |
| intel_pstate | This driver implements a scaling driver with an internal governor for Intel Core (SandyBridge and newer) processors. |
| acpi-cpufreq | CPUFreq driver which utilizes the ACPI Processor Performance States. This driver also supports Intel Enhanced SpeedStep (previously supported by the deprecated speedstep-centrino module).支持ACPI Processor Performance States的CPUFreq驱动。该驱动也支持Intel Enhanced SpeedStep（之前由已过期的模块speedstep-centrino支持）。 |
| speedstep-lib | CPUFreq drive for Intel speedstep enabled processors (mostly atoms and older pentiums (< 3)) 支持拥有speedstep功能的Intel处理器（通常是atom和奔腾3代或更老的处理器）CPUFreq驱动。 |
| powernow-k8 | CPUFreq driver for K8/K10 Athlon64/Opteron/Phenom processors. **Deprecated since linux 3.7 - Use acpi_cpufreq.**支持K8/K10 Athlon64/Opteron/Phenom处理器的CPUFreq驱动。**从linux 3.7开始进入淘汰阶段，使用acpi-cpufreq替代。** |
| pcc-cpufreq | This driver supports Processor Clocking Control interface by Hewlett-Packard and Microsoft Corporation which is useful on some Proliant servers.支持HP和微软提出的“处理器时钟频率控制”接口，这在一些Proliant服务器上很有用。 |
| p4-clockmod | CPUFreq driver for Intel Pentium 4 / Xeon / Celeron processors. When enabled it will lower CPU temperature by skipping clocks.
You probably want to use a Speedstep driver instead.支持Intel奔腾4 / 至强 / 赛扬 处理器的CPUFreq驱动。生效时会通过skipping clocks技术降低CPU发热量。
你可能更希望使用Speedstep驱动代替它。 |

查看所有可用的模块，运行以下命令：

```
$ ls /usr/lib/modules/$(uname -r)/kernel/drivers/cpufreq/

```

加载合适的模块 (see [Kernel modules](/index.php/Kernel_modules "Kernel modules") for details)。一旦合适的 cpufreq 驱动模块被加载成功，就可以通过以下命令查询到 CPU 的信息：

```
$ cpupower frequency-info

```

### 设置最大和最小频率

在罕见的情况下，可能有必要手动设置最大和最小频率。

运行以下命令设置最大时钟频率（*clock_freq* 为时钟频率，单位为：GHz, MHz）：

```
# cpupower frequency-set -u *clock_freq*

```

运行以下命令设置最小时钟频率：

```
# cpupower frequency-set -d *clock_freq*

```

运行以下命令设置运行于指定频率：

```
# cpupower frequency-set -f *clock_freq*

```

**注意:**

*   仅设置某一核心，添加参数 `-c *core_number*`。
*   The governor，频率的最大值和最小值可以在 `/etc/default/cpupower` 中设置。

## 调整调速器

调速器（见下表）是预设的 CPU 电源方案。在同一时刻只会有一个会调速器被激活。可以查询内核源码的 [内核文档](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) 得到更多的相关信息。

| 调速器 | 描述 |
| ondemand | 按需快速动态调整CPU频率， 一有cpu计算量的任务，就会立即达到最大频率运行，等执行完毕就立即回到最低频率（阙值为 95%） |
| performance | 运行于最大频率 |
| conservative | 按需快速动态调整CPU频率， 一有cpu计算量的任务，就会立即达到最大频率运行，等执行完毕就立即回到最低频率（阙值为 75%） |
| powersave | 运行于最小频率 |
| userspace | 运行于用户指定的频率 |

根据实际硬件，以下的调速器可能被默认启用：

*   `ondemand` ：AMD 及旧款 Intel CPU。
*   `powersave` ：Intel Sandy Bridge 和更新的CPU。

如果需要指定特定的调速器，运行以下命令：

```
# cpupower frequency-set -g *governor*

```

**注意:**

*   仅设置某一核心，请在命令的最后跟随以下参数 `-c *core_number*`。
*   激活某一调速器，需要特定的 [内核模块](/index.php/Kernel_modules "Kernel modules") （名为 `cpufreq_*governor*`）正确载入。在 3.4 内核上，这些模块应该已经自动加载。

也可以这样实现：

```
# echo *governor* | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor >/dev/null

```

**Tip:** 如果需要实时监测 CPU 的频率，运行以下命令：
```
$ watch grep \"cpu MHz\" /proc/cpuinfo

```

### 调节 ondemand 调速器

查看 [kernel documentation](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) 获得更多信息。

#### 开关阙值

设置到其他值（增加）的步长，执行以下命令：

```
# echo -n *percent* > /sys/devices/system/cpu/cpufreq/<governor>/up_threshold

```

设置到其他值（减小）的步长，执行以下命令：

```
# echo -n *percent* > /sys/devices/system/cpu/cpufreq/<governor>/down_threshold

```

#### 采样率

采样率决定调速器多久进行一次检查并调整CPU频率。 设置`sampling_down_factor`大于1将通过降低负载评估的消耗，并将CPU保持在最高运行频率而提高性能。这个可调参数对低CPU频率/负载没有效果。

要获取这个值 (default = 1)，运行：

```
$ cat /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

要设置这个值，运行：

```
# echo -n <value> > /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

## 与ACPI事件交互

用户可以把调速器配置为基于不同的ACPI事件自动切换的形式。例如接入外接电源，或是合上屏幕时。以下是一个简明的例子，但可能有必须通读一遍文章[acpid](/index.php/Acpid "Acpid").

事件是在`/etc/acpi/handler.sh`中定义的。如果[acpid](https://www.archlinux.org/packages/?name=acpid)软件包已经安装，这个文件应该已经存在并且设置为可执行。例如，当外接电源拔除时将调速器从`performance`改为`conservative`，而当电源再次接入时将它改回来：

```
/etc/acpi/handler.sh

```

```
[...]

 ac_adapter)
     case "$2" in
         AC*)
             case "$4" in
                 00000000)
                     echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor    
                     echo -n $minspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode start
                 ;;
                 00000001)
                     echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                     echo -n $maxspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode stop
                 ;;
             esac
         ;;
         *) logger "ACPI action undefined: $2" ;;
     esac
 ;;

[...]

```

## GNOME下的授权

**注意:** systemd引入了logind来处理consolekit和policykit行为。以下代码不再工作。

[GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")有一个不错的小工具来在线修改调速器。如果想在不需要root密码的情况下就能使用它，只需要建立一个文件`/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla`然后录入以下内容：

```
[org.gnome.cpufreqselector]
Identity=unix-user:USER
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

其中`USER`替换为期望的用户名。

[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中的软件包[desktop-privileges](https://aur.archlinux.org/packages/desktop-privileges/)包含一个类似的`.pkla`文件为所有`power` [用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")中的用户授权修改调速器。

## 疑难解答

*   一些应用程序，如[ntop](/index.php/Ntop "Ntop")，对自动频率调整不能很好地响应。在ntop的案例中它可能导致分段错误和大量信息丢失，因为在大量网络数据包突然到达被监控的网络接口时，`on-demand`调速器不能迅速反应，以致当前处理速度满足不了处理这些数据包所需的速度。

*   一些CPU在默认的`on-demand`调速器配置下可能受到比较严重的性能损失（例如flash视频不能平滑地播放，或窗口动画停顿）。为了解决这些问题，完全禁用掉频率调整不如采取更积极的措施——降低每个CPU的*up_threshold* [sysctl](/index.php/Sysctl "Sysctl")变量值。阅读[#修改on-demand调速器的阈值](#.E4.BF.AE.E6.94.B9on-demand.E8.B0.83.E9.80.9F.E5.99.A8.E7.9A.84.E9.98.88.E5.80.BC)章节以获得更多信息。

*   有时on-demand调速器可能达不到最高频率而只能达到次级频率。这个问题可以通过把max_freq值设置得稍微高于最大频率的方式来解决。例如，如果CPU的频率范围是2.00 GHz到3.00 GHz，把max_freq设置为3.01 GHz就是一个不错的主意。

*   [ALSA](/index.php/ALSA "ALSA")驱动和有些声音芯片配合工作时，可能导致在调速器改变频率时声音跳跃。改回non-changing调速器应该能够解决这个问题。

### BIOS频率限制

一些CPU/BIOS配置可能导致达不到最高频率或根本无法调高频率。这很可能是因为BIOS告诉操作系统限制频率，结果在`/sys/devices/system/cpu/cpu0/cpufreq/bios_limit`中设置了一个过低的值。

这种情况下需要在BIOS设置中修改指定的配置（频率，发热管理等）。这通常是由于有问题的/过旧的BIOS导致，也可能BIOS有特别的原因要求必须这样。

可能的原因有（假设你的机器是一台笔记本）电池被移除（或快要完全损坏），所以你只能用外接电源。这种情况下如果电源适配器提供的电能太弱，就会满足不了整个系统在峰值所需的电能，而且又没有电池辅助供电，就可能导致数据丢失，数据损坏或最坏的情况下损坏硬件！

不是所有的BIOS都会在这种情况下限制CPU频率，但如IBM/联想 Thinkpad就会。参考thinkwiki以获取更多信息[thinkpad related info on this topic](http://www.thinkwiki.org/wiki/Problem_with_CPU_frequency_scaling).

如果你检查后发现并没有不正确的BIOS设置，而且你也十分清楚自己在做什么以及可能导致的结果，你还可以选择让内核忽略BIOS限制。

**警告:** 请确保你读了并且完全明白上面一节内容。CPU频率限制是你BIOS的一个安全特性，通常情况下你不应该越过它。

一个特殊的参数需要传递给处理器模块。

临时尝试这办法时可以修改`/sys/module/processor/parameters/ignore_ppc`值从`0`到`1`。

要固化这个修改请参考[Kernel modules](/index.php/Kernel_modules#Configuration "Kernel modules")或继续阅读本文。 添加`processor.ignore_ppc=1`到内核启动参数或创建

 `/etc/modprobe.d/ignore_ppc.conf` 
```
# 如果你的机器受到错误的BIOS频率限制，这应该会有帮助
options processor ignore_ppc=1
```

## See also

*   [Linux CPUFreq - kernel documentation](https://www.kernel.org/doc/Documentation/cpu-freq/index.txt)
*   [Comprehensive explanation of pstate](http://www.reddit.com/r/linux/comments/1hdogn/acpi_cpufreq_or_intel_pstates/)
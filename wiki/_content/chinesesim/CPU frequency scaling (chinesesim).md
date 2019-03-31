**翻译状态：** 本文是英文页面 [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-07，点击[这里](https://wiki.archlinux.org/index.php?title=CPU+frequency+scaling&diff=0&oldid=436397)可以查看翻译后英文页面的改动。

相关文章

*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [PHC](/index.php/PHC "PHC")

CPU 调频允许操作系统通过提高或降低 CPU 频率来达到省电目的。CPU 频率可以根据系统负载或响应 ACPI 事件来自动调整，也可通过用户空间程序手工调整。

Linux 内核具有 CPU 调频实现，该基础架构称为 *cpufreq*。从 3.4 内核开始，必要的模块都会自动加载，而且推荐的调频器 [ondemand governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling") 默认启用。但是，在进行高级配置时，仍然会用到其他用户空间工具，例如 [cpupower](#cpupower)，[acpid](/index.php/Acpid "Acpid")，[laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools")，或桌面环境所提供的图形化工具。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 用户空间工具](#用户空间工具)
    *   [1.1 thermald](#thermald)
    *   [1.2 i7z](#i7z)
    *   [1.3 cpupower](#cpupower)
*   [2 CPU 频率驱动程序](#CPU_频率驱动程序)
    *   [2.1 设置最大和最小频率](#设置最大和最小频率)
*   [3 调整调速器](#调整调速器)
    *   [3.1 调节 ondemand 调速器](#调节_ondemand_调速器)
        *   [3.1.1 开关阙值](#开关阙值)
        *   [3.1.2 采样率](#采样率)
        *   [3.1.3 保存设置](#保存设置)
*   [4 与ACPI事件交互](#与ACPI事件交互)
*   [5 GNOME下的授权](#GNOME下的授权)
*   [6 疑难解答](#疑难解答)
    *   [6.1 BIOS频率限制](#BIOS频率限制)
*   [7 参阅](#参阅)

## 用户空间工具

### thermald

[thermald](https://aur.archlinux.org/packages/thermald/) 是一个 Linux 守护进程，用于防止平台过热。此守护进程会监控平台温度，并采用可用的冷却方式来降低温度。

默认情况下，在硬件采取激进的降温措施之前，它将利用现有的 CPU 数字温度传感器监控 CPU 温度，并保持 CPU 的温度处于可控范围。如果 sysfs 中存在表面温度传感器，那么它将让表面温度保持在 45℃ 以下。

### i7z

[i7z](https://www.archlinux.org/packages/?name=i7z) 是 i7 CPU （也同样适用于 i3 和 i5 CPU）的报告工具。可以在终端下输入 `i7z` 或者使用图形化工具 `i7z-gui` 来运行该工具。

### cpupower

[cpupower](https://www.archlinux.org/packages/?name=cpupower) 是一组为辅助 CPU 调频而设计的用户空间工具。该软件包并非必须，但强烈建议安装，因为它提供了方便的命令行实用程序，并且内置 [systemd](/index.php/Systemd "Systemd") 服务，可在启动时更改调频器。

*cpupower* 的配置文件位于 `/etc/default/cpupower`。此配置文件由 `/usr/lib/systemd/scripts/cpupower` 中的 bash 脚本读取，而该脚本由 *systemd* 通过 `cpupower.service` 激活。若要在启动时启用 *cpupower*，请执行：

```
# systemctl enable cpupower.service

```

## CPU 频率驱动程序

**注意:**

*   原生 CPU 模块将会自动加载。
*   对于现代 Intel CPU，将使用 `pstate` 功率驱动程序，而非下列其他驱动程序。此驱动程序的优先级高于其他驱动程序，并编入内核（而非编译为模块）。此驱动程序将自动用于 Sandy Bridge（以及更新的 CPU）。如果在使用这个驱动的时候遇到问题，建议您在 Grub 的内核参数中将其禁用（即修改 /etc/default/grub 文件，在 GRUB_CMDLINE_LINUX_DEFAULT= 后添加 `intel_pstate=disable`）。您可以使用与此驱动程序配套的用户空间工具，但这些工具**不受您的控制**。
*   尽管上述 P State 行为会受到 `/sys/devices/system/cpu/intel_pstate` 影响，例如：可以通过 `# echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo` 关闭 Intel 睿频加速，从而降低 CPU 的温度。
*   对于现代 Intel CPU，[Linux Thermal Daemon](https://01.org/linux-thermal-daemon) 也提供了一些其他的控制方法（例如 [thermald](https://aur.archlinux.org/packages/thermald/)），它们可以通过 P-state、T-state 或 Intel 节能驱动程序来主动控制系统温度。thermald 也适用于较老的 Intel CPU。如果最新版本的驱动程序不可用，那么守护进程会还原为 x86 MSR (Model Specific Register)，由 Linux“cpufreq 子系统”来控制系统冷却。

*cpupower* 需要相应模块来了解本地 CPU 的限制信息：

| 模块 | 描述 |
| intel_pstate | 此驱动程序通过内置调频器，实现面向 Intel Core（SandyBridge 和更新的型号）处理器的调频驱动。 |
| acpi-cpufreq | 此 CPUFreq 驱动程序可充分利用 ACPI Processor Performance States。此驱动程序也支持 Intel Enhanced SpeedStep（之前由 speedstep-centrino 模块（已废弃）提供支持）。 |
| speedstep-lib | 此 CPUFreq 驱动程序面向支持 Intel SpeedStep 的 CPU（主要包括 Atom 和早于 Pentinum 3 的 CPU）。 |
| powernow-k8 | 面向 K8/K10 Athlon 64/Opteron/Phenom 的 CPUFreq 驱动程序。从 Linux 3.7 开始，对于此系列中的较现代 CPU，将自动使用“acpi-cpufreq”。 |
| pcc-cpufreq | 此驱动程序支持 HP 和 Microsoft 提出的 Processor Clocking Control 接口，在某些 ProLiant 服务器上比较有用。 |
| p4-clockmod | 面向 Intel Pentium 4/Xeon/Celeron 处理器的 CPUFreq 驱动程序，可通过跳频来降低 CPU 温度。（您最好使用 SpeedStep 驱动程序。） |

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
| performance | 运行于最大频率 |
| powersave | 运行于最小频率 |
| userspace | 运行于用户指定的频率 |
| ondemand | 按需快速动态调整CPU频率， 一有cpu计算量的任务，就会立即达到最大频率运行，空闲时间增加就降低频率 |
| conservative | 按需快速动态调整CPU频率， 比 ondemand 的调整更保守 |
| schedutil | 基于调度程序调整 CPU 频率 [[1]](http://lwn.net/Articles/682391/), [[2]](https://lkml.org/lkml/2016/3/17/420). |

根据实际硬件，以下的调速器可能被默认启用：

*   `ondemand` ：AMD 及旧款 Intel CPU。
*   `powersave` ：Intel 使用 `intel_pstate` 驱动的 CPU(Sandy Bridge 和更新的CPU)。

**Note:** pstate 驱动仅支持 performance 和 powersave governors and the performance [可以比老的 ondemand governor 更省电](http://www.phoronix.com/scan.php?page=news_item&px=MTM3NDQ).

**Warning:** 修改默认调速器时，请使用 CPU 监控工具监控温度、电压等指标。

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

采样率决定调速器多久进行一次检查并调整CPU频率。 设置`sampling_down_factor`大于1将通过降低负载评估的消耗，并将CPU保持在最高运行频率而提高性能。`sampling_down_factor` 的可选数值是 1 到 100000。这个可调参数对低CPU频率/负载没有效果。

要获取这个值 (default = 1)，运行：

```
$ cat /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

要设置这个值，运行：

```
# echo -n <value> > /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

#### 保存设置

要在重启后自动启用设置，通常使用 [内核模式选项](/index.php/Kernel_modules "Kernel modules") 和 [systemd#Temporary files](/index.php/Systemd#Temporary_files "Systemd")。如果某些特殊情况下会出现时序问题，可以使用 [udev](/index.php/Udev "Udev")。

例如要将 CPU core `0` 的调速器设置为 performance，驱动是 `acpi_cpufreq`, 创建如下 udev 规则：

 `/etc/udev/rules.d/50-scaling-governor.rules` 
```
SUBSYSTEM=="module", ACTION=="add", KERNEL=="acpi_cpufreq", RUN+=" /bin/sh -c ' echo performance > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor ' "

```

要在 *initramfs* 中启用设置，请参考下面例子：[udev#Debug output](/index.php/Udev#Debug_output "Udev").

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

*   一些CPU在默认的`on-demand`调速器配置下可能受到比较严重的性能损失（例如flash视频不能平滑地播放，或窗口动画停顿）。为了解决这些问题，完全禁用掉频率调整不如采取更积极的措施——降低每个CPU的*up_threshold* [sysctl](/index.php/Sysctl "Sysctl")变量值。阅读[#修改on-demand调速器的阈值](#修改on-demand调速器的阈值)章节以获得更多信息。

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

## 参阅

*   [Linux CPUFreq - kernel documentation](https://www.kernel.org/doc/Documentation/cpu-freq/index.txt)
*   [Comprehensive explanation of pstate](http://www.reddit.com/r/linux/comments/1hdogn/acpi_cpufreq_or_intel_pstates/)
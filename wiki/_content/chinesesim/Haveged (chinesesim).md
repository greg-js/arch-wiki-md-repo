Related articles

*   [Rng-tools](/index.php/Rng-tools "Rng-tools")

**翻译状态：** 本文是英文页面 [Haveged](/index.php/Haveged "Haveged") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-13，点击[这里](https://wiki.archlinux.org/index.php?title=Haveged&diff=0&oldid=349739)可以查看翻译后英文页面的改动。

[haveged](http://www.issihosts.com/haveged/) 项目的目的是提供一个简单易用的不可预测 [随机数生成器](/index.php/Random_number_generation "Random number generation")，基于 HAVEGE 算法。Haveged 可以解决在某些情况下，系统熵过低的问题。

{{警告|此程序无法保证熵的质量([[1]](https://lwn.net/Articles/525459/)，[[2]](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines)). 如果对安全要求较高，请考虑使用硬件随机数生成器 [rng-tools](https://www.archlinux.org/packages/?name=rng-tools).

## Contents

*   [1 安装](#安装)
*   [2 检查当前的熵](#检查当前的熵)
*   [3 其它选择](#其它选择)
*   [4 Virtual machines](#Virtual_machines)
*   [5 参阅](#参阅)

## 安装

[安装](/index.php/Install "Install") 软件包 [haveged](https://www.archlinux.org/packages/?name=haveged).

[启动](/index.php/Start "Start") 和 [启用](/index.php/Enable "Enable") 服务 `haveged.service`。

## 检查当前的熵

要检查是否需要 Haveged, 使用下面命令查看当前收集到的熵:

```
# cat /proc/sys/kernel/random/entropy_avail

```

如果结果比较低 (<1000)，建议安装 haveged. 否则加密程序会等待系统有足够的熵。例如如果使用 [软件热点](/index.php/Software_access_point "Software access point")，网速会比较慢。

安装 haveged 之后，可以再次查看系统熵看下有无提升。

## 其它选择

Unless you have a specific reason to not trust any hardware random number generator on your system, you should try to use them with the [rng-tools](/index.php/Rng-tools "Rng-tools") first and if it turns out not to be enough (or if you do not have a hardware random number generator available), then use Haveged.

## Virtual machines

As discussed at [Is it appropriate to use haveged as a source of entropy on virtual machines?](http://security.stackexchange.com/questions/34523/is-it-appropriate-to-use-haveged-as-a-source-of-entropy-on-virtual-machines), it can be contested whether haveged provides quality entropy within a virtual environment. Haveged relies on the rdtsc instruction, which may be virtualized within a virtual machine resulting in lower quantity entropy. On some hypervisors, it is possible to disable the virtualization of rdtsc, which would in theory allow haveged to provide higher quality entropy.

To disable the virtualization of the rdtsc instruction in VMware ESXi, add the setting `monitor_control.virtual_rdtsc = "FALSE"` to the virtual machine’s .vmx configuration file. VMware recommends the setting for use when performing measurements that require a precise source of real time in the virtual machine. [[3]](http://www.vmware.com/files/pdf/Timekeeping-In-VirtualMachines.pdf)

## 参阅

*   [http://www.issihosts.com/haveged](http://www.issihosts.com/haveged)
*   [如何通过 haveged 增加系统的熵](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)
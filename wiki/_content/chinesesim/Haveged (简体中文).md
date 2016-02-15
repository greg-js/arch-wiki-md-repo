**翻译状态：** 本文是英文页面 [Haveged](/index.php/Haveged "Haveged") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-13，点击[这里](https://wiki.archlinux.org/index.php?title=Haveged&diff=0&oldid=349739)可以查看翻译后英文页面的改动。

[haveged](http://www.issihosts.com/haveged/) 项目的目的是提供一个简单易用的不可预测 [随机数生成器](/index.php/Random_number_generation "Random number generation")，基于 HAVEGE 算法。Haveged 可以解决在某些情况下，系统熵过低的问题。

## Contents

*   [1 检查当前的熵](#.E6.A3.80.E6.9F.A5.E5.BD.93.E5.89.8D.E7.9A.84.E7.86.B5)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 服务](#.E6.9C.8D.E5.8A.A1)
*   [4 其它选择](#.E5.85.B6.E5.AE.83.E9.80.89.E6.8B.A9)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 检查当前的熵

要检查是否需要 Haveged, 使用下面命令查看当前收集到的熵:

```
# cat /proc/sys/kernel/random/entropy_avail

```

如果结果比较低 (<1000)，建议安装 haveged. 否则加密程序会等待系统有足够的熵。例如如果使用 [软件热点](/index.php/Software_access_point "Software access point")，网速会比较慢。

安装 haveged 之后，可以再次查看系统熵看下有无提升。

## 安装

从[官方软件仓库](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Install "Install") 软件包 [haveged](https://www.archlinux.org/packages/?name=haveged).

## 服务

软件包提供了 `haveged.service`, 详情参阅 [systemd](/index.php/Systemd "Systemd").

## 其它选择

[rng-tools](https://www.archlinux.org/packages/?name=rng-tools) 提供了类似的服务.

## 参阅

*   [http://www.issihosts.com/haveged](http://www.issihosts.com/haveged)
*   [如何通过 haveged 增加系统的熵](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged)
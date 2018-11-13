**翻译状态：** 本文是英文页面 [Frequently asked questions](/index.php/Frequently_asked_questions "Frequently asked questions") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-06，点击[这里](https://wiki.archlinux.org/index.php?title=Frequently+asked+questions&diff=0&oldid=547713)可以查看翻译后英文页面的改动。

## Contents

*   [1 一般问题](#一般问题)
    *   [1.1 Q) Arch Linux 是什么？](#Q)_Arch_Linux_是什么？)
    *   [1.2 Q) 为什么我不想用Arch？](#Q)_为什么我不想用Arch？)
    *   [1.3 Q) Arch Linux 支持什么架构?](#Q)_Arch_Linux_支持什么架构?)
    *   [1.4 Arch 遵循 FHS 吗?](#Arch_遵循_FHS_吗?)
    *   [1.5 我是一个彻头彻尾的Linux新手，我应该用Arch吗？](#我是一个彻头彻尾的Linux新手，我应该用Arch吗？)
    *   [1.6 Q) Arch的安装和配置十分麻烦，社区的人总是让我去读那些死长死长的手册。](#Q)_Arch的安装和配置十分麻烦，社区的人总是让我去读那些死长死长的手册。)
    *   [1.7 Q) Arch是为服务器、桌面还是工作站设计的？](#Q)_Arch是为服务器、桌面还是工作站设计的？)
    *   [1.8 我太喜欢Arch了，希望开发团队实现一个新功能](#我太喜欢Arch了，希望开发团队实现一个新功能)
    *   [1.9 Q) 什么时候发布新版本？](#Q)_什么时候发布新版本？)
    *   [1.10 Q) Arch Linux 是否稳定？会不会经常坏掉？](#Q)_Arch_Linux_是否稳定？会不会经常坏掉？)
    *   [1.11 Q) Arch需要更多曝光（比如广告）。](#Q)_Arch需要更多曝光（比如广告）。)
    *   [1.12 Q) Arch需要更多开发者](#Q)_Arch需要更多开发者)
    *   [1.13 Q) 为什么Arch下网速比其他系统慢？](#Q)_为什么Arch下网速比其他系统慢？)
    *   [1.14 Q) Arch为什么用了我的所有内存？](#Q)_Arch为什么用了我的所有内存？)
    *   [1.15 Q) 我的磁盘空间被什么东西占用了？](#Q)_我的磁盘空间被什么东西占用了？)
*   [2 软件包管理](#软件包管理)
    *   [2.1 Q) 我发现了某个软件包的错误，该怎么办？](#Q)_我发现了某个软件包的错误，该怎么办？)
    *   [2.2 Q) Arch软件包需要独特的后缀名。“.pkg.tar.xz”太长了，而且令人困惑](#Q)_Arch软件包需要独特的后缀名。“.pkg.tar.xz”太长了，而且令人困惑)
    *   [2.3 Q) Pacman应该提供函数库接口，这样其他软件就可容易地获得软件包信息。](#Q)_Pacman应该提供函数库接口，这样其他软件就可容易地获得软件包信息。)
    *   [2.4 Pacman需要某某功能！](#Pacman需要某某功能！)
    *   [2.5 仓库和镜像的区别是什么？](#仓库和镜像的区别是什么？)
    *   [2.6 Q) 我刚刚安装了一个软件包，怎么启动呢？](#Q)_我刚刚安装了一个软件包，怎么启动呢？)
    *   [2.7 Q) 在官方仓库中，为什么只为每个共享链接库提供一个版本？](#Q)_在官方仓库中，为什么只为每个共享链接库提供一个版本？)
    *   [2.8 Q) 执行pacman -Syu时，显示某个共享库需要升级，但依赖它的程序没有升级，我该怎么做呢？](#Q)_执行pacman_-Syu时，显示某个共享库需要升级，但依赖它的程序没有升级，我该怎么做呢？)
    *   [2.9 会不会出现仓库中的内核主版本更新了，而某些驱动包没有一同升级的情况？](#会不会出现仓库中的内核主版本更新了，而某些驱动包没有一同升级的情况？)
    *   [2.10 升级前该做什么?](#升级前该做什么?)
    *   [2.11 我知道某个包已经更新,但是 pacman 并没有发现更新](#我知道某个包已经更新,但是_pacman_并没有发现更新)
    *   [2.12 *X* 上游项目已经发布了一个新版本，多长时间 Arch 才会更新到新版本？](#X_上游项目已经发布了一个新版本，多长时间_Arch_才会更新到新版本？)
    *   [2.13 如果需要一个老的软件库，可以 symlink 到新版本吗？](#如果需要一个老的软件库，可以_symlink_到新版本吗？)
*   [3 安装](#安装)
    *   [3.1 Q) Arch需要安装程序，比如带图形界面的。](#Q)_Arch需要安装程序，比如带图形界面的。)
    *   [3.2 我安装了Arch，现在正面对一个命令行登陆界面，怎么办？](#我安装了Arch，现在正面对一个命令行登陆界面，怎么办？)
    *   [3.3 Q) 哪个桌面环境或窗口管理器比较好？](#Q)_哪个桌面环境或窗口管理器比较好？)
    *   [3.4 Arch比起其他“小型”发行版，有何独特之处？](#Arch比起其他“小型”发行版，有何独特之处？)
*   [4 其他](#其他)
    *   [4.1 Q) AUR是什么？](#Q)_AUR是什么？)
*   [5 64-bit](#64-bit)
    *   [5.1 我如何确定我的处理器是否支持 x86_64?](#我如何确定我的处理器是否支持_x86_64?)
    *   [5.2 为什么使用64位?](#为什么使用64位?)

## 一般问题

### Q) Arch Linux 是什么？

**A)** 请阅读[Arch Linux](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。

### Q) 为什么我不想用Arch？

**A)** 您也许不想使用Arch，如果：

*   没有能力、时间、愿望去打理这样一个高度可定制的GNU/Linux发行版。
*   需要非x86_64平台支持。
*   你是狂热的自由软件爱好者，只希望发行版提供GNU定义的自由软件。
*   你认为好的操作系统应当是已经配置好的：安装介质应默认包含一套完整的应用软件、桌面环境——达到“开箱即用”。
*   你不需要使用滚动升级的发行版、
*   你对目前使用的操作系统感到满意。

### Q) Arch Linux 支持什么架构?

Arch Linux 现在只支持 x86_64 (有时称为amd64) 架构，[对 i686 架构的支持将逐渐终结](https://www.archlinux.org/news/phasing-out-i686-support/)。

*非官方支持* 的移植版本： [i686](https://archlinux32.org/) 和 [ARM](https://en.wikipedia.org/wiki/ARM_architecture "wikipedia:ARM architecture") [[1]](http://archlinuxarm.org/)。

### Arch 遵循 [FHS](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html) 吗?

Arch Linux 遵循适用于 [systemd](/index.php/Systemd "Systemd") 服务管理器的文件系统架构，[file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) 包含了每个文件夹的解释和设计。 `/bin`, `/sbin` 和 `/usr/sbin` 现在是 `/usr/bin` 的符号链接，`/lib` (以及 `/lib64`) 是 `/usr/lib` 的符号链接。

### 我是一个彻头彻尾的Linux新手，我应该用Arch吗？

如果你是新手，要使用 Arch 就必须愿意花时间学习新系统，接受 Arch 是一个 DIY 的系统，每个用户都是自己系统的组建者。

在开始问任何问题之前，自己先通过Google、Wiki或者论坛进行搜索。我们为你创建了这些资源并让你可以随时访问，上千**志愿者**为你提供了大量的信息资源。

推荐阅读: [Arch terminology#RTFM](/index.php/Arch_terminology#RTFM "Arch terminology") 。

### Q) Arch的安装和配置十分麻烦，社区的人总是让我去读那些死长死长的手册。

**A)** Arch是针对一部分特定用户群设计的，也许不适合你。

### Q) Arch是为服务器、桌面还是工作站设计的？

**A)** Arch并不是针对特定应用设计的，而是针对特定类型的用户设计的。Arch适合那些喜欢并有动手能力的用户，以及希望打造属于自己的独一无二的系统的用户。因此，对于这些用户，Arch能胜任各种工作。许多人把Arch同时当做桌面系统和工作站。此外，archlinux.org网站在Arch上运行。

### 我太喜欢Arch了，希望开发团队实现一个新功能

与大家分享你的代码或是解决方案。如果大家和开发者确实认同该功能，有可能会被添加到系统中。Arch社区依靠大众贡献分享的代码和工具蓬勃发展。

### Q) 什么时候发布新版本？

**A)** Arch Linux 的发布版本只是安装脚本加上[core]仓库的快照，一般每月上旬发布一次。

Arch使用滚动升级模式，只需执行一条命令，便可升级系统到最新版本。基于上述原因，发布新版本对Arch并不重要，滚动升级使系统永葆青春。使用`pacman -Syu`命令升级系统，无需重装系统即可更新到最新版本。同样，Arch的新发行版本并不会提供什么新的功能。新的功能通过`pacman -Syu`命令即可立即拥有。

### Q) Arch Linux 是否稳定？会不会经常坏掉？

“用户”应当对自己的滚动升级的系统稳定性负责任。用户自己决定何时升级、修改配置。Arch与其他发行版的一个不同是，Arch是真正的“DIY”发行版。抱怨系统损坏是无意义的，毕竟上游的改动不是Arch开发者的责任。

如果你想要系统变得更稳定，请参阅：[提高系统稳定性](/index.php/Enhancing_Arch_Linux_Stability_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Enhancing Arch Linux Stability (简体中文)")

### Q) Arch需要更多曝光（比如广告）。

**A)** Arch已经得到应得的新闻曝光机会。Arch Linux 的目标不是为了变大。我们的目标是使它变得更好。让它自然增长吧。试图强迫它成长得更快会造成诸多问题。

### Q) Arch需要更多开发者

**A)** 也许吧。欢迎你来帮助我们！逛逛[论坛](https://bbs.archlinux.org)，[IRC channels](/index.php/IRC_channels "IRC channels") 以及[邮件列表](https://mailman.archlinux.org/mailman/listinfo/)，看看有什么需要做的。或者，看看论坛的 Community Contributions 子版面吧。

### Q) 为什么Arch下网速比其他系统慢？

**A)**网络是否正确配置，读一读[网络配置](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")。

### Q) Arch为什么用了我的所有内存？

**A)** 实际上，内存不用就浪费了。

很多新用户发现，Linux内核对内存的处理和他们所想的有所不同。由于访问内存比访问磁盘要快速得多，内核会把最近访问的数据缓存到内存中。缓存数据会在空闲内存耗尽时被释放。

造成这种困惑的罪魁祸首，恐怕是`free`命令：

 `$ free -m` 
```
             total       used       free     shared    buffers     cached
Mem:          1009        741        267          0        104        359
-/+ buffers/cache:        278        731
Swap:         1537          0       1537
```

注意`-/+ buffers/cache:`这一行——第一个数据是真正的“正在使用”的内存，第二个数据是“可利用”的内存（但不是“未使用”）。

上述例子是从一台总内存1G的笔记本电脑上取得的，已使用的内存有741M，剩下的内存貌似连浏览器都开不了呢！然而，根据我们上面的解释，这台机器只有278M内存是正在使用的，而剩下的731M内存都是可以使用的。根据后面的数字，104M的内存作为缓冲区，359MB内存用来缓存数据，两者都可以在需要时被释放。剩下的267M内存是完全没有使用的。

有什么用？更好的性能！

如果对此十分好奇，请参见[此文](http://www.linuxjournal.com/article/2770)。

### Q) 我的磁盘空间被什么东西占用了？

**A)** 问题的答案因系统而异。有一些[实用程序](/index.php/Common_Applications#Disk_Usage_Display_Programs "Common Applications")或许能告诉你答案。

## 软件包管理

详情请参考 [pacman](/index.php/Pacman "Pacman")、[pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") 和 [Official repositories](/index.php/Official_repositories "Official repositories")。

### Q) 我发现了某个软件包的错误，该怎么办？

**A)** 首先你需要搞清楚Arch队伍是否能够解决这个错误。有时并非如此（Firefox崩溃也许是Mozilla开发团队的错误）——这便是所谓的*上游错误*。如果确实是Arch的问题，你可以采取以下步骤：

1.  在论坛中搜索有关信息。看是否有人已经注意到过。
2.  根据 [Bugtracker](https://bugs.archlinux.org) 指导，提交[Bug报告](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。
3.  也可在论坛中发篇帖子，阐述问题细节并说明你已经报告过。这会避免其他人重复报告同样的问题。

### Q) Arch软件包需要独特的后缀名。“.pkg.tar.xz”太长了，而且令人困惑

**A)** 在Arch邮件列表曾有过讨论。一些用户提议.pac作为文件扩展名。但就目前所知而言，没有计划改变软件包的扩展名。

正如Tobias Kieslich（一名Arch开发者）所说：“一个软件包**就是**一个[xz]压缩包！它可以被很多软件打开、研究和操作。此外，这种mime-type也可以被大多数软件自动地正确识别。”

### Q) Pacman应该提供函数库接口，这样其他软件就可容易地获得软件包信息。

**A)** [libalpm](https://www.archlinux.org/pacman/libalpm.3.html)（Arch Linux Package Management，Arch Linux 软件包管理）是 pacman 的后端，这个库大大方便了交互式前端的编写（例如图形化前端）。

### Pacman需要某某功能！

如果有新想法，可以在 [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/) 邮件列表进行讨论，或查看[官方论坛](https://bbs.archlinux.org/) 看看有没有类似想法。

也欢迎你自己实现新功能。也许你的代码或补丁不会被官方接受，但他人可能会用到。

### 仓库和镜像的区别是什么？

参考 [pacman#Repositories and mirrors](/index.php/Pacman#Repositories_and_mirrors "Pacman").

### Q) 我刚刚安装了一个软件包，怎么启动呢？

**A)** 如果正在使用像[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")和[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")这样的软件包，程序一般会自动出现在菜单中。如果是命令行程序，则可使用如下命令查看可执行文件名称和位置：

```
$ pacman -Qlq *package_name* | grep /usr/bin/

```

### Q) 在官方仓库中，为什么只为每个共享链接库提供一个版本？

**A)** 某些发行版，比如Debian，会为一个共享库提供多个版本，比如：`libfoo1`，`libfoo2`，`libfoo3`等等。这样，就可以同时安装那些依赖不同版本libfoo的程序。

Arch官方只对最新版的程序提供支持。摆脱了过时的软件包，包维护人员就可以全力维护新版本的程序。只要上游提供新版本的共享库，我们就会重新编译相关程序，更新仓库。

### Q) 执行`pacman -Syu`时，显示某个共享库需要升级，但依赖它的程序没有升级，我该怎么做呢？

**A)** 这种情况理应不会发生。假如官方源一个名为`foobaz`的程序，成功地使用新版本共享库`libbaz`编译成功，那么它应该和`libbaz`一同更新。如果编译不成功，由于旧的`foobaz`存在依赖关系，例如：

```
libbaz=1.5

```

所以当`libbaz`升级时，它会被移除。

如果`foobaz`是你自己编译的或是从AUR获取的，当`libbaz`升级时你应当重新编译它。如果编译失败，请通知`foobaz`开发者。

### 会不会出现仓库中的内核主版本更新了，而某些驱动包没有一同升级的情况？

不可能。当内核主版本升级时，所有支持的驱动一定会一同更新。然而，如果你安装有非内核支持的驱动包，比如`catalyst`，内核升级可能导致系统挂机。你应当在内核升级时自行重编译它们。

### 升级前该做什么?

在升级前,记得访问 [Arch Linux 新闻列表](https://www.archlinux.org/),[通告邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) (有时需要看看 [论坛](https://bbs.archlinux.org/)和[各个邮件列表](https://mailman.archlinux.org/mailman/listinfo/)),需要特别注意的事项都会列在那里.另见 [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance").

### 我知道某个包已经更新,但是 pacman 并没有发现更新

可能是 *pacman* 镜像还没有同步,最好等等或是换个镜像服务器. [MirrorStatus](https://www.archlinux.org/mirrors/status/) 可以帮助你区分那些镜像服务器是最新的.

### *X* 上游项目已经发布了一个新版本，多长时间 Arch 才会更新到新版本？

软件包将会在准备好后发布，发布的时间取决于上游的变动和打包人员的精力。如果发布的是小版本，可能只需要几个小时。如果发布的是大版本更新，可能需要数周时间。此外，有些软件包会在 [testing](/index.php/Testing "Testing") 仓库中停留一段时间进行小范围测试。[软件包维护者](/index.php/Package_maintainer "Package maintainer") 会尽量快点将稳定版本发布到仓库。如果发下官方软件仓库中的软件过旧，可以在 [软件包页面](https://www.archlinux.org/packages/) 进行标记。

### 如果需要一个老的软件库，可以 symlink 到新版本吗？

如果幸运，这个方式可以用来救急。但是这不是一个正确的方式：

*   软件库不会无缘无故更新版本 - API/ABI 可能发送变动，这些变动是否影响到使用只能听天由命。
*   软件包管理器不会记录软链接，新手执行这种操作，可能引起不好恢复的错误。
*   未被记录的老版本文件很快就会被忘掉，安全漏洞不会被修复。

推荐的方式是使用或编写[兼容软件包](https://aur.archlinux.org/packages/?SeB=n&K=compat)，用其提供需要的版本。

## 安装

### Q) Arch需要安装程序，比如带图形界面的。

**A)** 由于Arch通常不需要多次安装（采取滚动升级），安装程序并不是开发者和用户关注的重点。[Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)") 已经完全更新到使用命令行的版本。

### 我安装了Arch，现在正面对一个命令行登陆界面，怎么办？

建议阅读 [General recommendations](/index.php/General_recommendations "General recommendations").

### Q) 哪个桌面环境或窗口管理器比较好？

**A)** 有很多选项，选择最适合你的即可。参见：[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。

### Arch比起其他“小型”发行版，有何独特之处？

建议阅读 [Arch compared to other distributions (简体中文)](/index.php/Arch_compared_to_other_distributions_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch compared to other distributions (简体中文)").

## 其他

### Q) AUR是什么？

**A)** 参见：[Arch用户软件仓库#FAQ](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#FAQ "Arch User Repository (简体中文)")。

## 64-bit

### 我如何确定我的处理器是否支持 x86_64?

运行下面的命令：

```
$ less /proc/cpuinfo

```

查找 `flags` 条目。如果你看见 `lm` 标志，那么你的处理器是支持 x86_64 的。

Windows 用户可以使用免费软件 [CPU-Z](http://www.cpuid.com/cpuz.php)，可以确定CPU是否支持64位。

带有 AMD 的 "AMD64" 指令集或者英特尔的 "EM64T" 指令集的 CPU 兼容 x86_64 发行版和二进制包。

### 为什么使用64位?

64位系统(大多数情况下)更快，而且更安全。更安全是由于拥有 [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") 、 [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") 特性，以及 [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") (它在i686内核中由于禁用了PAE而无法使用)。如果你的计算机在运行4GB或者更多的内容，应该使用64位系统，因为多余的内存无法被32位系统分配。

编程人员也更加倾向于不关心32位系统，因为新的x86 CPU通常都支持64位扩展。

还有许多其他的理由让我们不使用32位系统，但是在内核、用户空间和单独的程序中我们没有办法列出所有的64位比32位做得好的地方。
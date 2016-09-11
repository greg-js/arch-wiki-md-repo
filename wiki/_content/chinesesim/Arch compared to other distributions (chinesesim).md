**翻译状态：** 本文是英文页面 [Arch_Compared_to_Other_Distributions](/index.php/Arch_Compared_to_Other_Distributions "Arch Compared to Other Distributions") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-22，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Compared_to_Other_Distributions&diff=0&oldid=420550)可以查看翻译后英文页面的改动。

本文在 Arch Linux 和其他流行的 GNU/Linux 发行版、类 UNIX 操作系统之间做了一些比较，以帮助用户判断 Arch Linux 是否能符合他们的需要。虽然对此进行一些描述有助于用户理解这些操作系统之间的不同点，但是比较 Arch Linux 和其他发行版的最好办法还是安装它们并进行亲身体验。

[w:Comparison of operating systems](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") 和 [w:Comparison of Linux distributions](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions") 包含了更详细的比较信息。

## Contents

*   [1 基于源码的发行版](#.E5.9F.BA.E4.BA.8E.E6.BA.90.E7.A0.81.E7.9A.84.E5.8F.91.E8.A1.8C.E7.89.88)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo.2FFuntoo_Linux)
*   [2 通用发行版](#.E9.80.9A.E7.94.A8.E5.8F.91.E8.A1.8C.E7.89.88)
    *   [2.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 新手友好的发行版](#.E6.96.B0.E6.89.8B.E5.8F.8B.E5.A5.BD.E7.9A.84.E5.8F.91.E8.A1.8C.E7.89.88)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
*   [4 与BSD系列的对比](#.E4.B8.8EBSD.E7.B3.BB.E5.88.97.E7.9A.84.E5.AF.B9.E6.AF.94)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 基于源码的发行版

基于源码的发行版非常容易移植，它们的优点是可以根据机器架构和使用情况最优地控制和编译整个系统和所有软件，而劣势是要在源码编译上消耗大量时间。Arch Linux 的基础包和其他所有软件包都只为 i686 和 x86-64 平台编译，相比基于 i386/i486/i586 二进制包的发行版,性能的优势和潜力更大。

### CRUX

*   在创建Arch之前，Judd Vinet使用CRUX并且对其相当赞赏（CRUX是 Per Lidén创建的一个极简发行版），在草创之初，ARCH就和CRUX、BSD秉承同样的理念，之后才有了用C完成的[pacman](/index.php/Pacman "Pacman")。
*   ARCH和CRUX拥有一些相同的指导理念，比如：针对硬件架构进行优化,极简化和K.I.S.S原则驱动。
*   ARCH和CRUX的发行版都提供类ports系统，并且和*BSD系统一样，都提供了一个基础系统以供用户在其之上进行构建。
*   ARCH使用pacman来进行二进制包管理,同时还使用[Arch Build System](/index.php/Arch_Build_System "Arch Build System")。CRUX使用一个叫prt-get的社区开发软件和它自己的ports系统来处理依赖关系解析。尽管如此，CRUX上所有的软件包都需要从源代码进行编译，虽然CRUX的基础系统是基于二进制包的。
*   ARCH官方只支持i686和x86_64架构.而CRUX官方只支持x86_64。
*   ARCH是一个滚动升级系统，其软件仓库提供大量编译好的二进制软件包,除此之外，还拥有[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")。CRUX的软件仓库比较逊色并且其ports系统也缺乏官方支持。

### LFS

*   LFS（Linux From Scratch）只以文档形式存在，提供的文档指导用户如何从零开始构建一个完全个性化的操作系统：从如何获取构建一个基础操作系统所需的源代码，到如何编译，如何打补丁，如何对系统进行配置。总之，LFS 提供一个构建和定制基础系统的良好教程。
*   LFS 不提供在线软件仓库；必须手动获取源代码，然后用 make 编译安装它们。（需要一些包管理方法,这点在 LFS Hints 里面提到过）
*   Arch 基础系统除了提供和 LFS 一样的软件包,还包含 [systemd](/index.php/Systemd "Systemd") ，[pacman](/index.php/Pacman "Pacman") 等一些额外的工具，并且这些软件都已经为 i686/x86_64 架构编译过了。Arch 社区和开发者提供了数以千计的软件包，这些软件包可以通过 [pacman](/index.php/Pacman "Pacman") 或者 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 脚本进行安装（PKGBUILD脚本需要和 [Arch Build System](/index.php/Arch_Build_System "Arch Build System") 一起使用）。除此之外，Arch 还包含了一个名叫 [makepkg](/index.php/Makepkg "Makepkg") 的工具来生成方便pacman使用的.pkg.tar.xz格式的包。
*   Judd Vinet 从零开始构建了 Arch，然后使用 C 开发了 Pacman。所以，Arch 有些时候被幽默的描述为“外带一个优秀包管理器的 Linux ”。

### Gentoo/Funtoo Linux

*   Arch Linux 和 Gentoo Linux 都是滚动升级的发行版，所以在上游软件发布很短时间后，其上就会有软件包可用。
*   Gentoo 的基础系统和软件包都是根据用户指定的 USE 标识直接从源代码构建。Gentoo 提供了一个类 ports 系统（ Ports 是 BSD 上的一个系统工具）来从源代码编译软件包，而 Arch 基础系统被设计为“直接由预构建好的 i686/x86_64 二进制软件包组成”。一般来说，Arch 更易于构建和升级，而 Gentoo 更易于进行系统化的定制。
*   Arch 支持 i686 和 x86_64 架构，Gentoo对x86、ppc、sparc、alpha、amd64、arm、mips、hppa、s390、sh和 itanium 架构都提供官方支持。
*   Gentoo 的官方包管理工具比 ArchLinux 的更复杂和强大，而且一些在 Gentoo 中处于核心位置的特性（比如 UES标记、SLOTs 等等）在 Arch 中并没有相对应的功能。究其原因，一是因为 ArchLinux 主要是一个二进制发行版，第二是因为 Gentoo 和 Arch 在设计哲学上有些差别。Arch 在原则上更偏向于架构的简洁性和避免过度设计。
*   因为 Gentoo 和 Arch 的安装包都只包含基本系统，所以它们两者都被认为是需要高度定制化的系统。一般来说，Gentoo 用户如果习惯于 systemd 的话，对Arch的大多数方面都会感到满意。

## 通用发行版

这些发行版提供长处和优点更为广泛,可以满足绝大部分对操作系统的需求.

### Debian GNU/Linux

*   Debian 是上游最大的发行版,其社区规模更大,提供稳定、测试和不稳定分支,包含超过43000个二进制包. ARCH 的软件仓库相对较小,但是如果包含AUR,那么支持的软件数量也差不多.
*   Debian 对自由软件更热情,但是也提供非自由软件仓库.ARCH对GNU定义的非自由（'non-free'）软件更显宽容.
*   Debian 对稳定分支的测试更详细彻底，软件基本冻结并提供[五年](https://wiki.debian.org/LTS)支持。Arch 提供的的软件包比 Debian Stable 和 testing 分支中的软件包更新,和 unstable 里的差不多，而且没有固定发布周期，滚动发布。
*   Debian 支持许多架构,包括 alpha,arm,hppa,i386,x86_64,ia64,m68k,mips,mipsel,powerpc,s390和sparc.而ARCH仅对 i686 和 x86_64 提供官方支持,其对 arm 的支持移植自社区项目(例如对Raspberry Pi的支持).
*   ARCH 对从源码创建软件包提供更好的支持,有一个类 ports 系统.Debian 不提供类 ports 系统,而是依靠它巨大的软件仓库.
*   ARCH 安装环境只提供最小的基本系统,然后通过编辑文本文件来配置系统.而 Debian 的配置方式更为自动化并且还提供多种安装方式.
*   在启动脚本上,Debian ( 8.0或更高版本 )和 ARCH 均使用 [systemd](/index.php/Systemd "Systemd") ,因为其总体性能优。
*   ARCH 一般将 lib 软件库与其头文件一同打包在一起，而 Debian 则将这两部分分别放到不同的 package 中。
*   ARCH 只在迫不得已时才打补丁,以避免出现上游无法审阅的问题. Debian 使用者众多,所以经常对软件包打补丁.

### Fedora

*   Fedora 由社区开发,并红帽提供公司级支持.它是红帽版的技术前导版,对新技术的采用非常激进. Fedora 的软件包和项目会被引入 RHEL 中,并最终被其他发行版采用.Arch 不像很多发行版一样提供测试分支,而是采用滚动方式进行升级.
*   Fedora 采用 RPM 包,用 DNF 包管理器并且提供图形化的包管理工具. Arch 使用 [pacman](/index.php/Pacman "Pacman") 管理 tar.xz 软件包.
*   Fedora 坚持开源理念,默认不提供有专利限制的软件,比如MP3支持.一些第三方源提供这些内容. Arch 对于 MP3 及非自由软件更加宽松，将决定权交给用户。
*   Fedora 提供很多安装选项,比如图形化安装和最小化安装.Fedora "spins" 还提供许多桌面环境以供用户选择(这些桌面环境都带一些默认的软件包).ARCH 仅提供了一些脚本来方便进行最小化系统安装
*   Fedora 发行周期固定,但官方支持通过 dnf-plugin-system-upgrade (适合大部分的版本)或 rpm-ostree (适合 Fedora Atomic Host)工具进行跨版本升级. Arch 是滚动升级系统.
*   ARCH 有 ports 系统,而 Fedora 没有.
*   ARCH 和 Fedora 都面向有经验的用户和开发者,都倡导用户积极为项目开发做贡献.
*   Fedora 在 SELinux 整合,GCJ 编译包( GCJ 的目的是解除对 Oracle JRE 的依赖)等方面走在前列,并且积极为上游开发做贡献.和其他项目相比,Red Hat 和 Fedora 开发者贡献的 Linux 内核代码最多.
*   Arch Linux Wiki 被认为是各发行版Wiki中内容最丰富的和最易用的.Fedora wiki 仅是开发者,测试者和用户间交流信息的平台,并不是和 Arch Wiki 一样为最终用户准备,其实它更像一个问题追踪和合作开发 wiki.

### Slackware

*   Slackware 和 Arch 很相似，二者都是小巧优雅的发行版。
*   Slackware 很少修改软件包，从内核往上全部都使用上游提供的软件。Arch 只有在避免出现严重问题或保证顺利打包时才使用补丁。
*   Slackware 使用 BSD 风格的初始化脚本，Arch 使用 [systemd](/index.php/Systemd "Systemd").
*   Arch 有一个健壮的包管理系统 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")。与 Slackware 的标准工具不同，它可以自己处理依赖关系并提供更自动化的系统升级方式。Slackware 用户更倾向于手动处理依赖关系，以尽可能控制自己的系统。Slackware也对预编译的库和依赖提供杰出的支持。
*   Arch 是一个滚动升级的系统，Slackware的发布更为保守，更喜欢提供稳定的软件包。在这个方面，Arch 更为“前卫”。
*   Arch 软件仓库提供成千上万的二进制包，而相比之下 Slackware 官方支持的软件包比较少。
*   Arch提供 [Arch Build System](/index.php/Arch_Build_System "Arch Build System")（一个类ports系统）和[AUR](/index.php/AUR "AUR")（用户贡献的数以万计的PKGBUILD）。 Slackware 提供一个相似的系统 [slackbuilds.org](http://www.slackbuilds.org)，它是半官方支持的Slackbuilds（和PKGBUILD相似）仓库。Slackware 用户一般会对 Arch 的多数方面感到满意。

## 新手友好的发行版

"新手友好版"有时也被叫做“新手发行版”.新手友好的发行版之间有许多相同之处,而Arch和他们其中的任何一个都不同.如果你想通过构建极简系统的方式来学习GNU/Linux,Arch也许是一个好选择,因为相比之下,Arch只需安装少量软件包.不同"新手发行版"之间的不同如下:

### Ubuntu

*   Ubuntu 是一个非常流行的基于Debian的发行版,由 Canonical 公司提供商业支持;而 Arch 是独立开发而成.
*   Ubuntu 和 Arch 的目标不同并且面向的用户群体也不一样.Arch 为那些渴望自己动手的用户设计,而 Ubuntu 提供自动配置好了的系统,对用户来说更"友好".Arch 设计了一个最小化的基础系统,然后严重依赖用户按自己的特定需求进行定制.一般来说,开发者和动手能力强的用户更喜欢 Arch.许多 Arch 用户都从 Ubuntu 起步,最终转向 Arch Linux.
*   现在 Ubuntu 开发和推广的重心好像都转移到了触摸屏设备上,而 Arch 的开发依然坚持以用户为中心,鼓励社区合作开发客制化的解决方案.
*   Ubuntu 每6个月发行一个新版本，而 Arch 是滚动升级.
*   Arch 提供类 ports 的软件包构建系统和[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")，用户可以分享源代码编译脚本，然后用[pacman](/index.php/Pacman "Pacman") 安装管理。Ubuntu 使用更复杂的 [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool "wikipedia:Advanced Packaging Tool"), 可以通过[PPA](https://launchpad.net/ubuntu/+ppas)分发软件。
*   这两个社区也有不尽相同/ Arch 社区更小,鼓励用户为Arch奉献一份力量.做为对比, Ubuntu 社区很大,并能容忍其中许多实际上并未为开发、打包和维护作贡献的用户.

### Linux Mint

*   [Linux Mint](http://www.linuxmint.com/) 最初是一个 [Ubuntu](#Ubuntu) 的衍生版本，后来有添加了 LMDE（Linux Mint的 Debian版本）这是一个基于 [Debian](#Debian_GNU.2FLinux) 的版本。而 Arch 是一个独立的发行版，它依赖自己的 [构建系统](/index.php/ABS "ABS") 和 [官方仓库](/index.php/Official_repositories "Official repositories")。
*   为了方便系统维护，Mint 包含了一些图形化工具，叫做 *MintTools(Mint工具)*，而 Arch 仅仅提供简单的命令行工具，例如 [pacman](/index.php/Pacman "Pacman")，因此 Arch 的系统管理工作需要由用户自己组织。
*   Mint 主要运行 [Cinnamon](/index.php/Cinnamon "Cinnamon") 和 [MATE](/index.php/MATE "MATE")作为它的图形界面，也可以选择 [KDE](/index.php/KDE "KDE") 或者[Xfce4](/index.php/Xfce4 "Xfce4")。 Mint 同时支持plus codecs、flash、DVD playback 和 MP3，这其中有一些是私有软件。
*   新的 Mint 系统每半年发布一次新版本。时间大约实在新的 Ubuntu 发布一个月以后。每一个版本都是基于最新的 Ubuntu LTS 而且有五年支持。 Mint 的 Debian 版本 (LMDE) 基于 Debian 稳定版。而且只接受来自 Mint 的更新或者安全性更新。而 Arch 则完全是一个滚动更新的发行版。

### openSUSE

*   openSUSE 以RPM格式软件包为中心.提供了优秀的 YaST2 图形配置工具。Arch 没有提供此类工具.一般 openSUSE 更适合经验较少或需要图形驱动界面、自动完成配置的用户。
*   openSUSE Leap 每年发布一个版本, 软件比 Arch 旧. Tumbleweed 是滚动更新的, 软件新旧和 Arch 差不多.
*   openSUSE 默认不提供有专利限制的软件,比如 MP3 支持.你需要添加第三方源来取得这些内容. Arch 对于 MP3 及非自由软件更加宽松，将决定权交给用户。

### Mandriva/Mageia

Mandriva Linux (以前的 Mandrake Linu x) 创建自1998年，它的目标是让 GNU/Linux 对任何人来说都很容易使用。它使用基于 RPM 的 urpmi 包管理器, 现在已经不再维护。Mageia 是一个由 Mandriva 前雇员创建的 Mandriva 分支，但是和 Mandriva 不一样的是，它是一个非盈利的由社区驱动的发行版。再一次重申：Arch 是一个比 Mandriva 或者 Mageia 要简单的发行版，基于文本，而且要依赖于更多的手动配置，Arch瞄准的是Linux中、高级用户。

## 与BSD系列的对比

*   *BSDs 都始于 UC Berkeley 大学的工作，致力于提供一个可以自由分发、免费的 UNIX 系统. 它们不是 GNU/Linux 发行版,而是UNIX-like系统， 从原版 AT&T `UNIX`代码演进而来。

*   Arch 和 *BSDs 都提供紧密整合的基本系统和 ports 系统。与GNU/Linux系统(比如Arch)不同 ,BSD 系统的内核和用户空间的程序,比如说 shell 和常用工具(像ls,cp,cat和ps),集中在单一的源代码仓库中开发.

*   BSD 协议注重保护程序员,而 GPL 注重保护代码.Arch 在 GPL 下发布.

*   要获得 *BSD 变体的更多信息，请阅读 [Wikipedia:Comparison of BSD operating systems](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems")。

## 参阅

*   [DistroWatch.com](http://distrowatch.com/)
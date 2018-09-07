相关文章

*   [AUR 帮助程序](/index.php/AUR_helpers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR helpers (简体中文)")
*   [AUR Trusted User Guidelines (简体中文)](/index.php/AUR_Trusted_User_Guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR Trusted User Guidelines (简体中文)")
*   [AurJson](/index.php/AurJson "AurJson")
*   [PKGBUILD (简体中文)](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")
*   [makepkg (简体中文)](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   [Pacman (简体中文)](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [.SRCINFO (简体中文)](/index.php/.SRCINFO_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) ".SRCINFO (简体中文)")
*   [Official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")
*   [Arch Build System (简体中文)](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

**翻译状态：** 本文是英文页面 [Arch_User_Repository](/index.php/Arch_User_Repository "Arch User Repository") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-04，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=488175)可以查看翻译后英文页面的改动。

[Arch用户软件仓库](https://aur.archlinux.org)（Arch User Repository，AUR）是为用户而建、由用户主导的Arch软件仓库。AUR中的软件包以软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")）的形式提供，用户自己通过[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")生成包，再由[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装。创建AUR的初衷是方便用户维护和分享新软件包，并由官方定期从中挑选软件包进入[community](/index.php/Community "Community")仓库。本文介绍用户访问和使用AUR的方法。

许多官方仓库软件包都来自AUR。通过AUR，大家相互分享新的软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")和其他相关文件）。用户还可以为软件包投票。如果一个软件包投票足够多、没有协议问题、打包质量好，那么它就很有希望被收录进官方[community]仓库（以后就可以直接通过[pacman](/index.php/Pacman "Pacman") 或 [abs](/index.php/ABS "ABS") 安装了）。

## Contents

*   [1 导读](#.E5.AF.BC.E8.AF.BB)
*   [2 历史](#.E5.8E.86.E5.8F.B2)
*   [3 搜索](#.E6.90.9C.E7.B4.A2)
*   [4 安装软件包](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [4.1 准备](#.E5.87.86.E5.A4.87)
    *   [4.2 获取软件包构建所需文件](#.E8.8E.B7.E5.8F.96.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.9E.84.E5.BB.BA.E6.89.80.E9.9C.80.E6.96.87.E4.BB.B6)
    *   [4.3 构建和安装软件包](#.E6.9E.84.E5.BB.BA.E5.92.8C.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [5 反馈](#.E5.8F.8D.E9.A6.88)
*   [6 分享和维护软件包](#.E5.88.86.E4.BA.AB.E5.92.8C.E7.BB.B4.E6.8A.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [6.1 提交软件包](#.E6.8F.90.E4.BA.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [6.1.1 提交软件包的规则](#.E6.8F.90.E4.BA.A4.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84.E8.A7.84.E5.88.99)
        *   [6.1.2 认证](#.E8.AE.A4.E8.AF.81)
        *   [6.1.3 创建软件包](#.E5.88.9B.E5.BB.BA.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [6.1.4 提交和更新软件包](#.E6.8F.90.E4.BA.A4.E5.92.8C.E6.9B.B4.E6.96.B0.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [6.2 维护软件包](#.E7.BB.B4.E6.8A.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [6.3 其他事项](#.E5.85.B6.E4.BB.96.E4.BA.8B.E9.A1.B9)
*   [7 AUR3 软件包的Git仓库](#AUR3_.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84Git.E4.BB.93.E5.BA.93)
*   [8 AUR translation](#AUR_translation)
*   [9 FAQ](#FAQ)
    *   [9.1 AUR是什么？](#AUR.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [9.2 什么样的软件包能被放到 AUR?](#.E4.BB.80.E4.B9.88.E6.A0.B7.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85.E8.83.BD.E8.A2.AB.E6.94.BE.E5.88.B0_AUR.3F)
    *   [9.3 如何给 AUR 中的软件包投票?](#.E5.A6.82.E4.BD.95.E7.BB.99_AUR_.E4.B8.AD.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.8A.95.E7.A5.A8.3F)
    *   [9.4 受信用户（或TU）是什么？](#.E5.8F.97.E4.BF.A1.E7.94.A8.E6.88.B7.EF.BC.88.E6.88.96TU.EF.BC.89.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [9.5 Arch User Repository和[community]仓库有何区别？](#Arch_User_Repository.E5.92.8C.5Bcommunity.5D.E4.BB.93.E5.BA.93.E6.9C.89.E4.BD.95.E5.8C.BA.E5.88.AB.EF.BC.9F)
    *   [9.6 AUR的某个软件包过时了，该怎么办？](#AUR.E7.9A.84.E6.9F.90.E4.B8.AA.E8.BD.AF.E4.BB.B6.E5.8C.85.E8.BF.87.E6.97.B6.E4.BA.86.EF.BC.8C.E8.AF.A5.E6.80.8E.E4.B9.88.E5.8A.9E.EF.BC.9F)
    *   [9.7 makepkg无法构建某个软件包怎么办？](#makepkg.E6.97.A0.E6.B3.95.E6.9E.84.E5.BB.BA.E6.9F.90.E4.B8.AA.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.80.8E.E4.B9.88.E5.8A.9E.EF.BC.9F)
    *   [9.8 如何编写PKGBUILD？](#.E5.A6.82.E4.BD.95.E7.BC.96.E5.86.99PKGBUILD.EF.BC.9F)
    *   [9.9 我想提交一个PKGBUILD，希望别人帮忙检查错误。](#.E6.88.91.E6.83.B3.E6.8F.90.E4.BA.A4.E4.B8.80.E4.B8.AAPKGBUILD.EF.BC.8C.E5.B8.8C.E6.9C.9B.E5.88.AB.E4.BA.BA.E5.B8.AE.E5.BF.99.E6.A3.80.E6.9F.A5.E9.94.99.E8.AF.AF.E3.80.82)
    *   [9.10 PKGBUILD（AUR软件包）怎样才能被收录到community软件仓库？](#PKGBUILD.EF.BC.88AUR.E8.BD.AF.E4.BB.B6.E5.8C.85.EF.BC.89.E6.80.8E.E6.A0.B7.E6.89.8D.E8.83.BD.E8.A2.AB.E6.94.B6.E5.BD.95.E5.88.B0community.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93.EF.BC.9F)
    *   [9.11 如何加速编译？](#.E5.A6.82.E4.BD.95.E5.8A.A0.E9.80.9F.E7.BC.96.E8.AF.91.EF.BC.9F)
    *   [9.12 foo 和 foo-git 的区别是什么?](#foo_.E5.92.8C_foo-git_.E7.9A.84.E5.8C.BA.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.3F)
    *   [9.13 为啥某个软件包从AUR消失了?](#.E4.B8.BA.E5.95.A5.E6.9F.90.E4.B8.AA.E8.BD.AF.E4.BB.B6.E5.8C.85.E4.BB.8EAUR.E6.B6.88.E5.A4.B1.E4.BA.86.3F)
    *   [9.14 我要怎么找出从AUR里消失的软件包?](#.E6.88.91.E8.A6.81.E6.80.8E.E4.B9.88.E6.89.BE.E5.87.BA.E4.BB.8EAUR.E9.87.8C.E6.B6.88.E5.A4.B1.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85.3F)
    *   [9.15 如何查找已经安装但是从 AUR 消失的软件包](#.E5.A6.82.E4.BD.95.E6.9F.A5.E6.89.BE.E5.B7.B2.E7.BB.8F.E5.AE.89.E8.A3.85.E4.BD.86.E6.98.AF.E4.BB.8E_AUR_.E6.B6.88.E5.A4.B1.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [9.16 想知道 AUR 里都有啥 ？](#.E6.83.B3.E7.9F.A5.E9.81.93_AUR_.E9.87.8C.E9.83.BD.E6.9C.89.E5.95.A5_.EF.BC.9F)
*   [10 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## 导读

用户可以从[AUR网站](https://aur.archlinux.org)下载[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")。[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")使用该文件生成软件包，最后由[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装。

*   确保 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组 已被安装 (`pacman -S --needed base-devel`)。
*   浏览[#FAQ](#FAQ)获取常见问题的答案。
*   在`/etc/makepkg.conf`中，针对处理器使用合适的CFLAGS、CXXFLAGS编译参数，以优化软件包编译。通过设置MAKEFLAGS变量，可以启用多线程编译，使用多核心处理器的话，将大大减少编译时间。详情参见[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")。
*   也可以通过 SSH 连接到 AUR: 运行 `ssh aur@aur.archlinux.org help` 获得可用指令的列表。

## 历史

最初，人们上传[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")、附属文件、编译好的软件包到 `ftp://ftp.archlinux.org/incoming`。文件一直存放在那里，直到[软件包维护人员](/index.php/Package_Maintainer "Package Maintainer")发现并收录。

后来，出现了受信用户软件仓库，部分社区用户拥有了建设自己的软件仓库的权力。以这个仓库为基础，为使其更加灵活易用，AUR出现了。事实上，AUR维护人员现在仍被称为受信用户（简称TU）。

从2015-06-08 到 2015-08-08，AUR 版本从 3.5.1 到 4.0.0，Git 仓库成为 PKGBUILD 的发布方式.

## 搜索

AUR提供了方便人们访问的[网页接口](https://aur.archlinux.org/)，以及另一个方便程序访问的[RPC接口](https://aur.archlinux.org/rpc.php)。网页上有一个搜索框，可以用它搜索软件包名称或描述。

软件包检索使用MySQL的LIKE比较字符串。这使得搜索规则更加灵活（例如，搜索“tool%like%grep”而非“tool like grep”）。如果需要搜索带有“%”的内容，用斜杠转义为“\%”即可。

## 安装软件包

从AUR（即[unsupported]仓库）安装软件包并不很困难。步骤如下：

1.  从AUR下载包含[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")和其他安装文件（比如 [systemd](/index.php/Systemd "Systemd") 和补丁，通常不是实际代码）的tar包。
2.  用命令 `tar -xvf packagename.tar.gz` 解包到一个仅用于编译AUR的空闲文件夹。
3.  验证[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")和其它相关文件,确保其中不含有恶意代码.
4.  在上述文件夹中运行 `makepkg -si`. 命令会自动调用[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")解决依赖关系，然后下载代码、编译并打包. 然后安装软件包。

### 准备

首先确定安装了 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组，其中包括[make](https://www.archlinux.org/packages/?name=make)和其他编译工具：

**Note:** AUR 中的软件包都会假定你已经安装了 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组(例如它们不会将这个组中的软件包列入依赖列表.

然后，选择一个合适的编译目录。这个目录用作生成软件包时的工作目录，任何空白目录都可以。下面的示例中使用`~/builds`作为编译目录。

### 获取软件包构建所需文件

通过搜索或任何方式，在AUR中找到要安装的软件包。阅读介绍，检查软件包更新日期，看看别人的评论。

确认无误后，下面三种方法可以不用 AUR 工具就下载到需要的编译文件。

*   从软件包信息页面点击“Download snapshot”（中文页面翻译做“下载快照”），保存压缩包到编译目录。以本文的foo软件包为例，压缩包名为“foo.tar.gz”（标准格式是“<pkgname>.tar.gz”）。

*   从终端下载：

```
 $ cd ~/builds
 $ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/foo.tar.gz

```

*   在"Package Details"中，找到"Git Clone URL"，然后下载 [Git](/index.php/Git "Git")仓库：

```
 $ cd ~/build-repos
 $ git clone [https://aur.archlinux.org/foo.git](https://aur.archlinux.org/foo.git)

```

	这样做的其中一个好处是你以后可以通过 `git pull` 的形式来更新。

### 构建和安装软件包

切换到编译目录，解压缩构建文件。如果是 Git 方式获取，无需解压。

```
$ cd ~/builds
$ tar -xvzf foo.tar.gz

```

这时应该出现了一个新的名为“foo”的目录。进入目录并检查脚本文件：

**警告:** **务必认真检查所有文件！**`cd` 到新建立的目录,然后仔细检查每个文件确保没有恶意或危险代码. `PKGBUILD`和所有`.install`文件都是shell脚本文件，包含若干函数，由`makepkg`调用并执行。这些函数可以调用**任何**命令，可能包含恶意或危险代码。`makepkg`通过fakeroot（意为“假root”）执行这些命令(所以不要以root用户运行makepkg)，能在一定程度防止恶意代码损坏系统，但还是小心为好。如有疑问，可以到论坛或邮件列表询问。

```
$ cd foo
$ less PKGBUILD
$ less foo.install

```

接下来开始生成软件包。检查文件后，执行[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")（以普通用户权限）：

```
$ makepkg -si

```

`-s`/`--syncdeps` 表示自动执行[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装依赖关系。`-i`/`--install` 会安装软件包。

有些选项可能有用：

*   `-r`/`--rmdeps` 会移除只在构建时需要的软件包，不过重新编译时就要再安装了。
*   `-c`/`--clean` 会在构建结束时删除临时文件。如果需要调试构建过程这会十分有用。

**注意:** 本文所涵盖的内容十分有限。如果想要对软件包构建有更深了解，推荐阅读[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")和[ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")。

## 反馈

[AUR网站](https://aur.archlinux.org)的评论机制为用户提供了一种对PKGBUILD提建议的渠道。注意，最好不要在评论处贴自己的代码，因为代码很占地方，还很容易被新的评论刷掉。最好直接email通知维护人员，或者用[pastebin](/index.php/Pastebin "Pastebin")贴代码。

'*所有的* Arch用户都可以通过AUR Web界面为软件包投票.大多数软件包都有机会被TU收录进[community](/index.php/Community "Community")仓库.投票数是[community]仓库软件包选拔的重要依据之一。

## 分享和维护软件包

AUR不包含任何编译过的二进制包，用户上传[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")，供其他用户下载使用。所有软件包都是非官方的，使用风险自担。

### 提交软件包

**Warning:** 在提交前请先熟悉 [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") 及所有的"相关文章".违反相应规则的软件包可能不经警告被直接删除。

如果对自己的PKGBUILD缺乏信心，可以先把它贴到[AUR邮件列表](https://mailman.archlinux.org/mailman/listinfo/aur-general)，[论坛AUR版](https://bbs.archlinux.org/viewforum.php?id=4)或 [IRC 频道](/index.php/IRC_Channels "IRC Channels")，让大家帮你检查。

#### 提交软件包的规则

提交软件包时请遵循下列的规则:

*   **任何提交的 PKGBUILD 都不能编译已经位于官方二进制软件包仓库的程序。** 如果认为官方仓库的软件包已过期，请标记它。如果它有问题或者缺少功能，请反馈[bug 报告](https://bugs.archlinux.org/)。

	**唯一的例外**是和官方打包版本相比增加或开启了新的功能。这时 pkgname 列应该不同。例如加入了边栏支持的 `screen` 应该命名为 `screen-sidebar`，同时添加 `provides=('screen')` 以避免与官方仓库中的包冲突。

*   查看AUR中是否已有相同软件包。如果已经有人维护某软件包，其他用户的提交将以评论形式报告给维护人员。如果软件包无人维护或不存在，用户提交的软件包将被收录,别创建重复的包.
*   仔细检查上传的文件。编写PKGBUILD前务必阅读[Arch软件打包标准](/index.php/Arch_packaging_standards_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch packaging standards (简体中文)")。劣质的PKGBUILD会影响软件的正常使用，不要指望别人会因为你糟糕的PKGBUILD浪费了他们的时间而收到感谢。
*   包含二进制文件或质量差的PKGBUILD有可能无提醒地被直接删除。
*   确保你的软件包有人需要，有人会用这个软件包吗?它非常特别吗?如果有一些人觉得它有用,就提交它.
*   AUR 官方软件仓库中放置通用软件和软件相关内容，包括：可执行文件、配置文件、软件的在线文档和软件直接使用的数据。
*   上传软件包之前务必掌握打包过程，自己打几个包练练手。
*   请在 `PKGBUILD` 最上端加入包含当前维护者和过去的维护者（作为贡献者）的信息，记得对邮件地址进行必要的处理以避免被垃圾邮件骚扰。然后移除所有不必要的行。例如：

	如果你从其它人接手了一个 PKGBUILD ，像这样把你的名字和邮件地址加到最上面。

```
# Maintainer: Your Name <address at domain dot tld>

```

	如果在你之前有其他的维护者，请将它们添加到贡献者中。（如果提交者不是你也如此。）：

```
# Maintainer: Your name <address at domain dot tld>
# Maintainer: Other maintainer's name <address at domain dot tld>
# Contributor: Previous maintainer's name <address at domain dot tld>	
# Contributor: Original submitter's name <address at domain dot tld>

```

#### 认证

要向AUR间写入软件包,用户需要创建一个[SSH key](/index.php/SSH_keys "SSH keys").将公钥 `.ssh/foo.pub` 导入到用户账户的 *我的帐号*一节,然后为 `aur.archlinux.org` 指定私钥的位置,例如:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

建议为 AUR 创建一个新的密钥(而不是用旧的)，这样出问题时可以直接废除密钥。在输入密钥时可以导入多个公钥，每行一个。

#### 创建软件包

要创建新的空本地 Git 仓库，可以用 `git clone` 相同名称的远程仓库，如果 AUR 中还不存在软件包，将会看到下面警告：

 `$ git clone git+ssh://aur@aur.archlinux.org/*package_name*.git` 
```
Cloning into '*package_name*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.

```

**Note:** 即使 AUR 中的软件包被删除 Git 仓库也不会删除，所以你可能会发现 clone 一个 AUR 中还不存在的软件包时不会看到这个警告。

如果已经有了 git 仓库，可以远程创建 AUR git 并获取它：

```
$ git remote add *remote_name* git+ssh://aur@aur.archlinux.org/*package_name*.git
$ git fetch *remote_name*

```

`*remote_name*` 是需要创建的仓库，参考 [Git#Using remotes](/index.php/Git#Using_remotes "Git")。

第一次 *push* 之后，AUR 上就会出现软件包。可以将源代码加入本地 Git 仓库，参考 [#维护软件包](#.E7.BB.B4.E6.8A.A4.E8.BD.AF.E4.BB.B6.E5.8C.85).

**Warning:** AUR 提交会通过 git 用户名和邮件定义作者，一旦提交很难改变。如果需要修改用户名和密码，请通过 `git config user.name [...]` 和 `git config user.email [...]` 修改。请一定在推送前进行检查。

#### 提交和更新软件包

要更新软件包的方法和创建类似，注意要确保每次推送都包含顶层目录的 `PKGBUILD` 和 [.SRCINFO](/index.php/.SRCINFO_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) ".SRCINFO (简体中文)")。

用 `git add` 将它们和其它需要的文件 (例如 `.install` 和像 `.patch` 一类的源码文件)添加到工作区域("staging area"),用 `git commit` 提交更改,最后用 `git push` 上传到AUR.

例如:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m 'Useful commit message'
$ git push origin master

```

**Warning:** 不想以全局身份提交?记得通过`git config user.name [...]` 和 `git config user.email [...]` 编辑自己的本地身份! 这可能会导致很难追踪提交历史, 参阅: [FS#45425](https://bugs.archlinux.org/task/45425). 在提交之前复查你的更改!

要更新某个软件包,修改需要的文件然后运行相应的操作把更改提交到AURgit仓库:

```
$ mksrcinfo
$ git commit -am 'Update to *1.0.0-2'*
$ git push

```

参阅 [Git](/index.php/Git "Git") 获得更多信息.

**Tip:** 如果你忘记在提交中包含`.SRCINFO`,即使你稍后补上AUR也会拒绝你的提交(因为每一次提交中都包含[.SRCINFO](/index.php/.SRCINFO ".SRCINFO")) 要解决这个问题,你可以使用[git rebase](https://git-scm.com/docs/git-rebase) 中的 `--root` 选项或是 [git filter-branch](https://git-scm.com/docs/git-filter-branch) 中的 `--tree-filter` 选项.

### 维护软件包

*   要更新软件包，重新提交更新过的PKGBUILD即可。
*   阅读其他用户的反馈，并试着听从建议改进软件包,这是个学习的过程!
*   升级软件包后，不要在评论中加入版本更新信息，这些信息会冲淡更重要的用户评论。[AUR helpers](/index.php/AUR_helpers "AUR helpers") 更适合检查更新。
*   不要提交软件包后就放任不管！PKGBUILD的和维护升级是用户自己的责任。
*   发觉自己没有精力维护某个软件包?可以通过AURweb界面 `disown` 一个软件包或是在AUR邮件列表发条消息. ["孤儿包"](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=&outdated=&SB=n&SO=a&PP=50&do_Orphans=Orphans) 用来表示那些所有维护者都 `disown` 的软件包.

### 其他事项

*   取消维护权限和删除软件包的请求可以通过右边"Package actions" 的 "File Request" 链接执行。这会给当前的维护者和 [aur-requests 邮件列表](https://mailman.archlinux.org/mailman/listinfo/aur-requests)自动发送邮件通知。[Trusted Users](/index.php/Trusted_Users "Trusted Users") 会接受或拒绝请求。
*   在aur-general邮件列表请求移除软件包或弃置他人的软件包，受信用户会作出决定。
*   请求中需包含**软件包名称和AUR页面链接**。
*   如果email通知当前软件包维护人员后两个星期内没有答复，弃置请求将得到许可。
*   **软件包尚无法改名**。如果需要，可以提交新软件包，并在邮件列表请求移除旧软件包。
*   移除请求格式如下（务必用英语）：
    *   软件包名称和AUR页面链接
    *   删除原因，至少一句话
        **注意：**不要以为在软件包评论处贴出移除理由就足够了，受信用户只会阅读邮件列表上的信息。
    *   详情说明，比如是因为修改名称而移除还是其他什么的。
    *   如果是合并请求，请注明需要合并到的软件包。

删除的条件比较严格。如果无法通过，弃置即可,其他用户可能会接手。

## AUR3 软件包的Git仓库

因为AUR的后端迁移到[Git](/index.php/Git "Git"),从2015年8月8日起无人维护的包已从AUR中移除,可以在Github上找到AUR3软件包归档: [AUR Archive](https://github.com/aur-archive)

## AUR translation

参阅 [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) 获得关于创建和维护AUR web界面翻译的详细信息.

## FAQ

### AUR是什么？

AUR 是 Arch User Repository （Arch用户软件仓库）的缩写，是Arch用户上传并分享软件、共享库等等的[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")的地方。用户可以为喜欢的软件包投票，票数多的将有机会进入[community]仓库并以二进制包的形式提供。

### 什么样的软件包能被放到 AUR?

AUR中的软件包仅是编译脚本，只要内容符合软件版权，满足上面提到的软件包要求，就能够放入。有时候，下载的链接具有 "you may not link" 条款，这时就不能提供下载链接，而是要用程序名称代替，用户需要用其它方式提前获取受限制的源代码。有疑问请及时询问。

### 如何给 AUR 中的软件包投票?

注册[AUR 网站](https://aur.archlinux.org/)账户，在浏览软件包时会看到投票选项。登录后，还可以通过 [aurvote](https://aur.archlinux.org/packages/aurvote/) 投票.

### 受信用户（或TU）是什么？

[受信用户](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")（TU，Trusted User）是选拔出的监督AUR和[community]仓库的用户。他们维护着[community]的热门软件，并维持AUR运转。

### Arch User Repository和[community]仓库有何区别？

Arch User Repository是储存所有用户提交的PKGBUILD的地方，软件包需通过[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")手动生成。吸引足够多的 community interest 及 TU 支持的 PKGBUILD 会被收录进[community]仓库（由TU维护），以二进制软件包形式提供，可以由[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装。

### AUR的某个软件包过时了，该怎么办？

点击软件包页面的“Flag Out-of-date”（中文版为“标记为过期”）即可。如果长期未更新，最好email通知维护人员。如果还是没有得到答复，如果这些软件包标记为过期的时间超过 3 个月，长期未更新，可以在aur-general要求弃置软件包，邮件中请包含过期的信息。

同时，你可以自行在本地更新 PKGBUILD - 通常软件更新不需要修改编译或打包方式，更新 `pkgver` 或 `source` 数组就足够了。

**Note:** [VCS 软件包](/index.php/VCS_package_guidelines "VCS package guidelines") 在 pkgver 变化时并不会过时，所以不要标记它们，AUR 维护者不应该仅为了 pkgver 进行提交。

### `makepkg`无法构建某个软件包怎么办？

你很可能忘了点啥。

1.  [更新系统](/index.php/Pacman#Upgrading_packages "Pacman")，系统软件过时可能导致软件包构建失败。
2.  确保安装了“base”和“base-devel”软件包组。
3.  在执行`makepkg`时，使用`-s`选项检查依赖关系。

先阅读 PKGBUILD 和 AUR 页面的评论。可能导致编译错误的还有不正确的CFLAGS、LDFLAGS和MAKEFLAGS设置。也有可能是PKGBUILD写错了，如果确实如此，请通知包维护人员。例如在 AUR 页面留言。

### 如何编写PKGBUILD？

建议阅读[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")一文。先检查AUR看看有没有相同软件包，不要再造轮子。

### 我想提交一个PKGBUILD，希望别人帮忙检查错误。

你可以在aur-general贴出你的PKGBUILD并征求他人意见，或到irc.freenode.net上的[IRC频道](/index.php/ArchChannel "ArchChannel")#archlinux-aur寻求帮助。也可以自己使用[namcap](/index.php?title=Namcap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Namcap (简体中文) (page does not exist)")检查PKGBUILD和软件包。

### PKGBUILD（AUR软件包）怎样才能被收录到community软件仓库？

一般至少需要10票，并且要有TU（受信用户）愿意维护，否则即便有上千票也不会收录。当然，如果某个受信用户愿意维护一个软件包的话,投票数往往不是决定因素。

一些流行的软件包未被收录的原因一般是：

*   Arch Linux的软件仓库中已经有了别的版本。
*   那个软件包的功能只和AUR相关（(e.g. 是个 [AUR helper](/index.php/AUR_helper "AUR helper"))）
*   没有再发布的授权许可

另见 [Rules for Packages Entering the community Repo](/index.php/AUR_Trusted_User_Guidelines#Rules_for_Packages_Entering_the_.5Bcommunity.5D_Repo "AUR Trusted User Guidelines").

### 如何加速编译？

如果经常用gcc编译同样的代码，[ccache](/index.php/Ccache_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ccache (简体中文)")对你可能有很大帮助。

### foo 和 foo-git 的区别是什么?

很多AUR软件包都包含稳定版本和开发版本.开发版本一般都会有像 `-cvs`, `-svn`, `-git`, `-hg`, `-bzr` 或者 `-darcs`一样的后缀. 开发版本并不是为日常使用而设计的,不过可能包含新功能或者bug修复.因为要从上游获取最新的源代码,所以当运行`makepkg`时版本号可能会发生变化.而且会跳过对源代码的完整性效验.

同时请参阅 [Enhancing Arch Linux Stability#Avoid development packages](/index.php/Enhancing_Arch_Linux_Stability#Avoid_development_packages "Enhancing Arch Linux Stability").

### 为啥某个软件包从AUR消失了?

软件包可能因为不满足[#提交软件包的规则](#.E6.8F.90.E4.BA.A4.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84.E8.A7.84.E5.88.99)或是其它原因而被删除,你可以在 [aur-requests archives](https://lists.archlinux.org/pipermail/aur-requests/) 找到对应删除记录的归档.

如果某个软件包在AUR3时期存在,它可能没 [迁移到AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). 参阅[#AUR3 软件包的Git仓库](#AUR3_.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84Git.E4.BB.93.E5.BA.93) 获得获取他们的更多信息.

### 我要怎么找出从AUR里消失的软件包?

可以用下面的命令实现:

```
$ for pkg in $(pacman -Qqm); do cower -s $pkg &>/dev/null || echo "$pkg not in AUR"; done

```

(来自 [https://bbs.archlinux.org/viewtopic.php?id=202160](https://bbs.archlinux.org/viewtopic.php?id=202160))

### 如何查找已经安装但是从 AUR 消失的软件包

通过网络访问检查：: $ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

### 想知道 AUR 里都有啥 ？

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   使用来自 [python3-aur](https://aur.archlinux.org/packages/python3-aur/) 的 `aurpkglist` 。

## 另请参阅

*   [AUR Web](https://aur.archlinux.org)
*   [AUR 邮件列表](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")
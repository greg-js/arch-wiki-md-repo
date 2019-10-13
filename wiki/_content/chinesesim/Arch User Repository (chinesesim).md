相关文章

*   [makepkg (简体中文)](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   [pacman (简体中文)](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [PKGBUILD (简体中文)](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")
*   [.SRCINFO (简体中文)](/index.php/.SRCINFO_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) ".SRCINFO (简体中文)")
*   [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface")
*   [AUR Trusted User Guidelines (简体中文)](/index.php/AUR_Trusted_User_Guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR Trusted User Guidelines (简体中文)")
*   [Official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")
*   [Arch Build System (简体中文)](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")
*   [Creating packages (简体中文)](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")
*   [AUR helpers (简体中文)](/index.php/AUR_helpers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR helpers (简体中文)")

**翻译状态：** 本文是英文页面 [Arch_User_Repository](/index.php/Arch_User_Repository "Arch User Repository") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-02-03，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=565667)可以查看翻译后英文页面的改动。

[Arch 用户软件仓库](https://aur.archlinux.org)（Arch User Repository，AUR）是为用户而建、由用户主导的 Arch 软件仓库。AUR 中的软件包以软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")）的形式提供，用户自己通过 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 生成包，再由 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装。创建 AUR 的初衷是方便用户维护和分享新软件包，并由官方定期从中挑选软件包进入 [community](/index.php/Community_repository "Community repository") 仓库。本文介绍用户访问和使用 AUR 的方法。

许多官方仓库软件包都来自 AUR。通过 AUR，大家相互分享新的软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 和其他相关文件）。用户还可以为软件包投票。如果一个软件包投票足够多、没有协议问题、打包质量好，那么它就很有希望被收录进官方 *community* 仓库（以后就可以直接通过 [pacman](/index.php/Pacman "Pacman") 或 [abs](/index.php/ABS "ABS") 安装了）。

**警告:** AUR 中的软件包是由其他用户编写的，使用这些文件的风险由您自行承担。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 入门](#入门)
*   [2 历史](#历史)
    *   [2.1 AUR3 软件包的 Git 仓库](#AUR3_软件包的_Git_仓库)
*   [3 安装软件包](#安装软件包)
    *   [3.1 准备](#准备)
    *   [3.2 获取软件包构建所需文件](#获取软件包构建所需文件)
    *   [3.3 构建和安装软件包](#构建和安装软件包)
*   [4 反馈](#反馈)
*   [5 分享和维护软件包](#分享和维护软件包)
    *   [5.1 提交软件包](#提交软件包)
        *   [5.1.1 提交软件包的规则](#提交软件包的规则)
        *   [5.1.2 认证](#认证)
        *   [5.1.3 创建软件包仓库](#创建软件包仓库)
        *   [5.1.4 提交和更新软件包](#提交和更新软件包)
    *   [5.2 维护软件包](#维护软件包)
    *   [5.3 其他事项](#其他事项)
*   [6 Web 接口翻译](#Web_接口翻译)
*   [7 评论语法](#评论语法)
*   [8 FAQ](#FAQ)
    *   [8.1 AUR 是什么？](#AUR_是什么？)
    *   [8.2 什么样的软件包能被放到 AUR？](#什么样的软件包能被放到_AUR？)
    *   [8.3 如何给 AUR 中的软件包投票？](#如何给_AUR_中的软件包投票？)
    *   [8.4 受信用户（TU）是什么？](#受信用户（TU）是什么？)
    *   [8.5 Arch User Repository 和 community 仓库有何区别？](#Arch_User_Repository_和_community_仓库有何区别？)
    *   [8.6 AUR 的某个软件包过时了，我该怎么办？](#AUR_的某个软件包过时了，我该怎么办？)
    *   [8.7 makepkg无法构建某个软件包，我该怎么办？](#makepkg无法构建某个软件包，我该怎么办？)
    *   [8.8 ERROR: One or more PGP signatures could not be verified! 我该怎么办？](#ERROR:_One_or_more_PGP_signatures_could_not_be_verified!_我该怎么办？)
    *   [8.9 如何编写 PKGBUILD？](#如何编写_PKGBUILD？)
    *   [8.10 我想提交一个 PKGBUILD，希望别人帮忙检查错误。](#我想提交一个_PKGBUILD，希望别人帮忙检查错误。)
    *   [8.11 PKGBUILD（AUR 软件包）怎样才能被收录到 community 软件仓库？](#PKGBUILD（AUR_软件包）怎样才能被收录到_community_软件仓库？)
    *   [8.12 如何加速编译？](#如何加速编译？)
    *   [8.13 foo 和 foo-git 的区别是什么？](#foo_和_foo-git_的区别是什么？)
    *   [8.14 为啥某个软件包从 AUR 消失了？](#为啥某个软件包从_AUR_消失了？)
    *   [8.15 我要怎么找出从 AUR 里消失的软件包？](#我要怎么找出从_AUR_里消失的软件包？)
    *   [8.16 想知道 AUR 里都有啥 ？](#想知道_AUR_里都有啥_？)
*   [9 另请参阅](#另请参阅)

## 入门

用户可以从 [AUR 网站](https://aur.archlinux.org)下载 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")。[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 使用该文件生成软件包，最后由 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装。

*   确保 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组已被完全安装 (`pacman -S --needed base-devel`)。
*   浏览 [#FAQ](#FAQ) 获取常见问题的答案。
*   在 `/etc/makepkg.conf` 中，针对处理器使用合适的 CFLAGS、CXXFLAGS 编译参数，以优化软件包编译。通过设置 MAKEFLAGS 变量，可以启用多线程编译，使用多核心处理器的话，将大大减少编译时间。详情参见 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")。
*   也可以通过 SSH 连接到 AUR: 运行 `ssh aur@aur.archlinux.org help` 获得可用指令的列表。

## 历史

最初，人们上传[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")、附属文件、编译好的软件包到 `ftp://ftp.archlinux.org/incoming`。文件一直存放在那里，直到[软件包维护人员](/index.php/Package_Maintainer "Package Maintainer")发现并收录。

后来，出现了受信用户软件仓库，部分社区用户拥有了建设自己的软件仓库的权力。以这个仓库为基础，为使其更加灵活易用，AUR 出现了。事实上，AUR 维护人员现在仍被称为受信用户（简称 TU）。

从 2015-06-08 到 2015-08-08，AUR 版本从 3.5.1 到 4.0.0，Git 仓库成为 PKGBUILD 的发布方式。

当时现存的所有软件包都会被删除，除非维护者将他们手动迁移到新的架构上。

### AUR3 软件包的 Git 仓库

Github 上的 [AUR Archive](https://github.com/aur-archive) 储存了迁移过程中的所有 AUR3 软件包仓库。 除此之外，[aur3-mirror](https://github.com/felixonmars/aur3-mirror/) 也提供了同样的内容。

## 安装软件包

从 AUR 安装软件包并不困难。基本步骤如下：

1.  从 AUR 下载包含 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 和其他安装文件（比如 [systemd](/index.php/Systemd "Systemd") 和补丁，通常不是实际代码）的 tar 包。
2.  用命令 `tar -xvf packagename.tar.gz` 解包到一个仅用于编译 AUR 的空闲文件夹。
3.  验证 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 和其它相关文件，确保其中不含有恶意代码。
4.  在上述文件夹中运行 `makepkg -si`。命令会自动调用 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 解决依赖关系，然后下载代码、编译并打包。然后安装软件包。

**注意:** AUR是不受支持的，所以更新这些软件包是*您的责任*而不是 pacman 的。如果官方仓库中的软件包更新了，您可能需要重建相关的 AUR 软件包。

### 准备

首先确定完整地安装了 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组，其中包括 [make](https://www.archlinux.org/packages/?name=make) 和其他编译工具：

**注意:** AUR 中的软件包都会假定您已经安装了 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组(例如它们不会将这个组中的软件包列入依赖列表）。

然后，选择一个合适的编译目录。这个目录用作生成软件包时的工作目录，任何空白目录都可以。下面的示例中使用 `~/builds` 作为编译目录。

### 获取软件包构建所需文件

通过搜索或任何方式，在 AUR 中找到要安装的软件包。阅读介绍，检查软件包更新日期，看看别人的评论。

确认无误后，通过下面三种方法可以获取到所需的编译文件：

*   在“Package Details”中，找到“Git Clone URL”，然后下载 [Git](/index.php/Git "Git") 仓库。这也是推荐的方法。

```
$ git clone https://aur.archlinux.org/*package_name*.git

```

	这样做的其中一个好处是您以后可以通过 `git pull` 的形式来更新。

*   从软件包信息页面点击“Download snapshot”（中文页面翻译做“下载快照”），保存压缩包到编译目录。

```
$ tar -xvf *package_name*.tar.gz

```

*   从终端下载：

```
$ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/*package_name*.tar.gz

```

### 构建和安装软件包

切换到含有软件包的 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 文件的目录：

```
$ cd *package_name*

```

**警告:** **务必认真检查所有文件！** `cd` 到新建立的目录，然后仔细检查每个文件确保没有恶意或危险代码。`PKGBUILD` 和所有 `.install` 文件都是 shell 脚本文件，包含若干函数，由 `makepkg` 调用并执行。这些函数可以调用**任何**命令，可能包含恶意或危险代码。`makepkg` 通过 fakeroot（意为“假root”）执行这些命令（所以不要以 root 用户运行makepkg），能在一定程度防止恶意代码损坏系统，但还是小心为好。如有疑问，可以到论坛或邮件列表询问。

查看所有提供的文件中的内容。例如使用 *less* 查看 `PKGBUILD`：

```
$ less PKGBUILD

```

**提示：** 如果您正在更新软件包，您可能需要查看最后一次提交以来的变动。

*   您可以使用 `git show` 来查看最后一次提交之后的变动。
*   您也可以使用 `git difftool @~..@ vimdiff`。使用 *vimdiff* 的好处是您可以查看到带有文件变动指示的所有文件内容。

接下来开始生成软件包。检查文件后，执行 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") （以普通用户权限）：

```
$ makepkg -si

```

*   `-s`/`--syncdeps` 表示自动执行 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装依赖关系。如果软件包依赖其他的 AUR 软件包，您需要先手动安装依赖。
*   `-i`/`--install` 会在顺利构建软件包之后安装软件包。除此之外，您还可以使用 `pacman -U *package*.pkg.tar.xz` 来手动安装软件包。

其他可能有用的选项：

*   `-r`/`--rmdeps` 会移除只在构建时需要的软件包，不过重新编译时就要再安装了。
*   `-c`/`--clean` 会在构建结束时删除临时文件。如果需要调试构建过程这会十分有用。

**注意:** 本文所涵盖的内容十分有限。如果想要对软件包构建有更深了解，推荐阅读 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 和 [ABS](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")。

## 反馈

[AUR 网站](https://aur.archlinux.org)的评论机制为用户提供了一种对 PKGBUILD 提建议的渠道。注意，最好不要在评论处贴自己的代码，因为代码很占地方，还很容易被新的评论刷掉。最好直接 email 通知维护人员，或者用 [pastebin](/index.php/Pastebin "Pastebin") 贴代码。

**所有的** Arch 用户都可以通过 AUR Web 界面为软件包投票。大多数软件包都有机会被 TU 收录进 [community](/index.php/Community_repository "Community repository") 仓库。投票数是 community 仓库软件包选拔的重要依据之一。

## 分享和维护软件包

AUR不包含任何编译过的二进制包，用户上传 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")，供其他用户下载使用。所有软件包都是非官方的，使用风险自担。

### 提交软件包

**警告:** 在提交前请先熟悉 [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") 及所有的"相关文章"。违反相应规则的软件包可能不经警告被直接删除。

如果对自己的 PKGBUILD 缺乏信心，可以先把它贴到[AUR 邮件列表](https://mailman.archlinux.org/mailman/listinfo/aur-general)，[论坛 AUR 版](https://bbs.archlinux.org/viewforum.php?id=4)或 [IRC 频道](/index.php/IRC_Channels "IRC Channels")，让大家帮您检查。

#### 提交软件包的规则

提交软件包时请遵循下列的规则:

*   仔细检查上传的文件。编写PKGBUILD前务必阅读 [Arch软件打包标准](/index.php/Arch_packaging_standards_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch packaging standards (简体中文)")。劣质的 PKGBUILD 会影响软件的正常使用，不要指望别人会因为您糟糕的 PKGBUILD 浪费了他们的时间而收到感谢。
*   任何提交的 PKGBUILD 都不能编译**已经**位于**官方**二进制软件包**仓库**的程序。如果认为官方仓库的软件包已过期，请标记它。如果它有问题或者缺少功能，请反馈 [bug 报告](https://bugs.archlinux.org/)。

	**唯一的例外**是和官方打包版本相比增加或开启了**新的功能**或者使用了不同的**补丁**。这时需要修改 pkgname 来表示新增的功能。例如加入了边栏支持的 `screen` 应该命名为 `screen-sidebar`。此外还需要同时添加 `provides=('screen')` 以避免与官方仓库中的包冲突。

*   **检查 AUR** 中是否**已有**相同软件包。如果已经有人维护某软件包，可以以评论的形式将变化报告给维护人员。如果软件包无人维护或不存在，用户提交的软件包将被认领。别创建重复的包。
*   确保您的软件包**有人需要**，有人会用这个软件包吗？它非常特别吗？如果有一些人觉得它有用，就提交它。

	AUR 和官方软件仓库中计划放置通用软件和软件相关的内容，包括：可执行文件、配置文件、软件的在线/离线文档和软件直接使用的媒体数据。

*   不要在 AUR PKGBUILD 中使用 `replaces`，除非这个软件包将要被重命名（例如当 *Ethereal* 变成 *Wireshark* 时）。如果这个软件包是已经存在的软件包的另一版本，使用 `conflicts` （或者如果这个软件包被其他软件需要时，使用 `provides`）。两者的主要区别是：在 pacman 同步（-Sy）之后，如果遇到与 `replaces` 匹配并已经安装的软件包时，pacman 会立刻想去替换它。而 `conflicts` 则在安装软件包时进行替换。
*   如果源代码是可取得的，请**避免**提交**二进制文件**。AUR不应当包含 `makepkg` 创建的二进制包，也不应当包含文件列表。
*   请在 `PKGBUILD` 最上端加入包含当前**维护者**和过去的**贡献者**的信息，记得对邮件地址进行必要的处理以避免被垃圾邮件骚扰。然后移除所有不必要的行。例如：

	如果您从其它人接手了一个 PKGBUILD，像这样把您的名字和邮件地址加到最上面。

```
# Maintainer: Your Name <address at domain dot tld>

```

	如果在您之前有其他的维护者，请将它们添加到贡献者中。如果您是协同维护者，也请加上现在的其他维护者。

```
# Maintainer: Your name <address at domain dot tld>
# Maintainer: Other maintainer's name <address at domain dot tld>
# Contributor: Previous maintainer's name <address at domain dot tld>	
# Contributor: Original submitter's name <address at domain dot tld>

```

#### 认证

要向 AUR 写入软件包，用户需要创建一个 [SSH key](/index.php/SSH_keys "SSH keys") 。将公钥导入到用户账户的*我的帐号*一节，然后为 `aur.archlinux.org` 指定私钥的位置，例如：

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

建议为 AUR 创建一个新的密钥（而不是用旧的），这样出问题时可以直接废除密钥：

```
$ ssh-keygen -f ~/.ssh/aur

```

**提示：** 在输入公钥时可以通过换行的方式设置添加多个公钥。

#### 创建软件包仓库

如果您正在[创建新的软件包](/index.php/Creating_packages "Creating packages")，请通过克隆所需的 [pkgbase](/index.php/PKGBUILD#pkgbase "PKGBUILD") 的方式建立一个远程 AUR 仓库和本地 Git 仓库。如果软件包还不存在，则会出现以下预料之中的警告：

 `$ git clone ssh://aur@aur.archlinux.org/*pkgbase*.git` 
```
Cloning into '*pkgbase*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**注意:** 即使 AUR 中的软件包被删除 Git 仓库也不会删除，所以您可能会发现 clone 一个 AUR 中还不存在的软件包时不会看到这个警告。

如果您已经有一个软件包了，如果它不是 Git 仓库的话，[初始化](/index.php/Git#Getting_a_Git_repository "Git")并添加远程 AUR 地址：

```
$ git remote add *label* ssh://aur@aur.archlinux.org/*pkgbase*.git

```

然后从远程[获取](/index.php/Git#Using_remotes "Git")文件并初始化。

**提示：** 使用[推送和变基](https://git-scm.com/docs/git-pull#git-pull---rebasefalsetruemergespreserveinteractive)来解决 `*pkgbase*` 匹配到已删除软件包的冲突问题。

#### 提交和更新软件包

**警告:** 不想以全局身份提交？记得通过 `git config user.name [...]` 和 `git config user.email [...]` 编辑自己的本地身份！

当释出新版本的软件时，更新 [pkgver](/index.php/PKGBUILD#pkgver "PKGBUILD") 或者 [pkgrel](/index.php/PKGBUILD#pkgrel "PKGBUILD") 变量来提示所有的用户更新。如果仅仅是对 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 的小修改（例如修正笔误），请不要更新这些变量。

无论何时 `PKGBUILD` 的元数据发生变动（例如更新了 `pkgver()`），都需要重新生成 [.SRCINFO](/index.php/.SRCINFO_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) ".SRCINFO (简体中文)") 。否则AUR不会显示更新后的版本号。

要上传或者更新一个软件包，*至少*要[添加](/index.php/Git#Staging_changes "Git") `PKGBUILD` 和 `.SRCINFO` 和其他所有新增的或者修改过的辅助文件（例如 [*.install*](/index.php/PKGBUILD#install "PKGBUILD") 文件或者如[补丁](/index.php/Patching_packages "Patching packages")之类的[本地源码文件](/index.php/PKGBUILD#source "PKGBUILD")），[提交](/index.php/Git#Committing_changes "Git")，最后[推送](/index.php/Git#Push_to_a_repository "Git")这些变动到AUR上。

例如:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*useful commit message*"
$ git push

```

**注意:** 如果您忘记在首次提交中包含 `.SRCINFO`，您可以使用 [rebasing with --root](https://git-scm.com/docs/git-rebase#git-rebase---root) 或是 [filtering the tree](https://git-scm.com/docs/git-filter-branch#git-filter-branch---tree-filterltcommandgt) 使得 AUR 接受您的第一次推送

**提示：** 为了保持工作目录和提交尽可能的干净，可以创建 [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) 文件来排除所有文件，然后再按需添加文件。

### 维护软件包

*   阅读其他用户的反馈，并试着听从建议改进软件包，这是个学习的过程！
*   升级软件包后，不要在评论中加入版本更新信息，这些信息会冲淡更重要的用户评论。
*   不要提交软件包后就放任不管！检查更新并改进 PKGBUILD 是维护者的责任。
*   发觉自己不再想维护某个软件包？可以通过 AUR web 界面 `disown` 一个软件包或是在 AUR 邮件列表发条消息。如果这个包的所有维护者都disown，那么它就会变成一个 [“orphaned”](https://aur.archlinux.org/packages/?SB=n&do_Orphans=Orphans) 软件包.

### 其他事项

取消维护权限、删除、合并请求可以通过右侧 "Package actions" 的 "File Request" 链接执行。这会给当前的维护者和 [aur-requests 邮件列表](https://mailman.archlinux.org/mailman/listinfo/aur-requests)自动发送邮件通知。[Trusted Users](/index.php/Trusted_Users "Trusted Users") 会接受或拒绝请求。

*   如果现在的维护者在两周之内没有反应，orphan 请求就会通过。
*   合并请求会删除软件包 base，并将现有的投票数、评论转移到另一个软件包 base 中。将要合并到的软件包 base 是必须的。请注意这和 git merge 或者 GitLab 的 merge request 没有任何关系。
*   移除请求需要如下信息（务必用英语）：
    *   简要解释请求删除的原因。注意仅仅在软件包下评论是不足以指出需要删除的原因的。因为在 TU 采取行动之前，aur-requests 是唯一能取得这些信息的地方。
    *   支持删除原因的详细内容，例如这个软件包已经由另一个软件包提供。
    *   移除请求可能会被拒绝。例如如果您是维护者的话，您很有可能被建议 disown 这个软件包，以便让其他打包者认领。
    *   软件包被删除之后，它的 Git 仓库仍然能从 AUR 中被获取。

## Web 接口翻译

参阅 [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) 获得关于创建和维护 AUR web 界面翻译的详细信息。

## 评论语法

评论支持 [Python-Markdown](https://python-markdown.github.io/) 语法。 它提供基本的 [Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown") 语法来格式化评论。请注意这一实现与[官方的语法](https://daringfireball.net/projects/markdown/syntax)有些[区别](https://python-markdown.github.io/#differences)。评论会被哈希进软件包的 Git 仓库，对 Flyspray 工单的引用会被自动转换成链接。长评论会被折叠并能根据需要展开。

## FAQ

### AUR 是什么？

AUR 是 Arch User Repository（Arch 用户软件仓库）的缩写，是 Arch 用户上传并分享软件、共享库等等的 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 的地方。用户可以为喜欢的软件包投票，票数多的将有机会进入community仓库并以二进制包的形式提供。

### 什么样的软件包能被放到 AUR？

AUR 中的软件包仅是编译脚本，只要内容符合软件版权，满足上面提到的软件包要求，就能够放入。有时候，下载的链接具有 "you may not link" 条款，这时就不能提供下载链接，而是要用程序名称代替，用户需要用其它方式提前获取受限制的源代码。有疑问请及时询问。

### 如何给 AUR 中的软件包投票？

注册[AUR 网站](https://aur.archlinux.org/)账户，在浏览软件包时会看到投票选项。登录后，还可以通过 [aurvote](https://aur.archlinux.org/packages/aurvote/)、[aurvote-git](https://aur.archlinux.org/packages/aurvote-git/) 或者 [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/) 投票。

此外，如果您已经按照上诉方法设立[ssh 认证](#认证)，您可以使用您的 ssh 密钥直接通过命令行投票。这意味着您不再需要保存或者输入您的 AUR 密码。

```
ssh aur@aur.archlinux.org vote <PACKAGE_NAME>

```

### 受信用户（TU）是什么？

[受信用户](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")（TU，Trusted User）是选拔出的监督 AUR 和 community 仓库的用户。他们维护着 community 的热门软件，并维持 AUR 运转。

### Arch User Repository 和 community 仓库有何区别？

Arch User Repository 是储存所有用户提交的 PKGBUILD 的地方，软件包需通过 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 手动生成。吸引足够多的 community interest 及 TU 支持的 PKGBUILD 会被收录进 community仓库（由 TU 维护），以二进制软件包形式提供，可以由 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装。

### AUR 的某个软件包过时了，我该怎么办？

点击软件包页面的“Flag Out-of-date”（中文版为“标记为过期”）即可。如果长期未更新，最好 email 通知维护人员。如果还是没有得到答复，如果这些软件包标记为过期的时间超过 3 个月，长期未更新，可以在 aur-general 要求弃置软件包，邮件中请包含过期的信息。

同时，您可以自行在本地更新 PKGBUILD - 通常软件更新不需要修改编译或打包方式，更新 `pkgver` 或 `source` 数组就足够了。

**Note:** [VCS 软件包](/index.php/VCS_package_guidelines "VCS package guidelines") 在 pkgver 变化时并不会过时，所以不要标记它们，AUR 维护者不应该仅为了 pkgver 进行提交。

### `makepkg`无法构建某个软件包，我该怎么办？

您很可能忘了点啥。

1.  [更新系统](/index.php/Pacman#Upgrading_packages "Pacman")，系统软件过时可能导致软件包构建失败。
2.  确保安装了 [base](https://www.archlinux.org/packages/?name=base) 和 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组。
3.  在执行`makepkg`时，使用`-s`选项检查依赖关系。

先阅读 PKGBUILD 和 AUR 页面的评论。可能导致编译错误的还有不正确的 CFLAGS、LDFLAGS 和 MAKEFLAGS 设置。也有可能是 PKGBUILD 写错了，如果确实如此，请通知包维护人员。例如在 AUR 页面留言。

为了检查 PKGBUILD 是否损坏，或者您的系统是否配置错误，您可以考虑在 chroot 环境中构建软件包。它会在一个干净的、只安装制定构建依赖、没有任何用户定制的 Arch Linux 环境中构建软件包。您需要安装 [devtools](https://www.archlinux.org/packages/?name=devtools) 并使用 `extra-x86_64-build` 替代 `makepkg`。对于 [multilib](/index.php/Multilib "Multilib") 软件包，运行 `multilib-build`。参见 [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") 以获得更多详细内容。如果在 chroot 环境中仍然构建失败，那么很有可能是 PKGBUILD 文件有些问题。

### ERROR: One or more PGP signatures could not be verified! 我该怎么办？

最有可能的情况是您没有所需的公钥来验证下载的文件。如果构建过程中下载了一个或者多个 .sig 文件， [makepkg 会自动验证对应的文件和它的签发人](/index.php/Makepkg#Signature_checking "Makepkg")。如果您没有所需的密钥，`makepkg` 就会无法进行验证。

推荐的解决办法是[手动](/index.php/GnuPG#Import_a_public_key "GnuPG")或者[从密钥服务器](/index.php/GnuPG#Use_a_keyserver "GnuPG")导入所需的公钥。通常来说，您能从 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 的 [validpgpkeys](/index.php/PKGBUILD#validpgpkeys "PKGBUILD") 部分找到所需公钥的指纹。

### 如何编写 PKGBUILD？

建议阅读[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")一文。先检查 AUR 看看有没有相同软件包，不要再造轮子。

### 我想提交一个 PKGBUILD，希望别人帮忙检查错误。

您可以在 aur-general 贴出您的 PKGBUILD 并征求他人意见，或到 irc.freenode.net 上的 [IRC频道](/index.php/ArchChannel "ArchChannel") #archlinux-aur 寻求帮助。也可以自己使用 [namcap](/index.php?title=Namcap_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Namcap (简体中文) (page does not exist)") 检查PKGBUILD和软件包。

### PKGBUILD（AUR 软件包）怎样才能被收录到 community 软件仓库？

一般至少需要 10 票，并且要有 TU（受信用户）愿意维护，否则即便有上千票也不会收录。当然，如果某个受信用户愿意维护一个软件包的话，投票数往往不是决定因素。

一些流行的软件包未被收录的原因一般是：

*   Arch Linux 的软件仓库中已经有了别的版本。
*   没有再发布的授权许可
*   那个软件包的功能只和 AUR 相关（(e.g. 是个 [AUR helper](/index.php/AUR_helper "AUR helper"))）

另见 [Rules for Packages Entering the community Repo](/index.php/AUR_Trusted_User_Guidelines#Rules_for_Packages_Entering_the_.5Bcommunity.5D_Repo "AUR Trusted User Guidelines").

### 如何加速编译？

参阅 [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg")。

### foo 和 foo-git 的区别是什么？

很多AUR软件包都包含稳定版本和开发版本。开发版本一般都会有像 `-cvs`、`-svn`、`-git`、`-hg`、`-bzr` 或者 `-darcs` 这样的后缀。 开发版本并不是为日常使用而设计的，不过可能包含新功能或者 bug 修复。因为要从上游获取最新的源代码，所以当运行 `makepkg` 时版本号可能会发生变化。而且会跳过对源代码的完整性效验。

同时请参阅 [System maintenance#Use proven software packages](/index.php/System_maintenance#Use_proven_software_packages "System maintenance")。

### 为啥某个软件包从 AUR 消失了？

有可能是 TU 认领了这个软件包，并把它收入到 [community](/index.php/Community_repository "Community repository") 仓库中了。

软件包可能因为不满足[#提交软件包的规则](#提交软件包的规则)或是其它原因而被删除，您可以在 [aur-requests archives](https://lists.archlinux.org/pipermail/aur-requests/) 找到对应删除记录的归档。

如果某个软件包在 AUR3 时期存在，它可能没 [迁移到 AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). 参阅 [#AUR3 软件包的 Git 仓库](#AUR3_软件包的_Git_仓库)获取关于它们的更多信息。

### 我要怎么找出从 AUR 里消失的软件包？

最简单的办法是检查软件包 AUR 页面的 HTTP 状态：

```
$ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

```

### 想知道 AUR 里都有啥 ？

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   使用来自 [python3-aur](https://aur.archlinux.org/packages/python3-aur/) 的 `aurpkglist` 。

## 另请参阅

*   [AUR Web 接口](https://aur.archlinux.org)
*   [AUR 邮件列表](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")
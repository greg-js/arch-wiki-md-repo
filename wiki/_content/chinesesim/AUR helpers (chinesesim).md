**翻译状态：** 本文是英文页面 [AUR helpers](/index.php/AUR_helpers "AUR helpers") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-10，点击[这里](https://wiki.archlinux.org/index.php?title=AUR+helpers&diff=0&oldid=532394)可以查看翻译后英文页面的改动。

**警告:** 这些工具都不是官方支持的,参见 [[1]](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310)。用户应当熟悉 [手动构建过程](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85 "Arch User Repository (简体中文)")，以方便排查问题。

在使用[Arch用户软件仓库](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")时，AUR工具可以自动完成某些任务。大多数工具可以自动下载包的PKGBUILD并构建软件包。大多数情况下，[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")不会为AUR软件包检查更新，所以一些工具也可以自动从AUR检查更新并再次构建新版本的软件包。请注意，即使软件包自身并没有更新，但由于某些库文件的更新，您可能仍需重新构建某些软件包、

由于AUR工具并不被官方支持，所以它们不在[官方软件仓库](/index.php/Official_repositories "Official repositories")中提供。

## Contents

*   [1 构建和搜索](#.E6.9E.84.E5.BB.BA.E5.92.8C.E6.90.9C.E7.B4.A2)
    *   [1.1 开发中](#.E5.BC.80.E5.8F.91.E4.B8.AD)
    *   [1.2 仅搜索](#.E4.BB.85.E6.90.9C.E7.B4.A2)
    *   [1.3 开发停止或有问题](#.E5.BC.80.E5.8F.91.E5.81.9C.E6.AD.A2.E6.88.96.E6.9C.89.E9.97.AE.E9.A2.98)
*   [2 图形化工具](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.B7.A5.E5.85.B7)
*   [3 库](#.E5.BA.93)
*   [4 维护](#.E7.BB.B4.E6.8A.A4)
*   [5 上传](#.E4.B8.8A.E4.BC.A0)

## 构建和搜索

**注意:** 在于[Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers")讨论之前，不要更改这部分的内容。

这些列的含义：

*   **文件检查**：默认不`[source](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Source "Help:Reading (简体中文)")` [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")，或者在`source`之前让用户有机会手动检查PKGBUILD。已知某些工具在用户可以检查PKGBUILD之前就执行了`source`，这会允许执行PKGBUILD中的恶意代码。**可选**意味着有一个命令行选项或者配置可以在执行`source`之前检查PKGBUILD。
*   **Clean build**：不会引入可能导致构建失败的新环境变量。
*   **原生pacman**：在代替[pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)执行pacman的命令（如`pacman-Syu`）时，默认情况遵守如下规则：
    *   不分割命令，例如`pacman -Syu`不会分为`pacman -Sy`和`pacman -S packages`来执行；
    *   直接使用`pacman`，而不是直接操作数据库或是使用`libalpm`；
    *   另外，不使用[可能有害的命令](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance")，例如`pacman -Ud`，`pacman -Rdd`，`pacman --ask`或`pacman --force`。

**警告:** 尽管有这些标准，但AUR helpers仍可能在某些方面与[pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)行为不同,特别对于[官方软件仓库](/index.php/Official_repositories "Official repositories")中的软件包。所以这些用法并不被支持或推荐。

*   **可靠的语法分析器**：有能力通过使用所提供的元数据（PRC/.SRCINFO）代替解析PKGBUILD以处理复杂包，例如[aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/)。
*   **可靠的求解器**：有能力正确处理复杂的依赖关系，例如[ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/)。
*   **包拆分**：有能力正确地构建和安装：
    *   对于有相同包基础的多个软件包，不重复构建和安装包基础，例如[clion](https://aur.archlinux.org/packages/clion/)。
    *   拆分依赖相同包基础的包（Split packages which depend on a package from the same package base）， 例如[libc++](https://aur.archlinux.org/packages/libc%2B%2B/) and [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/)。
    *   独立地拆分包，例如[python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/)和[python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/)。
*   **Git clone**：默认使用[git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1)从AUR获取相关文件。
*   **差异比较**：有检查包差异的能力。除了PKGBUILD，还包括对`.install`或`.patch`文件更改的检查。
*   **批量交互**：批量完成交互过程，特别是：

1.  检查PKGBUILD；
2.  显示要升级的包；
3.  解决包冲突和安装问题。

	星号表示功能需要手动启用。

*   **命令补全**：在列出的shell中支持命令补全。

**提示：**

*   表格按列的值排序。其中**是**或**不适用**优先于**部分**、**可选** 以及**否**，如果值相同，则按字母顺序排序。
*   **可选**意味着功能可用，但需要通过命令行选项或配置文件启用。**部分**意味着功能尚未完全实现，或者与标准有一些差别。

### 开发中

| 名称 | 语言 | 原生pacman | 文件检查 | Clean build | 可靠的语法分析器 | 可靠的求解器 | 包拆分 | Git clone | 差异比较 | 批量处理 | 命令补全 | 特性 |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | 是 | 是 | 是 | 是 | [是](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | 是 | 是 | 是 | 1，[2*，3*](https://github.com/polygamma/aurman#question-6) | bash，fish | 导入PGP密钥，按票数或欢迎度排序，显示新闻 |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | – | 是 | 是 | 是 | 是 | 是 | 是 | 是 | 1 | zsh | [vifm](/index.php/Vifm "Vifm")，[本地仓库](/index.php/Local_repository "Local repository")，[包签名](/index.php/Package_signing "Package signing")，[clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")支持，按票数或受欢迎度排序 |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | 是 | 是 | 是 | 是 | 是 | 是 | [是](https://github.com/Jguer/yay/pull/297) | [是](https://github.com/Jguer/yay/pull/447) | 1，[2*](https://github.com/Jguer/yay/commit/3bdb5343218d99d40f8a449b887348611f6bdbfc)，[3*](https://github.com/Jguer/yay/commit/ea5a94e0f8bb5f76879099e6d319c0c0102231c2) | bash，fish，zsh | 按票数排序，导入PGP密钥，[架构提示](https://github.com/Jguer/yay/commit/4bcd3a6297052714e91e3f886602ce5c12d15786) |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | [拆分](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) `-Syu` | 是 | [是](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | 是 | 是 | 是 | 是 | [是](https://github.com/kitsunyan/pakku/commit/396e9f44c4f5a79c7b9238835599387f6ff418fe) | 1 | bash，zsh | [ABS](/index.php/ABS "ABS")支持，AUR评论，导入PGP密钥 |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | [拆分](https://github.com/actionless/pikaur#pikaur) `-Syu` | 是 | 是 | 是 | 是 | [是](https://github.com/actionless/pikaur/commit/d409b958b4ff403d4fda06681231061854d32b3c) | 是 | 是 | 1，2，3 | bash，fish，zsh | [动态用户](http://0pointer.net/blog/dynamic-users-with-systemd.html)，[多语言](https://github.com/actionless/pikaur/tree/master/locale)，按票数或受欢迎度排序，显示新闻，[忽略错误](https://github.com/actionless/pikaur/commit/3688d828591d307c6864c3b5ad8c1f581396b865) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | [是](https://github.com/trizen/trizen/commit/9e7b40e110175ea5bc7a0fa002ffadbf1106704b) | 是 | 是 | [是](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | 是 | [部分](https://github.com/trizen/trizen/issues/46) | [是](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | 是 | 1* | bash，zsh，fish | 默认自动构建，使用`-G`以禁用，AUR评论 |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | 是 | 是 | 是 | 是 | 是 | 是 | 是 | 否 | 1 | bash，zsh | 信任管理，[ABS](/index.php/ABS "ABS")支持，Powerpill扩展 |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | [是](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | 可选 | 是 | 是 | 是 | [部分](https://github.com/Kwpolska/pkgbuilder/issues/39) | 是 | [否](https://github.com/Kwpolska/pkgbuilder/issues/36) | 1* | – | 默认自动构建，使用`-F`以禁用; 多语言 |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | – | 可选 | 是 | 是 | [部分](https://github.com/enckse/naaman/issues/19) | [部分](https://github.com/enckse/naaman/issues/20) | 是 | 否 | 1* | bash | 默认自动构建，使用`--fetch`以禁用，使用`-d`启用求解器 |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | [是](https://github.com/aurapm/aura/blob/master/aura/lib/Aura/Pacman.hs) | 可选 | 是 | [是](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | 否 | [否](https://github.com/aurapm/aura/issues/353) | [否](https://github.com/aurapm/aura/pull/346) | [部分](https://github.com/aurapm/aura/blob/89bf702bd0539fa757265c4c54ea2192155f85ed/aura/src/Aura/Pkgbuild/Records.hs) | 1* | bash，zsh | 默认自动构建，使用`--dryrun` 以禁用，[降级](/index.php/Downgrade "Downgrade")支持，多语言 |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | – | 可选 | 是 | 否 | 否 | 否 | 是 | 是 | 1* | – | 默认自动构建，使用`check`或`update`以禁用，[本地仓库](/index.php/Local_repository "Local repository")支持 |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | – | 可选 | 是 | 否 | 否 | [否](https://github.com/pbrisbin/aurget/issues/40) | 否 | [否](https://github.com/pbrisbin/aurget/issues/41) | – | bash，zsh | 按票数排序 |

### 仅搜索

| 名称 | 语言 | 文件检查 | 可靠的语法分析器 | 可靠的求解器 | Git clone | 命令补全 | 特性 |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | 是 | 是 | – | 是 | - | - |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | 是 | 是 | – | 可选 | bash | - |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | 是 | 是 | 是 | 否 | - | 显示构建顺序 |
| [cower](https://aur.archlinux.org/packages/cower/) | C | 是 | 是 | – | 否 | bash/zsh | 支持正则表达式，按票数受欢迎度排序 |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | 是 | 否 [[2]](https://github.com/archlinuxfr/package-query/issues/135) | – | – | - | - |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | 是 | 是 [[3]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | 否 | zsh | 支持[本地仓库](/index.php/Pacman/Tips_and_tricks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.87.AA.E5.BB.BA.E6.9C.AC.E5.9C.B0.E4.BB.93.E5.BA.93 "Pacman/Tips and tricks (简体中文)") |

### 开发停止或有问题

此表中的是已经停止开发的，或是在过去6个月内有未处理的**文件检查**，**Clean build**或是**原生pacman**的问题（查看[#构建和搜索](#.E6.9E.84.E5.BB.BA.E5.92.8C.E6.90.9C.E7.B4.A2))的项目。

| 名称 | 语言 | 原生pacman | 文件检查 | Clean build | 可靠的语法分析器 | 可靠的求解器 | 拆分包 | Git clone | 差异比较 | 批量处理 | 命令补全 | 特性 |
| [aurel](https://aur.archlinux.org/packages/aurel/) [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | – | 是 | – | – | – | – | 否 | – | – | – | Emacs插件，不自动构建 |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | [使用](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) `-Ud` | 是 | 是 | 是 | 是 | 是 | 是 | 是 | 1,3 | bash,zsh | 多语言, 按票数或受欢迎度排序 |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | 是 | 是 | 是 | 否 | 否 | 否 | 是 | 否 | – | – | 更新镜像列表显示新闻和AUR评论 |
| [spinach](https://aur.archlinux.org/packages/spinach/) [[6]](https://github.com/floft/spinach) | Bash | – | [是](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | 是 | 否 | 否 | 否 | 否 | 否 | – | – | – |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[7]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | – | 可选 | 是 | 否 | 否 | 否 | 否 | 否 | – | – | cower的包装 |
| [packer](https://aur.archlinux.org/packages/packer/) | Bash | 是 | 否 | 是 | 否 | 否 | 否 | 否 | 否 | – | – | – |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | 拆分 `-Syu` | 否 [[8]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[9]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | [否](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | 否 | [否](https://github.com/archlinuxfr/yaourt/issues/186) | [否](https://github.com/archlinuxfr/yaourt/issues/85) | 可选 | 可选 | 2 | bash,zsh,fish | 备份 ([更改pacman数据库！](https://github.com/archlinuxfr/yaourt/blob/5a82dfe/src/lib/alpm_backup.sh#L38)),ABS支持,显示AUR评论,多语言 |

## 图形化工具

**Warning:**

*   图形化的AUR工具通常针对于[基于Arch的发行版](/index.php/Arch-based_distributions "Arch-based distributions"). 在[Arch Linux](/index.php/Arch_Linux "Arch Linux") 中使用它们可能会导致系统故障，例如进行自动的[部分升级](/index.php/Partial_upgrades "Partial upgrades")。
*   如果某项工具有**已知的**有问题的行为，它将被标记为红色。

| 名称 | 语言 | GUI toolkit | 后端 | 注意 |
| [aarchup](https://aur.archlinux.org/packages/aarchup/) | C | GTK+ 2 | auracle | – |
| [argon](https://aur.archlinux.org/packages/argon/) | Python | GTK+ 3 | auracle, pacaur | – |
| [cylon](https://aur.archlinux.org/packages/cylon/) | Bash | TUI | auracle, trizen | – |
| [kalu](https://aur.archlinux.org/packages/kalu/) | C | GTK+ 3 | – | – |
| [pactray](https://aur.archlinux.org/packages/pactray/) | Python | GTK+3 | auracle | – |
| [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/) | Vala | GTK+ 3 | – | 使用[libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3)而不是[pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) |
| [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/) | Python | GTK+ 3 | pakku | – |
| [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/) | Python | Qt 5 | – | – |
| [updatehint](https://aur.archlinux.org/packages/updatehint/) | Bash | GTK+ 3 | auracle | – |
| [octopi](https://aur.archlinux.org/packages/octopi/) | C++ | Qt 5 | trizen, pacaur, yaourt | [默认启用的通知服务](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) 将进行 [部分升级](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) |

## 库

*   **haskell-archlinux** — 访问AUR和包元数据的库，使用Haskell语言编写。

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — 用于访问AUR包的信息并自动完成AUR交互的Python 3模块。

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## 维护

*   **aur-out-of-date** — 使用hoster的API检查AUR包的上游改动，

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — 监视上游网页的更改。

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — 帮助AUR包的维护者自动更新PKGBUILD，支持模板变量语法。

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — 解析PKGBUILD中的URL，并以发送递增的版本号的方式来检查更新。

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## 上传

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — 从包含多个包的git仓库拆分包，为每个提交添加更新`.SRCINFO`。
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — 使用aur4的子模块来替换较大的git仓库的包，包括`.SRCINFO`.
*   [aurpublish](https://github.com/eli-schwartz/aurpublish) — 对AUR的PKGBUILD管理框架。
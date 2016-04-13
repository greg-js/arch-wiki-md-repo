**翻译状态：** 本文是英文页面 [AUR_Trusted_User_Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-04-12，点击[这里](https://wiki.archlinux.org/index.php?title=AUR_Trusted_User_Guidelines&diff=0&oldid=424924)可以查看翻译后英文页面的改动。

**Trusted User (TU)** 是负责使 AUR 正常工作的社区成员。他们维护热门的包（[并在必要时与上游项目交涉或者向上游项目发送补丁](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)），并且参与管理事务的表决。TU 由现任的 TU 从活跃的社区成员中民主选举产生。 TU 是唯一具有决定 AUR 发展方向的权利的社区成员群体。

TU们依靠[TU bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html)来管理社区。

## Contents

*   [1 新 TU 的 TODO 列表](#.E6.96.B0_TU_.E7.9A.84_TODO_.E5.88.97.E8.A1.A8)
*   [2 TU 和 [unsupported]](#TU_.E5.92.8C_.5Bunsupported.5D)
*   [3 TU 和 [community], 包维护导引](#TU_.E5.92.8C_.5Bcommunity.5D.2C_.E5.8C.85.E7.BB.B4.E6.8A.A4.E5.AF.BC.E5.BC.95)
    *   [3.1 软件包进入 [community] 仓库的规则](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E8.BF.9B.E5.85.A5_.5Bcommunity.5D_.E4.BB.93.E5.BA.93.E7.9A.84.E8.A7.84.E5.88.99)
    *   [3.2 访问并更新仓库](#.E8.AE.BF.E9.97.AE.E5.B9.B6.E6.9B.B4.E6.96.B0.E4.BB.93.E5.BA.93)
    *   [3.3 停止维护软件包](#.E5.81.9C.E6.AD.A2.E7.BB.B4.E6.8A.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.4 将软件包从 unsupported 移到 [community]](#.E5.B0.86.E8.BD.AF.E4.BB.B6.E5.8C.85.E4.BB.8E_unsupported_.E7.A7.BB.E5.88.B0_.5Bcommunity.5D)
    *   [3.5 将软件包从 [community] 移至 unsupported](#.E5.B0.86.E8.BD.AF.E4.BB.B6.E5.8C.85.E4.BB.8E_.5Bcommunity.5D_.E7.A7.BB.E8.87.B3_unsupported)
    *   [3.6 将软件包从 [community-testing] 移至 [community]](#.E5.B0.86.E8.BD.AF.E4.BB.B6.E5.8C.85.E4.BB.8E_.5Bcommunity-testing.5D_.E7.A7.BB.E8.87.B3_.5Bcommunity.5D)
    *   [3.7 从 unsupported 删除软件包](#.E4.BB.8E_unsupported_.E5.88.A0.E9.99.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.8 另见](#.E5.8F.A6.E8.A7.81)

## 新 TU 的 TODO 列表

1.  仔细阅读本页面
2.  阅读 [TU Bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html)
3.  确认自己在 [AUR](/index.php/AUR "AUR") 的账户详细信息是最新的
4.  将你自己添加到 [Trusted Users](/index.php/Trusted_Users "Trusted Users") 页面
5.  订阅 Arch Linux 开发邮件列表 [arch-dev-public](https://lists.archlinux.org/listinfo/arch-dev-public).
6.  提醒 [BBS admin](https://bbs.archlinux.org/userlist.php?username=&show_group=1&sort_by=username&sort_dir=ASC&search=Submit) 更改你在论坛上的账户
7.  向先辈 TU 索要 #archlinux-tu@freenode 的密码并挂在上面。这不是必须的，但是这样会更方便。因为那儿是黑历史曝光和新想法提出的地方。

1.  为[软件包签名](/index.php/Package_signing "Package signing")创建 PGP key.
2.  按照此 [模板](https://www.archlinux.org/trustedusers/) 向 Ionuț Bîru (ibiru@archlinux.org) 或 Florian Pritz (bluewind@xinu.at)提交所有信息来获得 dev 接口的访问权限
3.  给 Florian 发一封加密邮件:
    *   包含一个 SSH 公钥，如果还没有，使用 `ssh-keygen` 生成。[Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") 包含更多信息。
    *   要求将你加入 arch-dev-public 白名单.
    *   告诉他你需要一个 @archlinux.org 电子邮箱.
4.  要求你的赞助者:
    *   在 AUR 赋予你 TU 状态.
    *   在 bug 管理系统的 "Keyring" 项目中提交任务，步骤参考 [这里](https://lists.archlinux.org/pipermail/arch-dev-public/2013-September/025456.html)，三个主密钥持有者会签名您的 PGP 密钥。
5.  给 Lukas Fleischer 发送一封附有 ssh 公钥的邮件。如果你没有一个公钥，使用`ssh-keygen`来生成一个。更多关于 ssh 密钥的信息请查看 [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") 页面
6.  安装 [devtools](https://www.archlinux.org/packages/?name=devtools) 软件包
7.  在 nymeria.archlinux.org 创建 `~/staging/community` 和 `~/staging/community-testing` 两个目录（如果你对维护 multilib 的软件包感兴趣也可以创建 `~/staging/multilib`）。这一步骤 **非常重要** 因为 devtools 脚本使用这些目录来处理输入的软件包。
8.  如果你在两天内没有在 bugtracker 被升级到 TU 组，在 arch-dev-public 发邮件询问
9.  开始你的贡献吧！

## TU 和 [unsupported]

TU 应该仔细检查那些被提交到 UNSUPPORTED 分类中的软件是否含有恶意代码，以及PKGBUILD包是否符合标准。在UNSUPPORTED 中，大约 80% 的 PKGBUILD 都非常简单，TU 团队可以很快的检查其可用性以及安全性。

TU 也应该检查 PKGBUILD 的一些小错误，提出修改以及改进建议。TU 应该努力确认所有的软件包遵循了Arch Packging Guidelines/Standards 并与其他打包者分享他们的技能和经验来提升 archlinux 的软件包发行版本的质量。

TU 也很适合撰写文档来记录一些值得推荐的行为。

## TU 和 [community], 包维护导引

### 软件包进入 [community] 仓库的规则

*   软件包还没有加入其它任何仓库，确保其它打包者没有同时提交软件包。阅读 AUR 中的评论，阅读 [aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general) 中文章的标题，在 [bugtracker 的全部项目](https://bugs.archlinux.org/index.php?project=0&do=index&switch=1)中搜索, [grep](https://en.wikipedia.org/wiki/Grep "wikipedia:Grep") [Subversion 日志](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.log.html)，然后向私有 TU [IRC channel](/index.php/IRC_channel "IRC channel") 发送消息.

*   只有“流行”的软件包才能进入仓库，如 [pkgstats](https://www.archlinux.de/?page=PackageStatistics) 规定的 1% 使用数或者 AUR 中 10 票以上

*   自动属于此规则的例外的软件包包括：
    *   i18n 包
    *   辅助功能软件包
    *   驱动程序
    *   满足“流行”定义的软件包所依赖的包，包括 makedeps 和 optdeps
    *   属于同一集合并一起发布的软件包，前提是这一集合的某些软件包满足“流行”定义

*   任何其他不属于上述例外的软件包想要进入仓库都需首先在 aur-general 邮件列表中提出申请，并解释成为例外的原因（例如重命名的软件包、新软件包等）。软件包进入仓库需要其他三名 TU 同意。维护大量的“不流行”软件包的 TU 的申请更有可能被拒绝。

*   强烈建议 TU 移除 [community] 仓库中他们正在维护的低使用率的软件包。尽管离职的 TU 的软件包在被采用之前会被过滤的情况会发生，移除的行为不会被强制要求

*   软件包从 AUR 提升到其它仓库时，应该将 **pkgrel** 的数值加 *1*，这样已经安装了软件包的用户还可以继续收到软件自动更新。还有一个好处就是避免 **pkgrel** 重置为 *1* 时用户收到本地软件包更新的警告.

### 访问并更新仓库

[community] 仓库现在使用和 [core] 和 [extra] 仓库相同的工具 **devtools** 来上传软件包。唯一的不同在于 [core] 和 [extra] 使用服务器 [https://archlinux.org](https://archlinux.org) 而 [community] 仓库使用服务器`nymeria.archlinux.org`。因此 [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") 页面中大多数指令都能在不用改动的情况下使用。这里介绍关于 [community] 仓库的一些特殊的信息。devtools 需要软件打包人员 [设置 PACKAGER 变量](/index.php/Arch_Build_System#Set_the_PACKAGER_variable_in_.2Fetc.2Fmakepkg.conf "Arch Build System"). 通过 `/usr/share/devtools/makepkg-{i686,x86_64}.conf` 配置，因为在干净的 chroot 中没有正常的配置文件。

首先，你应该做一个 [community] 软件仓库的 **非递归签出**：

```
svn checkout -N svn+ssh://svn-community@nymeria.archlinux.org/srv/repos/svn-community/svn

```

这一步骤将会创建一个名为 svn 的目录，里面只有包含 svn 信息的 .svn 目录。

关于 **签出**，**更新**所有软件包或**添加**一个软件包，请参见 [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") 。

要**移除**一个软件包：

```
 ssh nymeria.archlinux.org /community/db-remove community arch pkgname

```

在此以及接下来的文中，arch 可以是 Arch Linux 支持两个平台 i686 或 x86_64。（“any”怎么办？）

当你完成了 PKGBUILD 等之后，你应该 **提交** 你的更改（`svn commit`）。

用 `mkarchroot` 或帮助脚本 `extra-i686-build`/`extra-x86_64-build` 编译软件包.

用 `gpg --detach-sign *.pkg.tar.xz` 签署软件包.

如果你想要**发布**一个软件包，首先将软件包和签名用 scp 拷贝到 nymeria.archlinux.org 的 *staging/community* 目录下，然后通过进入 *pkgname/trunk* 目录并运行 `archrelease community-arch` 来为 **标识** 该软件包。这将在 *community-i686* 或 *community-x86_64* 目录下创建一份 trunk 条目的 svn 拷贝。这也表示这一软件包已经在所在平台的 [community] 仓库中了。

***注意：** 在有些情况下，特别是对于 community 软件包来说，x86_64 的 TU 也许会在 pkgrel 后加上 .1 （不是 +1）。这表示对于 PKGBUILD 的改动是仅限于 x86_64 平台的并且 i686 平台的维护者 **不应该** 为 i686 平台重建此软件包。如果 TU 想要提升 pkgrel ，那就应该按照通常的方法 +1 。然而，TU 在提升 pkgrel 时，pkgrel=2.1 不应该变为 pkgrel=3.1 而必须应变为 pkgrel=3 。简单的说，就是将 带有点（.） 发行的版本只留给维护 x86_64 平台的 TU 来避免混乱。*

软件包更新汇总：

*   **更新** 软件包目录 (`svn update some-package`)
*   **改变当前目录** 到软件包的 trunk 目录 (`cd some-package/trunk`)
*   **编辑** PKGBUILD，做出必要的更改，
*   **编译** 软件包：使用 `makechrootpkg` 或 `extra-i686-build`/`extra-x86_64-build`. **必须**在 [干净的chroot环境](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") 中构建软件包。
*   **[Namcap](/index.php/Namcap "Namcap")** PKGBUILD 文件和 pkg.tar.gz 二进制包
*   使用 `communitypkg "commit message"` **提交**、**签名**，**拷贝**并**标识** 此软件包。这将自动进行下面步骤
    *   将改变 **提交** 至 trunk (`svn commit`)
    *   **签署** 软件包: `gpg --detach-sign *.pkg.tar.xz`.
    *   将软件包和签名拷贝到 nymeria.archlinux.org (`scp pkgname-ver-rel-arch.pkg.tar.xz *.pkg.tar.xz.sig nymeria.archlinux.org:staging/community/`)
    *   **标识** 此软件包 (`archrelease community-{i686,x86_64`})
*   **更新** 软件仓库(`ssh nymeria.archlinux.org /community/db-update`)

另外请阅读 [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") 页面的 *Miscellaneours* 部分。对于 *Avoid having to enter your password all the time* 部分，使用 nymeria.archlinux.org 而不要使用 gerolde.archlinux.org。

### 停止维护软件包

如果一个 TU 不想再维护一个软件包了，他应该在 AUR 邮件列表中发出一个通知，以便其他的 TU 可以继续维护该软件包。一个软件包即是在没有其他 TU 维护的情况下仍然能够被一个 TU 停止维护。但是 TU 应该尽量不要放弃放弃很多软件包（他们不应该负责超过他们时间允许的工作）。如果一个软件包已经过时或者不再被使用，那么也应该被完全移除。

如果一个软件包已经被完全移除，它也可以重新上传到 UNSUPPORTED，使得普通用户可以替 TU 维护它。

### 将软件包从 unsupported 移到 [community]

按照普通的向 community 仓库添加软件包的步骤即可，但是记得将相应的软件包从 unsupported 中移除。

### 将软件包从 [community] 移至 unsupported

按照上面提到的方法移除软件包，并将你的源代码上传到 AUR 即可。

### 将软件包从 [community-testing] 移至 [community]

```
ssh nymeria.archlinux.org /srv/repos/svn-community/dbscripts/db-move community-testing community package

```

### 从 unsupported 删除软件包

没必要移除虚设的软件包，因为他们会在试图跟踪依赖关系时被重新创建。如果有人上传了一个实际的软件包，那么所有依赖的软件包都会指向正确的位置。

例如，一个虚设的软件包可以见 [https://aur.archlinux.org/packages.php?ID=23600](https://aur.archlinux.org/packages.php?ID=23600)

### 另见

*   [DeveloperWiki#Packaging Guidelines](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")
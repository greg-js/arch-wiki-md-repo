**翻译状态：** 本文是英文页面 [Pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-03-06，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman%2FRosetta&diff=0&oldid=464653)可以查看翻译后英文页面的改动。

这个页面用表格展示一些流行的 Linux 发行版[包管理器](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager")命令的对应关系。这是受到 [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison) 的启发而成的。

**Tip:** Arch 用户在临时处理其他发行版时可以用 [pacapt](https://github.com/icy/pacapt)，它是对其它包管理器的简单包装。

**Note:**

*   这里描述的一些工具只针对特定版本的 pacman。其中的 -Qk 选项是在 pacman 4.1 中新实现的。
*   您可以在 [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) 中找到 `pkgfile` 命令。

## Contents

*   [1 基本操作](#.E5.9F.BA.E6.9C.AC.E6.93.8D.E4.BD.9C)
*   [2 查询某个包的信息](#.E6.9F.A5.E8.AF.A2.E6.9F.90.E4.B8.AA.E5.8C.85.E7.9A.84.E4.BF.A1.E6.81.AF)
*   [3 查询包列表](#.E6.9F.A5.E8.AF.A2.E5.8C.85.E5.88.97.E8.A1.A8)
*   [4 查询包的依赖关系](#.E6.9F.A5.E8.AF.A2.E5.8C.85.E7.9A.84.E4.BE.9D.E8.B5.96.E5.85.B3.E7.B3.BB)
*   [5 管理软件源](#.E7.AE.A1.E7.90.86.E8.BD.AF.E4.BB.B6.E6.BA.90)
*   [6 Overrides](#Overrides)
*   [7 校验和修复](#.E6.A0.A1.E9.AA.8C.E5.92.8C.E4.BF.AE.E5.A4.8D)
*   [8 使用软件包文件和构建软件包](#.E4.BD.BF.E7.94.A8.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.96.87.E4.BB.B6.E5.92.8C.E6.9E.84.E5.BB.BA.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [9 参阅](#.E5.8F.82.E9.98.85)

## 基本操作

| **<font color="#707070">动作</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| 按名安装包 | pacman -S | dnf install | apt install | zypper install
zypper in | emerge [-a] |
| 按名移除包 | pacman -Rs | dnf remove | apt remove | zypper remove
zypper rm | emerge -C |
| 通过软件名、描述、简短描述来搜索包。默认搜索域依工具不同而异。Mostly options bring tools on par. | pacman -Ss | dnf search | apt search | zypper search
zypper se [-s] | emerge -S |
| 升级包（安装已有包的更新版本） | pacman -Syu | dnf upgrade | apt update; apt upgrade | zypper update zypper up | emerge -u world |
| 升级包（更新命令的另一种形式，可以进行更复杂形式的更新，例如发行版升级。当通常的更新命令会忽略软件更新时——例如依赖改变——本命令可以进行这些更新） | pacman -Syu | dnf distro-sync | apt full-upgrade | zypper dup | emerge -uDN world |
| 清除本地缓存（可能允许通过选项控制要清除拿些东西；autoclean 只清除过时的信息） | pacman -Sc
pacman -Scc | dnf clean all | apt-get clean / apt-get autoclean / aptitude clean | zypper clean | eclean distfiles |
| 移除不再需要的依赖（例如当依赖某包的软件被移除） | pacman -Qdtq | pacman -Rs - | dnf autoremove | apt-get autoremove | zypper rm -u | emerge --depclean |
| 移除不再处于任何仓库中的包 | pacman -Qm | pacman -Rs - | package-cleanup --orphans | aptitude purge '~o' |
| 将作为依赖安装的包指定为手动安装 | pacman -D --asexplicit | dnf mark install | apt-mark manual | emerge --select |
| 将包作为依赖安装 | pacman -S --asdeps | dnf install => dnf mark remove | aptitude install '$package&M' | emerge -1 |
| 仅下载而不解包或安装 | pacman -Sw | dnf download | apt-get install --download-only (into the package cache)
apt-get download (bypass the package cache) | zypper --download-only | emerge --fetchonly |
| 启动一个 shell 以便在一个会话中输入多个命令 | apt-config shell | zypper shell |
| 查看日志 | cat /var/log/pacman.log | dnf history | cat /var/log/dpkg.log | cat /var/log/zypp/history | located in /var/log/portage |
| 获取当前系统所有软件包的状态 | (see /var/lib/pacman/local) | (see /var/lib/rpm/Packages) | apt-cache stats | n/a | emerge --info |
| 包变更时发送邮件 | apt-get install apt-listchanges |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 查询某个包的信息

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| 显示包的全部或者部分信息。各种包管理工具默认显示的详细程度各不相同，但是可以通过设置选项使其一致。 | pacman -[S|Q]i | dnf list, dnf info | apt show / apt-cache policy | zypper info zypper if | emerge -S; emerge -pv; eix |
| 显示本地包信息，包括包名、版本、描述等。 | pacman -Qi | rpm -qi | dpkg -s / aptitude show | zypper info; rpm -qi | emerge -pv and emerge -S |
| 显示远程包信息，包括包名、版本、描述等。 | pacman -Si | dnf info | apt-cache show / aptitude show | zypper info | emerge -pv and emerge -S |
| 显示本地包提供的文件。 | pacman -Ql | rpm -ql | dpkg -L | rpm -Ql | equery files |
| 显示远程包提供的文件。 | pkgfile -l | dnf repoquery -l | apt-file list $pattern | pfl |
| 查询提供某个文件的包。 | pacman -Qo | rpm -qf (installed only) or dnf provides (everything) | dpkg -S / dlocate | zypper search -f | equery belongs |
| 列出包中的文件。其他更复杂的命令亦可以提供该功能。 | pacman -Ql
pkgfile -l | dnf repoquery -l | dpkg-query -L | rpm -ql | equery files |
| 查出文件是由哪一个包提供的，主要是为了检索特定文件。其他工具亦可通过搜索命令提供该功能。 | pkgfile | dnf provides | apt-file search | zypper what-provides zypper wp | equery belongs (only installed packages); pfl |
| 在所有包中查找包含指定文件的包。auto-apt 提供该功能。 | pkgfile -s | dnf provides | apt-file search | zypper search -f | equery belongs |
| 显示包的更新日志。 | pacman -Qc | rpm -q --changelog | apt-get changelog | rpm -q --changelog | equery changes -f |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 查询包列表

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par. | pacman -Ss | dnf search | apt search | zypper search zypper se [-s] | emerge -S |
| Lists packages which have an update available. Note: Some provide special commands to limit the output to certain installation sources, others use options. | pacman -Qu | dnf list updates, dnf check-update | apt-get upgrade -> n | zypper list-updates zypper patch-check (just for patches) | emerge -uDNp world |
| Display a list of all packages in all installation sources that are handled by the packages management. Some tools provide options or additional commands to limit the output to a specific installation source. | pacman -Sl | dnf list available | apt-cache dumpavail apt-cache dump (Cache only) apt-cache pkgnames | zypper packages | emerge -ep world |
| Generates a list of installed packages | pacman -Q | dnf list installed | dpkg --list | grep ^i | zypper search --installed-only | emerge -ep world |
| List packages that are installed but are not available in any installation source (anymore). | pacman -Qm | dnf list extras | deborphan | zypper se -si | grep 'System Packages' | eix-test-obsolete |
| List packages that were recently added to one of the installation sources, i.e. which are new to it. | (none) | dnf list recent | aptitude search '~N' / aptitude forget-new | n/a | eix-diff |
| List installed local packages along with version | pacman -Q | rpm -qa | dpkg -l | zypper search -s; rpm -qa | emerge -e world |
| Search locally installed package for names or descriptions | pacman -Qs | rpm -qa '*<str>*' | aptitude search '~i(~n $name|~d $description)' | eix -S -I |
| List packages not required by any other package | pacman -Qt | package-cleanup --all --leaves | deborphan -anp1 |
| List packages installed explicitly (not as dependencies) | pacman -Qe | apt-mark showmanual |
| List packages installed automatically (as dependencies) | pacman -Qd | apt-mark showauto |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 查询包的依赖关系

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Display packages which require X to be installed, aka show reverse dependencies. | pacman -Sii | dnf repoquery --alldeps --whatrequires | apt-cache rdepends / aptitude search ~D$pattern | zypper search --requires | equery depends |
| Display packages which conflict with given expression (often package). Search can be used as well to mimic this function. | dnf repoquery --conflicts | aptitude search '~C$pattern' |
| List all packages which are required for the given package, aka show dependencies. | pacman -[S|Q]i | dnf repoquery --requires | apt-cache depends / apt-cache show | zypper info --requires | emerge -ep |
| List what the current package provides | dnf provides | dpkg -s / aptitude show | zypper info --provides | equery files |
| List all packages that require a particular package | dnf repoquery --alldeps --whatrequires | aptitude search ~D{depends,recommends,suggests}:$pattern / aptitude why | zypper search --requires | equery depends -a |
| Display all packages that the specified packages obsoletes. | dnf list obsoletes | apt-cache show |
| Generates an output suitable for processing with dotty for the given package(s). | apt-cache dotty | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 管理软件源

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Installation sources management | ${EDITOR} /etc/pacman.conf | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | ${EDITOR} /etc/apt/sources.list | ${EDITOR} /etc/zypp/repos.d/${REPO}.repo | layman |
| Add an installation source to the system. Some tools provide additional commands for certain sources, others allow all types of source URI for the add command. Again others, like apt and dnf force editing a sources list. apt-cdrom is a special command, which offers special options design for CDs/DVDs as source. | /etc/pacman.conf | /etc/yum.repos.d/*.repo | apt-cdrom add | zypper service-add | layman, overlays |
| Refresh the information about the specified installation source(s) or all installation sources. | pacman -Sy ([always upgrade the whole system afterwards](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance")) | dnf clean expire-cache && dnf check-update | apt-get update | zypper refresh zypper ref | emerge --sync;layman -S |
| Prints a list of all installation sources including important information like URI, alias etc. | cat /etc/pacman.d/mirrorlist | cat /etc/yum.repos.d/* | apt-cache policy | zypper service-list | layman -l |
| Disable an installation source for an operation | dnf --disablerepo= | emerge package::repo-to-use |
| Download packages from a different version of the distribution than the one installed. | dnf --releasever= | apt-get install -t release package/ apt-get install package/release (deps not covered) | echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Overrides

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| 增加包锁定规则来保持其当前状态不被改变 | /etc/pacman.conf
modify IgnorePkg array | dnf.conf <--”exclude” option (add/amend) | apt-mark hold pkg | Put package name in /etc/zypp/locks, or zypper al | /etc/portage/package.mask |
| 删除包锁定规则 | remove package from IgnorePkg line in /etc/pacman.conf | apt-mark unhold pkg | Remove package name from /etc/zypp/locks or zypper rl | /etc/portage/package.mask (or package.unmask) |
| 列出所有锁定规则 | cat /etc/pacman.conf | /etc/apt/preferences | View /etc/zypp/locks or zypper ll | cat /etc/portage/package.mask |
| Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source. | ${EDITOR} /etc/pacman.conf
Modify HoldPkg and/or IgnorePkg arrays | /etc/apt/preferences, apt-cache policy | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
Add a line with =category/package-version |
| Remove a previously set priority | /etc/apt/preferences | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
remove offending line |
| Show a list of set priorities. | apt-cache policy /etc/apt/preferences | zypper lr -p | cat /etc/portage/package.keywords |
| Ignores problems that priorities may trigger. | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 校验和修复

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Verify single package | pacman -Qk[k] | rpm -V | debsums | rpm -V | equery check |
| Verify all packages | pacman -Qk[k] | rpm -Va | debsums | rpm -Va | equery check |
| Reinstall given Package - Will reinstall the given package without dependency hassle. | pacman -S | dnf reinstall | apt install --reinstall | zypper install --force | emerge [-a] |
| Verify dependencies of the complete system. Used if installation process was forcefully killed. | pacman -Dk | dnf repoquery --requires | apt-get check | zypper verify | emerge -uDN world |
| Use some magic to fix broken dependencies in a system | pacman dep level - pacman -Dk, shared lib level - findbrokenpkgs or lddd | dnf repoquery --unsatisfied | apt-get --fix-broken
aptitude install | zypper verify | revdep-rebuild |
| 为包系统增加一个检查点以便未来回滚 | (unnecessary, done on every transaction) | n/a |
| 删除系统中的一个检查点 | N/A | N/A | n/a |
| 提供所有系统检查点的列表 | N/A | dnf history list | n/a |
| 将所有包滚回特定日期或检查点 | N/A | dnf history rollback | n/a |
| 撤销特定改动 | N/A | dnf history undo | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 使用软件包文件和构建软件包

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg -I |
| List the contents of a package file | pacman -Qpl | rpmls rpm -qpl | dpkg -c | rpm -qpl |
| Installs local package file, e.g. app.rpm and uses the installation sources to resolve dependencies | pacman -U | dnf install | apt install | zypper in | emerge |
| Updates package(s) with local packages and uses the installation sources to resolve dependencies | pacman -U | dnf upgrade | debi | emerge |
| Add a local package to the local package cache mostly for debugging purposes. | cp $filename /var/cache/pacman/pkg/ | apt-cache add | n/a | cp $filename /usr/portage/distfiles |
| 解包 | tar -Jxvf | rpm2cpio | cpio -vid | dpkg-deb -x | rpm2cpio | cpio -vid | tar -jxvf |
| 安装/移除包以适合构建依赖（使用源码包中的信息） | automatic | dnf builddep | apt-get build-dep | zypper si -d | emerge -o |
| Display the source package to the given package name(s) | dnf repoquery -s | apt-cache showsrc | n/a |
| Downloads the corresponding source package(s) to the given package name(s) | Use [ABS](/index.php/ABS "ABS") && makepkg -o | dnf download --source | apt-get source / debcheckout | zypper source-install | emerge --fetchonly |
| Build a package | makepkg -s | rpmbuild -ba (normal)
mock (in chroot) | debuild | rpmbuild -ba; build; osc build | ebuild; quickpkg |
| Check for possible packaging issues | namcap | rpmlint | lintian | rpmlint | repoman |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## 参阅

*   [Changes in DNF CLI compared to Yum](http://dnf.readthedocs.org/en/latest/cli_vs_yum.html)
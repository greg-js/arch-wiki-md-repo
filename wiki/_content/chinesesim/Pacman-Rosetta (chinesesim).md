这个页面从 [openSUSE 的 Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison) 页拉取了大量内容。（This page pulls heavily from [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison).）我们对它进行了一些简化，把 Arch 加入对比列表，并且为了方便 Arch 用户而修改了不同发行版的顺序。

其他发行版的用户可以通过一个简单的包装器——[pacapt](https://github.com/icy/pacapt)——来享受 pacman 的好处。这个脚本也可以让 Arch 用户在临时处理其他发行版时使用。

[pacapt](https://github.com/icy/pacapt) 是 pacman 的 shell 脚本实现，它是为其他 Linux 发行版而制作的。

**注意:**

*   这里描述的一些工具只针对特定版本的 pacman。其中的 -Qk 选项是在 pacman 4.1 中新实现的。
*   您可以在 [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) 包中找到 `pkgfile` 命令。

| **<font color="#707070">动作</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |
| 按名安装包 | pacman -S | yum install | apt-get install | zypper install zypper in | emerge [-a] |
| 按名移除包 | pacman -Rc | yum remove/erase | apt-get remove | zypper remove zypper rm | emerge -C |
| 通过软件名、描述、简短描述来搜索包。默认搜索域依工具不同而异。Mostly options bring tools on par. | pacman -Ss | yum search | apt-cache search | zypper search zypper se [-s] | emerge -S |
| 升级包/安装已有包的更新版本 | pacman -Syu | yum update | apt-get upgrade | zypper update zypper up | emerge -u world |
| 更新包（更新命令的另一种形式，可以进行更复杂形式的更新，例如发行版升级。当通常的更新命令会忽略软件更新时——例如依赖改变——本命令可以进行这些更新） | pacman -Syu | yum distro-sync | apt-get dist-upgrade | zypper dup | emerge -uDN world |
| 重新安装指定的包（会重新安装指定的包而不考虑依赖） | pacman -S | yum reinstall | apt-get install --reinstall | zypper install --force | emerge [-a] |
| 安装本地包（例如app.rpm）并使用安装源解决依赖关系 | pacman -U | yum localinstall | dpkg -i && apt-get install -f | zypper in /path/to/local.rpm | emerge |
| 从本地更新包并使用安装源解决依赖关系 | pacman -U | yum localupdate | n/a | emerge |
| 使用一些手段来修复系统中的不完整依赖 | pacman dep level - testdb, shared lib level - findbrokenpkgs or lddd | package-cleanup --problems | apt-get --fix-broken / aptitude install | zypper verify | revdep-rebuild |
| 仅下载而不解包或安装 | pacman -Sw | yumdownloader (found in yum-utils package) | apt-get --download-only / aptitude download | zypper --download-only | emerge --fetchonly |
| 移除不再需要的依赖（例如当依赖某包的软件被移除） | pacman -Qdtq | pacman -Rs - | yum autoremove | apt-get autoremove | zypper rm -u | emerge --depclean |
| 下载给定名称包的源码包 | Use [ABS](/index.php/ABS "ABS") && makepkg -o | yumdownloader --source | apt-get source / debcheckout | zypper source-install | emerge --fetchonly |
| 移除不再处于任何仓库中的包 | package-cleanup --orphans |
| 安装/移除包以适合构建依赖（使用源码包中的信息） | automatic | yum-builddep | apt-get build-dep | zypper si -d | emerge -o |
| 增加包锁定规则来保持其当前状态不被改变 | ${EDITOR} /etc/pacman.conf
modify IgnorePkg array | yum.conf <--”exclude” option (add/amend) | echo "$PKGNAME hold" | dpkg --set-selections | Put package name in /etc/zypp/locks | /etc/portage/package.mask |
| 删除包锁定规则 | remove package from IgnorePkg line in /etc/pacman.conf | yum.conf <--”exclude” option (remove/amend) | echo "$PKGNAME install" | dpkg --set-selections | Remove package name from /etc/zypp/locks | /etc/portage/package.mask (or package.unmask) |
| 展示所有锁定规则的列表 | cat /etc/pacman.conf | yum.conf (research needed) | /etc/apt/preferences | View /etc/zypp/locks | cat /etc/portage/package.mask |
| 为包系统增加一个检查点以便未来回滚 | (unnecessary, done on every transaction) | n/a |
| 删除系统中的一个检查点 | N/A | N/A | n/a |
| 提供所有系统检查点的列表 | N/A | yum history list | n/a |
| 将所有包滚回特定日期或检查点 | N/A | yum history rollback | n/a |
| 撤销特定改动 | N/A | yum history undo | n/a |
| 明示要求将之前安装的某包作为依赖 | pacman -D --asexplicit | aptitude unmarkauto | emerge --select |
| 将某包作为依赖安装且不标记为明确要求安装 | pacman -S --asdeps | emerge -1 |
| ***Package information management*** |
| Get a dump of the whole system information - Prints, Saves or similar the current state of the package management system. Preferred output is text or XML. (Note: Why either-or here? No tool offers the option to choose the output format.) | (see /var/lib/pacman/local) | (see /var/lib/rpm/Packages) | apt-cache stats | n/a | emerge --info |
| Show all or most information about a package. The tools' verbosity for the default command vary. But with options, the tools are on par with each other. | pacman -[S|Q]i | yum list or info | apt-cache show / apt-cache policy | zypper info zypper if | emerge -S; emerge -pv; eix |
| Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par. | pacman -Ss | yum search | apt-cache search | zypper search zypper se [-s] | emerge -S |
| Lists packages which have an update available. Note: Some provide special commands to limit the output to certain installation sources, others use options. | pacman -Qu | yum list updates yum check-update | apt-get upgrade -> n | zypper list-updates zypper patch-check (just for patches) | emerge -uDNp world |
| Display a list of all packages in all installation sources that are handled by the packages management. Some tools provide options or additional commands to limit the output to a specific installation source. | pacman -Sl | yum list available | apt-cache dumpavail apt-cache dump (Cache only) apt-cache pkgnames | zypper packages | emerge -ep world |
| Displays packages which provide the given exp. aka reverse provides. Mainly a shortcut to search a specific field. Other tools might offer this functionality through the search command. | pkgfile <filename> | yum whatprovides yum provides | apt-file search <filename> | zypper what-provides zypper wp | equery belongs (only installed packages); pfl |
| Display packages which require X to be installed, aka show reverse/ dependencies. | pacman -Sii | yum resolvedep | apt-cache rdepends / aptitude search ~Dpattern | IN PROGRESS | equery depends |
| Display packages which conflict with given expression (often package). Search can be used as well to mimic this function. | (none) | repoquery --whatconflicts | aptitude search '~Cpattern' | IN PROGRESS |
| List all packages which are required for the given package, aka show dependencies. | pacman -[S|Q]i | yum deplist | apt-cache depends / apt-cache show | IN PROGRESS | emerge -ep |
| List what the current package provides | yum provides | IN PROGRESS | equery files |
| List the files that the package holds. Again, this functionality can be mimicked by other more complex commands. | pacman -Ql $pkgname
pkgfile -l | repoquery -l $pkgname | dpkg-query -L $pkgname | IN PROGRESS | equery files |
| List all packages that require a particular package | repoquery --whatrequires [--recursive] | equery depends -a |
| Search all packages to find the one which holds the specified file. auto-apt is using this functionality. | pkgfile -s | yum provides yum whatprovides | apt-file search | IN PROGRESS | equery belongs |
| Display all packages that the specified packages obsoletes. | yum list obsoletes | apt-cache show | IN PROGRESS |
| Verify dependencies of the complete system. Used if installation process was forcefully killed. | testdb | yum deplist | apt-get check | n/a | emerge -uDN world |
| Generates a list of installed packages | pacman -Q | yum list installed | dpkg --get-selections | zypper | emerge -ep world |
| List packages that are installed but are not available in any installation source (anymore). | pacman -Qm | yum list extras | deborphan | zypper se -si | grep 'System Packages' | eix-test-obsolete |
| List packages that were recently added to one of the installation sources, i.e. which are new to it. | (none) | yum list recent | aptitude search '~N' / aptitude forget-new | n/a | eix-diff |
| Show a log of actions taken by the software management. | cat /var/log/pacman.log | yum history cat /var/log/yum.log | cat /var/log/dpkg.log | cat /var/log/zypp/history | located in /var/log/portage |
| Clean up all local caches. Options might limit what is actually cleaned. Autoclean removes only unneeded, obsolete information. | pacman -Sc
pacman -Scc | yum clean all | apt-get clean / apt-get autoclean / aptitude clean | zypper clean | eclean distfiles |
| Add a local package to the local package cache mostly for debugging purposes. | cp $pkgname /var/cache/pacman/pkg/ | apt-cache add | n/a | cp $srcfile /usr/portage/distfiles |
| Display the source package to the given package name(s) | repoquery -s | apt-cache showsrc | n/a |
| Generates an output suitable for processing with dotty for the given package(s). | apt-cache dotty | n/a |
| Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source. | ${EDITOR} /etc/pacman.conf
Modify HoldPkg and/or IgnorePkg arrays | yum-plugin-priorities and yum-plugin-protect-packages | /etc/apt/preferences, apt-cache policy | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
Add a line with =category/package-version |
| Remove a previously set priority | /etc/apt/preferences | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
remove offending line |
| Show a list of set priorities. | apt-cache policy /etc/apt/preferences | n/a | cat /etc/portage/package.keywords |
| Ignores problems that priorities may trigger. | n/a |
| Installation sources management | ${EDITOR} /etc/pacman.conf | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | ${EDITOR} /etc/apt/sources.list | layman |
| Add an installation source to the system. Some tools provide additional commands for certain sources, others allow all types of source URI for the add command. Again others, like apt and yum force editing a sources list. apt-cdrom is a special command, which offers special options design for CDs/DVDs as source. | ${EDITOR} /etc/pacman.conf | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | apt-cdrom add | zypper service-add | layman, overlays |
| Refresh the information about the specified installation source(s) or all installation sources. | pacman -Sy | yum clean expire-cache && yum check-update | apt-get update | zypper refresh zypper ref | layman -f |
| Prints a list of all installation sources including important information like URI, alias etc. | cat /etc/pacman.d/mirrorlist | cat /etc/yum.repos.d/* | zypper service-list | layman -l |
| Disable an installation source for an operation | yum --disablerepo=${REPO} | emerge package::repo-to-use |
| Download packages from a different version of the distribution than the one installed. | yum --releasever=${VERSION} | apt-get install -t release package/ apt-get install package/release (deps not covered) | echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package |
| ***Other commands*** |
| Start a shell to enter multiple commands in one session | yum shell | apt-config shell | zypper shell |
| ***Package Verification*** |
| Single package | pacman -Qk[k] <package> | rpm -V <package> | debsums | rpm -V <package> | equery check |
| All packages | pacman -Qk[k] | rpm -Va | debsums | rpm -Va | equery check |
| ***Package Querying*** |
| List installed local packages along with version | pacman -Q | rpm -qa | dpkg -l | emerge -e world |
| Display local package information: Name, version, description, etc. | pacman -Qi | rpm -qi | dpkg -s | emerge -pv and emerge -S |
| Display remote package information: Name, version, description, etc. | pacman -Si | yum info | apt-cache show / aptitude show | emerge -pv and emerge -S |
| Display files provided by local package | pacman -Ql | rpm -ql | dpkg -L | equery files |
| Display files provided by a remote package | pkgfile -l | repoquery -l | pfl |
| Query the package which provides FILE | pacman -Qo | rpm -qf (installed only) or yum whatprovides (everything) | dpkg -S/dlocate | equery belongs |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg -I |
| Show the changelog of a package | pacman -Qc | rpm -q --changelog | apt-get changelog | equery changes -f |
| Search locally installed package for names or descriptions | pacman -Qs | aptitude search '~i(~nexpr|~dexpr)' | eix -S -I |
| List packages not required by any other package | pacman -Qt | package-cleanup --all --leaves | deborphan -an |
| ***Building Packages*** |
| Build a package | makepkg -s | rpmbuild -ba (normal) mock (in chroot) | debuild | rpmbuild -ba | ebuild; quickpkg |
| Check for possible packaging issues | rpmlint | lintian | repoman |
| List the contents of a package file | pacman -Qpl <file> | rpmls rpm -qpl | dpkg -c | rpm -qpl |
| Extract a package | tar -Jxvf | rpm2cpio | cpio -vid | ar vx | tar -zxvf data.tar.gz | rpm2cpio | cpio -vid | tar -jxvf |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg -I |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |
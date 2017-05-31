This page uses a table to display the correspondence of [package management](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") commands among some of the most popular Linux distributions. The original inspiration was given by [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison).

**Tip:** Arch users having to temporarily deal with another Linux distribution can use [pacapt](https://github.com/icy/pacapt), a simple wrapper around other package managers.

**Note:**

*   Some of the tools described here are specific to a certain version of pacman. The -Qk option is new in pacman 4.1.

## Contents

*   [1 Basic operations](#Basic_operations)
*   [2 Querying specific packages](#Querying_specific_packages)
*   [3 Querying package lists](#Querying_package_lists)
*   [4 Querying package dependencies](#Querying_package_dependencies)
*   [5 Installation sources management](#Installation_sources_management)
*   [6 Overrides](#Overrides)
*   [7 Verification and repair](#Verification_and_repair)
*   [8 Using package files and building packages](#Using_package_files_and_building_packages)
*   [9 See also](#See_also)

## Basic operations

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Install a package(s) by name | pacman -S | dnf install | apt install | zypper install
zypper in | emerge [-a] |
| Remove a package(s) by name | pacman -Rs | dnf remove | apt remove | zypper remove
zypper rm | emerge -C |
| Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par. | pacman -Ss | dnf search | apt search | zypper search
zypper se [-s] | emerge -S |
| Upgrade Packages - Install packages which have an older version already installed | pacman -Syu | dnf upgrade | apt update; apt upgrade | zypper update zypper up | emerge -u world |
| Upgrade Packages - Another form of the update command, which can perform more complex updates -- like distribution upgrades. When the usual update command will omit package updates, which include changes in dependencies, this command can perform those updates. | pacman -Syu | dnf distro-sync | apt full-upgrade | zypper dup | emerge -uDN world |
| Clean up all local caches. Options might limit what is actually cleaned. Autoclean removes only unneeded, obsolete information. | pacman -Sc
pacman -Scc | dnf clean all | apt-get clean / apt-get autoclean / aptitude clean | zypper clean | eclean distfiles |
| Remove dependencies that are no longer needed, because e.g. the package which needed the dependencies was removed. | pacman -Qdtq | pacman -Rs - | dnf autoremove | apt-get autoremove | zypper rm -u | emerge --depclean |
| Remove packages no longer included in any repositories. | pacman -Qm | pacman -Rs - | package-cleanup --orphans | aptitude purge '~o' |
| Mark a package previously installed as a dependency as explicitly required. | pacman -D --asexplicit | dnf mark install | apt-mark manual | emerge --select |
| Install package(s) as dependency / without marking as explicitly required. | pacman -S --asdeps | dnf install => dnf mark remove | aptitude install '$package&M' | emerge -1 |
| Only downloads the given package(s) without unpacking or installing them | pacman -Sw | dnf download | apt-get install --download-only (into the package cache)
apt-get download (bypass the package cache) | zypper --download-only | emerge --fetchonly |
| Start a shell to enter multiple commands in one session | apt-config shell | zypper shell |
| Show a log of actions taken by the software management. | cat /var/log/pacman.log | dnf history | cat /var/log/dpkg.log | cat /var/log/zypp/history | located in /var/log/portage |
| Get a dump of the whole system information - Prints, Saves or similar the current state of the package management system. Preferred output is text or XML. (Note: Why either-or here? No tool offers the option to choose the output format.) | (see /var/lib/pacman/local) | (see /var/lib/rpm/Packages) | apt-cache stats | n/a | emerge --info |
| e-mail delivery of package changes | apt-get install apt-listchanges |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Querying specific packages

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Show all or most information about a package. The tools' verbosity for the default command vary. But with options, the tools are on par with each other. | pacman -[S|Q]i | dnf list, dnf info | apt show / apt-cache policy | zypper info zypper if | emerge -S; emerge -pv; eix |
| Display local package information: Name, version, description, etc. | pacman -Qi | rpm -qi | dpkg -s / aptitude show | zypper info; rpm -qi | emerge -pv and emerge -S |
| Display remote package information: Name, version, description, etc. | pacman -Si | dnf info | apt-cache show / aptitude show | zypper info | emerge -pv and emerge -S |
| Display files provided by local package | pacman -Ql | rpm -ql | dpkg -L | rpm -Ql | equery files |
| Display files provided by a remote package | pacman -Fl | dnf repoquery -l | apt-file list $pattern | pfl |
| Query the package which provides FILE | pacman -Qo | rpm -qf (installed only) or dnf provides (everything) | dpkg -S / dlocate | zypper search -f | equery belongs |
| List the files that the package holds. Again, this functionality can be mimicked by other more complex commands. | pacman -Ql
pacman -Fl | dnf repoquery -l | dpkg-query -L | rpm -ql | equery files |
| Displays packages which provide the given exp. aka reverse provides. Mainly a shortcut to search a specific field. Other tools might offer this functionality through the search command. | pacman -Fo | dnf provides | apt-file search | zypper what-provides zypper wp | equery belongs (only installed packages); pfl |
| Search all packages to find the one which holds the specified file. auto-apt is using this functionality. | pacman -Fs | dnf provides | apt-file search | zypper search -f | equery belongs |
| Show the changelog of a package | pacman -Qc | rpm -q --changelog | apt-get changelog | rpm -q --changelog | equery changes -f |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Querying package lists

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

## Querying package dependencies

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Display packages which require X to be installed, aka show reverse dependencies. | pacman -Sii | dnf repoquery --alldeps --whatrequires | apt-cache rdepends / aptitude search ~D$pattern | zypper search --requires | equery depends |
| Display packages which conflict with given expression (often package). Search can be used as well to mimic this function. | dnf repoquery --conflicts | aptitude search '~C$pattern' |
| List all packages which are required for the given package, aka show dependencies. | pacman -[S|Q]i | dnf repoquery --requires | apt-cache depends / apt-cache show | zypper info --requires | emerge -ep |
| List what the current package provides | dnf provides | dpkg -s / aptitude show | zypper info --provides | equery files |
| List all packages that require a particular package | dnf repoquery --alldeps --whatrequires | aptitude search ~D{depends,recommends,suggests}:$pattern / aptitude why | zypper search --requires | equery depends -a |
| Display all packages that the specified packages obsoletes. | dnf list obsoletes | apt-cache show |
| Generates an output suitable for processing with dotty for the given package(s). | apt-cache dotty | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Installation sources management

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
| Add a package lock rule to keep its current state from being changed | /etc/pacman.conf
modify IgnorePkg array | dnf.conf <--”exclude” option (add/amend) | apt-mark hold pkg | Put package name in /etc/zypp/locks, or zypper al | /etc/portage/package.mask |
| Delete a package lock rule | remove package from IgnorePkg line in /etc/pacman.conf | apt-mark unhold pkg | Remove package name from /etc/zypp/locks or zypper rl | /etc/portage/package.mask (or package.unmask) |
| Show a listing of all lock rules | cat /etc/pacman.conf | /etc/apt/preferences | View /etc/zypp/locks or zypper ll | cat /etc/portage/package.mask |
| Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source. | ${EDITOR} /etc/pacman.conf
Modify HoldPkg and/or IgnorePkg arrays | /etc/apt/preferences, apt-cache policy | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
Add a line with =category/package-version |
| Remove a previously set priority | /etc/apt/preferences | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
remove offending line |
| Show a list of set priorities. | apt-cache policy /etc/apt/preferences | zypper lr -p | cat /etc/portage/package.keywords |
| Ignores problems that priorities may trigger. | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Verification and repair

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Verify single package | pacman -Qk[k] | rpm -V | debsums | rpm -V | equery check |
| Verify all packages | pacman -Qk[k] | rpm -Va | debsums | rpm -Va | equery check |
| Reinstall given Package - Will reinstall the given package without dependency hassle. | pacman -S | dnf reinstall | apt install --reinstall | zypper install --force | emerge [-a] |
| Verify dependencies of the complete system. Used if installation process was forcefully killed. | pacman -Dk | dnf repoquery --requires | apt-get check | zypper verify | emerge -uDN world |
| Use some magic to fix broken dependencies in a system | pacman dep level - pacman -Dk, shared lib level - findbrokenpkgs or lddd | dnf repoquery --unsatisfied | apt-get --fix-broken
aptitude install | zypper verify | revdep-rebuild |
| Add a checkpoint to the package system for later rollback | (unnecessary, done on every transaction) | n/a |
| Remove a checkpoint from the system | N/A | N/A | n/a |
| Provide a list of all system checkpoints | N/A | dnf history list | n/a |
| Rolls entire packages back to a certain date or checkpoint. | N/A | dnf history rollback | n/a |
| Undo a single specified transaction. | N/A | dnf history undo | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Using package files and building packages

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg -I |
| List the contents of a package file | pacman -Qpl | rpmls rpm -qpl | dpkg -c | rpm -qpl |
| Installs local package file, e.g. app.rpm and uses the installation sources to resolve dependencies | pacman -U | dnf install | apt install | zypper in | emerge |
| Updates package(s) with local packages and uses the installation sources to resolve dependencies | pacman -U | dnf upgrade | debi | emerge |
| Add a local package to the local package cache mostly for debugging purposes. | cp $filename /var/cache/pacman/pkg/ | apt-cache add | n/a | cp $filename /usr/portage/distfiles |
| Extract a package | tar -Jxvf | rpm2cpio | cpio -vid | dpkg-deb -x | rpm2cpio | cpio -vid | tar -jxvf |
| Install/Remove packages to satisfy build-dependencies. Uses information in the source package. | automatic | dnf builddep | apt-get build-dep | zypper si -d | emerge -o |
| Display the source package to the given package name(s) | dnf repoquery -s | apt-cache showsrc | n/a |
| Downloads the corresponding source package(s) to the given package name(s) | Use [ABS](/index.php/ABS "ABS") && makepkg -o | dnf download --source | apt-get source / debcheckout | zypper source-install | emerge --fetchonly |
| Build a package | makepkg -s | rpmbuild -ba (normal)
mock (in chroot) | debuild | rpmbuild -ba; build; osc build | ebuild; quickpkg |
| Check for possible packaging issues | namcap | rpmlint | lintian | rpmlint | repoman |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## See also

*   [Changes in DNF CLI compared to Yum](http://dnf.readthedocs.org/en/latest/cli_vs_yum.html)
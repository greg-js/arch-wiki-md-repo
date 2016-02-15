This page pulls heavily from [openSUSE's Software Management Command Line Comparison](http://en.opensuse.org/Software_Management_Command_Line_Comparison). It has been simplified and has added Arch to the comparison, as well as modified the order in which each distribution exists for the benefit of Arch users.

| **Action** | **arch** | **redhat/fedora** | **debian/ubuntu** | **old suse** | **opensuse** | **gentoo** |
| Instalacija paketa po imenu | pacman -S | yum install | apt-get install | rug install | zypper install zypper in | emerge [-a] |
| Uklanjanje paketa po imenu | pacman -R | yum remove/erase | apt-get remove | rug remove/erase | zypper remove zypper rm | emerge -C |
| Pretraga paketa. | pacman -Ss | yum search | apt-cache search | rug search | zypper search zypper se [-s] | emerge -S |
| Sinhronizacija riznice i nadograđivanje zastarelih paketa | pacman -Syu | yum update | apt-get upgrade | rug update | zypper update zypper up | emerge -u world |
| Nadogradnja nove distribucije. | pacman -Syu | yum upgrade | apt-get dist-upgrade | zypper dup | emerge -uDN world |
| Reinstalacija paketa. | pacman -S | apt-get install --reinstall | zypper install --force | emerge [-a] |
| Instalacija binarnih paketa koji se nalaze na fizičkom mediju | pacman -U | yum localinstall | dpkg -i && apt-get install -f | zypper in /path/to/local.rpm | emerge |
| Nadogradnja paketa koji su instalirani kao binarni | pacman -U | yum localupdate | n/a | emerge |
| Popravljanje loših međuzavisnosti | pacman dep level - testdb, shared lib level - findbrokenpkgs or lddd | apt-get --fix-broken | rug* solvedeps | n/a | revdep-rebuild |
| Preuzimanje zadatog paketa bez installacije, ili raspakivanja | pacman -Sw | yumdownloader (found in yum-utils package) | apt-get --download-only | n/a | emerge --fetchonly |
| Remove dependencies that are no longer needed, because e.g. the package which needed the dependencies was removed. | pacman -R `pacman -Qqtd` | apt-get autoremove | n/a | emerge --depclean |
| Downloads the corresponding source package(s) to the given package name(s) | yaourt -G <package> && makepkg -o | apt-get source | zypper source-install | emerge --fetchonly |
| Install/Remove packages to satisfy buid-dependencies. Uses information in the source package. | automatic | apt-get build-dep | zypper si -d | emerge -o |
| Add a package lock rule to keep its current state from being changed | ${EDITOR} /etc/pacman.conf
modify IgnorePkg array | yum.conf <--”exclude” option (add/amend) | echo "$PKGNAME hold" | dpkg --set-selections | rug* lock-add | Put package name in /etc/zypp/locks | /etc/portage/package.mask |
| Delete a package lock rule | remove package from IgnorePkg line in /etc/pacman.conf | yum.conf <--”exclude” option (remove/amend) | echo "$PKGNAME install" | dpkg --set-selections | rug* lock-delete | Remove package name from /etc/zypp/locks | /etc/portage/package.mask (or package.unmask) |
| Show a listing of all lock rules | cat /etc/pacman.conf | yum.conf (research needed) | /etc/apt/preferences | rug* lock-list | View /etc/zypp/locks | cat /etc/portage/package.mask |
| Add a checkpoint to the package system for later rollback | rug* checkpoint-add | n/a |
| Remove a checkpoint from the system | N/A | rug* checkpoint-remove | n/a |
| Provide a list of all system checkpoints | N/A | rug* checkpoints | n/a |
| Rolls entire packages back to a certain date or checkpoint. | N/A | rug* rollback | n/a |
| Package information management |
| Get a dump of the whole system information - Prints, Saves or similar the current state of the package management system. Preferred output is text or XML. One version of rug dumps information as a sqlite database. (Note: Why either-or here? No tool offers the option to choose the output format.) | (see /var/lib/pacman/local) | (see /var/lib/rpm/Packages) | apt-cache stats | rug dump | n/a | emerge --info |
| Show all or most information about a package. The tools\' verbosity for the default command vary. But with options, the tools are on par with each other. | pacman -[S|Q]i | yum list or info | apt-cache showpkg apt-cache show | rug info | zypper info zypper if | emerge -S; emerge -pv |
| Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par. | pacman -Ss | yum search | apt-cache search | rug search | zypper search zypper se [-s] | emerge -S |
| Lists packages which have an update available. Note: Some provide special commands to limit the output to certain installation sources, others use options. | pacman -Qu | yum list updates yum check-update | apt-get upgrade -> n | rug list-updates rug summary | zypper list-updates zypper patch-check (just for patches) | emerge -uDNp world |
| Display a list of all packages in all installation sources that are handled by the packages management. Some tools provide options or additional commands to limit the output to a specific installation source. | pacman -Sl | yum list available | apt-cache dumpavail apt-cache dump (Cache only) apt-cache pkgnames | rug packages | IN PROGRESS | emerge -ep world |
| Displays packages which provide the given exp. aka reverse provides. Mainly a shortcut to search a specific field. Other tools might offer this functionality through the search command. | pkgfile <filename> | yum whatprovides yum provides | apt-file search <filename> | rug what-provides | zypper what-provides    zypper wp | equery belongs (only installed packages) |
| Display packages which require X to be installed, aka show reverse/ dependencies. rug\'s what-requires can operate on more than just package names. | pacman -Qi | yum resolvedep | apt-cache rdepends | rug what-requires | IN PROGRESS | equery depends |
| Display packages which conflict with given expression (often package). Search can be used as well to mimic this function. rug\'s what-conflicts function operates on more than just package names | (none) | rug info-conflicts rug what-conflicts | IN PROGRESS |
| List all packages which are required for the given package, aka show dependencies. | pacman -[S|Q]i | yum deplist | apt-cache depends | rug info-requirements | IN PROGRESS | emerge -ep |
| List what the current package provides | yum provides | rug info-provides | IN PROGRESS |
| List the files that the package holds. Again, this functionality can be mimicked by other more complex commands. | pacman -Ql $pkgname
pkgfile -l | yum provides | apt-file list | rug* file-list | IN PROGRESS | equery files |
| Search all packages to find the one which holds the specified file. auto-apt is using this functionality. | pkgfile -s | yum provides yum whatprovides | apt-file search | rug* package-file rug what-provides | IN PROGRESS | equery belongs |
| Display all packages that the specified packages obsoletes. | yum list obsoletes | apt-cache / grep | rug info-obsoletes | IN PROGRESS |
| Verify dependencies of the complete system. Used if installation process was forcefully killed. | N/A | yum deplist | apt-get check ? apt-cache unmet | rug verify rug* dangling-requires | n/a | emerge -uDN world |
| Generates a list of installed packages | pacman -Q | yum list installed | apt-cache --installed | n/a | emerge -ep world |
| List packages that are installed but are not available in any installation source (anymore). | pacman -Qm | yum list extras | n/a |
| List packages that were recently added to one of the installation sources, i.e. which are new to it. Note: Synaptic has this functionality, however apt doesn\'t seem to be the provider. | (none) | yum list recent | n/a |
| Show a log of actions taken by the software management. | cat /var/log/pacman.log | cat /var/log/dpkg.log | rug history | n/a | located in /var/log/portage |
| Clean up all local caches. Options might limit what is actually cleaned. Autoclean removes only unneeded, obsolete information. | pacman -Sc
pacman -Scc | yum clean | apt-get clean apt-get autoclean | n/a |
| Add a local package to the local package cache mostly for debugging purposes. | cp $pkgname /var/cache/pacman/pkg/ | apt-cache add | n/a |
| Display the source package to the given package name(s) | apt-cache showsrc | n/a |
| Generates an output suitable for processing with dotty for the given package(s). | apt-cache dotty | n/a |
| Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source. | ${EDITOR} /etc/pacman.conf
Modify HoldPkg and/or IgnorePkg arrays | yum-plugin-priorities and yum-plugin-protect-packages | /etc/apt/preferences smart priority –set | n/a |
| Remove a previously set priority | /etc/apt/preferences smart priority --remove | n/a |
| Show a list of set priorities. | apt-cache policy /etc/apt/preferences smart priority --show | n/a |
| Ignores problems that priorities may trigger. | n/a |
| Installation sources management | ${EDITOR} /etc/pacman.conf |
| Add an installation source to the system. Some tools provide additional commands for certain sources, others allow all types of source URI for the add command. Again others, like apt and yum force editing a sources list. apt-cdrom is a special command, which offers special options design for CDs/DVDs as source. | ${EDITOR} /etc/pacman.conf | apt-cdrom add | rug service-add rug mount /local/dir | zypper service-add | layman, overlays |
| Refresh the information about the specified installation source(s) or all installation sources. | pacman -Sy | yum check-update | apt-get update | rug refresh | zypper refresh zypper ref | layman -f |
| Prints a list of all installation sources including important information like URI, alias etc. | cat /etc/pacman.d/mirrorlist | rug service-list | zypper service-list |
| Other commands |
| Start a shell Start a shell to enter multiple commands in one session | yum shell | apt-config shell | zypper shell |
| Package Verification |
| Single package | rpm -V <package> | debsums | rpm -V <package> | rpm -V <package> | equery check |
| All packages | rpm -Va | debsums | rpm -Va | rpm -Va | equery check |
| Package Querying |
| List installed local packages along with version | pacman -Q | rpm -qa | dpkg-query -l | emerge -e world |
| Display package information: Name, version, description, etc. | pacman -Qi | rpm -qi | dpkg-query -p | emerge -pv and emerge -S |
| Display files provided by package | pacman -Ql | rpm -ql | dpkg-query -L | equery files |
| Query the package which provides FILE | pacman -Qo | rpm -qf | dpkg-query -S |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg-deb -I |
| Show the changelog of a package | pacman -Qc | rpm -q --changelog | equery changes -f |
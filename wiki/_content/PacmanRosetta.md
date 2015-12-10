# Pacman/Rosetta

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

See [pacman](/index.php/Pacman "Pacman") for the main article.

This page pulls heavily from [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison). It has been simplified and has added Arch to the comparison, as well as modified the order in which each distribution exists for the benefit of Arch users.

**Tip:** Arch users having to temporarily deal with another Linux distribution can use [pacapt](https://github.com/icy/pacapt), a simple wrapper around other package managers.

**Note:**

*   Some of the tools described here are specific to a certain version of pacman. The -Qk option is new in pacman 4.1.
*   The command `pkgfile` can be found in the [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) package.

<table>

<tbody>

<tr>

<td align="center" style="background:#f0f0f0;">**<font color="#707070">Action</font>**</td>

<td align="center" style="background:#f0f0f0;">**Arch**</td>

<td align="center" style="background:#f0f0f0;">**Red Hat/Fedora**</td>

<td align="center" style="background:#f0f0f0;">**Debian/Ubuntu**</td>

<td align="center" style="background:#f0f0f0;">**SUSE/openSUSE**</td>

<td align="center" style="background:#f0f0f0;">**Gentoo**</td>

</tr>

<tr>

<td>Install a package(s) by name</td>

<td>pacman -S</td>

<td>dnf install</td>

<td>apt-get install</td>

<td>zypper install  
zypper in</td>

<td>emerge [-a]</td>

</tr>

<tr style="background:#e4e4e4">

<td>Remove a package(s) by name</td>

<td>pacman -Rs</td>

<td>dnf remove</td>

<td>apt-get autoremove</td>

<td>zypper remove  
zypper rm</td>

<td>emerge -C</td>

</tr>

<tr>

<td>Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par.</td>

<td>pacman -Ss</td>

<td>dnf search</td>

<td>apt-cache search</td>

<td>zypper search  
zypper se [-s]</td>

<td>emerge -S</td>

</tr>

<tr style="background:#e4e4e4">

<td>Upgrade Packages - Install packages which have an older version already installed</td>

<td>pacman -Syu</td>

<td>dnf upgrade</td>

<td>apt-get update; apt-get upgrade</td>

<td>zypper update zypper up</td>

<td>emerge -u world</td>

</tr>

<tr>

<td>Upgrade Packages - Another form of the update command, which can perform more complex updates -- like distribution upgrades. When the usual update command will omit package updates, which include changes in dependencies, this command can perform those updates.</td>

<td>pacman -Syu</td>

<td>dnf distro-sync</td>

<td>apt-get dist-upgrade</td>

<td>zypper dup</td>

<td>emerge -uDN world</td>

</tr>

<tr style="background:#e4e4e4">

<td>Reinstall given Package - Will reinstall the given package without dependency hassle.</td>

<td>pacman -S</td>

<td>dnf reinstall</td>

<td>apt-get install --reinstall</td>

<td>zypper install --force</td>

<td>emerge [-a]</td>

</tr>

<tr>

<td>Installs local package file, e.g. app.rpm and uses the installation sources to resolve dependencies</td>

<td>pacman -U</td>

<td>dnf install</td>

<td>dpkg -i && apt-get install -f</td>

<td>zypper in /path/to/local.rpm</td>

<td>emerge</td>

</tr>

<tr style="background:#e4e4e4">

<td>Updates package(s) with local packages and uses the installation sources to resolve dependencies</td>

<td>pacman -U</td>

<td>dnf upgrade</td>

<td>debi</td>

<td>emerge</td>

</tr>

<tr>

<td>Use some magic to fix broken dependencies in a system</td>

<td>pacman dep level - testdb, shared lib level - findbrokenpkgs or lddd</td>

<td>dnf repoquery --unsatisfied</td>

<td>apt-get --fix-broken  
aptitude install</td>

<td>zypper verify</td>

<td>revdep-rebuild</td>

</tr>

<tr style="background:#e4e4e4">

<td>Only downloads the given package(s) without unpacking or installing them</td>

<td>pacman -Sw</td>

<td>dnf download</td>

<td>apt-get install --download-only (into the package cache)  
apt-get download (bypass the package cache)</td>

<td>zypper --download-only</td>

<td>emerge --fetchonly</td>

</tr>

<tr>

<td>Remove dependencies that are no longer needed, because e.g. the package which needed the dependencies was removed.</td>

<td>pacman -Qdtq | pacman -Rs -</td>

<td>dnf autoremove</td>

<td>apt-get autoremove</td>

<td>zypper rm -u</td>

<td>emerge --depclean</td>

</tr>

<tr style="background:#e4e4e4">

<td>Downloads the corresponding source package(s) to the given package name(s)</td>

<td>Use [ABS](/index.php/ABS "ABS") && makepkg -o</td>

<td>dnf download --source</td>

<td>apt-get source / debcheckout</td>

<td>zypper source-install</td>

<td>emerge --fetchonly</td>

</tr>

<tr style="background:#e4e4e4">

<td>Remove packages no longer included in any repositories.</td>

<td>package-cleanup --orphans</td>

<td>aptitude purge '~o'</td>

</tr>

<tr>

<td>Install/Remove packages to satisfy build-dependencies. Uses information in the source package.</td>

<td>automatic</td>

<td>dnf builddep</td>

<td>apt-get build-dep</td>

<td>zypper si -d</td>

<td>emerge -o</td>

</tr>

<tr style="background:#e4e4e4">

<td>Add a package lock rule to keep its current state from being changed</td>

<td>/etc/pacman.conf  
modify IgnorePkg array</td>

<td>dnf.conf <--”exclude” option (add/amend)</td>

<td>apt-mark hold pkg</td>

<td>Put package name in /etc/zypp/locks, or zypper al</td>

<td>/etc/portage/package.mask</td>

</tr>

<tr>

<td>Delete a package lock rule</td>

<td>remove package from IgnorePkg line in /etc/pacman.conf</td>

<td>apt-mark unhold pkg</td>

<td>Remove package name from /etc/zypp/locks</td>

<td>/etc/portage/package.mask (or package.unmask)</td>

</tr>

<tr style="background:#e4e4e4">

<td>Show a listing of all lock rules</td>

<td>cat /etc/pacman.conf</td>

<td>/etc/apt/preferences</td>

<td>View /etc/zypp/locks</td>

<td>cat /etc/portage/package.mask</td>

</tr>

<tr>

<td>Add a checkpoint to the package system for later rollback</td>

<td>(unnecessary, done on every transaction)</td>

<td>n/a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Remove a checkpoint from the system</td>

<td>N/A</td>

<td>N/A</td>

<td>n/a</td>

</tr>

<tr>

<td>Provide a list of all system checkpoints</td>

<td>N/A</td>

<td>dnf history list</td>

<td>n/a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Rolls entire packages back to a certain date or checkpoint.</td>

<td>N/A</td>

<td>dnf history rollback</td>

<td>n/a</td>

</tr>

<tr>

<td>Undo a single specified transaction.</td>

<td>N/A</td>

<td>dnf history undo</td>

<td>n/a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Mark a package previously installed as a dependency as explicitly required.</td>

<td>pacman -D --asexplicit</td>

<td>apt-mark manual</td>

<td>emerge --select</td>

</tr>

<tr>

<td>Install package(s) as dependency / without marking as explicitly required.</td>

<td>pacman -S --asdeps</td>

<td>aptitude install 'pkg&M'</td>

<td>emerge -1</td>

</tr>

<tr>

<td>_**Package information management**_</td>

</tr>

<tr style="background:#e4e4e4">

<td>Get a dump of the whole system information - Prints, Saves or similar the current state of the package management system. Preferred output is text or XML. (Note: Why either-or here? No tool offers the option to choose the output format.)</td>

<td>(see /var/lib/pacman/local)</td>

<td>(see /var/lib/rpm/Packages)</td>

<td>apt-cache stats</td>

<td>n/a</td>

<td>emerge --info</td>

</tr>

<tr>

<td>Show all or most information about a package. The tools' verbosity for the default command vary. But with options, the tools are on par with each other.</td>

<td>pacman -[S|Q]i</td>

<td>dnf list, dnf info</td>

<td>apt-cache show / apt-cache policy</td>

<td>zypper info zypper if</td>

<td>emerge -S; emerge -pv; eix</td>

</tr>

<tr style="background:#e4e4e4">

<td>Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par.</td>

<td>pacman -Ss</td>

<td>dnf search</td>

<td>apt-cache search</td>

<td>zypper search zypper se [-s]</td>

<td>emerge -S</td>

</tr>

<tr>

<td>Display changelogs</td>

<td>apt-get changelog</td>

</tr>

<tr style="background:#e4e4e4">

<td>e-mail delivery of package changes</td>

<td>apt-get install apt-listchanges</td>

</tr>

<tr>

<td>Lists packages which have an update available. Note: Some provide special commands to limit the output to certain installation sources, others use options.</td>

<td>pacman -Qu</td>

<td>dnf list updates, dnf check-update</td>

<td>apt-get upgrade -> n</td>

<td>zypper list-updates zypper patch-check (just for patches)</td>

<td>emerge -uDNp world</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display a list of all packages in all installation sources that are handled by the packages management. Some tools provide options or additional commands to limit the output to a specific installation source.</td>

<td>pacman -Sl</td>

<td>dnf list available</td>

<td>apt-cache dumpavail apt-cache dump (Cache only) apt-cache pkgnames</td>

<td>zypper packages</td>

<td>emerge -ep world</td>

</tr>

<tr>

<td>Displays packages which provide the given exp. aka reverse provides. Mainly a shortcut to search a specific field. Other tools might offer this functionality through the search command.</td>

<td>pkgfile <filename></td>

<td>dnf provides</td>

<td>apt-file search <filename></td>

<td>zypper what-provides zypper wp</td>

<td>equery belongs (only installed packages); pfl</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display packages which require X to be installed, aka show reverse/ dependencies.</td>

<td>pacman -Sii</td>

<td>dnf provides</td>

<td>apt-cache rdepends / aptitude search ~Dpattern</td>

<td>IN PROGRESS</td>

<td>equery depends</td>

</tr>

<tr>

<td>Display packages which conflict with given expression (often package). Search can be used as well to mimic this function.</td>

<td>repoquery --whatconflicts</td>

<td>aptitude search '~Cpattern'</td>

</tr>

<tr style="background:#e4e4e4">

<td>List all packages which are required for the given package, aka show dependencies.</td>

<td>pacman -[S|Q]i</td>

<td>dnf repoquery --requires</td>

<td>apt-cache depends / apt-cache show</td>

<td>zypper info --requires</td>

<td>emerge -ep</td>

</tr>

<tr>

<td>List what the current package provides</td>

<td>dnf provides</td>

<td>dpkg -s / aptitude show</td>

<td>IN PROGRESS</td>

<td>equery files</td>

</tr>

<tr style="background:#e4e4e4">

<td>List the files that the package holds. Again, this functionality can be mimicked by other more complex commands.</td>

<td>pacman -Ql $pkgname  
pkgfile -l</td>

<td>dnf repoquery -l $pkgname</td>

<td>dpkg-query -L $pkgname</td>

<td>equery files</td>

</tr>

<tr>

<td>List all packages that require a particular package</td>

<td>repoquery --whatrequires [--recursive]</td>

<td>aptitude search \~D{depends,recommends,suggests}:pattern / aptitude why pkg</td>

<td>equery depends -a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Search all packages to find the one which holds the specified file. auto-apt is using this functionality.</td>

<td>pkgfile -s</td>

<td>dnf provides</td>

<td>apt-file search</td>

<td>equery belongs</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display all packages that the specified packages obsoletes.</td>

<td>dnf list obsoletes</td>

<td>apt-cache show</td>

<td>IN PROGRESS</td>

</tr>

<tr>

<td>Verify dependencies of the complete system. Used if installation process was forcefully killed.</td>

<td>testdb</td>

<td>dnf repoquery --requires</td>

<td>apt-get check</td>

<td>n/a</td>

<td>emerge -uDN world</td>

</tr>

<tr style="background:#e4e4e4">

<td>Generates a list of installed packages</td>

<td>pacman -Q</td>

<td>dnf list installed</td>

<td>dpkg --list | grep ^i</td>

<td>zypper</td>

<td>emerge -ep world</td>

</tr>

<tr>

<td>List packages that are installed but are not available in any installation source (anymore).</td>

<td>pacman -Qm</td>

<td>dnf list extras</td>

<td>deborphan</td>

<td>zypper se -si | grep 'System Packages'</td>

<td>eix-test-obsolete</td>

</tr>

<tr style="background:#e4e4e4">

<td>List packages that were recently added to one of the installation sources, i.e. which are new to it.</td>

<td>(none)</td>

<td>dnf list recent</td>

<td>aptitude search '~N' / aptitude forget-new</td>

<td>n/a</td>

<td>eix-diff</td>

</tr>

<tr>

<td>Show a log of actions taken by the software management.</td>

<td>cat /var/log/pacman.log</td>

<td>dnf history</td>

<td>cat /var/log/dpkg.log</td>

<td>cat /var/log/zypp/history</td>

<td>located in /var/log/portage</td>

</tr>

<tr style="background:#e4e4e4">

<td>Clean up all local caches. Options might limit what is actually cleaned. Autoclean removes only unneeded, obsolete information.</td>

<td>pacman -Sc  
pacman -Scc</td>

<td>dnf clean all</td>

<td>apt-get clean / apt-get autoclean / aptitude clean</td>

<td>zypper clean</td>

<td>eclean distfiles</td>

</tr>

<tr>

<td>Add a local package to the local package cache mostly for debugging purposes.</td>

<td>cp $pkgname /var/cache/pacman/pkg/</td>

<td>apt-cache add</td>

<td>n/a</td>

<td>cp $srcfile /usr/portage/distfiles</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display the source package to the given package name(s)</td>

<td>repoquery -s</td>

<td>apt-cache showsrc</td>

<td>n/a</td>

</tr>

<tr>

<td>Generates an output suitable for processing with dotty for the given package(s).</td>

<td>apt-cache dotty</td>

<td>n/a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source.</td>

<td>${EDITOR} /etc/pacman.conf  
Modify HoldPkg and/or IgnorePkg arrays</td>

<td>/etc/apt/preferences, apt-cache policy</td>

<td>zypper mr -p</td>

<td>${EDITOR} /etc/portage/package.keywords  
Add a line with =category/package-version</td>

</tr>

<tr>

<td>Remove a previously set priority</td>

<td>/etc/apt/preferences</td>

<td>zypper mr -p</td>

<td>${EDITOR} /etc/portage/package.keywords  
remove offending line</td>

</tr>

<tr style="background:#e4e4e4">

<td>Show a list of set priorities.</td>

<td>apt-cache policy /etc/apt/preferences</td>

<td>n/a</td>

<td>cat /etc/portage/package.keywords</td>

</tr>

<tr>

<td>Ignores problems that priorities may trigger.</td>

<td>n/a</td>

</tr>

<tr style="background:#e4e4e4">

<td>Installation sources management</td>

<td>${EDITOR} /etc/pacman.conf</td>

<td>${EDITOR} /etc/yum.repos.d/${REPO}.repo</td>

<td>${EDITOR} /etc/apt/sources.list</td>

<td>layman</td>

</tr>

<tr>

<td>Add an installation source to the system. Some tools provide additional commands for certain sources, others allow all types of source URI for the add command. Again others, like apt and dnf force editing a sources list. apt-cdrom is a special command, which offers special options design for CDs/DVDs as source.</td>

<td>/etc/pacman.conf</td>

<td>/etc/yum.repos.d/*.repo</td>

<td>apt-cdrom add</td>

<td>zypper service-add</td>

<td>layman, overlays</td>

</tr>

<tr style="background:#e4e4e4">

<td>Refresh the information about the specified installation source(s) or all installation sources.</td>

<td>pacman -Sy ([always upgrade the whole system afterwards](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance"))</td>

<td>dnf clean expire-cache && dnf check-update</td>

<td>apt-get update</td>

<td>zypper refresh zypper ref</td>

<td>layman -f</td>

</tr>

<tr>

<td>Prints a list of all installation sources including important information like URI, alias etc.</td>

<td>cat /etc/pacman.d/mirrorlist</td>

<td>cat /etc/yum.repos.d/*</td>

<td>apt-cache policy</td>

<td>zypper service-list</td>

<td>layman -l</td>

</tr>

<tr style="background:#e4e4e4">

<td>Disable an installation source for an operation</td>

<td>dnf --disablerepo=</td>

<td>emerge package::repo-to-use</td>

</tr>

<tr>

<td>Download packages from a different version of the distribution than the one installed.</td>

<td>dnf --releasever=</td>

<td>apt-get install -t release package/ apt-get install package/release (deps not covered)</td>

<td>echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package</td>

</tr>

<tr>

<td>_**Other commands**_</td>

</tr>

<tr>

<td>Start a shell to enter multiple commands in one session</td>

<td>apt-config shell</td>

<td>zypper shell</td>

</tr>

<tr style="background:#e4e4e4">

<td>_**Package Verification**_</td>

</tr>

<tr>

<td>Single package</td>

<td>pacman -Qk[k] <package></td>

<td>rpm -V <package></td>

<td>debsums</td>

<td>rpm -V <package></td>

<td>equery check</td>

</tr>

<tr style="background:#e4e4e4">

<td>All packages</td>

<td>pacman -Qk[k]</td>

<td>rpm -Va</td>

<td>debsums</td>

<td>rpm -Va</td>

<td>equery check</td>

</tr>

<tr>

<td>_**Package Querying**_</td>

</tr>

<tr style="background:#e4e4e4">

<td>List installed local packages along with version</td>

<td>pacman -Q</td>

<td>rpm -qa</td>

<td>dpkg -l</td>

<td>emerge -e world</td>

</tr>

<tr>

<td>Display local package information: Name, version, description, etc.</td>

<td>pacman -Qi</td>

<td>rpm -qi</td>

<td>dpkg -s / aptitude show</td>

<td>emerge -pv and emerge -S</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display remote package information: Name, version, description, etc.</td>

<td>pacman -Si</td>

<td>dnf info</td>

<td>apt-cache show / aptitude show</td>

<td>emerge -pv and emerge -S</td>

</tr>

<tr>

<td>Display files provided by local package</td>

<td>pacman -Ql</td>

<td>rpm -ql</td>

<td>dpkg -L</td>

<td>equery files</td>

</tr>

<tr style="background:#e4e4e4">

<td>Display files provided by a remote package</td>

<td>pkgfile -l</td>

<td>repoquery -l</td>

<td>apt-file list pattern</td>

<td>pfl</td>

</tr>

<tr>

<td>Query the package which provides FILE</td>

<td>pacman -Qo</td>

<td>rpm -qf (installed only) or dnf provides (everything)</td>

<td>dpkg -S / dlocate</td>

<td>equery belongs</td>

</tr>

<tr style="background:#e4e4e4">

<td>Query a package supplied on the command line rather than an entry in the package management database</td>

<td>pacman -Qp</td>

<td>rpm -qp</td>

<td>dpkg -I</td>

</tr>

<tr>

<td>Show the changelog of a package</td>

<td>pacman -Qc</td>

<td>rpm -q --changelog</td>

<td>apt-get changelog</td>

<td>equery changes -f</td>

</tr>

<tr style="background:#e4e4e4">

<td>Search locally installed package for names or descriptions</td>

<td>pacman -Qs</td>

<td>rpm -qa '*<str>*'</td>

<td>aptitude search '~i(~n name|~d description)'</td>

<td>eix -S -I</td>

</tr>

<tr>

<td>List packages not required by any other package</td>

<td>pacman -Qt</td>

<td>package-cleanup --all --leaves</td>

<td>deborphan -anp1</td>

</tr>

<tr>

<td>_**Building Packages**_</td>

</tr>

<tr style="background:#e4e4e4">

<td>Build a package</td>

<td>makepkg -s</td>

<td>rpmbuild -ba (normal)  
mock (in chroot)</td>

<td>debuild</td>

<td>rpmbuild -ba</td>

<td>ebuild; quickpkg</td>

</tr>

<tr>

<td>Check for possible packaging issues</td>

<td>namcap</td>

<td>rpmlint</td>

<td>lintian</td>

<td>repoman</td>

</tr>

<tr style="background:#e4e4e4">

<td>List the contents of a package file</td>

<td>pacman -Qpl <file></td>

<td>rpmls rpm -qpl</td>

<td>dpkg -c</td>

<td>rpm -qpl</td>

</tr>

<tr>

<td>Extract a package</td>

<td>tar -Jxvf</td>

<td>rpm2cpio | cpio -vid</td>

<td>dpkg-deb -x</td>

<td>rpm2cpio | cpio -vid</td>

<td>tar -jxvf</td>

</tr>

<tr style="background:#e4e4e4">

<td>Query a package supplied on the command line rather than an entry in the package management database</td>

<td>pacman -Qp</td>

<td>rpm -qp</td>

<td>dpkg -I</td>

</tr>

<tr>

<td align="center" style="background:#f0f0f0;">**<font color="#707070">Action</font>**</td>

<td align="center" style="background:#f0f0f0;">**Arch**</td>

<td align="center" style="background:#f0f0f0;">**Red Hat/Fedora**</td>

<td align="center" style="background:#f0f0f0;">**Debian/Ubuntu**</td>

<td align="center" style="background:#f0f0f0;">**SUSE/openSUSE**</td>

<td align="center" style="background:#f0f0f0;">**Gentoo**</td>

</tr>

</tbody>

</table>

## See also

*   [Changes in DNF CLI compared to Yum](http://dnf.readthedocs.org/en/latest/cli_vs_yum.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman/Rosetta&oldid=409661](https://wiki.archlinux.org/index.php?title=Pacman/Rosetta&oldid=409661)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")
Esta página usa uma tabela para exibir a correspondência dos comandos de [gerenciamento de pacotes](https://en.wikipedia.org/wiki/pt:Sistema_gestor_de_pacotes "wikipedia:pt:Sistema gestor de pacotes") entre algumas das distribuições Linux mais populares. A inspiração original foi dada pela [comparação da linha de comando de gerenciamento de software do openSUSE](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison).

**Dica:** Os usuários do Arch que precisam lidar temporariamente com outra distribuição Linux podem usar o [pacapt](https://github.com/icy/pacapt), um simples wrapper em torno de outros gerenciadores de pacotes.

**Nota:**

*   Algumas das ferramentas descritas aqui são específicas para uma determinada versão do *pacman*. A opção `-Qk` é nova no *pacman* 4.1.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Operações básicas](#Operações_básicas)
*   [2 Consultando pacotes específicos](#Consultando_pacotes_específicos)
*   [3 Consultando listas de pacotes](#Consultando_listas_de_pacotes)
*   [4 Consultando dependências de pacotes](#Consultando_dependências_de_pacotes)
*   [5 Gerenciamento de fontes de instalação](#Gerenciamento_de_fontes_de_instalação)
*   [6 Sobreposição](#Sobreposição)
*   [7 Verificação e correção](#Verificação_e_correção)
*   [8 Usando arquivos de pacotes e compilando pacotes](#Usando_arquivos_de_pacotes_e_compilando_pacotes)
*   [9 Veja também](#Veja_também)

## Operações básicas

| **<font color="#707070">Ação</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Instalar pacote(s) por nome | pacman -S | dnf install | apt install | zypper install
zypper in | emerge [-a] |
| Remover pacote(s) por nome | pacman -Rs | dnf remove | apt remove | zypper remove
zypper rm | emerge -vc |
| Procurar por pacote(s), pesquisando a expressão no nome, descrição, breve descrição. Quais campos exatos estão sendo pesquisados por padrão variam em cada ferramenta. Principalmente opções trazem ferramentas no par. | pacman -Ss | dnf search | apt search | zypper search
zypper se [-s] | emerge -S |
| Atualizar pacotes - Instalar pacotes que têm uma versão antiga já instalada | pacman -Syu | dnf upgrade | apt update && apt upgrade | zypper update zypper up | emerge -uDN @world |
| Atualizar pacotes - Outra forma do comando de atualização, que pode realizar atualizações mais complexas -- como atualizações de distribuição. Quando o comando de atualização usual omitir as atualizações de pacotes, que incluem alterações nas dependências, esse comando pode realizar essas atualizações. | pacman -Syu | dnf distro-sync | apt update && apt dist-upgrade | zypper dup | emerge -uDN @world |
| Limpar todos os caches locais. As opções podem limitar o que é realmente limpo. A limpeza automática remove apenas informações obsoletas e desnecessárias. | pacman -Sc
pacman -Scc | dnf clean all | apt autoclean
apt clean | zypper clean | eclean distfiles |
| Remover dependências que não são mais necessárias, porque, por exemplo, o pacote que precisava das dependências foi removido. | pacman -Qdtq | pacman -Rs - | dnf autoremove | apt autoremove | zypper rm -u | emerge --depclean |
| Remover pacotes não mais incluídos em nenhum repositório. | pacman -Qmq | pacman -Rs - | dnf repoquery --extras | aptitude purge '~o' |
| Marcar um pacote, previamente instalado como dependência, como explicitamente necessário. | pacman -D --asexplicit | dnf mark install | apt-mark manual | emerge --select |
| Instalar pacote(s) como dependência / sem marcar como explicitamente necessário. | pacman -S --asdeps | dnf install => dnf mark remove | apt-mark auto | emerge -1 |
| Baixar apenas o(s) pacote(s) fornecido(s) sem desempacotá-lo(s) ou instalá-lo(s) | pacman -Sw | dnf download | apt install --download-only (para o cache de pacotes)
apt download (evitar o cache de pacotes) | zypper --download-only | emerge --fetchonly |
| Iniciar um shell para inserir vários comandos em uma sessão | apt-config shell | zypper shell |
| Mostrar um registro log de ações realizadas pelo gerenciamento de softwares. | cat /var/log/pacman.log | dnf history | cat /var/log/dpkg.log | cat /var/log/zypp/history | located in /var/log/portage |
| Obter um despejo de toda a informação do sistema - Exibe, salva, ou outra operação semelhante, o estado atual do sistema de gerenciamento de pacotes. A saída preferida é texto ou XML. (Nota: Por que aqui? Nenhuma ferramenta oferece a opção de escolher o formato de saída.) | (see /var/lib/pacman/local) | (see /var/lib/rpm/Packages) | apt-cache stats | n/a | emerge --info |
| Entrega de e-mail de alterações de pacotes | apt install apt-listchanges |
| **<font color="#707070">Ação</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultando pacotes específicos

| **<font color="#707070">Ação</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Mostrar todas ou a maioria das informações sobre um pacote. A nível de detalhamento das ferramentas para o comando padrão varia. Mas com opções, as ferramentas estão no mesmo nível. | pacman -[S|Q]i | dnf list, dnf info | apt show / apt-cache policy | zypper info zypper if | emerge -S; emerge -pv; eix |
| Exibir informações de pacotes locais: Nome, versão, descrição, etc. | pacman -Qi | rpm -qi / dnf info installed | dpkg -s / aptitude show | zypper info; rpm -qi | emerge -pv e emerge -S |
| Exibir informações do pacote remoto: nome, versão, descrição etc. | pacman -Si | dnf info | apt-cache show / aptitude show | zypper info | emerge -pv e emerge -S ou equery m (meta) |
| Exibir arquivos fornecidos pelo pacote local | pacman -Ql | rpm -ql | dpkg -L | rpm -Ql | equery files; qlist |
| Exibir arquivos fornecidos por um pacote remoto | pacman -Fl | dnf repoquery -l ou repoquery -l (do pacote yum-utils) | apt-file list $pattern | pfl |
| Consultar o pacote que fornece um determinado arquivo | pacman -Qo | rpm -qf (instalado apenas) ou dnf provides (tudo) ou repoquery -f (do pacote yum-utils) | dpkg -S / dlocate | zypper search -f | equery belongs; qfile |
| Listar os arquivos que o pacote detém. Novamente, essa funcionalidade pode ser imitada por outros comandos mais complexos. | pacman -Ql
pacman -Fl | dnf repoquery -l | dpkg-query -L | rpm -ql | equery files; qlist |
| Exibir pacotes que fornecem a experiência, também conhecido como *reverse provides* (inverso de "provê"). É principalmente um atalho para procurar um campo específico. Outras ferramentas podem oferecer essa funcionalidade por meio do comando de pesquisa. | pacman -Fo | dnf provides | apt-file search | zypper what-provides zypper wp | equery belongs (apenas pacotes instalados); pfl |
| Pesquisar todos os pacotes para encontrar aquele que contém o arquivo especificado. O utilitário *auto-apt* está usando essa funcionalidade. | pacman -Fs | dnf provides | apt-file search | zypper search -f | equery belongs; qfile |
| Mostrar o registro das mudanças de um pacote | pacman -Qc | rpm -q --changelog | apt-get changelog | rpm -q --changelog | equery changes -f |
| **<font color="#707070">Ação</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultando listas de pacotes

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Search for package(s) by searching the expression in name, description, short description. What exact fields are being searched by default varies in each tool. Mostly options bring tools on par. | pacman -Ss | dnf search | apt search | zypper search zypper se [-s] | emerge -S; eix |
| Lists packages which have an update available. Note: Some provide special commands to limit the output to certain installation sources, others use options. | pacman -Qu | dnf list updates, dnf check-update | apt-get upgrade -> n | zypper list-updates zypper patch-check (just for patches) | emerge -uDNp @world |
| Display a list of all packages in all installation sources that are handled by the packages management. Some tools provide options or additional commands to limit the output to a specific installation source. | pacman -Sl | dnf list available | apt-cache dumpavail apt-cache dump (Cache only) apt-cache pkgnames | zypper packages | portageq all_best_visible / |
| Generates a list of installed packages | pacman -Q | dnf list installed | dpkg --list | grep ^i | zypper search --installed-only | qlist -IC |
| List packages that are installed but are not available in any installation source (anymore). | pacman -Qm | dnf list extras | deborphan | zypper se -si | grep 'System Packages' | eix-test-obsolete |
| List packages that were recently added to one of the installation sources, i.e. which are new to it. | (none) | dnf list recent | aptitude search '~N' / aptitude forget-new | n/a | eix-diff |
| List installed local packages along with version | pacman -Q | rpm -qa | dpkg -l | zypper search -s; rpm -qa | qlist -ICv |
| Search locally installed package for names or descriptions | pacman -Qs | rpm -qa '*<str>*' | aptitude search '~i(~n $name|~d $description)' | eix -S -I |
| List packages not required by any other package | pacman -Qt | dnf leaves | deborphan -anp1 | emerge -pc |
| List packages installed explicitly (not as dependencies) | pacman -Qe | dnf history userinstalled | apt-mark showmanual | emerge -pvO @selected; eix --selected |
| List packages installed automatically (as dependencies) | pacman -Qd | apt-mark showauto |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultando dependências de pacotes

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Display packages which require X to be installed, aka show reverse dependencies. | pacman -Sii | dnf repoquery --alldeps --whatrequires or repoquery --whatr[equires] | apt-cache rdepends / aptitude search ~D$pattern | zypper search --requires | emerge -pvc |
| Display packages which conflict with given expression (often package). Search can be used as well to mimic this function. | dnf repoquery --conflicts | aptitude search '~C$pattern' |
| List all packages which are required for the given package, aka show dependencies. | pacman -[S|Q]i | dnf repoquery --requires or repoquery -R | apt-cache depends / apt-cache show | zypper info --requires | emerge -ep |
| List what the current package provides | dnf provides | dpkg -s / aptitude show | zypper info --provides | equery files; qlist |
| List all packages that require a particular package | dnf repoquery --alldeps --whatrequires | aptitude search ~D{depends,recommends,suggests}:$pattern / aptitude why | zypper search --requires | equery depends -a |
| Display all packages that the specified packages obsoletes. | dnf list obsoletes | apt-cache show |
| Generates an output suitable for processing with dotty for the given package(s). | apt-cache dotty | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Gerenciamento de fontes de instalação

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Installation sources management | ${EDITOR} /etc/pacman.conf | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | ${EDITOR} /etc/apt/sources.list | ${EDITOR} /etc/zypp/repos.d/${REPO}.repo | layman; eselect repository |
| Add an installation source to the system. Some tools provide additional commands for certain sources, others allow all types of source URI for the add command. Again others, like apt and dnf force editing a sources list. apt-cdrom is a special command, which offers special options design for CDs/DVDs as source. | /etc/pacman.conf | /etc/yum.repos.d/*.repo | apt-cdrom add | zypper service-add | layman, overlays |
| Refresh the information about the specified installation source(s) or all installation sources. | pacman -Sy ([always upgrade the whole system afterwards](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance")) | dnf clean expire-cache && dnf check-update | apt-get update | zypper refresh zypper ref | emerge --sync;layman -S |
| Prints a list of all installation sources including important information like URI, alias etc. | cat /etc/pacman.d/mirrorlist | cat /etc/yum.repos.d/* | apt-cache policy | zypper service-list | layman -l; eselect repository list |
| List all packages from a certain repo | paclist <repo> | eix --in-overlay |
| Disable an installation source for an operation | dnf --disablerepo= | emerge package::repo-to-use |
| Download packages from a different version of the distribution than the one installed. | dnf --releasever= | apt-get install -t release package/ apt-get install package/release (deps not covered) | echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Sobreposição

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Add a package lock rule to keep its current state from being changed | /etc/pacman.conf
modify IgnorePkg array | dnf.conf <--”exclude” option (add/amend) | apt-mark hold pkg | Put package name in /etc/zypp/locks, or zypper al | /etc/portage/package.mask |
| Delete a package lock rule | remove package from IgnorePkg line in /etc/pacman.conf | apt-mark unhold pkg | Remove package name from /etc/zypp/locks or zypper rl | /etc/portage/package.mask (or package.unmask) |
| Show a listing of all lock rules | cat /etc/pacman.conf | /etc/apt/preferences | View /etc/zypp/locks or zypper ll | cat /etc/portage/package.mask |
| Set the priority of the given package to avoid upgrade, force downgrade or to overwrite any default behavior. Can also be used to prefer a package version from a certain installation source. | ${EDITOR} /etc/pacman.conf
Modify HoldPkg and/or IgnorePkg arrays | /etc/apt/preferences, apt-cache policy | zypper mr -p | ${EDITOR} /etc/portage/package.accept_keywords
Add a line with =category/package-version |
| Remove a previously set priority | /etc/apt/preferences | zypper mr -p | ${EDITOR} /etc/portage/package.accept_keywords
remove offending line |
| Show a list of set priorities. | apt-cache policy /etc/apt/preferences | zypper lr -p | grep -r . /etc/portage/package.accept_keywords |
| Ignores problems that priorities may trigger. | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Verificação e correção

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Verify single package | pacman -Qk[k] | rpm -V | debsums | rpm -V | equery check |
| Verify all packages | pacman -Qk[k] | rpm -Va | debsums | rpm -Va | equery check |
| Reinstall given Package - Will reinstall the given package without dependency hassle. | pacman -S | dnf reinstall | apt install --reinstall | zypper install --force | emerge -1O |
| Verify dependencies of the complete system. Used if installation process was forcefully killed. | pacman -Dk | dnf repoquery --requires | apt-get check | zypper verify | emerge -uDN @world |
| Use some magic to fix broken dependencies in a system | pacman dep level - pacman -Dk, shared lib level - findbrokenpkgs or lddd | dnf repoquery --unsatisfied | apt-get --fix-broken
aptitude install | zypper verify | revdep-rebuild |
| Add a checkpoint to the package system for later rollback | (unnecessary, done on every transaction) | n/a |
| Remove a checkpoint from the system | N/A | N/A | n/a |
| Provide a list of all system checkpoints | N/A | dnf history list | n/a |
| Rolls entire packages back to a certain date or checkpoint. | N/A | dnf history rollback | n/a |
| Undo a single specified transaction. | N/A | dnf history undo | n/a |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Usando arquivos de pacotes e compilando pacotes

| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Query a package supplied on the command line rather than an entry in the package management database | pacman -Qp | rpm -qp | dpkg -I |
| List the contents of a package file | pacman -Qpl | rpmls rpm -qpl | dpkg -c | rpm -qpl |
| Installs local package file, e.g. app.rpm and uses the installation sources to resolve dependencies | pacman -U | dnf install | apt install | zypper in | emerge |
| Updates package(s) with local packages and uses the installation sources to resolve dependencies | pacman -U | dnf upgrade | debi | emerge |
| Add a local package to the local package cache mostly for debugging purposes. | cp $filename /var/cache/pacman/pkg/ | apt-cache add | n/a | cp $filename /usr/portage/distfiles |
| Extract a package | tar -Jxvf | rpm2cpio | cpio -vid | dpkg-deb -x | rpm2cpio | cpio -vid | tar -jxvf |
| Install/Remove packages to satisfy build-dependencies. Uses information in the source package. | Use [ABS](/index.php/ABS "ABS") && makepkg -seoc | dnf builddep | apt-get build-dep | zypper si -d | emerge -o |
| Display the source package to the given package name(s) | dnf repoquery -s | apt-cache showsrc | n/a |
| Downloads the corresponding source package(s) to the given package name(s) | Use [ABS](/index.php/ABS "ABS") && makepkg -o | dnf download --source | apt-get source / debcheckout | zypper source-install | emerge --fetchonly |
| Build a package | makepkg -s | rpmbuild -ba (normal)
mock (in chroot) | debuild | rpmbuild -ba; build; osc build | ebuild; quickpkg |
| Check for possible packaging issues | namcap | rpmlint | lintian | rpmlint | repoman |
| **<font color="#707070">Action</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Veja também

*   [Changes in DNF CLI compared to Yum](http://dnf.readthedocs.org/en/latest/cli_vs_yum.html)
**Estado de la traducción**
Este artículo es una traducción de [Pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta"), revisada por última vez el **2018-11-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman/Rosetta&diff=0&oldid=549543) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Esta página utiliza una tabla comparativa para mostrar la correspondencia entre las órdenes para [gestionar paquetes](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") de algunas de las distribuciones de Linux más populares. La inspiración original fue dada por [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison).

**Sugerencia:** los usuarios de Arch que tengan que lidiar temporalmente con otra distribución de Linux pueden usar [pacapt](https://github.com/icy/pacapt), un [wrapper](https://en.wikipedia.org/wiki/es:Wrapper "wikipedia:es:Wrapper") sencillo prestado para gestionar paquetes de otros.

**Nota:** algunas de las herramientas que se describen aquí son específicas para una determinada versión de pacman. La opción `**-Qk**` es nueva en pacman 4.1.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Operaciones básicas](#Operaciones_básicas)
*   [2 Consultar paquetes específicos](#Consultar_paquetes_específicos)
*   [3 Consultar listas de paquetes](#Consultar_listas_de_paquetes)
*   [4 Consultar dependencias de paquetes](#Consultar_dependencias_de_paquetes)
*   [5 Gestionar fuentes o repositorios de instalación](#Gestionar_fuentes_o_repositorios_de_instalación)
*   [6 Anulaciones](#Anulaciones)
*   [7 Verificación y reparación](#Verificación_y_reparación)
*   [8 Utilizar archivos de paquetes y compilar paquetes](#Utilizar_archivos_de_paquetes_y_compilar_paquetes)
*   [9 Véase también](#Véase_también)

## Operaciones básicas

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Instala un paquete(s) por su nombre | `pacman -S` | dnf install | apt install | zypper install
zypper in | emerge [-a] |
| Elimina un paquete(s) por su nombre | `pacman -Rs` | dnf remove | apt remove | zypper remove
zypper rm | emerge -C |
| Busca paquete(s) por la expresión del nombre, descripción, etc. Según la distribución, varía cada campo buscado por defecto. La mayoría de las opciones que aportan las distintas herramientas (de las distribuciones) son parecidas. | `pacman -Ss` | dnf search | apt search | zypper search
zypper se [-s] | emerge -S |
| Actualizar paquete(s): instala los paquetes mas actuales respecto de los que haya una versión anterior instalada en el sistema. | `pacman -Syu` | dnf upgrade | apt update && apt upgrade | zypper update zypper up | emerge -u world |
| Actualizar paquete(s): otra forma de utilizar la orden anterior de actualización, que puede realizar cambios más complejos, como actualizaciones de la distribución. Cuando la orden usual para actualizar un paquete omite la actualización de dicho paquete porque requiere cambios en las dependencias, esta orden, por el contrario, si puede realizar dichas actualizaciones. | `pacman -Syu` | dnf distro-sync | apt update && apt dist-upgrade | zypper dup | emerge -uDN world |
| Limpia toda la memoria caché local. Las opciones pueden limitar lo que realmente se limpia. Autoclean solo elimina información innecesaria y obsoleta. | `pacman -Sc`
`pacman -Scc` | dnf clean all | apt autoclean
apt clean | zypper clean | eclean distfiles |
| Elimina las dependencias que ya no son necesarias, por ejemplo, en el caso de que el paquete que necesitaba las dependencias haya sido eliminado. | `pacman -Qdtq` | `pacman -Rs -` | dnf autoremove | apt autoremove | zypper rm -u | emerge --depclean |
| Eliminar paquetes que ya no están incluidos en ningún repositorio. | `pacman -Qmq`|`pacman -Rs -` | dnf repoquery --extras | aptitude purge '~o' |
| Marca un paquete como requerido explícitamente, el cual había sido previamente instalado como una dependencia. | `pacman -D --asexplicit` | dnf mark install | apt-mark manual | emerge --select |
| Instala paquete(s) como dependencia/sin marcar como requerido explícitamente. | `pacman -S --asdeps` | dnf install => dnf mark remove | apt-mark auto | emerge -1 |
| Descarga únicamente los paquetes dados sin descomprimirlos o instalarlos | `pacman -Sw` | dnf download | apt install --download-only (en la caché del paquete)
apt download (omite la caché del paquete) | zypper --download-only | emerge --fetchonly |
| Lanza un intérprete de órdenes para ingresar varias órdenes en una sesión | apt-config shell | zypper shell |
| Mostra un registro de las acciones realizadas por el gestor del software. | `cat /var/log/pacman.log` | dnf history | cat /var/log/dpkg.log | cat /var/log/zypp/history | ubicado en /var/log/portage |
| Se obtiene un volcado de toda la información del sistema: imprime, guarda o similar el estado actual del sistema de gestión de paquetes. La salida preferida es texto o XML. (Nota: ¿por qué esto es así? Ninguna herramienta ofrece la opción de elegir el formato de salida). | (véase `/var/lib/pacman/local`) | (véase /var/lib/rpm/Packages) | apt-cache stats | n/d | emerge --info |
| Entrega por correo electrónico los cambios de paquetes | apt install apt-listchanges |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultar paquetes específicos

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Muestra toda o la mayor parte de la información sobre un paquete. La precisión de la información proporcinada por las herramientas de las distintas distribuciones varía según la órden predeterminada. Pero con opciones adicionales, las herramientas están a la par unas con otras. | `pacman -[S|Q]i` | dnf list, dnf info | apt show / apt-cache policy | zypper info zypper if | emerge -S; emerge -pv; eix |
| Muestra información del paquete local: nombre, versión, descripción, etc. | `pacman -Qi` | rpm -qi | dpkg -s / aptitude show | zypper info; rpm -qi | emerge -pv and emerge -S |
| Muestra información del paquete remoto: nombre, versión, descripción, etc. | `pacman -Si` | dnf info | apt-cache show / aptitude show | zypper info | emerge -pv and emerge -S o equery m (meta) |
| Muestra los archivos proporcionados por un paquete local. | `pacman -Ql` | rpm -ql | dpkg -L | rpm -Ql | equery files |
| Muestra los archivos proporcionados por un paquete remoto. | `pacman -Fl` | dnf repoquery -l o repoquery -l (del paquete yum-utils) | apt-file list $pattern | pfl |
| Consulta el paquete que proporciona FILE. | `pacman -Qo` | pm -qf (solo instalado) o dnf provides (todo) o repoquery -f (del paquete yum-utils) | dpkg -S / dlocate | zypper search -f | equery belongs |
| Lista los archivos que contiene el paquete. De nuevo, esta funcionalidad puede ser compaginada por otras órdenes más complejas. | `pacman -Ql`
`pacman -Fl` | dnf repoquery -l | dpkg-query -L | rpm -ql | equery files |
| Muestra los paquetes que proporcionan la expresión. Principalmente es un atajo para buscar un campo específico. Otras herramientas pueden ofrecer esta funcionalidad a través de la orden de búsqueda. | `pacman -Fo` | dnf provides | apt-file search | zypper what-provides zypper wp | equery belongs (solo paquetes instalados); pfl |
| Busca en todos los paquetes para encontrar el que contiene el archivo especificado. auto-apt utiliza esta funcionalidad. | `pacman -Fs` | dnf provides | apt-file search | zypper search -f | equery belongs |
| Muestra el registro de cambios de un paquete. | `pacman -Qc` | rpm -q --changelog | apt-get changelog | rpm -q --changelog | equery changes -f |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultar listas de paquetes

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Busca el paquete(s) por la expresión dada, esto es por nombre o breve descripción. Los campos exactos que se buscan por defecto en cada herramientas son parecidas. | `pacman -Ss` | dnf search | apt search | zypper search zypper se [-s] | emerge -S |
| Enumera los paquetes que tienen una actualización disponible. Nota: Algunos proporcionan órdenes especiales para limitar la salida a ciertas fuentes o repositorios de instalación, otros usan opciones. | `pacman -Qu` | dnf list updates, dnf check-update | apt-get upgrade -> n | zypper list-updates zypper patch-check (just for patches) | emerge -uDNp world |
| Muestra una lista de todos los paquetes presentes en todos los repositorios de instalación que son manejados por el gestor de paquetes. Algunas herramientas proporcionan opciones u órdenes adicionales para limitar la salida a una fuente o repositorio de instalación específico. | `pacman -Sl` | dnf list available | apt-cache dumpavail apt-cache dump (solo caché) apt-cache pkgnames | zypper packages | emerge -ep world |
| Genera una lista de paquetes instalados. | `pacman -Q` | dnf list installed | dpkg --list | grep ^i | zypper search --installed-only | emerge -ep world |
| Enumera los paquetes que están instalados pero que ya no están disponibles en ningún repositorio de instalación (más). | `pacman -Qm` | dnf list extras | deborphan | zypper se -si | grep 'System Packages' | eix-test-obsolete |
| Enumera los paquetes que se agregaron recientemente a una de las fuentes o repositorios de instalación, es decir, que son nuevos en él. | (nada) | dnf list recent | aptitude search '~N' / aptitude forget-new | n/d | eix-diff |
| Lista los paquetes locales instalados junto con su versión. | `pacman -Q` | rpm -qa | dpkg -l | zypper search -s; rpm -qa | emerge -e world |
| Busca los paquetes instalados localmente por nombres o descripciones. | `pacman -Qs` | rpm -qa '*<str>*' | aptitude search '~i(~n $name|~d $description)' | eix -S -I |
| Lista los paquetes que no son requeridos por ningún otro paquete | `pacman -Qt` | package-cleanup --all --leaves | deborphan -anp1 |
| Lista los paquetes instalados explícitamente (no como dependencias). | `pacman -Qe` | dnf history userinstalled | apt-mark showmanual |
| Lista los paquetes instalados automáticamente (como dependencias). | `pacman -Qd` | apt-mark showauto |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Consultar dependencias de paquetes

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Muestra los paquetes que requieren X para instalarse, también se muestran las dependencias inversas. | `pacman -Sii` | dnf repoquery --alldeps --whatrequires o repoquery --whatr[equires] | apt-cache rdepends / aptitude search ~D$pattern | zypper search --requires | equery depends |
| Muestra los paquetes que entran en conflicto con la expresión dada (a menudo un paquete). La función de búsqueda también se puede utilizar para imitar esta característica. | dnf repoquery --conflicts | aptitude search '~C$pattern' |
| Enumere todos los paquetes que se requieren para el paquete dado, también conocido como mostrar dependencias. | `pacman -[S|Q]i` | dnf repoquery --requires o repoquery -R | apt-cache depends / apt-cache show | zypper info --requires | emerge -ep |
| Lista qué proporciona el paquete actual. | dnf provides | dpkg -s / aptitude show | zypper info --provides | equery files |
| Lista todos los paquetes que requiere un paquete particular. | dnf repoquery --alldeps --whatrequires | aptitude search ~D{depends,recommends,suggests}:$pattern / aptitude why | zypper search --requires | equery depends -a |
| Muestra todos los paquetes que se especifican como obsoletos. | dnf list obsoletes | apt-cache show |
| Genera una salida adecuada para el procesamiento con dotty para el paquete(s) dado. | apt-cache dotty | n/d |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Gestionar fuentes o repositorios de instalación

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Gestionar repositorios de instalación | `${EDITOR} /etc/pacman.conf` | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | ${EDITOR} /etc/apt/sources.list | ${EDITOR} /etc/zypp/repos.d/${REPO}.repo | layman |
| Añadir una fuente de instalación al sistema. Algunas herramientas proporcionan órdenes adicionales para ciertas fuentes, otras permiten todos los tipos de URI de fuente para la orden. Otros, como apt y dnf fuerzan la edición de una lista de fuentes. apt-cdrom es una orden especial, que ofrece opciones de diseño especial para CD/DVD como fuente. | `/etc/pacman.conf` | /etc/yum.repos.d/*.repo | apt-cdrom add | zypper service-add | layman, overlays |
| Actualizar la información sobre todas las fuentes de instalación o para aquellas especificadas. | `pacman -Sy` ([actualiza siempre todo el sistema posteriormente](/index.php/System_maintenance_(Espa%C3%B1ol)#Las_actualizaciones_parciales_no_son_compatibles "System maintenance (Español)")) | dnf clean expire-cache && dnf check-update | apt-get update | zypper refresh zypper ref | emerge --sync;layman -S |
| Imprimir una lista de todas las fuentes de instalación, incluida la información importante como URI, alias, etc. | `cat /etc/pacman.d/mirrorlist` | cat /etc/yum.repos.d/* | apt-cache policy | zypper service-list | layman -l |
| Lista todos los paquetes de un determinado repositorio. | `paclist <repositorio>` |
| Desactiva una fuente de instalación para una operación. | dnf --disablerepo= | emerge package::repo-to-use |
| Descarga los paquetes de una versión diferente de la distribución respecto de la que está instalada. | dnf --releasever= | apt-get install -t release package/ apt-get install package/release (dependencias no cubiertas) | echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Anulaciones

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Añade una regla de bloqueo de un paquete para evitar que se modifique su estado actual | `/etc/pacman.conf`
modificar matriz `IgnorePkg` | dnf.conf <--opción ”exclude” (agregar/enmendar) | apt-mark hold pkg | Coloque el nombre del paquete en /etc/zypp/locks, o zypper al | /etc/portage/package.mask |
| Elimina una regla de bloqueo de un paquete | quitar el paquete de la línea `IgnorePkg` en `/etc/pacman.conf` | apt-mark unhold pkg | Elimine el nombre del paquete de /etc/zypp/locks o zypper rl | /etc/portage/package.mask (o package.unmask) |
| Muestra una lista de todas las reglas de bloqueo | `cat /etc/pacman.conf` | /etc/apt/preferences | ver /etc/zypp/locks o zypper ll | cat /etc/portage/package.mask |
| Establece la prioridad del paquete dado para evitar su actualización, forzar la degradación o sobrescribir cualquier comportamiento predeterminado. También se puede utilizar para preferir una versión de paquete de una determinada fuente o repositorio de instalación. | `${EDITOR} /etc/pacman.conf`
Modificar las matrices `HoldPkg` y/o `IgnorePkg` | /etc/apt/preferences, apt-cache policy | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
Añadir una línea con =category/package-version |
| Elimina una prioridad previamente establecida. | /etc/apt/preferences | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
elimine línea ofensiva |
| Muestra una lista de prioridades establecidas. | apt-cache policy /etc/apt/preferences | zypper lr -p | cat /etc/portage/package.keywords |
| Ignora los problemas que las prioridades pueden desencadenar. | n/d |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Verificación y reparación

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Verifica un único paquete. | `pacman -Qk[k]` | rpm -V | debsums | rpm -V | equery check |
| Verifica todos los paquetes. | `pacman -Qk[k]` | rpm -Va | debsums | rpm -Va | equery check |
| Reinstala el paquete dado: reinstalará el paquete dado sin problemas de las dependencias que maneja. | `pacman -S` | dnf reinstall | apt install --reinstall | zypper install --force | emerge -1O |
| Verifica dependencias del sistema completo. Se usa si el proceso de instalación fue cancelado por la fuerza. | `pacman -Dk` | dnf repoquery --requires | apt-get check | zypper verify | emerge -uDN world |
| Utiliza algo de magia para arreglar dependencias rotas en un sistema. | `pacman dep level - pacman -Dk`, `shared lib level - findbrokenpkgs` o `lddd` | dnf repoquery --unsatisfied | apt-get --fix-broken
aptitude install | zypper verify | revdep-rebuild |
| Añade un punto de control al sistema de paquetes para una posterior reversión. | (innecesario, realizado en cada transacción) | n/d |
| Elimina un punto de control del sistema. | n/d | n/d | n/d |
| Proporciona una lista de todos los puntos de control del sistema. | n/d | dnf history list | n/d |
| Devuelve los paquetes completos a una fecha o punto de control determinados. | n/d | dnf history rollback | n/d |
| Deshace una sola transacción especificada. | n/d | dnf history undo | n/d |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Utilizar archivos de paquetes y compilar paquetes

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SLES/openSUSE** | **Gentoo** |
| Consulta un paquete suministrado en la línea de órdenes en lugar de una entrada en la base de datos del gestor de paquetes. | `pacman -Qp` | rpm -qp | dpkg -I |
| Lista el contenido de un archivo de paquete. | `pacman -Qpl` | rpmls rpm -qpl | dpkg -c | rpm -qpl |
| Instala el archivo del paquete local, por ejemplo. app.rpm y usa las fuentes de instalación para resolver dependencias. | `pacman -U` | dnf install | apt install | zypper in | emerge |
| Actualiza los paquetes con paquetes locales y utiliza las fuentes de instalación para resolver las dependencias. | `pacman -U` | dnf upgrade | debi | emerge |
| Agrega un paquete local a la caché del paquete local principalmente para propósitos de depuración de errores. | `cp $filename /var/cache/` `pacman/pkg/` | apt-cache add | n/d | cp $filename /usr/portage/distfiles |
| Extrae un paquete. | `tar -Jxvf` | rpm2cpio | cpio -vid | dpkg-deb -x | rpm2cpio | cpio -vid | tar -jxvf |
| Instala/elimina paquetes para satisfacer dependencias de compilación. Utiliza información presente en el paquete fuente. | automático | dnf builddep | apt-get build-dep | zypper si -d | emerge -o |
| Muestra el paquete fuente correspondiente al nombre del paquete(s) dado. | dnf repoquery -s | apt-cache showsrc | n/d |
| Descarga el paquete(s) fuente correspondiente al nombre del paquete(s) dado. | Utiliza [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") && `makepkg -o` | dnf download --source | apt-get source / debcheckout | zypper source-install | emerge --fetchonly |
| Compila un paquete. | `makepkg -s` | rpmbuild -ba (normal)
mock (en chroot) | debuild | rpmbuild -ba; build; osc build | ebuild; quickpkg |
| Comprueba posibles problemas de empaquetado. | `namcap` | rpmlint | lintian | rpmlint |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **SUSE/openSUSE** | **Gentoo** |

## Véase también

*   [Changes in DNF CLI compared to Yum](http://dnf.readthedocs.org/en/latest/cli_vs_yum.html)
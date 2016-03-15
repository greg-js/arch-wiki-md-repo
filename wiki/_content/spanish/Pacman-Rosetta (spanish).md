Esta página está fuertemente inspirada en [openSUSE's Software Management Command Line Comparison](http://old-en.opensuse.org/Software_Management_Command_Line_Comparison). Se ha simplificado la comparación y se le ha añadido Arch, y también se ha modificado el orden en el que se muestra cada distribución para una ilustración más clara en beneficio de los usuarios de Arch.

Los usuarios de otras distribuciones de Linux pueden beneficiarse de pacman usando un wrapper sencillo: [pacapt](https://github.com/icy/pacapt). El script también podría ser utilizado por los usuarios de Arch que tienen que tratar temporalmente con otra distribución.

[pacapt](https://github.com/icy/pacapt) es una implementación del script de la shell de pacman para otras distribuciones linux.

**Nota:**

*   Algunas de las herramientas que se describen aquí son específicas para una determinada versión de pacman. La opción `**-Qk**` es nueva en pacman 4.1.
*   La orden `pkgfile` se puede encontrar en el paquete [pkgfile](https://www.archlinux.org/packages/?name=pkgfile).

| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **(Antiguo) SUSE** | **openSUSE** | **Gentoo** |
| **ÓRDENES GENERALES** |
| **Instalar paquete(s):**
Por el nombre | `**pacman -S**` | yum install | apt-get install | rug install | zypper install zypper in | emerge [-a] |
| **Eliminar paquete(s):**
Por el nombre | `**pacman -Rc**` | yum remove/erase | apt-get remove | rug remove/erase | zypper remove zypper rm | emerge -C |
| **Buscar paquete(s):**
Por la expresión del nombre, descripción, etc. Según la distribución, varía cada campo buscado por defecto. La mayoría de las opciones que aportan las distintas herramientas (de las distribuciones) son parecidas. | `**pacman -Ss**` | yum search | apt-cache search | rug search | zypper search zypper se [-s] | emerge -S |
| **Actualizar paquete(s):**
Instala los paquetes mas actuales respecto de los que hay una versión anterior instalada en el sistema. | `**pacman -Syu**` | yum update | apt-get upgrade | rug update | zypper update zypper up | emerge -u world |
| **Actualizar paquete(s):**
Otra forma de utilizar la orden anterior de actualización, que puede realizar cambios más complejos, como actualizaciones de la distribución. Cuando la orden usual para actualizar un paquete omite la actualización del paquete porque requiere cambios en las dependencias, esta orden, por el contrario, si puede realizar dichas actualizaciones. | `**pacman -Syu**` | yum distro-sync | apt-get dist-upgrade | zypper dup | emerge -uDN world |
| **Reinstalar paquete(s):**
La orden reinstalará el paquete indicado, sin problemas de dependencias. | `**pacman -S**` | yum reinstall | apt-get install --reinstall | zypper install --force | emerge [-a] |
| **Instalar los archivos de un paquete local:**
Instala los archivos de paquetes locales, por ejemplo, app.rpm, y utiliza los repositorios para resolver dependencias. | `**pacman -U**` | yum localinstall | dpkg -i && apt-get install -f | zypper in /path/to/local.rpm | emerge |
| **Actualizar paquete(s) con paquetes locales:**
Actualiza un paquete(s) con paquetes locales, utilizando los repositorios para resolver las dependencias. | `**pacman -U**` | yum localupdate | N/D | emerge |
| **Arreglar dependencias rotas:**
Soluciona dependencias rotas en un sistema. | `**pacman dep level - testdb, shared lib level - findbrokenpkgs o lddd**` | package-cleanup --problems | apt-get --fix-broken | rug* solvedeps | zypper verify | revdep-rebuild |
| **Descargar paquete(s):**
Solo descarga el paquete indicado, sin instalar ni desempaquetar. | `**pacman -Sw**` | yumdownloader (encontrado en yum-utils package) | apt-get --download-only | zypper --download-only | emerge --fetchonly |
| **Eliminar dependencias:**
Quita las dependencias que ya no son necesarias, como cuando, por ejemplo, el paquete que las necesitaba se ha retirado. | `**pacman -Qdtq**` | `**pacman -Rs -**` | package-cleanup --leaves | apt-get autoremove | N/D | emerge --depclean |
| **Descargar fuentes:**
Descarga el paquete(s) fuente correspondiente al nombre(s) del paquete indicado. | Utilice `**[ABS](/index.php/ABS "ABS")**` && `**makepkg -o**` | yumdownloader --source | apt-get source | zypper source-install | emerge --fetchonly |
| Elimina los paquetes que ya no están presentes en nigún repositorio. | package-cleanup --orphans |
| **Instalar/desinstalar dependencias:**
Instala/desinstala paquetes para satisfacer las dependencias de compilación. Utiliza la información del paquete fuente. | automático | yum-builddep | apt-get build-dep | zypper si -d | emerge -o |
| **Bloquear descarga de paquete(s):**
Agrega una regla de bloqueo del paquete indicado para mantener su estado actual frente al cambio. | `**${EDITOR} /etc/pacman.conf**`
modifique la matriz IgnorePkg | yum.conf <--”exclude” option (add/amend) | echo "$PKGNAME hold" | dpkg --set-selections | rug* lock-add | Poner nombre del paquete en /etc/zypp/locks | /etc/portage/package.mask |
| **Desbloquear descarga de paquete(s):**
Elimina una regla de bloqueo de un paquete. | Elimine el nombre del paquete presente en la línea IgnorePkg de /etc/pacman.conf | yum.conf <--”exclude” option (remove/amend) | echo "$PKGNAME install" | dpkg --set-selections | rug* lock-delete | Remover nombre del paquete desde /etc/zypp/locks | /etc/portage/package.mask (o package.unmask) |
| **Listar reglas de bloqueo:**
Muestra una lista de todas las reglas de bloqueo. | `**cat /etc/pacman.conf**` | yum.conf (necesita buscar) | /etc/apt/preferences | rug* lock-list | View /etc/zypp/locks | cat /etc/portage/package.mask |
| **Crear punto de restauración**
Añade un punto de control al sistema de paquetes para poder restaurarlo más tarde. | (innecesario, hecho en cada transacción) | rug* checkpoint-add | N/D |
| **Eliminar punto de restauración**
Elimina un punto de restauración del sistema. | N/D | N/D | rug* checkpoint-remove | N/D |
| **Listar puntos de restauración:**
Proporciona una lista de todos los puntos de restauración del sistema. | N/D | yum history list | rug* checkpoints | N/D |
| **Revertir paquetes enteros:**
Restaura un conjunto de paquetes enteros a una fecha determinada o punto de restauración. | N/D | yum history rollback | rug* rollback | N/D |
| **Deshacer una transacción:**
Deshace una transacción especificada. | N/D | yum history undo | N/D |
| **Dependencias:**
Marcar un paquete previamente instalado como una dependencia requerida explícitamente como tal. | `**pacman -D --asexplicit**` | emerge --select |
| **Dependencias:**
Instalar paquetes como dependencias / sin marcar como explícitamente requerido. | `**pacman -S --asdeps**` | emerge -1 |
| **GESTIONAR INFORMACIÓN DE PAQUETES** |
| **Información del sistema:**
Obtiene un volcado de la información del sistema entero - Imprime, guarda o similar el estado actual del sistema de gestión de paquetes. La salida preferida es texto o XML. Una versión de la información básica volcada se creará como una base de datos sqlite. (Nota: ¿por qué esto es así? Ninguna herramienta ofrece la opción de elegir el formato de salida.) | (véase `**/var/lib/pacman/local**`) | (véase /var/lib/rpm/Packages) | apt-cache stats | rug dump | N/D | emerge --info |
| **Información de un paquete:**
Muestra toda o la mayor parte de la información sobre un paquete. La precisión de la información proporcinada por las herramientas de las distintas distribuciones varía según el comando por defecto. Pero con las opciones añadidas, las herramientas están a la par unas con otras. | `**pacman -[S|Q]i**` | yum list o info | apt-cache showpkg apt-cache show | rug info | zypper info zypper if | emerge -S; emerge -pv; eix |
| **Buscar paquete(s):**
Búsqueda de paquete(s) según la expresión proporcionada, como el nombre, descripción, etc. Qué campos exactos están siendo buscados por defecto varían según cada herramienta (de la distribución). La mayoría de las opciones son parecidas entre las distintas herramientas. | `**pacman -Ss**` | yum search | apt-cache search | rug search | zypper search zypper se [-s] | emerge -S |
| **Listar paquetes actualizables:**
Genera una lista de los paquetes que tienen una actualización disponible. Nota: algunas herramientas ofrecen órdenes especiales para limitar la salida a ciertas fuentes de instalación, otras proporcionan opciones. | `**pacman -Qu**` | yum list updates yum check-update | apt-get upgrade -> n | rug list-updates rug summary | zypper list-updates zypper patch-check (solo para parches) | emerge -uDNp world |
| **Listar paquetes disponibles:**
Muestra una lista de todos los paquetes presentes en todos los repositorios que son manejados por el gestor de paquetes. Algunas herramientas ofrecen opciones y órdenes adicionales para limitar la salida a un repositorio específico. | `**pacman -Sl**` | yum list available | apt-cache dumpavail apt-cache dump (solo caché) apt-cache pkgnames | rug packages | zypper packages | emerge -ep world |
| **Listar paquetes demandantes:**
Muestra los paquetes a los cuales da respuesta al nombre del paquete expresado, es decir provee la reversión (en otras palabras, enumera los paquetes a los que satisface dependencias). Principalmente es un atajo para buscar un entorno específico. Otras herramientas pueden ofrecer esta funcionalidad a través de las órdenes de búsqueda. | `**pkgfile <nombredelarchivo>**` | yum whatprovides yum provides | apt-file search <nombredelarchivo> | rug what-provides | zypper what-provides    zypper wp | equery belongs (solo paquetes instalados); pfl |
| **Buscar paquetes que requieran X para instalarse:**
Muestra los paquetes que requieren X para ser instalado, es decir, muestra las reversiones/dependencias. La orden what-requires de rug puede funcionar con algo más que los nombres de paquetes. | `**pacman -Sii**` | yum resolvedep | apt-cache rdepends | rug what-requires | EN PROCESO | equery depends |
| **Buscar paquetes en conflicto:**
Muestra los paquetes que entran en conflicto con la expresión dada (a menudo un paquete). Las órdenes de búsqueda pueden ser utilizadas también para imitar esta función. La función what-conflicts de rug realiza otras operaciones a parte de proveer el nombre de los paquetes. | (ninguno) | repoquery --whatconflicts | rug info-conflicts rug what-conflicts | EN PROCESO |
| **Lista los paquetes requeridos por un paquete:**
Genera una lista de todos los paquetes que son necesarios para el paquete indicado, esto es, muestra las dependencias. | `**pacman -[S|Q]i**` | yum deplist | apt-cache depends | rug info-requirements | EN PROCESO | emerge -ep |
| **Lista los componentes de un paquete:**
Genera una lista de lo que el paquete actual ofrece. | yum provides | rug info-provides | EN PROCESO | equery files |
| **Lista los archivos contenidos en un paquete:**
Genera una lista de los archivos que contiene un paquete. Una vez más, esta funcionalidad puede ser imitada por otras órdenes más complejas. | `**pacman -Ql $pkgname**`
`**pkgfile -l**` | yum provides | apt-file list | rug* file-list | EN PROCESO | equery files |
| **Lista los paquetes dependientes de otro:**
Muestra todos los paquetes que requieren un paquete en particular. | repoquery --whatrequires [--recursive] | equery depends -a |
| **Busca los paquetes que contienen un archivo:**
Busca en todos los paquetes para encontrar el que contiene el archivo especificado. auto-apt utiliza esta funcionalidad. | `**pkgfile -s**` | yum provides yum whatprovides | apt-file search | rug* package-file rug what-provides | EN PROCESO | equery belongs |
| **Muestra paquetes obsoletos:**
Muestra todos los paquetes que se especifican como obsoletos. | yum list obsoletes | apt-cache / grep | rug info-obsoletes | EN PROCESO |
| **Comprueba las dependencias del sistema:**
Se utiliza cuando el proceso de instalación fue forzado de antemano a terminar. | `**testdb**` | yum deplist | apt-get check ? apt-cache unmet | rug verify rug* dangling-requires | N/D | emerge -uDN world |
| **Lista los paquetes instalados:**
Genera una lista de los paquetes instalados. | `**pacman -Q**` | yum list installed | dpkg --get-selections | zypper | emerge -ep world |
| **Lista los paquetes huérfanos instalados:**
Genera una lista de los paquetes que están instalados, pero que no disponen (más) de ninguna fuente de instalación. | `**pacman -Qm**` | yum list extras | zypper se -si | grep 'System Packages' | eix-test-obsolete |
| **Lista los paquetes recientemente añadidos:**
Lista los paquetes que se han añadido recientemente a una de las fuentes de instalación, es decir, que son nuevos en la misma. Nota: Synaptic tiene esta funcionalidad, sin embargo, apt no parece proveerlo. | (ninguno) | yum list recent | N/D | eix-diff |
| **Registra la gestión del software:**
Muestra un registro de las acciones tomadas por la administración del software. | `**cat /var/log/pacman.log**` | yum history cat /var/log/yum.log | cat /var/log/dpkg.log | rug history | cat /var/log/zypp/history | located in /var/log/portage |
| **Limpia la caché:**
Limpia todas las cachés locales. Las opciones pueden limitar lo que en realidad se quiere limpiar. Autoclean elimina únicamente información innecesaria y obsoleta. | `**pacman -Sc**`
`**pacman -Scc**` | yum clean | apt-get clean apt-get autoclean | zypper clean | eclean distfiles |
| **Añade un paquete a la caché:**
Agrega un paquete local en la caché local de paquetes en su mayoría con fines de depuración. | `**cp $pkgname /var/cache/pacman/pkg/**` | apt-cache add | N/D | cp $srcfile /usr/portage/distfiles |
| **Muestra la fuente del paquete:**
Muestra el paquete fuente para el nombre del paquete dado. | repoquery -s | apt-cache showsrc | N/D |
| **Genera una salida:**
Genera una salida adecuada para el procesamiento con dotty para el paquete dado. | apt-cache dotty | N/D |
| **Prioridad de instalación:**
Establece la prioridad de un paquete dado para evitar la actualización, forzando el downgrade o para evitar sobrescribir cualquier comportamiento predeterminado. También se puede utilizar para preferir una versión de un paquete desde un repositorio determinado. | `**${EDITOR} /etc/pacman.conf**`
Modifique la matriz HoldPkg y/o IgnorePkg | yum-plugin-priorities y yum-plugin-protect-packages | /etc/apt/preferences smart priority –set | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
Añadir una línea con =category/package-version |
| **Prioridad de desinstalación:**
Elimina una prioridad previamente establecida. | /etc/apt/preferences smart priority --remove | zypper mr -p | ${EDITOR} /etc/portage/package.keywords
remover la línea afectada |
| **Muestra la lista de prioridades:**
Muestra una lista de las prioridades establecidas. | apt-cache policy /etc/apt/preferences smart priority --show | N/D | cat /etc/portage/package.keywords |
| **Ignora una prioridad establecida:**
Ignora los problemas que las prioridades puedan desencadenar. | N/D |
| **Gestión de repositorios:**
Administra las fuentes de instalación. | `**${EDITOR} /etc/pacman.conf**` | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | ${EDITOR} /etc/apt/sources.list | layman |
| **Añadir repositorios:**
Añade una fuente de instalación para el sistema. Algunas herramientas proporcionan comandos adicionales para ciertas fuentes, otros permiten todo tipo de URI de origen para el comando add. Algunas otras, como apt y yum, fuerzan la edición de la lista de fuentes. apt-cdrom es una orden especial, que ofrece opciones especiales diseñadas para gestionar los CD/DVD cuando funcionan como repositorios. | `**${EDITOR} /etc/pacman.conf**` | ${EDITOR} /etc/yum.repos.d/${REPO}.repo | apt-cdrom add | rug service-add rug mount /local/dir | zypper service-add | layman, overlays |
| **Actualizar repositorios:**
Actualiza la información del repositorio especificado o de todos los repositorios. | `**pacman -Sy**` | yum clean expire-cache && yum check-update | apt-get update | rug refresh | zypper refresh zypper ref | layman -f |
| **Imprimir la lista de repositorios:**
Imprime una lista de todas las fuentes de instalación, incluyendo información importante como URI, alias, etc. | `**cat /etc/pacman.d/mirrorlist**` | cat /etc/yum.repos.d/* | rug service-list | zypper service-list | layman -l |
| **Desactivar un repositorio para una operación:** | yum --disablerepo=${REPO} | emerge package::repo-to-use |
| **Descargar versiones diferentes:**
Descarga paquetes desde una versión diferente de la distribución respecto de la instalada. | yum --releasever=${VERSION} | echo "category/package ~amd64" >> /etc/portage/package.keywords && emerge package |
| **OTRAS ÓRDENES** |
| **Iniciar una shell**
Inicia una shell para introducir múltiples órdenes en una sola sesión | yum shell | apt-config shell. | zypper shell |
| **VERIFICAR PAQUETES** |
| **Para un paquete individual:**
 | `**pacman -Qk[k] <paquete>**` | rpm -V <paquete> | debsums | rpm -V <paquete> | rpm -V <paquete> | equery check |
| **Para todos los paquetes:**
 | `**pacman -Qk[k]**` | rpm -Va | debsums | rpm -Va | rpm -Va | equery check |
| **CONSULTAR PAQUETES** |
| **Lista los paquetes locales instalados por versión:**
Lista los paquetes locales instalados junto con la versión. | `**pacman -Q**` | rpm -qa | dpkg-query -l | emerge -e world |
| **Información sobre paquetes locales instalados:**
Muestra información del paquete local: Nombre, versión, descripción, etc. | `**pacman -Qi**` | rpm -qi | dpkg-query -p | emerge -pv y emerge -S |
| **Información sobre paquetes remotos:**
Muestra información del paquete remoto: Nombre, versión, descripción, etc. | `**pacman -Si**` | yum info | apt-cache show | emerge -pv y emerge -S |
| **Muestra los archivos proporcionados por un paquete local:** | `**pacman -Ql**` | rpm -ql | dpkg-query -L | equery files |
| **Muestra los archivos proporcionados por un paquete remoto:** | `**pkgfile -l**` | repoquery -l | pfl |
| **Consulta qué paquete contiene un archivo:** | `**pacman -Qo**` | rpm -qf (solo instalados) o yum whatprovides (todo) | dpkg-query -S | equery belongs |
| **Consulta un paquete en la línea de comandos:**
Consulta un paquete suministrado en la línea de órdenes en lugar de una entrada en la base de datos de la gestión de paquetes. | `**pacman -Qp**` | rpm -qp | dpkg-deb -I |
| **Muestra los cambios de un paquete:**
Muestra el registro de cambios de un paquete. | `**pacman -Qc**` | rpm -q --changelog | equery changes -f |
| **Busca paquetes por nombre:**
Busca los paquetes instalados localmente por nombres o descripción. | `**pacman -Qs**` | eix -S -I |
| **COMPILAR PAQUETES** |
| **Compila un paquete:** | `**makepkg -s**` | rpmbuild -ba (normal) mock (en chroot) | dpkg-buildpkg | rpmbuild -ba | rpmbuild -ba | ebuild; quickpkg |
| **Comprueba si hay problemas de empaquetado:** | rpmlint | lintian | repoman |
| **Lista los archivos contenidos en un paquete:** | `**pacman -Qpl <archivo>**` | rpmls rpm -qpl | rpm -qpl | rpm -qpl |
| **Extrae un paquete:** | `**tar -Jxvf**` | rpm2cpio | cpio -vid | ar vx | tar -zxvf data.tar.gz | rpm2cpio | cpio -vid | rpm2cpio | cpio -vid | tar -jxvf |
| **Consulta un paquete en línea de órdenes:**
Consulta un paquete suministrado en la línea de órdenes en lugar de una entrada en la base de datos de la gestión de paquetes. | `**pacman -Qp**` | rpm -qp | dpkg-deb -I |
| **<font color="#707070">Acción</font>** | **Arch** | **Red Hat/Fedora** | **Debian/Ubuntu** | **(Antiguo) SUSE** | **openSUSE** | **Gentoo** |
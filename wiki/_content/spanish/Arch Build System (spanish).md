**Estado de la traducción**
Este artículo es una traducción de [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), revisada por última vez el **2018-09-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_Build_System&diff=0&oldid=540727) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")
*   [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [Official repositories (Español)](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS")

Arch Build System (*«sistema de compilación de Arch»*), ABS para abreviar, es un sistema tipo *ports* para la construcción y empaquetado de software desde el código fuente. Mientras [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") es la herramienta especializada de Arch para la gestión de los paquetes binarios (incluyendo los paquetes creados con ABS), el sistema ABS es una colección de herramientas para compilar el código fuente y crear paquetes `.pkg.tar.xz` instalables.

*Ports* es un sistema utilizado por los sistemas basados en *BSD para automatizar el proceso de compilación del software desde el código fuente. El sistema utiliza un *puerto* para descargar, descomprimir, parchear, compilar e instalar el software especificado. Un *puerto* no es más que una carpeta pequeña creada en el ordenador del usuario, con el nombre del software correspondiente para ser instalado, que contiene algunos archivos con las instrucciones para construir e instalar el software desde el código fuente. Esto hace que la instalación del software sea tan simple como escribir `make` o `make install clean` desde la carpeta que sirve de puerto.

ABS es un concepto similar. ABS es un componente de un árbol de directorios (el árbol ABS) que se puede verificar utilizando SVN. Este árbol representa (pero no contiene) todo el *sotfware oficial de Arch*. Se hace referencia a cada subdirectorio, nominado por el nombre del paquete, como un «ABS», de igual manera a como si se refiriese a un «puerto». Estos ABS (o subdirectorios) no contienen el paquete de software ni el código fuente, sino más bien un archivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") y, a veces, otros archivos. Mediante la ejecución de la orden [makepkg](/index.php/Makepkg "Makepkg") dentro de un directorio que contiene un PKGBUILD, el sistema primero compila y luego *empaqueta* el software, dentro del directorio de compilación, antes de ser instalado. A continuación, se puede utilizar [pacman](/index.php/Pacman "Pacman"), el gestor de paquetes de Arch Linux, para instalar o actualizar el nuevo paquete.

## Contents

*   [1 Descripción general de ABS](#Descripción_general_de_ABS)
    *   [1.1 Árbol SVN](#Árbol_SVN)
*   [2 ¿Por qué utilizar ABS?](#¿Por_qué_utilizar_ABS?)
*   [3 ¿Cómo utilizar ABS?](#¿Cómo_utilizar_ABS?)
    *   [3.1 Obtener PKGBUILD usando Svn](#Obtener_PKGBUILD_usando_Svn)
        *   [3.1.1 Requisitos previos](#Requisitos_previos)
        *   [3.1.2 Descarga no recursiva](#Descarga_no_recursiva)
        *   [3.1.3 Rama de un paquete](#Rama_de_un_paquete)
    *   [3.2 Obtener PKGBUILD usando Git](#Obtener_PKGBUILD_usando_Git)
    *   [3.3 Compilar el paquete](#Compilar_el_paquete)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Conservar paquetes modificados](#Conservar_paquetes_modificados)
    *   [4.2 Descargar una versión anterior de un paquete](#Descargar_una_versión_anterior_de_un_paquete)
*   [5 Otras herramientas](#Otras_herramientas)

## Descripción general de ABS

«ABS» puede ser usado como un término genérico, ya que incluye y se basa en otros componentes adicionales, por lo que, aunque no es técnicamente exacto, «ABS» puede referirse a la siguiente estructura como un conjunto completo de herramientas:

	El árbol SVN

	La estructura del directorio que contiene los archivos necesarios para compilar todos los paquetes oficiales, pero no los paquetes en sí ni los archivos fuente del software. Estos están disponibles en los repositorios [svn](https://www.archlinux.org/svn/) y [git](https://projects.archlinux.org/svntogit/packages.git/).

	[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

	Un script de [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") que contiene la dirección URL del código fuente junto con las instrucciones de compilación y de empaquetado.

	[makepkg](/index.php/Makepkg "Makepkg")

	Herramienta del intérprete de órdenes de ABS que lee los PKGBUILD, los descarga automáticamente, compila el código fuente y crea un `.pkg.tar*` de acuerdo con lo dispuesto en la matriz `PKGEXT` presente en `makepkg.conf`. También puede utilizar makepkg para hacer sus propios paquetes desde el repositorio [AUR](/index.php/AUR "AUR") o desde fuentes de terceros. Consulte el artículo de la wiki [Creating packages](/index.php/Creating_packages "Creating packages") para obtener más información.

	[pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")

	pacman es completamente independiente, pero necesita ser invocado o por makepkg o manualmente, para instalar y eliminar los paquetes construidos y para resolver las dependencias.

	[AUR](/index.php/Arch_User_Repository "Arch User Repository")

	El repositorio de usuarios de Arch está separado de ABS, pero los PKGBUILD de AUR (sin soporte) pueden ser usados con la herramienta makepkg para compilar y empaquetar el software. En contraste con el árbol de ABS que reside en el propio equipo, AUR existe como una interfaz web. Contiene miles de PKGBUILD aportados por los usuarios para empaquetar software que no está disponible como un paquete oficial de Arch. Si necesita construir un paquete que esté fuera de la estructura oficial de Arch, es probable que pueda encontralo en AUR.

**Advertencia:** Se asume que los PKGBUILD oficiales son paquetes [compilados en un entorno chroot limpio](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot"). Crear software en un sistema de compilación «sucio» puede fallar o causar un comportamiento inesperado en el tiempo de ejecución, ya que si el sistema de compilación detecta las dependencias de forma dinámica, el resultado dependerá de qué paquetes estén disponibles en el sistema de compilación.

### Árbol SVN

Los [repositorios](/index.php/Official_repositories "Official repositories") *core*, *extra* y *testing* están en el repositorio SVN *packages* para [descargar](#Descarga_no_recursiva). Los repositorios *community* y *multilib* están en el repositorio SVN *community*.

Cada paquete tiene su propio subdirectorio. Dentro de él, están los directorios `repos` y `trunk`. El directorio `repos` se ramifica por el nombre del repositorio (por ejemplo, *core*) y por la arquitectura. Los PKGBUILD y los archivos encontrados en `repos` se utilizan en las compilaciones oficiales. Los archivos que se encuentran en `trunk` son utilizados por los desarrolladores para prepararlos antes de ser copiados a `repos`.

Por ejemplo, el árbol para [acl](https://www.archlinux.org/packages/?name=acl) se ve así:

```
acl
acl/repos
acl/repos/core-i686
acl/repos/core-i686/PKGBUILD
acl/repos/core-x86_64
acl/repos/core-x86_64/PKGBUILD
acl/trunk
acl/trunk/PKGBUILD

```

El código fuente para el paquete no está presente en el directorio ABS. En cambio, el `PKGBUILD` contiene una URL desde la que se descargará el código fuente cuando se vaya a compilar el paquete.

## ¿Por qué utilizar ABS?

El sistema de sompilación de Arch (siglas en inglés ABS) se utiliza para:

*   Compilar o recopilar un paquete, por cualquier motivo.
*   Hacer e instalar nuevos paquetes desde el código fuente del software para los que no se dispone todavía de paquetes —binarios— (véase [Creating packages](/index.php/Creating_packages "Creating packages")).
*   Personalizar paquetes existentes para satisfacer las necesidades propias (activar o desactivar opciones, aplicar parches...).
*   Reconstruir todo el sistema usando los flags del compilador, «al modo FreeBSD» (por ejemplo, con [pacman-src-git](https://aur.archlinux.org/packages/pacman-src-git/)).
*   Construir e instalar limpiamente su propio kernel personalizado (véase [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation")).
*   Obtener los módulos del kernel para que funcionen con el propio kernel personalizado.
*   Compilar e instalar fácilmente una versión reciente, antigua, beta, o en desarrollo de un paquete de Arch modificando el número de la versión en el PKGBUILD.

ABS no es necesario para usar Arch Linux, pero es útil para la automatización de ciertas tareas de compilación del código fuente.

## ¿Cómo utilizar ABS?

Para obtener el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") necesario para construir un paquete desde fuente, se pueden usar dos métodos: [Svn](/index.php/Svn "Svn") o [Git](/index.php/Git "Git") usando el paquete [asp](https://www.archlinux.org/packages/?name=asp), el cual esta diseñado para trabajar con repositorios svntogit. A continuación se va a describir el método basado en svn y el método [basado en git](#Obtener_PKGBUILD_usando_Git).

### Obtener PKGBUILD usando Svn

#### Requisitos previos

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [subversion](https://www.archlinux.org/packages/?name=subversion).

#### Descarga no recursiva

**Advertencia:** No descargue todo el repositorio, tan solo siga las instrucciones siguientes. El repositorio completo de SVN es gigantesco. No solo necesitaría bastante espacio en su disco, sino que también le costaría mucho al servidor de archlinux.org su descarga. Si abusa de este servicio, su dirección puede ser bloqueada. Nunca ejecute scripts en el SVN público.

Para descargar las ramas *core*, *extra*, y *testing* de los [repositorios](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

Para descargar las ramas *community* y *multilib* de los repositorios:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

En ambos casos se crea un directorio vacío, el cual tiene conocimiento de que será el destino de las ramas.

#### Rama de un paquete

En el directorio conteniendo el repositorio svn que esta revisando (esto es, *packages* o *community*), ejecute:

```
$ svn update *nombre-paquete*

```

Esto va a descargar el paquete dentro de su repositorio local. A partir de ahora cada vez que se ejecute *svn update* en el directorio del repositorio, el directorio local del paquete también se actualizara.

Si se especifica un paquete que no existe, svn no le mostrara una advertencia, solo mostrara algo similar a "At revision 115847", y no creara ningún archivo. Si esto sucede:

*   Confirme que escribió el nombre del paquete correctamente
*   Confirme que el paquete no se ha movido a otro repositorio (por ejemplo de *community* a *extra*)
*   Revise [https://www.archlinux.org/packages](https://www.archlinux.org/packages) para verificar si el paquete es construido con fuentes de otro paquete (por ejemplo, [python-tensorflow](https://www.archlinux.org/packages/?name=python-tensorflow) es construido con el PKGBUILD de [tensorflow](https://www.archlinux.org/packages/?name=tensorflow))

**Sugerencia:** Para descargar versiones antiguas de un paquete, consulte [#Descargar una versión anterior de un paquete](#Descargar_una_versión_anterior_de_un_paquete).

Es aconsejable actualizar todas las ramas que ha descargado si desea recompilar paquetes con versiones mas recientes de los repositorios. Para actualizar ejecute:

```
$ svn update

```

### Obtener PKGBUILD usando Git

Es necesario [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [asp](https://www.archlinux.org/packages/?name=asp).

Para clonar el repositorio del paquete, ejecute:

```
$ asp checkout *nombre-paquete*

```

Esta orden clona el repositorio git del paquete en un directorio con el mismo nombre del paquete.

Para actualizar el repositorio git, ejecute `asp update` seguido de `git pull` dentro del repositorio git.

Es más, se pueden usar el resto de órdenes de git para revisar versiones antiguas o para ver el histórico del paquete. Para más información sobre el uso de git, consulte la pagina de [git](/index.php/Git "Git").

Si desea copiar una instantánea del [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") para el paquete actual, ejecute:

```
$ asp export *nobre-paquete*

```

### Compilar el paquete

Consulte [makepkg](/index.php/Makepkg_(Espa%C3%B1ol)#Configuración "Makepkg (Español)") para configurar *makepkg* para la compilación de los [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") que esta revisando.

Después, copie el directorio que contiene el [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") a un lugar nuevo. Allí, modifique lo que considere necesario y utilice *makepkg* como se describe en [makepkg (Español)#Uso](/index.php/Makepkg_(Espa%C3%B1ol)#Uso "Makepkg (Español)") para crear un nuevo paquete.

## Consejos y trucos

### Conservar paquetes modificados

La actualización del sistema con pacman reemplazará un paquete modificado de ABS con el paquete del mismo nombre presente en los repositorios oficiales. Consulte las siguientes instrucciones sobre cómo evitar esto.

Inserte una matriz de grupo en PKGBUILD y agregue el paquete a un grupo llamado `modified`.

 `PKGBUILD`  `groups=('modified')` 

Agregue este grupo a la sección `IgnoreGroup` en `/etc/pacman.conf`.

 `/etc/pacman.conf`  `IgnoreGroup = modified` 

Si hay nuevas versiones disponibles en los repositorios oficiales durante una actualización del sistema, pacman imprime una nota que omite esta actualización porque está en la sección IgnoreGroup. En este punto, el paquete modificado debe reconstruirse a partir de ABS para evitar actualizaciones parciales.

### Descargar una versión anterior de un paquete

Dentro del repositorio svn que esté revisando, como se ha descrito en [#Descarga no recursiva](#Descarga_no_recursiva) (por ejemplo, «packages» o «community»), examine el registro:

```
$ svn log *nombre-paquete*

```

Encuentre la versión que le interesa, después especifique la versión que desea descargar. Por ejemplo, para descargar la versión `r1729` ejecute:

```
$ svn update -r1729 *nombre-paquete*

```

Esto actualizará la copia en el directorio local del paquete *nombre-paquete* a la versión deseada.

También es posible especificar una fecha. Si no hay una versión en ese día, svn tomara la versión mas reciente antes de ese momento. El ejemplo siguiente localiza en el repositorio una versión ocurrida el 2009-03-03:

```
$ svn update -r{20090303} *nombre-paquete*

```

Es posible verificar los paquetes en las versiones antes de que se hayan movido a otro repositorio también; revise los registros a fondo para la fecha en que se movieron o el último número de revisión.

## Otras herramientas

*   [pbget](http://xyne.archlinux.ca/projects/pbget/) — obtiene PKGBUILD para paquetes individuales directamente desde la interfaz web. Incluye soporte de AUR.
*   [asp](https://github.com/falconindy/asp) — una herramienta para administrar los archivos fuente de la compilación utilizados para crear paquetes de Arch Linux. Utiliza la interfaz git que ofrece fuentes más actualizadas.
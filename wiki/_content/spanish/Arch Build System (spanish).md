Artículos relacionados

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Official repositories (Español)](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

Este artículo proporciona una visión general de Arch Build System, junto con una guía para principiantes. No es una guía de referencia completa. Si necesita más información, consulte las páginas *man*.

**Nota:** ABS se sincroniza una vez al día, por lo que puede quedarse desfasado respecto a los paquetes que ya están disponibles en los repositorios.

## Contents

*   [1 ¿Qué es Arch Build System?](#.C2.BFQu.C3.A9_es_Arch_Build_System.3F)
    *   [1.1 ¿Qué es un sistema tipo *ports*?](#.C2.BFQu.C3.A9_es_un_sistema_tipo_ports.3F)
    *   [1.2 **ABS** es un concepto similar](#ABS_es_un_concepto_similar)
    *   [1.3 Descripción general de ABS](#Descripci.C3.B3n_general_de_ABS)
*   [2 ¿Por qué utilizar ABS?](#.C2.BFPor_qu.C3.A9_utilizar_ABS.3F)
*   [3 ¿Cómo utilizar ABS?](#.C2.BFC.C3.B3mo_utilizar_ABS.3F)
    *   [3.1 Obtener PKGBUILD usando Svn](#Obtener_PKGBUILD_usando_Svn)
        *   [3.1.1 Prerequisitos](#Prerequisitos)
        *   [3.1.2 Descarga no recursiva](#Descarga_no_recursiva)
        *   [3.1.3 Rama de un paquete](#Rama_de_un_paquete)
    *   [3.2 Obtener PKGBUILD usando Git](#Obtener_PKGBUILD_usando_Git)
    *   [3.3 Construcción del paquete](#Construcci.C3.B3n_del_paquete)
*   [4 Recomendaciones](#Recomendaciones)
    *   [4.1 Revisión de un paquete antiguo](#Revisi.C3.B3n_de_un_paquete_antiguo)

## ¿Qué es Arch Build System?

Arch Build System (*«Sistema de Compilación de Arch»*), **ABS** para abreviar, es un sistema tipo *ports* para la construcción y empaquetado de software desde el código fuente. Mientras [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") es la herramienta especializada de Arch para la gestión de los paquetes binarios (incluyendo los paquetes creados con ABS), el sistema ABS es una colección de herramientas para compilar el código fuente y crear paquetes `.pkg.tar.xz` instalables.

### ¿Qué es un sistema tipo *ports*?

*Ports* es un sistema utilizado por los sistemas basados en *BSD para automatizar el proceso de compilación del software desde el código fuente. El sistema utiliza un *puerto* para descargar, descomprimir, parchear, compilar e instalar el software especificado. Un *puerto* no es más que una carpeta pequeña creada en el ordenador del usuario, con el nombre del software correspondiente para ser instalado, que contiene algunos archivos con las instrucciones para construir e instalar el software desde el código fuente. Esto hace que la instalación del software sea tan simple como escribir `make` o `make install clean` desde la carpeta que sirve de puerto.

### **ABS** es un concepto similar

ABS es un componente de un árbol de directorios (el árbol ABS) que reside en `/var/abs`. Este árbol tiene muchos subdirectorios, cada uno dentro de una categoría y nombrado por el nombre de su respectivo paquete. Este árbol representa (pero no contiene) todo el *sotfware oficial de Arch*, recuperable a través del sistema SVN. Se hace referencia a cada subdirectorio, nominado por el nombre del paquete, como un «ABS», de igual manera a como si se refiriese a un «puerto». Estos ABS (o subdirectorios) no contienen el paquete de software ni el código fuente, sino más bien un archivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") (y a veces otros archivos). Un PKGBUILD es un sencillo script de compilación de Bash -un archivo de texto que contiene las instrucciones de compilación y de empaquetado, así como la dirección URL del archivo **tarball fuente** adecuado para ser descargado-. (El componente más importante de ABS son los propios PKGBUILD). Mediante la ejecución de la orden [makepkg](/index.php/Makepkg "Makepkg") de ABS, el sistema primero compila y luego *empaqueta* el software, dentro del directorio de compilación, antes de ser instalado. A continuación, se puede utilizar [pacman](/index.php/Pacman "Pacman"), el gestor de paquetes de Arch Linux, para instalar, actualizar y eliminar el nuevo paquete.

### Descripción general de ABS

«ABS» puede ser usado como un término genérico, ya que incluye y se basa en otros componentes adicionales, por lo que, aunque no es técnicamente exacto, «ABS» puede referirse a la siguiente estructura como un conjunto completo de herramientas:

	El árbol ABS

	La estructura de directorios ABS; una jerarquía de SVN en `/var/abs/` ubicado en el propio equipo (local). Contiene muchos subdirectorios, nominados por el software oficial de Arch Linux, disponibles todos desde los repositorios especificados en `/etc/abs.conf`, pero no los propios paquetes. El árbol se crea después de instalar el paquete [abs](https://www.archlinux.org/packages/?name=abs) con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y posteriormente ejecutando el script `abs`.

	[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

	Un script de [Bash](/index.php/Bash "Bash") que contiene la dirección URL del código fuente junto con las instrucciones de compilación y de empaquetado.

	[makepkg](/index.php/Makepkg "Makepkg")

	La orden de shell de ABS que lee los PKGBUILD, los descarga automáticamente, compila el código fuente y crea un `.pkg.tar*` de acuerdo con lo dispuesto en la matriz `PKGEXT` en `makepkg.conf`. También puede utilizar makepkg para hacer sus propios paquetes desde el repositorio [AUR](/index.php/AUR "AUR") o desde fuentes de terceros. (Consulte el artículo de la wiki [Creating packages](/index.php/Creating_packages "Creating packages").)

	[pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")

	Pacman es completamente independiente, pero necesita ser invocado o por makepkg o manualmente, para instalar y eliminar los paquetes construidos y para resolver las dependencias.

	[AUR](/index.php/Arch_User_Repository "Arch User Repository")

	El repositorio de usuarios de Arch está separado de ABS, pero los PKGBUILD de AUR (sin soporte) pueden ser usados con la herramienta makepkg para compilar y empaquetar el software. En contraste con el árbol de ABS que reside en el propio equipo, el AUR existe como una interfaz web. Contiene miles de PKGBUILD aportados por el usuario para empaquetar software no disponible como un paquete oficial de Arch. Si necesita construir un paquete que esté fuera de la estructura oficial de Arch, es probable que pueda encontralo en AUR.

## ¿Por qué utilizar ABS?

El Sistema de Compilación de Arch se utiliza para:

*   Compilar o recopilar un paquete, por cualquier motivo.
*   Hacer e instalar nuevos paquetes desde el código fuente del software para los que no se dispone todavía de paquetes (véase [Creating packages](/index.php/Creating_packages "Creating packages")).
*   Personalizar paquetes existentes para satisfacer las necesidades propias (activar o desactivar opciones, aplicar parches...).
*   Reconstruir todo el sistema usando los flags del compilador, «al modo FreeBSD» (por ejemplo, con [pacbuilder](/index.php/Pacbuilder "Pacbuilder")).
*   Construir e instalar limpiamente su propio kernel personalizado (véase [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation")).
*   Obtener los módulos del kernel para que funcionen con el propio kernel personalizado.
*   Compilar e instalar fácilmente una versión nueva, vieja, beta, o en desarrollo de un paquete de Arch modificando el número de la versión en el PKGBUILD.

ABS no es necesario para usar Arch Linux, pero es útil para la automatización de ciertas tareas de compilación del código fuente.

## ¿Cómo utilizar ABS?

Para obtener el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") necesario para construir un paquete desde fuente, se pueden usar dos métodos: [Svn](/index.php/Svn "Svn") o [Git](/index.php/Git "Git") usando el paquete [asp](https://www.archlinux.org/packages/?name=asp), el cual esta diseñado para trabajar con repositorios svntogit. A continuación se va a describir el método basado en svn y el método [basado en git](#Obtener_PKGBUILD_usando_Git).

### Obtener PKGBUILD usando Svn

#### Prerequisitos

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [subversion](https://www.archlinux.org/packages/?name=subversion).

#### Descarga no recursiva

**Advertencia:** No descargue todo el repositorio, solo siga las instrucciones debajo. El repositorio completo de SVN es gigantesco. No solo va a requerir bastante espacio en su disco, también le costara mucho al servidor de archlinux.org para su descarga. Si Ud. abusa de este servicio su dirección puede ser bloqueada. Nunca ejecute scripts en el SVN público.

Para revisar las ramas *core*, *extra*, y *testing* de los [repositorios](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

Para revisar las ramas *community* y *multilib* de los repositorios:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

En ambos casos se crea un directorio vacio, el cual tiene conocimiento de que esta contenido en las ramas.

#### Rama de un paquete

En el directorio conteniendo el repositorio svn que esta revisando (v.g., *extra* o *community*), ejecute:

```
$ svn update *nombre-paquete*

```

Esto va a descargar (*pull*) el paquete dentro de su repositorio local. Desde ahora cada vez que se ejecute *svn update* en el directorio del repositorio, el directorio del paquete también se actualizara.

Si se especifica un paquete que no existe, svn no le mostrara una advertencia, solo mostrara algo similar a "At revision 115847", y no creara ningún archivo. Si esto sucede:

*   Confirme que escribió el nombre del paquete correctamente
*   Confirme que el paquete no se ha movido a otro repositorio (v.g. de *community* a *extra*)
*   Revise [https://www.archlinux.org/packages](https://www.archlinux.org/packages) para verificar si el paquete es construido con fuente de otro paquete (por ejemplo, [python-tensorflow](https://www.archlinux.org/packages/?name=python-tensorflow) es construido con el PKGBUILD de [tensorflow](https://www.archlinux.org/packages/?name=tensorflow))

**Sugerencia:** Para revisar versiones antiguas de un paquete, vea [#Revisión de un paquete antiguo](#Revisi.C3.B3n_de_un_paquete_antiguo).

Es aconsejable actualizar todas las ramas que ha descargado si desea re-construir paquetes en versiones mas recientes de los repositorios. Para actualizar ejecute:

```
$ svn update

```

### Obtener PKGBUILD usando Git

Es necesario [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [asp](https://www.archlinux.org/packages/?name=asp).

Para clonar el repositorio del paquete ejecute:

```
$ asp checkout *nombre-paquete*

```

Este comando clona el repositorio git del paquete en un directorio con el nombre del paquete mismo.

Para actualizar el repositorio de git, ejecute `asp update` seguido de `git pull`dentro del repositorio de git.

Es más, se pueden usar el resto de comandos de git para revisar versiones antiguas o para ver el histórico del paquete. Para más información sobre el uso de git, vea la pagina de [git](/index.php/Git "Git").

Si desea copiar una instantánea del [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") para el paquete actual, ejecute:

```
$ asp export *nobre-paquete*

```

### Construcción del paquete

Vea [makepkg](/index.php/Makepkg_(Espa%C3%B1ol)#Configuraci.C3.B3n "Makepkg (Español)") para configurar *makepkg* para la construcción de los [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") que esta revisando.

Después, copie el directorio que contiene el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") a un lugar nuevo. Alla, modifique lo que considere necesario y use *makepkg* como esta descrito en [makepkg#Uso](/index.php/Makepkg_(Espa%C3%B1ol)#Uso "Makepkg (Español)") para crear un nuevo paquete.

## Recomendaciones

### Revisión de un paquete antiguo

Dentro del repositorio svn que esta revisando, como se ha descrito en [#Descarga no recursiva](#Descarga_no_recursiva) (v.g. "packages" o "community"), examine el histórico:

```
$ svn log *nombre-paquete*

```

Encuentre la revisión que le interesa, después especifique la revisión que desea modificar. Por ejemplo, para examinar la revisión `r1729` ejecute:

```
$ svn update -r1729 *nombre-paquete*

```

Esto actualizara la copia en el directorio local de *nombre-paquete* a la revisión deseada.

También es posible especificar una fecha. Si no hay una revisión en ese día, svn tomara la version mas reciente antes de ese momento. El ejemplo siguiente ubica el repositorio en una revisión ocurrida el 2009-03-03:

```
$ svn update -r{20090303} *nombre-paquete*

```
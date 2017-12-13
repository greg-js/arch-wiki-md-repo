Artículos relacionados

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg](/index.php/Makepkg "Makepkg")
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
    *   [3.1 Herramientas de instalación](#Herramientas_de_instalaci.C3.B3n)
    *   [3.2 /etc/abs.conf](#.2Fetc.2Fabs.conf)
    *   [3.3 El árbol ABS](#El_.C3.A1rbol_ABS)
        *   [3.3.1 Descargar el árbol ABS](#Descargar_el_.C3.A1rbol_ABS)
    *   [3.4 /etc/makepkg.conf](#.2Fetc.2Fmakepkg.conf)
        *   [3.4.1 Establecer la variable PACKAGER en /etc/makepkg.conf](#Establecer_la_variable_PACKAGER_en_.2Fetc.2Fmakepkg.conf)
            *   [3.4.1.1 Mostrar todos los paquetes (incluidos los de AUR)](#Mostrar_todos_los_paquetes_.28incluidos_los_de_AUR.29)
            *   [3.4.1.2 Motrar solo los paquetes contenidos en los Repositorios](#Motrar_solo_los_paquetes_contenidos_en_los_Repositorios)
    *   [3.5 Crear un directorio de compilación](#Crear_un_directorio_de_compilaci.C3.B3n)
    *   [3.6 Compilar el paquete](#Compilar_el_paquete)
        *   [3.6.1 fakeroot](#fakeroot)

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

La compilación de paquetes utilizando ABS consta de los siguientes pasos:

1.  Instale el paquete [abs](https://www.archlinux.org/packages/?name=abs) con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").
2.  Ejecute `abs`, como root, de modo que cree el árbol ABS sincronizado con los servidores de Arch Linux.
3.  Copie los archivos de compilación (por lo general ubicados en `/var/abs/<repo>/<pkgname>`) a un directorio de compilación.
4.  Vaya a ese directorio, edite PKGBUILD (si se desea o es necesario) y ejecute **makepkg**.
5.  makepkg, basándose en las instrucciones de PKGBUILD, descargará el paquete fuente correspondiente, lo descomprimirá, lo parcheará si fuera el caso, lo construirá de acuerdo a `CFLAGS` especificado en `makepkg.conf`, y, finalmente, comprimirá los archivos compilados en un paquete con la extensión `.pkg.tar.gz` o `.pkg.tar.xz`.
6.  La instalación del paquete creado es tan fácil como ejecutar `pacman -U <archivo.pkg.tar.xz>`. La eliminación del paquete también se gestiona con pacman.

### Herramientas de instalación

Para utilizar ABS, primero tiene que [instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [abs](https://www.archlinux.org/packages/?name=abs) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Esto instalará los scripts de sincronización de ABS, varios scripts de compilación y [rsync](/index.php/Rsync "Rsync") (como una dependencia, si no lo tiene).

Sin embargo, antes de que se pueda realmente construir cualquier cosa, también es necesario tener instaladas las herramientas básicas de compilación. Estas son hábilmente recogidas en el [grupo de paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Installing_package_groups "Pacman (Español)") [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/). Este grupo puede ser instalado con pacman.

### /etc/abs.conf

Como root, edite `/etc/abs.conf` para incluir los repositorios deseados.

Retire el signo `!` de delante de los repositorios correspondientes. Por ejemplo:

```
REPOS=(core extra community !testing)

```

### El árbol ABS

El árbol ABS es una jerarquía de directorios SVN localizados en `/var/abs` con una estructura similar a la siguiente:

```
| -- core/
|     || -- acl/
|     ||     || -- PKGBUILD
|     || -- attr/
|     ||     || -- PKGBUILD
|     || -- abs/
|     ||     || -- PKGBUILD
|     || -- autoconf/
|     ||     || -- PKGBUILD
|     || -- ...
| -- extra/
|     || -- acpid/
|     ||     || -- PKGBUILD
|     || -- apache/
|     ||     || -- PKGBUILD
|     || -- ...
| -- community/
|     || -- ...

```

El árbol ABS tiene exactamente la misma estructura que la base de datos del paquete:

*   Primer nivel: Nombre del repositorio.
*   Segundo nivel: Directorios con los nombres de los paquetes.
*   Tercer nivel: PKGBUILD (contiene la información necesaria para construir un paquete) y otros archivos relacionados (parches, así como otros archivos necesarios para construir el paquete).

El código fuente para el paquete no está presente en el directorio ABS. En su lugar, el archivo **PKGBUILD** contiene una URL de donde descargar el código fuente para cuando el paquete se vaya a construir. Así, el tamaño de árbol ABS es bastante pequeño.

#### Descargar el árbol ABS

Como root, ejecute:

```
# abs

```

El árbol ABS se creará en `/var/abs`. Tenga en cuenta que cada rama del árbol ABS se corresponden a los repositorios habilitados en `/etc/abs.conf`.

La orden abs se debe ejecutar periódicamente para mantenerse sincronizado con los repositorios oficiales. También se pueden descargar archivos individuales de paquetes ABS con:

```
# abs <repository>/<package>

```

De esta manera no se tiene que revisar todo el árbol ABS para construir un solo paquete.

### /etc/makepkg.conf

El archivo `/etc/makepkg.conf` especifica las variables globales del entorno y los flags del compilador que desee editar si está utilizando un sistema SMP, o especificar otras optimizaciones deseadas. Los ajustes por defecto son optimizaciones para i686 y x86_64 que no tendrán ningún problema para esas arquitecturas en sistemas con una sola CPU. (Los valores predeterminados funcionarán para la máquina SMP, pero solo utilizará un core/CPU al compilar - véase [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf").)

#### Establecer la variable PACKAGER en /etc/makepkg.conf

Establecer la variable PACKAGER en `/etc/makepkg.conf` es una operación opcional, pero *muy recomendable*. Esta opción permite establecer un "flag" para identificar rápidamente los paquetes que se han construido y/o instalado por el usuario, en lugar del mantenedor oficial. Esto se logra fácilmente utilizando **expac** disponible desde el repositorio community:

##### Mostrar todos los paquetes (incluidos los de AUR)

```
$ grep myname /etc/makepkg.conf
PACKAGER="myname <myemail@myserver.com>"

```

```
$ expac "%n %p" | grep "myname" | column -t
archey3 myname
binutils myname
gcc myname
gcc-libs myname
glibc myname
tar myname

```

##### Motrar solo los paquetes contenidos en los Repositorios

Este ejemplo solo muestra los paquetes contenidos en los repositorios definidos en `/etc/pacman.conf`:

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)
binutils
gcc
gcc-libs
glibc
tar

```

### Crear un directorio de compilación

Se recomienda crear una carpeta de compilación donde llevar a cabo la compilación, nunca se debe modificar el árbol ABS compilando los paquetes dentro de ella, ya que los datos se perderán (sobreescribiéndose) en cada actualización de ABS. Es una buena práctica utilizar el directorio «home», aunque algunos usuarios de Arch prefieren crear una carpeta «local» en `/var/abs/`, estableciendo la propiedad del usuario normal.

Cree un directorio de compilación, por ejemplo:

```
$ mkdir -p $HOME/abs

```

Copie el ABS desde el árbol (`/var/abs/<repository>/<pkgname>`) al directorio de compilación.

### Compilar el paquete

En nuestro ejemplo, vamos a construir el paquete del gestor de pantalla *slim*.

Copie el ABS slim desde el árbol ABS a un directorio de compilación:

```
$ cp -r /var/abs/extra/slim/ ~/abs

```

Acceda al directorio de compilación:

```
$ cd ~/abs/slim

```

Modifique el PKGBUILD para añadir o eliminar el apoyo a determinados componentes, para aplicar parches, para cambiar versiones de paquetes, etc. (opcional):

```
$ nano PKGBUILD

```

Ejecute makepkg como usuario normal (con el parámetro `-s` para instalar con la resolución automática de dependencias):

```
$ makepkg -s

```

**Nota:** Antes de que muestre error por la ausencia (make) de dependencias, recuerde que se supone que el grupo [base](https://www.archlinux.org/groups/x86_64/base/) está instalado en todos los sistemas de Arch Linux. El grupo «base-devel» se supone que se instala cuando se construye con **makepkg**. Véase [#Herramientas de instalación](#Herramientas_de_instalaci.C3.B3n).

Instale como root:

```
# pacman -U slim-1.3.0-2-i686.pkg.tar.xz

```

Eso es todo. Acaba de construir slim desde el código fuente y lo ha instalado limpiamente en su sistema con pacman. La eliminación del paquete también es manejado por pacman con `pacman -R slim`.

El método ABS agrega un nivel de comodidad y automatización, mientras que todavía mantiene una total transparencia y control de las funciones de compilación e instalación por su inclusión en PKGBUILD.

#### fakeroot

En esencia, se siguen los mismos pasos que se realizan en el método tradicional (que generalmente incluyen `./configure, make, make install`) pero el software se instala en un entorno *fake root*. (Un entorno *fake root* es simplemente un subdirectorio dentro del directorio de compilación que funciona y se comporta como el directorio root del sistema. Conjuntamente con el programa **fakeroot**, makepkg crea un directorio root falso, e instala los binarios compilados y los archivos asociados a él, con **root** como propietario). El *fake root*, o árbol de subdirectorios que contiene el software compilado, se comprime en un archivo con la extensión `.pkg.tar.xz`, o un *paquete*. Cuando se invoca, pacman extrae el paquete (lo instala) en el directorio root real del sistema (`/`).
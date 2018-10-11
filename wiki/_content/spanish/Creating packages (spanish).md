Artículos relacionados

*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   [Estándares de empaquetado en Arch](/index.php/Arch_packaging_standards_(Espa%C3%B1ol) "Arch packaging standards (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")
*   [Creating packages for other distributions](/index.php/Creating_packages_for_other_distributions "Creating packages for other distributions")
*   [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS")
*   [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")

Este artículo tiene como objetivo ayudar a los usuarios a crear sus propios paquetes utilizando el [sistema de compilación](/index.php/Arch_Build_System "Arch Build System") de Arch Linux, asi como subirlos en [AUR](/index.php/AUR "AUR"). Cubre la creación de un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") - un archivo de descripción de compilación de paquetes originado por `makepkg` para crear un paquete binario desde los archivos fuentes. Si ya está posee un archivo `PKGBUILD`, vea [makepkg](/index.php/Makepkg "Makepkg"). Para obtener instrucciones sobre las normas existentes y las formas de mejorar la calidad del paquete, consulte [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")

## Contents

*   [1 Resumen](#Resumen)
    *   [1.1 Metapaquetes y grupos](#Metapaquetes_y_grupos)
*   [2 Preparación](#Preparaci.C3.B3n)
    *   [2.1 Programas necesarios](#Programas_necesarios)
    *   [2.2 Descargar y probar la instalación](#Descargar_y_probar_la_instalaci.C3.B3n)
*   [3 Creando el PKGBUILD](#Creando_el_PKGBUILD)
    *   [3.1 Definiendo las variables del PKGBUILD](#Definiendo_las_variables_del_PKGBUILD)
    *   [3.2 Funciones PKGBUILD](#Funciones_PKGBUILD)
        *   [3.2.1 prepare()](#prepare.28.29)
        *   [3.2.2 pkgver()](#pkgver.28.29)
        *   [3.2.3 build()](#build.28.29)
        *   [3.2.4 check()](#check.28.29)
        *   [3.2.5 package()](#package.28.29)
*   [4 Prueba del PKGBUILD y del paquete](#Prueba_del_PKGBUILD_y_del_paquete)
    *   [4.1 Comprobación de la sanidad del paquete](#Comprobaci.C3.B3n_de_la_sanidad_del_paquete)
*   [5 Subir paquetes a AUR](#Subir_paquetes_a_AUR)
*   [6 Resumen](#Resumen_2)
    *   [6.1 Advertencias](#Advertencias)
*   [7 Directrices más detalladas](#Directrices_m.C3.A1s_detalladas)
*   [8 Generadores de PKGBUILD](#Generadores_de_PKGBUILD)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Resumen

Los paquetes en Arch Linux se construyen utilizando la utilidad [makepkg](/index.php/Makepkg "Makepkg") y la información almacenada en un archivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Cuando `makepkg` se ejecuta, busca un archivo `PKGBUILD` en el directorio actual y sigue las instrucciones en él para adquirir los archivos requeridos y/o copilarlos para enpaquetarlos en un archivo de paquete(`nombredelpaquete.pkg.tar.xz`). El paquete resultante contiene archivos binarios e instrucciones de instalación listas para ser instaladas por [pacman](/index.php/Pacman "Pacman").

Un paquete de Arch no es más que un archivo tar o 'tarball', comprimido usando xz, que contiene los siguientes archivos generados por makepkg:

*   Archivos binarios a instalar.

*   `.PKGINFO`: contiene todos los metadatos requeridos por pacman para tratar con paquetes, dependencias, etc.

*   `.MTREE`: contiene hashes y marcas de tiempo de los archivos que se incluyen en la base de datos local para que pacman pueda verificar la integridad del paquete.

*   `.INSTALL`: un archivo opcional utilizado para ejecutar comandos después de la fase de instalación/actualización/eliminación. (Este archivo sólo está presente si se especifica en el `.PKGBUILD`).

*   `Changelog`: un archivo opcional guardado por el responsable del paquete documentando los cambios del paquete. (No está presente en todos los paquetes.)

### Metapaquetes y grupos

Un grupo de paquetes es un conjunto de paquetes relacionados, definido por el empaquetador, que se pueden instalar o desinstalar simultáneamente utilizando el nombre de grupo como un sustituto para cada nombre de paquete individual. Si bien un grupo no es un paquete, puede instalarse de manera similar a un paquete, vea [Pacman#Installing package groups](/index.php/Pacman#Installing_package_groups "Pacman") y [PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

Un metapaquete a menudo (aunque no siempre) titulado con -meta sufijo, proporciona funcionalidad similar a un grupo de paquetes que permite que se instalen o desinstalen simultáneamente varios paquetes relacionados. Los metapaquetes pueden ser instalados como cualquier otro paquete, vea [Pacman#Installing specific packages](/index.php/Pacman#Installing_specific_packages "Pacman"). La única diferencia entre un paquete meta y un paquete regular es que una metapaquete está vacío y existe puramente para vincular paquetes relacionados a través de dependencias.

La ventaja de un metapaquete, en comparación con un grupo, es que cualquier nuevo miembro del paquete se instalará cuando el propio metapaquete sea actualizado con un nuevo conjunto de dependencias. Esto contrasta con un grupo en el que los nuevos miembros del grupo no se instalarán automáticamente. La desventaja de un metapaquete es que no es tan flexible como un grupo - puede elegir los miembros del grupo que desea instalar pero no puede elegir qué dependencias del metapaquete desea instalar. Asimismo, puede desinstalar los miembros del grupo sin tener que quitar el grupo entero, sin embargo no se pueden quitar dependencias del metapaquete sin tener que desinstalar el metapaquete en sí mismo.

## Preparación

### Programas necesarios

Asegúrese primero de que las herramientas necesarias estén instaladas. [Instalando](/index.php/Help:Reading#Installation_of_packages "Help:Reading") el grupo de paquetes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) debe ser suficiente; incluye **make** y herramientas adicionales necesarias para compilar desde el codigo fuente.

Una de las herramientas clave para la construcción de paquetes es [makepkg](/index.php/Makepkg "Makepkg") (proporcionado por [pacman](/index.php/Pacman "Pacman")), que hace lo siguiente:

1.  Comprueba que las dependencias del paquete están instaladas.
2.  Descarga el(los) archivo(s) fuente desde el(los) servidor(es) especificado(s).
3.  Desempaque el(los) archivo(s) fuente(s).
4.  Compila el software y lo instala en un entorno fakeroot.
5.  Despojar los símbolos innecesarios de los binarios y las bibliotecas.
6.  Genera el archivo del metapaquete que se incluye con cada paquete.
7.  Comprime el entorno fakeroot en un archivo de paquete.
8.  Almacena el archivo de paquete en el directorio de destino configurado, que es el directorio de trabajo actual de forma predeterminada.

### Descargar y probar la instalación

Descargue el tarball con el codigo fuente del software que desea empaquetar, extráigalo, y siga los pasos del autor para instalar el programa. Anote todos los comandos y/o pasos necesarios para compilarlo e instalarlo. Usted repetirá los mismos comandos en el archivo *PKGBUILD*. La mayoría de los autores de software se adhieren al ciclo de compilación de 3 pasos:

```
./configure
make
make install

```

Este es un buen momento para asegurarse de que el programa funciona correctamente.

## Creando el PKGBUILD

Cuando usted ejecuta `makepkg`, buscará un archivo `PKGBUILD` en el directorio de trabajo actual. Si se encuentra un archivo `PKGBUILD` se descargará el código fuente del software y compilará de acuerdo con las instrucciones especificadas en el archivo `PKGBUILD`. Las instrucciones deben ser completamente interpretables por el shell [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) "wikipedia:Bash (Unix shell)"). Después de la finalización satisfactoria, los binarios y metadatos resultantes del paquete, i.e. versión del paquete y dependencias, se empaquetan en un archivo de paquete `pkgname.pkg.tar.xz` que se puede instalar con `pacman -U <Archivo paquete>`.

Para comenzar con un nuevo paquete, primero debe crear un directorio de trabajo vacío, entre en ese directorio y cree un archivo `PKGBUILD`. Puede copiar el PKGBUILD de ejemplo desde el directorio `/usr/share/pacman/` a su directorio de trabajo o copiar un `PKGBUILD` de un paquete similar. Este último puede ser útil si sólo necesita cambiar algunas opciones.

### Definiendo las variables del `PKGBUILD`

Ejemplos de archivos PKGBUILD se encuentran en `/usr/share/pacman/`. Se puede encontrar una explicación de las posibles variables `PKGBUILD` en el artículo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

*makepkg* define dos variables que se debe utilizar como parte del proceso de creación e instalación:

	`srcdir`

	Esto apunta al directorio donde *makepkg* extrae o crea enlaces simbólicos de todos los archivos de la matriz de origen.

	`pkgdir`

	Esto apunta al directorio en el que *makepkg* agrupa el paquete instalado, que se convierte en el directorio raíz del paquete construido.

Todos ellos contienen rutas *absolutas*, lo que significa que no tiene que preocuparse por su directorio de trabajo si utiliza estas variables correctamente.

**Nota:** *makepkg* y, por tanto, las funciones `build()` y `package()`, están destinados a ser no interactivos. Utilidades interactivas o scripts llamados en esas funciones pueden romper *makepkg*, especialmente si se invoca con el registro de compilación habilitado (`-L`). ([FS#13214](https://bugs.archlinux.org/task/13214).)

**Nota:** aparte del actual mantenedor de paquetes, es posible que existan mantenedores anteriores listados como colaboradores.

### Funciones PKGBUILD

Hay cinco funciones, enumeradas aquí en el orden en que se ejecutan si todas existen. Si una no existe, simplemente se omite.

**Nota:** : Esto no se aplica a la función `package()`, como se requiere en cada PKGBUILD.

#### prepare()

Esta función, utiliza comandos para preparar las fuentes para la construcción que se ejecuta, como [parches](/index.php/Patching_in_ABS "Patching in ABS"). Esta función se ejecuta justo después de la extracción del paquete, antes de [pkgver()](#pkgver.28.29) y la función de build. Si la extracción se omite (`makepkg -e`), entonces `prepare()` no se ejecuta.

**Nota:** : (Desde [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5)) La función se ejecuta en modo `bash -e`, significa que cualquier comando que aparezca con un estado distinto de cero hará que la función termine.

#### pkgver()

`pkgver()` se ejecuta después de la obtención de las fuentes, la extracción y la ejecución de [prepare()](#prepare.28.29). Así que uested puede actualizar la variable pkgver durante la etapa makepkg.

Esto es particularmente útil si está haciendo [making git/svn/hg/etc. paquetes](/index.php/VCS_PKGBUILD_Guidelines "VCS PKGBUILD Guidelines"), donde el proceso de construcción puede seguir siendo el mismo, pero el codigo fuente podría ser actualizado todos los días, incluso cada hora. La vieja manera de hacer esto era poner la fecha en el campo del pkgver, donde si el Software no se actualizaba, makepkg aún así lo reconstruiría pensando que la versión había cambiado. Algunos comandos útiles para esto son `git describe`, `hg identify -ni`, etc. Por favor pruebe estos antes de enviar un PKGBUILD, ya que un error en la función `pkgver()` puede detener la compilación.

Nota: pkgver no puede contener espacios ni guiones (`-`). El uso de sed para corregir esto es común.

#### build()

Ahora necesita implementar la función `build()` en el archivo `PKGBUILD`. Esta función utiliza comandos de shell comunes en la sintaxis de [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) para compilar automáticamente el software y crear un directorio `pkg` para instalar el software. Esto permite a makepkg empaquetar archivos sin tener sin tener que filtrar el sistema de archivos.

El primer paso en la función `build()` es cambiar al directorio creado descomprimiendo el tarball de origen. *makepkg* cambiará el directorio actual a `$srcdir` antes de ejecutar la función `build()`. Por lo tanto, en la mayoría de los casos, como se sugiere en `/usr/share/pacman/PKGBUILD.proto`, el primer comando se verá así:

```
cd "$pkgname-$pkgver"

```

Ahora, necesita listar los mismos comandos que utilizó cuando compiló manualmente el software. La función `build()` en esencia automatiza todo lo que hizo a mano y compila el software en el entorno de compilación fakeroot. Si el software que está empaquetando utiliza un script, es una buena práctica usar `--prefix=/usr` al crear paquetes para pacman. Una gran cantidad de software instala archivos relativos al directorio `/usr/local`, que sólo se debe hacer si se está generando manualmente desde el codigo fuente. Todos los paquetes Arch Linux deben usar el directorio `/usr`. Como se ve en el archivo `/usr/share/pacman/PKGBUILD.proto`, las siguientes dos líneas suelen tener este aspecto:

```
./configure --prefix=/usr
make

```

**Nota:** : Si su software no necesita construir nada, NO utilice la función `build()`. La función `build()` no es necesaria, pero la La función `package()` si lo es.

#### check()

Momento para llamar a `make check` para hacer chequeos y rutinas similares de prueba. Es muy recomendable tener `check()`, ya que ayuda a asegurar que el software se ha construido correctamente y funciona bien con sus dependencias.

Usuarios que no lo necesitan (Y ocasionalmente los mantenedores que no pueden arreglar un paquete para que esto pase) puede inhabilitarlo usando `BUILDENV+=('!check')` en el PKGBUILD/makepkg.conf o llamar `makepkg` con flag `--nocheck`.

#### package()

El paso final es poner los archivos compilados en un directorio donde *makepkg* puede recuperarlos para crear un paquete. Por defecto es el directorio `pkg` - un simple entorno fakeroot. El directorio `pkg` replica la jerarquía del sistema de archivos raíz de las rutas de instalación del software. Si tiene que colocar manualmente los directorios raíz de su sistema de archivos, debe instalarlos en el directorio `pkg` bajo la misma estructura de directorios. Por ejemplo, si desea instalar un archivo en `/usr/bin`, debe colocarse en `$pkgdir/usr/bin`. Muy pocos procedimientos de instalación requieren que el usuario copie docenas de archivos manualmente. En su lugar, la mayoría de software `make install` lo hará. La última línea debe ser similar a la siguiente para poder instalar correctamente el software en el directorio `pkg`:

```
make DESTDIR="$pkgdir/" install

```

**Nota:** : A veces está el caso en que `DESTDIR` no se utiliza en el `Makefile`; puede que tenga que usar `prefix` en su lugar. Si el paquete está construido con *autoconf* / *automake*, use `DESTDIR`; esto es lo que se documenta en los [manuales](https://www.gnu.org/software/automake/manual/automake.html#Install). Si `DESTDIR` no funciona, trate de construir con `make prefix="$pkgdir/usr/" install`. Si eso no funciona, tendrá que buscar más en los comandos de instalación que son ejecutados por "`make <...> install`".

En algunos casos raros, el software espera ejecutarse desde un único directorio. En tales casos, es aconsejable simplemente copiarlos `$pkgdir/opt`.

A menudo, el proceso de instalación del software creará subdirectorios debajo del directorio `pkg`. Si no lo hace, *makepkg* generará muchos errores y necesitará crear manualmente subdirectorios añadiendo los comandos apropiados de `mkdir -p` en la función `build()` antes de ejecutar el procedimiento de instalación.

En los paquetes antiguos, no había ninguna función `package()`. Por lo tanto, los archivos se colocaban en el directorio *pkg* al final de la función `build()`. Si `package()` no está presente, `build()` se ejecuta a través de *fakeroot*. En paquetes nuevos, `package()` es necesario y se ejecuta a través de *fakeroot* en su lugar, y `build()` se ejecuta sin privilegios especiales.

`makepkg --repackage` ejecuta sólo la función `package()`, por lo que crea un archivo `*.pkg.*` archivo sin compilar el paquete. Esto puede ahorrar tiempo, e.g. si acaba de cambiar las variables `depends` del paquete.

**Nota:** La función `package()` es la única función requerida en un PKGBUILD. Si sólo debe copiar archivos en sus respectivos directorios para instalar un programa, no lo ponga en la función `build()`, póngalo en la función `package()`.

**Nota:** Crear enlaces simbólicos es un proceso un poco incómodo en la función `package()`. Utilizando el enfoque ingenuo `ln -s "${pkgdir}/from/foo" "${pkgdir}/to/goo"` resultará en un enlace simbólico roto al directorio de compilación. La manera correcta de crear una link es crearlo apuntando a una fuente inicialmente rota, `ln -s "/from/foo" "${pkgdir}/to/goo"`. Una vez instalado el paquete, el enlace apuntará al lugar correcto.

## Prueba del PKGBUILD y del paquete

Al escribir la función `build()`, querrá probar sus cambios frecuentemente para asegurarse de que no haya errores. Puedes hacerlo usando el comando `makepkg` en el directorio que contiene el archivo `PKGBUILD`. Con un `PKGBUILD` correctamente formateado, makepkg creará un paquete; con un `PKGBUILD` roto o inacabado, provocará un error.

Si makepkg finaliza correctamente, colocará un archivo denominado `pkgname-pkgver.pkg.tar.xz` en su directorio de trabajo. Este paquete puede ser instalado con el comando `pacman -U`. Sin embargo, sólo porque un archivo de paquete fue construido no implica que es totalmente funcional. Eso 11 Posiblemente sólo contenga el directorio y ningún archivo en si, por ejemplo, un prefijo se especificó incorrectamente. Puedes usar las funciones de consulta de pacman para mostrar una lista de archivos contenidos en el paquete y las dependencias que requiere con p`pacman -Qlp [package file]` y `pacman -Qip [package file]`, respectivamente.

¡Si el paquete parece sano, entonces usted a terminado! Sin embargo, si planea liberar el archivo `PKGBUILD`, es imperativo que compruebe y compruebe de nuevo el contenido de la matriz de `dependencias`.

También asegúrese de que los binarios del paquete realmente *funcionan* perfectamente! Es molesto liberar un paquete que contiene todos los archivos necesarios, pero se bloquea Debido a alguna opción de configuración poco clara que no funciona bien con el resto del sistema. Si solo va a compilar paquetes para su propio sistema, entonces usted no necesita preocuparse demasiado sobre este paso de aseguramiento de calidad, después de todo es la única persona que sufre de errores.

### Comprobación de la sanidad del paquete

Después de comprobar la funcionalidad del paquete, compruebe si hay errores con namcap:

```
$ namcap PKGBUILD
$ namcap *<package file name>*.pkg.tar.xz

```

Namcap deberá:

1.  Comprobar el contenido de PKGBUILD para buscar errores comunes y la jerarquía de archivos de paquetes para archivos innecesarios/extraviados.
2.  Escanea todos los archivos ELF en el paquete usando ldd, informando automáticamente qué paquetes con las bibliotecas compartidas requeridas faltan de las dependencias y que se pueden omitir como dependencias transitivas.
3.  Búsqueda heurística de dependencias perdidas y redundantes.

y mucho más. Adquiera el hábito de revisar sus paquetes con namcap para evitar tener que arreglar los errores más simples después de la subida del paquete.

## Subir paquetes a AUR

Por favor lea [Arch User Repository#Submitting packages](/index.php/Arch_User_Repository#Submitting_packages "Arch User Repository") de la guía de AUR. Para una descripción detallada del proceso.

## Resumen

1.  Descargue el código fuente del software que quiera empaquetar.
2.  Trate de compilar e instalar el software en un directorio arbitrario
3.  Copie el prototipo de `/usr/share/pacman/PKGBUILD.proto` y renómbrelo como `PKGBUILD` en un directorio de trabajo, preferiblemente ~/abs
4.  Edite el `PKGBUILD` de acuerdo a las necesidades de su paquete
5.  Ejecute `makepkg` para verificar si el paquete se construye correctamente
6.  Si no es así, repita los últimos dos pasos

### Advertencias

*   Antes de automatizar el proceso de construcción de paquetes, deberá haberlo hecho por lo menos una vez de manera manual para saber de antemano exactamente lo que esta haciendo. Desafortunadamente muchos autores de paquetes se apegan al proceso de 3 pasos de `./configure, make make install`, este no es siempre el caso y puede quedar un paquete en muy malas condiciones si no aplica el cuidado necesario para que todo funcione bien.
*   En algunos pocos casos, los paquetes no son disponibles en código fuente y habrá que recurrir a scripts como `sh instalador.run` para poder ejecutarlo, habrá de hacer una extensa investigación acerca de otros `PKGBUILD`, leer los `README`, buscar información del creador del programa, o buscar `EBUILDS` de Gentoo para poder ejecutar la instalación, recuerde que makepkg debe ser completamente automático y sin intervención del usuario.

## Directrices más detalladas

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## Generadores de PKGBUILD

Los PKGBUILD para algunos paquetes se pueden generar automáticamente.

**Nota:** Los usuarios aún son responsables de garantizar que el paquete cumpla con los estándares de alta calidad antes de enviar los archivos generados a [AUR](/index.php/AUR "AUR").

*   [Go](/index.php/Go "Go"): [go-makepkg](https://github.com/seletskiy/go-makepkg)
*   [Haskell](/index.php/Haskell "Haskell"): [cblrepo](https://github.com/magthe/cblrepo)
*   [Python](/index.php/Python "Python"): [pipman-git](https://aur.archlinux.org/packages/pipman-git/), [pip2arch-git](https://aur.archlinux.org/packages/pip2arch-git/), [python-pypi2pkgbuild](https://aur.archlinux.org/packages/python-pypi2pkgbuild/)
*   [Ruby](/index.php/Ruby "Ruby"): [gem2arch](https://aur.archlinux.org/packages/gem2arch/), [pacgem](https://aur.archlinux.org/packages/pacgem/)

## Véase también

*   [How to correctly create a patch file](https://bbs.archlinux.org/viewtopic.php?id=91408).
*   [Arch Linux Classroom IRC Logs of classes about creating PKGBUILDs](https://archwomen.org/media/project_classroom/classlogs/).
*   [Fakeroot approach for package installation](http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt)
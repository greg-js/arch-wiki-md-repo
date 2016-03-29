Este artículo pretende ayudar al usuario a crear sus propios paquetes usando el sistema de empaquetado “tipo ports” de Arch Linux. Cubre la creación de un archivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") – un archivo de descripción del paquete empaquetado acompañado del archivo `makepkg` que sirve para crear un archivo binario desde las fuentes. Si ya tiene un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), favor de leer la wiki de [makepkg](/index.php/Makepkg "Makepkg").

## Contents

*   [1 Resumen](#Resumen)
*   [2 Preparación](#Preparaci.C3.B3n)
    *   [2.1 Pre requisitos de software](#Pre_requisitos_de_software)
    *   [2.2 Descargar y probar la instalación](#Descargar_y_probar_la_instalaci.C3.B3n)
*   [3 Creando el PKGBUILD](#Creando_el_PKGBUILD)
    *   [3.1 Definiendo las variables del PKGBUILD](#Definiendo_las_variables_del_PKGBUILD)
    *   [3.2 La función build()](#La_funci.C3.B3n_build.28.29)
    *   [3.3 Guías adicionales.](#Gu.C3.ADas_adicionales.)
*   [4 Probando el PKGBUILD y el paquete](#Probando_el_PKGBUILD_y_el_paquete)
    *   [4.1 Ldd y namcap](#Ldd_y_namcap)
*   [5 Subir paquetes a AUR](#Subir_paquetes_a_AUR)
*   [6 Resumen](#Resumen_2)
    *   [6.1 Advertencias](#Advertencias)

## Resumen

Los paquetes en Arch Linux son ensamblados utilizando la utilidad [makepkg](/index.php/Makepkg "Makepkg") con la información guardada en el archivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Cuando se ejecuta `makepkg` este busca en el archivo `PKGBUILD` en el directorio que se encuentre y sigue las instrucciones ahí guardadas para ya sea compilar o descargar los archivos necesarios para ser empaquetados en un archivo comprimido (`nombredelpaquete.pkg.tar.xz`)

Un paquete en ArchLinux no es más que un archivo tar comprimido utilizando xz o “tarball” que contiene:

*   Los archivos binarios a instalar.

*   `.PKGINFO`: contiene toda la metadata necesaria para pacman para manejar los paquetes, dependencias, etc.

*   `.INSTALL`: Un archivo opcional con comandos a ejecutar después de la instalación/ actualización/desinstalación de un paquete (se encuentra presente solo si se especificó en el `.PKGBUILD`).

*   `Changelog`: Un archivo opcional mantenido por el administrador del paquete documentando los cambios del paquete (no está en todos los paquetes).

## Preparación

### Pre requisitos de software

En primer lugar garantizar que las herramientas necesarias están instaladas. El grupo de paquetes “base-devel” debe ser suficiente; incluye make y las herramientas necesarias para compilar desde fuentes.

```
# pacman -S base-devel

```

Una de las herramientas clave para armar paquetes es [makepkg](/index.php/Makepkg "Makepkg") (proporcionado por [pacman](https://www.archlinux.org/packages/?name=pacman)) que cumple con las siguientes características:

1.  Verificar si las dependencias están instaladas.
2.  Descargar el(los) archivo(s) fuente del (los) servidor(es)
3.  Desempaquetar el (los) archivo(s) fuente
4.  Compilar el software e instalarlo dentro de un ambiente de fakeroot
5.  Limpia de símbolos los binarios y librerías
6.  Generar el archivo de meta-paquete que se incluye en cada paquete
7.  Comprimir el ambiente de fakeroot en el archivo del paquete
8.  Crear y guardar el paquete creado en el directorio destino, que es el directorio de trabajo por default

### Descargar y probar la instalación

Descargue el archivo comprimido tarball del software que quiere empaquetar, extráigalo, y sigua las instrucciones del autor para instalar el programa. Tome nota de todos los comandos y pasos a seguir para compilar e instalar este software. Estará repitiendo esos mismos pasos en el archivo *PKGBUILD*.

Muchos autores se apegan al proceso de compilación e instalación tradicional:

./configure make make install También es buen momento para verificar que el programa cumpla su tarea correctamente.

## Creando el PKGBUILD

Cuando ejecuta `makepkg` buscara el archivo `PKGBUILD` en el directorio actual. Si este archivo es encontrado descargará el código fuente del software, y lo compilará de acuerdo a las instrucciones guardadas en el archivo `PKGBUILD`. Estas instrucciones deben ser completamente comprensibles para el [Bash](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash") Shell. Después de una compilación exitosa los binarios resultantes y la metadata del software (versión del software y dependencias) son empaquetadas en un archivo comprimido paquete.pkg.tar.xz que puede ser instalado con el comando `pacman -U [package file]`

### Definiendo las variables del `PKGBUILD`

El archivo `PKGBUILD` contiene metadata referente al software a instalar. Es un archivo de texto plano. El siguiente es un archivo PKGBUILD de ejemplo que se puede localizar en el directorio `/usr/share/pacman` junto con otras plantillas-.

```
/usr/share/pacman/PKGBUILD.proto

```

```
# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname=NAME
pkgver=VERSION
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #generate with 'makepkg -g'

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}

```

Una explicación de posibles variables del `PKGBUILD` se encuentra en la wiki de [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

### La función `build()`

Ahora hay que implementar la función `build()` en el archivo `PKGBUILD`. Esta función utiliza sintaxis de comandos comunes de [Bash](https://es.wikipedia.org/wiki/Bash) para compilar automáticamente el software y también crear el directorio `pkg` para instalar el software. Esto permite a `makepkg` empaquetar los archivos sin envegar entre directorios de su filesystem.

El primer paso de la función `build()` es entrar al directorio creado al descomprimir el archivo fuente. En la mayoría de los casos ese comando se vera como este:

```
cd $srcdir/$pkgname-$pkgver

```

Ahora hay que listar todos los comandos que utilizo al compilar e instalar manualmente el software. Esencialmente la función `build()` pretende automatizar todo esto y compilar el software en un ambiente de fakeroot. Si el software a instalar utiliza un script configure, es buena practica utilizar --prefix=/usr al crear paquetes para pacman. Hay mucho software que instala archivos en el directorio /usr/local, esto debería ser hecho solamente si usted esta instalando manualmente desde código fuente. Así como se especifica en el archivo /usr/share/pacman/PKGBUILD.proto, las siguientes dos líneas pueden ser parecidas a esto:

```
./configure --prefix=/usr
make

```

El paso final en la función `build()` es poner los archivos compilados donde makepkg los pueda llamar para crear un paquete. Esto por default es el directorio pkg – un simple entorno fakeroot. El directorio pkg replica la jerarquía del sistema de archivos raíz de las rutas de instalación del software, si necesita dejar archivos dentro de su sistema de archivos raíz, deberá instalarlos en el directorio `pkg` dentro de la misma estructura de directorios. Por ejemplo, si quiere instalar un programa dentro del directorio `/usr/bin`, debe ser ubicado dentro de `$pkgdir/usr/bin`. Hay muy pocos procedimientos de instalación que requieran que el usuario copie manualmente estos archivos, pero vale la pena aclararlo. En vez de eso, en la mayoría del software, llamar a make install automatizara esa tarea. La última línea deberá parecer a la siguiente, para instalar el software correctamente en el directorio `pkg`:

```
make DESTDIR=$pkgdir install

```

**Nota:** se puede dar el caso que el argumento `DESTDIR` no sea utilizado en el `Makefile`; en vez de esto habrá que utilizar el argumento `prefix`, si el paquete es compilado con *automake*/*autoconf*, utiliza `DESTDIR`, esto esta documentado en los manuales. Si `DESTDIR` no funciona trate de compilarlo con `make prefix="$pkgdir/usr/" install`. Si es no funciona, tendrá que investigar aun más en los comandos de instalación que son ejecutados por *make* e *install*.

En algunos casos raros, el software espera ser ejecutado dentro de algún directorio en específico. En estos casos se recomienda copiar estos a `$pkgdir/opt`. Muy seguido, el proceso de instalación creara subdirectorios dentro del directorio `pkg`. Si no es así, *makepkg* generara muchos errores y usted se vera obligado a crear estos directorios manualmente agregando los comandos `mkdir -p` dentro de la función `build()` antes de que inicie el proceso de instalación.

También *makepkg* define tres variables que deberá tomar en cuenta como parte del proceso de compilación e instalación:

	`startdir`

	Contiene la ruta absoluta al directorio donde el `PKGBUILD` esta localizado. Esta variable se utiliza en combinación con los postfijos `/src` o `/pkg`, sin embargo el uso de `srcdir` y `pkgdir` son los métodos modernos utilizados.`$startdir/src` no es garantía de ser igual a `$srcdir` y muy seguramente para `$pkgdir`. El uso de esta variable esta depreciado se recomienda ampliamente no utilizarlo.

	`srcdir`

	Apunta al directorio donde *makepkg´ extrae o copia todos los archivos fuente*

	`pkgdir`

	Apunta al directorio donde *makepkg* empaqueta el software instalado, que se convierte el directorio raíz del paquete construido.

**Nota:** *makepkg*, y por ende la función `build()` son pensadas para no ser interactivas. Las rutinas que requieran interacción del usuario que sean llamadas dentro de la función `build()` podrían destruir el *makepkg*, particularmente si es invocado con el registro de compilación habilitado (ver [Arch Linux Bug #13214](https://bugs.archlinux.org/task/13214))

### Guías adicionales.

Por favor lea los estándares de empaquetado de Arch para mejores prácticas y consideraciones adicionales.

## Probando el PKGBUILD y el paquete

Mientras escribe la función `build()` deberá probar los cambios con frecuencia para asegurarse de que no haya fallas. Puede hacerlo utilizando el comando `makepkg` en el directorio donde se encuentre el archivo `PKGBUILD`. Con un `PKGBUILD` correctamente compuesto `makepkg` será capaz de crear un paquete, con un `PKGBUILD` incorrecto o roto `PKGBUILD` mostrara un error.

Si `makepkg` finaliza correctamente, creara un archivo llamado `pkgname-pkgver.pkg.tar.xz` en su directorio de trabajo. Este paquete puede ser instalado con el comando `pacman -U`. Sin embargo solo por que un paquete haya sido correctamente construido esto no implica que sea completamente funcional, es concebible que contenga solo el directorio y ningún archivo si por ejemplo, un prefijo fue especificado incorrectamente. Puede utilizar las herramientas de consulta de pacman para ver la lista de archivos contenidos en el paquete y las dependencias que puede requerir con `pacman -Qlp [nombre del paquete]` y `pacman -Qip [nombre del paquete]`

Si el paquete se ve sano, entonces ha terminado!, sin embargo si va a publicar el `PKGBUILD`, es imperativo que revise y vuelva a revisar el contenido de la variable depends.

También asegúrese de que el software ejecute sin ningún fallo. Es molesto que al publicar un paquete que contenga todos los archivos necesarios deje de funcionar por alguna opción en alguna configuración obsoleta que ya no funciona en relación con el resto del sistema. Si solo va a compilar paquetes solo para su sistema, entonces no tendrá que preocuparse mucho de este procedimiento de seguranza de calidad, al final de cuentas solo usted sufrirá las consecuencias de una mala configuración.

### `Ldd` y `namcap`

Las dependencias incumplidas son el error más común del empaquetado. Hay dos excelentes herramientas para verificar el cumplimiento de las dependencias. La primera es *ldd* que mostrara las dependencias compartidas de librerías de ejecutables:

```
$ ldd gcc
linux-gate.so.1 =>  (0xb7f33000)
libc.so.6 => /lib/libc.so.6 (0xb7de0000)
/lib/ld-linux.so.2 (0xb7f34000)

```

La otra herramienta es *namcap*, que solo verifica por las dependencias y no por la sanidad del todo el paquete en si. Por favor lea el artículo sobre namcap para mayores referencias.

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

Antes de automatizar el proceso de construcción de paquetes, deberá haberlo hecho por lo menos una vez de manera manual para saber de antemano exactamente lo que esta haciendo. Desafortunadamente muchos autores de paquetes se apegan al proceso de 3 pasos de `./configure, make make install`, este no es siempre el caso y puede quedar un paquete en muy malas condiciones si no aplica el cuidado necesario para que todo funcione bien. En algunos pocos casos, los paquetes no son disponibles en código fuente y habrá que recurrir a scripts como `sh instalador.run` para poder ejecutarlo, habrá de hacer una extensa investigación acerca de otros `PKGBUILD`, leer los `README`, buscar información del creador del programa, o buscar `EBUILDS` de Gentoo para poder ejecutar la instalación, recuerde que makepkg debe ser completamente automático y sin intervención del usuario.
Un `PKGBUILD` es un archivo descriptivo de construcción de un paquete para Arch Linux (realmente es un script de shell) usado para la [Creación de paquetes](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)"). Este articulo describe posibles variables del `PKGBUILD`.

## Construyendo paquetes

Los paquetes en Arch Linux son construidos utilizando [makepkg](/index.php/Makepkg "Makepkg") y la información almacenada en un `PKGBUILD`. Cuando se ejecuta `makepkg` busca un `PKGBUILD` en el directorio actual y sigue las instrucciones ahí almacenadas para compilar y/o descargar y empaquetar todos los archivos necesarios en un archivo `pkgname.pkg.tar.xz`). Este archivo resultante contiene archivos binarios e instrucciones de instalación legibles para [pacman](/index.php/Pacman "Pacman").

Vea la documentación de [Creando paquetes (Español)](/index.php/Creando_paquetes_(Espa%C3%B1ol) "Creando paquetes (Español)") para mayor información

## Variables

Las siguientes son variables que pueden ser encontradas en el archivo `PKGBUILD`:

	`pkgname` 

	El nombre del paquete. Debe consistir de **caracteres alfanuméricos y guiones('-')** y todas las letras deben estar en **minúsculas**. Por el bien de la consistencia el nombre del `pkgname` debe coincidir con el nombre del archivo comprimido del código fuente del software que se esta empaquetando. Por ejemplo, si el software que se esta empaquetando es `foobar-2.5.tar.gz`, el nombre del `pkgname` debe ser *foobar*. En el directorio de trabajo el nombre del `PKGBUILD` también debe coincidir con el `pkgname`.

	`pkgver` 

	La versión del paquete . El valor debe ser el mismo que el del autor del software que se esta empaquetando. Puede contener letras, números y puntos pero no puede contener guiones medios ('-'). si el autor del paquete utiliza guiones medios en su sistema de versiones, remplazelos con un guion bajo ('_'). por ejemplo, si la versión de un paquete es *0.99-10*, deberá ser cambiada a *0.99_10*. si la variable pkgver es utilizada mas tarde en el PKGBUILD entonces el guion bajo puede ser sustituido fácilmente por un guion medio, por ejemplo: source=($pkgname-${pkgver//_/-}.tar.gz)

	`pkgrel` 

	El numero de versión del paquete especifico para Arch Linux. Este valor permite a los usuarios diferenciar entre empaquetados consecutivos de la misma versión del paquete. Cuando un paquete es liberado por primera vez, “el numero de versión empieza en 1”. cuando se hacen reparaciones y optimizaciones al mismo `PKGBUILD`, el paquete sera “reliberado” y el “numero de liberación” aumenta por 1\. cuando una nueva versión del paquete se libera (y no solo es una reparación u optimizacion) el numero de versión se resetea a 1.

	`pkgdesc` 

	La descripción del paquete. La descripción del paquete debe ser de 80 caracteres o menos y no debe incluir el nombre del paquete como auto referencia, por ejemplo “Nedit es un editor de texto para X11” debe ser escrito: “Un editor de texto para X11”.

	`arch` 

	Una lista de arquitecturas en las que el `PKGBUILD` suele compilar e instalar . Puede ser **i686** y/o **x86_64**, `arch=('i686' 'x86_64')`. El valor **any** puede referir a independiente de arquitectura. Puede acceder al valor de la variable desde `$CARCH` durante el empaquetado.

	`url` 

	La URL del sitio oficial del software que esta siendo empaquetado.

	`license` 

	La licencia en la que el software es distribuido. Un paquete [licenses](https://www.archlinux.org/packages/?name=licenses) has sido creado en `[core]` que contiene las licencias de uso común en `/usr/share/licenses/common` , p ej. `/usr/share/licenses/common/GPL`. Si un paquete es licenciado bajo alguna de estas licencias, el valor debe ser puesto al nombre del directorio, por ejemplo. `license=('GPL')`. Si la licencia no esta incluida en el paquete oficial [licenses](https://www.archlinux.org/packages/?name=licenses) hay varias cosas que hay que hacer:

1.  Los campos de la licencia deben ser incluidos en `/usr/share/licenses/**pkgname**/`, por ejemplo: `/usr/share/licenses/foobar/LICENSE`.
2.  Si el paquete fuente no contiene los detalles de la licencia y esta solo es mostrada en otro lado, por ejemplo un sitio web, entonces tendrá que copiar la licencia en un archivo e incluirla
3.  Agregue el valor **custom** a la variable `license`. Opcionalmente puede remplazar **custom** con **custom:nombre de la licencia**. Una vez que esta licencia sea utilizada en dos o mas paquetes de un repositorio oficial (incluyendo `[comunitario]`) se vuelve parte del paquete [licenses](https://www.archlinux.org/packages/?name=licenses)

*   Las licencias [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License"), [MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License"), [zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") y [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") son casos especiales y pueden no ser incluidos en el paquete [licenses](https://www.archlinux.org/packages/?name=licenses). Por el bien de la lista de `licencias` serán tratadas como una licencia en común (`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` y `license=('Python')`) pero técnicamente cada una de estas es una licencia diferente por que cada una de ellas tiene sus propias reglas de copyright, cada paquete instalado con cualquiera de estas licencias debe incluir su propia licencia almacenada en `/usr/share/licenses/**pkgname**`. Algunos paquetes tal vez no estén cubiertos por solo una licencia, en este caso, se pueden agregar múltiples entradas a la lista de licencias, por ejemplo: `license=('GPL' 'licencia personalizada')`.

*   Adicionalmente la (L)GPL tiene varias versiones y permutaciones. Para software bajo la (L)GPL la convención aceptada es:

*   *   (L)GPL - (L)GPLv2 o cualquier versión posterior
    *   (L)GPL2 - (L)GPL2 solamente
    *   (L)GPL3 - (L)GPL3 o cualquier versión posterior

	`groups` 

	El grupo al que pertenece el paquete. Por ejemplo, cuando usted instala el paquete [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/), instala todos los paquetes que pertenecen al grupo `kde`.

	`depends` 

	Una lista de paquetes que deben ser instalados antes de que el software empaquetado pueda ejecutarse. Si el software requiere una mínima versión de una dependencia, el operador **>=** puede ser utilizado para señalar esto, por ejemplo. `depends=('foobar>=1.8.0')`. No es necesario listar paquetes en los que su software dependa si hay otros paquetes instalados con esta dependencia ya instalada. Por ejemplo [gtk2](https://www.archlinux.org/packages/?name=gtk2) depende de [glib2](https://www.archlinux.org/packages/?name=glib2) y [glibc](https://www.archlinux.org/packages/?name=glibc). Pero [glibc](https://www.archlinux.org/packages/?name=glibc) no debe ser listado como una dependencia de [gtk2](https://www.archlinux.org/packages/?name=gtk2) por que ya es una dependencia de [glib2](https://www.archlinux.org/packages/?name=glib2).

	`makedepends` 

	Una lista de paquetes que deben estar instalados para compilar el paquete pero que son innecesarios para que este funcione despues de la instalacion. Puede especificar un numero mínimo de dependencias de la misma forma que la lista de `depends`.

**Advertencia:** Se asume que el grupo "base-devel" ya esta instalado cuando se construye un paquete con makepkg, los paquetes miembros del grupo base-devel" no deben ser incluidos en la lista de makedepends

	`optdepends` 

	Una lista de paquetes que no son necesarios para que el paquete funcione en si, pero que proveen características adicionales. Una pequeña descripción de lo que hace cada paquete debe ser incluido. Una lista de `optdepends` puede verse así

```
'optdepends=('cups: soporte de impresion'
'sane: soporte de scanners'
'libgphoto2: soporte de cámaras digitales'
'alsa-lib: soporte de sonido'
'giflib: GIF soporte de imágenes'
'libjpeg: JPEG soporte de imágenes'
'libpng: PNG soporte de imágenes)'

```

	`provides` 

	Una lista de nombres de paquetes que este paquete provee o cumple (o un paquete virtual como “cron o “sh”). Si utiliza esta variable, deberá agregar la versión (`pkgver` y tal vez el `pkgrel`) que este paquete provea si acaso hay dependencias afectadas por este. Por ejemplo, si usted provee un paquete modificado de “qt” llamado “qt-foobar” versión 3.3.8 que provee “qt” entonces la lista de `provides` deberá verse así: `provides=('qt=3.3.8')`. Poner la linea `provides=('qt')` causara que las dependencias fallen a la hora de requerir una versión especifica de “qt”. No agregue `pkgname` a su lista de provides, esto es hecho automáticamente.

	`conflicts` 

	Una lista de paquetes que pueden causar problemas con este paquete si es instalado. También puede especificar las propiedades de la versión de los paquetes conflictivos de la misma forma que la lista de `depends`.

	`replaces` 

	Una lista de paquetes obsoletos que son remplazados por este paquete, por ejemplo: `replaces=('wireshark')` para el paquete [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk). Después de sincronizar con `pacman -Sy` inmediatamente remplazara un paquete instalado al encontrarse en los repositorios con otro paquete coincidente en la lista `replaces`. Si acaso provee un paquete alternativo de un paquete ya existente utilize la variable `conflicts` que solo es evaluada cuando se esta instalando el paquete conflictivo.

	`backup` 

	Una lista de paquetes que son respaldados como `file.pacsave` cuando el paquete es removido. Esto es comúnmente utilizado por paquetes que aplican archivos de configuración en `/etc`. La ruta de archivo de esta lista deberá ser relativa (ejemplo: `etc/pacman.conf`) y no rutas absolutas como (e.g. `/etc/pacman.conf`).

	`options` 

	Esta lista permite sobre escribir algunos de los comportamientos por default de `makepkg`.para establecer una opción se debe incluir el nombre de la opción en la lista. Para revertir a el comportamiento default se debe agregar un **!** al inicio de la opción. Las siguientes opciones pueden ser agregadas a la lista:

*   ***strip*** - Tira de los símbolos de binarios y bibliotecas.
*   ***docs*** - Salva los directorios `/doc`
*   ***libtool*** – Deja los archivos de libtool (`.la`) en los paquetes.
*   ***emptydirs*** - Abandona los directorios vacíos de los paquetes
*   ***zipman*** – Comprime las paginas *man* y *info*con *gzip*.
*   ***ccache*** - permite el uso de `ccache` durante la compilación. Es mas útil si no esta activada con algunos paquetes que tienen conflicto de construir con `!ccache` activo.
*   ***distcc*** - permite el uso de `distcc` durante la compilación. Es mas útil si no esta activada con algunos paquetes que tienen conflicto de construir con `distcc` activo.
*   ***makeflags*** - Permite el uso de `makeflags` especificadas por el usuario durante la compilación. Es mas útil si no esta activada con algunos paquetes que tienen conflicto de construir con `makeflags` activo.
*   ***force*** - Forza al paquete a ser actualizado con una operación de actualización de pacman, incluso si el numero de versión no indica una actualización de versión. Esto es útil cuando el el esquema de versiones ha cambiado (o es alfabético) o que un downgrade es requerido por razones de seguridad.

	`install` 

	El nombre del script de instalación que sera incluido en el paquete. Pacman tiene la habilidad de almacenar y ejecutar un script especifico del paquete cuando instala, remueve o actualiza un paquete. El script contiene las siguientes funciones que se ejecutan en diferentes tiempos:

*   ***pre_install*** - Este script es ejecutado antes de extraer los archivos de instalación. Un argumento es pasado: nueva versión del paquete.
*   ***post_install*** - El script es ejecutado después de que los archivos son extraídos. Un argumento es pasado: nueva versión del paquete.
*   ***pre_upgrade*** - Este script es ejecutado antes de extraer los archivos de instalación. Dos nuevos argumentos son pasados en el siguiente orden: nueva versión del paquete, vieja versión del paquete.
*   ***post_upgrade*** - El script es ejecutado después de que los archivos son extraídos. Dos nuevos argumentos son pasados en el siguiente orden: nueva versión del paquete, vieja versión del paquete.
*   ***pre_remove*** - El script es ejecutado antes de que los archivos sean removidos. Un argumento es pasado: vieja versión del paquete.
*   ***post_remove*** – El script es ejecutado después de remover paquetes. Un argumento es pasado: vieja versión del paquete.

**Tip:** un prototipo del archivo `.install` esta guardado en `/usr/share/pacman/proto.install`.

	`source` 

	Una lista de archivos que son necesitados para construir el paquete. Debe contener la locación del código fuente del software, que en muchos casos es una dirección HTTP, FTP o URL. Las variables de `pkgname` y `pkgver` pueden ser utilizadas aquí (ejemplo: `source=(http://example.com/$pkgname-$pkgver.tar.gz)`).

**Nota:** Si necesita archivos que no puedan ser descargados en el momento (ejemplo: parches y configuraciones especiales) simplemente ubique esos archivos en el mismo directorio del `PKGBUILD` y agregue el nombre del archivo a la lista. Cualquier ruta que se agregue aquí sera relativa a la ubicación del `PKGBUILD`. Antes de que la compilación comience, todos los archivos de esta lista serán descargados y verificados en su existencia y`makepkg` no procederá si hay archivos perdidos.

	`noextract` 

	Una lista de archivos dentro de la lista `source` que no deben ser extraídos ni descomprimidos de su formato actual por `makepkg`. Esto aplica para ciertos archivos comprimidos en formato zip que no pueden ser manejados por bsdtar. En este caso “unzip” debe ser incluido como dependencia en la lista de `makedepends` y la primer linea del archivo `build()` debe contener las lineas

```
cd $srcdir/$pkgname-$pkgver
unzip [source].zip

```

	`md5sums` 

	Una lista de checksums MD5 de los archivos listados en la lista `source`. Una vez que todos los archivos de la lista `source`son descargados o están disponibles, un hash MD5 de cada archivo sera generado automáticamente y comparado con los valores de esta lista en el mismo orden que aparecen en la lista `source`. Mientras el orden de los archivos fuente en si no importa, es importante que coincida con el orden de esta lista por que `makepkg` no puede adivinar a que checksum pertenece a que archivo. Puede generar esta lista fácil y rápido utilizando el comando `makepkg -g` en el directorio que contiene el `PKGBUILD`. Note que el algoritmo MD5 es conocido por tener debilidades, así que debe considerar en utilizar una alternativa mas fuerte.

	`sha1sums` 

	Una lista de checksums SHA-1 160-bit. Esta es una alternativa a md5sums antes descrito, pero también es conocido de tener debilidades, así que debe considerar el uso de alternativas mas fuertes. Para habilitar el uso y la creación de estos checksum, asegúrese de poner la opción `INTEGRITY_CHECK` en `/etc/makepkg.conf`. Para mas información vea `man makepkg.conf`.

	`sha256sums, sha384sums, sha512sums` 

	Una lista de checksums SHA-2 de diferentes tamaños, de 256, 384 y 512 respectivamente. Se cree que estas alternativas a md5sum son mas fuertes. Para habilitar el uso y la creación de estos checksum, asegúrese de poner la opción `INTEGRITY_CHECK` en `/etc/makepkg.conf`. Para mas información vea `man makepkg.conf`.

Es practica común mantener el orden de las variables en el `PKGBUILD` como se muestran arriba. Aun así, este orden no es mandatorio, y lo único obligatorio en este contexto es sintaxis correcta de [Bash](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash").
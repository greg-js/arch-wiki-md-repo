**Los PKGBUILDs no deben instalar aplicaciones que ya se encuentren en los repositorios oficiales bajo ninguna circunstancia. La única excepción a esta regla son paquetes que contengan añadidos extra habilitados y/o parches en comparación con los oficiales. En tal caso, la variable pkgname deberá ser diferente.**

Al crear paquetes para Arch Linux deberás **seguir las directivas** delineadas en este articulo, especialmente si deseas **contribuir** con tu paquete a la Distribución. También deberías leer los manuales de [PKGBUILD](https://www.archlinux.org/pacman/PKGBUILD.5.html) y [makepkg](https://www.archlinux.org/pacman/makepkg.8.html).

## Contents

*   [1 Prototipo de PKGBUILD](#Prototipo_de_PKGBUILD)
*   [2 Reglas de etiquetado](#Reglas_de_etiquetado)
*   [3 Nombramiento de paquetes](#Nombramiento_de_paquetes)
*   [4 Directorios](#Directorios)
*   [5 Tareas de Makepkg](#Tareas_de_Makepkg)
*   [6 Arquitecturas](#Arquitecturas)
*   [7 Licencias](#Licencias)
*   [8 Enviar paquetes a AUR](#Enviar_paquetes_a_AUR)
*   [9 Guías Adicionales](#Gu.C3.ADas_Adicionales)
    *   [9.1 Paquetes VCS (SVN, GIT, HG, etc)](#Paquetes_VCS_.28SVN.2C_GIT.2C_HG.2C_etc.29)
    *   [9.2 Paquetes de plugins de Eclipse](#Paquetes_de_plugins_de_Eclipse)
    *   [9.3 Paquetes de GNOME](#Paquetes_de_GNOME)
    *   [9.4 Paquetes Go](#Paquetes_Go)
    *   [9.5 Paquetes Haskell](#Paquetes_Haskell)
    *   [9.6 Paquetes Java](#Paquetes_Java)
    *   [9.7 Paquetes KDE](#Paquetes_KDE)
    *   [9.8 Paquetes de módulos del kernel](#Paquetes_de_m.C3.B3dulos_del_kernel)
    *   [9.9 Paquetes Lisp](#Paquetes_Lisp)
    *   [9.10 Paquetes OCaml](#Paquetes_OCaml)
    *   [9.11 Paquetes Perl](#Paquetes_Perl)
    *   [9.12 Paquetes Python](#Paquetes_Python)
    *   [9.13 Paquetes Ruby Gem](#Paquetes_Ruby_Gem)
    *   [9.14 Paquetes Wine](#Paquetes_Wine)
    *   [9.15 Paquetes MinGW](#Paquetes_MinGW)

## Prototipo de PKGBUILD

```
# Maintainer: Tu Nombre <tuemail@mail.com>
pkgname=NOMBREDELPAQUETE
pkgver=VERSIONDELPAQUETE
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
md5sums=() #generar con 'makepkg -g'

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

Puedes encontrar otros prototipos en `/usr/share/pacman` de los paquetes de pacman y abs.

## Reglas de etiquetado

*   Los paquetes **nunca** deben ser instalados en `/usr/local`

*   Siempre que sea posible utiliza `|| return 1` en funciones importantes para la construcción del paquete. Por ejemplo:

```
 patch -Np1 -i ../patchfile.patch || return 1
 make || return 1
 make DESTDIR=$startdir/pkg install || return 1

```

*   **No introduzcas nuevas variables** en tu script PKGBUILD, excepto cuando el paquete no puede ser construido sin ellas, debido a que pueden haber posibles confictos con las variables usadas por el propio {{Ic|makepkg}. Si una nueva variable es absolutamente requerida, **añade el prefijo "_" a su nombre**, por ejemplo:

 `"_tuvariable"` 

El sistema AUR no puede detectar el uso de variables no estándar, por ende no puede usarlas en sustituciones. Esto puede ser visto frecuentemente en la variable `source`, por ejemplo:

 `source=(http://downloads.sourceforge.net/directxwine/$patchname.$patchver.diff.bz2)` 

Esto evita el buen funcionamiento de AUR.

*   **Evita** usar `/usr/libexec`. Usa el directorio `/usr/lib/${pkgname}/` en su lugar.

*   El campo `packager` del meta-archivo del paquete puede ser **personalizado** por el creador del paquete modificando la opción apropiada en `/etc/makepkg.conf`, creando `~/.makepkg.conf,` o alternativamente exportando la variable de entorno `PACKAGER` antes de compilar el paquete con `makepkg`, por ejemplo:

```
 # export PACKAGER="Juan Perez@tu.email"

```

*   Todos los mensajes importantes deben ser mostrados con el comando `echo` durante la instalación mediante el uso del archivo `.install`. Por ejemplo, si un paquete necesita trabajo adicional de configuración, las instrucciones deberían ser incluidas.

*   Cualquier **dependencia opcional** que no es necesaria para ejecutar el paquete o para su funcionamiento general no debe ser incluida, en su lugar, la información deberá añadirse en la variable **optdepends**:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')
```

Este ejemplo se toma del paquete **wine** en el repositorio `extra`. La información en optdepends se muestra automáticamente en la instalación/actualización, de manera que no se debe añadir este tipo de información en el archivo .install

*   Al escribir la **descripción del paquete**, no incluyas el nombre del paquete en un formato auto-referencial. Por ejemplo "Nedit es un editor de texto para X11" debería ser simplificado a "Editor de texto para X11". Intenta mantener las descripciones en aproximadamente 80 caracteres o menos.

*   Intenta mantener el **ancho de linea** de tu PKGBUILD debajo de los 100 caracteres.

*   Cuando sea posible **elimina las líneas vacias** de tu `PKGBUILD` (`provides`, `replaces`, etc.)

*   Es una practica común el **preservar el orden** de los campos en el `PKGBUILD` como se muestra más abajo. Aunque no es obligatorio debido a que el único requerimiento para esto es mantener la **corrección de la sintaxis bash**.

## Nombramiento de paquetes

*   Los nombres de paquetes deben consistir **solamente de caracteres alfanuméricos**; todas las letras deberán ser minúsculas.

*   Las versiones de los paquetes **deben ser las mismas que las usadas por el autor' *original del software. Las versiones pueden incluir letras si es necesario (ejemplo, la versión de nmap es 2.54BETA32). Los nombres de versión* ¡'no deben incluir guiones!** solo letras, numeros y puntos.

*   Los números de liberación del paquete (ejemplo, el `-1` en nmap-2.54BETA32**-1**) son **especificos a Arch Linux**. Estos permiten a los usuarios diferenciar entre un paquete viejo y uno nuevo. Cuando una nueva versión *del paquete* es liberada el contador **se inicia en 1**. Cuando correcciones y optimizaciones son realizadas, el paquete es redistribuido con un incremento de 1 en su numero de liberación. Cuando una nueva versión de *la aplicación* es distribuida el contador se reinicia a 1\. Los números de liberación siguen las mismas directivas que los números de versión.

## Directorios

*   Archivos de configuración deben almacenarse en el directorio `/etc`. Si existe mas de un archivo de configuración es costumbre **utilizar un subdirectorio** para mantener `/etc` lo mas limpio posible. Usa`/etc/{pkgname}/` cuando sea posible, o una alternativa relacionada, por ejemplo, apache utiliza `/etc/httpd`.

*   Los archivos de cada paquete deben seguir las siguientes directivas:

| `/etc` | Archivos de configuración. |
| `/usr/bin` | Binarios de la aplicación. |
| `/usr/lib` | Librerias |
| `/usr/include` | Cabeceras (archivos .h) |
| `/usr/lib/{pkgname`} | Módulos, agregados (plugins), etc. |
| `/usr/man` | Paginas del manual. |
| `/usr/share/{pkgname`} | Datos de la aplicación (temas, iconos, etc.). |
| `/etc/{pkgname`} | Archivos de configuración adicionales de {pkgname}. |
| `/opt` | Paquetes grandes y autocontenidos como KDE, Mozilla, Qt, etc. |

*   Los paquetes **no** deben contener los siguientes directorios:
    *   /dev
    *   /home
    *   /media
    *   /mnt
    *   /proc
    *   /root
    *   /selinux
    *   /sys
    *   /tmp
    *   /var/tmp

## Tareas de Makepkg

Cuando usas [makepkg](https://www.archlinux.org/pacman/makepkg.8.html) para crear un paquete, hace automaticamente lo siguiente:

1.  Verifica que las **dependencias** esten instaladas
2.  **Descarga las fuentes** del fichero desde el servidor
3.  **Comprueba la integridad** de las fuentes
4.  **Desempaqueta** las fuentes
5.  **Parcha** todo lo necesario
6.  **Crea** el software e instala en un directorio root falso
7.  **Elimina** `/usr/doc`, `/usr/info`, `/usr/share/doc`, y `/usr/share/info` desde el paquete
8.  **Obtiene** simbolos desde los binarios
9.  **Obtiene** debugging symbols desde las librerias
10.  Genera el **package meta file** que es incluido en cada paquete
11.  **Comprime** el directorio root falso
12.  **Almacena** el paquete en el directorio de destino configurado (cwd por defecto)

## Arquitecturas

La variable `arch` debe contener `'i686'` o `'x86_64'` dependiendo de las arquitecturas en las que se pueda instalar. También puedes usar `any` para paquetes que no dependen de la arquitectura.

## Licencias

La variable [licence](https://wiki.archlinux.org/index.php/Licenses) está implementandose en los repositorios oficiales, y también **debes** usarla en tus paquetes. Úsala de la siguiente manera:

*   Un paquete de licencias se ha creado en [core] y almacena licencias comunes en `/usr/share/licenses/common`, por ejemplo: {{Ic|/usr/share/licenses/common/GPL}. Si un paquete está licenciado bajo una de esas licencias, la variable licenses se nombrará con el nombre del directorio. En el ejemplo anterior: {{Ic|license=('GPL')}

*   Si la licencia apropiada no se incluye en el paquete oficial de licencias, se pueden hacer vairas cosas

1.  El archivo de la licencia debe ser incluido en /usr/share/licenses/$pkgname/, por ejemplo: /usr/share/licenses/dibfoo/LICENSE. Una buena forma de hacerlo es usando: `install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"` 
2.  Si las fuentes NO contienen los detalles de la licencia, y la licencia solo se muestra por ejemplo en un sitio web, copia la licencia en un archivo e incluyelo. Recuerda también llamarla de forma apropiada.
3.  Pon 'custom' en la variable de las licencias. Opcionalmente, puedes sustituir 'custom' por 'custom:"Nombre de la licencia"'.

*   Una vez que las licencias se utilizan dos o más veces en un repositorio oficial, incluyendo [community], se convierte en común.
*   Las licencias MIT, BSD, zlib/libpng y Python son casos especiales y no se pueden incluir en el paquete de licencias 'comunes'. Por el bien de la variable {{Ic|license}, se sigue tratando como una licencia común: (license=('BSD'), license=('MIT'), license=('ZLIB') or license=('Python')) pero por el bien del sistema, es una licencia personal (custom), porque cada una tiene su propia línea de copyright. Cada paquete con licencia MIT, BSD, zlib/libpng o Python debe tener su licencia individualmente almacenada en `/usr/share/licenses/$pkgname/`.
*   La (L)GPL tiene varias versiones y permutaciones de esas versiones. Para el software (L)GPL, la convención es:
    *   (L)GPL - (L)GPLv2 o cualquier versión posterior.
    *   (L)GPL2 - (L)GPLv2 solo.
    *   (L)GPL3 - (L)GPLv3 o cualquier versión posterior.

## Enviar paquetes a AUR

Asegurate de esto antes de subir un paquete a AUR:

1.  Los PKGBUILDs enviados **NO DEBEN** instalar aplicaciones que ya se encuentren en alguno de los repositorios oficiales bajo ninguna circunstancia. La única excepción a esta estricta regla pueden ser únicamente paquetes con características extra y/o parches en comparación con los oficiales. En tal caso la variable pkgname deberá ser diferente para expresar esa diferencia. Por ejemplo: Un PKGBUILD de GNU screen enviado que contiene el parche para la barra lateral, puede ser llamado screen-sidebar, etc. Adicionalmente la variable **provides=('screen')** deberá ser utilizada para evitar conflictos con el paquete oficial.
2.  Para asegurar la seguridad de los paquetes enviados a AUR, por favor, **asegúrate** e que has rellenado correctamente el campo `md5sum`. Los `md5sum` pueden ser generados usando el comando `makepkg -g`.
3.  Por favor **añade un comentario** al principio del PKGBUILD con el siguiente formato. Recuerda disfrazar tu email para protejerlo del spam: `# Maintainer: Your Name <address at domain dot com>` 

    Si asumes el rol de mantener un PKGBUILD existente, añade tu nombre al principio como se ha descrito y cambia el título del/los Mantenedor/es previo/s a Contribuidor

    ```
    # Maintainer: Your Name <address at domain dot com>
    # Contributor: Previous Name <address at domain dot com>
    ```

4.  Verifica **las dependencias** del paquete (p.ej. utiliza ldd en ejecutables dinámicos, comprueba las herramientas requeridas por los scripts, etc.) El equipo de TUs recomienda **fervientemente** el uso de la utilidad `namcap`, escrita por [Jason Chu](https://www.archlinux.org/fellows/#jason), para analizar el saneamiento de los paquetes. `namcap` te avisará sobre permisos erróneos, dependencias que falten, dependencias innecesarias, y otros errores comunes. Puedes instalar el paquete `namcap` con pacman. Recuerda que `namcap` puede ser usado para comprobar los archivos pkg.tar.gz y PKGBUILDs
5.  **Las dependencias** son el error de empaquetamiento más común. Namcap puede ayudar a detectarlos pero no siempre acierta. Verifica las dependencias mirando la documentación de las fuentes y la página web del programa.
6.  No uses `**replaces**` en un PKGBUILD a no ser que el paquete vaya a ser renombrado, por ejemplo, cuando *Ethereal* se convirtió en *Wireshark*. Si el paquete es una versión alternativa de un paquete ya existente, usa `conflicts` (y `provides` si el paquete es requerido por otros). La principal deferencia es: tras sincronizar (-Sy) pacman inmediatamente quere sustituir un 'ofensivo' paquete instalado cuando encuentra un paquete que lo incluya en `replaces` en cualquiera de sus repositorios; `conflicts` por otro lado solo es evaluado cuando realmente instalas el paquete, que normalmente es el comportamiento deseado porque es menos invasivo.
7.  Todos los archivos subidos a AUR deben estar contenidos en un archivo **tar comprimido que contenga un directorio con el** `PKGBUILD` **y** archivos de instalación adicionales **(parches, install, etc.) en el**.
    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    El nombre del archivo debe contener el nombre del paquete, por ej. foo.tar.gz.

    Cualquiera puede hacer un paquete tar que contenga los archivos requeridos utilizando `makepkg --source`. Esto creará un paquete tar llamado `$pkgname-$pkgver-$pkgrel.src.tar.gz`, que puede ser subido a AUR.

    El paquete tar **no debe** contener el paquete tar binario creado por makepkg, ni debe contener la lista de archivos

## Guías Adicionales

Asegúrate de leer antes esta guía - hay puntos importantes listados en esta página que no se van a repetir en las siguientes páginas de guías. Las guías específicas se han creado como un añadido a los estándars listados en esta página.

### Paquetes VCS (SVN, GIT, HG, etc)

Por favor mira la [Guía Arch de PKGBUILDs VCS](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")

### Paquetes de plugins de Eclipse

Por favor mira la [Guía de empaquetamiento de plugins de Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines")

### Paquetes de GNOME

Por favor mira la [Guía de empaquetamiento GNOME](/index.php/GNOME_Package_Guidelines "GNOME Package Guidelines")

### Paquetes Go

Por favor mira la [Guía para paquetes Go](/index.php/Go_Package_Guidelines "Go Package Guidelines")

### Paquetes Haskell

Por favor mira la [Guía de empaquetamiento Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines")

### Paquetes Java

Por favor mira la [Guía de empaquetamiento Java](/index.php/Java_Package_Guidelines "Java Package Guidelines")

### Paquetes KDE

Por favor mira la [Guía de empaquetamiento KDE](/index.php/KDE_Package_Guidelines "KDE Package Guidelines")

### Paquetes de módulos del kernel

Por favor mira la [Guía de empaquetamiento de Módulos del Kernel](/index.php/Kernel_Module_Package_Guidelines "Kernel Module Package Guidelines")

### Paquetes Lisp

Por favor mira la [Guía de empaquetamiento Llisp](/index.php/Lisp_Package_Guidelines "Lisp Package Guidelines")

### Paquetes OCaml

Por favor mira la [Guía de empaquetamiento OCaml](/index.php/OCaml_Package_Guidelines "OCaml Package Guidelines")

### Paquetes Perl

Por favor mira la [Guía de empaquetamiento Perl](/index.php/Perl_Package_Guidelines "Perl Package Guidelines")

### Paquetes Python

Por favor mira la [Guía de empaquetamiento Python](/index.php/Python_Package_Guidelines "Python Package Guidelines")

### Paquetes Ruby Gem

Por favor mira la [Guía de empaquetamiento Ruby](/index.php/Ruby_Gem_Package_Guidelines "Ruby Gem Package Guidelines")

### Paquetes Wine

Por favor mira la [Guía de empaquetamiento Wine](/index.php/Arch_wine_PKGBUILD_guidelines "Arch wine PKGBUILD guidelines")

### Paquetes MinGW

Por favor mira la [Guía de empaquetamiento MinGW](/index.php/MinGW_PKGBUILD_guidelines "MinGW PKGBUILD guidelines")

[Jorge Barroso](/index.php?title=User:Jogre_barroso&action=edit&redlink=1 "User:Jogre barroso (page does not exist)")

[talk](/index.php?title=User_talk:Jogre_barroso&action=edit&redlink=1 "User talk:Jogre barroso (page does not exist)")
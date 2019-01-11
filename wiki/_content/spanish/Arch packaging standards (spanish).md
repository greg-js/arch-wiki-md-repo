**Estado de la traducción**
Este artículo es una traducción de [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards"), revisada por última vez el **2018-10-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_packaging_standards&diff=0&oldid=507402) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

Al crear paquetes para Arch Linux deberá **adherirse a las pautas para los paquetes** de abajo, especialmente si desea **contribuir** con un nuevo paquete a Arch Linux. También debería leer los manuales de [PKGBUILD](https://www.archlinux.org/pacman/PKGBUILD.5.html) y [makepkg](https://www.archlinux.org/pacman/makepkg.8.html).

## Contents

*   [1 Prototipo de PKGBUILD](#Prototipo_de_PKGBUILD)
*   [2 Reglas de etiquetado de paquetes](#Reglas_de_etiquetado_de_paquetes)
*   [3 Nominación de paquetes](#Nominación_de_paquetes)
*   [4 Directorios](#Directorios)
*   [5 Deberes de makepkg](#Deberes_de_makepkg)
*   [6 Arquitecturas](#Arquitecturas)
*   [7 Licencias](#Licencias)
*   [8 Guías adicionales](#Guías_adicionales)

## Prototipo de PKGBUILD

```
# Maintainer: su nombre <su-email@mail.com>
pkgname=NOMBRE_DEL_PAQUETE
pkgver=VERSIÓN_DEL_PAQUETE
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

Puede encontrar otros prototipos en `/usr/share/pacman` para los paquetes de pacman y abs.

## Reglas de etiquetado de paquetes

*   Los paquetes **nunca** deben ser instalados en `/usr/local`
*   **No introduzca nuevas variables o funciones** en el script `PKGBUILD`, excepto cuando el paquete no puede ser compilado sin ellas, debido a que puede haber posibles **confictos** con las variables usadas por el propio makepkg.
*   Si una nueva variable o función es absolutamente requerida, **añádale a su nombre un guión bajo de prefijo** (`_`), por ejemplo `variable-personal=` 
*   **Evite** utilizar `/usr/libexec/`. Utilice `/usr/lib/$pkgname/` en su lugar.
*   El campo `packager` del metaarchivo del paquete puede ser **personalizado** por el creador del paquete modificando la opción apropiada en el archivo `/etc/makepkg.conf`, o alternativamente sobrescribiendo al crear `~/.makepkg.conf`.
*   Todos los mensajes importantes deben ser mostrados con la orden `echo` durante la instalación mediante el uso del archivo `.install`. Por ejemplo, si un paquete necesita trabajo adicional de configuración, las instrucciones deberían ser incluidas.
*   Las **dependencias** son el error de empaquetado más común. Tómese un tiempo para verificarlas cuidadosamente, por ejemplo ejecutando `ldd` en ejecutables dinámicos, verificando las herramientas requeridas por los scripts o mirando la documentación del software. La utilidad [namcap](/index.php/Namcap "Namcap") puede ayudarle en este sentido. Esta herramienta puede analizar tanto los PKGBUILD como el paquete resultante y le advertirá sobre permisos incorrectos, las dependencias que faltan, las dependencias redundantes y otros errores comunes.
*   Cualquier **dependencia opcional** que no sea necesaria para ejecutar el paquete o para su funcionamiento general, no debe ser incluida, en su lugar, la información deberá añadirse en la matriz **optdepends**:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

	Este ejemplo toma del paquete **wine** presente en el repositorio `extra`. La información en optdepends se muestra automáticamente en la instalación/actualización, de manera que **no** se debe añadir este tipo de información en el archivo `.install`

*   Al escribir la **descripción del paquete**, no incluya el nombre del paquete en un formato autorreferencial. Por ejemplo «Nedit es un editor de texto para X11» debería ser simplificado a «Editor de texto para X11». Intente mantener las descripciones dentro de aproximadamente 80 caracteres o menos.
*   Intente mantener el **ancho de linea** del PKGBUILD por debajo de los 100 caracteres.
*   Cuando sea posible **elimine las líneas vacías** de `PKGBUILD` (`provides`, `replaces`, etc.)
*   Es una practica común el **preservar el orden** de los campos en el `PKGBUILD` como se muestra más abajo. Aunque no es obligatorio debido a que el único requerimiento para esto es mantener la **corrección de la sintaxis de bash**.
*   **Entrecomille** variables que pueden contener espacios, como `"$pkgdir"` y `"$srcdir"`.
*   Para garantizar la **integridad** de los paquetes, asegúrese de que las [variables de integridad](/index.php/PKGBUILD#Integrity "PKGBUILD") contengan los valores correctos. Estas se pueden actualizar utilizando la herramienta `updpkgsums`.

## Nominación de paquetes

*   Los nombres de paquetes deben contener solamente caracteres alfanuméricos, incluido los siguientes `@`, `.`, `_`, `+`, `-`. No se permite que los nombres comiencen con guiones o puntos. Todas las letras deben estar en minúsculas.
*   Los nombres de los paquetes NO deben tener el sufijo del número de versión de lanzamiento principal en sentido ascendente (por ejemplo, no usaremos libfoo2 si el flujo ascendente lo llama libfoo v2.3.4) en caso de que la biblioteca y sus dependencias que se esperan puedan seguir usando la versión de la biblioteca más reciente con su respectivo lanzamiento en sentido ascendente. Sin embargo, para algunos programas o dependencias, esto no puede ser asumido. En el pasado, esto ha sido especialmente cierto para los conjuntos de herramientas de *widgets* como GTK y Qt. El software que depende de dichos conjuntos de herramientas generalmente no puede ser portado si más a una nueva versión principal. Como tal, en los casos en que el software no puede seguir funcionando sin más junto con sus dependencias, los nombres de los paquetes deben incluir el sufijo de la versión principal (por ejemplo, gtk2, gtk3, qt4, qt5). Para los casos en los que la mayoría de las dependencias pueden continuar con la versión más reciente, pero algunas no pueden (por ejemplo, el código privativo que necesita libpng12 o similar), una versión obsoleta de ese paquete podría llamarse libfoo1, mientras que la versión actual sería solo libfoo.
*   Las versiones de los paquetes **deben ser las mismas que las usadas por el autor** original del software. Las versiones pueden incluir letras si es necesario (por ejemplo, la versión de nmap es 2.54BETA32). Las etiquetas de la versión no deben incluir guiones, solo letras, numeros y puntos.
*   Las liberacones de paquetes son **especificos para Arch Linux**. Estos permiten a los usuarios diferenciar entre un paquete viejo y uno nuevo. Cuando una nueva versión del paquete es liberada el contador **se pone en 1**. Cuando se realizan correcciones y optimizaciones, el paquete es redistribuido **incremento en 1 su numero de liberación**. Cuando sale una nueva versión, el recuento de lanzamientos se restablece en 1\. Las etiquetas de liberación de paquetes siguen las **mismas restricciones de denominación que las etiquetas de versión**.

## Directorios

*   Los **archivos de configuración** deben localizarse en el directorio `/etc`. Si existe mas de un archivo de configuración es costumbre **utilizar un subdirectorio** para mantener `/etc` lo mas limpio posible. Utilice `/etc/{pkgname}/` donde `{pkgname}` es el nombre del paquete (o un lugar alternativo, por ejemplo, apache utiliza `/etc/httpd/`).

*   Los archivos de cada paquete deben seguir estas '*directrices generales de directorios*:

| `/etc` | Archivos de configuración **esenciales del sistema** |
| `/usr/bin` | Binarios de aplicaciones |
| `/usr/lib` | Bibliotecas |
| `/usr/include` | Cabeceras de archivos |
| `/usr/lib/{pkg}` | Módulos, complementos, etc. |
| `/usr/share/doc/{pkg}` | Application documentation |
| `/usr/share/info` | Archivos info del sistema GNU |
| `/usr/share/man` | Páginas de manuales |
| `/usr/share/{pkg}` | Datos de aplicaciones |
| `/var/lib/{pkg}` | Almacén persistente de aplicaciones |
| `/etc/{pkg}` | Archivos de configuración para `{pkg}` |
| `/opt/{pkg}` | Paquetes grandes y autocontenidos |

*   Los paquetes no deben contener ninguno de los siguientes directorios:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## Deberes de makepkg

Cuando se utiliza [makepkg](/index.php/Makepkg "Makepkg") para compilar un paquete, este hace lo siguiente automáticamente:

1.  Comprueba si el paquete tiene **dependencias** y **makedepends** instaladas.
2.  **Descarga las fuentes** desde los servidores.
3.  **Comprueba la integridad** de los archivos fuentes.
4.  **Desempaca** los archivos fuentes.
5.  Realiza cualquier **parche** necesario.
6.  **Compila** el software y lo instala en una raíz falsa.
7.  **Quita** los símbolos de los binarios.
8.  **Quita** y depuralos símbolos de las bibliotecas.
9.  **Comprime** las páginas de manual y/o información.
10.  Genera el **archivo meta del paquete** que se incluye con cada paquete.
11.  **Comprime** la raíz falsa en el archivo del paquete.
12.  **Almacena** el archivo del paquete en el directorio de destino configurado (cwd por defecto).

## Arquitecturas

La variable `arch` debe contener `'x86_64'` si el paquete compilado es específico de dicha arquitectura. Utilice `'any'` para paquetes que no dependen de la arquitectura.

## Licencias

Consulte [PKGBUILD#license](/index.php/PKGBUILD#license "PKGBUILD").

## Guías adicionales

Asegúrate de leer antes esta guía. Hay puntos importantes listados en esta página que no se van a repetir en las siguientes páginas de guías. Las guías específicas se han creado como un añadido a los estándares listados en esta página.

**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Los paquetes enviados a AUR deben además cumplir con [Arch User Repository (Español)#Reglas de envío](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#Reglas_de_envío "Arch User Repository (Español)").
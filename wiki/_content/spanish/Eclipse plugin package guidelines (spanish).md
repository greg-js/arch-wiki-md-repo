**Estado de la traducción**
Este artículo es una traducción de [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines"), revisada por última vez el **2018-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Eclipse_plugin_package_guidelines&diff=0&oldid=545792) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Hay muchas formas de instalar complementos de trabajo [Eclipse (Español)](/index.php/Eclipse_(Espa%C3%B1ol) "Eclipse (Español)"), especialmente desde la introducción del directorio *dropins* en Eclipse 3.4, pero algunos de ellos son desordenados, y tener una forma de empaquetado estandarizada y consistente es muy importante para llevar a una estructura de sistema limpia. Sin embargo, no es fácil lograr esto sin que el empaquetador sepa cada detalle sobre cómo funcionan los complementos de Eclipse. Esta página tiene como objetivo definir una estructura estándar y simple para el complemento Eclipse [PKGBUILDs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"), de modo que la estructura del sistema de archivos pueda permanecer consistente entre todos los complementos sin tener que empacar nuevamente el paquete para cada nuevo paquete.

## Contents

*   [1 Estructura e instalación de complementos de eclipse](#Estructura_e_instalación_de_complementos_de_eclipse)
*   [2 Empaquetado](#Empaquetado)
    *   [2.1 Muestra de PKGBUILD](#Muestra_de_PKGBUILD)
    *   [2.2 Cómo personalizar la construcción](#Cómo_personalizar_la_construcción)
    *   [2.3 Revisión en profundidad de PKGBUILD](#Revisión_en_profundidad_de_PKGBUILD)
        *   [2.3.1 Nombre del paquete](#Nombre_del_paquete)
        *   [2.3.2 Archivos](#Archivos)
            *   [2.3.2.1 Extracción](#Extracción)
            *   [2.3.2.2 Ubicaciones](#Ubicaciones)
        *   [2.3.3 La funsión build()](#La_funsión_build())
*   [3 Solución de problemas](#Solución_de_problemas)

## Estructura e instalación de complementos de eclipse

El complemento típico de Eclipse contiene dos directorios, `características` y `complementos`, y desde Eclipse 3.3 solo se pueden colocar en `/usr/lib/eclipse/`. El contenido de estos dos directorios podría mezclarse con el de otros complementos, lo que creó un desorden y dificultó la administración de la estructura. También fue muy difícil saber de un vistazo qué paquete contenía qué archivo.

Este método de instalación aún es compatible con Eclipse 3.4, pero el preferido ahora es usando el directorio`/usr/lib/eclipse/dropins/`. Dentro de este directorio pueden haber un número ilimitado de subdirectorios, cada uno con sus propias `características` y `complementos`. Esto permite mantener una estructura ordenada y limpia, y debe ser el método de empaquetado estándar.

## Empaquetado

### Muestra de PKGBUILD

Aquí hay un ejemplo, detallaremos cómo personalizarlo a continuación.

 `PKGBUILD-eclipse.proto` 
```
pkgname=eclipse-mylyn
pkgver=3.0.3
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('any')
url="https://eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(https://download.eclipse.org/tools/mylyn/update/mylyn-${pkgver}-e3.4.zip)
sha512sums=('aa6289046df4c254567010b30706cc9cb0a1355e9634adcb2052127030d2640f399caf20fce10e8b4fab5885da29057ab9117af42472bcc1645dcf9881f84236')

prepare() {
  # remove features and plug-ins containing sources
  rm -f features/*.source_*
  rm -f plugins/*.source_*
  # remove gz files
  rm -f plugins/*.pack.gz
}

package() {
  _dest="${pkgdir}/usr/lib/eclipse/dropins/${pkgname/eclipse-}/eclipse"

  # Features
  find features -type f | while read -r _feature ; do
    if [[ "${_feature}" =~ (.*\.jar$) ]] ; then
      install -dm755 "${_dest}/${_feature%*.jar}"
      cd "${_dest}/${_feature/.jar}"
      # extract features (otherwise they are not visible in about dialog)
      jar xf "${srcdir}/${_feature}" || return 1
    else
      install -Dm644 "${_feature}" "${_dest}/${_feature}"
    fi
  done

  # Plugins
  find plugins -type f | while read -r _plugin ; do
    install -Dm644 "${_plugin}" "${_dest}/${_plugin}"
  done
}

```

### Cómo personalizar la construcción

La principal variable que necesita ser personalizada es la `pkgname`. Si está empaquetando un complemento típico, entonces esto es lo único que debe hacer: la mayoría de los complementos se distribuyen en archivos zip que solo contienen dos subdirectorios `features` y `plugins`. Entonces, si está empaquetando el complemento `foo` y el archivo de origen solo contiene `features` y `plugins`, solo necesita cambiar `pkgname` a `eclipse-foo` y ya está configurado.

Siga leyendo para acceder a las partes internas de PKGBUILD, que ayudan a entender cómo configurar la compilación para todos los demás casos.

### Revisión en profundidad de PKGBUILD

#### Nombre del paquete

Los paquetes deben llamarse `eclipse-*pluginname*`, para que sean reconocibles como paquetes relacionados con Eclipse y sea fácil extraer el nombre del complemento con una simple sustitución de intérprete de órdenes como `${pkgname/eclipse-}`, sin tener que recurrir a una variable `${_realname}` innecesaria. El nombre del complemento es necesario para ordenar todo durante la instalación y evitar conflictos.

#### Archivos

##### Extracción

Algunos complementos necesitan las características para ser extraídos de los archivos jar. La utilidad `jar`, ya incluida en el JRE, se usa para hacer esto. Sin embargo, `jar` no puede extraer directorios que no sean el actual: esto significa que, después de cada creación de directorio, es necesario `cd` dentro de él antes de extraer. La variable `${_dest}` se utiliza en este contexto para mejorar la legibilidad y el orden de PKGBUILD.

##### Ubicaciones

Como dijimos, los archivos de origen proporcionan dos directorios, `características` y `complementos`, cada uno empaquetado con archivos jar. La estructura de dropins preferida debe verse así:

```
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature1/...
/usr/lib/eclipse/dropins/pluginname/eclipse/features/feature2/...
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

Esta estructura permite mezclar diferentes versiones de bibliotecas que pueden ser necesarias por diferentes complementos y tener claro qué paquete posee qué. También evitará conflictos en caso de que diferentes paquetes proporcionen la misma biblioteca. La única alternativa sería dividir cada paquete de sus bibliotecas, con todo el alboroto adicional que requiere, y ni siquiera se garantizaría que funcione debido a los paquetes que necesitan versiones anteriores de la biblioteca. Las características deben estar desactivadas ya que Eclipse no las detectará de otra manera, y la instalación completa del complemento no funcionará. Esto sucede porque Eclipse trata los sitios de actualización y las instalaciones locales de manera diferente (no pregunte por qué, simplemente lo hace).

#### La funsión build()

Lo primero que debe notarse es la orden `cd ${srcdir}`. Por lo general, los archivos de origen extraen las carpetas `features` y `plugins` directamente en `${srcdir}`, pero no siempre es así. De todos modos, para la mayoría de los complementos que no son *(de facto)*, ésta es la única línea que se debe cambiar. Algunas características lanzadas incluyen sus fuentes, también. Para una versión de lanzamiento normal, estas fuentes no son necesarias y se pueden eliminar. Además, las mismas características incluyen archivos `*.pack.gz`, que contienen los mismos archivos en comparación con los archivos jar. Así que estos archivos pueden ser eliminados, también.

La siguiente es la sección `features`. Crea los directorios necesarios, uno para cada archivo jar, y extrae el jar en el directorio correspondiente. De manera similar, la sección `plugins` instala los archivos jar en su directorio. Se utiliza un ciclo while para evitar archivos con nombres divertidos.

## Solución de problemas

*   Algunas veces la limpieza de Eclipse ayuda a reparar algunos problemas: `$ eclipse -clean` 
*   Si los nuevos complementos instalados no aparecen en Eclipse, intente con un directorio limpio `~/.eclipse`, por ejemplo, cambiando el nombre del existente. Tenga en cuenta que esto, por supuesto, hará que todos los complementos instalados por el usuario a través de Marketplace no estén disponibles.
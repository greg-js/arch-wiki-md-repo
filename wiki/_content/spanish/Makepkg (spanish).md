**Estado de la traducción**
Este artículo es una traducción de [makepkg](/index.php/Makepkg "Makepkg"), revisada por última vez el **2019-2-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Makepkg&diff=0&oldid=566504) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Crear paquetes](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")
*   [Pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")

makepkg es usado para compilar y construir paquetes capaces de instalar mediante [pacman](/index.php/Pacman "Pacman"), el manejador de paquetes de Arch Linux. makepkg es un script que automatiza el proceso de construcción de paquetes; este puede descargar y validar archivos fuente, resolver dependencias, configurar los parámetros de tiempo de compilación, compilar las fuentes e instalarlo dentro de un root temporal.

makepkg lo provee el paquete [pacman](https://www.archlinux.org/packages/?name=pacman).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuración](#Configuración)
    *   [1.1 Información del empaquetador](#Información_del_empaquetador)
    *   [1.2 Resultado del paquete](#Resultado_del_paquete)
    *   [1.3 Verificación de firmas](#Verificación_de_firmas)
    *   [1.4 fakeroot](#fakeroot)
*   [2 Utilización](#Utilización)
*   [3 Recomendaciones](#Recomendaciones)
    *   [3.1 Construir binarios optimizados](#Construir_binarios_optimizados)
    *   [3.2 Mejorar tiempos de compilación](#Mejorar_tiempos_de_compilación)
        *   [3.2.1 Compilación paralela](#Compilación_paralela)
        *   [3.2.2 Construir desde archivos en memoria](#Construir_desde_archivos_en_memoria)
        *   [3.2.3 Usar caché de compilación](#Usar_caché_de_compilación)
    *   [3.3 Generar nueva suma de verificación](#Generar_nueva_suma_de_verificación)
    *   [3.4 Usar otros algoritmos de compresión](#Usar_otros_algoritmos_de_compresión)
    *   [3.5 Uso de múltiples núcleos en la compresión](#Uso_de_múltiples_núcleos_en_la_compresión)
    *   [3.6 Ver paquetes con un empaquetador específico](#Ver_paquetes_con_un_empaquetador_específico)
    *   [3.7 Construir paquetes de 32-bit en un sistema de 64-bit](#Construir_paquetes_de_32-bit_en_un_sistema_de_64-bit)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 A veces makepkg falla al firmar un paquete sin preguntar la frase de firma](#A_veces_makepkg_falla_al_firmar_un_paquete_sin_preguntar_la_frase_de_firma)
    *   [4.2 CFLAGS/CXXFLAGS/LDFLAGS en makepkg.conf no funcionan en los paquetes basados en CMake](#CFLAGS/CXXFLAGS/LDFLAGS_en_makepkg.conf_no_funcionan_en_los_paquetes_basados_en_CMake)
    *   [4.3 CFLAGS/CXXFLAGS/LDFLAGS en makepkg.conf no funcionan en los paquetes basados en QMAKE](#CFLAGS/CXXFLAGS/LDFLAGS_en_makepkg.conf_no_funcionan_en_los_paquetes_basados_en_QMAKE)
    *   [4.4 Especificar el directorio de instalación para los paquetes basados en QMAKE](#Especificar_el_directorio_de_instalación_para_los_paquetes_basados_en_QMAKE)
    *   [4.5 ADVERTENCIA: Paquetes que contienen referencias a $srcdir](#ADVERTENCIA:_Paquetes_que_contienen_referencias_a_$srcdir)
    *   [4.6 Makepkg falla al descargar las dependencias a través de un proxy](#Makepkg_falla_al_descargar_las_dependencias_a_través_de_un_proxy)
        *   [4.6.1 Habilitar proxy estableciendo su URL en XferCommand](#Habilitar_proxy_estableciendo_su_URL_en_XferCommand)
        *   [4.6.2 Habilitar proxy via sudoer's env_keep](#Habilitar_proxy_via_sudoer's_env_keep)
    *   [4.7 Makepkg falla, pero el make termina bien](#Makepkg_falla,_pero_el_make_termina_bien)
*   [5 Véase también](#Véase_también)

## Configuración

El archivo principal de configuración de makepkg es `/etc/makepkg.conf` . la mayoría de los usuarios querrán configurar estas opciones de makepkg antes de construir cualquier paquete (por ejemplo modificar las variables `MAKEFLAGS` en sistemas con soporte SMP para [reducir tiempos de compilación](#Recomendaciones) , o personalizar la variable `PACKAGER` para personalizar paquetes. Lea la documentación de `PACKAGER` para más detalles

Para poder instalar paquetes con makepkg sin ser usuario administrador (con `makepkg -s`, información más delante), instale [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") y agregue los usuarios con estos privilegios en el archivo to `/etc/sudoers`:

```
USER_NAME    ALL=(ALL)    NOPASSWD: /usr/bin/pacman

```

La línea de arriba eliminara la necesidad de introducir un password cada vez que utilicemos pacman. Revise la wiki de [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") para mas información

Enseguida, puede configurar donde serán guardados los paquetes terminados. Este paso es meramente opcional; por definición los paquetes serán creados en el directorio donde makepkg se ejecute Cree el directorio:

```
$ mkdir /home/$USER/packages

```

Luego modifique la variable `PKGDEST` en el archivo `/etc/makepkg.conf` de acuerdo a esta directorio.

### Información del empaquetador

Cada paquete es etiquetado con meta información que identifica entre otros el *packager*. Por defecto, paquetes compilados por el usuario son marcados con `Unknown Packager`. Si múltiples usuarios van a compilar paquetes en un sistema o si planea distribuir sus paquetes con otros usuarios, es conveniente proveer un contacto real. Esto se puede hacer modificando la variable `PACKAGER` en el archivo `makepkg.conf`.

Para revisar esta variable en un paquete instalado ejecute:

 `$ pacman -Qi *paquete*` 
```
...
Packager       : John Doe <john@doe.com>
...

```

Para firmar sus paquete automaticamente, tambien modifique la variable `GPGKEY` en el archivo `makepkg.conf`.

### Resultado del paquete

Por defecto, *makepkg* crea tarballs de los paquetes en el directorio de trabajo y descarga las fuentes en el directorio `src/`. Rutas personalizadas pueden ser configuradas, por ejemplo para mantener todos los paquetes construidos en `~/build/packages/` y todas las fuentes en `~/build/sources/`.

Configure las siguientes variables en `makepkg.conf`, si lo considera necesario:

*   `PKGDEST` — directorio para guardar los paquetes resultantes
*   `SRCDEST` — directorio para guardar datos [fuente](/index.php/PKGBUILD_(Espa%C3%B1ol)#Variables "PKGBUILD (Español)"), (links simbólicos seran puestos en `src/` si la ruta es diferente)
*   `SRCPKGDEST` — directorio para guardar las fuentes resultantes (construido con `makepkg -S`)

### Verificación de firmas

**Nota:** La implementación de verificación de firmas en *makepkg* no usa el llavero de pacman, en su lugar depende en el llavero del usuario. [[1]](http://allanmcrae.com/2015/01/two-pgp-keyrings-for-package-management-in-arch-linux/)

Si una firma de la forma `.sig` o `.asc` es parte del [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") en la sección *source*, *makepkg* automáticamente intentara [verificarla](/index.php/GnuPG#Verify_a_signature "GnuPG"). En caso de que el llavero del usuario no contenga la clave pública para la verificación *makepkg* abortara el procedimiento con un mensaje que la clave PGP no pudo ser verificada.

Si una clave pública es necesaria, el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") probablemente tendrá una sección [validpgpkeys](/index.php/PKGBUILD#validpgpkeys "PKGBUILD") con las IDs requeridas. Se puede [importar](/index.php/GnuPG_(Espa%C3%B1ol)#Importar_una_clave "GnuPG (Español)") manualmente, o la puede ubicar en un [keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG") e importarla desde allí.

### `fakeroot`

`fakeroot` permite al usuario usar los permisos necesarios de root para crear paquetes en el ambiente de construcción sin necesidad de alterar todo el sistema. Si el proceso de construcción trata de alterar archivos fuera del ambiente de construcción entonces aparecerán mensajes de error y el empaquetado habrá fallado – esto es muy útil para verificar la calidad, seguridad e integridad de los PKGBUILD para su distribución. Por default `fakeroot` esta habilitado en el archivo de configuración `/etc/makepkg.conf`; los usuarios pueden utilizar el prefijo `!` en la variable `BUILDENV` para deshabilitar esto.

## Utilización

Antes de continuar, asegúrese de que el grupo de paquetes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) este [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)"). Los paquetes pertenecientes a este grupo no son requeridos en la lista de dependencias en los [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

Recuerde que se da por entendido que el grupo [base](https://www.archlinux.org/groups/x86_64/base/) esta instalado por defecto en **todos** los sistemas Arch Linux. El paquete [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) se da por entendió que también esta instalado cuando se crean paquetes con *makepkg*.

**Nota:**

*   Asegurese de haber configurado [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") correctamente al pasar comandos a [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").
*   Ejecutar *makepkg* como root no esta [permitido](https://lists.archlinux.org/pipermail/pacman-dev/2014-March/018911.html). Debido a que un `PKGBUILD` puede incluir comandos arbitrarios, construir como root se considera peligroso.

Para crear un paquete primero debe tener un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), como se describe en la guía de in [Creating packages](/index.php/Creating_packages "Creating packages"), o obtenga uno del [ABS tree](/index.php/Arch_Build_System "Arch Build System"), [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), u obténgalo de alguna otra fuente.

**Advertencia:** solo instale paquetes de fuentes confiables.

Una vez en posesión de un `PKGBUILD`, entre al directorio donde esta salvado este archivo y ejecute el siguiente comando para compilar y construir el paquete como lo fue descrito en el archivo un `PKGBUILD`:

```
$ makepkg

```

Si no se satisfacen algunas dependencias, *makepkg* mostrara una advertencia antes de fallar, para construir el paquete e instalar sus dependencias automáticamente, simplemente se utiliza el comando:

```
$ makepkg -s

```

**Nota:**

*   Estas dependencias deben estar disponibles dentro de los repositorios disponibles para pacman, vea [pacman (Español)#Repositorios y servidores de réplicas](/index.php/Pacman_(Espa%C3%B1ol)#Repositorios_y_servidores_de_réplicas "Pacman (Español)") para mayor información al respecto. También se pueden instalar las dependencias antes de construir el paquete (`pacman -S --asdeps dep1 dep2`).
*   Solo se utilizarán valores globales cuando se instalen las dependencias, por ejemplo, cualquier anulación hecha en la función de paquete dividido no sera usado. [[2]](https://patchwork.archlinux.org/patch/2271/)

Una vez que se hayan satisfecho todas las dependencias y el paquete se construyo satisfactoriamente, un archivo con el nombre (`pkgname-pkgver.pkg.tar.gz`) será creado en el directorio de trabajo. Para instalarlo (al igual que `pacman -U pkgname-pkgver.pkg.tar.gz`) simplemente se ejecuta:

```
$ makepkg -i

```

Para despejar archivos que no son necesarios, como los existentes en `$srcdir`, agregue la opción `-c`. Este comando es útil al actualizar la version de los paquetes usando el mismo directorio. Se previene la transferencia de archivos obsoletos en la nueva construcción.

```
$ makepkg -c

```

Para mas información, mire [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html).

## Recomendaciones

### Construir binarios optimizados

Una mejora de rendimiento del empaquetado de software se puede lograr habilitando optimizaciones en la máquina local. El inconveniente es que los binarios compilados para una arquitectura de procesador específico pueden no ejecutarse correctamente en otros ordenadores. En las máquinas x86_64 es raro ganar un rendimiento significativo que justifique invertir tiempo en reconstruir los paquetes oficiales.

Sin embargo es muy fácil disminuir el rendimiento utilizando FLAGS de compilación "no estandar". Muchas optimizaciones son útiles solo en determinadas situaciones y no debe de aplicarse para todos los paquetes. A no haya ser que puedas verificar que algo es más rápido, es una muy buena oportunidad ¡como no! Los artículos de Gentoo [Guía de optimización de compilación](https://wiki.gentoo.org/wiki/GCC_optimization/es) y [CFLAGS Seguros (en ingles)](http://wiki.gentoo.org/wiki/Safe_CFLAGS) proporciona mas información detallada sobre optimizaciones de compilador.

Las opciones pasadas al compilador C/C++ (e.g. [gcc](https://www.archlinux.org/packages/?name=gcc) o [clang](https://www.archlinux.org/packages/?name=clang)) están controladas por `CFLAGS`, `CXXFLAGS` y `CPPFLAGS` variables de entorno. Para usarlos en el sistema de construcción de Arch, *makepkg* muestra las variables de entorno según las opciones de configuración en `makepkg.conf`. Los valores por defecto están configurados para producir binarios genéricos que pueden ser instalados en un amplio rango de máquinas.

**Nota:**

*   Tener en cuenta que no todos los sistemas de construcciones utilizan las variables configuradas en `makepkg.conf`. Por ejemplo, *cmake* no tiene en cuenta las opciones de preprocesamiento `CPPFLAGS`. Consecuentemente, muchos [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") contiene métodos alternativos con opciones específicas para el sistema constructor usado por el gestor de paquetes.
*   La configuración proporcionada con el código fuente en el `Makefile` o algún argumento específico en la compilación desde la linea de comandos tiene preferencia y puede potencialmente sobrescribir el de `makepkg.conf`.

GCC puede detectar automáticamente y habilitar de forma segura las optimizaciones especificas de la arquitectura. Para utilizar esta función, primero elimina cualquier `-march` y `-mtune` flags, después añade `-march=native`. Por ejemplo:

 `/etc/makepkg.conf` 
```
CFLAGS="**-march=native** -O2 -pipe -fstack-protector-strong -fno-plt"
CXXFLAGS="${CFLAGS}"
```

Para ver que flags estan habilitadas en tu ordenador, ejecuta:

```
$ gcc -march=native -v -Q --help=target

```

**Nota:** Si especificas un valor diferente que `-march=native`, después `-Q --help=target` **puede no** funcionar como se espera.[[3]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) Necesitas ir por los pasos de la compilación para ver que opciones están habilitadas realmente. Mira [Find CPU-specific options](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) en la wiki de Gentoo para instrucciones.

### Mejorar tiempos de compilación

#### Compilación paralela

El sistema de construcción [make](https://www.archlinux.org/packages/?name=make) usa las `MAKEFLAGS` como variables de entorno para especificar opciones adicionales. Las variables también pueden ser definidas en el archivo `/etc/makepkg.conf`.

Usuarios con sistemas que poseen múltiples núcleos o CPU pueden especificar el número de trabajos a ejecutar simultáneamente. Esto se puede realizar usando *nproc* para determinar el número de procesadores disponibles, v.g. modificando la línea `MAKEFLAGS` en `/etc/makepkg.conf`.

```
MAKEFLAGS="**-j$(nproc)**"

```

Para decirle al compilador que use un número especifico de núcleos al momento de compilar, se usa el mismo parámetro `-j<numero_de_núcleos>`. El número recomendado es *n*+1, donde *n* es la cantidad de núcleos de tu procesador.

Por ejemplo un procesador de 2 núcleos (2+1=3):

 `/etc/makepkg.conf` 
```
...
#-- Make Flags: change this for DistCC/SMP systems
MAKEFLAGS="-j3"
...

```

Algunos [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") sobrescriben específicamente con `-j1`, por las condiciones en algunas versiones o porque simplemente no están soportadas en primer lugar. Paquetes que fallen la construcción por esto debe de ser [reportado](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") en el bug tracker (o en su caso de los paquetes del [AUR](/index.php/AUR "AUR"), al mantenedor del paquete) después de estar seguro que ese error lo causa su `MAKEFLAGS`.

Vea [make(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) para una lista completa de opciones.

#### Construir desde archivos en memoria

La compilación requiere muchas operaciones I/O y manejar muchos archivos pequeños, moviendo el directorio de trabajo a [tmpfs](/index.php/Tmpfs "Tmpfs") puede mejorar los tiempos de compilación.

La variable `BUILDDIR` se puede exportar temporalmente a *makepkg* para establecer el directorio de trabajo a un tmpfs existente. Por ejemplo:

$ BUILDDIR=/tmp/makepkg makepkg

La configuración duradera se puede hacer en `makepkg.conf` descomentando la opción `BUILDDIR`, que se encuentra al final de la sección `BUILD ENVIRONMENT` en el archivo `/etc/makepkg.conf` por defecto. Estableciendo el valor en, por ejemplo, `BUILDDIR=/tmp/makepkg` hará que make use el sistema de archivos temporal `/tmp` por defecto en Arch.

**Nota:**

*   Evita compilar paquetes grandes en tmpfs para prevenir que se ejecute fuera de memoria.
*   La carpeta tmpfs tiene que estar montada sin la opción `noexec`, si no evitara ejecutar la construcción de binarios.
*   Mantén en mente que los paquetes compilados en tmpfs no perdurarán en un reinicio. Considera establecer la opción [PKGDEST](#Resultado_del_paquete) apropiada para mover el paquete construido automáticamente a un directorio persistente.

#### Usar caché de compilación

El uso de [ccache](/index.php/Ccache "Ccache") puede mejorar los tiempos de compilación generando caché los resultados de las compilaciones para utilizarlos sucesivamente.

### Generar nueva suma de verificación

Instala [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) y ejecute el siguiente comando en el mismo directorio que el PKBUILD para generar una nueva suma de verificación:

```
$ updpkgsums

```

Las sumas de verificación pueden también obtenerse con, por ejemplo, `sha256sum` y añadirlo al array `sha256sums` a mano.

### Usar otros algoritmos de compresión

Para acelerar la empaquetación y la instalación, con la desventaja de tener paquetes más grandes, cambia `PKGEXT`. Por ejemplo, lo siguiente hace que el paquete se descomprima para una sola invocación:

```
$ PKGEXT='.pkg.tar' makepkg

```

Otro ejemplo, usar el algoritmo lzop, con el paquete necesario [lzop](https://www.archlinux.org/packages/?name=lzop):

```
$ PKGEXT='.pkg.tar.lzo' makepkg

```

Para hacer estas configuraciones permanentes, establece `PKGEXT` en `/etc/makepkg.conf`.

### Uso de múltiples núcleos en la compresión

[xz](https://www.archlinux.org/packages/?name=xz) es compatible con [Multiprocesamiento_simétrico (SMP)](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing") con el párametro `--threads` para acelerar la compresión. Para permitir que *makepkg* use tantos núcleos como sea possible al comprimir paquetes, edite la linea `COMPRESSXZ` en `/etc/makepkg.conf`:

```
COMPRESSXZ=(xz -c -z - **--threads=0**)

```

[pigz](https://www.archlinux.org/packages/?name=pigz) es una implementación paralela de [gzip](https://www.archlinux.org/packages/?name=gzip) en la que por defecto utiliza todos los núcleos de la CPU disponibles. El parámetro `-p/--processes` se puede utilizar para que utilice menos núcleos:

COMPRESSGZ=(**pigz** -c -f -n)

### Ver paquetes con un empaquetador específico

Esto muestra todos los paquetes instalados en el sistema con el empaquetador *nombreempaqueetador*:

$ expac "%n %p" | grep "*nombreempaquetador*" | column -t

Esto muestra todos los paquetes instalados en el sistema con el empaquetador establecido en la variable `PACKAGER` en el `/etc/makepkg`. Solo muestra los paquetes que están en el repositorio definido en `/etc/pacman.conf`.

$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)

### Construir paquetes de 32-bit en un sistema de 64-bit

Primero, habilite el repositorio [multilib](/index.php/Multilib "Multilib") e [instala](/index.php/Instala "Instala") [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/).

Después crea un archivo de configuración de 32-bit.

 `~/.makepkg.i686.conf` 
```
CARCH="i686"
CHOST="i686-unknown-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"
LDFLAGS="-m32 -Wl,-O1,--sort-common,--as-needed,-z,relro"
```

y ejecuta makepkg así

```
$ linux32 makepkg --config ~/.makepkg.i686.conf

```

## Solución de problemas

### A veces makepkg falla al firmar un paquete sin preguntar la frase de firma

Con [gnupg 2.1](https://www.gnupg.org/faq/whats-new-in-2.1.html), gpg inicializa sobre la marcha gpg-agent. El problema se presenta en la etapa `makepkg --sign`. Para permitir los privilegios correctos, [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) ejecuta la función `package()` inicializando gpg-agente con el mismo entorno fakeroot. En la salida, fakeroot limpia el codigo de señales causando que en el extremo de la escritura cierre esa instancia de gpg-agent con el resultado de un error. Si el mismo gpg-agent se ejecuta cuando `makepkg --sign` es el siguiente en ejecutarse, gpg-agent devuelve el código de salida 2; ocurriendo la siguiente salida:

```
==> Signing package...
==> WARNING: Failed to sign package file.

```

Este bug se está rastreando: [FS#49946](https://bugs.archlinux.org/task/49946). Una solución temporal para este problema es ejecutar `killall gpg-agent && makepkg --sign`. Este problema está solucionado dentro de [pacman-git](https://aur.archlinux.org/packages/pacman-git/), específicamente en el comentario hash `c6b04c04653ba9933fe978829148312e412a9ea7`

### CFLAGS/CXXFLAGS/LDFLAGS en makepkg.conf no funcionan en los paquetes basados en CMake

Con el fin de dejar que CMake use las variables definidas en `makepkg.conf`, simplemente no especifique la variable `-DCMAKE_BUILD_TYPE` cuando configure un proyecto cmake.[[4]](https://lists.archlinux.org/pipermail/arch-dev-public/2018-March/029181.html)

Esto causa que cmake utilice una construcción tipo `None` en la que utiliza las variables de entorno como `CFLAGS`, `CPPFLAGS`, etc.

### CFLAGS/CXXFLAGS/LDFLAGS en makepkg.conf no funcionan en los paquetes basados en QMAKE

Qmake establece automáticamente las variables `CFLAGS`, `CXXFLAGS` y `LDFLAGS` acorde con la configuración que él considera correcto. Con el fin de dejar que qmake utilice las variables definidas en el archivo de configuración makepkg, tienes que editar el PKGBUILD y pasar las variables [QMAKE_CFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cflags), [QMAKE_CXXFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cxxflags) y [QMAKE_LFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-lflags) a qmake. Por ejemplo:

 `PKGBUILD` 
```
...

build() {
  cd "$srcdir/$_pkgname-$pkgver-src"
  qmake-qt5 "$srcdir/$_pkgname-$pkgver-src/$_pkgname.pro" \
    PREFIX=/usr \
    QMAKE_CFLAGS="${CFLAGS}" \
    QMAKE_CXXFLAGS="${CXXFLAGS}" \
    QMAKE_LFLAGS="${LDFLAGS}"

  make
}

...

```

Alternativamente, en un sistema amplio de configuración, puedes crear tu propio `qmake.conf` y establecer las variables de entorno [QMAKESPEC](https://doc.qt.io/qt-5/qmake-environment-reference.html#qmakespec).

### Especificar el directorio de instalación para los paquetes basados en QMAKE

El makefile generado por qmake utiliza la variable de entorno INSTALL_ROOT para determinar dónde se va a instalar el programa. Así que esta funcion del paquete debería funcionar:

 `PKGBUILD` 
```
...

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir" install
}

...

```

Tenga en cuenta que qmake tiene que estar configurado correctamente, por ejemplo ponga esto en su archivo .pro:

 `YourProject.pro` 
```
...

target.path = /usr/local/bin
INSTALLS += target

...

```

### ADVERTENCIA: Paquetes que contienen referencias a $srcdir

Por alguna razón, las cadenas `$srcdir` o `$pkgdir` literales acaban en uno de los archivos de instalación en su paquete.

Para identificar que archivos son, ejecute lo siguiente desde el directorio de construcción de *makepkg*:

```
$ grep -R "$(pwd)/src" pkg/

```

### Makepkg falla al descargar las dependencias a través de un proxy

Cuando *makepkg* llama a las dependencias, llama a pacman para instalar los paquetes, que requieren permisos administrativos via *sudo*. De todas formas, *sudo* no pasa ninguna [variable de entorno](/index.php?title=Variable_de_entorno&action=edit&redlink=1 "Variable de entorno (page does not exist)") al entorno con privilegios, incluido las variables relacionadas con el proxy `ftp_proxy`, `http_proxy`, `https_proxy`, y `no_proxy`.

Para tener a *makepkg* trabajando a través de un proxy tiene que seguir uno de los dos métodos.

#### Habilitar proxy estableciendo su URL en XferCommand

XferCommand puede establecerse para utilizar la URL del proxy deseado en `/etc/pacman.conf`. Añade o descomenta la siguiente línea en su `pacman.conf`[[5]](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html):

 `/etc/pacman.conf` 
```
...
XferCommand = /usr/bin/curl -x http://username:password@proxy.proxyhost.com:80 -L -C - -f -o %o %u
...

```

#### Habilitar proxy via sudoer's env_keep

Alternativamente, puede querer utilizar la opción `env_keep`, que habilita preservar las variables dadas al entorno privilegiado. Vea [Sudo (Español)#Variables de entorno](/index.php/Sudo_(Espa%C3%B1ol)#Variables_de_entorno "Sudo (Español)") para más información.

### Makepkg falla, pero el make termina bien

Si algo se compila manualmente utilizando *make*, pero falla al utilizar *makepkg*, casi seguro que es porque el `/etc/makepkg.conf` establece la variable de compilación a algo que normalmente funciona, pero lo que usted esta compilando sea incompatible. Intente añadir estos parámetros a la linea `options` del PKGBUILD:

`!buildflags`, para evitar que utilice `CPPFLAGS`, `CFLAGS`, `CXXFLAGS`, y `LDFLAGS` dadas por defecto.

`!makeflags`, para evitar que utilice `MAKEFLAGS` por defecto, en caso de que se haya editado `/etc/makepkg.conf` para habilitar la compilación paralela.

`!debug`, para evitar que utilice `DEBUG_CFLAGS` y `DEBUG_CXXFLAGS` dadas por defecto, en caso de que su paquete sea una construcción debug.

Si alguno de estos parámetros soluciona el problema, lo puede indicar reportando un bug, si usted localiza que parámetro exactamente está causando el problema.

## Véase también

*   [makepkg(8) Manual Page](https://www.archlinux.org/pacman/makepkg.8.html)
*   [makepkg.conf(5) Manual Page](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [A Brief Tour of the Makepkg Process](https://gist.github.com/Earnestly/bebad057f40a662b5cc3)
*   [makepkg source code](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)
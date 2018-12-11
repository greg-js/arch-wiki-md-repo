Artículos relacionados

*   [Crear paquetes](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")
*   [Pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")

makepkg es usado para compilar y construir paquetes capaces de instalar mediante [pacman](/index.php/Pacman "Pacman"), el manejador de paquetes de Arch Linux. makepkg es un script que automatiza el proceso de construcción de paquetes; este puede descargar y validar archivos fuente, resolver dependencias, configurar los parámetros de tiempo de compilación, compilar las fuentes e instalarlo dentro de un root temporal.

El paquete makepkg lo provee el paquete [pacman](https://www.archlinux.org/packages/?name=pacman).

## Contents

*   [1 Configuración](#Configuración)
    *   [1.1 Información del empaquetador](#Información_del_empaquetador)
    *   [1.2 Resultado del paquete](#Resultado_del_paquete)
    *   [1.3 Verificación de firmas](#Verificación_de_firmas)
    *   [1.4 fakeroot](#fakeroot)
*   [2 Uso](#Uso)
*   [3 Recomendaciones](#Recomendaciones)
    *   [3.1 Construir binarios optimizados](#Construir_binarios_optimizados)
    *   [3.2 Mejorar tiempos de compilación](#Mejorar_tiempos_de_compilación)
        *   [3.2.1 Compilación paralela](#Compilación_paralela)
    *   [3.3 Generar nueva suma de verificación](#Generar_nueva_suma_de_verificación)
    *   [3.4 Uso de múltiples núcleos en la compresión](#Uso_de_múltiples_núcleos_en_la_compresión)

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

## Uso

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

**Nota:** Estas dependencias deben estar disponibles dentro de los repositorios disponibles para pacman, vea [pacman (Español)#Repositorios y servidores de réplicas](/index.php/Pacman_(Espa%C3%B1ol)#Repositorios_y_servidores_de_réplicas "Pacman (Español)") para mayor información al respecto. También se pueden instalar las dependencias antes de construir el paquete (`pacman -S --asdeps dep1 dep2`).

Una vez que se hayan satisfecho todas las dependencias y el paquete se construyo satisfactoriamente, un archivo con el nombre (`pkgname-pkgver.pkg.tar.gz`) será creado en el directorio de trabajo. Para instalarlo (al igual que `pacman -U pkgname-pkgver.pkg.tar.gz`) simplemente se ejecuta:

```
$ makepkg -i

```

Para despejar archivos que no son necesarios, como los existentes en `$srcdir`, agregue la opción `-c`. Este comando es útil al actualizar la version de los paquetes usando el mismo directorio. Se previene la transferencia de archivos obsoletos en la nueva construcción.

```
$ makepkg -c

```

## Recomendaciones

### Construir binarios optimizados

Una mejora de rendimiento del empaquetado de software se puede lograr habilitando optimizaciones en la máquina local. El inconveniente es que los binarios compilados para una arquitectura de procesador específico pueden no ejecutarse correctamente en otros ordenadores. En las máquinas x86_64 es raro ganar un rendimiento significativo que justifique invertir tiempo en reconstruir los paquetes oficiales.

Sin embargo es muy fácil disminuir el rendimiento utilizando FLAGS de compilación "no estandar". Muchas optimizaciones son útiles solo en determinadas situaciones y no debe de aplicarse para todos los paquetes. A no haya ser que puedas verificar que algo es más rápido, es una muy buena oportunidad ¡como no! Los artículos de Gentoo [Guía de optimización de compilación](https://wiki.gentoo.org/wiki/GCC_optimization/es) y [CFLAGS Seguros (en ingles)](http://wiki.gentoo.org/wiki/Safe_CFLAGS) proporciona mas información detallada sobre optimizaciones de compilador.

Las opciones pasadas al compilador C/C++ (e.g. [gcc](https://www.archlinux.org/packages/?name=gcc) o [clang](https://www.archlinux.org/packages/?name=clang)) están controladas por `CFLAGS`, `CXXFLAGS` y `CPPFLAGS` variables de entorno. Para usarlos en el sistema de construcción de Arch, *makepkg* muestra las variables de entorno según las opciones de configuración en `makepkg.conf`. Los valores por defecto están configurados para producir binarios genéricos que pueden ser instalados en un amplio rango de máquinas.

**Nota:**

*   Tener en cuenta que no todos los sistemas de construcciones utilizan las variables configuradas en `makepkg.conf`. Por ejemplo, *cmake* no tiene en cuenta las opciones de preprocesamiento `makepkg.conf`. Consecuentemente, muchos [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") contiene métodos alternativos con opciones específicas para el sistema constructor usado por el gestor de paquetes.
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

**Nota:** Si especificas un valor diferente que `-march=native`, después `-Q --help=target` **puede no** funcionar como se espera.[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) Necesitas ir por los pasos de la compilación para ver que opciones están habilitadas realmente. Mira [Find CPU-specific options](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) en la wiki de Gentoo para instrucciones.

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

Vea [make(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) para una lista completa de opciones.

### Generar nueva suma de verificación

Ejecute el siguiente comando en el mismo directorio que el PKBUILD para generar una nueva suma de verificación:

```
$ updpkgsums

```

### Uso de múltiples núcleos en la compresión

[xz](https://www.archlinux.org/packages/?name=xz) es compatible con [Multiprocesamiento_simétrico (SMP)](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing") con el párametro `--threads` para acelerar la compresión. Para permitir que *makepkg* use tantos núcleos como sea possible al comprimir paquetes, edite la linea `COMPRESSXZ` en `/etc/makepkg.conf`:

```
COMPRESSXZ=(xz -c -z - **--threads=0**)

```
Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [pacman](/index.php/Pacman "Pacman")
*   [Official repositories](/index.php/Official_repositories "Official repositories")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")

makepkg es usado para compilar y construir paquetes capaces de instalar mediante [pacman](/index.php/Pacman "Pacman"), el manejador de paquetes de Arch Linux. makepkg es un script que automatiza el proceso de construcción de paquetes; este puede descargar y validar archivos fuente, resolver dependencias, configurar los parámetros de tiempo de compilación, compilar las fuentes e instalarlo dentro de un root temporal.

El paquete makepkg lo provee el paquete [pacman](https://www.archlinux.org/packages/?name=pacman).

## Contents

*   [1 Configuración](#Configuraci.C3.B3n)
    *   [1.1 fakeroot](#fakeroot)
*   [2 Uso](#Uso)
*   [3 Recomendaciones](#Recomendaciones)
    *   [3.1 Compilación paralela](#Compilaci.C3.B3n_paralela)
    *   [3.2 Generar nueva suma de verificación](#Generar_nueva_suma_de_verificaci.C3.B3n)
    *   [3.3 Uso de múltiples núcleos en la compresión](#Uso_de_m.C3.BAltiples_n.C3.BAcleos_en_la_compresi.C3.B3n)

## Configuración

El archivo principal de configuración de makepkg es `/etc/makepkg.conf` . la mayoría de los usuarios querrán configurar estas opciones de makepkg antes de construir cualquier paquete (por ejemplo modificar las variables `MAKEFLAGS` en sistemas con soporte SMP para [reducir tiempos de compilación](/index.php/Makepkg_(Espa%C3%B1ol)#Recomendaciones "Makepkg (Español)") , o personalizar la variable `PACKAGER` para personalizar paquetes. Lea la documentación de `PACKAGER` para más detalles

Para poder instalar paquetes con makepkg sin ser usuario administrador (con `makepkg -s`, información más delante), instale [sudo](/index.php/Sudo "Sudo") y agregue los usuarios con estos privilegios en el archivo to `/etc/sudoers`:

```
USER_NAME    ALL=(ALL)    NOPASSWD: /usr/bin/pacman

```

La línea de arriba eliminara la necesidad de introducir un password cada vez que utilicemos pacman. Revise la wiki de [sudo](/index.php/Sudo "Sudo") para mas información

Enseguida, puede configurar donde serán guardados los paquetes terminados. Este paso es meramente opcional; por definición los paquetes serán creados en el directorio donde makepkg se ejecute Cree el directorio:

```
$ mkdir /home/$USER/packages

```

Luego modifique la variable `PKGDEST` en el archivo `/etc/makepkg.conf` de acuerdo a esta directorio.

### `fakeroot`

`fakeroot` permite al usuario usar los permisos necesarios de root para crear paquetes en el ambiente de construcción sin necesidad de alterar todo el sistema. Si el proceso de construcción trata de alterar archivos fuera del ambiente de construcción entonces aparecerán mensajes de error y el empaquetado habrá fallado – esto es muy útil para verificar la calidad, seguridad e integridad de los PKGBUILD para su distribución. Por default `fakeroot` esta habilitado en el archivo de configuración `/etc/makepkg.conf`; los usuarios pueden utilizar el prefijo `!` en la variable `BUILDENV` para deshabilitar esto

## Uso

Antes de continuar, asegúrese de que el grupo de paquetes [base-devel](https://www.archlinux.org/packages/?name=base-devel) estén instalados. Los paquetes pertenecientes a este grupo no necesariamente tienen que ser listados como dependencias en los [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Asegúrese de tener instalado este paquete ejecutando (como root):

```
# pacman -S base-devel

```

**Nota:**

*   Antes de quejarse por dependencias incumplidas en la rutina make, recuerde que se da por entendido que el grupo “base” esta instalado por default en todos los sistemas Arch Linux. El paquete “base-devel” se da por entendió que también esta instalado cuando se crean paquetes con makepkg.
*   Ejecutar *makepkg* como root no esta [permitido](https://lists.archlinux.org/pipermail/pacman-dev/2014-March/018911.html). Debido a que un `PKGBUILD` puede incluir comandos arbitrarios, construir como root se considera riesgoso.

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

**Nota:** Estas dependencias deben estar disponibles dentro de los repositorios disponibles para pacman, vea [pacman_(Español)#Repositorios y servidores de réplicas](/index.php/Pacman_(Espa%C3%B1ol)#Repositorios_y_servidores_de_r.C3.A9plicas "Pacman (Español)") para mayor información al respecto. También se pueden instalar las dependencias antes de construir el paquete (`pacman -S --asdeps dep1 dep2`).

Una vez que se hayan satisfecho todas las dependencias y el paquete se construyo satisfactoriamente, un archivo con el nombre (`pkgname-pkgver.pkg.tar.gz`) será creado en el directorio de trabajo. Para instalarlo (al igual que `pacman -U pkgname-pkgver.pkg.tar.gz`) simplemente se ejecuta:

```
$ makepkg -i

```

Para despejar archivos que no son necesarios, como los existentes en `$srcdir`, agregue la opción `-c`. Este comando es útil al actualizar la version de los paquetes usando el mismo directorio. Se previene la transferencia de archivos obsoletos en la nueva construcción.

```
$ makepkg -c

```

## Recomendaciones

### Compilación paralela

El sistema de construcción [make](https://www.archlinux.org/packages/?name=make) usa las `MAKEFLAGS` como variables de entorno para especificar opciones adicionales. Las variables también pueden ser definidas en el archivo `/etc/makepkg.conf`.

Usuarios con sistemas que poseen múltiples núcleos o CPU pueden especificar el número de trabajos a ejecutar simultáneamente. Esto se puede realizar usando *nproc* para determinar el numero de de procesadores disponibles, v.g. modificando la linea `MAKEFLAGS` en `/etc/makepkg.conf`.

```
MAKEFLAGS="**-j$(nproc)**"

```

Vea [make(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) para una lista completa de opciones.

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
Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [pacman](/index.php/Pacman "Pacman")
*   [Official repositories](/index.php/Official_repositories "Official repositories")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")

makepkg es usado para compilar y construir paquetes capaces de instalar mediante [pacman](/index.php/Pacman "Pacman"), el manejador de paquetes de Arch Linux. makepkg es un script que automatiza el proceso de construcción de paquetes; este puede descargar y validar archivos fuente, resolver dependencias, configurar los parámetros de tiempo de compilación, compilar las fuentes e instalarlo dentro de un root temporal.

El paquete makepkg lo provee el paquete [pacman](https://www.archlinux.org/packages/?name=pacman).

## Configuracion

El archivo principal de configuración de makepkg es `/etc/makepkg.conf` . la mayoría de los usuarios querrán configurar estas opciones de makepkg antes de construir cualquier paquete (por ejemplo modificar las variables `MAKEFLAGS` en sistemas con soporte SMP para reducir tiempos de compilación, o personalizr la variable `PACKAGER` para personalizar paquetes. Lea la documentación de `PACKAGER` para más detalles

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

Antes de continuar, asegúrese de que el grupo de paquetes “base-devel” estén instalados. Los paquetes pertenecientes a este grupo no necesariamente tienen que ser listados como dependencias en los [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Asegúrese de tener instalado este paquete ejecutando (como root):

```
# pacman -S base-devel

```

**Nota:** Antes de quejarse por dependencias incumplidas en la rutina make, recuerde que se da por entendido que el grupo “base” esta instalado por default en todos los sistemas Arch Linux. El paquete “base-devel” se da por entendió que también esta instalado cuando se crean paquetes con makepkg.

Para crear un paquete primero debe tener un a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), como se describe en la guía de in [Creating packages](/index.php/Creating_packages "Creating packages"), o obtenga uno del [ABS tree](/index.php/Arch_Build_System "Arch Build System"), [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), u obténgalo de alguna otra fuente.

**Advertencia:** solo o instale paquetes de fuentes confiables.

Una vez en posesión de un `PKGBUILD`, entre al directorio donde esta salvado este archivo y ejecute el siguiente comando para compilar y construir el paquete como lo fue descrito en el archivo un `PKGBUILD`:

```
$ makepkg

```

Si no se satisfacen algunas dependencias, makepkg mostrara una advertencia antes de fallar, para construir el paquete y cumplir sus dependencias automáticamente, simplemente utilizamos el comando: $ makepkg -s

Note que estas dependencias deben estar disponibles dentro de los repositorios disponibles para pacman, vea [pacman#Repositories](/index.php/Pacman#Repositories "Pacman") para mayor información al respecto. También se pueden instalar las dependencias previas antes de construir el paquete (`pacman -S dep1 dep2`).

Una vez que se hayan satisfecho todas las dependencias el paquete se habrá construido satisfactoriamente, un archivo con el nombre (`pkgname-pkgver.pkg.tar.gz`) será creado en el directorio de trabajo. Para instalarlo simplemente ejecutamos (como root):

1.  pacman -U pkgname-pkgver.pkg.tar.gz
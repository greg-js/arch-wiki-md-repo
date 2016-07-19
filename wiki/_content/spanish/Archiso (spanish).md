**Archiso** es un pequeño conjunto de scripts de bash capaz de construir imagenes live de CD o USB plenamente funcionales basadas en Arch Linux. Es una herramienta muy genérica, de manera que puede ser usada potencialmente para generar cualquier cosa, desde sistemas de rescate o discos de instalacion, hasta sistemas live CD/DVD/USB para intereses especiales, y quién sabe qué más. Simplemente, si involucra a Arch en una montaña brillante, puede hacerlo. El corazón y alma de Archiso es mkarchiso. Todas sus opciones están documentadas en su ayuda de uso, de manera que su uso directo no será tratado aquí. ¡En su lugar, este artículo actuará como guía para crear tus propios medios live en nada de tiempo!

## Contents

*   [1 Preparar la instalación](#Preparar_la_instalaci.C3.B3n)
*   [2 Configurar nuestro medio live](#Configurar_nuestro_medio_live)
    *   [2.1 Instalar paquetes](#Instalar_paquetes)
    *   [2.2 Añadir un usuario](#A.C3.B1adir_un_usuario)
    *   [2.3 Añadir archivos a la imagen](#A.C3.B1adir_archivos_a_la_imagen)
    *   [2.4 aitab](#aitab)
    *   [2.5 Cargador de arranque](#Cargador_de_arranque)
    *   [2.6 Gestor de inicio de sesión](#Gestor_de_inicio_de_sesi.C3.B3n)
*   [3 Construir la ISO](#Construir_la_ISO)
*   [4 Utilizar la ISO](#Utilizar_la_ISO)
    *   [4.1 CD](#CD)
    *   [4.2 USB](#USB)
    *   [4.3 grub4dos](#grub4dos)
    *   [4.4 Instalación](#Instalaci.C3.B3n)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Preparar la instalación

**Nota:** El script es para ser utilizado en una máquina x86_64.

Antes de empezar, necesitamos hacernos con los scripts de archiso que llevan a cabo gran parte del trabajo, para ello [instalaremos](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [archiso](https://www.archlinux.org/packages/?name=archiso) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Alternativamente, la versión GIT ([archiso-git](https://aur.archlinux.org/packages/archiso-git/)) puede ser construída e instalada desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

Crea un directorio para trabajar con el, aquí es donde todas las modificaciones de la imagen live tendrán lugar: `/home/tuusuario/**archlive**` está bien (y es el ejemplo que se utilizará a lo largo de esta guía):

```
$ mkdir /home/tuusuario/archlive

```

Ahora necesitamos copiar los scripts de archiso, que fueron previamente instalados en nuestro sistema, dentro de la carpeta creada, en la que trabajaremos.

Archiso tiene dos «perfiles»: *releng* y *baseline*. Si quieres crear una versión live de Arch Linux totalmente personalizada, preinstalada con todos tus programas favoritos y configuraciones, usa *releng.*

Si solo quieres crear el medio live más básico, sin paquetes preinstalados y configuraciones mínimas, usa *baseline*.

De manera que, dependiendo de tus necesidades, ejecuta lo siguiente, sustituyendo «PERFIL» por **releng** o **baseline**.

```
# cp -r /usr/share/archiso/configs/**PERFIL**/ /home/tuusuario/archlive

```

Si estás utilizando el perfil *releng* para hacer una imagen totalmente personalizada, puedes hacerlo en [Configurar nuestro medio live](#Configurar_nuestro_medio_live).

Si estás usando el perfil *baseline* para crear una imagen de instalación mínima, no necesitarás hacer ninguna personalización y puedes ir directamente a [Construir la ISO](#Construir_la_ISO)

## Configurar nuestro medio live

Esta sección detalla la configuración de la imagen que vas a ir creando, premitiendote definir los paquetes y configuraciones que quieres que tu imagen contenga.

Nos movemos al directorio que hemos creado antes (es decir, `/home/tuusuario/archlive/releng/` si estás siguiendo esta guía). Allí verás una serie de archivos y directorios; solo nos interesan unos pocos, principalmente: `packages.*` —aquí es donde harás una lista, línea a línea, de los paquetes que quieres tener instalados—; y el directorio `root-image` —este directorio actúa como cubierta y es donde harás todas tus personalizaciones—.

### Instalar paquetes

Querrás crear una lista de paquetes que quieres instalar en tu sistema live CD. Un archivo lleno de nombres de paquetes, uno por línea, es el formato correcto para hacer esto. Esto es ***muy bueno*** para crear live CD para intereses especiales, solamente especifica que paquetes quieres en `packages.both` y «cuece» la imagen. Los archivos `packages.i686` y `packages.x86_64` te permiten instalar software para solo 32bit o 64bit, respectivamente.

**Sugerencia:** También puedes crear un **[repositorio local personalizado (en)](/index.php/Custom_local_repository "Custom local repository")** para preparar paquetes personalizados o paquetes de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")/[ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). Simplemente añade tu repositorio local en la primera posición (para que tenga prioridad) del archivo **pacman.conf** de tu ordenador, ¡y listo!

### Añadir un usuario

Hay dos métodos para crear un usuario: con useradd, o copiando (y modificando) /etc/shadow, /etc/passwd, y /etc/group. Este último método se desarrolla a continuación.

Copia tus archivos `/etc/shadow`, `/etc/passwd`, y `/etc/group` de tu propio sistema **anfitrión** al directorio `/etc/` **de tu nuevo sistema live** (que debería ser `/home/tuusuario/archlive/releng/root-image/etc`), por ejemplo:

```
# cp /etc/{shadow,passwd,group} /home/tuusuario/archlive/releng/root-image/etc/

```

**Advertencia:** El archivo *shadow* contendrá tu clave encriptada. Se recomienda que antes de copiar el archivo shadow, cambies la contraseña de tu usuario del sistema anfitrión, por la que quieras que tenga tu usuario del sistema live, luego copias el archivo shadow, y, después, vuelves a cambiar la contraseña del usuario de tu sistema anfitrión.

### Añadir archivos a la imagen

**Nota:** Debes ser superusuario para hacer esto, no cambies el nombre del usuario titular de ninguno de los archivos que copies, **todo** dentro del directorio root-image debe ser propiedad de *root*. El nombre del usuario titular correcto se resolverá automáticamente.

El directorio root-image actua como una cubierta, piensa en él como el directorio raíz, `/`, de tu sistema anfitrión, de manera que cada archivo que pongas dentro se copiará al arranque.

Así que, si tienes un conjunto de scripts de iptables en tu sistema anfitrión que quieres poder usar en tu posterior imagen live, cópialos así:

```
# cp -r /etc/iptables /home/tuusuario/archlive/releng/root-image/etc

```

Poner archivos del directorio home del usuario en tu imagen live es un poco diferente. No los pongas en root-image/home; en lugar de eso crea un directorio `skel` dentro de `root-image/` y colócalos ahí. Después añadiremos las órdenes relevantes al archivo `customize_root_image.sh` que vamos a crear para copiarlos en el arranque y definir los permisos.

Primero, crea el directorio skel; asegúrate de que estás en `/home/tuusuario/archlive/releng/root-image/etc` (si es aquí donde estás trabajando):

```
# cd /home/tuusuario/archlive/releng/root-image/etc && mkdir skel

```

Ahora copia los archivos de «home» al directorio skel, ¡nuevamente haz todo como superusuario!, por ejemplo para .bashrc:

```
# cp /home/tuusuario/.bashrc /home/tuusuario/archlive/releng/root-image/etc/skel/

```

Ahora añade todo lo que sigue a `/home/tuusuario/archlive/releng/root-image/root/customize_root_image.sh`, sustituyendo «tuusuariolive» por el usuario que específicaste [antes](#A.C3.B1adir_un_usuario).

```
# Crear el directorio del usuario para la sesión live
if [ ! -d /home/**tuusuariolive** ]; then
    mkdir /home/**tuusuariolive** && chown **tuusuariolive** /home/**tuusuario**
fi
# Copiar los archivos a home
su -c "cp -r /etc/skel/.* /home/**tuusuariolive**/" **tuusuariolive**

```

### aitab

El archivo por defecto debería funcionar bien, de manera que no deberías necesitar tocarlo.

El archivo aitab tiene información acerca de las imágenes de los sistemas de archivos que deben ser creadas por mkarchiso y montadas en la fase de initramfs del *hook* archiso. Consiste en unos campos que definen el comportamiento de las imágenes.

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>

```

	<img>

	Nombre de la imagen sin extensión (.fs .fs.sfs .sfs).

	<mnt>

	Punto de montaje.

	<arch>

	Arquitectura { i686 | x86_64 | any }.

	<sfs_comp>

	Tipo de compresión de SquashFS { gzip | lzo | xz }.

	<fs_type>

	Define el tipo de sistema de archivos de la imagen { ext4 | ext3 | ext2 | xfs }. Un valor especial «none» denota que no se usa un sistema de archivos. En ese caso todos los archivos son usados directamente por el sistema de archivos de SquashFS.

	<fs_size>

	Un valor absoluto del tamaño de la imagen del sistema en MiB (ejemplo: 100, 1000, 4096, etc.). Un valor relativo del espacio libre del sistema [en porcentaje] {1%..99%} (ejemplo 50%, 10%, 7%). Es una estimación, y se calcula de forma simple. Espacio usado + 10% (estimación para gastos generales de metadatos) + % deseado

**Nota:** Algunas combinaciones son inválidas. Por ejemplo sfs_comp y fs_type se definen como none

### Cargador de arranque

El archivo por defecto debería funcionar bien, de manera que no deberías necesitar tocarlo.

Debido a la naturaleza modular de isolinux, puedes usar un montón de añadidos, ya que todos los archivos `*.c32` se pueden copiar y están disponibles para ti. Echa un vistazo al [sitio oficial de syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) y al [repositorio git de archiso](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Usando dichos añadidos, es posible hacer menús visualmente atractivos y complejos. Mira [aquí](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32)

### Gestor de inicio de sesión

Iniciar X con el arranque el sistema, se hacía modificando *inittab* en los sistemas [sysvinit](/index.php/SysVinit_(Espa%C3%B1ol) "SysVinit (Español)"). En un sistema basado en [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") las cosas se manejan activando el archivo *.service* de tu gestor de inicio de sesión. Si sabes qué enlace necesitas para el archivo *.service` en cuestión: bien. Si no, puedes averiguarlo fácilmente, en el caso de que estés usando el mismo gestor de pantalla en tu sistema. Solo escribe:*

```
# systemctl disable **nombredetugestordeiniciodesesión**

```

para desactivarlo temporalmente. Ahora pon la misma orden otra vez, sustituyendo *«disable»* por *«enable»*, para activarlo de nuevo. Systemctl muestra información acerca de los enlaces que crea. Ahora muévete al directorio `/home/tuusuario/archlive/releng/root-image/etc/systemd/system` y crea el mismo enlace ahí.

Un ejemplo (asegurate de que estás en `/home/tuusuario/archlive/releng/root-image/etc/systemd/system` o añádelo a la orden):

```
# ln -s /usr/lib/systemd/system/lxdm.service display-manager.service

```

Esto activará el gestor de de inicio de sesión LXDM al arranque del sistema de tu soporte live.

## Construir la ISO

Ya estás listo para poner tus archivos en la .iso, la cual podrás grabar en un CD o USB:

Dentro del directorio en el que estás trabajando, sea `/home/tuusuario/archlive/releng` o `/home/tuusuario/archlive/baseline`, ejecuta:

```
# ./build.sh -v

```

Este script descargará e instalará los paquetes que especificaste en `work/*/root-image`, creará las imágenes del kernel y de inicio, aplicará tus personalizaciones y finalmente construirá la iso en la carpetza `out/`.

## Utilizar la ISO

### CD

Simplemente grábala en un cd. Puedes seguir [CD Burning](/index.php/CD_Burning "CD Burning") como desees.

### USB

Ahora puedes grabar la imagen iso en un USB usando dd, un ejemplo:

```
# dd if=/home/tuusuario/archlive/releng/out/*.iso of=/dev/sdx

```

¡Tendrás que ajustarlo de forma acorde, y asegurarte de que eliges la salida correcta!. Un simple error aquí podría destruir la infomarción de tu disco duro.

### grub4dos

Grub4dos es una utilidad que puedes usar para crear usb multiarranque, capaces de arrancar varias distros linux desde el mismo usb.

Para arrancar el sistema generado en un usb con grub4dos ya instalado, monta la ISO y copia el directorio `/arch` entero en la **raíz del usb**. Después edita el archivo `menu.lst` de grub4dos (debe estar en la raíz del usb) y añade estas líneas:

```
title Archlinux x86_64
kernel /arch/boot/x86_64/vmlinuz archisolabel=<etiqueta de tu usb>
initrd /arch/boot/x86_64/archiso.img

```

Cambia `x86_64` según sea necesario y pon la etiqueta de tu usb **real**.

### Instalación

Arranque el CD/DVD/USB creado. Si desea instalar la Archiso creada **-tal como está-**, hay varios caminos para hacerlo, pero, en cualquier caso, hemos de tener presentes que estamos siguiendo la [Guía para Principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)") en su mayor parte.

Si no tiene una conexión a Internet en su equipo, o si no quiere descargar todos los paquetes que desea otra vez, siga la Guía, y al llegar a la [Instalación del sistema base](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalar_el_sistema_base "Beginners' guide (Español)"), en lugar de realizar la descarga, utilice esto: [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync"). (Más información aquí: [Talk:Archiso](/index.php/Talk:Archiso "Talk:Archiso"))

También puede probar: [Archboot](/index.php/Archboot "Archboot"), instalador gráfico.

## Véase también

*   [Página del proyecto Archiso (en)](https://projects.archlinux.org/?p=archiso.git;a=summary)
*   [Archiso como servidor pxe (en)](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Tutorial paso a paso para usar ArchISO (en)](https://kroweer.wordpress.com/2011/09/07/creating-a-custom-arch-linux-live-usb)
*   [Una distribución live para DJ basada en ArchLinux y construida con Archiso (en)](http://didjix.blogspot.com/)
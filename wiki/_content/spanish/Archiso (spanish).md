**Estado de la traducción**
Este artículo es una traducción de [Archiso](/index.php/Archiso "Archiso"), revisada por última vez el **2018-12-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Archiso&diff=0&oldid=558326) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Archboot (Español)](/index.php/Archboot_(Espa%C3%B1ol) "Archboot (Español)")
*   [Offline installation](/index.php/Offline_installation "Offline installation")

**Archiso** es un pequeño conjunto de scripts de bash capaz de compilar imagenes live en CD/DVD/USB plenamente funcionales basadas en Arch Linux. Es una herramienta muy genérica para generar imágenes oficiales, de manera que puede ser usada potencialmente para generar cualquier cosa, desde sistemas de rescate o discos de instalacion, hasta sistemas live CD/DVD/USB para intereses especiales, y quién sabe qué más. Simplemente, si involucra a Arch en una montaña brillante, puede hacerlo. El corazón y alma de Archiso es *mkarchiso*. Todas sus opciones están documentadas en la ayuda de utilización, de manera que su uso directo no será tratado aquí. En su lugar, este artículo actuará como guía para crear sus propios medios live en poco de tiempo.

Si necesita únicamente un resumen técnico de los requisitos y los pasos de compilación, véase también la [documentación oficial del proyecto](https://git.archlinux.org/archiso.git/tree/docs).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparar la instalación](#Preparar_la_instalación)
*   [2 Configurar el soporte live](#Configurar_el_soporte_live)
    *   [2.1 Instalar paquetes](#Instalar_paquetes)
        *   [2.1.1 Repositorio local personalizado](#Repositorio_local_personalizado)
        *   [2.1.2 Evitar la instalación de paquetes que pertenecen al grupo base](#Evitar_la_instalación_de_paquetes_que_pertenecen_al_grupo_base)
        *   [2.1.3 Instalar paquetes de multilib](#Instalar_paquetes_de_multilib)
    *   [2.2 Añadir archivos a la imagen](#Añadir_archivos_a_la_imagen)
    *   [2.3 Cargador de arranque](#Cargador_de_arranque)
        *   [2.3.1 UEFI Secure Boot](#UEFI_Secure_Boot)
    *   [2.4 Gestor de inicio de sesión](#Gestor_de_inicio_de_sesión)
    *   [2.5 Cambiar el acceso automáticamente](#Cambiar_el_acceso_automáticamente)
*   [3 Compilar la ISO](#Compilar_la_ISO)
    *   [3.1 Reconstruir la ISO](#Reconstruir_la_ISO)
*   [4 Utilizar la ISO](#Utilizar_la_ISO)
*   [5 Véase también](#Véase_también)
    *   [5.1 Documentación y tutoriales](#Documentación_y_tutoriales)
    *   [5.2 Ejemplo de plantilla personalizada](#Ejemplo_de_plantilla_personalizada)
    *   [5.3 Crear una ISO de instalación sin conexión](#Crear_una_ISO_de_instalación_sin_conexión)

## Preparar la instalación

**Nota:** Se recomienda actuar como root en todos los pasos siguientes. Si no es así, es muy probable que tenga problemas con los permisos más adelante.

Antes de empezar, necesitamos hacernos con los scripts de archiso que llevan a cabo gran parte del trabajo, para ello [instalaremos](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [archiso](https://www.archlinux.org/packages/?name=archiso) o ([archiso-git](https://aur.archlinux.org/packages/archiso-git/)).

Archiso viene con dos «perfiles»: *releng* y *baseline*.

*   Si desea crear una versión live totalmente personalizada de Arch Linux, con todos sus programas y configuraciones favoritas preinstalados, utilice releng.
*   Si solo desea crear el soporte live más básico, sin paquetes preinstalados y una configuración minimalista, utilice baseline.

Ahora, copie el perfil de su elección en un directorio (*archlive* en el ejemplo siguiente) donde puede realizar ajustes y compilarlo. Ejecute lo siguiente, reemplazando `**perfil**` con `releng` o `baseline`.

```
# cp -r /usr/share/archiso/configs/**perfil**/ *archlive*

```

*   Si está utilizando el perfil `releng` para hacer una imagen totalmente personalizada, puede seguir en [#Configurar el soporte live](#Configurar_el_soporte_live).

*   Si está utilizando el perfil `baseline` para crear una imagen de instalación mínima, no necesitará hacer ninguna personalización y puede ir directamente a [#Compilar la ISO](#Compilar_la_ISO)

## Configurar el soporte live

Esta sección detalla la configuración de la imagen que va a crear, premitiéndole definir los paquetes y configuraciones que quiere que contenga la imagen.

Dentro del directorio `*archlive*` creado según se ha indicado en [#Preparar la instalación](#Preparar_la_instalación) hay varios archivos y directorios; Solo nos interesan algunos de estos, principalmente:

*   el directorio `packages.x86_64`: aquí es donde se listan, línea por línea, los paquetes que desea instalar, y;
*   el directorio `airootfs`: este directorio actúa como una superposición o cubierte y es donde se realizan todas las personalizaciones.

En general, todas las tareas administrativas que normalmente haría después de una instalación nueva, excepto para la instalación de paquetes, pueden incluirse en `*archlive*/airootfs/root/customize_airootfs.sh`. Debe escribirse el script desde la perspectiva del nuevo entorno, por lo que la raíz `/` en la secuencia de órdenes del script se refiere a la raíz de la iso live que se creará.

### Instalar paquetes

Edite las listas de paquetes en `packages.x86_64` para indicar qué paquetes se instalarán en el soporte live.

**Nota:** Si desea utiliza un [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") en el Live CD, debe agregar los [controladores de vídeo](/index.php/Xorg_(Espa%C3%B1ol)#Instalación_del_controlador "Xorg (Español)"),necesarios y correctos, o el gestor de ventanas puede congelarse al cargar.

#### Repositorio local personalizado

Con el fin de preparar paquetes personalizados o paquetes de [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")/[Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"), también podría [crear un repositorio local personalizado](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado "Pacman/Tips and tricks (Español)"). Si desea admitir múltiples arquitecturas, se deben tomar precauciones para evitar que se produzcan errores. Cada arquitectura debe tener su propio árbol de directorios:

 `$ tree ~/customrepo/ | sed "s/$(uname -m)/<arch>/g"` 
```
/home/archie/customrepo/
└── <arch>
    ├── customrepo.db -> customrepo.db.tar.xz
    ├── customrepo.db.tar.xz
    ├── customrepo.files -> customrepo.files.tar.xz
    ├── customrepo.files.tar.xz
    └── personal-website-git-b99cce0-1-<arch>.pkg.tar.xz

1 directory, 5 files

```

Luego puede agregar su repositorio colocando lo siguiente en `~/archlive/pacman.conf`, encima de las otras entradas del repositorio (para darle la máxima prioridad):

 `~/archlive/pacman.conf` 
```
...
# custom repository
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch
...
```

El ejecutable *repo-add* verifica si el paquete es apropiado. Si este no es el caso, se encontrará con mensajes de error similares a este:

```
==> ERROR: '/home/archie/customrepo/<arch>/foo-<arch>.pkg.tar.xz' does not have a valid database archive extension.

```

#### Evitar la instalación de paquetes que pertenecen al grupo base

De forma predeterminada, `/usr/bin/mkarchiso`, un script que utiliza `~/archlive/build.sh`, llama a uno de los [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) denominado `pacstrap` sin el indicador `-i`, lo que hace que [Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") no espere la confirmación del usuario para instalar los paquetes durante el proceso de instalación.

Al incluir en la lista negra los paquetes del grupo base agregándolos a la línea `IgnorePkg` en el archivo `~/archlive/pacman.conf`, [Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") pregunta si aún deben instalarse, lo que significa que lo harán cuando se omita la confirmación del usuario. Para deshacerse de estos paquetes hay varias opciones:

*   **Engorroso**: añada el indicador `-i` a cada línea que llame a `pacstrap` en `/usr/bin/mkarchiso`.

*   **Limpio**: cree una copia de `/usr/bin/mkarchiso` en la que agregue el indicador y adapte `~/archlive/build.sh` para que llame a la versión modificada del script de mkarchiso.

*   **Avanzado**: cree una función para `~/archlive/build.sh` que elimine explícitamente los paquetes después de la instalación base. Esto le dejaría la comodidad de no tener que pulsar tantas veces «intro» durante el proceso de instalación.

#### Instalar paquetes de multilib

Para instalar paquetes desde el repositorio [multilib](/index.php/Multilib "Multilib") simplemente descoméntelo del repositorio en `~/archlive/pacman.conf`:

 `pacman.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

### Añadir archivos a la imagen

**Nota:** Debe ser superusuario para hacer esto, no cambie el nombre del usuario titular de ninguno de los archivos que copie, **todo** dentro del directorio airootfs debe ser propiedad de root. El nombre del usuario titular correcto se resolverá automáticamente.

El directorio airootfs actua como una cubierta, piense en él como el directorio raíz, `/`, de su sistema anfitrión, de manera que cada archivo que ponga dentro se copiará al arranque.

Así que, si tiene un conjunto de scripts de iptables en su sistema anfitrión que quiere poder usar en la posterior imagen live, cópielos así:

```
# cp -r /etc/iptables ~/archlive/airootfs/etc

```

Colocar archivos del directorio home del usuario en la imagen live es un poco diferente. No los ponga en `airootfs/home`, en lugar de eso cree un directorio `skel` dentro de `airootfs/` y colóquelos ahí. Después añadiremos las órdenes relevantes al archivo `customize_airootfs.sh` que vamos a crear para copiarlos en el arranque y definir los permisos.

Primero, cree el directorio skel:

```
# mkdir ~/archlive/airootfs/etc/skel

```

Ahora copie los archivos de «home» al directorio skel, por ejemplo para `.bashrc`:

```
# cp ~/.bashrc ~/archlive/airootfs/etc/skel/

```

Cuando se ejecuta `~/archlive/airootfs/root/customize_airootfs.sh` y se crea un nuevo usuario, los archivos del directorio skel se copiarán automáticamente a la nueva carpeta de inicio («home»), con los permisos establecidos correctamente.

De manera similar, es necesario tener cuidado con los archivos de configuración especiales que residen en algún lugar descendiente de la jerarquía. Como ejemplo, el archivo de configuración `/etc/X11/xinit/xinitrc` reside en una ruta que puede sobrescribirse al instalar un paquete. Para emplazar el archivo de configuración, se debe colocar el archivo `xinitrc` personalizado en `~/archlive/airootfs/etc/skel/` y luego modificar `customize_airootfs.sh` para moverlo apropiadamente .

### Cargador de arranque

El archivo por defecto debería funcionar bien, de manera que no debería necesitar tocarlo.

Debido a la naturaleza modular de isolinux, puedes usar un montón de añadidos, ya que todos los archivos `*.c32` se pueden copiar y están disponibles. Eche un vistazo al [sitio oficial de syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) y al [repositorio git de archiso](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Utilizando dichos añadidos, es posible hacer menús visualmente atractivos y complejos. Consulte [esto](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

#### UEFI Secure Boot

Si desea que su Archiso pueda iniciarse en un entorno donde esté activado UEFI Secure Boot, debe usar un cargador de arranque firmado. Puede seguir las instrucciones en [Secure Boot#Using a signed boot loader](/index.php/Secure_Boot#Using_a_signed_boot_loader "Secure Boot").

### Gestor de inicio de sesión

Iniciar X con el arranque el sistema, en un sistema basado en [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), las cosas se manejan activando el archivo *.service* de su gestor de inicio de sesión. Si sabe qué enlace necesita para el archivo *.service* en cuestión: perfecto. Si no, puede averiguarlo fácilmente, en el caso de que esté usando el mismo gestor de pantallas en su sistema. Basta con escribir::

```
# ls -l /etc/systemd/system/display-manager.service

```

Ahora cree el mismo enlace de software en `~/archlive/airootfs/etc/systemd/system`. Para LXDM:

```
# ln -s /usr/lib/systemd/system/lxdm.service ~/archlive/airootfs/etc/systemd/system/display-manager.service

```

Esto activará LXDM al inicio del sistema en su sistema live.

Por otro lado, puede activar el servicio en `airootfs/root/customize_airootfs.sh` junto con otros servicios que estés activados allí.

Si desea que el entorno gráfico se inicie automáticamente durante el arranque, asegúrese de editar `airootfs/root/customize_airootfs.sh` y reemplace

```
systemctl set-default multi-user.target

```

con

```
systemctl set-default graphical.target

```

### Cambiar el acceso automáticamente

La configuración para el inicio de sesión automático de getty se encuentra en `airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf`.

Puede modificar este archivo para cambiar el usuario que inicie sesión automáticamente:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

O elimínelo por completo para desactivar el inicio de sesión automático.

## Compilar la ISO

Ya está listo para poner sus archivos en la .iso, la cual podrá grabar en un CD o USB:

Primero cree el directorio `out/`(opcional, build.sh lo creará si no existe):

```
# mkdir ~/archlive/out/

```

luego dentro de `~/archlive`, ejecute:

```
# ./build.sh -v

```

Este script descargará e instalará los paquetes que especificó en `work/*/airootfs`, creará las imágenes del kernel y de init, aplicará las personalizaciones y finalmente compilará la iso en la carpeta `out/`.

### Reconstruir la ISO

La reconstrucción de la ISO después de las modificaciones no tiene soporte oficial. Sin embargo, es fácilmente factible aplicando dos pasos. Primero tiene que eliminar los archivos de bloqueo presentes en el directorio de trabajo:

```
# rm -v work/build.make_*

```

Además, se requiere editar el script `airootfs/root/customize_airootfs.sh`, y añadir una orden `id` al comienzo de la línea `useradd` como se muestra aquí. De lo contrario, la reconstrucción se detiene en este punto porque el usuario que se va a agregar ya existe [FS#41865](https://bugs.archlinux.org/task/41865).

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

También elimine los datos persistentes, como los usuarios creados, o los enlaces simbólicos, como `/etc/sudoers`.

Las reconstrucciones pueden acelerarse ligeramente editando el script pacstrap (ubicado en /bin/pacstrap) y cambiando lo siguiente en la línea 361:

Antes:

```
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then

```

Después:

```
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then

```

Esto aumenta la velocidad del arranque inicial, ya que no tiene que descargar ni instalar ninguno de los paquetes básicos que ya están instalados.

## Utilizar la ISO

Véase la [Guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") para conocer distintas opciones.

## Véase también

### Documentación y tutoriales

*   [Página del proyecto Archiso](https://projects.archlinux.org/archiso.git)
*   [Documentación oficial](https://projects.archlinux.org/archiso.git/tree/docs)

### Ejemplo de plantilla personalizada

*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://easy.open.and.free.fr/didjix/)

### Crear una ISO de instalación sin conexión

*   [Archiso offline](/index.php/Archiso_offline "Archiso offline")
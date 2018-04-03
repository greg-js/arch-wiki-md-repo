Artículos relacionados

*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")

**Estado de la traducción:** este artículo es una versión traducida de [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting"). Fecha de la última traducción/revisión: **2016-04-10**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=General_troubleshooting&diff=0&oldid=430728).

Este artículo explica algunos métodos para solucionar problemas de forma general. Para cuestiones específicas relativas a una aplicación, remítase a la página de la wiki para ese programa en particular.

## Contents

*   [1 Procedimientos generales](#Procedimientos_generales)
    *   [1.1 Preste atención al detalle](#Preste_atenci.C3.B3n_al_detalle)
    *   [1.2 Interróguese a sí mismo](#Interr.C3.B3guese_a_s.C3.AD_mismo)
    *   [1.3 Sea más específico](#Sea_m.C3.A1s_espec.C3.ADfico)
    *   [1.4 Obtenga apoyo adicional](#Obtenga_apoyo_adicional)
*   [2 Problemas de arranque](#Problemas_de_arranque)
    *   [2.1 Pantalla en blanco con el vídeo Intel](#Pantalla_en_blanco_con_el_v.C3.ADdeo_Intel)
    *   [2.2 Atascado mientras se carga el kernel](#Atascado_mientras_se_carga_el_kernel)
    *   [2.3 Sistema no arrancable](#Sistema_no_arrancable)
    *   [2.4 Depurar errores de módulos del kernel](#Depurar_errores_de_m.C3.B3dulos_del_kernel)
    *   [2.5 Depurar errores de hardware](#Depurar_errores_de_hardware)
*   [3 Administrar paquetes](#Administrar_paquetes)
*   [4 fuser](#fuser)
*   [5 Permisos de sesión](#Permisos_de_sesi.C3.B3n)
*   [6 error while loading shared libraries](#error_while_loading_shared_libraries)
*   [7 file: could not find any magic files!](#file:_could_not_find_any_magic_files.21)
*   [8 La revisión ortográfica marca todo el texto como incorrecto](#La_revisi.C3.B3n_ortogr.C3.A1fica_marca_todo_el_texto_como_incorrecto)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Procedimientos generales

### Preste atención al detalle

Con el fin de resolver un problema que le ha surgido, es *absolutamente crucial* comprender bien cómo funciona el sistema específico. Cómo funciona y qué necesita para funcionar sin errores. Si no puede contestar cómodamente estas preguntas, entonces se aconseja encarecidamente que revise el artículo de [Archwiki](/index.php/Table_of_contents "Table of contents") para conocer la función respecto de la que está teniendo problemas. Una vez que considere que ha entendido el sistema específico, será más fácil que pueda precisar la problema.

### Interróguese a sí mismo

A continuación se presentan una serie de preguntas que deberá hacerse a sí mismo cada vez que surjan problemas en el funcionamiento del sistema. Bajo cada pregunta hay notas que explican el método para dar respuesta a cada pregunta, seguido de algunos ejemplos claros sobre cómo recopilar fácilmente la salida de datos y qué herramientas se pueden utilizar para revisar los registros y el diario (*journal*).

1.  ¿Cuál es el problema?

    	Sea *lo más preciso posible* . Esto le ayudará a que no se confunda y/o que no siga un camino equivocado cuando se esté buscando información específica.

2.  ¿Hay mensajes de error? (si los hay)

    	Copie las *salidas completas* que contienen los **mensajes de error** relacionadas con su problema , y péguelas en un archivo separado como `$HOME/issue.log`. Por ejemplo, para enviar la salida de la siguiente orden de [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") a `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  ¿Se puede reproducir el problema?

    	Si es así, indique *exactamente* **paso a paso** las instrucciones/órdenes necesarias para reproducirlo.

4.  ¿Cuándo se encontró por primera vez el problema, y qué ha cambiando entre ese momento y antes de que el sistema comenzase a funcionar erróneamente?

    	Si se produjo justo después de una actualización, entonces, liste **todos los paquetes que se han actualizado**. Incluya, también, los *números de versión*, copiando toda la actualización de [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`). También tome nota de los estados de *cualquier* servicio(s) que se necesita para dar soporte a la aplicación(s) que está funcionando mal, usando las herramientas systemctl de [systemd](/index.php/Systemd "Systemd"). Por ejemplo, para enviar la salida de la siguiente orden de [systemd](/index.php/Systemd#Basic_systemctl_usage "Systemd") a `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Nota:** Utilice el signo `**>>**` para asegurarse de que cualquier texto presente en `$HOME/issue.log` no se sobrescribirá.

### Sea más específico

Cuando se trate de resolver un problema, **nunca** se aproxime al mismo con expresiones como:

*Aplicación X no funciona.*

En su lugar, mírelo en su totalidad:

*La aplicación X produce el error Y al realizar las tareas Z en condiciones A y B.*

### Obtenga apoyo adicional

Ahora tiene toda la información disponible. Con ello debe tener una buena idea de lo que está pasando en su sistema. Y se puede empezar a trabajar en una solución adecuada.

Si necesita ayuda adicional, puede encontrarla en los [foros](https://bbs.archlinux.org) o en IRC en irc.freenode.net #archlinux

## Problemas de arranque

Véase [Boot debugging](/index.php/Boot_debugging "Boot debugging") para recuperar información adicional.

### Pantalla en blanco con el vídeo Intel

Esto es muy probablemente debido a un problema con la [configuración de la modalidad del kernel](/index.php/Kernel_mode_setting "Kernel mode setting"). Pruebe [desactivar modesetting](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") o cambiar el [puerto del vídeo](/index.php/Intel#KMS_Issue:_console_is_limited_to_small_area "Intel").

### Atascado mientras se carga el kernel

Pruebe a desactivar ACPI mediante la adición de `acpi=off` a los parámetros del kernel.

### Sistema no arrancable

Si el sistema no arranca en absoluto, simplemente arranque desde una [imagen live](https://www.archlinux.org/download/) y [realice chroot](/index.php/Change_root "Change root") para iniciar sesión en el sistema y solucionar el problema.

### Depurar errores de módulos del kernel

Véase [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules").

### Depurar errores de hardware

Véase [udev#Debug output](/index.php/Udev#Debug_output "Udev").

## Administrar paquetes

Véase [Pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman") para temas generales, y [pacman/Package signing#Troubleshooting](/index.php/Pacman/Package_signing#Troubleshooting "Pacman/Package signing") para los problemas con las claves PGP.

## fuser

*fuser* es una utilidad de línea de órdenes para la identificación de los procesos que utilizan recursos como archivos, sistemas de archivos y puertos TCP/UDP.

*fuser* es proporcionado por el paquete [psmisc](https://www.archlinux.org/packages/?name=psmisc), que debe estar ya instalado como parte del grupo [base](https://www.archlinux.org/groups/x86_64/base/).

## Permisos de sesión

**Nota:** Debe utilizar [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como su sistema de inicio para que las sesiones locales funcionen [[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) —que se requiere para que [polkit](https://en.wikipedia.org/wiki/es:PolicyKit "wikipedia:es:PolicyKit") y [ACL](https://en.wikipedia.org/wiki/es:Lista_de_control_de_acceso "wikipedia:es:Lista de control de acceso") puedan definir permisos para distintos dispositivos (ver `/usr/lib/udev/rules.d/70-uaccess.rules` y [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))—.

En primer lugar, asegúrese de que tiene una sesión local válida dentro de X:

```
$ loginctl show-session $XDG_SESSION_ID

```

Esta debe contener `Remote=no` y `Active=yes` en la salida. Si no es así, asegúrese de que X se ejecuta en la misma tty donde se produjo el inicio de sesión. Esto es necesario a fin de preservar la sesión iniciada. Esto es manejado de forma predeterminada por `/etc/X11/xinit/xserverrc`.

También debe iniciarse una sesión de D-Bus junto con X. Véase [D-Bus (Español)#Iniciar la sesión de usuario](/index.php/D-Bus_(Espa%C3%B1ol)#Iniciar_la_sesi.C3.B3n_de_usuario "D-Bus (Español)") para más información sobre esto.

Las acciones [polkit](/index.php/Polkit "Polkit") no requieren una configuración posterior. Algunas acciones polkit requieren una autenticación adicional, incluso con una sesión local. Un agente de autenticación polkit debe estar en ejecución para que esto funcione. Ver [Agentes de autenticación](/index.php/Polkit#Authentication_agents "Polkit") para más información sobre esto.

## error while loading shared libraries

Si, durante el uso de un programa, se produce un error similar al siguiente:

```
error while loading shared libraries: libusb-0.1.so.4: cannot open shared object file: No such file or directory

```

Utilice [pacman](/index.php/Pacman "Pacman") o [pkgfile](/index.php/Pkgfile "Pkgfile") para buscar el paquete al cual pertenece la biblioteca que falta:

 `$ pacman -Fs libusb-0.1.so.4` 
```
extra/libusb-compat 0.1.5-1
    usr/lib/libusb-0.1.so.4

```

En este caso, el paquete [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) necesita ser [instalado](/index.php/Installed "Installed").

El error también puede significar que el paquete que ha utilizado para instalar el programa no enumera la biblioteca como una dependencia en su [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"): si se trata de un paquete oficial, [informe del error](/index.php/Report_a_bug "Report a bug"); si se trata de un paquete de [AUR](/index.php/AUR "AUR"), informe a su mantenedor en su página del sitio web de AUR.

## file: could not find any magic files!

*Ejemplo:* después de una actualización o de la instalación de un paquete le da el siguiente error:

```
# file: could not find any magic files!

```

Lo más probable es que el sistema haya quedado inoperativo. Y, cualquier intento de recompilar/reinstalar el paquete(s) responsable de la rotura se traducirá en un error. Además, cualquier intento para tratar de reconstruir [initramfs](/index.php/Mkinitcpio "Mkinitcpio") resultará en lo siguiente:

```
# mkinitcpio -p linux
==> Building image from preset: 'default'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux.img
file: could not find any magic files!
==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'
==> Building image from preset: 'fallback'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-fallback.img -S autodetect
file: could not find any magic files!
@==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'

```

Por lo general, una aplicación previamente instalada habrá colocado un archivo de configuración dentro de `/etc/ld.so.conf.d/` o habrá hecho cambios en `/etc/ld.so.conf` que no son ahora válidos.

1.  Arranque con el CD live/soporte de instalación de Arch Linux.
2.  Monte su partición root (`**/**`) en `/mnt` y, usando [arch-chroot](/index.php/Change_root#Change_root "Change root"), efectúe [chroot](/index.php/Change_root "Change root") en su sistema.
    **Nota:** [arch-chroot](/index.php/Change_root#Change_root "Change root") deja montar la partición `/boot` por el usuario.

3.  Examine `/etc/ld.so.conf` y elimine cualquier línea no válida que se encuentre.
4.  Examine Los archivos que se encuentran dentro del directorio `/etc/ld.so.conf.d/` y elimine todos los archivos no válidos.
5.  Reconstruya [initramfs](/index.php/Initramfs "Initramfs"): ` # mkinitcpio -p linux` 
6.  Reinicie y entre de nuevo en el sistema instalado.
7.  Una vez reiniciado, vuelva a instalar el paquete que era responsable de dejar el sistema inoperativo con: ` # pacman -S <paquete>` 

## La revisión ortográfica marca todo el texto como incorrecto

¿Ha instalado un diccionario [aspell](https://www.archlinux.org/packages/?name=aspell)? Utilice `pacman -Ss aspell` para ver los diccionarios disponibles para su descarga.

Si la instalación de los archivos de diccionario no ha podido solucionar el problema, lo más probable es que sea un problema con `enchant`. Compruebe si hay archivos de diccionario conocidos:

 `$ aspell dicts` 
```
en
en_GB
...etc
```

Si el diccionario de la lengua en cuestión aparece, añádalo a `/usr/share/enchant/enchant.ordering`. En el ejemplo anterior, sería:

```
en_GB:aspell

```

## Véase también

*   [Fix the Most Common Problems](http://www.tuxradar.com/content/how-fix-most-common-linux-problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)
Este artículo explica algunos métodos para solucionar problemas de forma general. Para cuestiones específicas relativas a una aplicación, remítase a la página de la wiki para ese programa en particular.

## Contents

*   [1 Preste atención al detalle](#Preste_atenci.C3.B3n_al_detalle)
*   [2 Interróguese a sí mismo](#Interr.C3.B3guese_a_s.C3.AD_mismo)
*   [3 Sea más específico](#Sea_m.C3.A1s_espec.C3.ADfico)
*   [4 Obtenga apoyo adicional](#Obtenga_apoyo_adicional)
*   [5 Compruebe los permisos de sesión](#Compruebe_los_permisos_de_sesi.C3.B3n)
*   [6 Acceda en modo usuario único](#Acceda_en_modo_usuario_.C3.BAnico)
*   [7 Ejemplos específicos](#Ejemplos_espec.C3.ADficos)
    *   [7.1 Solución](#Soluci.C3.B3n)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Preste atención al detalle

Con el fin de resolver un problema que le ha surgido, es _absolutamente crucial_ comprender bien cómo funciona el sistema específico. Cómo funciona y qué necesita para funcionar sin errores. Si no puede contestar cómodamente estas preguntas, entonces se aconseja encarecidamente que revise el artículo de [Archwiki](/index.php/Table_of_contents "Table of contents") para conocer la función respecto de la que está teniendo problemas. Una vez que considere que ha entendido el sistema específico, será más fácil que pueda precisar la problema.

## Interróguese a sí mismo

A continuación se presentan una serie de preguntas de debe hacerse a sí mismo cada vez que surjan problemas en el funcionamiento del sistema. Bajo cada pregunta hay notas que explican el método para dar respuesta a cada pregunta, seguido de algunos ejemplos claros sobre cómo recopilar fácilmente la salida de datos y qué herramientas se pueden utilizar para revisar los registros y el diario (_journal_).

1.  ¿Cuál es el problema?

    	Sea _lo más preciso posible_ . Esto le ayudará a que no se confunda y/o que no siga un camino equivocado cuando se esté buscando información específica.

2.  ¿Hay mensajes de error? (si los hay)

    	Copie las _salidas completas_ que contienen los **mensajes de error** relacionadas con su problema , y péguelas en un archivo separado como `$HOME/issue.log`. Por ejemplo, para enviar la salida de la siguiente orden de [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") a `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  ¿Se puede reproducir el problema?

    	Si es así, indique _exactamente_ **paso a paso** las instrucciones/órdenes necesarias para reproducirlo.

4.  ¿Cuándo se encontró por primera vez el problema, y qué ha cambiando entre ese momento y antes de que el sistema comenzase a funcionar erróneamente?

    	Si se produjo justo después de una actualización, entonces, liste **todos los paquetes que se han actualizado**. Incluya, también, los _números de versión_, copiando toda la actualización de [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`). También tome nota de los estados de _cualquier_ servicio(s) que se necesita para dar soporte a la aplicación(s) que está funcionando mal, usando las herramientas systemctl de [systemd](/index.php/Systemd "Systemd"). Por ejemplo, para enviar la salida de la siguiente orden de [systemd](/index.php/Systemd#Basic_systemctl_usage "Systemd") a `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Nota:** Utilice el signo `**>>**` para asegurarse de que cualquier texto presente en `$HOME/issue.log` no se sobrescribirá.

## Sea más específico

Cuando se trate de resolver un problema, **nunca** se aproxime al mismo con expresiones como:

_Aplicación X no funciona._

En su lugar, mírelo en su totalidad:

_Aplicación X produce error Y al realizar las tareas Z en condiciones A y B._

## Obtenga apoyo adicional

Ahora tiene toda la información disponible. Con ello debe tener una buena idea de lo que está pasando en su sistema. Y se puede empezar a trabajar en una solución adecuada.

Si necesita ayuda adicional, puede encontrarla en los [foros](https://bbs.archlinux.org) o en IRC en irc.freenode.net #archlinux

## Compruebe los permisos de sesión

**Nota:** Debe utilizar [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como su sistema de inicio para que las sesiones locales funcionen —que se requiere para que [polkit](https://en.wikipedia.org/wiki/es:PolicyKit "wikipedia:es:PolicyKit") y [ACL](https://en.wikipedia.org/wiki/es:Lista_de_control_de_acceso "wikipedia:es:Lista de control de acceso") puedan definir permisos para distintos dispositivos (ver `/usr/lib/udev/rules.d/70-uaccess.rules` y [[1]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))—.

En primer lugar, asegúrese de que tiene una sesión local válida dentro de X:

```
$ loginctl show-session $XDG_SESSION_ID

```

Esta debe contener `Remote=no` y `Active=yes` en la salida. Si no es así, asegúrese de que X se ejecuta en la misma tty donde se produjo el inicio de sesión. Esto es necesario a fin de preservar la sesión iniciada. Esto es manejado de forma predeterminada por `/etc/X11/xinit/xserverrc`.

También debe iniciarse una sesión de D-Bus junto con X. Véase [D-Bus (Español)#Iniciar la sesión de usuario](/index.php/D-Bus_(Espa%C3%B1ol)#Iniciar_la_sesi.C3.B3n_de_usuario "D-Bus (Español)") para más información sobre esto.

Las acciones [polkit](/index.php/Polkit "Polkit") no requieren una configuración posterior. Algunas acciones polkit requieren una autenticación adicional, incluso con una sesión local. Un agente de autenticación polkit debe estar en ejecución para que esto funcione. Ver [Agentes de autenticación](/index.php/Polkit#Authentication_agents "Polkit") para más información sobre esto.

## Acceda en modo usuario único

Si no puede arrancar debido a los errores causados por un demonio, gestor de pantallas o Xorg, tendría que ser capaz de utilizar el [runlevel](/index.php/Runlevels "Runlevels") de usuario único:

1.  Arranque en modo single-user. Para GRUB(2):
    1.  En el menú de arranque GRUB(2), seleccione la entrada de Arch Linux, y pulse `e` para editarlo.
    2.  Encuentra la línea del kernel; se iniciará con `linux /boot/vmlinuz-linux...`
    3.  Añada `1` o `s` al final de esta línea
    4.  Presione F2 para iniciar el proceso de arranque
2.  Después desactive el servicio de [systemd](/index.php/Systemd "Systemd") que está causando el problema.
3.  Cambie al [target](/index.php/Systemd#Targets "Systemd") de modo multi-user de systemd.
4.  A continuación, intente localizar el problema ejecutando el servicio manualmente.

## Ejemplos específicos

_Ejemplo:_ Después de una actualización o de la instalación de un paquete le da el siguiente error:

```
# file: could not find any magic files!
<small>_«archivo: no se pudo encontrar ningún archivo mágico»_</small>

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

### Solución

Por lo general, una aplicación previamente instalada habrá colocado un archivo de configuración dentro de `/etc/ld.so.conf.d/` o habrá hecho cambios en `/etc/ld.so.conf` que no son ahora válidos.

1.  Arranque con el CD live/soporte de instalación de Arch Linux.
2.  Monte su partición root (`**/**`) en `/mnt` y, usando [arch-chroot](/index.php/Change_root#Change_root "Change root"), efectúe [chroot](/index.php/Change_root "Change root") en su sistema.
    **Nota:** [arch-chroot](/index.php/Change_root#Change_root "Change root") deja montar la partición `/boot` por el usuario.

3.  Examine `/etc/ld.so.conf` y elimine cualquier línea no válida que se encuentre.
4.  Examine Los archivos que se encuentran dentro del directorio `/etc/ld.so.conf.d/` y elimine todos los archivos no válidos.
5.  Reconstruya [initramfs](/index.php/Initramfs "Initramfs"): ` # mkinitcpio -p linux` 
6.  Reinicie y entre de nuevo en su sistema instalado.
7.  Una vez reiniciado, vuelva a instalar el paquete que era responsable de dejar el sistema inoperativo con: ` # pacman -S <paquete>` 

## Véase también

*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Fix the Most Common Problems](http://www.maximumpc.com/article/features/linux_troubleshooting_guide_fix_most_common_problems)
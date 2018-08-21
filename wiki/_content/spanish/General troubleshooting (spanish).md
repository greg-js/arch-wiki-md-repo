**Estado de la traducción:** este artículo es una versión traducida de [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting"). Fecha de la última traducción/revisión: **2018-08-18**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=General_troubleshooting&diff=0&oldid=516784).

Artículos relacionados

*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")

Este artículo explica algunos métodos para solucionar problemas generales. Para cuestiones específicas relativas a una aplicación, remítase a la página wiki para ese programa en particular.

## Contents

*   [1 Procedimientos generales](#Procedimientos_generales)
    *   [1.1 Atención al detalle](#Atenci.C3.B3n_al_detalle)
    *   [1.2 Preguntas/lista de control](#Preguntas.2Flista_de_control)
    *   [1.3 Enfoque](#Enfoque)
    *   [1.4 Soporte adicional](#Soporte_adicional)
*   [2 Problemas de arranque](#Problemas_de_arranque)
    *   [2.1 Mensajes de la consola](#Mensajes_de_la_consola)
        *   [2.1.1 Control de flujo](#Control_de_flujo)
        *   [2.1.2 Desplazamiento hacia atrás](#Desplazamiento_hacia_atr.C3.A1s)
        *   [2.1.3 Salida de depuración](#Salida_de_depuraci.C3.B3n)
    *   [2.2 Shell de recuperación](#Shell_de_recuperaci.C3.B3n)
    *   [2.3 Pantalla en blanco con una tarjeta gráfica Intel](#Pantalla_en_blanco_con_una_tarjeta_gr.C3.A1fica_Intel)
    *   [2.4 Atascado mientras se carga el núcleo](#Atascado_mientras_se_carga_el_n.C3.BAcleo)
    *   [2.5 Sistema no arrancable](#Sistema_no_arrancable)
    *   [2.6 Depurar los errores de los módulos del núcleo](#Depurar_los_errores_de_los_m.C3.B3dulos_del_n.C3.BAcleo)
    *   [2.7 Depurar errores de hardware](#Depurar_errores_de_hardware)
*   [3 Administrar paquetes](#Administrar_paquetes)
*   [4 fuser](#fuser)
*   [5 Permisos de sesión](#Permisos_de_sesi.C3.B3n)
*   [6 error while loading shared libraries](#error_while_loading_shared_libraries)
*   [7 file: could not find any magic files!](#file:_could_not_find_any_magic_files.21)
*   [8 La revisión ortográfica marca todo el texto como incorrecto](#La_revisi.C3.B3n_ortogr.C3.A1fica_marca_todo_el_texto_como_incorrecto)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Procedimientos generales

### Atención al detalle

Para resolver un problema que esté teniendo, es *absolutamente crucial* comprender básicamente cómo funciona ese subsistema específico. ¿Cómo funciona y qué necesita para ejecutarse sin error? Si no puede contestar cómodamente a estas preguntas, entonces es mejor que revise el artículo [Archwiki](/index.php/Table_of_contents_(Espa%C3%B1ol) "Table of contents (Español)") del subsistema con el que tiene problemas. Una vez que sienta que lo ha entendido, le será más fácil identificar la causa del problema.

### Preguntas/lista de control

A continuación se presentan una serie de preguntas que deberá hacerse a sí mismo cuando se trata de un sistema que no funciona bien. Debajo de cada pregunta, hay notas que explican el método para dar respuesta a cada pregunta, seguido de algunos ejemplos claros sobre cómo recopilar fácilmente los datos y qué herramientas se pueden usar para revisar los registros y el diario *(journal)*.

1.  ¿Cuál es el problema?

    	Sea *lo más preciso posible*. Esto le ayudará a no confundirse y/o no seguir un camino incorrecto cuando al buscar información específica.

2.  ¿Hay mensajes de error? (si los hay)

    	Copie y pegue las *salidas completas* que contienen los **mensajes de error** relacionadas con su problema en un archivo separado como `$HOME/issue.log`. Por ejemplo, para enviar la salida de la siguiente orden de [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") a `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  ¿Puede reproducir el problema?

    	Si es así, indique *exactamente* **paso a paso** las/os instrucciones/comandos necesarias/os para reproducirlo.

4.  ¿Cuándo se encontró por primera vez con este problema, y qué cambió entre ese momento y antes de que el sistema comenzase a funcionar erróneamente?

    	Si ocurrió justo después de una actualización, enumere **todos los paquetes que se han actualizado**. Incluya los *números de versión*, copiando toda la actualización de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").log (`/var/log/pacman.log`). También tome nota de los estados de *cualquier* servicio necesario para dar soporte a la(s) aplicación(es) que está funcionando mal, usando las herramientas systemctl de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). Por ejemplo, para reenviar la salida del siguiente comando de [systemd](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") a `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Nota:** Utilizar `**>>**` asegurará que cualquier texto presente en `$HOME/issue.log` no se sobrescribirá.

### Enfoque

En lugar de abordar un problema diciendo,

*La aplicación X no funciona.*

le resultará más útil formular su problema en el contexto del sistema como un todo, como:

*La aplicación X produce el/los error(es) Y al realizar las tareas Z bajo las condiciones A y B.*

### Soporte adicional

Con toda la información delante suya, debe tener una buena idea de lo que está sucediendo con el sistema y ahora puede comenzar a trabajar en una solución adecuada.

Si necesita soporte adicional, puede encontrarlo en [los foros](https://bbs.archlinux.org) o el IRC en irc.freenode.net #archlinux. Consulte [Canales de IRC](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") para otras opciones.

**Nota:** [Soporte *solo* para la distribución Arch Linux](/index.php/Code_of_conduct_(Espa%C3%B1ol)#Soporte_.2Asolo.2A_para_la_distribuci.C3.B3n_Arch_Linux "Code of conduct (Español)") y no [Distribuciones basadas en Arch](/index.php/Arch-based_distributions_(Espa%C3%B1ol) "Arch-based distributions (Español)").

Cuando solicite ayuda, publique las salidas/registros completas/os, no solo las secciones que considere importantes. Las fuentes de información incluyen:

*   Salida completa de cualquier comando involucrado - no seleccione únicamente lo que considere relevante.
*   Salida de `journalctl` de systemd. Para una salida más extensa, utilice el parámetro de arranque `systemd.log_level=debug`.
*   Archivos de registro (eche un vistazo a `/var/log`)
*   Archivos de configuración relevantes
*   Controladores involucrados
*   Versiones de paquetes involucrados
*   Núcleo: `dmesg`. Para un problema de arranque, al menos las últimas 10 líneas mostradas, preferiblemente más
*   Redes: Salida exacta de los comandos involucrados, y cualquier archivo de configuración
*   Xorg: `/var/log/Xorg.0.log`, y registros *(logs)* anteriores si ha sobrescrito el problemático
*   Pacman: si una actualización reciente rompió algo, busque en `/var/log/pacman.log`

Una de las mejores formas de publicar esta información es usar un *pastebin* en línea. Puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [pbpst](https://www.archlinux.org/packages/?name=pbpst) o [gist](https://www.archlinux.org/packages/?name=gist) para enviar información automáticamente. Por ejemplo, para enviar el contenido de su diario systemd desde este arranque, debe hacer lo siguiente:

```
# journalctl -xb | pbpst -S

```

Luego se mostrará un enlace que puede pegar en el foro o IRC.

Además, antes de publicar su pregunta, puede revisar [cómo hacer preguntas inteligentes](http://www.catb.org/esr/faqs/smart-questions.html). Consulte también [Código de conducta](/index.php/Code_of_conduct_(Espa%C3%B1ol) "Code of conduct (Español)").

## Problemas de arranque

El diagnóstico de errores durante el [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)") implica cambiar los [parámetros del núcleo](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") y reiniciar el sistema.

Si no es posible arrancar el sistema, inicie desde una [imagen en vivo](https://www.archlinux.org/download/) y [cambie la raíz](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") al sistema existente.

### Mensajes de la consola

Después del proceso de inicio, la pantalla se borra y aparece el mensaje de inicio de sesión, lo que deja a los usuarios incapaces de leer los mensajes del arranque y los de error. Este comportamiento predeterminado puede cambiarse utilizando los métodos descritos en las secciones siguientes.

Tenga en cuenta que, independientemente de la opción elegida, los mensajes del núcleo pueden mostrarse para su inspección después del arranque utilizando `dmesg` o todos los registros del arranque actual con `journalctl -b`.

#### Control de flujo

Esta es una administración básica que se aplica a la mayoría de los emuladores de terminal, incluidas las consolas virtuales (vc):

*   Pulse `Ctrl+S` para pausar la salida
*   Y `Ctrl+Q` para reanudarla

Esto pausa no solo la salida, sino también los programas que intentan imprimir en el terminal, ya que bloquearán sobre las llamadas `write()` mientras la salida esté en pausa. Si su *init* parece congelado, asegúrese de que la consola del sistema no esté en pausa.

Para ver los mensajes de error que ya han mostrado, consulte [Haga que los mensajes de inicio permanezcan en tty1](/index.php/Getty#Have_boot_messages_stay_on_tty1 "Getty").

#### Desplazamiento hacia atrás

El desplazamiento hacia atrás *(scrollback)* permite al usuario retroceder y ver el texto que se desplazó de la pantalla de una consola de texto. Esto es posible gracias a un búfer creado entre el adaptador de vídeo y el dispositivo de visualización llamado búfer de desplazamiento. Por defecto, las combinaciones de teclas `Shift+PageUp` y `Shift+PageDown` desplazan el búfer hacia arriba y hacia abajo respectivamente.

Si al desplazarse hacia arriba hasta el final no le muestra la información suficiente, necesita expandir su búfer de desplazamiento para tener más salida. Esto se hace ajustando la consola de framebuffer del núcleo (fbcon) con el [parámetro del núcleo](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `fbcon=scrollback:Nk` donde `N` es el tamaño de búfer deseado es kilobytes. El tamaño predeterminado es 32k.

Si esto no le funciona, es posible que su consola de framebuffer no esté habilitada correctamente. Consulte la [documentación sobre la consola de framebuffer](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) para conocer otros parámetros, por ejemplo para cambiar el controlador de framebuffer.

#### Salida de depuración

La mayoría de los mensajes del núcleo están ocultos durante el arranque. Puede ver más de estos mensajes añadiendo diferentes parámetros de núcleo. Los más simples son:

*   `debug` habilita los mensajes de depuración tanto para el núcleo como para [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   `ignore_loglevel` fuerza a que se impriman todos los mensajes del núcleo

Otros parámetros que puede añadir y que podrían ser útiles en ciertas situaciones son:

*   `earlyprintk=vga,keep` imprime los primeros mensajes en el proceso de arranque del núcleo, en caso de que el núcleo falle antes de que se muestre el resultado. Debe cambiar `vga` a `efi` para los sistemas [EFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   `log_buf_len=16M` asigna un búfer de mensajes del núcleo más grande (16MB), para garantizar que la salida de depuración no se sobrescriba

También hay una serie de parámetros de depuración separados para permitir la depuración en subsistemas específicos, poe ejemplo `bootmem_debug`, `sched_debug`. Consulte la [documentación de los parámetros del núcleo](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt) para obtener información específica.

**Nota:** Si no puede desplazarse hacia atrás lo suficiente para ver la salida del arranque deseada, debe aumentar el tamaño del [búfer del desplazamiento hacia atrás](#Desplazamiento_hacia_atr.C3.A1s).

### Shell de recuperación

Obtener un shell interactivo en algún momento del proceso de arranque puede ayudarle a identificar exactamente dónde y por qué está fallando algo. Hay varios parámetros del núcleo para hacerlo, pero todos ellos lanzan un shell normal que le permite ejecutar `exit`, lo que posibilita al núcleo reanudar lo que estaba haciendo:

*   `rescue` inicia un shell poco después de que el sistema de archivos raíz se vuelva a leer/escribir
*   `emergency` inicia un shell incluso más temprano, antes de que se instalen la mayoría de los sistemas de archivos
*   `init=/bin/sh` (como último recurso) cambia el programa init a un shell de superusuario *(root)*. `rescue` y `emergency` dependen de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), pero esto debería funcionar incluso si *systemd* falla

Otra opción es el shell de depuración de systemd que añade un shell de superusuario en `tty9` (accesible con Ctrl+Alt+F9). Se puede habilitar añadiendo `systemd.debug-shell` a los [parámetros del núcleo](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), o [habilitando](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `debug-shell.service`. Asegúrese de desactivar el servicio cuando lo haya hecho para evitar el riesgo de seguridad por dejar abierto un shell de superusuario en cada arranque.

### Pantalla en blanco con una tarjeta gráfica Intel

Esto es debido muy probablemente a un problema con la [configuración del modo del núcleo](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)"). Pruebe a [desactivar modesetting](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Desactivar_modesetting "Kernel mode setting (Español)") o cambiar el [puerto de la tarjeta gráfica](/index.php/Intel_graphics_(Espa%C3%B1ol)#Problema_KMS:_la_consola_est.C3.A1_limitada_a_una_peque.C3.B1a_porci.C3.B3n_de_la_pantalla "Intel graphics (Español)").

### Atascado mientras se carga el núcleo

Pruebe a desactivar ACPI añadiendo `acpi=off` a los parámetros del núcleo.

### Sistema no arrancable

Si el sistema no arranca en absoluto, simplemente arranque desde una [imagen live](https://www.archlinux.org/download/) y [realice chroot](/index.php/Change_root "Change root") para iniciar sesión en el sistema y solucionar el problema.

### Depurar los errores de los módulos del núcleo

Consulte esta sección sobre [como obtener información](/index.php/Kernel_modules_(Espa%C3%B1ol)#Obtener_informaci.C3.B3n "Kernel modules (Español)") de los módulos del núcleo.

### Depurar errores de hardware

*   Puede visualizar información adicional de depuración sobre su hardware siguiendo [udev#Debug output](/index.php/Udev#Debug_output "Udev").
*   Asegúrese de que las actualizaciones de [microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") se aplican en su sistema.
*   Pruebe la memoria RAM de su dispositivo con [Memtest86+](http://www.memtest.org/). La RAM inestable puede ocasionar algunos problemas extremadamente extraños, que van desde fallos aleatorias hasta la corrupción de datos.

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
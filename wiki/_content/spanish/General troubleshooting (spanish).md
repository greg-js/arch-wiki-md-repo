**Estado de la traducción**
Este artículo es una traducción de [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting"), revisada por última vez el **2018-09-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=General_troubleshooting&diff=0&oldid=543735) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")
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
    *   [2.4 Atascado mientras se carga el kernel](#Atascado_mientras_se_carga_el_kernel)
    *   [2.5 Sistema no arrancable](#Sistema_no_arrancable)
    *   [2.6 Depurar los errores de los módulos del kernel](#Depurar_los_errores_de_los_m.C3.B3dulos_del_kernel)
    *   [2.7 Depurar errores de hardware](#Depurar_errores_de_hardware)
*   [3 Kernel panics](#Kernel_panics)
    *   [3.1 Examinar los mensajes de pánico](#Examinar_los_mensajes_de_p.C3.A1nico)
        *   [3.1.1 Escenario de ejemplo: módulo defectuoso](#Escenario_de_ejemplo:_m.C3.B3dulo_defectuoso)
    *   [3.2 Reiniciar en una shell de superusuario y solucionar el problema](#Reiniciar_en_una_shell_de_superusuario_y_solucionar_el_problema)
*   [4 Administrar paquetes](#Administrar_paquetes)
*   [5 fuser](#fuser)
*   [6 Permisos de sesión](#Permisos_de_sesi.C3.B3n)
*   [7 Mensaje: "error while loading shared libraries"](#Mensaje:_.22error_while_loading_shared_libraries.22)
*   [8 Mensaje: "file: could not find any magic files!"](#Mensaje:_.22file:_could_not_find_any_magic_files.21.22)
    *   [8.1 Problema](#Problema)
    *   [8.2 Solución](#Soluci.C3.B3n)
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

Si necesita soporte adicional, puede encontrarlo en [los foros](https://bbs.archlinux.org) o el IRC en irc.freenode.net #archlinux. Véase [Canales de IRC](/index.php/IRC_channel_(Espa%C3%B1ol) "IRC channel (Español)") para otras opciones.

**Nota:** [Soporte *solo* para la distribución Arch Linux](/index.php/Code_of_conduct_(Espa%C3%B1ol)#Soporte_.2Asolo.2A_para_la_distribuci.C3.B3n_Arch_Linux "Code of conduct (Español)") y no [Distribuciones basadas en Arch](/index.php/Arch-based_distributions_(Espa%C3%B1ol) "Arch-based distributions (Español)").

Cuando solicite ayuda, publique las salidas/registros completas/os, no solo las secciones que considere importantes. Las fuentes de información incluyen:

*   Salida completa de cualquier comando involucrado - no seleccione únicamente lo que considere relevante.
*   Salida de `journalctl` de systemd. Para una salida más extensa, utilice el parámetro de arranque `systemd.log_level=debug`.
*   Archivos de registro (eche un vistazo a `/var/log`)
*   Archivos de configuración relevantes
*   Controladores involucrados
*   Versiones de paquetes involucrados
*   Kernel: `dmesg`. Para un problema de arranque, al menos las últimas 10 líneas mostradas, preferiblemente más
*   Redes: Salida exacta de los comandos involucrados, y cualquier archivo de configuración
*   Xorg: `/var/log/Xorg.0.log`, y registros *(logs)* anteriores si ha sobrescrito el problemático
*   Pacman: si una actualización reciente rompió algo, busque en `/var/log/pacman.log`

Una de las mejores formas de publicar esta información es usar un *pastebin* en línea. Puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [pbpst](https://www.archlinux.org/packages/?name=pbpst) o [gist](https://www.archlinux.org/packages/?name=gist) para enviar información automáticamente. Por ejemplo, para enviar el contenido de su diario systemd desde este arranque, debe hacer lo siguiente:

```
# journalctl -xb | pbpst -S

```

Luego se mostrará un enlace que puede pegar en el foro o IRC.

Además, antes de publicar su pregunta, puede revisar [cómo hacer preguntas inteligentes](http://www.catb.org/esr/faqs/smart-questions.html). Véase también [Código de conducta](/index.php/Code_of_conduct_(Espa%C3%B1ol) "Code of conduct (Español)").

## Problemas de arranque

El diagnóstico de errores durante el [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)") implica cambiar los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") y reiniciar el sistema.

Si no es posible arrancar el sistema, inicie desde una [imagen en vivo](https://www.archlinux.org/download/) y [cambie la raíz](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") al sistema existente.

### Mensajes de la consola

Después del proceso de inicio, la pantalla se borra y aparece el mensaje de inicio de sesión, lo que deja a los usuarios incapaces de leer los mensajes del arranque y los de error. Este comportamiento predeterminado puede cambiarse utilizando los métodos descritos en las secciones siguientes.

Tenga en cuenta que, independientemente de la opción elegida, los mensajes del kernel pueden mostrarse para su inspección después del arranque utilizando `dmesg` o todos los registros del arranque actual con `journalctl -b`.

#### Control de flujo

Esta es una administración básica que se aplica a la mayoría de los emuladores de terminal, incluidas las consolas virtuales (vc):

*   Pulse `Ctrl+S` para pausar la salida
*   Y `Ctrl+Q` para reanudarla

Esto pausa no solo la salida, sino también los programas que intentan imprimir en el terminal, ya que bloquearán sobre las llamadas `write()` mientras la salida esté en pausa. Si su *init* parece congelado, asegúrese de que la consola del sistema no esté en pausa.

Para ver los mensajes de error que ya han mostrado, véase [Haga que los mensajes de inicio permanezcan en tty1](/index.php/Getty#Have_boot_messages_stay_on_tty1 "Getty").

#### Desplazamiento hacia atrás

El desplazamiento hacia atrás *(scrollback)* permite al usuario retroceder y ver el texto que se desplazó de la pantalla de una consola de texto. Esto es posible gracias a un búfer creado entre el adaptador de vídeo y el dispositivo de visualización llamado búfer de desplazamiento. Por defecto, las combinaciones de teclas `Shift+PageUp` y `Shift+PageDown` desplazan el búfer hacia arriba y hacia abajo respectivamente.

Si al desplazarse hacia arriba hasta el final no le muestra la información suficiente, necesita expandir su búfer de desplazamiento para tener más salida. Esto se hace ajustando la consola de framebuffer del kernel (fbcon) con el [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `fbcon=scrollback:Nk` donde `N` es el tamaño de búfer deseado es kilobytes. El tamaño predeterminado es 32k.

Si esto no le funciona, es posible que su consola de framebuffer no esté habilitada correctamente. Véase la [documentación sobre la consola de framebuffer](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) para conocer otros parámetros, por ejemplo para cambiar el controlador de framebuffer.

#### Salida de depuración

La mayoría de los mensajes del kernel están ocultos durante el arranque. Puede ver más de estos mensajes añadiendo diferentes parámetros de kernel. Los más simples son:

*   `debug` habilita los mensajes de depuración tanto para el kernel como para [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   `ignore_loglevel` fuerza a que se impriman todos los mensajes del kernel

Otros parámetros que puede añadir y que podrían ser útiles en ciertas situaciones son:

*   `earlyprintk=vga,keep` imprime los primeros mensajes en el proceso de arranque del kernel, en caso de que el kernel falle antes de que se muestre el resultado. Debe cambiar `vga` a `efi` para los sistemas [EFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   `log_buf_len=16M` asigna un búfer de mensajes del kernel más grande (16MB), para garantizar que la salida de depuración no se sobrescriba

También hay una serie de parámetros de depuración separados para permitir la depuración en subsistemas específicos, poe ejemplo `bootmem_debug`, `sched_debug`. Véase la [documentación de los parámetros del kernel](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt) para obtener información específica.

**Nota:** Si no puede desplazarse hacia atrás lo suficiente para ver la salida del arranque deseada, debe aumentar el tamaño del [búfer del desplazamiento hacia atrás](#Desplazamiento_hacia_atr.C3.A1s).

### Shell de recuperación

Obtener un shell interactivo en algún momento del proceso de arranque puede ayudarle a identificar exactamente dónde y por qué está fallando algo. Hay varios parámetros del kernel para hacerlo, pero todos ellos lanzan un shell normal que le permite ejecutar `exit`, lo que posibilita al kernel reanudar lo que estaba haciendo:

*   `rescue` inicia un shell poco después de que el sistema de archivos raíz se vuelva a leer/escribir
*   `emergency` inicia un shell incluso más temprano, antes de que se instalen la mayoría de los sistemas de archivos
*   `init=/bin/sh` (como último recurso) cambia el programa init a un shell de superusuario *(root)*. `rescue` y `emergency` dependen de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), pero esto debería funcionar incluso si *systemd* falla

Otra opción es el shell de depuración de systemd que añade un shell de superusuario en `tty9` (accesible con Ctrl+Alt+F9). Se puede habilitar añadiendo `systemd.debug-shell` a los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), o [habilitando](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `debug-shell.service`. Asegúrese de desactivar el servicio cuando lo haya hecho para evitar el riesgo de seguridad por dejar abierto un shell de superusuario en cada arranque.

### Pantalla en blanco con una tarjeta gráfica Intel

Esto es debido muy probablemente a un problema con la [configuración del modo del kernel](/index.php/Kernel_mode_setting_(Espa%C3%B1ol) "Kernel mode setting (Español)"). Pruebe a [desactivar modesetting](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Desactivar_modesetting "Kernel mode setting (Español)") o cambiar el [puerto de la tarjeta gráfica](/index.php/Intel_graphics_(Espa%C3%B1ol)#Problema_KMS:_la_consola_est.C3.A1_limitada_a_una_peque.C3.B1a_porci.C3.B3n_de_la_pantalla "Intel graphics (Español)").

### Atascado mientras se carga el kernel

Pruebe a desactivar ACPI añadiendo `acpi=off` a los parámetros del kernel.

### Sistema no arrancable

Si el sistema no arranca en absoluto, simplemente arranque desde una [imagen live](https://www.archlinux.org/download/) y [realice chroot](/index.php/Change_root "Change root") para iniciar sesión en el sistema y solucionar el problema.

### Depurar los errores de los módulos del kernel

Véase [como obtener información](/index.php/Kernel_modules_(Espa%C3%B1ol)#Obtener_informaci.C3.B3n "Kernel modules (Español)") de los módulos del kernel.

### Depurar errores de hardware

*   Puede visualizar información adicional de depuración sobre su hardware siguiendo [udev#Debug output](/index.php/Udev#Debug_output "Udev").
*   Asegúrese de que las actualizaciones de [microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") se aplican en su sistema.
*   Pruebe la memoria RAM de su dispositivo con [Memtest86+](http://www.memtest.org/). La RAM inestable puede ocasionar algunos problemas extremadamente extraños, que van desde fallos aleatorias hasta la corrupción de datos.

## Kernel panics

Un pánico del kernel (o *Kernel panic*) ocurre cuando el kernel de Linux entra en un estado de fallo irrecuperable. El estado generalmente se origina en controladores de hardware defectuosos que provocan que la máquina quede estancada, no responda y requiera un reinicio. Justo antes del interbloqueo, se genera un mensaje de diagnóstico que consiste en: el "estado de la máquina" cuando ocurrió el fallo, un "seguimiento de la llamada" *(call trace)* que conduce a la función del kernel que reconoció el fallo y una lista de módulos cargados en ese momento. Afortunadamente, estos *pánicos* no ocurren muy a menudo usando versiones *mainline* del kernel, como los suministrados por los repositorios oficiales, pero cuando suceden, debe saber como manejarlos.

**Nota:** Los *Kernel panic* a veces se conocen como *oops* o *kernel oops*. Si bien estos y los errores ocurren como resultado de un estado de error, un *oops* es más general ya que no conducen *necesariamente* a una máquina bloqueada: a veces el kernel puede recuperarse de un *oops* eliminando la tarea afectada para poder continuar.

**Sugerencia:** Pase el parámetro del kernel `oops=panic` al arrancar o escriba `1` en `/proc/sys/kernel/panic_on_oops` para forzar a un *oops* recuperable a emitir un *panic* en su lugar. Esto es aconsejable si le preocupa la pequeña posibilidad de sufrir una inestabilidad en el sistema como resultado de un *oops* recuperable que pueda hacer que los futuros errores sean difíciles de diagnosticar.

### Examinar los mensajes de pánico

Si se produce un *kernel panic* al inicio del proceso de arranque, es posible que aparezca un mensaje en la consola que contenga "Kernel panic - not syncing:" pero una vez que [Systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") se está ejecutando, los mensajes del kernel serán capturados y escritos en el registro del sistema. Sin embargo, cuando se produce un *kernel panic*, el mensaje de diagnóstico generado por el kernel "casi nunca" se escribe en el archivo de registro en el disco porque los interbloqueos de la máquina antes de `system-journald` tienen la ocasión. Por lo tanto, la única forma de examinar el mensaje de pánico es verlo en la consola como sucede (sin recurrir a la configuración de un *kdump crashkernel*). Puede hacerlo arrancando con los siguientes parámetros del kernel e intentando reproducir el mensaje de pánico en tty1:

 `systemd.journald.forward_to_console=1 console=tty1` 
**Sugerencia:** En caso de que el mensaje de pánico se desplace demasiado rápido como para examinarlo, intente pasar el parámetro del kernel `pause_on_oops=*segundos*` al arrancar.

#### Escenario de ejemplo: módulo defectuoso

Es posible adivinar qué subsistema o módulo está causando el pánico usando la información en el mensaje de diagnóstico. En este escenario, tenemos un *pánico* en una máquina (imaginaria) durante el arranque. Preste atención a las líneas resaltadas en **negrita**:

```
**kernel: BUG: unable to handle kernel NULL pointer dereference at (null)** [1]
**kernel: IP: fw_core_init+0x18/0x1000 [firewire_core]** [2]
kernel: PGD 718d00067 
kernel: P4D 718d00067 
kernel: PUD 7b3611067 
kernel: PMD 0 
kernel: 
kernel: Oops: 0002 [#1] PREEMPT SMP
**kernel: Modules linked in: firewire_core(+) crc_itu_t cfg80211 rfkill ipt_REJECT nf_reject_ipv4 nf_log_ipv4 nf_log_common xt_LOG nf_conntrack_ipv4 ...** [3] 
kernel: CPU: 6 PID: 1438 Comm: modprobe Tainted: P           O    4.13.3-1-ARCH #1
kernel: Hardware name: Gigabyte Technology Co., Ltd. H97-D3H/H97-D3H-CF, BIOS F5 06/26/2014
kernel: task: ffff9c667abd9e00 task.stack: ffffb53b8db34000
kernel: RIP: 0010:fw_core_init+0x18/0x1000 [firewire_core]
kernel: RSP: 0018:ffffb53b8db37c68 EFLAGS: 00010246
kernel: RAX: 0000000000000000 RBX: 0000000000000000 RCX: 0000000000000000
kernel: RDX: 0000000000000000 RSI: 0000000000000008 RDI: ffffffffc16d3af4
kernel: RBP: ffffb53b8db37c70 R08: 0000000000000000 R09: ffffffffae113e95
kernel: R10: ffffe93edfdb9680 R11: 0000000000000000 R12: ffffffffc16d9000
kernel: R13: ffff9c6729bf8f60 R14: ffffffffc16d5710 R15: ffff9c6736e55840
kernel: FS:  00007f301fc80b80(0000) GS:ffff9c675dd80000(0000) knlGS:0000000000000000
kernel: CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
kernel: CR2: 0000000000000000 CR3: 00000007c6456000 CR4: 00000000001406e0
kernel: Call Trace:
**kernel:  do_one_initcall+0x50/0x190** [4]
kernel:  ? do_init_module+0x27/0x1f2
kernel:  do_init_module+0x5f/0x1f2
kernel:  load_module+0x23f3/0x2be0
kernel:  SYSC_init_module+0x16b/0x1a0
kernel:  ? SYSC_init_module+0x16b/0x1a0
kernel:  SyS_init_module+0xe/0x10
kernel:  entry_SYSCALL_64_fastpath+0x1a/0xa5
kernel: RIP: 0033:0x7f301f3a2a0a
kernel: RSP: 002b:00007ffcabbd1998 EFLAGS: 00000246 ORIG_RAX: 00000000000000af
kernel: RAX: ffffffffffffffda RBX: 0000000000c85a48 RCX: 00007f301f3a2a0a
kernel: RDX: 000000000041aada RSI: 000000000001a738 RDI: 00007f301e7eb010
kernel: RBP: 0000000000c8a520 R08: 0000000000000001 R09: 0000000000000085
kernel: R10: 0000000000000000 R11: 0000000000000246 R12: 0000000000c79208
kernel: R13: 0000000000c8b4d8 R14: 00007f301e7fffff R15: 0000000000000030
kernel: Code: <c7> 04 25 00 00 00 00 01 00 00 00 bb f4 ff ff ff e8 73 43 9c ec 48 
kernel: RIP: fw_core_init+0x18/0x1000 [firewire_core] RSP: ffffb53b8db37c68
kernel: CR2: 0000000000000000
kernel: ---[ end trace 71f4306ea1238f17 ]---
**kernel: Kernel panic - not syncing: Fatal exception** [5]
kernel: Kernel Offset: 0x80000000 from 0xffffffff810000000 (relocation range: 0xffffffff800000000-0xfffffffffbffffffff
kernel: ---[ end Kernel panic - not syncing: Fatal exception
```

*   [1] Indica el tipo de error que causó el pánico. En este caso, era un error del programador.
*   [2] Indica que el pánico ocurrió en una función llamada *fw_core_init* en el módulo *firewire_core*.
*   [3] Indica que *firewire_core* fue el último módulo que se inició.
*   [4] Indica que la función que llamó a la función *fw_core_init* fue *do_one_initcall*.
*   [5] Indica que este mensaje de *oops* es, de hecho, un *kernel panic* y el sistema está ahora bloqueado.

Podemos suponer entonces que el pánico ocurrió durante la rutina de inicialización del módulo *firewire_core* al iniciarse. (Podríamos suponer, entonces, que el hardware firewire de la máquina es incompatible con esta versión del módulo del controlador firewire debido a un error del programador, y tendrá que esperar una nueva versión.) Mientras tanto, la forma más fácil de hacer funcionar la máquina nuevamente es evitar que el módulo se inicie. Podemos hacer esto de una de estas dos maneras:

*   Si el módulo se está iniciando durante la ejecución de *initramfs*, reinicie con el parámetro del kernel `rd.blacklist=firewire_core`.
*   De lo contrario, reinicie con el parámetro del kernel `module_blacklist=firewire_core`.

### Reiniciar en una shell de superusuario y solucionar el problema

Necesitará un shell de superusuario para realizar cambios en el sistema para que no se produzca el pánico. Si se produce un pánico durante el arranque, existen varias estrategias para obtener un shell de superusuario antes de que la máquina se bloquee:

*   Reinicie con el parámetro del kernel `emergency`, `rd.emergency`, o `-b` para obtener una manera de iniciar sesión justo después de que se monte el sistema de archivos raíz y `systemd` se ha iniciado.

**Nota:** En este punto, el sistema de archivos raíz se montará como **solo lectura**. Ejecute `# mount -o remount,rw /` para poder realizar cambios.

*   Reinicie con el parámetro del kernel `rescue`, `rd.rescue`, `single`, `s`, `S`, o { {ic|1}} para poder iniciar sesión justo después de montar los sistemas de archivos locales.
*   Reinicie con el parámetro del kernel `systemd.debug-shell=1` para obtener un shell de superusuario al iniciar en tty9\. Cambie a este presionando `Ctrl-Alt-F9`.
*   Experimente reiniciando con diferentes conjuntos de parámetros del kernel para posibilitar la deshabilitación de la función del kernel que está causando el pánico. Pruebe los "viejos recursos" `acpi=off` y `nolapic`.

**Sugerencia:** Véase `Documentation/admin-guide/kernel-parameters.txt` en el código fuente del kernel de Linux para ver todos los parámetros.

*   Como último recurso, arranque con el **CD de instalación de Arch Linux** y monte el sistema de archivos raíz en `/mnt` y luego ejecute `# arch-chroot /mnt`.

Deshabilite el servicio o programa que causa el pánico, invierta una actualización defectuosa o solucione un problema de configuración.

## Administrar paquetes

Véase [solución de problemas con pacman](/index.php/Pacman_(Espa%C3%B1ol)#Soluci.C3.B3n_de_problemas "Pacman (Español)") para los temas más generales, y [solución de problemas de cifrado de paquetes con pacman](/index.php/Pacman/Package_signing_(Espa%C3%B1ol)#Soluci.C3.B3n_de_problemas "Pacman/Package signing (Español)") para los problemas con las claves PGP.

## fuser

*fuser* es una utilidad de línea de órdenes para la identificación de los procesos que utilizan recursos como archivos, sistemas de archivos y puertos TCP/UDP.

*fuser* está incluido en el paquete [psmisc](https://www.archlinux.org/packages/?name=psmisc), que debe estar ya instalado como parte del grupo [base](https://www.archlinux.org/groups/x86_64/base/). Véase [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) para más detalles.

## Permisos de sesión

**Nota:** Debe utilizar [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como su sistema de inicio para que las sesiones locales funcionen [[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) —que se requiere para que [polkit](https://en.wikipedia.org/wiki/es:PolicyKit "wikipedia:es:PolicyKit") y [ACL](https://en.wikipedia.org/wiki/es:Lista_de_control_de_acceso "wikipedia:es:Lista de control de acceso") puedan definir permisos para distintos dispositivos (ver `/usr/lib/udev/rules.d/70-uaccess.rules` y [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))—.

En primer lugar, asegúrese de que tiene una sesión local válida dentro de X:

```
$ loginctl show-session $XDG_SESSION_ID

```

Esta debe contener `Remote=no` y `Active=yes` en la salida. Si no es así, asegúrese de que X se ejecuta en la misma tty donde se produjo el inicio de sesión. Esto es necesario a fin de preservar la sesión iniciada. Esto es manejado de forma predeterminada por `/etc/X11/xinit/xserverrc`.

Las acciones [polkit](/index.php/Polkit "Polkit") no requieren una configuración posterior. Algunas acciones polkit requieren una autenticación adicional, incluso con una sesión local. Un agente de autenticación polkit debe estar en ejecución para que esto funcione. Véase [Agentes de autenticación](/index.php/Polkit#Authentication_agents "Polkit") para más información.

## Mensaje: "error while loading shared libraries"

Si, durante el uso de un programa, se produce un error similar al siguiente:

```
error while loading shared libraries: libusb-0.1.so.4: cannot open shared object file: No such file or directory

```

Utilice [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o [pkgfile](/index.php/Pkgfile_(Espa%C3%B1ol) "Pkgfile (Español)") para buscar el paquete al cual pertenece la biblioteca que falta:

 `$ pacman -Fs libusb-0.1.so.4` 
```
extra/libusb-compat 0.1.5-1
    usr/lib/libusb-0.1.so.4

```

En este caso, el paquete [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) necesita ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)").

El error también puede significar que el paquete que ha utilizado para instalar el programa no enumera la biblioteca como una dependencia en su [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"): si se trata de un paquete oficial, [informe del error](/index.php/Report_a_bug "Report a bug"); si se trata de un paquete de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), informe a su mantenedor en su página del sitio web de AUR.

## Mensaje: "file: could not find any magic files!"

Si ve este mensaje, es probable que indique que la actualización de un paquete ha dañado el archivo de enlaces de tiempo de ejecución del vinculador dinámico y su sistema ahora está esencialmente *lisiado*. No podrá volver a compilar o reinstalar el paquete responsable ni reconstruir el [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") hasta que lo solucione.

### Problema

Es probable que una actualización del paquete haya agregado un `*archivo*.conf` no válido al directorio `/etc/ld.so.conf.d` o editado `/etc/ld.so.conf` incorrectamente. El resultado es que el archivo de enlaces de tiempo de ejecución del vinculador dinámico `/etc/ld.so.cache` se vuelve a generar con datos no válidos. Esto puede causar que fallen todos los programas del sistema que dependan de bibliotecas compartidas (es decir, casi todos).

### Solución

1.  Arranque con el ***CD de instalación de Arch Linux***.
2.  Monte su sistema de archivos raíz `/` en `/mnt` y su sistema de archivos `/boot` en `/mnt/boot` y entre en el sistema dañado ejecutando `# arch-chroot /mnt`.
3.  Examine el archivo `/etc/ld.so.conf` y elimine las líneas no válidas encontradas.
4.  Examine los archivos ubicados en el directorio `/etc/ld.so.conf.d/` y elimine los archivos no válidos.
5.  Reconstruya el archivo de enlaces de tiempo de ejecución del vinculador dinámico `/etc/ld.so.cache` ejecutando `# ldconfig`.
6.  Reconstruya el [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") ejecutando `# mkinitcpio -p linux`.
7.  Salga del chroot, desmonte los sistemas de archivos y reinicie de nuevo el sistema.

## Véase también

*   [Fix the Most Common Problems](http://www.tuxradar.com/content/how-fix-most-common-linux-problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Memtest-like tools to add to grub.cfg on UltimateBootCD.com
*   [Wikipedia:BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [REISUB](/index.php/REISUB "REISUB")
*   [Debug Logging to a Serial Console](http://freedesktop.org/wiki/Software/systemd/Debugging#Debug_Logging_to_a_Serial_Console) en Freedesktop.org
*   [How to Isolate Linux ACPI Issues](https://web.archive.org/web/20120217124742/http://www.lesswatts.org/projects/acpi/debug.php) en Archive.org
**Estado de la traducción**
Este artículo es una traducción de [Getty](/index.php/Getty "Getty"), revisada por última vez el **2018-10-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Getty&diff=0&oldid=551325) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")

Un [getty](https://en.wikipedia.org/wiki/getty_(Unix) "w:getty (Unix)") es el nombre genérico de un programa que gestiona una línea de terminal y su terminal conectada. Su propósito es proteger el sistema del acceso no autorizado. En general, cada proceso getty se inicia mediante [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") y gestiona una sola línea de terminal.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Añadir consolas virtuales adicionales](#Añadir_consolas_virtuales_adicionales)
*   [3 Inicio de sesión automático a la consola virtual](#Inicio_de_sesión_automático_a_la_consola_virtual)
    *   [3.1 Consola virtual](#Consola_virtual)
    *   [3.2 Consola serie](#Consola_serie)
    *   [3.3 Consola Nspawn](#Consola_Nspawn)
*   [4 Mantener los mensajes de arranque en tty1](#Mantener_los_mensajes_de_arranque_en_tty1)
*   [5 Véase también](#Véase_también)

## Instalación

*agetty* es el getty predeterminado en Arch Linux, como parte del paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux). Modifica la configuración de TTY mientras espera un inicio de sesión para que las nuevas líneas no se traduzcan a CR-LF. Esto tiende a causar un "efecto escalera" para los mensajes impresos en la consola. Agetty gestiona las consolas virtuales y seis de estas consolas virtuales se proporcionan de forma predeterminada en Arch Linux. Normalmente se puede acceder a ellas presionando desde `Control+Alt+F1` hasta `Control+Alt+F6`.

Las alternativas incluyen:

*   **mingetty** — Un getty mínimo que permite inicios de sesión automáticos.

	[mingetty](https://aur.archlinux.org/packages/mingetty/) || [mingetty](https://aur.archlinux.org/packages/mingetty/)

*   **fbgetty** — Una consola getty como mingetty, que soporta framebuffers.

	[http://projects.meuh.org/fbgetty/](http://projects.meuh.org/fbgetty/) || [fbgetty](https://aur.archlinux.org/packages/fbgetty/)

*   **mgetty** — Un programa versátil para manejar todos los aspectos de un módem bajo Unix.

	[http://mgetty.greenie.net/](http://mgetty.greenie.net/) || [mgetty](https://aur.archlinux.org/packages/mgetty/)

## Añadir consolas virtuales adicionales

Abra el archivo `/etc/systemd/logind.conf` y configure la opción **NAutoVTs=6** a la cantidad de consolas virtuales que desee al inicio.

Si desea iniciar una temporalmente, puede iniciar un servicio getty en el TTY deseado escribiendo:

```
$ systemctl start getty@ttyN.service

```

## Inicio de sesión automático a la consola virtual

La configuración se basa en [archivos de entrada](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)") de systemd para anular los parámetros predeterminados pasados ​​a *agetty*.

La configuración es diferente para las consolas virtuales y las serie. En la mayoría de los casos, quiere configurar el inicio de sesión automático en una consola virtual, cuyo nombre de dispositivo es `tty*N*`, donde `*N*` es un número. La configuración de inicio de sesión automático para consolas serie será ligeramente diferente. Los nombres de los dispositivos de las consolas serie aparecen como `ttyS*N*`, donde `*N*` es un número.

### Consola virtual

**Note:** [Se ha informado](https://bbs.archlinux.org/viewtopic.php?id=238576) que este método puede interferir con el proceso de hibernación.

[Edite la unidad provista](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)") ya sea manualmente creando el siguiente fragmento de código, o ejecutando `systemctl edit getty@tty1` y pegando su contenido:

 `/etc/systemd/system/getty@tty1.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I $TERM
```

**Sugerencia:** La opción `Type=idle` que se encuentra en el `getty@.service` predeterminado retrasará el inicio del servicio hasta que todos los trabajos (solicitudes de cambio de estado a las unidades) se completen en orden para evitar contaminar el mensaje de inicio de sesión con mensajes de arranque. Cuando [inicie X automáticamente](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)"), puede ser útil iniciar `getty@tty1.service` inmediatamente añadiendo `Type=simple` en la [fragmento de entrada](/index.php/Drop-in_snippet_(Espa%C3%B1ol) "Drop-in snippet (Español)"). Tanto el sistema init como *startx* pueden ser [silenciados](/index.php/Silent_boot "Silent boot") para evitar el intercalado de sus mensajes durante el arranque.

Si desea utilizar un *tty* distinto a *tty1*, véase el [FAQ de systemd](/index.php/Systemd_FAQ_(Espa%C3%B1ol)#¿Cómo_puedo_cambiar_el_número_de_gettys_ejecutadas_por_defecto? "Systemd FAQ (Español)").

### Consola serie

Cree el siguiente archivo (y directorios principales):

 `/etc/systemd/system/serial-getty@ttyS0.service.d/autologin.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* -s %I 115200,38400,9600 vt102
```

### Consola Nspawn

Para configurar el inicio de sesión automático para un contenedor [systemd-nspawn](/index.php/Systemd-nspawn_(Espa%C3%B1ol) "Systemd-nspawn (Español)"), anule el servicio *console-getty*:

 `/etc/systemd/system/console-getty.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --noclear --autologin *username* --keep-baud console 115200,38400,9600 $TERM
```

## Mantener los mensajes de arranque en tty1

De manera predeterminada, Arch tiene habilitado el servicio `getty@tty1`. El archivo de servicio ya pasa `--noclear`, lo que evita que Agetty borre la pantalla. Sin embargo [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") borra la pantalla antes de iniciarla. Para deshabilitar este comportamiento, cree `/etc/systemd/system/getty@tty1.service.d/noclear.conf`:

 `/etc/systemd/system/getty@tty1.service.d/noclear.conf` 
```
[Service]
TTYVTDisallocate=no
```

Esto reemplaza solo `TTYVTDisallocate` para *agetty* en TTY1, y deja el archivo de servicio global `/usr/lib/systemd/system/getty@.service` sin tocar. Véase [Systemd (Español)#Modificar los archivos de unidad suministrados](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)").

**Nota:**

*   Asegúrese de eliminar `quiet` de los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").
*   El inicio tardío de KMS puede hacer que se borren los primeros mensajes de arranque. Véase [KMS (Español)#Iniciar KMS tempranamente](/index.php/KMS_(Espa%C3%B1ol)#Iniciar_KMS_tempranamente "KMS (Español)") o [KMS (Español)#Desactivar modesetting](/index.php/KMS_(Espa%C3%B1ol)#Desactivar_modesetting "KMS (Español)").

## Véase también

*   [Systemd (Español)#Cambiar el target predeterminado para arrancar](/index.php/Systemd_(Espa%C3%B1ol)#Cambiar_el_target_predeterminado_para_arrancar "Systemd (Español)")
*   [El TTY desmitificado](http://www.linusakesson.net/programming/tty/)
*   [Wikipedia:es:Tty (unix)](https://en.wikipedia.org/wiki/es:Tty_(unix) "wikipedia:es:Tty (unix)")
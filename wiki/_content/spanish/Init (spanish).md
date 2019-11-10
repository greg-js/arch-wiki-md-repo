Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [ConsoleKit](/index.php/ConsoleKit "ConsoleKit")

**Estado de la traducción**
Este artículo es una traducción de [init](/index.php/Init "Init"), revisada por última vez el **2019-11-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Init&diff=0&oldid=587711) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Advertencia:** Arch Linux solo tiene soporte oficial para [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). [[1]](https://lists.archlinux.org/pipermail/arch-general/2015-July/039460.html)Cuando utilice un sistema init diferente, por favor mencione esto en las solicitudes de soporte.

[Init](https://en.wikipedia.org/wiki/es:Init "wikipedia:es:Init") (abreviatura del término inglés *initialization*) es el primer proceso que se inicia durante el arranque del sistema. Es un demonio cuyo proceso continúa ejecutándose hasta que se apaga el sistema. Init es el ancestro directo o indirecto de todos los demás procesos, y adopta automáticamente todos los procesos huérfanos. El kernel lo inicia utilizando un nombre de archivo codificado. Si el kernel no puede iniciarlo, se producirá un [«kernel panic»](https://en.wikipedia.org/wiki/es:Kernel_panic "wikipedia:es:Kernel panic"). A init generalmente se le asigna el [identificador de proceso (PID)](https://en.wikipedia.org/wiki/es:Identificador_de_proceso "wikipedia:es:Identificador de proceso") 1.

Los *scripts* de init (o *rc*) son lanzados para garantizar la funcionalidad básica en el inicio y apagado del sistema. Esto incluye el (des)montaje del [sistemas de archivos](/index.php/File_system "File system") y el lanzamiento de los [demonios](/index.php/Daemons "Daemons"). Un *gestor de servicios* va un paso más allá al proporcionar un control activo sobre los procesos ejecutados, o la [supervisión de procesos](https://en.wikipedia.org/wiki/Process_Supervision "wikipedia:Process Supervision"). Un ejemplo es monitorear los bloqueos y reiniciar los procesos en consecuencia.

Estos componentes se combinan con el *sistema* init. Algunos inits incluyen el administrador de servicios en el proceso de inicio, o tienen scripts de inicio en estrecha relación con ellos. A estas entradas se hace referencia como «integradas», aunque las entradas en diferentes categorías pueden depender explícitamente entre sí.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Inits (integrados)](#Inits_(integrados))
*   [2 Inits](#Inits)
*   [3 Scripts de init](#Scripts_de_init)
*   [4 Gestores de servicios](#Gestores_de_servicios)
*   [5 Configuración](#Configuración)
    *   [5.1 Migrar servicios en ejecución](#Migrar_servicios_en_ejecución)
    *   [5.2 logind](#logind)
    *   [5.3 Tareas programadas](#Tareas_programadas)
    *   [5.4 Dbus](#Dbus)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 systemd-nspawn](#systemd-nspawn)
    *   [6.2 Reemplazar udev](#Reemplazar_udev)
*   [7 Véase también](#Véase_también)

## Inits (integrados)

*   **anopa** — Sistema de inicialización construido alrededor del conjunto de supervisión s6

	[https://jjacky.com/anopa/](https://jjacky.com/anopa/) || [anopa](https://aur.archlinux.org/packages/anopa/)

*   **GNU Shepherd** — Sistema de inicialización escrito en [Guile](https://www.gnu.org/software/guile/).

	[https://www.gnu.org/software/shepherd/](https://www.gnu.org/software/shepherd/) || [shepherd](https://aur.archlinux.org/packages/shepherd/)

*   **[OpenRC](/index.php/OpenRC "OpenRC")** — Sistema de inicialización basado en dependencias.

	[http://www.gentoo.org/proj/en/base/openrc/](http://www.gentoo.org/proj/en/base/openrc/) || [openrc](https://aur.archlinux.org/packages/openrc/) [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/)

*   **[systemd](/index.php/Systemd "Systemd")** — Sistema de inicialización basado en dependencias con una notable paralelización, supervisión de procesos mediante cgroups y capacidad de depender de un punto de montaje dado o servicio dbus.

	[https://freedesktop.org/wiki/Software/systemd/](https://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

## Inits

*   **[BusyBox](/index.php/BusyBox "BusyBox")** — Utilidades para sistemas de rescate e incrustados.

	[http://busybox.net/](http://busybox.net/) || [busybox](https://www.archlinux.org/packages/?name=busybox)

*   **ninit** — Fork de [minit](http://www.fefe.de/minit/)

	[http://riemann.fmi.uni-sofia.bg/ninit/](http://riemann.fmi.uni-sofia.bg/ninit/) || [ninit](https://aur.archlinux.org/packages/ninit/)

*   **sinit** — Init simple inicialmente basado en la inicialización mínima de Rich Felker.

	[http://core.suckless.org/sinit](http://core.suckless.org/sinit) || [sinit](https://aur.archlinux.org/packages/sinit/)

*   **[SysVinit](/index.php/SysVinit "SysVinit")** — Sistema tradicional V de init.

	[http://savannah.nongnu.org/projects/sysvinit](http://savannah.nongnu.org/projects/sysvinit) || [sysvinit](https://aur.archlinux.org/packages/sysvinit/)

## Scripts de init

*   **initscripts-fork** — Fork de los scripts de SysVinit mantenido en Arch Linux.

	[https://bitbucket.org/TZ86/initscripts-fork/overview](https://bitbucket.org/TZ86/initscripts-fork/overview) || [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/)

*   **minirc** — Script de inicialización mínimo diseñado para BusyBox.

	[https://github.com/hut/minirc/](https://github.com/hut/minirc/) || [minirc-git](https://aur.archlinux.org/packages/minirc-git/)

## Gestores de servicios

*   **daemontools** — Colección de herramientas para gestionar servicios UNIX.

	[http://cr.yp.to/daemontools.html](http://cr.yp.to/daemontools.html) || [daemontools](https://aur.archlinux.org/packages/daemontools/)

*   **[Monit](/index.php/Monit "Monit")** — Monit es una herramienta de supervisión de procesos para Unix y Linux. Con monit, el estado del sistema se puede ver directamente desde la línea de órdenes o mediante el servidor web HTTP(S) nativo.

	[http://mmonit.com/monit/](http://mmonit.com/monit/) || [monit](https://www.archlinux.org/packages/?name=monit)

*   **perp** — Supervisor de proceso persistente (servicio) y marco de administración para UNIX.

	[http://b0llix.net/perp/](http://b0llix.net/perp/) || [perp](https://aur.archlinux.org/packages/perp/)

*   **[runit](/index.php/Runit "Runit")** — Esquema de inicialización de UNIX con supervisión de servicio, un reemplazo para SysVinit y otros esquemas de init.

	[http://smarden.org/runit/](http://smarden.org/runit/) || [runit](https://aur.archlinux.org/packages/runit/)

*   **s6** — Pequeño conjunto de programas para UNIX, diseñado para permitir la supervisión del servicio en la línea de daemontools y runit.

	[http://skarnet.org/software/s6/](http://skarnet.org/software/s6/) || [s6](https://aur.archlinux.org/packages/s6/)

## Configuración

### Migrar servicios en ejecución

Para ejecutar demonios bajo el nuevo init, guarde una lista de demonios en ejecución:

```
$ systemctl list-units --state=running "*.service" > daemons.list

```

y configure los [#Scripts de init](#Scripts_de_init) en consecuencia. Vea también [[2]](http://unix.stackexchange.com/questions/175380/how-to-list-all-running-daemons).

**Nota:** [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8), [kernel modules](/index.php/Kernel_modules "Kernel modules") y [sysctl](/index.php/Sysctl "Sysctl") puede que también necesiten configuración.

### logind

[logind](https://www.freedesktop.org/wiki/Software/systemd/logind/) requiere que *systemd* sea el proceso de inicio. [[3]](https://www.freedesktop.org/wiki/Software/systemd/InterfacePortabilityAndStabilityChart/) Como tal, las [sesiones locales](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") y otras funciones no estarán disponibles.

**Sugerencia:** una versión independiente de *logind* está disponible como [elogind-git](https://aur.archlinux.org/packages/elogind-git/) [[4]](https://lists.gnu.org/archive/html/guix-devel/2015-04/msg00352.html)

	Permisos del dispositivo

Añada usuarios a los [grupos de usuarios](/index.php/User_group "User group") respectivos para acceder al dispositivo y reiniciarlo. La pertencia actual al grupo debe verificarse primero con `id *user*`.

```
# usermod -a -G video,audio,power,disk,storage,optical,lp,scanner *user*

```

Consulte también [Users and groups#Pre-systemd groups](/index.php/Users_and_groups#Pre-systemd_groups "Users and groups"). Para crear reglas de grupo para usar con [Polkit](/index.php/Polkit "Polkit"), vea [Polkit#Bypass password prompt](/index.php/Polkit#Bypass_password_prompt "Polkit").

	Rootless X (1.16)

Como `Xorg.wrap` no verifica si logind está activo [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=86975#c5), los [derechos de root para Xorg](/index.php/Xorg#Rootless_Xorg "Xorg") deben activarse manualmente:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = yes` 

	Administración de energía

Consulte [pm-utils](https://aur.archlinux.org/packages/pm-utils/) y [acpid](/index.php/Acpid "Acpid") para reemplazar la [administración de energía con systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Tareas programadas

Arch utiliza los archivos [timer](/index.php/Systemd#Timers "Systemd") en lugar de [cron](/index.php/Cron "Cron") por defecto. Vea [archlinux-cronjobs](https://github.com/notfoss/archlinux-cronjobs) para conocer trabajos cron básicos.

### Dbus

Las instancias de usuario de *dbus-daemon* son lanzadas por [systemd/User](/index.php/Systemd/User "Systemd/User") [[6]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/). Cuando requiera [IPC](https://en.wikipedia.org/wiki/es:Se%C3%B1al_(inform%C3%A1tica) (del inglés «comunicación inter procesos) entre aplicaciones de escritorio, restaure `30-dbus.sh`:

 `/etc/X11/xinit/xinitrc.d/30-dbus.sh` 
```
#!/bin/bash

# launches a session dbus instance
if [ -z "${DBUS_SESSION_BUS_ADDRESS-}" ] && type dbus-launch >/dev/null; then
  eval $(dbus-launch --sh-syntax --exit-with-session)
fi
```

## Consejos y trucos

### systemd-nspawn

[systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") es una herramienta para sistemas systemd. Sin embargo, desde Linux 2.6.19 es posible ejecutar systemd en un sistema no systemd utilizando el espacio de nombres PID. Para ello, el kernel debe configurarse con `CONFIG_PID_NS` y `CONFIG_NAMESPACES`).

El espacio de nombres PID crea una nueva jerarquía de procesos que comienzan con PID 1\. Además de esto, systemd requiere que se monte un sistema de archivos raíz enjaulado (chrooteado). Por lo tanto, debe al menos realizar un montaje de «bind», porque de lo contrario algunos servicios fallarán con:

```
"Failed at step NAMESPACE spawning" due to "Invalid operation" 

```

dado que systemd intentará volver a montar la raíz con la opción `private`.

Para configurar un entorno enjaulado (chroot) con un nuevo espacio de nombre PID puede usar jchroot.[[7]](http://vincent.bernat.im/en/blog/2011-jchroot-isolation.html) [[8]](https://github.com/vincentbernat/jchroot). Asegúrese de no montar `/proc` dentro de la nueva raíz antes de realizar chroot, de lo contrario, systemd detectará el entorno chroot. Puede montarlo más tarde una vez que se esté ejecutando systemd.

### Reemplazar udev

**Advertencia:** reemplazar udev no es necesario ya que *systemd-udev* es funcional sin *systemd* como PID 1\. Algunos reemplazos como *eudev* tampoco pueden coexistir con [systemd](https://www.archlinux.org/packages/?name=systemd) —asegúrese de que un init alternativo se inicie **antes** de su instalación—.

*   **eudev** — eudev es un fork de udev iniciado por el proyecto Gentoo. Está diseñado y probado principalmente con OpenRC.

	[https://wiki.gentoo.org/wiki/Eudev](https://wiki.gentoo.org/wiki/Eudev) || [eudev](https://aur.archlinux.org/packages/eudev/) [eudev-git](https://aur.archlinux.org/packages/eudev-git/)

*   **mdev** — Administrador de dispositivos para su utilización en sistemas integrados.

	[https://git.busybox.net/busybox/plain/docs/mdev.txt](https://git.busybox.net/busybox/plain/docs/mdev.txt) || [busybox](https://www.archlinux.org/packages/?name=busybox)

## Véase también

*   [Debian init system debate](https://wiki.debian.org/Debate/initsystem)
*   [How to run s6-svscan as process 1](http://skarnet.org/software/s6/s6-svscan-1.html)
*   [Replace systemd with busybox + minirc](https://bbs.archlinux.org/viewtopic.php?id=162606&p=1)
*   [Experiments of Manjaro](http://www.troubleshooters.com/linux/init/manjaro_experiments.htm)
*   [Init vs. runsv](https://busybox.net/~vda/init_vs_runsv.html)
*   [Demystifying the init system](https://felipec.wordpress.com/2013/11/04/init/)
*   [A history of modern init systems (1992-2015)](http://blog.darknedgy.net/technology/2015/09/05/0/)
*   [Comparison of init systems (gentoo wiki)](https://wiki.gentoo.org/wiki/Comparison_of_init_systems)
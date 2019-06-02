**Estado de la traducción**
Este artículo es una traducción de [Power management](/index.php/Power_management "Power management"), revisada por última vez el **2019-05-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Power_management&diff=0&oldid=572520) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Power management/Suspender e hibernar](/index.php/Power_management/Suspend_and_hibernate_(Espa%C3%B1ol) "Power management/Suspend and hibernate (Español)")
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   [CPU escala de frecuencia](/index.php/CPU_frequency_scaling_(Espa%C3%B1ol) "CPU frequency scaling (Español)")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Módulos del núcleo](/index.php/Kernel_module_(Espa%C3%B1ol) "Kernel module (Español)")
*   [sysctl](/index.php/Sysctl "Sysctl")
*   [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")

[Power management](https://en.wikipedia.org/wiki/es:Power_management "wikipedia:es:Power management") es una característica que apaga la alimentación o los interruptores del sistema para un menor consume de energía cuando está incactivo.

En Arch Linux, la administración de energía consiste en dos partes principales:

1.  Configurar el kernel de Linux, que interactua con el hardware.
    *   [Parámetros del nucleo](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)")
    *   [Módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)")
    *   Reglas [udevs](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")
2.  Las herramientas de configuración del espacio del usuario pueden interactuar con el núcleo y reaccionar a sus eventos. Muchas de estás herramientas le permiten también modificar la configuración del núcleo de una forma fácil. Vea [#Herramientas de espacio del usuario](#Herramientas_de_espacio_del_usuario) para las opciones.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Herramientas de espacio del usuario](#Herramientas_de_espacio_del_usuario)
    *   [1.1 Consola](#Consola)
    *   [1.2 Gráficos](#Gráficos)
*   [2 Administración de energía con systemd](#Administración_de_energía_con_systemd)
    *   [2.1 Eventos de ACPI](#Eventos_de_ACPI)
        *   [2.1.1 Administradores de energía](#Administradores_de_energía)
        *   [2.1.2 xss-lock](#xss-lock)
    *   [2.2 Suspensión e hibernación](#Suspensión_e_hibernación)
        *   [2.2.1 Suspensión híbrida en suspensión o en hibernación](#Suspensión_híbrida_en_suspensión_o_en_hibernación)
    *   [2.3 Sleep hooks](#Sleep_hooks)
        *   [2.3.1 Archivos de servicios para suspender/reanudar](#Archivos_de_servicios_para_suspender/reanudar)
        *   [2.3.2 Archivo de servicio combinando suspensión/reanudación](#Archivo_de_servicio_combinando_suspensión/reanudación)
        *   [2.3.3 Hooks en /usr/lib/systemd/system-sleep](#Hooks_en_/usr/lib/systemd/system-sleep)
    *   [2.4 Solución de problemas](#Solución_de_problemas)
        *   [2.4.1 Acción retardada del interruptor de la tapa](#Acción_retardada_del_interruptor_de_la_tapa)
        *   [2.4.2 La suspensión desde la tecla Fn correspondiente del portátil no funciona](#La_suspensión_desde_la_tecla_Fn_correspondiente_del_portátil_no_funciona)
*   [3 Ahorrar energía](#Ahorrar_energía)
    *   [3.1 Procesadores con soporte HWP (Hardware P-state)](#Procesadores_con_soporte_HWP_(Hardware_P-state))
    *   [3.2 Audio](#Audio)
    *   [3.3 Retroiluminación](#Retroiluminación)
    *   [3.4 Bluetooth](#Bluetooth)
    *   [3.5 Cámara web](#Cámara_web)
    *   [3.6 Parámetros Kernel](#Parámetros_Kernel)
        *   [3.6.1 Desactivar NMI watchdog](#Desactivar_NMI_watchdog)
        *   [3.6.2 Tiempo de reescritura](#Tiempo_de_reescritura)
        *   [3.6.3 Modo portátil](#Modo_portátil)
    *   [3.7 Interfaces de red](#Interfaces_de_red)
        *   [3.7.1 Tarjetas inalámbricas Intel (iwlwifi)](#Tarjetas_inalámbricas_Intel_(iwlwifi))
    *   [3.8 Administración de energía bus](#Administración_de_energía_bus)
        *   [3.8.1 Administración de energía en estado activo](#Administración_de_energía_en_estado_activo)
        *   [3.8.2 Administración de energía PCI en tiempo de ejecución](#Administración_de_energía_PCI_en_tiempo_de_ejecución)
        *   [3.8.3 Auto suspensión USB](#Auto_suspensión_USB)
        *   [3.8.4 Administración de energía de enlace activo SATA](#Administración_de_energía_de_enlace_activo_SATA)
    *   [3.9 Controlador de disco duro](#Controlador_de_disco_duro)
    *   [3.10 Controlador CD-ROM o DVD](#Controlador_CD-ROM_o_DVD)
*   [4 Herramientas y scripts](#Herramientas_y_scripts)
    *   [4.1 Utilizar un script y una regla udev](#Utilizar_un_script_y_una_regla_udev)
    *   [4.2 Ajustes de energía de la impresora](#Ajustes_de_energía_de_la_impresora)
*   [5 Vea también](#Vea_también)

## Herramientas de espacio del usuario

Utilizando estas herramientas puede remplazar la configuración de muchos ajustes a mano. Solo ejecute **una** de estas herramientas para evitar conflictos ya que todas trabajan más o menos de la misma forma. Eche un vistazo a la [categoria de administracion de energía](/index.php/Category:Power_management "Category:Power management") para tener una noción de las opciones de administración energética que existen en Arch Linux.

Aquí están los scripts y herramientas más populares para ahorrar energía:

### Consola

*   **[acpid](/index.php/Acpid "Acpid")** — Un demonio para llevar los eventos de energía ACPI con soporte netlink.

	[http://sourceforge.net/projects/acpid2/](http://sourceforge.net/projects/acpid2/) || [acpid](https://www.archlinux.org/packages/?name=acpid)

*   **[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")** — Utilidad para configurar los ajustes de administración de energía de los portátiles considerado por muchos una utilidad clave para ahorrar energía, puede requerir un poco de configuración.

	[https://github.com/rickysarraf/laptop-mode-tools](https://github.com/rickysarraf/laptop-mode-tools) || [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)

*   **[powertop](/index.php/Powertop "Powertop")** — Una herramienta para diagnosticar problemas con el consumo y la administración de energía para ayudarle a establecer ajustes de ahorro de energía.

	[https://01.org/powertop/](https://01.org/powertop/) || [powertop](https://www.archlinux.org/packages/?name=powertop)

*   **[systemd](/index.php/Systemd "Systemd")** — Un administrador de servicios y del sistema.

	[https://freedesktop.org/wiki/Software/systemd/](https://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[TLP](/index.php/TLP "TLP")** — Administración avanzada de energía de Linux.

	[http://linrunner.de/tlp](http://linrunner.de/tlp) || [tlp](https://www.archlinux.org/packages/?name=tlp)

### Gráficos

*   **batterymon-clone** — Simplemente un icono de la bandeja del sistema del monitor de la batería.

	[https://github.com/jareksed/batterymon-clone](https://github.com/jareksed/batterymon-clone) || [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/)

*   **cbatticon** — Icono de batería ligero y rápido que se encuentra en la bandeja del sistema.

	[https://github.com/valr/cbatticon](https://github.com/valr/cbatticon) || [cbatticon](https://www.archlinux.org/packages/?name=cbatticon)

*   **GNOME Power Statistics** — Información y estadísticas de la energía del sistema para GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-power-manager](https://gitlab.gnome.org/GNOME/gnome-power-manager) || [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager)

*   **KDE Power Devil** — Módulo de administración de energía para Plasma.

	[https://userbase.kde.org/Power_Devil](https://userbase.kde.org/Power_Devil) || [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/)

*   **LXQt Power Management** — Módulo de administración de energía para LXQt.

	[https://github.com/lxqt/lxqt-powermanagement](https://github.com/lxqt/lxqt-powermanagement) || [lxqt-powermanagement](https://www.archlinux.org/packages/?name=lxqt-powermanagement)

*   **MATE Power Management** — Herramientas de administración de energía para MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **MATE Power Statistics** — Información y estadísticas de la energía del sistema para MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **Xfce Power Manager** — Administración de energía para Xfce.

	[https://docs.xfce.org/xfce/xfce4-power-manager/start](https://docs.xfce.org/xfce/xfce4-power-manager/start) || [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager)

*   **vattery** — Aplicación de monitorización de la batería escrito en Vala que muestra el estado de la batería del portátil en la bandeja del sistema.

	[http://www.jezra.net/projects/vattery](http://www.jezra.net/projects/vattery) || [vattery](https://aur.archlinux.org/packages/vattery/)

## Administración de energía con systemd

### Eventos de ACPI

*Systemd* puede manejar algunos eventos [ACPI](https://en.wikipedia.org/wiki/es:Advanced_Configuration_and_Power_Interface "wikipedia:es:Advanced Configuration and Power Interface") (*«Interfaz Avanzada de Configuración y Energía»*) cuyas acciones pueden configurarse en `/etc/systemd/logind.conf` o en `/etc/systemd/logind.conf.d/*.conf` — vea [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5). En sistemas que no tienen un administrador de energía dedicado puede que los ajustes se remplacen con el demonio [acpid](/index.php/Acpid "Acpid") que se usa normalmente para reaccionar a los eventos ACPI.

La acción especificada para cada evento puede ser una de las siguientes: `ignore`, `poweroff`, `reboot`, `halt`, `suspend`, `hibernate`, `hybrid-sleep`, `suspend-then-hibernate`, `lock` o `kexec`. En caso de hibernar y suspender deben [ajustarse](/index.php/Power_management/Suspend_and_hibernate_(Espa%C3%B1ol) "Power management/Suspend and hibernate (Español)") apropiadamente. Si un evento no esta configurado *systemd* utilizara la acción por defecto.

| Controlador de evento | Descripción | Acción por defecto |
| `HandlePowerKey` | Especifica qué acción se invoca cuando el botón de encendido se pulsa. | `poweroff` |
| `HandleSuspendKey` | Especifica qué acción se invoca cuando se pulsa el botón de suspensión. | `suspend` |
| `HandleHibernateKey` | Especifica qué acción se invoca cuando se pulsa el botón de hibernación. | `hibernate` |
| `HandleLidSwitch` | Especifica qué acción se invoca cuando la tapa del portátil se cierra a excepción de los casos descritos más abajo. | `suspend` |
| `HandleLidSwitchDocked` | Especifica que acción se invoca la tapa del portátil se cierra si el sistema está insertado en una estación de acoplamiento o si hay más de una pantalla conectada. | `ignore` |
| `HandleLidSwitchExternalPower` | TEspecifica que acción se invoca la tapa del portátil se cierra si el sistema está conectado a una fuente de corriente externa. | Acción establecida por `HandleLidSwitch` |

Para aplicar cualquier cambio [reinicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `systemd-logind.service` (esto terminará todas las sesiones iniciadas).

**Nota:** *Systemd* no puede manejar los eventos de AC y de Batería que realiza ACPI, así que sigue siendo necesario el uso de [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") u otras herramientas similares a [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)").

#### Administradores de energía

Algunos [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") incluyen administradores de energía que [inhiben](http://www.freedesktop.org/wiki/Software/systemd/inhibit/) (desactiva temporalmente) algunos o todos los ajustes ACPI de *systemd*. Si hay algún administrador de energía ejecutándose las acciones ACPI solo se pueden configurar en el administrador de energía. Los cambios en `/etc/systemd/logind.conf` o `/etc/systemd/logind.conf.d/*.conf` solo se necesitan hacer solo si desea configurar algún evento particular que no inhibe el administrador de energía.

Tenga en cuenta que el administrador de energía no inhibe *systemd* en los eventos apropiados en los que pueden terminar con una situación en la que *systemd* suspenda su sistema y después de que systemd lo despierte el otro administrador de energía vuelva a suspender el equipo. En diciembre de 2016 los administradores de energía como [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"), [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), [Xfce](/index.php/Xfce_(Espa%C3%B1ol) "Xfce (Español)") y [MATE](/index.php/MATE_(Espa%C3%B1ol) "MATE (Español)") solucionan los comandos necesarios *inhibidos*. Si los comandos *inhibidos* no se han solucionado, como cuando se utiliza [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)") o otros administradores de eventos ACPI, establezca la opción `Handle` a `ignore`. Vea también [systemd-inhibit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-inhibit.1).

#### xss-lock

[xss-lock](https://www.archlinux.org/packages/?name=xss-lock) Funciona con los eventos de systemd `suspend`, `hibernate`, `lock-session`, y `unlock-session` con las acciones apropiadas (ejecutar el bloqueador y espera al usuario para desbloquearse o terminar el bloqueador). *xss-lock* también reacciona a los eventos [DPMS](/index.php/DPMS "DPMS") y ejecuta o termina el bloqueador en respuesta.

Inicie xss-lock en su [archivo de inicio en el arranque](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)") así:

```
xss-lock -- i3lock -n -i *background_image.png* &

```

### Suspensión e hibernación

*Systemd* proporciona órdenes para suspender en RAM, hibernar y una suspensión hibrida usando le funcionalidad de suspensión/reanudación nativa del kernel. También existen mecanismos para agregar hooks para personalizar las acciones de pre y post-suspensión.

`systemctl suspend` debería funcionar tras su instalación, sin embargo, para que `systemctl hibernate` pueda trabajar en su sistema debe seguir las instrucciones de [hibernar](/index.php/Power_management/Suspend_and_hibernate_(Espa%C3%B1ol)#Hibernar "Power management/Suspend and hibernate (Español)").

Aquí hay dos modos de combinar la suspensión y la hibernación:

*   `systemctl hybrid-sleep` suspende el sistema en RAM y en disco, así cuando el sistema se quede completamente sin energía no se perderán los datos. Este modo se llama también [suspensión híbrida](/index.php/Power_management/Suspend_and_hibernate_(Espa%C3%B1ol) "Power management/Suspend and hibernate (Español)").
*   `systemctl suspend-then-hibernate` inicialmente suspende el sistema en RAM y si no se interrumpe en el periodo de tiempo especificado en `HibernateDelaySec` en [systemd-sleep.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.conf.5) el sistema se despertará utilizando una alarma RTC y se hibernará.

**Nota:** *Systemd* también puede utilizar otros [backends](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end") (como por ejemplo [Uswsusp](/index.php/Uswsusp "Uswsusp")), en conjunción con el banckend por defecto del *kernel*, con el fin de poner el ordenador a dormir o hibernar. Véase [Uswsusp con systemd](/index.php/Uswsusp#With_systemd "Uswsusp") para obtener un ejemplo.

#### Suspensión híbrida en suspensión o en hibernación

Es posible configurar systemd para que siempre haga una *suspensión híbrida* cuando se realice una petición de *suspensión* o *hibernación*.

La acción por defecto de *suspender* e *hibernar* se pueden configurar en el archivo `/etc/systemd/sleep.conf`. Para establecer ambas acciones a *suspensión híbrida*:

 `/etc/systemd/sleep.conf` 
```
[Sleep]
# suspend=hybrid-sleep
SuspendMode=suspend
SuspendState=disk
# hibernate=hybrid-sleep
HibernateMode=suspend
HibernateState=disk
```

Vea la página [sleep.conf.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.conf.d.5) del manual para más detalles y la [documentación de los estados de energía del kernel linux](https://www.kernel.org/doc/html/latest/admin-guide/pm/sleep-states.html#basic-sysfs-interfaces-for-system-suspend-and-hibernation).

### Sleep hooks

#### Archivos de servicios para suspender/reanudar

Los archivos de servicios pueden ser asociados a *suspend.target*, *hibernate.target*, *sleep.target*, *hybrid-sleep.target* y *suspend-then-hibernate.target* para ejecutar acciones antes o después de suspender/hibernar. Deben crearse archivos separados para las acciones del usuario y las acciones de root/sistema. [Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") los servicios `suspend@*user*` y `resume@*user*` para que se inicien en el arranque. Ejemplos:

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=User suspend actions
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= -/usr/bin/pkill -u %u unison ; /usr/local/bin/music.sh stop ; /usr/bin/mysql -e 'slave stop'
ExecStart=/usr/bin/sflock

[Install]
WantedBy=sleep.target
```
 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStartPre=/usr/local/bin/ssh-connect.sh
ExecStart=/usr/bin/mysql -e 'slave start'

[Install]
WantedBy=suspend.target
```

**Nota:** Los bloqueadores de pantalla puede que vuelvan antes de que la pantalla se halla "bloqueado" y puede retomar la suspensión. Añadir un pequeño tiempo via `ExecStartPost=/usr/bin/sleep 1` ayuda a prevenir esto.

Para las acciones de root/sistema ([active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `root-resume` y los servicios `root-suspend` para iniciarlos en el arranque):

 `/etc/systemd/system/root-suspend.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=simple
ExecStart=/usr/bin/systemctl restart mnt-media.automount

[Install]
WantedBy=suspend.target
```
 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system suspend actions
Before=sleep.target

[Service]
Type=simple
ExecStart=-/usr/bin/pkill -9 sshfs

[Install]
WantedBy=sleep.target
```

**Sugerencia:** Unos consejos útiles acerca de estos archivos de servicio (más información en [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)):

*   Si está presente `Type=OneShot`, entonces puede utilizar múltiples líneas `ExecStart=`. De lo contrario, solo está permitida una línea ExecStart. No obstante, puede agregar más órdenes con `ExecStartPre` o mediante la separación de las órdenes con un punto y coma (véase el primer ejemplo de arriba; fíjese en los espacios en blanco antes y después del punto y coma... ¡estos son necesarios!).
*   Una orden con un prefijo `-` causará un código de salida distinto de cero que será ignorado y la orden será tratada como cumplida.
*   El mejor método para encontrar errores a fin de solucionar problemas con estos archivos de servicios es, por supuesto, con [journalctl](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)").

#### Archivo de servicio combinando suspensión/reanudación

Con el archivo de servicio que combina suspender/reanudar, un solo hook puede hacer todo el trabajo para las diferentes fases (dormir/continuar) y para diferentes objetivos (suspender/hibernar/suspensión híbrida).

He aquí un ejemplo y su explicación:

 `/etc/systemd/system/wicd-sleep.service` 
```
[Unit]
Description=Wicd sleep hook
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=-/usr/share/wicd/daemon/suspend.py
ExecStop=-/usr/share/wicd/daemon/autoconnect.py

[Install]
WantedBy=sleep.target
```

*   `RemainAfterExit=yes`: Después de que se inicie el servicio se mantendrá siempre activo hasta que se detenga explícitamente.
*   `StopWhenUnneeded=yes`: Cuando se active, el servicio se detendrá si ningún servicio activo lo requiere. En este caso el servicio se detendrá después de que se detenga *sleep.target*.
*   Debido a que *sleep.target* es apartado por *suspend.target*, *hibernate.target* y *hybrid-sleep.target* y debido a que *sleep.target* es en sí mismo un servicio *StopWhenUnneeded* garantiza que el hook iniciará/detendrá correctamente las diferentes tareas.

#### Hooks en /usr/lib/systemd/system-sleep

**Systemd** iniciará todos los archivos ejecutables ubicados en `/usr/lib/systemd/system-sleep/`, y pasará dos argumentos a cada uno de ellos:

*   Argument 1: o bien `pre` o `post`, dependiendo de si la máquina se está durmiendo o despertando.
*   Argument 2: `suspend`, `hibernate` o `hybrid-sleep`, dependiendo de lo que se ha invocado.

*Systemd* ejecutará estos scripts en paralelo y no uno tras el otro.

Las salidas de cualquier script personalizado se registrarán por *systemd-suspend.service*, *systemd-hibernate.service* o *systemd-hybrid-sleep.service*. Se pueden ver las salidas en el [journal](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)") de systemd:

```
# journalctl -b -u systemd-suspend.service

```

**Nota:** Tenga en cuenta que también puede utilizar *sleep.target*, *suspend.target*, *hibernate.target* o *hybrid-sleep.target* para conectar la unidad al estado de suspensión, en lugar de utilizar scripts personalizados.

He aquí un ejemplo de script de sleep personalizado:

 `/usr/lib/systemd/system-sleep/example.sh` 
```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    ;;
  post/*)
    echo "Waking up from $2..."
    ;;
esac
```

No debemos olvidarnos de hacer el script ejecutable:

```
# chmod a+x /usr/lib/systemd/system-sleep/example.sh

```

Véanse [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7) y [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8) para obtener más información.

### Solución de problemas

#### Acción retardada del interruptor de la tapa

Al hacer cambios en la tapa muy rápido, *logind* retarda la acción de suspender hasta 90s para detectar posibles muelles. [[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-January/027131.html) Este retardo se hizo configurable en systemd v220: [[2]](https://github.com/systemd/systemd/commit/9d10cbee89ca7f82d29b9cb27bef11e23e3803ba)

 `/etc/systemd/logind.conf` 
```
...
HoldoffTimeoutSec=30s
...
```

#### La suspensión desde la tecla Fn correspondiente del portátil no funciona

Si, independientemente de la configuración de logind.conf, el botón dormir no funciona (presionándolo no produce ningún mensaje en syslog) logind probablemente no vea el dispositivo de teclado. [[3]](http://lists.freedesktop.org/archives/systemd-devel/2015-February/028325.html) Realice:

```
# journalctl --grep="Watching system buttons"

```

Debería ver algo como esto:

```
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event2 (Power Button)
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event3 (Sleep Button)
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event4 (Video Bus)

```

Note que no hay ningún dispositivo teclado. Ahora obtenga el nombre ATTRS del dispositivo de teclado [[4]](http://systemd-devel.freedesktop.narkive.com/Rbi3rjNN/patch-1-2-logind-add-support-for-tps65217-power-button) :

 `# udevadm info -a /dev/input/by-path/*-kbd` 
```
...
KERNEL=="event0"
...
ATTRS{name}=="AT Translated Set 2 keyboard"
```

Ahora escriba una regla personalizada udev para añadir la etiqueta "power-switch":

 `/etc/udev/rules.d/70-power-switch-my.rules` 
```
ACTION=="remove", GOTO="power_switch_my_end"
SUBSYSTEM=="input", KERNEL=="event*", ATTRS{name}=="AT Translated Set 2 keyboard", TAG+="power-switch"
LABEL="power_switch_my_end"

```

Reinicie los servicios y recargue las reglas:

```
# systemctl restart systemd-udevd.service
# udevadm trigger
# systemctl restart systemd-logind.service

```

Ahora debe ver `Watching system buttons on /dev/input/event0` en syslog.

## Ahorrar energía

**Nota:** Vea la [configuración de ordenadores portátiles](/index.php/Laptop_(Espa%C3%B1ol)#Configuración_de_ordenadores_portátiles "Laptop (Español)") para administraciones específicas de energía para portátiles como el monitoreo de la batería.

Esta sección es una referencia para crear scripts personalizados y ajustar el ahorro energético mediante las reglas udev. Asegurese de que no están administradas por alguna [otra herramienta](#Herramientas_de_espacio_del_usuario) para evitar conflictos.

Casi todas las características que se listan aquí serán útiles dependiendo de si el ordenador está conectado a corriente o a la batería. Muchas tiene un impacto considerable en el rendimiento y no están habilitadas por defecto porque normalmente causan problemas con los controladores/hardware. Reducir el uso de energía significa reducir el calor con el que se puede conseguir un mayor rendimiento en un CPU Intel o AMD moderno gracias al [overclocking dinámico](https://en.wikipedia.org/wiki/es:Intel_Turbo_Boost "wikipedia:es:Intel Turbo Boost").

### Procesadores con soporte HWP (Hardware P-state)

Las preferencias disponibles para la energía de un procesador que soporta HWP son `default performance balance_performance balance_power power`.

Esto se puede comprobar con `$ cat /sys/devices/system/cpu/cpufreq/policy?/energy_performance_available_preferences`

Para conservar más energía puede configurarlo creando la siguiente línea:

 `/etc/tmpfiles.d/energy_performance_preference.conf` 
```
w /sys/devices/system/cpu/cpufreq/policy?/energy_performance_preference - - - - balance_power

```

Vea las páginas de manual [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) y [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) para más detalles.

### Audio

Por defecto el ahorro de energía de audio está apagado por muchos controladores. Se puede activar ajustando el parámetro `power_save`: tiempo (en segundos) para cambiar al modo en reposo. Para dejar en reposo la tarjeta de sonido después de un segundo crea la siguiente línea para las tarjetas de sonido Intel.

 `/etc/modprobe.d/audio_powersave.conf`  `options snd_hda_intel power_save=1` 

Alternativamente, utilice la siguiente para ac97:

```
options snd_ac97_codec power_save=1

```

**Nota:**

*   Para recuperar el fabricante y el controlador correspondiente del núcleo que se está utilizando en su tarjeta de sonido ejecute `lspci -k`.
*   Cambiar el estado de energía de las tarjetas de sonido puede causar que suene un estallido o una latencia notable en algún dispositivo roto.

Es posible reducir los requerimientos de energía de audio desactivando la salida de audio HDMI que se puede hacer añadiendo en la [lista negra](/index.php/Kernel_module_(Espa%C3%B1ol)#Lista_negra "Kernel module (Español)") los módulos del núcleo apropiados (por ejemplo en caso de dispositivos Intel `snd_hda_codec_hdmi`).

### Retroiluminación

Vea [retroiluminación](/index.php/Backlight "Backlight").

### Bluetooth

Para desactivar completamente el bluetooth añada en la [lista negra](/index.php/Kernel_module_(Espa%C3%B1ol)#Lista_negra "Kernel module (Español)") los módulos `btusb` y `bluetooth`.

Para apagar el bluetooth temporalmente utilice *rfkill*:

```
# rfkill block bluetooth

```

O con una regla udev:

 `/etc/udev/rules.d/50-bluetooth.rules` 
```
# disable bluetooth
SUBSYSTEM=="rfkill", ATTR{type}=="bluetooth", ATTR{state}="0"

```

### Cámara web

Si no va a utilizar la cámara web integrada añada en la [lista negra](/index.php/Kernel_module_(Espa%C3%B1ol)#Lista_negra "Kernel module (Español)") el módulo `uvcvideo`.

### Parámetros Kernel

Esta sección utiliza las configuraciones en `/etc/sysctl.d/` que es *"un directorio para los parámetros de sysctl del kernel."* Vea [Los nuevos archivos de configuración](http://0pointer.de/blog/projects/the-new-configuration-files) y más especificamente [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5) para más información.

#### Desactivar NMI watchdog

El watchdog [NMI](https://en.wikipedia.org/wiki/es:Interrupci%C3%B3n_no_enmascarable "wikipedia:es:Interrupción no enmascarable") es una característica de desarrollador que captura los cuelgues que causan el kernel panic. En algunos sistemas puede generar muchas interrupciones causando un aumento del uso energético:

 `/etc/sysctl.d/disable_watchdog.conf`  `kernel.nmi_watchdog = 0` 

o añada `nmi_watchdog=0` al [parámetro kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para desactivarlo completamente desde el principio del arranque.

#### Tiempo de reescritura

Aumentando el tiempo de reescritura de la sucia memoria virtual ayuda a agregar discos I/O juntos reduciendo así las escrituras en disco distribuidas y aumentando el ahorro energético. Para establecer este valor en 60 segundos (por defecto está en 5 segundos):

 `/etc/sysctl.d/dirty.conf`  `vm.dirty_writeback_centisecs = 6000` 

Para hacer lo mismo con las actualizaciones de journal en los sistemas de ficheros soportados (p.ej. ext4, btrfs...) utilice `commit=60` como una opción en [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)").

Note que modificando este valor tiene un efecto secundario de la configuración del modo portátil descrito a continuación. Vea también [memoria virtual](/index.php/Sysctl#Virtual_memory "Sysctl") para otros parámetros que afectan al rendimiento I/O y ahorran energía.

#### Modo portátil

Vea la [documentación del kernel](https://www.kernel.org/doc/Documentation/laptops/laptop-mode.txt) en el modo portatil 'knob.' *"Un valor sensible para knob es 5 segundos."*

 `/etc/sysctl.d/laptop.conf`  `vm.laptop_mode = 5` 
**Nota:** Estos ajustes son relevantes para los controladores de discos giratorios.

### Interfaces de red

[Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") Puede ser una característica útil pero si no va hacer uso de ella es simplemente un consumo extra de energía esperando un paquete mágico mientras está en suspensión. Puede adaptar la regla [udev](/index.php/Wake-on-LAN#udev "Wake-on-LAN") para deactivar la característica para todas las interfaces de red. Para activar el ahorro de energía con [iw](https://www.archlinux.org/packages/?name=iw) en todas las interfaces inalámbricas:

 `/etc/udev/rules.d/**81**-wifi-powersave.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", RUN+="/usr/bin/iw dev $name set power_save on"` 

El nombre del archivo de configuración es importante. Con el uso de [nombres fijos de dispositivos](/index.php/Network_configuration_(Espa%C3%B1ol)#Cambiar_el_nombre_de_dispositivo "Network configuration (Español)"), en systemd la regla de red de arriba, nombrado léxico-gráficamente **después** `80-net-setup-link.rules`, se aplica después de que el servicio se renombre con un nombre fijo p.ej `wlan0` renombrada a `wlp3s0`. Tenga en cuenta que el comando `RUN` se ejecuta después de que todas las reglas se hayan procesado y tienen que utilizar de cualquier forma el nombre fijo disponible en `$name` para el dispositivo emparejado.

#### Tarjetas inalámbricas Intel (iwlwifi)

Se pueden activar funciones adicionales de ahorro de energía de las tarjetas inalámbricas Intel con el controlador `iwlwifi` pasando los parámetros correctos al módulo kernel. Para hacerlo permanente se puede guardad añadiendo la línea de debajo al archivo `/etc/modprobe.d/iwlwifi.conf` file:

```
options iwlwifi power_save=1 d0i3_disable=0 uapsd_disable=0
options iwldvm force_cam=0

```

Tenga en mente que estas opciones de ahorro de energía son experimentales y pueden causar inestabilidades en el sistema.

### Administración de energía bus

#### Administración de energía en estado activo

Si cree que el ordenador no soporta [ASPM](https://en.wikipedia.org/wiki/Active_State_Power_Management "wikipedia:Active State Power Management") se desactivará en el aranque:

```
# lspci -vv | grep 'ASPM.*abled;'

```

ASPM lo maneja la BIOS. Si ASPM está desactivado puede ser [porque](http://wireless.kernel.org/en/users/Documentation/ASPM):

1.  La BIOS lo ha desactivado por alguna razón (¿Por conflictos?).
2.  La PCIE requiere ASPM pero L0s es opcional (puede que L0s esté desactivado y solo esté activado L1).
3.  La BIOS aún no ha sido programada para ello.
4.  La BIOS esta defectuosa.

Si cree que el ordenador tiene soporte para ASPM se puede forzar al kernel que se encargue con el [parámetro kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `pcie_aspm=force`.

**Advertencia:**

*   Forzar ASPM puede causar un congelamiento/error fatal. Así que asegurese que tiene alguna forma de deshacer la opción si no funciona.
*   En los sistemas que no soportan forzar ASPM pueden incrementar el consumo de energía.
*   Esto fuerza ASPM en el kernel mientras puede estar desactivado en el hardware y no funcione. Para comprobar si este es el caso se puede utilizar el comando `dmesg | grep ASPM` y si es el caso se debe consultar el artículo Wiki específico del hardware.

Para ajustar el `powersave` ejecute (el siguiente comando no funcionara a no ser que este activado):

```
# echo powersave > /sys/module/pcie_aspm/parameters/policy

```

Por defecto se mostrara como esto:

 `$ cat /sys/module/pcie_aspm/parameters/policy` 
```
[default] performance powersave

```

#### Administración de energía PCI en tiempo de ejecución

 `/etc/udev/rules.d/pci_pm.rules`  `SUBSYSTEM=="pci", ATTR{power/control}="auto"` 

La regla de arriba apaga todos los dispositivos no utilizados pero algunos dispositivos no se despertarán. Para permitir la administración de energía PCI en tiempo de ejecución que sabe que funcionan utilice simplemente la combinación de vendedor y el ID del dispositivo (utilice `lspci -nn` para obtener estos valores):

 `/etc/udev/rules.d/pci_pm.rules` 
```
# Lista blanca para la auto suspensión pci
SUBSYSTEM=="pci", ATTR{vendor}=="0x1234", ATTR{device}=="0x1234", ATTR{power/control}="auto"

```

Alternativamente para poner en la lista negra los dispositivos que no funcionan con la administración de energía PCI en tiempo de ejecución y activarlo para todos los demás dispositivos:

 `/etc/udev/rules.d/pci_pm.rules` 
```
# Lista negra para la administración de energía PCI en tiempo de ejecución
SUBSYSTEM=="pci", ATTR{vendor}=="0x1234", ATTR{device}=="0x1234", ATTR{power/control}="on", GOTO="pci_pm_end"

SUBSYSTEM=="pci", ATTR{power/control}="auto"
LABEL="pci_pm_end"

```

#### Auto suspensión USB

El kernel Linux puede suspender automáticamente los dispositivos USB cuando no se utilizan. Esto ocasionalmente puede ahorrar un poco de energía. Sin embargo algunos dispositivos USB no son compatibles con el ahorro de energía USB y se inicia con un mal comportamiento (normalmente con ratones y teclados). Las reglas [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") basadas en la lista blanca o lista negra puede ayudar a mitigar el problema.

Lo más simple y seguramente inservible es habilitar la auto suspensión para todos los dispositivos USB:

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{power/control}="auto"

```

Para permitir auto suspender solo los dispositivos que sabe que van a funcionar simplemente utilice la combinación entre vendedor y el ID del producto (utilice *lsusb* para obtener estos valores):

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
# Lista blanca auto suspensión usb
ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{idVendor}=="05c6", ATTR{idProduct}=="9205", ATTR{power/control}="auto"

```

Alternativamente para poner en la lista negra los dispositivos que no funcionan con la auto suspensión USB y activarlo para el resto de dispositivos:

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
# Lista negra auto suspensión usb
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="05c6", ATTR{idProduct}=="9205", GOTO="power_usb_rules_end"

ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{power/control}="auto"
LABEL="power_usb_rules_end"

```

El tiempo de retardo por defecto en la auto suspensión se controla con el parámetro `autosuspend` del [módulo kernel](/index.php/Kernel_module_(Espa%C3%B1ol) "Kernel module (Español)") `usbcore`. Para establecer el retardo a 5 segundos en vez de los 2 segundos por defecto:

 `/etc/modprobe.d/usb-autosuspend.conf` 
```
options usbcore autosuspend=5

```

De forma similar para `power/control` el tiempo de retardo puede personalizarse para cada dispositivo ajustando el atributo `power/autosuspend`.

Vea la [documentación kernel de Linux](https://www.kernel.org/doc/Documentation/usb/power-management.txt) para más información sobre la administración de energía USB.

#### Administración de energía de enlace activo SATA

**Advertencia:** La administración de energía de enlace activo SATA puede ocasionar pérdida de datos en algunos dispositivos. No active estos ajustes a no haya ser que realice copias de seguridad frecuentemente.

Desde Linux 4.15 hay un [nuevo ajuste](https://hansdegoede.livejournal.com/18412.html) llamado `med_power_with_dipm` que marca el comportamiento de los ajustes del controlador Windows IRST y no debería causar pérdida de datos en discos SSD/HDD recientes. El ahorro de energía puede ser insignificante, entre [1.0 a 1.5 Vatios (en reposo)](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=ebb82e3c79d2a956366d0848304a53648bd6350b). Será un ajuste por defecto en los portátiles basados en Intel en Linux 4.16 [[5]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=ebb82e3c79d2a956366d0848304a53648bd6350b).

Los ajustes actuales se pueden leer desde `/sys/class/scsi_host/host*/link_power_management_policy` como sigue:

```
# cat /sys/class/scsi_host/host*/link_power_management_policy

```

<caption>Ajustes ALPM disponibles</caption>
| Ajuste | Descripción | Ahorro energético |
| max_performance | Actualmente por defecto | Ninguno |
| medium_power | - | ~1.0 Vatios |
| med_power_with_dipm | Ajuste recomendado | ~1.5 Vatios |
| min_power | **ADVERTENCIA: Posible pérdida de datos** | ~1.5 Vatios |

 `/etc/udev/rules.d/hd_power_save.rules`  `ACTION=="add", SUBSYSTEM=="scsi_host", KERNEL=="host*", ATTR{link_power_management_policy}="med_power_with_dipm"` 
**Nota:** Esto añade latencia cuando se accede al disco desde que este estaba en reposo, por tanto, es una de las pocas configuraciones que pueden valer la pena alternar en función de si está conectado a la alimentación de CA o no.

### Controlador de disco duro

Vea [Configuración energética hd](/index.php/Hdparm#Power_management_configuration "Hdparm") para más información sobre los parámentros que se pueden establecer.

El ahorro energético no es efectivo cuando varios programas están escribiendo en el disco duro. Siga todos los programas y como y cuando escriben en el disco para poder limitar el uso del disco. Utilice [iotop](https://www.archlinux.org/packages/?name=iotop) para ver qué programas utilizan el disco frecuentemente. Vea [mejorar el rendimiento de dispositivos de almacenamiento](/index.php/Improving_performance_(Espa%C3%B1ol)#Dispositivos_de_almacenamiento "Improving performance (Español)") para otros consejos.

También detalles como ajustar la opción [noatime](/index.php/Fstab_(Espa%C3%B1ol)#Opciones_atime "Fstab (Español)") puede ayudar. Si hay suficiente RAM disponible considere limitar o deshabilitar [swappiness](/index.php/Swap_(Espa%C3%B1ol)#Swappiness "Swap (Español)") limitando posiblemente un gran número de escrituras a disco.

### Controlador CD-ROM o DVD

Vea [dispositivos que no permanecen desmontados (udisks)](/index.php/Udisks#Devices_do_not_remain_unmounted_(udisks) "Udisks").

## Herramientas y scripts

### Utilizar un script y una regla udev

Desde que los usuarios de systemd pueden suspender o hibernar a través de `systemctl suspend` o `systemctl hibernate` y encargarse de los eventos acpi con `/etc/systemd/logind.conf` puede ser interesante eliminar *pm-utils* y [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)"). Solo hay una cosa que systemd no puede hacer (a partir de systemd-204): administrar la energía dependiendo su el sistema está ejecutando con AC o con batería. Para solventar esto puede crear una regla [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") simple que ejecute un script cuando el adaptador AC se conecte y desconecte:

 `/etc/udev/rules.d/powersave.rules` 
```
SUBSYSTEM=="power_supply", ATTR{online}=="0", RUN+="/path/to/your/script true"
SUBSYSTEM=="power_supply", ATTR{online}=="1", RUN+="/path/to/your/script false"

```

**Nota:** Puede utilizar el mismo script que utiliza *pm-powersave*. Solo lo tiene que hacer ejecutable y colocarlo en algún lugar (como por ejemplo `/usr/local/bin/`).

Ejemplo de un script de powersave:

*   [ftw](https://github.com/supplantr/ftw), paquete: [ftw-git](https://aur.archlinux.org/packages/ftw-git/)
*   [powersave](https://github.com/Unia/powersave)
*   [throttle](https://github.com/quequotion/pantheon-bzr-qq/blob/master/EXTRAS/indicator-powersave/throttle), de [indicator-powersave](https://aur.archlinux.org/packages/indicator-powersave/)

Las reglas udev de arriba suelen funcionar como se esperan pero su sus ajustes de energía no se actualizan después de suspender o hibernar debe añadir un script en `/usr/lib/systemd/system-sleep/` con el siguiente contenido:

 `/usr/lib/systemd/system-sleep/00powersave` 
```
#!/bin/sh

case $1 in
    pre) /ruta/a/su/script false ;;
    post)       
	if cat /sys/class/power_supply/AC0/online | grep 0 > /dev/null 2>&1
	then
    		/ruta/a/su/script true	
	else
    		/ruta/a/su/script false
	fi
    ;;
esac
exit 0

```

¡No olvide hacerlo ejecutable!

**Nota:** Tenga en cuenta que AC0 puede ser diferente en su portátil, cámbielo si ese es el caso.

### Ajustes de energía de la impresora

Este script ajusta la administra energéticamente la impresora y otras propiedades para los dispositivos PCI y USB. Note que se necesitan permisos root para ver todos los ajustes.

```
#!/bin/bash

for i in $(find /sys/devices -name "bMaxPower")
do
	busdir=${i%/*}
	busnum=$(<$busdir/busnum)
	devnum=$(<$busdir/devnum)
	title=$(lsusb -s $busnum:$devnum)

	printf "

+++ %s
  -%s
" "$title" "$busdir"

	for ff in $(find $busdir/power -type f ! -empty 2>/dev/null)
	do
		v=$(cat $ff 2>/dev/null|tr -d "
")
		[[ ${#v} -gt 0 ]] && echo -e " ${ff##*/}=$v";
		v=;
	done | sort -g;
done;

printf "

+++ %s
" "Kernel Modules"
for mod in $(lspci -k | sed -n '/in use:/s,^.*: ,,p' | sort -u)
do
	echo "+ $mod";
	systool -v -m $mod 2> /dev/null | sed -n "/Parameters:/,/^$/p";
done

```

## Vea también

*   [ThinkWiki:Como reducir el consumo energético (en inglés)](http://www.thinkwiki.org/wiki/How_to_reduce_power_consumption).
*   [Como tener una mayor duración de la batería en Linux (en inglés)](http://ivanvojtko.blogspot.sk/2016/04/how-to-get-longer-battery-life-on-linux.html).
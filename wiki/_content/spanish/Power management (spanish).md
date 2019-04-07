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
    *   [1.1 Console](#Console)
    *   [1.2 Graphical](#Graphical)
*   [2 Administración de energía con systemd](#Administración_de_energía_con_systemd)
    *   [2.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [2.2 Suspensión e hibernación](#Suspensión_e_hibernación)
    *   [2.3 Sleep hooks](#Sleep_hooks)
        *   [2.3.1 Archivos de servicios para suspender/reanudar](#Archivos_de_servicios_para_suspender/reanudar)
        *   [2.3.2 Archivo de servicio combinando suspensión/reanudación](#Archivo_de_servicio_combinando_suspensión/reanudación)
        *   [2.3.3 Hooks en /usr/lib/systemd/system-sleep](#Hooks_en_/usr/lib/systemd/system-sleep)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Activar opciones de ahorro de energía RC6](#Activar_opciones_de_ahorro_de_energía_RC6)
*   [4 Consulte también](#Consulte_también)

## Herramientas de espacio del usuario

Using these tools can replace setting a lot of settings by hand. Only run **one** of these tools to avoid possible conflicts as they all work more or less similarly. Have a look at the [power management category](/index.php/Category:Power_management "Category:Power management") to get an overview on what power management options exist in Arch Linux.

These are the more popular scripts and tools designed to help power saving:

### Console

*   **[acpid](/index.php/Acpid "Acpid")** — A daemon for delivering ACPI power management events with netlink support.

	[http://sourceforge.net/projects/acpid2/](http://sourceforge.net/projects/acpid2/) || [acpid](https://www.archlinux.org/packages/?name=acpid)

*   **[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")** — Utility to configure laptop power saving settings, considered by many to be the de facto utility for power saving though may take a bit of configuration.

	[https://github.com/rickysarraf/laptop-mode-tools](https://github.com/rickysarraf/laptop-mode-tools) || [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)

*   **[powertop](/index.php/Powertop "Powertop")** — A tool to diagnose issues with power consumption and power management to help set power saving settings.

	[https://01.org/powertop/](https://01.org/powertop/) || [powertop](https://www.archlinux.org/packages/?name=powertop)

*   **[systemd](/index.php/Systemd "Systemd")** — A system and service manager.

	[https://freedesktop.org/wiki/Software/systemd/](https://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[TLP](/index.php/TLP "TLP")** — Advanced power management for Linux.

	[http://linrunner.de/tlp](http://linrunner.de/tlp) || [tlp](https://www.archlinux.org/packages/?name=tlp)

### Graphical

*   **batterymon-clone** — Simple battery monitor tray icon.

	[https://github.com/jareksed/batterymon-clone](https://github.com/jareksed/batterymon-clone) || [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/)

*   **cbatticon** — Lightweight and fast battery icon that sits in your system tray.

	[https://github.com/valr/cbatticon](https://github.com/valr/cbatticon) || [cbatticon](https://www.archlinux.org/packages/?name=cbatticon)

*   **GNOME Power Statistics** — System power information and statistics for GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-power-manager](https://gitlab.gnome.org/GNOME/gnome-power-manager) || [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager)

*   **KDE Power Devil** — Power management module for Plasma.

	[https://userbase.kde.org/Power_Devil](https://userbase.kde.org/Power_Devil) || [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/)

*   **LXQt Power Management** — Power management module for LXQt.

	[https://github.com/lxqt/lxqt-powermanagement](https://github.com/lxqt/lxqt-powermanagement) || [lxqt-powermanagement](https://www.archlinux.org/packages/?name=lxqt-powermanagement)

*   **MATE Power Management** — Power management tool for MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **MATE Power Statistics** — System power information and statistics for MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **Xfce Power Manager** — Power manager for Xfce.

	[https://docs.xfce.org/xfce/xfce4-power-manager/start](https://docs.xfce.org/xfce/xfce4-power-manager/start) || [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager)

*   **vattery** — Battery monitoring application written in Vala that will display the status of a laptop battery in a system tray.

	[http://www.jezra.net/projects/vattery](http://www.jezra.net/projects/vattery) || [vattery](https://aur.archlinux.org/packages/vattery/)

## Administración de energía con systemd

### Eventos de ACPI

Systemd puede manejar algunos eventos [ACPI](https://en.wikipedia.org/wiki/es:Advanced_Configuration_and_Power_Interface "wikipedia:es:Advanced Configuration and Power Interface") (*«Interfaz Avanzada de Configuración y Energía»*) relacionados con la energía. Esto se configura a través de las siguientes opciones en `/etc/systemd/logind.conf`:

*   `HandlePowerKey`: especifica qué acción se invoca cuando el botón de encendido se pulsa.
*   `HandleSuspendKey`: especifica qué acción se invoca cuando se pulsa el botón de suspensión.
*   `HandleHibernateKey`: especifica qué acción se invoca cuando se pulsa el botón de hibernación.
*   `HandleLidSwitch`: especifica qué acción se invoca cuando la tapa del portátil es cerrada.

La acción especificada puede ser una cualquiera de las siguientes: `ignore`, `poweroff`, `reboot`, `halt`, `suspend`, `hibernate` o `kexec`.

Si estas opciones no están configuradas, systemd utilizará los valores predeterminados: `HandlePowerKey=poweroff`, `HandleSuspendKey=suspend`, `HandleHibernateKey=hibernate`, y `HandleLidSwitch=suspend`.

En los sistemas que funcionan sin configuración gráfica o solo un simple administrador de ventanas como [i3](/index.php/I3 "I3") o [awesome](/index.php/Awesome "Awesome"), esto puede reemplazar al demonio [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)") que se utiliza generalmente para administrar estos eventos ACPI.

**Nota:**

*   Ejecute `systemctl restart systemd-logind.service` para que los cambios surtan efecto.
*   Systemd no puede manejar los eventos de AC y de Batería que realiza ACPI, así que sigue siendo necesario el uso de [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") u otras herramientas similares a [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)").

En la versión actual de systemd, las opciones `Handle*` se aplican a todo el sistema, a menos que sean «inhibidas» (desactivadas temporalmente) por un programa, como un administrador de energía de un entorno de escritorio. Si estos inhibidores no son usados, se puede terminar en una situación en la que systemd suspenda el sistema, para luego, cuando se active el administrador de energía, este lo suspenda de nuevo.

**Advertencia:** Actualmente, los administradores de energía en las nuevas versiones de [KDE](/index.php/KDE "KDE") y [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") son los únicos que poseen los comandos necesarios para «inhibir». Hasta tanto los otros lo hagan, tendrá que configurar manualmente las opciones `Handle` a `ignore` si desea administrar los eventos ACPI con [Xfce](/index.php/Xfce "Xfce"), [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)") u otros programas.

### Suspensión e hibernación

*systemd* proporciona órdenes para suspender en RAM, hibernar y una suspensión hibrida usando le funcionalidad de suspensión/reanudación nativa del kernel. También existen mecanismos para agregar hooks para personalizar las acciones de pre y post-suspensión.

**Nota:** *systemd* también puede utilizar otros [backends](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end") (como por ejemplo [Uswsusp](/index.php/Uswsusp "Uswsusp") o [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")), en conjunción con el banckend por defecto del *kernel*, con el fin de poner el ordenador a dormir o hibernar. Véase [Uswsusp#With systemd](/index.php/Uswsusp#With_systemd "Uswsusp") para obtener un ejemplo.

`systemctl suspend` debería funcionar tras su instalación, sin embargo, para que `systemctl hibernate` pueda trabajar en su sistema debe seguir las instrucciones de [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate").

### Sleep hooks

#### Archivos de servicios para suspender/reanudar

Los archivos de servicios pueden ser asociados a suspend.target, hibernate.target y sleep.target para ejecutar acciones antes o después de suspender/hibernar. Deben crearse archivos separados para las acciones del usuario y las acciones de root/sistema. Para activar los archivos de servicios del usuario, ejecute: `# systemctl enable suspend@<usuario> && systemctl enable resume@<usuario>`. Ejemplos:

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=User suspend actions
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= -/usr/bin/pkill -u %u unison ; /usr/local/bin/music.sh stop ; /usr/bin/mysql -e 'slave stop'
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

Para las acciones de root/sistema (se activa con `# systemctl enable root-suspend`):

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

Unos consejos útiles acerca de estos archivos de servicio (más información en [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)):

*   Si está presente `Type=OneShot`, entonces puede utilizar múltiples líneas `ExecStart=`. De lo contrario, solo está permitida una línea ExecStart. No obstante, puede agregar más órdenes con `ExecStartPre` o mediante la separación de las órdenes con un punto y coma (véase el primer ejemplo de arriba —fíjese en los espacios en blanco antes y después del punto y coma... ¡estos son necesarios!—).
*   Una orden con un prefijo `-` causará un código de salida distinto de cero que será ignorado y la orden será tratada como cumplida.
*   El mejor método para encontrar errores a fin de solucionar problemas con estos archivos de servicios es, por supuesto, con `journalctl`.

#### Archivo de servicio combinando suspensión/reanudación

Con el archivo de servicio que combina suspender/reanudar, un solo hook puede hacer todo el trabajo para las diferentes fases (sleep/resume) y para diferentes objetivos (suspend/hibernate/hybrid-sleep).

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

*   `RemainAfterExit=yes`: Después de iniciado, el servicio se mantiene siempre activo hasta que se detenga explícitamente.
*   `StopWhenUnneeded=yes`: Cuando se activa, el servicio se detendrá después de que se detenga sleep.target.
*   Debido a que sleep.target es apartado por suspend.target, hibernate.target y hybrid-sleep.target y sleep.target son en sí mismo un servicio StopWhenUnneeded, lo que nos garantiza que el hook iniciará/detendrá correctamente las diferentes tareas.

#### Hooks en /usr/lib/systemd/system-sleep

**systemd** iniciará todos los archivos ejecutables ubicados en `/usr/lib/systemd/system-sleep/`, y pasará dos argumentos a cada uno de ellos:

*   Argument 1: o bien `pre` o `post`, dependiendo de si la máquina se está durmiendo o despertando.
*   Argument 2: `suspend`, `hibernate` o `hybrid-sleep`, ependiendo de lo que se ha invocado.

systemd ejecutará estos scripts en paralelo y no uno tras el otro.

Las salidas de cualquier script personalizado se registrarán por `systemd-suspend.service`, `systemd-hibernate.service` o `systemd-hybrid-sleep.service`. Se pueden ver las salidas en el [journal](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)") de systemd:

```
# journalctl -b -u systemd-suspend

```

**Nota:** Tenga en cuenta que también puede utilizar `sleep.target`, `suspend.target`, `hibernate.target` o `hybrid-sleep.target` para conectar la unidad al estado de suspensión, en lugar de utilizar scripts personalizados.

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

## Solución de problemas

### Activar opciones de ahorro de energía RC6

```
 i915_enable_rc6=#Nr

```

Donde *#Nr*:

*   **1**: activa rc6
*   **3**: activa rc6 y profundiza rc6
*   **5**: activa rc6 y profundiza más rc6
*   **7**: activa rc6, y profundiza aún más rc6

## Consulte también

*   [Laptop#Power management](/index.php/Laptop#Power_management "Laptop") describes power management specific for laptops - especially battery monitoring.
*   [Administración de energía en Recomendaciones generales](/index.php/General_recommendations_(Espa%C3%B1ol)#Administración_de_energía "General recommendations (Español)")
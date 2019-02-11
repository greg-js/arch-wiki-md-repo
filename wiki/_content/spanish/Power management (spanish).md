Artículos relacionados

*   [Power saving](/index.php/Power_saving "Power saving")
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")

El propósito de esta página es proporcionar información general sobre la administración de energía en Arch Linux. Como Arch Linux utiliza [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), como administrador del sistema, este artículo se centra en él.

Hay varios lugares donde se puede cambiar la configuración de administración de energía:

*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   Reglas [udevs](/index.php/Udev "Udev")

También hay muchas herramientas de administración de energía:

*   [systemd](/index.php/Systemd "Systemd")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [TLP](/index.php/TLP "TLP")
*   [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)")

**Nota:** Los ajustes relativos a la energía que se han establecido en un lugar/con alguna herramienta, pueden ser sobrescritos en otro lugar/con otras herramientas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Administración de energía con systemd](#Administración_de_energía_con_systemd)
    *   [1.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [1.2 Suspensión e hibernación](#Suspensión_e_hibernación)
    *   [1.3 Sleep hooks](#Sleep_hooks)
        *   [1.3.1 Archivos de servicios para suspender/reanudar](#Archivos_de_servicios_para_suspender/reanudar)
        *   [1.3.2 Archivo de servicio combinando suspensión/reanudación](#Archivo_de_servicio_combinando_suspensión/reanudación)
        *   [1.3.3 Hooks en /usr/lib/systemd/system-sleep](#Hooks_en_/usr/lib/systemd/system-sleep)
*   [2 Solución de problemas](#Solución_de_problemas)
    *   [2.1 Activar opciones de ahorro de energía RC6](#Activar_opciones_de_ahorro_de_energía_RC6)
*   [3 Consulte también](#Consulte_también)

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
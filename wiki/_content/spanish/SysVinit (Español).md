**Advertencia:** SysVinit está en desuso en Arch Linux [[1]](https://www.archlinux.org/news/end-of-initscripts-support/) y se ha retirado de los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)"). Es necesario actualizar a [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

En los sistemas basados en SysVinit, **init** es el primer proceso que se ejecuta una vez que se carga el Kernel de Linux. Por defecto, el programa init usado por el kernel es `/sbin/init` proveido por [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) (de forma predeterminada en las instalaciones nuevas, véase [systemd](/index.php/Systemd "Systemd")) o [sysvinit](https://aur.archlinux.org/packages/sysvinit/). La palabra **init** siempre se refiere a sysvinit en este artículo.

**inittab** es el archivo de configuración inicial que encuentra init en `/etc`. Contiene las instrucciones de inicio de los programas y scripts que van a funcionar al iniciar el nivel de ejecución especificado.

Aunque un sistema Arch basado en SysVinit no utiliza init, la mayor parte del trabajo se delega en los [#Scripts Principales de Arranque](#Scripts_Principales_de_Arranque). Este artículo se centra en init e inittab.

## Contents

*   [1 Migración a systemd](#Migraci.C3.B3n_a_systemd)
    *   [1.1 Consideraciones previas antes de pasarse a systemd](#Consideraciones_previas_antes_de_pasarse_a_systemd)
    *   [1.2 Proceder a la instalación](#Proceder_a_la_instalaci.C3.B3n)
    *   [1.3 Información complementaria](#Informaci.C3.B3n_complementaria)
*   [2 Descripción de init e inittab](#Descripci.C3.B3n_de_init_e_inittab)
*   [3 Instalación](#Instalaci.C3.B3n)
*   [4 Cambiar runlevel (nivel de ejecución)](#Cambiar_runlevel_.28nivel_de_ejecuci.C3.B3n.29)
    *   [4.1 A través del gestor de arranque](#A_trav.C3.A9s_del_gestor_de_arranque)
    *   [4.2 Después de arrancar](#Despu.C3.A9s_de_arrancar)
*   [5 inittab](#inittab)
    *   [5.1 Runlevel por defecto](#Runlevel_por_defecto)
    *   [5.2 Scripts principales de arranque](#Scripts_principales_de_arranque)
    *   [5.3 Arranque en modalidad de usuario único](#Arranque_en_modalidad_de_usuario_.C3.BAnico)
    *   [5.4 Gettys e inicio de sesión](#Gettys_e_inicio_de_sesi.C3.B3n)
    *   [5.5 Ctrl+Alt+Supr](#Ctrl.2BAlt.2BSupr)
    *   [5.6 Programas de X](#Programas_de_X)
    *   [5.7 Scripts Power-Sensing](#Scripts_Power-Sensing)
    *   [5.8 Solicitud de teclado personalizado](#Solicitud_de_teclado_personalizado)
        *   [5.8.1 Lanzar kbrequest](#Lanzar_kbrequest)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)
*   [7 Enlaces externos](#Enlaces_externos)

## Migración a systemd

**Nota:**

*   [systemd](https://www.archlinux.org/packages/?name=systemd) y [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) son utilizados de forma predeterminada en los nuevos soportes de instalación desde el [2012-10-13](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/). Esta sección está dedicada a las instalaciones de Arch Linux que todavía dependen de sysvinit e initscripts.
*   Si se está utilizando Arch Linux en un [VPS](https://en.wikipedia.org/wiki/es:Servidor_virtual_privado "wikipedia:es:Servidor virtual privado"), véase [la página apropiada](https://wiki.archlinux.org/index.php/Virtual_Private_Server#Moving_your_VPS_from_initscripts_to_systemd).

### Consideraciones previas antes de pasarse a systemd

*   Para una aproximación al tema son recomendables [algunas lecturas](http://freedesktop.org/wiki/Software/systemd/) acerca de systemd.
*   Tenga en cuenta el hecho de que _systemd_ tiene un sistema _journal_ que sustituye a _syslog_, aunque los dos pueden coexistir. Véase la [sección sobre journal](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)").
*   Aunque systemd puede reemplazar algunas de las funcionalidades de _cron_, _acpid_, o _xinetd_, no hay necesidad de abandonar el uso de los demonios tradicionales a menos que así lo desee.
*   La interacción con los initscripts no está funcionando con systemd. En particular, _netcfg-menu_ [no puede](https://bugs.archlinux.org/task/31377) ser usado al inicio del sistema.

### Proceder a la instalación

1.  Instale [systemd](https://www.archlinux.org/packages/?name=systemd) y añada a la [línea de órdenes del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") lo siguiente: `init=/usr/lib/systemd/systemd`
2.  Una vez hecho, puede habilitar los servicios deseados mediente el uso de `systemctl enable <nombre_del_servicio>` (los cuales equivalen aproximadamente a los demonios incluidos en la matriz `DAEMONS` con [nombres diferentes](/index.php/Daemons_List "Daemons List")).
3.  Reinicie el sistema y compruebe que `systemd` está realmente activo mediante la orden siguiente: `cat /proc/1/comm`. Esta debería devolver la salida: `systemd`.
4.  Asegúrese de que el nombre del equipo está configurado correctamente en systemd: `hostnamectl set-hostname elnombredemiequipo` o `/etc/hostnam`.
5.  Proceda a eliminar [initscripts](https://www.archlinux.org/packages/?name=initscripts) y [sysvinit](https://aur.archlinux.org/packages/sysvinit/) del sistema e instale [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat).
6.  Opcionalmente, retire el parámetro `init=/usr/lib/systemd/systemd` en cuanto que ya no es necesario. [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) proporciona un enlace simbólico a init de _systemd_ cuando _sysvinit_ es usado

### Información complementaria

*   Se si utiliza `quiet` en los parámetros del kernel, es posible removerlo durante el primer incio de systemd para identificar eventuales problemas durante el arranque.

*   No es necesario añadir su usuario a los [grupos](/index.php/Users_and_Groups_(Espa%C3%B1ol) "Users and Groups (Español)") (`sys`, `disk`, `lp`, `network`, `video`, `audio`, `optical`, `storage`, `scanner`, `power`, etc.) para la mayoría de los casos con systemd. Los grupos pueden, incluso, causar alguna disfuncionalidad. Por ejemplo, el grupo de audio impedirá el cambio rápido de usuarios y permitirá que las aplicaciones bloqueen el software de mezcla. Cada inicio de sesión PAM proporciona una sesión logind, que, durante una sesión local, le dará permisos a través de [POSIX ACLs](https://en.wikipedia.org/wiki/es:Lista_de_control_de_acceso "wikipedia:es:Lista de control de acceso") para dispositivos de audio/vídeo, y permitirá ciertas operaciones, como el montaje de discos extraíbles, a través de [udisks](/index.php/Udev_(Espa%C3%B1ol)#Udisks "Udev (Español)").

*   Consulte el artículo sobre [Network Configuration](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)") para saber cómo configurar los targets de las conexiones de red.

## Descripción de init e inittab

init es siempre un proceso y, aparte de gestionar el espacio de intercambio, es el proceso padre a **todos** los demás procesos. Usted puede imaginar dónde se encuentra init en la jerarquía de procesos de su sistema con `pstree`:

 `$ pstree -Ap` 

```
init(1)-+-acpid(3432)
        |-crond(3423)
        |-dbus-daemon(3469)
        |-gpm(3485)
        |-mylogin(3536)
        |-ngetty(3535)---login(3954)---zsh(4043)---pstree(4326)
        |-polkitd(4033)---{polkitd}(4035)
        |-syslog-ng(3413)---syslog-ng(3414)
        `-udevd(643)-+-udevd(3194)
                     `-udevd(3218)

```

Además de la inicialización normal del sistema (como su nombre indica), init también se encarga de reiniciar, apagar y arrancar en modo de recuperación (single-user mode).

Para apoyar a ésto, inittab contiene grupos con diferentes **niveles de ejecución** .

Los niveles de ejecución usados por Arch son 0 para detener, 1 (S como alias) para el modo single-user, 3 para el arranque normal (modo multi-usuario), 5 para X y 6 para reiniciar el sistema. Otras distribuciones pueden adoptar otros convenios, pero los significados de 0, 1 y 6 son universales.

Tras la ejecución, init explora inittab y lleva a cabo las acciones oportunas. Una entrada en inittab toma la forma siguiente:

```
id:runlevels:action:process

```

Donde `id` es un identificador único para la entrada (sólo un nombre, sin efecto real en init), y `runlevels` es una cadena de los niveles de ejecución (no incluida). Si el nivel de ejecución de init está indicado en `runlevels`, la acción se llevará a cabo `action` , ejecutando `process` en su caso. Algunas acciones especiales de `action`s podrían hacer que init hiciese caso omiso de `runlevels` y adoptar un método de ejecución especial. Una explicación más detallada a continuación en la siguiente sección.

## Instalación

## Cambiar runlevel (nivel de ejecución)

### A través del gestor de arranque

Para cambiar el nivel de ejecución (runlevel) al iniciar el sistema, simplemente agregue el nivel de ejecución deseado `n` a la línea de configuración del gestor de arranque. Una solución similar a ésto se consigue con [inittab](/index.php/Start_X_at_login#inittab "Start X at login"). Para arrancar con el nivel de ejecución deseado, agregue su número a los [parámetros del Kernel](/index.php/Kernel_parameters "Kernel parameters") (por ejemplo, `3` para el runlevel 3).

El nivel de ejecución se añade al final, por lo que el kernel sabe el nivel de ejecución que debe iniciar. Para utilizar otro programa de inicio (por ejemplo, [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")), añada `init=/bin/systemd` o similar.

**Nota:** Si está usando un parámetro de init distinto de sysvinit, el valor de runlevel puede ser ignorado.

### Después de arrancar

Después de que el sistema ha arrancado, puede invocar `telinit n` para informar a init que cambie el nivel de ejecución a `n`. init lee el nivel de ejecución n de inittab y "diffs", cancela la ejecución del runlevel anterior, y permite llevar a cabo acciones que no están presentes en el nivel de ejecución anterior. Los procesos actuales en los dos niveles de ejecución se deja intacto. El procedimiento de cancelación es en realidad un poco complejo, de nuevo, los detalles técnicos se pueden encontrar en la página de init manpage.

init no revisa inittab. Será necesario recurrir a `telinit` explícitamente e introducir modificaciones en inittab. El comando `telinit q` hace que init re-examine inittab pero no cambia el nivel de ejecución.

## inittab

En esta sección se examinan las entradas comunes de inittab, en el mismo orden en que aparecen en el inittab por defecto utilizado por Arch. Después de ver algunos ejemplos le ayudarán a crear su propia entrada de inittab.

**Advertencia:** Siempre que modifique `/etc/inittab` pruébelo con `telinit q` antes de reiniciar, dado que un error de sintaxis pequeño puede evitar que su sistema arranque.

### Runlevel por defecto

El nivel de ejecución (runlevel) predeterminado es 3\. Coméntelo, y descomente la opción que sigue si prefiere arrancar en el nivel 5 (que se utiliza para X comunmente) por defecto:

```
id:5:initdefault:

```

### Scripts principales de arranque

Se trata de la secuencia de comandos de inicio principal de Arch.

```
rc::sysinit:/etc/rc.sysinit
rs:S1:wait:/etc/rc.single
rm:2345:wait:/etc/rc.multi
rh:06:wait:/etc/rc.shutdown

```

### Arranque en modalidad de usuario único

A veces, su Kernel puede no arrancar del todo, debido a un disco duro dañado o un sistema de archivos corrupto, ausencia de claves de archivos, etc En este caso, su imagen de inicio puede entrar de forma automática en **modo de usuario único**, que sólo se permite el acceso como root y utiliza `/sbin/sulogin` en lugar de `/sbin/login` para controlar el proceso de inicio de sesión. Usted puede entrar en modo de usuario único mediante la adición de la letra `S` a la de línea de comandos del kernel en la configuración de [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), o [syslinux](/index.php/Syslinux "Syslinux"). Si desea ejecutar algo que no sea `sulogin`, especifique ésto:

```
su:S:wait:/sbin/sulogin -p

```

### Gettys e inicio de sesión

Estas son los elementos básicos que se están ejecutando en sus terminales [gettys](/index.php/Getty "Getty"). La mayoría de las configuraciones por defecto tendrá gettys que se ejecutan en varios ttyS1-6, que hará visualizar en la pantalla el símbolo de login. Véase también openvt, chvt, stty, y ioctl.

```
c1:234:respawn:/sbin/agetty 9600 tty1 xterm-color
c5:5:respawn:/sbin/agetty 57600 tty2 xterm-256color

```

### Ctrl+Alt+Supr

Cuando se presiona la secuencia especial de teclas `Ctrl+Alt+Supr`, esta entrada determina la acción a realizar.

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

```

### Programas de X

Si usted está interesado en la depuración de errores, puede lanzar cualquier aplicación que utilice desde `inittab`. Un programa útil a ejecutar es el gestor de inicio de sesión, que se lanzará cuando el nivel de ejecución es 5, multi-user-x-mode. En el siguiente ejemplo se puede ver cómo empezar [SLiM](/index.php/SLiM "SLiM") cuando se le coloca el nivel de ejecución 5.

```
x:5:respawn:/usr/bin/slim >/dev/null 2>&1
#x:5:respawn:/usr/bin/xdm -nodaemon -confi /etc/X11/xdm/archlinux/xdm-config

```

### Scripts Power-Sensing

Init puede comunicarse con el dispositivo UPS y ejecutar procesos basados ​​en el status de UPS. He aquí algunos ejemplos:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

```

### Solicitud de teclado personalizado

La línea siguiente agrega una función personalizada para cuando una secuencia especial de teclas se pulsa. Usted puede modificar esta secuencia de teclas especial como quiera, siguiendo la sintexis de `Ctrl+Alt+Del`.

```
kb::kbrequest:/usr/bin/wall "Keyboard Request -- edit /etc/inittab to customize"

```

#### Lanzar kbrequest

Usted puede activar la secuencia especial de teclas **kbrequest** mediante el envío de la señal WINCH al proceso init (1) como root (a través de sudo). Con este comando:

```
 kill -WINCH 1

```

escribiendo mediante `wall` en todas las ttys:

```
Broadcast message from root@askapachehost (console) (Wed Oct 27 14:02:26 2010):
Keyboard Request -- edit /etc/inittab to customize

```

## Véase también

*   [Automatic login to virtual console (Español)](/index.php/Automatic_login_to_virtual_console_(Espa%C3%B1ol) "Automatic login to virtual console (Español)")
*   [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")
*   [Start X at Login (Español)](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)")
*   [xinitrc (Español)](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")
*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [SLiM](/index.php/SLiM "SLiM")

## Enlaces externos

*   [Wikipedia: Init](http://en.wikipedia.org/wiki/Init)
*   [Linux Knowledge Base and Tutorial. Run Levels.](http://www.linux-tutorial.info/modules.php?name=MContent&pageid=65)
*   [Linux.com. Introduction to runlevels and inittab](http://www.linux.com/articles/114107)
*   [Linux.com. An introduction to services, runlevels, and rc.d scripts.](http://www.linux.com/news/enterprise/systems-management/8116-an-introduction-to-services-runlevels-and-rcd-scripts)
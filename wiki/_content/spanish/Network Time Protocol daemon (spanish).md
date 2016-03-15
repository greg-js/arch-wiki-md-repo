[Network Time Protocol](https://en.wikipedia.org/wiki/es:Network_Time_Protocol de un sistema GNU/Linux con los servidores horarios de Internet. Está diseñado para mitigar los efectos de la variable de latencia de la red y, por lo general, pueden mantener el horario dentro de un margen de decenas de milisegundos respecto a Internet. La precisión en las redes de área local es aún mejor, hasta un milisegundo.

[El Proyecto NTP](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) proporciona una implementación de referencia del protocolo llamado simplemente NTP. Una alternativa a NTP es [Chrony](/index.php/Chrony "Chrony"), un dial-up amigable y diseñado específicamente para los sistemas que no están en línea todo el tiempo, y [OpenNTPD](/index.php/OpenNTPD "OpenNTPD"), que forma parte del proyecto OpenBSD y que actualmente no se mantiene para Linux.

En este artículo se describe, además, cómo configurar y ejecutar el demonio NTP, tanto como cliente, así como servidor.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configurar conexión a servidores NTP](#Configurar_conexi.C3.B3n_a_servidores_NTP)
    *   [2.2 Configurar el propio servidor NTP](#Configurar_el_propio_servidor_NTP)
    *   [2.3 Otros recursos para la configuración de NTP](#Otros_recursos_para_la_configuraci.C3.B3n_de_NTP)
*   [3 Usar sin demonio](#Usar_sin_demonio)
    *   [3.1 Sincronizar cada vez que arranque](#Sincronizar_cada_vez_que_arranque)
    *   [3.2 Netctl](#Netctl)
*   [4 Ejecutar como un demonio](#Ejecutar_como_un_demonio)
    *   [4.1 Comprobar si el demonio está sincronizando correctamente](#Comprobar_si_el_demonio_est.C3.A1_sincronizando_correctamente)
    *   [4.2 NetworkManager](#NetworkManager)
    *   [4.3 Ejecutar en un entorno chroot](#Ejecutar_en_un_entorno_chroot)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [ntp](https://www.archlinux.org/packages/?name=ntp), disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

## Configuración

El demonio principal es *ntpd*, que está configurado en `/etc/ntp.conf`. El paquete *ntp* proporciona un archivo de configuración por defecto que debe hacer funcionar *ntpd* en modo cliente, sin necesidad de configuración personalizada.

### Configurar conexión a servidores NTP

El primer elemento a definir en el archivo `/etc/ntp.conf` serán los servidores a los que el equipo se va a conectar para sincronizar el tiempo (fecha y hora).

Los servidores NTP se clasifican en un sistema jerárquico con muchos niveles llamados *strata* (estrato): los dispositivos que se consideran fuentes independientes de tiempo horario son clasificados como fuentes de *stratum 0*; los servidores conectados directamente a dispositivos de *stratum 0* son clasificados como fuentes de *stratum 1*; los servidores conectados a fuentes de *stratum 1* se clasifican consiguientemente como fuentes de *stratum 2* y así sucesivamente.

Se ha de entender que el stratum de un servidor no puede ser tomado como un indicador de su precisión o fiabilidad. Normalmente, los servidores de stratum 2 se utilizan con fines de sincronización generales: si no sabe aún los servidores a los que se va a conectar, debe mirar los servidores en [pool.ntp.org](http://www.pool.ntp.org/) ([enlace alternativo](http://support.ntp.org/bin/view/Servers/NTPPoolServers)) y seleccionar el grupo de servidores que esté más cercano a su zona.

A modo de ejemplo:

 `/etc/ntp.conf` 
```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

```

La opción `iburst` está recomendada, ya que envía una serie (*«burst»*) de paquetes solo si no se puede obtener una conexión con el primer intento. Por otro lado, la opción `burst` siempre está presente, incluso en el primer intento, pero nunca debe utilizarse sin permiso explícito, dado que puede incluirse en blacklist.

### Configurar el propio servidor NTP

Si va a configurar un servidor NTP, es necesario agregar [*local clock*](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) como un servidor, por lo que , si el ordenador pierde el acceso a internet, continuará el mismo como un servidor dando el horario a la red; añada *local clock* como un servidor de stratum 10 (use la orden *fudge*) de modo que nunca se hará uso de esa función a menos que el acceso a internet se pierda:

```
server 127.127.1.0
fudge  127.127.1.0 stratum 10

```

A continuación, defina las reglas que permiten a los clientes conectarse a su servicio (*localhost* es considerado igualmente un cliente) usando la orden *restrict*; le debe quedar en el archivo una línea como la siguiente:

```
restrict default nomodify nopeer noquery

```

Estas opciones impiden que nadie pueda modificar algo y evitan igualmente que alguien pueda consultar el estado de su time server: `nomodify` impide la reconfiguración de ntpd (con *ntpq* o *ntpdc*), y `noquery` impide conocer el estado dumping de los datos de ntpd (también con *ntpq* o *ntpdc*).

También puede agregar estas otras opciones:

```
restrict default kod nomodify notrap nopeer noquery

```

**Nota:** Aún con las opciones anteriores, estas todavía permiten a otras personas consultar el time server. Para evitarlo, es necesario añadir `noserve` a fin de detener la función de servir el tiempo horario. También impide la sincronización horaria, ya que bloquea todos los paquetes, excepto las consultas de ntpd y ntpdc.

La documentación completa para la opción "restrict" se encuentra en `man ntp_acc`. Consulte [https://support.ntp.org/bin/view/Support/AccessRestrictions](https://support.ntp.org/bin/view/Support/AccessRestrictions) para obtener instrucciones detalladas.

Siguiendo con la configuración, debe decirle a *ntpd* qué debe permitir a través del propio servidor; la siguiente línea es suficiente si no va a configurar un servidor NTP:

```
restrict 127.0.0.1

```

Si desea forzar la resolución de DNS para el namespace de IPv6, escriba `-6` antes de la dirección IP o nombre de host (`-4` obliga a IPv4 en su lugar), por ejemplo:

```
restrict -6 default kod nomodify notrap nopeer noquery
restrict -6 ::1    # ::1 is the IPv6 equivalent for 127.0.0.1

```

Por último, especifique la ubicación del archivo drift (que realiza un seguimiento de la desviación del horario del sistema) y, opcionalmente, la ubicación del archivo de registro:

```
driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

Un archivo de configuración muy básica se vería así:

 `/etc/ntp.conf` 
```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

restrict 127.0.0.1
restrict -6 ::1  

driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

**Nota:** La definición del archivo de registro no es obligatoria, pero es siempre una buena idea tener retroalimentación de las operaciones de *ntpd*.

### Otros recursos para la configuración de NTP

En conclusión, no olvide consultar las páginas man: es probable que `man ntp.conf` responda a cualquier duda que todavía pudiera tener (consulta las páginas man relacionadas: `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`).

## Usar sin demonio

Para sincronizar el reloj del sistema en un momento dado, sin iniciar el demonio NTP, ejecute:

```
# ntpd -qg

```

**Nota:** Esto tiene el mismo efecto que el programa `ntpdate`, [que ahora está en desuso](http://support.ntp.org/bin/view/Dev/DeprecatingNtpdate).

Después de actualizar el reloj del sistema, guarde el horario para el reloj del hardware de manera que se conserve al reiniciar:

```
# hwclock -w

```

### Sincronizar cada vez que arranque

**Advertencia:** El uso de este método no se recomienda en los servidores y, en general, en las máquinas que necesitan funcionar de forma continua durante más de 2 o 3 días, ya que el reloj del sistema se actualiza solo una vez durante el arranque.

Escriba una unidad *oneshot* de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"):

 `/etc/systemd/system/ntp-once.service` 
```
[Unit]
Description=Network Time Service (once)
After=network.target nss-lookup.target 

[Service]
Type=oneshot
ExecStart=/usr/bin/ntpd -q -g -u ntp:ntp ; /sbin/hwclock -w

[Install]
WantedBy=multi-user.target
```

y actívela.

**Nota:** Tenga en cuenta que una unidad de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") del tipo *oneshot* se ejecuta solo una vez. Por tanto, la opción `ntpd -q` no se debe utilizar en este caso.

### Netctl

Puede sincronizar el reloj del sistema con una conexión de red mediante el uso de [Netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)"). Para ello, añada la siguiente línea a su perfil netctl.

 `ExecUpPost='/usr/bin/ntpd -q || true'` 
**Nota:** La etiqueta `-q` fuerza a *ntpd* a que ajuste la hora **una vez** y salir, es decir, no se iniciará el demonio. Si esta operación no tiene éxito, no se sincronizará el reloj del sistema. Véase [ejecutar como un demonio](#Ejecutar_como_un_demonio) para obtener una solución alternativa.

## Ejecutar como un demonio

[Inicie](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `ntpd.service`. Para iniciarlo en el arranque o bien actívelo o, alternativamente, utilice la orden:

```
# timedatectl set-ntp 1

```

### Comprobar si el demonio está sincronizando correctamente

Utilice la herramienta ntpq para ver la lista de pares (*«peers»*) configurados:

 `$ ntpq -np` 

Las columnas delay, offset y jitter deben mostrar una fluctuación distinta de cero. Los servidores ntpd que se estén sincronizando aparecerán con un asterisco como prefijo. Pueden pasar varios minutos antes que ntpd seleccione un servidor para sincronizarse, pruebe a comprobar pasados 17 minutos (1024 segundos).

### NetworkManager

**Nota:** ntpd debe seguir funcionando cuando la red no funciona, si el demonio hwclock está desactivado, por lo que no es necesario utilizar este último.

*ntpd* puede ser puesto up/down junto con una conexión de red mediante el uso de los [scripts de NetworkManager dispatcher](/index.php/NetworkManager_(Espa%C3%B1ol)#Servicios_de_red_con_NetworkManager_dispatcher "NetworkManager (Español)"). Puede ser necesario instalar [networkmanager-dispatcher-ntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-ntpd) desde los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

### Ejecutar en un entorno chroot

**Note:** ntpd se debe ejecutar como usuario no root antes que intentar configuralo en un entorno chroot (predefinido en el paquete vanilla de Arch Linux), ya que desde entornos chroots es relativamente inútil para asegurar procesos ejecutados como root.

Edite `/etc/conf.d/ntpd.conf` y cambie

```
NTPD_ARGS="-g -u ntp:ntp"

```

por

```
NTPD_ARGS="-g -i /var/lib/ntp -u ntp:ntp"

```

A continuación, edite `/etc/ntp.conf` para cambiar la ruta de driftfile de modo que sea dirigida al directorio chroot, en lugar de a la raíz del sistema real. Cambie:

```
driftfile       /var/lib/ntp/ntp.drift

```

por

```
driftfile       /ntp.drift

```

Crear un entorno chroot adecuado para que getaddrinfo() funcione mediante la creación de directorios y archivos pertinentes (como root):

```
# mkdir /var/lib/ntp/etc /var/lib/ntp/lib /var/lib/ntp/proc
# touch /var/lib/ntp/etc/resolv.conf /var/lib/ntp/etc/services
```

y seguidamente montar los enlaces a los archivos arriba indicados:

 `/etc/fstab` 
```
...
#ntpd chroot mounts
/etc/resolv.conf  /var/lib/ntp/etc/resolv.conf none bind 0 0
/etc/services	  /var/lib/ntp/etc/services none bind 0 0
/lib		  /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```
 `# mount -a` 

Por último, reinicie el demonio `ntpd` de nuevo.

Es relativamente difícil estar seguro de que su configuración driftfile está realmente trabajando sin tener que esperar un tiempo, dado que ntpd no lee ni escribe muy a menudo. Si se equivoca, se registrará un error, y si se hace bien, se actualizará la fecha y hora (*«timestamp»*). Si no aparece ningún error al respecto después de un día completo de funcionamiento, y timestamp se actualiza, puede estar seguro de haberlo hecho correctamente.

## Véase también

*   [Time (Español)](/index.php/Time_(Espa%C3%B1ol) "Time (Español)") (para más información sobre la gestión del horario del ordenador)
*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)
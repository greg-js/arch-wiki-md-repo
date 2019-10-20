**Estado de la traducción**
Este artículo es una traducción de [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd"), revisada por última vez el **2019-10-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd-timesyncd&diff=0&oldid=586260) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)")
*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")

De la [lista de correo de systemd](http://lists.freedesktop.org/archives/systemd-devel/2014-May/019537.html):

	*systemd-timesyncd* es un demonio que se ha añadido para sincronizar el reloj del sistema a través de la red. Implementa un cliente SNTP. A diferencia de las implementaciones de NTP como [chrony](/index.php/Chrony "Chrony") o el servidor de referencia NTP, este solo implementa un lado del cliente y no molesta con la complejidad completa de NTP, centrándose solo en consultar el tiempo de un servidor remoto y sincronizar el reloj local con él. A menos que tenga la intención de servir NTP a clientes en red o desee conectarse a relojes de hardware locales, este simple cliente NTP debería ser más que apropiado para la mayoría de las instalaciones. El demonio se ejecuta con privilegios mínimos y se conecta a networkd para operar solo cuando la conectividad de red esté disponible. El demonio guarda el reloj actual en el disco cada vez que se adquiere una nueva sincronización NTP, y utiliza esto para corregir, si es posible, el reloj del sistema antes del arranque, a fin de acomodar los sistemas que carecen de un RTC como el Raspberry Pi y los dispositivos integrados, y asegurarse de que el tiempo progrese de forma monotónica en estos sistemas, incluso si no siempre es correcto. Para hacer uso de este demonio, es necesario crear un nuevo usuario y grupo del sistema «systemd-timesync» en la instalación de systemd.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuración](#Configuración)
*   [2 Utilización](#Utilización)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 systemd-timesyncd no puede iniciarse después de la actualización 242.0-1 update](#systemd-timesyncd_no_puede_iniciarse_después_de_la_actualización_242.0-1_update)
*   [4 Véase también](#Véase_también)

## Configuración

[Inicie/active](/index.php/Start/enable "Start/enable") `systemd-timesyncd.service` que está disponible con [systemd](https://www.archlinux.org/packages/?name=systemd).

Al comenzar, *systemd-timesyncd* leerá el archivo de configuración de `/etc/systemd/timesyncd.conf`, que se ve así:

 `/etc/systemd/timesyncd.conf` 
```
[Time]
#NTP=
#FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
#RootDistanceMaxSec=5
#PollIntervalMinSec=32
#PollIntervalMaxSec=2048
```

Para añadir [servidores de horas](/index.php/Network_Time_Protocol_daemon#Connection_to_NTP_servers "Network Time Protocol daemon") o cambiar los proporcionados, elimine el comentario de la línea correspondiente y enumere sus nombres de equipo o IP separados por un espacio. Por ejemplo, puede usar cualquier servidor proporcionado por [the NTP pool project](http://www.pool.ntp.org/) o utilizar [uno de los predefinidos de Arch](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ntp&id=1b485f87c9e1384eaf069d031e415515e8ead92d) (también proporcionado por el proyecto de agrupación NTP):

 `/etc/systemd/timesyncd.conf` 
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```

Para verificar su configuración, utilice `timedatectl show-timesync --all`:

 `$ timedatectl show-timesync --all` 
```
LinkNTPServers=
SystemNTPServers=
FallbackNTPServers=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
ServerName=0.arch.pool.ntp.org
ServerAddress=103.47.76.177
RootDistanceMaxUSec=5s
PollIntervalMinUSec=32s
PollIntervalMaxUSec=34min 8s
PollIntervalUSec=1min 4s
NTPMessage={ Leap=0, Version=4, Mode=4, Stratum=2, Precision=-21, RootDelay=177.398ms, RootDispersion=142.196ms, Reference=C342F10A, OriginateTimestamp=Mon 2018-07-16 13:53:43 +08, ReceiveTimestamp=Mon 2018-07-16 13:53:43 +08, TransmitTimestamp=Mon 2018-07-16 13:53:43 +08, DestinationTimestamp=Mon 2018-07-16 13:53:43 +08, Ignored=no PacketCount=1, Jitter=0 }
Frequency=22520548
```

Además de la configuración del demonio, los servidores NTP también se pueden proporcionar a través de una configuración [systemd-networkd](/index.php/Systemd-networkd#[NetDev]_section "Systemd-networkd") con la opción `NTP=` o, dinámicamente, a través de un servidor DHCP.

El servidor que NTP utilizará se determinará utilizando las siguientes reglas:

*   Cualquier servidor NTP por interfaz obtenido de la configuración de `systemd-networkd.service(8)` o mediante DHCP, tendrán prioridad.
*   Los servidores NTP definidos en `/etc/systemd/timesyncd.conf` se añadirán a la lista por interfaz en tiempo de ejecución y el demonio se pondrá en contacto con dichos servidores sucesivamente hasta que se encuentre uno que responda.
*   Si no se obtiene información del servidor NTP después de completar los pasos anteriores, se utilizarán los nombres de equipos de servidor NTP o las direcciones IP definidas en `FallbackNTP=`.

**Nota:** el servicio escribe en un archivo local `/var/lib/systemd/timesync/clock` con cada sincronización. Esta ubicación está codificada y no se puede cambiar. Esto puede ser problemático para ejecutarlo en una partición raíz de solo lectura o tratar de minimizar las escrituras en una tarjeta SD.

## Utilización

Para activarlo e iniciarlo, simplemente ejecute:

```
# timedatectl set-ntp true 

```

El proceso de sincronización puede ser notablemente lento. Esto se debe presumir, por lo que debe esperar un poco antes de considerar que hay un problema. Para verificar el estado del servicio, utilice `timedatectl status`:

 `$ timedatectl status` 
```
               Local time: Thu 2015-07-09 18:21:33 CEST
           Universal time: Thu 2015-07-09 16:21:33 UTC
                 RTC time: Thu 2015-07-09 16:21:33
                Time zone: Europe/Amsterdam (CEST, +0200)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no

```

Para ver información detallada del servicio, utilice `timedatectl timesync-status`:

 `$ timedatectl timesync-status` 
```
       Server: 103.47.76.177 (0.arch.pool.ntp.org)
Poll interval: 2min 8s (min: 32s; max 34min 8s)
         Leap: normal
      Version: 4
      Stratum: 2
    Reference: C342F10A
    Precision: 1us (-21)
Root distance: 231.856ms (max: 5s)
       Offset: -19.428ms
        Delay: 36.717ms
       Jitter: 7.343ms
 Packet count: 2
    Frequency: +267.747ppm

```

## Solución de problemas

### systemd-timesyncd no puede iniciarse después de la actualización 242.0-1 update

Si el registro muestra este error:

```
ExecStart=/usr/lib/systemd/systemd-timesyncd (code=exited, status=238/STATE_DIRECTORY)

```

Ejecute las siguientes órdenes para solucionar el problema:

```
# rm -rf /var/lib/systemd/timesync
# rm -rf /var/lib/private/systemd/timesync

```

## Véase también

*   [Forum: systemd-timesyncd is not syncing time](https://bbs.archlinux.org/viewtopic.php?id=182600)
*   [Forum: Using systemd-timesync instead of NTP](https://bbs.archlinux.org/viewtopic.php?id=182172)
*   [Git Sourcecode of timesyncd](https://github.com/systemd/systemd/blob/master/src/timesync/timesyncd.c)
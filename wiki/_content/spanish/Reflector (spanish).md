**Estado de la traducción**
Este artículo es una traducción de [Reflector](/index.php/Reflector "Reflector"), revisada por última vez el **2019-10-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Reflector&diff=0&oldid=586484) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)")
*   [Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")

[Reflector](http://xyne.archlinux.ca/projects/reflector/) es un script que puede recuperar la última lista de servidores de réplicas desde la página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrar la mayoría de los servidores de réplicas actualizados, ordénarlos por velocidad y sobrescribir el archivo `/etc/pacman.d/mirrorlist`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Ejemplos](#Ejemplos)
*   [3 Automatización](#Automatización)
    *   [3.1 Hook de pacman](#Hook_de_pacman)
    *   [3.2 Servicio systemd](#Servicio_systemd)
    *   [3.3 Temporizador de systemd](#Temporizador_de_systemd)
    *   [3.4 Paquete reflector-timer](#Paquete_reflector-timer)
    *   [3.5 Tarea de cron](#Tarea_de_cron)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [reflector](https://www.archlinux.org/packages/?name=reflector).

## Utilización

**Advertencia:**

*   En los siguientes ejemplos, se sobrescribirá el archivo `/etc/pacman.d/mirrorlist`. Haga una copia de seguridad antes de continuar.
*   Asegúrese de que el archivo `/etc/pacman.d/mirrorlist` resultante no contenga entradas que considere poco fiables antes de sincronizar o actualizar con [Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

Para ver todos las órdenes disponibles, ejecute la siguiente orden:

```
# reflector --help

```

### Ejemplos

Para clasificar y ordenar detalladamente los cinco servidores de réplicas sincronizados más recientes por velocidad de descarga y sobrescribir el archivo `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Para seleccionar los 200 servidores de réplicas HTTP o HTTPS más recientemente sincronizados, ordenarlos por velocidad de descarga y sobrescribir el archivo `/etc/pacman.d/mirrorlist`:

```
# reflector --latest 200 --protocol http --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

Para seleccionar los 200 servidores de réplicas HTTPS sincronizados en las últimas 12 horas y ubicados en Francia o Alemania, ordenarlos por velocidad de descarga y sobrescribir el archivo `/etc/pacman.d/mirrorlist`:

```
# reflector --country France --country Germany --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

## Automatización

### Hook de pacman

Puede crear un [hook de pacman](/index.php/Pacman_hook "Pacman hook") que ejecute *reflector* y elimine el archivo *.pacnew* creado cada vez que [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) obtenga una actualización:

 `/etc/pacman.d/hooks/mirrorupgrade.hook` 
```
[Trigger]
Operation = Upgrade
Type = Package
Target = pacman-mirrorlist

[Action]
Description = Actualizar pacman-mirrorlist con reflector y eliminar pacnew...
When = PostTransaction
Depends = reflector
Exec = /bin/sh -c "reflector --country 'United States' --latest 200 --age 24 --sort rate --save /etc/pacman.d/mirrorlist; rm -f /etc/pacman.d/mirrorlist.pacnew"

```

Asegúrese de sustituir los argumentos de *reflector* con los que desee.

### Servicio systemd

Este es un ejemplo de unidad de servicio (de systemd) que espera a que la red esté activa y conectada antes de ejecutar reflector:

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Actualizar la lista de servidores de réplica de pacman
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target
```

[Inicie](/index.php/Start "Start") `reflector.service` para actualizar la lista de servidores de réplica. Para actualizar la lista de servidores de réplica cada vez que arranque el equipo, [active](/index.php/Enable "Enable") el servicio.

**Nota:** para obtener más información sobre la implementación de la dependencia de la conexión de red, consulte [Systemd#Running services after the network is up](/index.php/Systemd#Running_services_after_the_network_is_up "Systemd").

### Temporizador de systemd

Si desea ejecutar `reflector.service` semanalmente, cree un archivo *.timer* asociado. Por ejemplo::

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Ejecutar reflector semanalmente

[Timer]
OnCalendar=Mon *-*-* 7:00:00
RandomizedDelaySec=15h
Persistent=true

[Install]
WantedBy=timers.target
```

Y luego solo tiene que [iniciar](/index.php/Start "Start") `reflector.timer`.

### Paquete reflector-timer

[Instale](/index.php/Install "Install") [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) to run *reflector* weekly.

La configuración predeterminada, que se puede editar para adaptarse a sus necesidades, es:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate
### eliminar una entrada si no la quiere como protocolo disponible
PROTOCOL1='-p http'
PROTOCOL2='-p https'
PROTOCOL3='-p ftp'
```

Asegúrese de [activar](/index.php/Enable "Enable") `reflector.timer`.

### Tarea de cron

Para actualizar la lista servidores de réplica diariamente, considere lo siguiente:

 `/etc/cron.daily/mirrorlist` 
```
#!/bin/bash

# Obtener los del país
/usr/bin/reflector -c "India" -p http --sort rate > /etc/pacman.d/mirrorlist

# Trabajar con otras alternativas
/usr/bin/reflector -p http  --latest 20 -p https -p ftp --sort rate >> /etc/pacman.d/mirrorlist
```
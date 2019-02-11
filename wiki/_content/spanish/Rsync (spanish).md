Artículos relacionados

*   [Full system backup with rsync (Español)](/index.php/Full_system_backup_with_rsync_(Espa%C3%B1ol) "Full system backup with rsync (Español)")
*   [Backup programs](/index.php/Backup_programs "Backup programs")

[rsync](https://rsync.samba.org/) es una herramienta de código abierto que permite transferir archivos rápidamente y de forma incremental.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Uso](#Uso)
    *   [2.1 Como alternativa a cp](#Como_alternativa_a_cp)
    *   [2.2 Como herramienta para copias de seguridad](#Como_herramienta_para_copias_de_seguridad)
        *   [2.2.1 Automated backup](#Automated_backup)
        *   [2.2.2 Respaldo automático con SSH](#Respaldo_automático_con_SSH)
        *   [2.2.3 Respaldo automático con NetworkManager](#Respaldo_automático_con_NetworkManager)
        *   [2.2.4 Copia automatizada con systemd y inotify](#Copia_automatizada_con_systemd_y_inotify)
        *   [2.2.5 Copia de seguridad diferencial en una semana](#Copia_de_seguridad_diferencial_en_una_semana)
        *   [2.2.6 Instantánea de copia de seguridad](#Instantánea_de_copia_de_seguridad)
*   [3 Interfaces gráficas](#Interfaces_gráficas)

## Instalación

Puedes [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [rsync](https://www.archlinux.org/packages/?name=rsync) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") ejecutando el comando:

```
`# pacman -S rsync`

```

## Uso

Para ver más ejemplos, pueden buscar en los foros [Community Contributions](https://bbs.archlinux.org/viewforum.php?id=27) y [General Programming](https://bbs.archlinux.org/viewforum.php?id=33).

### Como alternativa a cp

rsync puede usarse como sustituto avanzado del comando `cp`. especialmente en la copia de ficheros grandes:

```
$ rsync -P origen destino

```

La opción `-P` es igual que `--partial --progress`, que mantiene los archivos parcialmente transferidos y muestra una barra de progreso durante la transferencia.

Quizás quiera usar la opción `-r --recursive` para recorrer recursivamente los directorios, o la opción `-R` para usar nombres de rutas relativos (recreando la jerarquía completa de carpetas en la carpeta de destino).

### Como herramienta para copias de seguridad

El protocolo rsync puede usarse para hacer copias de seguridad, transfiriendo solo aquellos ficheros que hayan cambiado desde la última copia. Esta sección describe un sencillo script programdo para hacer copias de seguridad usando rsync, generalmente usado para hacer copias a dispositivos extraibles. Para ver un ejemplo más detallado y con **opciones adicionales para preservar determinados archivos del sistema**, véase [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

#### Automated backup

A modo de ejemplo, el script es creado en el directorio `/etc/cron.daily` , y se ejecutará a diario si un [demonio](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") cron se instala y configura adecuadamente. Configurar y usar [cron](/index.php/Cron "Cron") no entra en el ámbito de este artículo.

Primero, cree un script que contenga las opciones de comandos apropiadas:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete /carpeta/a/respaldar  /carpeta/de/copia/de/seguridad &> /dev/null
```

	`-a` 

	indica que los ficheros deberían ser archivados, lo cual significa que se preservarán casi todos las características (**no** así las ACLS, los enlaces duros o atributos extendidos como capacidades)

	`--delete` 

	indica que los ficheros borrados en origen también serán borrados en destino.

Aquí, `/carpeta/a/resguardar` debería cambiarse a aquella que se quiera respaldar (`/home`, por ejemplo) y `/carpeta/de/copia/de/seguridad` es donde la copia de seguridad debería salvarse (`/media/disk`, por ejemplo).

Finalmente, el script debe tener permisos de ejecución:

```
# chmod +x /etc/cron.daily/rsync.backup

```

#### Respaldo automático con SSH

Si se respalda a una máquina remota usando [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)"), use este script en su lugar:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete -e ssh /carpeta/a/respaldar  usuarioremoto@maquinaremota:/carpeta/de/copia/de/seguridad &> /dev/null
```

	`-e ssh` 

	indica a rsync que use SSH

	`remoteuser` 

	es el usuario en la `maquinaremota`

	`-a` 

	agrupa todas estas opciones `-rlptgoD` (recursivo, enlaces, permisos, tiempos, grupos, propietario, dispositivos)

#### Respaldo automático con NetworkManager

Este script inicia una copia de respaldo cuando conecta el cable de red.

Primero, cree un script que contenga las opciones de comandos apropiadas:

 `/etc/NetworkManager/dispatcher.d/backup` 
```
#!/bin/bash

if [ x"$2" = "xup" ] ; then
        rsync --force --ignore-errors -a --delete --bwlimit=2000 --files-from=files.rsync /carpeta/a/respaldar  /carpeta/de/copia/de/seguridad
fi
```

	`-a` 

	agrupa todas estas opciones `-rlptgoD` (recursivo, enlaces, permisos, tiempos, grupos, propietario, dispositivos)

	`--files-from` 

	lee la ruta relativa de */carpeta/a/respaldar* desde este archivo

	`--bwlimit` 

	limita el ancho de banda de E/S; KBytes por segundo

#### Copia automatizada con systemd y inotify

**Nota:**

*   Debido a las limitaciones de inotify y systemd (véase [esta pregunta y su respuesta](http://www.quora.com/Linux-Kernel/Inotify-monitoring-of-directories-is-not-recursive-Is-there-any-specific-reason-for-this-design-in-Linux-kernel)), la monitorización de archivos recursiva no es posible. Aunque puede vigilar un directorio y su contenido, no vigilará recursivamente los subdirectorios ni sus respectivos contenidos; debe especificar explícitamente cada directorio a monitorizar, aunque ese directorio sea hijo de otro que ya esté siendo vigilado.
*   Esta configuración esta basada en una instancia de [systemd/User](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)").

En vez de basar los respaldos en copias intervalos programados de tiempo, como los implementados en [cron](/index.php/Cron "Cron"), es posible ejecutar una copia de seguridad cada vez que un fichero cambie. Las unidades `systemd.path` usan `inotify` para monitorizar el sistema de archivos, y pueden ser usadas en conjunto con los archivos `systemd.service` para iniciar cualquier proceso (en este caso el respaldo de [rsync](/index.php/Rsync "Rsync") ) basado en un evento del sistema de archivos.

Primero, cree el fichero `systemd.path` que monitorizará los fichero que quiere respaldar:

 `~/.config/systemd/user/backup.path` 
```
[Unit]
Description=Comprueba si rutas que están siendo respaldadas han cambiado

[Path]
PathChanged=%h/documentos
PathChanged=%h/musica

[Install]
WantedBy=default.target
```

Entonces hay que crear un fichero `systemd.service` que será activado cuando detecte un cambio. Por defecto un fichero de servicio del mismo nombre que la unidad de ruta (en este caso `backup.path`) será activado, excepto con la extension `.service` en vez de la extensión `.path` (en este caso `backup.service`).

**Nota:** Si necesita ejecutar multiples comando rsync , use `Type=oneshot`. Esto le permite especificar multiples parametros `ExecStart=`, uno por cada comando [rsync](/index.php/Rsync "Rsync"), que será ejecutado. En su lugar, también puede simplemente escribit un script que haga todos sus copias de seguridad, como los scripts de [cron](/index.php/Cron "Cron").
 `~/.config/systemd/user/backup.service` 
```
[Unit]
Description=Respalda ficheros

[Service]
ExecStart=/usr/bin/rsync %h/./documentos %h/./musica -CERrltm --delete ubuntu:
```

Tan solo resta iniciar/habilitar `backup.path` como si de un servicio systemd normal se tratase y este comenzará a monitorizar cambios en los ficheros e iniciará en consecuencia `backup.service`:

```
systemctl --user start backup.path
systemctl --user enable backup.path
```

#### Copia de seguridad diferencial en una semana

Esta es una opción muy útil de rsync, crear una copia completa y una copia diferencial por cada día de la semana.

Primero, cree un script que contenga las opciones de comandos apropiadas::

 `/etc/cron.daily/backup` 
```
#!/bin/bash

DAY=$(date +%A)

if [ -e  /carpeta/de/copia/de/seguridad/incr/$DAY ] ; then
  rm -fr  /carpeta/de/copia/de/seguridad/incr/$DAY
fi

rsync -a --delete --inplace --backup --backup-dir= /carpeta/de/copia/de/seguridad/incr/$DAY /carpeta/a/respaldar  /carpeta/de/copia/de/seguridad/completa/ &> /dev/null
```

	`--inplace` 

	implica actualización de los ficheros de destino `--partial` in-place

#### Instantánea de copia de seguridad

La misma idea se puede aplicar a mantener un árbol de instantáneas de sus ficheros. En otras palabras, un directorio de copias ordenadas de sus ficheros. Las copias se hacen empleando enlaces duros, lo cual implica que solo aquellos ficheros que hayan cambiado ocuparán espacio. En terminos generales, esta es la idea tras el funcionamiento de la máquina del tiempo de Apple.

Este script implementa una versión más simple de ello:

 `/usr/local/bin/rsnapshot.sh` 
```
#!/bin/bash

## Mi propio procedimient de copia de seguridad de instantáneas basado  en rsync
## (cc) marcio rps AT gmail.com

# config vars

SRC="/home/username/files/" #¡No olviden la barra final!
SNAP="/snapshots/nombredeusuario"
OPTS="-rltgoi --delay-updates --delete --chmod=a-w"
MINCHANGES=20

# Ejectuar este proceso con prioridad real baja

ionice -c 3 -p $$
renice +12  -p $$

# sincronizar

rsync $OPTS $SRC $SNAP/latest >> $SNAP/rsync.log

# Comprobar si han habido cambios suficientes y en caso afirmativo
# hacer una copia de enlace duro nombrada con la fecha

COUNT=$( wc -l $SNAP/rsync.log|cut -d" " -f1 )
if [ $COUNT -gt $MINCHANGES ] ; then
        DATETAG=$(date +%Y-%m-%d)
        if [ ! -e $SNAP/$DATETAG ] ; then
                cp -al $SNAP/latest $SNAP/$DATETAG
                chmod u+w $SNAP/$DATETAG
                mv $SNAP/rsync.log $SNAP/$DATETAG
               chmod u-w $SNAP/$DATETAG
         fi
fi

```

Para simplificar mucho las cosas puede ejecutar este script desde una unidad de systemd.

## Interfaces gráficas

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [grsync](https://www.archlinux.org/packages/?name=grsync) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").
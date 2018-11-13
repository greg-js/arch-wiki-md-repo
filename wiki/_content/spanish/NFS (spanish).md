Artículos relacionados

*   [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting")

Según la [Wikipedia](https://en.wikipedia.org/wiki/es:Network_File_System "wikipedia:es:Network File System"):

	*El Network File System (Sistema de archivos de red), o NFS, es un protocolo de nivel de aplicación, desarrollado originariamente por Sun Microsystems en 1984, que permite a un usuario de un equipo cliente acceder a archivos remotos a través de una red, de una manera similar a como se accede a los archivos almacenados localmente.*

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Servidor](#Servidor)
    *   [2.2 Iniciar/Habilitar servicios](#Iniciar/Habilitar_servicios)
        *   [2.2.1 Mapeo de ID](#Mapeo_de_ID)
        *   [2.2.2 Sistema de archivos](#Sistema_de_archivos)
        *   [2.2.3 Exportación](#Exportación)
        *   [2.2.4 Arrancando el servidor](#Arrancando_el_servidor)
        *   [2.2.5 Configuración del cortafuegos](#Configuración_del_cortafuegos)
    *   [2.3 Cliente](#Cliente)
        *   [2.3.1 Montaje en Linux](#Montaje_en_Linux)
            *   [2.3.1.1 Ajustes en /etc/fstab](#Ajustes_en_/etc/fstab)
            *   [2.3.1.2 Uso de autofs](#Uso_de_autofs)
        *   [2.3.2 Montaje en Windows](#Montaje_en_Windows)
        *   [2.3.3 Montaje en OS X](#Montaje_en_OS_X)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Ajustar el rendimiento](#Ajustar_el_rendimiento)
    *   [3.2 Manejar el montaje automático](#Manejar_el_montaje_automático)
        *   [3.2.1 NetworkManager dispatcher](#NetworkManager_dispatcher)
    *   [3.3 Configurar puertos fijos para NFS](#Configurar_puertos_fijos_para_NFS)
*   [4 Solución de problemas](#Solución_de_problemas)
*   [5 Véase también](#Véase_también)

## Instalación

Tanto el cliente como el servidor necesitan únicamente de la [instalación](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") del paquete [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Nota:** Es SUMAMENTE recomendable el uso de un demonio de sincronización horaria en TODOS los nodos de su red para mantener sincronizados los relojes de cliente y servidor. ¡Si no hay un ajuste preciso en los relojes de todos los nodos, el NFS puede presentar retrasos indeseados! El sistema [NTP](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") es recomendable para sincronizar tanto el servidor como los clientes con los servidores NTP extremadamente precisos disponibles en Internet.

## Configuración

### Servidor

### Iniciar/Habilitar servicios

Para hacer uso del servidor sera necesario iniciar el servicio de nfs-server y habilitarlo si se desea dejar permanente.

Iniciar

```
# systemctl start nfs-server.service

```

Habilitar

```
# systemctl enable nfs-server.service

```

#### Mapeo de ID

Edite `/etc/idmapd.conf` y establezca el campo `Domain` con su nombre de dominio.

 `/etc/idmapd.conf` 
```
[General]

Verbosity = 1
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
Domain = atomic

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

```

#### Sistema de archivos

**Nota:** Por razones de seguridad, es recomendable que use una raíz de exportación NFS con lo que mantendrá a los usuarios únicamente dentro de ese punto de montaje. El siguiente ejemplo ilustrará esta idea.

Defina los archivos de NFS compartidos en `/etc/exports` con una ruta relativa a la raíz de NFS. En este ejemplo, la raíz NFS será `/srv/nfs4` y el recurso compartido será `/mnt/music`.

 `# mkdir -p /srv/nfs4/music` 

Deberá otorgar permisos de lectura/escritura al directorio music para que los clientes puedan escribir en él.

Ahora monte el directorio que desea compartir, en este caso `/mnt/music`, en el directorio compartido de NFS a través de la instrucción de montaje:

 `# mount --bind /mnt/music /srv/nfs4/music` 

Para hacer que los cambios sean permanentes en cada reinicio del servidor, añada el enlace de montaje a `fstab`:

 `/etc/fstab` 
```
/mnt/music /srv/nfs4/music  none   bind   0   0

```

#### Exportación

Añada los directorios que se compartirán y la dirección IP o nombre de servidor de las máquinas cliente a las que les estará permitido montarlas en `exports`:

 `/etc/exports` 
```
/srv/nfs4/ 192.168.0.1/24(rw,fsid=root,no_subtree_check)
/srv/nfs4/music 192.168.0.1/24(rw,no_subtree_check,nohide) # note the nohide option which is applied to mounted directories on the file system.

```

Los usuarios no necesitan abrir el material compartido a la subred completa; se puede especificar solo una dirección IP o un nombre de servidor.

Para más información sobre todas las opciones disponibles vea [exports(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/exports.5).

Si usted modifica `/etc/exports` mientras el servidor está funcionando, debe volver a exportarlos para que los cambios surtan efecto:

 `# exportfs -rav` 

#### Arrancando el servidor

[Encienda/habilite](/index.php/Daemons "Daemons") los servicios `rpcbind.service` y `nfs-client.target`:

```
# systemctl start rpcbind nfs-client.target

```

Observe que esas unidades requieren de otros servicios, que serán lanzados automáticamente por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

#### Configuración del cortafuegos

Para activar el acceso a través de un cortafuegos, necesita abrir los puertos 111, 2049, y 20048 para tcp y udp. Para configurar dichos puertos para [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)"), edite `/etc/iptables/iptables.rules` para incluir las líneas siguientes:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
-A INPUT -p udp -m udp --dport 111 -j ACCEPT
-A INPUT -p udp -m udp --dport 2049 -j ACCEPT
-A INPUT -p udp -m udp --dport 20048 -j ACCEPT

```

Para aplicar los cambios, reinicie el servicio `iptables`.

### Cliente

Los clientes necesitan de [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) para conectarse, y para evitar una demora aproximadamente de 15 segundos a la que acompaña un error que dice: «RPC: AUTH_GSS upcall timed out», obligando a los usuarios a iniciar el servicio `rpc-gssd` en cualquier equipo cliente.

**Nota:** Los servidores NFS4 no necesitan ejecutar este servicio.

#### Montaje en Linux

Muestre los sistemas de archivos exportados por el servidor:

 `$ showmount -e servername` 

A continuación móntelos omitiendo la raíz de exportación del servidor NFS:

 `# mount -t nfs4 servername:/music /mountpoint/on/client` 

##### Ajustes en /etc/fstab

El uso de [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") es útil para un servidor que siempre esté operativo, y los recursos compartidos a través de NFS estén disponible en cualquier lugar que arranque el cliente. Edite el archivo `/etc/fstab`, y añada la línea de configuración apropiada. De nuevo, deberá omitir la ruta de la raíz de exportación del servidor NFS.

 `/etc/fstab` 
```
servername:/music   /mountpoint/on/client   nfs4   rsize=8192,wsize=8192,timeo=14,intr,_netdev	0 0

```

**Nota:** Consulte la página principal de NFS para obtener más información.

Algunas opciones de montaje adicionales que puede tener en cuenta para incluir son:

	rsize y wsize

	El valor `rsize` es el número de bytes usados cuando se lee desde el servidor. El valor `wsize` es el número de bytes usados cuando se escribe en el servidor. El valor predeterminado para ambos es 1024, pero si se usan valores mayores como 8192 puede mejorar el rendimiento. Esto no es así de manera general. Es recomendable hacer pruebas antes de hacer definitivos estos cambios, véase [#Ajustar el rendimiento](#Ajustar_el_rendimiento).

	timeo

	El valor `timeo` es la cantidad de tiempo, en décimas de segundo, que se debe esperar antes de volver a enviar una transmisión después de un tiempo de espera RPC. Después del primer tiempo de espera, este valor se doblará en cada reintento hasta alcanzar un máximo de 60 segundos o hasta que se produzca un tiempo de espera mayor. Si la conexión se realiza con un servidor lento o en una red muy concurrida, puede conseguir un mayor rendimiento si aumenta este tiempo de espera.

	intr

	La opción `intr` permite enviar señales para interrumpir las operación de los archivos si ocurre un tiempo de espera mayor en la partición compartida.

	_netdev

	La opción `_netdev` le dice al sistema que espere hasta que la red esté operativa después de intentar montar el recurso compartido. systemd lo hace de manera predeterminada para NFS, pero de todas formas es una buena práctica usarlo para todos los tipos de sistemas de archivos en red.

##### Uso de autofs

El uso de [autofs](/index.php/Autofs "Autofs") es útil cuando varías máquinas se quieren conectar a través de NFS; ya sean clientes o servidores. La razón por la cual este método es perferible a los más actuales es que si el servidor se apaga, el cliente no mostrará mensajes de error al ser incapaz de encontrar los archivos compartidos. Revise [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs") para obtener mayor información.

#### Montaje en Windows

**Nota:** Solo las ediciones Ultimate y Enterprise de Windows 7 y la edición Enterprise de Windows 8 incluyen «Cliente de NFS».

Los archivos compartidos a través de NFS pueden ser montados desde Windows si el servicio «Cliente de NFS» está activo (no lo está de manera predeterminada). Para instalar el servicio vaya a «Programas y características» en el Panel de Control y pulse en «Encender o apagar las características de Windows». Busque los «Servicios de NFS» y actívelos conjuntamente con los subservicios («Herramientas administrativas» y «Cliente de NFS»).

Puede seleccionar algunas opciones generales abriendo los «Servicios para Network File System» (localícelo con la caja de búsquedas) y pulse con el botón secundario del ratón en cliente → propiedades.

**Advertencia:** Pueden producirse problemas graves de rendimiento (de forma aleatoria tarda 30-60 segundos en mostrar la carpeta, velocidades de copia de 2 MB/s en una red LAN Gigabit, ...) para lo cual, Microsoft no tiene aún una solución.[[1]](https://social.technet.microsoft.com/Forums/en-CA/w7itpronetworking/thread/40cc01e3-65e4-4bb6-855e-cef1364a60ac)

Para montar un recurso compartido mediante Explorer:

`Mi PC` > `Conectar una unidad de red` > `nombre de servidor:/srv/nfs4/music`

#### Montaje en OS X

**Nota:** OS X usa de forma predeterminada un puerto inseguro (>1024) para montar los recursos compartidos.

O bien exporte del recurso compartido con la marca `insecure`, y monte usando Finder:

`Go` > `Connect to Server` > `nfs://servername/`

O, monte el recurso compartido usando un puerto seguro usando la terminal:

 `# sudo mount -t nfs -o resvport servername:/srv/nfs4 /Volumes/servername` 

## Consejos y trucos

### Ajustar el rendimiento

Con el fin de obtener el máximo rendimiento de NFS, es necesario ajustar las opciones de montaje de `rsize` y `wsize` para satisfacer los requisitos de la configuración de la red.

### Manejar el montaje automático

Este consejo es muy útil para los portátiles que requieren compartir NFS desde una red inalámbrica local. Si el equipo NFS se vuelve inaccesible, el recurso compartido NFS se desmontará para evitar que el sistema se bloquea cuando usemos la opción `hard mount`. Véase [https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240](https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240)

Asegúrese de que los puntos de montaje NFS están indicados correctamente en `/etc/fstab`:

 `$ cat /etc/fstab` 
```
lithium:/mnt/data           /mnt/data	        nfs noauto,noatime,rsize=32768,wsize=32768,intr,hard 0 0
lithium:/var/cache/pacman   /var/cache/pacman	nfs noauto,noatime,rsize=32768,wsize=32768,intr,hard 0 0

```

La opción de montaje `noauto` le dice a systemd que no monte automáticamente los recursos compartidos en el arranque. De otro modo, systemd intentará montar los recursos compartidos nfs, que puedan o no existir en la red, demorando el proceso de arranque con una pantalla en blanco.

Con el fin de poder montar el recurso compartido NFS por un usuario normal, puede ser necesario añadir la opción `user` a la entrada fstab. También le posibilitará que active rpc-statd.service.

Cree el script `auto_share`, que será utilizado por *cron* para comprobar si el equipo NFS está accesible:

 `/root/bin/auto_share` 
```
#!/bin/bash

SERVER="YOUR_NFS_HOST"

MOUNT_POINTS=$(sed -e '/^.*#/d' -e '/^.*:/!d' -e 's/\t/ /g' /etc/fstab | tr -s " " | cut -f2 -d" ")

ping -c 1 "${SERVER}" &>/dev/null

if [ $? -ne 0 ]; then
    # The server could not be reached, unmount the shares
    for umntpnt in ${MOUNT_POINTS}; do
        umount -l -f $umntpnt &>/dev/null
    done
else
    # The server is up, make sure the shares are mounted
    for mntpnt in ${MOUNT_POINTS}; do
        mountpoint -q $mntpnt || mount $mntpnt
    done
fi

```

```
# chmod +x /root/bin/auto_share

```

Cree la entrada cron de root para ejecutar `auto_share` en todo momento:

 `# crontab -e` 
```
* * * * * /root/bin/auto_share

```

Un archivo de unidad de systemd también puede ser utilizado para montar los recursos compartidos NFS en el arranque. El archivo de unidad no es necesario si NetworkManager está instalado y configurado en el sistema cliente. Véase [#NetworkManager dispatcher](#NetworkManager_dispatcher).

 `/etc/systemd/system/auto_share.service` 
```
[Unit]
Description=NFS automount

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/root/bin/auto_share

[Install]
WantedBy=multi-user.target

```

Ahora active `auto_share`.

#### NetworkManager dispatcher

Además del método descrito anteriormente, NetworkManager también se puede configurar para ejecutar un script para cuando cambie el estado de la conexión de red.

Active e inicie el servicio `NetworkManager-dispatcher`.

El método más fácil para montar recursos compartidos al cambiar el estado de la red es creando un enlace simbólico al script `auto_share`:

```
# ln -s /root/bin/auto_share /etc/NetworkManager/dispatcher.d/30_nfs.sh

```

O, usando el script de montaje siguiente, que comprueba la disponibilidad de la red:

 `/etc/NetworkManager/dispatcher.d/30_nfs.sh` 
```
#!/bin/bash

SSID="CHANGE_ME"

MOUNT_POINTS=$(sed -e '/^.*#/d' -e '/^.*:/!d' -e 's/\t/ /g' /etc/fstab | tr -s " " | cut -f2 -d" ")

ISNETUP=$(nmcli dev wifi | \grep $SSID | tr -s ' ' | cut -f 10 -d ' ') 2>/dev/null

# echo "$ISNETUP" >> /tmp/nm_dispatch_log

if [[ "$ISNETUP" == "yes" ]]; then
    for mntpnt in ${MOUNT_POINTS}; do
        mountpoint -q $mntpnt || mount $mntpnt
    done
else
    for srvexp in ${MOUNT_POINTS}; do
        umount -l -f $srvexp &>/dev/null
    done
fi

```

Ahora, cuando el SSID inalámbrico "CHANGE_ME" se encienda o se apaque, el script `nfs.sh` será llamado para montar o desmontar los recursos compartidos, tan pronto le sea posible.

### Configurar puertos fijos para NFS

Si tiene un [cortafuegos](/index.php/Firewalls_(Espa%C3%B1ol) "Firewalls (Español)") configurado a través de un puerto, es posible que desee establecer puertos fijos. Para `rpc.statd` y `rpc.mountd` debe configurar los ajustes siguientes en `/etc/conf.d/nfs-common` y `/etc/conf.d/nfs-server` (los puertos pueden ser diferentes):

 `/etc/conf.d/nfs-common`  `STATD_OPTS="-p 4000 -o 4003"`  `/etc/conf.d/nfs-server`  `MOUNTD_OPTS="--no-nfs-version 2 -p 4002"`  `/etc/modprobe.d/lockd.conf` 
```
# Static ports for NFS lockd
options lockd nlm_udpport=4001 nlm_tcpport=4001
```

Después de reiniciar los demonios `nfs-common`, `nfs-server` y recargar los módulos `lockd`, puede comprobar los puertos utilizados con la siguiente orden:

 `$ rpcinfo -p` 
```
   program vers proto   port  service
    100000    4   tcp    111  portmapper
    100000    3   tcp    111  portmapper
    100000    2   tcp    111  portmapper
    100000    4   udp    111  portmapper
    100000    3   udp    111  portmapper
    100000    2   udp    111  portmapper
    100024    1   udp   4000  status
    100024    1   tcp   4000  status
    100021    1   udp   4001  nlockmgr
    100021    3   udp   4001  nlockmgr
    100021    4   udp   4001  nlockmgr
    100021    1   tcp   4001  nlockmgr
    100021    3   tcp   4001  nlockmgr
    100021    4   tcp   4001  nlockmgr
    100003    2   tcp   2049  nfs
    100003    3   tcp   2049  nfs
    100003    4   tcp   2049  nfs
    100003    2   udp   2049  nfs
    100003    3   udp   2049  nfs
    100003    4   udp   2049  nfs
    100005    3   udp   4002  mountd
    100005    3   tcp   4002  mountd

```

A continuación, es necesario abrir los puertos 111-2049-4000-4001-4002-4003 TCP y UDP.

## Solución de problemas

*Hay un artículo dedicado a la solución de problemas: [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting").*

## Véase también

*   Véase también [Avahi](/index.php/Avahi "Avahi"), una implementación de Zeroconf que permite la detección automática de recursos compartidos NFS.
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [Very helpful](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   Si va a configurar el servidor NFS con Arch Linux para ser usado por clientes con Windows mediante el SFU de Microsoft, sería aconsejable mirar [este mensaje del foro](https://bbs.archlinux.org/viewtopic.php?pid=523934#p523934) primero.
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [Unix interoperability and Windows Vista](http://blogs.msdn.com/sfu/archive/2007/05/01/unix-interoperability-and-windows-vista.aspx) Requisitos previos para conectarse a NFS con Windows Vista.
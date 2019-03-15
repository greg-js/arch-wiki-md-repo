**Estado de la traducción**
Este artículo es una traducción de [Glusterfs](/index.php/Glusterfs "Glusterfs"), revisada por última vez el **2019-03-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Glusterfs&diff=0&oldid=568751) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Ceph](/index.php/Ceph "Ceph")

[Glusterfs](https://www.gluster.org/) es un [sistema de archivos](/index.php/Filesystem_(Espa%C3%B1ol) "Filesystem (Español)") en red escalable.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [glusterfs](https://www.archlinux.org/packages/?name=glusterfs).

## Configuración

Glusterfs puede configurarse para ejecutarse en muchas opciones diferentes según las necesidades operativas, incluidas las distribuidas y las replicadas. Para el ejemplo a continuación, se está creando un servidor replicado de dos nodos, con los nodos gluster1 y gluster2\. Cada uno tiene dos discos, uno que contiene el sistema operativo (`sda`), el otro para ser compartido por glusterfs (`sdb`). A menos que se indique, toda la configuración se realiza en gluster1:

*   [Inicie/Active](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") `glusterd.service` en ambos servidores.

*   Conecte los servidores:

```
# gluster peer probe gluster2

```

*   Particione y formatee la unidad glusterfs en ambos servidores.
    *   Se recomienda crear una única partición y formatearla como xfs.

*   En ambos servidores se montan automáticamente las unidades [añadiendo](/index.php/Append "Append") `/etc/fstab` para incluir la siguiente linea, donde `/dev/sd*XY*` es el dispositivo apropiado (por ejemplo, `/dev/sdb1`):

 `/etc/fstab`  `/dev/sd*XY* /export/sd*XY* xfs defaults 0 0` 

*   En ambos servidores [monte](/index.php/Mount_(Espa%C3%B1ol) "Mount (Español)") los discos. Luego cree un *brick*:

```
# mkdir -p /export/sd*XY*/brick

```

*   Active la replicación en el servidor primario:

```
# gluster volume create gv0 replica 2 gluster1.mydomain.net:/export/sdb1/brick gluster2.mydomain.net:/export/sdb1/brick

```

*   Asegúrese de que el volumen se crea correctamente:

```
# gluster volume info

```

*   Inicie el volumen:

```
# gluster volume start gv0

```

*   Y finalmente, monte el volumen:

```
# mkdir -p /mnt/glusterClientMount
# mount -t glusterfs gluster1:/gv0 /mnt/glusterClientMount

```

## Véase también

*   [Guía oficial de instalación de glusterfs](https://docs.gluster.org/en/latest/Install-Guide/Overview/)
*   [Blog que cubre la configuración de Glusterfs en Arch Linux](https://blog.bastelfreak.de/2016/05/short-tip-setup-glusterfs-share-on-arch-linux/)
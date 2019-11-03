**Estado de la traducción**
Este artículo es una traducción de [Advanced Format](/index.php/Advanced_Format "Advanced Format"), revisada por última vez el **2019-10-30**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Advanced_Format&diff=0&oldid=587479) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El [formato avanzado](https://en.wikipedia.org/wiki/Advanced_Format "wikipedia:Advanced Format") es un término genérico que pertenece a cualquier formato de sector de disco utilizado para almacenar datos sobre discos magnéticos en [unidades de disco duro](https://en.wikipedia.org/wiki/hard_disk_drives "wikipedia:hard disk drives") (HDD) que utiliza sectores de 4 kilobytes en lugar de los tradicionales sectores de 512 bytes. La idea principal detrás del uso de sectores de 4096 bytes es aumentar la densidad de bits en cada pista reduciendo el número de espacios que contienen información Sync/DAM (memoria de acceso directo) y ECC (código de corrección de errores) entre sectores de datos. El formato anterior daba una eficiencia de formato del 88.7%, mientras que el formato avanzado da como resultado una eficiencia de formato del 97.3%.

Hay dos tipos de unidades de formato avanzado (siglas en inglés AF):

*   Unidades de formato avanzado, marcadas con un logotipo naranja «AF»: internamente, utilizan sectores 4k, pero proporcionan una capa de emulación para compatibilidad con sistemas operativos que carecen de soporte para ellos.
*   Unidades nativas de formato avanzado 4k, marcadas con un logotipo azul «4Kn»": requieren soporte del sistema operativo (Windows 8+ o Linux 2.6.31+). Debido a que no necesitan una capa de traducción, son más baratos, sin embargo, pueden ser incompatibles con las herramientas antiguas.

## Cómo determinar si HDD emplea un sector de 4k

El tamaño del sector físico y lógico del disco duro `/dev/sd*X*` se puede determinar leyendo las siguientes entradas de sysfs:

```
$ cat /sys/class/block/sd*X*/queue/physical_block_size
$ cat /sys/class/block/sd*X*/queue/logical_block_size

```

Las unidades con una capa de traducción (ver arriba) generalmente informarán un tamaño de bloque lógico de 512 (para compatibilidad con versiones anteriores) y un tamaño de bloque físico de 4096 (lo que indica que son unidades AF).

Las herramientas que informa del sector físico de una unidad (siempre que la unidad lo informe —al kernel— correctamente) incluyen:

*   [smartmontools](/index.php/S.M.A.R.T. "S.M.A.R.T.") a partir de 5.41: `smartctl -a /dev/sd*X* | grep 'Sector Size:'`
*   [hdparm](/index.php/Hdparm "Hdparm") a partir de 9.12: `hdparm -I /dev/sd*X* | grep 'Physical Sector size:'`

Tenga en cuenta que ambos funcionan incluso para discos conectados por USB (si el puente USB admite SAT conocida como [SCSI/ATA Translation (SAT)](https://en.wikipedia.org/wiki/SCSI_/_ATA_Translation "wikipedia:SCSI / ATA Translation"), [ANSI](https://en.wikipedia.org/wiki/es:Instituto_Nacional_Estadounidense_de_Est%C3%A1ndares "wikipedia:es:Instituto Nacional Estadounidense de Estándares") INCITS 431-2007).

## Véase también

*   [Western Digital’s Advanced Format: The 4K Sector Transition Begins](http://www.anandtech.com/Show/Index/2888)
*   [White paper entitled "Advanced Format Technology."](http://www.wdc.com/wdproducts/library/WhitePapers/ENG/2579-771430.pdf)
*   El fallo al alinear HDD se traduce en un pobre rendimiento de lectura/escritura. Véase [este artículo](http://www.linuxconfig.org/linux-wd-ears-advanced-format) para ejemplos específicos.
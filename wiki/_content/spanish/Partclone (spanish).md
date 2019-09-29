**Estado de la traducción**
Este artículo es una traducción de [Partclone](/index.php/Partclone "Partclone"), revisada por última vez el **2019-09-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Partclone&diff=0&oldid=583609) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Partclone](http://partclone.org), como el conocido [Partimage](http://www.partimage.org/Main_Page), se puede usar para hacer una copia de seguridad y restaurar una partición, considerando solo los bloques usados.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilizar Partclone con una partición formateada con ext4](#Utilizar_Partclone_con_una_partición_formateada_con_ext4)
    *   [2.1 Sin compresión](#Sin_compresión)
    *   [2.2 Con compresión](#Con_compresión)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [partclone](https://www.archlinux.org/packages/?name=partclone).

## Utilizar Partclone con una partición formateada con ext4

### Sin compresión

Para hacer una copia de seguridad *sin* compresión:

```
$ partclone.ext4 -c -s /dev/sda1 -o ~/image_sda1.pcl

```

Para restaurarla:

```
$ partclone.ext4 -r -s ~/image_sda1.pcl -o /dev/sda1

```

### Con compresión

Para hacer una copia de seguridad *con* compresión:

```
$ partclone.ext4 -c -s /dev/sda1 | gzip -c > ~/image_sda1.pcl.gz

```

**Nota:** para una máxima compresión, utilice «gzip -c9»

Para restaurarla:

```
zcat ~/image_sda1.pcl.gz | partclone.ext4 -r -o /dev/sda1

```
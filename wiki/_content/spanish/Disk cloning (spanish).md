**Estado de la traducción**
Este artículo es una traducción de [Disk cloning](/index.php/Disk_cloning "Disk cloning"), revisada por última vez el **2019-09-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Disk_cloning&diff=0&oldid=583611) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance (Español)#Copias de respaldo](/index.php/System_maintenance_(Espa%C3%B1ol)#Copias_de_respaldo "System maintenance (Español)")
*   [System backup (Español)](/index.php/System_backup_(Espa%C3%B1ol) "System backup (Español)")

La clonación de disco es el proceso por el cual se obtiene una imagen de una partición o de un disco duro completo. Esto puede ser útil para copiar la unidad a otros equipos y para propósitos de [copias de respaldo](/index.php/System_maintenance_(Espa%C3%B1ol)#Copias_de_respaldo "System maintenance (Español)") y de [recuperación](/index.php/File_recovery "File recovery").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilizar dd](#Utilizar_dd)
*   [2 Utilizar ddrescue](#Utilizar_ddrescue)
*   [3 Clonar sistema de archivos](#Clonar_sistema_de_archivos)
    *   [3.1 Utilizar e2image](#Utilizar_e2image)
*   [4 Software de clonación de disco](#Software_de_clonación_de_disco)
    *   [4.1 dd spin-offs](#dd_spin-offs)
*   [5 Véase también](#Véase_también)

## Utilizar dd

Vea [dd (Español)#Clonación y restauración de discos](/index.php/Dd_(Espa%C3%B1ol)#Clonación_y_restauración_de_discos "Dd (Español)").

## Utilizar ddrescue

[ddrescue](https://www.archlinux.org/packages/?name=ddrescue) es una herramienta diseñada para clonar y recuperar datos. Copia datos de un archivo o dispositivo de bloque (disco duro, cdrom, etc.) a otro, tratando de rescatar primero las partes buenas para el caso de errores de lectura, con el fin de maximizar los datos recuperados.

Para clonar una unidad defectuosa o agonizante, ejecute dos veces *ddrescue*. En la primera ronda, se copia cada bloque sin error de lectura y registra los errores en `rescue.log`.

```
# ddrescue -f -n /dev/sd*X* /dev/sd*Y* rescue.log

```

donde `*X*` y `*Y*` son las letras de las particiones deseadas de los [dispositivos de bloques](/index.php/Device_file_(Espa%C3%B1ol)#Dispositivos_de_bloque "Device file (Español)").

En la segunda ronda, copia solo los bloques defectuosos e intenta leerlos 3 veces desde la fuente antes de desistir.

```
# ddrescue -d -f -r3 /dev/sd*X* /dev/sd*Y* rescue.log

```

Ahora se puede verificar si el sistema de archivos está dañado y montar la nueva unidad.

```
# fsck -f /dev/sd*Y*

```

## Clonar sistema de archivos

### Utilizar e2image

*e2image* es una herramienta incluida en [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) con fines de depuración. Se puede usar para copiar particiones ext2, ext3 y ext4 de manera eficiente al realizar copias solo de los bloques usados. Tenga en cuenta que esto solo funciona para los sistemas de archivos ext2, ext3 y ext4, y los bloques no utilizados no se copian, por lo que puede que esta herramienta no le sea útil si lo que espera es recuperar archivos eliminados.

Para clonar una partición desde el disco físico `/dev/sda`, partición 1, al disco físico `/dev/sdb`, partición 1, con e2image, ejecute:

```
# e2image -ra -p /dev/sda1 /dev/sdb1

```

**Sugerencia:** [GNU Parted](/index.php/Parted "Parted") utiliza *e2image* para copiar eficientemente las particiones ext2/3/4.

## Software de clonación de disco

Estas aplicaciones permiten realizar fácilmente copias de seguridad de sistemas de archivos completos y recuperación en caso de falla, generalmente en forma de un CD Live o unidad USB. Contienen imágenes completas del sistema realizadas en uno o más momentos específicos en el tiempo y se utilizan con frecuencia para registrar configuraciones buenas conocidas. Vea [Wikipedia:Comparison of disk cloning software](https://en.wikipedia.org/wiki/Comparison_of_disk_cloning_software "wikipedia:Comparison of disk cloning software") para su comparación.

Véase también [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para ver otras aplicaciones que pueden tomar instantáneas completas del sistema, entre otras funciones.

*   **Arch Backup** — Un script básico de copia de seguridad con una configuración simple:
    *   Método de compresión configurable.
    *   Múltiples objetivos de respaldo.

	[https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/](https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **[Clonezilla](https://en.wikipedia.org/wiki/es:Clonezilla "wikipedia:es:Clonezilla")** — Una solución de recuperación ante desastres, clonación de discos, creación e implementación de imágenes:
    *   Arranca desde CD Live, unidad flash USB o servidor PXE.
    *   Admite ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs, FAT32, NTFS, HFS+ y otros.
    *   Utiliza Partclone (predeterminado), Partimage (opcional), ntfsclone (opcional) o dd para crear imágenes o clonar una partición.
    *   Servidor de multidifusión para restaurar varias máquinas a la vez.
    *   Incluido en los medios de instalación de Arch Linux.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **Deepin Clone** — Herramienta de Deepin para hacer copias de seguridad y restauración. Permite clonar, realizar copias de seguridad y restaurar discos o particiones.

	[https://www.deepin.org/en/original/deepin-clone/](https://www.deepin.org/en/original/deepin-clone/) || [deepin-clone](https://www.archlinux.org/packages/?name=deepin-clone)

*   **FSArchiver** — Una herramienta segura y flexible de copia de seguridad y despliegue de sistemas de archivos:
    *   Soporte para atributos básicos de archivo (permisos, propietario, ...).
    *   Soporte para múltiples sistemas de archivos por compresión.
    *   Soporte para atributos extendidos (son utilizados por SELinux).
    *   Soporte para atributos básicos del sistema de archivos (etiqueta, uuid, tamaño de bloque) para todos los sistemas de archivos Linux.
    *   Soporte para [sistemas de archivos NTFS](http://www.fsarchiver.org/Cloning-ntfs) (capacidad para crear clones flexibles de particiones de Windows).
    *   Realiza suma de comprobación de todo lo que está escrito en el archivo (encabezados, bloques de datos, archivos completos).
    *   Posibilidad de restaurar un archivo que está dañado (solo omitirá el archivo actual).
    *   Compresión multihilo lzo, gzip, bzip2, lzma.
    *   Soporte para dividir archivos grandes en varios archivos con un tamaño máximo fijo.
    *   Cifrado del archivo usando una contraseña. Basado en blowfish de libcrypto de [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Soporte de copia de seguridad de un sistema de archivos raíz montado (opción `-A`).
    *   Se puede encontrar en el [System Rescue CD](http://www.sysresccd.org/Main_Page).

	[http://www.fsarchiver.org/](http://www.fsarchiver.org/) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/es:Mondo_Rescue "wikipedia:es:Mondo Rescue")** — Una solución de recuperación ante desastres para crear medios de respaldo que pueden usarse para volver a implementar el sistema dañado:
    *   Realiza copias de seguridad basadas en imágenes, compatibles con Linux/Windows.
    *   La tasa de compresión es ajustable.
    *   Puede respaldar sistemas live (sin tener que detenerlo).
    *   Puede dividir la imagen en varios archivos.
    *   Admite el arranque en un CD Live para realizar una restauración completa.
    *   Puede realizar copias de seguridad/restaurar a través de NFS, desde CD, unidades de cinta y otros medios.
    *   Puede verificar las copias de seguridad.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

*   **[Partclone](/index.php/Partclone "Partclone")** — Una herramienta que se puede usar para hacer una copia de seguridad y restaurar una partición, considerando solo los bloques usados:
    *   Admite ext2, ext3, ext4, hfs+, reiserfs, reiser4, btrfs, vmfs3, vmfs5, xfs, jfs, ufs, ntfs, fat(12/16/32), exfat.
    *   Soporta compresión.
    *   Opcionalmente, se puede usar una interfaz *ncurses*.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — Una utilidad de clonación de disco *ncurses* para entornos Linux/UNIX.
    *   Tiene un CD live.
    *   Admite los sistemas de archivos más populares en Linux, Windows y Mac OS.
    *   Compresión.
    *   Guarda en múltiples CD o DVD o en una red usando Samba/NFS.
    *   El desarrollo se detuvo a favor de FSArchiver.p

	[http://www.partimage.org](http://www.partimage.org) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **J7Z** — GUI para Linux en Java que intenta simplificar la compresión de datos y la copia de seguridad. Puede crear archivos 7z, BZip2, Zip, GZip, Tar:
    *   Actualiza archivos existentes rápidamente.
    *   Realiza copia de seguridad de múltiples carpetas en una ubicación de almacenamiento.
    *   Crea o extrae archivos protegidos.
    *   Disminuya el esfuerzo mediante el uso de archivar perfiles y listas.

	[http://j7z.xavion.name/](http://j7z.xavion.name/) || [j7z](https://aur.archlinux.org/packages/j7z/)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — Una aplicación de respaldo y recuperación ante desastres que se ejecuta desde una imagen de CD de Linux arrancable:
    *   Es capaz de realizar copias de seguridad y recuperación de particiones de disco.
    *   Utiliza [xPUD](http://www.xpud.org/) y [Partclone](/index.php/Partclone "Partclone") para el backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) ||

*   **System Tar & Restore** — Realiza copia de seguridad y restauración del sistema usando tar o transfiriéndolo con rsync:
    *   Interfaces GUI y CLI interfaces.
    *   Crea empaquetados *.tar.gz* , *.tar.bz2* , *.tar.xz* o *.tar*
    *   Soporta encriptación openssl/gpg.
    *   Utiliza rsync para transferir un sistema en ejecución.
    *   Compatible con Grub2, Syslinux, EFISTUB/efibootmgr y Systemd/bootctl.

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

### dd spin-offs

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) es un reemplazo de dd con capacidad de [funciones hash](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash") realizada sobre la marcha que ayuda a garantizar la integridad. Acepta la mayoría de los parámetros de dd e incluye salida de estado. Una versión estable de *dcfldd* fue [lanzada por última vez en 2006](http://dcfldd.sourceforge.net/).

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) es una herramienta de recuperación de datos capaz de ignorar los errores de lectura. *ddrescue* no está relacionado con dd de ninguna manera, excepto que ambos pueden usarse para copiar datos de un dispositivo a otro. La diferencia clave es que *ddrescue* usa un algoritmo sofisticado para copiar datos de unidades defectuosas causándoles el menor daño adicional posible. Consulte el [manual de ddrescue](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) para obtener más detalles.

## Véase también

*   [Lista de software de clonación de disco](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Hilo del foro Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=4329)
Según [Wikipedia](https://en.wikipedia.org/wiki/es:Unidad_de_disco_%C3%B3ptico "wikipedia:es:Unidad de disco óptico")

	*En informática, una unidad de disco óptico es una unidad de disco que usa una luz láser u ondas electromagnéticas cercanas al espectro de la luz como parte del proceso de lectura o escritura de datos desde un archivo a discos ópticos. Algunas unidades solo pueden leer discos, pero las unidades más recientes usualmente son tanto lectoras como grabadoras. Para referirse a las unidades con ambas capacidades se suele usar el término lectograbadora. Los discos compactos (CD), DVD (Disco versátil digital) , y Blu-ray Disc (también conocido como Blu-ray o BD) son los tipos de soportes ópticos más comunes que pueden ser leídos y grabados por estas unidades.*

## Contents

*   [1 Grabación](#Grabaci.C3.B3n)
    *   [1.1 Instalar utilidades de grabación](#Instalar_utilidades_de_grabaci.C3.B3n)
    *   [1.2 Crear una imagen ISO con archivos presentes en el disco duro](#Crear_una_imagen_ISO_con_archivos_presentes_en_el_disco_duro)
        *   [1.2.1 parámetros básicos](#par.C3.A1metros_b.C3.A1sicos)
        *   [1.2.2 graft-points](#graft-points)
    *   [1.3 Montar una imagen ISO](#Montar_una_imagen_ISO)
    *   [1.4 Convertir imagen img/ccd en una imagen ISO](#Convertir_imagen_img.2Fccd_en_una_imagen_ISO)
    *   [1.5 Conocer el nombre de la unidad óptica](#Conocer_el_nombre_de_la_unidad_.C3.B3ptica)
    *   [1.6 Leer una imagen ISO desde un CD, DVD o BD](#Leer_una_imagen_ISO_desde_un_CD.2C_DVD_o_BD)
    *   [1.7 Borrar CD-RW y DVD-RW](#Borrar_CD-RW_y_DVD-RW)
    *   [1.8 Grabar una imagen ISO al CD, DVD o BD](#Grabar_una_imagen_ISO_al_CD.2C_DVD_o_BD)
    *   [1.9 Verificar la imagen ISO grabada](#Verificar_la_imagen_ISO_grabada)
    *   [1.10 ISO 9660 y grabación al vuelo (*On-The-Fly*)](#ISO_9660_y_grabaci.C3.B3n_al_vuelo_.28On-The-Fly.29)
    *   [1.11 Multisesión](#Multisesi.C3.B3n)
        *   [1.11.1 Multisesión con wodim](#Multisesi.C3.B3n_con_wodim)
        *   [1.11.2 Multisesión con growisofs](#Multisesi.C3.B3n_con_growisofs)
        *   [1.11.3 Multisesión con xorriso](#Multisesi.C3.B3n_con_xorriso)
    *   [1.12 Defect Management en BD (Blu-ray disc)](#Defect_Management_en_BD_.28Blu-ray_disc.29)
    *   [1.13 Grabar un CD de audio](#Grabar_un_CD_de_audio)
    *   [1.14 Grabar una imagen bin/cue](#Grabar_una_imagen_bin.2Fcue)
        *   [1.14.1 TOC/CUE/BIN para discos en modalidad mixta](#TOC.2FCUE.2FBIN_para_discos_en_modalidad_mixta)
    *   [1.15 Problemas con los backend de grabación](#Problemas_con_los_backend_de_grabaci.C3.B3n)
    *   [1.16 Grabar CD/DVD/BD con una GUI](#Grabar_CD.2FDVD.2FBD_con_una_GUI)
        *   [1.16.1 Programas GUI libres](#Programas_GUI_libres)
        *   [1.16.2 Nero Linux](#Nero_Linux)
*   [2 Reproducir DVD](#Reproducir_DVD)
*   [3 Ripear DVD](#Ripear_DVD)
    *   [3.1 dvd::rip](#dvd::rip)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 K3b y el error sobre el locale](#K3b_y_el_error_sobre_el_locale)
    *   [4.2 Brasero falla al encontrar discos en blanco](#Brasero_falla_al_encontrar_discos_en_blanco)
    *   [4.3 Brasero falla al normalizar el CD de audio](#Brasero_falla_al_normalizar_el_CD_de_audio)
    *   [4.4 VLC: Error «... could not open the disc /dev/dvd»](#VLC:_Error_.C2.AB..._could_not_open_the_disc_.2Fdev.2Fdvd.C2.BB)
    *   [4.5 Unidad DVD con ruidos](#Unidad_DVD_con_ruidos)
    *   [4.6 La reproducción no funciona con el equipo nuevo (unidad DVD nueva)](#La_reproducci.C3.B3n_no_funciona_con_el_equipo_nuevo_.28unidad_DVD_nueva.29)
    *   [4.7 Ninguno de los programas descritos puede ripear/codificar un DVD en el disco duro](#Ninguno_de_los_programas_descritos_puede_ripear.2Fcodificar_un_DVD_en_el_disco_duro)
    *   [4.8 El registro del programa GUI indica problemas con el programa del backend](#El_registro_del_programa_GUI_indica_problemas_con_el_programa_del_backend)
        *   [4.8.1 Caso especial: medium error / write error](#Caso_especial:_medium_error_.2F_write_error)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Grabación

El proceso de grabación de las unidades de disco óptico consiste en la creación o la obtención de una imagen y escribirla en un soporte óptico. La imagen puede ser cualquier archivo de datos, en principio. Si, a continuación, desea montar el medio resultante, se tratará, por lo general, de un archivo de imagen del sistema de archivos ISO 9660\. Los CD de audio y multimedia se queman con frecuencia desde un archivo BIN, bajo el control de un archivo TOC o un archivo CUE, que describen el trazado de la pista deseada.

### Instalar utilidades de grabación

Si desea utilizar programas con interfaz gráfica siga [esta sección](#Optical_Disc_Drive_.28Espa.C3.B1ol.29.23Grabar_CD.2FDVD.2FBD_con_una_GUI).

Los programas enumerados aquí son los backends utilizados por la mayoría de los programas GUI gratuitos para grabar CD, DVD y BD. Están orientados a su utilización en la líneas de órdenes. Los usuarios que utilicen interfaces gráficas pueden servirse del conocimiento de aquellos cuando intenten resolver problemas o para crear scripts para actividades de grabación.

Necesitará, al menos, un programa para la creación de imágenes de sistemas de archivos y un programa que sea capaz de grabar los datos en el tipo de soporte deseado.

Los programas disponibles para la creación de imágenes ISO 9660 son:

*   `genisoimage` del paquete [cdrkit](https://www.archlinux.org/packages/?name=cdrkit)
*   `mkisofs` del paquete [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   `xorriso` y `xorrisofs` del paquete [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

La elección tradicional es `genisoimage`.

Los programas disponibles para grabar las imágenes en un soporte óptico son:

*   `cdrdao` del paquete [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) (CD únicamente, TOC/CUE/BIN únicamente)
*   `cdrecord` del paquete [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   `cdrskin` del paquete [libburn](https://www.archlinux.org/packages/?name=libburn)
*   `growisofs` del paquete [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) (DVD y BD únicamente)
*   `wodim` del paquete [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) (CD únicamente, DVD obsoleto)
*   `xorriso` y `xorrecord` del paquete [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Las elecciones tradicionales son `wodim` para CD y `growisofs` para DVD y Blu-ray Disc. Para growisofs y BD-R consulte la solución de errores a continuación. Para escribir archivos TOC/CUE/BIN a CD, instale `cdrdao`.

Los programas GUI gratuitos para grabar CD, DVD y BD dependen, al menos, de uno de los paquetes anteriores.

Los programas `genisoimage`, `mkisofs`, y `xorrisofs` son compatibles con las opciones genisoimage y se muestran en este documento.

Los programas `cdrecord`, `cdrskin` y `wodim` son compatibles con las opciones wodim mostradas aquí. El programa `xorrecord` da soporte a aquellos que no se ocupan de los CD de audio.

**Nota:**

*   La instalación de los paquetes [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) y [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) entrará en conflicto. Instale únicamente uno de ellos.
*   Si desea instalar cdrtools, asegúrese de que genera un paquete usando [makepkg](/index.php/Makepkg "Makepkg") e instálelo con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). En cambio, los wrappers de pacman podrán resolver esto para cdrkit.

### Crear una imagen ISO con archivos presentes en el disco duro

Esto se puede lograr mediante el uso tanto de *mkisofs* o su fork *cdrkit* de *genisoimage*.

La manera más simple de crear una imagen ISO es copiar los archivos necesarios a una carpeta, por ejemplo `./for_iso`.

Luego, utilizar `mkisofs` o `genisoimage` de la manera indicada en el siguiente ejemplo:

```
$ genisoimage -V "ARCHIVE_2013_07_27" -J -r -o isoimage.iso ./for_iso

```

Cada una de las etiquetas/parámetros usados en el ejemplo se explican a continuación:

#### parámetros básicos

	-V

	Da al sistema de archivos un nombre que, probablemente, se mostrará como punto de montaje, si el soporte se monta automáticamente. Las especificaciones de la ISO solo permiten 32 caracteres como máximo: «A» a «Z», «0» a «9», y «_». Esta etiqueta del volumen, probablemente se mostrará como punto de montaje, si el soporte se monta automáticamente.

	-J

	Prepara nombres de hasta 64 caracteres UTF-16 para los lectores de MS- Windows. Conocido como «Joliet».

	-joliet-long

	Permitiría 103 caracteres UTF-16 para los lectores de MS-Windows. No conformes con las especificaciones de Joliet.

	-r

	Prepara nombres de un máximo de 255 caracteres para los lectores de Unix y le da permiso de lectura para todos. Conocido como «Rock Ridge».

	-o

	Define la ruta del archivo de la imagen ISO resultante.

#### graft-points

También es posible utilizar genisoimage o mkisofs para recolectar archivos y directorios de varias rutas:

```
$ genisoimage -V "BACKUP_2013_07_27" -J -r -o backup_2013_07_27.iso \
  -graft-points \
  /photos=/home/user/photos \
  /mail=/home/user/mail \
  /photos/holidays=/home/user/holidays/photos

```

	-graft-points

	Activa el reconocimiento de *pathspecs* que contiene una dirección de destino en el sistema de archivos ISO (por ejemplo '`/photos`) y una dirección de origen en el disco duro (por ejemplo `/home/user/photos`). Ambas están separadas por un carácter «=».

En el siguiente ejemplo se ponen los directorios del disco `/home/user/photos`, `/home/user/mail` y `/home/user/holidays/photos`, en la imagen ISO como `/photos`, `/mail` y `/photos/holidays`, respectivamente.

Los programas `mkisofs` y `xorrisofs` aceptan las mismas opciones. Para copias de respaldo seguras considere utilizar `xorrisofs` con la opción `--for_backup`, que registra las ACL eventuales y almacena una suma de comprobación MD5 para cada archivo de datos.

Consulte los manuales de los programas ISO 9660 para obtener más información acerca de sus opciones:

*   [genisoimage](http://linux.die.net/man/1/genisoimage)

*   [mkisofs](http://cdrecord.berlios.de/private/man/cdrecord/mkisofs.8.html)

*   [xorrisofs](http://www.gnu.org/software/xorriso/man_1_xorrisofs.html)

**Nota:** Este proceso se puede considerar desde una doble perspectiva:

*   por un lado, como crear un archivo (que no es tan distinto, salvando las diferencias, de la creación de un archivo comprimido ZIP o TAR —por ejemplo, `.tar.gz`—);
*   por otro, como crear y *poblar* un sistema de archivos para el volumen, que se articula en forma de una imagen de «disco» (archivo) y que conserva, tanto como sea posible, el contenido, nombre, estructura/jerarquía/colocación relativa a los directorios, y, posiblemente, otros metadatos/propiedades (aspectos) generales del sistema de archivos tales como marca de tiempo, propietarios, permisos.

### Montar una imagen ISO

Para probar si la imagen ISO es adecuada, puede montarla (como root):

```
# mount -t iso9660 -o ro,loop=/dev/loop0 cd_image /cdrom

```

Deberá cargar primero el módulo loop:

```
# modprobe loop

```

No se olvide de desmontar la imagen cuando la comprobación de la imagen haya terminado:

```
# umount /cdrom

```

Véase también [montar imágenes como usuario normal](/index.php/Mounting_images_as_user "Mounting images as user") para montar sin privilegios de root.

### Convertir imagen img/ccd en una imagen ISO

Para convertir una imagen `img`/`ccd`, puede usar [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso):

```
$ ccd2iso ~/image.img ~/image.iso

```

### Conocer el nombre de la unidad óptica

Para el resto de esta sección se supone que el nombre de su dispositivo de grabación es `/dev/sr0`.

Compruebe esta condición con:

```
$ wodim dev=/dev/sr0 -checkdrive

```

Que debe mostar el «Vendor_info» y la «Identification» de la unidad.

Si no se encuentra ninguna unidad, compruebe si existe algún `/dev/sr*` y si tiene permisos de lectura/escritura (`wr-`) para usted y a su grupo. En el caso de que no exita `/dev/sr*` inténtelo con: [loading](/index.php/Kernel_modules "Kernel modules") module `sr_mod` manually.

### Leer una imagen ISO desde un CD, DVD o BD

Se debe determinar el tamaño del sistema de archivos de la ISO antes de copiarlo al disco duro. La mayoría de los soportes ópticos admiten más datos de lo que se escribe en ellos con la ejecución de las grabadores más reciente.

Utilice el programa `isosize` del paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux) para obtener el tamaño de la imagen:

```
$ blocks=$(expr $(isosize /dev/sr0) / 2048)

```

Echa un vistazo al número obtenido de bloques para determinar si es aceptable:

 `$ echo "That would be $(expr $blocks / 512) MB"` 
```
That would be 589 MB

```

A continuación, copie el importe determinado de los datos del soporte al disco duro:

```
$ dd if=/dev/sr0 of=isoimage.iso bs=2048 count=$blocks

```

Omita `count=$blocks` si no determina el tamaño. Probablemente obtendrá más datos de los necesarios. El archivo resultante, sin embargo, será montable. Dicha imagen debe encajar en un soporte del mismo tipo que el soporte desde el que ha copiado la imagen.

Si el soporte original fuese arrancable, entoces la copia será una imagen de arranque. Puede usarla como un pseudo CD para una máquina virtual o grabarla en un disco óptico que se convertirá en arrancable.

### Borrar CD-RW y DVD-RW

Los soportes ​​CD-RW que contienen datos deben ser previamente borrados antes de poder grabarlos. Esto se hace así:

```
$ wodim -v dev=/dev/sr0 blank=fast

```

Los DVD-RW sin formatear necesitan el mismo tratamiento anterior antes de usarlos. Sin embargo, el borrado rápido les priva de la capacidad multisesión y del registro de los flujos de longitud imprevistos. Así que debe borrarlos formateándolos como sigue:

```
$ dvd+rw-format -blank=full /dev/sr0

```

`dvd+rw-format` forma parte del paquete [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools). Otras órdenes alternativas para la operación anterior serían:

```
$ cdrecord -v dev=/dev/sr0 blank=all
$ cdrskin -v dev=/dev/sr0 blank=all
$ xorriso -outdev /dev/sr0 -blank as_needed

```

Los soportes DVD-RW formateados se pueden sobrescribir sin ser previamente borrados. Así que considere la posibilidad de aplicar el formato una vez durante su vida útil:

```
$ dvd+rw-format -force /dev/sr0

```

Otras órdenes alternativas a la anterior:

```
$ cdrskin -v dev=/dev/sr0 blank=format_overwrite
$ xorriso -outdev /dev/sr0 -format as_needed

```

El resto de los soportes solo pueden escribirse una vez (CD-R, DVD-R, DVD+R, BD-R) o son sobrescribibles sin necesidad de borrarle los datos (DVD-RAM, DVD+RW, BD-RE).

### Grabar una imagen ISO al CD, DVD o BD

Para grabar rápidamente en un CD una imagen ISO (archivo `isoimage.iso`):

```
$ wodim -v -sao dev=/dev/sr0 isoimage.iso

```

y en un DVD o BD:

```
$ growisofs -dvd-compat -Z /dev/sr0=isoimage.iso

```

Los programas `cdrecord`, `cdrskin` y `xorrecord` pueden ser usados ​​en todo tipo de soportes ópticos con las opciones `wodim`.

**Nota:**

*   Asegúrese de que el soporte óptico no está montado cuando comience la grabación. El montaje puede realizarse automáticamente si el soporte contiene un sistema de archivos legible. En el mejor de los casos, impedirá que los programas de grabación utilicen la grabadora. En el peor de los casos, habrá grabados erróneos perturbando las operaciones de lectura de la unidad.

Así que, en caso de duda, haga:

```
# umount /dev/sr0

```

*   `growisofs` tiene un pequeño error en los soportes BD-R en blanco. Emite un mensaje de error después de finalizar la grabación. Los programas como `k3b` terminarán la grabación advirtiendo que falló.
    Para evitar esto, o bien:
    *   formatee el BD-R en blanco con `dvd+rw-format /dev/sr0` antes de ejecutar growisofs,
    *   o utilice la opción `-use-the-force-luke=spare:none` con growisofs.

### Verificar la imagen ISO grabada

Puede verificar la integridad del soporte grabado para asegurarse de que no contiene errores. Siempre, antes de verificar la imagen del soporte, expúlselo del dispositivo de grabación y vuelva a ponerlo de nuevo. El kernel podrá acceder sobre el contenido del soporte solo después de esa reinserción.

Calcule primero la suma md5 de la imagen ISO original:

 `$ md5sum isoimage.iso` 
```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

Después, calcule la suma md5 del sistema de archivos ISO presente en el soporte óptico.

Hay que tener en cuenta que, aunque algunos tipos de soportes contienen exactamente la misma cantidad de datos que se han presentado en el programa de grabación, otros, en cambio, contienen apéndices que arrastran basura cuando se está leyendo. Por lo tanto, se debe limitar la lectura al tamaño del archivo de la imagen ISO.

```
$ blocks=$(expr $(du -b isoimage.iso | awk '{print $1}') / 2048)

```
 `$ dd if=/dev/sr0 bs=2048 count=$blocks | md5sum` 
```
 43992+0 records in
 43992+0 records out
 90095616 bytes (90 MB) copied, 0.359539 s, 251 MB/s
 e5643e18e05f5646046bb2e4236986d8  -

```

Ambas salidas deben producir la misma suma MD5 (aquí: `e5643e18e05f5646046bb2e4236986d8`). Si no coinciden, probablemente también reciba un mensaje de error de entrada/salida al ejecutar `dd`. `dmesg` podría ayudarle a contar respecto a los errores SCSI y a los números de bloques, si está interesado.

### ISO 9660 y grabación al vuelo (*On-The-Fly*)

No es necesario almacenar un sistema de archivos ISO emergente en el disco duro antes de escribirlo en un soporte óptico. Solo las unidades de CD muy antiguas en ordenadores viejos podrían sufrir errores de grabación debido al búfer vacío.

Si se omite la opción `-o` de `genisoimage` se escribirá la imagen ISO en la salida estándar. Esto puede canalizarse hacia la salida estándar del programa de grabación.

```
$ genisoimage -V "ARCHIVE_2013_07_27" -J -r ./for_iso | \
  wodim -v dev=/dev/sr0 -waiti -

```

La opción `-waiti` no es realmente necesaria aquí. Evita que `wodim` escriba en el soporte antes de que `genisoimage` inicie la grabación. Esto permitirá a `genisoimage` leer el soporte óptico sin perturbar una grabación ya iniciada. Véase la sección siguiente sobre multisesión.

Respecto a los DVD y BD puede dejar que `growisofs` gestione `genisoimage` para realizar la grabación sobre la marcha.

```
$ export MKISOFS="genisoimage"
$ growisofs -Z /dev/sr0 -V "ARCHIVE_2013_07_27" -r -J ./for_iso

```

### Multisesión

Multisesión ISO 9660 significa que un soporte con el sistema de archivos legible sigue siendo modificable en su primera alineación del bloque no utilizado, y que un nuevo árbol de directorios ISO se escribirá a esa parte del disco no utilizada. El nuevo árbol es acompañado por los bloques de contenido de archivos de datos que acaba de agregar o sobrescribir. Los bloques de los archivos de datos, que quedarán como tal en el árbol antiguo de la ISO, no se escribirán de nuevo.

Linux y muchos otros sistemas operativos montan el árbol de directorios en el último período de sesiones del soporte. Este árbol más reciente, normalmente, mostrará los archivos de las sesiones anteriores, también.

#### Multisesión con wodim

Los CD-R y CD-RW pueden permanecer abiertos para escribirse (conocido como *«appendable»* -con capacidad para ampliarse, ampliable-) si utilizan la opción `-multi` de wodim:

```
$ wodim -v -multi dev=/dev/sr0 isoimage.iso

```

Posteriormente, el soporte puede ser preguntado por los parámetros de la próxima sesión:

```
$ m=$(wodim dev=/dev/sr0 -msinfo)

```

Con la ayuda de estos parámetros y del soporte reutilizable insertado en la unidad puede realizar la sesión ISO complementaria:

```
$ genisoimage -M /dev/sr0 -C "$m" \
   -V "ARCHIVE_2013_07_28" -J -r -o session2.iso ./more_for_iso

```

Por último, agregue la sesión al soporte y manténgalo con capacidad de ampliarse, de nuevo:

```
$ wodim -v -multi dev=/dev/sr0 session2.iso

```

Los programas `cdrskin` y `xorrecord` pueden hacer esto también con los DVD-R, DVD+R, BD-R, y DVD-RW sin formatear. El programa `cdrecord` no tiene capacidad multisesión con, al menos, los DVD-R y DVD-RW. Todos los programas, por supuesto, puede realizar esta operación para los CD-R y CD-RW.

La mayoría de los tipos de soporte reutilizables no registran un historial de sesiones que sería reconocible para un kernel de montaje. Pero con la norma ISO 9660, es posible lograr el efecto multisesión, incluso en tales soportes.

`growisofs` y `xorriso` pueden hacer esto y ahorrarnos la mayor parte de la complejidad.

#### Multisesión con growisofs

`growisofs` acepta la mayoría de los argumentos de estos programas para un programa que sea compatible con `mkisofs`. Véanse los ejemplos anteriores sobre `genisoimage`. La opción `-o` está vetada y la opción `-C` está obsoleta. Por defecto, el nombre usado para el probrama instalado es «mkisofs». Se puede elegir entre un programa u otro definiendo `MKISOFS` como la variable del entorno:

```
$ export MKISOFS="genisoimage"
$ export MKISOFS="xorrisofs"

```

Si deseacomenzar con un nuevo sistema de archivos ISO en el soporte óptico, expréselo mediante la opción `-Z`

```
$ growisofs -Z /dev/sr0 -V "ARCHIVE_2013_07_27" -r -J ./for_iso

```

Si desea añadir más archivos como una nueva sesión a un sistema de archivos ISO existente, expréselo mediante la opción `-M`

```
$ growisofs -M /dev/sr0 -V "ARCHIVE_2013_07_28" -r -J ./more_for_iso

```

Para más detalles, véase el [manual de growisofs](http://linux.die.net/man/1/growisofs) y los manuales de `genisoimage`, `mkisofs` y `xorrisofs`.

#### Multisesión con xorriso

`xorriso` necesita inicarse con un nuevo sistema de archivos ISO en un soporte óptico en blanco. Por lo tanto, es conveniente vaciarlo si contiene datos. La orden `-blank as_needed` se aplica a todo tipo de soportes reutilizables e incluso a las imágenes ISO de archivos de datos presentes en el disco duro. No causa errores si se aplica a un soporte en blanco escribible una sola vez.

```
$ xorriso -outdev /dev/sr0 -blank as_needed \
          -volid "ARCHIVE_2013_07_27" -joliet on -add ./for_iso --

```

En el soporte escribible non-blank xorriso añade los archivos del disco recién indicados si se usa la orden `-dev` en lugar de `-outdev`. Por supuesto, ninguna orden `-blank` debe aparecer aquí:

```
$ xorriso -dev /dev/sr0 \
          -volid "ARCHIVE_2013_07_28" -joliet on -add ./more_for_iso --

```

Para más detalles vea la [página del manual](http://www.gnu.org/software/xorriso/man_1_xorriso.html) y especialmente sus [ejemplos](http://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES).

### Defect Management en BD (Blu-ray disc)

BD-RE y el soporte BD-R formateado se escriben normalmente con *Defect Management* activado. Esta función lee los bloques escritos, durante su almacenamiento en el búfer. En caso de mala calidad de lectura de los bloques, estos se escriben de nuevo o son redirigidos a la *Spare Area* donde los datos se almacenan en bloques de repuesto.

Esta comprobación de lectura reduce la velocidad de escritura a la mitad como máximo de la velocidad nominal que puede alcanzar la unidad y el soporte BD. A veces incluso más. El uso intensivo de la «Zona de Repuesto» provoca grandes retrasos durante las operaciones de lectura. De modo que la activación de *Defect Management* no siempre es deseable.

`cdrecord` no formatea BD-R. Sin embargo, no tiene medios para evitar *Defect Management* en soportes BD-RE.

`growisofs` formatea BD-R por defecto. Esto se puede evitar mediante la opción `-use-the-force-luke=spare:none`. Sin embargo, ello no evita *Defect Management* en los soportes BD-RE.

`cdrskin`, `xorriso`, y `xorrecord` no formatean BD-R por defecto. Lo hacen con `cdrskin blank=format_if_needed`, `xorriso -format as_needed` y `xorrecord blank=format_overwrite`, respectivamente. Estos tres programas pueden desactivar *Defect Management* en BD-RE y en BD-R ya formateada con `cdrskin stream_recording=on`, `xorriso -stream_recording on` y `xorrecord stream_recording=on`, respectivamente.

### Grabar un CD de audio

Crea sus pistas de audio y guardarlas sin comprimir, como archivos WAV estéreos de 16-bit. Para convertir MP3 a WAV, compruebe que [lame](https://www.archlinux.org/packages/?name=lame) está instalado, muévase con la orden `cd` al directorio donde tiene los archivos MP3, y ejecute:

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

En el caso de que obtenga un error cuando intente grabar los archivos WAV convertidos con lame, pruebe con el decodificador [mpg123](https://www.archlinux.org/packages/?name=mpg123):

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

Nomine los archivos de audio de manera tal que las pistas aparezcan listadas en el orden deseado cuando se presenten por orden alfabético, como, por ejemplo `01.wav`, `02.wav`, `03.wav`, etc. Utilice la siguiente orden para simular la grabación de los archivos wav como un CD de audio:

```
$ wodim -dummy -v -pad speed=1 dev=/dev/sr0 -dao -swab *.wav

```

En caso de detectar errores o pistas vacías como:

```
Track 01: audio    0 MB (00:00.00) no preemp pad

```

pruebe con otro decodificador (por ejemplo, mpg123) o pruebe utilizando cdrecord del paquete [cdrtools](https://www.archlinux.org/packages/?name=cdrtools).

Tenga en cuenta que [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) también contiene una orden cdrecord, pero es solo un enlace simbólico a *wodim*. Si funcionó todo puede quitar la etiqueta dummy para grabar el CD real:

Para probar el nuevo CD de audio, utilice [MPlayer](/index.php/MPlayer "MPlayer"):

```
$ mplayer cdda://

```

### Grabar una imagen bin/cue

Para grabar una imagen bin/cue ejecute:

```
$ cdrdao write --device /dev/sr0 image.cue

```

#### TOC/CUE/BIN para discos en modalidad mixta

La imágenes ISO solo almacenan una única pista de datos. Si desea crear una imagen de un disco de modo mixto (pista de datos con varias pistas de audio), entonces necesitará crear un emparejamiento TOC/BIN:

```
$ cdrdao read-cd --read-raw --datafile IMAGE.bin --driver generic-mmc:0x20000 --device /dev/cdrom IMAGE.toc

```

Algunos programas de software solo emparejan CUE/BIN, por lo que puede hacer una hoja CUE con `toc2cue` (parte de `cdrdao`):

```
$ toc2cue IMAGE.toc IMAGE.cue

```

### Problemas con los backend de grabación

Si tiene algún problema, puede pedir asesoramiento a la lista de correo [cdwrite@other.debian.org](mailto:cdwrite@other.debian.org). O pida asesoramiento a las direcciones de correo electrónico de apoyo que suelen encontrarse al final de las páginas del manual del programa.

Comente las líneas de órdenes que ha probado, el tipo de soporte (por ejemplo, CD-R, DVD+RW, etc.), y los síntomas de los fallos (mensajes del programa, expectativas del usuario no obtenidas, etc.). Probablemente querrá respuestas sobre la versión más reciente o en desarrollo del programa afectado y la realización de pruebas de funcionamiento. Pero la respuesta bien podría ser, que la unidad no tolera el soporte en particular.

### Grabar CD/DVD/BD con una GUI

[Wikipedia - Comparativa de software de creación de discos Existen varias aplicaciones disponibles para grabar los CD en un entorno gráfico](https://en.wikipedia.org/wiki/Comparison_of_disc_authoring_software "wikipedia:Comparison of disc authoring software").

#### Programas GUI libres

*   **[AcetoneISO](https://en.wikipedia.org/wiki/AcetoneISO "wikipedia:AcetoneISO")** — Herramienta para ISO todo en uno (soporta BIN, MDF, NRG, IMG, DAA, DMG, CDI, B5I, BWI, PDI e ISO).

	[http://sourceforge.net/projects/acetoneiso](http://sourceforge.net/projects/acetoneiso) || [acetoneiso2](https://www.archlinux.org/packages/?name=acetoneiso2)

*   **BashBurn** — Frontend de menú basado en terminal para herramientas de grabación de CD/DVD.

	[http://bashburn.dose.se/](http://bashburn.dose.se/) || [bashburn](https://www.archlinux.org/packages/?name=bashburn)

*   **[Brasero](https://en.wikipedia.org/wiki/Brasero_(software) "wikipedia:Brasero (software)")** — Aplicación de grabación de discos del escritorio de GNOME que está diseñado para ser lo más simple posible. Parte de [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[http://projects.gnome.org/brasero/](http://projects.gnome.org/brasero/) || [brasero](https://www.archlinux.org/packages/?name=brasero)

*   **cdw** — Frontend ncurses para cdrecord, mkisofs, growisofs, dvd+rw-mediainfo, dvd+rw-format y xorriso.

	[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)

*   **[GnomeBaker](https://en.wikipedia.org/wiki/GnomeBaker "wikipedia:GnomeBaker")** — Aplicación de grabación completa de CD/DVD para el escritorio de GNOME.

	[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)

*   **Graveman** — Aplicación de grabación de CD/DVD basada en GTK. Es necesario configurarla para que apunte al dispositivo correcto.

	[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)

*   **[isomaster](https://en.wikipedia.org/wiki/ISO_Master "wikipedia:ISO Master")** — Editor de imágenes ISO.

	[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Aplicación de grabación de CD, rica en características y fácil de manejar, basado en KDElibs.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/X-CD-Roast "wikipedia:X-CD-Roast")** — Frontend ligero de cdrtools para escribir CD y DVD.

	[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)

*   **Xfburn** — Frontend sencillo para las bibliotecas libburnia con soporte para CD/DVD(-RW), imágenes ISO y BurnFree.

	[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

*   **xorriso-tcltk** — Frontend gráfico para grabar ISO y herramienta de grabación de xorriso para CD/DVD/BD.

	[http://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif](http://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif) || [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

#### Nero Linux

Nero Linux es una suite comercial de grabación creada por Nero para Windows - Nero AG. La mayor ventaja de Nero Linux es que tiene la interfaz similar a la versión de windows. Por lo tanto, los usuarios que migran desde windows les va a resultar fácil operar con él. La versión de Linux incluye ahora Nero Express, un asistente que dirige a los usuarios a través del proceso de grabación de CD y DVD paso a paso, con el que los usuarios de la versión de Windows estarán familiarizados. Otra novedad en la versión 4 es la gestión de defectos de discos Blu -ray, la integración de Isolinux para crear un dispositivo de arranque y el apoyo a Musepack y formatos de audio AIFF...

Nero Linux 4 se vende a £17.99 con una versión de prueba gratuita también disponible.

*   [Nero Linux 4](http://www.nero.com/enu/linux4.html)
*   Paquete [nerolinux](https://aur.archlinux.org/packages/nerolinux/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

Nero Linux ofrece algunas características, como:

*   Fácil, interfaz de usuario estilo «wizard» para guiar la grabación con Nero Linux Express 4.
*   Soporte de grabación completo para Blu-ray.
*   Soporte surning de audio CD (CD-DA), ISO 9660 (soporte Joliet), CD-text, ISOLINUX arrancable, disco multisesión, DVD-Vídeo y miniDVD, soporte doble capa DVD.
*   Grabación avanzada con Nero Burning ROM y cliente de línea de órdenes.

**Nota:** Para Nero Linux poder funcionar necesita cargar el módulo `sg` en el arranque. Ponga un archivo con nombre homónimo en `/etc/modules-load.d`: `/etc/modules-load.d/sg.config` 
```
sg

```
Hay algunas actualizaciones del módulo `sg` que hacen que no se cargue automáticamente y Nero lo necesita.

## Reproducir DVD

[DVD](https://en.wikipedia.org/wiki/es:DVD "wikipedia:es:DVD"), también conocido como Digital Versatile Disc or Digital Video Disc, es un formato de soporte de almacenamiento de disco óptico utilizado para vídeo y almacenamiento de datos.

Si desea reproducir DVD encriptados, debe instalar los paquetes libdvd*:

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

Además, debe instalar el software reproductor. Los reproductores más populares de DVD son [MPlayer](/index.php/MPlayer "MPlayer"), [xine](https://en.wikipedia.org/wiki/Xine "wikipedia:Xine") y [VLC](/index.php/VLC "VLC"). Véase el listado de [reproductores de vídeo](/index.php/List_of_Applications/Multimedia#Video_players "List of Applications/Multimedia") y las instrucciones específicas para [MPlayer](/index.php/MPlayer#DVD_playing "MPlayer").

**Sugerencia:** Los usuarios pueden necesitar pertener al [grupo](/index.php/Users_and_groups "Users and groups") `optical` para poder acceder a la unidad de DVD. Para añadir `NOMBREDEUSUARIO` al grupo `optical`, ejecute:
```
# gpasswd -a NOMBREDEUSUARIO optical

```
No se olvide reiniciar sesión para que los cambios surtan efecto. Puede ver a qué grupos actuales pertenece su usuario con la orden `groups`.

## Ripear DVD

[Ripear](https://en.wikipedia.org/wiki/es:Ripping "wikipedia:es:Ripping") es el proceso de copiar el contenido de audio o vídeo al disco duro, normalmente desde soportes extraíbles o transmisiones multimedias.

A menudo, el proceso de extracción de un DVD puede ser dividido en dos subtareas:

1.  **La extracción de datos** - Copiar los datos de audio y/o de vídeo al disco duro,
2.  [Transcodificar](https://en.wikipedia.org/wiki/es:Transcode "wikipedia:es:Transcode") - Convertir los datos extraídos a un abanico de formatos.

Algunas utilidades realizan ambas tareas, mientras que otras se centran en uno u otro aspecto:

*   **dvd-vr** — Herramienta que convierte fácilmente archivos VRO extraídos de un [DVD-VR](https://en.wikipedia.org/wiki/DVD-VR "wikipedia:DVD-VR") y los divide en archivos VOB corrientes.

	[http://www.pixelbeat.org/programs/dvd-vr/](http://www.pixelbeat.org/programs/dvd-vr/) || [dvd-vr](https://aur.archlinux.org/packages/dvd-vr/)

*   **[dvdbackup](/index.php/Dvdbackup "Dvdbackup")** — Herramienta para la extracción pura de datos pero no los transcodifica. Es útil para crear copias *exactas* de DVD encriptados en combinación con **libdvdcss** o para descifrar vídeos de otras utilidades que no pueden leer DVD encriptados.

	[http://dvdbackup.sourceforge.net/](http://dvdbackup.sourceforge.net/) || [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Completa y libre solución de audio y vídeo de Internet live para Linux/Unix, capaz de hacer un ripeado directo en cualquier formato (audio/vídeo) de una imagen de ISO de DVD-Video, basta con seleccionar la entrada como imagen ISO y continuar con las opciones deseadas. También permite downmixing, shrinking, spliting, seleccionar streams entre otras características.

	[http://ffmpeg.org/](http://ffmpeg.org/) || Véase este [artículo](/index.php/FFmpeg#Package_installation "FFmpeg")

*   **HandBrake** — Multiproceso transcodificador de vídeo, que ofrece tanto una interfaz gráfica como en línea de órdenes con muchas configuraciones preestablecidas.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **Hybrid** — Fronted multiplataforma basado en Qt útil para muchas herramientas que puede convertir casi todas la entradas a x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac contenidas en formato mp4/m2ts/mkv/webm/mov/avi, en un Blu-ray o una estructura AVCHD.

	[http://www.selur.de/](http://www.selur.de/) || [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/)

*   **[MEncoder](/index.php/MEncoder "MEncoder")** — Herramienta libre en línea de órdenes para decodificar, codificar y filtar vídeo lanzado bajo licencia GNU General Public License. Es parecido a MPlayer y puede convertir todos los formatos que MPlayer reconoce en una variedad de formatos comprimidos y sin comprimir utilizando diferentes códecs. Programas Wrapper como [h264enc](https://aur.archlinux.org/packages/h264enc/) y [undvd](https://aur.archlinux.org/packages/undvd/) pueden proporcionar una interfaz de asistencia. Están disponibles muchos [frontends](/index.php/MEncoder#GUI_frontends "MEncoder").

	[http://www.mplayerhq.hu/](http://www.mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Ripeador y codificador de vídeo/DVD para terminal/consola.

	[http://tcforge.berlios.de/](http://tcforge.berlios.de/) || [transcode](https://www.archlinux.org/packages/?name=transcode)

### dvd::rip

dvd::rip es un frontend para [transcode](https://www.archlinux.org/packages/?name=transcode), que se utiliza para extraer y transcodificar sobre la marcha.

Se deben instalar los siguientes paquetes:

*   [dvdrip](https://www.archlinux.org/packages/?name=dvdrip): frontend GTK para [transcode](https://www.archlinux.org/packages/?name=transcode), que realiza la extracción y codificación
*   [libdv](https://www.archlinux.org/packages/?name=libdv): códec para vídeo DV
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): si desea codificar sus archivos ripeados como XviD, he aquí un códec de vídeo MPEG-4 de código abierto (alternativa gratis de DivX)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/): si desea codificar sus archivos ripeados como DivX (disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"))

Las preferencias de dvd::rip están, en su mayoría, mejor documentadas/explicadas. Si necesita ayuda, consulte [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

Ripear un DVD es, a menudo, tan simple como elegir su códec preferido, seleccionar los títulos deseados y clicar sobre el botón «Rip».

## Solución de problemas

### K3b y el error sobre el locale

Cuando ejecute K3B , si aparece el siguiente mensaje:

```
System locale charset is ANSI_X3.4-1968
Your system's locale charset (i.e. the charset used to encode file names) is 
set to ANSI_X3.4-1968\. It is highly unlikely that this has been done intentionally.
Most likely the locale is not set at all. An invalid setting will result in
problems when creating data projects.Solution: To properly set the locale 
charset make sure the LC_* environment variables are set. Normally the distribution 
setup tools take care of this.

```

significará que su locale no está bien ajustado.

Para arreglarlo:

*   Quite `/etc/locale.gen`
*   Reinstale [glibc](https://www.archlinux.org/packages/?name=glibc)
*   Edite `/etc/locale.gen`, descomente todas las líneas que correspondan a su idioma ADEMÁS de la opción `en_US`, para la compatibilidad:

```
es_ES.UTF-8 UTF-8
es_ES ISO-8859-1

```

*   Reconstruya los perfiles con `locale-gen`:

 `# locale-gen` 
```
Generating locales...
en_US.UTF-8... done
en_US.ISO-8859-1... done
es_ES.UTF-8... done
es_ES.ISO-8859-1... done
Generation complete.

```

Más información [aquí](https://bbs.archlinux.org/viewtopic.php?pid=251512%29;).

### Brasero falla al encontrar discos en blanco

Brasero utiliza [gvfs](https://www.archlinux.org/packages/?name=gvfs) para gestionar grabadoras de CD/DVD. Asegurese también de que los permisos de su sesión [no están rotos](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

### Brasero falla al normalizar el CD de audio

Al intentar grabar puede pararse en el primer paso llamado Normalización.

Como solución alternativa se puede deshabilitar el plugin de normalización mediante el menú *Editar > Plugins*

### VLC: Error «... could not open the disc /dev/dvd»

Si recibe el error «vlc dvdread could not open the disc "/dev/dvd"» puede ser porque no hay ningún nodo de dispositivo `/dev/dvd` en su sistema. Udev no creará más `/dev/dvd` y, en su lugar, utilizará `/dev/sr0`. Para solucionar este problema, edite el archivo de configuración de VLC (`~/.config/vlc/vlcrc`):

```
# DVD device (string)                                                           
dvd=/dev/sr0

```

### Unidad DVD con ruidos

Si la reproducción de vídeos de DVD provoca que el sistema sea muy ruidoso, puede ser porque el disco está girando más rápido de lo que necesita. Para cambiar temporalmente la velocidad de la unidad, como usuario root, ejecute:

```
# eject -x 12 /dev/dvd

```

En ocasiones:

```
# hdparm -E12 /dev/dvd

```

Se puede utilizar cualquier velocidad que sea compatible con la unidad, o 0 para la velocidad máxima.

[Configuración de la velocidad de unidades de CD-ROM y DVD-ROM](http://hektor.umcs.lublin.pl/~mikosmul/computing/tips/cd-rom-speed.html)

### La reproducción no funciona con el equipo nuevo (unidad DVD nueva)

Si la reproducción no funciona y tiene un equipo nuevo (nueva unidad DVD) la razón podría ser que el [código de la región](https://en.wikipedia.org/wiki/es:DVD_region_code "wikipedia:es:DVD region code") no esté ajustado. Puede leer y establecer el código de la región con [regionset](https://aur.archlinux.org/packages/regionset/) disponible en [AUR](/index.php/AUR "AUR").

### Ninguno de los programas descritos puede ripear/codificar un DVD en el disco duro

Asegúrese de la región de su lector DVD está configurada correctamente, de lo contrario obtendrá un montón de errores inexplicables relacionados con CSS. Utilice [regionset](https://aur.archlinux.org/packages/regionset/) para hacerlo.

### El registro del programa GUI indica problemas con el programa del backend

Si utiliza un programa gráfico y experimenta problemas que el registro de dicho programa culpa a algún programa backend, intente reproducir el problema accediendo a los argumentos del programa backend. Si tiene éxito con la reproducción o no, puede informar de las líneas registradas y de sus propias conclusiones a los lugares mencionados en [esta sección](#Problemas_con_los_backend_de_grabaci.C3.B3n).

#### Caso especial: medium error / write error

Estos son algunos mensajes típicos de la unidad que no tolera el soporte. La única forma de resolverlo es mediante el uso de una unidad diferente o un soporte diferente. Un programa diferente difícilmente ayudará.

K3b con el backend wodim:

```
Sense Bytes: 70 00 03 00 00 00 00 12 00 00 00 00 0C 00 00 00
Sense Key: 0x3 Medium Error, Segment 0
Sense Code: 0x0C Qual 0x00 (write error) Fru 0x0

```

Brasero con el backend growisofs:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero con el backend libburn:

```
BraseroLibburn Libburn reported an error SCSI error on write(16976,16): [3 0C 00] Write error

```

## Véase también

*   RIAA and actual laws allow backup of physically obtained media under these conditions [RIAA - the law](https://www.riaa.com/physicalpiracy.php?content_selector=piracy_online_the_law).
*   [Convert any Movie to DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")
*   [Main page of the project Libburnia](http://libburnia-project.org/)
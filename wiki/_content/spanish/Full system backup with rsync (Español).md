Este artículo trata sobre como usar [rsync (Español)](/index.php/Rsync_(Espa%C3%B1ol) "Rsync (Español)") para transferir una copia de su árbol de directorios desde "/" , excluyendo algunas carpetas seleccionadas. Este enfoque es considerado mejor que el [clonado de disco](/index.php/Disk_cloning "Disk cloning") con `dd` ya que permite usar un tamaño, una tabla de particiones y un sistema de ficheros distinto, y también se considera mejor que copiar con `cp -a`, permite mayor control sobre los permisos de ficheros, sus atributos, sobre Listas de Control de Acceso y sobre atributos extendidos.[[1]](http://www.bestbits.at/acl/about.html)

Cualquier método funcionará incluso con el sistema en ejecución. Dado que suele tardar bastante tiempo, puede dedicarse a navegar por la web durante el transcurso de la copia. En el peor de los casas no se guardarán las pestañas mientras estaba navegando. Un mal menor.

## Contents

*   [1 Con un solo comando](#Con_un_solo_comando)
*   [2 Automatizado](#Automatizado)
*   [3 Requerimientos en el arranque](#Requerimientos_en_el_arranque)
    *   [3.1 Actualizar fstab](#Actualizar_fstab)
    *   [3.2 Actualizar el fichero de configuración del gestor de arranque](#Actualizar_el_fichero_de_configuraci.C3.B3n_del_gestor_de_arranque)
*   [4 Primer arranque](#Primer_arranque)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Con un solo comando

Este comando depende de que la expansión de llaves este disponible en los intérpretes de órdenes [bash](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) y [zsh](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Brace-Expansion). Cuando use otro [intérprete de órdenes](/index.php/Shell "Shell"), los patrones `--exclude` deben repetirse manualmente.

```
# rsync -aAXv --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} /* _/ruta/a/la/carpeta/de/respaldo_

```

Usando el conjunto de opciones `-aAX`, los ficheros son transferidos en modo archivo, asegurándose que los enlaces simbólicos, dispositivos, permisos y atributos de propiedad,tiempos de modificación, [ACLs](/index.php/ACL "ACL") y atributos extendidos son preservados.

La opción `--exclude` hará que aquellos ficheros que coincidan con los patrones dados sean excluidos. Los contenidos de `/dev`, `/proc`, `/sys`, `/tmp` y `/run` se excluyeron porque son inicializados al cargar el sistema (mientras que las carpetas en si mismas _no_ son creadas), `/lost+found` es específico del sistema de archivos. Entrecomillar los patrones de exclusión evitará su expansión por parte del [intérprete de ordenes](/index.php/Shell "Shell"), lo que es necesario cuando, por ejemplo, se hacen copias de seguridad por [SSH (Español)](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)").

**Nota:**

*   Si planea hacer una copia de seguridad de su sistema en algún lugar que no sea `/mnt` o `/media`, no olvide añadirlo a la lista de exclusión para evitar bucles infinitos.
*   Si hay montajes bind en su sistema, deberían ser igualmente excluidos, de manera que los contenidos en esos puntos de montajes solo sean copiados una vez.
*   Si usa un [archivo swap](/index.php/Swap_(Espa%C3%B1ol)#Archivo_swap "Swap (Español)"), asegúrese de excluirlo también.
*   Considere si desea también respaldar la carpeta `/home/`. Si contiene sus datos, serán considerablemente más cuantiosos que los del sistema. De otro modo considere excluir subdirectorios no importantes como `/home/*/.thumbnails/*`, `/home/*/.cache/mozilla/*`, `/home/*/.cache/chromium/*`, `/home/*/.local/share/Trash/*`, dependiendo del software que tenga instalado en su sistema. Si [GVFS](/index.php/GVFS "GVFS") está instalado, `/home/*/.gvfs` debe ser excluido para evitar errores de rsync.

Puede que quiera incluir algunas opciones más de [rsync](/index.php/Rsync_(Espa%C3%B1ol) "Rsync (Español)"), como las listadas a continuación (vea `man rsync` para una lista completa):

*   Si usted usa con frecuencia enlaces duros, puede que quiera añadir la opción `-H`, que viene por desactivada por defecto pues consume mucha memoria, aunque en máquinas modernas no debería suponer un problema. Hay muchos enlaces duros en la carpeta `/usr/`, lo cual ahorra espacio en disco.
*   Puede que quiera añadir a rsync la opción `--delete` si lo ejecuta reiteradamente sobre la misma carpeta de respaldo.
*   Si usa archivos dispersos, como disco virtuales, imágenes de [Docker](/index.php/Docker "Docker") y similares, debería añadir la opción `-S`.
*   La opción `--numeric-ids` deshabilitará el mapeado de nombres de usuarios y grupos, el número de grupo y los IDs de usuarios serán transferidos en su lugar. Esto es útil cuando se respalda mediante [SSH (Español)](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)") o cuando se use un sistema vivo para respaldar diferente discos de sistema.

## Automatizado

Vea [Backup_programs#Rsync-type_backups](/index.php/Backup_programs#Rsync-type_backups "Backup programs").

## Requerimientos en el arranque

Tener un respaldo arrancable puede ser útil en caso de que el sistema de ficheros se corrompa o si una actualización rompe el sistema. El respaldo puede usarse también como sistema de pruebas, con el repo [testing] habilitado, etc. Si transfirió el sistema a una partición o disco distinto y quiere arrancarlo, el proceso es tan simple como actualizar el fichero `/etc/fstab` del respaldo y el fichero de configuración del gestor de arranque.

### Actualizar fstab

Sin reiniciar, edite el fichero [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") del respaldo para reflejar los cambios:

 `/ruta/al/respaldo/etc/fstab` 

```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

<font color="#888888">_/dev/sda1    /boot         ext2      defaults                 0   2
/dev/sda5    none          swap      defaults                 0   0
/dev/sda6    /             ext4      defaults                 0   1
/dev/sda7    /home         ext4      defaults                 0   2_</font>
```

Como rsync ha hecho una copia recursiva del sistema de ficheros raíz _entera_, todos los puntos de montaje `sda` son problemáticos y arrancar el respaldo fallará. En este ejemplo, todas las entradas conflictivas son reemplazadas por una sola:

 `/ruta/al/respaldo/etc/fstab` 

```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

/dev/**sdb1**    /             ext4      defaults                 0   1
```

Recuerde usar el nombre de dispositivo y tipo de sistema de archivos correctos.

### Actualizar el fichero de configuración del gestor de arranque

Esta sección asume que el respaldo de su sistema se encuentra en otra partición o disco, que su gestor de arranque funciona correctamente, y que quiere arrancar desde su respaldo.

Para [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), todo lo que necesita es duplicar la entrada actual, pero modificando el disco y/o partición donde se encuentre el respaldo.

**Sugerencia:** En vez de editar `syslinux.cfg`, puede editar temporalmente el menú durante el arranque. Cuando aparezca el menú, pulse la tecla `Tab` y cambie las entradas pertinentes. Las particiones se cuentan en base 1, los disco se cuentan en base 0.

Para [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), se recomienda que [regenere el fichero de configuración principal](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuraci.C3.B3n_principal "GRUB (Español)").

Verifique además la nueva entrada del menú en `/boot/grub/grub.cfg`. Asegúrese que el UUID corresponde a la nueva partición, de otra manera aún podría arrancar el antiguo sistema. Encuentre el UUID de la partición de la siguiente forma:

```
# lsblk -no NAME,UUID /dev/sdb3

```

donde debe sustituir /dev/sdb3 por la partición en su caso. Para listar los UUID de las particiones que GRUB puede arrancar, use grep:

```
# grep UUID= /boot/grub/grub.cfg

```

Si el que encontró con lsblk no lo encuentra con grep, entonces grub-mkconfig no funcionó correctamente. Probablemente, tendrá que hacer un [chroot](/index.php/Change_root "Change root") con el sistema de archivos duplicado y desde dentro usar [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Por ejemplo, si había usado rsync para duplicar el sistema en /dev/sdb3 entonces haga un chroot y use mkinitcpio de la siguiente forma:

```
# mkdir /mnt/arch
# mount /dev/sdb3 /mnt/arch
# cd /mnt/arch
# mount -t proc proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/
# chroot /mnt/arch /bin/bash
# mkinitcpio -p linux

```

Al salir, regenere grub.cfg y verifique que el nuevo UUID está incluido.

## Primer arranque

Reinicie el ordenador y seleccione la entrada correcta en el gestor de arranque. Esto cargará el sistema por primera vez. Todos los periféricos deberían ser detectados y todos las carpetas vacías en `/` serán inicializadas.

Ahora puede editar `/etc/fstab` para añadir las particiones y puntos de montajes eliminados anteriormente.

Si transfirió los datos de un HDD a un SDD (disco de estado solido), no olvide activar el TRIM. Considere además usar disco HDD y puntos de montajes tmpfs para reducir el desgaste del disco SSD - véase [Montando /tmp en RAM](/index.php/Maximizing_performance_(Espa%C3%B1ol)#Montando_.2Ftmp_en_RAM "Maximizing performance (Español)") y [Consejo para minimizar las L/E en discos SSD](/index.php/Solid_State_Drives#Tips_for_Minimizing_SSD_Read.2FWrites "Solid State Drives").

**Nota:** Puede que tenga que reiniciar para que todos los servicios y demonios funcionen correctamente. En mi caso, pulseaudio no inicializaba por un error al cargar un modulo. Reinicié el servicio dbus.service para hacerlo funcionar.

## Véase también

*   [Howto – Copias de seguridad de instantáneas locales y remotas usando rsync con enlaces duros](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) Incluye de-duplicación de archivos con enlaces duros, Firma de integridad con MD5, protección contra 'chattr', reglas de filtrado,cuota de disco, políticas de retención con distribución exponencial (rotación de respaldos priorizando las copias recientes sobre las más antiguas)
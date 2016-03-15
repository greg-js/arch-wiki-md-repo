**ext4** constituye la siguiente etapa en la evolución del sistema de archivos (o ficheros; en inglés, *filesystem*) denominado **extended**, que indudablemente se ha convertido en uno de los más utilizados por los usuarios de Linux.

Es importante destacar que las modificaciones introducidas por ext4 han sido más numerosas y significativas en comparación a las realizadas por su antecesor sobre ext2\. En otras palabras, ext4 presenta modificaciones en las estructuras internas del mismo sistema (de ficheros), como sucede en el caso de aquellas destinadas a la preservación de los datos propios de cada fichero, mientras que ext3 se caracterizó principalmente por haber introducido la funcionalidad *journaling*, inexistente en ext2.

En síntesis, el resultado ha sido un sistema mejor diseñado, más eficiente y confiable, y por supuesto con mayores prestaciones.

**Nota:** Sírvase consultar el texto original en [inglés](http://kernelnewbies.org/Ext4), mas tenga en cuenta que la presente traducción dista de ser literal.

## Contents

*   [1 Creación de Particiones ext4](#Creaci.C3.B3n_de_Particiones_ext4)
*   [2 Migrando de ext3](#Migrando_de_ext3)
    *   [2.1 Montando Particiones como ext4](#Montando_Particiones_como_ext4)
        *   [2.1.1 Prólogo](#Pr.C3.B3logo)
        *   [2.1.2 Procedimiento](#Procedimiento)
    *   [2.2 Convirtiendo Particiones en ext3 a ext4](#Convirtiendo_Particiones_en_ext3_a_ext4)
        *   [2.2.1 Prólogo](#Pr.C3.B3logo_2)
        *   [2.2.2 Requisitos](#Requisitos)
        *   [2.2.3 Procedimiento](#Procedimiento_2)
        *   [2.2.4 Migrando Ficheros a Extents](#Migrando_Ficheros_a_Extents)
*   [3 Solución de Problemas](#Soluci.C3.B3n_de_Problemas)
    *   [3.1 Kernel Panic](#Kernel_Panic)
    *   [3.2 GRUB Error 13](#GRUB_Error_13)
    *   [3.3 Corrupción de Datos](#Corrupci.C3.B3n_de_Datos)
    *   [3.4 Incrementando el Desempeño](#Incrementando_el_Desempe.C3.B1o)

## Creación de Particiones ext4

Aquí le presentamos un método a utilizar para crear particiones en ext4\. Recuerde que puede modificarlo de acuerdo con sus necesidades:

1.  Actualice su sistema: `pacman -Syu`
2.  Dé formato a la partición que desee: `mkfs.ext4 /dev/<partición>` (Reemplace */dev/<partición>* por la ruta de la partición deseada: por ejemplo, */dev/sda1*).
3.  Monte la partición: `mount -text4 /dev/<partición>` (Utilice aquí el mismo valor para */dev/<partición>* que utilizó en el comando anterior).
4.  Añada una entrada a `/etc/fstab` especificando *type* como ext4.

**Nota:** Necesitará realizar el último paso únicamente si desea que la partición sea montada automáticamente cada vez que se inicie el sistema.

**Sugerencia:** Vea el manual (*man page*) de mkfs.ext4 para más información.
Puede asimismo ver o editar el archivo `/etc/mke2fs.conf` en caso que desee modificar las opciones por defecto.

## Migrando de ext3

Existen dos métodos para migrar particiones de ext3 a ext4:

*   montando las particiones en ext3 como particiones de tipo ext4 sin realizar conversión alguna (modo de compatibilidad).
*   conviritiendo la partición a ext4 (mayor desempeño).

### Montando Particiones como ext4

* * *

#### Prólogo

En lugar de convertir la partición completamente a ext4, es posible montarla como si su formato fuera ext4. No obstante, tenga antes en cuenta los siguientes puntos a favor y en contra.

**A Favor:**

*   Compatibilidad: El sistema puede continuar montándose como ext3, permitiéndoles a los usuarios continuar trabajando sobre el mismo desde otras distribuciones de Linux o desde otros sistemas operativos sin soporte directo (por ejemplo, desde Windows, instalando previamente los controladores para ext3).

*   Desempeño mejorado. Por supuesto, quizá no tanto como en el caso de una partición en ext4\. (Véase, en inglés: [ext4](http://kernelnewbies.org/Ext4)).

**En Contra:**

*   Funcionalidades propias del formato ext4 no podrán ser aprovechadas, dado que la partición continúa en ext3.

**Nota:** Exceptuando su relativa juventud, lo que puede ocasionar que se considere a ext4 riesgoso, **no existe mayor riesgo o inconveniente en la aplicación del presente método**

#### Procedimiento

1.  Edite `/etc/fstab` cambiando el tipo (*type*) de la partición en cuestión a ext4\. Repita el proceso para todas las particiones que desee montar como ext4.
2.  Vuelva a montar las particiones afectadas (recuerde: `mount -a` montará todas las particiones especificadas en `/etc/fstab`).

### Convirtiendo Particiones en ext3 a ext4

* * *

#### Prólogo

Para experimentar los beneficios que provee ext4, deberá inexorablemente convertir las particiones a este nuevo formato.

**Advertencia:** Recuerde que el proceso de conversión es **irreversible**. Realice previamente una copia de seguridad de sus datos.

Como sugerimos anteriormente, tenga en cuenta además los siguientes puntos a favor y en contra:

**A Favor:**

*   Desempeño claramente mejorado y nuevas prestaciones disponibles. (Véase, en inglés: [ext4](http://kernelnewbies.org/Ext4)).

**En Contra:**

*   La partición no podrá leerse o escribirse utilizando controladores de ext3, (tenga en cuenta que aún no existe un controlador de ext4 para Windows).

*   El proceso es **irreversible**: las particiones en ext4 no podrán *degradarse* (*downgrade*) a ext3.

#### Requisitos

Si desea convertir su partición */boot* a ext4, deberá instalar asimismo `grub (0.97 o superior)`

**Nota:** `grub (0.97 o superior)` requiere un parche para ext4, el mismo se encuentra actualmente incluido por defecto en el paquete *GRUB* de Arch (si bien esto sucede actualmente, es altamente probable que no cambie). De lo contrario, necesitará [GRUB2](/index.php/GRUB2 "GRUB2") para poder arrancar el sistema desde una partición en ext4.

**Advertencia:** GRUB no soporta "oficialmente" el arranque del sistema desde una partición en ext4, y [GRUB2](/index.php/GRUB2 "GRUB2") aún se encuentra en desarrollo. Si bien GRUB funciona actualmente, la opción más "segura" es arrancar desde una partición cuyo formato sea ext2 o ext3\. **CONSIDÉRESE ADVERTIDO**.

**Nota:** Instalar Arch utilizando la última *release* (2009.02) es altamente recomendado. Otras imágenes más antiguas (anteriores a 2008.06) acarrean versiones anteriores del *software* requerido (por ejemplo, de `e2fsprogs`); no obstante, es sencillo actualizar el *software* con `pacman -Sy` y luego `pacman -S e2fsprogs` desde la línea de comando luego de instalar Arch y luego de configurar la red. Una alternativa es utilizar [SystemRescueCD (1.1.4 o superior)](http://www.sysresccd.org/Download), que contiene las versiones apropiadas, siendo además un práctico CD para tener a mano.

**Sugerencia:** Puede asimismo instalar Arch desde Internet, obteniendo de esa forma las últimas versiones disponibles de cada *software* requerido.

**Advertencia:** Recientemente se ha discutido en los foros oficiales de Arch acerca de la peligrosidad que subyace al uso de `pacman -Sy <paquete>` para instalar paquetes, ya que la actualización previa de las bases de datos en conjunción a la instalación de un paquete puede generar inconsistencias en las dependencias de otros ya instalados. Consulte en los foros para más información.

#### Procedimiento

Estas instrucciones han sido adaptadas de [ext4 Wiki](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) y [Foros de Arch (Hilo #61602)](https://bbs.archlinux.org/viewtopic.php?id=61602). Fueron examinadas y verificadas por el autor hasta el 16 de Enero de 2009.

*   **ACTUALICE SU SISTEMA**: Haga una actualización global de su sistema para asegurarse de que su *software* esté al día: `pacman -Syu`.

*   **REALICE UN BACK-UP**: Haga una copia de seguridad de las particiones que convertirá a ext4.
    Aunque ext4 se considere "estable" para el uso general, es aún relativamente jóven y no ha sido evaluado exhaustivamente. Además, el proceso de conversión se ha evaluado únicamente en un entorno (en un sistema) de simple configuración; es imposible evaluar este proceso en todas las posibles configuraciones que los usuarios pudieran tener. (Véase la siguiente entrada, en inglés: [Back-Up Programs](/index.php/Backup_programs "Backup programs")).

*   Edite `/etc/fstab` modificando el tipo (*type*) a ext4 para cada partición que desee convertir.

**Advertencia:** ext4 es *backwards-compatible* (compatible *hacia atrás*) con ext3 hasta tanto se hayan habilitado las nuevas funcionalidades (como *extent*). Si posee particiones compartidas actualmente con otro sistema operativo (SO; OS en inglés) que aún no puede leer particiones en ext4, podrá montarlas como ext4 en Arch sin modificarlas (véase el método anterior). Tenga en consideración que los beneficios serán menores si las mismas no son eventualmente convertidas a ext4.
También tenga en cuenta que luego del siguiente paso **la partición en cuestión poseerá un nuevo formato: ext4**.

*   El proceso de conversión con `e2fsprogs` deberá realizarse cuando la partición no se encuentre montada. Si desea convertir la partición *root* (/), hágalo desde otra distribución o desde algún medio que le permita acceder a una línea de comando, (véanse los requisitos previos detallados anteriormente).

**Nota:** Aunque se utilice en este texto el término *partición* para hacer referencia a ciertos directorios específicos (por ejemplo, */boot*), no es en absoluto necesario que los mismos se encuentren vinculados a *particiones dedicadas*.

*   Arranque el sistema desde el que trabajará (si fuera necesario).
*   Por cada partición a convertir:
    *   Asegúrese de que la partición **NO** esté montada.
    *   Ejecute: `tune2fs -O extents,uninit_bg,dir_index /dev/<partición>` (donde */dev/<partición>* es la ruta de la partición que desea convertir).
    *   Ejecute: `fsck -fp /dev/<partición>`

**Nota:** Usted **DEBE** ejecutar *fsck* en el sistema de ficheros, de lo contrario **quedará ilegible**. Esta ejecución de *fsck* es necesaria para volver el sistema a un estado consistente. **Se encontrarán errores en las checksums (sumas de verifiación) de los descriptores de grupo**, esto es esperable. La opción "-f" le solicita a *fsck* que fuerce la verifiación incluso si el sistema parece estar limpio. Por su parte, "-p" solicita a *fsck* que **repare automáticamente** (de lo contrario, *fsck* le pedirá instrucciones por cada error encontrado).

*   Reinicie Arch.

**Advertencia:** Si convirtió la partición *root* (/), es posible que se produzca un *kernel panic* al intentar iniciar el sistema. Si sucediere, simplemente reinicie nuevamente el sistema, arranque desde *fallback* y vuelva a crear el *ramdisk* inicial con `mkinitcpio -p linux`

#### Migrando Ficheros a Extents

Aunque la partición ya se ha convertido a ext4, los ficheros que fueron escritos previamente aún no comenzaron a aprovechar las ventajas de la nueva funcionalidad *extents* que el mismo provee. Al modificar esta situación, se mejorará el desempeño del sistema, particularmente con los ficheros grandes, como así se reducirá la fragmentación del mismo y el tiempo de verificación.

En conclusión, para aprovechar ext4 completamente, todos los ficheros deberán ser reescritos. (Una utilidad llamada `e4defrag` está siendo desarrollada para encargarse de esta tarea, sin embargo, aún no está lista para ser utilizada).

Afortunadamente, es posible utilizar todavía el programa *chattr* (*change attribute*), que le ordenará al kernel reescribir los ficheros utilizando *extents*. Si bien es posible ejecutar el comando en todos los ficheros y directorios de una partición (por ejemplo, si */home* estuviera en una partición separada):

```
find /home -xdev -type f -print0 | xargs -0 chattr +e
find /home -xdev -type d -print0 | xargs -0 chattr +e

```

Se recomienda verificar el funcionamiento de los comandos antedichos en un pequeño grupo de ficheros previamente, a fin de evitar poner en riesgo la totalidad de los mismos.

Quizá también resulte útil verificar el sistema de ficheros luego de realizar la conversión (el manual, la *man page*, de *fsck* puede ayudarle, consúltela).

Con el comando *lsattr* (*list attributes*) podrá cotejar que los ficheros estén efectivamente utilizando *extents*. La letra **e** deberá aparecer en la lista de atributos de cada archivo.

## Solución de Problemas

### Kernel Panic

<u>Problema</u>: *kernel panic* luego de realizar la conversión a ext4 de la partición *root* (/).

<u>Causa</u>: el *ramdisk* inicial detectaba el formato de la partición como *ext4dev* en lugar de ext4.

<u>Solución</u>: Arrancar el sistema utilizando la imagen *fallback* y recrear el *ramdisk* inicial. `# mkinitcpio -p linux` 

Durante el proceso de creación, `mkinitcpio` correctamente detectó e incluyó los módulos de ext4 en el *ramkdisk* inicial.

### GRUB Error 13

<u>Problema</u>: Al intentar arrancar el sistema desde una partición (normalmente montada en */boot*) convertida a ext4, GRUB notifica: `Error 13: Invalid or unsupported executable format` 

<u>Solución</u>:

*   Iniciar desde el medio de instalación de Arch el sistema *live*.
*   Ejecutar los comandos en la siguiente lista, preferentemente respetando el orden de los mismos:

```
# mkdir /mnt/arch
# mount -t ext4 /dev/<partición> /mnt/arch
# mount -t proc proc /mnt/arch/proc
# mount -t sysfs sys /mnt/arch/sys
# mount -o bind /dev /mnt/arch/dev
# chroot /mnt/arch /bin/bash

```

Si */boot* se encuentra en una partición aislada (dedicada), entonces también deberá montarse:

```
# mount -t ext4 /dev/<partición> /boot

```

Finalmente, el siguiente comando deberá solucionar el problema, (¿sabe alguien por qué?):

```
# grub-install --recheck /dev/<partición>

```

**Nota:** Reemplace cada ocurrencia de */dev/<partición>* por la ruta congruente con el comando a ejecutar.

### Corrupción de Datos

Algunos adoptantes iniciales de ext4 han visto sus datos corrompidos después de un *hard reboot* (reinicio desde la máquina y no desde el sistema). Por favor, vea (en inglés) [Ext4 data loss; explanations and workarounds](http://www.h-online.com/open/Ext4-data-loss-explanations-and-workarounds--/news/112892) para más información.

Desde el kernel 2.6.30, ext4 se considera seguro (o más seguro). Diversos parches contribuyeron a incrementar su robustez, tal vez a costa del rendimiento.

Una nueva opción puede ser utilizada (`auto_da_alloc`) para desactivar este comportamiento. Para más información, vea (en inglés) [Linux 2 6 30 - Filesystems performance improvements](http://kernelnewbies.org/Linux_2_6_30#head-329ba44b44a7f58c98ae22b8f2730418cdd6630d).

Para versiones del kernel menores a 2.6.30, considere agregar `rootflags=data=ordered=0` a la línea `kernel` en el archivo `menu.lst` de GRUB como una medida preventiva.

### Incrementando el Desempeño

Desde el kernel 2.6.30, el desempeño de ext4 ha decrecido debido a cambios destinados a incrementar la integridad de los datos y su preservación (véase, en inglés: [[1]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1)). Los usuarios ahora pueden incrementar el desempeño especificando la opción `nobarrier` al montar la partición; no obstante, eliminar las barreras **puede constituir un peligro** que resulte en la pérdida de datos o en la corrupción de los mismos luego de problemas de índole energética. Para desactivar las barreras automáticamente, añada la opción `barrier=0` a la lista de la partición deseada en `/etc/fstab`. Por ejemplo:

 `/dev/sda5  /  ext4  noatime,barrier=0  0  1`
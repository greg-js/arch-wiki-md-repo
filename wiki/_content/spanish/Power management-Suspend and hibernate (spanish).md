**Estado de la traducción**
Este artículo es una traducción de [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"), revisada por última vez el **2019-04-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Power_management/Suspend_and_hibernate&diff=0&oldid=568198) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Uswsusp](/index.php/Uswsusp "Uswsusp")
*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [Power management (Español)](/index.php/Power_management_(Espa%C3%B1ol) "Power management (Español)")

Actualmente hay tres métodos de suspensión disponibles: **suspender en RAM** (llamado solo **suspender**), **suspender en disco** (conocido como **hibernar**) y **suspensión híbrida** (a veces llamado **suspender a ambos**):

*   **Suspender en RAM**: Este método corta la corriente en muchas partes del sistema excepto de la RAM, que es necesaria para restaurar el estado de la máquina, de ahí el gran ahorro energético. Es recomendable para los portátiles que entre en este modo automáticamente cuando el ordenador esta consumiendo baterías y la pantalla está cerrada (o el usuario está inactivo por un periodo de tiempo).

*   **Suspender en disco**: Este método guarda el estado de la máquina en [espacio swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") y apaga completamente la máquina. Cuando la máquina se enciende el estado se restaura. Hasta entonces no hay consumo de energía.

*   **Suspensión híbrida**: Este método guarda el estado en el espacio swap, pero no apaga la máquina. En su lugar, invoca un suspender en RAM. De esta forma si la batería no se agota, el sistema puede continuar desde RAM. Si se agota, el sistema puede continuar desde el disco, que es más lento que continuar desde RAM, pero el estado de la máquina no se pierde.

Hay varias interfaces de bajo nivel (backends) que proporcionan una funcionalidad básica y varias interfaces de alto nivel que proporcionan retoques para encargarse de los controladores de hardware problemáticos/módulos kernel (p.ej. reinicialización de la tarjeta de vídeo).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Interfaces de bajo nivel](#Interfaces_de_bajo_nivel)
    *   [1.1 Núcleo (swsusp)](#Núcleo_(swsusp))
    *   [1.2 Uswsusp](#Uswsusp)
*   [2 Interfaces de alto nivel](#Interfaces_de_alto_nivel)
    *   [2.1 Systemd](#Systemd)
*   [3 Hibernar](#Hibernar)
    *   [3.1 Sobre el tamaño de la partición/archivo swap](#Sobre_el_tamaño_de_la_partición/archivo_swap)
    *   [3.2 Parámetros necesarios del kernel](#Parámetros_necesarios_del_kernel)
        *   [3.2.1 Hibernar en un archivo swap](#Hibernar_en_un_archivo_swap)
    *   [3.3 Configurar initramfs](#Configurar_initramfs)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 ACPI_OS_NAME](#ACPI_OS_NAME)
    *   [4.2 Usuarios VAIO](#Usuarios_VAIO)
    *   [4.3 Suspender/hibernar no funciona o no es consistente](#Suspender/hibernar_no_funciona_o_no_es_consistente)
    *   [4.4 Wake-on-LAN](#Wake-on-LAN)
    *   [4.5 Despertar instantáneo desde la suspensión](#Despertar_instantáneo_desde_la_suspensión)
    *   [4.6 El sistema no se apaga cuando hiberna](#El_sistema_no_se_apaga_cuando_hiberna)

## Interfaces de bajo nivel

Aunque estas interfaces se pueden usar directamente es aconsejable que se utilice alguna [interfaz de alto nivel](#Interfaces_de_alto_nivel) para suspender/hibernar. Utilizar interfaces de bajo nivel es significativamente más rápido que utilizar las interfaces de alto nivel, ya que ejecutar los pre y post hooks lleva tiempo, pero estos hooks pueden establecer apropiadamente el reloj hardware, restaurar las redes inalámbricas, etc.

### Núcleo (swsusp)

Lo más directo es informar directamente al núcleo (kernel) el código de suspensión del software para cambiar a un estado de suspensión (swsusp); el método exacto y el estado depende del nivel que soporta el hardware. En los núcleos modernos, el principal mecanismo para lanzar esta suspensión es escribir las apropiadas instrucciones en `/sys/power/state`.

vea la [documentación del kernel (en inglés)](https://www.kernel.org/doc/Documentation/power/states.txt) para más detalles.

### Uswsusp

La suspensión de software de espacio de usuario ('uswsusp') es un envoltorio del mecanismo de suspensión a RAM del núcleo que realiza algunas manipulaciones del adaptador gráfico desde el espacio de usuario antes de suspender y después de reanudar. Vea el articulo del manual [Uswsusp](/index.php/Uswsusp "Uswsusp").

## Interfaces de alto nivel

El objetivo de estos paquetes es proporcionar script/binarios que puedan invocar y realizar la suspensión/hibernación. En realidad los enlaces a los botones de encendido o a los clic en un menú o a los eventos de la tapa de un portátil se les deja a otras herramientas. Para suspender/hibernar automáticamente en ciertos eventos de energía, como el cierre de la tapa del ordenador o bajo porcentaje de batería puede que estés buscando ejecutar [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)").

### Systemd

[Systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") proporciona de forma nativa comandos para suspender, hibernar y suspender de forma híbrida, vea [administración de energía con systemd (en inglés)](/index.php/Power_management#Power_management_with_systemd "Power management") para más detalles. Esta es la interfaz por defecto usada en Arch Linux.

Vea [sleep hooks](/index.php/Power_management_(Espa%C3%B1ol)#Sleep_hooks "Power management (Español)") como información adicional para configurar los hook de suspensión/hibernación. Vea también [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1), [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8), y [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7).

## Hibernar

Para utilizar la hibernación, necesita crear la partición o el archivo [swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"). Necesitará que el kernel apunte a su swap utilizando el parámetro del kernel `resume=`, configurado a través del gestor de arranque. También necesitará [configurar los initramfs](#Configurar_initramfs). Esto le dice al kernel que se reanude desde un espacio inicial específico del swap. Abajo se describen en detalle estos tres pasos.

**Nota:** Vea [soporte de suspensión en disco](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol)#Con_soporte_para_suspensión_en_disco "Dm-crypt/Swap encryption (Español)") cuando utilice el [cifrado](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)").

### Sobre el tamaño de la partición/archivo swap

Incluso si su partición swap es más pequeña que la RAM, tiene grandes oportunidades de hibernar correctamente. Acorde con la Even if your swap partition is smaller than RAM, you still have a big chance of hibernating successfully. According to [documentación del kernel (en inglés)](https://www.kernel.org/doc/Documentation/power/interface.txt):

	*`/sys/power/image_size` controla el tamaño de la imagen creada para el mecanismo suspender en disco. Se puede escribir representando un número entero no negativo que se utilizará como límite de la imagen creada, en bytes. El mecanismo suspender en disco se asegurará que la imagen no exceda ese número. Sin embargo, si es imposible, intentará suspender de cualquier forma utilizando la imagen más pequeña posible. Particularmente si en el archivo está escrito un "0" la imagen de suspensión sera lo más pequeña posible. Si se le ese archivo mostrará el actual límite de la imagen, que se establece 2/5 de la RAM disponible por defecto.*

Puede disminuir el valor de `/sys/power/image_size` para hacer que la imagen sea lo más pequeña que sea posible (para particiones swap pequeñas) o aumentar para acelerar el proceso de hibernación.

Vea [archivos temporales de systemd](/index.php/Systemd_(Espa%C3%B1ol)#Archivos_temporales "Systemd (Español)") para hacer este cambio permanente.

### Parámetros necesarios del kernel

El parámetro del kernel `resume=*swap_partition*` se tiene que usar. Ya sea con el nombre que le asigna el kernel a la partición o su [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") se puede utilizar como `*partición swap*`. Por ejemplo:

*   `resume=/dev/sda1`
*   `resume=UUID=4209c845-f495-4c43-8a03-5363dd433153`
*   `resume=/dev/archVolumeGroup/archLogicVolume` -- Ejemplo utilizando LVM

Generalmente, el método de nombrar utilizado por el parámetro `resume` debe de ser el mismo utilizado por el parámetro `root`.

La configuración depende del [gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)") utilizado, para más detalles vea [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").

#### Hibernar en un archivo swap

**Advertencia:** [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") en el kernel Linux antes de la versión 5.0 no soporta archivos swap. Incumplir esta advertencia puede causar que se corrompa el sistema de archivos. Mientras que el archivo swap se utilice en Btrfs cuando está montado a través de un dispositivo loop hace que se degrade severamente el rendimiento de la swap.

Utilizar un archivo swap en vez de una partición swap requiere un parámetro adicional del kernel `resume_offset=*compensación_del_archivo_swap*`.

el valor de `*compensación_del_archivo_swap*` se puede obtener ejecutando `filefrag -v *archivo_swap*`, la salida de este comando esta en un formato de tabla y el valor requerido se localiza en la primera fila de la columna `physical_offset`. Por ejemplo:

 `# filefrag -v /swapfile` 
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...

```

En el ejemplo el valor de la `*compensación_del_archivo_swap*` es el primer `38912` con dos puntos.

**Sugerencia:** El siguiente comando se puede utilizar para identificar la `*compensación_del_archivo_swap*`: `filefrag -v /swapfile | awk '{ if($1=="0:"){print $4} }'`.

**Nota:**

*   Antes de hibernar por primera vez es necesario reiniciar para activar la característica.
*   el valor de `*compensación_del_archivo_swap*` se puede obtener también ejecutando `swap-offset *archivo_swap*`. El binario *swap-offset* lo proporciona el conjunto de herramientas [uswsusp (en inglés)](/index.php/Uswsusp "Uswsusp"). Si utiliza este método después se tiene que proporcionar estos dos parámetros en `/etc/suspend.conf` a través de `resume device` y `resume offset`. No se necesita reiniciar en este caso.

**Sugerencia:** Puede que quiera disminuir el [swappiness](/index.php/Swap_(Espa%C3%B1ol)#Swappiness "Swap (Español)") de su archivo swap si el único objetivo es ser capaz de hibernar y no expandir la RAM.

### Configurar initramfs

*   Cuando se utiliza el hook `base` en el [initramfs](/index.php/Arch_boot_process_(Espa%C3%B1ol)#initramfs "Arch boot process (Español)"), que está por defecto, es necesario el hook `resume` en `/etc/mkinitcpio.conf`. La partición swap está referenciada, ya sea por etiqueta o por UUID, a un nodo del dispositivo udev, por tanto el hook `resume` debe de ir *después* del hook `udev`. Este ejemplo se ha realizado partiendo de la configuración por defecto:

	 `HOOKS=(base udev autodetect keyboard modconf block filesystems **resume** fsck)` 

	Recuerde [regenerar los initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)") para que los cambios surtan efecto.

**Nota:** Los usuarios [LVM](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") deben añadir el hook `resume` después de `lvm2`.

*   Cuando se utiliza el hook `systemd` en el initramfs ya se proporciona el mecanismo de reanudación y no se necesita añadir nuevos hooks.

## Solución de problemas

### ACPI_OS_NAME

Puede que quiera retocar su **tabla DSDT** para hacer que funcione. Vea el artículo [DSDT (en inglés)](/index.php/DSDT "DSDT").

### Usuarios VAIO

Añada el [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `acpi_sleep=nonvs` a su gestor de arranque.

### Suspender/hibernar no funciona o no es consistente

Ha habido muchos informes sobre que la pantalla se vuelve negra sin ver los errores fácilmente o poder hacer algo cuando se va a suspender/hibernar y vuelve atrás. Estos problemas se han visto tanto en portátiles como en escritorio. Esta es una solución no oficial pero cambiar a un kernel más antiguo, especialmente un kernel-LTS, resolverá probablemente este problema.

También puede surgir el problema cuando se utiliza un temporizador de vigilancia hardware (desactivado por defecto, vea `RuntimeWatchdogSec=` en [systemd-system.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-system.conf.5#OPCIONES)). Un temporizador con errores puede reiniciar el ordenador antes de que se cree la imagen de hibernación.

A veces la pantalla se vuelve negra en el inicio del dispositivo desde dentro del initramfs. Eliminar cualquier módulo que puede que tenga en [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#MÓDULOS "Mkinitcpio (Español)") y reconstruir los initramfs, posiblemente puede solucionar este error, especialmente con controladores gráficos para [iniciar de forma anticipada KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Iniciar_de_forma_anticipada_KMS "Kernel mode setting (Español)"). Iniciar tales dispositivos antes de reanudar puede causar inconsistencias que evitan reanudar desde la hibernación. Esto no afecta a reanudar desde RAM. También compruebe el artículo del blog [mejores prácticas para depurar errores de suspensión](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues).

Para los controladores gráficos de Intel, activar KMS anticipado puede ayudar a solucionar el problema de la pantalla en negro. Vea [iniciar de forma anticipada KMS](/index.php/Kernel_mode_setting_(Espa%C3%B1ol)#Iniciar_de_forma_anticipada_KMS "Kernel mode setting (Español)") para más detalles.

Después de actualizar al kernel 4.15.3 puede fallar al reanudar con un cursor estático (sin parpadear) en la pantalla negra. After upgrading to kernel 4.15.3, resume may fail with a static (non-blinking) cursor on a black screen. Poner en el módulo `nvidiafb` en la [lista negra](/index.php/Kernel_module_(Espa%C3%B1ol)#Lista_negra "Kernel module (Español)") puede ayudar. [[1]](https://bbs.archlinux.org/viewtopic.php?id=234646)

### Wake-on-LAN

Si [wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") está activado la tarjeta de red consumirá energía incluso si el ordenador está hibernado.

### Despertar instantáneo desde la suspensión

Se informa que para algunos sistemas Intel Haswell con el chipset LynxPoint y LynxPoint-LP se despiertan de forma instantánea después de suspender. Estos enlazan de forma errónea a las implementaciones ACPI BIOS y como lo interpreta el modulo `xhci_hcd` durante el inicio. Como un trabajo por turnos los sistemas afectados y reportados se añaden a una lista negra (llamada `XHCI_SPURIOUS_WAKEUP`) en el núcleo caso por caso. [[2]](https://bugzilla.kernel.org/show_bug.cgi?id=66171#c6)

Puede que se despierte de forma instantánea debido a un dispositivo USB que está conectado durante la suspensión y los disparadores ACPI para despertar el dispositivo se activan. Una solución viable para dichos sistemas es desactivar los disparadores para despertar el dispositivo si no están aún en la lista negra. A continuación un ejemplo para desactivar el despertar a través del USB. [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1575617)

Para ver la configuración actual:

 `$ cat /proc/acpi/wakeup` 
```
Device  S-state   Status   Sysfs node
...
EHC1      S3    *enabled  pci:0000:00:1d.0
EHC2      S3    *enabled  pci:0000:00:1a.0
XHC       S3    *enabled  pci:0000:00:14.0
...

```

Los dispositivos relevantes son `EHC1`, `EHC2` y `XHC` (para USB 3.0). Para cambiar su estado tiene que repetir el nombre del dispositivo al archivo como root.

```
# echo EHC1 > /proc/acpi/wakeup
# echo EHC2 > /proc/acpi/wakeup
# echo XHC > /proc/acpi/wakeup

```

Esto hará que la suspensión vuelva a funcionar otra vez. Sin embargo estos ajustes son temporales y debe de establecerlos en cada reinicio. Para automatizar eche un vistazo a [escribir archivos unitarios](/index.php/Systemd_(Espa%C3%B1ol)#Escribir_archivos_de_unidad "Systemd (Español)"). Vea el [hilo BBS](https://bbs.archlinux.org/viewtopic.php?pid=1575617#p1575617) para una posible solución y más información.

Si utiliza el controlador `nouveau` la razón para el despertar instantáneo puede ocurrir por un error en el controlador que a veces previene que se suspenda la tarjeta gráfica. Una posible solución es no cargar el módulo del núcleo `nouveau` antes de suspender y cargarlo después de despertar. Para hacerlo cree el siguiente script:

 `/usr/lib/systemd/system-sleep/10-nouveau.sh` 
```
#!/bin/bash

case $1/$2 in
  pre/*)
    # echo "Going to $2..."
    /usr/bin/echo "0" > /sys/class/vtconsole/vtcon1/bind
    /usr/bin/rmmod nouveau
    ;;
  post/*)
    # echo "Waking up from $2..."
    /usr/bin/modprobe nouveau
    /usr/bin/echo "1" > /sys/class/vtconsole/vtcon1/bind
    ;;
esac
```

La primera línea echo desata nouveaufb del controlador del dispositivo de almacenamiento de fotogramas de la consola (fbcon). Normalmente es `vtcon1` como en este ejemplo, pero puede haber otro `vtcon*`. Vea `/sys/class/vtconsole/vtcon*/name` que uno de ellos es un "dispositivo de almacenamiento de fotogramas" [[4]](https://nouveau.freedesktop.org/wiki/KernelModeSetting/).

### El sistema no se apaga cuando hiberna

Cuando hiberna sus sistema el sistema se debe de apagar (después de guardar el estado en el disco). A veces puede que vea el LED de energía siga encendido. Si esto ocurre puede ser recomendable establecer el `HibernateMode` a `shutdown` en [sleep.conf.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.conf.d.5):

 `/etc/systemd/sleep.conf.d/hibernatemode.conf` 
```
[Sleep]
HibernateMode=shutdown
```

Con la configuración de arriba, si todo lo demás está configurado correctamente, en la invocación a `systemctl hibernate` el sistema se apagará guardando el estado en el disco.
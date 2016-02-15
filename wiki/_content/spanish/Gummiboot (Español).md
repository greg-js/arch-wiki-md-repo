De la [página principal de gummiboot](http://freedesktop.org/wiki/Software/gummiboot/):

	_gummiboot es un sencillo gestor de arranque UEFI que ejecuta imágenes EFI configuradas. La entrada predeterminada es seleccionada por un patrón configurado (glob) o un menú en pantalla_.

Es fácil de configurar, pero solo puede iniciar ejecutables EFI, [EFISTUB](/index.php/EFISTUB "EFISTUB") del kernel de Linux , Shell UEFI, grub.efi, y similares.

**Advertencia:** gummiboot simplemente ofrece un menú de arranque para los EFISTUB del kernel. En caso de tener problemas al arrancar el kernel con EFISTUB como en [FS#33745](https://bugs.archlinux.org/task/33745), debe utilizar un gestor de arranque que no utilice EFISTUB, como [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") o [ELILO](/index.php/Bootloaders#ELILO "Bootloaders").

**Nota:** En todo el artículo, `$esp` hace referencia al punto de montaje de la [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI") conocida como ESP.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Actualización](#Actualizaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configuración básica](#Configuraci.C3.B3n_b.C3.A1sica)
    *   [2.2 Añadir entradas de arranque](#A.C3.B1adir_entradas_de_arranque)
    *   [2.3 Añadir seguridad](#A.C3.B1adir_seguridad)
    *   [2.4 Soporte para hibernación](#Soporte_para_hibernaci.C3.B3n)
*   [3 Dentro del menú de arranque](#Dentro_del_men.C3.BA_de_arranque)
    *   [3.1 Teclas](#Teclas)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 Entrada manual usando efibootmgr](#Entrada_manual_usando_efibootmgr)
    *   [4.2 El menú no aparece después de la actualización de Windows](#El_men.C3.BA_no_aparece_despu.C3.A9s_de_la_actualizaci.C3.B3n_de_Windows)
*   [5 Referencias](#Referencias)

## Instalación

En primer lugar, asegúrese de que arranca en modo UEFI para que [las variables EFI estén accesibles](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Requisitos_del_soporte_de_las_variables_UEFI_para_que_funcione_correctamente "Unified Extensible Firmware Interface (Español)"), que la partición del sistema EFI se monta correctamente y que su kernel e initramfs se copian en ESP, ya que, de otro modo, gummiboot no cargará los binarios EFI ubicados en otras particiones. Es altamente recomendable montar ESP en `/boot` si utiliza gummiboot.

Después, [instale](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes "Pacman (Español)") el paquete [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Por último, escriba la orden siguiente para copiar el binario gummiboot a la partición del sistema EFI y así añadir gummiboot como la aplicación por defecto EFI (entrada de inicio por defecto) para que se cargue por el EFI Boot Manager. Si no ha arrancado en modo UEFI y las variables EFI no están accesibles, la entrada de arranque creada fallará. Sin embargo, todavía podrá ser capaz de arrancar gummiboot copiando el binario gummiboot a la ubicación del binario EFI por defecto en su ESP (`$esp/EFI/boot/bootx64.efi` en sistemas x64) a menos que una aplicación EFI que no sea gummiboot ya está presente con el mismo nombre de archivo.

```
# gummiboot --path=_$esp_ install

```

### Actualización

gummiboot asume que EFI System Partition se monta en `/boot`, en cuyo caso, cada vez que una nueva versión gummiboot esté disponible, la orden `gummiboot --path=_$esp_ update` será llamada automáticamente por el método `post_install` del script de instalación. Si la ESP no está montada en `/boot`, tendrá que ajustar manualmente esta orden.

## Configuración

### Configuración básica

La configuración básica se mantiene en `$esp/loader/loader.conf`, con solo dos posibles opciones de configuración:

*   `default` – entrada por defecto para seleccionar (sin el sufijo `.conf`); se puede utilizar un comodín como `arch-*`

*   `timeout` – tiempo de espera del menú en segundos. Si este no se ha establecido, el menú solo se muestra cuando se mantiene pulsada la tecla de espacio durante el arranque.

Ejemplo:

 `$esp/loader/loader.conf` 

```
default  arch
timeout  4

```

Tenga en cuenta que ambas opciones se pueden cambiar en el mismo menú de arranque, que se almacenará como variables de EFI.

**Nota:** Si no se ha configurado ningún tiempo de espera y no se pulsa ninguna tecla durante el arranque, la entrada por defecto se ejecutará de inmediato.

### Añadir entradas de arranque

gummiboot busca los items para el menú de arranque en `$esp/loader/entries/*.conf` —cada archivo encontrado debe contener exactamente una entrada de arranque—. Las opciones posibles son:

*   `title` – nombre del sistema operativo. **Necesario.**

*   `version` – versión del kernel, que se muestra solamente cuando existan varias entradas con el mismo título. Opcional.

*   `machine-id` – identificador de la máquina desde `/etc/machine-id`, que se muestra solamente cuando existan varias entradas con la misma versión y título. Opcional.

*   `efi` – programas EFI a iniciar, que se encuentren en la ESP (`$esp`); por ejemplo, `/vmlinuz-linux`. Tanto este como `linux` (véase a continuación) son **necesarios.**

*   `options` – opciones de línea de órdenes para pasar al programa EFI. Opcional, pero es necesario al menos `initrd=_ruta-a-efi_` y `root=_dev_` para arrancar Linux.

Para Linux, puede especificar `linux _ruta-a-vmlinuz_` y `initrd _ruta-a-initramfs_`; esto se traducirá automáticamente en `_ruta_ a efi` y `options initrd=_ruta_` —esta sintaxis solo es apoyada por eficacia y no altera su función—.

Puede encontrar la PARTUUID de sus dispositivos con la orden `blkid -s PARTUUID -o value /dev/sdxx` (/dev/sdxx debe ser su partición raíz y no $esp)

Una entrada de ejemplo para Arch Linux:

 `$esp/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Tenga en cuenta que, en el ejemplo anterior, PARTUUID/PARTLABEL identifica una partición de una tabla de particionado GPT, y difiere de la UUID/LABEL, que identifica un sistema de archivos. Utilizar PARTUUID/PARTLABEL es ventajoso porque es invariante si reformatea la partición con otro sistema de archivos o el mapeado /dev/sd* cambia por alguna razón. También es útil si la partición en cuestión no tiene un sistema de archivos (o se utiliza LUKS, que no admite etiquetas).

Un ejemplo de entrada para la raiz (root) encriptada (dm-crypt con LUKS)

 `$esp/loader/entries/arch-encrypted.conf` 

```
title          Arch Linux (Encrypted)
linux          /ruta/a/vmlinuz-linux
options        initrd=/ruta/a/initramfs-linux.img cryptdevice=UUID=<UUID>:luks-<UUID> root=UUID=<luks-UUID> rw
```

En el ejemplo de cifrado, advierta que initrd está en _options_ —esto no parece ser discrecional en este momento—. También tenga en cuenta que en este ejemplo se utiliza UUID. PARTUUID debe ser capaz de reemplazar UUID, si así se desea.

También puede agregar otros programas EFI como `\EFI\arch\grub.efi`.

**Nota:** gummiboot comprobará automáticamente «**Windows Boot Manager**» (`\EFI\Microsoft\Boot\Bootmgfw.efi`), «**EFI Shell**» (`\shellx64.efi`) y «**EFI Default Loader**» (`\EFI\Boot\bootx64.efi`), y mostrará las entradas para ellos si están presentes, por lo que no tiene que crear manualmente las entradas para los mismos. Sin embargo, no autodetecta otras aplicaciones EFI (a diferencia de rEFInd), por lo que para arrancar el kernel, deben crearse manualmente las entradas de configuración como se mencionó anteriormente.

### Añadir seguridad

Hay que señalar que los parámetros de la línea de órdenes del kernel se pueden editar desde el menú del gestor de arranque de gummiboot (ver [#Teclas](#Teclas)) pulsando `e`. Esto supone un importante problema de seguridad, ya que si se redefine el argumento del kernel `init=` con `init=/bin/bash` por ejemplo, esto va a hacer que la máquina arranque directamente como root sin pedir ninguna contraseña, puenteandose fácilmente la contraseña de root que haya sido definida previamente. gummiboot actualmente no tiene una función para configurar contraseñas y no tiene capacidad para prevenir los cambios de los parámetros del kernel, por tanto, es necesario asegurarse de establecer una contraseña a nivel de hardware (UEFI/BIOS) que impida que el equipo arranque si no se ha introducido la contraseña correcta.

Dado que la seguridad es de varios niveles y el acceso físico ya rompe cualquier sistema de seguridad, tal vez el cifrado de su disco con [dm-crypt](/index.php/Dm-crypt "Dm-crypt") sería muy útil, sobre todo si el equipo es un portátil. Pero esto es un problema de otro tema, que no concierne a gummiboot.

### Soporte para hibernación

Remítase al artículo [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate"), especialmente a [ejemplo para gummiboot](/index.php/Suspend_and_hibernate#Example_for_gummiboot "Suspend and hibernate").

## Dentro del menú de arranque

### Teclas

Las siguientes teclas se utilizan dentro del menú:

*   `Arriba/Abajo` - selecciona la entrada
*   `Intro` - arranca la entrada seleccionada
*   `d` - selecciona la entrada por defecto para arrancar (almacenado en una variable de EFI no volátil)
*   `-/T` - disminuye el tiempo de espera (almacenado en una variable de EFI no volátil)
*   `+/t` - aumenta el tiempo de espera (almacenado en una variable de EFI no volátil)
*   `e` - edita la línea de órdenes del kernel
*   `v` - muestra la versión de gummiboot y de UEFI
*   `Q` - sale
*   `P` - imprime la configuración actual
*   `h/?` - ayuda

Las siguientes teclas son de acceso rápido, de modo que cuando se pulsan dentro del menú o durante el arranque, inician directamente una entrada específica:

*   `l` - Linux
*   `w` - Windows
*   `a` - OS X
*   `s` - Shell EFI
*   `1-9` - número de entrada

## Solución de problemas

### Entrada manual usando efibootmgr

Si la orden `gummiboot install` falla, puede crear una entrada de arranque EFI manualmente con la utilidad `efibootmgr`:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/gummiboot/gummibootx64.efi -L "Gummiboot"

```

Donde `/dev/sdXY` es la partición Efisys.

### El menú no aparece después de la actualización de Windows

Por ejemplo, si se ha actualizado de Windows 8 a Windows 8.1, y ya no se ve un menú de arranque después de la actualización (es decir, Windows se inicia de inmediato):

*   Asegúrese de que Secure Boot (en la configuración de la BIOS) y Fast Startup (valor de la opción de energía de Windows) están desactivados.
*   Asegúrese de que su BIOS prefiere Linux Boot Manager antes que Windows Boot Manager (dependiendo de su BIOS, esto podría aparecer bajo una configuración de Hard Disk Drive Priority).

## Referencias

*   [http://freedesktop.org/wiki/Software/gummiboot/](http://freedesktop.org/wiki/Software/gummiboot/)
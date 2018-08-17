**Estado de la traducción:** este artículo es una versión traducida de [Systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Fecha de la última traducción/revisión: **2016-09-19**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=448431).

Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")

**systemd-boot**, anteriormente llamado **gummiboot**, es un sencillo gestor de arranque UEFI que ejecuta imágenes EFI configuradas. La entrada predeterminada es seleccionada por un patrón configurado (glob) o un menú en pantalla. Se incluye en el paquete [systemd](https://www.archlinux.org/packages/?name=systemd), que se instala en un sistema Arch de forma predeterminada.

Es fácil de configurar, pero solo puede iniciar ejecutables EFI, tales como [EFISTUB](/index.php/EFISTUB "EFISTUB") del kernel de Linux, Shell UEFI, GRUB, el Windows Boot Manager, y similares.

**Advertencia:** *systemd-boot* simplemente ofrece un menú de arranque para los EFISTUB del kernel. En caso de tener problemas al arrancar el kernel con EFISTUB como en [FS#33745](https://bugs.archlinux.org/task/33745), debe utilizar un gestor de arranque que no utilice EFISTUB, como [GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") o cualquier otro [gestor de arranque](/index.php/Boot_loader "Boot loader") que no dependa exclusivamente de [UEFI](/index.php/UEFI "UEFI").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Arranque EFI](#Arranque_EFI)
    *   [1.2 Arranque Legacy](#Arranque_Legacy)
    *   [1.3 Actualizar](#Actualizar)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configuración básica](#Configuraci.C3.B3n_b.C3.A1sica)
    *   [2.2 Añadir entradas de arranque](#A.C3.B1adir_entradas_de_arranque)
        *   [2.2.1 Instalaciones de root estándar](#Instalaciones_de_root_est.C3.A1ndar)
        *   [2.2.2 Instalaciones de root sobre LVM](#Instalaciones_de_root_sobre_LVM)
        *   [2.2.3 Instalaciones de root cifrado](#Instalaciones_de_root_cifrado)
        *   [2.2.4 Instalaciones de root sobre subvolumen btrfs](#Instalaciones_de_root_sobre_subvolumen_btrfs)
        *   [2.2.5 Shells EFI u otras aplicaciones de EFI](#Shells_EFI_u_otras_aplicaciones_de_EFI)
    *   [2.3 Soporte para hibernación](#Soporte_para_hibernaci.C3.B3n)
*   [3 Teclas dentro del menú de arranque](#Teclas_dentro_del_men.C3.BA_de_arranque)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 Entrada manual utilizando efibootmgr](#Entrada_manual_utilizando_efibootmgr)
    *   [4.2 El menú no aparece después de actualizar Windows](#El_men.C3.BA_no_aparece_despu.C3.A9s_de_actualizar_Windows)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

### Arranque EFI

1.  Asegúrese de que ha arrancado en modo UEFI.
2.  Verifique que [las variables EFI son accesibles](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface").
3.  Monte la [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) correctamente. En este artículo se utiliza `*esp*` para indicar su punto de montaje.
    **Nota:** *systemd-boot* no puede cargar archivos binarios de EFI desde otras particiones. Por ello se recomienda montar la ESP en `/boot`. Vea [#Actualizar](#Actualizar) para obtener más información y trabajar sobre ello, en el caso de que desee separar `/boot` de ESP.

4.  Si la partición ESP **no** utiliza la partición /boot deberá copiar el kernel e initramfs a aquella en la que esté la ESP.
    **Nota:** Para obtener una forma de mantener actualizado automáticamente el kernel en la ESP, eche un vistazo al [artículo EFISTUB](/index.php/EFISTUB#Using_systemd "EFISTUB") para conocer algunas unidades de systemd que se pueden adaptar. Si la partición efi utiliza automount, necesita añadir `vfat` a un archivo en `/etc/modules-load.d/` para asegurarse de que el kernel que se está ejecutando ha cargado el módulo `vfat` en el arranque, antes de que ocurra cualquier actualización del kernel que podría remplazar el módulo por la versión actualmente en ejecución, haciendo imposible el montaje de `/boot/efi` hasta el reinicio.

5.  Escriba la siguiente órden para instalar *systemd-boot*: `# bootctl --path=*esp* install` Se copiará el binario *systemd-boot* a la partición EFI System Partition (`*esp*/EFI/systemd/systemd-bootx64.efi` y `*esp*/EFI/Boot/BOOTX64.EFI` —ambos idénticos— en sistemas x64) y añadirá el propio *systemd-boot* como aplicación EFI por defecto (entrada de arranque por defecto) cargada por el gestor de arranque EFI.
6.  Por último, debe [configurar](#Configuraci.C3.B3n) el gestor de arranque para que funcione correctamente.

### Arranque Legacy

**Advertencia:** Este no es el proceso recomendado.

También puede instalar con éxito *systemd-boot* si arranca con un sistema operativo antiguo. Sin embargo, esto requiere que más tarde se le diga a su firmware que lance el archivo EFI de *systemd-boot* en el arranque:

*   que, o bien tiene una shell EFI trabajando en algún lugar;
*   o la interfaz de su firmware le proporciona una forma de establecer adecuadamente el archivo EFI que se cargará en el arranque.

**Nota:** Por ejemplo, en la serie Latitude de Dell, la interfaz de firmware proporciona todo lo necesario para la configuración de arranque EFI y la shell EFI no será capaz de escribir en la ROM del ordenador.

Si puede hacerlo, la instalación es fácil: entre en la shell EFI o en la interfaz de configuración del firmware y cambie los archivos EFI por defecto del equipo por `*esp*/EFI/systemd/systemd-bootx64.efi` (`systemd-bootia32.efi` en sistemas i686).

### Actualizar

*systemd-boot* ([bootctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bootctl.1)) asume que EFI System Partition se monta en `/boot`. A diferencia del anterior paquete separado *gummiboot*, que se actualizaba automáticamente en cada nueva versión del paquete con un script `post_install`, las actualizaciones de las nuevas versiones de *systemd-boot* ahora son manejadas manualmente por el usuario:

```
# bootctl update

```

Si la ESP no está montada en `/boot`, la opción `--path=` puede pasar la ruta. Por ejemplo:

```
# bootctl --path=*esp* update

```

**Nota:** Esta es también la orden a utilizar cuando se migra de *gummiboot*, antes de eliminar el paquete. Si, no obstante, dicho paquete ya se eliminó, ejecute `bootctl --path=*esp* install`.

## Configuración

### Configuración básica

La configuración básica se coloca en `*esp*/loader/loader.conf`, con tres posibles opciones de configuración:

*   `default` – entrada por defecto para seleccionar (sin el sufijo `.conf`); se puede utilizar un comodín como `arch-*`

*   `timeout` – tiempo de espera del menú, en segundos. Si este no se ha establecido, el menú solo se muestra cuando se mantiene pulsada la tecla de espacio durante el arranque.

*   `editor` - si se quiere activar el editor de los parámetros del kernel o no. `1` (por defecto) es para activar, `0` es para desactivar. Dado que el usuario puede añadir `init=/bin/bash` para puentear la contraseña de root y acceder como tal, se recomienda encarecidamente establecer esta opción en `0`.

Ejemplo:

 `*esp*/loader/loader.conf` 
```
default  arch
timeout  4
editor   0

```

**Nota:** Tenga en cuenta que las dos primeras opciones se pueden cambiar en el mismo menú de arranque, que se almacenará como variables de EFI.

**Sugerencia:** Un ejemplo de archivo de configuración básico puede encontralo en `/usr/share/systemd/bootctl`.

### Añadir entradas de arranque

**Nota:**

*   *bootctl* buscará automáticamente para "**Windows Boot Manager**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) y "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`). En caso de detectarse, las entradas también se generarán automáticamente para ellos. Sin embargo, no se autodetectan otras aplicaciones EFI (a diferencia de [rEFInd](/index.php/REFInd "REFInd")), por lo que para arrancar el kernel, deben ser creadas entradas de configuración manuales.
*   Si tiene un arranque dual con Windows, se recomienda encarecidamente desactivar la opción por defecto [Fast Start-Up](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows").
*   Recuerde que debe cargar el [microcode](/index.php/Microcode "Microcode") de intel con `initrd` si procede.
*   Puede encontrar el identificador `PARTUUID` de la partición root con la orden `blkid -s PARTUUID -o value /dev/sd*xY*`, donde `*x*` es la letra del dispositivo, y `*Y*` es el número de la partición. Esto solo es necesario para la partición raíz, no para `*esp*`.

*bootctl* buscará los elementos para el menú de arranque en `*esp*/loader/entries/*.conf` —cada archivo encontrado debe contener exactamente una entrada de arranque—. Las opciones posibles son:

*   `title` – nombre del sistema operativo. **Necesario.**

*   `version` – versión del kernel, que se muestra solamente cuando existan varias entradas con el mismo título. Opcional.

*   `machine-id` – identificador de la máquina desde `/etc/machine-id`, que se muestra solamente cuando existan varias entradas con la misma versión y título. Opcional.

*   `efi` – programas EFI a iniciar, que se encuentren en la ESP (`esp`); por ejemplo, `/vmlinuz-linux`. Tanto este como `linux` (véase a continuación) son **necesarios.**

*   `options` – opciones de línea de órdenes para pasar al programa EFI. Opcional, pero es necesario al menos `initrd=*ruta-a-efi*` y `root=*dev*` para arrancar Linux.

Para Linux, puede especificar `linux *ruta-a-vmlinuz*` y `initrd *ruta-a-initramfs*`; esto se traducirá automáticamente en `*ruta* a efi` y `options initrd=*ruta*` —esta sintaxis solo es apoyada por eficacia y no altera su función—.

#### Instalaciones de root estándar

He aquí un ejemplo de entrada para una partición raíz sin LVM o LUKS:

 `*esp*/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

Note que, en el ejemplo anterior, `PARTUUID`/`PARTLABEL` identifica una partición GPT, y difiere de `UUID`/`LABEL`, que identifica un sistema de archivos. El uso de `PARTUUID`/`PARTLABEL` es ventajoso porque es invariable (es decir, que no cambia) si vuelve a formatear la partición con otro sistema de archivos, o si el mapeado de `/dev/sd*` cambia por cualquier razón. También es útil si no se tiene un sistema de archivos en la partición (o utiliza LUKS, que no soporta `LABEL`s).

**Sugerencia:** Puede encontrar un archivo de ejemplo en `/usr/share/systemd/bootctl`.

#### Instalaciones de root sobre LVM

**Advertencia:** *systemd-boot* no puede ser utilizado sin un sistema de archivos `/boot` separado fuera de LVM.

Este es un ejemplo para una partición root utilizando la [gestión de volúmenes lógicos (LVM)](/index.php/LVM "LVM"):

 `*esp*/loader/entries/arch-lvm.conf` 
```
title          Arch Linux (LVM)
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=/dev/mapper/<GrupodeVolúmenes-VolumenLógico> rw
```

Sustituya `<GrupodeVolúmenes-VolumenLógico>` con los nombres reales del Grupo de Volúmenes y del Volumen Lógico (por ejemplo `root=/dev/mapper/volgroup00-lvolroot`). Alternativamente, también es posible utilizar una UUID en su lugar:

```
....
options  root=UUID=<identificador UUID> rw

```

Advierta que `root=**UUID**=` es usado en lugar de `root=**PARTUUID**=`, que es utilizado para las particiones Root sin LVM o LUKS.

#### Instalaciones de root cifrado

Este es un ejemplo de un archivo de configuración para una partición root cifrada ([DM-Crypt / LUKS](/index.php/Dm-crypt "Dm-crypt")):

 `*esp*/loader/entries/arch-encrypted.conf` 
```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<nombre-dispositivo-mapeado> root=/dev/mapper/<nombre-dispositivo-mapeado> quiet rw
```

En este ejemplo se utiliza el identificador UUID; pero podría remplazar el UUID con el identificador `PARTUUID`, si lo desea. También puede remplazar la ruta `/dev` con el UUID propio. El `nombre-dispositivo-mapeado` será el que quiera ponerle. Vea [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

Si está utilizando LVM, su línea cryptdevice se verá así:

 `*esp*/loader/entries/arch-encrypted-lvm.conf` 
```
title Arch Linux Encrypted LVM
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:GrupodeVolúmenes root=/dev/mapper/GrupodeVolúmenes-VolumenLógicoRoot quiet rw
```

También se pueden añadir otros programas tales como `\EFI\arch\grub.efi`.

#### Instalaciones de root sobre subvolumen btrfs

Si se arranca un subvolumen [btrfs](/index.php/Btrfs "Btrfs") como root, modifique la línea `options` con `rootflags=subvol=<root subvolume>`. En el siguiente ejemplo, la raíz se ha montado como un subvolumen btrfs llamado «ROOT» (por ejemplo, `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `*esp*/loader/entries/arch-btrfs-subvol.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

Si no se hace según se ha indicado, dará como resultado el siguiente mensaje de error: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### Shells EFI u otras aplicaciones de EFI

En el caso de que haya instalado shells de EFI u otras aplicaciones EFI dentro de la ESP, puede utilizar los siguientes fragmentos:

 `*esp*/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```
 `*esp*/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title  UEFI Shell x86_64 v2
efi    /EFI/shellx64_v2.efi
```

### Soporte para hibernación

Véase [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Teclas dentro del menú de arranque

Las siguientes teclas se utilizan dentro del menú:

*   `Arriba/Abajo` - selecciona la entrada
*   `Intro` - arranca la entrada seleccionada
*   `d` - selecciona la entrada por defecto para arrancar (almacenado en una variable de EFI no volátil)
*   `-/T` - disminuye el tiempo de espera (almacenado en una variable de EFI no volátil)
*   `+/t` - aumenta el tiempo de espera (almacenado en una variable de EFI no volátil)
*   `e` - edita la línea de órdenes del kernel
*   `v` - muestra la versión de systemd-boot y de UEFI
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

### Entrada manual utilizando efibootmgr

Si la orden `bootctl install` cfalla, puede crear una entrada de arranque EFI manualmente con la utilidad [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr):

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/systemd/systemd-bootx64.efi -L "Linux Boot Manager"

```

Donde `/dev/sdXY` es la [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

### El menú no aparece después de actualizar Windows

Véase [UEFI#Windows changes boot order](/index.php/UEFI#Windows_changes_boot_order "UEFI").

## Véase también

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)
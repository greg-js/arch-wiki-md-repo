**Estado de la traducción**
Este artículo es una traducción de [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), revisada por última vez el **2018-12-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=553630) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")

**systemd-boot**, anteriormente llamado **gummiboot**, es un sencillo [gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)") UEFI que ejecuta imágenes EFI configuradas. La entrada predeterminada es seleccionada por un patrón configurado ([glob](https://en.wikipedia.org/wiki/es:Glob_(inform%C3%A1tica) "wikipedia:es:Glob (informática)")) o un menú en pantalla. Se incluye en el paquete [systemd](https://www.archlinux.org/packages/?name=systemd), que se instala en un sistema Arch de forma predeterminada.

Es fácil de configurar, pero solo puede iniciar ejecutables EFI, tales como [EFISTUB (Español)](/index.php/EFISTUB_(Espa%C3%B1ol) "EFISTUB (Español)") del kernel de Linux, Intérprete de órdenes de UEFI, GRUB o Windows Boot Manager.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Instalar el gestor de arranque EFI](#Instalar_el_gestor_de_arranque_EFI)
    *   [1.2 Actualizar el gestor de arranque EFI](#Actualizar_el_gestor_de_arranque_EFI)
        *   [1.2.1 Actualización manual](#Actualización_manual)
        *   [1.2.2 Actualización automática](#Actualización_automática)
*   [2 Configuración](#Configuración)
    *   [2.1 Configurar el cargador](#Configurar_el_cargador)
    *   [2.2 Añadir entradas al cargador](#Añadir_entradas_al_cargador)
        *   [2.2.1 Intérpretes de órdenes de EFI y otras aplicaciones EFI](#Intérpretes_de_órdenes_de_EFI_y_otras_aplicaciones_EFI)
    *   [2.3 Arrancar con la configuración del firmware de EFI](#Arrancar_con_la_configuración_del_firmware_de_EFI)
    *   [2.4 Preparar los kernels para /EFI/Linux](#Preparar_los_kernels_para_/EFI/Linux)
    *   [2.5 Proporcionar soporte para hibernación](#Proporcionar_soporte_para_hibernación)
    *   [2.6 Proteger con contraseña el editor de parámetros del kernel](#Proteger_con_contraseña_el_editor_de_parámetros_del_kernel)
*   [3 Teclas utilizadas en el menú de arranque](#Teclas_utilizadas_en_el_menú_de_arranque)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Instalación después de arrancar en modo BIOS](#Instalación_después_de_arrancar_en_modo_BIOS)
    *   [4.2 Crear entrada manual utilizando efibootmgr](#Crear_entrada_manual_utilizando_efibootmgr)
    *   [4.3 El menú no aparece después de actualizar Windows](#El_menú_no_aparece_después_de_actualizar_Windows)
*   [5 Véase también](#Véase_también)

## Instalación

### Instalar el gestor de arranque EFI

Para instalar el gestor de arranque EFI *systemd-boot* primero asegúrese de que el sistema haya arrancado en modo UEFI y que las [variables de UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Variables_de_UEFI "Unified Extensible Firmware Interface (Español)") son accesibles. Esto se puede verificar ejecutando la orden `efivar --list`.

Cabe señalar que *systemd-boot* solo puede cargar el kernel [EFISTUB](/index.php/EFISTUB "EFISTUB") desde la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") (ESP). Para mantener el kernel actualizado, es más sencillo y, por lo tanto, mas **recomendable** montar la ESP en `/boot`. Si la ESP **no** está montada en `/boot`, los archivos kernel y de initramfs deben copiarse en dicha ESP. Consulte [EFI system partition (Español)#Puntos de montaje alternativos](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Puntos_de_montaje_alternativos "EFI system partition (Español)") para más detalles.

`*esp*`se usará a lo largo de esta página para indicar el punto de montaje ESP, es decir, `/boot`.

Con la ESP montada en `*esp*`, utilice [bootctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bootctl.1) para instalar *systemd-boot* en la partición del sistema EFI ejecutando:

```
# bootctl --path=*esp* install

```

Esto copiará el cargador de arranque *systemd-boot* a la partición EFI: en un sistema de arquitectura x64 los dos binarios idénticos `*esp*/EFI/systemd/systemd-bootx64.efi` y `*esp*/EFI/BOOT/BOOTX64.EFI` se transferirán a la ESP. A continuación, establecerá *systemd-boot* como la aplicación EFI predeterminada (entrada de arranque predeterminada) cargada por el gestor de arranque EFI («*EFI Boot Manager*»).

Luego, vaya a la sección [#Configuración](#Configuración) para agregar entradas de arranque para que *systemd-boot* funcione correctamente en el momento del arranque.

### Actualizar el gestor de arranque EFI

Siempre que haya una nueva versión de *systemd-boot*, el gestor de arranque debe ser actualizado por el usuario. Esto se puede realizar bien manualmente o bien la actualización se puede activar automáticamente utilizando los hooks de pacman. Los dos enfoques se describen a continuación.

#### Actualización manual

*systemd-boot* pueden ser actualizado por *systemd-boot*. Si el parámetro `path` no se especifica, `/efi`, `/boot`, y `/boot/efi` se verifican a su vez.

```
# bootctl update

```

Si la ESP está montada en una ubicación diferente, la opción `--path=` puede pasar la ruta apropiada. Por ejemplo:

```
# bootctl --path=*esp* update

```

**Nota:** esta es también la orden a utilizar cuando se migra de *gummiboot*, antes de eliminar el paquete. Si, no obstante, dicho paquete ya se eliminó, ejecute `bootctl --path=*esp* install`.

#### Actualización automática

El paquete [systemd-boot-pacman-hook](https://aur.archlinux.org/packages/systemd-boot-pacman-hook/) proporciona un [hook de pacman](/index.php/Pacman_hook "Pacman hook") para automatizar el proceso de actualización. Al [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete, este agregará un hook que se ejecutará cada vez que se actualice el paquete [systemd](https://www.archlinux.org/packages/?name=systemd). En otro caso, para replicar lo que hace el paquete *systemd-boot-pacman-hook* sin instalarlo, coloque el siguiente hook de pacman en el directorio `/etc/pacman.d/hooks/`:

 `/etc/pacman.d/hooks/systemd-boot.hook` 
```
[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Updating systemd-boot
When = PostTransaction
Exec = /usr/bin/bootctl update
```

## Configuración

### Configurar el cargador

La configuración del cargador se coloca en `*esp*/loader/loader.conf`, y está compuesto por las siguientes opciones:

*   `default` — entrada por defecto para seleccionar como se define [#Añadir entradas al cargador](#Añadir_entradas_al_cargador); se da sin el sufijo *.conf* y se puede utilizar un comodín como `arch-*`;

*   `timeout` — tiempo de espera del menú, en segundos. Si este no se ha establecido, el menú solo se muestra cuando se mantiene pulsada la tecla `espaciadora` (aunque también funcionan la mayoría de las otras teclas) durante el arranque;

*   `editor` — si se quiere activar el editor de los parámetros del kernel o no. `yes` (por defecto) es para activar, `no` es para desactivar. Dado que el usuario puede añadir `init=/bin/bash` para puentear la contraseña de root y acceder como tal, se recomienda encarecidamente establecer esta opción en `no`;

*   `auto-entries` — muestra entradas automáticas para Windows, EFI Shell y Default Loader si se configura en `1` (default), `0` para ocultar;

*   `auto-firmware` — muestra la entrada para reiniciar en las configuraciones de firmware UEFI si está configurado en `1` (default), `0` para ocultar;

*   `console-mode` — cambia el modo de consola UEFI: `0` para 80x25, `1` para 80x50, `2` y superior para modos no estándar proporcionado por el firmware del dispositivo, si existe, `auto` selecciona un modo adecuado automáticamente, `max` para el modo más alto disponible, `keep` (default) para el modo de firmware seleccionado.

Consulte el [manual de loader.conf](https://www.freedesktop.org/software/systemd/man/loader.conf.html) para ver la lista completa de opciones.

He aquí un ejemplo de configuración del cargador:

 `*esp*/loader/loader.conf` 
```
default  arch
timeout  4
console-mode max
editor   no

```

**Sugerencia:**

*   `default` y `timeout` se pueden cambiar en el menú de inicio y los cambios se almacenarán como variables EFI, sobrescribiendo estas opciones.
*   Un archivo básico de configuración del cargador se encuentra en `/usr/share/systemd/bootctl/loader.conf`.

### Añadir entradas al cargador

*bootctl* busca elementos del menú de arranque en `*esp*/loader/entries/*.conf` —cada archivo encontrado debe contener exactamente un cargador—. Las opciones posibles son:

*   `title` — nombre del sistema operativo. **Necesario.**

*   `version` — versión del kernel, que se muestra solamente cuando existan varias entradas con el mismo título. Opcional.

*   `machine-id` — identificador de la máquina desde `/etc/machine-id`, que se muestra solamente cuando existan varias entradas con la misma versión y título. Opcional.

*   `efi` — programas EFI a iniciar, que se encuentren en la ESP (`esp`); por ejemplo, `/vmlinuz-linux`. **Tanto** este parámetro como `linux` (véase a continuación) son **necesarios.**

*   `options` — opciones de línea de órdenes para pasar al programa EFI o los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"). Opcional, pero es necesario al menos `initrd=*ruta-a-efi*` y `root=*dev*` para arrancar Linux.

Para el arranque de Linux, también puede usar, en lugar de `efi` y `options`, la siguiente sintaxis:

*   `linux` y `initrd` seguidos de la ruta relativa de los archivos correspondientes en el ESP; por ejemplo `/vmlinuz-linux`; esto se traducirá automáticamente a `efi *path*` y `options initrd=*path*` —esta sintaxis solo se admite por comodidad y no tiene diferencias en la función—.

Un ejemplo de un archivo de carga para iniciar Arch desde una partición con la etiqueta *arch_os* y cargar el [microcode (Español)](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") de la CPU de Intel sería:

 `*esp*/loader/entries/arch.conf` 
```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options root=LABEL=*arch_os* rw
```

*bootctl* buscará automáticamente para «**Windows Boot Manager**» (`\EFI\Microsoft\Boot\Bootmgfw.efi`), «**EFI Shell**» (`\shellx64.efi`) y «**EFI Default Loader**» (`\EFI\Boot\bootx64.efi`). En caso de detectarlas, las entradas también se generarán automáticamente para ellos. Sin embargo, no autodetecta otras aplicaciones EFI (a diferencia de lo que hace [rEFInd](/index.php/REFInd "REFInd")), por lo que para arrancar el kernel, deben ser creadas entradas de configuración manualmente.

**Nota:**

*   Si realiza un arranque dual con Windows, se recomienda encarecidamente que desactive la opción predeterminada [Fast Start-Up](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows").
*   Recuerde cargar el *microcódigo* de Intel con `initrd` si procede, se proporciona un ejemplo en [Microcode (Español)#systemd-boot](/index.php/Microcode_(Espa%C3%B1ol)#systemd-boot "Microcode (Español)").
*   La partición raíz se puede identificar con su `LABEL` o `PARTUUID`. Este último se puede encontrar con la orden `blkid -s PARTUUID -o value /dev/sd*xY*`, donde `*x*` es la letra del dispositivo y `*Y*` es el número de partición. Esto es necesario solo para identificar la partición raíz, no la partición `*esp*`.

**Sugerencia:**

*   Las entradas de arranque disponibles que se han configurado pueden enumerarse con la orden `bootctl list`.
*   Un archivo de entrada de ejemplo se encuentra en `/usr/share/systemd/bootctl/arch.conf`.
*   Los [kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para escenarios como [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") o [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") se pueden encontrar en sus páginas respectivas.

#### Intérpretes de órdenes de EFI y otras aplicaciones EFI

En el caso de que haya instalado instérpretes de órdenes de EFI u otras aplicaciones EFI dentro de la partición ESP, puede utilizar los siguientes fragmentos:

**Nota:** el parámetro de ruta del archivo para la línea `efi` es relativo a su punto de montaje *esp*. Si está montada en `/boot` y los archivos binarios de EFI residen en `/boot/EFI/xx.efi` y `/boot/yy.efi`, entonces especifique los parámetros como `efi/EFI/xx.efi` y `efi/yy.efi` respectivamente.

Ejemplos de entradas para los cargadores del intérprete de órdenes de UEFI personalizadas:

 `*esp*/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title   UEFI Shell x86_64 v1
efi     /EFI/shellx64_v1.efi

```
 `*esp*/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title   UEFI Shell x86_64 v2
efi     /EFI/shellx64_v2.efi

```

### Arrancar con la configuración del firmware de EFI

La mayoría de los firmware del sistema configurado para el inicio de EFI agregarán sus propias entradas [efibootmgr](/index.php/Efibootmgr "Efibootmgr") para arrancar en la «Configuración del Firmware de UEFI».

### Preparar los kernels para /EFI/Linux

*/EFI/Linux* busca archivos del kernel especialmente preparados, que agrupan el kernel, el disco RAM de inicio (initrd), la línea de órdenes del kernel y `/etc/os-release` en un solo archivo . Este archivo se puede firmar fácilmente para «secure boot».

**Nota:** `systemd-boot` requiere que el archivo `os-release` contenga bien `VERSION_ID` o bien `BUILD_ID` para generar una ID y agregar automáticamente la entrada, que el archivo `os-release` de Arch no hace. Mantenga su propia copia con uno de ellos o haga que su script de agrupación lo genere automáticamente.

Coloque la línea de órdenes del kernel que desea usar en un archivo y cree un archivo de agrupación como este:

 `Kernel packaging command:` 
```
objcopy \
    --add-section .osrel="/usr/lib/os-release" --change-section-vma .osrel=0x20000 \
    --add-section .cmdline="kernel-command-line.txt" --change-section-vma .cmdline=0x30000 \
    --add-section .linux="vmlinuz-file" --change-section-vma .linux=0x40000 \
    --add-section .initrd="initrd-file" --change-section-vma .initrd=0x3000000 \
    "/usr/lib/systemd/boot/efi/linuxx64.efi.stub" "*linux*.efi"
```

Opcionalmente firme el archivo `*linux*.efi` producido anteriormente.

Copie `*linux*.efi` en `*esp*/EFI/Linux`.

### Proporcionar soporte para hibernación

Véase [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

### Proteger con contraseña el editor de parámetros del kernel

Alternativamente, puede instalar [systemd-boot-password](https://aur.archlinux.org/packages/systemd-boot-password/) que admite `password` como opción de configuración básica. Utilice `sbpctl generate` para generar un valor para esta opción.

Instale *systemd-boot-password* con la siguiente orden:

 `# sbpctl install *esp*` 

Con el editor activado, se le solicitará su contraseña antes de poder editar los parámetros del kernel.

## Teclas utilizadas en el menú de arranque

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
*   `s` - Shell de EFI
*   `1-9` - número de entrada

## Solución de problemas

### Instalación después de arrancar en modo BIOS

**Advertencia:** esto no es recomendable.

Si se inicia en el modo BIOS, aún puede instalar *systemd-boot*, sin embargo, este proceso requiere que le diga al firmware que inicie el archivo EFI de *systemd-boot* en el arranque, lo cual se puede hacer generalmente de dos maneras:

*   tiene un intérprete de órdenes de EFI en funcionamiento en otro lugar;
*   su interfaz de firmware proporciona una forma de configurar correctamente el archivo EFI que debe cargarse en el momento del arranque.

Si puede hacerlo, la instalación es más fácil: ingrese en el intérprete de órdenes de EFI o en la interfaz de configuración de su firmware y cambie el archivo EFI predeterminado de su equipo a `*esp*/EFI/systemd/systemd-bootx64.efi` (o `systemd-bootia32.efi` dependiendo de si el firmware de su sistema es de 32 bits).

**Nota:** la interfaz de firmware de la serie Latitude de Dell proporciona todo lo que necesita para configurar el arranque EFI, pero el intérprete de órdenes de EFI no podrá escribir en la ROM del equipo.

### Crear entrada manual utilizando efibootmgr

Si la orden `bootctl install` falla, puede crear una entrada de arranque EFI manualmente con la utilidad [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr):

```
# efibootmgr -c -d /dev/sdX -p Y -l "\EFI\systemd\systemd-bootx64.efi" -L "Linux Boot Manager"

```

Donde `/dev/sdXY` es la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)").

**Nota:** la ruta a la imagen EFI debe usar la barra invertida (`\`) como separador.

### El menú no aparece después de actualizar Windows

Véase [UEFI#Windows changes boot order](/index.php/UEFI#Windows_changes_boot_order "UEFI").

## Véase también

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)
*   [https://github.com/systemd/systemd/tree/master/src/boot/efi](https://github.com/systemd/systemd/tree/master/src/boot/efi)
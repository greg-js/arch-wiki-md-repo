## Contents

*   [1 Métodos alternativos de instalación](#M.C3.A9todos_alternativos_de_instalaci.C3.B3n)
    *   [1.1 Instalar en un dispositivo USB externo](#Instalar_en_un_dispositivo_USB_externo)
        *   [1.1.1 BIOS](#BIOS)
        *   [1.1.2 EFI](#EFI)
    *   [1.2 Instalar en un disco con o sin particiones](#Instalar_en_un_disco_con_o_sin_particiones)
    *   [1.3 Generar sólo core.img](#Generar_s.C3.B3lo_core.img)
*   [2 Herramientas GUI de configuración](#Herramientas_GUI_de_configuraci.C3.B3n)
*   [3 Configuración del aspecto](#Configuraci.C3.B3n_del_aspecto)
    *   [3.1 Ajustar la resolución del framebuffer](#Ajustar_la_resoluci.C3.B3n_del_framebuffer)
    *   [3.2 Introducir 915resolution](#Introducir_915resolution)
    *   [3.3 Imagen de fondo y fuentes bitmap](#Imagen_de_fondo_y_fuentes_bitmap)
    *   [3.4 Temas](#Temas)
    *   [3.5 Colores del menú](#Colores_del_men.C3.BA)
    *   [3.6 Menú oculto](#Men.C3.BA_oculto)
    *   [3.7 Desactivar framebuffer](#Desactivar_framebuffer)
*   [4 Iniciar una imagen ISO9660 directamente desde GRUB](#Iniciar_una_imagen_ISO9660_directamente_desde_GRUB)
*   [5 Nomenclatura permanente de dispositivos de bloque](#Nomenclatura_permanente_de_dispositivos_de_bloque)
*   [6 Utilizar etiquetas](#Utilizar_etiquetas)
*   [7 Proteger con contraseña el menú de GRUB](#Proteger_con_contrase.C3.B1a_el_men.C3.BA_de_GRUB)
    *   [7.1 Protección con contraseña sólo para las opciones de edición y consola de GRUB](#Protecci.C3.B3n_con_contrase.C3.B1a_s.C3.B3lo_para_las_opciones_de_edici.C3.B3n_y_consola_de_GRUB)
*   [8 Ocultar GRUB y hacerlo aparecer mediante la tecla Mayús](#Ocultar_GRUB_y_hacerlo_aparecer_mediante_la_tecla_May.C3.BAs)
*   [9 Combinar la utilización de UUID con scripts](#Combinar_la_utilizaci.C3.B3n_de_UUID_con_scripts)
*   [10 Creación manual de grub.cfg](#Creaci.C3.B3n_manual_de_grub.cfg)
*   [11 Múltiples entradas](#M.C3.BAltiples_entradas)
    *   [11.1 Desactivar submenú](#Desactivar_submen.C3.BA)
    *   [11.2 Recordar el último sistema arrancado](#Recordar_el_.C3.BAltimo_sistema_arrancado)
    *   [11.3 Cambiar la entrada por defecto del menú](#Cambiar_la_entrada_por_defecto_del_men.C3.BA)
    *   [11.4 Efectuar el arranque de una entrada no predeterminada por una sola vez](#Efectuar_el_arranque_de_una_entrada_no_predeterminada_por_una_sola_vez)
*   [12 Tocar una melodía](#Tocar_una_melod.C3.ADa)
*   [13 Configuración manual de la imagen del núcleo para un arranque rápido](#Configuraci.C3.B3n_manual_de_la_imagen_del_n.C3.BAcleo_para_un_arranque_r.C3.A1pido)
*   [14 Lecturas adicionales de UEFI](#Lecturas_adicionales_de_UEFI)
    *   [14.1 Método de instalación alternativo](#M.C3.A9todo_de_instalaci.C3.B3n_alternativo)
    *   [14.2 Solución al firmware de UEFI](#Soluci.C3.B3n_al_firmware_de_UEFI)
    *   [14.3 Crear una entrada GRUB en el gestor de arranque del firmware](#Crear_una_entrada_GRUB_en_el_gestor_de_arranque_del_firmware)
    *   [14.4 GRUB independiente](#GRUB_independiente)
    *   [14.5 Información técnica](#Informaci.C3.B3n_t.C3.A9cnica)

## Métodos alternativos de instalación

### Instalar en un dispositivo USB externo

#### BIOS

Supongamos que la primera partición de su memoria USB es FAT32 y su partición es /dev/sdy1

```
# mkdir -p /mnt/usb
# mount /dev/sdy1 /mnt/usb
# grub-install --target=i386-pc --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

Opcionalmente puede hacer una copia de seguridad de `grub.cfg`:

```
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
# sync; umount /mnt/usb

```

#### EFI

Para que grub escriba su imagen EFI en `/boot/efi/EFI/BOOT/BOOTX64.efi`, y el firmware de arranque sea capaz de encontrarlo sin ninguna entrada de arranque UEFI, use `--removable` cuando ejecute `grub-install`.

### Instalar en un disco con o sin particiones

**Advertencia:** GRUB **desaconseja encarecidamente** su instalación en un sector de arranque de partición o un disco sin particiones como lo hace GRUB Legacy o Syslinux. Esta configuración es propensa a romperse, especialmente durante las actualizaciones, y **no es soportada** por los desarrolladores de Arch.

Para configurar grub en un sector de inicio de partición, en un disco sin particiones (también llamado superfloppy) o en un disquete, ejecútelo (utilizando, por ejemplo`/dev/sdaX` como la partición `/boot`):

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

**Nota:**

*   `/dev/sdaX` se utiliza sólo como ejemplo.
*   `--target=i386-pc` indica a `grub-install` que se instale sólo para sistemas BIOS. Se recomienda utilizar siempre esta opción para eliminar la ambigüedad en *grub-install*.

Debe usar la opción `--force` para permitir el uso de listas de bloqueo (blocklists) y no debería usar `--grub-setup=/bin/true` (que es similar a simplemente generar `core.img`).

`grub-install` dará advertencias y le darán una idea de lo que podría fallar con este enfoque:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

Sin `--force` puede obtener el siguiente error y `grub-setup` no configurará su código de arranque en el sector de arranque de la partición:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

Con `--force` debería obtener:

```
Installation finished. No error reported.

```

La razón por la que `grub-setup` no lo permite por defecto es que en caso de partición o disco sin particiones GRUB confía en las listas de bloques integradas en el sector de arranque de la partición para localizar el archivo `/boot/grub/i386-pc/core.img` y el directorio de prefijos `/boot/grub` . Las ubicaciones de sector de `core.img` pueden cambiar cada vez que se altere el sistema de archivos de la partición (archivos copiados, eliminados, etc.). Para más información, véase [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) y [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

La solución es establecer el indicador invariable en `/boot/grub/i386-pc/core.img`. (usando el comando `chattr`} como se mencionó anteriormente) para que las ubicaciones de sector del archivo `core.img` en el disco no se alteren. El indicador invariable en `/boot/grub/i386-pc/core.img` sólo debe configurarse si GRUB está instalado en un sector de arranque de partición o en un disco sin particiones, no en el caso de la instalación en MBR o la simple generación de `core.img` sin integrar ningún sector de arranque (mencionado anteriormente).

Desafortunadamente, el archivo `grub.cfg` que se crea no contendrá el UUID apropiado para iniciar, incluso si no hay informe de errores.Vea [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604). Para solucionar este problema, ejecute los siguientes comandos:

```
# mount /dev/sdxY /mnt        #Your root partition.
# mount /dev/sdxZ /mnt/boot   #Your boot partition (if you have one).
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Generar sólo core.img

Para completar el directorio `/boot/grub` y generar un `/boot/grub/i386-pc/core.img` **sin** incorporar ningún código de sector de inicio GRUB en el MBR, región post-MBR o partición del sector de arranque, agregue `--grub-setup=/bin/true` a `grub-install`:

```
# grub-install --target=i386-pc --grub-setup=/bin/true --debug /dev/sda

```

**Nota:**

*   `/dev/sda` usado sólo como ejemplo.
*   `--target=i386-pc` ordena a `grub-install` a instalar solo para sistemas BIOS. Se recomienda utilizar siempre esta opción para eliminar la ambigüedad en grub-install.

A continuación, puede encadenar GRUB `core.img` de GRUB Legacy o syslinux como kernel de Linux o como núcleo de arranque múltiple (consulte también [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)")).

## Herramientas GUI de configuración

Es posible obtener estas herramientas gráficas instalando los siguientes paquetes:

*   **grub-customizer** — Para personalizar el gestor de arranque (GRUB o BURG)

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor-frameworks** — Un módulo de control de KDE para configurar el gestor de arranque GRUB2\. *Port* no oficial KF5

	[https://github.com/maz-1/grub2-editor](https://github.com/maz-1/grub2-editor) || [grub2-editor-frameworks](https://aur.archlinux.org/packages/grub2-editor-frameworks/)

*   **startupmanager** — Aplicación gráfica para cambiar la configuración de GRUB Legacy, GRUB, Usplash y Splashy ([abandonned](https://launchpad.net/startup-manager/+announcement/8300))

	[http://sourceforge.net/projects/startup-manager/](http://sourceforge.net/projects/startup-manager/) || [startupmanager](https://aur.archlinux.org/packages/startupmanager/)

## Configuración del aspecto

En GRUB puede cambiar el aspecto del menú. Asegúrese de haber inicializado el terminal gráfico de GRUB (gfxterm), utilizando una modalidad de vídeo adecuado (gfxmode). Para más información se puede consultar este [apartado](/index.php/GRUB_(Espa%C3%B1ol)#Corregir_el_error_de_GRUB:_.C2.ABno_suitable_mode_found.C2.BB "GRUB (Español)"). La modalidad de vídeo establecida a continuación, se pasará al kernel a través de «gfxpayload», por lo tanto, esta solicitud asegurará que cada configuración del aspecto tenga efecto.

### Ajustar la resolución del framebuffer

GRUB permite ajustar el framebuffer tanto para él mismo como para el kernel. El antiguo parámetro `vga=` está en desuso. El método recomendado es modificar `/etc/default/grub` de la siguiente manera:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep
```

Se pueden especificar múltiples resoluciones, incluyendo la opción `auto` por defecto, por lo que es recomendable que modifique la línea en cuestión, de modo que quede como esta `GRUB_GFXMODE=<resolución deseada>,<para fallback 1024x768>,auto`. Para obtener más información, remítase a [the GRUB gfxmode documentation](https://www.gnu.org/software/grub/manual/html_node/gfxmode.html#gfxmode). La propiedad [gfxpayload](https://www.gnu.org/software/grub/manual/html_node/gfxpayload.html#gfxpayload) se asegurará de que el kernel mantiene la resolución.

**Nota:**

*   Solo las modalidades soportadas por la tarjeta gráfica a través de [VESA BIOS Extensions (VBE)](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions "wikipedia:VESA BIOS Extensions") pueden ser utilizadas. Para ver la lista de las modalidades compatibles, instale [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) y ejecute `hwinfo --framebuffer` como root. Como alternativa, entre en la línea de órdenes de GRUB y ejecute la orden `videoinfo`.
*   Las versiones anteriores del driver propietario [NVIDIA](/index.php/NVIDIA "NVIDIA") (probado con GeForce GTX 970, driver: nvidia 370) admite `GRUB_GFXMODE` en formato `*<width>*x*<height>*-*<depth>*` (e.g. `1920x1200-24`, pero no `1920x1200x24`). Esto no parece aplicarse a las nuevas tarjetas y controladores. Las tarjetas Pascal con controladores más recientes (probadas con GeForce GTX 1060 y nvidia 381.22) no funcionarán con el formato sugerido, por lo que si se intenta utilizarlas se producirán graves problemas, entre los que se incluyen, sin limitarse a ellos, caídas del sistema y bloqueos de hardware. El controlador y las tarjetas actuales se configuran mejor con `GRUB_GFXMODE` en el formato estándar `*<width>*x*<height>*x*<depth>*`.
*   Asegúrese de ejecutar `grub-mkconfig -o /boot/grub/grub.cfg` después de realizar cambios.

Si este método falla, la antigua opción `vga=` sigue siendo válida. Añadimos `vga=` a la opción `"GRUB_CMDLINE_LINUX_DEFAULT="` en `/etc/default/grub`. Por ejemplo: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` establece una resolución de `1024x768`

### Introducir 915resolution

Si está usando tarjeta de vídeo de Intel, puede ocurrir que ni `# hwinfo --framebuffer` ni `vbeinfo` muestre la resolución deseada. En este caso, puede utilizar este arreglo, para cambiar temporalmente la BIOS de la tarjeta de vídeo mediante la adición de la resolución requerida. Consulte la página [915resolution](http://915resolution.mango-lang.org/).El paquete se puede encontrar aquí: [915resolution](https://aur.archlinux.org/packages/915resolution/)

En primer lugar, debe elegir un modo de vídeo para editar más tarde. Para ello necesitamos utilizar la shell de órdenes de GRUB:

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

La orden antes descrita sobreescribirá `Mode 30` con la resolución de `1440x900`.

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Línea insertada**
set gfxmode=${GRUB_GFXMODE}
[...]

```

Ahora tendrá que establecer el valor en `GRUB_GFXMODE`, como se explicó anteriormente, reconstruya el archivo `grub.cfg` y reinicie para comprobar los cambios.

### Imagen de fondo y fuentes bitmap

GRUB es compatible con imágenes de fondo y fuentes de mapa de bits en el formato `pf2`. La fuente unifont está incluida en el paquete [grub](https://www.archlinux.org/packages/?name=grub) con el nombre `unicode.pf2` o, solo para carácteres ASCII, con el nombre `ascii.pf2`.

Los formatos de imagen soportados incluyen tga, png e jpeg, siempre que los respectivos módulos se carguen. La resolución máxima aplicable depende del hardware en uso.

Antes de continuar, siga las disposiciones indicadas en [resolución del framebuffer](#Ajustar_la_resoluci.C3.B3n_del_framebuffer).

A continuación, edite el archivo `/etc/default/grub` como sigue:

```
GRUB_BACKGROUND="/boot/grub/mi_imagen"
#GRUB_THEME="/ruta/a/gfxtheme"
GRUB_FONT="/ruta/a/font.pf2"

```

**Nota:** Si ha instalado GRUB en una partición separada, `/boot/grub/mi_imagen` automáticamente se convierte en `/grub/mi_imagen` en `grub.cfg`.

[Regenere](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuraci.C3.B3n_principal "GRUB (Español)") `grub.cfg` para aplicar los cambios. Si la inserción de la imagen se realiza correctamente, debería ver el mensaje `Found background image...`, al ejecutar la orden anterior. Si no, quiere decir que la imagen no se ha incorporado en el archivo `grub.cfg`.

En este caso, compruebe que:

*   La ruta y el nombre de la imagen en `/etc/default/grub` es correcta.
*   La imagen tiene un tamaño y formato adecuados (tga, png, jpg a 8 bits).
*   La imagen se guarda en modo RGB y no indexado.
*   La modalidad consola no está habilitada en el archivo `/etc/default/grub`.
*   La orden de `grub-mkconfig` se ha hecho para poner la información relativa en un segundo plano en el archivo `/boot/grub/grub.cfg`.
*   Los scripts `grub-mkconfig` no harán referencia al nombre del archivo en `grub.cfg` si contienen espacios , así que asegúrese de que no los tiene

### Temas

A continuación se muestra un ejemplo para la configuración propuesta con el tema Starfield, incluido en el paquete suministrado con Arch.

Modifique `/etc/default/grub`:

```
GRUB_THEME="/boot/grub/themes/starfield/theme.txt"

```

[Regenere](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuraci.C3.B3n_principal "GRUB (Español)") `grub.cfg` para aplicar los cambios. Si el tema se ha configurado correctamente, aparecerá en el terminal el mensaje `Found theme: /boot/grub/themes/starfield/theme.txt`.

La imagen de fondo, por lo general, no se visualiza cuando se utiliza un tema.

### Colores del menú

Como sucedía con GRUB Legacy, se pueden cambiar los colores del menú de GRUB. La lista de colores disponibles se pueden encontrar [aquí](http://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format). A continuación, un ejemplo:

Modifique `/etc/default/grub` de la siguiente manera:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

### Menú oculto

Una de las características de GRUB es la capacidad de ocultar el menú y hacer que sea visible pulsando la tecla `Esc`, si es necesario. También puede decidir si se debe mostrar la cuenta atrás.

Modifique el archivo `/etc/default/grub` como sigue. Estas son las líneas que hay que añadir para activar esta función, la cuenta atrás se establece en 5 segundos y se hace visible para el usuario:

```
GRUB_TIMEOUT=5
GRUB_TIMEOUT_STYLE='countdown'

```

GRUB_TIMEOUT es usado para indicar cuántos segundos tardará en mostrase el menú.

### Desactivar framebuffer

Si utiliza el controlador propietario de NVIDIA, puede que tenga que desactivar el framebuffer de GRUB, ya que podría interferir con el controlador.

Para desactivarlo, edite `/etc/default/grub` y descomente la siguiente línea:

```
GRUB_TERMINAL_OUTPUT=console

```

Otra opción, si desea conservar el framebuffer para GRUB, es revertir al modo de texto justo antes de iniciarse el kernel. Para conseguir esto, modifique la variable en `/etc/default/grub`:

```
GRUB_GFXPAYLOAD_LINUX=text

```

## Iniciar una imagen ISO9660 directamente desde GRUB

GRUB soporta el arranque de imágenes ISO directamente a través de dispositivos loopback, véase [Multiboot USB drive#Using GRUB and loopback devices](/index.php/Multiboot_USB_drive#Using_GRUB_and_loopback_devices "Multiboot USB drive") para obtener ejemplos.

## Nomenclatura permanente de dispositivos de bloque

Un esquema de nomenclatura de [nombres persistentes para dispositivos de bloque](/index.php/Persistent_block_device_naming "Persistent block device naming") es usar UUID, que son únicos y globales, para detectar particiones, en lugar de la «vieja» nomenclatura `/dev/sd*`. Las ventajas de este método están tratadas en el artículo anteriormente enlazado.

La nomenclatura persistente a través de las UUID del sistema de archivos se utiliza por defecto en GRUB.

**Nota:** El archivo `/boot/grub.cfg` necesita regenerarse con las UUID nuevas en `/etc/default/grub` cada vez que se redimensiona o se formatea una partición. Recuerde esto al modificar las particiones y sistemas de archivos con un CD-Live.

Cuando se usan las UUID son controladas por una opción en `/etc/default/grub`:

 `# GRUB_DISABLE_LINUX_UUID=true` 

## Utilizar etiquetas

Puede utilizar las etiquetas (cadenas que identifican particiones de una manera legible por el usuario), usando la opción `--label` con la orden `search`. En primer lugar, coloque una etiqueta a las particiones:

```
# tune2fs -L *ETIQUETA DE LA PARTICIÓN*

```

A continuación, agregue una entrada usando la etiqueta. He aquí un ejemplo:

```
menuentry "Arch Linux, session texte" {
 search --label --set=root archroot
 linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
 initrd /boot/initramfs-linux.img
}

```

## Proteger con contraseña el menú de GRUB

**Advertencia:** Si alguien tiene acceso físico a su máquina y es capaz de arrancar un disco/USB live (BIOS permite arrancar desde un disco externo), es bastante trivial que se modifiquen los archivos de configuración de GRUB para evitar esto si `/boot` reside en una partición no cifrada. Ver [#Encriptación](/index.php/GRUB_(Espa%C3%B1ol)#Encriptaci.C3.B3n "GRUB (Español)") y [Security#Disk encryption](/index.php/Security#Disk_encryption "Security").

Si desea hacer GRUB más seguro, de modo que nadie pueda cambiar los parámetros de arranque o utilizar la línea de órdenes, puede agregar un nombre de usuario y contraseña para los archivos de configuración de GRUB. Para ello, ejecute `grub-mkpasswd_pbkdf2`. Es necesario introducir una contraseña y confirmarla:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

Después, añada las siguientes cadenas a `/etc/grub.d/40_custom`:

 `/etc/grub.d/40_custom` 
```
set superusers="**nombreusuario**"
password_pbkdf2 **nombreusuario** **<contraseña>**

```

Donde `<contraseña>` corresponde a la cadena generada por `grub-mkpasswd_pbkdf2`.

Hay que regenerar el archivo de configuración. La línea de órdenes y los parámetros de arranque de grub ahora estarán protegidos.

Los ajustes anteriores se pueden hacer menos restrictivos y personalizar mediante la adición de más usuarios, como se explica en el capítulo sobre «Seguridad» del [manual de GRUB](https://www.gnu.org/software/grub/manual/grub.html#Security).

### Protección con contraseña sólo para las opciones de edición y consola de GRUB

Añadiendo `--unrestricted` a la entrada de menú permitirá a cualquier usuario arrancar el sistema operativo , al tiempo que se evita que el usuario edite la entrada y el acceso a la consola de comandos *grub*. Sólo un superusuario o usuarios especificos con el modificador `--user` podrán editar la entrada del menú.

 `/boot/grub/grub.cfg`  `menuentry 'Arch Linux' --unrestricted --class arch --class gnu-linux --class os ...` 

## Ocultar GRUB y hacerlo aparecer mediante la tecla Mayús

Para reducir al mínimo el tiempo de arranque es posible ocultar el menú de GRUB durante el tiempo de espera, lo que permite a GRUB ocultar el menú, haciéndolo aparecer unicamente cuando se presione la tecla `Mayús` durante la fase de inicio de GRUB.

Para obtener este comportamiento, añada lo que sigue al archivo `/etc/default/grub`:

```
 GRUB_FORCE_HIDDEN_MENU="true"

```

A continuación cree el archivo [[1]](https://gist.githubusercontent.com/anonymous/8eb2019db2e278ba99be/raw/257f15100fd46aeeb8e33a7629b209d0a14b9975/gistfile1.sh), haga ejecutable el archivo y después regenere el archivo de configuración de grub:

```
# chmod a+x /etc/grub.d/31_hold_shift
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** Esta configuración utiliza el estado de las teclas para detectar el evento de pulsación de las mismas, por lo que es posible que no funcione en algunas máquinas la tecla Mayús, debido a la distribución del teclado,eS posible que funcione con otras.

## Combinar la utilización de UUID con scripts

Si desea utilizar la asignación de UUID para superar los mapeados poco fiables de los dispositivos realizadas por la BIOS, o si está teniendo dificultades con la sintaxis de GRUB, aquí hay un ejemplo que utiliza las UUID y un pequeño script para GRUB, para que apunte a las particiones correspondientes. Todo lo que uno debe hacer, es sustituir el ejemplo con las UUID correctas para su sistema (el ejemplo se aplica a sistemas con una partición de arranque separada y debe modificarse en consecuencia en caso de particiones adicionales).

```
 menuentry "Arch Linux 64" {
         # Set the UUIDs for your boot and root partition respectively
         set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07
         set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

         # (Note: This may be the same as your boot partition)

         # Get the boot/root devices and set them in the root and grub_boot variables
         search --fs-uuid $the_root_uuid --set=root
         search --fs-uuid $the_boot_uuid --set=grub_boot

         # Check to see if boot and root are equal.
         # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
         if [ $the_boot_uuid == $the_root_uuid ] ; then
             set grub_boot=($grub_boot)/boot
         else
             set grub_boot=($grub_boot)
         fi

         # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
         linux $grub_boot/vmlinuz-linux root=/dev/disk/by-uuid/$the_root_uuid ro
         initrd $grub_boot/initramfs-linux.img
 }

```

## Creación manual de grub.cfg

**Advertencia:** El archivo grub.cfg es generado por la orden `grub-mkconfig`, lo cual es preferible a editar el archivo `/etc/default /grub` o uno de los scripts contenidos en el directorio `/etc/grub.d.`

Un archivo `grub.cfg` básico contendrá las siguientes opciones:

*   `(hd*X*,*Y*)` indica la partición Y en el disco X. La numeración de partición comienza en 1, mientras que la del disco comienza en 0
*   `set default=*N*` le permite elegir qué entrada se inicia por defecto
*   `set timeout=*M*` indica el límite de tiempo en segundos antes que la elección predefinida se inicie
*   `menuentry "title" {opciones de entrada}` es una entrada de arranque con nombres `title`
*   `set root=(hd*X*,*Y*)` establece la partición de arranque, es decir, la que contiene el kernel y los módulos de GRUB (no es necesario una partición `/boot` separada, puede estar contenida como un deirecorio dentro de la partición root `/`).

## Múltiples entradas

### Desactivar submenú

Si tiene varios kernels instalados, por ejemplo linux y linux-lts, por defecto `grub-mkconfig` los agrupa en un submenú. Si no le gusta este comportamiento se puede volver a un solo menú, añadiendo la siguiente línea a `/etc/default/grub`:

```
 GRUB_DISABLE_SUBMENU=y

```

### Recordar el último sistema arrancado

GRUB puede recordar el último sistema arrancado y utilizarlo por defecto la próxima vez que ejecute el arranque. Esta característica es útil si tiene varios kernels (por ejemplo, el kernel actual de Arch y el LTS como fallback) o más sistemas operativos. Modifique `/etc/default/grub` y cambie el valor de `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

Esto permitirá que GRUB arranque el sistema operativo guardado. Para activar la recuperación de la entrada seleccionada, añada la siguiente línea a `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

**Nota:** La entradas del menú añadidas manualmente a `/etc/grub.d/40_custom` o `/boot/grub/custom.cfg` (para Windows, por ejemplo) necesitan ir acompañadas de la opción `savedefault`.

### Cambiar la entrada por defecto del menú

Para cambiar la entrada seleccionada por defecto, edite `/etc/default/grub` y cambie el valor de `GRUB_DEFAULT`:

Utilizar números :

```
GRUB_DEFAULT="1>2"

```

Grub identifica las entradas generadas en el menú contando desde cero. Eso significa que 0 se refiere a la primera entrada, la cual es el valor predeterminado, 1 para la segunda y así sucesivamente.Las entradas del menú principal y de los submenús están separadas por `>`.

El ejemplo anterior arranca la tercera entrada desde el menú principal 'Opciones avanzadas para Arch Linux'.

O usar títulos de menú :

```
GRUB_DEFAULT='Arch Linux, with Linux core repo kernel'

```

### Efectuar el arranque de una entrada no predeterminada por una sola vez

La orden `grub-reboot` es muy útil para arrancar otra entrada distinta de la predeterminada solo por una vez. GRUB carga la entrada especificada como primer argumento de la orden, de modo que la próxima vez, cuando el sistema reinicie, arrancará el sistema operativo indicado. Lo más importante es que GRUB vuelve a cargar la entrada por defecto para todos los sucesivos arranques. Por tanto, no es necesario cambiar el archivo de configuración o seleccionar una entrada en el menú de GRUB.

**Nota:** Esta operación requiere la opción `GRUB_DEFAULT=saved` en `/etc/default/grub` (y después regenerar el archivo `grub.cfg`) o, en el caso de un archivo `grub.cfg` configurado manualmente, la línea `set default="${saved_entry}"`.

## Tocar una melodía

Puede reproducir una melodía a través del altavoz del PC mientras arranca modificando la variable `GRUB_INIT_TUNE`. Por ejemplo, para tocar el extracto de *Berlioz de Sabbath Night of Symphonie Fantastique* se puede añadir lo siguiente: (parte bassoon):

`GRUB_INIT_TUNE="312 262 3 247 3 262 3 220 3 247 3 196 3 220 3 220 3 262 3 262 3 294 3 262 3 247 3 220 3 196 3 247 3 262 3 247 5 220 1 220 5"`

Para obtener información al respecto, puede consultar `info grub -n play`.

## Configuración manual de la imagen del núcleo para un arranque rápido

Si necesita un mapa de teclado especial u otros pasos complejos que GRUB no puede configurar automáticamente para hacer que `/boot` esté disponible para el entorno GRUB, puede generar una imagen del núcleo usted mismo. En los sistemas UEFI, la imagen del núcleo es el archivo `grubx64.efi` que carga el firmware de arranque. La creación de su propia imagen del núcleo le permitirá integrar cualquier módulo necesario para un inicio muy rápido, así como una secuencia de comandos de configuración para arrancar GRUB.

En primer lugar, tomando como ejemplo un requisito para el mapa de teclado `dvorak` integrado en el booteo-rápido en orden para ingresar una contraseña para encriptar `/boot` en un sistema UEFI:

Determine a partir del archivo generado `/boot/grub/grub.cfg` qué módulos son necesarios para montar el `/boot` encriptado. Por ejemplo, debajo de su entrada `menuentry` debería ver líneas similares a:

```
insmod diskfilter cryptodisk luks gcry_rijndael gcry_rijndael gcry_sha256
insmod ext2
cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
```

Tome nota de todos esos módulos: deberán incluirse en la imagen del núcleo. Ahora, cree un tarball que contenga su mapa de teclado. Esto se incluirá en la imagen del núcleo como un *memdisk*:

```
# ckbcomp dvorak | grub-mklayout > dvorak.gkb
# tar cf memdisk.tar dvorak.gkb

```

Ahora cree un archivo de configuración para utilizarlo en la imagen del núcleo de GRUB. Este está en el mismo formato que su configuración normal de grub, pero sólo necesita contener unas pocas líneas para encontrar y cargar el archivo de configuración principal en la partición `/boot`:

 `early-grub.cfg` 
```
root=(memdisk)
prefix=($root)/

terminal_input at_keyboard
keymap /dvorak.gkb

cryptomount -u 1234abcdef1234abcdef1234abcdef
set root='cryptouuid/1234abcdef1234abcdef1234abcdef'
set prefix=($root)/grub

configfile grub.cfg
```

Finalmente, genere la imagen principal, enumerando todos los módulos que se determinan necesarios en el `grub.cfg`, junto con cualquier módulo utilizado en el script `early-grub.cfg`. El ejemplo anterior necesita `memdisk`, `tar`, `at_keyboard`, `keylayouts` y `configfile`.

```
# grub-mkimage -c early-grub.cfg -o grubx64.efi -O x86_64-efi -m memdisk.tar diskfilter cryptodisk luks gcry_rijndael gcry_sha256 ext2 memdisk tar at_keyboard keylayouts configfile

```

La imagen del núcleo de EFI generada ahora se puede usar de la misma manera que la imagen que se genera automáticamente mediante `grub-install`: colóquela en su partición EFI y habilítela con `efibootmgr`, o configúrela según corresponda para el firmware de su sistema.

## Lecturas adicionales de UEFI

A continuación encontrará otra información relevante sobre la instalación de Arch a través de UEFI.

### Método de instalación alternativo

Normalmente, GRUB guarda todos los archivos, incluidos los de configuración, en `/boot`, independientemente de dónde esté montada la partición de sistema EFI.

Si desea mantener estos archivos dentro de la propia partición del sistema EFI, añada `--boot-directory=*esp*` al comando grub-install:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=grub --boot-directory=*esp* --debug

```

Esto pone todos los archivos GRUB en `*esp*/grub`, en lugar de en `/boot/grub`. Cuando utilice este método, asegúrese de que *grub-mkconfig* ha puesto el archivo de configuración en el mismo lugar:

```
# grub-mkconfig -o *esp*/grub/grub.cfg

```

Por lo demás, la configuración es la misma.

### Solución al firmware de UEFI

Algunos firmware UEFI requieren que el código de arranque *.efi* tenga un nombre específico y se coloque en una ubicación específica: `*esp*/EFI/boot/bootx64.efi` (donde `*esp*` es el punto de montaje de la partición UEFI). De lo contrario, en estos casos, la instalación no se podrá iniciar. Afortunadamente, esto no causará ningún problema con otro firmware que no lo requiera..

Para ello, primero cree el directorio necesario y, a continuación, copie la parte de grub `.efi`, renombrándolo en el proceso:

```
# mkdir *esp*/EFI/boot
# cp *esp*/EFI/grub_uefi/grubx64.efi *esp*/EFI/boot/bootx64.efi

```

### Crear una entrada GRUB en el gestor de arranque del firmware

`grub-install` intenta crear automáticamente una entrada de menú en el gestor de arranque. Si no lo hace, vea [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)") para instrucciones de uso y `efibootmgr` para crear una entrada de menú. Sin embargo, es probable que el problema sea que no haya arrancado su CD/USB en modo UEFI, vea también como [Crear un USB arrancable con UEFI desde la ISO](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Crear_un_USB_arrancable_con_UEFI_desde_la_ISO "Unified Extensible Firmware Interface (Español)").

### GRUB independiente

Esta sección asume que está creando un GRUB independiente para sistemas x86_64 (x86_64-efi). Para los sistemas EFI de 32 bits (IA32), reemplace `x86_64-efi` con `i386-efi` cuando corresponda.

Es posible crear una aplicación `grubx64_standalone.efi` que tenga todos los módulos integrados en un archivo tar dentro de la aplicación UEFI, eliminando así la necesidad de tener un directorio separado con todos los módulos de GRUB UEFI y otros archivos relacionados. Esto se hace usando el comando `grub-mkstandalone` (incluido en [grub](https://www.archlinux.org/packages/?name=grub)) de la siguiente manera:

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg
# grub-mkstandalone -d /usr/lib/grub/x86_64-efi/ -O x86_64-efi --modules="part_gpt part_msdos" --locales="en@quot" --themes="" -o "*esp*/EFI/grub/grubx64_standalone.efi" "boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

A continuación, copie el fichero de configuración de GRUB en `*esp*/EFI/grub/grub.cfg` y cree una entrada UEFI Boot Manager para `*esp*/EFI/grub/grubx64_standalone.efi` usando [efibootmgr](/index.php/UEFI#efibootmgr "UEFI").

**Nota:** La opción `--modules="part_gpt part_msdos"` (con las comillas) es necesaria para que la `${cmdpath}` funcione correctamente.

**Advertencia:** Puede encontrar que el archivo `grub.cfg` no esté cargado debido a que `${cmdpath}` falte una barra oblicua (i.e. `(hd1,msdos2)EFI/Boot` en lugar de `(hd1,msdos2)/EFI/Boot`) y por lo tanto le envie a una shell de GRUB. Si esto sucede, determine lo que está configurado en (`echo ${cmdpath}` ) y, a continuación, carge el archivo de configuración manualmente (por ejemplo, `configfile (hd1,msdos2)/EFI/Boot/grub.cfg`).

### Información técnica

El archivo GRUB EFI siempre espera que su archivo de configuración esté en `${prefix}/grub.cfg`. Sin embargo, en el archivo independiente de GRUB EFI, el `${prefix}` se encuentra dentro de un archivo tar e integrado dentro del propio archivo EFI de GRUB (dentro del entorno GRUB, se indica con `"(memdisk)"`, sin comillas). Este archivo tar contiene todos los archivos que se almacenarían normalmente en `/boot/grub` en caso de una instalación normal de GRUB EFI.

A causa del empaquetamiento de los contenidos de `/boot/grub` dentro de la imagen independiente, no depende del `/boot/grub` (externo) para nada. Por lo tanto, en el caso del archivo GRUB EFI independiente `${prefix}==(memdisk)/boot/grub` y las lecturas del archivo GRUB EFI esperan que el archivo de configuración esté en `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`.

Por lo tanto, para asegurarnos de que el archivo EFI de GRUB independiente , lee el `grub.cfg` externo ubicado en el mismo directorio que el archivo EFI (dentro del entorno GRUB, está indicado por `${cmdpath}` ), creamos un simple `/tmp/grub.cfg` que encarga a GRUB a usar `${cmdpath}/grub.cfg` como su configuración (`configfile ${cmdpath}/grub.cfg` ordenado en `(memdisk)/boot/grub/grub.cfg`). A continuación, le pedimos a *grub-mkstandalone* que copie este archivo `/tmp/grub.cfg` en `${prefix}/grub.cfg` (que en realidad es `(memdisk)/boot/grub/grub.cfg`) utilizando la opción `"boot/grub/grub.cfg=/tmp/grub.cfg"`.

De esta forma, el archivo independiente de GRUB EFI y el archivo actual `grub.cfg` pueden almacenarse en cualquier directorio dentro de la partición del sistema EFI (siempre que estén en el mismo directorio), haciéndolos portátiles.
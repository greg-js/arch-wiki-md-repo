**Estado de la traducción:** este artículo es una versión traducida de [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks"). Fecha de la última traducción/revisión: **2015-06-23**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=GRUB/Tips_and_tricks&diff=0&oldid=375290).

Véa el artículo principal [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)").

## Contents

*   [1 Herramientas GUI de configuración](#Herramientas_GUI_de_configuraci.C3.B3n)
*   [2 Configuración del aspecto](#Configuraci.C3.B3n_del_aspecto)
    *   [2.1 Ajustar la resolución del framebuffer](#Ajustar_la_resoluci.C3.B3n_del_framebuffer)
    *   [2.2 Introducir 915resolution](#Introducir_915resolution)
    *   [2.3 Imagen de fondo y fuentes bitmap](#Imagen_de_fondo_y_fuentes_bitmap)
    *   [2.4 Temas](#Temas)
    *   [2.5 Colores del menú](#Colores_del_men.C3.BA)
    *   [2.6 Menú oculto](#Men.C3.BA_oculto)
    *   [2.7 Desactivar framebuffer](#Desactivar_framebuffer)
*   [3 Iniciar una imagen ISO9660 directamente desde GRUB](#Iniciar_una_imagen_ISO9660_directamente_desde_GRUB)
*   [4 Nomenclatura permanente de dispositivos de bloque](#Nomenclatura_permanente_de_dispositivos_de_bloque)
*   [5 Utilizar etiquetas](#Utilizar_etiquetas)
*   [6 Proteger con contraseña el menú de GRUB](#Proteger_con_contrase.C3.B1a_el_men.C3.BA_de_GRUB)
*   [7 Ocultar GRUB y hacerlo aparecer mediante la tecla Mayús](#Ocultar_GRUB_y_hacerlo_aparecer_mediante_la_tecla_May.C3.BAs)
*   [8 Combinar la utilización de UUID con scripts](#Combinar_la_utilizaci.C3.B3n_de_UUID_con_scripts)
*   [9 Creación manual de grub.cfg](#Creaci.C3.B3n_manual_de_grub.cfg)
*   [10 Múltiples entradas](#M.C3.BAltiples_entradas)
    *   [10.1 Desactivar submenú](#Desactivar_submen.C3.BA)
    *   [10.2 Recordar el último sistema arrancado](#Recordar_el_.C3.BAltimo_sistema_arrancado)
    *   [10.3 Cambiar la entrada por defecto del menú](#Cambiar_la_entrada_por_defecto_del_men.C3.BA)
    *   [10.4 Efectuar el arranque de una entrada no predeterminada por una sola vez](#Efectuar_el_arranque_de_una_entrada_no_predeterminada_por_una_sola_vez)

## Herramientas GUI de configuración

Es posible obtener estas herramientas gráficas instalando los siguientes paquetes:

*   **grub-customizer** — Para personalizar el gestor de arranque (GRUB o BURG)

	[https://launchpad.net/grub-customizer](https://launchpad.net/grub-customizer) || [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/)

*   **grub2-editor** — Módulo de control de KDE4 para configurar el gestor de arrranque GRUB

	[http://kde-apps.org/content/show.php?content=139643](http://kde-apps.org/content/show.php?content=139643) || [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

*   **startupmanager** — Aplicación gráfica para cambiar la configuración de GRUB Legacy, GRUB, Usplash y Splashy

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

**Nota:** Solo las modalidades soportadas por la tarjeta gráfica a través de [VESA BIOS Extensions (VBE)](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions "wikipedia:VESA BIOS Extensions") pueden ser utilizadas. Para ver la lista de las modalidades compatibles, instale [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) y ejecute `hwinfo --framebuffer` como root. Como alternativa, entre en la línea de órdenes de GRUB y ejecute la orden `vbeinfo`.

Si este método falla, la antigua opción `vga=` sigue siendo válida. Añadimos `vga=` a la opción `"GRUB_CMDLINE_LINUX_DEFAULT="` en `/etc/default/grub`. Por ejemplo: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` establece una resolución de `1024x768`

### Introducir 915resolution

Si está usando tarjeta de vídeo de Intel, puede ocurrir que ni `# hwinfo --framebuffer` ni `vbeinfo` muestre la resolución deseada. En este caso, puede utilizar este arreglo, para cambiar temporalmente la BIOS de la tarjeta de vídeo mediante la adición de la resolución requerida. Consulte la página [915resolution](http://915resolution.mango-lang.org/).

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

Antes de continuar, siga las disposiciones indicadas en [este apartado](/index.php/GRUB2_(Espa%C3%B1ol)#Ajustar_la_resoluci.C3.B3n_del_framebuffer "GRUB2 (Español)").

A continuación, edite el archivo `/etc/default/grub` como sigue:

```
GRUB_BACKGROUND="/boot/grub/mi_imagen"
#GRUB_THEME="/ruta/a/gfxtheme"
GRUB_FONT="/ruta/a/font.pf2"

```

**Nota:** Si va a instalar GRUB en una partición separada, `/boot/grub/mi_imagen` se convierte en `/grub/mi_imagen`

[Regenere](#Generar_el_archivo_de_configuraci.C3.B3n_principal) `grub.cfg` para aplicar los cambios. Si la inserción de la imagen se realiza correctamente, debería ver el mensaje `Found background image...`, al ejecutar la orden anterior. Si no, quiere decir que la imagen no se ha incorporado en el archivo `grub.cfg`.

En este caso, compruebe que:

*   La ruta y el nombre de la imagen en `/etc/default/grub` es correcta.
*   La imagen tiene un tamaño y formato adecuados (tga, png, jpg a 8 bits).
*   La imagen se guarda en modo RGB y no indexado.
*   La modalidad consola no está habilitada en el archivo `/etc/default/grub`.
*   La orden de `grub-mkconfig` se ha hecho para poner la información relativa en un segundo plano en el archivo `/boot/grub/grub.cfg`.

### Temas

A continuación se muestra un ejemplo para la configuración propuesta con el tema Starfield, incluido en el paquete suministrado con Arch.

Modifique `/etc/default/grub`:

```
GRUB_THEME="/boot/grub/themes/starfield/theme.txt"

```

[Regenere](#Generar_el_archivo_de_configuraci.C3.B3n_principal) `grub.cfg` para aplicar los cambios. Si el tema se ha configurado correctamente, aparecerá en el terminal el mensaje `Found theme: /boot/grub/themes/starfield/theme.txt`.

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

Si desea hacer GRUB más seguro, de modo que nadie pueda cambiar los parámetros de arranque o utilizar la línea de órdenes, puede agregar un nombre de usuario y contraseña para los archivos de configuración de GRUB. Para ello, ejecute `grub-mkpasswd_pbkdf2`. Es necesario introducir una contraseña y confirmarla:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

Después, añada las siguientes cadenas a `/etc/grub.d/40_header`:

 `/etc/grub.d/40_header` 
```
set superusers="**nombreusuario**"
password_pbkdf2 **nombreusuario** **<contraseña>**

```

Donde `<contraseña>` corresponde a la cadena generada por `grub-mkpasswd_pbkdf2`.

Hay que regenerar el archivo de configuración. La línea de órdenes y los parámetros de arranque de grub ahora estarán protegidos.

Los ajustes anteriores se pueden hacer menos restrictivos y personalizar mediante la adición de más usuarios, como se explica en el capítulo sobre «Seguridad» del [manual de GRUB](https://www.gnu.org/software/grub/manual/grub.html#Security).

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

Utilizar números consecutivos :

```
GRUB_DEFAULT=0

```

Grub identifica las entradas generadas en el menú contando desde cero. Eso significa que 0 se refiere a la primera entrada, la cual es el valor predeterminado, 1 para la segunda y así sucesivamente.

O utilizar los nombres en el menú :

```
GRUB_DEFAULT='Arch Linux, with Linux core repo kernel'

```

### Efectuar el arranque de una entrada no predeterminada por una sola vez

La orden `grub-reboot` es muy útil para arrancar otra entrada distinta de la predeterminada solo por una vez. GRUB carga la entrada especificada como primer argumento de la orden, de modo que la próxima vez, cuando el sistema reinicie, arrancará el sistema operativo indicado. Lo más importante es que GRUB vuelve a cargar la entrada por defecto para todos los sucesivos arranques. Por tanto, no es necesario cambiar el archivo de configuración o seleccionar una entrada en el menú de GRUB.

**Nota:** Esta operación requiere la opción `GRUB_DEFAULT=saved` en `/etc/default/grub` (y después regenerar el archivo `grub.cfg`) o, en el caso de un archivo `grub.cfg` configurado manualmente, la línea `set default="${saved_entry}"`.
**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – <a class="mw-selflink selflink">Configurar el sistema</a> – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/System_configuration&diff=0&oldid=555873) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Sugerencia:** Si necesita desbloquear de forma remota la raíz u otros sistemas de archivos de arranque temprano (máquinas sin encabezados, servidores distantes ...), siga las instrucciones específicas de [dm-crypt/Specialties (Español)#Desbloqueo remoto de la partición (u otro volumen) raíz](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol)#Desbloqueo_remoto_de_la_partición_(u_otro_volumen)_raíz "Dm-crypt/Specialties (Español)").

## Contents

*   [1 mkinitcpio](#mkinitcpio)
    *   [1.1 Ejemplos](#Ejemplos)
*   [2 Cargador de arranque](#Cargador_de_arranque)
    *   [2.1 Parámetros del Kernel](#Parámetros_del_Kernel)
        *   [2.1.1 root](#root)
        *   [2.1.2 resume](#resume)
    *   [2.2 Utilizar el hook encrypt](#Utilizar_el_hook_encrypt)
        *   [2.2.1 cryptdevice](#cryptdevice)
        *   [2.2.2 cryptkey](#cryptkey)
        *   [2.2.3 crypto](#crypto)
    *   [2.3 Utilizar el hook sd-encrypt](#Utilizar_el_hook_sd-encrypt)
        *   [2.3.1 rd.luks.uuid](#rd.luks.uuid)
        *   [2.3.2 rd.luks.name](#rd.luks.name)
        *   [2.3.3 rd.luks.options](#rd.luks.options)
        *   [2.3.4 rd.luks.key](#rd.luks.key)
        *   [2.3.5 Tiempo de espera («*timeout*»)](#Tiempo_de_espera_(«timeout»))
*   [3 crypttab](#crypttab)
    *   [3.1 Montaje en el momento del arranque](#Montaje_en_el_momento_del_arranque)
        *   [3.1.1 Montaje de un dispositivo de bloque apilado](#Montaje_de_un_dispositivo_de_bloque_apilado)
    *   [3.2 Montaje bajo demanda](#Montaje_bajo_demanda)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 El espacio del sistema en el arranque/solicitud de contraseña no se muestra](#El_espacio_del_sistema_en_el_arranque/solicitud_de_contraseña_no_se_muestra)

## mkinitcpio

Dependiendo de los escenarios particulares, tendrá que activarse un conjunto de los siguientes hooks de [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

| busybox | systemd | Caso de uso |
| `encrypt` | `sd-encrypt` | Siempre necesario cuando se cifra la partición raíz, o una partición que necesita ser montada *antes* de la raíz. No es necesario en todos los demás casos, ya que los scripts de inicialización del sistema como `/etc/crypttab` se encargan de desbloquear otras particiones cifradas. Este enlace debe colocarse *después* del hook `udev` o `systemd`. |
| `keyboard` | Necesario para hacer que los teclados funcionen en el espacio temprano del usuario. |
| `keymap` | `sd-vconsole` | Proporciona soporte para mapas de teclas no estadounidenses para escribir contraseñas de cifrado; debe colocarse *antes* del hook `encrypt`. Configure su mapa de teclas en `/etc/vconsole.conf`, vea [Keyboard configuration in console (Español)#Configuración permanente](/index.php/Keyboard_configuration_in_console_(Espa%C3%B1ol)#Configuración_permanente "Keyboard configuration in console (Español)"). |
| `consolefont` | Carga un titpo de letra de consola alternativo en el espacio temprano del usuario. Configure su tipo de letra en `/etc/vconsole.conf`, vea [Linux console#Persistent configuration](/index.php/Linux_console#Persistent_configuration "Linux console"). |

[Otros hooks](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Hooks_más_comunes "Mkinitcpio (Español)") necesarios deben quedar limpios en otros pasos manuales seguidos durante la instalación del sistema.

Recuerde [regenerar initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)") después de guardar los cambios.

### Ejemplos

He aquí una configuración típica del archivo `/etc/mkinitcpio.conf` utilizando el hook `encrypt`:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base udev autodetect keyboard keymap consolefont modconf block encrypt lvm2 filesystems fsck)
...
```

Aquí una configuración con initramfs basada ​​en systemd utilizando el hook `sd-encrypt`:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base systemd autodetect keyboard sd-vconsole modconf block sd-encrypt sd-lvm2 filesystems fsck)
...
```

## Cargador de arranque

Para activar el arranque de una partición raíz cifrada, es necesario configurar un conjunto de los siguientes parámetros del kernel. Consulte los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener instrucciones específicas para su [cargador de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)").

Por ejemplo, si utiliza [GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Partición_de_arranque "GRUB (Español)"), los parámetros relevantes se añadirán a `/etc/default/grub` antes de [generar el archivo de configuración principal](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuración_principal "GRUB (Español)"). Vea también [GRUB (Español)#Advertencias cuando se instala en entorno chroot](/index.php/GRUB_(Espa%C3%B1ol)#Advertencias_cuando_se_instala_en_entorno_chroot "GRUB (Español)") como otro punto a tener en cuenta al instalar el cargador GRUB.

Los parámetros del kernel que necesita especificar dependen de si está utilizando el hook `encrypt` o `sd-encrypt`.

### Parámetros del Kernel

Los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") como `root` y `resume` se especifican de la misma manera que los hooks `encrypt` y `sd-encrypt`.

#### root

El parámetro `root=` especifica el `*dispositivo*` del sistema de archivos raíz real (descifrado):

```
root=*dispositivo*

```

*   Si el sistema de archivos está formateado directamente en el dispositivo descifrado, este será `/dev/mapper/*nombre_del_dispositivo_mapeado*`.
*   Si un LVM se activa primero y contiene un [volumen lógico raíz cifrado](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system"), el formato anterior se aplica igual.
*   Si el sistema de archivos raíz está contenido en un volumen lógico de un [LVM cifrado](/index.php/Encrypted_LVM "Encrypted LVM"), el mapeador de dispositivos para él vendrá formulado de forma general como `root=/dev/*grupo de volúmenes*/*volumen lógico*`.

**Sugerencia:** No es necesario especificar este parámetro manualmente cuando utiliza [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") y se genera `grub.cfg` con *grub-mkconfig*. Al ejecutar el script *grub-mkconfig*, este determinará el UUID correcto del sistema de archivos descifrado y lo añadirá al archivo `grub.cfg` automáticamente.

#### resume

```
resume=*dispositivo*

```

*   `*dispositivo*` es el dispositivo del sistema de archivos descifrado (espacio de intercambio) utilizado para [suspender en disco](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate"). Si el espacio de intercambio está en una partición separada, lo estará en el formato `/dev/mapper/swap`. Véase también [dm-crypt/Swap encryption (Español)](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)").

### Utilizar el hook encrypt

**Nota:** comparado con el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), `encrypt` tiene algunas limitaciones. No es compatible con:

*   desbloquear [varios discos cifrados](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties") ([FS#23182](https://bugs.archlinux.org/task/23182)). Solo **un** dispositivo se puede desbloquear en initramfs;
*   utilizar un [encabezado LUKS separado](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") ([FS#42851](https://bugs.archlinux.org/task/42851)).

#### cryptdevice

Este parámetro hará que el sistema solicite la contraseña para desbloquear el dispositivo que contiene la raíz cifrada en un [arranque en frío](https://en.wikipedia.org/wiki/es:Arranque_en_fr%C3%ADo "wikipedia:es:Arranque en frío"). Es analizado mediante el hook `encrypt` para identificar qué dispositivo contiene el sistema cifrado:

```
cryptdevice=*dispositivo*:*nombre del dipositivo mapeado*

```

*   `*dispositivo*` es la ruta al dispositivo que contiene al dispositivo cifrado. Se recomienda el uso de [nombres de dispositivos de bloques persistentes](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").
*   `*nombre del dipositivo mapeado*` es el nombre del **d**ispositivo - **m**apeado dado al dispositivo después de descifrarlo, que estará disponible como `/dev/mapper/*nombre del dipositivo mapeado*`.
*   Si un LVM contiene el volúmen [root cifrado](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an entire system (Español)"), el LVM se activa primero y el grupo de volúmenes que contiene el volumen lógico de la raíz cifrada sirve como *dispositivo*. A continuación, lo que sigue al grupo de volúmenes le corresponderá la raíz mapeada. El parámetro sigue el formato siguiente: `cryptdevice=*/dev/nombre_del_grupo_de_volúmenes/nombre_del_volumen_lógico*:*nombre_del_dispositivo_mapeado*`

#### cryptkey

Este parámetro especifica la ubicación de un archivo de claves y es requerido por el hook `*encrypt*` para leer dicho archivo de claves para desbloquear `*cryptdevice*` (a menos que haya una clave en la ubicación por defecto, ver más abajo). Puede tener tres conjuntos de parámetros, dependiendo de si el archivo de claves existe como un archivo en un dispositivo en particular, como un flujo de bits que comienza en una ubicación específica o como un archivo en initramfs.

Para un archivo en un dispositivo, el formato es:

```
cryptkey=*dispositivo*:*tipo de sistema de archivos*:*ruta*

```

*   `*dispositivo*` es el dispositivo de bloque sin formato donde existe la clave.
*   `*tipo de sistema de archivos*` es el tipo de sistema de archivos del `*dispositivo*` (o auto).
*   `*ruta*` es la ruta absoluta del archivo de claves dentro del dispositivo.

Ejemplo: `cryptkey=/dev/usbstick:vfat:/secretkey`

Para un flujo de bits en un dispositivo, la ubicación de la clave se especifica con el formato siguiente:

```
cryptkey=*dispositivo*:*desplazamiento*:*tamaño* 

```

donde el desplazamiento («[offset](https://en.wikipedia.org/wiki/es:Offset_(inform%C3%A1tica) "wikipedia:es:Offset (informática)")») y el tamaño («**size**») están en bytes. Ejemplo: `cryptkey=/dev/sdZ:0:512` lee un archivo de claves de 512 bytes desde el principio del dispositivo.

**Sugerencia:** Si la ruta del dispositivo al que desea acceder contiene el carácter `:`, se debe soslayar con una barra invertida `\`. En ese caso, el parámetro cryptkey sería el siguiente: `cryptkey=/dev/disk/by-id/usb-123456-0\:0:0:512` para una clave en un usb con el id `usb-123456-0:0`.

Para un archivo [incrustado](/index.php/Mkinitcpio_(Espa%C3%B1ol)#BINARIOS_y_ARCHIVOS "Mkinitcpio (Español)") en initramfs el formato sería [[1]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n14):

```
cryptkey=rootfs:*ruta'*

```

Ejemplo: `cryptkey=rootfs:/secretkey`

También tenga en cuenta que si `cryptkey` no se especifica, por defecto es `/crypto_keyfile.bin` (en initramfs).[[2]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n8)

Véase también [dm-crypt/Device encryption (Español)#Archivos de claves](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Archivos_de_claves "Dm-crypt/Device encryption (Español)").

#### crypto

Este parámetro es específico para pasar las opciones de la modalidad plain de *dm-crypt* al hook *encrypt*.

Toma el formato siguiente:

```
crypto=<hash>:<algoritmo de cifrado>:<tamaño clave>:<desplazamiento>:<salto>

```

Los argumentos se relacionan directamente con las opciones de *cryptsetup*. Consulte [dm-crypt/Device encryption (Español)#Opciones de cifrado para la modalidad plain](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Opciones_de_cifrado_para_la_modalidad_plain "Dm-crypt/Device encryption (Español)")

Para un disco cifrado con solo las opciones predeterminadas de *plain*, se deben especificar los argumentos de `crypto`, pero cada entrada se puede dejar en blanco:

```
crypto=::::

```

Un ejemplo específico de argumentos sería:

```
crypto=sha512:twofish-xts-plain64:512:0:

```

### Utilizar el hook sd-encrypt

En todo lo que sigue `rd.luks` puede reemplazarse con `luks`. Los parámetros `rd.luks` solo son respetados por initrd. Los parámetros `luks` son respetados tanto por el sistema principal como por initrd. A menos que desee controlar dispositivos que se desbloqueen después del inicio desde la línea de órdenes del kernel, use `rd.luks`. Vea [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8) para más opciones y detalles.

**Sugerencia:**

*   Si existe el archivo `/etc/crypttab.initramfs`, [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") lo agregará a initramfs como `/etc/crypttab`, pudiendo especificar allí los dispositivos que deben desbloquearse en el arranque. La sintaxis está documentada en [#crypttab](#crypttab) y [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5).
*   `/etc/crypttab.initramfs` no se limita a usar solo UUID como `rd.luks`. Puede usar cualquiera de los [métodos para asignar nombres permanentes a dispositivos de bloques](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#Métodos_para_nombrar_los_dispositivos_de_forma_permanente "Persistent block device naming (Español)").

**Nota:**

*   Todos los parámetros de `rd.luks` se pueden especificar reiteradas veces para desbloquear varios volúmenes cifrados con LUKS.
*   Los parámetros `rd.luks` solo admiten el desbloqueo de dispositivos LUKS detectables. Para desbloquear un dispositivo dm-crypt sin formato o un dispositivo LUKS con un encabezado separado, debe especificarlo en `/etc/crypttab.initramfs`. Vea [#crypttab](#crypttab) para la sintaxis.

**Advertencia:** Si está utilizando `/etc/crypttab` o `/etc/crypttab.initramfs` junto con parámetros de `luks.*` o `rd.luks.*`, solo se activarán los dispositivos especificados en la línea de órdenes del kernel y verá el mensaje `Not creating device 'devicename' because it was not specified on the kernel command line.`. Para activar todos los dispositivos en `/etc/crypttab` no especifique ningún parámetro `luks.*` y utilice `rd.luks.*`. Para activar todos los dispositivos en `/etc/crypttab.initramfs` no especifique ningún parámetro `luks.*` o `rd.luks.*`.

#### rd.luks.uuid

**Sugerencia:** `rd.luks.uuid` se puede omitir cuando se utiliza `rd.luks.name`.

```
rd.luks.uuid=*UUID*

```

Especifique el [UUID](/index.php/UUID "UUID") del dispositivo que se va a descifrar en el arranque con este indicador. Si el UUID está en `/etc/crypttab.initramfs`, se usarán las opciones enumeradas allí. Para `luks.uuid` se usarán las opciones de `/etc/crypttab.initramfs` o `/etc/crypttab`.

De forma predeterminada, el dispositivo mapeado estará ubicado en `/dev/mapper/luks-*UUID*` donde *UUID* es el UUID de la partición LUKS.

#### rd.luks.name

```
rd.luks.name=*UUID*=*nombre*

```

Especifique el nombre del dispositivo mapeado después de que la partición LUKS esté abierta. Por ejemplo, al especificar `*UUID*=cryptroot` indica que el dispositivo desbloqueado se encuentra en `/dev/mapper/cryptroot`. Si no se especifica nada, el dispositivo mapeado se entenderá ubicado en `/dev/mapper/luks-*UUID*` donde *UUID* es el UUID de la partición LUKS. Cuando use este parámetro, puede omitir `rd.luks.uuid`.

Esto es equivalente al segundo parámetro de `cryptdevice` para `encrypt`.

#### rd.luks.options

```
rd.luks.options=UUID=*opciones*

```

o

```
rd.luks.options=*opciones*

```

Especifique las opciones para el dispositivo listado después de `UUID` o, si no se especifica, para todos los UUID no especificados en otra parte (por ejemplo, crypttab).

Esto es aproximadamente equivalente al tercer parámetro de `cryptdevice` para `encrypt`.

Sigue un formato similar a las opciones en crypttab: las opciones están separadas por comas, y, a su vez, las opciones con valores se especifican usando `*option*=*valores*`.

Por ejemplo:

```
rd.luks.options=timeout=10s,swap,cipher=aes-cbc-essiv:sha256,size=256

```

#### rd.luks.key

**Nota:** El hook `sd-encrypt` solo admite archivos de clave incrustados en initramfs (es decir, especificado en la matriz `FILES` en `/etc/mkinitcpio.conf`).[systemd issue 9181](https://github.com/systemd/systemd/issues/9181).

```
rd.luks.key=UUID=*archivo de claves*

```

o

```
rd.luks.key=*archivo de claves*

```

Indique la ubicación de un archivo de claves utilizado para descifrar el dispositivo especificado en `rd.luks.UUID`. No hay una ubicación predeterminada como la que hay con el hook `encrypt` para el parámetro `cryptkey`.

#### Tiempo de espera («*timeout*»)

Hay dos opciones que afectan el tiempo de espera para ingresar la contraseña durante el inicio:

*   `rd.luks.options=timeout=*tiempo de espera*` especifica el tiempo de espera para consultar una contraseña.
*   `rootflags=x-systemd.device-timeout=*tiempo de espera*` especifica cuánto tiempo debe esperar systemd para que se muestre el dispositivo rootfs antes de retirarlo (el valor predeterminado es 90 segundos).

Si desea desactivar el tiempo de espera por completo, establezca ambos tiempos en cero:

```
rd.luks.options=timeout=0 rootflags=x-systemd.device-timeout=0

```

## crypttab

El archivo `/etc/crypttab` (tabla de dispositivos cifrados) es similar al archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") y contiene una lista de dispositivos cifrados que se desbloquearán durante el inicio del sistema. Este archivo se puede utilizar para montar automáticamente dispositivos de intercambio cifrados o sistemas de archivos secundarios.

`crypttab` se lee *antes* que `fstab`, por lo que los contenedores de dm-crypt se pueden desbloquear antes de que se monte el sistema de archivos que contiene en su interior. Tenga en cuenta que `crypttab` se lee *después* de que el sistema se haya iniciado, por lo tanto, no reemplaza el desbloqueo de particiones cifradas mediante el uso de hooks de [mkinitcpio](#mkinitcpio) y [opciones del cargador de arranque](#Cargador_de_arranque) como en el caso de la [partición raíz cifrada](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)"). El procesado de `crypttab` en el momento del arranque se realiza mediante `systemd-cryptsetup-generator` automáticamente.

Consulte [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) para obtener detalles, lea a continuación algunos ejemplos, y la sección [#Montaje en el momento del arranque](#Montaje_en_el_momento_del_arranque) para obtener instrucciones sobre cómo usar los UUID para montar un dispositivo cifrado.

**Nota:** Cuando se usa [systemd-boot](/index.php/Systemd-boot "Systemd-boot") y el hook `sd-encrypt`, si la contraseña de una partición no raíz es la misma que la de la partición raíz, no hay necesidad de poner esa partición que no es raíz en crypttab debido al almacenamiento en caché de la contraseña. Consulte [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=219859) para obtener más información.

**Advertencia:**

*   Si se especifica la opción *nofail*, la pantalla de ingreso de la contraseña puede desaparecer mientras se escribe la contraseña. *nofail*, por lo tanto, solo debe usarse junto con los archivos de claves.
*   Hay problemas con [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") al procesar la entradas de `crypttab` para dispositivos cifrados en [modo plain](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") de *dm-crypt* (`--type plain`):
    *   Para los dispositivos `--type plain` con un archivo de claves, es necesario agregar la opción `hash=plain` a crypttab debido a una [incompatibilidad de systemd](https://bugs.freedesktop.org/show_bug.cgi?id=52630). **No** utilice `systemd-cryptsetup` manualmente para que la creación del dispositivo funcione a su alrededor.
    *   También puede ser necesario agregar la opción `plain` explícitamente para forzar a `systemd-cryptsetup` reconocer un dispositivo `--type plain`) en el arranque. Consulte [systemd número 442](https://github.com/systemd/systemd/issues/442).

 `/etc/crypttab` 
```
# Ejemplo de archivo crypttab. Los campos son: nombre, dispositivo subyacente, contraseña, opciones de cryptsetup.

# Montar /dev/lvm/swap recifrándolo con una clave nueva en cada reinicio.
 swap	/dev/lvm/swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256

# Montar /dev/lvm/tmp como /dev/mapper/tmp utilizando modalidad plain de dm-crypt con una contraseña aleatoria, haciendo que su contenido no se pueda recuperar después de que se desmonte.
tmp	/dev/lvm/tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256 

# Montar /dev/lvm/home como /dev/mapper/home utilizando LUKS, y solicitar la contraseña en el momento del arranque.
home   /dev/lvm/home

# Montar /dev/sdb1 como /dev/mapper/backup utilizando LUKS, con una contraseña almacenada en un archivo.
backup /dev/sdb1       /home/alice/backup.key
```

### Montaje en el momento del arranque

Si desea montar una unidad cifrada en el momento del arranque, ingrese el UUID del dispositivo en `/etc/crypttab`. Obtenga el UUID (de la partición) usando la orden `lsblk -f` y agregándolo a `crypttab` como sigue:

 `/etc/crypttab`  `externaldrive         UUID=2f9a8428-ac69-478a-88a2-4aa458565431        none    luks,timeout=180` 

El primer parámetro es el nombre que prefiera del dispositivo mapeado para la unidad cifrada. La opción `none` expondrá un prompt durante el inicio para escribir la contraseña que desbloquee la partición. La opción `timeout` define un tiempo de espera en segundos para ingresar la contraseña de descifrado durante el arranque.

**Nota:** Tenga en cuenta que la opción `timeout` en `crypttab` solo determina el tiempo permitido para *ingresar la contraseña* del dispositivo cifrado. Además, [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") también tiene un tiempo de espera predeterminado que fija la cantidad de tiempo permitido para que *el dispositivo esté disponible* (prefijado en 90 segundos), que es independiente del temporizador fijado para la contraseña. En consecuencia, incluso cuando la opción `timeout` en `crypttab` fija un valor superior a 90 segundos (o tiene su valor predeterminado a 0, lo que significa tiempo ilimitado), *systemd* solo esperará un máximo de 90 segundos para que se desbloquee el dispositivo. Para cambiar el tiempo en que *systemd* mantiene un dispositivo disponible, se puede establacer la opción `x-systemd.device-timeout` (consulte [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5)) en [fstab](/index.php/Fstab "Fstab") para dicho dispositivo. Probablemente sea deseable, entonces, que el tiempo de la opción `timeout` en `crypttab` sea igual al tiempo fijado con la opción `x-systemd.device-timeout` en `fstab` para cada dispositivo montado al momento del arranque.

También se puede configurar un [archivo de claves](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Archivos_de_claves "Dm-crypt/Device encryption (Español)") y remitirse a él en lugar de esteblecer `none`. Esto da como resultado un desbloqueo automático, si se puede acceder al archivo de claves durante el inicio. Dado que LUKS ofrece la opción de tener varias claves, la opción elegida también se puede cambiar más adelante.

Utilice el nombre que ha definido en `/etc/crypttab` para el mapeado del dispositivo en `/etc/fstab` de la siguiente manera:

 `/etc/fstab`  `/dev/mapper/externaldrive      /mnt/backup               ext4    defaults,errors=remount-ro  0  2` 

Dado que `/dev/mapper/externaldrive` ya es el resultado de un mapeado de partición único, no es necesario especificar un UUID para ello. En cualquier caso, el dispositivo mapeado con el sistema de archivos tendrá un UUID diferente al de la partición en la que está cifrado.

#### Montaje de un dispositivo de bloque apilado

Los generadores de systemd también procesan automáticamente los dispositivos de bloque apilados en el arranque.

Por ejemplo, puede crear una configuración [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"), utilizar cryptsetup para cifrarlo y crear un volumen lógico [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") con el sistema de archivos correspondiente dentro del dispositivo de bloque cifrado. El resultado será esto:

 `$ lsblk -f` 
```
─sdXX                  linux_raid_member    
│ └─md0                 crypto_LUKS   
│   └─cryptedbackup     LVM2_member 
│     └─vgraid-lvraid   ext4              /mnt/backup
└─sdYY                  linux_raid_member    
  └─md0                 crypto_LUKS       
    └─cryptedbackup     LVM2_member 
      └─vgraid-lvraid   ext4              /mnt/backup

```

que le pedirá la contraseña y se montará automáticamente en el arranque.

Dado que se han especificado las entradas correctas para crypttab (por ejemplo, UUID para el dispositivo `crypto_LUKS`) y para fstab (`/dev/vgraid/lvraid`) respectivametne, no hay necesidad de agregar más configuraciones/hooks de mkinitcpio, porque el procesamiento de `/etc/crypttab` se aplica solo a montajes no root. Una excepción es cuando el hook `mdadm_udev` se usa *ya* (por ejemplo, para el dispositivo raíz). En este caso, `/etc/madadm.conf` e initramfs necesitan actualizarse para lograr que la correcta raid de la raíz se elija primero.

### Montaje bajo demanda

Puede [iniciar](/index.php/Start "Start") `systemd-cryptsetup@externaldrive.service` en lugar de usar:

```
# cryptsetup luksOpen UUID=... externaldrive

```

cuando tenga una entrada como sigue en su `/etc/crypttab`:

 `/etc/crypttab`  `externaldrive UUID=... none noauto` 

De esa manera no necesita recordar las opciones exactas de crypttab. Le pedirá la contraseña si es necesario.

El archivo *unit* correspondiente será generado automáticamente por [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8). Puede listar todos los archivos *unit* generados usando:

```
$ systemctl list-unit-files | grep systemd-cryptsetup

```

## Solución de problemas

### El espacio del sistema en el arranque/solicitud de contraseña no se muestra

Si está usando [Plymouth (Español)](/index.php/Plymouth_(Espa%C3%B1ol) "Plymouth (Español)"), asegúrese de cargar los módulos correctos (vea: [Plymouth#The plymouth hook](/index.php/Plymouth#The_plymouth_hook "Plymouth")) o desactívelos. De lo contrario, Plymouth no asumirá la solicitud de contraseña, haciendo imposible el inicio del sistema.
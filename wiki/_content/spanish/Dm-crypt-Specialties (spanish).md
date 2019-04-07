**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – <a class="mw-selflink selflink">Especialidades</a>

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Specialties&diff=0&oldid=552071) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Asegurar la partición de arranque no cifrada](#Asegurar_la_partición_de_arranque_no_cifrada)
    *   [1.1 Arrancar desde un dispositivo extraíble](#Arrancar_desde_un_dispositivo_extraíble)
    *   [1.2 chkboot](#chkboot)
    *   [1.3 mkinitcpio-chkcryptoboot](#mkinitcpio-chkcryptoboot)
        *   [1.3.1 Instalación](#Instalación)
        *   [1.3.2 Descripción técnica](#Descripción_técnica)
    *   [1.4 AIDE](#AIDE)
    *   [1.5 STARK](#STARK)
*   [2 Utilizar archivos de claves cifrados con GPG, LUKS o OpenSSL](#Utilizar_archivos_de_claves_cifrados_con_GPG,_LUKS_o_OpenSSL)
*   [3 Desbloqueo remoto de la partición (u otro volumen) raíz](#Desbloqueo_remoto_de_la_partición_(u_otro_volumen)_raíz)
    *   [3.1 Desbloqueo remoto (hooks: systemd, systemd-tool)](#Desbloqueo_remoto_(hooks:_systemd,_systemd-tool))
    *   [3.2 Desbloqueo remoto (hooks: netconf, dropbear, tinyssh, ppp)](#Desbloqueo_remoto_(hooks:_netconf,_dropbear,_tinyssh,_ppp))
    *   [3.3 Desbloqueo remoto a través de wifi (hooks: construya el suyo propio)](#Desbloqueo_remoto_a_través_de_wifi_(hooks:_construya_el_suyo_propio))
*   [4 Soporte Discard/TRIM para unidades de estado sólido (SSD)](#Soporte_Discard/TRIM_para_unidades_de_estado_sólido_(SSD))
*   [5 El hook encrypt y varios discos](#El_hook_encrypt_y_varios_discos)
    *   [5.1 Expandir LVM en varios discos](#Expandir_LVM_en_varios_discos)
        *   [5.1.1 Añadir una nueva unidad](#Añadir_una_nueva_unidad)
        *   [5.1.2 Extender el volumen lógico](#Extender_el_volumen_lógico)
    *   [5.2 Modificar el hook encrypt para varias particiones](#Modificar_el_hook_encrypt_para_varias_particiones)
        *   [5.2.1 Sistema de archivos raíz que abarca múltiples particiones](#Sistema_de_archivos_raíz_que_abarca_múltiples_particiones)
        *   [5.2.2 Múltiples particiones no root](#Múltiples_particiones_no_root)
*   [6 Sistema cifrado usando un encabezado LUKS separado](#Sistema_cifrado_usando_un_encabezado_LUKS_separado)
    *   [6.1 Utilizar el hook systemd](#Utilizar_el_hook_systemd)
    *   [6.2 Modificar el hook encrypt](#Modificar_el_hook_encrypt)
*   [7 Cifrado/arranque y un encabezado LUKS separado en USB](#Cifrado/arranque_y_un_encabezado_LUKS_separado_en_USB)
    *   [7.1 Preparar las particiones de los discos](#Preparar_las_particiones_de_los_discos)
        *   [7.1.1 Preparar la llave USB](#Preparar_la_llave_USB)
        *   [7.1.2 Preparar la unidad principal](#Preparar_la_unidad_principal)
    *   [7.2 Procedimiento de instalación y personalización del hook encrypt](#Procedimiento_de_instalación_y_personalización_del_hook_encrypt)
        *   [7.2.1 Cargador de arranque](#Cargador_de_arranque)
    *   [7.3 Cambiar el archivo de claves LUKS](#Cambiar_el_archivo_de_claves_LUKS)

## Asegurar la partición de arranque no cifrada

La partición `/boot` y el [Master Boot Record](/index.php/Partitioning_(Espa%C3%B1ol)#Master_Boot_Record "Partitioning (Español)") son ​​las dos áreas del disco que no están cifradas, incluso en una configuración de [raíz cifrada](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)"). Por lo general, no se pueden cifrar porque el [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") y la BIOS (respectivamente) no pueden desbloquear un contenedor dm-crypt para continuar el proceso de arranque. Una excepción es [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), que tiene una función para desbloquear `/boot` cifrado —véase [dm-crypt/Encrypting an entire system (Español)#Cifrar partición de arranque (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Cifrar_partición_de_arranque_(GRUB) "Dm-crypt/Encrypting an entire system (Español)")—.

Esta sección describe los pasos que se pueden tomar para hacer que el proceso de arranque sea más seguro.

**Advertencia:** tenga en cuenta que proteger la partición `/boot` y el MBR puede mitigar los numerosos ataques que se pueden producir durante el proceso de arranque, pero los sistemas configurados de esta manera pueden ser vulnerables a la manipulación de la BIOS/UEFI/firmware, a través de los [registradores de teclas](https://en.wikipedia.org/wiki/es:Keylogger "wikipedia:es:Keylogger") del hardware, los [ataques de arranque en frío](https://en.wikipedia.org/wiki/es:Ataque_de_arranque_en_fr%C3%ADo "wikipedia:es:Ataque de arranque en frío") y muchas otras amenazas cuyo estudio queda fuera del alcance de este artículo. Para obtener una descripción general de los problemas relacionados con la fiabilidad del sistema y cómo se relacionan con el cifrado del disco completo, consulte [[1]](http://www.youtube.com/watch?v=pKeiKYA03eE).

### Arrancar desde un dispositivo extraíble

**Advertencia:** en la versión 230 de systemd, cryptsetup generador emite `RequiresMountsFor` para el archivo de claves de cifrado. Por lo tanto, cuando el sistema de archivos que contiene este archivo no está montado, también detiene el servicio cryptsetup. Este comportamiento es incorrecto porque el sistema de archivos y la clave de cifrado solo se requieren una vez, cuando el contenedor criptográfico está inicialmente configurado. Consulte [systemd issue 3816](https://github.com/systemd/systemd/issues/3816).

El uso de un dispositivo separado para iniciar un sistema es un procedimiento bastante sencillo y ofrece una mejora de seguridad significativa contra algunos tipos de ataques. En un [sistema de archivos raíz cifrado](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") hay dos partes que emplea el sistema que resultan vulnerables, estas son:

*   el [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), y
*   la partición `/boot`.

Estos deben almacenarse sin cifrar para que el sistema pueda iniciarse. Para protegerlos de manipulación indebida, es recomendable almacenarlos en un medio extraíble, como una unidad USB, y arrancar desde esa unidad en lugar del disco duro. Siempre que tenga su disco USB a buen recaudo, puede estar seguro de que esos componentes no han sido manipulados, lo que hace que la autenticación sea mucho más segura al desbloquear el sistema.

Se supone que ya tiene su sistema configurado con una partición dedicada montada en `/boot`. Si no lo hace, siga los pasos indicados en [dm-crypt/System configuration (Español)#Cargador de arranque](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol)#Cargador_de_arranque "Dm-crypt/System configuration (Español)"), sustituyendo su disco duro por una unidad extraíble.

**Nota:** debe asegurarse de que su sistema admita el arranque desde el medio elegido, ya sea una unidad USB, un disco duro externo, una tarjeta SD o cualquier otro medio.

Prepare la unidad extraíble (`/dev/sdx`).

```
# gdisk /dev/sdx #formatear si es necesario. Alternativamente, utilice cgdisk, fdisk, cfdisk, gparted...
# mkfs.ext2 /dev/sdx1
# mount /dev/sdx1 /mnt

```

Copie los contenidos existentes de `/boot` en el nuevo.

```
# cp -ai /boot/* /mnt/

```

Monte la nueva partición. No olvide actualizar su archivo [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") en consecuencia.

```
# umount /boot
# umount /mnt
# mount /dev/sdx1 /boot
# genfstab -p -U / > /etc/fstab

```

Actualice [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"). El script `grub-mkconfig` debería detectar el nuevo UUID de la partición automáticamente, pero es posible que las entradas del menú personalizado deban actualizarse manualmente.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install /dev/sdx #intalar en el dispositivo extraíble, no en el disco duro.

```

Reinicie y pruebe la nueva configuración. Recuerde configurar en la BIOS o en [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") el orden de inicio del dispositivo desde el que arrancar. Si el sistema no se inicia, aún debería poder iniciar desde el disco duro para corregir el problema.

### chkboot

**Advertencia:** chkboot realiza **una prueba de comprobación posencendido** de una partición `/boot`, no **una prueba de comprobación preencendido**. Cuando se ejecuta el script chkboot, ya se ha ingresado la contraseña, por lo que su cargador de arranque, el kernel o initrd pueden quedar potencialmente comprometidos. Si el sistema da fallo tras la prueba de integridad de chkboot, no se podrá garantizar la seguridad de sus datos.

Remitiéndonos al artículo de ct-magazine (Número 3/12, página 146, 01.16.2012, [[2]](http://www.heise.de/ct/inhalt/2012/03/6/)), el siguiente script comprueba los archivos presentes en `/boot` para cambios de [hash](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash") [SHA-1](https://en.wikipedia.org/wiki/es:Secure_Hash_Algorithm#SHA-1 "wikipedia:es:Secure Hash Algorithm"), [inodo](https://en.wikipedia.org/wiki/es:Inodo "wikipedia:es:Inodo") y bloques ocupados en el disco duro. También verifica el [Master Boot Record](/index.php/Partitioning_(Espa%C3%B1ol)#Master_Boot_Record "Partitioning (Español)"). El script no puede evitar cierto tipo de ataques, pero otros muchos los hace más difíciles. Ninguna configuración del script en sí misma se almacena en `/boot` que no está cifrado. Con un sistema cifrado bloqueado/apagado, esto hace que sea más difícil para algunos atacantes porque no es evidente que se realice una comparación de suma de comprobación automática de la partición en el arranque. Sin embargo, un atacante que anticipe estas precauciones puede manipular el firmware para ejecutar su propio código en la parte superior del kernel e interceptar el acceso al sistema de archivos, por ejemplo, a `boot`, y este le presente los archivos no protegidos. En general, ninguna medida de seguridad por debajo del nivel del firmware puede garantizar la fiabilidad y la evidencia de falsificación.

El script con instrucciones de instalación está [disponible](ftp://ftp.heise.de/pub/ct/listings/1203-146.zip) (Author: Juergen Schmidt, ju at heisec.de; License: GPLv2), También hay un paquete [chkboot](https://aur.archlinux.org/packages/chkboot/) para [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)").

Después de la instalación, agregue un archivo de servicio (el paquete incluye uno basado en lo siguiente) y [actívelo](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)"):

```
[Unit]
Description=Check that boot is what we want
Requires=basic.target
After=basic.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/chkboot.sh

[Install]
WantedBy=multi-user.target

```

Hay una pequeña advertencia para systemd. Al momento de escribir (este artículo), el script original `chkboot.sh` suministrado contiene un espacio vacío al comienzo de `#!/bin/bash` que debe ser eliminado para que el servicio se inicie con éxito.

Como `/usr/local/bin/chkboot_user.sh` debe ejecutarse justo después del inicio de sesión, debe agregarlo al [inicio automático](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)") (por ejemplo, en KDE -> *Configuración del sistema -> Inicio y apagado -> Autostart* ; en GNOME 3: *gnome-session-properties*).

Con Arch Linux, los cambios en `/boot` son bastante frecuentes, por ejemplo, con la incorporación de nuevos kernels. Por lo tanto, puede ser útil usar los scripts con cada actualización completa del sistema. Una forma de hacerlo sería:

```
#!/bin/bash
#
# Nota: inserte su <usuario> y ejecútelo con sudo para que pacman y chkboot funcionen automáticamente
#
echo "Pacman update [1] Quickcheck before updating" & 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
/usr/local/bin/chkboot.sh
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
echo "Pacman update [2] Syncing repos for pacman" 
pacman -Syu
/usr/local/bin/chkboot.sh
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user>
echo "Pacman update [3] All done, let us roll on ..."

```

### mkinitcpio-chkcryptoboot

**Advertencia:** este hook no cifra el código [GRUB](/index.php/GRUB "GRUB"), el código (MBR) o el apéndice EFI, ni protege contra situaciones en las que un atacante puede modificar el comportamiento del cargador de arranque para comprometer el kernel y/o initramfs en tiempo de ejecución.

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) es un hook de [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") que realiza verificaciones de integridad durante el primer espacio de usuario y aconseja al usuario que no ingrese su contraseña para desbloquear la partición raíz si el sistema parece estar comprometido. La seguridad se logra a través de una [partición de arranque cifrada](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Cifrar_partición_de_arranque_(GRUB) "Dm-crypt/Encrypting an entire system (Español)"), que se desbloquea utilizando el módulo `cryptodisk.mod` para [GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Partición_de_arranque "GRUB (Español)"), y una partición del sistema de archivos raíz, que se cifra con una contraseña diferente de la anterior. De esta manera, [Initramfs (Español)](/index.php/Initramfs_(Espa%C3%B1ol) "Initramfs (Español)") y el [kernel (Español)](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") están protegidos contra la manipulación fuera de línea, y la partición raíz puede permanecer segura incluso si la contraseña de la partición `/boot` se ingresa en un equipo comprometido (siempre que el hook chkcryptoboot detecte que el equipo se ha visto comprometido, y el mismo no se ha visto comprometido en tiempo de ejecución).

Este hook requiere la versión >=2.00 del paquete [grub](https://www.archlinux.org/packages/?name=grub) para que funcione, y una partición dedicada, `/boot` cifrada con LUKS con su propia contraseña para que sea seguro.

#### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") [mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) y edite `/etc/default/chkcryptoboot.conf`. Si desea disponer de la capacidad de detectar si su partición de arranque se baipaseó (o puenteó), modifique las variables `CMDLINE_NAME` y `CMDLINE_VALUE` con valores que solo usted conozca. Puede seguir el consejo de usar dos funciones de hash como se sugiere, inmediatamente después de la instalación. Además, asegúrese de hacer los cambios apropiados en la [línea de órdenes del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") en `/etc/default/grub`. Edite la línea `HOOKS=` en `/etc/mkinitcpio.conf`, e inserte el hook `chkcryptoboot` **antes** de `encrypt`. Cuando haya terminado, [regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

#### Descripción técnica

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) consiste en un hook de instalación y un hook en tiempo de ejecución para mkinitcpio. El hook de instalación se ejecuta cada vez que se reconstruye initramfs, y comprueba el hash del apéndice de [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") de GRUB (`$esp/EFI/grub_uefi/grubx64.efi`) (en el caso de los sistemas [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") ) o los primeros 446 bytes del disco en el que está instalado GRUB (en el caso de los sistemas BIOS), y almacena ese hash dentro de los initramfs ubicados dentro de la partición cifrada `/boot`. Cuando se inicia el sistema, GRUB solicita la contraseña para desbloquear `/boot`, luego el hook en tiempo de ejecución realiza la misma operación de comparación de hash antes de solicitar la contraseña de la partición raíz. Si no coinciden, el hook imprimirá un error como este:

```
CHKCRYPTOBOOT ALERT!
CHANGES HAVE BEEN DETECTED IN YOUR BOOT LOADER EFISTUB!
YOU ARE STRONGLY ADVISED NOT TO ENTER YOUR ROOT CONTAINER PASSWORD!
Please type uppercase yes to continue:

```

Además del hash del cargador de arranque, el hook también verifica los parámetros del kernel en ejecución con los configurados en `/etc/default/chkcryptoboot.conf`. Esto se comprueba tanto en tiempo de ejecución como después de que se realiza el proceso de arranque. Esto permite que el hook detecte si la configuración de GRUB no se baipaseó tanto en el tiempo de ejecución como después, para detectar si la partición `/boot` completa ha sido manipulada.

Para los sistemas BIOS, el hook crea un hash del gestor de arranque de la primera etapa de GRUB (instalado en los primeros 446 bytes del dispositivo de arranque) para compararlo en los procesos de arranque posteriores. La segunda etapa principal del gestor de arranque GRUB, `core.img`, no será comprobado.

### AIDE

Como alternativa a los scripts anteriores, se puede configurar una comprobación de hash con [AIDE](/index.php/AIDE "AIDE") que se puede personalizar a través de un archivo de configuración muy flexible.

### STARK

Si bien alguno de los métodos descritos arriba deberían dar respuesta a la demanda de la mayoría de los usuarios, los mismos no resuelven todos los problemas de seguridad que se pueden presentar asociados con `/boot` sin cifrar. Un enfoque que intenta proporcionar una cadena de arranque completamente autenticada fue publicado con POTTS como una tesis académica para implementar el marco de autenticación [STARK](http://www1.informatik.uni-erlangen.de/stark)

La prueba de concepto de POTTS utiliza Arch Linux como una distribución base e implementa una cadena de arranque del sistema con:

*   POTTS: un menú de inicio para un mensaje de autenticación de una sola vez.
*   TrustedGrub - una implementación de [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") que autentica el kernel e initramfs contra los registros de [chips TPM](https://en.wikipedia.org/wiki/es:M%C3%B3dulo_de_plataforma_confiable "wikipedia:es:Módulo de plataforma confiable").
*   TRESOR: un parche del kernel que implementa AES pero mantiene la clave maestra no en la RAM sino en los registros de la CPU durante el tiempo de ejecución.

Como parte de la tesis [installation](http://13.tc/p/potts/manual.html), se han publicado instrucciones basadas en Arch Linux (ISO a partir de 2013-01). Si desea probarlo, tenga en cuenta que estas herramientas no se encuentran en los repositorios estándar y que la solución llevará mucho tiempo de mantenimiento.

## Utilizar archivos de claves cifrados con GPG, LUKS o OpenSSL

Las siguientes publicaciones del foro brindan instrucciones para usar dos factores de autenticación, archivos de claves cifrados con gpg o openssl, en lugar de un archivo de clave de texto plano descrito anteriormente en este artículo wiki [System Encryption using LUKS with GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=120243):

*   GnuPG: [Post regarding GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=943338#p943338) Esta publicación tiene las instrucciones genéricas.
*   OpenSSL: [Post regarding OpenSSL encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=947805#p947805) Esta publicación solo tiene los hooks `ssldec`.
*   OpenSSL: [Post regarding OpenSSL salted bf-cbc encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=155393) Esta publicación tiene los hooks `bfkf` de initcpio, install y el script generador del archivo de claves cifrado.
*   LUKS: [Post regarding LUKS encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=1502651#p1502651) con un hook `lukskey` de initcpio. O [#Cifrado/arranque y un encabezado LUKS separado en USB](#Cifrado/arranque_y_un_encabezado_LUKS_separado_en_USB) a continuación con un hook encrypt personalizado para initcpio.

Tenga en cuenta que:

*   Puede seguir las instrucciones anteriores con solo dos particiones primarias, una partición de arranque (requerida debido al cifrado) y una partición LVM primaria. Dentro de la partición LVM puede tener tantas particiones como necesite, pero lo más importante es que contenga volumenes lógicos para, al menos, las particiones raíz, de intercambio y «*home*». Esto tiene la ventaja adicional de tener solo un archivo de claves para todas sus particiones y tener la capacidad de hibernar su equipo (suspender en disco) donde la partición de intercambio está encriptada. Si decide hacerlo, los hooks en `/etc/mkinitcpio.conf` deberían tener este aspecto: `HOOKS=( ... usb usbinput (etwo o ssldec) encrypt (si se utiliza openssl) lvm2 resume ... )` y debe agregar `resume=/dev/<NombredelGrupodeVolúmenes>/<NombredelVolumenLógicodeIntecambio>` a sus [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)").
*   Si necesita almacenar temporalmente el archivo de claves desencriptado en algún lugar, no lo almacene en un disco sin cifrado. Es mejor asegúrese de guardarlos en la memoria RAM como `/dev/shm`.
*   Si desea usar un archivo de claves encriptado con GPG, necesita usar una versión 1.4 de GnuPG compilada estáticamente o puede editar los hooks y usar este paquete AUR [gnupg1](https://aur.archlinux.org/packages/gnupg1/)
*   Es posible que una actualización de OpenSSL pueda romper el hook `ssldec` personalizado, mencionada en la segunda publicación del foro.

## Desbloqueo remoto de la partición (u otro volumen) raíz

Si desea poder reiniciar un sistema totalmente cifrado con LUKS de forma remota, o iniciarlo con un servicio [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") [(véase también)](https://en.wikipedia.org/wiki/es:Wake_on_LAN que configure una interfaz de red. Algunos de los paquetes que se enumeran a continuación contribuyen con varios [hooks compilados de mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Build_hooks "Mkinitcpio (Español)") para facilitar la configuración.

**Nota:**

*   Tenga en cuenta que debe usar los nombres de dispositivos del kernel para la interfaz de red (por ejemplo, `eth0`) y no uno de [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") (por ejemplo, `enp1s0`), ya que no funcionarán.
*   Podría ser necesario agregar [el módulo de su tarjeta de red](/index.php/Network_configuration_(Espa%C3%B1ol)#Controlador_del_dispositivo "Network configuration (Español)") a la matriz [MODULES](/index.php/Mkinitcpio_(Espa%C3%B1ol)#MÓDULOS "Mkinitcpio (Español)").

### Desbloqueo remoto (hooks: systemd, systemd-tool)

El paquete de AUR [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) proporciona un hook [systemd](https://www.archlinux.org/packages/?name=systemd) pensado para mkinitcpio denominado *systemd-tool* con el siguiente conjunto de características para systemd en initramfs:

| 

Características principales proporcionadas por el hook:

*   configuración unificada systemd + mkinitcpio
*   aprovisionamiento automático de recursos binarios y de configuración
*   invocación bajo demanda de scripts mkinitcpio y funciones en línea

 | 

Características proporcionadas por las unidades de servicio incluidas:

*   depuración de errores de initrd
*   configuración de red temprana
*   intérprete de órdenes de usuario interactiva
*   acceso ssh remoto en initrd
*   cryptsetup + agente de contraseña personalizada

 |

El paquete [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) requiere el [hook systemd](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio"). Para obtener más información, lea [README](https://github.com/random-archer/mkinitcpio-systemd-tool/blob/master/README.md) del proyecto, así como el valor predeterminado proporcionado por defecto por [systemd service unit files](https://github.com/random-archer/mkinitcpio-systemd-tool) para comenzar.

Los hooks recomendados son: `base autodetect modconf block filesystems keyboard fsck systemd systemd-tool`.

### Desbloqueo remoto (hooks: netconf, dropbear, tinyssh, ppp)

Otra combinación de paquetes que proporciona inicios de sesión remotos para initcpio es [mkinitcpio-netconf](https://www.archlinux.org/packages/?name=mkinitcpio-netconf) y/o [mkinitcpio-ppp](https://aur.archlinux.org/packages/mkinitcpio-ppp/) (para el desbloqueo remoto usando un [Protocolo punto a punto (PPP)](https://en.wikipedia.org/wiki/es:Point-to-Point_Protocol el paquete [mkinitcpio-utils](https://www.archlinux.org/packages/?name=mkinitcpio-utils). Las instrucciones a continuación se pueden utilizar con cualquier combinación de los paquetes anteriores. Cuando haya diferentes caminos, se advertirá.

1.  Si aún no tiene un par de claves SSH, [genere uno](/index.php/SSH_keys_(Espa%C3%B1ol)#Generando_las_llaves_SSH "SSH keys (Español)") en el sistema cliente (el que se usará para desbloquear la máquina remota).
    **Nota:** `tinyssh` solo admite los tipos de claves [Ed25519](/index.php/SSH_keys#Ed25519 "SSH keys") y [ECDSA](/index.php/SSH_keys#ECDSA "SSH keys"). Si elige usar [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh), necesitará crear/usar una de estas.

2.  Inserte su clave pública SSH (es decir, la que normalmente coloca en los hosts para poder ingresar sin contraseña, o la que acaba de crear y que termina en *.pub* ) en el archivo `/etc/dropbear/root_key` o `/etc/tinyssh/root_key` del equipo remoto.
    **Sugerencia:** este método se puede usar más adelante para agregar otras claves públicas SSH según sea necesario; en el caso de que simplemente esté copiando el contenido el archivo `~/.ssh/authorized_keys` remoto, asegúrese de verificar que solo contenga las claves que desea utilizar para desbloquear la máquina remota. Si agrega claves adicionales, regenere initrd también usando `mkinitcpio`. Vea también [Secure Shell (Español)#Protección](/index.php/Secure_Shell_(Espa%C3%B1ol)#Protección "Secure Shell (Español)").

3.  Agregue los tres [hooks](/index.php/Mkinitcpio_(Espa%C3%B1ol)#HOOKS "Mkinitcpio (Español)"),`<netconf y/o ppp> <dropbear o tinyssh> encryptssh` antes de `filesystems` dentro de la matriz «HOOKS» en `/etc/mkinitcpio.conf` (el hook `encryptssh` reemplaza al hook `encrypt`). Después [regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").
    **Nota:** El hook `net` proporcionado por [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) **no** es necesario.

4.  Configure el [parámetro](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol)#Cargador_de_arranque "Dm-crypt/System configuration (Español)") `cryptdevice=` requerido y agregue el [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") `ip=` a la configuración de su gestor de arranque con los argumentos apropiados. Por ejemplo, si el servidor DHCP no atribuye una IP estática a su sistema remoto, lo que dificultaría el acceso con SSH a través de reinicios, puede indicar explícitamente la IP que desea usar: `ip=192.168.1.1:::::eth0:none` Alternativamente, también puede especificar la máscara de subred y la puerta de enlace requeridas por la red: `ip=192.168.1.1::192.168.1.254:255.255.255.0::eth0:none` 
    **Nota:** a partir de la versión 0.0.4 de [mkinitcpio-netconf](https://www.archlinux.org/packages/?name=mkinitcpio-netconf), puede anidar múltiples parámetros `ip=` con el fin de configurar múltiples interfaces. No puede mezclarlo con `ip=dhcp` (`ip=:::::eth0:dhcp`) solo. Se debe especificar una interfaz.
     `ip=ip=192.168.1.1:::::eth0:none:ip=172.16.1.1:::::eth1:none` Para una descripción detallada eche un vistazo a [la sección de mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Usar_la_red "Mkinitcpio (Español)"). Cuando termine, actualice la configuración de su [gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)").
5.  Finalmente, reinicie el sistema remoto e intente ejecutar [ssh para él](/index.php/Secure_Shell_(Espa%C3%B1ol)#Cliente "Secure Shell (Español)"), **indicando explícitamente el nombre de usuario «root»** (incluso si la cuenta de root está desactivada en la máquina, ya que este usuario root se utiliza solo en initrd con el propósito de desbloquear el sistema remoto). Si está utilizando el paquete [mkinitcpio-dropbear](https://www.archlinux.org/packages/?name=mkinitcpio-dropbear) y también tiene el paquete [openssh](https://www.archlinux.org/packages/?name=openssh) instalado, lo más probable es que no reciba ninguna advertencia antes de iniciar sesión, ya que convierte y usa el mismo juego de claves openssh del host (excepto las claves Ed25519, ya que dropbear no las admite). En caso de que esté utilizando [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh), tiene la opción de instalar [tinyssh-convert](https://www.archlinux.org/packages/?name=tinyssh-convert) o [tinyssh-convert-git](https://aur.archlinux.org/packages/tinyssh-convert-git/) para que pueda usar las mismas claves que su instalación [openssh](https://www.archlinux.org/packages/?name=openssh) (actualmente solo son claves Ed25519). En cualquier caso, debería haber ejecutado [el demonio ssh](/index.php/Secure_Shell_(Espa%C3%B1ol)#Gestión_del_Demonio "Secure Shell (Español)") al menos una vez, utilizando las unidades systemd suministradas, para que las claves se puedan generar primero. Después de reiniciar la máquina, se le solicitará que introduzca la contraseña para desbloquear el dispositivo raíz. El sistema completará su proceso de arranque y luego puede iniciar sesión en él [como lo haría normalmente](/index.php/Secure_Shell_(Espa%C3%B1ol)#Cliente "Secure Shell (Español)") (con el usuario remoto que elija).

**Sugerencia:** si simplemente desea una buena solución para montar otras particiones cifradas (como `/home`) de forma remota, puede consultar [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?pid=880484).

### Desbloqueo remoto a través de wifi (hooks: construya el suyo propio)

El hook net se usa normalmente con una conexión [cableada](https://en.wikipedia.org/wiki/es:Ethernet "wikipedia:es:Ethernet"). En caso de que desee configurar un equipo que solo dispone de conexión inalámbrica y desbloquearla a través de wifi, puede crear un hook personalizado para conectarse a una red wifi antes de ejecutar el hook de red, net.

El siguiente ejemplo muestra una configuración utilizando un adaptador wifi USB, que se conecta a una red wifi protegida con WPA2-PSK. En caso de que utilice, por ejemplo, WEP u otro, es posible que necesite cambiar algunas cosas.

1.  Modifique `/etc/mkinitcpio.conf`:
    *   Agregue el módulo del kernel necesario para su adaptador wifi específico.
    *   Incluya los archivos binarios `wpa_passphrase` y `wpa_supplicant`.
    *   Agregue un hook `wifi` (o el nombre que elija, este es el hook personalizado que se creará) antes del hook `net`.
        ```
        MODULES=(*módulo*)
        BINARIES=(wpa_passphrase wpa_supplicant)
        HOOKS=(base udev autodetect ... **wifi** net ... dropbear encryptssh ...)
        ```

2.  Cree el hook `wifi` en `/etc/initcpio/hooks/wifi`:
    ```
    run_hook ()
    {
    	# demorar unos segundos, dejando que wlan0 sea configurado por kernel
    	sleep 5

    	# configurar wlan0 a up
    	ip link configurar wlan0 up

    	# asociar con la red wifi
    	# 1\. guardar el archivo config temporal
    	wpa_passphrase « *network ESSID* » « *passrase* »> /tmp/wifi 

    	# 2\. crear asociación
    	wpa_supplicant -B -D nl80211, wext -i wlan0 -c /tmp/wifi

    	# demorar unos segundos para que wpa_supplicant termine de conectarse
    	sleep 5

    	# wlan0 ahora debería estar conectado y listo para que el hook net pueda asignar una ip
    }

    	run_cleanuphook ()
    {
    	# wpa_supplicant que se ejecuta en segundo plano
    	killall wpa_supplicant

    	# configurar wlan0 link a down 
    	ip link set wlan0 down

    	# wlan0 ahora debería estar completamente desconectado de la red wifi
    }
    ```

3.  Cree el archivo de instalación de hook en`/etc/initcpio/install/wifi`:
    ```
    build ()
    {
    	add_runscript
    }
    help ()
    {
    cat<<HELPEOF
    	Activar wifi en el arranque, para desbloquear dropbear ssh del disco..
    HELPEOF
    }
    ```

4.  Agregue `ip=:::::wlan0:dhcp` a los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"). Elimine `ip=:::::eth0:dhcp` para que no entre en conflicto.
5.  Opcionalmente, cree una entrada de arranque adicional con el parámetro del kernel `ip=:::::eth0:dhcp`.
6.  [Regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").
7.  Actualice la configuración de su [cargador de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)").

Recuerde configurar [wifi](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)"), de modo que pueda iniciar sesión una vez que el sistema haya arrancado completamente. En caso de que no pueda conectarse a la red wifi, intente aumentar los tiempos de demora un poco.

## Soporte Discard/TRIM para unidades de estado sólido (SSD)

Los usuarios de [unidades de estado sólido](/index.php/Solid_state_drive "Solid state drive") deben tener en cuenta que, de forma predeterminada, las órdenes [TRIM](https://en.wikipedia.org/wiki/es:TRIM "wikipedia:es:TRIM") no están activadas por el mapeador de dispositivos, es decir, los dispositivos de bloque se montan sin la opción `discard` a menos que anule el valor predeterminado.

Los mantenedores de device-mapper han dejado claro que la compatibilidad con TRIM nunca se activará de forma predeterminada en los dispositivos dm-crypt debido a las posibles implicaciones de seguridad. [[3]](http://www.saout.de/pipermail/dm-crypt/2011-September/002019.html)[[4]](http://www.saout.de/pipermail/dm-crypt/2012-April/002420.html) Es posible la fuga mínima de datos en forma de información liberada del bloque, tal vez suficiente para determinar el sistema de archivos en uso, en dispositivos con TRIM activado. Una ilustración y discusión de los problemas que surgen de la activación de TRIM está disponible en el [blog](http://asalor.blogspot.de/2011/08/trim-dm-crypt-problems.html) de un desarrollador de «cryptsetup». Si le preocupan estos factores, también tenga en cuenta que las amenazas pueden aumentar: por ejemplo, si su dispositivo todavía está cifrado con el algoritmo de cifrado predeterminado anterior (cryptsetup <1.6.0) `--cipher aes-cbc-essiv`, es posible que se produzcan más fugas de información a partir de la observación del sector «*trimmed*», que con las actuales opciones de cifrado [predeterminadas](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Opciones_de_cifrado_para_la_modalidad_LUKS "Dm-crypt/Device encryption (Español)").

Se distinguen los siguientes casos:

*   El dispositivo está cifrado con la modalidad LUKS de dm-crypt predeterminado:
    *   De forma predeterminada, el encabezado LUKS se almacena al comienzo del dispositivo y usar TRIM es útil para proteger las modificaciones del encabezado. Si, por ejemplo, se revoca una contraseña LUKS comprometida, sin TRIM activado, el encabezado anterior en general todavía estará disponible para leer hasta que otra operación lo sobrescriba; mientras tanto, si se roba la unidad, los atacantes podrían, en teoría, encontrar una manera de localizar el encabezado anterior y usarlo para descifrar el contenido con la contraseña comprometida. Consulte [cryptsetup, sección 5.19 ¿Qué hay de las unidades de estado sólido, flash y unidades híbridas?](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) y [Cifrado de disco completo en un ssd](https://www.reddit.com/r/archlinux/comments/2f370s/full_disk_encryption_on_an_ssd/ck5p5c5).
    *   TRIM puede dejarse desactivado si los problemas de seguridad indicados en la parte superior de esta sección se consideran una amenaza peor que los indicados en la viñeta anterior.

	Véase también [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk").

*   El dispositivo está cifrado con la modalidad plain de dm-crypt, o el encabezado LUKS se almacena [por separado](#Cifrado/arranque_y_un_encabezado_LUKS_separado_en_USB):
    *   Si se requiere una [negación plausible](https://en.wikipedia.org/wiki/es:Cifrado_negable "wikipedia:es:Cifrado negable"), TRIM **nunca** debe ser usado debido a las consideraciones dadas en la parte superior de esta sección, o el uso del cifrado se dará a conocer.
    *   Si no se requiere una negación plausible, se puede usar TRIM por sus mejoras de rendimiento, siempre que los peligros de seguridad descritos en la parte superior de esta sección no sean motivo de preocupación.

**Advertencia:** antes de activar TRIM en una unidad, asegúrese de que el dispositivo sea totalmente compatible con las órdenes TRIM, o de lo contrario puede provocar pérdida de datos. Consulte [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

En versiones 3.1 de [linux](https://www.archlinux.org/packages/?name=linux) y posteriores, el soporte para TRIM de dm-crypt se puede alternar al crear el dispositivo o montarlo con dmsetup. El soporte para esta opción también existe en la versión 1.4.0 de [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) y superior. Para agregar soporte durante el arranque, deberá añadir `:allow-discards` a la opción `cryptdevice`. La opción TRIM puede verse así:

```
cryptdevice=/dev/sdaX:root:allow-discards

```

Para las opciones de configuración principales de `cryptdevice` antes de `:allow-discards` vea [Dm-crypt/System configuration (Español)](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)").

Si está utilizando initrd basado en systemd, debe pasar la opción:

```
rd.luks.options=discard

```

**Nota:** la opción `rd.luks.options=discard` del kernel no tiene ningún efecto en los dispositivos incluidos en el archivo `/etc/crypttab` para la imagen de initramfs (`/etc/crypttab.initramfs` en la raíz real). Debe especificar la opción `discard` en `/etc/crypttab.initramfs`.

Además de la opción del kernel, también se requiere ejecutar periódicamente `fstrim` o montar el sistema de archivos (por ejemplo, `/dev/mapper/root` en este ejemplo) con la opción `discard` en `/etc/fstab`. Para obtener más información, consulte la página de [TRIM](/index.php/TRIM "TRIM").

Para los dispositivos LUKS desbloqueados a través de `/etc/crypttab` use la opción `discard`, por ejemplo:

 `/etc/crypttab`  `luks-123abcdef-etc UUID=123abcdef-etc none discard` 

Cuando desbloquee manualmente los dispositivos en la consola, use `--allow-discards`.

Con LUKS2 puede establecer `allow-discards` como un indicador predeterminado para un dispositivo abriéndolo una vez con la opción `--persistent`:

```
# cryptsetup --allow-discards --persistent open --type luks2 /dev/sdaX root

```

Puede confirmar que el indicador se ha establecido de forma permanente en el encabezado LUKS2 comprobando la salida de `cryptsetup luksDump`

 `# cryptsetup luksDump /dev/sdaX | grep Flags` 
```
Flags:          allow-discards

```

En cualquier caso, puede verificar si el dispositivo realmente se abrió con discards inspeccionando la salida de `dmsetup table`:

 `# dmsetup table` 
```
luks-123abcdef-etc: 0 1234567 crypt aes-xts-plain64 000etc000 0 8:2 4096 1 allow_discards

```

## El hook encrypt y varios discos

**Sugerencia:** el hook `sd-encrypt` admite el desbloqueo de múltiples dispositivos. Se pueden especificar en la línea de órdenes del kernel o en el archivo `/etc/crypttab.initramfs`. Consulte [dm-crypt/System configuration (Español)#Utilizar el hook sd-encrypt](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol)#Utilizar_el_hook_sd-encrypt "Dm-crypt/System configuration (Español)").

El hook `encrypt` solo permite una **única** entrada `cryptdevice=` ([FS#23182](https://bugs.archlinux.org/task/23182)). En las configuraciones del sistema con múltiples unidades, esto puede ser limitante, ya que *dm-crypt* no tiene una función que permita exceder al dispositivo físico. Por ejemplo, tomemos «LVM sobre LUKS»: todo el volumen LVM existe dentro de un mapeado LUKS. Esto está perfectamente bien para un sistema de una sola unidad, ya que solo hay un dispositivo para descifrar. Pero, ¿qué sucede cuando desea aumentar el tamaño de LVM? No puede, al menos no sin modificar el hook `encrypt`.

Las siguientes secciones muestran sucintamente las alternativas para superar dicha limitación. El primero trata sobre cómo expandir una configuración [LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an entire system (Español)") a un nuevo disco. El segundo consiste en la modificación del hook `encrypt` para poder desbloquear varios discos en las configuraciones LUKS sin LVM.

### Expandir LVM en varios discos

La gestión de discos múltiples es una característica básica de [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") y una de las principales razones para su flexibilidad de particionado. También se puede utilizar con *dm-crypt*, pero solo si se emplea LVM como primer mapeador. En tal configuración [LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an entire system (Español)") los dispositivos encriptados se crean dentro de los volúmenes lógicos (con una clave/contraseña por volumen). Lo siguiente cubre los pasos para saber cómo expandir esa configuración a otro disco.

**Advertencia:** realice una copia de seguridad. Si bien el cambio de tamaño de los sistemas de archivos puede estar estandarizada, tenga en cuenta que las operaciones **pueden** ir mal y lo explicado a continuación podría no ajustarse a su configuración particular. En general, extender un sistema de archivos para liberar espacio en el disco es menos problemático que reducir uno. Esto se aplica, en particular, cuando se usan mapeadores apilados, como es el caso del siguiente ejemplo.

#### Añadir una nueva unidad

Primero, prepare un nuevo disco de acuerdo con [dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)"). Segundo, partíciónelo como un LVM, por ejemplo, asigne todo el espacio a `/dev/sdY1` con el tipo de partición `8E00` (Linux LVM). Y tercero, adjunte el nuevo disco/partición al grupo de volúmenes LVM existente, por ejemplo:

```
# pvcreate /dev/sdY1
# vgextend MyStorage /dev/sdY1

```

#### Extender el volumen lógico

El siguiente paso, consiste en la asignación final del nuevo espacio del disco al el volumen lógico que se va a extender, para lo cual dicho volumen lógico tiene que ser desmontado. Se puede realizar para la partición raíz `cryptdevice`, pero en este caso el procedimiento se debe realizar desde una imagen ISO de instalación de Arch.

En este ejemplo, se supone que el volumen lógico para `/home` (nombre del volúmen lógico `homevol`) se expandirá al espacio del disco nuevo:

```
# umount /home
# fsck /dev/mapper/home
# cryptsetup luksClose /dev/mapper/home
# lvextend -l +100%FREE MyStorage/homevol

```

Ahora, una vez extendido el volumen lógico, el contenedor LUKS viene a continuación:

```
# cryptsetup open /dev/MyStorage/homevol home
# umount /home      # Como seguridad, para el caso de que fuera automática remontar
# cryptsetup --verbose resize home

```

Finalmente, redimensionamos el sistema de archivos:

```
# e2fsck -f /dev/mapper/home
# resize2fs /dev/mapper/home

```

¡Hecho! Si este era su plan, `/home` se puede volver a montar y ahora incluirá el espacio del nuevo disco:

```
# mount /dev/mapper/home /home

```

Tenga en cuenta que la acción `cryptsetup resize` no afecta a las claves de cifrado y, por tanto, estas no habrán cambiado.

### Modificar el hook encrypt para varias particiones

#### Sistema de archivos raíz que abarca múltiples particiones

Es posible modificar el hook encrypt para permitir descifrar múltiples unidades de disco duro raíz (`/`) en el arranque. En un solo paso:

```
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2
# cp /usr/lib/initcpio/hooks/encrypt  /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptdevice/cryptdevice2/" /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptkey/cryptkey2/" /etc/initcpio/hooks/encrypt2

```

Agregue `cryptdevice2=` a sus opciones de arranque (y `cryptkey2=` si es necesario), y agregue el hook `encrypt2` a [mkinitcpio.conf](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") antes de regenerarlo. Vea [dm-crypt/System configuration (Español)](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)").

#### Múltiples particiones no root

Tal vez tenga la necesidad de usar el hook `encrypt` en una partición no root. Arch no admite esto de forma automática sino que necesita intervención manual, sin embargo, puede cambiar fácilmente los valores de cryptdev y cryptname en `/lib/initcpio/hooks/encrypt` (el primero en su partición `/dev/sd*`, el segundo para el nombre que desea atribuirle). Eso debería bastar.

La gran ventaja es que puede tener todo automatizado, mientras que configurar `/etc/crypttab` con un archivo de claves externa (es decir, el archivo de claves no está en ninguna partición interna del disco duro) puede ser una molestia. Asegúrese de que el dispositivo USB/FireWire/... se monte antes que la partición encriptada, lo que significa que debe cambiar el orden de `/etc/fstab` (al menos).

Por supuesto, si se actualiza el paquete [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup), tendrá que cambiar este script nuevamente. A diferencia de `/etc/crypttab`, solo se admite una partición, pero con un poco más de picardía se pueden desbloquear varias particiones.

Si desea implementar esto en una partición RAID por software, hay una cosa más que debe hacer. No basta con configurar el dispositivo `/dev/mdX` en `/lib/initcpio/hooks/encrypt`; el hook `encrypt` fallará al no poder encontrar la clave por algún motivo y tampoco mostrará un prompt para pedirle una contraseña. Parece que los dispositivos RAID no se activan hasta que se ejecuta el hook `encrypt`. Puede resolver esto colocando la matriz RAID en `/boot/grub/menu.lst`, así:

```
kernel /boot/vmlinuz-linux md=1,/dev/hda5,/dev/hdb5

```

Si configura su partición raíz como un RAID, advertirá avisos similares con esa configuración. [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") puede manejar múltiples definiciones de matriz muy bien:

```
kernel /boot/vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1 md=1,/dev/sda5,/dev/sdb5,/dev/sdc5

```

## Sistema cifrado usando un encabezado LUKS separado

Este ejemplo sigue la misma configuración que en [dm-crypt/Encrypting an entire system (Español)#Modalidad plain de dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Modalidad_plain_de_dm-crypt "Dm-crypt/Encrypting an entire system (Español)"), que debería leer primero antes de seguir esta guía.

Al utilizar un encabezado separado, el dispositivo de bloque cifrado solo transporta datos cifrados, lo que proporciona [cifrado denegable](https://en.wikipedia.org/wiki/Deniable_encryption para obtener más información.

Consulte [dm-crypt/Device encryption (Español)#Opciones de cifrado para la modalidad LUKS](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Opciones_de_cifrado_para_la_modalidad_LUKS "Dm-crypt/Device encryption (Español)") para ver las opciones de cifrado antes de realizar el primer paso para configurar la partición del sistema cifrado y crear un archivo de encabezado para usar con `cryptsetup`:

```
# dd if=/dev/zero of=header.img bs=4M count=1 conv=notrunc
# cryptsetup luksFormat --type luks2 /dev/sdX --align-payload 8192 --header header.img

```

**Sugerencia:** cuando use la opción `--header`, `--align-payload` permite especificar el inicio de datos cifrados en un dispositivo. Al reservar un espacio al comienzo del dispositivo, tiene la opción posteriormente de [volver a colocar el encabezado LUKS](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Restaurar_utilizando_cryptsetup "Dm-crypt/Device encryption (Español)"). Consulte [cryptsetup(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup.8) para conocer los valores admitidos por`--align-payload`.

Abra el contenedor:

```
# cryptsetup open --header header.img /dev/sdX enc

```

Ahora siga los pasos de la [configuración de LVM sobre LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Preparar_las_particiones_que_no_son_de_arranque_(boot) "Dm-crypt/Encrypting an entire system (Español)") según sus necesidades. Lo mismo se aplica a la [preparación de la partición de arranque](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#_Preparar_la_partición_de_arranque_4 "Dm-crypt/Encrypting an entire system (Español)") en el dispositivo extraíble (porque de lo contrario, no tiene sentido tener un archivo de encabezado separado para desbloquear el cifrado disco). Luego mueva el `header.img` sobre él:

```
# mv header.img /mnt/boot

```

Siga el procedimiento de instalación hasta el paso mkinitcpio (ahora debería realizar `arch-chroot` dentro del sistema cifrado).

**Sugerencia:** Se dará cuenta de que, como la partición del sistema solo tiene datos «aleatorios», no tiene una tabla de particiones y, por lo tanto, un `UUID` o un `LABEL`. Pero aún puede tener una mapeado consistente utilizando el [Persistent block device naming (Español)#by-id y by-path](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-id_y_by-path "Persistent block device naming (Español)"). Por ejemplo usando la identificación del disco de `/dev/disk/by-id/`.

Hay dos opciones para que initramfs admita un encabezado LUKS separado.

### Utilizar el hook systemd

Primero cree `/etc/crypttab.initramfs` y agregue el dispositivo cifrado a él. La sintaxis se define en [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5)

 `/etc/crypttab.initramfs`  `enc	/dev/disk/by-id/*your-disk_id*	none	header=/boot/header.img` 

Modifique `/etc/mkinitcpio.conf` [para usar systemd](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Hooks_más_comunes "Mkinitcpio (Español)") y agregue la imagen header a `FILES`.

 `/etc/mkinitcpio.conf` 
```
...
FILES=(**/boot/header.img**)
...
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)
...
```

[Regenerar initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)") y listo.

**Nota:** no es necesario pasar ningún parámetro cryptsetup a la línea de órdenes del kernel, ya que `/etc/crypttab.initramfs` se agregará como `/etc/crypttab` en initramfs. Si desea especificarlos en la línea de órdenes del kernel, consulte [dm-crypt/System configuration (Español)#Utilizar el hook sd-encrypt](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol)#Utilizar_el_hook_sd-encrypt "Dm-crypt/System configuration (Español)") para ver las opciones admitidas.

### Modificar el hook encrypt

Este método muestra cómo modificar el hook `encrypt` para usar un encabezado LUKS separado. Ahora el hook `encrypt` debe modificarse para que `cryptsetup` use el encabezado separado ([FS#42851](https://bugs.archlinux.org/task/42851); fuente base e idea para estos cambios [publicado en BBS](https://bbs.archlinux.org/viewtopic.php?pid=1076346#p1076346)). Haga una copia para que no se sobrescriba en una actualización de [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

```
# cp /usr/lib/initcpio/hooks/encrypt /etc/initcpio/hooks/encrypt2
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2

```
 `/etc/initcpio/hooks/encrypt2 (around line 52)` 
```
warn_deprecated() {
    echo "The syntax 'root=${root}' where '${root}' is an encrypted volume is deprecated"
    echo "Use 'cryptdevice=${root}:root root=/dev/mapper/root' instead."
}

**local headerFlag=false**
for cryptopt in ${cryptoptions//,/ }; do
    case ${cryptopt} in
        allow-discards)
            cryptargs="${cryptargs} --allow-discards"
            ;;  
        **header)
            cryptargs="${cryptargs} --header /boot/header.img"
            headerFlag=true
            ;;**
        *)  
            echo "Encryption option '${cryptopt}' not known, ignoring." >&2 
            ;;  
    esac
done

if resolved=$(resolve_device "${cryptdev}" ${rootdelay}); then
    if **$headerFlag ||** cryptsetup isLuks ${resolved} >/dev/null 2>&1; then
        [ ${DEPRECATED_CRYPT} -eq 1 ] && warn_deprecated
        dopassphrase=1
```

Ahora edite el archivo [mkinitcpio.conf](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para agregar los hooks `encrypt2` y `lvm2` a `HOOKS`, el archivo `header.img` a `FILES` y el modulo `loop` a `MODULES`, aparte de otras configuraciones que requiera el sistema:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(**loop**)
...
FILES=(**/boot/header.img**)
...
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt2** **lvm2** filesystems fsck)
...
```

Esto es necesario para que el encabezado LUKS esté disponible en el arranque y permita el descifrado del sistema, eximiéndonos de una configuración más complicada como montar otro dispositivo USB separado para acceder al encabezado. Después de esta configuración se creará [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

A continuación, [configure el cargador de arranque](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Configurar_el_gestor_de_arranque_4 "Dm-crypt/Encrypting an entire system (Español)") para especificar `cryptdevice=` pasando también la nueva opción `header` a dicha configuración:

```
cryptdevice=/dev/disk/by-id/*your-disk_id*:enc:header

```

Para finalizar, seguimos [dm-crypt/Encrypting an entire system (Español)#Posinstalación](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Posinstalación "Dm-crypt/Encrypting an entire system (Español)") que es particularmente útil con una partición `/boot` en un medio de almacenamiento USB.

## Cifrado/arranque y un encabezado LUKS separado en USB

En lugar de incrustar la imagen `header.img` y el archivo de claves en [initramfs](/index.php/Initramfs "Initramfs"), esta configuración hará que su sistema dependa completamente de la llave usb en lugar de tan solo la imagen de arranque, y del archivo de claves cifrado que contiene la partición de arranque cifrada. Como el encabezado y el archivo de claves no están embebidos en la imagen [initramfs](/index.php/Initramfs "Initramfs") y el hook encrypt personalizado está específicamente para [by-id](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-id_y_by-path "Persistent block device naming (Español)"), literalmente necesitará la llave usb para arrancar.

Para la unidad usb, ya que está cifrando la unidad y el archivo de claves en su interior, es preferible colocar en cascada los algoritmos de cifrado para no usar el mismo dos veces. Es discutible si un [ataque de intermediario](https://en.wikipedia.org/wiki/es:ataque_de_intermediario "wikipedia:es:ataque de intermediario") sería realmente factible. Puede ser [twofish](https://en.wikipedia.org/wiki/es:Twofish "wikipedia:es:Twofish")-[serpent](https://en.wikipedia.org/wiki/es:Serpent "wikipedia:es:Serpent") o serpent-twofish.

### Preparar las particiones de los discos

Se asumirá que `sdb` es la unidad USB, y que `sda` es el disco duro principal.

Prepare los dispositivos de acuerdo con [dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)").

#### Preparar la llave USB

Utilice [gdisk](/index.php/Gdisk "Gdisk") para particionar el disco según el diseño [mostrado aquí](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#_Preparar_el_disco_5 "Dm-crypt/Encrypting an entire system (Español)"), con la excepción de que solo debe incluir las dos primeras particiones. De este modo:

 `# gdisk /dev/sdb` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem

```

Antes de ejecutar `cryptsetup`, consulte [opciones de cifrado para la modalidad LUKS](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#_Opciones_de_cifrado_para_la_modalidad_LUKS "Dm-crypt/Device encryption (Español)") y [algoritmos de cifrado y modalidades de operación](/index.php/Disk_encryption_(Espa%C3%B1ol)#Algoritmos_de_cifrado_y_modalidades_de_operación "Disk encryption (Español)") .

[Prepare la partición de arranque](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Preparar_la_partición_de_arranque_5 "Dm-crypt/Encrypting an entire system (Español)") pero no ejecute `mount` sobre ninguna partición todavía y [formatee la partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Formatear_la_partición "EFI system partition (Español)").

```
# mount /dev/mapper/cryptboot /mnt
# dd if=/dev/urandom of=/mnt/key.img bs=*tamaño_del_archivo* count=1
# cryptsetup --align-payload=1 luksFormat /mnt/key.img
# cryptsetup open /mnt/key.img lukskey

```

El *tamaño_del_archivo* está en bytes pero puede ir seguido de un sufijo como `M`. Tener un archivo demasiado pequeño le dará un desagradable error `Requested offset is beyond real size of device /dev/loop0`. Como referencia aproximada, la creación de un archivo de 4M lo cifrará correctamente. Debe hacer que el archivo sea más grande que el espacio necesario, ya que el dispositivo loop cifrado será un poco más pequeño que el tamaño del archivo.

Con un archivo grande, puede usar `--keyfile-offset=*desplazamiento*` y `--keyfile-size=*tamaño*` para navegar a la posición correcta. [[5]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)

Ahora debería tener `lukskey` abierto en un dispositivo loop (en `/dev/loop1`), mapeado como `/dev/mapper/lukskey`.

#### Preparar la unidad principal

```
# truncate -s 2M /mnt/header.img
# cryptsetup --key-file=/dev/mapper/lukskey --keyfile-offset=*desplazamiento* --keyfile-size=*tamaño* luksFormat /dev/sda --align-payload 4096 --header /mnt/header.img

```

Elija un *desplazamiento* y un *tamaño* en bytes (8192 bytes es el tamaño máximo de archivo de claves para `cryptsetup`).

```
# cryptsetup open --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* /dev/sda enc 
# cryptsetup close lukskey
# umount /mnt

```

Siga con los pasos para la [preparación de los volúmenes lógicos](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Preparar_los_volúmenes_lógicos "Dm-crypt/Encrypting an entire system (Español)") para configurar LVM sobre LUKS.

Consulte [Partitioning (Español)#Particiones dedicadas](/index.php/Partitioning_(Espa%C3%B1ol)#Particiones_dedicadas "Partitioning (Español)") para obtener recomendaciones sobre el tamaño de sus particiones.

Una vez que su partición raíz esté montada, realice `mount` sobre su partición de arranque cifrada como `/mnt/boot` y su partición del sistema EFI como `/mnt/efi`.

### Procedimiento de instalación y personalización del hook encrypt

Siga la [installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") hasta el paso `mkinitcpio` pero no lo haga todavía, y omita los pasos de partición, formateo y montaje como ya se han hecho.

Para que la configuración cifrada funcione, necesita crear su propio hook, que afortunadamente es fácil de hacer y aquí está el código que necesita. Tendrá que seguir [Persistent block device naming (Español)#by-id y by-path](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-id_y_by-path "Persistent block device naming (Español)") para averiguar sus propios valores `by-id` para el disco usb y para el disco principal (están vinculados -> a `sda` o `sdb`).

Debería usar `by-id` en lugar de `sda` o `sdb` porque `sdX` puede cambiar, y aquel garantiza que sea el dispositivo correcto .

Puede nombrar `customencrypthook` como quiera, y los hooks de compilación personalizados se pueden colocar en las carpetas `hooks` e `install` de `/etc/initcpio`. Mantenga una copia de seguridad de ambos archivos (`cp` a la partición `/home` o al directorio `/home` de su usuario después de crearlos). `/usr/bin/ash` no es un error tipográfico.

 `/etc/initcpio/hooks/customencrypthook` 
```
#!/usr/bin/ash

run_hook() {
    modprobe -a -q dm-crypt >/dev/null 2>&1
    modprobe loop
    [ "${quiet}" = "y" ] && CSQUIET=">/dev/null"

    while [ ! -L '/dev/disk/by-id/*usbdrive*-part2' ]; do
     echo 'Waiting for USB'
     sleep 1
    done

    cryptsetup open /dev/disk/by-id/*usbdrive*-part2 cryptboot
    mkdir -p /mnt
    mount /dev/mapper/cryptboot /mnt
    cryptsetup open /mnt/key.img lukskey
    cryptsetup --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=''offset'' --keyfile-size=''size'' open /dev/disk/by-id/*harddrive* enc
    cryptsetup close lukskey
    umount /mnt
}

```

`*usbdrive*` es su unidad USB `by-id`, y `*harddrive*` su unidad de disco duro principal `by-id`.

**Sugerencia:** también puede cerrar `cryptboot` usando `cryptsetup close`, pero tenerlo abierto facilita el montaje de las actualizaciones del sistema usando [Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y regenere initramfs con [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"). La partición `/boot` debe estar montada para las actualizaciones que afectan al [Kernel (Español)](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") o [Initramfs (Español)](/index.php/Initramfs_(Espa%C3%B1ol) "Initramfs (Español)"), e initramfs se regenerará automáticamente después de estas actualizaciones.

```
# cp /usr/lib/initcpio/install/encrypt /etc/initpcio/install/customencrypthook

```

Ahora edite el archivo copiado y elimine la sección `help()` ya que no es necesaria.

 `/etc/mkinitcpio.conf (edite solo esta parte, no lo reemplace, estos son solo extractos de las partes necesarias)` 
```
MODULES=(loop)
...
HOOKS=(base udev autodetect modconf block customencrypthook lvm2 filesystems keyboard fsck)
```

Las matrices `files=()` y `binaries=()` están vacías, y no debería tener que reemplazar la matriz `HOOKS=(...)` completa, basta colocar `customencrypthook lvm2` después de `block` y antes de `filesystems`, y asegúrese de `systemd`, `sd-lvm2` y `encrypt` son quitados.

#### Cargador de arranque

Finalice la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol)#Initramfs "Installation guide (Español)") desde el paso `mkinitcpio`. Para arrancar, necesitaría [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o [Unified Extensible Firmware Interface (Español)#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)"). Tenga en cuenta que puede usar [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") para admitir los discos encriptados mediante la [configuración del cargador de arranque](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Configurar_el_gestor_de_arranque_6 "Dm-crypt/Encrypting an entire system (Español)"), pero modificar la línea `GRUB_CMDLINE_LINUX` no es necesario para esta configuración.

O use Direct UEFI Secure boot para generar claves con [cryptboot](https://aur.archlinux.org/packages/cryptboot/), firmando luego initramfs y el kernel y creando un archivo de arranque *.efi* para la partición del sistema EFI con [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/). Antes de usar cryptboot o sbupdate, observe este extracto de [Secure Boot#Using your own keys](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"):

**Sugerencia:** tenga en cuenta que [cryptboot](https://aur.archlinux.org/packages/cryptboot/) requiere que la partición de arranque cifrada se especifique en `/etc/crypttab` antes de que se ejecute, y si lo está utilizando en combinación con [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), sbupdate espera a que los archivos `/boot/efikeys/db.*` creados por cryptboot se capitalicen como `DB.*` a menos que se configure de otro modo en `/etc/default/sbupdate`. Los usuarios que no usen systemd para manejar el cifrado pueden no tener nada en su archivo `/etc/crypttab` y necesitarán crear una entrada.

```
# efibootmgr -c -d /dev/*device* -p *partition_number* -L "Arch Linux Signed" -l "EFI\Arch\linux-signed.efi"

```

Consulte [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) para obtener una explicación de las opciones.

Asegúrese de que el orden de inicio ponga `Arch Linux Signed` primero. Si no es así, cámbielo con `efibootmgr -o XXXX,YYYY,ZZZZ`.

### Cambiar el archivo de claves LUKS

```
# cryptsetup --header /boot/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksChangeKey /dev/mapper/enc /dev/mapper/lukskey2 --new-keyfile-size=*newsize* --new-keyfile-offset=*newoffset*

```

Después, ejecute `cryptsetup close lukskey`, haga [shred](/index.php/Shred "Shred") o [dd](/index.php/Securely_wipe_disk#dd "Securely wipe disk") sobre el archivo de claves antiguo con datos aleatorios antes de borrarlo, y asegúrese de que el nuevo archivo de claves tenga el mismo nombre que el anterior: `key.img` u otro nombre.
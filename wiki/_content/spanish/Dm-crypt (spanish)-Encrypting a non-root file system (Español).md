**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt (Español)/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Device encryption (Español)") – <a class="mw-selflink selflink">Cifrar sistema de archivos no root</a> – [Cifrar un sistema completo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt (Español)/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt_(Espa%C3%B1ol)/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt_(Espa%C3%B1ol)/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt (Español)/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol) "Dm-crypt (Español)/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol) "Dm-crypt (Español)/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system"), revisada por última vez el **2019-09-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_a_non-root_file_system&diff=0&oldid=582800) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Los siguientes son ejemplos de encriptación de un sistema de archivos secundario, es decir, no raíz, con dm-crypt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Descripción general](#Descripción_general)
*   [2 Partición](#Partición)
    *   [2.1 Montaje y desmontaje manual](#Montaje_y_desmontaje_manual)
    *   [2.2 Desbloqueo y montaje automatizados](#Desbloqueo_y_montaje_automatizados)
        *   [2.2.1 En el momento del arranque](#En_el_momento_del_arranque)
        *   [2.2.2 En el inicio de sesión del usuario](#En_el_inicio_de_sesión_del_usuario)
*   [3 Dispositivo loop](#Dispositivo_loop)
    *   [3.1 Sin losetup](#Sin_losetup)
    *   [3.2 Con losetup](#Con_losetup)
        *   [3.2.1 Desmontar y montar manualmente](#Desmontar_y_montar_manualmente)

## Descripción general

El cifrado de un sistema de archivos secundario generalmente protege solo los datos confidenciales, mientras deja el sistema operativo y los archivos de programa sin cifrar. Esto es útil para cifrar un medio externo, como una unidad USB, de modo que se pueda mover a diferentes equipos de forma segura. También se podría optar por encriptar conjuntos de datos por separado según quién tenga acceso a ellos.

Como dm-crypt es una capa de cifrado de [nivel de bloque](/index.php/Disk_encryption_(Espa%C3%B1ol)#Cifrar_dispositivos_de_bloques "Disk encryption (Español)"), solo cifra dispositivos completos, [#Partición](#Partición) completa y [#Dispositivo loop](#Dispositivo_loop). Para cifrar archivos individuales se requiere una capa de cifrado de nivel de sistema de archivos, como [eCryptfs](/index.php/ECryptfs "ECryptfs") o [EncFS](/index.php/EncFS "EncFS"). Consulte [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") para obtener información general sobre cómo proteger datos privados.

## Partición

Este ejemplo cubre el cifrado de la partición `/home`, pero se puede aplicar a cualquier otra partición no raíz comparable que contenga datos de usuario.

**Sugerencia:** puede tener el directorio `/home` de un solo usuario en una partición, o crear una partición común para todos los directorios `/home` de los usuarios.

Primero asegúrese de que la partición esté vacía (sin un sistema de archivos asociado). Elimine la partición y cree una vacía si tiene un sistema de archivos. Luego prepare la partición borrándola con seguridad, vea [Dm-crypt (Español)/Drive preparation (Español)#Borrar de forma segura la unidad de disco duro](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol)#Borrar_de_forma_segura_la_unidad_de_disco_duro "Dm-crypt (Español)/Drive preparation (Español)").

Cree la partición que contendrá el contenedor cifrado.

Luego configure el encabezado LUKS con:

```
# cryptsetup *opciones* luksFormat --type luks2 *dispositivo*

```

Sustituya `*dispositivo*` por la partición creada anteriormente. Vea [Dm-crypt (Español)/Device encryption (Español)#Opciones de cifrado para la modalidad LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Opciones_de_cifrado_para_la_modalidad_LUKS "Dm-crypt (Español)/Device encryption (Español)") para conocer los detalles disponibles para `*opciones*`.

Para obtener acceso a la partición cifrada, desbloquéala con el mapeador de dispositivos, utilizando:

```
# cryptsetup open *dispositivo* *nombre*

```

Después de desbloquear la partición, estará disponible en `/dev/mapper/*nombre*`. Ahora crea un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") de su elección con:

```
# mkfs.*sistema_de_archivos* /dev/mapper/*nombre*

```

Monte el sistema de archivos en `/home`, o si solo un usuario tiene acceso en `/home/*nombre_de_usuario*`, vea [#Montaje y desmontaje manual](#Montaje_y_desmontaje_manual).

**Sugerencia:** monte y desmonte una vez para verificar que el mapeado está funcionando como se espera.

### Montaje y desmontaje manual

Para montar la partición:

```
# cryptsetup open *dispositivo* *nombre*
# mount -t *sistema_de_archivos* /dev/mapper/*nombre* /mnt/home

```

Para desmontarla:

```
# umount /mnt/home
# cryptsetup close *nombre*

```

**Sugerencia:** [GVFS](/index.php/GVFS "GVFS") también puede montar particiones cifradas. Se puede usar un administrador de archivos con soporte para gvfs (por ejemplo, [Thunar (Español)](/index.php/Thunar_(Espa%C3%B1ol) "Thunar (Español)")) permite montar la partición, y hará emerger un cuadro de diálogo solicitando la contraseña. Para otros escritorios, [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) también proporciona una interfaz gráfica.

### Desbloqueo y montaje automatizados

Existen tres soluciones diferentes para automatizar el proceso de desbloqueo de la partición y el montaje del sistema de archivos.

#### En el momento del arranque

Utilizando el archivo de configuración `/etc/crypttab`, el desbloqueo ocurre en el momento del arranque mediante el análisis automático de systemd. Esta es la solución recomendada si desea utilizar una partición común para todas las particiones «home» de los usuarios o montar automáticamente otro dispositivo de bloques cifrado.

Consulte [Dm-crypt (Español)/System configuration (Español)#crypttab](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#crypttab "Dm-crypt (Español)/System configuration (Español)") para obtener referencias y [Dm-crypt (Español)/System configuration (Español)#Montaje en el momento del arranque](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#Montaje_en_el_momento_del_arranque "Dm-crypt (Español)/System configuration (Español)") para ver un ejemplo de configuración.

#### En el inicio de sesión del usuario

Utilizando *pam_exec* es posible desbloquear (*cryptsetup open*) la partición en el inicio de sesión del usuario: esta es la solución recomendada si desea tener el directorio «home» de un solo usuario en una partición. Vea [dm-crypt (Español)/Mounting at login (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt (Español)/Mounting at login (Español)").

También es posible desbloquear el inicio de sesión del usuario con [pam_mount](/index.php/Pam_mount "Pam mount").

## Dispositivo loop

Hay dos métodos para usar un [dispositivo loop](https://en.wikipedia.org/wiki/es:Loop_device "wikipedia:es:Loop device") como un contenedor cifrado, uno que usa directamente `losetup` y otro no.

### Sin losetup

La utilización de losetup directamente se puede evitar completamente haciendo lo siguiente [[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile):

```
# dd if=/dev/urandom of=key.img bs=20M count=1
# cryptsetup --align-payload=1 luksFormat key.img
```

Antes de ejecutar `cryptsetup`, mire primero las [opciones de cifrado para la modalidad LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#_Opciones_de_cifrado_para_la_modalidad_LUKS "Dm-crypt (Español)/Device encryption (Español)") y los [algoritmos de cifrado y modalidades de operación](/index.php/Disk_encryption_(Espa%C3%B1ol)#Algoritmos_de_cifrado_y_modalidades_de_operación "Disk encryption (Español)") para seleccionar la configuración adicional deseada.

Las instrucciones para abrir el dispositivo y el [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") son las mismas que para [#Partición](#Partición).

Tener un archivo demasiado pequeño le dará un error `Requested offset is beyond real size of device /dev/loop0`, pero, como referencia aproximada, la creación de un archivo 4 MiB lo encriptará con éxito. [[2]](http://archive.is/VOh2p)

IfSi se crea un archivo más grande, `dd` de `/dev/urandom` se detendrá después de 32 MiB, requiriendo la opción `iflag=fullblock` para completar la escritura. [[3]](https://unix.stackexchange.com/questions/178949/why-does-dd-from-dev-urandom-stops-early)

El procedimiento de montar y desmontar manualmente es equivalente a [#Montaje y desmontaje manual](#Montaje_y_desmontaje_manual).

### Con losetup

Un dispositivo de looppermite asignar un dispositivo de bloques a un archivo con la herramienta estándar `losetup` de util-linux. El archivo puede contener un sistema de archivos, que se puede usar como cualquier otro sistema de archivos. Muchos usuarios conocen [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") como una herramienta para crear contenedores cifrados. Casi la misma funcionalidad se puede lograr con un sistema de archivos loopback cifrado con LUKS y es el que se muestra en el siguiente ejemplo.

Primero, comience creando un contenedor cifrado, utilizando un [generador de números aleatorios](/index.php/Random_number_generator "Random number generator") apropiado:

```
# dd if=/dev/urandom of=/bigsecret bs=1M count=10

```

Esto creará el archivo `bigsecret` con un tamaño de 10 megabytes.

**Nota:** para evitar tener que [redimensionar](/index.php/Dm-crypt/Device_encryption#Loopback_filesystem "Dm-crypt/Device encryption") el contenedor más adelante, asegúrese de hacerlo más grande que el tamaño total de los archivos que se cifrarán, para al menos también alojar los metadatos asociados que necesita el sistema de archivos interno. Si va a usar el modo LUKS, su encabezado de metadatos requiere de uno a dos megabytes por sí solo.

A continuación, cree el nodo del dispositivo `/dev/loop0`,de modo que podamos montar/usar nuestro contenedor:

```
# losetup /dev/loop0 /bigsecret

```

**Nota:** si le da el error `/dev/loop0: No such file or directory`, primero debe cargar el módulo del kernel con `modprobe loop`. En estos tiempos (Kernel 3.2) se crean dispositivos loop bajo demanda. Solicite un nuevo dispositivo loop con `# losetup -f`.

A partir de ahora, el procedimiento es el mismo que para [#Partición](#Partición), excepto por el hecho de que el contenedor ya está asignado al azar y no necesitará otro borrado seguro.

**Sugerencia:** los contenedores con *dm-crypt* pueden ser muy flexibles. Eche un vistazo a las características y documentación de [Tomb](/index.php/Tomb "Tomb"). Proporciona un script de *dm-crypt* para un manejo rápido y flexible.

#### Desmontar y montar manualmente

Para desmontar el contenedor:

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

Para montar el contenedor de nuevo:

```
# losetup /dev/loop0 /bigsecret
# cryptsetup open /dev/loop0 secret
# mount -t ext4 /dev/mapper/secret /mnt/secret

```
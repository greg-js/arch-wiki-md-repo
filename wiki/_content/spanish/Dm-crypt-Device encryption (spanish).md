**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – <a class="mw-selflink selflink">Cifrar dispositivo</a> – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Device_encryption&diff=0&oldid=555421) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Esta sección explica cómo utilizar manualmente *dm-crypt* desde la línea de órdenes para cifrar un sistema.

## Contents

*   [1 Preparación](#Preparación)
*   [2 Utilización de cryptsetup](#Utilización_de_cryptsetup)
    *   [2.1 Contraseñas y claves de cryptsetup](#Contraseñas_y_claves_de_cryptsetup)
*   [3 Opciones de cifrado con dm-crypt](#Opciones_de_cifrado_con_dm-crypt)
    *   [3.1 Opciones de cifrado para la modalidad LUKS](#Opciones_de_cifrado_para_la_modalidad_LUKS)
    *   [3.2 Opciones de cifrado para la modalidad plain](#Opciones_de_cifrado_para_la_modalidad_plain)
*   [4 Cifrar dispositivos con cryptsetup](#Cifrar_dispositivos_con_cryptsetup)
    *   [4.1 Cifrar dispositivos con la modalidad LUKS](#Cifrar_dispositivos_con_la_modalidad_LUKS)
        *   [4.1.1 Formatear particiones LUKS](#Formatear_particiones_LUKS)
            *   [4.1.1.1 Utilizar LUKS para formatear particiones con un archivo de claves](#Utilizar_LUKS_para_formatear_particiones_con_un_archivo_de_claves)
        *   [4.1.2 Desbloquear/mapear particiones LUKS con el mapeador de dispositivos](#Desbloquear/mapear_particiones_LUKS_con_el_mapeador_de_dispositivos)
    *   [4.2 Cifrar dispositivos con la modalidad plain](#Cifrar_dispositivos_con_la_modalidad_plain)
*   [5 Acciones de cryptsetup específicas para LUKS](#Acciones_de_cryptsetup_específicas_para_LUKS)
    *   [5.1 Gestión de claves](#Gestión_de_claves)
        *   [5.1.1 Añadir claves LUKS](#Añadir_claves_LUKS)
        *   [5.1.2 Eliminar claves LUKS](#Eliminar_claves_LUKS)
    *   [5.2 Copia de seguridad y restauración](#Copia_de_seguridad_y_restauración)
        *   [5.2.1 Realizar copia de seguridad utilizando cryptsetup](#Realizar_copia_de_seguridad_utilizando_cryptsetup)
        *   [5.2.2 Restaurar utilizando cryptsetup](#Restaurar_utilizando_cryptsetup)
        *   [5.2.3 Copia de seguridad y restauración manuales](#Copia_de_seguridad_y_restauración_manuales)
    *   [5.3 Volver a cifrar dispositivos](#Volver_a_cifrar_dispositivos)
        *   [5.3.1 Cifrar un sistema de archivos no cifrado](#Cifrar_un_sistema_de_archivos_no_cifrado)
        *   [5.3.2 Recifrar una partición LUKS existente](#Recifrar_una_partición_LUKS_existente)
*   [6 Cambiar el tamaño de dispositivos cifrados](#Cambiar_el_tamaño_de_dispositivos_cifrados)
    *   [6.1 Sistema de archivos de loopback](#Sistema_de_archivos_de_loopback)
*   [7 Archivos de claves](#Archivos_de_claves)
    *   [7.1 Tipos de archivos de claves](#Tipos_de_archivos_de_claves)
        *   [7.1.1 Frase de contraseña](#Frase_de_contraseña)
        *   [7.1.2 Texto aleatorio](#Texto_aleatorio)
        *   [7.1.3 Binario](#Binario)
    *   [7.2 Crear un archivo claves con caracteres aleatorios](#Crear_un_archivo_claves_con_caracteres_aleatorios)
        *   [7.2.1 Almacenar el archivo de claves en un sistema de archivos](#Almacenar_el_archivo_de_claves_en_un_sistema_de_archivos)
            *   [7.2.1.1 Sobrescribir de forma segura los archivos de claves almacenados](#Sobrescribir_de_forma_segura_los_archivos_de_claves_almacenados)
        *   [7.2.2 Almacenar el archivo de claves en ramfs](#Almacenar_el_archivo_de_claves_en_ramfs)
    *   [7.3 Configurar LUKS para que haga uso del archivo de claves](#Configurar_LUKS_para_que_haga_uso_del_archivo_de_claves)
    *   [7.4 Desbloquear manualmente una partición usando un archivo de claves](#Desbloquear_manualmente_una_partición_usando_un_archivo_de_claves)
    *   [7.5 Desbloquear una partición secundaria en el arranque](#Desbloquear_una_partición_secundaria_en_el_arranque)
    *   [7.6 Desbloquear la partición raíz en el arranque](#Desbloquear_la_partición_raíz_en_el_arranque)
        *   [7.6.1 Con un archivo de claves almacenado en un medio externo](#Con_un_archivo_de_claves_almacenado_en_un_medio_externo)
            *   [7.6.1.1 Configurar mkinitcpio](#Configurar_mkinitcpio)
            *   [7.6.1.2 Configurar parámetros del kernel](#Configurar_parámetros_del_kernel)
        *   [7.6.2 Con un archivo de clave incrustado en initramfs](#Con_un_archivo_de_clave_incrustado_en_initramfs)

## Preparación

Antes de usar [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup), debe asegurarse de que el [módulo del kernel](/index.php/Kernel_module "Kernel module") `dm_crypt` esté cargado.

## Utilización de cryptsetup

*Cryptsetup* es la herramienta de línea de órdenes para interactuar con *dm-crypt*, para crear, acceder y gestionar dispositivos cifrados. La herramienta se expandió posteriormente para admitir diferentes tipos de cifrado que dependen de los módulos del kernel de Linux **d**evice-**m**apper y **crypt**ographic. La expansión más notable fue para la extensión de configuración de clave unificada de Linux («*Linux Unified Key Setup*» siglas en inglés [LUKS](https://en.wikipedia.org/wiki/es:LUKS "wikipedia:es:LUKS")), que almacena toda la información de configuración necesaria para dm-crypt en el propio disco y abstrae la partición y la gestión de claves en un intento por mejorar la facilidad de uso. Los dispositivos a los que se accede a través de *device-mapper* se denominan dispositivos de bloque. Para obtener más información, consulte [Disk encryption (Español)#Cifrar dispositivos de bloques](/index.php/Disk_encryption_(Espa%C3%B1ol)#Cifrar_dispositivos_de_bloques "Disk encryption (Español)").

La herramienta se utiliza de la siguiente manera:

```
# cryptsetup <OPCIONES> <acción> <opciones-específicas-de-la-acción> <dispositivo> <nombre_dispositivo_mapeado>

```

Cryptsetup tiene valores predeterminados en su compilación para las opciones y el modo de cifrado, que se utilizarán si no se especifican otros en la línea de órdenes. Mire esto:

```
$ cryptsetup --help

```

que enumera las opciones, las acciones y los parámetros predeterminados para los modos de cifrado en ese orden. Una lista completa de opciones se puede encontrar en la página del manual. Como los diferentes parámetros son obligatorios u opcionales, según el modo de encriptación y la acción, las siguientes secciones señalan las diferencias más destacadas. El cifrado de dispositivos de bloques es rápido, pero la velocidad también importa mucho. Debido a que es difícil cambiar el [algoritmo de cifrado](https://en.wikipedia.org/wiki/es:CS-Cipher "wikipedia:es:CS-Cipher") de un dispositivo de bloque después de la configuración, es importante verificar el rendimiento de *dm-crypt* para los parámetros individuales de antemano:

```
$ cryptsetup benchmark 

```

puede proporcionar orientación sobre la decisión de un algoritmo de cifrado y un tamaño de clave antes de su instalación. Si ciertos cifrados AES sobresalen con un rendimiento considerablemente mayor, estos son probablemente los que tienen soporte de hardware en la CPU.

**Sugerencia:** Es posible que desee practicar el cifrado de un disco duro virtual en una [máquina virtual](/index.php/Category:Virtualization_(Espa%C3%B1ol) "Category:Virtualization (Español)") para aprender.

### Contraseñas y claves de cryptsetup

Un dispositivo de bloque encriptado está protegido por una clave. Una clave es, o bien:

*   una frase de contraseña, ver [Security#Passwords](/index.php/Security#Passwords "Security"); o bien,
*   un archivo de claves, ver [#Archivos de claves](#Archivos_de_claves).

Ambos tipos de clave tienen tamaños máximos predeterminados: las frases de contraseña (o simplemente, contraseña) pueden tener hasta 512 caracteres y los archivos de clave hasta 8192kiB.

Una distinción importante de *LUKS* que se debe tener en cuenta en este punto es que la clave se utiliza para desbloquear la clave maestra de un dispositivo cifrado con LUKS y se puede cambiar con acceso de privilegios de root. Otros modos de cifrado no admiten el cambio de la clave después de la configuración, ya que no emplean una clave maestra para el cifrado. Consulte [Disk encryption (Español)#Cifrar dispositivos de bloques](/index.php/Disk_encryption_(Espa%C3%B1ol)#Cifrar_dispositivos_de_bloques "Disk encryption (Español)") para más detalles.

## Opciones de cifrado con dm-crypt

*Cryptsetup* admite diferentes modos de operación de cifrado para usar con *dm-crypt*:

*   `--type luks` para usarlo por defecto y el más común,
*   `--type luks2` para usar la última versión disponible de luks que permite extensiones adicionales,
*   `--type loopaes`, para un modo heredado de loopaes,
*   `--type tcrypt`, para un modo de compatibilidad con [TrueCrypt](/index.php/TrueCrypt "TrueCrypt").

Las opciones criptográficas básicas para algoritmo de cifrado y [funciones hash](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash") disponibles se pueden utilizar para todos las modalidades y se basan en las características del [backend](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end") [criptográfico](https://en.wikipedia.org/wiki/es:Criptograf%C3%ADa "wikipedia:es:Criptografía") del kernel. Todos los que se cargan en tiempo de ejecución y disponible para usar como opciones se pueden ver con:

```
$ less /proc/crypto 

```

**Sugerencia:** si la lista es corta, ejecute `$ cryptsetup benchmark` que activará la carga de los módulos disponibles.

A continuación se presentan las opciones de cifrado para los modos `luks`, `luks2` y `plain`. Tenga en cuenta que las tablas enumeran las opciones utilizadas en los ejemplos respectivos de este artículo y no todas las disponibles.

### Opciones de cifrado para la modalidad LUKS

La acción *cryptsetup* para configurar un nuevo dispositivo dm-crypt en la modalidad de cifrado LUKS es *luksFormat*. El nombre es engañoso pues no formatea el dispositivo, pero configura el encabezado del dispositivo LUKS y cifra la clave maestra con las opciones criptográficas deseadas.

Como LUKS es el modo de cifrado predeterminado, todo lo que necesita para crear un nuevo dispositivo LUKS con parámetros predeterminados (`-v` es opcional) es:

```
# cryptsetup -v luksFormat *dispositivo*

```

Para que sirva de comparación, podemos especificar las opciones predeterminadas manualmente también:

```
# cryptsetup -v --type luks --cipher aes-xts-plain64 --key-size 256 --hash sha256 --iter-time 2000 --use-urandom --verify-passphrase luksFormat *dispositivo*

```

Los valores predeterminados se comparan con un ejemplo de especificación criptográficamente superior en la tabla siguiente, que se acompañan de comentarios:

| Opciones | Cryptsetup 1.7.0 por defecto | Ejemplo | Comentario |
| --cipher

-c

 | `aes-xts-plain64` | `aes-xts-plain64` | [Release 1.6.0](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.6/v1.6.0-ReleaseNotes) cambió los valores predeterminados a un [algoritmo de cifrado](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") AES en modo [XTS](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory") (ver elemento 5.16 [de FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)). Se recomienda no utilizar el valor predeterminado anterior `--cipher aes-cbc-essiv` debido a su conocido [problema](https://en.wikipedia.org/wiki/Disk_encryption_theory#Cipher-block_chaining_.28CBC.29 "wikipedia:Disk encryption theory") y prácticos [ataques](http://www.jakoblell.com/blog/2013/12/22/practical-malleability-attack-against-cbc-encrypted-luks-partitions/) contra ellos. |
| --key-size

-s

 | `256` | `512` | Por defecto, se utiliza un tamaño de clave de 256 bits. Sin embargo, tenga en cuenta que [XTS divide la clave suministrada a la mitad](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory"), así que para usar AES-256 en lugar de AES-128 debe configurar el tamaño de la clave XTS a `512`. |
| --hash

-h

 | `sha256` | `sha512` | Algoritmo de hash utilizado para [derivación de clave](/index.php/Disk_encryption_(Espa%C3%B1ol)#Metadatos_criptográficos "Disk encryption (Español)"). La versión 1.7.0 cambió los valores predeterminados de `sha1` a `sha256` «*no por razones de seguridad [sino] principalmente para evitar problemas de compatibilidad en sistemas endurecidos donde SHA1 ya está [siendo] eliminado*»[[1]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). El antiguo valor predeterminado de `sha1` todavía se puede utilizar para la compatibilidad con versiones anteriores de *cryptsetup*, ya que es [considerado seguro](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) (ver elemento 5.20). |
| --iter-time

-i

 | `2000` | `5000` | Número de milisegundos para gastar con el procesamiento de la frase de contraseña PBKDF2\. La versión 1.7.0 cambió los valores predeterminados de `1000` a `2000` paraa «*tratar de mantener el recuento de iteraciones PBKDF2 lo suficientemente alto y también aceptable para los usuarios.*»[[2]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). Esta opción solo es relevante para las operaciones LUKS que establecen o cambien frases de contraseña, como *luksFormat* o *luksAddKey*. Al especificar 0 como parámetro, se selecciona el valor predeterminado compilado. |
| --use-{u,}random | `--use-urandom` | `--use-random` | Selecciona qué [generador de números aleatorios](/index.php/Random_number_generator "Random number generator") usar. Por citar la página del manual de cryptsetup: «En una situación de baja entropía (por ejemplo, en un sistema integrado), ambas selecciones son problemáticas. El uso de /dev/urandom puede dar lugar a claves débiles. El uso de /dev/random puede bloquear mucho tiempo, potencialmente para siempre, si no es suficiente la entropía puede ser cosechada por el kernel». |
| --verify-passphrase

-y

 | Yes | - | Por defecto solo para luksFormat y luksAddKey. No hay necesidad de escribir para Arch Linux con la modalidad LUKS en este momento. |

Las propiedades y características de LUKS se describen en la [especificación de LUKS1](https://gitlab.com/cryptsetup/cryptsetup/wikis/Specification) (pdf) y en las especificaciones de [LUKS2](https://gitlab.com/cryptsetup/cryptsetup/blob/master/docs/on-disk-format-luks2.pdf) (pdf).

**Sugerencia:** he aquí la presentación resumida del proyecto de los desarrolladores [devconfcz2016](https://mbroz.fedorapeople.org/talks/DevConf2016/devconf2016-luks2.pdf) (pdf) que motiva la actualización de la especificación principal a LUKS2.

### Opciones de cifrado para la modalidad plain

En la modalidad *plain* de dm-crypt, no hay una clave maestra en el dispositivo, por lo tanto, no es necesario configurarla. En su lugar, las opciones de cifrado que se emplearán se utilizan directamente para crear la asignación entre un disco cifrado y un dispositivo con nombre. El mapeado se puede crear frente a una partición o a un dispositivo completo. En este último caso, ni siquiera se necesita una tabla de particiones.

Para crear una mapeado de modo *plain* con los parámetros predeterminados de cryptsetup:

```
# cryptsetup <opciones> open --type plain <dispositivo> <nombre-dispositivo-mapeado>

```

Al ejecutarlo se le pedirá una contraseña, que debería tener una entropía muy alta. A continuación, se muestra la comparación de los parámetros predeterminados con el ejemplo en [dm-crypt/Encrypting an entire system (Español)#Modalidad plain de dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Modalidad_plain_de_dm-crypt "Dm-crypt/Encrypting an entire system (Español)")

| Opción | Cryptsetup 1.7.0 por defecto | Ejemplo | Comentario |
| --hash

-h

 | `ripemd160` | - | El hash se utiliza para crear la clave desde la frase de contraseña; no se utiliza en un archivo de claves. |
| --cipher

-c

 | `aes-cbc-essiv:sha256` | `twofish-xts-plain64` | El cifrado consta de tres partes: generador cipher-chainmode-IV (vector de inicialización). Consulte [Disk encryption (Español)#Algoritmos de cifrado y modalidades de operación](/index.php/Disk_encryption_(Espa%C3%B1ol)#Algoritmos_de_cifrado_y_modalidades_de_operación "Disk encryption (Español)") para obtener una explicación de esta configuración, y la [DMCrypt documentación](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) para algunas de las opciones disponibles. |
| --key-size

-s

 | `256` | `512` | El tamaño de la clave (en bits). El tamaño dependerá del algoritmo que se use y también del modo de cadena (chainmode) en uso. El modo Xts requiere el doble del tamaño que la clave de cbc. |
| --offset

-o

 | `0` | `0` | El desplazamiento desde el principio del disco de destino (en bytes) a partir del cual se inicia el mapeado |
| --key-file

-d

 | por defecto utiliza una frase de contraseña | `/dev/sd*Z*` (o, por ejemplo, `/boot/keyfile.enc`) | El dispositivo o archivo que se utilizará como clave. Consulte [#Archivos de claves](#Archivos_de_claves) para más detalles. |
| --keyfile-offset | `0` | `0` | Desplazamiento desde el principio del archivo donde se inicia la clave (en bytes). Esta opción es compatible desde *cryptsetup* 1.6.7 en adelante. |
| --keyfile-size

-l

 | `8192kB` | - (se aplica por defecto) | Limita los bytes leídos del archivo clave. Esta opción es compatible desde *cryptsetup* 1.6.7 en adelante. |

Utilizando el dispositivo `/dev/sd*X*`, la columna de ejemplo de arriba daría como resultado:

```
# cryptsetup --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd*Z* --key-size=512 open --type=plain /dev/sdX enc

```

A diferencia del cifrado con LUKS, la orden anterior debe ejecutarse *en su totalidad* siempre que el mapeado deba restablecerse, por lo que es importante recordar los datos de cifrado, el hash y el archivo claves. Ahora podemos comprobar que el mapeo se ha realizado:

```
# fdisk -l

```

Debería existir una entrada para `/dev/mapper/enc`.

## Cifrar dispositivos con cryptsetup

Esta sección muestra cómo emplear las opciones para crear nuevos dispositivos de bloques encriptados y acceder a ellos manualmente.

**Advertencia:** GRUB no admite encabezados LUKS2\. Por lo tanto, si planea [desbloquear con GRUB una partición de arranque cifrada](/index.php/GRUB_(Espa%C3%B1ol)#Partición_de_arranque "GRUB (Español)"), no especifique `luks2` para el tipo de parámetro de cifrado en particiones de arranque.

### Cifrar dispositivos con la modalidad LUKS

#### Formatear particiones LUKS

Para configurar una partición como una partición cifrada con LUKS, ejecute:

```
# cryptsetup luksFormat --type luks2 *dispositivo*

```

A continuación, se le solicitará que ingrese una contraseña y la verifique.

Consulte [#Opciones de cifrado para la modalidad LUKS](#Opciones_de_cifrado_para_la_modalidad_LUKS) para ver las opciones de la línea de órdenes.

Puede consultar los resultados con:

```
# cryptsetup luksDump *dispositivo*

```

Notará que el volcado no solo muestra la información del algoritmo de cifrado del encabezado, sino también las ranuras de claves en uso para la partición LUKS.

El siguiente ejemplo creará una partición raíz cifrada en `/dev/sda1` utilizando el algoritmo de cifrado [AES](https://en.wikipedia.org/wiki/es:Advanced_Encryption_Standard "wikipedia:es:Advanced Encryption Standard") predeterminado en modo XTS con un cifrado efectivo de 256 bits:

```
# cryptsetup -s 512 luksFormat --type luks2 /dev/sda1

```

##### Utilizar LUKS para formatear particiones con un archivo de claves

Al crear una nueva partición encriptada con LUKS, se puede asociar un archivo de claves con la partición al crearla, ejecutando:

```
# cryptsetup luksFormat --type luks2 *dispositivo* */ruta/a/archivo_de_claves*

```

Consulte [#Archivos de claves](#Archivos_de_claves) para obtener instrucciones sobre cómo generar y gestionar archivos de claves.

#### Desbloquear/mapear particiones LUKS con el mapeador de dispositivos

Una vez que se han creado las particiones LUKS, se pueden desbloquear.

El proceso de desbloqueo asignará a las particiones un nuevo nombre de dispositivo utilizando el mapeador de dispositivos («*device mapper*»). Esto alerta al kernel de que el `*dispositivo*` es, en realidad, un dispositivo cifrado y debe redireccionarlo a través de LUKS utilizando `/dev/mapper/*nombre_dispositivo_mapeado*` para no sobrescribir los datos encriptados. Para protegerse contra la sobrescritura accidental, lea acerca de las posibilidades para [realizar una copia de seguridad del encabezado cifrado](#Copia_de_seguridad_y_restauración) después de finalizar la configuración.

Para abrir una partición cifrada con LUKS ejecute:

```
# cryptsetup open *dispositivo* *nombre_dispositivo_mapeado*

```

A continuación, se le solicitará la contraseña para desbloquear la partición. Por lo general, el nombre del dispositivo mapeado es descriptivo de la función de la partición que se le asigna. Por ejemplo, la siguiente orden desbloquea una partición `/dev/sda1` cifrada con luks y le asignamos un dispositivo mapeado llamado `cryptroot`:

```
# cryptsetup open /dev/sda1 cryptroot 

```

Una vez abierta, la dirección del dispositivo de la partición raíz será `/dev/mapper/cryptroot`, en lugar de la partición en sí (por ejemplo, `/dev/sda1`).

Para configurar LVM sobre la capa de cifrado, el dispositivo para el grupo de volúmenes descifrados sería algo como `/dev/mapper/cryptroot`, en lugar de `/dev/sda1`. LVM le dará nombres adicionales a todos los volúmenes lógicos creados, por ejemplo, `/dev/lvmpool/root` y `/dev/lvmpool/swap`.

Para escribir datos encriptados en la partición se debe acceder a través del nombre mapeado del dispositivo. El primer paso de acceso generalmente será [crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)"). Por ejemplo:

```
# mkfs -t ext4 /dev/mapper/cryptroot

```

El dispositivo `/dev/mapper/cryptroot` puede ser [montado](/index.php/Mount "Mount") como cualquier otra partición.

Para cerrar el contenedor luks, desmonte la partición y escriba:

```
# cryptsetup close cryptroot

```

### Cifrar dispositivos con la modalidad plain

La creación y el acceso subsiguiente de un cifrado en modo plain de *dm-crypt* no requieren más que usar la acción *cryptsetup* `open` con los [parámetros](#Opciones_de_cifrado_para_la_modalidad_plain) correctos. Lo siguiente muestra dos ejemplos de dispositivos que no son raíz, pero agrega una peculiaridad al apilar ambos (es decir, el segundo se crea dentro del primero). Obviamente, apilar el cifrado duplica la sobrecarga. El caso usado aquí es simplemente para ilustrar otro ejemplo de la utilzación de la opción del algoritmo de cifrado.

Se crea un primer mapeado con los valores predeterminados del modo plain de *cryptsetup*, como se describe en la columna izquierda de la tabla de arriba

 `# cryptsetup --type plain -v open /dev/sdaX plain1` 
```
Enter passphrase: 
Command successful.

```

Ahora agregamos el segundo dispositivo de bloque en su interior, utilizando diferentes parámetros de cifrado y con un desplazamiento —offset— (opcional), creamos un sistema de archivos y lo montamos:

 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10  open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# lsblk -p` 
```
 NAME                                                     
 /dev/sda                                     
 ├─/dev/sdaX          
 │ └─/dev/mapper/plain1     
 │   └─/dev/mapper/plain2              
 ...

```

```
# mkfs -t ext2 /dev/mapper/plain2
# mount -t ext2 /dev/mapper/plain2 /mnt
# echo "This is stacked. one passphrase per foot to shoot." > /mnt/stacked.txt

```

Cerramos la pila para comprobar que funciona el acceso:

```
# cryptsetup close plain2
# cryptsetup close plain1

```

Primero, intentemos abrir el sistema de archivos directamente:

```
# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/sdaX plain2

```
 `# mount -t ext2 /dev/mapper/plain2 /mnt` 
```
mount: wrong fs type, bad option, bad superblock on /dev/mapper/plain2,
      missing codepage or helper program, or other error

```

¿Por qué no ha funcionado? Porque el bloque de inicio de «plain2» (`10`) todavía está cifrado con el algoritmo de cifrado de «plain1». Solo se puede acceder a través del mapeador apilado. El error es arbitrario, sin embargo, daría el mismo resultado si probráramos con una contraseña incorrecta o con las opciones de cifrado incorrectas. Para la modalidad plain de *dm-crypt*, la acción `open` no generará errores.

Intentémoslo de nuevo en el orden correcto:

```
# cryptsetup close plain2 # mapeador disfuncional del intento anterior

```
 `# cryptsetup --type plain open /dev/sdaX plain1` 
```
Enter passphrase:

```
 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# mount /dev/mapper/plain2 /mnt && cat /mnt/stacked.txt` 
```
This is stacked. one passphrase per foot to shoot.

```

*dm-crypt* también manejará el cifrado apilado con algunos modos mixtos. Por ejemplo, el modo LUKS podría apilarse sobre el mapeador «plain1». Su encabezado se cifraría dentro de «plain1» cuando se cierra.

Disponible solo para la modalidad plain está la opción `--shared`. Con ella, un solo dispositivo se puede segmentar en diferentes mapeadores no superpuestos. Lo hacemos en el siguiente ejemplo, usando un modo de algoritmo de cifrado compatible con *loopaes*, para «plain2» esta vez:

 `# cryptsetup --type plain --offset 0 --size 1000 open /dev/sdaX plain1`  `Enter passphrase:`  `# cryptsetup --type plain --offset 1000 --size 1000 --shared --cipher=aes-cbc-lmk --hash=sha256 open /dev/sdaX plain2`  `Enter passphrase:`  `# lsblk -p` 
```
NAME                    
dev/sdaX                    
├─/dev/sdaX               
│ ├─/dev/mapper/plain1     
│ └─/dev/mapper/plain2     
...

```

Como muestra el árbol del dispositivo, ambos dispositivos mapeados residen en el mismo nivel, es decir, no están apilados y «plain2» se puede abrir individualmente.

## Acciones de cryptsetup específicas para LUKS

### Gestión de claves

Es posible definir hasta 8 claves diferentes por partición LUKS. Esto permite al usuario crear claves de acceso para guardar una copia de respaldo: es lo que llamamos custodia de clave, una clave se usa para el uso diario, otra se mantiene en custodia para obtener acceso a la partición en caso de que se olvide la frase de contraseña diaria o o se pierda/dañe un archivo de claves. También se podría usar una ranura de claves diferente para otorgar acceso a una partición a un usuario emitiéndole una segunda clave y luego revocándosela.

Una vez que se ha creado una partición cifrada, se crea con ella la ranura de claves inicial 0 (si no se ha especificado ninguna otra forma manual). Las ranuras de claves adicionales están numeradas del 1 al 7\. Las ranuras de claves utilizadas se pueden ver emitiendo:

 `# cryptsetup luksDump /dev/<dispositivo> | grep BLED` 
```
Key Slot 0: ENABLED
Key Slot 1: ENABLED
Key Slot 2: ENABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED

```

Donde <dispositivo> es el volumen que contiene el encabezado LUKS. Esta y las demás órdenes en esta sección también funcionan en los archivos de respaldo del encabezado.

#### Añadir claves LUKS

Agregar nuevas ranuras de claves («*keylot*») se logra usando cryptsetup con la acción `luksAddKey`. Por razones de seguridad, se solicitará siempre una clave válida existente («any passphrase») antes de que se pueda ingresar otra nueva, lo cual es aplicable también para dispositivos ya desbloqueados:

 `# cryptsetup luksAddKey /dev/<dispositivo> (/path/to/<additionalkeyfile>)` 
```
Enter any passphrase:
Enter new passphrase for key slot:
Verify passphrase: 

```

Si se proporciona la `/ruta/al/<archivo_de_claves_adicional>`, cryptsetup agregará una nueva ranura de claves para el <archivo_de_claves_adicional>. De lo contrario, se le pedirá una nueva frase de contraseña dos veces. Para usar un *archivo de claves* existente que autorice la acción, la opción `--key-file` o `-d` seguida de la opción «antiguo» <archivo_de_claves> intentará desbloquear todas las ranuras de archivos de claves disponibles:

```
# cryptsetup luksAddKey /dev/<dispositivo> (/path/to/<additionalkeyfile>) -d /path/to/<keyfile>

```

Si está decidido a usar varias claves y cambiarlas o revocarlas después, la opción `--key-slot` o `-S` se puede usar para especificar la ranura en cuestión:

 `# cryptsetup luksAddKey /dev/<dispositivo> -S 6` 
```
Enter any passphrase: 
Enter new passphrase for key slot: 
Verify passphrase:

```
 `# cryptsetup luksDump /dev/sda8 | grep 'Slot 6'` 
```
Key Slot 6: ENABLED

```

Para mostrar una acción asociada en este ejemplo, decidimos cambiar la clave de inmediato:

 `# cryptsetup luksChangeKey /dev/<dispositivo> -S 6` 
```
Enter LUKS passphrase to be changed: 
Enter new LUKS passphrase:

```

Antes de continuar retirándolo.

#### Eliminar claves LUKS

Hay tres acciones diferentes para eliminar claves del encabezado:

*   `luksRemoveKey` se usa para eliminar una clave al especificar su contraseña/archivo de claves.
*   `luksKillSlot` puede usarse para eliminar una clave de una ranura de clave específica (usando otra clave). Obviamente, esto es extremadamente útil si ha olvidado una frase de contraseña, perdió un archivo de claves o no tiene acceso a él.
*   `luksErase` se usa para eliminar rápidamente **todas** las claves activas.

**Advertencia:**

*   ¡Todas las acciones anteriores se pueden usar para eliminar irrevocablemente la última clave activa para un dispositivo cifrado!
*   La orden `luksErase` se agregó en la versión 1.6.4 para acceder rápidamente al dispositivo. ¡Esta acción **no** pedirá una frase de contraseña válida! No [limpia el encabezado de LUKS](/index.php/Dm-crypt/Drive_preparation#Wipe_LUKS_header "Dm-crypt/Drive preparation"), sino todos los conjuntos de claves de una vez y, por lo tanto, no podrá recuperar el acceso a menos que tenga una copia de seguridad válida del encabezado de LUKS .

Para la advertencia anterior, es bueno saber que la clave que queremos **mantener** es válida. Una comprobación fácil es desbloquear el dispositivo con la opción `-v`, que especificará qué ranura ocupa:

 `# cryptsetup -v open /dev/<dispositivo> testcrypt` 
```
Enter passphrase for /dev/<dispositivo>: 
Key slot 1 unlocked.
Command successful.

```

Ahora podemos eliminar la clave agregada en la subsección anterior usando su frase de contraseña:

 `# cryptsetup luksRemoveKey /dev/<dispositivo>` 
```
Enter LUKS passphrase to be deleted:

```

Si hubiéramos usado la misma frase de contraseña para dos ranuras de claves, la primera ranura se borraría ahora. Solo ejecutándolo de nuevo eliminaría la segunda.

Alternativamente, podemos especificar la ranura de la clave:

 ` # cryptsetup luksKillSlot /dev/<dispositivo> 6 ` 
```
Ingrese cualquier frase de contraseña LUKS restante:

```

Tenga en cuenta que en ambos casos, no se requerirá confirmación.

 `# cryptsetup luksKillSlot /dev/<dispositivo> 6` 
```
Enter any remaining LUKS passphrase:

```

Para repetir la advertencia anterior: si se hubiera utilizado la misma frase de contraseña para las ranuras de claves 1 y 6, ambas se habrían eliminado.

### Copia de seguridad y restauración

Si el encabezado de una partición encriptada con LUKS se destruye, no podrá descifrar sus datos. Es un dilema tan grande como olvidar la frase de contraseña o dañar un archivo de claves utilizado para desbloquear la partición. Puede dañarse por un fallo propio al volver a particionar el disco posteriormente o por programas de terceros que malinterpretan la tabla de particiones. Por lo tanto, tener una copia de seguridad del encabezado y almacenarlo en otro disco puede ser una buena idea.

**Nota:** Si una de las frases de acceso de las particiones cifradas con LUKS se ve comprometida, debe revocarla en *cada* copia del encabezado cifrado, incluso aquellas de las que haya realizado una copia de seguridad. De lo contrario, se puede usar una copia de repaldo del encabezado que usa la frase de contraseña comprometida para determinar la clave maestra que, a su vez, puede usarse para descifrar la partición asociada (incluso su partición real, no solo la versión respaldada). Por otro lado, si la clave maestra se ve comprometida, debe volver a cifrar toda la partición. Consulte [FAQ de LUKS](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#6-backup-and-data-recovery) para obtener más detalles.

#### Realizar copia de seguridad utilizando cryptsetup

La acción `luksHeaderBackup` de Cryptsetup almacena una copia de seguridad binaria de la cabecera LUKS y del área de ranuras de claves:

```
# cryptsetup luksHeaderBackup /dev/<dispositivo> --header-backup-file /mnt/<backup>/<file>.img

```

donde <dispositivo> es la partición que contiene el volumen LUKS.

**Sugerencia:** También puede hacer una copia de seguridad del encabezado de texto sin formato en ramfs y cifrarlo en el ejemplo con gpg antes de escribir en el depósito persistente de la copia de seguridad, ejecutando las órdenes de abajo.

```
# mkdir /root/<tmp>/
# mount ramfs /root/<tmp>/ -t ramfs
# cryptsetup luksHeaderBackup /dev/<dispositivo> --header-backup-file /root/<tmp>/<file>.img
# gpg2 --recipient <User ID> --encrypt /root/<tmp>/<file>.img 
# cp /root/<tmp>/<file>.img.gpg /mnt/<backup>/
# umount /root/<tmp>

```

**Advertencia:** Tmpfs puede acudir al disco duro si tiene poca memoria, por lo que no se recomienda aquí.

#### Restaurar utilizando cryptsetup

**Advertencia:** ¡Restaurar el encabezado incorrecto o restaurar una partición sin cifrar causará la pérdida de datos! La acción no puede realizar una verificación sobre si el encabezado es en realidad el correcto para ese dispositivo en particular.

Con el fin de evitar la restauración de un encabezado incorrecto, puede asegurarse de que funciona si lo usa primero como un `--header` remoto:

 `# cryptsetup -v --header /mnt/<backup>/<file>.img open /dev/<dispositivo> test` 
```
Key slot 0 unlocked.
Command successful.

```

```
# mount /dev/mapper/test /mnt/test && ls /mnt/test 
# umount /mnt/test 
# cryptsetup close test 

```

Ahora que la comprobación se realizó correctamente, la restauración se puede realizar:

```
# cryptsetup luksHeaderRestore /dev/<dispositivo> --header-backup-file ./mnt/<backup>/<file>.img

```

Ahora que todas las áreas de las ranuras de claves están sobrescritas; solo las ranuras de claves activas del archivo de respaldo estarán disponibles después de emitir la orden.

#### Copia de seguridad y restauración manuales

El encabezado siempre reside al comienzo del dispositivo y también se puede realizar una copia de seguridad sin acceso a *cryptsetup*. Primero tiene que averiguar el desplazamiento («*offset*») de la carga útil de la partición encriptada:

 `# cryptsetup luksDump /dev/<dispositivo> | grep "Payload offset"` 
```
Payload offset:	4040

```

Segundo, controle el tamaño del sector de la unidad:

 `# fdisk -l /dev/<dispositivo> | grep "Sector size"` 
```
Sector size (logical/physical): 512 bytes / 512 bytes

```

Ahora que conoce los valores, puede hacer una copia de seguridad del encabezado con una simple orden dd:

```
# dd if=/dev/<dispositivo> of=/ruta/a/<archivo>.img bs=512 count=4040

```

y almacenarlo de forma segura.

Luego, se puede realizar una restauración utilizando los mismos valores que los usados cuando se realizó la copia de seguridad:

```
# dd if=./<archivo>.img of=/dev/<dispositivo> bs=512 count=4040

```

### Volver a cifrar dispositivos

El paquete [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) contiene la herramienta *cryptsetup-reencrypt*. Se puede usar para convertir un sistema de archivos sin cifrar existente a uno LUKS cifrado (opción `--new`) y eliminar permanentemente el cifrado LUKS (`--decrypt`) de un dispositivo. Como su nombre sugiere, también se puede usar para volver a cifrar un dispositivo cifrado con LUKS existente, sin embargo, no es posible volver a cifrarlo para un encabezado LUKS separado u otras modalidades de cifrado (por ejemplo, modo plain). Para volver a cifrar es posible cambiar las [#Opciones de cifrado para la modalidad LUKS](#Opciones_de_cifrado_para_la_modalidad_LUKS). Las acciones *cryptsetup-reencrypt* solo se pueden realizar en dispositivos sin montar. Consulte [cryptsetup-reencrypt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup-reencrypt.8) para obtener más información.

Una aplicación del recifrado puede ser asegurar los datos nuevamente después de que una frase de contraseña o [#Archivos de claves](#Archivos_de_claves) hayan sido comprometidos *y* no se puede estar seguro de que no se haya obtenido una copia del encabezado LUKS. Por ejemplo, si solo se ha utilizado el sistema cifrado por una frase de contraseña pero no se ha tenido acceso físico/lógico al dispositivo, sería suficiente cambiar solo la frase de contraseña/clave respectiva ([#Gestión de claves](#Gestión_de_claves).

**Advertencia:** ¡Asegúrese siempre de que esté disponible una **copia de seguridad fiable** y verifique las opciones que especifique antes de usar la herramienta!

A continuación se muestra un ejemplo para cifrar una partición del sistema de archivos sin cifrar, así como un nuevo cifrado de un dispositivo cifrado con LUKS existente.

#### Cifrar un sistema de archivos no cifrado

Un encabezado de cifrado LUKS siempre se almacena al principio del dispositivo. Como a un sistema de archivos existente generalmente se le asignarán todos los sectores de partición, el primer paso es reducirlo para hacer espacio para el encabezado LUKS.

Las algoritmos de cifrado [predeterminado](#Opciones_de_cifrado_para_la_modalidad_LUKS) para cifrar LUKS requieren `4096` sectores de 512 bytes. Verificamos el espacio y lo mantenemos simple al reducir el sistema de archivos `ext4` existente en `/dev/sdaX` a su mínimo actual posible:

```
# umount /mnt

```
 `# e2fsck -f /dev/sdaX` 
```
e2fsck 1.43-WIP (18-May-2015)
Pass 1: Checking inodes, blocks, and sizes
...
/dev/sda6: 12/166320 files (0.0% non-contiguous), 28783/665062 blocks

```
 `# resize2fs -M /dev/sdaX` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/sdaX to 26347 (4k) blocks.
The filesystem on /dev/sdaX is now 26347 (4k) blocks long.

```

Ahora lo ciframos, utilizando el algoritmo de cifrado predeterminado, el cual no tenemos que especificarlo explícitamente.

 `# cryptsetup-reencrypt /dev/sdaX --new  --reduce-device-size 4096S` 
```
Enter new passphrase: 
Verify passphrase:
Finished, time 00:05.126,  952 MiB written, speed 185,7 MiB/s

```

Una vez finalizado, el cifrado se habrá realizado en la partición completa, es decir, no solo el espacio al que se redujo el sistema de archivos (`sdaX` tiene `2.6GiB` y la CPU utilizada en el ejemplo no tiene instrucciones AES de hardware). Como paso final, extendemos nuevamente el sistema de archivos del dispositivo ahora encriptado para que ocupe el espacio disponible:

 `# cryptsetup open /dev/sdaX recrypt` 
```
Enter passphrase for /dev/sdaX: 
...

```
 `# resize2fs /dev/mapper/recrypt` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/mapper/recrypt to 664807 (4k) blocks.
The filesystem on /dev/mapper/recrypt is now 664807 (4k) blocks long.

```

```
# mount /dev/mapper/recrypt /mnt

```

y ya estará hecho.

#### Recifrar una partición LUKS existente

En este ejemplo, se vuelve a cifrar un dispositivo LUKS existente.

**Advertencia:** ¡Vuelva a verificar que se han especificado las opciones de cifrado para *cryptsetup-reencrypt* correctamente y *nunca* recifre sin tener una **copia de seguridad fiable**!

Para volver a cifrar un dispositivo con sus opciones de cifrado existentes, no es necesario especificarlas. Un simple:

 `# cryptsetup-reencrypt /dev/sdaX` 
```
Enter passphrase for key slot 0: 
Progress: 100,0%, ETA 00:00, 2596 MiB written, speed  36,5 MiB/s

```

lo realiza.

Un posible caso de uso es volver a cifrar los dispositivos LUKS que tienen opciones de cifrado no actuales. Además de la advertencia anterior sobre la especificación de las opciones correctamente, la capacidad de cambiar el encabezado LUKS también puede verse limitada por su tamaño. Por ejemplo, si el dispositivo se cifró inicialmente utilizando un algoritmo de cifrado del [modo CBC](https://en.wikipedia.org/wiki/es:Modo_CBC_(Cipher-block_chaining) y un tamaño de clave de 128 bits, el encabezado LUKS tendrá la mitad del tamaño de los `4096` sectores mencionados anteriormente:

 `# cryptsetup luksDump /dev/sdaX |grep -e "mode" -e "Payload" -e "MK bits"` 
```
Cipher mode:   	cbc-essiv:sha256
Payload offset:	**2048**
MK bits:       	128

```

Si bien es posible actualizar el cifrado de un dispositivo de este tipo, actualmente solo es posible en dos pasos. Primero, vuelva a encriptar con las mismas opciones de encriptación, pero use la opción `--reduce-device-size` para hacer el espacio del encabezado LUKS más grande. En segundo lugar, vuelva a cifrar todo el dispositivo con el cifrado deseado. Por este motivo y por el hecho de que se debe crear una copia de seguridad en cualquier caso, la creación de un nuevo dispositivo cifrado para restaurar es siempre la opción más rápida.

## Cambiar el tamaño de dispositivos cifrados

Si un dispositivo de almacenamiento cifrado con dm-crypt se clona (con una herramienta como dd) a otro dispositivo más grande, el dispositivo dm-crypt subyacente debe redimensionarse para usar todo el espacio.

El dispositivo de destino es /dev/sdX2 en este ejemplo, se utilizará todo el espacio disponible adyacente a la partición:

```
# cryptsetup luksOpen /dev/sdX2 sdX2
# cryptsetup resize sdX2

```

Entonces el sistema de archivos subyacente debe ser redimensionado.

### Sistema de archivos de loopback

Suponiendo que un sistema de archivos loopback está montado en `/mnt/secret`, por ejemplo siguiendo a [dm-crypt/Encrypting a non-root file system (Español)#Dispositivo loop](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Dispositivo_loop "Dm-crypt/Encrypting a non-root file system (Español)"), primero desmonte el contenedor cifrado:

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

A continuación, expanda el archivo contenedor con el tamaño de los datos que desea agregar:

**Advertencia:** Tenga cuidado de usar realmente **dos** `>`, o anulará su contenedor actual.

```
# dd if=/dev/urandom bs=1M count=1024 | cat - >> /bigsecret

```

Ahora mapee el contenedor al dispositivo de loop:

```
# losetup /dev/loop0 /bigsecret
# cryptsetup open /dev/loop0 secret

```

Después de esto, cambie el tamaño de la parte cifrada del contenedor al tamaño máximo del archivo contenedor:

```
# cryptsetup resize secret

```

Finalmente, realice una comprobación del sistema de archivos y, si está bien, cambie su tamaño (ejemplo para ext2/3/4):

```
# e2fsck -f /dev/mapper/secret
# resize2fs /dev/mapper/secret

```

Ahora puede montar el contenedor de nuevo:

```
# mount /dev/mapper/secret /mnt/secret

```

## Archivos de claves

**Nota:** Esta sección describe el uso de un archivo de claves de texto plano. Si desea cifrar su archivo de claves dándole una autenticación de dos factores, consulte [Using GPG or OpenSSL Encrypted Keyfiles](/index.php/Dm-crypt/Specialties#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties") para obtener más información, pero no deje de leer esta sección.

**¿Qué es un archivo de claves?**

Un archivo de claves es un archivo cuyos datos se utilizan como frase de contraseña para desbloquear un volumen cifrado. Eso significa que si un archivo de este tipo se pierde o se modifica, ya no será posible descifrar el volumen.

**Sugerencia:** Defina una frase de contraseña además del archivo de claves para el acceso de respaldo a los volúmenes cifrados en caso de que el archivo de claves definido se pierda o cambie.

**¿Por qué usar un archivo de claves?**

Hay muchos tipos de archivos de claves. Cada tipo de archivo de claves utilizado tiene ventajas y desventajas que se resumen a continuación:

### Tipos de archivos de claves

#### Frase de contraseña

Este es un archivo de claves que contiene una frase de contraseña simple. El beneficio de este tipo de archivo de claves es que si se pierde el archivo, los datos que contiene son conocidos y, con suerte, recordados fácilmente por el propietario del volumen cifrado. Sin embargo, la desventaja es que esto no agrega ninguna seguridad al ingresar una frase de contraseña durante la fase inicial del sistema.

Ejemplo: `1234`

**Nota:** El archivo de claves que contiene la contraseña no debe contener una nueva línea en él. Una opción es crearlo usando:
```
# echo -n 'your_passphrase' > /path/to/<keyfile>
# chown root:root /path/to/<keyfile>; chmod 400 /path/to/<keyfile>

```

#### Texto aleatorio

Este es un archivo de claves que contiene un bloque de caracteres aleatorios. La ventaja de este tipo de archivo de claves es que es mucho más resistente a los [ataques de diccionario](https://en.wikipedia.org/wiki/es:Ataque_de_diccionario "wikipedia:es:Ataque de diccionario") que una simple frase de contraseña. Se puede utilizar una fuerza adicional de archivos de claves en esta situación, que es la longitud de los datos utilizados. Dado que no se trata de una cadena que debe memorizar una persona para su entrada, es intrascendente crear archivos que contengan miles de caracteres aleatorios como clave. La desventaja es que si este archivo se pierde o cambia, lo más probable es que no sea posible acceder al volumen cifrado sin una frase de contraseña de respaldo.

Ejemplo: `fjqweifj830149-57 819y4my1-38t1934yt8-91m 34co3;t8y;9p3y-`

#### Binario

Este es un archivo binario que se ha definido como un archivo de claves. Al identificar archivos como candidatos para un archivo de claves, se recomienda elegir archivos que sean relativamente estáticos, como fotos, música, videoclips. La ventaja de estos archivos es que cumplen una doble función que puede dificultar su identificación como archivos de claves. En lugar de tener un archivo de texto con una gran cantidad de texto aleatorio, el archivo de claves se verá como un archivo de imagen normal o un clip de música para el observador casual. La desventaja es que si este archivo se pierde o cambia, lo más probable es que no sea posible acceder al volumen cifrado sin una frase de contraseña de respaldo. Además, existe una pérdida teórica de aleatoriedad en comparación con un archivo de texto generado aleatoriamente. Esto se debe al hecho de que las imágenes, los videos y la música tienen alguna relación intrínseca entre los bits de datos vecinos que no existe para un archivo de texto. Sin embargo, esto es controvertido y nunca ha sido explotado públicamente.

Ejemplo: imágenes, texto, video, ...

### Crear un archivo claves con caracteres aleatorios

#### Almacenar el archivo de claves en un sistema de archivos

Un archivo de claves puede ser de contenido y tamaño arbitrario.

Aquí `dd` se utiliza para generar un archivo de claves de 2048 bytes aleatorios, almacenándolo en el archivo `/etc/mykeyfile`:

```
# dd bs=512 count=4 if=/dev/random of=/etc/mykeyfile

```

Si planea almacenar el archivo de claves en un dispositivo externo, también puede simplemente cambiar el archivo de salida al directorio correspondiente:

```
# dd bs=512 count=4 if=/dev/random of=/media/usbstick/mykeyfile

```

Para denegar cualquier acceso para otros usuarios, entonces limítelo a `root`:

```
# chmod 600 /etc/mykeyfile

```

##### Sobrescribir de forma segura los archivos de claves almacenados

Si almacenó su archivo de claves temporalmente en un dispositivo de almacenamiento físico y desea eliminarlo, recuerde no solo eliminar el archivo de claves sin más, sino usar algo como:

```
# shred --remove --zero mykeyfile

```

para sobrescribirlo de forma segura. Para sistemas de archivos tradicionales como FAT o ext2, esto será suficiente, mientras que en el caso de sistemas de archivos con registro por diario, hardware de memoria flash y otros casos, se recomienda encarecidamente [limpiar todo el dispositivo](/index.php/Securely_wipe_disk "Securely wipe disk").

#### Almacenar el archivo de claves en ramfs

Alternativamente, puede montar un ramfs para almacenar el archivo de claves temporalmente:

```
# mkdir /root/myramfs
# mount ramfs /root/myramfs/ -t ramfs
# cd /root/myramfs

```

La ventaja es que reside en la memoria RAM y no en un disco físico, por lo que no se puede recuperar después de desmontar la ramfs. Después de copiar el archivo de claves en otro sistema de archivos seguro y persistente, desmonte la ramfs nuevamente con:

```
# umount /root/myramfs

```

### Configurar LUKS para que haga uso del archivo de claves

Agregue una ranura de claves para el archivo de claves al encabezado LUKS:

 `# cryptsetup luksAddKey /dev/sda2 /etc/mykeyfile` 
```
Enter any LUKS passphrase:
key slot 0 unlocked.
Command successful.

```

### Desbloquear manualmente una partición usando un archivo de claves

Utilice la opción `--key-file` al abrir el dispositivo LUKS:

```
# cryptsetup open /dev/sda2 *nombre_dispositivo_mapeado* --key-file /etc/mykeyfile

```

### Desbloquear una partición secundaria en el arranque

Si el archivo de claves para un sistema de archivos secundario se almacena dentro de una raíz cifrada, está seguro mientras el sistema está apagado, pero se puede solicitar que desbloquee automáticamente el montaje durante el arranque mediante [crypttab](/index.php/Crypttab "Crypttab"). Siguiendo el primer ejemplo anterior que utiliza [UUID](/index.php/UUID "UUID"):

 `/etc/crypttab` 
```
home    UUID=<UUID identifier>    /etc/mykeyfile

```

es todo lo que necesita para desbloquearlo, y

 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

para montar el dispositivo de bloques LUKS con el archivo de claves generado.

**Sugerencia:** Si prefiere usar un dispositivo de bloque en modo `--plain`, las opciones de cifrado necesarias para desbloquearlo se deben especificar en `/etc/crypttab`. Tenga cuidado de aplicar la solución de systemd mencionada en [crypttab](/index.php/Crypttab "Crypttab") en este caso.

### Desbloquear la partición raíz en el arranque

Esto es simplemente cuestión de configurar [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para incluir los módulos o archivos necesarios y configurar el [parámetro del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") [cryptkey](/index.php/Dm-crypt/System_configuration#cryptkey "Dm-crypt/System configuration") para saber dónde encontrar el archivo de claves.

Dos casos se tratan a continuación:

1.  usar un archivo de claves almacenado en un medio externo (aquí una memoria USB);
2.  usar un archivo de claves incrustado en initramfs.

#### Con un archivo de claves almacenado en un medio externo

##### Configurar mkinitcpio

Debe agregar un módulo en `/etc/mkinitcpio.conf` para el sistema de archivos de la unidad (el módulo `vfat` en el siguiente ejemplo):

```
MODULES=(vfat)

```

En este ejemplo, se supone que utiliza una unidad USB con formato FAT (módulo `vfat`). Reemplace esos nombres de módulos si usa otro sistema de archivos en su memoria USB (por ejemplo, `ext2`) u otra página de códigos. Si el sistema se queja de la existencia de un superbloque defectuoso y una página de códigos incorrecta en el arranque, entonces necesita un módulo de página de códigos adicional para cargar. Por ejemplo, es posible que necesite el módulo `nls_iso8859-1` para la página de códigos `iso8859-1`.

Si tiene un teclado no estadounidense, puede resultar útil cargar la distribución del teclado antes de que se le solicite ingresar la contraseña para desbloquear la partición raíz en el inicio. Para esto, necesitará el hook `keymap` antes de `encrypt`.

[regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

##### Configurar parámetros del kernel

Agregue las siguientes opciones a los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") si usa el hook `encrypt`. Si usa `sd-encrypt` vea [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration").

```
cryptdevice=/dev/*<partición1>*:root cryptkey=/dev/*<partición2>*:<tipo-de-sistema-de-archivos>:<ruta>

```

Por ejemplo:

```
cryptdevice=/dev/sda3:root cryptkey=/dev/sdb1:vfat:/keys/secretkey

```

La elección de un nombre de archivo plano para su clave proporciona un bit de [«seguridad por oscuridad»](https://en.wikipedia.org/wiki/es:Seguridad_por_oscuridad "wikipedia:es:Seguridad por oscuridad"), pero tenga en cuenta que la línea de órdenes del kernel se registra en el log del kernel (*dmesg*). El archivo de claves no puede ser un archivo oculto, lo que significa que el nombre de archivo no puede comenzar con un punto, o el hook `encrypt` no podrá encontrar el archivo de claves durante el proceso de arranque. Alternativamente, se podría ocultar el archivo de claves entre las particiones y usarlo:

```
cryptkey=/dev/sdb1:offset:size

```

Como ventaja, es más difícil eliminar la clave accidentalmente.

No se garantiza que la denominación de nodos de dispositivos como `/dev/sdb1` permanezca igual en todos los reinicios. En su lugar, es más fiable acceder al dispositivo con los [nombre de dispositivo de bloque persistente](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") de udev. Para asegurarse de que el hook `encrypt` encuentre su archivo de claves al leerlo desde un dispositivo de almacenamiento externo, se deben usar nombres de dispositivos de bloques persistentes. Consulte el artículo [persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").

#### Con un archivo de clave incrustado en initramfs

**Advertencia:** Utilice un archivo de claves incrustado **solo** si tiene de antemano algún tipo de mecanismo de autenticación que proteja suficientemente el archivo de claves. De lo contrario, se producirá el descifrado automático, anulando por completo el propósito de bloquear el cifrado del dispositivo.

Este método permite usar un archivo de claves con un nombre especial que se incrustará en [initramfs](/index.php/Initramfs "Initramfs") y se rescatará por el [hook](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `encrypt` para desbloquear el sistema de archivos raíz (`cryptdevice`) automáticamente. Puede ser útil aplicar cuando se usa la función [GRUB early cryptodisk](/index.php/GRUB#Boot_partition "GRUB"), para evitar el ingreso de dos frases de contraseña durante el inicio.

El hook `encrypt` permite al usuario especificar un archivo de claves con el parámetro del kernel `cryptkey`: en el caso de initramfs, la sintaxis es `rootfs:*ruta*`. Consulte [dm-crypt/System configuration#cryptkey](/index.php/Dm-crypt/System_configuration#cryptkey "Dm-crypt/System configuration"). Además, este parámetro del kernel utiliza de manera predeterminada `/crypto_keyfile.bin`, y si initramfs contiene una clave válida con este nombre, el descifrado se producirá automáticamente sin necesidad de configurar el parámetro `cryptkey`.

Si usa `sd-encrypt` en lugar de `encrypt`, especifique la ubicación del archivo de claves con el parámetro del kernel `rd.luks.key`. Consulte [dm-crypt/System configuration#rd.luks.key](/index.php/Dm-crypt/System_configuration#rd.luks.key "Dm-crypt/System configuration").

[Genere el archivo de claves](#Crear_un_archivo_claves_con_caracteres_aleatorios), otórguele los permisos adecuados y [agréguelo como una clave LUKS](#Añadir_claves_LUKS):

```
# dd bs=512 count=4 if=/dev/random of=/crypto_keyfile.bin
# chmod 000 /crypto_keyfile.bin
# chmod 600 /boot/initramfs-linux*
# cryptsetup luksAddKey /dev/sdX# /crypto_keyfile.bin

```

**Advertencia:** Cuando los permisos de initramfs están configurados en 644 (por defecto), todos los usuarios podrán volcar el archivo de claves. Asegúrese de que los permisos sigan siendo 600 si instala un nuevo kernel.

Incluya la clave en la [matriz de FILES de mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#BINARIOS_y_ARCHIVOS "Mkinitcpio (Español)"):

 `/etc/mkinitcpio.conf`  `FILES=(/crypto_keyfile.bin)` 

Finalmente [regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

En el siguiente reinicio, solo debe ingresar la frase de contraseña de descifrado del contenedor una vez.

([fuente](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/#bonus-login-once))
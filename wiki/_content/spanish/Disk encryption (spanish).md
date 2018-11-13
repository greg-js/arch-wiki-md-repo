**Estado de la traducción**
Este artículo es una traducción de [Disk encryption](/index.php/Disk_encryption "Disk encryption"), revisada por última vez el **2018-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Disk_encryption&diff=0&oldid=543198) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [eCryptfs](/index.php/ECryptfs "ECryptfs")
*   [EncFS](/index.php/EncFS "EncFS")
*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [Tomb](/index.php/Tomb "Tomb")
*   [tcplay](/index.php/Tcplay "Tcplay")
*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives")

Este artículo trata sobre el software de [cifrado de discos](https://en.wikipedia.org/wiki/es:Cifrado_de_disco o directorio. Ejemplos de dispositivos de bloque son discos duros, unidades flash y DVD.

El cifrado de disco solo debe ser visto como un complemento a los mecanismos de seguridad existentes en el sistema operativo —se enfoca a asegurar el acceso físico fuera de línea—, al tiempo que se delega en *otras* partes del sistema que proporcinan elementos confiables como la seguridad de la red y la seguridad del usuario basada en el control de acceso.

## Contents

*   [1 ¿Por qué utilizar la criptografía?](#¿Por_qué_utilizar_la_criptografía?)
*   [2 Cifrar datos del sistema](#Cifrar_datos_del_sistema)
*   [3 Métodos disponibles](#Métodos_disponibles)
    *   [3.1 Cifrar sistemas de archivos apilados](#Cifrar_sistemas_de_archivos_apilados)
        *   [3.1.1 Optimizar el almacenamiento en la nube](#Optimizar_el_almacenamiento_en_la_nube)
    *   [3.2 Cifrar dispositivos de bloques](#Cifrar_dispositivos_de_bloques)
    *   [3.3 Cifrar dispositivo de bloques vs cifrar de sistema de archivos apilados](#Cifrar_dispositivo_de_bloques_vs_cifrar_de_sistema_de_archivos_apilados)
    *   [3.4 Cuadro comparativo](#Cuadro_comparativo)
*   [4 Preparación](#Preparación)
    *   [4.1 Elegir una configuración](#Elegir_una_configuración)
    *   [4.2 Ejemplos](#Ejemplos)
    *   [4.3 Elegir una frase de acceso sólida](#Elegir_una_frase_de_acceso_sólida)
    *   [4.4 Preparar el disco](#Preparar_el_disco)
*   [5 Cómo funciona el cifrado](#Cómo_funciona_el_cifrado)
    *   [5.1 Principio básico](#Principio_básico)
    *   [5.2 Claves, archivo de claves y frase de acceso](#Claves,_archivo_de_claves_y_frase_de_acceso)
    *   [5.3 Metadatos criptográficos](#Metadatos_criptográficos)
    *   [5.4 Algoritmos de cifrado y modalidades de operación](#Algoritmos_de_cifrado_y_modalidades_de_operación)
    *   [5.5 Negabilidad plausible](#Negabilidad_plausible)

## ¿Por qué utilizar la criptografía?

El cifrado de discos garantiza que los archivos siempre se almacenan en el disco de forma cifrada. Los archivos solo están disponibles en forma legible para el sistema operativo y las aplicaciones, mientras el sistema está funcionando y desbloqueado por un usuario de confianza. Una persona no autorizada que mire el contenido del disco directamente solo encontrará datos aleatorios confusos en lugar de los archivos reales.

Por ejemplo, esto sirve para evitar la visualización no autorizada de los datos cuando el ordenador o el disco duro se encuentre:

*   situado en un lugar donde personas que no son de confianza pueden tener acceso a él mientras se está ausente,
*   perdido o robado, cosa que puede ocurrir a portátiles, netbooks o dispositivos de almacenamiento externo,
*   en el taller de reparaciones,
*   desechados después del final de su vida útil.

Además, el cifrado del disco también se puede utilizar para añadir un plus de seguridad frente a los intentos no autorizados de manipulación del sistema operativo, por ejemplo, instalando [keyloggers](https://en.wikipedia.org/wiki/es:Keylogger por [hacker](https://en.wikipedia.org/wiki/es:Hacker_(seguridad_inform%C3%A1tica) que pueden tener acceso físico al sistema, mientras se está ausente.

**Advertencia:** El cifrado de discos **no** protege los datos contra todas las amenazas

Se seguirá siendo vulnerable a:

*   Los atacantes que pueden irrumpir en su sistema (por ejemplo, a través de Internet) mientras se está funcionando y después de que se han desbloqueado y montado las partes cifradas del disco.
*   Los atacantes que son capaces de tener acceso físico al ordenador mientras está en ejecución (incluso si se utiliza un screenlocker), o muy poco *después* de haberlo ejecutado, si tienen los recursos para llevar a cabo un [ataque de arranque en frío](https://en.wikipedia.org/wiki/es:Ataque_de_arranque_en_fr%C3%ADo "wikipedia:es:Ataque de arranque en frío").
*   Una entidad gubernamental, que no solo cuenta con los recursos para realizar fácilmente los ataques anteriores, sino que también puede simplemente obligar a renunciar a sus claves/frases de acceso mediante diversas técnicas de [coerción](https://en.wikipedia.org/wiki/es:Coerci%C3%B3n "wikipedia:es:Coerción"). En la mayoría de los países no democráticos de todo el mundo, así como en los EE.UU. y el Reino Unido, puede ser legal para las agencias de seguridad acceder si tienen sospechas de que se podría estar ocultando algo de interés.

Se requiere una fuerte configuración de cifrado de disco (por ejemplo, el cifrado completo del sistema con comprobación de su autenticidad y sin partición de arranque en modo texto plano) para tener una cierta ventaja contra los atacantes profesionales que son capaces de alterar el sistema *antes* de que lo utilice. Y aun así no es seguro de que realmente se pueda prevenir todo tipo de manipulación (por ejemplo, keyloggers tipo hardware). El mejor remedio podría ser el [cifrado de disco completo basado en hardware](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption") y la [computación confiable](https://en.wikipedia.org/wiki/es:Trusted_Computing "wikipedia:es:Trusted Computing").

**Advertencia:** El cifrado de discos tampoco lo protegerá contra alguien que simplemente [borre el disco](/index.php/Securely_wipe_disk "Securely wipe disk"). Es recomendable realizar [copias de respaldo regulares](/index.php/Backup_programs "Backup programs") para mantener sus datos protegidos.

## Cifrar datos del sistema

Cuando solo se cifra los datos del propio usuario (a menudo situado en el directorio `/home` o en un medio extraíble como un DVD de datos), el cifrado de datos es el uso más simple y menos intrusivo del cifrado de discos, pero tiene algunos inconvenientes significativos. En los sistemas informáticos modernos, hay muchos procesos ejecutados en segundo plano que puede almacenar, por ejemplo en caché, información sobre los datos del usuario o partes de datos en zonas no cifrados del disco duro, como:

*   particiones swap
    *   (posibles remedios: desactivar swap o realizar el [cifrado del espacio de intercambio](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") también)
*   `/tmp` ( archivos temporales creados por las aplicaciones del usuario)
    *   (posibles remedios: evitar este tipo de aplicaciones; montar `/tmp` dentro de [ramdisk](/index.php/Ramdisk "Ramdisk"))
*   `/var` (archivos de registros, bases de datos y similares; por ejemplo, mlocate almacena un índice de todos los nombres de los archivos en `/var/lib/mlocate/mlocate.db`)

La solución es cifrar los datos del sistema y del usuario, evitando el acceso físico no autorizado a los datos privados que el sistema puede almacenar en la memoria caché. Sin embargo, esto tiene la desventaja de que el desbloqueo de las partes cifradas del disco tiene que ocurrir en el momento del arranque. Otro beneficio del cifrado de datos del sistema es que complica la instalación de malware como [keyloggers](https://en.wikipedia.org/wiki/es:Keylogger "wikipedia:es:Keylogger") o [rootkits](https://en.wikipedia.org/wiki/es:Rootkit "wikipedia:es:Rootkit") para alguien con acceso físico.

## Métodos disponibles

Todos los métodos de cifrado de discos operan de tal manera que a pesar de que el disco en realidad posee los datos cifrados, el sistema operativo y las aplicaciones los «ven» como sus correspondientes datos legibles normales, siempre y cuando el contenedor cifrado (es decir, la parte lógica del disco que contiene los datos cifrados) haya sido «desbloqueado» y montado.

Para que esto suceda, cierta «información secreta» (por lo general en forma de un archivo de claves y/o frase de acceso) debe ser suministrada por el usuario, de la cual, se deriva la clave de cifrado real (y se almacena en el llavero del kernel mientras dure la sesión).

Si no se está completamente familiarizado con este tipo de operaciones, lea también la sección siguiente [#Cómo funciona el cifrado](#Cómo_funciona_el_cifrado).

Los métodos de cifrado del disco disponibles se pueden separar en dos tipos por su capa de operación:

### Cifrar sistemas de archivos apilados

Las soluciones del cifrado del sistema de archivos apilados se implementan como una capa que se superpone en la parte superior de un sistema de archivos existente, haciendo que todos los archivos escritos a una carpeta habilitada para cifrarlos se cifren sobre la marcha antes de que el sistema de archivos subyacente los grabe en el disco, y se descifran cuando el sistema de archivos los lee desde el disco. De esta manera, los archivos se almacenan en el sistema de archivos anfitrión en forma cifrada (lo que significa que sus contenidos y, por lo general, también sus nombres de archivo/carpeta, se sustituyen por datos aleatorios de más o menos la misma longitud), pero, aparte, siguen existiendo en ese sistema de archivos como lo harían sin cifrar, a modo de archivos normales / enlaces simbólicos / enlaces duros / etc.

La forma en que se implementa consiste en que para desbloquear la carpeta donde se almacenan los archivos cifrados en bruto en el sistema de archivos anfitrión («directorio inferior»), ésta debe montarse ( utilizando un pseudo sistema de archivos apilados especial) sobre sí misma u, opcionalmente, en una ubicación diferente («directorio superior» ), donde los mismos archivos aparecen entonces en forma legible —hasta que se desmonta de nuevo o se apaga el sistema—.

Las soluciones disponibles en esta categoría son [eCryptfs](/index.php/ECryptfs "ECryptfs") y [EncFS](/index.php/EncFS "EncFS").

#### Optimizar el almacenamiento en la nube

Si está implementando un sistema de cifrado de archivos apilados para lograr una sincronización con [prueba de conocimiento nulo](https://en.wikipedia.org/wiki/es:Prueba_de_conocimiento_cero "wikipedia:es:Prueba de conocimiento cero") (en inglés «*Zero-Knowledge*») en ubicaciones controladas por terceros, como los servicios de almacenamiento en la nube, es posible que desee considerar alternativas a eCryptfs y EncFS, ya que no están optimizados para la transmisión de archivos a través de Internet. Hay algunas soluciones diseñadas para este propósito en su lugar:

*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [cryptomator](https://aur.archlinux.org/packages/cryptomator/) (multiplataforma)
*   [cryfs](https://www.archlinux.org/packages/?name=cryfs)

Tenga en cuenta que algunos servicios de almacenamiento en la nube ofrecen cifrado con prueba de conocimiento nulo directamente a través de su propia [aplicaciones de cliete](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet").

### Cifrar dispositivos de bloques

Los métodos de cifrado de dispositivo de bloque, por el contrario, operan como una capa *debajo* del sistema de archivos y se aseguran que todo lo escrito en un determinado dispositivo de bloques (es decir, un disco completo o una partición o un archivo que actúa como un [dispositivo loop](https://en.wikipedia.org/wiki/es:Loop_device "wikipedia:es:Loop device")) quede cifrado. Esto significa que mientras el dispositivo de bloque no está en línea, todo su contenido se parece a una amalgama de datos aleatorios, y no hay forma de determinar qué tipo de sistema de archivos y qué datos contiene. El acceso a los datos ocurre, de nuevo, mediante el montaje del contenedor protegido (en este caso el dispositivo de bloque) a una ubicación arbitraria con un método especial.

Las siguientes soluciones de «cifrado de dispositivos de bloques» están disponibles en Arch Linux:

	loop-AES

	loop-AES es un descendiente de cryptoloop y es una solución segura y rápida para el cifrado del sistema. Sin embargo, loop-AES se considera menos fácil de usar que otras opciones, ya que requiere soporte del kernel no estándar.

	dm-crypt

	[dm-crypt](/index.php/Dm-crypt "Dm-crypt") es la funcionalidad de cifrado para el mapeado de dispositivos estándar proporcionada por el kernel de Linux. Puede ser utilizado directamente por aquellos que les gusta tener un control total sobre todos los aspectos de la partición y la gestión de claves. La gestión de dm -crypt se hace con la utilidad [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) en el espacio de usuario. Se puede utilizar para los siguientes tipos de cifrado de dispositivos de bloques: *LUKS* (por defecto), *plain*, y con carácterística limitadas por dispositivos *loopAES* y *Truecrypt*.

*   LUKS, utilizado por defecto, es una capa adicional eficaz que almacena toda la información necesaria de configuración para dm-crypt, la partición abstacta y la gestión de las claves, en el propio disco en un intento de mejorar la facilidad de uso y la seguridad criptográfica.
*   la modalidad plain de dm-crypt, aun siendo la funcionalidad original del kernel, no tiene la misma capa de eficacia. Es más difícil de obtener la misma fuerza criptográfica con ella. Para lograrlo, las claves deben ser más largas (frases de acceso, archivos de claves) para conseguir dicho resultado. Sin embargo, tiene otras ventajas, que se describen en la sección [#Cifrar dispositivo de bloques vs cifrar de sistema de archivos apilados](#Cifrar_dispositivo_de_bloques_vs_cifrar_de_sistema_de_archivos_apilados).

	TrueCrypt/VeraCrypt

	A portable format, supporting encryption of whole disks/partitions or file containers, with compatibility across all major operating systems. [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") was discontinued by its developers in May 2014\. The VeraCrypt fork was audited in 2016.

Para conocer las implicaciones prácticas de la capa de operación elegida, consulte la siguiente [tabla comparativa](#Cifrar_dispositivo_de_bloques_vs_cifrar_de_sistema_de_archivos_apilados), así como el escrito general para [eCryptfs](http://ksouedu.com/doc/ecryptfs-utils/ecryptfs-faq.html#compare). Vea [Category:Encryption (Español)](/index.php/Category:Encryption_(Espa%C3%B1ol) "Category:Encryption (Español)") para el contenido disponible de los métodos comparados más abajo, así como otras herramientas no incluidas en la tabla.

### Cifrar dispositivo de bloques vs cifrar de sistema de archivos apilados

| Aspecto | Cifrar dispositivos de bloques | Cifrar sistemas de archivos apilados |
| Cifrados | dispositivos de bloque completo | archivos |
| El contenedor para datos encriptados puede ser... | un disco o partición de disco / un archivo que actúa como una partición virtual | un directorio en un sistema de archivos existente |
| Relación con el sistema de archivos | opera debajo de la capa del sistema de archivos: no le importa si el contenido del dispositivo de bloque cifrado es un sistema de archivos, una tabla de particiones, una configuración de LVM o cualquier otra cosa | agrega una capa adicional a un sistema de archivos existente, para cifrar/descifrar automáticamente los archivos cada vez que se escriben/leen |
| Los metadatos del archivo (número de archivos, estructura de directorios, tamaños de archivos, permisos, mtimes, etc.) están cifrados | ✔ | ✘
(los nombres de archivo y directorios pueden estar encriptados) |
| Se puede utilizar para cifrar de forma personalizada unidades de disco duro completas (incluidas las tablas de particionado) | ✔ | ✘ |
| Se puede utilizar para cifrar el espacio de intercambio | ✔ | ✘ |
| Se puede utilizar sin asignar previamente una cantidad fija de espacio para el contenedor de datos cifrados | ✘ | ✔ |
| Se puede utilizar para proteger sistemas de archivos existentes sin acceso a dispositivos de bloque, por ejemplo, NFS o Samba, almacenamiento en la nube, etc. | ✘ | ✔ |
| Permite realizar copias de seguridad de archivos cifrados sin conexión | ✘ | ✔ |

### Cuadro comparativo

La columna «dm-crypt +/- LUKS» denota características de dm-crypt tanto para la modalidad de cifrado LUKS («+») como plain («-»). Si una característica específica requiere el uso de LUKS, esto se indica con «(con LUKS). De la misma manera «(sin LUKS)» indica que el uso de LUKS es contraproducente para lograr la función y el modo plain es el aconsejado.

| Resumen | Loop-AES | [dm-crypt](/index.php/Dm-crypt "Dm-crypt") +/- LUKS | [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") | VeraCrypt | [eCryptfs](/index.php/ECryptfs "ECryptfs") | [EncFS](/index.php/EncFS "EncFS") |
| Tipo de cifrado | cifrado de dispositivos de bloques | cifrado de dispositivos de bloques | cifrado de dispositivos de bloques | cifrado de dispositivos de bloques | cifrado de sistemas de archivos apilados | cifrado de sistemas de archivos apilados |
| Nota | el más longevo; posiblemente el más rápido; funciona en sistemas antiguos | estándar de hecho para el cifrado de dispositivos de bloques en Linux; muy flexible | solución muy portable, bien pulida y controlada pero abandonada | bifurcación mantenida de TrueCrypt | ligeramente más rápido respecto a EncFS; cifra archivos singulares portables a otros sistemas | fácil de usar; permite la adminitración por usuario normal |
| Disponibilidad en Arch Linux | necesita compilar manualmente un kernel personalizado | *módulos del kernel:* ya cargados por el kernel por defecto; *herramientas:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) | [truecrypt](https://www.archlinux.org/packages/?name=truecrypt) | [veracrypt](https://www.archlinux.org/packages/?name=veracrypt) | *módulos del kernel:* ya cargados por el kernel por defecto; *herramientas:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) | [encfs](https://www.archlinux.org/packages/?name=encfs) |
| Licencia | GPL | GPL | TrueCrypt License 3.1 | Apache License 2.0, partes sujetas a la licencia de TrueCrypt v3.0 | GPL | GPL |
| Cifrado implementado en... | en el espacio del kernel | en el espacio del kernel | en el espacio del kernel | en el espacio del kernel | en el espacio del kernel | en el espacio del usuario (utilizando [FUSE](/index.php/FUSE "FUSE")) |
| Metadatos criptográficos almacedados en... | ? | con LUKS: en la cabecera de LUKS | al principio/final del dispositivo (descifrado) | al principio/final del dispositivo (descifrado) ([formato específico](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | en la cabecera de cada archivo cifrado | en el archivo de control al principio de cada contenedor EncFs |
| Clave de cifrado almacenada en... | ? | con LUKS: encabezado LUKS | al principio/final del dispositivo | al principio/final del dispositivo ([formato específico](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | el archivo de claves se puede almacenar en cualquier lugar | el archivo de claves se puede almacenar en cualquier lugar

[[1]](https://github.com/rfjakob/encfs/blob/next/encfs/encfs.pod#environment-variables)[[2]](https://github.com/vgough/encfs/issues/48#issuecomment-69301831)

 |
| Características de usabilidad | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Los usuarios normales pueden crear/eliminar los contenedores para datos cifrados | ✘ | ✘ | ✘ | ✘ | limitada | ✔ |
| Proporciona una interfaz gráfica | ✘ | ✘ | ✔ | ✔ | ✘ | ✔

[opcional](/index.php/EncFS#Gnome_Encfs_Manager "EncFS")

 |
| Soporte para montarse automáticamente al iniciar sesión | ? | ✔ | ✔

con [systemd y /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔

con [systemd y /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔ | ✔ |
| Soporte para desmontarse automáticamente en caso de inactividad | ? | ? | ? | ? | ? | ✔ |
| Características de seguridad | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Algoritmos de cifrado soportados | AES | AES, Anubis, CAST5/6, Twofish, Serpent, Camellia, Blowfish,… (cada algoritmo de cifrado es ofrecido por el Crypto API del kernel) | AES, Twofish, Serpent | AES, Twofish, Serpernt, Camellia, Kuznyechik | AES, Blowfish, Twofish... | AES, Blowfish, Twofish, y cualquier otro algoritmo de cifrado disponible en el sistema |
| Soporte para salting | ? | ✔
(con LUKS) | ✔ | ✔ | ✔ | ? |
| Soporte para múltiples sistemas de cifrado en cascada | ? | No en un solo dispositivo, pero permite conectarse a dispositivos de bloques en cascada | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ? | ✘ |
| Soporte para la difusión del key-slot | ? | ✔
(con LUKS) | ? | ? | ? | ? |
| Protección contra el forzado de clave | ✔ | ✔
(sin LUKS) | ? | ? | ? | ? |
| Soporte para múltiples claves (revocables independientemente) para los mismos datos cifrados | ? | ✔
(con LUKS) | ? | ? | ? | ✘ |
| Características de rendimiento | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Soporte [multithreading](https://en.wikipedia.org/wiki/es:Multihilo "wikipedia:es:Multihilo") | ? | ✔
[[3]](http://kernelnewbies.org/Linux_2_6_38#head-49f5f735853f8cc7c4d89e5c266fe07316b49f4c) | ✔ | ✔ | ? | ? |
| Soporte para cifrado de hardware acelerado | ✔ | ✔ | ✔ | ✔ | ✔ | ✔
[[4]](https://github.com/vgough/encfs/issues/118) |
| Específico del cifrado de dispositivos de bloques | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt |
| Soporte para redimensionar (manualmente) el dispositivo de bloque cifrado in situ | ? | ✔ | ✘ | ✘ |
| Específico del cifrado de sistemas de archivos apilados | eCryptfs | EncFs |
| Sistemas de archivos soportados | ext3, ext4, xfs (con salvedades), jfs, nfs... | ext3, ext4, xfs (con salvedades), jfs, nfs, cifs...

[[5]](https://github.com/vgough/encfs)

 |
| Capacidad para cifrar los nombres de los archivos | ✔ | ✔ |
| Capacidad para *no* cifrar los nombres de los archivos | ✔ | ✔ |
| Optimizado para el manejo de archivos dispersos | ✘ | ✔ |
| compatibilidad y prevalencia | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Versiones del kernel de Linux que lo soportan | 2.0 o posterior | modalidad CBC a partir de 2.6.4, ESSIV 2.6.10, LRW 2.6.20, XTS 2.6.24 | ? | ? | ? | 2.4 o posterior |
| Los datos cifrados también pueden ser leídos desde Windows | ✔
(con [CrossCrypt](https://en.wikipedia.org/wiki/CrossCrypt "wikipedia:CrossCrypt"), [LibreCrypt](https://github.com/t-d-k/LibreCrypt)) | ?
(with [FreeOTFE](https://en.wikipedia.org/wiki/es:FreeOTFE "wikipedia:es:FreeOTFE"), [LibreCrypt](https://github.com/t-d-k/LibreCrypt)) | ✔ | ✔ | ? | ?
[[6]](http://members.ferrara.linux.it/freddy77/encfs.html) |
| Los datos cifrados también pueden ser leídos desde Mac OS X | ? | ? | ✔ | ✔ | ? | ✔
[[7]](https://sites.google.com/a/arg0.net/www/encfs-mac-build) |
| Los datos cifrados también pueden ser leídos desde FreeBSD | ? | ? | ✔

(con VeraCrypt)

 | ✔
 | ? | ✔
[[8]](http://www.freshports.org/sysutils/fusefs-encfs/) |
| Utilizado por | ? | Instalador de Debian/Ubuntu (cifrado del sistema)
Instalador de Fedora | ? | ? | Instalador de Ubuntu (cifrado del directorio home)
Chromium OS (cifrado de los datos del usuario en la memoria caché [[9]](https://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data)) | ? |

1.  Un solo archivo en esos sistemas de archivos podría usarse como un contenedor (dispositivo loop virtual) pero en realidad uno ya no estaría usando el sistema de archivos (y las características que proporciona)

## Preparación

### Elegir una configuración

Qué configuración de cifrado de disco es apropiada para cada usuario dependerá de los propósitos del usuario (léase [#¿Por qué utilizar la criptografía?](#¿Por_qué_utilizar_la_criptografía?) más arriba) y de los parámetros del sistema.

Entre otras, tendrá que responder a las siguientes preguntas:

	¿Contra qué tipo de «ataques» quiere proteger su sistema?

*   Usuario ocasional de ordenador husmeando el disco cuando el sistema está apagado / robado / etc.
*   Criptoanalista profesional que puede conseguir acceso de lectura/escritura repetidamente al sistema antes y después de usarse
*   Ninguno de los anteriores

	¿Qué estrategia de cifrado desea emplear?

*   Cifrado de datos
*   Cifrado del sistema
*   Cualquiera de los anteriores

	¿Cómo deben tratarse swap, `/tmp`, etc.?

*   Ignorar, y con la esperanza de que no se hayan filtrado datos
*   Desactivar o montar como disco de memoria
*   Cifrar *(como parte del cifrado del disco completo o por separado)*

	¿Cómo deben desbloquearse las partes del disco cifradas?

*   Con contraseña/frase de acceso *(igual que la contraseña de inicio de sesión, o por separado)*
*   Con archivo de claves *(por ejemplo, en una memoria USB, que se mantenga en un lugar seguro o portarlo uno mismo)*
*   Con ambas

	¿*Cuándo* deben desbloquearse las partes del disco cifradas?

*   Antes del arranque
*   Durante del arranque
*   Al iniciar sesión
*   Manualmente bajo demanda *(después de iniciar sesión)*

	¿Cómo deben ser acomodados varios usuarios?

*   No hacer nada
*   Usar una clave/frase de acceso compartida
*   Usar claves/frases de acceso emitidas de forma independiente y revocables para la misma parte del disco cifrado
*   Crear partes cifradas separadas del disco para los diferentes usuarios

A continuación, se puede pasar a tomar las decisiones técnicas necesarias (vea [#Métodos disponibles](#Métodos_disponibles) más arriba, y [#Cómo funciona el cifrado](#Cómo_funciona_el_cifrado) más adelante), en relación con:

*   elegir entre cifrar sistemas de archivos apilados *versus* cifrar dispositivos de bloques
*   la gestión de las claves
*   el algoritmo de cifrado y la modalidad de la operación
*   el almacenamiento de los metadatos
*   la ubicación del «directorio inferior» (en caso de cifrado de sistemas de archivos apilados)

### Ejemplos

En la práctica, podría resultar algo así:

	Ejemplo 1

	cifrado sencillo de datos (en disco duro interno), utilizando una carpeta virtual denominada «~/Private» en el directorio home del usuario, cifrado con [EncFS](/index.php/EncFS "EncFS")

*   las versiones cifradas de los archivos serán almacenadas en la carpeta ~/.Private del disco
*   desbloqueada bajo demanda con una frase de acceso dedicada

	Ejemplo 2

	cifrado parcial del sistema con el **directorio home** de cada usuario cifrado con [ECryptfs](/index.php/ECryptfs "ECryptfs")

*   desbloqueado por el respectivo usuario al iniciar sesión, utilizando la frase de acceso
*   las particiones `swap` and `/tmp` serán cifradas con [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)"), utilizando una clave de un solo uso generada automáticamente para casa sesión
*   indexación/caché de contenidos de `/home` por *slocate* (y aplicaciones similares) desactivada.

	Ejemplo 3

	cifrado completo del sistema —disco duro entero, excepto la partición `/boot`)—, (sin embargo, `/boot` puede ser cifrado con [GRUB](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Cifrar_partición_de_arranque_(GRUB) "Dm-crypt/Encrypting an entire system (Español)")) cifrado con [Dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")

*   desbloqueado durante el arranque, mediante frases de contraseña o desde una memoria USB con un archivo de claves
*   se pueden tener diferentes frases/claves por usuario, independientes y revocables
*   el cifrado puede abarcar múltiples unidades o permitir flexibilidad en el esquema de particionado con [LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an entire system (Español)")

	Ejemplo 4

	cifrado completo del sistema oculto/con plain —disco duro entero—, cifrado con [plain dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")

*   arranque desde USB, usando frase de acceso dedicada + lápiz USB que almacena un archivo de claves
*   datos revisados ​​antes de montar la partición
*   `/boot` se encuentra en la mencionada memoria USB

Otras muchas combinaciones son posibles, por supuesto. Se debe planificar cuidadosamente qué tipo de configuración será la apropiada para su sistema.

### Elegir una frase de acceso sólida

Véase [Security#Passwords](/index.php/Security#Passwords "Security").

### Preparar el disco

Antes de configurar el cifrado de un disco (o parte de él), considere realizar previamente un borrado seguro. Esto consiste en sobrescribir todo el disco o la partición con un flujo de bytes cero o bytes aleatorios, y se hace por una o ambas de las siguientes razones:

	Impedir la recuperación de los datos almacenados previamente'

El cifrado del disco no cambia el hecho de que los distintos sectores del mismo solo se sobrescriben bajo demanda, esto es, cuando el sistema de archivos crea o modifica los datos contenidos en esos sectores (véase [#Cómo funciona el cifrado](#Cómo_funciona_el_cifrado) a continuación). Los sectores que el sistema de archivos considera que «no se están utilizando actualmente» no los toca, y todavía pueden contener restos de datos del sistemas de archivos anterior. La única manera de asegurarse de que todos los datos guardados previamente en la unidad no pueden ser [recuperados](https://en.wikipedia.org/wiki/es:Recuperaci%C3%B3n_de_datos "wikipedia:es:Recuperación de datos"), es borrarlos manualmente. Para este propósito, no importa si se utilizan bytes cero o bytes aleatorios (aunque limpiando con bytes cero será mucho más rápido).

	Impedir la divulgación de los patrones de uso de la unidad cifrada

Lo ideal sería que toda la parte cifrada del disco fuera indistinguible desde la uniformidad de datos aleatorios. De esta manera, ninguna persona no autorizada podría saber cuáles y cuántos sectores contienen realmente datos cifrados —que puede ser un objetivo deseable en sí mismo (como parte de la verdadera confidencialidad)—, y que también sirve como una barrera adicional contra los atacantes que traten de romper el cifrado.
Para satisfacer este objetivo, limpiar el disco utilizando bytes aleatorios de alta calidad es crucial.

El segundo objetivo solo tiene sentido en combinación con el cifrado de dispositivos de bloques, ya que en el caso del cifrado de sistemas de archivos apilados, los datos cifrados se pueden localizar fácilmente de todos modos (en forma de archivos cifrados distintos en el sistema de archivos anfitrión). También tenga en cuenta que, incluso si solo se va a cifrar una carpeta en particular, tendrá que borrar la partición entera si quiere deshacerse de los archivos que estaban almacenados previamente en esa carpeta sin cifrar (debido a la [fragmentación del disco](https://en.wikipedia.org/wiki/es:Fragmentaci%C3%B3n_de_un_sistema_de_ficheros "wikipedia:es:Fragmentación de un sistema de ficheros")). Si hay otras carpetas en la misma partición, habrá que hacerles una copia de respaldo y restablecerlas de nuevo más tarde.

Una vez que haya decidido qué tipo de borrado de disco desea realizar, remítase al artículo [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") para conocer instrucciones más técnicas.

**Sugerencia:** Al decidir qué método utilizar para el borrado seguro de una unidad de disco duro, recuerde que esto no será necesario realizarlo más que una vez durante el tiempo que la unidad se utiliza como una unidad cifrada.

## Cómo funciona el cifrado

Esta sección pretende ser una introducción general a los conceptos y procesos que se encuentran en el corazón de las configuraciones habituales del cifrado de discos.

No se entra en detalles técnicos o matemáticos (consulte la literatura apropiada para ello), sino que desea proporcionar a un administrador del sistema una comprensión general sobre cómo las diferentes opciones de configuración (en especial en relación con la gestión de claves) pueden afectar a su usabilidad y seguridad.

### Principio básico

A los efectos del cifrado de discos, cada dispositivo de bloque (o archivo individual en el caso del cifrado de sistemas de archivos apilados) se divide en **sectores** de igual longitud, por ejemplo, 512 bytes (4.096 bits). El cifrado/descifrado se realiza después en función de cada sector, por lo que el sector n del archivo/dispositivo de bloque en el disco almacenará la versión cifrada del sector n de los datos originales.

Cada vez que el sistema operativo o una aplicación solicita un determinado fragmento de datos del archivo/dispositivo de bloque, todo el sector (o sectores) que contienen los datos serán leídos desde el disco, descifrados sobre la marcha y almacenados temporalmente en la memoria:

```
             ╔═══════╗
    sector 1 ║"???.."║
             ╠═══════╣        ╭┈┈┈┈┈┈┈╮
    sector 2 ║"???.."║        ┊ clave ┊
             ╠═══════╣        ╰┈┈┈┬┈┈┈╯
             :       :            │
             ╠═══════╣            ▼             ┣┉┉┉┉┉┉┉┫
    sector n ║"???.."║━━━━━━━(descifrado)━━━━━━▶┋"abc.."┋ sector n
             ╠═══════╣                          ┣┉┉┉┉┉┉┉┫
             :       :
             ╚═══════╝

 Dispositivo de bloque                          datos no cifrados
     o archivo cifrado                          en memoria RAM
           en el disco

```

Del mismo modo, en cada operación de escritura, todos los sectores que se ven afectados deben ser cifrados de nuevo completamente (mientras que el resto de los sectores permanecen intactos).

Con el fin de ser capaz de descifrar/cifrar los datos, el sistema de cifrado del disco necesita saber la «clave» única secreta asociada a él. Cada vez que el dispositivo de bloque o la carpeta en cuestión debe ser montada, su clave correspondiente (llamada a partir de ahora «llave maestra») debe ser suministrada.

La entropía de la clave es de suma importancia para la seguridad del cifrado. Una cadena de bytes generada al azar, de una cierta longitud, por ejemplo, 32 bytes (256 bits), reúne las propiedades deseables, pero no es fácil de recordar ni de aplicar manualmente durante el montaje.

Por esa razón se utilizan dos técnicas auxiliares. La primera es la aplicación de la criptografía para aumentar las propiedades entrópicas de la llave maestra, que, generalmente, incluye una frase de acceso separada legible por los humanos. Para los diferentes tipos de cifrado consulte sus características propias en la lista del [#Cuadro comparativo](#Cuadro_comparativo). El segundo método consiste en crear un archivo de claves con alta entropía y almacenarlo en un medio separado de la unidad que contiene los datos cifrados.

Véase también [Wikipedia:Authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "wikipedia:Authenticated encryption").

### Claves, archivo de claves y frase de acceso

Los siguientes son ejemplos de cómo almacenar y asegurar criptográficamente una llave maestra con un archivo de claves:

	Almacenada en un archivo de claves de texto plano

Almacenar simplemente la llave maestra en un archivo (en formato legible) es la opción más sencilla . El archivo —llamado un «keyfile» o «archivo de claves»— se puede colocar en una memoria USB mantenida en un lugar seguro y que se conecte al ordenador cuando se quieran montar las partes cifradas del disco (por ejemplo, durante el arranque o el inicio de sesión).

	Almacenada en forma de frase de acceso protegida en un archivo de claves o en el propio disco

La llave maestra (y, por lo tanto, los datos cifrados con ella) se puede proteger con una contraseña secreta, que tendrá que recordar e introducir cada vez que desea montar el dispositivo de bloque o carpeta. Véase [#Metadatos criptográficos](#Metadatos_criptográficos) a continuación para obtener más detalles.

	Generada de forma aleatoria sobre la marcha para cada sesión

En algunos casos, por ejemplo, al cifrar el espacio de intercambio o la partición `/tmp`, no es necesario tener una llave maestra permanente en absoluto. Se puede generar de forma aleatoria una llave nueva para un solo uso para cada sesión, sin necesidad de interacción del usuario. Esto significa que una vez desmontada, todos los archivos guardados en la partición en cuestión nunca pueden ser descifrados de nuevo por *nadie* —que para estos casos particulares está perfectamente bien—.

### Metadatos criptográficos

Con frecuencia las técnicas de cifrado utilizan funciones criptográficas para mejorar la seguridad de la llave maestra en sí. En el montaje de los dispositivos cifrados, la contraseña o el archivo de claves se hace pasar a través de dichas funciones y solo el resultado puede desbloquear la llave maestra para descifrar los datos.

Una configuración común es aplicar la llamada «key stretching» («que podríamos traducir como *prolongar la clave*») para la frase de acceso (a través de la «función derivadora de claves»), y utiliza el resultado mejorado como clave de montaje para descifrar la llave maestra vigente (que se ha almacenado previamente de forma cifrada):

```
 ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                               ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
 ┊ frase de acceso de montaje ┊━━━━━━⎛función derivadora⎞━━━━▶┊ clave de montaje ┊
 ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯  ,───⎝     de clave     ⎠     ╰┈┈┈┈┈┈┈┈┬┈┈┈┈┈┈┈┈┈╯
 ╭──────╮                       ╱                                      │
 │ sal  │──────────────────────´                                       │
 ╰──────╯                                                              │
 ╭────────────────────────────╮                                        ▼          ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
 │ llave maestra cifrada      │━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━(descifrado)━━━▶┊ llave maestra ┊
 ╰────────────────────────────╯                                                   ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯

```

La **función derivadora de claves** (por ejemplo PBKDF2 o scrypt) es deliberadamente lenta (se aplican muchas [iteraciones](https://en.wikipedia.org/wiki/es:Iteraci%C3%B3n "wikipedia:es:Iteración") de una [función hash](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash"), por ejemplo, 1.000 iteraciones de HMAC-SHA-512), de modo que los posibles ataques de fuerza bruta destinados a encontrar la frase de acceso se presentan inviables. Para el caso de su utilización normal por un usuario autorizado, solo será necesario realizar el cálculo una vez por sesión, por lo que la pequeña desaceleración no es un problema. También toma un [blob](https://en.wikipedia.org/wiki/es:Binary_large_object "wikipedia:es:Binary large object") adicional de datos, que se denomina [«**sal**»](https://en.wikipedia.org/wiki/es:Sal_(criptografia) "wikipedia:es:Sal (criptografia)"), como un argumento —este se genera aleatoriamente una vez durante la puesta en marcha del cifrado del disco y se almacena sin protección como parte de los metadatos criptográficos—. Debido a que será un valor diferente para cada configuración, esto hace que sea imposible para los atacantes acelerar los ataques de fuerza bruta usando tablas precalculadas para acceder a la función derivadora de claves.

La **llave maestra cifrada** se puede almacenar en el disco junto con los datos cifrados. De esta manera, la confidencialidad de los datos cifrados depende completamente de la frase secreta.

Para aumentar la seguridad se puede almacenar la llave maestra cifrada en un archivo de claves, por ejemplo, en una memoria USB. Esto proporciona **dos factores de autenticación**, a saber: el acceso a los datos cifrados ahora requiere algo que solo usted *sabe* (la frase de acceso), y, además, algo que solo usted *tiene* (el archivo de claves).

Otra forma de lograr un doble factor de autenticación es aumentar el esquema de obtención de claves, previo a su matematización, «combinando» la frase de acceso con la lectura de datos de byte en uno o más archivos externos (situados en una memoria USB o similar), antes de pasarla por la función derivadora de claves.
Los archivos en cuestión pueden ser cualquier cosa, por ejemplo, imágenes JPEG normales, lo que puede ser beneficioso para la [#Negabilidad plausible](#Negabilidad_plausible). Estos, sin embargo, todavía se llaman «keyfiles» en el presente contexto.

Después de que la llave maestra se haya derivado con éxito, esta se almacena de forma segura en la memoria (por ejemplo, en un anillo de claves del kernel), durante el tiempo que esté montado el dispositivo de bloque o carpeta.

Por lo general, sin embargo, no se utiliza para cifrar/descifrar los datos del disco directamente. Por ejemplo, en el caso de cifrado del sistema de archivos apilados, cada archivo puede asignarse automáticamente su propia clave de cifrado. Cada vez que el archivo ha de ser leído/modificado, esta clave del archivo debe primero ser descifrada usando la llave maestra, antes de que pueda ser utilizada por sí para cifrar/descifrar el contenido del archivo:

```
                                ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
                                ┊ llave maestra ┊
   archivo en disco:            ╰┈┈┈┈┈┈┈┬┈┈┈┈┈┈┈╯
  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐         │
  ╎╭─────────────────────────╮╎         ▼         ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
  ╎│ archivo de clave cifrado│━━━━(descifrado)━━━▶┊archivo de clave┊
  ╎╰─────────────────────────╯╎                   ╰┈┈┈┈┈┈┈┬┈┈┈┈┈┈┈┈╯
  ╎┌─────────────────────────┐╎                           ▼                  ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
  ╎│ contenidos del          │◀━━━━━━━━━━━━━━━━━━(cifrado/descifrado)━━━━━━━▶┊ contenidos del  ┊
  ╎│ archivo cifrados        │╎                                              ┊ archivo legibles┊
  ╎└─────────────────────────┘╎                                              └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘

```

De una manera similar, una clave separada (por ejemplo, una por cada carpeta) se puede utilizar para el cifrado de nombres de archivos en el caso del cifrado de sistemas de archivos apilados.

En el caso de dispositivos de bloques cifrados se utiliza una llave maestra por dispositivo y, por lo tanto, para todos los datos del mismo. Algunos métodos ofrecen características para asignar múltiples frases de acceso/archivos de claves para el mismo dispositivo, y otros métodos, en cambio, no. Algunos métodos utilizan funciones mencionadas más arriba para asegurar la llave maestra y otros dan el control sobre la seguridad de la llave completamente al usuario. Se explican dos ejemplos para los parámetros criptográficos usados ​​por [dm-crypt](/index.php/Dm-crypt "Dm-crypt") en las modalidades plain o LUKS.

Al comparar los parámetros utilizados por ambas modalidades se deduce que el modo plain de dm-crypt tiene parámetros relacionados con la forma de localizar el archivo de claves (por ejemplo, `--keyfile-size`, `--keyfile-offset`). El modo LUKS de dm-crypt no necesita esto, ya que cada dispositivo de bloque contiene un encabezado con los metadatos criptográficos al principio. La cabecera incluye el sistema de cifrado utilizado, la llave maestra cifrada en sí y los parámetros necesarios para su derivación para descifrarla. Los últimos parámetros sirven para cambiar el resultado de las opciones que usará la llave maestra durante su cifrado incicial (por ejemplo `--iter-time`, `--use-random`).

Para conocer las ventajas/desventajas de las diferentes técnicas, remítase al anterior [#Cuadro comparativo](#Cuadro_comparativo) o visite páginas más específicas.

Véase también:

*   [Wikipedia:es:Frase de contraseña](https://en.wikipedia.org/wiki/es:Frase_de_contrase%C3%B1a "wikipedia:es:Frase de contraseña")
*   [Wikipedia:es:Criptografía asimétrica](https://en.wikipedia.org/wiki/es:Criptograf%C3%ADa_asim%C3%A9trica "wikipedia:es:Criptografía asimétrica")
*   [Wikipedia:Key management](https://en.wikipedia.org/wiki/Key_management "wikipedia:Key management")
*   [Wikipedia:Key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function "wikipedia:Key derivation function")

### Algoritmos de cifrado y modalidades de operación

El algoritmo real utilizado para servir de traductor entre las piezas de datos no cifradas y las cifradas (llamado «texto plano» y «texto cifrado», respectivamente), que se interrelacionan entre sí a través de una clave de cifrado dada, se llama un «**algoritmo de cifrado**».

El cifrado de discos emplea «algoritmos de cifrado de bloques», que operan sobre bloques de datos de una longitud fija, por ejemplo 16 bytes (128 bits). En el momento de escribir estas líneas, los más usados son:

 tamaño bloque | tamaño clave | comentario |
| [AES](https://en.wikipedia.org/wiki/es:Advanced_Encryption_Standard "wikipedia:es:Advanced Encryption Standard") | 128 bits | 128, 192 o 256 bits | *aprobado por la NSA para la protección de información clasificada «SECRET» y «TOP SECRET» por el gobierno de EE.UU. (cuando se utiliza con un tamaño de clave de 192 o 256 bits)* |
| [Blowfish](https://en.wikipedia.org/wiki/es:Blowfish "wikipedia:es:Blowfish") | 64 bits | 32–448 bits | *uno de los primeros sistemas de cifrado seguro con licencia libre que se puso a disposición del público, por lo tanto, muy bien consolidado en Linux* |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bits | 128, 192 o 256 bits | *desarrollado como sucesor de Blowfish, pero sin haber alcanzado un uso tan amplio* |
| [Serpent](https://en.wikipedia.org/wiki/es:Serpent "wikipedia:es:Serpent") | 128 bits | 128, 192 o 256 bits | Considerado el más seguro de los cinco finalistas de la competición AES[[10]](http://csrc.nist.gov/archive/aes/round2/r2report.pdf)[[11]](https://www.cl.cam.ac.uk/~rja14/Papers/serpentcase.pdf)[[12]](https://www.cl.cam.ac.uk/~rja14/Papers/serpent.pdf). |

Cifrar/descifrar un sector ([véase más arriba](#Principio_básico)) se consigue mediante su división en pequeños bloques, haciéndolos coincidir con el tamaño del bloque cifrado, y siguiendo, después, cierto conjunto de reglas (que antes hemos llamado «**modalidad de operación**») que informan sobre cómo aplicar el algoritmo de cifrado a los bloques individuales.

Aplicar el algoritmo de cifrado sin más a cada bloque por separado sin modificaciones (denominada modalidad «*electronic codebook (ECB)*») no sería seguro, ya que si los mismos 16 bytes de texto plano siempre producen los mismos 16 bytes de texto cifrado, un atacante podría reconocer fácilmente los patrones en el texto cifrado que se almacenan en el disco.

La modalidad más básica (y común) de operar utilizada en la práctica es la denominada «*cipher-block chaining (CBC)*». Al cifrar un bloque de un sector con esta modalidad, cada bloque de datos de texto plano se combina de forma matemática con el texto cifrado del bloque anterior antes de cifrarlo, utilizando el algoritmo de cifrado. Para el primer bloque, ya que no tiene texto cifrado anterior que usar, se utiliza un bloque de datos pregenerado especial almacenado con los metadatos criptográficos del sector y llamado «**vector de inicialización (siglas en inglés IV)**»:

```
                                                   ╭──────────────╮
                                                   │vector de     │
                                                   │inicialización│
                                                   ╰──────┬───────╯
           ╭     ╠══════════╣              ╭─clave        │           ┣┉┉┉┉┉┉┉┉┉┉┫        
           │     ║          ║              ▼              ▼           ┋          ┋          . INICIO
           ┴     ║"????????"║◀━━(algoritmo de cifrado)━━━(+)━━━━━━━━━━┋"Hello, W"┋ bloque  ╱╰────┐
      sector n   ║          ║                                         ┋          ┋ 1       ╲╭────┘
   del archivo   ║          ║─────────────────────────────╮           ┋          ┋          ' 
         o del   ╟──────────║              ╭─clave        │           ┠┈┈┈┈┈┈┈┈┈┈┨
   dispositivo   ║          ║              ▼              ▼           ┋          ┋
     de bloque   ║"????????"║◀━━(algoritmo de cifrado)━━━(+)━━━━━━━━━━┋"orld !!!"┋ bloque
           ┬     ║          ║                                         ┋          ┋ 2
           │     ║          ║──────────────────╮                      ┋          ┋
           │     ╟──────────╢                  │                      ┠┈┈┈┈┈┈┈┈┈┈┨
           │     ║          ║                  ▼                      ┋          ┋
           :     :   ...    :        ...      ...      ...    ...     :   ...    : ...

                texto cifrado                                         texto plano
                     en disco                                         en RAM

```

Al descifrar, el procedimiento se invierte de forma análoga.

Una cosa a destacar es la generación del vector de inicialización único para cada sector. La opción más sencilla consiste en calcularlo de una manera predecible a partir de un valor fácilmente disponible, como puede ser el número del sector. Sin embargo, esto podría permitir que un atacante con acceso reiterado al sistema pudiera realizar el llamado [watermarking attack](https://en.wikipedia.org/wiki/Watermarking_attack "wikipedia:Watermarking attack"). Para evitar esto, un método llamado «Encrypted salt-sector initialization vector (**ESSIV**)» se puede utilizar para generar vectores de inicialización de una manera que hace que se vean completamente aleatorios por un atacante potencial.

También hay otras opciones disponibles, modalidades de operación más complicadas para cifrar el disco, que ya ofrecen seguridad integrada contra este tipo de ataques (y, por lo tanto, no requieren ESSIV). Otras opciones también pueden garantizar, además, la autenticidad de los datos cifrados (es decir, confirmar que no se han modificado/corrompido por alguien que no tiene acceso a la clave).

Véase también:

*   [Wikipedia:Disk encryption theory](https://en.wikipedia.org/wiki/Disk_encryption_theory "wikipedia:Disk encryption theory")
*   [Wikipedia:es:Cifrado por bloques](https://en.wikipedia.org/wiki/es:Cifrado_por_bloques "wikipedia:es:Cifrado por bloques")
*   [Wikipedia:es:Modos de operación de una unidad de cifrado por bloques](https://en.wikipedia.org/wiki/es:Modos_de_operaci%C3%B3n_de_una_unidad_de_cifrado_por_bloques "wikipedia:es:Modos de operación de una unidad de cifrado por bloques")

### Negabilidad plausible

Véase [Wikipedia:Plausible deniability](https://en.wikipedia.org/wiki/Plausible_deniability "wikipedia:Plausible deniability")
Artículos relacionados

*   [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")
*   [GnuPG (Español)](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [eCryptfs](/index.php/ECryptfs "ECryptfs")
*   [EncFS](/index.php/EncFS "EncFS")
*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [Tomb](/index.php/Tomb "Tomb")
*   [tcplay](/index.php/Tcplay "Tcplay")
*   [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives")

**Estado de la traducción:** este artículo es una versión traducida de [Disk encryption](/index.php/Disk_encryption "Disk encryption"). Fecha de la última traducción/revisión: **2015-06-21**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Disk_encryption&diff=0&oldid=378165).

En este artículo se analizan las técnicas comunes disponibles en Arch Linux para proteger criptográficamente una parte lógica de un disco de almacenamiento (carpeta, partición, disco completo, ...), de modo que todos los datos que se escriban en él se cifren automáticamente y descifren sobre la marcha cuando se lee de nuevo.

«Los discos de almacenamiento» en el presente contexto comprenden los discos duros del ordenador, los dispositivos externos, tales como unidades flash USB o DVD, así como los discos *virtuales* de almacenamiento, tales como los dispositivos [loop-back](https://en.wikipedia.org/wiki/es:Loopback "wikipedia:es:Loopback") o de almacenamiento en la nube *(siempre y cuando Arch Linux puede tratarlos como un dispositivo de bloques o un sistema de archivos)*.

Si ya sabe *qué* desea proteger y *cómo* desea cifrarlo, se le anima a dirigirse directamente a los *artículos relacionados* que figuran en la parte derecha.

## Contents

*   [1 ¿Por qué utilizar la criptografía?](#.C2.BFPor_qu.C3.A9_utilizar_la_criptograf.C3.ADa.3F)
*   [2 Cifrar datos *versus* cifrar sistema](#Cifrar_datos_versus_cifrar_sistema)
*   [3 Métodos disponibles](#M.C3.A9todos_disponibles)
    *   [3.1 Cifrar sistemas de archivos apilados](#Cifrar_sistemas_de_archivos_apilados)
    *   [3.2 Cifrar dispositivos de bloques](#Cifrar_dispositivos_de_bloques)
    *   [3.3 Cuadro comparativo](#Cuadro_comparativo)
        *   [3.3.1 *sinopsis*](#sinopsis)
        *   [3.3.2 *características básicas*](#caracter.C3.ADsticas_b.C3.A1sicas)
        *   [3.3.3 *implicaciones prácticas*](#implicaciones_pr.C3.A1cticas)
        *   [3.3.4 *características de usabilidad*](#caracter.C3.ADsticas_de_usabilidad)
        *   [3.3.5 *características de seguridad*](#caracter.C3.ADsticas_de_seguridad)
        *   [3.3.6 *características de rendimiento*](#caracter.C3.ADsticas_de_rendimiento)
        *   [3.3.7 *específico del cifrado de dispositivos de bloques*](#espec.C3.ADfico_del_cifrado_de_dispositivos_de_bloques)
        *   [3.3.8 *específico del cifrado de sistemas de archivos apilados*](#espec.C3.ADfico_del_cifrado_de_sistemas_de_archivos_apilados)
        *   [3.3.9 *compatibilidad y prevalencia*](#compatibilidad_y_prevalencia)
*   [4 Preparación](#Preparaci.C3.B3n)
    *   [4.1 Elegir una configuración](#Elegir_una_configuraci.C3.B3n)
    *   [4.2 Ejemplos](#Ejemplos)
    *   [4.3 Elegir una frase de acceso sólida](#Elegir_una_frase_de_acceso_s.C3.B3lida)
    *   [4.4 Preparar el disco](#Preparar_el_disco)
*   [5 Cómo funciona el cifrado](#C.C3.B3mo_funciona_el_cifrado)
    *   [5.1 Principio básico](#Principio_b.C3.A1sico)
    *   [5.2 Claves, archivo de claves y frase de acceso](#Claves.2C_archivo_de_claves_y_frase_de_acceso)
    *   [5.3 Metadatos criptográficos](#Metadatos_criptogr.C3.A1ficos)
    *   [5.4 Algoritmos de cifrado y modalidades de operación](#Algoritmos_de_cifrado_y_modalidades_de_operaci.C3.B3n)
    *   [5.5 Negabilidad plausible](#Negabilidad_plausible)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## ¿Por qué utilizar la criptografía?

El cifrado de discos garantiza que los archivos siempre se almacenan en el disco de forma cifrada. Los archivos solo están disponibles en forma legible para el sistema operativo y las aplicaciones, mientras el sistema está funcionando y desbloqueado por un usuario de confianza. Una persona no autorizada que mire el contenido del disco directamente solo encontrará datos aleatorios confusos en lugar de los archivos reales.

Por ejemplo, esto sirve para evitar la visualización no autorizada de los datos cuando el ordenador o el disco duro se encuentre:

*   situado en un lugar donde personas que no son de confianza pueden tener acceso a él mientras se está ausente,
*   perdido o robado, cosa que puede ocurrir a portátiles, netbooks o dispositivos de almacenamiento externo,
*   en el taller de reparaciones,
*   desechados después del final de su vida útil.

Además, el cifrado del disco también se puede utilizar para añadir un plus de seguridad frente a los intentos no autorizados de manipulación del sistema operativo, por ejemplo, instalando [keyloggers](https://en.wikipedia.org/wiki/es:Keylogger "wikipedia:es:Keylogger") o troyanos por «crackers» que pueden tener acceso físico al sistema, mientras se está ausente.

**Advertencia:** El cifrado de discos **no** protege los datos contra todas las amenazas

Se seguirá siendo vulnerable a:

*   Los atacantes que pueden irrumpir en su sistema (por ejemplo, a través de Internet) mientras se está funcionando y después de que se han desbloqueado y montado las partes cifradas del disco.
*   Los atacantes que son capaces de tener acceso físico al ordenador mientras está en ejecución (incluso si se utiliza un screenlocker), o muy poco *después* de haberlo ejecutado, si tienen los recursos para llevar a cabo un [ataque de arranque en frío](https://en.wikipedia.org/wiki/Cold_boot_attack "wikipedia:Cold boot attack").
*   Una entidad gubernamental, que no solo cuenta con los recursos para realizar fácilmente los ataques anteriores, sino que también puede simplemente obligar a renunciar a sus claves/frases de acceso mediante diversas técnicas de [coerción](https://en.wikipedia.org/wiki/Coercion "wikipedia:Coercion"). En la mayoría de los países no democráticos de todo el mundo, así como en los EE.UU. y el Reino Unido, puede ser legal para las agencias de seguridad acceder si tienen sospechas de que se podría estar ocultando algo de interés.

Se requiere una fuerte configuración de cifrado de disco (por ejemplo, el cifrado completo del sistema con comprobación de su autenticidad y sin partición de arranque en modo texto plano) para tener una cierta ventaja contra los atacantes profesionales que son capaces de alterar el sistema *antes* de que lo utilice. Y aun así no es seguro de que realmente se pueda prevenir todo tipo de manipulación (por ejemplo, keyloggers tipo hardware). El mejor remedio podría ser el [cifrado de disco completo basado en hardware](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption") y la [computación confiable](https://en.wikipedia.org/wiki/es:Trusted_Computing "wikipedia:es:Trusted Computing").

**Advertencia:** El cifrado de discos tampoco lo protegerá contra alguien que simplemente [borre el disco](/index.php/Securely_wipe_disk "Securely wipe disk"). [Copias de respaldo regulares](/index.php/Backup_programs "Backup programs") son recomendadas para mantener sus datos protegidos.

## Cifrar datos *versus* cifrar sistema

	Cifrar los datos

	Se define como el cifrado de los datos del propio usuario (a menudo situado en el directorio `/home` o en un medio extraíble como un DVD de datos), el cifrado de datos es el uso más simple y menos intrusivo del cifrado de discos, pero tiene algunos inconvenientes significativos.

	En los sistemas informáticos modernos, hay muchos procesos ejecutados en segundo plano que puede almacenar, por ejemplo en caché, información sobre los datos del usuario o partes de datos en zonas no cifrados del disco duro, como:

*   particiones swap
    *   *(posibles remedios: desactivar swap o realizar el [cifrado del espacio de intercambio swap](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") también)*
*   `/tmp` ( archivos temporales creados por las aplicaciones del usuario)
    *   *(posibles remedios : evitar este tipo de aplicaciones; montar `/tmp` dentro de [ramdisk](/index.php/Ramdisk "Ramdisk"))*
*   `/var` (archivos de registros, bases de datos y similares; por ejemplo, mlocate almacena un índice de todos los nombres de los archivos en `/var/lib/mlocate/mlocate.db`)

	Además, el mero cifrado de datos lo dejará vulnerable a ataques de manipulación del sistema offline (por ejemplo, instalando un programa oculto que [grabe](https://en.wikipedia.org/wiki/Keystroke_logging "wikipedia:Keystroke logging") la frase de acceso utilizada para desbloquear los datos cifrados, o que espera a que lo desbloque el usuario y luego copia/envía algunos de los datos a una ubicación donde el atacante puede recuperarla).

	Cifrar el sistema

	Se define como el cifrado del sistema operativo *y* los datos del usuario. El cifrado del sistema ayuda a hacer frente a algunas de las insuficiencias antes mencionadas del cifrado de datos.

	Ventajas:

*   impide el acceso físico no autorizado a (y la manipulación con) de los archivos del sistema operativo *(pero con las advertencias anteriores)*;
*   impide el acceso físico no autorizado a los datos privados que puede dejar en caché el sistema.

	Desventajas:

*   desbloquear las partes cifradas del disco ya no puede realizarse durante o después del inicio de sesión del usuario; ahora debe realizarse en el momento del arranque.

En la práctica, no siempre hay una línea clara entre el cifrado de datos y el cifrado del sistema, y es posible combinar diferentes y personalizadas configuraciones.

En cualquier caso, el cifrado de disco solo debe ser visto como un complemento a los mecanismos de seguridad existentes en el sistema operativo —se enfoca a asegurar el acceso físico fuera de línea—, al tiempo que se delega en *otras* partes del sistema que proporcinan elementos confiables como la seguridad de la red y la seguridad del usuario basada en el control de acceso.

Véase también [Wikipedia:Disk encryption](https://en.wikipedia.org/wiki/Disk_encryption "wikipedia:Disk encryption").

## Métodos disponibles

Todos los métodos de cifrado de discos operan de tal manera que a pesar de que el disco en realidad posee los datos cifrados, el sistema operativo y las aplicaciones los «ven» como sus correspondientes datos legibles normales, siempre y cuando el contenedor cifrado (es decir, la parte lógica del disco que contiene los datos cifrados) haya sido «desbloqueado» y montado.

Para que esto suceda, cierta «información secreta» (por lo general en forma de un archivo de claves y/o frase de acceso) debe ser suministrada por el usuario, de la cual, se deriva la clave de cifrado real (y se almacena en el llavero del kernel mientras dure la sesión).

Si no se está completamente familiarizado con este tipo de operaciones, lea también la sección siguiente [#Cómo funciona el cifrado](#C.C3.B3mo_funciona_el_cifrado).

Los métodos de cifrado del disco disponibles se pueden separar en dos tipos por su capa de operación:

### Cifrar sistemas de archivos apilados

Las soluciones del cifrado del sistema de archivos apilados se implementan como una capa que se superpone en la parte superior de un sistema de archivos existente, haciendo que todos los archivos escritos a una carpeta habilitada para cifrarlos se cifren sobre la marcha antes de que el sistema de archivos subyacente los grabe en el disco, y se descifran cuando el sistema de archivos los lee desde el disco. De esta manera, los archivos se almacenan en el sistema de archivos anfitrión en forma cifrada (lo que significa que sus contenidos y, por lo general, también sus nombres de archivo/carpeta, se sustituyen por datos aleatorios de más o menos la misma longitud), pero, aparte, siguen existiendo en ese sistema de archivos como lo harían sin cifrar, a modo de archivos normales / enlaces simbólicos / enlaces duros / etc.

La forma en que se implementa consiste en que para desbloquear la carpeta donde se almacenan los archivos cifrados en bruto en el sistema de archivos anfitrión («directorio inferior»), ésta debe montarse ( utilizando un pseudo sistema de archivos apilados especial) sobre sí misma u, opcionalmente, en una ubicación diferente («directorio superior» ), donde los mismos archivos aparecen entonces en forma legible —hasta que se desmonta de nuevo o se apaga el sistema—.

Las soluciones disponibles en esta categoría son [eCryptfs](/index.php/ECryptfs "ECryptfs") y [EncFS](/index.php/EncFS "EncFS").

### Cifrar dispositivos de bloques

Los métodos de cifrado de dispositivo de bloque, por el contrario, operan como una capa *debajo* del sistema de archivos y se aseguran que todo lo escrito en un determinado dispositivo de bloques (es decir, un disco completo o una partición o un archivo que actúa como un dispositivo loop-back virtual) quede cifrado. Esto significa que mientras el dispositivo de bloque no está en línea, todo su contenido se parece a una amalgama de datos aleatorios, y no hay forma de determinar qué tipo de sistema de archivos y qué datos contiene. El acceso a los datos ocurre, de nuevo, mediante el montaje del contenedor protegido (en este caso el dispositivo de bloque) a una ubicación arbitraria con un método especial.

Las siguientes soluciones de «cifrado de dispositivos de bloques» están disponibles en Arch Linux:

	loop-AES

	loop-AES es un descendiente de cryptoloop y es una solución segura y rápida para el cifrado del sistema. Sin embargo, loop-AES se considera menos fácil de usar que otras opciones, ya que requiere soporte del kernel no estándar.

	dm-crypt

	[dm-crypt](/index.php/Dm-crypt "Dm-crypt") es la funcionalidad de cifrado para el mapeado de dispositivos estándar proporcionada por el kernel de Linux. Puede ser utilizado directamente por aquellos que les gusta tener un control total sobre todos los aspectos de la partición y la gestión de claves. La gestión de dm -crypt se hace con la utilidad [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) en el espacio de usuario. Se puede utilizar para los siguientes tipos de cifrado de dispositivos de bloques: *LUKS* (por defecto), *plain*, y con carácterística limitadas por dispositivos *loopAES* y *Truecrypt*.

*   LUKS, utilizado por defecto, es una capa adicional eficaz que almacena toda la información necesaria de configuración para dm-crypt, la partición abstacta y la gestión de las claves, en el propio disco en un intento de mejorar la facilidad de uso y la seguridad criptográfica.
*   la modalidad plain dm-crypt, aun siendo la funcionalidad original del kernel, no tiene la misma capa de eficacia. Es más difícil de obtener la misma fuerza criptográfica con ella. Para lograrlo, las claves deben ser más largas (frases de acceso, archivos de claves) para conseguir dicho resultado. Sin embargo, tiene otras ventajas, que se describen más adelante.

	TrueCrypt

	Véase [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"):Tenga en cuenta que los desarrolladores de [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") no prestan soporte desde mayo de 2014.

Para conocer las implicaciones prácticas de la capa de operación elegida, consulte la siguiente [tabla comparativa](#implicaciones_pr.C3.A1cticas), así como el escrito general para [eCryptfs](http://ksouedu.com/doc/ecryptfs-utils/ecryptfs-faq.html#compare). Vea [Category:Encryption](/index.php/Category:Encryption "Category:Encryption") para el contenido disponible de los métodos comparados más abajo, así como otras herramientas no incluidas en la tabla.

### Cuadro comparativo

La columna «dm-crypt +/- LUKS» denota características de dm-crypt tanto para la modalidad de cifrado LUKS («+») como plain («-»). Si una característica específica requiere el uso de LUKS, esto se indica con «(con LUKS). De la misma manera «(sin LUKS)» indica que el uso de LUKS es contraproducente para lograr la función y el modo plain es el aconsejado.

| 

##### *sinopsis*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

tipo

 | cifrado de dispositivos de bloques | cifrado de sistemas de archivos apilados |

pricipales puntos fuertes

 | el más longevo; posiblemente el más rápido; funciona en sistemas antiguos | estándar de hecho para el cifrado de dispositivos de bloques en Linux; muy flexible | solución muy portable, bien pulida y controlada | ligeramente más rápido respecto a EncFS; cifra archivos singulares portables a otros sistemas | fácil de usar; permite la adminitración por usuario normal |

disponibilidad en Arch Linux

 | necesita compilar manualmente un kernel personalizado | *módulos del kernel:* ya cargados por el kernel por defecto; *herramientas:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) [core] | [truecrypt 7.1a-2](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/truecrypt&id=efe03070990f9e3554508bd982b1bd5a654aa095) [extra] (función de solo lectura en versiones posteriores) | *módulos del kernel:* ya cargados por el kernel por defecto; *herramientas:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) [community] | [encfs](https://www.archlinux.org/packages/?name=encfs) [community] |

licencia

 | GPL | GPL | custom | GPL | GPL |
| 

##### *características básicas*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

para cifrar...

 | todos los dispositivos de bloques | archivos |

el contenedor para los datos cifrados puede ser...

 | 

*   un disco o una partición del disco
*   un archivo que se comporta como una partición virtual

 | 

*   un directorio en un sistema de archivos existente

 |

relación con el sistema de archivos...

 | opera por debajo de la capa del sistema de archivos - no importa si el contenido del dispositivo de bloque es un sistema de archivos, una tabla de particiones, una configuración LVM, o cualquier otra cosa | añade una capa adicional a un sistema de archivos existente, para cifrar/descifrar automáticamente los archivos cuando se escriben/leen |

cifrado implementado en...

 | en el espacio del kernel | en el espacio del usuario
*(utilizando FUSE)* |

metadatos criptográficos almacedados en...

 |  ? | con LUKS: en la cabecera de LUKS | al principio/final del dispositivo (descifrado)([format](http://www.truecrypt.org/docs/volume-format-specification)) | en la cabecera de cada archivo cifrado | en el archivo de control al principio de cada contenedor EncFs |

clave de cifrado almacenada en...

 |  ? | con LUKS: en la cabecera de LUKS | el archivo de claves se puede almacenar en cualquier lugar | en el archivo de control al principio de cada contenedor EncFs |
| 

##### *implicaciones prácticas*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

los metadatos de los archivos (número de archivos, estructura de directorios, tamaños de archivos, permisos, mtimes, etc.) están cifrados

 | ✔ | ✖
*(sin embargo, se pueden cifrar nombres de archivos y de directorios)* |

puede ser utilizado para cifrar discos duros enteros (incluyendo las tablas de particiones)

 | ✔ | ✖ |

puede ser utilizado para cifrar el espacio de intercambio (swap)

 | ✔ | ✖ |

puede ser utilizado sin preasignar una cantidad fija de espacio para el contenedor de datos cifrados

 | ✖ | ✔ |

puede ser utilizado para proteger los sistemas de archivos existentes sin acceso al dispositivo de bloque, por ejemplo, recursos compartidos NFS o Samba, almacenamiento en la nube, etc.

 |     ✖ | ✔ |

permite copias de seguridad basadas en archivos offline de los archivos cifrados

 | ✖ | ✔ |
| 

##### *características de usabilidad*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

soporte para montaje automático al iniciar sesión

 |  ? | ✔ |  ? | ✔ | ✔ |

soporte para desmontaje automático en caso de inactividad

 |  ? |  ? |  ? |  ? | ✔ |

los usuarios normales pueden crear/eliminar los contenedores para datos cifrados

 | ✖ | ✖ | ✖ | limitada | ✔ |

proporciona una GUI

 | ✖ | ✖ | ✔ | ✖ | ✔ |
| 

##### *características de seguridad*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

algoritmos de cifrado soportados

 | AES | AES, Anubis, CAST5/6, Twofish, Serpent, Camellia, Blowfish, … (cada algoritmo de cifrado es ofrecido por el Crypto API del kernel) | AES, Twofish, Serpent | AES, Blowfish, Twofish... | AES, Blowfish |

soporte para salting

 |  ? | ✔
(con LUKS) | ✔ | ✔ |  ? |

soporte para múltiples sistemas de cifrado en cascada

 |  ? | No en un solo dispositivo, pero permite conectarse a dispositivos de bloques en cascada | ✔ |  ? | ✖ |

soporte para la difusión del key-slot

 |  ? | ✔
(con LUKS) |  ? |  ? |  ? |

protección contra el forzado de clave

 | ✔ | ✔
(sin LUKS) |  ? |  ? |  ? |

soporte para múltiples claves (revocables independientemente) para los mismos datos cifrados

 |  ? | ✔
(con LUKS) |  ? |  ? | ✖ |
| 

##### *características de rendimiento*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

soporte [multithreading](https://en.wikipedia.org/wiki/es:Multihilo "wikipedia:es:Multihilo")

 |  ? | ✔ | ✔ |  ? |  ? |

soporte para cifrado de hardware acelerado

 | ✔ | ✔ | ✔ | ✔ |
| 

##### *específico del cifrado de dispositivos de bloques*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt |

soporte para redimensionar (manualmente) el dispositivo de bloque cifrado

 |  ? | ✔ | ✖ |
| 

##### *específico del cifrado de sistemas de archivos apilados*

 | eCryptfs | EncFs |

sistemas de archivos soportados

 | ext3, ext4, xfs (con salvedades), jfs, nfs... |  ? |

capacidad para cifrar los nombres de los archivos

 | ✔ | ✔ |

capacidad para *no* cifrar los nombres de los archivos

 | ✔ | ✔ |

optimizado para el manejo de archivos dispersos

 | ✖ | ✔ |
| 

##### *compatibilidad y prevalencia*

 | Loop-AES | dm-crypt +/- LUKS | Truecrypt | eCryptfs | EncFs |

versiones del kernel de Linux que lo soportan

 | 2.0 o posterior | modalidad CBC a partir de 2.6.4, ESSIV 2.6.10, LRW 2.6.20, XTS 2.6.24 |  ? |  ? | 2.4 o posterior |
 los datos cifrados también pueden ser leídos desde... | Windows | ✔ (con ) | ✔ (con ) | ✔ |  ? |     ? |
 Mac OS X |  ? |  ? | ✔ |  ? |     ✔ |
 FreeBSD |  ? |  ? | ✖ |  ? |     ✔ |

utilizado por...

 |  ? | 

*   Instalador de Debian/Ubuntu (cifrado del sistema)
*   Instalador de Fedora

 |  ? | 

*   Instalador de Ubuntu (cifrado del directorio home)
*   Chromium OS (cifrado de los datos del usuario en caché)

 |  ? |

## Preparación

### Elegir una configuración

Qué configuración de cifrado de disco es apropiada para cada usuario dependerá de los propósitos del usuario (léase [#¿Por qué utilizar la criptografía?](#.C2.BFPor_qu.C3.A9_utilizar_la_criptograf.C3.ADa.3F) más arriba) y de los parámetros del sistema.
Entre otras, tendrá que responder a las siguientes preguntas:

*   ¿Contra qué tipo de *ataques* quiere proteger su sistema?
    *   Usuario ocasional de ordenador husmeando el disco cuando el sistema está apagado / robado / etc.
    *   Criptoanalista profesional que puede conseguir acceso de lectura/escritura repetidamente al sistema antes y después de usarse
    *   Ninguno de los anteriores

*   ¿Qué estrategia de cifrado desea emplear?
    *   Cifrado de datos
    *   Cifrado del sistema
    *   Cualquiera de los anteriores

*   ¿Cómo deben tratarse swap, `/tmp`, etc.?
    *   Ignorar, y con la esperanza de que no se hayan filtrado datos
    *   Desactivar o montar como disco de memoria
    *   Cifrar *(como parte del cifrado del disco completo o por separado)*

*   ¿Cómo deben desbloquearse las partes del disco cifradas?
    *   Con contraseña/frase de acceso *(igual que la contraseña de inicio de sesión, o por separado)*
    *   Con archivo de claves *(por ejemplo, en una memoria USB, que se mantenga en un lugar seguro o portarlo uno mismo)*
    *   Con ambas

*   ¿*Cuándo* deben desbloquearse las partes del disco cifradas?
    *   Antes del arranque
    *   Durante del arranque
    *   Al iniciar sesión
    *   Manualmente bajo demanda *(después de iniciar sesión)*

*   ¿Cómo deben ser acomodados varios usuarios?
    *   No hacer nada
    *   Usar una clave/frase de acceso compartida
    *   Usar claves/frases de acceso emitidas de forma independiente y revocables para la misma parte del disco cifrado
    *   Crear partes cifradas separadas del disco para los diferentes usuarios

A continuación, se puede pasar a tomar las decisiones técnicas necesarias (vea [#Métodos disponibles](#M.C3.A9todos_disponibles) más arriba, y [#Cómo funciona el cifrado](#C.C3.B3mo_funciona_el_cifrado) más adelante), en relación con:

*   elegir entre cifrar sistemas de archivos apilados *versus* cifrar dispositivos de bloques
*   la gestión de las claves
*   el algoritmo de cifrado y la modalidad de la operación
*   el almacenamiento de los metadatos
*   la ubicación del «directorio inferior» (en caso de cifrado de sistemas de archivos apilados)

### Ejemplos

En la práctica, podría resultar algo así:

	Ejemplo 1

	cifrado sencillo de datos (en disco duro interno), utilizando una carpeta virtual denominada «~/Private» en el directorio home del usuario, cifrado con [EncFS](/index.php/EncFS "EncFS")
└──> las versiones cifradas de los archivos serán almacenadas en la carpeta ~/.Private del disco
└──> desbloqueada bajo demanda con una frase de acceso dedicada

	Ejemplo 2

	cifrado sencillo de datos (en medio extraible), utilizando una unidad USB cifrada con [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
└──> desbloqueado cuando está conectado al ordenador (usando la frase de acceso dedicada + usando ~/photos/2006-09-04a.jpg como keyfile encubierto)

	Ejemplo 3

	cifrado parcial del sistema con el **directorio home** de cada usuario cifrado con [ECryptfs](/index.php/ECryptfs "ECryptfs")
└──> desbloqueado por el respectivo usuario al iniciar sesión, utilizando la frase de acceso
└──> las particiones **swap** y **/tmp** serán cifradas con [Dm-crypt con LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)"), utilizando una clave de un solo uso generada automáticamente para casa sesión
└──> indexación/caché de contenidos de /home por slocate (y aplicaciones similares) desactivada.

	Ejemplo 4

	cifrado completo del sistema —disco duro entero— (excepto la partición /boot), cifrado con [dm-crypt con LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")
└──> desbloqueado durante el arranque, mediante frases de contraseña o desde una memoria USB con un archivo de claves
└──> se pueden tener diferentes frases/claves por usuario, independientes y revocables
└──> el cifrado puede abarcar múltiples unidades o permitir flexibilidad en el esquema de particionado con [LUKS sobre LVM](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LUKS_sobre_LVM "Dm-crypt/Encrypting an entire system (Español)")

	Ejemplo 5

	cifrado completo del sistema oculto/con plain —disco duro entero—, cifrado con [plain dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")
└──> arranque desde USB, usando frase de acceso dedicada + lápiz USB que almacena un archivo de claves
└──> datos revisados ​​antes de montar la partición
└──> /boot se encuentra en la mencionada memoria USB

Otras muchas combinaciones son posibles, por supuesto. Se debe planificar cuidadosamente qué tipo de configuración será la apropiada para su sistema.

### Elegir una frase de acceso sólida

Véase [Security#Passwords](/index.php/Security#Passwords "Security").

### Preparar el disco

Antes de configurar el cifrado de un disco (o parte de él), considere realizar previamente un borrado seguro. Esto consiste en sobrescribir todo el disco o la partición con un flujo de bytes cero o bytes aleatorios, y se hace por una o ambas de las siguientes razones:

*   **Impedir la recuperación de los datos almacenados previamente**

    El cifrado del disco no cambia el hecho de que los distintos sectores del mismo solo se sobrescriben bajo demanda, esto es, cuando el sistema de archivos crea o modifica los datos contenidos en esos sectores (véase [#Cómo funciona el cifrado](#C.C3.B3mo_funciona_el_cifrado) a continuación). Los sectores que el sistema de archivos considera que «no se están utilizando actualmente» no los toca, y todavía pueden contener restos de datos del sistemas de archivos anterior. La única manera de asegurarse de que todos los datos guardados previamente en la unidad no pueden ser [recuperados](https://en.wikipedia.org/wiki/es:Recuperaci%C3%B3n_de_datos "wikipedia:es:Recuperación de datos"), es borrarlos manualmente.
    Para este propósito, no importa si se utilizan bytes cero o bytes aleatorios (aunque limpiando con bytes cero será mucho más rápido).

*   **Impedir la divulgación de los patrones de uso de la unidad cifrada**

    Lo ideal sería que toda la parte cifrada del disco fuera indistinguible desde la uniformidad de datos aleatorios. De esta manera, ninguna persona no autorizada podría saber cuáles y cuántos sectores contienen realmente datos cifrados —que puede ser un objetivo deseable en sí mismo (como parte de la verdadera confidencialidad)—, y que también sirve como una barrera adicional contra los atacantes que traten de romper el cifrado.
    Para satisfacer este objetivo, limpiar el disco utilizando bytes aleatorios de alta calidad es crucial.

El segundo objetivo solo tiene sentido en combinación con el cifrado de dispositivos de bloques, ya que en el caso del cifrado de sistemas de archivos apilados, los datos cifrados se pueden localizar fácilmente de todos modos (en forma de archivos cifrados distintos en el sistema de archivos anfitrión). También tenga en cuenta que, incluso si solo se va a cifrar una carpeta en particular, tendrá que borrar la partición entera si quiere deshacerse de los archivos que estaban almacenados previamente en esa carpeta sin cifrar (debido a la [fragmentación del disco](https://en.wikipedia.org/wiki/es:Fragmentaci%C3%B3n_de_un_sistema_de_ficheros "wikipedia:es:Fragmentación de un sistema de ficheros")). Si hay otras carpetas en la misma partición, habrá que hacerles una copia de respaldo y restablecerlas de nuevo más tarde.

Una vez que haya decidido qué tipo de borrado de disco desea realizar, remítase al artículo [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") para conocer instrucciones más técnicas.

**Sugerencia:** Al decidir qué método utilizar para el borrado seguro de una unidad de disco duro, recuerde que esto no será necesario realizarlo más que una vez durante el tiempo que la unidad se utiliza como una unidad cifrada.

## Cómo funciona el cifrado

Esta sección pretende ser una introducción general a los conceptos y procesos que se encuentran en el corazón de las configuraciones habituales del cifrado de discos.

No se entra en detalles técnicos o matemáticos (consulte la literatura apropiada para ello), sino que desea proporcionar a un administrador del sistema una comprensión general sobre cómo las diferentes opciones de configuración (en especial en relación con la gestión de claves) pueden afectar a su usabilidad y seguridad.

### Principio básico

A los efectos del cifrado de discos, cada dispositivo de bloque (o archivo individual en el caso del cifrado de sistemas de archivos apilados) se divide en **sectores** de igual longitud, por ejemplo, 512 bytes (4096 bits). El cifrado/descifrado se realiza después en función de cada sector, por lo que el sector n del archivo/dispositivo de bloque en el disco almacenará la versión cifrada del sector n de los datos originales.

Cada vez que el sistema operativo o una aplicación solicita un determinado fragmento de datos del archivo/dispositivo de bloque, todo el sector (o sectores) que contienen los datos serán leídos desde el disco, descifrados sobre la marcha y almacenados temporalmente en la memoria:

```
            ╔═══════╗
   sector 1 ║"???.."║
            ╠═══════╣        ╭┈┈┈┈┈┈┈╮
   sector 2 ║"???.."║        ┊ clave ┊
            ╠═══════╣        ╰┈┈┈┬┈┈┈╯
            :       :            │
            ╠═══════╣            ▼             ┣┉┉┉┉┉┉┉┫
   sector n ║"???.."║━━━━━━━(descifrado)━━━━━━▶┋"abc.."┋ sector n
            ╠═══════╣                          ┣┉┉┉┉┉┉┉┫
            :       :
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

*   ***Almacenada en un archivo de claves de texto plano***

    Almacenar simplemente la llave maestra en un archivo (en formato legible) es la opción más sencilla . El archivo —llamado un «keyfile» o «archivo de claves»— se puede colocar en una memoria USB mantenida en un lugar seguro y que se conecte al ordenador cuando se quieran montar las partes cifradas del disco (por ejemplo, durante el arranque o el inicio de sesión).

*   ***Almacenada en forma de frase de acceso protegida en un archivo de claves o en el propio disco***

    La llave maestra (y, por lo tanto, los datos cifrados con ella) se puede proteger con una contraseña secreta, que tendrá que recordar e introducir cada vez que desea montar el dispositivo de bloque o carpeta. Véase [#Cryptographic metadata](#Cryptographic_metadata) a continuación para obtener más detalles.

*   ***Generada de forma aleatoria sobre la marcha para cada sesión***

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

La **función derivadora de claves** (por ejemplo PBKDF2 o scrypt) es deliberadamente lenta (se aplican muchas [iteraciones](https://en.wikipedia.org/wiki/es:Iteraci%C3%B3n "wikipedia:es:Iteración") de una [función hash](https://en.wikipedia.org/wiki/es:Funci%C3%B3n_hash "wikipedia:es:Función hash"), por ejemplo, 1.000 iteraciones de HMAC-SHA-512), de modo que los posibles ataques de fuerza bruta destinados a encontrar la frase de acceso se presentan inviables. Para el caso de su utilización normal por un usuario autorizado, solo será necesario realizar el cálculo una vez por sesión, por lo que la pequeña desaceleración no es un problema.

También toma un [blob](https://en.wikipedia.org/wiki/es:Binary_large_object "wikipedia:es:Binary large object") adicional de datos, que se denomina [«**sal**»](https://en.wikipedia.org/wiki/es:Sal_(criptografia) "wikipedia:es:Sal (criptografia)"), como un argumento —este se genera aleatoriamente una vez durante la puesta en marcha del cifrado del disco y se almacena sin protección como parte de los metadatos criptográficos—. Debido a que será un valor diferente para cada configuración, esto hace que sea imposible para los atacantes acelerar los ataques de fuerza bruta usando tablas precalculadas para acceder a la función derivadora de claves.

La **llave maestra cifrada** se puede almacenar en el disco junto con los datos cifrados. De esta manera, la confidencialidad de los datos cifrados depende completamente de la frase secreta.

Para aumentar la seguridad se puede almacenar la llave maestra cifrada en un archivo de claves, por ejemplo, en una memoria USB. Esto proporciona **dos factores de autenticación**, a saber: el acceso a los datos cifrados ahora requiere algo que solo usted *sabe* (la frase de acceso), y, además, algo que solo usted *tiene* (el archivo de claves).

Otra forma de lograr un doble factor de autenticación es aumentar el esquema de obtención de claves, previo a su matematización, «combinando» la frase de acceso con la lectura de datos de byte en uno o más archivos externos (situados en una memoria USB o similar), antes de pasarla por la función derivadora de claves.
Los archivos en cuestión pueden ser cualquier cosa, por ejemplo, imágenes JPEG normales, lo que puede ser beneficioso para la [#Negabilidad plausible](#Negabilidad_plausible). Estos, sin embargo, todavía se llaman «keyfiles» en el presente contexto.

Después de que la llave maestra se haya derivado con éxito, esta se almacena de forma segura en la memoria (por ejemplo, en un anillo de claves del kernel), durante el tiempo que esté montado el dispositivo de bloque o carpeta.

Por lo general, sin embargo, no se utiliza para cifrar/descifrar los datos del disco directamente. Por ejemplo, en el caso de cifrado del sistema de archivos apilados, cada archivo puede asignarse automáticamente su propia clave de cifrado. Cada vez que el archivo ha de ser leído/modificado, esta clave del archivo debe primero ser descifrada usando la llave maestra, antes de que pueda ser utilizada por sí para cifrar/descifrar el contenido del archivo:

```
                               ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
                               ┊ llave maestra ┊
  *archivo en disco:*            ╰┈┈┈┈┈┈┈┬┈┈┈┈┈┈┈╯
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

*   [Wikipedia:Passphrase](https://en.wikipedia.org/wiki/Passphrase "wikipedia:Passphrase")
*   [Wikipedia:Key (cryptography)](https://en.wikipedia.org/wiki/Key_(cryptography) "wikipedia:Key (cryptography)")
*   [Wikipedia:Key management](https://en.wikipedia.org/wiki/Key_management "wikipedia:Key management")
*   [Wikipedia:Key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function "wikipedia:Key derivation function")

### Algoritmos de cifrado y modalidades de operación

El algoritmo real utilizado para servir de traductor entre las piezas de datos no cifradas y las cifradas (llamado «texto plano» y «texto cifrado», respectivamente), que se interrelacionan entre sí a través de una clave de cifrado dada, se llama un «**algoritmo de cifrado**».

El cifrado de discos emplea «algoritmos de cifrado de bloques», que operan sobre bloques de datos de una longitud fija, por ejemplo 16 bytes (128 bits). En el momento de escribir estas líneas, los más usados son:

 tamaño del bloque | tamaño de la clave | comentario |
| [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") | 128 bits | 128, 192 o 256 bits | *aprobado por la NSA para la protección de información clasificada «SECRET» y «TOP SECRET» por el gobierno de EE.UU. (cuando se utiliza con un tamaño de clave de 192 o 256 bits)* |
| [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher) | 64 bits | 32–448 bits | *uno de los primeros sistemas de cifrado seguro con licencia libre que se puso a disposición del público, por lo tanto, muy bien consolidado en Linux* |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bits | 128, 192 o 256 bits | *desarrollado como sucesor de Blowfish, pero sin haber alcanzado un uso tan amplio* |
| [Serpent](https://en.wikipedia.org/wiki/Serpent_(cipher) | 128 bits | 128, 192 o 256 bits | Considerado el más seguro de los cinco finalistas de la competición AES. |

Cifrar/descifrar un sector ([véase más arriba](#Principio_b.C3.A1sico)) se consigue mediante su división en pequeños bloques, haciéndolos coincidir con el tamaño del bloque cifrado, y siguiendo, después, cierto conjunto de reglas (que antes hemos llamado «**modalidad de operación**») que informan sobre cómo aplicar el algoritmo de cifrado a los bloques individuales.

Aplicar el algoritmo de cifrado sin más a cada bloque por separado sin modificaciones (denominada modalidad «*electronic codebook (ECB)*») no sería seguro, ya que si los mismos 16 bytes de texto plano siempre producen los mismos 16 bytes de texto cifrado, un atacante podría reconocer fácilmente los patrones en el texto cifrado que se almacenan en el disco.

La modalidad más básica (y común) de operar utilizada en la práctica es la denominada «*cipher-block chaining (CBC)*». Al cifrar un bloque de un sector con esta modalidad, cada bloque de datos de texto plano se combina de forma matemática con el texto cifrado del bloque anterior antes de cifrarlo, utilizando el algoritmo de cifrado. Para el primer bloque, ya que no tiene texto cifrado anterior que usar, se utiliza un bloque de datos pregenerado especial almacenado con los metadatos criptográficos del sector y llamado «**vector de inicialización**»:

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
    de bloque   ║"????????"║◀━━(algoritmo de cifrado)━━━(+)━━━━━━━━━━┋"orld !!!"┋ bloque
          ┬     ║          ║                                         ┋          ┋ 2
          │     ║          ║──────────────────╮                      ┋          ┋
          │     ╟──────────╢                  │                      ┠┈┈┈┈┈┈┈┈┈┈┨
          │     ║          ║                  ▼                      ┋          ┋
          :     :   ...    :        ...      ...      ...    ...     :   ...    : ...

               texto cifrado                                         texto plano
                    en disco                                         en RAM

```

Al descifrar, el procedimiento se invierte de forma análoga.

Una cosa a destacar es la generación del vector de inicialización único para cada sector. La opción más sencilla consiste en calcularlo de una manera predecible a partir de un valor fácilmente disponible, como puede ser el número del sector. Sin embargo, esto podría permitir que un atacante con acceso reiterado al sistema pudiera realizar el llamado [watermarking attack](https://en.wikipedia.org/wiki/Watermarking_attack "wikipedia:Watermarking attack"). Para evitar esto, un método llamado «Encrypted salt-sector initialization vector (**ESSIV**)» se puede utilizar para generar vectores de inicialización de una manera que hace que se vean completamente aleatorios por un atacante potencial.

También hay otras opciones disponibles, modalidades de operación más complicadas para cifrar el disco, que ya ofrecen seguridad integrada contra este tipo de ataques (y, por lo tanto, no requieren ESSIV). Otras opciones también pueden garantizar, además, la autenticidad de los datos cifrados (es decir, confirmar que no se han modificado/corrompido por alguien que no tiene acceso a la clave).

Véase también:

*   [Wikipedia:Disk_encryption_theory](https://en.wikipedia.org/wiki/Disk_encryption_theory "wikipedia:Disk encryption theory")
*   [Wikipedia:Block_cipher](https://en.wikipedia.org/wiki/Block_cipher "wikipedia:Block cipher")
*   [Wikipedia:Block_cipher_modes_of_operation](https://en.wikipedia.org/wiki/Block_cipher_modes_of_operation "wikipedia:Block cipher modes of operation")

### Negabilidad plausible

Véase [Wikipedia:Plausible deniability](https://en.wikipedia.org/wiki/Plausible_deniability "wikipedia:Plausible deniability")

## Véase también

<small></small>

<small>

1.  [^](#sinopsis) véase [http://www.truecrypt.org/legal/license](http://www.truecrypt.org/legal/license)
2.  [^](#implicaciones_pr.C3.A1cticas) well, a single file in those filesystems could be used as a container (virtual loop-back device!) but then one wouldn't actually be using the filesystem (and the features it provides) anymore
3.  [^](#compatibilidad_y_prevalencia) [CrossCrypt](http://www.scherrer.cc/crypt) - Open Source AES and TwoFish Linux compatible on the fly encryption for Windows XP and Windows 2000
4.  [^](#compatibilidad_y_prevalencia) (1) [FreeOTFE (on sf.net)](http://sourceforge.net/projects/freeotfe.mirror/) (2) [FreeOTFE (archived)](http://web.archive.org/web/20130531062457/http://freeotfe.org/) - supports Windows 2000 and later (for PC), and Windows Mobile 2003 and later (for PDA)
5.  [^](#compatibilidad_y_prevalencia) véase [EncFs build instructions for Mac](http://www.arg0.net/encfs-mac-build)
6.  [^](#compatibilidad_y_prevalencia) véase [http://www.freshports.org/sysutils/fusefs-encfs/](http://www.freshports.org/sysutils/fusefs-encfs/)
7.  [^](#compatibilidad_y_prevalencia) véase [http://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data](http://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data)
8.  [^](#compatibilidad_y_prevalencia) [http://kernelnewbies.org/Linux_2_6_38#head-49f5f735853f8cc7c4d89e5c266fe07316b49f4c](http://kernelnewbies.org/Linux_2_6_38#head-49f5f735853f8cc7c4d89e5c266fe07316b49f4c)
9.  [^](#compatibilidad_y_prevalencia) [http://members.ferrara.linux.it/freddy77/encfs.html](http://members.ferrara.linux.it/freddy77/encfs.html)
10.  [^](#compatibilidad_y_prevalencia) [http://csrc.nist.gov/archive/aes/round2/r2report.pdf](http://csrc.nist.gov/archive/aes/round2/r2report.pdf)
11.  [^](#compatibilidad_y_prevalencia) [https://www.cl.cam.ac.uk/~rja14/Papers/serpentcase.pdf](https://www.cl.cam.ac.uk/~rja14/Papers/serpentcase.pdf)
12.  [^](#compatibilidad_y_prevalencia) [https://www.cl.cam.ac.uk/~rja14/Papers/serpent.pdf](https://www.cl.cam.ac.uk/~rja14/Papers/serpent.pdf)
13.  [^](#encfs_acceleration) [https://code.google.com/p/encfs/issues/detail?id=131](https://code.google.com/p/encfs/issues/detail?id=131)
14.  [^](#compatibility_.26_prevalence) [DOXBOX](https://github.com/t-d-k/doxbox) - support to open dm-crypt / LUKS in newer Windows releases (includes fork from OTFE)

</small>

<small></small>
Artículos relacionados

*   [GnuPG (Español)](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)")

La herramienta pacman-key se usa tanto para configurar como para administrar las firmas de los paquetes con los que trabaja [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"), el gestor de paquetes de Arch Linux, mediante claves [PGP](https://es.wikipedia.org/wiki/Pretty_Good_Privacy).

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Configuración de pacman](#Configuraci.C3.B3n_de_pacman)
    *   [2.2 Inicializar el archivo de claves o *keyring*](#Inicializar_el_archivo_de_claves_o_keyring)
*   [3 Gestión del archivo de claves](#Gesti.C3.B3n_del_archivo_de_claves)
    *   [3.1 Verificación de las cinco Claves Maestras](#Verificaci.C3.B3n_de_las_cinco_Claves_Maestras)
    *   [3.2 Añadir claves de Desarrolladores](#A.C3.B1adir_claves_de_Desarrolladores)
    *   [3.3 Añadir claves no oficiales](#A.C3.B1adir_claves_no_oficiales)
    *   [3.4 Using gpg](#Using_gpg)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 No puedo importar llaves](#No_puedo_importar_llaves)
    *   [4.2 Desactivar la comprobación de firmas](#Desactivar_la_comprobaci.C3.B3n_de_firmas)
    *   [4.3 Restablecer todas las llaves](#Restablecer_todas_las_llaves)
    *   [4.4 Eliminar paquetes inservibles](#Eliminar_paquetes_inservibles)
*   [5 Bibliografía complementaria](#Bibliograf.C3.ADa_complementaria)

## Introducción

Pacman se sirve de [claves GnuPG](http://www.gnupg.org/) siguiendo el modelo de la [red de confianza](http://www.gnupg.org/gph/en/manual.html#AEN385) para comprobar la autenticidad de los paquetes. Actualmente hay cinco [Claves Maestras de firmado](https://www.archlinux.org/master-keys/). Se usan por lo menos tres de esas Claves Maestras para firmar los paquetes de los desarrolladores oficiales y las subclaves de los usuarios de confianza o TUs —del inglés: *trusted user*— con las que estos firman sus paquetes. El usuario también posee una clave PGP exclusiva que se genera cuando se configura pacman-key. La clave del usuario queda enlazada por tanto a las cinco Claves Maestras.

Ejemplos de redes de confianza:

*   **Paquetes propios**: el usuario elabora el paquete y lo firma con su clave personal.
*   **Paquetes no oficiales**: paquetes creados y firmados por desarrolladores. El usuario usa su clave personal para firmar las de cada uno de esos desarrolladores.
*   **Paquetes oficiales**: paquetes creados y firmados por desarrolladores. Las claves de esos desarrolladores se firmaron previamente usando las claves maestras de Arch Linux. El usuario usa su clave para firmar las claves maestras y, por tanto, tiene plena confianza en los desarrolladores.

**Nota:** el protocolo HKP usa el puerto 11371 para establecer la conexión. Este puerto es necesario para obtener las claves firmadas de los servidores mediante pacman-key.

## Instalación

### Configuración de pacman

La opción `SigLevel` en `/etc/pacman.conf` será la que determine el nivel de confianza a la hora de instalar un paquete. Para una explicación más detallada de SigLevel, consultar la [página man de pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) y los comentarios en la misma. La comprobación del firmado de claves se puede establecer de forma global o por repositorio. En caso de configurar SigLevel globalmente en la sección [options] para exigir que todos los paquetes estén firmados, los paquetes que el usuario compile también tendrán que estar firmados usando `makepkg`.

**Nota:** aunque todos los paquetes oficiales están firmados; a fecha de junio de 2012, la firma de la bases de datos de paquetes está todavía en proceso. Si se especifica `Required` entonces también hay que poner `DatabaseOptional`. Por ejemplo: `SigLevel = Required DatabaseOptional TrustedOnly` Pacman instalará así tan sólo aquellos paquetes que estén firmados con claves que sean de confianza.

**Nota:** parece ser que `SigLevel = PackageRequired` va a ser el estándar para verificar paquetes oficiales::
```
[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

**Advertencia:** la opción `TrustAll` solamente existe para fines de depuración de código y hace que sea muy fácil confiar en claves que no se han verificado. Hay que usar `TrustedOnly` sólo para los repositorios oficiales.

### Inicializar el archivo de claves o *keyring*

Para configurar el archivo de claves de pacman hay que ejecutar:

```
# pacman-key --init

```

Arch Linux necesita [entropía](https://es.wikipedia.org/wiki/Entrop%C3%ADa_%28computaci%C3%B3n%29) para arrancar el archivo de claves de pacman. Mover el ratón, presionar teclas aleatoriamente o ejecutar algún tipo de tarea que haga funcionar a una unidad. He aquí algunos ejemplos de esto último: `ls -R /`, `find / -name foo` o `dd if=/dev/sda8 of=/dev/tty7`. Si el sistema no tiene suficiente entropía, este paso puede durar horas. Generando entropía de forma activa se puede completar este proceso mucho más rápidamente.

La aleatoriedad que se crea se usa para configurar un archivo de claves (`/etc/pacman.d/gnupg`) y la firma de la clave GPG del sistema.

**Nota:** si se quiere ejecutar `pacman-key --init` de forma remota a través de SSH, hay que instalar el paquete [haveged](https://www.archlinux.org/packages/?name=haveged) en el equipo en el que se está configurando el archivo de claves. Hay que conectarse usando SSH y ejecutar lo siguiente:
```
# haveged -w 1024
# pacman-key --init

```

Tan sólo hay que detener y eliminar haveged cuando pacman-key esté funcionando.

```
# pkill haveged
# pacman -Rs haveged

```

Usar [haveged](https://www.archlinux.org/packages/?name=haveged) no sirve sólo para cuando se instala a través de SSH; es una buena forma de generar entropía rápidamente. Si el usuario nota que el proceso de `pacman-key --init` tarda demasiado en completarse, es buena idea usarlo.

## Gestión del archivo de claves

### Verificación de las cinco Claves Maestras

Para empezar a configurar las claves hay que ejecutar:

```
# pacman-key --populate archlinux

```

No hay que tener prisa a la hora de verificar las [Claves Maestras](https://www.archlinux.org/master-keys/) cuando el sistema pregunte por ellas puesto que son las que se van a usar para firmar y, por ende, validar las claves de todos los demás paquetes.

Las llaves PGP son demasiado extensas (2048 bits o más) para que las personas trabajen con ellas. Es por esto que normalmente se reducen a un código hash para crear una huella de 40 dígitos hexadecimales que puede usarse para comparar manualmente que dos claves son exactamente iguales. Los últimos 8 dígitos son el 'nombre' la clave y se les conoce como el ID de la clave (key ID).

### Añadir claves de Desarrolladores

Las claves oficiales de los desarrolladores y las de los TUs se firman con las claves maestras por lo que no es necesario que el usuario las firme por si mismo haciendo uso de la herramienta pacman-key. Cuando pacman se encuentra con una clave que no reconoce, pedirá descargarla del `keyserver` establecido en `/etc/pacman.d/gnupg/gpg.conf` (o usando la opción `--keyserver` en la consola). En la Wikipedia se puede encontrar una [lista de servidores de claves](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

Una vez que se ha descargado una clave de un desarrollador no es necesario descargarla de nuevo. Además, se puede usar para verificar otros paquetes que ese desarrollador haya firmado.

**Nota:** el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), que figura entre las dependencias de pacman, contiene las claves actualizadas. En cualquier caso, es posible actualizarlas ejecutando:
```
# pacman-key --refresh-keys

```
Al ejecutar pacman-key con la opción `--refresh-keys`, se buscará la clave local en el servidor de claves remoto y aparecerá un mensaje alertando de que no ha sido posible encontrar dicha clave. Esto es normal y no es algo por lo que haya que preocuparse.

### Añadir claves no oficiales

Lo primero es obtener la ID del dueño de la clave. Ejecutar para ello:

 `# pacman-key -r <keyid>` 

para descargarla de un servidor de claves. Hay que asegurarse de verificar la huella; como si de una clave maestra o cualquier otra clave que se va a firmar se tratase. Una vez verificada la huella hay que firmar esta clave en el sistema:

 `# pacman-key --lsign-key <keyid>` 

Ahora se confía en esta clave para firmar paquetes.

### Using gpg

Si pacman-key no es suficiente, se puede administrar el archivo de claves de pacman con **gpg**:

```
# gpg --homedir /etc/pacman.d/gnupg $OPTIONS

```

o con

```
# env GNUPGHOME=/etc/pacman.d/gnupg gpg $OPTIONS

```

## Solución de problemas

**Advertencia:** pacman-key depende de [system time](/index.php/System_time "System time"). Si la hora del sistema no es la correcta, aparecerá lo siguiente:

	error: PackageName: signature from "User <email@archlinux.org>" is invalid

	error: failed to commit transaction (invalid or corrupted package (PGP signature))

	Errors occured, no packages were upgraded.

### No puedo importar llaves

Algunos proveedores de internet o ISPs —del inglés: *Internet Service Provider*— bloquean el puerto que se usa para importar las claves PGP. Una forma de solventar este problema es usar el servidor de claves MIT, el cual se sirve de un puerto alternativo. Para ello hay que editar el fichero `/etc/pacman.d/gnupg/gpg.conf` y cambiar la línea del servidor de claves por:

 `keyserver hkp://pgp.mit.edu:11371` 

En caso de olvidar ejecutar `pacman-key --populate archlinux`, cabe la posibilidad de encontrarse con algunos errores al importar las claves.

### Desactivar la comprobación de firmas

**Advertencia:** usar con precaución. Desactivar las firmas de los paquetes hará que pacman instale automáticamente paquetes de fuentes no confiables.

Si no se está interesado en el firmado de paquetes, se puede desactivar la comprobación de las claves PGP por completo. Editar el fichero`/etc/pacman.conf` y descomentar la siguiente lína en [options]:

```
SigLevel = Never

```

Hay que descomentar las opciones específicas de SigLevel de cada repositorio también ya que ignoran la configuración global. Esto hará que no haya comprobación alguna de firmas de claves; así es como se procedía habitualmente antes de la llegada de pacman 4\. No es necesario configurar el archivo de claves con pacman-key si se decide optar por esta opción. Esta opción se puede modificar más adelante sin problema alguno si se decide activar la verificación de paquetes.

### Restablecer todas las llaves

Para eliminar o restablecer todas las claves instaladas en el sistema, eliminar el directorio `/etc/pacman.d/gnupg` como root y volver a ejecutar `pacman-key --init` . Una vez hecho esto, se pueden añadir las claves que se consideren necesarias.

### Eliminar paquetes inservibles

Si hay paquetes que siguen dando error y se está seguro de haber configurado correctamente pacman-key, entonces hay que probar a eliminarlos como por ejemplo con `rm /var/cache/pacman/pkg/paqueteconflictivo*` para que se vuelvan a descargar.

Probablemente esta sea la solución al problema del mensaje que aparece al actualizar `error: linux: signature from "Some Person <Some.Person@example.com>" is invalid`; o parecido. Esto no tiene por qué significar que se esté siendo de un ataque; ni mucho menos. Es tan sólo que el fichero descargargado está corrupto.

## Bibliografía complementaria

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman")
*   [El cifrado de paquetes de pacman – 1: Makepkg y Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [El cifrado de paquetes de pacman – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [El cifrado de paquetes de pacman – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [El cifrado de paquetes de pacman – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)
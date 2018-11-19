**Estado de la traducción**
Este artículo es una traducción de [Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing"), revisada por última vez el **2018-11-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman/Package_signing&diff=0&oldid=551079) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [GnuPG (Español)](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)")
*   [DeveloperWiki:Package signing](/index.php/DeveloperWiki:Package_signing "DeveloperWiki:Package signing")

*pacman* se sirve de [claves GnuPG](http://www.gnupg.org/) siguiendo el modelo de la [red de confianza](http://www.gnupg.org/gph/en/manual.html#AEN385) para comprobar la autenticidad de los paquetes. Actualmente hay cinco claves maestras que se encuentran [aquí](https://www.archlinux.org/master-keys/). Se usan por lo menos tres de esas Claves Maestras para firmar los paquetes de los desarrolladores oficiales y las subclaves de los usuarios de confianza o TUs —del inglés: *trusted user*— con las que estos firman sus paquetes. El usuario también posee una clave PGP exclusiva que se genera cuando se configura pacman-key. La clave del usuario queda enlazada por tanto a las cinco Claves Maestras.

Ejemplos de redes de confianza:

*   **paquetes personalizados**: el usuario elabora el paquete y lo firma con su clave personal.
*   **paquetes no oficiales**: paquetes creados y firmados por desarrolladores. El usuario usa su clave personal para firmar las de cada uno de esos desarrolladores.
*   **paquetes oficiales**: paquetes creados y firmados por desarrolladores. Las claves de esos desarrolladores se firmaron previamente usando las claves maestras de Arch Linux. El usuario usa su clave para firmar las claves maestras y, por tanto, tiene plena confianza en los desarrolladores.

**Nota:** el protocolo HKP utiliza el puerto 11371/tcp para establecer la conexión. Este puerto es necesario para obtener las claves firmadas de los servidores mediante pacman-key.

## Contents

*   [1 Configuración](#Configuración)
    *   [1.1 Configurar pacman](#Configurar_pacman)
    *   [1.2 Inicializar el depósito de claves](#Inicializar_el_depósito_de_claves)
*   [2 Gestionar el depósito de claves](#Gestionar_el_depósito_de_claves)
    *   [2.1 Verificar las claves maestras](#Verificar_las_claves_maestras)
    *   [2.2 Añadir las claves de los desarrolladores](#Añadir_las_claves_de_los_desarrolladores)
    *   [2.3 Añadir claves no oficiales](#Añadir_claves_no_oficiales)
    *   [2.4 Depurar errores con gpg](#Depurar_errores_con_gpg)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 No se pueden importar las claves](#No_se_pueden_importar_las_claves)
    *   [3.2 Desactivar la comprobación de las firmas](#Desactivar_la_comprobación_de_las_firmas)
    *   [3.3 Restablecer todas las claves](#Restablecer_todas_las_claves)
    *   [3.4 Eliminar paquetes inservibles](#Eliminar_paquetes_inservibles)
    *   [3.5 La firma es de confianza desconocida](#La_firma_es_de_confianza_desconocida)
    *   [3.6 Actualizar claves a través de proxy](#Actualizar_claves_a_través_de_proxy)
*   [4 Véase también](#Véase_también)

## Configuración

### Configurar pacman

La opción `SigLevel` en `/etc/pacman.conf` será la que determine el nivel de confianza a la hora de instalar un paquete. Para una explicación más detallada de SigLevel, consulte el [manual de pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) y los comentarios del mismo. La comprobación del firmado de claves se puede establecer de forma global o por repositorio. En caso de configurar SigLevel globalmente en la sección [options] para exigir que todos los paquetes estén firmados, los paquetes que el usuario compile también tendrán que estar firmados usando `makepkg`.

{{Nota|aunque todos los paquetes oficiales están firmados; a fecha de junio de 2012, la firma de la bases de datos de paquetes está todavía en proceso. Si se especifica `Required` entonces también hay que poner `DatabaseOptional`.

Se puede usar una configuración predeterminada para instalar únicamente paquetes firmados por claves de confianza:

 `/etc/pacman.conf`  `SigLevel = Required DatabaseOptional` 

Esto se debe a que `TrustedOnly` es un parámetro *pacman* predeterminado en su compilación. Así que lo anterior conduce al mismo resultado que el ajuste global de:

```
SigLevel = Required DatabaseOptional TrustedOnly

```

Lo anterior también se puede lograr en un nivel más abajo del repositorio en la configuración del archivo, por ejemplo:

```
[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

agrega explícitamente la comprobación de firmas para los paquetes en cuestión del repositorio, pero no requiere que la base de datos esté firmada. `Optional` aquí desactivaría un `Required` global para este repositorio.

**Advertencia:** la opción `TrustAll` de SigLevel solamente existe para fines de depuración de código y hace que sea muy fácil confiar en claves que no se han verificado. Hay que usar `TrustedOnly` solo para los repositorios oficiales.

### Inicializar el depósito de claves

Para configurar el depósito de claves de *pacman* hay que ejecutar:

```
# pacman-key --init

```

Arch Linux necesita [entropía](https://es.wikipedia.org/wiki/Entrop%C3%ADa_%28computaci%C3%B3n%29) para arrancar el archivo de claves de pacman. Mover el ratón, presionar teclas aleatoriamente o ejecutar algún tipo de tarea que haga funcionar a una unidad. He aquí algunos ejemplos de esto último: `ls -R /`, `find / -name foo` o `dd if=/dev/sda8 of=/dev/tty7`. Si el sistema no tiene suficiente entropía, este paso puede durar horas. Generando entropía de forma activa se puede completar este proceso mucho más rápidamente.

La aleatoriedad que se crea se usa para configurar un archivo de claves (`/etc/pacman.d/gnupg`) y la firma de la clave GPG del sistema.

**Nota:** si necesita ejecutar `pacman-key --init` en un equipo que no genere mucha entropía (por ejemplo, un servidor sin encabezado), la generación de claves puede llevar mucho tiempo. Para generar una pseudo-entropía, instale [haveged](/index.php/Haveged "Haveged") o [rng-tools](/index.php/Rng-tools "Rng-tools") en el equipo de destino e inicie el servicio correspondiente antes de ejecutar `pacman-key --init`.

## Gestionar el depósito de claves

### Verificar las claves maestras

Para empezar a configurar las claves hay que ejecutar:

```
# pacman-key --populate archlinux

```

No hay que tener prisa a la hora de verificar las [claves de firmas maestras](https://www.archlinux.org/master-keys/) cuando el sistema pregunte por ellas puesto que son las que se van a usar para firmar y, por ende, validar las claves de todos los demás paquetes.

Las llaves PGP son demasiado extensas (2048 bits o más) para que las personas trabajen con ellas. Es por esto que normalmente se reducen a un código hash para crear una huella de 40 dígitos hexadecimales que puede usarse para comparar manualmente que dos claves son exactamente iguales. Los últimos 8 dígitos son el «nombre» de la clave y se les conoce como el ID breve de la clave (key ID —short—) (los últimos dieciséis dígitos de la huella digital supondría la «ID larga de la clave»).

### Añadir las claves de los desarrolladores

Las claves oficiales de los desarrolladores y las de los TUs se firman con las claves maestras por lo que no es necesario que el usuario las firme por si mismo haciendo uso de la herramienta pacman-key. Cuando pacman se encuentra con una clave que no reconoce, pedirá descargarla del `keyserver` establecido en `/etc/pacman.d/gnupg/gpg.conf` (o usando la opción `--keyserver` en la consola). En la Wikipedia se puede encontrar una [lista de servidores de claves](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

Una vez que se ha descargado una clave de un desarrollador no es necesario descargarla de nuevo. Además, se puede usar para verificar otros paquetes que ese desarrollador haya firmado.

**Nota:** el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), que figura entre las dependencias de pacman, contiene las claves actualizadas. En cualquier caso, es posible actualizarlas ejecutando `pacman-key --refresh-keys` (como root). Al ejecutar pacman-key con la opción `--refresh-keys`, se buscará la clave local en el servidor de claves remoto y aparecerá un mensaje alertando de que no ha sido posible encontrar dicha clave. Esto es normal y no es algo por lo que haya que preocuparse.

### Añadir claves no oficiales

Este método se puede utilizar, por ejemplo, para agregar su propia clave al depósito de claves de *pacman*, o para activar los [unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") firmados.

Primero, obtenga el **ID de la clave** (`*keyid*`) de su propiedad. Luego agréguelo al depósito de claves usando uno de los dos métodos siguientes:

1.  Si la clave se encuentra en un servidor de claves, impórtela con: `# pacman-key --recv-keys *keyid*` 
2.  De lo contrario, será facilitado un enlace a un archivo de claves, descárguelo y ejecute: `# pacman-key --add */path/to/downloaded/keyfile*` 

Se recomienda verificar la huella digital, como con cualquier clave maestra o cualquier otra clave que vaya a firmar:

```
$ pacman-key --finger *keyid*

```

Por último, debe firmar localmente la clave importada:

```
# pacman-key --lsign-key *keyid*

```

Ahora otórguele el nivel de confianza a esta clave para firmar paquetes.

### Depurar errores con gpg

Con el propósito de depurar errores, puede acceder al depósito de claves de *pacman* directamente con *gpg*, por ejemplo:

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## Solución de problemas

**Advertencia:** pacman-key depende de [system time](/index.php/System_time "System time"). Si la hora del sistema no es la correcta, aparecerá lo siguiente:
```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```

### No se pueden importar las claves

Existen varias causas posibles de este problema:

*   Un paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) desactualizado.
*   Fecha incorrecta.
*   Su ISP bloqueó el puerto utilizado para importar claves PGP.
*   La memoria caché de *pacman* contiene copia de paquetes sin firmar de intentos anteriores.
*   `dirmngr` no está configurado correctamente

Es posible que se quede bloqueado debido a que el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) no se haya actualizado al realizar una actualización del sistema. Pruebe [actualizar el sistema de nuevo](/index.php/Pacman#Upgrading_packages "Pacman") para ver si así se arregla. Si el problema persiste, asegúrese de que existe el siguiente archivo `/root/.gnupg/dirmngr_ldapservers.conf` y que puede ejecutar con éxito `# dirmngr`. Cree un archivo vacío si no tiene éxito y ejecute `#dirmngr` nuevamente.

Si esto tampoco funciona y la fecha del equipo es correcta, podría intentar cambiar al servidor de claves MIT, que proporciona un puerto alternativo. Para hacer esto, edite `/etc/pacman.d/gnupg/gpg.conf` y cambie la línea `keyserver` a:

```
keyserver hkp://pgp.mit.edu:11371

```

Si ni siquiera el puerto 80 funciona (por ejemplo, cuando la empresa utiliza algún tipo de proxy «transparente» solo para http, en lugar de enrutamiento), lo siguiente podría funcionar:

```
keyserver hkps://hkps.pool.sks-keyservers.net:443

```

Si tiene IPv6 desactivada, *gpg* fallará cuando encuentre alguna dirección IPv6\. En este caso, intente con un servidor de claves solo para IPv4, como:

```
keyserver hkp://ipv4.pool.sks-keyservers.net:11371

```

Si olvida ejecutar `pacman-key --populate archlinux`, es posible que obtenga algunos errores al importar las claves.

Si nada de lo anterior ayuda, la memoria caché de *pacman*, ubicada en `/var/cache/pacman/pkg/` puede contener paquetes sin firmar de intentos anteriores. Intente limpiar la memoria caché manualmente o ejecute:

```
# pacman -Sc

```

que elimina todos los paquetes de la caché que no se han instalado.

### Desactivar la comprobación de las firmas

**Advertencia:** utilice esta opción con precaución. Desactivar las firmas de los paquetes hará que pacman instale automáticamente paquetes de fuentes no confiables.

Si no se está interesado en el firmado de paquetes, se puede desactivar la comprobación de las claves PGP por completo. Edite el fichero `/etc/pacman.conf` y descomente la siguiente lína en `[options]`:

```
SigLevel = Never

```

Hay que descomentar las opciones específicas de SigLevel de cada repositorio también ya que ignoran la configuración global. Esto hará que no haya comprobación alguna de firmas de claves; así es como se procedía habitualmente antes de la llegada de pacman 4\. No es necesario configurar el archivo de claves con *pacman-key* si se decide optar por esta opción. Esta opción se puede modificar más adelante sin problema alguno si se decide activar la verificación de paquetes.

### Restablecer todas las claves

Para eliminar o restablecer todas las claves instaladas en el sistema, elimine el directorio `/etc/pacman.d/gnupg` como root y vuelva a ejecutar `pacman-key --init`. Una vez hecho esto, se pueden añadir las claves que se consideren necesarias.

### Eliminar paquetes inservibles

Si hay paquetes que siguen dando error y se está seguro de haber configurado correctamente *pacman-key*, entonces hay que probar a eliminarlos como por ejemplo con `rm /var/cache/pacman/pkg/*badpackage**` para que se vuelvan a descargar.

Probablemente esta sea la solución al problema del mensaje que aparece al intentar actualizar (`error: linux: signature from "Some Person <Some.Person@example.com>" is invalid`, o parecido). Esto no tiene por qué significar que se esté siendo víctima de un ataque [MITM](https://en.wikipedia.org/wiki/es:Ataque_de_intermediario "wikipedia:es:Ataque de intermediario"), ni mucho menos; indica tan sólo que el archivo descargargado está corrupto.

### La firma es de confianza desconocida

A veces, al ejecutar `pacman -Suy` puede encontrar este error:

```
error: *package-name*: signature from "*packager*" is unknown trust

```

Esto ocurre porque la clave de `*packager*` utilizada en el paquete `*package-name*` no está presente y/o no es de confianza en la base de datos gpg local de pacman-key. Al parecer pacman no siempre puede verificar si la clave fue recibida y marcada como confiable antes de continuar. Mitigue esto [firmando manualmente la clave no confiable localmente](#Adding_unofficial_keys) o [restableciendo todas las claves](#Resetting_all_the_keys).

### Actualizar claves a través de proxy

Para usar un proxy al actualizar las claves, la opción `honor-http-proxy` debe configurarse tanto en `/etc/gnupg/dirmngr.conf` como en `/etc/pacman.d/gnupg/dirmngr.conf`. Vea [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG") para más información.

**Nota:** si se usa *pacman-key* sin la opción `honor-http-proxy` y falla, un reinicio puede resolver el problema.

## Véase también

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/DeveloperWiki:Package_Signing_Proposal_for_Pacman "DeveloperWiki:Package Signing Proposal for Pacman")
*   [Pacman Package Signing – 1: Makepkg and Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Pacman Package Signing – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Pacman Package Signing – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Pacman Package Signing – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)
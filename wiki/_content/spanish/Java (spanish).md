Originario de [Wikipedia article](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)"):

	Java es un lenguaje de programación desarrollado originalmente por Sun Microsystems lanzado en 1995 como un componente central de Sun Microsystems' Java Platform. El lenguaje se deriva en gran parte de la sintaxis de C y C++ pero tiene un modelo de objetos más sencillo y menos facilidades de bajo nivel. Las aplicaciones java son normalmente compiladas en códigos de bytes que pueden correr en alguna máquina virtual java (JVM por sus siglas en inglés) independientemente de la arquitectura de la computadora.

Arch Linux oficialmente soporta el paquete de código abierto [OpenJDK](http://openjdk.java.net/) versión 7,8,9 y 10\. Todas las JVM pueden ser instaladas sin conflictos e intercambiadas antes de usar con la ayuda de un script `archlinux-java`. Otros ambientes java están disponibles en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") pero no son oficialmente soportados.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Paquetes con soporte oficial](#Paquetes_con_soporte_oficial)
    *   [1.2 Paquetes sin soporte oficial](#Paquetes_sin_soporte_oficial)
*   [2 Marcar paquetes como antiguos](#Marcar_paquetes_como_antiguos)
*   [3 Cambiar entre ambientes de JVM](#Cambiar_entre_ambientes_de_JVM)
    *   [3.1 Lista de ambientes de Java instalados](#Lista_de_ambientes_de_Java_instalados)
    *   [3.2 Cambiar el ambiente de Java](#Cambiar_el_ambiente_de_Java)
    *   [3.3 De-seleccionar el ambiente actual de Java](#De-seleccionar_el_ambiente_actual_de_Java)
    *   [3.4 Arreglo un ambiente de Java](#Arreglo_un_ambiente_de_Java)
    *   [3.5 Ejecutar una aplicación con un ambiente no seleccionado de Java](#Ejecutar_una_aplicación_con_un_ambiente_no_seleccionado_de_Java)

## Instalación

**Nota:**

*   Instalar JDK automáticamente descargara la dependencia JRE.
*   Después de la instalación, el entorno de Java debe ser reconocido por la shell en la variable `$PATH`. Esto se puede hacer modificando `/etc/profile` o simplemente cerrando y abriendo la sesión de nuevo.

Dos paquetes *comunes* llamados [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (contiene archivos comunes para el Runtine de un entorno de Java) y [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (contiene archivos comunes para el kit de desarrollo de Java). El archivo de entorno `/etc/profile.d/jre.sh` contiene un link a `/usr/lib/jvm/default/bin`, el cual se puede modificar con el script `archlinux-java`. Los links en `/usr/lib/jvm/default` y `/usr/lib/jvm/default-runtime` **solo** se deben modificar con `archlinux-java`. Este script apunta a una versión valida y sin conflictos de un ambiente de Java en `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}` o a un runtime de Java en `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}/jre`.

La mayoría de los ejecutables de Java se proveen como links directos en `/usr/bin`, mientras que otros están disponibles en `$PATH`.

**Advertencia:** El archivo `/etc/profile.d/jdk.sh` no es proporcionado por ningun paquete.

### Paquetes con soporte oficial

**OpenJDK 10** — La implementación de referencia de código abierto de Java SE.

	[http://openjdk.java.net/projects/jdk/10/](http://openjdk.java.net/projects/jdk/10/) || [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless) [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk) [jdk10-openjdk](https://www.archlinux.org/packages/?name=jdk10-openjdk) [openjdk10-doc](https://www.archlinux.org/packages/?name=openjdk10-doc) [openjdk10-src](https://www.archlinux.org/packages/?name=openjdk10-src)

**OpenJDK 9** — La implementación de referencia de código abierto de la novena edición de Java SE.

	[http://openjdk.java.net/projects/jdk9/](http://openjdk.java.net/projects/jdk9/) || [jre9-openjdk-headless](https://www.archlinux.org/packages/?name=jre9-openjdk-headless) [jre9-openjdk](https://www.archlinux.org/packages/?name=jre9-openjdk) [jdk9-openjdk](https://www.archlinux.org/packages/?name=jdk9-openjdk) [openjdk9-doc](https://www.archlinux.org/packages/?name=openjdk9-doc) [openjdk9-src](https://www.archlinux.org/packages/?name=openjdk9-src)

**OpenJDK 8** — La implementación de referencia de código abierto de la octava edición de Java SE.

	[http://openjdk.java.net/projects/jdk8/](http://openjdk.java.net/projects/jdk8/) || [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src)

**OpenJDK 7** — La implementación de referencia de código abierto de la séptima edición de Java SE.

	[http://openjdk.java.net/projects/jdk7/](http://openjdk.java.net/projects/jdk7/) || [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src)

**OpenJFX 8** — La implementación de referencia de código abierto de JavaFX. [No es](https://wiki.openjdk.java.net/display/OpenJFX/Repositories+and+Releases) necesario instalar este paquete si se hace uso de Java SE. Este paquete es solo para usuarios que buscan la implementacion de codigo abierto de Java (Proyecto OpenJDK).

	[http://openjdk.java.net/projects/openjfx/](http://openjdk.java.net/projects/openjfx/) || [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src)

### Paquetes sin soporte oficial

**Java SE** — Implementación de JRE y JDK de la empresa Oracle.

	[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre6](https://aur.archlinux.org/packages/jre6/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre9](https://aur.archlinux.org/packages/jre9/) [jre-devel](https://aur.archlinux.org/packages/jre-devel/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk9](https://aur.archlinux.org/packages/jdk9/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**OpenJ9** — Implementación de JRE por Eclipse, contribuida por IBM.

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/) [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/)

**IBM J9 8** — Implementación de la octava edición de JRE por IBM.

	[https://developer.ibm.com/javasdk/downloads/sdk8/](https://developer.ibm.com/javasdk/downloads/sdk8/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/)

**IBM J9 7** — Implementación de la séptima edición de JRE por IBM.

	[https://developer.ibm.com/javasdk/downloads/sdk7/](https://developer.ibm.com/javasdk/downloads/sdk7/) || [jdk7-j9-bin](https://aur.archlinux.org/packages/jdk7-j9-bin/) [jdk7r1-j9-bin](https://aur.archlinux.org/packages/jdk7r1-j9-bin/)

**Parrot VM** — Una maquina virtual con soporte experimental para Java [[1]](http://trac.parrot.org/parrot/wiki/Languages) mediante dos métodos: ya sea [Java VM bytecode](http://code.google.com/p/parrot-jvm/), o como [compilador de Java focalizado a Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://aur.archlinux.org/packages/parrot/)

**Nota:** Versiones de 32-bit de Java SE se pueden encontrar con el prefijo `bin32-`, v.g. [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) y [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/). Estos usan [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/), el cual funciona como [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) con el sufijo `32`, v.g. `java32`. La misma analogía se aplica a [java32-environment-common](https://aur.archlinux.org/packages/java32-environment-common/), que solo se usa para paquete de 32-bit de JDK.

## Marcar paquetes como antiguos

Aunque las versiones de los paquetes de Arch Linux pueden contener referencia a las versiones propietarias en las cuales se basan, el proyecto de código abierto tiene su propio esquema de versiones:

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk), y [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) deben ser marcados como antiguos de acuerdo a la [versión de *IcedTea*](http://icedtea.wildebeest.org/download/source) (v.g. `2.4.3`), y no a la versión de referencia de la empresa Oracle (v.g. `u45` en el lanzamiento `7.u45_2.4.3-1`).
*   [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web), este paquete debe ser marcado como antiguo basado en la [versión de *IcedTea Web*](http://icedtea.wildebeest.org/download/source) (v.g. `1.4.1`). Esta es independiente de la versión de *IcedTea*.

## Cambiar entre ambientes de JVM

El script `archlinux-java` provee dicha funcionalidad:

```
archlinux-java <COMMANDO>

COMMANDO:
	status		Lista de ambientes de Java instalados y el que esta seleccionado
	get		Responde con el nombre corto del ambiente de Java seleccionado por defecto
	set <JAVA_ENV>	Se obliga que <AMBIENTE_JAVA> sea por defecto
	unset		De-seleccionar el ambiente actual de Java
	fix		Arregla un ambiente roto/invalido de Java

```

### Lista de ambientes de Java instalados

```
$ archlinux-java status

```

Ejemplo:

```
$ archlinux-java status
Available Java environments:     ### Ambientes de Java disponibles
  java-7-openjdk (default)
  java-8-openjdk/jre

```

Note que el *(default)* denota que la versión `java-7-openjdk` esta actualmente seleccionada por defecto. Al ejecutar `java` y otros binarios se usará esa instalación. También note que solo la parte de JRE de OpenJDK 8 esta instalada.

### Cambiar el ambiente de Java

```
# archlinux-java set <AMBIENTE_JAVA>

```

Ejemplo:

```
# archlinux-java set java-8-openjdk/jre

```

**Sugerencia:** Para ver posibles nombres de `<AMBIENTE_JAVA>`, use `archlinux-java status`.

Note que `archlinux-java` no lo dejara seleccionar un nombre invalido. En el ejemplo anterior [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) esta instalado pero [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) **no**, así que intentar seleccionar `java-8-openjdk` fallara:

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path  ### no es un ambiente de Java valido

```

### De-seleccionar el ambiente actual de Java

No debería existir la necesidad de de-seleccionar un ambiente ya que el paquete que lo provee debería hacerlo. De cualquier manera, si lo desea hacer solo necesita el comando `unset`:

```
# archlinux-java unset

```

### Arreglo un ambiente de Java

Si se ha hecho un link que no es valido en un ambiente de Java, ejecutando `archlinux-java fix` intenta repararlo. Nótese que si ningún ambiente esta seleccionado, este buscara nombres validos y seleccionara uno. Paquetes oficialmente soportados "OpenJDK 7" y "OpenJDK 8" tendrán preferencia y serán considerados de primero, después se consideraran los paquetes de [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

```
# archlinux-java fix

```

### Ejecutar una aplicación con un ambiente no seleccionado de Java

Si desea ejecutar una aplicación con otra versión de Java, se puede envolver la aplicación en un pequeño script de bash que localmente cambia el PATH que Java usara. Por ejemplo, si la versión por defecto es jre7 y se desea usar jre8:

```
#!/bin/sh 

export PATH=/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH
exec /ruta/a/aplicación "$@"

```
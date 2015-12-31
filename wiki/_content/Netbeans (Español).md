# Netbeans (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**NetBeans** es un entorno de desarrollo integrado (**IDE** por sus siglas en inglés). Permite desarrollar en Java, JavaScript, PHP, Python, Ruby, Groovy, C/C++, Scala, Clojure, etc.

De [Wikipedia](http://es.wikipedia.org/wiki/NetBeans):

«**NetBeans** es un entorno de desarrollo integrado libre, hecho principalmente para el lenguaje de programación **Java**. Existe además un número importante de módulos para extenderlo. **NetBeans IDE** es un producto libre y gratuito sin restricciones de uso.»

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Consejos](#Consejos)
    *   [2.1 Antialiasing de las fuentes en NetBeans](#Antialiasing_de_las_fuentes_en_NetBeans)
        *   [2.1.1 Solo NetBeans](#Solo_NetBeans)
        *   [2.1.2 Java en general](#Java_en_general)
    *   [2.2 «Look and feel» estilo GTK](#.C2.ABLook_and_feel.C2.BB_estilo_GTK)
*   [3 Problemas conocidos](#Problemas_conocidos)
    *   [3.1 OpenJDK vs SunJDK](#OpenJDK_vs_SunJDK)
    *   [3.2 Glassfish server - No puede descargar Glassfish server. I/O Exception](#Glassfish_server_-_No_puede_descargar_Glassfish_server._I.2FO_Exception)
    *   [3.3 NetBeans no se ejecuta despues de la primera ejecución](#NetBeans_no_se_ejecuta_despues_de_la_primera_ejecuci.C3.B3n)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Primero tendrás que instalar algún entorno de desarrollo java. El recomendado es [jdk](https://aur.archlinux.org/packages/jdk/)<sup><small>AUR</small></sup>, la implementación de java por Oracle. También puedes instalar otro entorno [Java](/index.php/Java "Java"). Ten en cuenta que la dependencia requerida será java-environment.

Los paquetes de instalación de Netbeans en español están en el [AUR](/index.php/Arch_User_Repository "Arch User Repository"):

1.  [netbeans-es](https://aur.archlinux.org/packages/netbeans-es/)<sup><small>AUR</small></sup>

## Consejos

**Nota:** El archivo global de configuración `/usr/share/netbeans/etc/netbeans.conf` es sobreescrito en las actualizaciones. Para mantener los cambios realizados escribalos en el archivo local de configuración `~/.netbeans/<version>/etc/netbeans.conf` (Será necesario crear el directorio `/etc` y el archivo `.conf`).

### Antialiasing de las fuentes en NetBeans

#### Solo NetBeans

Añada `-J-Dswing.aatext=TRUE -J-Dawt.useSystemAAFontSettings=on` en la linea «netbeans_default_options» de su archivo de configuración.

#### Java en general

Vease [Java#Better font rendering](/index.php/Java#Better_font_rendering "Java") (en inglés).

### «Look and feel» estilo GTK

Para cambiar la aparencia de NetBeans a GTK añada `--laf com.sun.java.swing.plaf.gtk.GTKLookAndFeel` en la sección «netbeans_default_options» del archivo de configuración o en el archivo `.desktop` con el que lanza la aplicación.

## Problemas conocidos

### OpenJDK vs SunJDK

NetBeans 7.0-1 no siempre funciona con OpenJDK, algunos de los errores son:

*   En algunas situaciones NetBeans no se ejecuta.
*   El script `.sh` de instalación de netbeans no ejecuta la GUI del instalador.
*   El modulo JavaFX no funciona. Vease [FS#29843](https://bugs.archlinux.org/task/29843) (en inglés).

### Glassfish server - No puede descargar Glassfish server. I/O Exception

Esta situación ocurre cuando se intenta añadir un nuevo Glassfish server y NetBeans devuelve

```
 I/O Exception: [http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip](http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip)

```

La solución consiste en:

*   Descargar GlassFish Server Open Source Edition manualmente desde el sitio oficial ([http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip](http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip)).
*   Descomprimir el .zip en cualquier directorio.

### NetBeans no se ejecuta despues de la primera ejecución

Si esto ocurriese ejecute NetBeans desde una terminal:

 `# netbeans -h` 

```
  Exception in thread "main" java.lang.UnsatisfiedLinkError: /usr/lib/jvm/java-6-openjdk/jre/lib/i386/libsplashscreen.so: libgif.so.4: cannot open shared object file: No such file or directory

```

Si la terminal le devuelve una salida como la de arriba entonces tiene dos opciones:

*   Ejecutar NetBeans usando la opción `--nosplash`

```
 # netbeans --nosplash

```

*   Instalar el paquete que falta ([libungif](https://www.archlinux.org/packages/?name=libungif)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>). NetBeans debería funcionar correctamente ahora.

Para más información consultar este [hilo](https://bbs.archlinux.org/viewtopic.php?id=118930) del foro

## Véase también

*   [Pagina oficial de NetBeans](http://www.netbeans.org)
*   [Articulo de NetBeans en la Wikipedia](http://es.wikipedia.org/wiki/NetBeans)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Netbeans_(Español)&oldid=413925](https://wiki.archlinux.org/index.php?title=Netbeans_(Español)&oldid=413925)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development (Español)](/index.php/Category:Development_(Espa%C3%B1ol) "Category:Development (Español)")
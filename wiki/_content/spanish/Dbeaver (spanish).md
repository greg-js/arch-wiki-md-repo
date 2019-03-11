**Estado de la traducción**
Este artículo es una traducción de [Dbeaver](/index.php/Dbeaver "Dbeaver"), revisada por última vez el **2019-02-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dbeaver&diff=0&oldid=567403) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Dbeaver es una herramienta de administración de base de datos multiplataforma. Para más información acerca de las características vea la [página oficial](https://dbeaver.jkiss.org/).

Soporta bases de datos populares tales como [MySQL](/index.php/MySQL_(Espa%C3%B1ol) "MySQL (Español)"), [MariaDB](/index.php/MariaDB "MariaDB"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [SQLite](/index.php/SQLite "SQLite"), [Oracle](/index.php/Oracle "Oracle").

Proporciona una arquitectura de complementos (basado en la arquitectura de complementos de Eclipse) que permite modificar gran parte del comportamiento de la aplicación para proveer funcionalidad específica de la base de datos o características que son independientes de la base de datos. Esto es una aplicación de escritorio escrito en Java y basado en la plataforma de Eclipse.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dbeaver](https://www.archlinux.org/packages/?name=dbeaver).

También hay algunos complementos disponibles:

*   [dbeaver-plugin-apache-poi](https://www.archlinux.org/packages/?name=dbeaver-plugin-apache-poi) - Biblioteca DBeaver para documentos Microsoft Office
*   [dbeaver-plugin-batik](https://www.archlinux.org/packages/?name=dbeaver-plugin-batik) - Biblioteca DBeaver para formato SVG
*   [dbeaver-plugin-office](https://www.archlinux.org/packages/?name=dbeaver-plugin-office) - Complemento DBeaver para exportar datos a formato Microsoft Office
*   [dbeaver-plugin-svg-format](https://www.archlinux.org/packages/?name=dbeaver-plugin-svg-format) - Complemento DBeaver para almacenar diagramas en formato SVG

## Solución de problemas

Si recibe un error como éste:

```
 JVM terminated. Exit code=1
 /bin/java
 -XX:+IgnoreUnrecognizedVMOptions
 -Xms64m
 -Xmx1024m
 -jar /usr/lib/dbeaver//plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar
 -os linux
 -ws gtk
 -arch x86_64
 -showsplash
 -launcher /usr/lib/dbeaver/dbeaver
 -name Dbeaver
 --launcher.library /usr/lib/dbeaver//plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.551.v20171108-1834/eclipse_1630.so
 -startup /usr/lib/dbeaver//plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar
 --launcher.overrideVmargs
 -exitdata 5b000e
 -vm /bin/java
 -vmargs
 -XX:+IgnoreUnrecognizedVMOptions
 -Xms64m
 -Xmx1024m
 -jar /usr/lib/dbeaver//plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar

```

Intente agregar `export _JAVA_OPTIONS="-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel"` en su [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)").
Dbeaver is a free multi-platform database database administration tool. For more information about features, see the [official homepage](https://dbeaver.jkiss.org/).

It supports popular databases such as [MySQL](/index.php/MySQL "MySQL"), [MariaDB](/index.php/MariaDB "MariaDB"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [SQLite](/index.php/SQLite "SQLite"), [Oracle](/index.php/Oracle "Oracle").

It provides a plugin architecture (based on Eclipse plugins architecture) that allows to modify much of the application behavior to provide database-specific functionality or features that are database-independent. This is a desktop application written in Java and based on Eclipse platform.

## Installation

[Install](/index.php/Install "Install") the [dbeaver](https://www.archlinux.org/packages/?name=dbeaver) package.

There are also some plugins available:

*   [dbeaver-plugin-apache-poi](https://www.archlinux.org/packages/?name=dbeaver-plugin-apache-poi) - DBeaver library for Microsoft Office documents
*   [dbeaver-plugin-batik](https://www.archlinux.org/packages/?name=dbeaver-plugin-batik) - DBeaver library for SVG format
*   [dbeaver-plugin-office](https://www.archlinux.org/packages/?name=dbeaver-plugin-office) - DBeaver plugin to export data to Microsoft Office format
*   [dbeaver-plugin-svg-format](https://www.archlinux.org/packages/?name=dbeaver-plugin-svg-format) - DBeaver plugin to save diagrams in SVG format

## Troubleshooting

If you are getting an error like this:

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

Try adding `export _JAVA_OPTIONS="-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel"` to your [xinitrc](/index.php/Xinitrc "Xinitrc").
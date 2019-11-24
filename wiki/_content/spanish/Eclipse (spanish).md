**Estado de la traducción**
Este artículo es una traducción de [Eclipse](/index.php/Eclipse "Eclipse"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Eclipse&diff=0&oldid=544551) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Eclipse](https://eclipse.org) es un proyecto de la comunidad de código abierto, que tiene como objetivo proporcionar una plataforma de desarrollo universal. El proyecto Eclipse es ampliamente conocido por su entorno de desarrollo integrado multiplataforma (IDE). Los paquetes de Arch Linux (y esta guía) se relacionan específicamente con el IDE.

El IDE de Eclipse está escrito principalmente en Java, pero se puede usar para desarrollar aplicaciones en varios lenguajes, incluidos Java, C/C++, PHP, Perl y Python. El IDE también puede proporcionar soporte de subversión y administración de tareas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Complementos](#Complementos)
    *   [2.1 Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualización_predeterminado)
    *   [2.2 Eclipse Marketplace](#Eclipse_Marketplace)
    *   [2.3 Administrador de complementos](#Administrador_de_complementos)
        *   [2.3.1 Actualizaciones a través del administrador de complementos](#Actualizaciones_a_través_del_administrador_de_complementos)
    *   [2.4 Lista de complementos](#Lista_de_complementos)
*   [3 Habilitar la integración de javadoc](#Habilitar_la_integración_de_javadoc)
    *   [3.1 Versión en linea](#Versión_en_linea)
    *   [3.2 Versión fuera de línea](#Versión_fuera_de_línea)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Ctrl+X cierra Eclipse](#Ctrl+X_cierra_Eclipse)
    *   [4.2 Tema oscuro](#Tema_oscuro)
    *   [4.3 Cambiar el tamaño de fuente del título predeterminado de la ventana](#Cambiar_el_tamaño_de_fuente_del_título_predeterminado_de_la_ventana)
    *   [4.4 Deshabilitar GTK+ 3](#Deshabilitar_GTK+_3)
    *   [4.5 Freshplayerplugin](#Freshplayerplugin)
    *   [4.6 Eclipse 4.6 no puede abrir marketplace adecuadamente](#Eclipse_4.6_no_puede_abrir_marketplace_adecuadamente)
    *   [4.7 Mostrar en el Explorador del sistema no funciona](#Mostrar_en_el_Explorador_del_sistema_no_funciona)
    *   [4.8 Muestra problemas en Wayland](#Muestra_problemas_en_Wayland)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") uno de los siguientes paquetes:

*   [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee) para Desarrolladores Java EE
*   [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java) para Desarrolladores Java
*   [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp) para Desarrolladores C/C++
*   [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) para Desarrolladores PHP
*   [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript) para Desarrolladores JavaScript

No puede instalar múltiples de estos al mismo tiempo ya que entran en conflicto, ver [FS#45577](https://bugs.archlinux.org/task/45577): elija el paquete que más se ajusta a sus necesidades, y luego agregue soporte para cualquier idioma adicional requerido a través de [#Complementos](#Complementos).

## Complementos

Muchos complementos se instalan fácilmente usando **pacman** (ver [Eclipse plugin package guidelines (Español)](/index.php/Eclipse_plugin_package_guidelines_(Espa%C3%B1ol) "Eclipse plugin package guidelines (Español)") para mayor información). Esto también los mantendrá actualizados. Alternativamente, puede elegir entre [Eclipse Marketplace](#Eclipse_Marketplace) o la terminal [Administrador de complementos](#Administrador_de_complementos).

### Agregar el sitio de actualización predeterminado

Asegúrese de verificar que el sitio de actualización predeterminado para su versión de Eclipse esté configurado para que las dependencias del complemento puedan instalarse automáticamente. La versión más reciente de Eclipse es Photon y el sitio de actualización predeterminado es: [http://download.eclipse.org/releases/photon](http://download.eclipse.org/releases/photon). Vaya a Ayuda> Instalar nuevo software> Agregar, complete el nombre para luego identificar fácilmente el sitio de actualización, por ejemplo, Photon Software Repository, y complete la ubicación con la url.

### Eclipse Marketplace

**Nota:** asegúrate de haber seguido la sección [Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualización_predeterminado).

Para usar Eclipse Marketplace, instálelo primero: vaya a Ayuda> Instalar nuevo software> Cambiar al sitio de actualización predeterminado> Herramientas de propósito general> Cliente de Marketplace. Reinicie Eclipse y estará disponible en Ayuda > Eclipse Marketplace.

### Administrador de complementos

**Nota:** asegúrate de haber seguido la sección [Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualización_predeterminado).

Utilice el administrador de complementos de Eclipse para descargar e instalar complementos desde sus repositorios originales: en este caso debe encontrar el repositorio necesario en el sitio web del complemento, luego vaya a *Ayuda> Instalar nuevo software...*, ingrese el repositorio en el campo *Trabajar con* , seleccione el complemento para instalar de la lista a continuación y siga las instrucciones.

**Nota:**

*   Si instala complementos con el administrador de complementos de Eclipse, se le recomienda iniciar Eclipse como root: de esta manera los complementos se instalarán en `/usr/lib/eclipse/plugins/`; si los instaló como usuario normal, se almacenarán en una carpeta de versión dependiente dentro de `~/.eclipse/`, y, después de actualizar Eclipse, ya no serían reconocidos
*   No use Eclipse como root para su trabajo diario.

#### Actualizaciones a través del administrador de complementos

Ejecute Eclipse y seleccione *Ayuda> Buscar actualizaciones* . Si los ha instalado como root como se recomienda en la sección anterior, debe ejecutar Eclipse como root.

Para que los complementos se actualicen, debe verificar que sus repositorios de actualización estén habilitados en *Ventana> Preferencias> Instalar / Actualizar> Sitios de software disponibles* : puede encontrar los repositorios de cada plugin en el sitio web del proyecto respectivo. Para agregar, editar, eliminar ... los repositorios solo usan los botones a la derecha del panel *Sitios de software disponibles* . Para Eclipse 4.5 (Marte), verifique que haya habilitado este repositorio:

```
[http://download.eclipse.org/releases/mars](http://download.eclipse.org/releases/mars)

```

Para recibir notificaciones de actualización, vaya a *Ventana> Preferencias> Instalar / Actualizar> Actualizaciones automáticas* . Si desea recibir notificaciones de plugins instalados como root, se debe ejecutar Eclipse como root, vaya a *Ventana> Preferencias> Instalar / Actualizar> Sitios disponibles sobre software* , seleccionar los repositorios relacionados con los plugins instalados y *Exportar' ', luego ejecutar Eclipse como usuario normal e "Importarlos" en el mismo panel.*

### Lista de complementos

*   **AVR** — complemento de microcontrolador AVR.

	[http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) || [eclipse-avr](https://aur.archlinux.org/packages/eclipse-avr/)

*   **Aptana** — soporte HTML5/CSS3/JavaScript/Ruby/Rails/PHP/Pydev/Django. También disponible como aplicación independiente.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **IvyDE** — administrador de dependencias IvyDE.

	[https://ant.apache.org/ivy/ivyde/](https://ant.apache.org/ivy/ivyde/) || [eclipse-ivyde](https://aur.archlinux.org/packages/eclipse-ivyde/)

*   **Markdown** — editor de complementos para Eclipse Markdown.

	[http://www.winterwell.com/software/markdown-editor.php](http://www.winterwell.com/software/markdown-editor.php) || [eclipse-markdown](https://aur.archlinux.org/packages/eclipse-markdown/)

*   **PyDev** — soporte [Python (Español)](/index.php/Python_(Espa%C3%B1ol) "Python (Español)").

	[http://pydev.org/](http://pydev.org/) || [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

*   **Subclipse** — soporte [Subversion (Español)](/index.php/Subversion_(Espa%C3%B1ol) "Subversion (Español)").

	[https://github.com/subclipse/subclipse](https://github.com/subclipse/subclipse) || [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)

*   **Subversive** — Soporte alternativo de Subversion.

	[https://www.eclipse.org/subversive/](https://www.eclipse.org/subversive/) || [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

*   **TestNG** — soporte TestNG.

	[http://testng.org/doc/eclipse.html](http://testng.org/doc/eclipse.html) || [eclipse-testng](https://aur.archlinux.org/packages/eclipse-testng/)

*   **TeXlipse** — soporte [TeX Live (Español)](/index.php/TeX_Live_(Espa%C3%B1ol) "TeX Live (Español)").

	[http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/) || [eclipse-texlipse](https://aur.archlinux.org/packages/eclipse-texlipse/)

*   **Checkstyle** — Soporte de Eclipse Checkstyle.

	[http://eclipse-cs.sourceforge.net/](http://eclipse-cs.sourceforge.net/) || [eclipse-checkstyle](https://aur.archlinux.org/packages/eclipse-checkstyle/)

## Habilitar la integración de javadoc

¿Desea ver las entradas de la API al colocar el puntero del mouse sobre los métodos estándar de Java?

### Versión en linea

Si tiene acceso constante a Internet en su máquina, puede usar la documentación en línea:

1.  Vaya a *Ventana> Preferencias* , luego vaya a *Java> JRE instalados* .
2.  Debería haber uno llamado "java" con el tipo "VM estándar". Seleccione esto y haga clic en *Editar* .
3.  Seleccione el elemento `/opt/java/jre/lib/rt.jar` en "Bibliotecas de sistema de JRE:", luego haga clic en "Ubicación de Javadoc ...".
4.  Ingrese "[https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)" en el campo de texto "Ruta de ubicación de Javadoc:".

### Versión fuera de línea

Puede almacenar la documentación localmente instalando el paquete [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc). Eclipse puede encontrar los javadocs automáticamente. Si eso no funciona, configure la ubicación de Javadoc para rt.jar en `file:/usr/share/doc/java8-openjdk/api`.

## Solución de problemas

### Ctrl+X cierra Eclipse

Parte de [este](https://bugs.eclipse.org/bugs/show_bug.cgi?id=318177) error. Solo busque en `~/workspace/.metadata/.plugins/org.eclipse.e4.workbench/workbench.xmi` y elimine la combinación incorrecta de `Ctrl + X`. Por lo general, es el primero.

### Tema oscuro

Eclipse proporciona un tema oscuro que se puede habilitar en Ventana> Preferencias> General> Apariencia y seleccionando el tema "Oscuro". El tema oscuro usa sus propios colores en lugar de los colores del tema GTK, si prefiere respetar completamente la configuración de color GTK, quite o mueva a la subcarpeta de respaldo todos los archivos .css de `/usr/share/eclipse/plugins/org.eclipse.ui.themes_1.0.0.xxxx/css/`.

### Cambiar el tamaño de fuente del título predeterminado de la ventana

No puede cambiar el tamaño de la fuente del título de la ventana con las preferencias de Eclipse, debe editar los archivos .css del tema real. Tenga en cuenta que tendrá que volver a hacer esto cuando actualice Eclipse. Están ubicados debajo

```
/usr/share/eclipse/plugins/org.eclipse.platform_4.3.<su número de versión>/css

```

Abra el archivo apropiado con su editor de texto, es decir, e4_default_gtk.css si está utilizando el "tema GTK". Busque .MPartStack y cambie el tamaño de la fuente al tamaño deseado.

```
.MPartStack {
       font-size: 9;
       swt-simple: false;
       swt-mru-visible: false;
}

```

### Deshabilitar GTK+ 3

Cuando la interfaz de usuario SWT GTK + 3 tiene errores y, a veces, no se puede utilizar, puede intentar desactivar el uso de GTK + 3 con SWT_GTK3 = 0 [Environment variables (Español)](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") cuando se inicia eclipse:

Otra opción para lograr el mismo efecto es agregar lo siguiente a `/usr/lib/eclipse/eclipse.ini`.

```
--launcher.GTK_version
2

```

Esas dos líneas se deben agregar *'antes de'* :

```
--launcher.appendVmargs

```

### Freshplayerplugin

Eclipse no es compatible con [freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/). Ver [https://github.com/i-rinat/freshplayerplugin/issues/298](https://github.com/i-rinat/freshplayerplugin/issues/298).

### Eclipse 4.6 no puede abrir marketplace adecuadamente

Ver [este](https://bugs.eclipse.org/bugs/show_bug.cgi?id=497729) error. Puede seguir los dos pasos siguientes para solucionarlo:

```
eclipse -consoleLog -application org.eclipse.equinox.p2.director -uninstallIU org.apache.httpcomponents.httpclient/4.3.6.v201411290715
cd /usr/lib/eclipse/ && sudo rm plugins/org.apache.httpcomponents.httpclient_4.3.6.v201411290715.jar

```

### Mostrar en el Explorador del sistema no funciona

Ver [ésta](http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.platform.doc.user%2Freference%2Fref-9.htm&cp=0_4_1_52) guía. Ir a *'Ventana'* > *'Preferencias'* > *'General'* > *'Área de trabajo'* y cambie el explorador del sistema de ejecución de comandos. Como usuario de Xfce, puede cambiarlo a `thunar $ {selected_resource_uri`} para abrir la carpeta seleccionada con thunar.

### Muestra problemas en Wayland

Al ejecutar Eclipse en Wayland, puede encontrar problemas de renderizado, como un tiempo de respuesta lento a los eventos del mouse o ventanas de diálogo cortadas (informe de errores [[1]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=483545)). Una solución posible para este problema es forzar a Eclipse a ejecutar bajo XWayland.

Con el superusuario, abrir el archivo `/usr/bin/eclipse` y anexar esta línea antes de la línea `exec`:

```
export GDK_BACKEND=x11

```

Esto forzará la ejecución de Eclipse en XWayland.

## Véase también

*   [¿Cómo usar Subversion con Eclipse?](https://www.ibm.com/developerworks/library/os-ecl-subversion/)
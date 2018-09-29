**Estado de la traducción:** este artículo es una versión traducida de [Eclipse](/index.php/Eclipse "Eclipse"). Fecha de la última traducción/revisión: **2018-09-29**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Eclipse&diff=0&oldid=544551).

[Eclipse](https://eclipse.org) es un proyecto de la comunidad de código abierto, que tiene como objetivo proporcionar una plataforma de desarrollo universal. El proyecto Eclipse es ampliamente conocido por su entorno de desarrollo integrado multiplataforma (IDE). Los paquetes de Arch Linux (y esta guía) se relacionan específicamente con el IDE.

El IDE de Eclipse está escrito principalmente en Java, pero se puede usar para desarrollar aplicaciones en varios idiomas, incluidos Java, C/C++, PHP, Perl y Python. El IDE también puede proporcionar soporte de subversión y administración de tareas.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Complementos](#Complementos)
    *   [2.1 Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualizaci.C3.B3n_predeterminado)
    *   [2.2 Eclipse Marketplace](#Eclipse_Marketplace)
    *   [2.3 Administrador de complementos](#Administrador_de_complementos)
        *   [2.3.1 Actualizaciones a través del administrador de complementos](#Actualizaciones_a_trav.C3.A9s_del_administrador_de_complementos)
    *   [2.4 List of plugins](#List_of_plugins)
*   [3 Enable javadoc integration](#Enable_javadoc_integration)
    *   [3.1 Online version](#Online_version)
    *   [3.2 Offline version](#Offline_version)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ctrl+X closes Eclipse](#Ctrl.2BX_closes_Eclipse)
    *   [4.2 Dark theme](#Dark_theme)
    *   [4.3 Change Default Window Title Font Size](#Change_Default_Window_Title_Font_Size)
    *   [4.4 Disable GTK+ 3](#Disable_GTK.2B_3)
    *   [4.5 Freshplayerplugin](#Freshplayerplugin)
    *   [4.6 Eclipse 4.6 may not open the marketplace properly](#Eclipse_4.6_may_not_open_the_marketplace_properly)
    *   [4.7 Show in System Explorer does not work](#Show_in_System_Explorer_does_not_work)
    *   [4.8 Display issues under Wayland](#Display_issues_under_Wayland)
*   [5 See also](#See_also)

## Instalación

[Instalar](/index.php/Instalar "Instalar") uno de los siguientes paquetes:

*   [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee) para Desarrolladores Java EE
*   [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java) para Desarrolladores Java
*   [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp) para Desarrolladores C/C++
*   [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) para Desarrolladores PHP
*   [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript) para Desarrolladores JavaScript

No puede instalar múltiples de estos al mismo tiempo ya que entran en conflicto, vea [FS#45577](https://bugs.archlinux.org/task/45577): elija el paquete que más se ajusta a sus necesidades, y luego agregue soporte para cualquier idioma adicional requerido a través de [#Plugins](#Plugins).

## Complementos

Muchos complementos se instalan fácilmente usando **pacman** (vea [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") para mayor información). Esto también los mantendrá actualizados. Alternativamente, puede elegir entre [Eclipse Marketplace](#Eclipse_Marketplace) o la terminal [plugin manager](#Plugin_manager).

### Agregar el sitio de actualización predeterminado

Asegúrese de verificar que el sitio de actualización predeterminado para su versión de Eclipse esté configurado para que las dependencias del complemento puedan instalarse automáticamente. La versión más reciente de Eclipse es Photon y el sitio de actualización predeterminado es: [http://download.eclipse.org/releases/photon](http://download.eclipse.org/releases/photon). Vaya a Ayuda> Instalar nuevo software> Agregar, complete el nombre para luego identificar fácilmente el sitio de actualización, por ejemplo, Photon Software Repository, y complete la ubicación con la url.

### Eclipse Marketplace

**Nota:** asegúrate de haber seguido la sección [Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualizaci.C3.B3n_predeterminado).

Para usar Eclipse Marketplace, instálelo primero: vaya a Ayuda> Instalar nuevo software> Cambiar al sitio de actualización predeterminado> Herramientas de propósito general> Cliente de Marketplace. Reinicie Eclipse y estará disponible en Ayuda > Eclipse Marketplace.

### Administrador de complementos

**Nota:** asegúrate de haber seguido la sección [Agregar el sitio de actualización predeterminado](#Agregar_el_sitio_de_actualizaci.C3.B3n_predeterminado).

Utilice el administrador de complementos de Eclipse para descargar e instalar complementos desde sus repositorios originales: en este caso debe encontrar el repositorio necesario en el sitio web del complemento, luego vaya a *Ayuda> Instalar nuevo software...*, ingrese el repositorio en el campo *Trabajar con* , seleccione el complemento para instalar de la lista a continuación y siga las instrucciones.

**Nota:**

*   Si instala complementos con el administrador de complementos de Eclipse, se le recomienda iniciar Eclipse como root: de esta manera los complementos se instalarán en `/usr/lib/eclipse/plugins/`; si los instaló como usuario normal, se almacenarán en una carpeta de versión dependiente dentro de `~/.eclipse/`, y, después de actualizar Eclipse, no serían reconocidos por más tiempo.
*   No use Eclipse como root para su trabajo diario.

#### Actualizaciones a través del administrador de complementos

Ejecute Eclipse y seleccione *Ayuda> Buscar actualizaciones* . Si los ha instalado como root como se recomienda en la sección anterior, debe ejecutar Eclipse como root.

Para que los complementos se actualicen, debe verificar que sus repositorios de actualización estén habilitados en *Ventana> Preferencias> Instalar / Actualizar> Sitios de software disponibles* : puede encontrar los repositorios de cada plugin en el sitio web del proyecto respectivo. Para agregar, editar, eliminar ... los repositorios solo usan los botones a la derecha del panel *Sitios de software disponibles* . Para Eclipse 4.5 (Marte), verifique que haya habilitado este repositorio:

```
[http://download.eclipse.org/releases/mars](http://download.eclipse.org/releases/mars)

```

Para recibir notificaciones de actualización, vaya a *Ventana> Preferencias> Instalar / Actualizar> Actualizaciones automáticas* . Si desea recibir notificaciones de plugins instalados como root, se debe ejecutar Eclipse como root, vaya a *Ventana> Preferencias> Instalar / Actualizar> Sitios disponibles sobre software* , seleccionar los repositorios relacionados con los plugins instalados y *Exportar' ', luego ejecutar Eclipse como usuario normal e "Importarlos" en el mismo panel.*

### List of plugins

*   **AVR** — AVR microcontroller plugin.

	[http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) || [eclipse-avr](https://aur.archlinux.org/packages/eclipse-avr/)

*   **Aptana** — HTML5/CSS3/JavaScript/Ruby/Rails/PHP/Pydev/Django support. Also available as standalone application.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **IvyDE** — IvyDE dependency Manager.

	[https://ant.apache.org/ivy/ivyde/](https://ant.apache.org/ivy/ivyde/) || [eclipse-ivyde](https://aur.archlinux.org/packages/eclipse-ivyde/)

*   **Markdown** — Markdown editor plugin for Eclipse.

	[http://www.winterwell.com/software/markdown-editor.php](http://www.winterwell.com/software/markdown-editor.php) || [eclipse-markdown](https://aur.archlinux.org/packages/eclipse-markdown/)

*   **PyDev** — [Python](/index.php/Python "Python") support.

	[http://pydev.org/](http://pydev.org/) || [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

*   **Subclipse** — [Subversion](/index.php/Subversion "Subversion") support.

	[https://github.com/subclipse/subclipse](https://github.com/subclipse/subclipse) || [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)

*   **Subversive** — Alternative Subversion support.

	[https://www.eclipse.org/subversive/](https://www.eclipse.org/subversive/) || [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

*   **TestNG** — TestNG support.

	[http://testng.org/doc/eclipse.html](http://testng.org/doc/eclipse.html) || [eclipse-testng](https://aur.archlinux.org/packages/eclipse-testng/)

*   **TeXlipse** — [LaTeX](/index.php/LaTeX "LaTeX") support.

	[http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/) || [eclipse-texlipse](https://aur.archlinux.org/packages/eclipse-texlipse/)

*   **Checkstyle** — Eclipse Checkstyle support.

	[http://eclipse-cs.sourceforge.net/](http://eclipse-cs.sourceforge.net/) || [eclipse-checkstyle](https://aur.archlinux.org/packages/eclipse-checkstyle/)

## Enable javadoc integration

Want to see API entries when hovering the mouse pointer over standard Java methods?

### Online version

If you have constant Internet access on your machine, you can use the on-line documentation:

1.  Go to *Window > Preferences*, then go to *Java > Installed JREs*.
2.  There should be one named "java" with the type "Standard VM". Select this and click *Edit*.
3.  Select the `/opt/java/jre/lib/rt.jar` item under "JRE system libraries:", then click *Javadoc Location...*.
4.  Enter "[https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)" in the "Javadoc location path:" text field.

### Offline version

You can store the documentation locally by installing the [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) package. Eclipse may be able to find the javadocs automatically. If that does not work, set Javadoc location for rt.jar to `file:/usr/share/doc/java8-openjdk/api`.

## Troubleshooting

### Ctrl+X closes Eclipse

Part of [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=318177) bug. Just look in `~/workspace/.metadata/.plugins/org.eclipse.e4.workbench/workbench.xmi` and delete the wrong `Ctrl+X` combination. Usually it is the first one.

### Dark theme

Eclipse supplies a Dark theme which can be enabled in Window > Preferences > General > Appearance and selecting the 'Dark' theme.

The dark theme uses its own colours rather than the GTK theme colours, if you prefer it to fully respect GTK colour settings, then remove or move to backup sub folder all of the .css files from `/usr/share/eclipse/plugins/org.eclipse.ui.themes_1.0.0.xxxx/css/`.

### Change Default Window Title Font Size

You cannot change the window title font size using the Eclipse preferences, you must edit the actual theme .css files. Note, that you will have to redo this when you upgrade eclipse. They are located under

```
/usr/share/eclipse/plugins/org.eclipse.platform_4.3.<your version number>/css

```

Open the appropriate file with your text editor, ie e4_default_gtk.css if you are using the "GTK theme". Search for .MPartStack, and change the font-size to your desired size

```
.MPartStack {
       font-size: 9;
       swt-simple: false;
       swt-mru-visible: false;
}

```

### Disable GTK+ 3

When the SWT GTK+ 3 UI is buggy and sometimes unusable, You can try to disable the use of GTK+ 3 with the SWT_GTK3=0 [environment variable](/index.php/Environment_variable "Environment variable") when you start eclipse:

```
SWT_GTK3=0 eclipse

```

Another option to achieve the same effect is to add the following to `/usr/lib/eclipse/eclipse.ini`.

```
--launcher.GTK_version
2

```

Those two lines must be added **before**:

```
--launcher.appendVmargs

```

### Freshplayerplugin

Eclipse is not compatible with [freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/). See [https://github.com/i-rinat/freshplayerplugin/issues/298](https://github.com/i-rinat/freshplayerplugin/issues/298).

### Eclipse 4.6 may not open the marketplace properly

See [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=497729) bug. You can take following two steps to fix it:

```
eclipse -consoleLog -application org.eclipse.equinox.p2.director -uninstallIU org.apache.httpcomponents.httpclient/4.3.6.v201411290715
cd /usr/lib/eclipse/ && sudo rm plugins/org.apache.httpcomponents.httpclient_4.3.6.v201411290715.jar

```

### Show in System Explorer does not work

See [this](http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.platform.doc.user%2Freference%2Fref-9.htm&cp=0_4_1_52) guide. Go to **Window** > **Preferences** > **General** > **Workspace** and change the command launching system explorer. As Xfce user you may like to change it to `thunar ${selected_resource_uri}` to open the selected folder with thunar.

### Display issues under Wayland

When running Eclipse on Wayland, you may encounter rendering issues such as slow response time to mouse events or chopped dialog windows (Bug report [[1]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=483545)). A possible workaround for this issue is to force Eclipse to run under XWayland.

With the superuser, open the file `/usr/bin/eclipse` and append this line before the `exec` line :

```
   export GDK_BACKEND=x11

```

This will force the execution of Eclipse on XWayland.

## See also

*   [How to use Subversion with Eclipse](https://www.ibm.com/developerworks/library/os-ecl-subversion/)
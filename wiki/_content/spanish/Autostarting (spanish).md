Este artículo trata sobre los diversos métodos para lanzar scripts o aplicaciones automáticamente cuando algún evento especial se produce, como puede ser el inicio del sistema o apagado, inicio o cierre de una sesión de shell y así sucesivamente.

## Contents

*   [1 Demonios](#Demonios)
    *   [1.1 Systemd](#Systemd)
    *   [1.2 Runit](#Runit)
*   [2 Shell](#Shell)
    *   [2.1 /etc/profile](#.2Fetc.2Fprofile)
*   [3 Gráfica](#Gr.C3.A1fica)
    *   [3.1 Inicio de sesión de X](#Inicio_de_sesi.C3.B3n_de_X)
    *   [3.2 Entradas de Desktop](#Entradas_de_Desktop)
    *   [3.3 GNOME, KDE, Xfce](#GNOME.2C_KDE.2C_Xfce)
    *   [3.4 LXDE](#LXDE)
    *   [3.5 Fluxbox](#Fluxbox)
    *   [3.6 Openbox](#Openbox)

## Demonios

Se pueden comenzar fácilmente los scripts o aplicaciones como demonios, consulte [Demonios](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)").

### Systemd

*systemd* es un reemplazo para *initscripts* que permite procesos de arranque más rápidos al simultanear el inicio de los servicios. Los servicios que se inician por *systemd* se encuentran en las subcarpetas de `/etc/systemd/system/`. Los servicios se pueden habilitar mediante la orden `systemctl`. Para obtener más información acerca de *systemd* y cómo escribir scripts autostarts para él, consulte el artículo sobre [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

### Runit

*runit* es un reemplazo maduro para *initscripts*, que ofrece supervisión de procesos, puesta en marcha en paralelo, árboles de servicios por cada usuario, manipulación detallada de los cgroup, sistema de dependencias flexible, y tiempos de arranque no penalizados por dbus. Los servicios de nivel-root son enlaces simbólicos en `/service` cuyos directorios de servicio reales están en `/etc/sv`. Consulte el artículo sobre [Runit](/index.php/Runit "Runit") para obtener más información.

## Shell

Para los programas de inicio automático en la consola o en el momento de inicio de sesión, puede utilizar la shell para iniciar archivos/directorios. Lea la documentación de su shell, o los artículos correspondientes de ArchWiki, por ejemplo [Bash#Configuration file sourcing order at startup](/index.php/Bash#Configuration_file_sourcing_order_at_startup "Bash") o [Zsh#Autostarting applications](/index.php/Zsh#Autostarting_applications "Zsh").

Véase también [Wikipedia:Unix shell#Configuration files for shells](https://en.wikipedia.org/wiki/Unix_shell#Configuration_files_for_shells "wikipedia:Unix shell").

### /etc/profile

`/etc/profile` provee a todas las shells compatibles con Bourne al iniciar sesión: dicho archivo establece un entorno al inicio de sesión y la configuración específica de aplicaciones para cualquier scripts leible de `/etc/profile.d/*.sh`.

## Gráfica

Se pueden iniciar programas automáticamente al abrir su [Gestor de Ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") o [Entorno de Escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)").

### Inicio de sesión de X

Consulte [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") y [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)").

### Entradas de Desktop

Las siguientes carpetas contienen archivos `*.desktop`, que se ejecutan cada vez que se inicia una sesión de X, y que determina qué programas se cargan y para qué entorno de escritorio:

*   `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` por defecto)
*   `/usr/share/gnome/autostart/` (solo para GNOME)
*   `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` por defecto)

Los usuarios pueden sobrescribir los archivos `*.desktop` que afectan a todo el sistema copiandolos en la carpeta `~/.config/autostart/` del usuario en cuestión.

Para obtener una explicación de la norma sobre los archivos desktop consulte [Desktop Entry Specification](http://standards.freedesktop.org/desktop-entry-spec/latest/). Para una descripción más específica de los directorios utilizados, [Desktop Application Autostart Specification](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html). Tenga en cuenta que este método solo es compatible con los entornos de escritorio compilados en XDG.

### GNOME, KDE, Xfce

[GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE") y [Xfce](/index.php/Xfce "Xfce"), todos ellos han creado una interfaz gráfica de usuario para la configuración del inicio automático de aplicaciones, consulte los artículos respectivos.

### LXDE

Véase [LXDE#Autostart programs](/index.php/LXDE#Autostart_programs "LXDE").

### Fluxbox

Véase [Fluxbox#Autostarting Applications](/index.php/Fluxbox#Autostarting_Applications "Fluxbox").

### Openbox

Véase [Openbox#Autostart](/index.php/Openbox#Autostart "Openbox").
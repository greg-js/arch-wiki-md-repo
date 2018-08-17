Artículos relacionados

*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Thunar (Español)](/index.php/Thunar_(Espa%C3%B1ol) "Thunar (Español)")
*   [LXDE (Español)](/index.php/LXDE_(Espa%C3%B1ol) "LXDE (Español)")
*   [GNOME (Español)](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)")

De Xfce - [Acerca de](http://www.xfce.org/about):

*Xfce encarna la filosofía tradicional UNIX de modularidad y reutilización. Se compone de una serie de componentes que proporcionan toda la funcionalidad que se puede esperar de un moderno entorno de escritorio. Se empaquetan por separado y puede escogerse entre los paquetes disponibles para crear elentorno de trabajo personal óptimo.*

## Contents

*   [1 ¿Qué es Xfce?](#.C2.BFQu.C3.A9_es_Xfce.3F)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Iniciando Xfce](#Iniciando_Xfce)
    *   [3.1 Automaticámente al Inicio](#Automatic.C3.A1mente_al_Inicio)
    *   [3.2 Manualmente](#Manualmente)
    *   [3.3 Apagado, Reinicio y Automontaje en Xfce](#Apagado.2C_Reinicio_y_Automontaje_en_Xfce)
        *   [3.3.1 Apagado y Reinicio desde el menú usando Systemd](#Apagado_y_Reinicio_desde_el_men.C3.BA_usando_Systemd)
*   [4 Trucos y Consejos](#Trucos_y_Consejos)
    *   [4.1 Configuración mediante Xfconf](#Configuraci.C3.B3n_mediante_Xfconf)
    *   [4.2 Panel](#Panel)
        *   [4.2.1 Remplazando el applet de menú por defecto](#Remplazando_el_applet_de_men.C3.BA_por_defecto)
        *   [4.2.2 Cómo remover elementos del Menú del Sistema](#C.C3.B3mo_remover_elementos_del_Men.C3.BA_del_Sistema)
            *   [4.2.2.1 Método 1](#M.C3.A9todo_1)
            *   [4.2.2.2 Método 2](#M.C3.A9todo_2)
            *   [4.2.2.3 Método 3](#M.C3.A9todo_3)
            *   [4.2.2.4 Método 4](#M.C3.A9todo_4)

## ¿Qué es Xfce?

Xfce es un entorno de escritorio al igual que [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") o [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") . Contiene una serie de aplicaciones asi como administrador de archivos, administrador de ventanas, paneles, etc. Xfce fué escrito usando las herramientas GTK2 y contiene sus propios entornos de desarrollo (daemons, librerias, etc), de forma similar a otros entornos de escritorio.

*   Mas ligero que otros Entornos de escritorio (GNOME, KDE)
*   Su método de configuración es totalmente mediante GUI, Xfce no trata de esconder nada al usuario.
*   Xfwm viene provisto con un compositor que le permite verdadera transparencia ademas de todos los beneficios de la aceleración GPU
*   Trabaja Exelente en multipes monitores.

## Instalación

Antes de Empezar, asegurate que haz instalado y configurado correctamante el [Servidor X](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)").

**Note:** Xfce algo modular. esto significa que no tienes que instalar o usar todas sus partes, puedes elegir solamente aquellos elementos que deseas usar.

El sistema Xfce básico puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") mediante un grupo de paquetes contenidos en [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/), disponible en los [Repositorios Oficiales](/index.php/Official_repositories "Official repositories").

Pacman te preguntará que paquetes deseas instalar, pero probablemente es mejor instalarlos todos simplemente presionando `Enter`. Paquetes adicionales, como plugins para el panel, notificaciones y otras herramientas del sistema estan disponibles en el grupo de paquetes [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

**Sugerencia:** Instalar [Gamin](/index.php/Gamin_(Espa%C3%B1ol) "Gamin (Español)") (sucesor de [FAM](/index.php/FAM_(Espa%C3%B1ol) "FAM (Español)")) es altamente recomendado.

Si deseas usar que xfce4-mixer funcione con [Alsa](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)"), necesitas instalar [gstreamer0.10-base-plugins](https://aur.archlinux.org/packages/gstreamer0.10-base-plugins/). Para [OSS](/index.php/OSS "OSS") mira [mas abajo](#OSS).

## Iniciando Xfce

### Automaticámente al Inicio

Hay dos maneras de iniciar Xfce (de hecho, cualquier Entorno de Escritorio o Gestor de Ventanas) al inicio:

*   Ejecutar Xfce mediante un [Gestor de inicio](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)").
*   Ejecutar Xfce utilizando [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit), combinando [Inicio de sesión gráfica automatica](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)") y [Login automático en la consola virtual](/index.php/Automatic_login_to_virtual_console_(Espa%C3%B1ol) "Automatic login to virtual console (Español)").

### Manualmente

**Note:** Mira [xinitrc](/index.php/Xinitrc "Xinitrc") para detalles, como preservar la sesión logind (y/o consolekit).

y agrega la siguiente linea

```
exec startxfce4

```

Para iniciar Xfce ejecuta:

```
$ startxfce4

```

Un ejemplo:

 `~/.xinitrc` 
```
#!/bin/sh

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

exec startxfce4
```

**Note:** La manera correcta de iniciar Xfce es mediante el comando `startxfce4`, no utilices `xfce4-session` directamente, dado que ya esta contenido en `startxfce4`.

### Apagado, Reinicio y Automontaje en Xfce

Ver [Problemas Comunes#Permisos de sesión](/index.php/Problemas_Comunes#Permisos_de_sesi.C3.B3n "Problemas Comunes").

Si no tienes problemas Apagando y Reiniciando, pero no puedes auto-montar medios externos y discos duros, quizá necesites instalar el paquete [gvfs](https://www.archlinux.org/packages/?name=gvfs). Más información en la sección [Medios Extraibles](#Medios_Extraibles).

#### Apagado y Reinicio desde el menú usando Systemd

Si utilizas systemd en lugar de sysvinit, tratar de apagar o reiniciar desde el menú de xfce4 sólo terminará la sesión, instalando [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) corrige este comportamiento.

**Nota:**

El [Medio de instalación](https://archlinux.org/download/) más reciente, incluye [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) como parte del sistema core instalado. Sin embargo, Xfce4.10 ya no necesita dicho paquete para Reiniciar y Apagar correctamente.

## Trucos y Consejos

### Configuración mediante Xfconf

Xfconf es donde Xfce guarda las opciones de configuración y muchas de las configuraciones de Xfce pueden ser hechas mediante Xconf (de una ú otra manera). Hay varias maneras de modificar estos parámetros:

*   La manera mas obvia es ir a "Configuración" en el menú principal y seleccionar la categoría que deseemos. Como sea, no todas las opciones de configuración estan disponibles solamente ahí.
*   Una manera menos amigable pero mas general es ir a: `Configuración -> Editor de Configuración`, Donde puedes ver y modificar todas las opciones de configuración. Cualquier campo modificado tomará efecto inmediatamente. El Editor de Configuracipon también puede ser ejecutado desde la linea de comandos mediante `xfce4-settings-editor`.
*   La personalización puede ser hecha completamente mediante linea de comandos con el programa `xfconf-query`. Mira [La Documentación En Linea de Xfce](http://docs.xfce.org/xfce/xfconf/xfconf-query) para mas información y ejemplos.
*   Las configuraciones se guardan en archivos XML en `~/.config/xfce4/xfconf/xfce-perchannel-xml/` que pueden ser editados a mano, hecho de esta manera no tomarán efecto inmediatamente.
*   Para mas Información: [documentación Xfconf](http://docs.xfce.org/xfce/xfconf/start)

### Panel

#### Remplazando el applet de menú por defecto

El applet para panel (GNOME) "Ubuntu System Panel" tiene características similares a las encontradas en su equivalente KDE v4.2\. Puede ser agregado a un panel xfce4-panel usando el applet 'XfApplet', que permite usar applets GNOME en Xfce-panel.

Está disponible en [AUR](/index.php/Arch_User_Repository "Arch User Repository") como el paquete [usp2](https://aur.archlinux.org/packages/usp2/).

#### Cómo remover elementos del Menú del Sistema

##### Método 1

Con el editor de menús integrado, no es posible remover elementos del Menú del Sistema. Pero pueden ser ocultados de la siguiente manera:

1.  Abre una Terminal (Xfce menu > System > Terminal) luego ve a la carpeta `/usr/share/applications`: `$ cd /usr/share/applications` 
2.  Ésta carpeta está llena de archivos `.desktop`. Para ver la lista ingresa el comando: `$ ls` 
3.  Agrega `NoDisplay=true` al archive `.desktop`. Por ejemplo, si deseas ocultar Firefox, escribe en la terminal: `$ sudo sh -c 'echo "NoDisplay=true" >> firefox.desktop'` Éste comando añade el texto `NoDisplay=true` al final del archivo `.desktop`.

##### Método 2

Otro método es copiar todo el contenido de la carpeta applications global, hacia la carpeta applications local del usuario, y luego proceder a modificar y (o) desabilitar elementos .desktop no deseados. Esto tiene la ventaja de no ser afectado por actualizaciones, ya que los archivos en la carpeta `/usr/share/applications` son reemplazados cuando el paquete al que pertenecen es actualizado.

1.  En la terminal, copia todo de `/usr/share/applications` a `~/.local/share/applications/`: `$ cp /usr/share/applications/* ~/.local/share/applications/` 
2.  Por cada elemento que se desea ocultar del menú, agregar la opción `NoDisplay=true`: `$ echo "NoDisplay=true" >> ~/.local/share/applications/foo.desktop` 

También en posible editar la categoría de la aplicación, editando el archive `.desktop` con un editor de texto y modificando la línea `Categories=`.

##### Método 3

El tercer método es el **más limpio** y recemendado en la [wike de Xfce](http://wiki.xfce.org/howto/customize-menu).

Crea el archive `~/.config/menus/xfce-applications.menu` y copia la siguiente:

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
  "http://www.freedesktop.org/standards/menu-spec/1.0/menu.dtd">

<Menu>
    <Name>Xfce</Name>
    <MergeFile type="parent">/etc/xdg/menus/xfce-applications.menu</MergeFile>

    <Exclude>
        <Filename>xfce4-run.desktop</Filename>

        <Filename>exo-terminal-emulator.desktop</Filename>
        <Filename>exo-file-manager.desktop</Filename>
        <Filename>exo-mail-reader.desktop</Filename>
        <Filename>exo-web-browser.desktop</Filename>

        <Filename>xfce4-about.desktop</Filename>
        <Filename>xfhelp4.desktop</Filename>
    </Exclude>

    <Layout>
        <Merge type="all"/>
        <Separator/>

        <Menuname>Settings</Menuname>
        <Separator/>

        <Filename>xfce4-session-logout.desktop</Filename>
    </Layout>

</Menu>

```

La etiqueta `<MergeFile>` incluye el archivo del menú por defecto. Ésto es importante.

La etiqueta `<Exclude>` excluye aplicaciones que no deseamos que aparezcan en el menú. En el ejemplo se excluyen algunos accesos directos de Xfce, pero se puede excluir `firefox.desktop` o cuasquiet otra aplicación.

La etiqueta `<Layout>` define la disposición del menú. Las aplicaciones pueden ser organizadas on carpetas o como se desee. Para más detalles ver la mencionada wiki de Xfce.

##### Método 4

Alternativamente, la herramienta llamada [lxmed](http://lxmed.sourceforge.net/) puede ser usada. Lxmed es una herramienta con interfaz gráfica escrita en java para editar elementos de menú en LXDE, pero también funciona en Xfce4\. Lxmed está disponible en en paquete [lxmed](https://aur.archlinux.org/packages/lxmed/) de [AUR](/index.php/AUR "AUR").
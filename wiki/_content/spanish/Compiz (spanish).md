Compiz es un [Compositing Window manager](https://es.wikipedia.org/wiki/Ventana_(informática)). Al proveer su propio window manager, no puede ser usado simultáneamente con otros, tales como [Openbox](/index.php/Openbox "Openbox"), [Fluxbox](/index.php/Fluxbox "Fluxbox"), [Enlightenment](/index.php/Enlightenment "Enlightenment") - aquellos usuarios que quieran mantener su actual window manager y agregarle algunos efectos podrían probar con [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") en su lugar.

**Note:** En español es común traducir Window manager como administrador de ventanas, o manejador de ventanas, pero durante la traducción se prefirió dejarlo en ingles.

Compiz es el núcleo del proyecto Compiz-Fusion, el cual trabajó en añadir muchas funciones / plugins al WM (window manager) y ahora esta siendo fusionado de nuevo. Ambos proyectos están activos y sometidos a constante desarrollo. Para mas información, consulte el articulo [Compiz Fusion vs. Compiz](http://wiki.compiz-fusion.org/CompizFusionVsCompiz).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Instalación desde Community](#Instalaci.C3.B3n_desde_Community)
    *   [1.2 Lista de paquetes por grupo](#Lista_de_paquetes_por_grupo)
    *   [1.3 Chequeo de configuración](#Chequeo_de_configuraci.C3.B3n)
*   [2 Iniciando Compiz Fusion](#Iniciando_Compiz_Fusion)
    *   [2.1 Manual (con "fusion-icon")](#Manual_.28con_.22fusion-icon.22.29)
    *   [2.2 KDE](#KDE)
        *   [2.2.1 Manual (sin "fusion-icon")](#Manual_.28sin_.22fusion-icon.22.29)
        *   [2.2.2 Inicio automatico (con "fusion-icon")](#Inicio_automatico_.28con_.22fusion-icon.22.29)
        *   [2.2.3 Inicio automático (sin "fusion-icon")](#Inicio_autom.C3.A1tico_.28sin_.22fusion-icon.22.29)
            *   [2.2.3.1 Método 1 – Link para inicio automático](#M.C3.A9todo_1_.E2.80.93_Link_para_inicio_autom.C3.A1tico)
            *   [2.2.3.2 Método 2 - exportar KDEWM (anular KWIN)](#M.C3.A9todo_2_-_exportar_KDEWM_.28anular_KWIN.29)
            *   [2.2.3.3 Método 3 - Usar Configuración de sistema de KDE 4](#M.C3.A9todo_3_-_Usar_Configuraci.C3.B3n_de_sistema_de_KDE_4)
    *   [2.3 GNOME](#GNOME)
        *   [2.3.1 inicio automático (sin "fusion-icon")](#inicio_autom.C3.A1tico_.28sin_.22fusion-icon.22.29_2)
        *   [2.3.2 Inicio automático (sin "fusion-icon", Gnome anterior al 2.24)](#Inicio_autom.C3.A1tico_.28sin_.22fusion-icon.22.2C_Gnome_anterior_al_2.24.29)
        *   [2.3.3 Inicio automático (con "fusion-icon")](#Inicio_autom.C3.A1tico_.28con_.22fusion-icon.22.29)
    *   [2.4 Xfce](#Xfce)
        *   [2.4.1 Xfce inicio automático (sin "fusion-icon")](#Xfce_inicio_autom.C3.A1tico_.28sin_.22fusion-icon.22.29)
        *   [2.4.2 Xfce, inicio automático (con "fusion-icon")](#Xfce.2C_inicio_autom.C3.A1tico_.28con_.22fusion-icon.22.29)
            *   [2.4.2.1 Método 1:](#M.C3.A9todo_1:)
            *   [2.4.2.2 Método 2:](#M.C3.A9todo_2:)
    *   [2.5 LXDE](#LXDE)
        *   [2.5.1 Inicio automatico (sin "fusion-icon")](#Inicio_automatico_.28sin_.22fusion-icon.22.29)
        *   [2.5.2 Inicio automatico (con "fusion-icon")](#Inicio_automatico_.28con_.22fusion-icon.22.29_2)
    *   [2.6 Como WM independiente](#Como_WM_independiente)
        *   [2.6.1 Añadir un menú de raíz](#A.C3.B1adir_un_men.C3.BA_de_ra.C3.ADz)
*   [3 Varios](#Varios)
    *   [3.1 Usando compiz-manager](#Usando_compiz-manager)
    *   [3.2 Usando gtk-window-decorator](#Usando_gtk-window-decorator)
    *   [3.3 gconf: Configuraciones adicionales para Compiz](#gconf:_Configuraciones_adicionales_para_Compiz)
    *   [3.4 Atajos de teclado](#Atajos_de_teclado)
*   [4 Recursos adicionales](#Recursos_adicionales)

# Instalación

La instalación básica puede ser hecha usando los repositorios Community (ver más abajo).

La segunda forma es usando los paquetes mas recientes, git. Mirar [Compiz_Fusion_Git](/index.php?title=Compiz_Fusion_Git&action=edit&redlink=1 "Compiz Fusion Git (page does not exist)") para mas información.

## Instalación desde Community

Cerciórese de que el repositorio Community esta activado y ejecute este comando como root para instalar todo:

```
# pacman -S compiz-fusion 

```

Ejecute este si solo quiere paquetes basados en gtk instalados:

```
# pacman -S compiz-fusion-gtk 

```

o este si solo quiere paquetes basados en kde instalados:

```
# pacman -S compiz-fusion-kde 

```

Los usuarios que deseen seleccionar los paquetes individualmente pueden consultar la siguiente lista:

## Lista de paquetes por grupo

	Grupo completo de Compiz-Fusion

	ccsm, compiz-core, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-gconf, compizconfig-backend-kconfig, emerald, emerald-themes, fusion-icon

	Grupo KDE de Compiz-Fusion

	ccsm, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-kconfig, emerald, emerald-themes, fusion-icon

	Grupo GTK de Compiz-Fusion

	ccsm, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-gconf, emerald, emerald-themes, fusion-icon

	groupless / legacy (?)

	compiz-decorator-gtk, compiz-decorator-kde, compiz-manager

*   ccsm es la primer opción para un buen frontend para configurar compiz.
*   Emerald es el decorador de ventanas propio de compiz.
*   fusion-icon ofrece un tray icon (icono en el área de notificación) y una buena forma de iniciar compiz, iniciar ccsm y cambiar el WM / Window Decorator.
*   Se dice que compiz-manager trae mejores capacidades de manejo de sesiones (¡necesita confirmación!).
*   compiz-decorator-gtk y compiz-decorator-kde son alternativas a Emerald, en caso de preferir usar la configuración por defecto (también necesita confirmación).

## Chequeo de configuración

	Compatibilidad

	El script [compiz-check](http://forlong.blogage.de/entries/pages/Compiz-Check) ejecuta varias pruebas relacionadas a compiz y puede ayudar a descubrir problemas de hardware y configuración. Esta disponible desde [aur](https://aur.archlinux.org/packages.php?ID=17163).

	Backend

	Dependiendo de los paquetes que hayas instalado, puedes usar diferentes backend para administrar la configuración de compiz. Mientras que gconf/kconf deberían ser suficientes para Gnome/KDE, la configuración básica de archivo plano de respaldo debe ser tu opción si querés probar compiz en diferentes entornos sin perder las configuraciones en el medio del cambio o simplemente usar un entorno de escritorio diferente. Podes cambiar el backend usado con ccsm (“Preferencias=>Perfil & Backend=> Backend”).

	¡Activar plugins importantes!

	Antes de hacer cualquier otra cosa, puede que desee chequear si los plugins que proveen de comportamiento básico al window manager están activados o no tendrá posibilidad de arrastrar, escalar o cerrar ventanas ni bien compiz sea activado. Entre esos plugins están "Decoración de ventanas" en efectos y "Mover ventana" y "Cambiar de tamaño la ventana" en Administrador de ventanas. (ccsm puede ser usado para activar estos.)

# Iniciando Compiz Fusion

## Manual (con "fusion-icon")

Inicie el icono de notificación de Compiz Fusion:

```
$ fusion-icon 

```

Clic derecho en el icono en el panel e ir a 'select window manager'. Elegir "Compiz" si no estaba seleccionado.

Si esto falla puede iniciar Compiz usando los siguientes comandos:

```
$ fusion-icon 
$ emerald --replace 
$ compiz-manager 

```

Si quiere usar las decoraciones de ventana de compiz asegúrese de que tiene el plugin "Window Decoration" marcado en la configuración de compiz.

## KDE

### Manual (sin "fusion-icon")

Inicie compiz con el siguiente comando una vez terminada la instalación :

```
$ compiz --replace ccp & 

```

Iniciar el nuevo administrador de configuraciones:

```
$ ccsm & 

```

Seleccione todos los plugins que le gusten incluyendo “Decoración de ventanas”, agregue

```
$ kde-window-decorator --replace 

```

como comando en el plugin “Decoración de ventanas”

### Inicio automatico (con "fusion-icon")

Añada un enlace simbólico al lanzador fusion-icon en tu directorio de KDE de aplicaciones al inicio (generalmente localizado en ~/.kde/Autostart):

```
$ ln -s /usr/bin/fusion-icon ~/.kde/Autostart/fusion-icon 

```

En el siguiente inicio de KDE, este iniciará fusion-icon automáticamente.

### Inicio automático (sin "fusion-icon")

#### Método 1 – Link para inicio automático

*   Puede asegurarse de que Compiz Fusion siempre iniciará al iniciar sesión añadiendo un archivo .desktop al directorio de inicio automático de KDE. Cree el archivo *~/.kde/Autostart/compiz.desktop* con el siguiente contenidos:

```
[Desktop Entry] 
Encoding=UTF-8 
Exec=compiz --replace ccp 
StartupNotify=false 
Terminal=false 
Type=Application 
X-KDE-autostart-after=kdesktop 

```

*   Si quiere usar la aplicación opcional `fusion-icon`, solo ejecute *fusion-icon*. Si termina la sesión de manera normal con “fusion-icon” corriendo, KDE debería restaurar su sesión y lanzar *fusion-icon* la próxima ves que inicie sesión si la opción esta activada . Si no parece estar funcionando, asegúrese de tener la siguiente linea en *~/.kde/share/config/ksmserverrc*:

```
loginMode=restorePreviousLogout 

```

#### Método 2 - exportar KDEWM (anular KWIN)

Usando este método cargará Compiz-Fusion como el WM por defecto en lugar de KWin desde el inicio. Este método es más rápido que cargar Compiz-Fusion en el directorio ~ / .kde4/Autostart / (método 1), ya que primero evita la carga por defecto de KDE WM (KWin). Esta forma también detiene ese molesto parpadeo de la pantalla negra que puedes ver usando otros métodos (cuando kwin cambia a compiz en la pantalla de carga del escritorio de KDE).

Debe crear, como root, un script haciendo lo siguiente en la terminal. Esto le permitirá cargar compiz con los cambios porqué haciéndolo directamente vía `export KDEWM="compiz --replace ccp --sm-disable"` no parece funcionar.

```
$ echo "compiz --replace ccp --sm-disable &" > /usr/bin/compiz-fusion 

```

Si esto no funciona, instale el paquete "fusion-icon" y luego use esta linea en su lugar:

```
$ echo "fusion-icon &" > /usr/bin/compiz-fusion 

```

Asegúrese de que "/usr/bin/compiz-fusion" tiene permisos de ejecución (+x).

```
$ chmod a+x /usr/bin/compiz-fusion 

```

Edite su archivo ~/.bashrc y agregue lo siguiente, así KDE cargará compiz (vía el script que acaba de crear) en lugar de KWin.

```
$ export KDEWM="compiz-fusion" 

```

**Nota:** Si usa el directorio /usr/local/bin esto podría no funcionar. En ese caso deberá exportar el script con la ruta, es decir, `export KDEWM="/usr/local/bin/compiz-fusion"`.

**Nota:** La forma elegante para el método mencionado arriba es incluir:

```
KDEWM="compiz-fusion" 

```

en ~/.kde4/env/compiz.sh (local) o /usr/env/compiz.sh (en todo el sistema).

#### Método 3 - Usar Configuración de sistema de KDE 4

Diríjase a Preferencias del sistema --> Aplicaciones preferidas --> Gestor de ventanas --> Usar un gestor de ventanas diferente

Si necesita ejecutar compiz con opciones personalizadas seleccione "Compiz custom" (cuando se ejecuta fusion-icon de una terminal se puede ver la línea de comandos con la que se inició compiz). Cree un archivo "compiz-kde-launcher" en su directorio /usr/bin. Luego hágalo ejecutable: "chmod +x /usr/bin/compiz-kde-launcher". Aquí hay un ejemplo para el compiz-kde-launcher:

```
 #!/bin/bash 
 LIBGL_ALWAYS_INDIRECT=1 
 compiz --replace --sm-disable --ignore-desktop-hints ccp --indirect-rendering & 
 wait 

```

Asegúrese de que tiene el plugin "Window Decorations" activado. Dependiendo de los paquetes que haya descargado podrá elegir entre varios WD (window decorators/decoradores de ventana). Los recomendados para KDE son emerald y kde4-window-decorator. Emerald tiene la ventaja de que este funciona mejor con el manejo de las ventanas de compiz. Use "CompizConfig Settings Manager (ccsm)" para cambiar el decorador por defecto: Decorador de ventanas -> Comando: emerald --replace or kde4-window-decorator --replace.

Si no tiene decorador de ventana intente añadir las siguientes lineas al archivo "compiz-kde-launcher":

```
 sleep 1 
 kde4-window-decorator --replace& 
 # o si quiere usar Emerald (debe quitar el # y agregarlo en la primera linea) 
 # emerald --replace& 

```

* * *

## GNOME

### inicio automático (sin "fusion-icon")

**1)** Cree un archivo /usr/share/applications/compiz.desktop que contenga lo siguiente:

```
[Desktop Entry] 
Type=Application 
Encoding=UTF-8 
Name=Compiz 
Exec=compiz ccp 
NoDisplay=true 
# name of loadable control center module 
X-GNOME-WMSettingsModule=compiz 
# autostart phase 
X-GNOME-Autostart-Phase=WindowManager 
X-GNOME-Provides=windowmanager 
# name we put on the WM spec check window 
X-GNOME-WMName=Compiz 
# back compat only 
X-GnomeWMSettingsLibrary=compiz 

```

**Nota:** Si eso no funciona intente:

```
Exec=compiz ccp --indirect-rendering 

```

o

```
Exec=compiz --replace --sm-disable --ignore-desktop-hints ccp --indirect-rendering 

```

En lugar de:

```
Exec=compiz ccp 

```

**2)** Establezca algunos parámetros de Gconf usando el comando gconftool-2 en una terminal:

```
gconftool-2 --set -t string /desktop/gnome/session/required_components/windowmanager compiz 
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/current /usr/bin/compiz 
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/default /usr/bin/compiz 

```

### Inicio automático (sin "fusion-icon", Gnome anterior al 2.24)

Esta es una forma que trabaja si usa GDM (y supongo que KDM también).

Cree un archivo llamado /usr/local/bin/compiz-start-boot con los siguientes contenidos:

```
#!/bin/bash 
export WINDOW_MANAGER="compiz ccp" 
exec gnome-session 

```

y hágalo ejecutable (`chmod +x`). Luego cree el archivo /etc/X11/sessions/Compiz.desktop conteniendo lo siguiente:

```
[Desktop Entry] 
Version=1.0 
Encoding=UTF-8 
Name=Compiz en GNOME 
Exec=/usr/local/bin/compiz-start-boot 
Icon= 
Type=Application 

```

Seleccione Compiz en Gnome como su sesión y listo.

### Inicio automático (con "fusion-icon")

Para iniciar Compiz Fusion automáticamente cuando inicie sesión vaya a Sistema > Preferencias > Aplicaciones al Inicio. En la pestaña Programas al inicio, haga clic en el botón Añadir.

Ahora vera el dialogo Añadir programa al inicio. Complete lo de la siguiente manera:

Nombre:

```
Compiz Fusion 

```

Comando:

```
fusion-icon 

```

Comentario: (Escribe cualquier cosa o dejalo en blanco.)

Cuando termine haga clic en Añadir. Ahora debería ver su programa en la lista en la pestaña Programas al inicio. Debe estar marcado para que este habilitado. Lo puede desmarcar para quitar compiz del inicio y cambiar a Metacity.

También puede que necesite usar el comando gconftool-2 en una terminal para establecer el siguiente parámetro, de lo contrario fusion-icon puede no cargar el decorador de ventanas.

```
gconftool-2 --type bool --set /apps/metacity/general/compositing_manager false 

```

## Xfce

### Xfce inicio automático (sin "fusion-icon")

Iniciando compiz con el administrador de sesiones de XFCE. Esto iniciará compiz directamente sin cargar Xfwm.

Esto cambio en los archivos de configuración xml solo funciona en versiones de Xfce a partir de la 4.2

Para instalar el administrador de sesión, ejecute lo siguiente como root:

```
# pacman -S xfce4-session 

```

Ahora tiene que configurar la sesión default/failsafe de XFCE.

Edite el siguiente archivo:

```
# nano ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml 

```

O para hacer el cambio para todos los usuarios de XFCE (Requiere acceso de super usuario -root-)

```
# nano /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml 

```

Reemplace el comando de inicio xfwm:

```
 <property name="Client0_Command" type="array"> 
   <value type="string" value="xfwm4"/> 
 </property> 

```

con el siguiente:

```
 <property name="Client0_Command" type="array"> 
   <value type="string" value="compiz"/> 
   <value type="string" value="ccp"/> 
 </property> 

```

Para evitar que la sesión predeterminada sea sobrescrita puede agregar esto::

```
 <property name="general" type="empty"> 
   ... 
   ... 
   <property name="SaveOnExit" type="bool" value="false"/> 
 </property> 

```

Para quitar las sesiones existentes ejecute:

```
rm -r ~/.cache/sessions

```

### Xfce, inicio automático (con "fusion-icon")

#### Método 1:

Esto cargará Xfwm primero luego reemplacelo por Compiz.

Abra el administrador de configuraciones de XFCE > Sesiones > Inicio. Haga clic en la pestaña inicio automático de aplicaciones.

Agregue

```
  (Name:) Compiz Fusion 

```

```
  (Command:) fusion-icon 

```

#### Método 2:

Edite el siguiente archivo (las configuraciones en este archivo se usan por preferencia)

```
nano ~/.config/xfce4-session/xfce4-session.rc 

```

O para hacer el cambio para todos los usuarios de XFCE(se requiere acceso de root)

```
# nano /etc/xdg/xfce4-session/xfce4-session.rc 

```

Agregar lo siguiente:

```
[Failsafe Session] 
Client0_Command=fusion-icon 

```

Comment out Client0_Command=xfwm4 if it exists.

Esto hará que XFCE cargue compiz en lugar de Xfwm cuando el usuario no tenga configurada la sesión.

Para prevenir que la sesión por defecto sea sobrescrita se puede agregar:

```
[General] 
AutoSave=false 
SaveOnExit=false 

```

Para remover las sesiones existentes:

```
rm -r ~/.cache/sessions 

```

## LXDE

Openbox, el gestor de ventanas por defecto de LXDE, pueden ser reemplazados fácilmente por otros gestores de ventanas como fvwm, icewm, DWM, metacity, compiz ... etc

### Inicio automatico (sin "fusion-icon")

LXDE intentará usar gestor de ventanas desde el archivo de configuración de usuario lxsession /.config/lxsession/LXDE/desktop.conf. Si no existe, entonces se intenta utilizar el archivo de configuración global /etc/xdg/lxsession/LXDE/desktop.conf.

Reemplace el comando openbox-lxde con el gestor de ventanas de su elección:

 `~/.config/lxsession/LXDE/desktop.conf` 
```
[Session]
window_manager=openbox-lxde
```

Por compiz:

 `~/.config/lxsession/LXDE/desktop.conf` 
```
[Session]
window_manager=compiz ccp --indirect-rendering
```

### Inicio automatico (con "fusion-icon")

Copia el lanzador de "fusion-icon" a la carpeta de programas de inicio generalmente ~/.config/autostart.

```
$ cp /usr/bin/fusion-icon ~/.config/autostart

```

## Como WM independiente

Un método simple, usando un sencillo script nombrado **start-fusion.sh**:

```
#!/bin/sh 
# agregue mas aplicaciones aquí de ser necesario o iniciar otro panel, área de notificación como pypanel, bmpanel, stalonetray 
xfce4-panel& 
fusion-icon 

```

Hágalo ejecutable y agréguelo a ~/.xinitrc, de esta manera:

```
exec start-fusion.sh 

```

Siéntase libre de usar otro panel, área de notificación, o comenzar un montón de aplicaciones con su sesión. Mire este[hilo en el foro](https://bbs.archlinux.org/viewtopic.php?id=51282) para mas info.

### Añadir un menú de raíz

Para añadir un menú raíz similar al de Openbox, Fluxbox, Blackbox etc. debe instalar el paquete compiz-deskmenu desde [AUR](/index.php/AUR "AUR"). Después de un reinicio de Compiz-Fusion, debería ser capaz de hacer clic en medio de su escritorio para abrir el menú.

Si esto no funciona automáticamente, inicie el CCSM, y en la pestaña Comandos, dentro del menú de configuración General, asegúrese de que hay un comando para lanzar Compiz-Deskmenu, y que la combinación de teclas correspondiente sea Control+Space.

Si sigue sin funcionar, ingrese al menú Viewport Switcher, y cambie "Plugin for initiate action" a core (NOTA: para versiones 0.8.2+ es 'commands' en lugar de 'core'), y "Action name for initiate" a run_command0_key.

# Varios

## Usando compiz-manager

Para usar compiz-manager, necesita instalarlo desde community:

```
pacman -S compiz-manager 

```

Compiz-manager, que ahora esta instalado en /usr/bin/compiz-manager, es un contenedor simple para Compiz y todas sus opciones. Pro ejemplo, puede ejecutar:

```
compiz-manager 

```

y ver que devuelve la consola. Lo puede usar en todos los scripts que inician compiz. ¡Muy simple!

## Usando gtk-window-decorator

Para utilizar gtk-window-decorator, instale el paquete *compiz-decorator-gtk* y seleccione "GTK Window Decorator" en lugar de "Emerald" como su window decorator en fusion-icon o cualquier otro programa que este usando para configurar compiz.

## gconf: Configuraciones adicionales para Compiz

Para lograr resultados más satisfactorios con Compiz, puede ajustar su configuración con gconf-editor:

```
 gconf-editor & 

```

Note que compiz-core no esta construido con soporte para gconf; Ahora esta en compiz-decorator-gtk. Entonces, necesita instalar este si quiere usar gconf-editor para configurar compiz. La configuración de compiz esta en **apps** > **compiz** > **general** > **allscreens** > **options**

Active plugins es donde especifica los plugins que desee usar, simplemente edite la llave y agregue en value(se refiere a **apps** > **compiz** > **plugins**). Los plugins que encontré útiles son screenshot, png, fade, minimize. Por favor, no quite los que se encuentran activos por defecto.

## Atajos de teclado

Los atajos de teclado por defecto para los plugins (!plugins tienen que estar activados!)

*   Cambiar ventanas = Alt + Tab
*   Cambiar escritorios con el cubo = Ctrl + Alt + flecha derecha/izquierda
*   Mover la ventana = Alt + clic con botón izquierdo
*   Redimensionar la ventana = Alt + clic con botón derecho

Una lista mas detallada puede ser encontrada en [CommonKeyboardShortcuts](http://wiki.compiz-fusion.org/CommonKeyboardShortcuts) en la wiki de Compiz o puede echar un vistazo a su configuración en ccsm.

# Recursos adicionales

*   [Compiz Troubleshooting](/index.php/Compiz_Troubleshooting "Compiz Troubleshooting") -- sub article
*   [Compiz configuration](/index.php/Compiz_configuration "Compiz configuration") -- sub article
*   [Compiz Website](http://compiz.org) -- including wiki and forum
*   [Composite](/index.php/Composite "Composite") -- A Xorg extension required by composite managers
*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") -- A simple composite manager capable of drop shadows and primitive transparency

*   Wikipedia: [Compositing Window Managers](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")
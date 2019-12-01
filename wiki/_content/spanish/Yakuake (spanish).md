**Estado de la traducción**
Este artículo es una traducción de [Yakuake](/index.php/Yakuake "Yakuake"), revisada por última vez el **2019-11-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Yakuake&diff=0&oldid=590474) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [KDE](/index.php/KDE "KDE")

[Yakuake](https://www.kde.org/applications/system/yakuake/) es un terminal desplegable desde la parte superior de la pantalla para [KDE](/index.php/KDE "KDE"), al estilo de [Guake](/index.php/Guake "Guake") para [GNOME](/index.php/GNOME "GNOME"), [Tilda](/index.php/Tilda "Tilda") o el terminal utilizado en Quake.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Realizar script para Yakuake](#Realizar_script_para_Yakuake)
    *   [3.1 dbus-send en lugar de qdbus](#dbus-send_en_lugar_de_qdbus)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [yakuake](https://www.archlinux.org/packages/?name=yakuake).

## Utilización

Una vez instalado, puede iniciar Yakuake desde un terminal con:

```
$ yakuake

```

Después de que Yakuake se haya iniciado, puede hacer clic en configurar Yakuake sobre el botón *Abrir del menú* (botón central situado en la parte inferior derecha de la interfaz) y seleccionar *Configurar los accesos rápidos* para cambiar la tecla de acceso rápido para abrir/retraer el terminal automáticamente, que está configurado por defecto en F12.

## Realizar script para Yakuake

Al igual que [Guake](/index.php/Guake "Guake"), Yakuake permite controlarse en tiempo de ejecución enviando los mensajes del servicio [D-Bus](/index.php/D-Bus "D-Bus"). Por lo tanto, se puede utilizar para iniciar Yakuake en una sesión definida por el usuario. Puede crear pestañas, asignarles nombres y también solicitar ejecutar cualquier orden específica en cualquier pestaña abierta o simplemente mostrar/ocultar la ventana de Yakuake, manualmente en un terminal o creando un script personalizado para ello.

Ejemplo de tal script se da a continuación. Esto incluye abrir pestañas, cambiar el nombre de pestañas, dividir intérpretes de órdenes y ejecutar órdenes.

```
#!/bin/bash
# Inicia Yakuake según las preferencias del usuario. Información basada en  [http://forums.gentoo.org/viewtopic-t-873915-start-0.html](http://forums.gentoo.org/viewtopic-t-873915-start-0.html)
# Agrega sesiones del sitio web previo roto, según esto: [http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/](http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/)

# Esta línea es necesaria en caso de que Yakuake no acepte entradas fcitx.
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot &

# Le da a Yakuake un par de segundos antes de enviar órdenes del servicio dbus
sleep 2

# Inicia htop en la pestaña y la divide en el terminal del usuario y ejecute iotop
TERMINAL_ID_0=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId 0)
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 0 "user"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "htop"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_0}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "iotop

# Inicia sesiones root divididas (solicitud de contraseña) arriba y abajo
SESSION_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_1})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 1 "root"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "su"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalTopBottom ${TERMINAL_ID_1}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 3 "su"

# Inicia irssi en su propia pestaña. 
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 2 "irssi"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 4 "ssh home -t 'tmux attach -t irssi; bash -l'" 

# Inicia intérpretes de órdenes de ssh divididas en su propia pestaña.
SESSION_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_2})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 3 "work server"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 5 "ssh work"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_2}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 6 "ssh work" 

```

### dbus-send en lugar de qdbus

Puede reemplazar *qdbus* incluido con [Qt](/index.php/Qt "Qt") con el más común *dbus-send*. Por ejemplo, para mostrar/ocultar Yakuake:

```
$ dbus-send --type=method_call --dest=org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState

```

## Véase también

*   [Yakuake scripting on coderwall.com](https://coderwall.com/p/kq9ghg/yakuake-scripting)
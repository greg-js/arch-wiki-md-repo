Artículos relacionados

*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Start X at Login (Español)](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)")

El [gestor de pantalla](https://en.wikipedia.org/wiki/es:X_Display_Manager y de [entornos de escritorios](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"). Estos gestores suelen proporcionar un cierto grado de personalización y disponibilidad de temas con cada uno.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Lista de gestores de pantalla](#Lista_de_gestores_de_pantalla)
    *   [1.1 De consola](#De_consola)
    *   [1.2 Gráficos](#Gráficos)
*   [2 Cargar el gestor de inicio de sesión](#Cargar_el_gestor_de_inicio_de_sesión)
    *   [2.1 Utilizar systemd-logind](#Utilizar_systemd-logind)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Lista de sesión](#Lista_de_sesión)
    *   [3.2 Iniciar automáticamente](#Iniciar_automáticamente)
*   [4 Problemas conocidos](#Problemas_conocidos)
    *   [4.1 Incompatibilidad con systemd](#Incompatibilidad_con_systemd)

## Lista de gestores de pantalla

### De consola

*   **[CDM](/index.php/CDM "CDM") (Console Display Manager)** — Gestor de pantallas ultraminimalista, pero con todas las funciones de un administrador de inicio de sesión, escrito en bash

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

### Gráficos

*   **[GDM](/index.php/GDM "GDM")** — Gestor de inicio de sesión de [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)")

	[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **KDM** — Gestor de inicio de sesión de [KDE](/index.php/KDE "KDE")4

	[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **[LightDM](/index.php/LightDM "LightDM")** — Gestor de pantalla multiescritorio, que puede utilizar varios frontends escritos en cualquier conjunto de herramientas

	[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — Gestor de inicio de sesión de [LXDE](/index.php/LXDE "LXDE"). Puede usarse independientemente del entorno de escritorio LXDE.

	[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — Gestor de inicio de sesión de MDM, fork de GDM 2

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   **[Qingy](/index.php/Qingy "Qingy")** — Acceso gráfico para el inicio de sesión independiente para X Windows, altamente configurable y muy ligero (utiliza DirectFB)

	[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)

*   **SDDM** — Gestor de pantalla basado en QML

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[SLiM](/index.php/SLiM "SLiM") (Simple Login Manager)** — Solución de acceso gráfico para el inicio de sesión elegante y ligero

	[http://slim.berlios.de/](http://slim.berlios.de/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X Display Manager con soporte para XDMCP, host chooser.

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Cargar el gestor de inicio de sesión

Para [activar](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") el acceso gráfico, ejecute el demonio del <a class="mw-selflink selflink">gestor de pantallas</a> preferido (por ejemplo, [SDDM](/index.php/SDDM "SDDM")).

```
# systemctl enable sddm

```

Esto debería funcionar sin configuración adicional. En su defecto, quizás tenga un *default.target* establecido manualmente o procedente de una instalación antigua

 `$ ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Bastaría con eliminar el enlace simbólico y *systemd* utilizará su *default.target* existente (es decir, *graphical.target*).

```
# rm /etc/systemd/system/default.target

```

Después de activar sddm debe mostrarse un enláce simbólico de «display-manager.service» establecido en /etc/systemd/system/

 `$ ls -l /etc/systemd/system/display-manager.service`  `/etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/sddm.service` 

### Utilizar systemd-logind

Con el fin de comprobar el estado de la sesión del usuario, puede utilizar `loginctl`. Todas las acciones [polkit](/index.php/Polkit "Polkit"), como suspender el sistema o montar unidades externas, funcionarán sin configuración adicional.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Consejos y trucos

### Lista de sesión

Muchos gestores de pantalla leen las sesiones disponibles en el directorio `/usr/share/xsessions/`. Este contiene [archivos de entrada de escritorio](https://specifications.freedesktop.org/desktop-entry-spec/latest/) estándar para cada gestor de pantalla/gestor de ventanas.

Para añadir/eliminar entradas en la lista de sesión del gestor de pantalla, cree/quite los archivos .desktop de `/usr/share/xsessions/` según desee. Un archivo .desktop típico se vería así:

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

### Iniciar automáticamente

La mayor parte de las fuentes de los gestores de pantallas son `/etc/xprofile`, `~/.xprofile` y `/etc/X11/xinit/xinitrc.d/`. Para más información, consulte [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)").

## Problemas conocidos

### Incompatibilidad con systemd

*Gestores de inicio de sesión afectados: MDM, SDDM, [SLiM](/index.php/SLiM "SLiM")*

Algunos gestores de pantallas no son totalmente compatibles con systemd, porque utilizan los procesos de sesión de PAM. Esto provoca diversos problemas, en el segundo inicio de sesión, por ejemplo:

*   El applet de NetworkManager no funciona.
*   El volumen de PulseAudio no se puede ajustar.
*   Falla el acceso a GNOME con otro usuario.

Véanse los siguientes informes bugtacker para más detalles:

*   MDM: [[1]](https://github.com/linuxmint/mdm/issues/32)
*   SDDM: [[2]](https://github.com/sddm/sddm/pull/95) (fixed in git master)
*   SLiM: [[3]](https://bugs.archlinux.org/task/34329) [[4]](http://developer.berlios.de/bugs/?func=detailbug&bug_id=19102&group_id=2663)
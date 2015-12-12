# Display manager (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Artículos relacionados

*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Start X at Login (Español)](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)")

El [gestor de pantalla](https://en.wikipedia.org/wiki/es:X_Display_Manager "wikipedia:es:X Display Manager") (siglas en inglés DM) también conocido como gestor de inicio de sesión, es una interfaz gráfica que se muestra al final del proceso de arranque, en lugar de la shell por defecto. Hay varios tipos de gestores de pantalla, al igual que existen diferentes tipos de [gestores de ventanas](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)") y de [entornos de escritorios](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)"). Estos gestores suelen proporcionar un cierto grado de personalización y disponibilidad de temas con cada uno.

## Contents

*   [1 Lista de gestores de pantalla](#Lista_de_gestores_de_pantalla)
    *   [1.1 De consola](#De_consola)
    *   [1.2 Gráficos](#Gr.C3.A1ficos)
*   [2 Cargar el gestor de inicio de sesión](#Cargar_el_gestor_de_inicio_de_sesi.C3.B3n)
    *   [2.1 Utilizar systemd-logind](#Utilizar_systemd-logind)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Lista de sesión](#Lista_de_sesi.C3.B3n)
    *   [3.2 Iniciar automáticamente](#Iniciar_autom.C3.A1ticamente)
*   [4 Problemas conocidos](#Problemas_conocidos)
    *   [4.1 Incompatibilidad con systemd](#Incompatibilidad_con_systemd)

## Lista de gestores de pantalla

### De consola

*   **[CDM](/index.php/CDM "CDM") (Console Display Manager)** — Gestor de pantallas ultraminimalista, pero con todas las funciones de un administrador de inicio de sesión, escrito en bash

[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)<sup><small>AUR</small></sup>

### Gráficos

*   **[GDM](/index.php/GDM "GDM")** — Gestor de inicio de sesión de [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)")

[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — Gestor de inicio de sesión de [KDE](/index.php/KDE "KDE")

[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)

*   **[LightDM](/index.php/LightDM "LightDM")** — Gestor de pantalla multiescritorio, que puede utilizar varios frontends escritos en cualquier conjunto de herramientas

[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — Gestor de inicio de sesión de [LXDE](/index.php/LXDE "LXDE"). Puede usarse independientemente del entorno de escritorio LXDE.

[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — Gestor de inicio de sesión de MDM, fork de GDM 2

[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)<sup><small>AUR</small></sup>

*   **[Qingy](/index.php/Qingy "Qingy")** — Acceso gráfico para el inicio de sesión independiente para X Windows, altamente configurable y muy ligero (utiliza DirectFB)

[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qingy)]</sup>

*   **SDDM** — Gestor de pantalla basado en QML

[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm), [sddm-qt5](https://aur.archlinux.org/packages/sddm-qt5/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sddm-qt5)]</sup>

*   **[SLiM](/index.php/SLiM "SLiM") (Simple Login Manager)** — Solución de acceso gráfico para el inicio de sesión elegante y ligero

[http://slim.berlios.de/](http://slim.berlios.de/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X Display Manager con soporte para XDMCP, host chooser.

[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Cargar el gestor de inicio de sesión

Para activar el acceso gráfico, ejecute el demonio del [gestor de pantallas](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)") preferido (por ejemplo, [KDM](/index.php/KDM "KDM")).

```
# systemctl enable kdm

```

Esto debería funcionar sin configuración adicional. En su defecto, quizás tenga un _default.target_ establecido manualmente o procedente de una instalación antigua

 `$ ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Bastaría con eliminar el enlace simbólico y _systemd_ utilizará su _default.target_ existente (es decir, _graphical.target_).

```
# rm /etc/systemd/system/default.target

```

Después de activar kdm debe mostrarse un enláce simbólico de «display-manager.service» establecido en /etc/systemd/system/

 `$ ls -l /etc/systemd/system/display-manager.service`  `/etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/kdm.service` 

### Utilizar systemd-logind

Con el fin de comprobar el estado de la sesión del usuario, puede utilizar `loginctl`. Todas las acciones [polkit](/index.php/Polkit "Polkit"), como suspender el sistema o montar unidades externas, funcionarán sin configuración adicional.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Consejos y trucos

### Lista de sesión

Muchos gestores de pantalla leen las sesiones disponibles en el directorio `/usr/share/xsessions/`. Este contiene [archivos de entrada de escritorio](http://standards.freedesktop.org/desktop-entry-spec/latest/) estándar para cada gestor de pantalla/gestor de ventanas.

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

_Gestores de inicio de sesión afectados: MDM, SDDM, [SLiM](/index.php/SLiM "SLiM")_

Algunos gestores de pantallas no son totalmente compatibles con systemd, porque utilizan los procesos de sesión de PAM. Esto provoca diversos problemas, en el segundo inicio de sesión, por ejemplo:

*   El applet de NetworkManager no funciona.
*   El volumen de PulseAudio no se puede ajustar.
*   Falla el acceso a GNOME con otro usuario.

Véanse los siguientes informes bugtacker para más detalles:

*   MDM: [[1]](https://github.com/linuxmint/mdm/issues/32)
*   SDDM: [[2]](https://github.com/sddm/sddm/pull/95) (fixed in git master)
*   SLiM: [[3]](https://bugs.archlinux.org/task/34329) [[4]](http://developer.berlios.de/bugs/?func=detailbug&bug_id=19102&group_id=2663)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Display_manager_(Español)&oldid=411571](https://wiki.archlinux.org/index.php?title=Display_manager_(Español)&oldid=411571)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers (Español)](/index.php/Category:Display_managers_(Espa%C3%B1ol) "Category:Display managers (Español)")
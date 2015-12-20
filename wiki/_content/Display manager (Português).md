# Display manager (Português)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Artigos relacionados

*   [Start_X_at_Boot_(Português)](/index.php/Start_X_at_Boot_(Portugu%C3%AAs) "Start X at Boot (Português)")

Um [gestor de display](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), ou gerenciador de login, é tipicamente uma interface gráfica de usuário que é exibida no final do processo de inicialização no lugar do shell padrão. Há várias implementações de gestores de display, assim como existem vários tipos de [gerenciadores de janelas](/index.php/Window_manager "Window manager") e [ambientes desktop](/index.php/Desktop_environment "Desktop environment"). Geralmente, há uma certa quantidade de personalização e themeability disponível com cada um

## Contents

*   [1 Lista de gestores de display](#Lista_de_gestores_de_display)
    *   [1.1 Console](#Console)
    *   [1.2 Gráfico](#Gr.C3.A1fico)
*   [2 Carregando o gestor de display](#Carregando_o_gestor_de_display)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Falha no segundo logout](#Falha_no_segundo_logout)

## Lista de gestores de display

### Console

*   **[CDM](/index.php/CDM "CDM") (Console Display Manager)** — ultra-minimalista, ainda gerenciador de login completo escrito em bash

[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)<sup><small>AUR</small></sup>

### Gráfico

*   **[SLiM](/index.php/SLiM "SLiM") (Simple Login Manager)** — solução de login gráfico leve e elegante

[http://slim.berlios.de/](http://slim.berlios.de/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[Qingy](/index.php/Qingy "Qingy")** — ultraleve e muito configurável login gráfico independente em X Windows (usa DirectFB)

[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qingy)]</sup>

*   **[XDM](/index.php/XDM "XDM")** — X Gestor de Display com suporte para XDMCP.

[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

*   **[GDM](/index.php/GDM "GDM")** — Gestor de Display do [GNOME](/index.php/GNOME "GNOME")

[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — Gestor de Display do [KDE](/index.php/KDE "KDE")

[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>

*   **[LXDM](/index.php/LXDM "LXDM")** — Gestor de Display do [LXDE](/index.php/LXDE "LXDE"). Pode ser usado independente do ambiente desktop LXDE.

[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **[wdm](/index.php/Wdm "Wdm")** — WINGs Display Manager

[http://voins.program.ru/wdm/](http://voins.program.ru/wdm/) || [wdm](https://aur.archlinux.org/packages/wdm/)<sup><small>AUR</small></sup>

*   **[LightDM](/index.php/LightDM "LightDM")** — Substituto do Ubuntu para GDM usando WebKit

[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm), [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)<sup><small>AUR</small></sup>

*   **SDDM** — Gestor de Display baseado em QML

[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm-git](https://aur.archlinux.org/packages/sddm-git/)<sup><small>AUR</small></sup>, [sddm-qt5-git](https://aur.archlinux.org/packages/sddm-qt5-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sddm-qt5-git)]</sup>

## Carregando o gestor de display

Vários getores de display vem empacotados com um arquivo de serviço [systemd](/index.php/Systemd "Systemd"). Veja [aqui](/index.php/Systemd#Running_DMs_under_systemd "Systemd").

## Solução de problemas

### Falha no segundo logout

Com a mudança para systemd, muitos gerenciadores de display falham no segundo logout. Para resolver este problema, basta adicionar uma linha ao final do arquivo de configuração pam apropriado. O exemplo seguinte é para SDDM:

 `/etc/pam.d/sddm` 

```
...
session 	required 	pam_systemd.so

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Display_manager_(Português)&oldid=412797](https://wiki.archlinux.org/index.php?title=Display_manager_(Português)&oldid=412797)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers (Português)](/index.php/Category:Display_managers_(Portugu%C3%AAs) "Category:Display managers (Português)")
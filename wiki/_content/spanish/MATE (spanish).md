Artículos relacionados

*   [GNOME (Español)](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)")

Tomado de la [pagina de MATE](http://mate-desktop.org/):

	*MATE Desktop Environment es la continuación de GNOME 2\. Proporciona un entorno de escritorio atractivo e intuitivo utilizando metáforas tradicionales para Linux y otros sistemas operativos Unix. MATE está [bajo desarrollo activo](https://github.com/mate-desktop) de añadir soporte para nuevas tecnologías, preservando una experiencia de escritorio tradicional.*

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Paquetes adicionales MATE](#Paquetes_adicionales_MATE)
*   [2 Iniciando MATE](#Iniciando_MATE)
    *   [2.1 Acceso grafico](#Acceso_grafico)
    *   [2.2 Manualmente](#Manualmente)
*   [3 Aplicaciones](#Aplicaciones)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Habilitar composicion](#Habilitar_composicion)
    *   [4.2 Habilitar ajuste de ventanas](#Habilitar_ajuste_de_ventanas)
    *   [4.3 Centrar ventanas nuevas](#Centrar_ventanas_nuevas)
*   [5 Solucion de problemas](#Solucion_de_problemas)
    *   [5.1 Habilitar sombra del panel](#Habilitar_sombra_del_panel)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

MATE está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y puede ser [instalado](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") con dos grupos de paquetes:

*   [mate](https://www.archlinux.org/groups/x86_64/mate/) contiene el entorno de escritorio básico y aplicaciones necesarias para la experiencia estándar de MATE.

*   [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) contiene varias herramientas opcionales, como un salvapantallas, una calculadora, un editor y otras aplicaciones no problemáticas que van bien con el escritorio MATE. La instalación de este grupo es opcional.

**Nota:** Tenga en cuenta que la instalación únicamente del grupo [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) no instala el grupo [mate](https://www.archlinux.org/groups/x86_64/mate/) como dependencia: si realmente lo quiere todo debe instalar ambos grupos de forma explícita.

### Paquetes adicionales MATE

Paquetes oficiales adicionales no incluidos en [mate](https://www.archlinux.org/groups/x86_64/mate/) o [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/).

*   **GNOME Main Menu** — Miniaplicación para el panel de MATE similar al menu principal tradicional, pero con algunas adiciones.

	[http://mate-desktop.org](http://mate-desktop.org) || [gnome-main-menu](https://aur.archlinux.org/packages/gnome-main-menu/)

*   **MATE Netbook** — Miniaplicación para el panel de MATE que podría ser útil para propietarios de dispositivos de pantalla pequeña, como una Netbook. La miniaplicación maximiza automáticamente todas las ventanas y proporciona una miniaplicación para cambiar aplicaciones.

	[http://mate-desktop.org](http://mate-desktop.org) || [mate-netbook](https://www.archlinux.org/packages/?name=mate-netbook)

También hay otras aplicaciones de MATE no oficiales que son mantenidas por la comunidad de MATE y por lo tanto no incluidas en los grupos [mate](https://www.archlinux.org/groups/x86_64/mate/) o [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/).

*   **MATE AccountsDialog** — Una aplicación para ver y modificar información de cuentas de usuario de MATE.

	[https://github.com/NiceandGently/mate-accountsdialog](https://github.com/NiceandGently/mate-accountsdialog) || [mate-accountsdialog](https://www.archlinux.org/packages/?name=mate-accountsdialog)

*   **Lock Keys Applet** — Miniaplicación para el panel de MATE que muestra cuales de las teclas CapsLock, NumLock y ScrollLock están encendidas y cuales están apagadas.

	[http://www.zavedil.com/mate-lock-keys-applet/](http://www.zavedil.com/mate-lock-keys-applet/) || [mate-applet-lockkeys](https://aur.archlinux.org/packages/mate-applet-lockkeys/)

*   **Online Radio Applet** — Miniaplicación para el panel de MATE que deja reproducir tu radio favorita en linea con un solo clic.

	[http://www.zavedil.com/online-radio-applet/](http://www.zavedil.com/online-radio-applet/) || [mate-applet-streamer](https://www.archlinux.org/packages/?name=mate-applet-streamer)

*   **MATE Color Manager** — Aplicación de gestión de color para MATE.

	[https://github.com/NiceandGently/mate-color-manager](https://github.com/NiceandGently/mate-color-manager) || [mate-color-manager](https://aur.archlinux.org/packages/mate-color-manager/)

*   **MATE Disk Utility** — Aplicación de gestión de disco para MATE.

	[https://github.com/NiceandGently/mate-disk-utility](https://github.com/NiceandGently/mate-disk-utility) || [mate-disk-utility](https://aur.archlinux.org/packages/mate-disk-utility/)

*   **MATE Screensaver Hacks** — Habilita salvapantallas de xscreensaver en MATE.

	[http://www.jwz.org/xscreensaver/](http://www.jwz.org/xscreensaver/) || [mate-screensaver-hacks](https://aur.archlinux.org/packages/mate-screensaver-hacks/)

*   **MATE Themes Extras** — Colección de temas de escritorio GTK2/3 para MATE.

	[https://github.com/NiceandGently/mate-themes-extras](https://github.com/NiceandGently/mate-themes-extras) || [mate-themes-extras](https://www.archlinux.org/packages/?name=mate-themes-extras)

*   **Variety** — Variety permite rotar los fondos de pantalla en forma automática, descargando las imágenes desde una buena variedad de sitios populares.

	[http://peterlevi.com/variety/](http://peterlevi.com/variety/) || [variety](https://www.archlinux.org/packages/?name=variety)

Lo siguiente también está disponible a través de AUR y se integra con MATE pero el paquete no es mantenido por el equipo de MATE.

*   **MintMenu** — Menú de Linux Mint para MATE.

	[http://packages.linuxmint.com/pool/main/m/mintmenu](http://packages.linuxmint.com/pool/main/m/mintmenu) || [mintmenu](https://aur.archlinux.org/packages/mintmenu/)

## Iniciando MATE

MATE puede iniciarse mediante un gestor de pantalla o manualmente.

### Acceso grafico

Seleccione *MATE* en el menú del [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") que ha elegido. El equipo de MATE recomienda [LightDM](/index.php/LightDM "LightDM") con el greeter GTK como el gestor de pantalla, que puede ser instalado con el paquete [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter).

### Manualmente

Para iniciar MATE manualmente, debe agregar

```
exec mate-session

```

al archivo `[~/.xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")` y luego ejecutar

```
$ startx

```

**Nota:** Consulte [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para más detalles, tales como la conservación de la sesión de logind (y/o consolekit).

## Aplicaciones

Es importante tener en cuenta que muchas aplicaciones principales de GNOME fueron derivadas y renombradas en MATE, como los términos de licencia. Estas son las aplicaciones más importantes tomadas de GNOME.

| Aplicación | GNOME 2 | MATE |
| Editor de menú | Alacarte | Mozo |
| Gestor de archivos | Nautilus | Caja |
| Gestor de ventanas | Metacity | Marco |
| Editor de textos | Gedit | Pluma |
| Visor de imágenes | Eye of GNOME | Eye of MATE |
| Visor de documentos | Evince | Atril |
| Gestor de archivadores | File Roller | Engrampa |

Otras aplicaciones y componentes básicos prefijados con GNOME (como GNOME Panel, GNOME Menus, etc) simplemente han tenido el prefijo renombrado a "MATE", para así convertirse en MATE Panel, MATE Menus, etc.

## Consejos y trucos

### Habilitar composicion

La composición no está habilitada de forma predeterminada. Para habilitarla vaya a `Sistema -> Preferencias -> Ventanas` y en la pestaña `General` haga clic en la casilla **Habilitar gestor de ventanas de composicion por software**. Alternativamente, puede ejecutar lo siguiente desde el terminal:

```
$ dconf write /org/mate/marco/general/compositing-manager true

```

### Habilitar ajuste de ventanas

El ajuste de ventanas no está habilitado de forma predeterminada, para habilitarlo vaya a `Sistema -> Preferencias -> Ventanas` y en la pestaña `Ubicación` haga clic en la casilla **Activar posicionamiento de ventanas lado a lado**. Alternativamente, puede ejecutar lo siguiente desde el terminal:

```
$ dconf write /org/mate/marco/general/side-by-side-tiling true

```

### Centrar ventanas nuevas

Por defecto, las ventanas nuevas son colocadas en la esquina superior izquierda,. Para centrar ventanas nuevas vaya a `Sistema -> Preferencias -> Ventanas` y en la pestaña `Ubicación` haga clic en la casilla **Centrar ventanas nuevas**. Alternativamente, puede ejecutar lo siguiente desde el terminal:

```
$ dconf write /org/mate/marco/general/center-new-windows true

```

## Solucion de problemas

### Habilitar sombra del panel

Debido a una condición de carrera, la sombra del panel no aparece luego de iniciar sesión en el escritorio MATE, incluso con la composición habilitada. [[1]](https://github.com/mate-desktop/mate-panel/issues/193)

Agregue un retraso a *marco*:

 `/usr/share/applications/marco.desktop` 
```
X-MATE-Autostart-Phase=**Applications**
**X-MATE-Autostart-Delay=2**
X-MATE-Provides=windowmanager
X-MATE-Autostart-Notify=true
```

**Nota:** Los retrasos sólo están permitidos en la fase applications, por lo tanto `X-MATE-Autostart-Phase` debe ser establecido a `Applications`.

Si esto no tiene efecto, aumentar la duración de retraso.

## Véase también

*   [Página oficial de MATE](http://mate-desktop.org)
*   [Wiki de MATE para Arch Linux](http://wiki.mate-desktop.org/archlinux_custom_repo)
*   [*Imágenes del escritorio MATE*](http://mate-desktop.org/gallery/1.8/)
*   [*The MATE Desktop Environment*](https://bbs.archlinux.org/viewtopic.php?pid=1018647) - Hilo del foro de Arch Linux acerca de MATE
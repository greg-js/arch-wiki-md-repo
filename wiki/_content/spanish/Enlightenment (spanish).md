**Estado de la traducción**
Este artículo es una traducción de [Enlightenment](/index.php/Enlightenment "Enlightenment"), revisada por última vez el **2019-02-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Enlightenment&diff=0&oldid=565831) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)")
*   [Gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 Instalación](#Instalación)
        *   [1.1.1 Del AUR](#Del_AUR)
    *   [1.2 Iniciar Enlightenment](#Iniciar_Enlightenment)
        *   [1.2.1 Entrance](#Entrance)
        *   [1.2.2 Iniciar Enlightenment manualmente](#Iniciar_Enlightenment_manualmente)
    *   [1.3 Configuración](#Configuración)
        *   [1.3.1 Redes](#Redes)
        *   [1.3.2 Agente Polkit](#Agente_Polkit)
        *   [1.3.3 Integración con GNOME Keyring](#Integración_con_GNOME_Keyring)
        *   [1.3.4 Bandeja del sistema](#Bandeja_del_sistema)
        *   [1.3.5 Notificaciones](#Notificaciones)
    *   [1.4 Temas](#Temas)
        *   [1.4.1 GTK+](#GTK+)
    *   [1.5 Módulos y Gadgets](#Módulos_y_Gadgets)
        *   [1.5.1 Módulos "Extra"](#Módulos_"Extra")
    *   [1.6 Atajos de teclado predeterminados](#Atajos_de_teclado_predeterminados)
    *   [1.7 Solución de problemas](#Solución_de_problemas)
        *   [1.7.1 Composición](#Composición)
        *   [1.7.2 Las fuentes son ilegibles](#Las_fuentes_son_ilegibles)
        *   [1.7.3 El brillo siempre está atenuado](#El_brillo_siempre_está_atenuado)
        *   [1.7.4 El tema del cursor es inconsistente](#El_tema_del_cursor_es_inconsistente)
        *   [1.7.5 Imágenes de fondo](#Imágenes_de_fondo)
*   [2 Enlightenment DR16](#Enlightenment_DR16)
    *   [2.1 Instalar E16](#Instalar_E16)
    *   [2.2 Configuración básica](#Configuración_básica)
        *   [2.2.1 Iniciar/reiniciar/detener scripts](#Iniciar/reiniciar/detener_scripts)
        *   [2.2.2 Compositor](#Compositor)
*   [3 Véase también](#Véase_también)

## Enlightenment

Consta tanto del [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") [Enlightenment](https://www.enlightenment.org/) como de Enlightenment Foundation Libraries (EFL), que proporcionan características adicionales de entorno de escritorio, como, por ejemplo, un toolkit, un lienzo de objetos y objetos abstractos. Ha estado en desarrollo desde 2005, pero en febrero de 2011 las principales EFLs vieron su primera versión estable 1.0\.

### Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [enlightenment](https://www.archlinux.org/packages/?name=enlightenment).

También es posible que desee instalar [terminology](https://www.archlinux.org/packages/?name=terminology), que es un emulador de terminal basado en EFL que se integra bien con Enlightenment.

#### Del AUR

**Advertencia:** Algunos de estos PKGBUILDs usan código de desarrollo inestable. Usélos bajo su propia responsabilidad.

Los PKGBUILDs de desarrollo que descargan e instalan el último código de desarrollo están disponibles como [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/) y sus dependencias.

Las siguientes son aplicaciones basadas en EFL, la mayoría en una etapa temprana de desarrollo y aún no publicadas:

*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) - Editor de texto Ecrire
*   [edi](https://aur.archlinux.org/packages/edi/) - Un IDE basado en EFL
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/) - Navegador web Elbow
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/) - Navegador de fotos Eluminance
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) - Reproductor de música [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy)
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) - Visor de tablas periódicas [Eperiodique](http://eperiodique.sourceforge.net/)
*   [ephoto](https://aur.archlinux.org/packages/ephoto/) y [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) - Visor de imágenes [Ephoto](http://smhouston.us/ephoto/)
*   [epour](https://aur.archlinux.org/packages/epour/) - Cliente torrent basado en EFL
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/) - E Python Media Center
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) - Calculadora de equivalencias
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) - Regla de pantalla y herramientas de medición Eruler
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) - *Escape from Booty Bay* juego del estilo de *Angry Birds*
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) - [Elemines](http://elemines.sourceforge.net/), juego del estilo del *Buscaminas*
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) - Inspector *Espionage D-Bus*
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) - Visor de imágenes simple EV
*   [rage](https://aur.archlinux.org/packages/rage/) y [rage-git](https://aur.archlinux.org/packages/rage-git/) - Reproductor de vídeo Rage

### Iniciar Enlightenment

Simplemente elija la sesión *Enlightenment* de su [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") favorito o configure [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para iniciarla desde la consola.

#### Entrance

**Advertencia:** Entrance es altamente experimental, y no tiene el soporte adecuado para systemd. Úselo bajo su propia responsabilidad.

Enlightenment tiene un nuevo gestor de pantalla llamado Entrance, que se proporciona con el paquete [entrance-git](https://aur.archlinux.org/packages/entrance-git/). Entrance es bastante sofisticado y su configuración está controlada por `/etc/entrance/entrance.conf`. Se puede utilizar [activando](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `entrance.service`.

#### Iniciar Enlightenment manualmente

Si prefiere iniciar Enlightenment manualmente desde la consola, agregue la siguiente línea a su archivo `~/.xinitrc`:

 `~/.xinitrc` 
```
exec enlightenment_start

```

Posteriormente, se puede iniciar Enlightenment ejecutando `startx`. Véase [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para obtener más detalles.

Para probar el compositor experimental [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)"), ejecute `enlightenment_start` en un [tty](/index.php/Getty_(Espa%C3%B1ol) "Getty (Español)").

### Configuración

Enlightenment tiene un sofisticado sistema de configuración al que se puede acceder desde el submenú *Configuración* del menú principal.

#### Redes

**ConnMan**

El administrador de red preferido de Enlightenment es [ConnMan](/index.php/ConnMan "ConnMan") que se puede instalar desde el paquete [connman](https://www.archlinux.org/packages/?name=connman). Siga las instrucciones de [ConnMan](/index.php/ConnMan "ConnMan") para llevar a cabo la configuración.

Para la configuración extendida, también puede instalar Econnman (disponible en el AUR como [econnman](https://aur.archlinux.org/packages/econnman/) o [econnman-git](https://aur.archlinux.org/packages/econnman-git/)) y sus dependencias asociadas.

**Agregar el gadget ConnMan al estante**

1.  Vaya a *Configuración -> Extensiones -> Módulos*
2.  En *Sistema*
3.  *Administrador de conexiones*
4.  Cárguelo (primero selecciónelo y luego presione *Cargar*).
5.  Haga clic derecho en el estante en la parte inferior de la pantalla.
6.  Vaya a *Estante -> Contenidos*
7.  Luego, simplemente desplácese hacia abajo y seleccione *ConnMan*.
8.  Finalmente, haga clic en *Añadir*.

**NetworkManager**

También puede utilizar [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) para gestionar sus conexiones de red, véase [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") para obtener más información.

Sin embargo, tenga en cuenta que el applet necesitará el soporte de Appindicator para mostrarse en la [bandeja del sistema](#Bandeja_del_sistema) de Enlightenment. Véase [NetworkManager#Appindicator](/index.php/NetworkManager#Appindicator "NetworkManager"). Como alternativa al uso del applet, NetworkManager incluye las interfaces CLI y TUI para la configuración de la red, véase [NetworkManager#Usage](/index.php/NetworkManager#Usage "NetworkManager").

#### Agente Polkit

Enlightenment no se expide con un [agente de autentificación gráfico polkit](/index.php/Polkit#Authentication_agents "Polkit"). Si desea acceder a algunas acciones con privilegios (por ejemplo, montar un sistema de archivos en un dispositivo del sistema), debe instalar uno e iniciarlo automáticamente. Para ello, debe ir a *Panel de preferencias > Aplicaciones > Aplicaciones al inicio > Sistema* y añadirlo. Hay un agente de autenticación basado en EFL disponible en el AUR, [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/).

#### Integración con GNOME Keyring

Es posible utilizar gnome-keyring en Enlightenment. Sin embargo, se necesita hacer un pequeño truco para que funcione a pleno rendimiento. Primero, debe decirle a Enlightenment que inicie automáticamente gnome-keyring. Para ello, debe ir a *Panel de preferencias > Aplicaciones > Aplicaciones al inicio > Sistema* y añadir *Certificados y almacenamiento de claves*, *Agente de claves GPG*, *Agente de claves SSH* y *Servicio de almacenamiento de secretos*. Después, debe editar el archivo `~/.pam_environment` y agregar lo siguiente:

```
      #Set gnome-keyring as the ssh authentication agent
      SSH_AUTH_SOCK=/run/user/${UID}/keyring/ssh

```

Este "truco" se usa para anular la configuración automática de la variable "enlightenment-start" desde "ssh-agent" a gnome-keyring.

Véase más información sobre este tema en el artículo [GNOME Keyring](/index.php/GNOME/Keyring_(Espa%C3%B1ol) "GNOME/Keyring (Español)").

#### Bandeja del sistema

**Nota:** Desde Enlightenment 20, la compatibilidad con Xembed se ha eliminado [[1]](https://twitter.com/_enlightenment_/status/538000507315314688) lo que significa que muchos applets "heredados" ya no se pueden mostrar en el Systray. Para usar estos applets, deberá usar en su lugar una aplicación standalone de bandeja del sistema como, por ejemplo, [stalonetray](https://www.archlinux.org/packages/?name=stalonetray).

Enlightenment es compatible con una bandeja del sistema, pero no está habilitada de forma predeterminada. Para habilitar la bandeja del sistema, abra el menú principal de Enlightenment, navegue hasta el submenú *Preferencias* y haga clic en la opción *Módulos*. Desplácese hacia abajo hasta que vea la opción *Systray*. Resalte esa opción y haga clic en *Cargar*. Ahora que el módulo se ha cargado, se puede agregar al estante. Haga clic derecho en el estante al que desea agregar Systray, resalte el submenú *Estante* y haga clic en la opción *Contenidos*. Desplácese hacia abajo hasta que vea *Systray*. Resalte esa opción y haga clic en el botón *Añadir*.

#### Notificaciones

Enlightenment proporciona un servidor de notificaciones a través de su extensión de Notificaciones.

*   Las notificaciones se pueden mostrar en cualquier esquina de la "pantalla" como se describe a continuación
*   Las reglas de pantalla disponibles son Pantalla principal, Pantalla actual, Todas las pantallas y Xinerama
*   Las notificaciones se pueden filtrar según la urgencia (baja, normal o crítica en cualquier combinación)
*   Se puede establecer un tiempo de espera de notificación predeterminado y se puede aplicar opcionalmente para todas las notificaciones
*   El servidor de notificaciones también puede ignorar opcionalmente las solicitudes de reemplazo de ID

### Temas

Se pueden encontrar más temas para personalizar el aspecto de Enlightenment en:

*   [extra.enlightenment.org](https://extra.enlightenment.org/themes/)
*   [enlightenment-themes.org](https://www.enlightenment-themes.org/)
*   [relighted.c0n.de](http://relighted.c0n.de/#100) para el tema predeterminado en 200 colores diferentes
*   [git.enlightenment.org](http://git.enlightenment.org/themes) (git clone el tema que le guste, ejecute 'make' y terminará con un archivo de tema .edj)
*   [packages.bodhilinux.com](http://packages.bodhilinux.com/bodhi/pool/stable/b/) tiene una buena colección (deberá extraer el archivo .edj del .deb; bsdtar hará esto y es parte de la instalación base de ArchLinux). Un buen catálogo puede verse en [su wiki](https://web.archive.org/web/20140120083020/http://art.bodhilinux.com/doku.php?id=bodhi_e17_themes_v3).
*   [exchange.enlightenment.org](https://web.archive.org/web/20161025233126/https://exchange.enlightenment.org/theme) (archivado)

Puede instalar los temas (que vienen en formato .edj) usando el cuadro de diálogo de configuración del tema o moviéndolos a `~/.e/e/themes`.

**Nota:** Enlightenment no proporciona una API de tema estable, y han habido numerosos cambios en la API de tema a lo largo de los años, incluso después de que se lanzara E17\. Los temas que no se hayan actualizado regularmente probablemente no funcionen.

**Sugerencia:** Para hacer que las aplicaciones GTK y Qt coincidan con el tema predeterminado de Enlightenment, puede descargar un tema como, por ejemplo, [E17 GTK theme](http://gnome-look.org/content/show.php/?content=163472). Colóquelo en `~/.themes/` o instale el paquete [gtk-theme-e17gtk-git](https://aur.archlinux.org/packages/gtk-theme-e17gtk-git/), seleccione los temas de aplicaciones desde la configuración de Enlightenment y establézcalos, logrando así que todas las aplicaciones GTK2 y GTK3 coincidan con el tema predeterminado de Enlightenment. Luego puede configurar las aplicaciones Qt (o configurar las opciones predeterminadas de Qt) para usar el tema Gtk+ de modo que imite el tema que utilizan sus aplicaciones GTK, para de esta manera asegurarse de que la mayoría de las aplicaciones combinan perfectamente con el tema de Enlightenment predeterminado. Véase [Aspecto uniforme para aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)").

#### GTK+

Para modificar el tema GTK+, vaya a *Preferencias > Todo > Apariencia > Tema de las aplicaciones*.

### Módulos y Gadgets

	Módulo

	Nombre utilizado en Enlightenment para referirse al código de "respaldo" de un gadget.

	Gadget

	Front-end o interfaz de usuario que debería ayudar a los usuarios finales de Enlightenment a hacer algo.

Muchos módulos proporcionan gadgets que se pueden agregar a su escritorio o a un estante. Algunos módulos (como, por ejemplo, CPUFreq) solo proporcionan un Gadget único, mientras que otros (como, por ejemplo, Composite) proporcionan características adicionales sin ningún gadget. Tenga en cuenta que ciertos gadgets, como Systray, solo se pueden agregar a un estante, mientras que otros, como Moon, solo se pueden cargar en el escritorio.

#### Módulos "Extra"

**Advertencia:** Estos son módulos de terceros y no están soportados oficialmente por los desarrolladores de Enlightenment. También se extraen directamente de git, por lo que es código de desarrollo que puede dejar de funcionar en cualquier momento. Úselo bajo su propia responsabilidad.

Además de los módulos aquí descritos, se pueden encontrar más módulos "extra" en [e-modules-extra-git](https://aur.archlinux.org/packages/e-modules-extra-git/).

**Scale Windows**

El módulo *Scale Windows*, que requiere que la composición esté habilitada, agrega varias características. El efecto Scale Windows reduce todas las ventanas abiertas y las pone a la vista. Esto se conoce como "Mission Control" en macOS. El efecto aleja el zoom y muestra todos los escritorios como una pared, como el plugin compiz expo. Ambos pueden agregarse al escritorio como un gadget o asignarse a un atajo de teclado, a un atajo de ratón o a un atajo de borde (de pantalla).

A algunas personas les gusta cambiar la asignación de teclas predeterminada de selección de ventanas `ALT + Tab` para usar Scale Windows para seleccionar ventanas. Para cambiar esta configuración, vaya a *Menú > Preferencias > Panel de preferencias > Entrada > Atajos de teclado*. Desde aquí, puede establecer cualquier combinación de teclas que desee.

Para reemplazar el atajo de teclado de selección de ventanas por Scale Windows, desplácese por el panel izquierdo hasta que encuentre la sección *ALT* y luego busque y seleccione `ALT + Tab`. Luego, desplácese por el panel derecho en busca de la sección "Scale Windows" y elija o bien *Seleccionar siguiente* o *Seleccionar siguiente (todo)* dependiendo de si desea ver las ventanas solo desde el escritorio actual o desde todos los escritorios. Haga clic en *Aplicar* para guardar los cambios.

Disponible en [upstream git](https://git.enlightenment.org/enlightenment/modules/comp-scale.git/).

### Atajos de teclado predeterminados

<caption>Algunos atajos de teclado predeterminados de Enlightenment</caption>
| Mayus + F10 | Maximizar verticalmente |
| Ctrl + Menú | Mostrar menú de clientes |
| Alt + Escape | Mostrar lanzador "Everything" (aplicaciones, ventanas, etc.) |
| Win + Izquierda | Maximizar izquierda |
| Win + Derecha | Maximizar derecha |
| Alt + Mayus + F10 | Maximizar horizontalmente |
| Alt + Mayus + Izquierda | Voltear escritorio a la izquierda |
| Alt + Mayus + Derecha | Voltear escritorio a la derecha |
| Ctrl + Alt + D | Mostrar escritorio |
| Ctrl + Alt + F | Alternar pantalla completa |
| Ctrl + Alt + I | Alternar modo minimizado |
| Ctrl + Alt + K | Matar ventana |
| Ctrl + Alt + L | Bloquear escritorio |
| Ctrl + Alt + N | Maximizar ventana |
| Ctrl + Alt + R | Alternar "Enrollar arriba" |
| Ctrl + Alt + W | Menú de ventana |
| Ctrl + Alt + X | Cerrar ventana |
| Ctrl + Alt + Abajo | Bajar una ventana |
| Ctrl + Alt + Arriba | Elevar una ventana |
| Ctrl + Alt + Izquierda | Voltear el escritorio linealmente a la izquierda |
| Ctrl + Alt + Derecha | Voltear el escritorio linealmente a la derecha |
| Ctrl + Alt + Supr | Controles del sistema |
| Ctrl + Alt + Insert | Ejecutar la terminal por defecto |

### Solución de problemas

Si encuentra algún comportamiento inesperado, puede probar varias cosas:

1.  intente ver si se da el mismo comportamiento con el tema predeterminado
2.  deshabilite cualquier módulo de terceros que pueda tener instalado
3.  haga una copia de seguridad del archivo `~/.e` y después elimínelo (por ejemplo, `mv ~/.e ~/.e.copia`)

Si está seguro de haber encontrado un error, repórtelo [directamente a la fuente](https://phab.enlightenment.org/maniphest/task/create/).

#### Composición

Cuando sea necesario restablecer la configuración y no se pueda acceder a la ventana de preferencias, los ajustes del compositor se pueden restablecer mediante el atajo de teclado `Ctrl + Alt + Mayus + Inicio`.

#### Las fuentes son ilegibles

Si las fuentes son demasiado pequeñas y su pantalla es ilegible, asegúrese de que los paquetes de fuentes correctos se encuentran instalados. Por ejemplo, [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) y [ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera) son candidatos válidos.

Puede configurar el escalado de las fuentes en *Preferencias > Panel de preferencias > Apariencia > Escalado*.

#### El brillo siempre está atenuado

Es posible que Enlightenment disminuya habitualmente el brillo al 30% al cerrar sesión y solo lo restaurará al 100% cuando inicie sesión con otra sesión de Enlightenment. Esto es especialmente problemático cuando se utiliza otro entorno de escritorio junto con Enlightenment, ya que el brillo no se restaurará automáticamente a su nivel normal cuando se utilize ese entorno de escritorio. Para solucionar este problema, abra el *Panel de preferencias* de Enlightenment y, en la pestaña *Apariencia*, haga clic en la opción *Composición*. Marque la casilla *No atenuar retroiluminación* y haga clic en *Aplicar*.

#### El tema del cursor es inconsistente

Es posible que el tema del cursor para el escritorio sea distinto al utilizado en otras aplicaciones como [Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)"). Esto se debe a que las aplicaciones de escritorio usan temas de cursor de Xorg mientras que Enlightenment tiene su propia colección de temas de cursor. Por consistencia, puede configurar Enlightenment para usar siempre el tema del cursor de Xorg. Para ello, abra el *Panel de preferencias* de Enlightenment y haga clic en la pestaña *Entrada*. Haga clic en la opción *Ratón*. Cambie el tema de *Enlightenment* a *X* y haga clic en *Aplicar*. Ahora debería observar que el mismo tema del cursor se usa en todas partes. Si el tema del cursor de Xorg no es siempre consistente, véase [Cursor themes#XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes").

#### Imágenes de fondo

Tiene que copiar los fondos de pantalla deseados a la carpeta `~/.e/e/backgrounds/`

Al hacer clic con el botón central o derecho del ratón en cualquier parte del escritorio tendrá acceso a la configuración; seleccione `/Desktop/Backgrounds/`.

Cualquier nueva imagen copiada a la carpeta `~/.e/e/backgrounds/` hará que la lista de fondos disponibles se actualize automáticamente. Seleccione el fondo de pantalla que desee en el menú desplegable. Dentro de las pestañas apropiadas en la configuración global, puede aplicar ajustes como: mosaico, rellenar, etc.

## Enlightenment DR16

Enlightenment, Development Release 16 se lanzó por primera vez en el año 2000 y alcanzó la versión 1.0 en el 2009\. Originalmente, DR16 representaba la versión 0.16 del proyecto Enlightenment. Lo puede encontrar actualmente como "Enlightenment16" en los repositorios de Arch, aunque todavía está en desarrollo a día de hoy, siendo actualizado regularmente por su mantenedor Kim 'kwo' Woelders. Con composición, sombras y transparencias, E16 mantuvo toda la velocidad que presidió su fundación por el autor original Carsten "Rasterman" Haitzler, pero con un refinamiento actualizado.

### Instalar E16

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [enlightenment16](https://aur.archlinux.org/packages/enlightenment16/).

Véase `/usr/share/doc/e16/e16.html` para documentación más detallada. La página de manual está en [e16(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/e16.1) y solo da opciones de arranque.

### Configuración básica

La mayoría de los archivos de configuración de E16 se encuentran en `~/.e16` y están basados en texto, por lo que se pueden editar a voluntad. Eso también incluye los menús.

Las teclas de acceso directo se pueden modificar a mano o con el software e16keyedit que se proporciona como código fuente en la página [sourceforge](http://sourceforge.net/projects/enlightenment/) del proyecto e16\. Tenga en cuenta que el archivo de los accesos directos del teclado no se crea en `~/.e16` de forma predeterminada. Puede copiar la versión empaquetada a su directorio de inicio si desea realizar cambios:

```
$ cp /usr/share/e16/config/bindings.cfg ~/.e16

```

#### Iniciar/reiniciar/detener scripts

Cree una carpeta Init, una carpeta Start y una carpeta Stop en su directorio `~/.e16`: cualquier script .sh que se encuentre allí se ejecutará o bien al inicio (de la carpeta Init), o en cada reinicio (de la carpeta Start) , o en el apagado (de la carpeta Stop); siempre que lo permita a través del botón central del ratón / preferencias / sesión / <habilitar scripts> y los haga ejecutables con `chmod +x *suscript.sh*`. Los ejemplos típicos incluyen el inicio de pulseaudio o su applet de administrador de red favorito.

#### Compositor

Las sombras, los efectos de transparencia *et al* se pueden encontrar accediendo con el botón central/derecho del ratón / Preferencias, Composición.

## Véase también

*   [Página web de Enlightenment](http://www.enlightenment.org/)
*   [Enlightenment Exchange](http://exchange.enlightenment.org/)
*   [Documentación de desarollo de Enlightenment](http://docs.enlightenment.org/)
*   [Guía Bodhi para Enlightenment](http://www.bodhilinux.com/e17guide/e17guideES/)
*   [Cosas para E17](http://www.e17-stuff.org/)
*   [Recurso de descarga de DR16](http://sourceforge.net/projects/enlightenment/)
*   [Lista de correos de los usuarios de Enlightenment](https://lists.sourceforge.net/lists/listinfo/enlightenment-users)
*   [Lista de correos de los desarrolladores de Enlightenment](https://lists.sourceforge.net/lists/listinfo/enlightenment-devel)
*   [ircs://chat.freenode.net#e](ircs://chat.freenode.net#e)
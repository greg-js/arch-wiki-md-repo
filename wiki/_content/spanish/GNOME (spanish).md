Artículos relacionados

*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [GTK+](/index.php/GTK%2B "GTK+")
*   [GDM (Español)](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)")
*   [Nautilus (Español)](/index.php/Nautilus_(Espa%C3%B1ol) "Nautilus (Español)")
*   [Gedit](/index.php/Gedit "Gedit")
*   [Epiphany](/index.php/Epiphany "Epiphany")
*   [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")

Tomado de la [página de GNOME](http://www.gnome.org/about/%7Cla):

	*«El Proyecto GNOME se inició en 1997 por —en aquellos días— dos estudiantes universitarios, Miguel de Icaza y Federico Mena. Su objetivo: producir un [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") de código libre. Desde entonces, GNOME se ha convertido en una empresa exitosa. Usado por millones de personas en todo el mundo, es el entorno de escritorio más popular para GNU/Linux y sistemas operativos tipo UNIX. El escritorio se ha utilizado con éxito en empresas de gran escala, y en despliegues públicos, y las tecnologías del proyecto desarrollador se utilizan en un gran número de dispositivos móviles populares.»*

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Iniciar GNOME](#Iniciar_GNOME)
*   [3 Usar la shell](#Usar_la_shell)
    *   [3.1 Hoja de trucos y atajos de GNOME](#Hoja_de_trucos_y_atajos_de_GNOME)
    *   [3.2 Reiniciar la shell](#Reiniciar_la_shell)
    *   [3.3 La shell se bloquea](#La_shell_se_bloquea)
    *   [3.4 La shell se congela](#La_shell_se_congela)
*   [4 Integración de pacman: GNOME PackageKit](#Integraci.C3.B3n_de_pacman:_GNOME_PackageKit)
    *   [4.1 Notificaciones de actualizaciones de paquetes](#Notificaciones_de_actualizaciones_de_paquetes)
*   [5 Personalizar la apariencia de GNOME](#Personalizar_la_apariencia_de_GNOME)
    *   [5.1 Apariencia general](#Apariencia_general)
        *   [5.1.1 Gsettings](#Gsettings)
        *   [5.1.2 GNOME Tweak Tool](#GNOME_Tweak_Tool)
        *   [5.1.3 Temas GTK3 a través de settings.ini](#Temas_GTK3_a_trav.C3.A9s_de_settings.ini)
        *   [5.1.4 Temas para iconos](#Temas_para_iconos)
    *   [5.2 Totem](#Totem)
    *   [5.3 Panel de GNOME](#Panel_de_GNOME)
        *   [5.3.1 Mostrar fecha en la barra superior](#Mostrar_fecha_en_la_barra_superior)
        *   [5.3.2 Ocultar iconos en la barra superior](#Ocultar_iconos_en_la_barra_superior)
            *   [5.3.2.1 Ocultar iconos con las extensiones shell](#Ocultar_iconos_con_las_extensiones_shell)
            *   [5.3.2.2 Modificar manualmente el script del panel de GNOME](#Modificar_manualmente_el_script_del_panel_de_GNOME)
        *   [5.3.3 Mostrar el icono de la batería](#Mostrar_el_icono_de_la_bater.C3.ADa)
        *   [5.3.4 Eliminar la demora al salir](#Eliminar_la_demora_al_salir)
        *   [5.3.5 Mostrar el monitor del sistema](#Mostrar_el_monitor_del_sistema)
        *   [5.3.6 Mostrar información meteorológica](#Mostrar_informaci.C3.B3n_meteorol.C3.B3gica)
    *   [5.4 Vista de actividades](#Vista_de_actividades)
        *   [5.4.1 Eliminar entradas de la vista de Aplicaciones](#Eliminar_entradas_de_la_vista_de_Aplicaciones)
        *   [5.4.2 Quitar lanzadores de Wine desde el menú de Aplicaciones](#Quitar_lanzadores_de_Wine_desde_el_men.C3.BA_de_Aplicaciones)
        *   [5.4.3 Cambiar el tamaño de los iconos de las aplicaciones](#Cambiar_el_tama.C3.B1o_de_los_iconos_de_las_aplicaciones)
        *   [5.4.4 Cambiar el tamaño de los iconos del menú izquierdo](#Cambiar_el_tama.C3.B1o_de_los_iconos_del_men.C3.BA_izquierdo)
        *   [5.4.5 Cambiar el tamaño de iconos con el alternador (alt-tab)](#Cambiar_el_tama.C3.B1o_de_iconos_con_el_alternador_.28alt-tab.29)
        *   [5.4.6 Cambiar el tamaño de los iconos de la bandeja del sistema](#Cambiar_el_tama.C3.B1o_de_los_iconos_de_la_bandeja_del_sistema)
        *   [5.4.7 Desactivar la esquina flotante del menú Actividades](#Desactivar_la_esquina_flotante_del_men.C3.BA_Actividades)
        *   [5.4.8 Desactivar bandeja de mensajes flotante](#Desactivar_bandeja_de_mensajes_flotante)
    *   [5.5 Barra de titulo](#Barra_de_titulo)
        *   [5.5.1 Reducir el tamaño de la barra de titulo](#Reducir_el_tama.C3.B1o_de_la_barra_de_titulo)
        *   [5.5.2 Reordenar los botones de la barra de titulo](#Reordenar_los_botones_de_la_barra_de_titulo)
        *   [5.5.3 Ocultar la barra de títulos cuando se maximiza](#Ocultar_la_barra_de_t.C3.ADtulos_cuando_se_maximiza)
    *   [5.6 Pantalla de acceso](#Pantalla_de_acceso)
        *   [5.6.1 Imagen de fondo de la pantalla de acceso](#Imagen_de_fondo_de_la_pantalla_de_acceso)
        *   [5.6.2 Fuentes más grandes para la pantalla de acceso](#Fuentes_m.C3.A1s_grandes_para_la_pantalla_de_acceso)
        *   [5.6.3 Apagar el sonido](#Apagar_el_sonido)
        *   [5.6.4 Hacer interactivo el botón de encendido](#Hacer_interactivo_el_bot.C3.B3n_de_encendido)
        *   [5.6.5 Distribución del teclado GDM](#Distribuci.C3.B3n_del_teclado_GDM)
    *   [5.7 Gestión de energía](#Gesti.C3.B3n_de_energ.C3.ADa)
        *   [5.7.1 Evitar suspender en la RAM (S3) al cerrar la tapa](#Evitar_suspender_en_la_RAM_.28S3.29_al_cerrar_la_tapa)
        *   [5.7.2 Sin reacción al cerrar la tapa](#Sin_reacci.C3.B3n_al_cerrar_la_tapa)
        *   [5.7.3 Cambiar la acción del nivel de batería crítico (para portátiles)](#Cambiar_la_acci.C3.B3n_del_nivel_de_bater.C3.ADa_cr.C3.ADtico_.28para_port.C3.A1tiles.29)
    *   [5.8 Otros consejos](#Otros_consejos)
*   [6 Ajustes diversos](#Ajustes_diversos)
    *   [6.1 Revertir el comportamiento de la barra de desplazamiento](#Revertir_el_comportamiento_de_la_barra_de_desplazamiento)
    *   [6.2 Lanzar programas automáticamente al iniciar sesión](#Lanzar_programas_autom.C3.A1ticamente_al_iniciar_sesi.C3.B3n)
    *   [6.3 Editar el menú de aplicaciones](#Editar_el_men.C3.BA_de_aplicaciones)
    *   [6.4 Algunas «configuraciones del sistema» no permanecen](#Algunas_.C2.ABconfiguraciones_del_sistema.C2.BB_no_permanecen)
    *   [6.5 Borde interno en el Terminal de Gnome](#Borde_interno_en_el_Terminal_de_Gnome)
    *   [6.6 Desactivar el cursor intermitente en la Terminal](#Desactivar_el_cursor_intermitente_en_la_Terminal)
    *   [6.7 Hacer nuevas pestañas que hereden los directorios en curso presentes en el Terminal de Gnome (3.8+)](#Hacer_nuevas_pesta.C3.B1as_que_hereden_los_directorios_en_curso_presentes_en_el_Terminal_de_Gnome_.283.8.2B.29)
    *   [6.8 Mover ventanas de diálogo](#Mover_ventanas_de_di.C3.A1logo)
    *   [6.9 Mostrar iconos del menú contextual](#Mostrar_iconos_del_men.C3.BA_contextual)
    *   [6.10 Extensiones de GNOME shell](#Extensiones_de_GNOME_shell)
    *   [6.11 Gestor de archivos por defecto/sustituir Nautilus](#Gestor_de_archivos_por_defecto.2Fsustituir_Nautilus)
    *   [6.12 Visor PDF predeterminado](#Visor_PDF_predeterminado)
    *   [6.13 Terminal predeterminado](#Terminal_predeterminado)
    *   [6.14 Aplicaciones predeterminadas](#Aplicaciones_predeterminadas)
    *   [6.15 Navegador web predeterminado](#Navegador_web_predeterminado)
    *   [6.16 Emulación del botón central del ratón](#Emulaci.C3.B3n_del_bot.C3.B3n_central_del_rat.C3.B3n)
    *   [6.17 Atenuar la pantalla](#Atenuar_la_pantalla)
*   [7 Características ocultas](#Caracter.C3.ADsticas_ocultas)
    *   [7.1 Cambiar teclas de acceso rápido](#Cambiar_teclas_de_acceso_r.C3.A1pido)
        *   [7.1.1 Nautilus 3.4 y posterior](#Nautilus_3.4_y_posterior)
    *   [7.2 Grabar lo que visualiza en la pantalla](#Grabar_lo_que_visualiza_en_la_pantalla)
    *   [7.3 Modificar la distribución del teclado con XkbOptions](#Modificar_la_distribuci.C3.B3n_del_teclado_con_XkbOptions)
    *   [7.4 Alternar distribuciones de teclado](#Alternar_distribuciones_de_teclado)
*   [8 Mensajería integrada (Empathy)](#Mensajer.C3.ADa_integrada_.28Empathy.29)
*   [9 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [9.1 No se pueden establecer ajustes en Dconf-Editor](#No_se_pueden_establecer_ajustes_en_Dconf-Editor)
    *   [9.2 Cuando una extensión rompe GNOME](#Cuando_una_extensi.C3.B3n_rompe_GNOME)
    *   [9.3 Las extensiones no funcionan después de actualizar GNOME 3](#Las_extensiones_no_funcionan_despu.C3.A9s_de_actualizar_GNOME_3)
    *   [9.4 La tecla «Windows»](#La_tecla_.C2.ABWindows.C2.BB)
    *   [9.5 Quitar extensiones de Gnome Shell](#Quitar_extensiones_de_Gnome_Shell)
    *   [9.6 Los atajos del teclado no funcionan cuando únicamente se ejecuta conky](#Los_atajos_del_teclado_no_funcionan_cuando_.C3.BAnicamente_se_ejecuta_conky)
    *   [9.7 La nueva ventana se abre detras de otras ventanas cuando se utilizan varios monitores](#La_nueva_ventana_se_abre_detras_de_otras_ventanas_cuando_se_utilizan_varios_monitores)
    *   [9.8 Varios monitores y la extensión dock](#Varios_monitores_y_la_extensi.C3.B3n_dock)
    *   [9.9 Gnome establece la distribución del teclado de EE.UU. después de cada inicio de sesión](#Gnome_establece_la_distribuci.C3.B3n_del_teclado_de_EE.UU._despu.C3.A9s_de_cada_inicio_de_sesi.C3.B3n)
    *   [9.10 El acceso directo «Mostrar Escritorio» no funciona](#El_acceso_directo_.C2.ABMostrar_Escritorio.C2.BB_no_funciona)
    *   [9.11 Nautilus no se inicia](#Nautilus_no_se_inicia)
    *   [9.12 «No se puede aplicar la configuración guardada para los monitores»](#.C2.ABNo_se_puede_aplicar_la_configuraci.C3.B3n_guardada_para_los_monitores.C2.BB)
    *   [9.13 El botón de bloqueo del touchpad falla al reactivarlo](#El_bot.C3.B3n_de_bloqueo_del_touchpad_falla_al_reactivarlo)
    *   [9.14 No es posible conectarse a redes Wi-Fi protegidas](#No_es_posible_conectarse_a_redes_Wi-Fi_protegidas)
    *   [9.15 «Cualquier orden viene definida como 33»](#.C2.ABCualquier_orden_viene_definida_como_33.C2.BB)
    *   [9.16 GDM y GNOME utilizan los cursores de X11](#GDM_y_GNOME_utilizan_los_cursores_de_X11)
    *   [9.17 Tracker & Documentos no enumeran todos los archivos locales](#Tracker_.26_Documentos_no_enumeran_todos_los_archivos_locales)
    *   [9.18 Las contraseñas no se recuerdan](#Las_contrase.C3.B1as_no_se_recuerdan)
    *   [9.19 Las ventanas no se pueden modificar con la tecla Alt + botón del ratón](#Las_ventanas_no_se_pueden_modificar_con_la_tecla_Alt_.2B_bot.C3.B3n_del_rat.C3.B3n)
    *   [9.20 Gnome-shell 3.8.x falla al cargarse con una pantalla en negro + el cursor](#Gnome-shell_3.8.x_falla_al_cargarse_con_una_pantalla_en_negro_.2B_el_cursor)
    *   [9.21 Los elementos de la interfaz de usuario de Gnome 3.10 tienen una escala incorrecta](#Los_elementos_de_la_interfaz_de_usuario_de_Gnome_3.10_tienen_una_escala_incorrecta)
*   [10 Enlaces externos](#Enlaces_externos)

## Introducción

GNOME 3 tiene *dos* interfaces:

*   **GNOME** es la modalidad estándar, con un diseño innovador.

*   **GNOME Classic** es la modalidad con el diseño de escritorio tradicional, similar a la interfaz de usuario de GNOME 2 al tiempo que usa la tecnología de GNOME 3 estándar. Lo hace mediante el uso de extensiones y parámetros preactivados (véase [esto](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) para obtener un listado). Por lo tanto, consiste más en un GNOME Shell personalizado que en una modalidad verdaderamente distinta.

Ambos usan GNOME Shell y el gestor de ventanas Mutter. Mutter actúa como un gestor de composición para el escritorio, empleando aceleración gráfica de hardware para proporcionar efectos dirigidos a reducir el desorden de la pantalla. El gestor de sesiones de GNOME detecta automáticamente si el controlador de vídeo es capaz de ejecutar GNOME Shell y restaura el renderizado de software usando *llvmpipe* cuando es apropiado.

## Instalación

GNOME 3 está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con dos grupos de paquetes:

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) contiene el entorno de escritorio básico y aplicaciones necesarias para la experiencia estándar de GNOME.

*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) contiene varias herramientas opcionales, como un reproductor multimedia, una calculadora, un editor y otras aplicaciones no problemáticas que van bien con el escritorio GNOME. La instalación de este grupo es opcional.

**Nota:** Tenga en cuenta que la instalación únicamente del grupo [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) no instala el grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) como dependencia: si realmente lo quiere todo debe [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") ambos grupos de forma explícita.

### Iniciar GNOME

**Acceso gráfico**

Para una mejor integración con el escritorio es aconsejable el uso del gestor de pantala **GDM**. Pueden ser utilizados otros gestores de inicio de sesión (también conocidos como gestores de pantalla) en lugar de GDM. Eche un vistazo al artículo de la wiki sobre [gestores de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") para saber cómo se inician los entornos de escritorio.

El administrador de inicio de sesión es un proceso limitado, encargado de las tareas imprescindibles para el sistema. El [artículo wiki sobre PolicyKit](/index.php/PolicyKit "PolicyKit") aborda el tema del control de acceso a todo el sistema.

**Sugerencia:** Consulte el artículo [GDM](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)") para instrucciones de instalación y configuración.

**Iniciar GNOME manualmente**

Si prefiere iniciar GNOME manualmente desde la consola, agregue la siguiente línea al archivo `~/.xinitrc`:

 `~/.xinitrc` 
```
exec gnome-session    

```

O `exec gnome-session --session=gnome-classic` para GNOME Classic. Después de modificar `~/.xinitrc`, GNOME se puede iniciar escribiendo `startx`.

Véase [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") para obtener más detalles, por ejemplo, cómo conservar la sesión de logind.

## Usar la shell

### Hoja de trucos y atajos de GNOME

El sitio web de GNOME cuenta con una útil [hoja de trucos y atajos de GNOME Shell](https://live.gnome.org/GnomeShell/CheatSheet) que explica el cambio de tareas, el uso del teclado, el control de las ventanas, el panel, el modo de vista general, y más.

### Reiniciar la shell

Después de realizar modificaciones en la apariencia de gnome mediante tweaks, a menudo se le pedirá que reinicie la shell de GNOME (GNOME shell). Se podría cerrar la sesión y volver a iniciarla, pero es más sencillo y rápido usar la siguiente combinación de teclas: reinicie la shell pulsando `Alt` + `F2`, luego escriba la letra `r` y, finalmente, presione la tecla `Intro`.

### La shell se bloquea

Ciertos ajustes y/o repetidos reinicios de la Shell, pueden hacer que la shell se bloquee cuando se intenta un nuevo reinicio. En este caso, se le informa del error y se le forzará a salir. Algunos cambios de shell, no se pueden lograr a través de un reinicio mediante la combinación del teclado antes descrita, sino que se debe cerrar la sesión y volver a iniciarla para efectuar tal cambio.

Es de sentido común —pero vale la pena repetirlo— que los documentos importantes deben ser guardados (y tal vez cerrados) antes de intentar reiniciar la shell. No es que sea estrictamente necesario; ventanas y documentos abiertos, por lo general, permanecen intactos después de un reinicio de la shell.

### La shell se congela

En algunas ocasiones, las extensiones de GNOME Shell hacen que esta se congele. En este caso, una estrategia posible es cambiar a otro terminal mediante `Ctrl+Alt+F2` o a través de `Ctrl+Alt+F6`, iniciar sesión y reiniciar gnome-shell con:

```
# pkill -HUP gnome-shell

```

Todas las aplicaciones abiertas seguirán estando disponibles después de reiniciar la shell.

A veces, sin embargo, simplemente reiniciar la shell podría no ser suficiente. Entonces será necesario reiniciar X, con lo que perderá todo el trabajo en curso. Puede reiniciar X con la orden:

```
# pkill X

```

GNOME Shell se reiniciará automáticamente.

Si esto no funciona, puede intentar reiniciar el gestor de pantalla. Por ejemplo, si usa GDM, intente:

```
# systemctl restart gdm.service

```

**Sugerencia:** También puede usar **htop** en la tty; pulse *t*, seleccione el árbol *gnome-shell*, pulse *k* y envíe *SIGKILL*.

## Integración de pacman: GNOME PackageKit

GNOME 3 tiene su propia integración GUI con **pacman**: [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit).

El uso del backend **alpm**, es compatible con las siguientes características:

*   Instala y desinstala paquetes desde los repositorios.
*   Refrecar periódicamente la base de datos de los paquetes y el prompt para actualizaciones.
*   Instala paquetes desde tarballs.
*   Búsqueda de paquetes por nombre, descripción, categoría o archivo.
*   Muestra las dependencias del paquete, los archivos y dependencias inversas.
*   Ignora IgnorePkgs y retiene HoldPkgs.
*   Informa de dependencias opcionales, archivos .pacnew, etc.

Puede cambiar la operación `remove` de -Rc a -Rsc estableciendo la clave DConf `org.gnome.packagekit.enable-autoremove`.

### Notificaciones de actualizaciones de paquetes

Si quiere que GNOME compruebe automáticamente si hay actualizaciones, debe [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [gnome-settings-daemon-updates](https://aur.archlinux.org/packages/gnome-settings-daemon-updates/) desde AUR. La dependencia opcional [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome) **es requerida** si ejecuta GNOME como usuario normal.

## Personalizar la apariencia de GNOME

### Apariencia general

GNOME 3 puede haber «empezado desde cero», pero, como la mayoría de los grandes proyectos de software, se ensambla a partir de piezas que datan de diferentes épocas. No hay **una** herramienta de configuración que lo abarque todo. La nueva herramienta: *Configuración del Sistema* es una gran mejora respecto de los paneles de control anteriores. La herramienta *Configuración del Sistema* está bien organizada, pero puede que encuentre que tiene escaso control sobre la apariencia del sistema.

Los instrumentos actuales de configuración se hacen cada vez más familiares: algunos de ellos todavía funcionan; otros muchos no lo harán. Algunos ajustes no están fácilmente expuestos para que pueda modificarlos. Indudablemente, muchos ajustes migrarán a las nuevas herramientas y/o se expondrán a medida que pase el tiempo y la comunidad, en general, adopte y se extienda al último escritorio de GNOME.

#### Gsettings

`gsettings` es una nueva herramienta de línea de órdenes que almacena datos en un formato binario, a diferencia de las herramientas anteriores que utilizaban texto XML. El tutorial [«Customizing the GNOME Shell»](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) explora a fondo el poder de GSettings.

#### GNOME Tweak Tool

Esta herramienta gráfica personaliza tipos de letras, temas, botones en la barra de título y otros ajustes. El paquete [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

#### Temas GTK3 a través de settings.ini

Es posible definir un tema GTK3 en `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` (normalmente `~/.config/gtk-3.0/settings.ini`).

El tema por defecto de GNOME 3, *Adwaita,* es parte del paquete [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard). Otros temas GTK3 se pueden encontrar en [el sitio web Deviantart](http://browse.deviantart.com/customization/skins/linuxutil/desktopenv/gnome/gtk3/). He aquí un ejemplo de configuración:

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
gtk-fallback-icon-theme = gnome
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

Es necesario [reiniciar la shell de GNOME](#Reiniciar_la_shell) para aplicar los ajustes. Más opciones GTK se encuentran en: [Documentación para desarrolladores de GNOME.](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties)

#### Temas para iconos

A partir de la version 3.0.3 de [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), se puede colocar cualquier tema de iconos que se desee utilizar dentro del directorio `~/.icons`.

Provechosamente, GNOME 3 es compatible con temas de iconos de GNOME 2, lo que significa que no hay obligación de usar los iconos por defecto. Para instalar un nuevo conjunto de iconos, copie la carpeta de su tema de iconos deseado en el directorio `~/.icons`. Por ejemplo:

```
$ cp -R /home/user/Desktop/mi_tema_de_iconos ~/.icons

```

El nuevo tema (por ejemplo *mi_tema_de_iconos*) se puede seleccionar usando `gnome-tweak-tool` sobre la entrada *interfaz*.

También, se puede seleccionar textualmente el tema de iconos sin necesidad de gnome-tweak-tool. Agregue el nombre del tema de iconos GTK al archivo `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`. Procure no utilizar `""`, de lo contrario su configuración no se reconocerá.

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
... líneas previas ...

gtk-icon-theme-name = mi_tema_de_iconos
```

### Totem

Para reproducir vídeos h.264, es necesario [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [gst-libav](https://www.archlinux.org/packages/?name=gst-libav)

Para obtener más información sobre la aceleración de hardware de gstreamer, véase [Gstreamer: Hardware Acceleration](/index.php/GStreamer#Hardware_acceleration "GStreamer").

### Panel de GNOME

#### Mostrar fecha en la barra superior

De forma predeterminada, GNOME muestra solo el día de la semana y la hora en la barra superior. Esto se puede cambiar con la siguiente orden. Los cambios surten efecto inmediatamente.

```
# gsettings set org.gnome.desktop.interface clock-show-date true

```

#### Ocultar iconos en la barra superior

Cuando se realiza una instalación de GNOME, algunos iconos no deseados pueden aparecer en el panel. Estos iconos se pueden eliminar utilizando las extensiones de GNOME shell o editando manualmente el script del panel de GNOME.

##### Ocultar iconos con las extensiones shell

Para quitar, por ejemplo, el icono de accesibilidad, se puede utilizar la extensión [https://extensions.gnome.org/extension/112/remove-accesibility/](https://extensions.gnome.org/extension/112/remove-accesibility/).

La mejor manera de utilizar las extensiones es instalándolas desde la página web de gnome extensions como la de arriba.

##### Modificar manualmente el script del panel de GNOME

Para eliminar, por ejemplo, el **icono de acceso universal** comente la línea 'a11y' en PANEL_ITEM_IMPLEMENTATIONS:

 `/usr/share/gnome-shell/js/ui/panel.js` 
```
const PANEL_ITEM_IMPLEMENTATIONS = {
    'activities': ActivitiesButton,
    'appMenu': AppMenuButton,
    'dateMenu': imports.ui.dateMenu.DateMenuButton,
//    'a11y': imports.ui.status.accessibility.ATIndicator,
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'lockScreen': imports.ui.status.lockScreenMenu.Indicator,
    'keyboard': imports.ui.status.keyboard.InputSourceIndicator,
    'powerMenu': imports.gdm.powerMenu.PowerMenuButton,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

A continuación, guarde los cambios y reinicie la shell para ver los resultados:

1.  `Alt+F2`
2.  `r`
3.  `Intro`

#### Mostrar el icono de la batería

Para mostrar el icono de batería en el panel, [instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

#### Eliminar la demora al salir

El siguiente ajuste elimina el cuadro de diálogo de confirmación y, por tanto, los sesenta segundos de retraso para cerrar la sesión.

Este cuadro de diálogo aparece normalmente al cerrar la sesión desde el menú de estado. Este ajuste afecta también el diálogo de ***Apagado***. Esto no es un cambio que afecte a todo el sistema, sino que afecta solo al usuario que lo utiliza. El cambio tiene lugar inmediatamente después de ingresar la siguiente orden:

```
$ gsettings set org.gnome.SessionManager logout-prompt 'false'

```

#### Mostrar el monitor del sistema

Instale la extensión [gnome-shell-system-monitor-applet-git](https://aur.archlinux.org/packages/gnome-shell-system-monitor-applet-git/) disponible en el repositorio [AUR](/index.php/AUR "AUR").

#### Mostrar información meteorológica

Instale la extensión [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

### Vista de actividades

#### Eliminar entradas de la vista de Aplicaciones

Al igual que otros entornos de escritorio, GNOME utiliza archivos .desktop para poblar su vista de Aplicaciones. Estos archivos de texto se encuentran en **`/usr/share/applications`**. No es posible editar estos archivos desde una carpeta visualizada en Nautilus —Nautilus no trata a sus iconos como archivos de texto—. Utilice un terminal para ver o editar las entradas del archivo .desktop.

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

Para que los cambios se apliquen en todo el sistema, modifique los archivos en **`/usr/share/applications`**. Para que los cambios sean locales, realice una copia del archivo *foo.desktop* en la propia carpeta personal.

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

Modifique los archivos .desktop según sus necesidades.

**Nota:** Eliminar archivos con extension .desktop no desinstala una aplicación, sino que elimina su integración en el escritorio: los tipos MIME, accesos directos, etc.

La siguiente orden añade una línea al final de un archivo .desktop que oculta su icono asociado en la vista de Aplicaciones:

```
$ echo "NoDisplay=true" >> foo.desktop

```

#### Quitar lanzadores de Wine desde el menú de Aplicaciones

Vaya a `~/.local/share/applications/wine/Programs/` y busque el nombre de la aplicación wine. En los directorios son los archivos «.desktop» los que configuran los lanzadores. Elimine el directorio del programa para quitar fácilmente los lanzadores.

#### Cambiar el tamaño de los iconos de las aplicaciones

Un desatino de los diseñadores de GNOME fue su selección de iconos muy grandes para la vista de Aplicaciones. Este punto de vista es contraproducente cuando se trabaja con una pantalla pequeña que contiene muchos iconos de aplicaciones grandes. Hay una manera de reducir el tamaño del icono. Se realiza mediante la modificación del tema en GNOME Shell.

Modifique los archivos del sistema directamente (haga una copia de seguridad primero) o copie los archivos de temas en una carpeta local y modifíquelos.

*   Para el tema **predeterminado**, modifique el archivo **`/usr/share/gnome-shell/theme/gnome-shell.css`**

*   Para los **temas de usuario**, modifique el archivo **`/usr/share/themes/<UserTheme>/gnome-shell/gnome-shell.css`**

Edite *gnome-shell.css* y reemplace los siguientes valores. Después, [reinicie la shell de GNOME.](#Reiniciar_la_shell)

 `gnome-shell.css` 
```
 ...
 /* Application Launchers and Grid */

 .icon-grid {
     spacing: 18px;
     -shell-grid-horizontal-item-size: 82px;
     -shell-grid-vertical-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }
 ...

```

#### Cambiar el tamaño de los iconos del menú izquierdo

La vista de actividades de GNOME tiene un menú en el lado izquierdo, donde el tamaño de los iconos en este menú cambia en función de la cantidad de iconos a mostrar. La escala puede ser manipulada o ajustada a un tamaño de icono constante. Para ello, modifique `/usr/share/gnome-shell/js/ui/dash.js`.

 `dash.js` 
```
 ...

        let iconSizes = [ 16, 22, 24, 32, 48, 64 ];

 ...

```

#### Cambiar el tamaño de iconos con el alternador (alt-tab)

GNOME viene con un alternador de tareas donde el tamaño de los iconos de este conmutador de tareas se modifica en función de la cantidad de iconos a mostrar. La escala puede ser manipulada o ajustada a un tamaño de icono constante. Para ello, edite `/usr/share/gnome-shell/js/ui/altTab.js`

 `altTab.js` 
```
 ...

        const iconSizes = [96, 64, 48, 32, 22];

 ...

```

#### Cambiar el tamaño de los iconos de la bandeja del sistema

GNOME viene con una lograda bandeja del sistema, visible cuando el cursor del ratón se mueve sobre la parte inferior de la pantalla. El tamaño de los iconos de esta bandeja se ajusta a un valor fijo de 24\. Para cambiar este valor, edite `/usr/share/gnome-shell/js/ui/messageTray.js`

 `messageTray.js` 
```
 ...

    ICON_SIZE: 24,

 ...

```

#### Desactivar la esquina flotante del menú Actividades

Para desactivar la esquina flotante del menú Actividades cuando el cursor del ratón es ubicado allí, edite `/usr/share/gnome-shell/js/ui/layout.js` (*panel.js* en GNOME 3.0.x) :

 `layout.js` 
```
 this._corner = new Clutter.Rectangle({ name: 'hot-corner',
                                       width: 1,
                                       height: 1,
                                       opacity: 0,
                                       reactive: true });icon-size: 48px;
 }

```

y cambie la opción `reactive` a `false`. GNOME Shell debe ser reiniciado después de este cambio para que surta efecto.

#### Desactivar bandeja de mensajes flotante

La bandeja de mensaje se muestra cuando el puntero del ratón se posa en la parte inferior de la pantalla durante un segundo. Para desactivar este comportamiento, comente la siguiente línea en `/usr/share/gnome-shell/js/ui/messageTray.js`:

 `messageTray.js` 
```
        //pointerWatcher.addWatch(TRAY_DWELL_CHECK_INTERVAL, Lang.bind(this, this._checkTrayDwell));

```

Es necesario reiniciar GNOME Shell. La bandeja de mensajes seguirá siendo visible en la vista de Actividades.

### Barra de titulo

#### Reducir el tamaño de la barra de titulo

*   **Para cambios globales** - edite `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`, busque la opción `title_vertical_pad` y reduzca su valor a `0`.
*   **Para cambios que afecten únicamente al usuario** - copie `/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml` a `/home/$USER/.themes/Adwaita/metacity-1/metacity-theme-3.xml`, después busque la opción `title_vertical_pad` y reduzca su valor a `0`.

Por último, [reinicie GNOME shell.](#Reiniciar_la_shell)

Para reestablecer los valores por defecto, [instale](/index.php/Pacman "Pacman") el paquete [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") o elimine el archivo `/home/$USER/.themes/Adwaita/metacity-1/metacity-theme-3.xml`

#### Reordenar los botones de la barra de titulo

Por el momento esta configuración puede realizarse a traves de **dconf-editor.**

Por ejemplo, movamos el botón cerrar y minimizar hacia el lado izquierdo de la barra de titulo. Abra **dconf-editor** y localice la clave ***org.gnome.shell.overrides.button_layout.*** Cambie su valor a **`close,minimize:`** (Los dos puntos representan el espacio designado entre la izquierda y la derecha de la barra de título). Use cualquier botón en el orden que prefiera. No puede usar mas de un botón a la vez. Además, tenga en cuenta que algunos botones están en desuso. [Reinicie la shell de GNOME](#Reiniciar_la_shell) para ver la nueva disposición de los botones.

#### Ocultar la barra de títulos cuando se maximiza

```
# sed -i -r 's|(<frame_geometry name="max")|\1 has_title="false"|' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[Reinicie la shell de GNOME.](#Reiniciar_la_shell) Después de este arreglo, puede que le resulte difícil desmaximizar una ventana cuando no hay ninguna barra de título donde agarrar.

Con combinaciones de teclas adecuadas, usted debería ser capaz de usar `Alt+F5`, `Alt+F10` o `Alt+Space` para poner remedio a esa situación.

Para prevenir que `metacity-theme-3.xml` sobreescriba el paquete [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) cada vez que se actualice, añada el nombre del paquete a `/etc/pacman.conf` con el parámetro `NoUpgrade`.

 `/etc/pacman.conf` 
```
... líneas previas ...

# Pacman no actualizará los paquetes listados en IgnorePkg y los pertenecientes a IgnoreGroup
# IgnorePkg   =
# IgnoreGroup =

NoUpgrade = usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml    # No añada la primera barra a la ruta

... más líneas ...
```

Para restaurar los valores originales del tema Adwaita, instale el paquete [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard).

### Pantalla de acceso

#### Imagen de fondo de la pantalla de acceso

Una vez que las variables de sesión se han exportado como se explicó anteriormente, puede emitir órdenes para recuperar o establecer elementos usados ​​por GDM.

La forma más fácil de realizar los cambios de configuración es lanzando la interfaz gráfica del «Editor de Configuración» con la siguiente orden:

```
$ dconf-editor

```

La posición de cada configuración es la misma en el estilo de línea de órdenes de configuración que se muestra a continuación:

Lo que sigue es el enfoque de línea de órdenes para recuperar o establecer el nombre del archivo que se utiliza para el wallpaper de GDM.

```
 $  GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri 'file:///usr/share/backgrounds/gnome/SundownDunes.jpg'

 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-options 'zoom'
 ## Valores posibles: centered, none, scaled, spanned, stretched, wallpaper, zoom
```

**Nota:** Debe especificar un archivo que el usuario «gdm» tenga permisos para leer. GDM no puede leer archivos del directorio personal.

Una interfaz gráfica alternativa para cambiar los temas (gtk3, iconos y cursores), fondos de pantalla y otras configuraciones menores de la pantalla de acceso de GDM, puede obtenerla instalando [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/) desde AUR.

#### Fuentes más grandes para la pantalla de acceso

Este ajuste agranda las fuentes del inicio de sesión con un factor de escalada. Es el mismo método empleado por la *Configuracion del acceso universal* en el escritorio.

Debe [exportar las variables de la sesión GDM](#Pantalla_de_acceso) antes de realizar este ajuste.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.interface text-scaling-factor '1.25'

```

#### Apagar el sonido

Este ajuste desactiva (permite no oir) la realimentación acústica que se escucha cuando el volumen del sistema se ajusta (con el teclado) en la pantalla de inicio de sesión. En primer lugar, debe exportar las variables de sesión de GDM.

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds 'false'

```

Si el anterior ajuste no funciona en su caso o no puede exportar las variables de sesión de GDM, hay siempre una solución más fácil para el problema de «sonido preparado»: silenciar o bajar el sonido, mientras se inicia la pantalla de sesión de GDM, usando las teclas multimedia (si están disponibles) de su teclado.

#### Hacer interactivo el botón de encendido

La instalación por defecto establece el botón de encendido para suspender el sistema. ***Apagar*** o ***Mostrar diálogo*** es una mejor opción. En primer lugar, debe exportar las variables de sesión de GDM como se indica [más arriba.](#Pantalla_de_acceso)

```
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-power 'interactive'
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-hibernate 'interactive'
 $ gsettings list-recursively org.gnome.settings-daemon.plugins.power

```

**Advertencia:** Tenga en cuenta que el demonio [acpid](/index.php/Acpid "Acpid") maneja tanto el evento «power button» como «hibernate button» . La ejecución de ambos sistemas al mismo tiempo puede dar lugar a un comportamiento inesperado.

#### Distribución del teclado GDM

GDM no sabe nada de las configuraciones del teclado del escritorio de GNOME 3\. Para cambiar la configuración del teclado usado ​​por GDM, establezca la distribución usando la configuración de Xorg. Remítase a la sección correspondiente de la [Guía para Principiantes.](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)")

### Gestión de energía

#### Evitar suspender en la RAM (S3) al cerrar la tapa

Desde GNOME 3.0 las opciones necesarias se eliminan de la configuración del sistema y desde GNOME 3.6 (compilado para Systemd), incluso las opciones de configuración restantes se eliminan de dconf. El enfoque actual es la gestión de la energía según los criterios de [Systemd](/index.php/Power_management#ACPI_events "Power management"). Cambie la variable **HandleLidSwitch** a **ignore** en `/etc/systemd/logind.conf`

 `/etc/systemd/logind.conf`  `HandleLidSwitch=ignore` 

#### Sin reacción al cerrar la tapa

Al configurar los comportamientos esperados al cerrar la tapa mediante [Systemd#Power management](/index.php/Systemd#Power_management "Systemd"), los ajustes pueden parecer no haber tenido ningún efecto. Si se tiene un monitor externo conectado al portátil, este es el comportamiento por defecto de GNOME. Desconecte el monitor y los ajustes deberían funcionar, de lo contrario el archivo `/etc/systemd/logind.conf` puede estar configurado incorrectamente.

#### Cambiar la acción del nivel de batería crítico (para portátiles)

La interfaz gráfica [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) no tiene una opción: "do nothing" (*«no hacer nada»*) en los portátiles sobren el nivel de batería crítico. Para modificar manualmente esto, abra [dconf](https://www.archlinux.org/packages/?name=dconf)-editor -> org -> gnome -> settings-daemon -> plugins -> power. Modifique la opción "critical-battery-action" al valor "nothing".

### Otros consejos

Véase [GNOME Tips](/index.php/GNOME_Tips "GNOME Tips").

## Ajustes diversos

### Revertir el comportamiento de la barra de desplazamiento

Si no le gusta el nuevo comportamiento de la barra de desplazamiento solo hay que poner `gtk-primary-button-warps-slider = false` en la sección `[Settings]` de `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false
...

```

### Lanzar programas automáticamente al iniciar sesión

Es posible especificar qué programas se inician automáticamente después de conectarse, mediante `gnome-session-properties`. Esta herramienta forma parte del paquete [gnome-session](https://www.archlinux.org/packages/?name=gnome-session).

```
$ gnome-session-properties

```

### Editar el menú de aplicaciones

[gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) proporciona *gmenu-simple-editor* que puede mostrar/ocultar las entradas del menú.

[alacarte](https://www.archlinux.org/packages/?name=alacarte) proporciona un editor del menú más completo para añadir/editar entradas de menú.

### Algunas «configuraciones del sistema» no permanecen

GNOME 3 está usando [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") (un demonio init para Linux) con capacidades más modernas. Anteriormente, los programas de GNOME fueron alterados para utilizar las funcionalidades de inicio de Arch para aglutinar los ajustes, bien fuera por necesidades de mantenimiento requeridas para ello o, posiblemente, se debiera a la transición hacia el nuevo sistema init (leer más sobre esto [aquí](https://bbs.archlinux.org/viewtopic.php?pid=1115208#p1115208)). Las áreas que la configuración no conserva son la **Fecha y Hora** y la adición de perfiles ICC en el menú **Color**, y posiblemente otras.

Para obtener de nuevo la funcionalidad, [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") tiene que estar instalado y los servicios *gdm.service* y *NetworkManager.service* deben ser activados.

### Borde interno en el Terminal de Gnome

Para mover la salida del terminal alejada de los bordes de la ventana cree la hoja de estilo `~/.config/gtk-3.0/gtk.css` con el siguiente ajuste:

```
   TerminalScreen {
     -VteTerminal-inner-border: 10px 10px 10px 10px;
   }

```

### Desactivar el cursor intermitente en la Terminal

Desde Gnome 3.8 y dconf la clave requerida para modificar la desactivación del cursor parpadeante en el terminal difiere ligeramente con respecto a la clave del antiguo gconf. Para desactivar el cursor en Gnome 3.8 utilice:

```
gsettings set org.gnome.desktop.interface cursor-blink false

```

### Hacer nuevas pestañas que hereden los directorios en curso presentes en el Terminal de Gnome (3.8+)

En Gnome 3.8, el comportamiento de cómo se realiza un seguimiento de los directorios actuales ha cambiado. Para restaurar este comportamiento, debe poner esto en el archivo `.bashrc`:

```
   export PS1='\[$(__vte_ps1)\]'$PS1

```

o, para los usuarios de zsh:

```
   chpwd_functions+=(__vte_ps1)

```

### Mover ventanas de diálogo

La configuración predeterminada para los diálogos no le permitirá moverlos porque causa problemas en algunos casos. Para cambiar esta limitación tendrá que usar gconf-editor y modificar esta configuración, como sigue:

```
/desktop/gnome/shell/windows/attach_modal_dialogs

```

Después de la modificación tendrá que reiniciar la shell para que surta efecto.

### Mostrar iconos del menú contextual

Algunos programas tienen iconos de menú de contexto que, sin embargo, están desactivados de forma predeterminada para mostrase en Gnome. Con el fin de mostrarlos establezca `org.gnome.desktop.interface menus-have-icons` a `true`.

### Extensiones de GNOME shell

GNOME Shell se puede personalizar con extensiones. Estas proporcionan características como un dock o un widget para cambiar el tema.

Muchas extensiones son recogidas y auspiciadas por [extensions.gnome.org](https://extensions.gnome.org/). Se pueden realizar búsquedas e instalarlas simplemente activándolas a través del navegador. Más información acerca de las extensiones de la shell de gnome se pueden encontrar [aquí](https://extensions.gnome.org/about/).

Véase [cuando una extensión rompe GNOME](#Cuando_una_extensi.C3.B3n_rompe_GNOME) para información sobre solución de problemas.

### Gestor de archivos por defecto/sustituir Nautilus

Puede engañar a GNOME utilizando otro explorador de archivos mediante la edición de la línea `Exec` en `/usr/share/applications/nautilus.desktop`. Véanse los parámetros correctos en el archivo `.desktop` del administrador de archivos elegido, por ejemplo:

 `/usr/share/applications/nautilus.desktop` 
```
[...]
Exec=thunar %F
O
Exec=pcmanfm %U
O
Exec=nemo %U
[...]
```

### Visor PDF predeterminado

En algunos casos, cuando se ha instalado Inkscape u otros programas gráficos, el Visor de Documentos Evince podría dejar de ser seleccionado como la aplicación PDF predeterminada. Si no está disponible en la entrada **Abrir con**, que sería la solución desde la interfaz gráfica del usuario, se puede utilizar la orden siguiente para que aquel sea la aplicación por defecto.

```
xdg-mime default evince.desktop application/pdf

```

### Terminal predeterminado

`gsettings` (que reemplaza a `gconftool-2`) se utiliza para establecer el terminal predeterminado. El ajuste afecta a **nautilus-open-terminal** (una extensión de Nautilus). Para hacer [urxvt](/index.php/Urxvt "Urxvt") predeterminado, ejecute:

```
gsettings set org.gnome.desktop.default-applications.terminal exec urxvtc
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "'-e'"

```

**Nota:** El flag `-e` es para ejecutar una orden. Cuando *nautilus-open-terminal* invoca `urxvtc`, pone la orden `cd` al final de cada línea de órdenes para que el nueva terminal se inicie en el directorio correcto para abrirlo desde él. Otras terminales requerirán una orden `exec-arg` diferente (tal vez dejarlo vacío) .

### Aplicaciones predeterminadas

Aunque se puede hacer clic con el botón principal sobre cualquier archivo y configurar las aplicaciones por defecto en «Preferencia», los ajustes se guardan realmente en `$HOME/.local/share/applications/mimeapps.list` y `$HOME/.local/share/applications/mimeinfo.cache`

### Navegador web predeterminado

Para configurar el navegador web utilizado por el paquete [gnome-gmail-notifier](https://aur.archlinux.org/packages/gnome-gmail-notifier/) de AUR, abra gconf-editor y modifique la clave `/desktop/gnome/url-handlers/http/`. Es posible que desee cambiar las claves `https/`, `about/` y `unknown/` aprovechando que está editando dicho archivo.

### Emulación del botón central del ratón

Por defecto, GNOME 3 deshabilita la emulación del botón central del ratón, independientemente de la configuración de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") (**Emulate3Buttons**). Para activarlo utilice la siguiente orden:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Atenuar la pantalla

Por defecto, GNOME 3 tiene un tiempo de espera de diez segundos de inactividad para oscurecer la pantalla, independientemente del estado de la batería y AC:

```
gsettings get org.gnome.settings-daemon.plugins.power idle-dim-time

```

Para establecer un tipo de valor nuevo escriba lo siguiente:

```
gsettings set org.gnome.settings-daemon.plugins.power idle-dim-time <int>

```

donde <int> es el valor en segundos.

## Características ocultas

GNOME 3 esconde muchas opciones útiles que se pueden personalizar con **dconf-editor.** GNOME 3 también da soporte a **gconf-editor** para ajustes que aún no han migrado a dconf.

### Cambiar teclas de acceso rápido

Algunas combinaciones de teclas no se pueden cambiar directamente a través de Configuración -> Teclado -> Atajos. Para cambiar estas teclas , utilice dconf-editor. Un ejemplo de particular interés es la combinación de teclas Alt-Above_Tab. En teclados de US, esto es Alt-`: es una combinación de teclas de uso frecuente en el editor [Emacs](/index.php/Emacs "Emacs").Se puede cambiar mediante la apertura de dconf-editor y modificar la clave *switch-group* que se encuentra en `org.gnome.desktop.wm.keybindings`.

Es posible cambiar manualmente las teclas a través del denominado archivo de mapa de aceleración de la aplicación. Dichos archivos acompañan a la correspondiente aplicación: por ejemplo, el de Thunar está en ~/.config/Thunar/accels.scm, mientras que el de Nautilus está localizado en ~/.config/nautilus/accels y ~/.gnome2/accels/nautilus en las versiones antiguas.

El archivo debe contener una lista de posibles combinaciones de teclas, cada línea permanece sin cambios al estar comentada con un punto y coma «;» que tiene que ser eliminado para que se active. Por ejemplo, para sustituir a la tecla de acceso utilizado por Nautilus para mover archivos a la papelera, cambie la línea :

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this :

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerate regularly so don't waist time on commenting the file. The uncommented line will stay but every comment you may add will be lost.

#### Nautilus 3.4 y posterior

En primer lugar, utilice **dconf-editor** para colocar una marca de verificación junto a `can-change-accels` en la clave llamada *org.gnome.desktop.interface.*

Vamos a sustituir la *tecla de acceso directo* —(«hotkey»), también conocido como atajo del teclado o acelerador del teclado— utilizada por Nautilus para mover archivos a la Papelera.

La asignación, por defecto, es un poco incómoda: `Ctrl+Supr`.

*   Abra Nautilus, seleccione cualquier archivo, y haga clic en **Editar** en la barra de menú.
*   Posicione el ratón sobre el elemento del menú *Mover a la Papelera*.
*   Al desplazarse, oprima `Supr`. El atajo actual estará ahora desactivado.
*   Pulse cualquier tecla para crear la nueva clave para el atajo.
*   Presione `Supr` para hacer que el nuevo atajo sea la tecla Suprimir.

Asegúrese de seleccionar un archivo o carpeta, de lo contrario *Mover a la Papelera* será de color gris y no se podrá hacer clic. Por último, desactive nuevamente `can-change-accels` para evitar cambios accidentales con las teclas de acceso rápido.

### Grabar lo que visualiza en la pantalla

Gnome viene con la función *possbility* incorporada para crear [screencasts](https://en.wikipedia.org/wiki/es:Screencast los plugins [gst](https://www.archlinux.org/packages/?name=gst) que son:

```
$ pacman -Qs gst

```

### Modificar la distribución del teclado con XkbOptions

Utilice **dconf-editor**, vaya a la clave denominada *org.gnome.desktop.input-sources.xkb-options* y añada las XkbOptions deseadas (por ejemplo, 'caps:swapescape') a la lista.

Véase `/usr/share/X11/xkb/rules/xorg` para conocer todas las XkbOptions y, luego, `/usr/share/X11/xkb/symbols/*` para conocer sus respectivas descripciones.

**Nota:** Para activar la combinación `Ctrl+Alt+Retroceso` para terminar Xorg, utilice el paquete [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Una vez en Gnome Tweak Tool, navegue a *Escritura > Terminate* y seleccione la opción `Ctrl+Alt+Backspace` del menú desplegable.

### Alternar distribuciones de teclado

Gnome no considera ninguna configuración establecida en `/etc/X11/conf.d/*.conf`, antes bien, tiene que configurar la orden para alternar distribuciones, bien a través de control center con las opciones *Switch to previous source* y *Switch to next source* o bien, si desea utilizar la combinación Alt - Mayús, a través de Gnome-Tweak-Tool donde tendrá que ajustar *Escritura → Modifiers-only input sources → seleccione Alt-shift*. Para más información véase tambien este [hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=152127).

## Mensajería integrada (Empathy)

Empathy, el motor de mensajería integrada, y todos los ajustes del sistema basados en cuentas de mensajería, no se mostrarán a menos que el grupo de paquetes [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) o, al menos, uno de los backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble) o [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), por ejemplo) estén [instalados](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)").

Estos paquetes no están incluidos, por defecto, en la instalación de GNOME que instala Arch. Puede instalar Telepathy y, opcionalmente, algún backends con:

```
# pacman -S telepathy

```

Sin telepathy, Empathy no abrirá el diálogo de administración de cuentas y se puede bloquear en ese estado. Si esto ocurre —incluso después de dejar limpia Empathy— la aplicación `/usr/bin/empathy-accounts` puede permanecer en funcionamiento y tendrá que ser terminada antes de poder agregar nuevas cuentas.

Vea la descripción de los componentes de telepathy en la [Freedesktop.org Telepathy Wiki](http://telepathy.freedesktop.org/wiki/Components).

## Solución de problemas

### No se pueden establecer ajustes en Dconf-Editor

Cuando no se pueden establecer configuraciones en [dconf](https://www.archlinux.org/packages/?name=dconf), es posible que sus configuraciones de usuario dconf estén corruptas. En este caso, lo mejor es borrar los archivos dconf del usuario en ` .config/dconf/user* ` y establecer los ajustes de dconf-editor después.

### Cuando una extensión rompe GNOME

Cuando al habilitar las extensiones de shell provoca la rotura de GNOME, primero debe remover el *user-theme* y *auto-move-windows* desde el directorio de instalación.

El directorio de instalación podría ser uno de los siguientes: **`~/.local/share/gnome‑shell/extensions`** y **`/usr/share/gnome‑shell/extensions`** o **`/usr/local/share/gnome‑shell/extensions`**. La eliminación de estos dos carpetas que contienen la extensión podrá arreglar la ruptura. De lo contrario, procure aislar la extensión que cause el problema con el método del ensayo-error.

La eliminación o adición de una carpeta de extensión que contiene los directorios mencionados, elimina o añade la extensión correspondiente a su sistema. Los detalles sobre las extensiones de GNOME Shell están disponibles en el [sitio web de GNOME.](https://live.gnome.org/GnomeShell/Extensions)

### Las extensiones no funcionan después de actualizar GNOME 3

Busque la carpeta donde se instalan las extensiones. Puede ser **`~/.local/share/gnome-shell/extensions`** o **`/usr/share/gnome-shell/extensions`**.

Edite cada aparición de **`metadata.json`** que exista en cada subcarpeta de la extensión.

| Inserte: | **`"shell-version": ["3.6"]`** |
| en lugar de (por ejemplo): | **`"shell-version": ["3.4"]`** |

**"3.x"** indica que la extensión funciona con todas las versiones de Shell. Si se rompe, usted sabrá donde volver para arreglarlo.

### La tecla «Windows»

De forma predeterminada, este tecla asigna la «tecla de superposición» para lanzar la Vista General. Puede eliminar la asignación de esta tecla para liberar la `tecla de Windows` (también llamada `Mod4`), que GNOME llama `Super_L`, utilizando `gsettings`.

Ejemplo: `gsettings set org.gnome.mutter overlay-key 'Foo';`. Puede omitir **Foo** para remover simplemente cualquier enlace a esa función.

**Nota:** GNOME también usa `Alt+F1` para lanzar la vista general.

### Quitar extensiones de Gnome Shell

Si tiene problemas con la desinstalación de extensiones de Gnome a través [https://extensions.gnome.org/local/](https://extensions.gnome.org/local/), entonces probablemente se han instalado antes como una extensión de todo el sistema con `pacman -S gnome-shell-extensions`. Para quitarlas, hay que tener cuidado, porque la siguiente instrucción elimina todas las extensiones de cualquier usuario, también:

```
`pacman -R gnome-shell-extensions`

```

Después de eso, actualice Gnome Shell pulsando ALT+F2 y escribiendo `restart`

Luego vaya a [https://extensions.gnome.org/local/](https://extensions.gnome.org/local/) de nuevo y eche un vistazo a la lista de extensiones instaladas. Debería haber cambiado.

El resto de extensiones deben ser desmontables pulsando el icono X rojo de la derecha. Si no es así, algo se podría romper.

Como último recurso, se pueden quitar manualmente desde `~/.local/share/gnome-shell/extensions/*` y/o `/usr/share/gnome-shell/extensions`. Reinicie Gnome Shell de nuevo para que surta efecto.

### Los atajos del teclado no funcionan cuando únicamente se ejecuta conky

Los atajos del teclado de gnome-shell como `Alt+F2`, `Alt+F1`, y los atajos de las teclas multimedia, no funcionan si conky es el único programa en ejecución. Sin embargo, si otra aplicación, como gedit, está en marcha, los atajos del teclado funcionan.

Solución: edite .conkyrc

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### La nueva ventana se abre detras de otras ventanas cuando se utilizan varios monitores

Esto es posiblemente un error en GNOME Shell, que hace que las nuevas ventanas se abran detrás de otras. Desmarcando «workspaces_only_on_primary» en `desktop/gnome/shell/windows`, con la utilización de gconf-editor, soluciona este problema.

### Varios monitores y la extensión dock

Si tiene varios monitores configurados con Nvidia TwinView, la extensión dock puede quedar encajonada en medio de los monitores. Usted puede editar el código fuente de esta extensión para cambiar la recolocación de dock a la posición de su elección.

Edite: `/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js` y busque esta línea en la fuente:

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

El primer parámetro es la posición X respecto a la extensión dock en la pantalla, de mondo que restando 15 píxeles en lugar de 2 lo recolocará correctamente en el monitor principal; es posible jugar con cualquier par de coordinadas X,Y para obtener el efecto deseado.

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### Gnome establece la distribución del teclado de EE.UU. después de cada inicio de sesión

Véase [este informe de error](https://bugzilla.redhat.com/show_bug.cgi?id=530452) para obtener más información. Se relaciona con GDM y puede ser reparado con la elección de la correcta distribución en el inicio de sesión de GDM. Sin embargo, los usuarios que no utilizan GDM o utilicen cualquier otro gestor de inicio con un puro enfoque startx, tienen que utilizar una solución. Cree el archivo `~/.keyboard` y hágalo ejecutable con `chmod +x`:

```
# Establecer la distribución correcta del teclado después del inicio de Gnome
setxkbmap -layout "us,pl" -variant altgr-intl -option "grp:alt_shift_toggle" nodeadkeys

```

A continuación, ejecute `gnome-session-properties` y añada este archivo .keyboard a los programas que se ejecutan al inicio:

```
Nombre: Keyboard layout 
Comando: /home/username/.keyboard
Comentario: Establecer la distribución correcta del teclado después del inicio de Gnome

```

Además, es necesario crear el archivo ejecutable `/etc/pm/sleep.d/90_keyboard` con el siguiente contenido a fin de lanzar el script al reanudar desde la suspensión e hibernación.

```
#!/bin/bash
case $1 in
    resume|thaw)
        /home/username/.keyboard
        ;;
esac

```

### El acceso directo «Mostrar Escritorio» no funciona

Los desarrolladores de GNOME han considerado la asociación de botones correspondientes como un error (véase [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609)) ya que la función de minimización está en desuso. Para utilizar de nuevo la función «Mostrar Escritorio», asigne la combinación ALT+STRG+D con el siguiente ajuste:

```
Configuración del sistema --> Teclado --> Atajos --> Navegación --> Ocultar todas las ventanas normales

```

### Nautilus no se inicia

1.  Presione `Alt+F2`
2.  Introduzca `gnome-tweak-tool` y pulse intro.
3.  Seleccione la pestaña *Escritorio*.
4.  Coleque la opción *Hacer que el gestor de archivos gestione el escritorio* y asegúrese que está en **off**.

### «No se puede aplicar la configuración guardada para los monitores»

Si encuentra este mensaje (*«Unable to apply stored configuration for monitors»*), pruebe a desactivar el plugin xrandr de gnome-settings-daemon:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### El botón de bloqueo del touchpad falla al reactivarlo

Algunos portátiles tienen un botón de bloqueo del touchpad que desactiva la pantalla táctil para que los usuarios puedan escribir sin tener que preocuparse por tocar el touchpad. Parece que, aunque actualmente GNOME puede bloquear la pantalla táctil al presionar este botón, no puede volver a activarla. Si el touchpad se queda bloqueado puede hacer lo siguiente para volver a activarlo:

1.  Iniciar un terminal. Puede hacer esto presionando `Alt+F2`, escribiendo `gnome-terminal` y presionando `Intro`.
2.  Escriba en el terminal la siguiente orden:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### No es posible conectarse a redes Wi-Fi protegidas

Es posible que se encuentre en la situación de que puede ver la lista de conexiones de red, pero al elegir una red cifrada no se muestra el cuadro de diálogo para ingresar la clave. Puede que tenga que [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet). Véase [configurar NetworkManager en GNOME](/index.php/NetworkManager_(Espa%C3%B1ol)#GNOME "NetworkManager (Español)").

### «Cualquier orden viene definida como 33»

Cuando se pulsa la tecla `Imprimir Pantalla` (a veces etiquetada como `PrntScr` o `PrtSc`) para tomar una captura de pantalla, y obtiene el mensaje *«Any command has been defined 33»*, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [metacity](https://www.archlinux.org/packages/?name=metacity).

### GDM y GNOME utilizan los cursores de X11

Para solucionar este problema escriba, como root, lo siguiente en `/usr/share/icons/default/index.theme` (creando la carpeta `/usr/share/icons/default` si fuese necesario):

 `/usr/share/icons/default/index.theme` 
```
[Icon Theme]
Inherits=Adwaita

```

**Nota:** En lugar de «Adwaita», puede elegir otro tema para el cursor (por ejemplo, Human).

También puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [gnome-cursors-fix](https://aur.archlinux.org/packages/gnome-cursors-fix/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

### Tracker & Documentos no enumeran todos los archivos locales

Para que Tracker (y, por lo tanto, los Documentos) puedan detectar los archivos locales, los mismos deben ser guardados en carpetas conocidas por ellos. Si sus documentos están contenidos en uno de los directorios estándar de XDG habituales (por ejemplo, «Documentos» o «Música»), debe [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) y ejecutar:

```
 # xdg-user-dirs-update

```

Esto creará todas las carpetas habituales de XDG en su directorio personal, si no existen ya, y generará el archivo de configuración donde definirá estas carpetas de las que Tracker y Documentos dependen.

### Las contraseñas no se recuerdan

Si se recibe una solicitud de contraseña cada vez que se conecta, y se encuentra con que las contraseñas no se guardan, es posible que deba crear/establecer un *«gestor de claves»* por defecto:

```
$ pacman -S seahorse

```

Abra *«Contraseñas y claves»* en el menú o ejecute «seahorse». Seleccione *Ver* → *Mediante Keyring*. Si no hay ningún archivo *keyring* en la columna de la izquierda (que estará marcado con un icono de bloqueo), vaya a *Archivo* → *Nuevo* → *Contraseña de Keyring* y adjudíquele un nombre. Se le pedirá que introduzca una contraseña. Podemos omitir la contraseña, que hará que se desbloquee automáticamente, incluso cuando se utiliza autologin, pero las contraseñas no se guardarán de forma segura. Por último, haga clic en el archivo de claves que acaba de crear y seleccione «Establecer como predeterminado».

### Las ventanas no se pueden modificar con la tecla Alt + botón del ratón

Cambie el dconf-setting *«org.gnome.desktop.wm.preferences.mouse-button-modifier»* de <Super> a <Alt>. No es posible cambiar esto con la *«Configuración del sistema»* → «Teclado» → «Accesos directos», donde encontrará que están presentes solamente las combinaciones de teclas habituales. Los desarrolladores de GNOME decidieron cambiar esto de la versión 3.4 a 3.6 debido a este informe de error [https://bugzilla.gnome.org/show_bug.cgi?id=607797](https://bugzilla.gnome.org/show_bug.cgi?id=607797)

### Gnome-shell 3.8.x falla al cargarse con una pantalla en negro + el cursor

Si tiene activado un idioma sin UTF8, Gnome 3 puede fallar al cargarse. Desactive los locales sin UTF-8 y ejecute locale-gen hasta que esto se resuelva. Para obtener más información, consulte el informe de error: [https://bugzilla.gnome.org/show_bug.cgi?id=698952](https://bugzilla.gnome.org/show_bug.cgi?id=698952)

### Los elementos de la interfaz de usuario de Gnome 3.10 tienen una escala incorrecta

Gnome 3.10 introduce soporte HDPI. Si la información EDID de su monitor no contiene el tamaño correcto de su pantalla, pero la resolución es correcta, esto puede dar lugar a escaladas incorrectas de los elementos de la interfaz de usuario. Para solucionar este problema se puede abrir dconf-editor y localizar la clave `scaling-factor` en `org.gnome.desktop.interface`. Ajústela a 1 para obtener la escala estándar.

## Enlaces externos

*   [Sitio oficial de GNOME](http://www.gnome.org/)
*   [Extensiones para GNOME-shell](http://extensions.gnome.org/)
*   Temas, iconos e imágenes de fondo:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   Programas GTK/GNOME:
    *   [Archivos de GNOME](http://www.gnomefiles.org/)
    *   [Listado de Proyectos de GNOME](http://www.gnome.org/projects/)
Artículos relacionados

*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Oblogout](/index.php/Oblogout "Oblogout")

Openbox es un gestor de ventanas ligero, altamente configurable y con amplia compatibilidad con los estándares. Sus posibilidades están bien documentadas en el [Sitio Web Oficial](http://openbox.org/wiki). Este artículo se referirá a como ejecutar Openbox en Arch Linux.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Actualizando a Openbox 3.5](#Actualizando_a_Openbox_3.5)
*   [3 Openbox Solo](#Openbox_Solo)
*   [4 Openbox como WM junto a otros entornos de escritorio](#Openbox_como_WM_junto_a_otros_entornos_de_escritorio)
    *   [4.1 GNOME](#GNOME)
    *   [4.2 KDE](#KDE)
    *   [4.3 Xfce4](#Xfce4)
*   [5 Configuración](#Configuraci.C3.B3n)
    *   [5.1 Cofiguración Manual](#Cofiguraci.C3.B3n_Manual)
    *   [5.2 ObConf](#ObConf)
    *   [5.3 Personalización de Aplicaciones](#Personalizaci.C3.B3n_de_Aplicaciones)
*   [6 Menús](#Men.C3.BAs)
    *   [6.1 Manualmente](#Manualmente)
    *   [6.2 Iconos en el Menú](#Iconos_en_el_Men.C3.BA)
    *   [6.3 MenuMaker](#MenuMaker)
    *   [6.4 Obmenu](#Obmenu)
        *   [6.4.1 Obm-xdg](#Obm-xdg)
    *   [6.5 openbox-menu](#openbox-menu)
    *   [6.6 Script Menú xdg Basado en Python](#Script_Men.C3.BA_xdg_Basado_en_Python)
    *   [6.7 Generador Automático De Menú](#Generador_Autom.C3.A1tico_De_Men.C3.BA)
    *   [6.8 menús Dinámicos (Pipe menus)](#men.C3.BAs_Din.C3.A1micos_.28Pipe_menus.29)
*   [7 Programas en el arranque](#Programas_en_el_arranque)
    *   [7.1 Habilitar el auto-arranque](#Habilitar_el_auto-arranque)
    *   [7.2 Script de inicio (autostart)](#Script_de_inicio_.28autostart.29)
*   [8 Temas y apariencia](#Temas_y_apariencia)
    *   [8.1 Temas de Openbox](#Temas_de_Openbox)
    *   [8.2 Cursores , Iconos y Fondos de Escritorio](#Cursores_.2C_Iconos_y_Fondos_de_Escritorio)
*   [9 Consejos y trucos](#Consejos_y_trucos)
    *   [9.1 Programas recomendados](#Programas_recomendados)
    *   [9.2 Obtener rápidamente valores xprop para ajustes individualizados](#Obtener_r.C3.A1pidamente_valores_xprop_para_ajustes_individualizados)
    *   [9.3 Ligando el menú a una orden](#Ligando_el_men.C3.BA_a_una_orden)
    *   [9.4 Control de volumen por teclado](#Control_de_volumen_por_teclado)
        *   [9.4.1 Alsa](#Alsa)
        *   [9.4.2 Pulseaudio](#Pulseaudio)
    *   [9.5 Sin teclas multimedia](#Sin_teclas_multimedia)
*   [10 Recursos adicionales](#Recursos_adicionales)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [openbox](https://www.archlinux.org/packages/?name=openbox) disponible desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Una vez instalado, pacman te indicará que copies los archivos `rc.xml`, `rc.xml`, `autostart` y `environment` de la configuración por defecto a `~/.config/openbox/`.

**Note:** haz esto como un usuario normal, no como root.

```
$ mkdir -p ~/.config/openbox
$ cp /etc/xdg/openbox/{rc.xml,menu.xml,autostart, environment} ~/.config/openbox

```

Estos archivos son la base de tu configuración en openbox. Cada archivo apunta a un único aspecto de la configuración y cumplen los siguientes roles:

	`rc.xml` 

	Es el principal archivo de configuración de Openbox. Se utiliza para configurar los atajos de teclado, temas, escritorios virtuales demás propiedades.

	`menu.xml` 

	Controla el menú de aplicaciones de Openbox que aparece al hacer click secundario en el escritorio. [ver la sección menú](#Men.C3.BAs).

	`autostart` 

	Este es el archivo que se lee al iniciar la sesión de openbox. Contiene los programas que se iniciarán con la sesión. típicamente es usado para lanzar páneles/docks, establecer la imagen de fondo o ejecutar scripts al inicio.

	`environment` 

	Este archivo establece las variables del entorno openbox. Cualquier variable establecida será ejcutada en cada inicio de sesión. Usado para iniciar IMEs, exportar módulos de idioma, indicar el directorio por defecto y demás.

## Actualizando a Openbox 3.5

Si has actualizado openbox a su versión 3.5 o superiores, debes tener en cuenta lo siguiente:

*   Hay un nuevo achivo llamado `environment` que deberia ser copiado de /etc/xdg/openbox a ~/.config/openbox.
*   El archivo anteriormente llamado `austart.sh` pasa a llamarse simplemente `austart`, debes renombrarlo.
*   La gramatica en algunas secciones del `rc.xml` han cambiado. Openbox seguirá entendiendo las viejas opciones pero sería aconsejable comparar tu `rc.xml` con el que se encuentra en /etc/xdg/openbox para averiguar los cambios que pueden afectarte.

## Openbox Solo

Para ejecutar Openbox en solitario,(es decir, sin ningún entorno de escritorio) solo tiene que añadir lo siguiente al final de **~/.xinitrc**:

```
exec openbox-session

```

mira [xinitrc](/index.php/Xinitrc "Xinitrc") para mas detalles.

Si usaste otro gestor de ventanas anteriormente (como xfwm) y ahora openbox no inicia después de cerrar la sesión de X, trata moviendo la carpeta autostart:

```
mv ~/.config/autostart ~/.config/autostart.bak

```

**Note:** python2-xdg es requerido para iniciar openbox mediante xdg-autostart.

## Openbox como WM junto a otros entornos de escritorio

Openbox puede ser usado para remplazar el gestor de ventanas en otro Entorno de escritorio.

### GNOME

1.  Si utiliza GDM, seleccione la opción de sesión "GNOME/Openbox"
2.  Si utiliza startx, añada **exec openbox-gnome-session** a ~/.xinitrc
3.  Desde la shell:

```
xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  Si utiliza KDM, seleccione la opción de sesión "KDE/Openbox"
2.  Si utiliza startx, añada **exec openbox-kde-session** a ~/.xinitrc
3.  Desde la the shell:

```
xinit /usr/bin/openbox-kde-session

```

### Xfce4

Ingrese en una sesión normal de Xfce4\. Desde su terminal de preferencia, haga:

```
killall xfwm4 ; openbox & exit

```

Esto matará al proceso xfwm4, ejecutará Openbox, y cerrará el terminal. Salga, asegurándose de marcar la casilla "Guardar sesion para futuros ingresos". En el próximo ingreso, Xfce4 utilizará Openbox como su gestor de ventanas. Para poder salir de la sesión mediante xfce4-session, abra su archivo **~/.config/openbox/menu.xml**.

Busque la entrada:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

y cámbiela a:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Si no lo hace, utilizar la entrada "Exit" del primer nivel del menú provocará que Openbox termine su ejecución, dejándole sin un gestor de ventanas.

Si tiene problemas al cambiar de escritorio virtual con la rueda del ratón, abra su archivo **~/.config/openbox/rc.xml** y cambie de posición las ligaduras del ratón file que tiene acciones tipo "DesktopPrevious" y "DesktopNext" desde el contexto "Desktop" al contexto "Root" (puede que tenga que definir el contexto Root).

Si quiere utilizar el nivel principal del menú de Openbox en vez del que utiliza Xfce, puede terminar el proceso Xfdesktop ejecutando en un terminal la siguiente orden:

```
xfdesktop --quit

```

Por otra parte, Xfdesktop se encarga también del fondo y de los iconos de escritorio, lo que le obliga a utilizar otras utilidades, como por ejemplo ROX, para estas funciones.

(Cuando se termina Xfdesktop, el asunto anterior de los escritorios virtuales deja de ser un problema.)

## Configuración

Actualmente, hay dos opciones para configurar las preferencias esenciales de Openbox:

### Cofiguración Manual

Para configurar manualmente Openbox, tienes que editar **~/.config/openbox/rc.xml**con su editor de texto favorito. El archivo contiene comentarios explicativos,para mas detalles puedes visitar la [OpenBox wiki.](http://openbox.org/wiki/Help:Configuration)

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) es una herramienta de interfaz gráfica para la configuración de Openbox, que puede establecer la mayor parte de las preferencias incluyendo los temas, los escritorios virtuales, las propiedades de ventana y los márgenes del escritorio. Puede ser instalado con el paquete [obconf](https://www.archlinux.org/packages/?name=obconf), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

ObConf no sirve para configurar ni atajos de teclado, ni otras características avanzadas. Para hacer este tipo de modificaciones, debes editar `rc.xml`, alternativamente, puedes utilizar [obkey](https://aur.archlinux.org/packages/obkey/) desde [AUR](/index.php/AUR "AUR").

### Personalización de Aplicaciones

Openbox permite personalización de aplicaciones, permitiendo definir reglas de ejecución. Por ejemplo:

*   Iniciar tu navegador web en un específico escritorio virtual.
*   Abrir una terminal sin decoración de ventana.
*   Hacer que tu cliente de bit-torrent aparezca en determinada posición de la pantalla.

Estas configuraciones se pueden definir en `~/.config/openbox/rc.xml`. Las instrucciones se encuentran en los comentarios del archivo. Mas detalles en la [Openbox wiki](http://openbox.org/wiki/Help:Applications)

## Menús

El menú de Openbox incluye por defecto una serie de aplicaciones para que pueda comenzar, pero tendrá probablemente que personalizarlo hasta cierto punto. Hay varias maneras de hacer esto:

### Manualmente

De manera similar a como se hace con al archivo `rc.xml`, puede editar `~/.config/openbox/menu.xml` con su editor de texto favorito.

### Iconos en el Menú

Desde la versión 3.5.0 puedes tener íconos en las entradas del menú, de la siguiente manera:

*   agrega <showIcons>yes</showIcons> en la sección <menu> del archivo `rc.xml`.
*   edita las entradas del menú en `menu.xml` agregando icons="<path>" así:

```
<menu id="apps-menu" label="Aplicacion" icon="/home/usuario/.icons/applicacion.png">

```

luego ejecuta `openbox --reconfigure` ó `openbox --restart` si el menú no se actualiza adecuadamente.

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) es una poderosa herramienta que que crea menús basados en XML para una serie de gestores de ventana, incluyendo Openbox. MenuMaker buscará los programas ejecutables que estén instalados en su ordenador y creará en menú XML basánodse en los resultados. Se la puede configurar para que excluya lsa viejas aplicaciones de X, o las de GNOME, KDE, y Xfce a gusto del usuario.

MenuMaker está disponible desde el [AUR](https://aur.archlinux.org/packages.php?ID=10894).

Una vez instalado, puede generar un menú completo ejecutando:

```
$ mmaker -v OpenBox3

```

Por defecto, MenuMaker no sobreescribirá un archivo menu.xml anterior. Para hacerlo así, ejecútelo con el argumento -f (force):

```
$ mmaker -vf OpenBox3

```

Para consultar una lista completa de opciones, ejecute **mmaker --help**

Esto le proporcionará un menú bastante completo. Ahora puede modificar el archivo menu.xml a mano, o simplemente regenerar la lista cuando instale nuevo software.

### Obmenu

Obmenu es un editor gráfico para el menu de Openbox. Para todos aquellos que no les gusta mucho enredar con el codigo fuente XML. ésta es probablemente la mejor opción para usted. Se instala mediante el paquete [obmenu](https://www.archlinux.org/packages/?name=obmenu), disponible en los [repositorios oficiales.](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")

Una vez instalado, tan sólo debe ejecutar `obmenu` y añadir o quitar las aplicaciones que se desee.

#### Obm-xdg

`obm-xdg` es una herramienta en línea de comandos que viene con Obmenu. Puede generar un submenú categorizado de las aplicaciones GTK/GNOME instaladas.

Para utilizar obm-xdg, añada la siguiente línea a `~/.config/openbox/menu.xml`:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Ejecute entonces `openbox --reconfigure` para actualizar el menú de Openbox. Debería ver ahora en su menú, un submenú etiquetado como **xdg**.

**Note:** Si no tiene GNOME instalado, deberá instalar entonces el paquete [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) para que funcione obm-xdg.

### openbox-menu

[Openbox-menu](http://mimasgpc.free.fr/openbox-menu_en.html) usa [menu-cache](http://sourceforge.net/projects/lxde/files/menu-cache/) del proyecto LXDE para generar menús para Openbox.

Puede ser instalado con el paquete [openbox-menu](https://aur.archlinux.org/packages/openbox-menu/) vía [AUR](/index.php/AUR "AUR").

Si obtienes un error cuando trates de abrir el menú, intenta [añadir íconos](#Iconos_en_el_Men.C3.BA) al menú de Openbox .

### Script Menú xdg Basado en Python

Este script se encuentra en el paquete de Openbox para Fedora. Solamente debes guardarlo en cualquier lugar y crear una entrada en el menú. La útima versión del script puede [encontrarse aquí](http://pkgs.fedoraproject.org/cgit/openbox.git/tree/xdg-menu%7C).

Descarga el script antes mencionado y guárdalo en el directorio que mas te parezca. Edita el archivo `rc.xml` con tu editor de texto favorito y agrega la siguiente entrada, Por supuesto, puedes cambiar la etiqueta en el parámetro "label":

```
<menu id="apps-menu" label="xdg-menu" execute="python2 /path/to/xdg-menu"/>

```

Guarda el archivo y ejecuta `openbox --reconfigure`.

**Note:** Si no tiene GNOME instalado, deberá instalar entonces el paquete [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) para que funcione obm-xdg.

### Generador Automático De Menú

Sino desea editar el archivo **~/.config/openbox/menu.xml** con los métodos anteriores, puede utilizar la aplicación [obmenugen-bin,](https://aur.archlinux.org/packages.php?ID=27300) (disponible en AUR), para generar las nuevas entradas en el menú. Este utiliza los archivos .desktop para generar el menú. Una vez instalado ejecutar:

```
$ obmenugen               # Crear el nuevo menu
$ openbox --reconfigure   # Para ver el nuevo menu generado

```

### menús Dinámicos (Pipe menus)

Al igual que otros gestores de ventanas, Openbox permite scripts para para crear menús dinámicos, Ejemplos serían : monitores del sistema, controles de reproducción multimedia, o monitores de clima. Ejemplos de menús dinámicos pueden ser encontrados en la página [Openbox:Pipemenus](http://openbox.org/wiki/Openbox:Pipemenus), en el sitio oficial de Openbox.

Algunos scripts interesantes proporcionados por los usuarios de Openbox:

*   **obfilebrowser** — Un menú para navegar entre directorios.

	[http://xyne.archlinux.ca/projects/obfilebrowser/](http://xyne.archlinux.ca/projects/obfilebrowser/) || [obfilebrowser](https://aur.archlinux.org/packages/obfilebrowser/)

*   **obdevicemenu** — Un menú capaz de gestionar dispositivos extraíbles utilizando udisks.

	[https://bbs.archlinux.org/viewtopic.php?id=114702](https://bbs.archlinux.org/viewtopic.php?id=114702) || [obdevicemenu](https://aur.archlinux.org/packages/obdevicemenu/)

## Programas en el arranque

Openbox proporciona la posibilidad de ejecutar diversos programas en el arranque. Esto se consigue por la orden **openbox-session**.

### Habilitar el auto-arranque

Hay dos maneras de habilitar el auto-arranque:

1.  Si utilizas startx para iniciar sesión , edita `~/.xinitrc` y cambi la línea de ***openbox*** a **openbox-session**.
2.  Si utilizas GDM/KDM, selecciona entonces la sesión *Openbox* y se utilizará automáticamente el guión autostart.

### Script de inicio (autostart)

Openbox proporciona un script de inicio de todo el sistema que se aplica a todos los usuarios y se encuentra en `/etc/xdg/openbox/autostart`. Los usuarios también pueden indicar que programas al iniciar sesión creando o editando el archivo `~/.config/openbox/autostart`.

Otras instrucciones están disponibles en [Help:Autostart](http://openbox.org/wiki/Help:Autostart) en el sitio oficial de Openbox.

**Note:** Todos los programas en el archivo autostart deben ser ejecutados como demonios o en segundo plano, de lo contrario los elementos en `/etc/xdg/openbox/autostart` no arrancán.

Openbox también se inicia cualquier archivo *.desktop en la carpeta `/etc/xdg/autostart`. Esto sucede independientemente del script de inicio del usuario. nm-applet, por ejemplo, instala un archivo en esta ubicación, y puede causar que se ejecute dos veces para los usuarios con el habitual `(sleep 3 && / usr / bin / nm-applet - sm-disable)` en su script de inicio. Hay una Discusión acerca de esto [[1]](https://bbs.archlinux.org/viewtopic.php?pid=993738).

## Temas y apariencia

Ver Artículo Principal: [Openbox Themes and Apps (Español)#Temas y Aparencia](/index.php/Openbox_Themes_and_Apps_(Espa%C3%B1ol)#Temas_y_Aparencia "Openbox Themes and Apps (Español)").

### Temas de Openbox

Los temas de Openbox controlan la apariencia de los bordes de ventana, incluyendo la barra del título y sus botones ademas de las notificaciones (OSD). Una serie de temas estan disponibles instalando el paquete [openbox-themes](https://www.archlinux.org/packages/?name=openbox-themes), disponible desde los repositorios oficiales.

[Box-Look](http://www.box-look.org/index.php?xcontentmode=7402) es una gran fuente de recursos para obtener temas de Openbox.

Los temas descargados deberían ser desempaquetados en **~/.themes** y puede ser instalados o seleccionados con la herramienta ObConf.

### Cursores , Iconos y Fondos de Escritorio

Los temas para Xcursor pueden ser instalados con el paquete [xcursor-themes](https://www.archlinux.org/packages/?name=xcursor-themes), otros paquetes como [xcursor-bluecurve](https://www.archlinux.org/packages/?name=xcursor-bluecurve), [xcursor-vanilla-dmz](https://www.archlinux.org/packages/?name=xcursor-vanilla-dmz) ó [xcursor-pinux](https://www.archlinux.org/packages/?name=xcursor-pinux) y muchos otros estan disponibles en los repositorios o vía [AUR](/index.php/AUR "AUR")

Los temas para iconos estan disponibles vía repositorio, por ejemplo [lxde-icon-theme](https://www.archlinux.org/packages/?name=lxde-icon-theme), [tangerine-icon-theme](https://www.archlinux.org/packages/?name=tangerine-icon-theme) ó [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) muchos mas pueden ser encontrados en los repositorios oficiales o en [AUR](/index.php/AUR "AUR")

Los fondos de escritorio pueden ser fácilmente establecidos con herramientas como [Nitrogen](/index.php/Nitrogen_(Espa%C3%B1ol) "Nitrogen (Español)"), [Feh](/index.php/Feh_(Espa%C3%B1ol) "Feh (Español)") or `hsetroot`.

mas información sobre temas de personalización en [Openbox Themes and Apps (Español)](/index.php/Openbox_Themes_and_Apps_(Espa%C3%B1ol) "Openbox Themes and Apps (Español)")

## Consejos y trucos

### Programas recomendados

Ver Artículo Principal: [Openbox Themes and Apps (Español)#Programas Recomendados](/index.php/Openbox_Themes_and_Apps_(Espa%C3%B1ol)#Programas_Recomendados "Openbox Themes and Apps (Español)").

### Obtener rápidamente valores xprop para ajustes individualizados

Si utiliza frecuentemente ajustes individualizados para cada aplicación, podría encontra útil este alias de bash:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

Para utilizarlo, ejecute **xp** y haga click en un programa que esté ejecutándose y para el que quiera definir un ajuste individualizado. El resultado mostrará únicamente la información que requiere Openbox, por ejemplo, los valores de WM_WINDOW_ROLE y de WM_CLASS (nombre y clase):

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

### Ligando el menú a una orden

Podría haber gente que quisiera ligar el menú principal de Openbox, o cualquier otra cosa, a una orden. Esto es útil para crear por ejemplo, un botón de menú en un panel. Aunque Openbox no proporciona esto, un guión muy sencillo, xdotool, puede simular la pulsación de una tecla ejecutando una orden. Xdotool está disponible en AUR [aquí](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Para utilizarlo, sólo tiene que añadir el siguiente código a la sección <keyboard> de su archivo lxde-rc.xml:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Rearranque/reconfigure Openbox. Ahora puede hacer la magia de invocar su menu en la posición del cursor ejecutando la siguiente orden:

```
# xdotool key ctrl+alt+q

```

Por supuesto, puede cambiar la combinación de letras a su gusto.

### Control de volumen por teclado

Para los teclados multimedia es posible habilitar las teclas de control de volumen. Para esto editar el archivo **~/.config/openbox/rc.xml** en la sección <keyboard>, y agregar:

#### Alsa

```
<keybind key="XF86AudioRaiseVolume">
  <action name="Execute">
    <command>amixer set Master 5%+ unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
  <action name="Execute">
    <command>amixer set Master 5%- unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioMute">
  <action name="Execute">
    <command>amixer set Master toggle</command>
  </action>
</keybind>

```

El ejemplo anterior debería funcionar para la mayoría de los teclados multimedia. Debe permitir el subir, bajar y silenciar el Master Control del dispositivo de audio. Nótese también que en este ejemplo:

*   El Silencio debe activar el Master Control si ya está en modo de silencio.
*   El Subir/Bajar el volumen debe activar/desactivar el Master Control cuando se llega a valores limites.

#### Pulseaudio

```
<keybind key="XF86AudioRaiseVolume">
  <action name="Execute">
    <command>amixer -D pulse set Master 5%+ unmute</command>
  </action>
</keybind>
<keybind key="XF86AudioLowerVolume">
  <action name="Execute">
    <command>amixer -D pulse set Master 5%- unmute</command>
  </action>
</keybind>
 <keybind key="XF86AudioMute">
  <action name="Execute">
    <command>amixer set Master toggle</command>
  </action>
</keybind>

```

Esta configuración de teclas deben funcionar para la mayoría de los sistemas. Otros ejemplos se pueden encontrar [aquí](http://ubuntuforums.org/showthread.php?t=987149).

### Sin teclas multimedia

En el caso de que tu teclado no disponga de las teclas multimedia puedes crear combinaciones de teclas para el conol de volumen, por ejemplo:

```
  <keybind key="W-Up">
    <action name="Execute">
      <command>amixer set Master 5%+</command>
    </action>
  </keybind>

```

```
  <keybind key="W-Down">
    <action name="Execute">
      <command>amixer set Master 5%-</command>
    </action>
  </keybind>

```

# Recursos adicionales

*   [Sitio web de Openbox](http://openbox.org/wiki) - El sitio web oficial
*   [Planet Openbox](http://planetob.openmonkey.com/) - Portal de noticias de Openbox
*   [Box-Look.org](http://www.box-look.org/) - Una buena fuente de temas y recursos gráficos
*   [Recomendaciones de aplicaciones](http://archux.com/page/application-recommendations)
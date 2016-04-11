## Contents

*   [1 Introducción a PekWM](#Introducci.C3.B3n_a_PekWM)
*   [2 Instalando PekWM](#Instalando_PekWM)
*   [3 Iniciando PekWM](#Iniciando_PekWM)
    *   [3.1 Método 1: kdm/gdm](#M.C3.A9todo_1:_kdm.2Fgdm)
    *   [3.2 Método 2: xinitrc](#M.C3.A9todo_2:_xinitrc)
*   [4 Configurando PekWM](#Configurando_PekWM)
    *   [4.1 Menús](#Men.C3.BAs)
        *   [4.1.1 MenuMaker](#MenuMaker)
        *   [4.1.2 Manualmente](#Manualmente)
    *   [4.2 Teclas Rápidas](#Teclas_R.C3.A1pidas)
    *   [4.3 Ratón](#Rat.C3.B3n)
    *   [4.4 Programas de inicio](#Programas_de_inicio)
    *   [4.5 Variables](#Variables)
    *   [4.6 Auto propiedades](#Auto_propiedades)
*   [5 Temas](#Temas)
    *   [5.1 Aspecto GTK](#Aspecto_GTK)
*   [6 Estableciendo un Fondo de pantalla](#Estableciendo_un_Fondo_de_pantalla)
*   [7 Problemas Comunes](#Problemas_Comunes)
    *   [7.1 Cuando se utiliza Nvidia TwinView, Las ventanas se maximizan en ambas pantallas](#Cuando_se_utiliza_Nvidia_TwinView.2C_Las_ventanas_se_maximizan_en_ambas_pantallas)
    *   [7.2 Composición/transparencia no funciona correctamente](#Composici.C3.B3n.2Ftransparencia_no_funciona_correctamente)
*   [8 Enlaces Externos](#Enlaces_Externos)

## Introducción a PekWM

[El manejador de ventanas Pek](http://pekwm.org) es desarrollado por Claes Nästen. El código esta basado en el manejador de ventanas [aewm++](/index.php?title=Aewm%2B%2B&action=edit&redlink=1 "Aewm++ (page does not exist)"), pero ha evolucionado lo suficiente que ya no se parece a [aewm++](/index.php?title=Aewm%2B%2B&action=edit&redlink=1 "Aewm++ (page does not exist)") en absoluto. También cuenta con un conjunto ampliado de características, incluyendo el agrupamiento de ventanas (no muy diferente a [ion3](/index.php/Ion3 "Ion3"), [pwm](/index.php?title=Pwm&action=edit&redlink=1 "Pwm (page does not exist)"), o incluso [fluxbox](/index.php/Fluxbox "Fluxbox")), auto propiedades, xinerama, un capturador de teclado que soporta atajos en cadena, y mucho más.

## Instalando PekWM

Instalar PekWM desde los repositorios.

```
pacman -S pekwm

```

## Iniciando PekWM

### Método 1: kdm/gdm

Lo más probable es que luego de instalar se añada automáticamente a la lista de inicio de sesión. Seleccione pekwm desde el menú.

Si no se agrega automáticamente, usted tendrá que crear un archivo .desktop en /usr/share/xsessions llamado Pekwm.desktop.

Cree /usr/share/xsessions/Pekwm.desktop con el siguiente contenido:

```
[Desktop Entry] 
Encoding=UTF-8 
Name=PekWM
Comment=Start PekWM
Exec=/usr/bin/pekwm
Icon= 
Type=Application

```

*Nota:* Para utilizar esto tendrá que tener un **gestor de acceso** habilitado primero. Para obtener instrucciones de cómo hacer eso, mire [aquí](/index.php/Display_manager "Display manager").

### Método 2: xinitrc

En su directorio personal añada el siguiente código a su archivo .xinitrc (~/.xinitrc)

```
exec pekwm

```

## Configurando PekWM

La configuración principal se guarda en el archivo ~/.pekwm/config. Controla todo el resto configuraciones. Controla el espacio de trabajo y las configuraciones de ventanas, el comportamiento del menú y el muelle de aplicaciones, resistencia de las ventanas al borde, y más. Hay un archivo de ejemplo con una documentación completa que se encuentra [here](http://www.pekwm.org/files/pekwm/doc/git/html/config/configfile.html).

### Menús

Cuando se instala PekWM por defecto mediante los repositorios de arch viene con algunos menús pre-creados. Estos no reflejan lo que existe en sus sistema y por tanto es muy probable que sea muy inexacto a lo que realmente tiene instalado. Estos deben de ser vistos como un ejemplo y deberían de ser editados.

Sus menús son almacenados en .pekwm/menu en su directorio home (~/.pekwm/menu)

#### MenuMaker

Una manera de configurar automáticamente los menús para sus aplicaciones instaladas es Menumaker. Para configurar los menús con todas las aplicaciones instaladas, ejecute el siguiente comando::

```
mmaker --no-desktop pekwm

```

**Nota:** Tenga en cuenta que esto no sobrescribirá el archivo del menú existente. Si usted quiere sobrescribir, añada el parámetro -f al comando anterior.

Para ver una lista completa de opciones, ejecute **mmaker --help**

Esto creará un menú muy completo. Ahora puede modificar el menú a mano, o simplemente regenerar la lista siempre que instale un nuevo software.

#### Manualmente

Como había mencionado el archivo del menú esta en ~/.pekwm/menu. La sintaxis para el archivo del menú es bastante sencilla. Una entrada simple tiene la siguiente estructura:

```
Entry = "NOMBRE" { Actions = "Exec COMANDO &" }

```

Un submenú tiene la siguiente sintaxis:

```
Submenu = "NOMBRE" {
     Entry = "NOMBRE" { Actions = "Exec COMANDO &" }
     Entry = "NOMBRE" { Actions = "Exec COMANDO &" }
}

```

(Asegúrese de que los corchetes siempre estén cerrados, o usted tendrá errores y su menú no se mostrará)

Para añadir un separador de línea al menú, utilice lo siguiente:

```
Separator {}

```

PekWM también soporta menús dinámicos. Esto es básicamente entradas del menú o submenús que muestran la salida de un script que se ejecuta cada vez que se accede a la entrada o al submenú.

Usted puede encontrar algunos menús dinámicos en Internet. Compruebe la sintaxis exacta que requiere el menú, ya que puede variar. No hay muchos scripts acerca de menús dinámicos, desafortunamente. Usted puede encontrar menús dinámicos para Gmail y conexiones de red [aquí](http://www.hewphoria.com/?p=submission&type=config), y uno para mostrar la hora y la fecha [aquí](http://urukrama.wordpress.com/2008/01/02/show-the-date-and-time-in-pekwms-menu/). También hay un proyecto llamado [pekwm_menu_tools](http://www.pekwm.org/projects/11) el cual tiene por objeto ser un conjunto de aplicaciones útiles para la generación de menús dinámicos para PekWM.

### Teclas Rápidas

La configuración de las teclas rápidas se almacena en ~/.pekwm/keys. Este archivo controla todos los enlaces y atajos de teclado utilizados en PekWM. Puede añadir atajos de teclado para lanzar aplicaciones o realizar acciones en PekWM, como mostrar un menú, mover una ventana, cambiar de escritorio, etc. Para una lista completa de acciones de PekWM, consulte [la documentación](http://www.pekwm.org/files/pekwm/doc/git/html/config/keys_mouse.html#config-keys_mouse-actions).

Puede tener más de una acción atribuida a una combinación de teclas. Para ello, separe las acciones por un punto y coma. Aquí está un ejemplo:

```
KeyPress = "Ctrl Mod1 R" { Actions = "Exec osdctl -s 'Reconfiguring'; Reload" }

```

Cuando usted pulse Ctrl+Alt+R Pekwm mostrara en la pantalla de texto 'Reconfigurando' (osdctl -s 'Reconfigurando') y reconfigurar (Reload). (Tenga en cuenta que esto requiere que osdsh este instalado)

También puede hacer "cadenas" de teclas, por ejemplo el código

```
Chain = "Ctrl Mod1 C" {
     KeyPress = "Q" { Actions = "MoveToEdge TopLeft" }
     KeyPress = "W" { Actions = "MoveToEdge TopCenterEdge" }
}

```

De manera que si primero presiona Ctrl+Alt+C y después Q mueve la ventana activa a la esquina superior izquierda de la pantalla, y si presiona Ctrl+Alt+C y después W se moverá la ventana a el principio centrado del borde.

### Ratón

La configuración del ratón se guarda en ~/.pekwm/mouse. Este archivo también se explica bastante por si mismo en su diseño. Por ejemplo:

```
FrameTitle {
     ButtonRelease = "1" { Actions = "Raise; Focus" }
}

```

significa que cuando se suelta el botón 1 (generalmente el botón izquierdo del ratón) en el marco del título de una ventana será "elevara" por encima de las otras ventanas y se convertirá en la ventana central.

Una de las cosas que PekWM tiene configurado por defecto es centrar las ventanas cuando el ratón pasa sobre ellas (en contraste con el estilo "click para enfocar"). Esto es una de las cosas que a muy pocos usuarios le gustaría cambiar a la forma más "tradicional". Para cambiar esto, busque las siguientes líneas en el archivo y hacer lo que dice (Esto es poco de lo primero, pero solo es una ocurrencia de la segundo):

```
# Remove the following line if you want to use click to focus.
# Uncomment the following line if windows should raise when clicked.

```

```
# Quitar las siguientes lineas si quiere usar el click con enfoque.
# Descomentar la siguiente línea si desea resaltar las ventanas al hacer clic.

```

### Programas de inicio

El archivo de programas de inicio esta en ~/.pekwm/start. Si desea mostrar una imagen de fondo o un lanzar un panel cuando Pekwm se inicia, puede añadir entradas para esas cosas al archivo. Nota, sin embargo, que estás aplicaciones se ejecutan cada vez que Pekwm se ejecute - incluso cuando se ejecuta "Reiniciar" en el menú raíz. Los comandos se ejecutan sólo después que Pekwm se inicia.

Para agregar una aplicación, utilice la siguiente estructura:

```
nombredelaaplicación &

```

El & es fundamental al final, o nada se ejecutara después. Para darle un ejemplo lo que este archivo podría ser, este es el mío:

```
xfce4-panel &
conky &
hsetroot -fill ~/images/darkwood.jpg &

```

Antes de poder usar este archivo, usted tendrá que hacerlo ejecutable con el siguiente comando:

```
chmod +x ~/.pekwm/start

```

### Variables

El archivo que contiene las variables generales utilizadas en PekWM, la entrada por defecto debería explicarse claramente

```
$TERM="xterm -fn fixed +sb -bg white -fg black"

```

Siempre que la variable $TERM se utiliza en algun archivo de configuración de PekWM, el comando xterm -fn fixed +sb -bg white -fg black will be run. Por ejemplo cambia a:

```
$TERM="urxvt"

```

Significa que urxvt estará cargada por los comandos de terminal.

### Auto propiedades

Si deseas abrir ciertas aplicaciones en determinados espacios de trabajo, tener un cierto título, saltos (ventana) menús, o de manera automática junto con pestañas, puede especificar todo eso aquí. Es probablemente el archivo de configuración más confuso en PekWM, pero también es el archivo más potente. La cantidad de cosas que se pueden establecer en este archivo son demasiadas para ponerlas aquí, pero se explica con detalles en la [página de documentación de autoproperties](http://www.pekwm.org/files/pekwm/doc/git/html/config/autoprops.html). El archivo por defecto es ~/.pekwm/autoproperties también contiene un curso de autopropping.

## Temas

Enlaces a algunos sitios de temas son proporcionados abajo. Para instalar un tema extraer el archivo al directorio de temas los directorios por defecto son:

*   global - /usr/share/pekwm/themes
*   solo usuario - ~/.pekwm/themes

### Aspecto GTK

Para personalizar el aspecto de las aplicaciones GTK puede utilizar [LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance) (disponible en [AUR](https://aur.archlinux.org/packages.php?ID=16047))

## Estableciendo un Fondo de pantalla

Puesto que PekWM es solo un manejador de ventanas, requiere de un programa separado para establecer un fondo de escritorio. Algunos populares son:

*   [feh](/index.php/Feh "Feh")
*   [Nitrogen](/index.php/Nitrogen "Nitrogen")
*   [xli](/index.php?title=Xli&action=edit&redlink=1 "Xli (page does not exist)")
*   [esetroot](/index.php?title=Esetroot&action=edit&redlink=1 "Esetroot (page does not exist)")
*   [hsetroot](/index.php?title=Hsetroot&action=edit&redlink=1 "Hsetroot (page does not exist)")

## Problemas Comunes

### Cuando se utiliza Nvidia TwinView, Las ventanas se maximizan en ambas pantallas

Editar ~/.pekwm/config y buscar la línea:

```
 HonourRandr = "True"

```

y cambialo a:

```
 HonourRandr = "False"

```

[Fuente](https://projects.pekdon.net/projects/pekwm/tasks/124)

### Composición/transparencia no funciona correctamente

Como la v0.1.11, PekWM parece no soportar correctamente composición. Opciones básicas de xcompmgr funcionan, pero docks transparentes, paneles, y sombreado de ventanas no, creando fallos gráficos. Para solucionar esto hay que establecer una transparecia de .999 a cada ventana (o algún otro valor) con devilspie o transset-df, entonces el sombreado de ventadas trabajara normalmente.

Un ejemplo de un script devilspie estableciendo la transparencia a cada ventana a .999 con transset-df:

```
(spawn_async (str "transset-df -i " (window_xid) " .999" ))

```

## Enlaces Externos

*   [Pekwm Homepage](http://pekwm.org/)
*   [Box-Look PekWM Themes](http://box-look.org/index.php?xcontentmode=7403)
*   [Hewphoria PekWM Themes](http://hewphoria.com/?p=submission&type=theme&cat=1)
*   [Freshmeat PekWM Themes](http://themes.freshmeat.net/search/?q=pekwm&section=projects)
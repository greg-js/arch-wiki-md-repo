**Estado de la traducción**
Este artículo es una traducción de [ranger](/index.php/Ranger "Ranger"), revisada por última vez el **2019-12-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Ranger&diff=0&oldid=583919) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")
*   [nnn](/index.php/Nnn "Nnn")
*   [vifm](/index.php/Vifm "Vifm")

[ranger](http://ranger.github.io/) es un administrador de archivos basado en texto, escrito en [Python](/index.php/Python "Python"). Los directorios se muestran en un panel con tres columnas. Moverse entre ellos se logra pulsando teclas, marcadores, el ratón o el historial de órdenes. Las vistas previas de los archivos y el contenido de los directorios se muestran automáticamente con la selección actual.

Las características incluyen: combinaciones de teclas de estilo [vi](/index.php/Vi "Vi"), marcadores, selecciones, etiquetado, pestañas, historial de órdenes, la capacidad de crear enlaces simbólicos, varios modos de consola y una vista de tareas. *ranger* tiene órdenes personalizables y definiciones de teclas, incluidos enlaces a scripts externos. ranger también viene con su propia función de [apertura de archivos](/index.php/File_opener "File opener"), [rifle(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rifle.1). Los competidores más cercanos son [Vifm](/index.php/Vifm "Vifm") y [lf](https://github.com/gokcehan/lf).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Configuración](#Configuración)
    *   [3.1 Mover a la papelera](#Mover_a_la_papelera)
    *   [3.2 Definir órdenes](#Definir_órdenes)
    *   [3.3 Esquemas de color](#Esquemas_de_color)
    *   [3.4 Asociación de archivos](#Asociación_de_archivos)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Archivar](#Archivar)
        *   [4.1.1 Extracción de archivos](#Extracción_de_archivos)
        *   [4.1.2 Compresión](#Compresión)
    *   [4.2 Unidades externas](#Unidades_externas)
    *   [4.3 Archivos ocultos](#Archivos_ocultos)
    *   [4.4 Montar imágenes](#Montar_imágenes)
    *   [4.5 Nueva pestaña en la carpeta actual](#Nueva_pestaña_en_la_carpeta_actual)
    *   [4.6 Vista previa del archivo PDF](#Vista_previa_del_archivo_PDF)
    *   [4.7 Consejos para el intérprete de órdenes](#Consejos_para_el_intérprete_de_órdenes)
        *   [4.7.1 Sincronizar ruta](#Sincronizar_ruta)
        *   [4.7.2 Iniciar un intérprete de órdenes desde ranger](#Iniciar_un_intérprete_de_órdenes_desde_ranger)
            *   [4.7.2.1 Una solución más simple](#Una_solución_más_simple)
        *   [4.7.3 Prevenir instancias de ranger anidadas](#Prevenir_instancias_de_ranger_anidadas)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Alteraciones en la vista previa de imágenes](#Alteraciones_en_la_vista_previa_de_imágenes)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [ranger](https://www.archlinux.org/packages/?name=ranger), o [ranger-git](https://aur.archlinux.org/packages/ranger-git/) para la versión de desarrollo.

## Utilización

Para iniciar ranger, lance un [terminal](/index.php/List_of_applications#Terminal_emulators "List of applications") e invoque `ranger`.

<caption></caption>
| Clave | Orden |
| `?` | Abre el manual o enumera las combinaciones de teclas, órdenes y configuraciones |
| `l`, `Intro` | Lanza archivos |
| `j`, `k` | Selecciona archivos en el directorio actual |
| `h`, `l` | Viaja arriba y abajo en el árbol de directorios |

## Configuración

Después de iniciarse, ranger crea un directorio `~/.config/ranger`.Para copiar la configuración predeterminada a este directorio, emita la siguiente orden:

```
$ ranger --copy-config=all

```

*   `rc.conf` — órdenes de inicio y combinaciones de teclas.
*   `commands.py` — órdenes que se inician con `:`.
*   `rifle.conf` — aplicaciones que se utilizan cuando se lanza un tipo de archivo determinado.

`rc.conf` solo necesita incluir cambios desde el archivo predeterminado, ya que ambos están cargados. Para `commands.py`, si no incluye el archivo íntegro, coloque esta línea en la parte superior:

```
from ranger.api.commands import *

```

Vea [ranger(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ranger.1) para conocer la configuración general.

### Mover a la papelera

Para agregar una combinación de teclas que mueva archivos a su directorio de reciclaje `~/.local/share/Trash/files/` con `DD`, añada a `~/.config/ranger/rc.conf`:

```
map DD shell mv %s /home/${USER}/.local/share/Trash/files/

```

Alternativamente, use la herramienta de línea de órdenes GIO proporcionada por el paquete [glib2](https://www.archlinux.org/packages/?name=glib2):

```
map DD shell gio trash %s

```

La inspección y el vaciado de la «papelera» normalmente son compatibles con los administradores de archivos gráficos como [nautilus](https://www.archlinux.org/packages/?name=nautilus), pero también puede ver la papelera con la orden `gio list trash://`, y vaciarla con: `gio trash --empty`.

### Definir órdenes

Continuando con el ejemplo anterior, añada la siguiente entrada a `~/.config/ranger/commands.py` para vaciar la papelera `~/.Trash`.

```
class empty(Command):
    """:empty

    Empties the trash directory ~/.Trash
    """

    def execute(self):
        self.fm.run("rm -rf /home/myname/.Trash/{*,.[^.]*}")

```

Para usarla, escriba `:empty` e `Intro` con obtener el completado por tabulación según se desee.

**Advertencia:** `[^.]` es una parte esencial de la orden anterior. Sin él, todos los archivos y directorios con el formato `..*` se eliminarán, borrando todo en su directorio de inicio.

### Esquemas de color

ranger viene con cuatro esquemas de color: `default`, `jungle`, `snow` y `solarized`. Puede cambiar su combinación de colores usando:

```
set colorscheme *scheme*

```

Los esquemas de color personalizados se pueden colocar en `~/.config/ranger/colorschemes`.

### Asociación de archivos

ranger usa su propio lanzador de archivos llamado `rifle`. Está configurado en `~/.config/ranger/rifle.conf`. Ejecute `ranger --copy-config=rifle`, si no existe. Por ejemplo, la siguiente línea hace que [kile](https://www.archlinux.org/packages/?name=kile) sea el programa predeterminado para archivos tex:

```
ext tex = kile "$@"

```

Para abrir todos los archivos con [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), asegúrese de que `$EDITOR` y `$PAGER` estén configurados y añadidos:

```
else = xdg-open "$1"
label editor = "$EDITOR" -- "$@"
label pager  = "$PAGER" -- "$@"

```

## Consejos y trucos

### Archivar

Estas órdenes usan [atool](https://www.archlinux.org/packages/?name=atool) para realizar operaciones de archivo.

#### Extracción de archivos

La siguiente orden implementa la extracción de archivos copiando (yy) uno o más archivos y luego ejecutando `:extracthere` en el directorio deseado.

```
import os
from ranger.core.loader import CommandLoader

class extracthere(Command):
    def execute(self):
        """ Extract copied files to current directory """
        copied_files = tuple(self.fm.copy_buffer)

        if not copied_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        one_file = copied_files[0]
        cwd = self.fm.thisdir
        original_path = cwd.path
        au_flags = ['-X', cwd.path]
        au_flags += self.line.split()[1:]
        au_flags += ['-e']

        self.fm.copy_buffer.clear()
        self.fm.cut_buffer = False
        if len(copied_files) == 1:
            descr = "extracting: " + os.path.basename(one_file.path)
        else:
            descr = "extracting files from: " + os.path.basename(one_file.dirname)
        obj = CommandLoader(args=['aunpack'] + au_flags \
                + [f.path for f in copied_files], descr=descr, read=True)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

```

#### Compresión

La siguiente orden permite a los usuarios comprimir varios archivos en el directorio actual marcándolos y luego llamando a `:compress *package name*`. Admite sugerencias de nombres al obtener el nombre base del directorio actual y agregar varias posibilidades para la extensión. Debe tener instalado [atool](https://www.archlinux.org/packages/?name=atool), de lo contrario, verá un mensaje de error cuando cree el archivo comprimido.

```
import os
from ranger.core.loader import CommandLoader

class compress(Command):
    def execute(self):
        """ Compress marked files to current directory """
        cwd = self.fm.thisdir
        marked_files = cwd.get_selection()

        if not marked_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        original_path = cwd.path
        parts = self.line.split()
        au_flags = parts[1:]

        descr = "compressing files in: " + os.path.basename(parts[1])
        obj = CommandLoader(args=['apack'] + au_flags + \
                [os.path.relpath(f.path, cwd.path) for f in marked_files], descr=descr, read=True)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

    def tab(self, tabnum):
        """ Complete with current folder name """

        extension = ['.zip', '.tar.gz', '.rar', '.7z']
        return ['compress ' + os.path.basename(self.fm.thisdir.path) + ext for ext in extension]

```

### Unidades externas

Las unidades externas se pueden montar automáticamente con [udev](/index.php/Udev "Udev") o [udisks](/index.php/Udisks "Udisks"). Unidades montadas en `/media` Se puede acceder fácilmente a las unidades montadas con `gm` (ir a /media).

### Archivos ocultos

Puede alternar la visibilidad de los archivos ocultos con la siguiente orden: `:set show_hidden!`, o utilizar `:set show_hidden true` para hacer visibles los archivos ocultos.

Para hacer esto permanente, agregue dicho ajuste en su archivo de configuración:

 `rc.conf` 
```
set show_hidden true

```

De otro modo, los archivos ocultos se pueden alternar presionando `zh`.

### Montar imágenes

La siguiente orden asume que está utilizando [CDemu](/index.php/CDemu "CDemu") como su montador de imágenes y algún tipo de sistema como [autofs](/index.php/Autofs "Autofs") que monta el disco virtual en una ubicación específica («/media/virtualrom» en este caso). **No olvide cambiar mountpath para reflejar la configuración de su sistema**.

Para montar una imagen (o imágenes) en un disco virtual cdemud desde ranger, seleccione los archivos de imágenes y luego escriba «:mount» en la consola. El montaje puede tardar algo de tiempo dependiendo de su configuración (algunos pueden tardar hasta un minuto), por lo que la orden usa un cargador personalizado que espera hasta que se monte el directorio de montaje y luego lo abre en segundo plano en la pestaña 9.

```
import os, time
from ranger.core.loader import Loadable
from ranger.ext.signals import SignalDispatcher
from ranger.ext.shell_escape import *

class MountLoader(Loadable, SignalDispatcher):
    """
    Wait until a directory is mounted
    """
    def __init__(self, path):
        SignalDispatcher.__init__(self)
        descr = "Waiting for dir '" + path + "' to be mounted"
        Loadable.__init__(self, self.generate(), descr)
        self.path = path

    def generate(self):
        available = False
        while not available:
            try:
                if os.path.ismount(self.path):
                    available = True
            except:
                pass
            yield
            time.sleep(0.03)
        self.signal_emit('after')

class mount(Command):
    def execute(self):
        selected_files = self.fm.thisdir.get_selection()

        if not selected_files:
            return

        space = ' '
        self.fm.execute_command("cdemu -b system unload 0")
        self.fm.execute_command("cdemu -b system load 0 " + \
                space.join([shell_escape(f.path) for f in selected_files]))

        mountpath = "/media/virtualrom/"

        def mount_finished(path):
            currenttab = self.fm.current_tab
            self.fm.tab_open(9, mountpath)
            self.fm.tab_open(currenttab)

        obj = MountLoader(mountpath)
        obj.signal_bind('after', mount_finished)
        self.fm.loader.add(obj)

```

### Nueva pestaña en la carpeta actual

Es posible que haya notado que hay dos métodos abreviados para abrir una nueva pestaña (`g``n` y `Ctrl+n`). Vuelva a vincular `Ctrl+n`:

 `rc.conf` 
```
map <c-n>  eval fm.tab_new('%d')

```

### Vista previa del archivo PDF

Por defecto, ranger previsualizará los archivos PDF como texto. Sin embargo, puede obtener una vista previa de los archivos PDF como una imagen en ranger convirtiendo primero el archivo PDF en una imagen. ranger almacena las vistas previas de imágenes en `~/.cache/ranger/`. Debe crear este directorio manualmente o establecer `preview_images` en `true` en `~/.config/ranger/rc.conf` para indicarle a `ranger` que lo cree automáticamente en el próximo inicio. Sin embargo, tenga en cuenta que `preview_images` no necesita establecerse en `true` todo el tiempo para obtener una vista previa del archivo PDF como imágenes, solo se necesita el directorio `~/.cache/ranger`.

Para activar esta función, descomente las líneas apropiadas en `/usr/share/doc/ranger/config/scope.sh`, o agregue/descomente estas líneas en su archivo local `~/.config/ranger/scope.sh`.

### Consejos para el intérprete de órdenes

#### Sincronizar ruta

ranger proporciona un [función](/index.php/Bash/Functions "Bash/Functions") para el intérprete de órdenes `/usr/share/doc/ranger/examples/bash_automatic_cd.sh`. Ejecute `ranger-cd` en lugar de `ranger` que realizará automáticamente *cd* a la última carpeta examinada.

Si inicia ranger desde un lanzador gráfico (como `$TERMCMD -e ranger`, donde TERMCMD es un terminal de X), no puede usar `ranger-cd`. En su lugar, cree un script ejecutable:

 `ranger-launcher.sh` 
```
#!/bin/sh
export RANGERCD=true
$TERMCMD

```

Y agregue lo siguiente al final de la configuración de su intérprete de órdenes:

 `.*shell*rc` 
```
$RANGERCD && unset RANGERCD && ranger-cd

```

Esto lanzará `ranger-cd` solo si se establece la variable `RANGERCD`. Es importante desarmar (con la función «unset») esta variable nuevamente, de lo contrario, al iniciar otro intérprete de órdenes desde este terminal, se volverá a lanzar automáticamente `ranger`.

#### Iniciar un intérprete de órdenes desde ranger

Con el método anterior, puede cambiar a un intérprete de órdenes en la última ruta explorada simplemente dejando ranger. Sin embargo, es posible que no desee abandonar ranger por varias razones (numerosas pestañas abiertas, copia en progreso, etc.). Puede iniciar otro intérprete de órdenes con (`S` por defecto) sin perder su sesión de ranger. Desafortunadamente, el intérprete de órdenes no cambiará a la carpeta actual automáticamente. Nuevamente, esto se puede resolver con un script ejecutable:

 `shellcd` 
```
#!/bin/sh
export AUTOCD="$(realpath "$1")"

$SHELL

```

y, como antes, agregue esto al final de la configuración del intérprete de órdenes:

 `shellrc` 
```
cd "$AUTOCD"

```

Ahora puede cambiar su enlace del intérprete de órdenes para ranger:

 `rc.conf` 
```
map S shell shellcd %d

```

Alternativamente, puede hacer uso de su archivo de historial del intérprete de órdenes si tiene uno. Por ejemplo, puede hacer esto para [zsh](/index.php/Zsh#Dirstack "Zsh"):

 `shellcd` 
```
## Prepend argument to zsh dirstack.
BUF="$(realpath "$1")
$(grep -v "$(realpath "$1")" "$ZDIRS")"
echo "$BUF" > "$ZDIRS"

zsh

```

Cambie ZDIRS para su dirstack.

##### Una solución más simple

 `rc.conf` 
```
map S shell bash -c "cd %d; bash"

```

Probablemente esto también se pueda adaptar a otras intérpretes de órdenes. En lugar de ejecutar simplemente un intérprete de órdenes (conforme la configuración predeterminada), la solución anterior ejecutará `cd` en un intérprete de órdenes, y luego lanzará un terminal interactivo que no hará que termine inmediatamente para que pueda continuar con lo que quería.

#### Prevenir instancias de ranger anidadas

Puede iniciar un intérprete de órdenes en el directorio actual con `S`, cuando salga del mismo volverá a su instancia de ranger.

Sin embargo, cuando olvida que ya se encuentra en un intérprete de órdenes de ranger y vuelve a iniciar ranger, termina con un ranger que ejecuta un intérprete de órdenes que ejecuta ranger.

Para evitar esto, puede crear la siguiente función en su [archivo de inicio de shell](/index.php/Autostarting#On_shell_login_.2F_logout "Autostarting"):

```
ranger() {
    if [ -z "$RANGER_LEVEL" ]; then
        /usr/bin/ranger "$@"
    else
        exit
    fi
}

```

## Solución de problemas

### Alteraciones en la vista previa de imágenes

Las columnas sin bordes pueden causar rayas en las vistas previas de imágenes. [[1]](https://bbs.linuxdistrocommunity.com/showthread.php?tid=1051). En `~/.config/ranger/rc.conf` establecer:

```
set draw_borders true

```

## Véase también

*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=93025)
*   [DotShare.it configurations](http://dotshare.it/category/fms/ranger/)
*   [GitHub](https://github.com/hut/ranger)
*   [Official User Guide](https://github.com/ranger/ranger/wiki/Official-user-guide)
*   [Installing and using ranger](https://www.digitalocean.com/community/tutorials/installing-and-using-ranger-a-terminal-file-manager-on-a-ubuntu-vps)
*   [Mailing list](https://lists.nongnu.org/mailman/listinfo/ranger-users)
*   [Ranger tutorial](https://bloerg.net/2012/10/17/ranger-file-manager.html)
**Estado de la traducción**
Este artículo es una traducción de [Copying text from a terminal](/index.php/Copying_text_from_a_terminal "Copying text from a terminal"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Copying_text_from_a_terminal&diff=0&oldid=554979) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

La mayoría de los emuladores de terminal maduros permiten a los usuarios copiar o guardar sus contenidos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Enfoque general](#Enfoque_general)
    *   [1.1 Terminales sin selección de PORTAPAPELES](#Terminales_sin_selección_de_PORTAPAPELES)
    *   [1.2 Interceptar la salida de los comandos](#Interceptar_la_salida_de_los_comandos)
    *   [1.3 Acceder al backlog de una terminal Linux](#Acceder_al_backlog_de_una_terminal_Linux)
*   [2 Comparación de emuladores comunes](#Comparación_de_emuladores_comunes)
*   [3 Casos especiales](#Casos_especiales)
    *   [3.1 putty](#putty)
    *   [3.2 urxvt](#urxvt)
    *   [3.3 xterm](#xterm)

## Enfoque general

En los emuladores gráficos de terminal, los contenidos generalmente se seleccionan con el ratón y luego se pueden copiar utilizando el menú contextual, el menú *Editar* o una combinación de teclas como `Ctrl+Shift+C`.

### Terminales sin selección de PORTAPAPELES

Algunos emuladores no admiten la [selección de PORTAPAPELES](/index.php/Clipboard_(Espa%C3%B1ol)#Selecciones "Clipboard (Español)") de manera nativa, y copian los datos a la selección PRIMARIA. Para ellos se puede usar [xclip](https://www.archlinux.org/packages/?name=xclip):

```
$ xclip -o | xclip -selection clipboard -i

```

El comando anterior lee los datos de la selección PRIMARIA y los escribe en la selección PORTAPAPELES.

Otros [gestores de portapapeles](/index.php/Clipboard_(Espa%C3%B1ol)#Gestores "Clipboard (Español)") como [autocutsel](https://www.archlinux.org/packages/?name=autocutsel) proporcionan sincronización automática entre los buffers de selección.

### Interceptar la salida de los comandos

Use [tee](https://en.wikipedia.org/wiki/es:Tee_(Unix) para interceptar la salida de un comando.

```
$ command 2>&1 | archivo de salida tee

```

Después de que se ejecute `command`, `output-file` contendrá su salida.

### Acceder al backlog de una terminal Linux

Se puede acceder al backlog de una terminal nativa llamada `/dev/ttyN` a través de `/dev/vcsN`. Por lo tanto, si uno está trabajando en `/dev/tty1`, el siguiente fragmento de código permitirá almacenar el backlog en un archivo `output-file`:

```
# cat /dev/vcs1 >archivo de salida

```

## Comparación de emuladores comunes

A menos que la columna "Combinación de teclas" indique lo contrario, la combinación de teclas es `Ctrl+Shift+c`.

| Emulador | Seleccionar a PRIMARIO | PORTAPAPELES |
| Combinación de teclas | Menú contextual | Menú de ventana | Seleccionar |
| [aterm](https://aur.archlinux.org/packages/aterm/) | Sí | No | No | No | No |
| [eterm](https://aur.archlinux.org/packages/eterm/) | Sí | No | No | No | No |
| [germinal](https://aur.archlinux.org/packages/germinal/) | Sí | Sí | Sí | No | No |
| [Guake](/index.php/Guake "Guake") | Sí | Sí | Sí | No | No |
| [konsole](https://www.archlinux.org/packages/?name=konsole) | Sí | Sí | Sí | Sí | Opcional |
| [lilyterm-git](https://aur.archlinux.org/packages/lilyterm-git/) | Sí | Sí `Ctrl+Supr` | Sí | No | No |
| [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | Sí | Sí | Sí | Sí | No |
| [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Sí | Sí | Sí | Sí | No |
| [mlterm](https://aur.archlinux.org/packages/mlterm/) | Sí | No | No | No | Sí |
| [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | Sí | Sí | Sí | No | No |
| [PuTTY](/index.php/PuTTY "PuTTY") | Sí | No | No | No | No |
| [qterminal](https://www.archlinux.org/packages/?name=qterminal) | Sí | Sí | Sí | Sí | No |
| [roxterm](https://aur.archlinux.org/packages/roxterm/) | Sí | Sí | Sí | Sí | No |
| [rxvt](https://aur.archlinux.org/packages/rxvt/) | Sí | No | No | No | No |
| [sakura](https://www.archlinux.org/packages/?name=sakura) | Sí | Sí | Sí | Sí | No |
| [st](/index.php/St "St") | Sí | Sí | No | No | No |
| [Terminator](/index.php/Terminator "Terminator") | Sí | Sí | Sí | No | No |
| [terminology](https://www.archlinux.org/packages/?name=terminology) | Sí | Sí | Sí | No | No |
| [Termite](/index.php/Termite "Termite") | Sí | Sí | No | No | No |
| [Tilda](/index.php/Tilda "Tilda") | Sí | Sí | Sí | No | No |
| [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/) | Sí | Sí | No | No | No |
| [urxvt](/index.php/Urxvt "Urxvt") | Sí | Sí `Ctrl+Alt+c` | No | No | Opcional |
| [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | Sí | Sí | Sí | Sí | No |
| [xterm](/index.php/Xterm "Xterm") | Sí | Opcional[[1]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=588785) | No | No | Sí |
| [Yakuake](/index.php/Yakuake "Yakuake") | Sí | Sí | Sí | No | Opcional |

## Casos especiales

### putty

El [enfoque xclip](#Terminales_sin_selección_de_PORTAPAPELES) funciona para *putty*: solo hay que recordar que la invocación *xclip* debe realizarse en el ordenador local (en otra terminal), no en la máquina remota a la que está conectada *putty*.

### urxvt

La selección de texto al PORTAPAPELES requiere la extensión perl `selection-to-clipboard`. Consulte [Rxvt-unicode#Cortar y pegar](/index.php/Rxvt-unicode_(Espa%C3%B1ol)#Copiar_y_pegar "Rxvt-unicode (Español)") para más detalles.

### xterm

El acceso a la selección del PORTAPAPELES en *xterm* requiere [pasos adicionales](/index.php/Xterm#PRIMARY_or_CLIPBOARD "Xterm").
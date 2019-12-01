**Estado de la traducción**
Este artículo es una traducción de [Terminator](/index.php/Terminator "Terminator"), revisada por última vez el **2019-12-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Terminator&diff=0&oldid=590623) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Terminator](http://gnometerminator.blogspot.com/p/introduction.html) es un [emulador de terminal](https://en.wikipedia.org/wiki/es:Emulador_de_terminal "wikipedia:es:Emulador de terminal") que admite pestañas y múltiples paneles de terminales redimensionables en una misma ventana. Se basa en [GNOME terminal](https://en.wikipedia.org/wiki/es:GNOME_Terminal "wikipedia:es:GNOME Terminal").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuration](#Configuration)
    *   [2.1 Personalización GTK](#Personalización_GTK)
*   [3 Órdenes de teclado](#Órdenes_de_teclado)
*   [4 Gestionar perfiles](#Gestionar_perfiles)
    *   [4.1 Arrastrar y soltar](#Arrastrar_y_soltar)
    *   [4.2 Más órdenes de teclado](#Más_órdenes_de_teclado)
*   [5 Véase también](#Véase_también)

## Instalación

[terminator](https://www.archlinux.org/packages/?name=terminator) está disponibles en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Instale [terminator-gtk3-bzr](https://aur.archlinux.org/packages/terminator-gtk3-bzr/) para obtener la última versión (troncal).

## Configuration

Vea la [página del manual](https://en.wikipedia.org/wiki/es:man_(Unix) o haga clic con el botón secundario del ratón en la interfaz de Terminator y luego haga clic en *Preferencias*.

```
man terminator_config

```

La configuración específica del usuario se puede encontrar en `~/.config/terminator/config`.

### Personalización GTK

Terminator admite pestañas. La altura del encabezado de la pestaña a veces se considera demasiado grande. Esto se puede solucionar con la estilización GTK. Desde la versión 1.9 Terminator utiliza GTK 3, de modo que la configuración se puede realizar en `~/.config/gtk-3.0/gtk.css`. Los elementos para personalizar son 'panel de pestaña', 'botón de panel de pestaña' (tenga en cuenta que esto también afecta a otras aplicaciones gtk3).

Ejemplo de configuración:

 `~/.config/gtk-3.0/gtk.css` 
```
notebook tab {
  min-height: 0;
  padding: 2px;
}

notebook tab button {
  min-height: 0;
  min-width: 0;
  padding: 1px;
  margin: 1px;
}

```

## Órdenes de teclado

`F11` Alternar pantalla completa

`Ctrl + Mayús + O` Dividir terminales h**o**rizontalmente

`Ctrl + Mayús + E` Dividir terminales v**e**rticalmente

`Ctrl + Mayús + W` Cerrar el panel actual

`Ctrl + Mayús + T` Abrir nueva pestaña

`Alt + ↑` Moverse al terminal encima del actual

`Alt + ↓` Moverse al terminal debajo del actual

`Alt + ←` Moverse a la terminal a la izquierda de la actual

`Alt + →` Moverse al terminal a la derecha del actual

## Gestionar perfiles

Es posible iniciar Terminator con un perfil aleatorio cada vez. Para evitar comportamientos inesperados, debe comenzar con una sección `[profiles]` limpia. Puede copiar el perfil de este archivo: [http://pastebin.com/gGvYH6zD](http://pastebin.com/gGvYH6zD). Contiene muchos esquemas de color bien conocidos. Copie su contenido en su archivo `config`, que se encuentra en `~/.config/terminator/`. Luego, con la orden `cat` envíe su lista de perfiles al destino de su elección.

```
cat $HOME/.config/terminator/config | grep -B 1 'background_color' | grep '\]\]' | tr -d '[]' > $HOME/.config/terminator/profiles

```

Si agrega más perfiles en el futuro y desea que se incluyan en el grupo de inicio, deberá volver a emitir la orden anterior. Puede crear un [alias](/index.php/Alias "Alias").

Ahora debe modificar el archivo desktop de Terminator para que seleccione un perfil aleatorio de esta lista al inicio.

```
sudoedit /usr/share/applications/terminator.desktop

```

Busque la línea `Exec` y coméntela con un signo almohadilla (`#`). Agregue su propia línea `Exec` de la siguiente manera:

```
# Exec=terminator
Exec=sh -c "terminator -p $( shuf -n 1 $HOME/.config/terminator/profiles )"

```

Guarde el archivo y reinicie su [entorno de escritorio](/index.php/Desktop_environment "Desktop environment").

**Nota:** vaya a las preferencias de Terminador y en la pestaña «Asociaciones de teclas», tome nota de cómo cambiar al siguiente perfil. De esta manera, si el perfil con el que Terminator comenzó no es de su agrado, puede cambiarlo rápidamente.

### Arrastrar y soltar

El diseño se puede modificar moviendo terminales con la función «Arrastrar y soltar».

### Más órdenes de teclado

```
man terminator

```

## Véase también

*   [Terminator](http://gnometerminator.blogspot.com/p/introduction.html) — Sitio oficial
*   [Terminator BZR](http://code.launchpad.net/terminator/) — Código fuente
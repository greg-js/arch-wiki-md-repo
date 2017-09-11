[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) es un [emulador de terminal](/index.php?title=Terminal_Emulator&action=edit&redlink=1 "Terminal Emulator (page does not exist)") altamente configurable derivado de [rxvt](https://en.wikipedia.org/wiki/Rxvt con el fin de minimizar el uso de los recursos del sistema. Desarrollado por Marc Lehmann, algunas de las características más sobresalientes de rxvt-unicode son el soporte de idiomas internacionales a través de [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"), asi como la habilidad de mostrar múltiples tipografias y soporte para extensiones [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl").

## Contents

*   [1 Installación](#Installaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Creaando ~/.Xresources](#Creaando_.7E.2F.Xresources)
        *   [2.1.1 Ejemplo ~/.Xresources #1](#Ejemplo_.7E.2F.Xresources_.231)
        *   [2.1.2 Ejemplo ~/.Xresources #2](#Ejemplo_.7E.2F.Xresources_.232)
*   [3 Consejos & Trucos](#Consejos_.26_Trucos)
    *   [3.1 URIs cliqueables](#URIs_cliqueables)
    *   [3.2 Yankable URIs (Sin Mouse)](#Yankable_URIs_.28Sin_Mouse.29)
    *   [3.3 Copiar y pegar](#Copiar_y_pegar)
        *   [3.3.1 Clipboard Management](#Clipboard_Management)
        *   [3.3.2 Script de gestión automática](#Script_de_gesti.C3.B3n_autom.C3.A1tica)
    *   [3.4 Scrollbar](#Scrollbar)
    *   [3.5 Tabs](#Tabs)
    *   [3.6 Font Declaration Methods](#Font_Declaration_Methods)
    *   [3.7 Improved Kuake-like Behavior in Openbox](#Improved_Kuake-like_Behavior_in_Openbox)
        *   [3.7.1 Scriptlets](#Scriptlets)
        *   [3.7.2 urxvtq with tabbing](#urxvtq_with_tabbing)
            *   [3.7.2.1 Tab control](#Tab_control)
        *   [3.7.3 Openbox configuration](#Openbox_configuration)
        *   [3.7.4 Further configuration](#Further_configuration)
        *   [3.7.5 Related scripts](#Related_scripts)
    *   [3.8 Rxvt-unicode as gmrun terminal](#Rxvt-unicode_as_gmrun_terminal)
    *   [3.9 Improving Performance](#Improving_Performance)
    *   [3.10 Remote Hosts](#Remote_Hosts)
    *   [3.11 True Transparency](#True_Transparency)
*   [4 Problems](#Problems)
    *   [4.1 Transparency not working after upgrade to V9.09](#Transparency_not_working_after_upgrade_to_V9.09)
*   [5 External resources](#External_resources)

## Installación

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) es parte del repositorio [official Arch Linux (extra) repositories](/index.php/Official_repositories "Official repositories")

Install the latest version of rxvt-unicode:

```
# pacman -S rxvt-unicode

```

## Configuración

### Creaando ~/.Xresources

El aspecto y las funciones de rxvt-unicode son especificados en el archivo `.[Xresources](/index.php/Xresources "Xresources")`.

Si usas `startx`, añada este a tu `~/.xinitrc`:

```
xrdb -merge ~/.Xresources

```

**Note:** Command-line arguments override and take precedence over the resource settings established in this file.

Crear si no existe:

```
$ touch ~/.Xresources

```

Todo lo que hay que hacer es introducir los ajustes deseados editanto el archivo.

#### Ejemplo ~/.Xresources #1

[rxvt-unicode Example #1 Screenshot](http://i275.photobucket.com/albums/jj281/adamchrista/Arch%20Linux/Wiki%20Examples/urxvt-man.png)

```
URxvt.buffered:         true
URxvt.background:       black
URxvt.foreground:       white
URxvt.cursorColor:      green
URxvt.underlineColor:   yellow
URxvt.font:             xft:Terminus:pixelsize=14:antialias=false
URxvt.boldFont:         xft:Terminus:bold:pixelsize=14:antialias=false
URxvt.perl-ext-common:  default,tabbed
URxvt.title:            ArchWiki Example

```

Mira la [pagina de referencia de rxvt-unicode](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) para ver una lista completa de ajustes disponibles.

#### Ejemplo ~/.Xresources #2

[rxvt-unicode Example #2 Screenshot](http://nsa14.casimages.com/img/2010/05/08/100508043340911093.png)

```
URxvt.geometry: 400x30 
URxvt.buffered: true
URxvt.background: black
URxvt.foreground: green
URxvt.cursorColor: yellow
URxvt.underlineColor: green
URxvt.font:xft:Bitstream Vera Sans Mono:pixelsize=12:antialias=true

!------------
!True Transparency
!------------
!set to 32-bit for real transparency (compositing required (see xcompmgr)
urxvt*depth:             32
!transparent=0000 opaque=ffff
urxvt*background: rgba:1111/1111/1111/dddd
!urxvt*background: rgba:1111/1111/1111/0000

!------------------
!False tranparency
!------------------
!URxvt.transparent: true
!URxvt.shading: 50 

Urxvt.secondaryScroll:  true    # Enable Shift-PageUp/Down in screen

```

## Consejos & Trucos

### URIs cliqueables

Puedes lograr URIs cliqueables en la terminal si tienes Perl instalado. Por ejemplo, para abrir enlaces en [Firefox](/index.php/Firefox "Firefox") añade lo siguiente a `~/.Xresources`:

```
URxvt.perl-ext-common:  default,matcher
URxvt.urlLauncher:      /usr/bin/firefox
URxvt.matcher.button:   1 

```

**Nota:** En caso de usar otro navegador, cambiar `/usr/bin/firefox` , por `/usr/bin/EXPLORADOR`)

### Yankable URIs (Sin Mouse)

Además, puede seleccionar y abrir direcciones URL en su navegador web, sin necesidad de utilizar el ratón.

Instala el paquete [urxvt-url-select](https://www.archlinux.org/packages/?name=urxvt-url-select) y modifica tu `~.Xresources` como sea necesario. Un ejemplo es el siguiente:

```
URxvt.perl-ext:      default,url-select
URxvt.keysym.M-u:    perl:url-select:select_next
URxvt.urlLauncher:   firefox
URxvt.underlineURLs: true

```

**Nota:** Esta extensión reemplaza el de las URIs cliqueables mencionada anteriormente.

**Comandos de teclado:**

`Alt` + `U` Entrar en modo selección. La última URI en tu pantalla sera seleccionada. Puedes repetir `Alt`+`U` para seleccionar la URI que sigue hacia arriba.

`K` Selecciona la URI por encima

`J` Selecciona la URI por debajo

`Return` Abre la URI seleccionada en el navegador y sale del modo selección

`O` Abre la URI seleccionada sin salir del modo selección

`Y` Copia (yank) la URI seleccionada y sale del modo selección

`Esc` Cancelar modo selección

### Copiar y pegar

Para los usuarios no familiarizados con el modo de transferencia de datos de [Xorg](/index.php/Xorg "Xorg"), el intercambio de información desde y hacia rxvt-unicode puede convertirse en un dolor de cabeza.

#### Clipboard Management

*   [Parcellite](http://parcellite.sourceforge.net/) es un gestor de portapapeles GTK+ que también puede correr en segundo plano como demonio.

*   [autocutsel](http://www.nongnu.org/autocutsel/)provee de interfaz en línea de comandos y demonio para sincronizar los portapapeles.

*   [Glipper](http://glipper.sourceforge.net/) es un applet para el panel de [GNOME](/index.php/GNOME "GNOME") con antiguas versiones que pueden ser usadas en escritorios no GNOME.

*   [Clipman](http://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin) (xfce-clipman-plugin) es un gestor de portapapeles grafico para el panel de [Xfce](/index.php/Xfce "Xfce") (xfpanel).

#### Script de gestión automática

Skottish[[1]](https://bbs.archlinux.org/viewtopic.php?pid=506845#p506845) creó un script en Perl que automáticamente copia cualquier seleccion en urxvt al portapapeles. Guarda lo siguiente como `/usr/lib/urxvt/perl/clipboard`:

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query=quotemeta $_[0]->selection;
    $query=~ s/
/\
/g;
    $query=~ s/\r/\\r/g;
    system( "echo -en " . $query . " | xsel -i -b -p" );
}

```

Xyne creó tambien su propia version del script de Skottish's (el cual esta tambien disponible en el AUR [urxvt-clipboard](https://aur.archlinux.org/packages/urxvt-clipboard/)):

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query = $_[0]->selection;
    open (my $pipe,'|-','xsel -ibp') or die;
    print $pipe $query;
    close $pipe;
}

```

Necessita [xsel](https://www.archlinux.org/packages/?name=xsel) y debe estar habilitado en `*perl-ext-common` o `*perl-ext` en `~/.Xresources`. Por ejemplo:

```
URxvt.perl-ext-common: default,clipboard

```

### Scrollbar

La apariencia de la scrollbar puede ser establecida a través de la siguiente entrada en `~/.Xresources`:

```
! scrollbar style - rxvt (default), plain, next, or xterm
URxvt*scrollstyle:rxvt

```

De las cuales "plain" es la más compacta de todas.

### Tabs

To add tabs to urxvt, add the following to your `~/.Xresources`:

```
URxvt.perl-ext-common:  default,tabbed

```

To control tabs use:

`Shift`+`↓` new tab

`Shift`+`←` go to left tab

`Shift`+`→` go to right tab

`Ctrl`+`←` move tab to the left

`Ctrl`+`→` move tab to the right

`Ctrl`+`D`: close tab

You can change the colors of tabs with the following:

```
URxvt.tabbed.tabbar-fg: 2
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg:    3
URxvt.tabbed.tab-bg:    0

```

Colors must be specified using color indexes: 0 to 15 correspond to your `~/.Xresources` colors, -1 is the background color and -2 is the foreground color. Colors are declared like this:

```
XTerm.color0: #000000
XTerm.color2: #aece92
XTerm.color3: #968a38

```

For named tabs, see [this package in the AUR](https://aur.archlinux.org/packages.php?ID=38990), (Shift+Up: names a tab).

### Font Declaration Methods

```
URxvt.font:            9x15

```

is the same as

```
-misc-fixed-medium-r-normal--15-140-75-75-c-90-iso8859-1

```

and

```
URxvt.font:            9x15bold

```

is the same as

```
URxvt.font:            -misc-fixed-bold-r-normal--15-140-75-75-c-90-iso8859-1

```

The complete list of short names for X core fonts can be found in `/usr/share/fonts/misc/fonts.alias`. (There are also fonts.alias files in some of the other subdirectories of `/usr/share/fonts/`, but as they are packaged separately from the actual fonts, they may list fonts you don't actually have installed.) It is worth noting that these short aliases select for ISO-8859-1 versions of the fonts rather than ISO-10646-1 (Unicode) versions, and 75 DPI rather than 100 DPI versions, so you're probably better off avoiding them and choosing fonts by their full long names instead.

### Improved Kuake-like Behavior in Openbox

This was originally posted on the forum by Xyne and it relies on [xdotool](https://www.archlinux.org/packages/?name=xdotool) which is available in the [Official repositories](/index.php/Official_repositories "Official repositories").

#### Scriptlets

Save this scriptlet from the `urxvtc` man page somewhere on your system as `urxvtc` (e.g., in `~/.config/openbox`):

```
#!/bin/sh
urxvtc "$@"
if [ $? -eq 2 ]; then
   urxvtd -q -o -f
   urxvtc "$@"
fi

```

and save this one as `urxvtq`:

```
#!/bin/bash

wid=$(xdotool search --classname urxvtq)
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 80x28
  wid=$(xdotool search --classname urxvtq | head -1)
  xdotool windowfocus $wid
  xdotool key Control_L+l
else
  if [ -z "$(xdotool search --onlyvisible --classname urxvtq 2>/dev/null)" ]; then
    xdotool windowmap $wid
    xdotool windowfocus $wid
  else
    xdotool windowunmap $wid
  fi
fi

```

A previous version of xdotool introduced a bug which disabled recognition of visible windows and thus led some users to use the following scriptlet in place of the previous one. This is no longer necessary as [xdotool](https://www.archlinux.org/packages/?name=xdotool) >= 1.20100416.2809, but it has been left here for future reference.

```
#!/bin/bash

wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 200x28
  wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
  xdotool windowfocus $wid
  xdotool key Control_L+l
else
  if [ -z "$(xprop -id $wid | grep 'window state: Normal' 2>/dev/null)" ]; then
    xdotool windowmap $wid
    xdotool windowfocus $wid
  else
    xdotool windowunmap $wid
  fi
fi

```

Make sure that you change `/path/to/urxvtc` to the actual path to the `urxvtc` scriptlet that you saved above. We'll be using `urxvtc` to launch both regular instances of `urxvt` and the kuake-like instance.

#### urxvtq with tabbing

If you want to have tabs in your kuake-like `urxvtc` (here called `urxvtq`) just replace the third line in your `urxvtq`:

```
wid=$(xdotool search --name urxvtq)

```

with:

```
wid=$(xdotool search --name urxvtq | grep -m 1 "" )

```

To activate the tab support, you can either replace the fifth line of your `urxvtq`:

```
/path/to/urxvtc -name urxvtq -geometry 80x28

```

with:

```
/path/to/urxvtc -name urxvtq -pe tabbed -geometry 80x28

```

or replace this line of your `.Xresources`:

```
URxvt.perl-ext-common: default,matcher

```

with

```
URxvt.perl-ext-common: default,matcher,tabbed

```

##### Tab control

<SHIFT>-Left: Switch to the tab left of current one

<SHIFT>-Right: Switch to the tab right of current one

<SHIFT>-Down: Create a new tab

You can also use your mouse to switch the tabs by clicking the wished one and create a new tab by clicking on *[NEW].\\*

To close a tab just enter 'exit' like you'll close a terminal.

#### Openbox configuration

Now add the following lines to the `<applications>` section of `~/.config/openbox/rc.xml`:

```
<application name="urxvtq">
   <decor>no</decor>
   <position force="yes">
     <x>center</x>
     <y>0</y>
   </position>
   <desktop>all</desktop>
   <layer>above</layer>
   <skip_pager>yes</skip_pager>
   <skip_taskbar>yes</skip_taskbar>
   <maximized>Horizontal</maximized>
</application>

```

and add these lines to the `<keyboard>` section:

```
<keybind key="W-t">
  <action name="Execute">
    <command>/path/to/urxvtc</command>
  </action>
</keybind>
<keybind key="W-grave">
  <action name="Execute">
    <execute>/path/to/urxvtq</execute>
  </action>
</keybind>

```

Here too you need to change the `/path/to/*` lines to point to the scripts that you saved above. Save the file and then reconfigure Openbox. You should now be able to launch regular instances of urxvt with the Windows/Super key + "**t**", and toggle the kuake-like console with Windows/Super+grave (**`**).

#### Further configuration

The advantage of this configuration over the urxvt kuake perl script is that Openbox provides more keybinding options such as modifier keys. The kuake script hijacks an entire physical key regardless of any modifier combination. Review the [Openbox bindings documentation](http://icculus.org/openbox/index.php/Help:Bindings) for the full range or possibilities.

The [Openbox per-app settings](http://icculus.org/openbox/index.php/Help:Applications) can be used to further configure the behavior of the kuake-like console (e.g. screen position, layer, etc). You may need to change the "geometry" parameter in the `urxvtq` scriptlet to adjust the height of the console.

#### Related scripts

*   hbekel has posted a generalized version of the `urxvtq` [here](https://bbs.archlinux.org/viewtopic.php?pid=550380#p550380) which can be used to toggle any application using `xdotool`.

*   [http://www.jukie.net/~bart/blog/20070503013555](http://www.jukie.net/~bart/blog/20070503013555) - A script for opening url's with your keyboard instead of mouse with urxvt.

### Rxvt-unicode as gmrun terminal

Unlike some other terminals, urxvt expects the arguments to -e to be given separately, rather than grouped together with quotes. This causes trouble with gmrun, which assumes the opposite behavior. This can be worked around by putting an "eval" in front of gmrun's "Terminal" variable in .gmrunrc:

```
Terminal = eval urxvt
TermExec = ${Terminal} -e

```

(gmrun uses /bin/sh to execute commands, so the "eval is understood here.) The "eval" has the side-effect of "breaking up" the argument to -e in the same way $@ does in bash, making the command intelligible to urxvt.

### Improving Performance

*   Avoid the use of Xft fonts. If Xft fonts must be used, append `:antialias=false` to the setting value.

*   Build rxvt-unicode with disabled support for unnecessary features, `--disable-xft` and `--disable-unicode3` in particular.

*   Limit the number of `saveLines` (option `-sl`) in the scrollback buffer to reduce memory usage.

*   Consider running `urxvtd` as a daemon accepting connections from `urxvtc` clients.

### Remote Hosts

If you are logging into a remote host, you may encounter problems when running text-mode programs under rxvt-unicode. This can be fixed by copying `/usr/share/terminfo/r/rxvt-unicode` from your local machine to your host at `~/.terminfo/r/rxvt-unicode`.

### True Transparency

To enable true transparency, make sure you have a WM that supports compositing and a compositing manager installed and enabled, then add the following lines to your `.Xresources` changing the rgba values to whatever color you would like:

```
URxvt.depth: 32
URxvt*background: rgba:0000/0000/0000/cccc

```

## Problems

### Transparency not working after upgrade to V9.09

The rxvt-unicode devs removed compatibility code for a lot of non standard wallpaper setters with this update. Using a non compatible wallpaper setter will break transparency support. Recommended wallpaper setters:

*   [feh](/index.php/Feh "Feh")
*   hsetroot
*   esetroot

To make true transparency work, make sure to comment urxvt*tintColor and urxvt*inheritPixmap.

## External resources

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Official site
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Official FAQ
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Official manual page
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Official Perl extension reference
*   [urxvt(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/urxvt.1)
# echinus

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [dmenu](/index.php/Dmenu "Dmenu")

[echinus](http://plhk.ru/) is a simple and lightweight tiling and floating window manager for X11\. Started as a [dwm](/index.php/Dwm "Dwm") fork with easier configuration, echinus became a full-featured reparenting window manager with [EWMH](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html) support.

Unlike dwm, echinus does not need to be re-compiled after changes have been made to the config. It supports [Xft](http://www.freedesktop.org/wiki/Software/Xft) (freetype) out of the box and has the option of configurable titlebars.

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 Rules](#Rules)
*   [3 Starting echinus](#Starting_echinus)
*   [4 Using echinus](#Using_echinus)
    *   [4.1 Panels & Pagers](#Panels_.26_Pagers)
*   [5 Resources](#Resources)
    *   [5.1 Screenshots](#Screenshots)

## Installing

[Install](/index.php/Install "Install") [echinus](https://aur.archlinux.org/packages/echinus/)<sup><small>AUR</small></sup>. You might also want to install [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>, a lightweight EWMH taskbar, originally designed for echinus (also in AUR), and [dmenu](http://tools.suckless.org/dmenu/).

After successfully installing, copy all files from `/etc/xdg/echinus` to `~/.echinus`(for user).

## Configuring

echinus is configured in one simple text file, in Xresources format: `~/.echinus/echinusrc`. Details for all of the configuration options are in `/usr/share/doc/echinus/README`. A section of a sample config file looks like:

```
Echinus*selected.border: #404040
Echinus*selected.button: #d3d7cf
Echinus*selected.bg: #262626
Echinus*selected.fg: #d3d7cf

```

### Rules

Rules can be set up to spawn applications in specific tags. The following rule, for example, would open firefox in the "web" tag:

```
Echinus*rule0: firefox.* web 0 1

```

Opening applications in a terminal requires that you explicitly set the -title tag when spawning them so that echinus can manage them:

```
Echinus*spawn0: CA + m = urxvtc -title mutt -e mutt

```

Similarly, when spawning [dmenu](/index.php/Dmenu "Dmenu"), you will need to declare the requisite properties, like so:

```
Echinus*spawn1: Menu = dmenu_run -fn "-*-dina-medium-r-*-*-*-100-*-*-*-*-*-*" -nb "#1A1A1A" -nf "#696969" -sb "#1A1A1A" -sf "#D3D7Cf"

```

## Starting echinus

To start echinus with `startx` or the [SLiM](/index.php/SLiM "SLiM") login manager, simply append the following to `~/.xinitrc`:

```
exec echinus

```

## Using echinus

After making changes to `echinusrc`, you can reload the config without recompiling by restarting echinus, with `Alt` + `Shift` + `q`. This keybinding, and any other, can be customized to suit your preference or muscle-memory.

Further details for manipulating windows are in the manpage and the `README`.

### Panels & Pagers

echinus supports some parts of EWMH - the following are known to work:

*   [tint2](/index.php/Tint2 "Tint2")
*   [fbpanel](http://fbpanel.sourceforge.net/)
*   [ipager](http://useperl.ru/ipager/index.en.html)
*   [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>

## Resources

*   [echinus website](http://plhk.ru/)
*   [GitHub repository](https://github.com/polachok/echinus)

### Screenshots

*   [http://www.flickr.com/photos/jasonwryan/5270660692/lightbox/](http://www.flickr.com/photos/jasonwryan/5270660692/lightbox/)
*   [http://plhk.ru/gallery/echinus-0.4.6.png](http://plhk.ru/gallery/echinus-0.4.6.png)
*   [http://plhk.ru/gallery/profont.png](http://plhk.ru/gallery/profont.png)
*   [http://plhk.ru/gallery/echinus027.png](http://plhk.ru/gallery/echinus027.png)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Echinus&oldid=410328](https://wiki.archlinux.org/index.php?title=Echinus&oldid=410328)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")
[D-Bus](https://en.wikipedia.org/wiki/D-Bus "wikipedia:D-Bus") je software poskytující aplikacím jednoduchý způsob jak vzájemně komunikovat. Skládá se z démona, který může být spuštěn jak v rámci celého systému, tak v rámci uživatelských sezení, a sady knihoven umožňující aplikacím D-Bus využívat.

## Instalace

[dbus](https://www.archlinux.org/packages/?name=dbus) může být nainstalován z [core]. Vzhledem k tomu, že je D-Bus vyžádován poměrně velkým počtem aplikací, je lepší ho mít nainstalovaný.

Pro ruční spuštění vizte [instrukce v článku o démonech](/index.php/Daemon_(%C4%8Cesky)#Ruční_spouštění_a_zastavování "Daemon (Česky)"). Můžete si ho také přidat do [seznamu démonů](/index.php/Daemon_(%C4%8Cesky)#Spouštění_po_startu "Daemon (Česky)") v `/etc/rc.conf`, aby se spouštěl automaticky při bootování.

## Spuštění uživatelského sezení

[gnome-session](/index.php/GNOME_(%C4%8Cesky) "GNOME (Česky)"), [startkde](/index.php/KDE_(%C4%8Cesky) "KDE (Česky)") a [startxfce4](/index.php/Xfce_(%C4%8Cesky) "Xfce (Česky)") spouští D-Bus sezení automaticky, pokud už neběží. Šablona pro `~/.xinitrc` (`/etc/skel/.xinitrc`) udělá to samé jako skripty v `/etc/X11/xinit/xinitrc.d/`. Ujistěte se, že je tento kód obsažen ve vašem [~/.xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
#!/bin/sh

# Source scripts in /etc/X11/xinit/xinitrc.d/
if [ -d /etc/X11/xinit/xinitrc.d ]; then
    for f in /etc/X11/xinit/xinitrc.d/*; do
        [ -x "$f" ] && . "$f"
    done
    unset f
fi

exec $your_window_manager

```

## Viz také

*   [Stránky D-Bus na freedesktop.org](http://www.freedesktop.org/wiki/Software/dbus)
*   [Úvod do D-Bus](http://www.freedesktop.org/wiki/IntroductionToDBus) na freedesktop.org
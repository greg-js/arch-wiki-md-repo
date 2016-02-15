Tento článek popisuje konfiguraci témat GTK+ aplikací. GTK+ (GIMP Toolkit) je multiplatformní knihovna pro tvorbu grafických uživatelských rozhraní, původně stvořená pro [gimp](https://www.archlinux.org/packages/?name=gimp), ale v současnosti velmi oblíbená s bindingy pro mnoho programovacích jazyků. Tento článek prozkoumává nástroje pro konfigurací GTK+ témat, stylu, ikon, fontů a velikosti fontů. Popíše též detailní ruční konfiguraci.

## Contents

*   [1 Témata](#T.C3.A9mata)
    *   [1.1 GTK+ 1.x](#GTK.2B_1.x)
    *   [1.2 GTK+ 2.x](#GTK.2B_2.x)
    *   [1.3 GTK a QT](#GTK_a_QT)
*   [2 Zdroje](#Zdroje)

## Témata

### GTK+ 1.x

Staré GTK1 aplikace (XMMS) často zpočátku nevypadají moc pěkně. To je způsobeno tím, že ve výchozím nastavení používají ošklivá témata. Abyste to změnili, musíte:

1.  stáhnout a nainstalovat nějaká pěkná témata
2.  změnit téma

Pár pěkných témat je v [extra]. Abyste je nainstalovali:

```
# pacman -S gtk-smooth-engine

```

Pro změnu téma můžete použít gtk-theme-switch:

```
# pacman -S gtk-theme-switch

```

Spustťe ho s příkazem "switch".

### GTK+ 2.x

Hlavní [desktopová prostředí](/index.php/Category:Desktop_environments_(%C4%8Cesky) "Category:Desktop environments (Česky)") poskytují nástroje pro konfiguraci GTK téma, ikon, fontů a velikosti fontů. Alternativně mohou být použity nástroje jako [lxappearance](https://www.archlinux.org/packages/?name=lxappearance), [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme), [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2) a [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs). [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) je konfigurační nástroj z projektu LXDE nezávislý na desktopovém prostředí, který nepotřebuje pro svůj běh žádnou jinou část z LXDE. Nainstalujte některý z těchto balíčků, viz:

```
# pacman -S lxappearance

# pacman -S gtk-chtheme

# pacman -S gtk-theme-switch2

# pacman -S gtk2_prefs

```

Je doporučeno nainstalovat též nějaká GTK2 témata. Populární téma _Clearlooks_ je součástí balíčku [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines):

```
# pacman -S gtk-engines

```

Další témata můžete nalézt v [AUR](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)"):

*   [https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go)
*   [https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go)

Alternativně může být nastavení GTK konfigurováno ručně úpravami `~/.gtkrc-2.0`. Seznam všech nastavení v GTK můžete nalézt v [knihovně Gnome (anglicky)](http://library.gnome.org/devel/gtk/stable/GtkSettings.html). Pro ruční změnu GTK téma, ikon, fontu a velikosti fontu přidejte do `~/.gtkrc-2.0` následující:

 `~/.gtkrc-2.0` 

```
gtk-icon-theme-name = "[jméno-téma-ikon]"
gtk-theme-name = "[jméno-téma]"
gtk-font-name = "[jméno-fontu] [velikost]"
```

Například:

 `~/.gtkrc-2.0` 

```
gtk-icon-theme-name = "Tango"
gtk-theme-name = "Murrine-Gray"
gtk-font-name = "DejaVu Sans 8"
```

**Note:** Výše zmíněný příklad vyžaduje balíčky [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu), [tango-icon-theme](https://aur.archlinux.org/packages/tango-icon-theme/), [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine) a [gtk-theme-murrine-collection](https://aur.archlinux.org/packages/gtk-theme-murrine-collection/).

### GTK a QT

Pokud máte na svém desktopu aplikace pro GTK i Qt (KDE), víte, že jejich vzhledy spolu moc neladí. Pokud si přejete změnit styl GTK tak, aby následoval styl Qt nebo naopak, přečtěte si [Uniform Look for QT and GTK Applications (anglicky)](/index.php/Uniform_Look_for_QT_and_GTK_Applications "Uniform Look for QT and GTK Applications").

## Zdroje

*   [Oficiální stránky GTK (anglicky)](http://www.gtk.org/)
*   [Tutoriál pro GTK2 (anglicky)](http://www.gtk.org/tutorial/)
*   [Článek o GTK na Wikipedii (anglicky)](http://en.wikipedia.org/wiki/GTK%2B)
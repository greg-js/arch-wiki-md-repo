## Contents

*   [1 Úvod](#.C3.9Avod)
    *   [1.1 Úplný návod](#.C3.9Apln.C3.BD_n.C3.A1vod)
    *   [1.2 Jak nainstalovat Fluxbox](#Jak_nainstalovat_Fluxbox)
    *   [1.3 Spuštění Fluxboxu](#Spu.C5.A1t.C4.9Bn.C3.AD_Fluxboxu)
        *   [1.3.1 Metoda 1: Display manager](#Metoda_1:_Display_manager)
        *   [1.3.2 Metoda 2: ~/.xinitrc](#Metoda_2:_.7E.2F.xinitrc)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Úprava menu](#.C3.9Aprava_menu)
        *   [2.1.1 Rychlá metoda:](#Rychl.C3.A1_metoda:)
        *   [2.1.2 Doporučená metoda: MenuMaker](#Doporu.C4.8Den.C3.A1_metoda:_MenuMaker)
        *   [2.1.3 Menu Arch Linux programem Xdg](#Menu_Arch_Linux_programem_Xdg)
        *   [2.1.4 Vytvoření uživatelského menu pomocí programu fluxconf](#Vytvo.C5.99en.C3.AD_u.C5.BEivatelsk.C3.A9ho_menu_pomoc.C3.AD_programu_fluxconf)
        *   [2.1.5 Manuální tvorba/editace menu](#Manu.C3.A1ln.C3.AD_tvorba.2Feditace_menu)
    *   [2.2 Klávesové zkratky](#Kl.C3.A1vesov.C3.A9_zkratky)
    *   [2.3 Pracovní plochy (workspaces)](#Pracovn.C3.AD_plochy_.28workspaces.29)
    *   [2.4 Pozadí](#Pozad.C3.AD)
        *   [2.4.1 Další poznámky pro uživatele, kteří chtějí často měnit pozadí plochy](#Dal.C5.A1.C3.AD_pozn.C3.A1mky_pro_u.C5.BEivatele.2C_kte.C5.99.C3.AD_cht.C4.9Bj.C3.AD_.C4.8Dasto_m.C4.9Bnit_pozad.C3.AD_plochy)
        *   [2.4.2 Feh](#Feh)
    *   [2.5 Témata](#T.C3.A9mata)
    *   [2.6 Témata GTK2](#T.C3.A9mata_GTK2)
    *   [2.7 Spouštění aplikací při startu](#Spou.C5.A1t.C4.9Bn.C3.AD_aplikac.C3.AD_p.C5.99i_startu)
    *   [2.8 Nepoužití souboru xorg.conf](#Nepou.C5.BEit.C3.AD_souboru_xorg.conf)
        *   [2.8.1 Nastavení klávesnice](#Nastaven.C3.AD_kl.C3.A1vesnice)
        *   [2.8.2 Vypnutí šetření energie](#Vypnut.C3.AD_.C5.A1et.C5.99en.C3.AD_energie)
*   [3 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

# Úvod

## Úplný návod

Autorem úplného návodu je narada. Nalézt jej můžete zde: [[1]](https://bbs.archlinux.org/viewtopic.php?id=77729)

## Jak nainstalovat Fluxbox

Instalace je poměrně jednoduchá, vše je v repozitářích. Začínajícím uživatelům doporučuji nainstalovat také menumaker a fluxconf.

```
pacman -S fluxbox fluxconf menumaker

```

## Spuštění Fluxboxu

### Metoda 1: [Display manager](/index.php/Display_manager "Display manager")

O přidání nabídky do správce přihlášení [Display manager](/index.php/Display_manager "Display manager") se automaticky postará instalátor. Při přihlašování vyberte fluxbox.

### Metoda 2: ~/.xinitrc

Ve svém domovském adresáři přijdete do souboru `~/.xinitrc` následující řádek:

```
exec fluxbox

```

pokud chcete fluxbox spustit souborem 'startfluxbox', vložte:

```
exec startfluxbox

```

Je doporučeno spouštět fluxbox souborem <tt>startfluxbox</tt>, protože při startu spustí programy, definované v souboru `~/.fluxbox/startup`.

**Note:** V souboru `~/.xinitrc` může být pouze jeden řádek <tt>exec</tt>.

Pokud se při startu vyskytnou problémy, může být problém v locale. Nastavením LC_ALL na předvolenou hodnotu "C" může pomoci. Viz [1](https://bbs.archlinux.org/viewtopic.php?t=25797).

# Konfigurace

Za nastavením Fluxboxu stojí tři soubory, které se nachází v domovském adresáři uživatele v adresáři /.fluxbox -> menu, keys, init. V těchto souborech je možné nastavit úplně vše, od základního fungovaní (init), klavesových zkratek (keys), až po jeho menu (menu). Tyto soubory lze editovat ručně, nebo pomocí utility zvané FluxConf.

## Úprava menu

### Rychlá metoda:

pomocí příkazu:

```
$ fluxbox-generate_menu

```

se vygeneruje soubor ~/.fluxbox/menu v závislosti na programech, které máte nainstalované. V menu fluxboxu je položka "helper / regenerate menu", která vykoná totéž.
Základní struktura menu:

```
[begin] (Nadpis menu)
[submenu]  (Nadpis submenu)
[exec] (Název aplikace) {/cesta/k/programu}
[include] (/cesta/k_souboru/s_menu)
[end]
[nop] (--------)
[separator]
[workspaces] (Název submenu s pracovními plochami)
[stylesdir] (/cesta/k_adresari/se_styly)
[config] (Název submenu s konfigurací fluxboxu)
[restart] (Restart Fluxboxu)
[exit] (Konec sezení ve Fluxboxu) 

```

*   [nop] - Slouží jako oddělovač, do závorek je možné uvést libovolný text. Tento bude uveden v menu, nespouští však žádný příkaz.
*   [separator] - Oddělovač v podobě horizontální linky.

Ukázka souboru .fluxbox/menu:

```
# Generated by fluxbox-generate_menu
#
# If you read this it means you want to edit this file manually, so here
# are some useful tips:
#
# - You can add your own menu-entries to ~/.fluxbox/usermenu
#
# - If you miss apps please let me know and I will add them for the next
#   release.
#
# - The -r option prevents removing of empty menu entries and lines which
#   makes things much more readable.
#
# - To prevent any other app from overwriting your menu
#   you can change the menu name in .fluxbox/init to:
#     session.menuFile: /home/you/.fluxbox/my-menu
[begin] (Fluxbox-1.0rc3)
     [exec] (urxvt) {urxvt}
     [exec] (opera) {env QT_XFT=true opera}
[submenu] (Terminals)
     [exec]   (xterm) {xterm}
     [exec]   (urxvt) {urxvt}
     [exec]   (urxvtc) {urxvtc}
     [exec]   (mlterm) {mlterm}
[end]
[submenu] (Net)
[submenu] (Browsers)
     [exec]   (dillo) {dillo}
     [exec]   (vncviewer) {vncviewer}
     [exec]   (links-graphic) {links -driver x fluxbox.org}
     [exec]   (opera) {env QT_XFT=true opera}
     [exec]   (links) {urxvt -e links fluxbox.org}
[end]
[submenu] (IM)
     [exec]   (gaim) {gaim}
[end]
[submenu] (Mail)
     [exec]   (sylpheed-claws) {sylpheed-claws}
     [exec]   (mutt) {urxvt -e mutt}
[end]
[submenu] (IRC)
     [exec]   (irssi) {urxvt -e irssi}
[end]
[submenu] (ftp)
     [exec]   (gftp) {gftp}
     [exec]   (ftp) {urxvt -e ftp}
[end]
     [exec]   (xnmap) {xnmap}
     [exec]   (skype) {skype}
[end]
[submenu] (Editors)
     [exec]   (gvim) {gvim}
     [exec]   (xedit) {xedit}
     [exec]   (evim) {evim}
     [exec]   (scite) {scite}
     [exec]   (nano) {urxvt -e nano}
     [exec]   (vim) {urxvt -e vim}
     [exec]   (vi) {urxvt -e vi}
[end]
[submenu] (File utils)
     [exec]   (rox) {rox}
     [exec]   (mc) {urxvt -e mc}
[end]
[submenu] (Multimedia)
[submenu] (Graphics)
     [exec]   (inkscape) {inkscape}
     [exec]   (gqview) {gqview}
     [exec] (blender) {blender -w}
[end]
[submenu] (Audio)
     [exec]   (xmms) {xmms}
     [exec]   (alsaplayer) {alsaplayer}
     [exec]   (easytag) {easytag}
     [exec]   (audacity) {audacity}
     [exec]   (beep-media-player) {beep-media-player}
     [exec]   (alsamixer) {urxvt -e alsamixer}
[end]
[submenu] (Video)
     [exec]   (xine) {xine}
     [exec]   (aviplay) {aviplay}
     [exec]   (gmplayer) {gmplayer}
     [exec]   (vlc) {vlc}
     [exec] (dvdrip) {nohup dvdrip}
[end]
[submenu] (X-utils)
     [exec]   (xfontsel) {xfontsel}
     [exec]   (xman) {xman}
     [exec]   (xload) {xload}
     [exec]   (xbiff) {xbiff}
     [exec]   (editres) {editres}
     [exec]   (viewres) {viewres}
     [exec]   (xclock) {xclock}
     [exec]   (xmag) {xmag}
     [exec]   (gkrellm) {gkrellm}
     [exec]   (vmware) {vmware}
     [exec] (Reload .Xdefaults) {xrdb -load /home/tobias/.Xdefaults}
[end]
[end]
[submenu] (Office)
     [exec]   (xclock) {xclock}
     [exec]   (xcalc) {xcalc}
     [exec] (Open Office)      {soffice}
     [exec]   (abiword) {abiword}
     [exec]   (acroread) {acroread}
     [exec]   (xpdf) {xpdf}
     [exec]   (gv) {gv}
[end]
[submenu] (Games)
     [exec]   (bzflag) {bzflag}
     [exec]   (xeyes) {xeyes}
[end]
[submenu] (System Tools)
     [exec]   (top) {urxvt -e top}
[end]
[submenu] (fluxbox menu)
     [config] (Configure)
[submenu] (System Styles) {Choose a style...}
     [stylesdir] (/usr/share/fluxbox/styles)
[end]
[submenu] (User Styles) {Choose a style...}
     [stylesdir] (~/.fluxbox/styles)
[end]
     [workspaces] (Workspace List)
[submenu] (Tools)
     [exec] (Window name) {xprop WM_CLASS|cut -d \" -f 2|xmessage -file - -center}
     [exec] (Screenshot - JPG) {import screenshot.jpg && display -resize 50% screenshot.jpg}
     [exec] (Screenshot - PNG) {import screenshot.png && display -resize 50% screenshot.png}
     [exec] (gtk-theme-switch) {switch}
     [exec] (gtk2-theme-switch) {switch2}
     [exec] (Regen Menu) {fluxbox-generate_menu}
[end]
[submenu] (Window)
     [restart] (openbox) {openbox}
[end]
     [commanddialog] (Fluxbox Command)
     [reconfig] (Reload config)
     [restart] (Restart)
     [exec] (About) {(fluxbox -v; fluxbox -info | sed 1d) 2> /dev/null | xmessage -file - -center}
     [separator]
     [exit] (Exit)
[end]
[end]

```

### Doporučená metoda: MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) je kvalitní nástroj, který vytvoří menu v XML, které lze použít v různých okenních správcích, včetně Fluxboxu. MenuMaker prohledá váš počítač a vygeneruje menu podle programů, které najde. Může být nastaven tak, aby vynechal programy z X, GNOME, KDE nebo Xfce.

MenuMaker je dostupný v repozitáři [community]:

```
# pacman -S menumaker

```

Po nainstalování lze menu vygenerovat příkazem:

```
$ mmaker -v Fluxbox

```

Kompletní nápovědu lze zobrazit příkazem **mmaker --help**

### Menu Arch Linux programem Xdg

Vyžaduje nainstalovat balíček [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu)

```
$ xdg_menu --fullmenu --format fluxbox --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/menu

```

**Tip:** náhrada předvoleného xterm/urxvt:

```
$ sed -i 's/xterm/urxvt/g' ~/.fluxbox/menu

```

Další info:

```
$ xdg_menu --help

```

*Viz také: [XdgMenu](/index.php/XdgMenu "XdgMenu")*

### Vytvoření uživatelského menu pomocí programu fluxconf

Tvorba menu se spustí příkazem:

```
$ fluxmenu

```

V okně vidíte tři sloupce: Type, Title, & Command/Comment.
Kliknutím na položku ji můžete editovat.
Kliknutím na "Add sub" přidáte submenu.
Kliknutím na "Add exec" přidáte program.

Sloupec type má několik platných možností:

1.  begin, požadovaný pro začátek souboru menu. Title je název hlavičky menu.

2.  submenu, "adresář" uvnitř menu. Title je název submenu.

3.  exec, příkazový řádek. Title je co se zobrazí a Command/Comment je program, který bude spuštěn.
4.  separator, oddělovač menu. Bez parametrů.
5.  workspaces, seznam pracovních ploch a které programy běží na které. Title je název, zobrazený uživateli.
6.  stylesdir, adresář, obsahující styly. Title je cesta k adresáři. Doporučuje se styly ukládat do vlastních podadresářů, aby se jich více vešlo. Adresáře jsou: /usr/share/fluxbox/styles ~/.fluxbox/styles .
7.  config, menu s mnoha volbami konfigurace chování fluxboxu. Title je název, zobrazený uživateli.
8.  reconfig, znovu nahraje konfigurační soubor. Title je název, zobrazený uživateli.
9.  restart, restartuje fluxbox. Title je název, zobrazený uživateli.
10.  exit, ukončí fluxbox, vrátí se do přihlašovacího manažeru nebo ukončí X podle metody, použité při spuštění. Title je název, zobrazený uživateli.

Před ukončením nezapomeňte soubor uložit kliknutím na save

### Manuální tvorba/editace menu

Použijte příkaz:

```
$ nano ~/.fluxbox/menu

```

Pak vkládejte řádky tímto způsobem:

```
[exec] (name) {command}

```

Pokud chcete vložit submenu:

```
[submenu] (Name)
...
...
[end]

```

Nakonec klikněte na save a exit. Není třeba restartovat fluxbox.

## Klávesové zkratky

Nastavení klávesových zkratek se nachází v souboru:

```
~/.fluxbox/keys

```

Klávesa Control je reprezentována příkazem "Control". Mod1 odpovídá klávese Alt a Mod4 klávese Meta (není standardní klávesa, většinou je mapována na klávesu win).

Např. úroveň hlasitosti pomocí kláves CTRL-ALT + šipka nahoru nebo dolů lze nastavit takto:

```
Control Mod1 Up :Exec amixer sset Master,0 5%+  
Control Mod1 Down :Exec amixer sset Master,0 5%-  

```

Pokud máte nainstalovaný program fluxconf, můžete použít grafickou konfiguraci příkazem:

```
$ fluxkeys

```

První textové pole je pro klávesu a druhé pro akci. Pro nastavení příkazu zvolte execCommand a vložte jméno příkazu do třetího textového pole.

Další funkce lze použít z druhého textového pole (je dostupné drop down menu)

## Pracovní plochy (workspaces)

Fluxbox poskytuje ve výchozím nastavení uživateli čtyři pracovní plochy, dostupné použitím kláves Alt+F1 až F4 nebo šipkami na toolbaru vedle místa, kde je vypsán název současné pracovní plochy.

Kliknutím pravého tlačítka na ploše a vstupem do Workspaces menu (uživatelé menumakeru: FluxBox>Workspaces, uživatelé fluxconf: položka workspaces) můžete pracovní plochy upravovat.

Menu Workspaces:

```
Icons - zobrazí minimalizované aplikace
--separator--
Workspaces names (default: one,two,three,four) - zobrazí všechny aplikace na této ploše
--separator--
New Workspace - přidá pracovní plochu
Edit Current workspace name - dovolí vám změnit popisek pracovní plochy na cokoliv budete chtít. Ten se ukáže na levé straně toolbaru.
Remove Last - odstraní poslední pracovní plochu v seznamu a přesune všechny aplikace běžící na dané ploše na plochu předcházející

```

## Pozadí

Nastavení pozadí se provádí dalším softwarem. Lze nainstalovat např. následující balíčky:

*   eterm
*   feh (postrádající průhlednost menu).

Existují další, ale tyto dva jsou doporučené. Další programy jsou uvedené v dokumentaci k fbsetbg v kapitole "Additional Links section" Pozadí se nastavuje příkazem:

```
$ fbsetbg /path/to/background.image

```

Můžete přidat nebo modifikovat tento řádek v souboru ~/.fluxbox/init:

```
session.screen0.rootCommand:	fbsetbg /path/to/wallpaper

```

nebo jednoduše:

```
session.screen0.rootCommand:	fbsetbg -l

```

#### Další poznámky pro uživatele, kteří chtějí často měnit pozadí plochy

Přidejte do svého fluxbox menu toto submenu:

```
[submenu] (Backgrounds)
[wallpapers] (~/.fluxbox/backgrounds)
[wallpapers] (/usr/share/fluxbox/backgrounds)
[end]

```

Přidejte svoje obrázky pozadí plochy do adresáře ~/.fluxbox/backgrounds nebo jiného specifikovaného, budou se nastavovat podobně, jako styly.

### Feh

Instalace feh:

```
# pacman -S feh

```

Můžete si do souboru `~/.fluxbox/menu` přidat submenu, které umožní měnit plochu za běhu:

```
[submenu] (Wallpaper)
[wallpapers] (/path/to/your/wallpapers) {feh --bg-scale}
[end]

```

Aby mohl být feh spuštěn při příštím startu fluxboxu, proveďte následující:

**1.** Nastavte soubor `.fehbg` jako spustitelný:

```
$ chmod 770 ~/.fehbg

```

**2.** Přidejte (nebo modifikujte) následující řádek do souboru `~/.fluxbox/init`:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** nebo přidejte (či modifikujte) tento řádek v souboru `~/.fluxbox/startup`:

```
~/.fehbg

```

## Témata

Téma se instaluje rozbalením archivu s tématem do jednoho z adresářů:

*   globálně dostupné - /usr/share/fluxbox/styles
*   pouze pro daného uživatele - ~/.fluxbox/styles

Odkazy na některé servery s tématy jsou uvedené níže.

## Témata GTK2

*Viz: [GTK+](/index.php/GTK%2B "GTK+")*

## Spouštění aplikací při startu

Uživatelé xinitrc by měli veškerý kód vložit do souboru `~/.xinitrc`. Ovšem fluxbox nabízí vlastní možnost spouštění aplikací:

soubor `~/.fluxbox/startup` je skript, ve kterém je nastaveno, které programy fluxbox při startu spustí. Znak # označuje komentáře.

Příklad:

```
fbsetbg -l # nastavuje poslední pozadí plochy, velice praktické a doporučené.
# Znak (&), uvedený u příkazů níže, je vyžadován pro spouštění programů, které se po spuštění okamžitě neukončí.
# Pokud se vynechá, fluxbox se nespustí.
idesk & 
xterm &
# exec je pro samotné spuštění fluxboxu, nezadávejte za něj znak (&), nebo se fluxbox ihned ukončí
exec /usr/bin/fluxbox
# pokud chcete výpis do logu, odkomentujte spodní řádek a zakomentujte horní:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

## Nepoužití souboru xorg.conf

Xorg již nepotřebuje konfigurační soubor xorg.conf. Tradičně se v něm mění nastavení klávesnice a úspora energie. Naštěstí existují elegantnější řešení bez použití souboru xorg.conf.

### Nastavení klávesnice

Přidejte následující řádek do souboru `~/.fluxbox/startup`:

```
setxkbmap us -variant intl & # umožní použít us klávesnici se speciálními znaky (např. éóíáú)

```

Místo 'us' můžete zadat svůj kód jazykové sady a odstranit parametr variant. Další možnosti viz man setxkbmap.

Přepínač klávesnice lze do menu v souboru `~/.fluxbox/menu` přidat takto:

```
[submenu] (Keyboard)
      [exec] (normální) {setxkbmap us}
      [exec] (mezinárodní) {setxkbmap us -variant intl}
[end]

```

### Vypnutí šetření energie

Znáte situaci, kdy vám šetřič energie vypne monitor během sledování filmu? Gratulujeme, Xorg zrovna detekoval, že nic neděláte :). Toto lze softwarově vypnout, ovšem když budete potom chtít vypnout monitor, musíte to udělat ručně.

Přidejte následující řádek na začátek souboru `~/.fluxbox/startup`:

```
xset s off -dpms &

```

# Další zdroje

*   [Fluxbox Homepage](http://fluxbox.sourceforge.net/)
*   [Gentoo Wiki about Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Themes for Fluxbox](http://box-look.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [fbsetbg documentation](http://www.xs4all.nl/~hanb/software/fbsetbg/fbsetbg.html)
*   [Application recommendations](http://archux.com/page/application-recommendations)
*   [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide")
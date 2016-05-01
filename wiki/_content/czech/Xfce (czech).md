## Contents

*   [1 Co je Xfce?](#Co_je_Xfce.3F)
*   [2 Proč používat Xfce?](#Pro.C4.8D_pou.C5.BE.C3.ADvat_Xfce.3F)
*   [3 Proč nepoužívat Xfce?](#Pro.C4.8D_nepou.C5.BE.C3.ADvat_Xfce.3F)
*   [4 Jak nainstalovat Xfce](#Jak_nainstalovat_Xfce)
*   [5 Spouštění Xfce](#Spou.C5.A1t.C4.9Bn.C3.AD_Xfce)
*   [6 Jak používat Xfce spolu se správci displeje](#Jak_pou.C5.BE.C3.ADvat_Xfce_spolu_se_spr.C3.A1vci_displeje)
*   [7 Jak vypínat a restartovat z Xfce](#Jak_vyp.C3.ADnat_a_restartovat_z_Xfce)
*   [8 Tipy](#Tipy)
    *   [8.1 Příkazy pro správce nastavení](#P.C5.99.C3.ADkazy_pro_spr.C3.A1vce_nastaven.C3.AD)
    *   [8.2 Vysouvací konzole jako ve Quake](#Vysouvac.C3.AD_konzole_jako_ve_Quake)
    *   [8.3 Jak zapnout kompozitor (Xfce 4.4)](#Jak_zapnout_kompozitor_.28Xfce_4.4.29)
    *   [8.4 Proč se moje plocha neobnovuje?](#Pro.C4.8D_se_moje_plocha_neobnovuje.3F)
    *   [8.5 Průhledné pozadí pro popisky ikon na ploše](#Pr.C5.AFhledn.C3.A9_pozad.C3.AD_pro_popisky_ikon_na_plo.C5.A1e)
    *   [8.6 Jak si přizpůsobit pozadí panelu Xfce](#Jak_si_p.C5.99izp.C5.AFsobit_pozad.C3.AD_panelu_Xfce)
    *   [8.7 Jak si přizpůsobit spouštění Xfce](#Jak_si_p.C5.99izp.C5.AFsobit_spou.C5.A1t.C4.9Bn.C3.AD_Xfce)
    *   [8.8 Jak do Xfce přidat témata](#Jak_do_Xfce_p.C5.99idat_t.C3.A9mata)
    *   [8.9 Jak odstranit položky ze systémového menu](#Jak_odstranit_polo.C5.BEky_ze_syst.C3.A9mov.C3.A9ho_menu)
        *   [8.9.1 Ale co dělat s položkami menu, které nejsou v /usr/share/applications?](#Ale_co_d.C4.9Blat_s_polo.C5.BEkami_menu.2C_kter.C3.A9_nejsou_v_.2Fusr.2Fshare.2Fapplications.3F)
    *   [8.10 Jak dosáhnout toho, aby spolupracovaly xfce4-mixer a OSS4 (Xfce 4.4 a starší)](#Jak_dos.C3.A1hnout_toho.2C_aby_spolupracovaly_xfce4-mixer_a_OSS4_.28Xfce_4.4_a_star.C5.A1.C3.AD.29)
*   [9 Související články](#Souvisej.C3.ADc.C3.AD_.C4.8Dl.C3.A1nky)
*   [10 Externí zdroje](#Extern.C3.AD_zdroje)

## Co je Xfce?

Xfce je, stejně jako GNOME nebo KDE, desktopové prostředí. Obsahuje balík aplikací jako správce oken, správce souborů, panel, aplikace kořenového okna atd. Xfce je napsáno s použitím toolkitu GTK2 (stejně jako GNOME) a obsahuje vlastní vývojářské prostředí (knihovny, daemoni atd.) podobné jiným velkým DE. Na rozdíl od GNOME nebo KDE, Xfce je odlehčené a navržené spíše kolem CDE než kolem Windows nebo Mac. Má mnohem pomalejší vývojový cyklus, ale je velmi stabilní a rychlé. Xfce je výborné pro starší hardware.

**Warning:** Tento článek pojednává o Xfce verzi 4.4\. Pokud máte novější verzi, některé postupy nemusí být stále funkční.

## Proč používat Xfce?

Zde je (subjektivní) seznam důvodů, proč používat Xfce::

*   Je rychlé; rychlejší než ostatní hlavní desktopová prostředí
*   Je stabilní. Za ten dlouhý čas, co je Xfce4 venku, byla i přes celkem velký počet jeho stoupenců objevena jenom malá hrstka chyb.
*   Je pěkné. Používá GTK2 a lze měnit témata. Též má plně antialiasované fonty. Xfce může vypadat velmi hezky.
*   Pracuje skvěle s více monitory. Podpora Xineramy v Xfce je jasně nejlepší ze všech okenních správců/desktopových prostředí.
*   Nestaví se vám do cesty. Zjistíte, že Xfce vám spíše pomáhá při práci než že by překáželo.
*   Přichází s vestavěným kompozitorem, jenž kromě jiných skvělých věcí umožňuje opravdovou průhlednost.

## Proč nepoužívat Xfce?

Zde je (subjektivní) seznam důvodů, proč **ne**používat Xfce:

*   Neobsahuje všechny schopnosti a integraci hlavních desktopových prostředí.
*   Pomalejší vývojový cyklus.
*   Protože je založené na návrhu CDE, rozvržení nemusí být tak známé.

## Jak nainstalovat Xfce

Zdrojové kódy Xfce a dokumentace jsou dostupné na [http://www.xfce.org/](http://www.xfce.org/). Ale jelikož používáte Arch Linux, můžete nainstalovat Xfce pacmanem.

Xfce je modulární. To znamená, že není třeba, abyste měli nainstalovány všechny jeho části; můžete si vybírat. Z toho důvodu tvoří Xfce v Archu několik sdružených balíčků.

Abyste nainstalovali základní systém Xfce, spusťte:

```
# pacman -S xfce4

```

Pokud chcete dodatečné věci jako pluginy pro panel a další témata, spusťte toto:

```
# pacman -S xfce4-goodies gtk2-themes-collection

```

Pokud chcete být schopni přehrávat zvukové soubory, měli byste též nainstalovat ESD, jenž slouží jako zvukový daemon Xfce. (Nebo můžete nainstalovat xfmedia, což je výchozí multimediální přehrávač Xfce, a ten s sebou nainstaluje ESD jako závislost.)

```
# pacman -S esd

```

**Tip:** Místo esd můžete též nainstalovat jeho nástupce, zvukový server PulseAudio, jenž je v [community]. Viz článek [PulseAudio (anglicky)](/index.php/PulseAudio "PulseAudio").

Pokud si po přihlášení přejete obdivovat "Tipy a triky", nainstalujte balíček **fortune-mod**:

```
# pacman -S fortune-mod

```

## Spouštění Xfce

Jsou dvě cesty spouštění Xfce. Jedna z nich je "automatická" metoda. Abyste Xfce spustili z konzole, můžete jednoduše zadat:

```
# startxfce4

```

**Note:** startxfce4 standardně nastavuje DPI na 96, takže velikosti fontů budou jiné než při spouštění z .xinitrc.

*   Pro přizpůsobení startu Xfce s použitím této metody můžete zkopírovat /etc/xdg/xfce4/xinitrc do $HOME/.xfce4 a upravit tento soubor.
*   Pro přidání programů po spuštění s použitím této metody přidejte symlinky požadovaných programů do $HOME/Desktop/Autostart.

Pokud chcete více ovládat své výchozí nastavení a to, co se spouští, můžete do svého souboru $HOME/.xinitrc přidat tyto položky (vynechte nebo přidejte cokoliv chcete):

```
xfce-mcs-manager
xfwm4 --daemon
xfdesktop &
exec xfce4-panel

```

nebo

```
exec xfce4-session

```

## Jak používat Xfce spolu se správci displeje

Počínaje verzí Xfce 4.2.0 balíčky v Archu obsahují náležité soubory sezení. Jsou obsaženy v balíčku xfce-utils, který by měl být přítomný v základní instalaci. Jednoduše [zapněte správce displeje](/index.php/Display_manager_(%C4%8Cesky) "Display manager (Česky)").

## Jak vypínat a restartovat z Xfce

Ujistěte se, že jsou aktivováni DBus a HAL (v řádku DAEMONS v /etc/[rc.conf](/index.php/Rc.conf "Rc.conf")). Poté přidejte svého běžného uživatele do skupiny *power*:

```
# gpasswd -a UŽIVATEL power

```

**Note:** Tato skupina je používána pouze HALem, takže pro vypnutí systému v příkazové řádce (halt/poweroff/shutdown) stále budete potřebovat privilegia superuživatele.

## Tipy

### Příkazy pro správce nastavení

Pro spouštěné příkazy není žádná oficiální dokumentace. Je třeba se podívat na soubory .desktop v adresáři */usr/share/applications/*. Pro ušetření úsilí je zde pro lidi, kteří chtějí vědět, co se přesně děje, praktický seznam:

```
xfce-setting-show backdrop
xfce-setting-show display
xfce-setting-show keyboard
xfce4-menueditor
xfce-setting-show sound
xfce-setting-show mouse
xfce-setting-show session
xfce-setting-show
xfce-setting-show splash
xfce-setting-show ui
xfce-setting-show xfwm4
xfce-setting-show wmtweaks
xfce-setting-show workspaces
xfce-setting-show printing_system
xfce4-appfinder
xfce4-autostart-editor
xfce4-panel -c

```

Pro přehled všech dostupných příkazů pro správce nastavení spusťte v terminálu následující:

```
$ grep xfce-setting-show /usr/share/applications/xfce*settings*

```

### Vysouvací konzole jako ve Quake

```
# pacman -S tilda

```

nainstaluje tildu, vysouvací konzoli podobnou yakuake ve KDE. Používá celkem dost RAM; odlehčenější alternativou by byl **stjerm**, jehož můžete nalézt v AUR.

### Jak zapnout kompozitor (Xfce 4.4)

Xfce 4.4 přichází s vestavěným kompozitorem, jenž umožňuje ozdobné efekty oken, stíny, průhlednost a tak dále.

Můžete ho najít v *Settings -> Window manager tweaks*. Pokud tam nicméně není, učiňte následující kroky:

*   Otevřete $HOME/.config/xfce4/mcs_settings/wmtweaks.xml a ujistěte se, že je v souboru přítomné *<option name="Xfwm/UseCompositing" type="int" value="1"/>*. Pokud tam není soubor wmtweaks, otevřete *Settings->Window manager tweaks* a změňte pár věcí, pak dialog zavřete a soubor by se měl objevit.
*   Ujistěte se, že ve vašem souboru /etc/X11/xorg.conf jsou následující řádky:

```
Section "Extensions"
	Option "Composite" "Enable"
EndSection

```

*   Nakonec restartujte X a kompozitor by měl být dostupný.

### Proč se moje plocha neobnovuje?

Xfce 4.4 k tomu, aby bylo uvědomeno když se změní nějaký soubor nebo adresář, používá FAM (File Alteration Monitor). Nezapomeňte přidat "fam" do seznamu DAEMONS v /etc/[rc.conf](/index.php/Rc.conf "Rc.conf").

### Průhledné pozadí pro popisky ikon na ploše

Pro změnu výchozího bílého pozadí popisků ikon na ploše na něco vhodnějšího otevřete soubor .gtkrc-2.0 ve svém domovském adresáři a přidejte následující (pokud je třeba, soubor vytvořte):

```
style "xfdesktop-icon-view" {
XfdesktopIconView::label-alpha = 10
base[NORMAL] = "#000000"
base[SELECTED] = "#71B9FF"
base[ACTIVE] = "#71FFAD"
fg[NORMAL] = "#ffffff"
fg[SELECTED] = "#71B9FF"
fg[ACTIVE] = "#71FFAD" }
widget_class "*XfdesktopIconView*" style "xfdesktop-icon-view"

```

### Jak si přizpůsobit pozadí panelu Xfce

To samé, upravte ~/.gtkrc-2.0\. (<tt>foo.bar</tt> je cesta k vašemu obrázku.)

```
 style "panel-background" {
   bg_pixmap[NORMAL]        = "foo.bar"
   bg_pixmap[PRELIGHT]      = "foo.bar"
   bg_pixmap[ACTIVE]        = "foo.bar"
   bg_pixmap[SELECTED]      = "foo.bar"
   bg_pixmap[INSENSITIVE]   = "foo.bar"
 }
 widget_class "*Panel*" style "panel-background"

```

### Jak si přizpůsobit spouštění Xfce

Toto zahrnuje dostávání potřebných proměnných prostředí do GUI.

*   Zkopírujte soubor /etc/xdg/xfce4/xinitrc do ~/.config/xfce4/
*   Upravte tento soubor. Například můžete někde uprostřed přidat něco jako:

```
source $HOME/.bashrc
# start rxvt-unicode server
urxvtd -q -o -f

```

### Jak do Xfce přidat témata

```
# pacman -S xfce-mcs-plugins

```

1.  Jděte na [xfce-look.org](http://xfce-look.org) a klikněte v levém navigačním pruhu na *"Themes"*. Porozhlédněte se po nějakém téma, které se vám bude líbit, a klikněte na *"Download"*.
2.  Jděte do adresáře, kam jste stáhli ten soubor/tarball a rozbalte ho pomocí Squeeze/Xarchiver/CLI.
3.  Přesuňte rozbalenou složku do /usr/share/themes (pro všechny uživatele) nebo ~/.themes (jen pro vás). Uvnitř /usr/share/themes/abc je složka se jménem xfwm4, jenž bude obsahovat všechny soubory zahrnuté v daném téma.
4.  GTK téma je dostupné zde: *Menu --> Settings --> User Interface Settings*
    Téma xfwm vybíráte v: *Menu --> Settings --> Window Manager Settings*

### Jak odstranit položky ze systémového menu

Pomocí vestavěného editoru menu nemůžete odstraňovat položky ze systémového menu. Zde je návod, jak je schovat:

1.  Jděte do složky /usr/share/applications. Zadejte v terminálu (Menu Xfce > System > Terminal): `$ cd /usr/share/applications` 
2.  Tato složka by měla být plná souborů .desktop. Abyste viděli, kolik jich je, zadejte: `$ ls` Řekněme že ten, který chcete upravit, je Firefox. Zadejte v terminálu: `$ sudo mousepad firefox.desktop` 
3.  Na konec souboru vložte následující: `NoDisplay=true` 
4.  Uložte soubor a zavřete editor. Nyní se Firefox nebude ukazovat v systémovém menu. Tohoto můžete docílit u jakéhokoliv programu.

#### Ale co dělat s položkami menu, které nejsou v /usr/share/applications?

Toto se týká například aplikací nainstalovaných skrze WINE. Hledejte tyto položky v adresáři **~/.local/share/applications/**.

### Jak dosáhnout toho, aby spolupracovaly xfce4-mixer a OSS4 (Xfce 4.4 a starší)

Zdá se, že balíček v binárních repozitářích je zkompilován pouze s podporou ALSA. Pro ty z nás co používají OSS4 je zde velmi jednoduchý způsob, jak přimět xfce4-mixer aby OSS4 podporoval. Nejdříve se dostaňte na SVN záznam pro balíček xfce4-mixer: [[1]](https://repos.archlinux.org/viewvc.cgi/xfce4-mixer/repos/extra-i686/):

Poté na svém stroji do jednoho adresáře stáhněte soubory **PKGBUILD** a **.install**. Dále se přesuňte do toho adresáře a najděte v souboru PKGBUILD tento řádek (je poblíž konce souboru):

```
--with-sound=alsa || return 1

```

Změňte v tom řádku **alsa** na **oss** a soubor uložte. Poté spusťte:

```
$ makepkg

```

Toto zabere pár minut v závislosti na rychlosti vašeho systému a volbách pro kompilaci v /etc/makepkg.conf. Poté se v aktuálním adresáři objeví soubor .pkg.tar.gz. Vše, co musíte udělat pro dokončení instalace xfce4-mixer je:

```
# pacman -U xfce4-mixer-4.4.2-2-i686.pkg.tar.gz

```

**Note:** Vaše verze souboru a architektura se mohou lišit. Na svém systému jsem s předchozím příkazem nainstaloval 32-bitovou verzi 4.4.2-2.

**Tip:** V AUR je pod xfce4-mixer-oss4 upravená verze xfce4-mixer, kterou jednoduše můžete nainstalovat stejně jako jakýkoliv balíček z ABS a dosáhnout stejného výsledku jako výše.

## Související články

*   [Jak dosáhnout toho, aby GTK aplikace vypadaly hezky](/index.php/Improve_GTK_Application_Looks "Improve GTK Application Looks") (anglicky)

## Externí zdroje

*   [Xfce.org](http://www.us.xfce.org/documentation/) - Kompletní dokumentace (anglicky)
*   [Xfce-Look](http://www.xfce-look.org/) - Témata, tapety a více (anglicky)
*   [Xfce Wikia FAQ](http://xfce.wikia.com/wiki/Frequently_Asked_Questions) - Jak upravit automaticky generované menu editorem menu (anglicky)
*   [Xfce Wiki](http://wiki.xfce.org) (anglicky)
*   [Návod: Odstraňování položek ze systémového menu](https://xubuntu.wordpress.com/2006/08/04/howto-remove-menu-entries-from-the-system-menu/) (anglicky)
*   [Témata Xfce na linuxquestions.org](http://www.linuxquestions.org/questions/linux-general-1/how-to-use-xfce-themes-658354/) (anglicky)
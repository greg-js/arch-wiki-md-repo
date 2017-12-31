## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
    *   [2.1 Standardní](#Standardn.C3.AD)
    *   [2.2 Zdrojové kódy](#Zdrojov.C3.A9_k.C3.B3dy)
*   [3 Spouštění](#Spou.C5.A1t.C4.9Bn.C3.AD)
*   [4 Nastavení](#Nastaven.C3.AD)
    *   [4.1 Nastavení awesome](#Nastaven.C3.AD_awesome)
    *   [4.2 Podpůrné aplikace](#Podp.C5.AFrn.C3.A9_aplikace)
*   [5 Problémy](#Probl.C3.A9my)
    *   [5.1 XCB](#XCB)
*   [6 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

# Úvod

**Poznámka:** tento text se vztahuje k awesome 3.x. Konfigurační soubory v této verzi NEJSOU zpětně kompatibilní s verzí 2.x, a proto pokud jste nějaké měli, bude potřeba je přepsat.

Awesome (překl. děsivý, strašlivý, strašně dobrý) je [dlaždicový správce oken](http://www.root.cz/clanky/tiled-desktopy-vsude-same-dlazdice/), který vyniká především tím, že je malý, snadno rozšiřitelný a vysoce konfigurovatelný. Tím se stává ideálním nástrojem pro pokročilejší uživatele nebo vývojáře, kteří dávají přednost nenáročným manažerům, které si mohou přizpůsobit k obrazu svému. Ruku v ruce s tím ovšem jde nutnost vynaložit větší úsilí při jeho nastavení.

# Instalace

## Standardní

Awesome je dostupný ve standardním repozitáři <tt>[community]</tt>:

```
# pacman -S awesome

```

## Zdrojové kódy

Zdrojové kódy awesome jsou uloženy v git repozitáři, čili pokud si přejete kompilovat ručně, tak klonovat:

```
$ git clone [git://git.naquadah.org/awesome.git](git://git.naquadah.org/awesome.git)

```

a následně se řídit instrukcemi v README, nebo můžete využít [awesome-git](https://aur.archlinux.org/packages/awesome-git/) z AUR:

```
$ yaourt -S awesome-git

```

# Spouštění

Pokud používáte správce přihlašování, tak si awesome přidejte do jeho nastavení (dobrou kombinací k awesome je [SLiM](http://slim.berlios.de/)). V opačném případě vložte

```
exec awesome

```

do startovacího skriptu, který používáte (<tt>~/.xinitrc</tt>).

Pokud ještě s awesome (nebo jiným dlaždicovým manažerem) nemáte zkušenosti, pak vězte, že velmi intenzivně využívá klávesových zkratek. Proto je vhodné si je nejprve nastudovat z konfiguračního souboru (viz dále), jinak se vám může stát, že nebudete schopni manažer vůbec ovládat.

# Nastavení

## Nastavení awesome

Awesome 3.x používá pro svou konfiguraci skript, který lze nalézt v <tt>~/.config/awesome/rc.lua</tt> (popř. jinde, viz manuál). Jak přípona napovídá, obsah je nově napsán v jazyce lua, což umožňuje na rozdíl od předchozích verzí větší volnost při tvorbě nastavení.

Další novinkou je přítomnost témat, která určují barevné vzezření manažeru (více viz knihovna [beautiful](http://awesome.naquadah.org/wiki/index.php?title=Beautiful)).

Celkově vzato je ovšem nastavení awesome nad rámec této wiki, proto podrobnější informace hledejte na [wiki](http://awesome.naquadah.org/wiki/index.php?title=Main_Page) awesome.

Pokud s awesome začínáte a nemáte ještě žádné konfigurační soubory z kterých byste mohli vyjít, můžete se nechat inspirovat těmito (další opět viz awesome wiki):

*   [http://git.glacicle.com/other/configs.git/.config/awesome/rc_30.lua](http://git.glacicle.com/other/configs.git/.config/awesome/rc_30.lua)
*   [http://www.gigamo.be/stuff/rc.lua](http://www.gigamo.be/stuff/rc.lua)
*   [http://oxmoz.no-ip.org/awesome/rc.lua](http://oxmoz.no-ip.org/awesome/rc.lua)

## Podpůrné aplikace

Jelikož awesome nenabízí žádné menu pro spouštění aplikací, budete možná chtít využít např. [dmenu](http://www.suckless.org/programs/dmenu.html). Tento prográmek vám umožní spouštět aplikace na základě vstupu z klávesnice, přičemž s každým napsaným znakem inkrementálně zužuje výběr.

Příklad použití:

```
$ dmenu_path | dmenu -b

```

a integrace do awesome, při stisku win+p:

```
keybinding({ modkey }, "p", function () awesome.spawn("exec `dmenu_path |  dmenu -b`") end):add()

```

# Problémy

## XCB

Awesome využívá asynchronní knihovnu XCB, proto je potřeba aby i závislosti tuto knihovnu podporovaly. Pokud se vám tedy stane, že awesome nespustíte nebo nezkompilujete a na vině budou chybějící symboly, které v názvu ponesou XCB, zkuste příslušnou aplikaci/knihovnu zkompilovat s podporou XCB.

V mém případě to byla knihovna <tt>cairo</tt>, stačilo potom:

```
# abs
$ cp /var/abs/extra/cairo ~/progs/abs/ -r
$ cd ~/progs/abs/cairo
$ makepkg -c
# yaourt -U cairo-$VER-$PLAT.pkg.tar.gz

```

# Další zdroje

*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - domovská stránka awesome
*   [http://awesome.naquadah.org/wiki/index.php?title=Main_Page](http://awesome.naquadah.org/wiki/index.php?title=Main_Page) - awesome wiki
Tato stránka je zamýšlena jako demystifikace běžných termínů používaných v komunitě kolem Arch Linuxu. Bez obav přidávejte nebo upravujte jakýkoli termín, ale používejte prosím volbu úpravy jednotlivé části. Pokud se rozhodnete něco přidat, pak prosím používejte při přidávání abecední pořadí.

## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 ABS](#ABS)
*   [3 AUR](#AUR)
*   [4 PKGBUILD](#PKGBUILD)
*   [5 TU, Trusted User](#TU.2C_Trusted_User)
*   [6 TUR, Trusted User Repository (zastaralé)](#TUR.2C_Trusted_User_Repository_.28zastaral.C3.A9.29)
*   [7 bbs](#bbs)
*   [8 community/[community]](#community.2F.5Bcommunity.5D)
*   [9 core/[core]](#core.2F.5Bcore.5D)
*   [10 custom/user repository](#custom.2Fuser_repository)
*   [11 developer](#developer)
*   [12 devfs](#devfs)
*   [13 /etc/network-profiles](#.2Fetc.2Fnetwork-profiles)
*   [14 /etc/rc.conf](#.2Fetc.2Frc.conf)
*   [15 /etc/rc.d](#.2Fetc.2Frc.d)
*   [16 /etc/rc.local](#.2Fetc.2Frc.local)
*   [17 extra/[extra]](#extra.2F.5Bextra.5D)
*   [18 hwd](#hwd)
*   [19 hwdetect](#hwdetect)
*   [20 initramfs](#initramfs)
*   [21 initrd](#initrd)
*   [22 makepkg](#makepkg)
*   [23 namcap](#namcap)
*   [24 package](#package)
*   [25 pacman](#pacman)
*   [26 pacman.conf](#pacman.conf)
*   [27 release/[release]](#release.2F.5Brelease.5D)
*   [28 repository/repo](#repository.2Frepo)
*   [29 RTFM](#RTFM)
*   [30 taurball](#taurball)
*   [31 testing/[testing]](#testing.2F.5Btesting.5D)
*   [32 udev](#udev)
*   [33 wiki](#wiki)

## Arch Linux

Na Arch by se mělo odkazovat takto:

*   **Arch Linux**
*   **Arch** (Linux je implicitní)
*   **archlinux** (UNIXové jméno)

Archlinux, ArchLinux, archLinux, aRcHlInUx, a tak dále, jsou všechny divné, a divnější mutace.

Oficiálně, 'Arch' v názvu "Arch Linux" se vyslovuje /ˈɑrtʃ/ jako v "archer"/bowman, nebo "arch-nemesis", a ne jako "ark" nebo "archangel".

## ABS

Arch Build System (zkratka ABS) je užitečný k:

*   Tvorba nových balíčků softwaru, pro který ještě nejsou balíčky dostupné
*   Přizpůsobení/Úprava existujících balíčků, tak aby vyhovovaly vašim potřebám (povolení nebo zákázání určitých voleb)
*   Sestavení celého systém za použití voleb kompilace "a la Gentoo"
*   Udělat funkční jaderné moduly s vaším uživatelským jádrem

ABS není nutné k používání Arch Linuxu, ale je užitečné.

Pro více informací viz stránka [ABS](/index.php/ABS "ABS")

## AUR

Arch Linux User Community Repository (AUR) je repozitář řízený komunitou pro uživatele Arch Linuxu. AUR byl zpočátku koncipován k organizaci sdílení PKGBUILDů mezi širší komunitou a k uspíšení zahrnutí populárních balíčků přidaných uživateli do [core] a [extra] repozitářů skrze AUR [community] repozitář.

AUR je rodiště nových balíčků Arch Linuxu. Uživatelé přispívají svými vlastními balíčky do AUR. AUR komunita hlasuje pro své favoritní balíčky a eventuálně, jakmile balíček nasbíral dost hlasů, AUR Trusted User (důveryhodný uživatel) může tento balíček dát do repozitáře [community], který je zpřístupněný přes pacman a ABS.

Můžete přistupovat do Arch Linux User Commnity Repository [zde](https://aur.archlinux.org)

## PKGBUILD

PKGBUILDy jsou malé skripty používané pro vytvoření balíčků Arch Linuxu. Viz [Creating packages](/index.php/Creating_packages "Creating packages") for více detailní informace.

## TU, Trusted User

Trusted User je někdo, kdo udržuje AUR a [commmunity] repozitář. Důvěryhodní uživatelé můžou přesouvat balíček do [community] repozitáře, pokud se stal populárním (dle hlasů). Důvěryhodní Uživatelé (TUs) jsou jmenováni většinou hlasů existujícími TUs.

Důvěryhodní uživatelé se řídí [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") a [TU by-laws](https://archlinux.org/~simo/TUbylaws.html)

## TUR, Trusted User Repository (zastaralé)

Když ještě nebyl AUR a [community], TUs měli vlastní repozitáře s aplikacemi, které nebyly dostupné v officiálních repozitářích. Kdokoli může udělat repozitář, ale TURs byly "zárukou" vyšší kvality, protože TUs jsou voleni pro svoje znalosti a práci.

## bbs

*B*ulletin *b*oard *s*ystem, ale v případě Arch Liuxu se jedná pouze o podpůrné fórum umístěné na adrese [https://bbs.archlinux.org](https://bbs.archlinux.org).

## community/[community]

community repozitář je místo, kde předvytvořené balíčky jsou zpřístupněny Důvěryhodnými Uživateli (Trusted Users). Většina balíčků v community má původ v AUR.

Pokud chcete používat community repozitář, odkomentujte příšlušnou řádku v konfiguračním souboru /etc/pacman.conf.

## core/[core]

Repozitář "Core" obsahuje balíčky holého Arch Linuxu. Obsahuje všechno, co je potřeba k fungující příkazové řádce.

## custom/user repository

Kdokoli může vytvářet repozitáře a zpřístupnit je ostatním uživatelům. K vytvoření repozitáře je třeba určitá množina balíčků a kompatibilní pacman databáze souborů vašich balíčků. Zpřístupněte vaše soubory online a kdokoli může použít váš repozitář jako běžné repozitáře.

Viz [Custom local repository](/index.php/Custom_local_repository "Custom local repository").

## developer

"Poloviční bohové" pracující na na vylepšení/rozšíření Arch Linuxu bez finančních příjmů za tuto činnost.

## devfs

*dev*ice *f*ile *s*ystem. DevFS dynamicky spravuje, vytváří, odstraňuje a pracuje s právy souborů zařízení v /dev adresáři. Byl to výchozí správce zařízení v Arch Linuxu až do vydání 0.7\. Nyní je DevFS zavrhovaný a je odstraňován z Linuxu (jádra). DevFS je nahrazen [udev](/index.php/Udev "Udev").

Poznámka: instalační CD Arch Linuxu před 0.7.1 používá scháma pojmenování devfs, když se vytváří /etc/fstab položky.

## /etc/network-profiles

Pomocí tohoto můžete vytvářet různé konfigurace sítě. Toto je velmi užitečné pro uživatele laptopů, kteří velmi často střídají sítě. Např. mezi domácí a kancelářskou sítí. Dodatečně může být použita s wpa-supplicant, který může spravovat všechny vaše bezdrátové sítě. Pro každou konfiguraci je třeba vytvořit konfigurační soubor. Nejjednoduššeji to lze udělat zkopírováním šablony. Po dokončení je třeba konfiguraci povolit v /etc/rc.conf

Po aplikování změn byste měli restartovat vaši síť použitím, jako root,

```
 /etc/rc.d/network restart

```

## /etc/rc.conf

/etc/rc.conf je hlavní konfigurační soubor Arch Linuxu. Umožňuje nastavení klávesnice, časové zóny, hostname, síť, démony, které se mají spustit, a moduly, které se mají zavést při startu systému, profily a více. Detailní popis konfiguračních volbe je zde: [Rc.conf](/index.php/Rc.conf "Rc.conf")

## /etc/rc.d

/etc/rc.d je adresář obsahující skripty, které se starají od start a zastavení služeb. Při každém startu systému, služby přítomné v poli DAEMONS= v /etc/rc.conf jsou startovány spuštěním odpovídajícího skriptu v /etc/rc.d.

Je rovněž možná řídit služby z příkazového řádku (jako root), např.

```
/etc/rc.d/cupsd start

```

by spustilo démona CUPS. Typickými argumenty těchto skriptů jsou start, stop a restart.

## /etc/rc.local

Tento skript je spuštěn na konci každého startu systému. Je určen pro různé příkazy, které byste mohli chtít vykonat před "login prompt" (přihlášení se do systému). Nedoporučuje se přidávat jakékoli služby nebo nastavení do /etc/rc.local, které by mohli být nastartovány nebo nastaveny z /etc/rc.conf.

## extra/[extra]

Množina oficiálních balíčků je dosti kompaktní, zato poskytujeme rozsáhlejší, kompletnější "extra" repozitář, který obsahuje hodně balíčků, které nebyly vytvořeny pro pro "core" množinu balíčků. Tento repozitář konstantně roste s pomocí balíčků poskytnutých naší silnou komunitou. V tomto repozitáři lze nalézt desktop environments (desktopová prostředí, např. Gnome, KDE aj.), správce oken a běžné programy.

## hwd

Hwd; hardware detect for Arch Linux, je pro devfs i pro udev a rovněž pro jádra 2.4.x a 2.6.x. Místo toho aby spouštěl auto-konfigurační skript, který může být očekáván, Hwd (/usr/bin/hwd) nemění existující konfiguraci. Detekuje hardware a moduly, a poskytuje informace, jak manuálně provést změny. Toto umožňuje uživateli kontrolu nad svým systémem; základní filozofie Arch Linuxu. Hwd je dostupný v [AUR](https://aur.archlinux.org/packages.php?ID=26913).

## hwdetect

[hwdetect](/index.php/Hwdetect "Hwdetect") je skript pro detekci hardware primárně používaný k načtení modulů a seznamu modulů pro použití v [rc.conf](/index.php/Rc.conf "Rc.conf") nebo [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). Tento skript využívá informací exportovaných sysfs subsystémem linuxového jádra.

## initramfs

## initrd

Speciální soubor /dev/initrd je blokové zařízení, které je pouze ke čtení. Zařízení /dev/initrd je RAM disk, který je inicializován (např. načten) boot manažerem, dříve než se nastartuje jádro. Jádro poté může používat obsah tohoto blokového zařízení v dvoufázovém načtení operačního systému.

V první fázi startu systému jádro spouští a přimountovává počáteční kořenový systém souborů z obsahu /dev/initrd (např. RAM disk incializovaný boot manažerem). V druhé fázi dodatečné ovladače nebo jiné moduly jsou načteny z obsahu počátečního kořenového zařízení. Po načtení dodatečných modulů je přimountován nový kořenový systém souborů (tedy běžný kořenový systém souborů) z jiného zařízení.

## makepkg

makepkg slouží k sestavení balíčků pro vás. makepkg čte metadata vyžadované z PKGBUILD souboru. Všechno, co potřebuje, je linuxová platforma schopná sestavení, wget a různé sestavovací skripty. Přednost před skriptově-založeném sestavení je v tom, že tuto práci je třeba udělat pouze jednou. Poté co máte sestavovací skript pro balíček, je třeba spustit makepkg a makepkg zajistí zbytek; stažení a ověření zdrojových souborů, kontrolu závislostí, konfigurace parametrů při sestavení, vytvoření balíčku, instalace balíčku do dočasného kořenového adresáře, změna parametrů, vygenerování meta-info, a balíček jako úplnou věc pro použití v pacman.

## namcap

namcap je utilitka pro analýzu problémů s balíčky pro Arch Linux nebo s jejich PKGBUILD soubory. Může aplikovat pravidla na seznam souborů, na soubory samy o sobě, nebo na individuální PKGBUILD soubory.

Pravidla vrací seznam zpráv. Každá zpráva může být jedním ze tří typů: chyba, varování nebo informace (uvažujte o nich jako o poznámkách či komentářích). Chyby (označovanými 'E:') jsou věci, u kterých si je namcap velmi jistý, že jsou špatné a je třeba je opravit. Varování (označované 'W:') jsou věci, o kterých si namcpa myslí, že by měly být změněny, ale pokud víte, co děláte, může tyto věci nechat být. Informace (označované 'I:') se zobrazují pouze tehdy, když použijete argument info. Informační zprávy podávají informace, které můžou být užitečné, ale nejsou to věci, které by byly třeba změnit.

## package

Package (balíček) je archiv obsahující

*   všechny (zkompilované) soubory aplikace
*   metadata o aplikaci, jako název aplikace, verze, závislosti...
*   instalační soubory a adresáře pro pacman
*   (volitelně) extra soubory, které vám ulehčují život, jako jsou start/stop skripty

Správce balíčků v Arch Linuxu může nainstalovat, aktualizovat a odebrat programy čistě těchto balíčků. Použití balíčků místo ruční kompilace a instalace má různé výhody:

*   jednoduchá aktualizace: pacman aktualizuje existující balíčky, jakmile jsou aktualizace dostupné
*   kontrola závislostí: pacman spravuje závislosti pro vás, je třeba pouze specifikovat program a pacman ho nainstaluje spolu s všemi programy, které potřebuje
*   čisté odstranění: pacman má seznam všech souborů patřících do určitého balíčku. Touto cestou nejsou ponechány žádné soubory v systému, když se rozhodnete pro odstranění balíčku

Poznámka: různé GNU/Linux distribuce používají odlišné balíčky a správce balíčků, proto nelze třeba použít pacman k instalaci balíčků Debianu na Arch Linuxu.

## pacman

Správce balíčků [Pacman](/index.php/Pacman "Pacman") je jedna z nádherných "výšin" Arch Linuxu. Kombinuje jednoduchý formát binárních balíčků s jednodušše se používajícím sestavovacím systémem (viz [ABS](/index.php/ABS "ABS")). Pacman umožňuje jednoduchou správu a přizpůsobení balíčků, ať už jsou z oficiálních Arch repozitářů nebo vytvořené samotným uživatelem. Systém repozitářů umožňuje uživateli sestavení a údržbu uživatelových vlastních repozitářů, což povzbuzuje růst komunity a přispívání (viz [AUR](/index.php/AUR "AUR")).

Pacman může udržovat systém aktualizovaný synchronizací seznamu balíčků s hlavním serverem. Tento server/klient model rozvněž umožňuje stáhnout/nainstalovat balíčky jednoduchým příkazem, doplňujícím všechny požadované závislosti (podobně jako apt-get v Debianu).

Poznámka: Pacman byl napsán Judd Vinetem, tvůrcem Arch Linuxu. Je používán rovněž jako nástroj správy balíčků v jiných distribucích, jako FugalWare, Rubix, UfficioZero (italsky, založeném na Ubuntu) a samozřejmě odvozeniny Arch Linuxu jako Archie a AEGIS.

## pacman.conf

Toto je konfigurační soubor správce balíčků, programu pacman. Nachází se v /etc. Pro úplný výklad jeho možností, napiště do příkazového řádku:

```
man pacman.conf

```

## release/[release]

Repozitář "release" následuje téměř pravidelný snímek a neaktualizuje, dokud není vydán další snímek/iso. Na příklad, Release repozitář se odkazuje na všechny balíčky na 0.5 ISO, dokud nevydáme 0.6; potom se bude odkazovat na 0.6 balíčky, dokud verze 0.7 není vydána. Toto je užitečné, pokud pouze chcete aktualizovat váš systém, když je dostupné nové vydání.

## repository/repo

Repozitář obsahuje předkompilované balíčky jednoho nebo (běžně) více PKGBUILDů. Oficiální repozitáře jsou

*   core: obsahuje nejnovější verzi balíčků vyžadovaných pro kompletní systém s příkazovou řádkou
*   extra: obsahuje nejnovější verze balíčků, které nejsou třeba pro fungující systém, ale jsou třeba pro příjemný systém ;)
*   community: obsahuje balíčky přicházející z [AUR](https://aur.archlinux.org), které získali dost hlasů od uživatelů

Pacman užívá těchto repozitářů k hledání balíčků a jejich nainstalování. Repozitář může být lokální (to jest na vašem vlastním počítači) nebo vzdálený (to jest balíčky se stahují před tím, než se nainstalují).

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

"Read The Fucking (or Fine) Manual" ("Přečti Si Ten Zasranej (nebo Skvělej) Manuál"). Tato jednoduchá zpráva je odpovědí nováčkům, kteří se ptají na funkcionalitu programu, která je jasně vymezena v manuálu k tomuto programu.

Často je používána, když sám uživatel neprojevil snahu nalezení řešení. Pokud vám někdo řekne toto, nesnaží se vás urazit, je zrovna frustrován vašim nedostatkem úsilí (při řešení problému).

Nejlepší věc, kterou byste měli udělat, pokud je vám toto řečeno, je přečíst si manuálovou stránku.

*   Ke čtení manuálové stránky programu zadejte toto do příkazového řádku:

```
man PROGRAM-NAME

```

kde POROGRAM-NAME je název programu, o kterém je třeba zjistit více informací.

Pokud nenaleznete odpověď na vaši otázku v programovém manuálu, existuje víc způsobů, jak najít odpověď. Můžete:

*   prohledat [wiki](/index.php/Special:Search "Special:Search")
*   prohledat [fórum](https://bbs.archlinux.org)
*   prohledat [e-mailové seznamy](http://www.google.com/#hl=en&q=arch+site%3Ahttp%3A%2F%2Fwww.archlinux.org%2Fpipermail%2F)
*   prohledat [web](http://www.google.com)

## taurball

PKGBUILD zabalený pomocí programu tar a lokální zdrojové soubory, které požaduje makepkg k vytvoření instalovatelného binárního balíčku. Jméno se odvozuje z praxe, kdy jsou uploudovány takové tarbally do AUR, odtud "tAURball".

## testing/[testing]

Toto je repozitář obsahující hlavní aktualizace balíčků předcházející vydání v hlavních repozitářích, tak je možné je testovat (chyby), můžou se objevit problémy s aktualizací. Ve výchozím nastavení je tento repozitář zakázán, může ale být povolen v konfiguračním souboru `/etc/pacman.conf`

## udev

[udev](/index.php/Udev "Udev") poskytuje dynamický adresář zařízení obsahující pouze ty soubory zařízení, které se aktuálně vyskytují v systému. Vytváří nebo odstraňuje soubory zařízení v /dev adresáři nebo přejmenovává síťová rozhraní.

Obvykle udev je spuštěn jako udevd(8) a příjímá události přímo z jádra, pokud nějaké zařízení je přidáno/odstraněno z/do systému.

Pokud udev přijme událost tykájící se nějakého zařízení, porovná pravidla ve svém konfiguračním souboru s dostupnými atributy zařízení poskytnutými sysfs k identifikaci zařízení. Pravidla, která odpovídají, mohou poskytovat informace o zařízení nebo specifikovat soubor zařízení nebo vícero jmen odkazů a dát pokyn udev, aby spustil dodatečné programy jako součást obsluhy události zařízení.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[Toto!](/index.php/Main_page "Main page") Místo, kde lze najít dokumentaci o Arch Linuxu. Kdokoli může přidávat a upravovat dokumentaci.
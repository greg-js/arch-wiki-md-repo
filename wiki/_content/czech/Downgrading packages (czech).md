Tento průvodce vás provede procesem návratu k předchozí (starší) verzi balíčku. Návrat k předchozí verzi (tzv. downgrade) se obvykle nedoporučuje, ale může to být nutné v případě, že nový balíček obsahuje chyby.

Než přistoupíte k návratu k předchozí verzi, zvažte dobře důvody, proč to děláte. Pokud je to kvůli chybě v balíčku, pomozte prosím Archu i původním vývojářům tím, že obětujete několik minut nahlášení chyby pomocí [Arch Bug Tracker](https://bugs.archlinux.org) nebo přímo vývojářům balíku. Protože je Arch Linux tzv. "rolling release" distribucí, budete pravděpodobě neustále setkávat s novými balíčky a čas od času i s nějakou tou chybou.

Jak my, tak původní vývojáři ocení vaše úsilí při ohlašování chyb. Každá doplňující informace může ušetřit hodiny testování a ladění a rovněž přispěje vydávání stabilnějšího software.

## Contents

*   [1 Důvody](#D.C5.AFvody)
*   [2 Podrobnosti](#Podrobnosti)
*   [3 Jak se vrátit k předchozí verzi balíčku](#Jak_se_vr.C3.A1tit_k_p.C5.99edchoz.C3.AD_verzi_bal.C3.AD.C4.8Dku)
*   [4 Jak nalézt starší verzi balíčku](#Jak_nal.C3.A9zt_star.C5.A1.C3.AD_verzi_bal.C3.AD.C4.8Dku)
    *   [4.1 Nesynchronizovaná zrcadla](#Nesynchronizovan.C3.A1_zrcadla)
    *   [4.2 Arch Rollback Machine](#Arch_Rollback_Machine)
    *   [4.3 Re-kompilace balíčku](#Re-kompilace_bal.C3.AD.C4.8Dku)
*   [5 Další informace](#Dal.C5.A1.C3.AD_informace)
*   [6 A co závislosti?](#A_co_z.C3.A1vislosti.3F)
*   [7 Jak zabránit pacmanu v aktualizaci balíčku](#Jak_zabr.C3.A1nit_pacmanu_v_aktualizaci_bal.C3.AD.C4.8Dku)
*   [8 Návrat k předchozímu stavu souborového systému](#N.C3.A1vrat_k_p.C5.99edchoz.C3.ADmu_stavu_souborov.C3.A9ho_syst.C3.A9mu)

## Důvody

Proces návratu k předchozí verzi spočívá v odebrání novějšího balíčku a instalace předchozí verze. Předchozí verzí se rozumí bezprostředně předchozí verze balíčku nebo prostě některá ze starších verzí.

Důvody pro návratu k předchozí verzi mezi jinými jsou: nová verze obsahuje chybu, nová verze neposkytuje požadovanou funkčnost nebo experimentujeme s verzemi balíčků. V každém případě je třeba zvážit zda návrat k předchozí verzi nepřinese více problémů než prostě počkat na vydání nové verze balíčku.

Návrat k předchozí verzi jednoho balíčku může způsobit, že bude nutné použít i jiné balíčky starších verzí. Pro ty, kteří nainstalovali větší množství experimentálních balíčků z repozitáře testing může být vhodnější přistoupit spíše k reinstalaci systému než ke snížení verze balíčku.

## Podrobnosti

Každý uživatel musí mít na mysli následující. Především je třeba uvážit závislosti každé aplikace, jejíž verzi snižujeme. S novou verzí aplikace se občas mění verze knihoven, které požaduje a rovněž funkčnost poskytovaná knihovnami se verze od (i zcela) verze liší. Řešení pak vyžaduje návrat k předchozí verzi vyžadovaných knihoven (tedy dalších balíků).

Za druhé, je se ujistit, zda potřebné soubory starších verzí balíčků již nebyly ze systému odstraněny, případně zda jsou dostupné z jiných zdrojů. Repozitáře Arch linuxu respektují princip "rolling release" a neobsahují starší verze balíčků. Viz. níže.

Za třetí, musíme brát ohled na související konfigurační soubory a skripty. V současnosti se při návratu k předchozím verzím balíčků spoléháme na nástroj pacman, který nám ovšem nezaručí i odpovídající změnu konfiguračních souborů.

Problematika snižování verze balíčků souvisí s nejnovějším vývojem balíčkovacího systému. Celý koncept [Arch Rollback Machine](#Arch_Rollback_Machine) (viz níže) se aktivně vyvíjí a očekává se jeho použitelné začlenění do nástroje pacman. Až k tomu dojde, bude tento proces automatizován. Do té doby platí následující instrukce.

## Jak se vrátit k předchozí verzi balíčku

*   Otázka: Použil jsem příkaz `pacman -Syu` a balíček *ABC* byl aktualizován z verze N na verzi M. Nový balíček ovšem způsobuje problémy, jak se vrátím od verze balíčku M ke starší verzi tohoto balíčku - N?
*   Odpověď: Jednoduše se podívejte do adresáře `/var/cache/pacman/pkg` ve vašem systému, nachází-li se zde starší verze dotčeného balíčku. (Pokud jste v nedávné době nepoužili příkaz `pacman -Scc`, měli byste ho zde najít.) Pak nainstalujete starší verzi balíčku příkazem: `pacman -U /var/cache/pacman/pkg/stary_balicek-stara_verze.pkg.tar.gz`.

Tento proces odebere nový balíček, vyřeší potřebné změny v závislostech mezi balíčky a nainstaluje starší verzi balíčku i s potřebnými závislostmi.

**Note:** Pokud tímto způsobem změníte základní část OS, ovlivníte doslova tisíce závislých balíčků, které nahradíte jejich staršími verzemi. Pak můžete skončit jako Popelka přebírající balíčky a opět aktualizující jeden po druhém, aniž by změnila ten jeden, o který jde.

V uživatelském repozitáři [AUR](/index.php/AUR "AUR") je nástroj [downgrade](https://aur.archlinux.org/packages/downgrade/). Je to jednoduchý bash skript, který ověří v adresáři obsahujícím místní cache přítomnost starší verze balíčku. Nenajde-li ji zde, prohledá [ARM](#Arch_Rollback_Machine) a pak nabídne k výběru starší verzi balíčku k instalaci. V podstatě automatizuje proces naznačený výše. Viz. `downgrade --help` pro návod k použití.

Mocnějším nástrojem je [downgrader](https://aur.archlinux.org/packages.php?ID=50246), který pracuje přímo s logy pacmana, umí hledat starší verze balíčků v adresáři cache, v repozitáři [ARM](#Arch_Rollback_Machine) a dokáže pracovat i se seznamy balíčků (pro případ kdy je systém nestabilní po aktualizaci více balíčků a vy nevíte, který to způsobuje).

## Jak nalézt starší verzi balíčku

Zde máme tři možnosti.

### Nesynchronizovaná zrcadla

Když nemůžete najít potřebnou starší verzi balíčku, podívejte se, jestli některé ze zrcadel oficiálních repozitářů není v nesynchronním stavu (out of sync). Na této stránce naleznete [stav zrcadel](http://users.archlinux.de/~gerbra/mirrorcheck.html) repozitářů. (Poznámka: tato stránka je německy a nás zajímá v přehledu repozitářů sloupec "Verzögerung".)

Také můžete vyzkoušet tento repozitář, který ukládá staré balíčky:

*   [http://schlunix.org/?page_id=11](http://schlunix.org/?page_id=11)

### Arch Rollback Machine

[Arch Rollback Machine](http://arm.konnichi.com/) (ARM) obsahuje archiv všech oficiálních repozitářů zpětně až do listopadu 2009\. Verze balíčků starších než 1.11.2009 již neobsahuje; balíčky od 1\. října 2008 byly ztraceny.

Zajímá.li vás ARM, přečtěte si [toto vlákno](https://bbs.archlinux.org/viewtopic.php?id=53665) v diskusním fóru, dozvíte se nejnovější informace o jeho vývoji.

Jak se v tomto vláknu mimo jiné dozvíte cílem ARMu je poskytnou vhodně konstruovanou url, aby mohl jednoduchý skript využívající wget a pacman zajistit snadný návrat všech balíčků systému k určitému datu. Proces, jak by toto mohlo být automatizováno, není zatím jasný. Pokud ovšem budete chtít snížit verzi jednotlivého balíčku, jednoduše použijte toto [vyhledávání v systému ARM](http://arm.konnichi.com/search/).

### Re-kompilace balíčku

V nejhorším případě - pokud není potřebná verze balíčku z žádného zdroje dostupná,budete muset sami zkompilovat starší verzi . K tomu budete potřebovat odpovídající PKGBUILD; můžete upravit stávající PKGBUILD, který poskytuje ABS, aby použil starší zdrojový kód nebo můžete získat zdrojové kódy z verzovacího systému GIT, který najdete zde: [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) a balíček vytvořit pomocí makepkg.

## Další informace

Základní kontrolu nad správou balíčků nám poskytuje konfigurace uložená v souboru pacman.conf. Pro jeho úpravu je třeba se přihlásit v konzoli jako root a použít příkaz `nano /etc/pacman.conf`. (V některých případech je to možné udělat pomocí správce běžícího v grafickém rozhraní jako je například Shaman, častěji je vhodnější použít CLI. Je doporučeno vyčistit tento soubor o balastu, když už je otevřen.

**Note:** Pozn. překl.: Shaman je dnes již "mrtvá" aplikace a žádný balast se v pacman.conf objevit nemůže. Změny v pacman.conf provádí sám pacman při aktualizaci sama sebe a ukládá je jako návrh konfigurace ve tvaru pacman.conf.pacnew. Jediný balast si tam může zavést sám uživatel experimentováním s neoficiálními repozitáři a pak o něm samozřejmě ví.

Změnit repozitáře ve kterých pacman hledá aktualizované balíčky je jednoduché. Zapsáním znaku "#" na začátek řádku s adresou libovolného repozitáře vyřadíme tento repozitář z těch, ve kterých pacman hledá aktualizované balíčky.

Například, přidání repozitáře ARM spočívá v pouhém zakomentování odpovídajícího oficiálního repozitáře a přidáním tohoto řádku:

```
[core]
#Server=http://mirrors.gigenet.com/archlinux/core/os/i686
Server=http://arm.konnichi.com/2009/11/01/core/os/i686

```

Takto zadaný repozitář ARMu poskytne verze balíčků aktuální k 1.1.2009 (viz. část relativní cesty "../2009/11/01/..). Uvědomte si, že všechny repozitáře ARMu jsou otisky oficiálních repozitářů. Stačí pak jen nastavit ARM jako prioritní zrcadlo v souboru `/etc/pacman.d/mirrorlist` zapsáním http://arm.konnichi.com/2009/11/01/$repo/os/i686 na první řádek, aby došlo k nahrazení všech oficiálních repozitářů uvedených v `/etc/pacman.conf` a pak "aktualizovat" systém příkazy:

```
pacman -Syy  # obnovení databáze balíčků
pacman -Suu  # snížení verze všech balíčků, jejichž verze v repozitáři je starší než ve vašem systému

```

To samo o sobě nezajistí hladký návrat k předchozímu stavu celého systému, často dojde ke konfliktům mezi verzemi balíčků. V takovém případě můžeme použít globální repozitář [http://arm.konnichi.com/core/os/i686](http://arm.konnichi.com/core/os/i686), který poskytuje všechny verze balíčků; povšimněte si chybějícího datumu v relativní cestě.

**Note:** Pozn. překl.:

**ARM funguje takto:**

```
* repo `[http://arm.konnichi.com/2009/11/01/core/os/i686](http://arm.konnichi.com/2009/11/01/core/os/i686)` poskytuje obraz balíčků oficiálního repa pro architekturu i686 `core` k datu uvedenému v cestě.
* repo `[http://arm.konnichi.com/core/os/i686](http://arm.konnichi.com/core/os/i686)` poskytuje dostupné verze balíčků pro arch. i686, které obsahovalo oficiální repo `core` až k 1.1.2009\. 
* podobně repo `[http://arm.konnichi.com/extra/os/x86_64](http://arm.konnichi.com/extra/os/x86_64)` obsahuje všechny balíčky, které obsahoval oficiální repozitář extra, tentokrát pro x86_64\. 

```

Tyto globální repozitáře jsou tedy vhodné pro instalaci pomocí příkazu `pacman -U url` - ano, můžete pacmanu předhodit přímo url souboru v repu, např. `pacman -U [http://arm.konnichi.com/core/os/i686/acl-2.2.48-1-i686.pkg.tar.gz](http://arm.konnichi.com/core/os/i686/acl-2.2.48-1-i686.pkg.tar.gz)`. Závislosti budete muset ovšem řešit ručně, opět instalací dalších balíčku z ARMu.

Snížení verze balíčků napříč celým systémem, k nějakému vzdálenějšímu datu, jak je popsán výše, vysloveně nedoporučuji - i kdybyste uspěli, nebudete mít instalovány důležité a bezpečnostní aktualizace, když už se do toho pustíte, je dobré postoupit např. jen o jeden den zpět a to v případě, že potřebujete rychle funkční systém a nevíte, který balíček chybu způsobuje. Obecně snižování verze čehokoli, co je v repozitáři `core` je dobré se pokud možno vyvarovat.

**Konfigurace pacman.conf:**

Zápis repozitáře v pacman.conf v současné době vypadá takto:

```
[extra]
#SigLevel = PackageOptional
Include = /etc/pacman.d/mirrorlist

```

Všechny oficiální repozitáře tedy použijí preferované zrcadlo ze souboru /etc/pacman.d/mirrorlist. Pamatujte, že pokud jako preferované zrcadlo nastavíte ARM ovlivníte nastavení VŠECH oficiálních repozitářů najednou, ale naopak neovlivníte nastavení neoficiálních repozitářů, které můžete mít přímo v pacman.conf, protože ty obvykle nemají žádná zrcadla.

Přesměrování jednoho z oficiálních repozitářu na ARM provedete takto:

```
[extra]
#SigLevel = PackageOptional
#Include = /etc/pacman.d/mirrorlist
Server = [http://http://arm.konnichi.com/2012/01/30/extra/os/i686/](http://http://arm.konnichi.com/2012/01/30/extra/os/i686/)  #stav repa extra k 30.1.2012

```
Ne vždy je třeba rovnou přistupovat ke snížení verze. Častěji, než, že nový balíček obsahuje chybu jsme v situaci, kdy potřebujeme starší již nevyvíjenou aplikaci, která vyžaduje starší verzi sdílené knihovny. Pak je vhodné se nejprve porozhlédnout po AURu, zda již někdo potřebnou knihovnu neposkytuje (např. knihoven libpng nebo libjpeg je v AUR i několik starších verzí, které, lze mít v systému současně).

## A co závislosti?

*   Q: Nemohu snížit verzi balíčku ABC kvůli závislostem.
*   A: Můžete při instalaci ignorovat závislosti použitím přepínače 'd', tj. **pacman -Ud stary_balicek-stara_verze.pkg.tar.gz**, ale riskujete, že se víc věcí rozbije než spraví.

## Jak zabránit pacmanu v aktualizaci balíčku

*   Q: Jak zabránit pacmanu v aktualizaci již instalované starší verze balíčku?
*   A: Použijte proměnnou "IgnorePkg"v souboru `/etc/pacman.conf`.

`"IgnorePkg = stary_balicek_1 stary_balicek_1 ..."` v souboru `pacman.conf` přikáže pacmanu tyto balíčky při aktualizaci systému ignorovat.

## Návrat k předchozímu stavu souborového systému

*   Q: Chtěl bych se prostě vrátit do stavu v jakém byl můj systém včera.
*   A: Toho snadno dosáhnete pomocí tzv. pravidelných snapshotů, které poskytuje systém LVM - viz. [LVM](/index.php/LVM "LVM").
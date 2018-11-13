Následujících pět principů obsahuje to, co se obvykle označuje jako *Cesta Arch Linuxu* (z ang. *The Arch Way*), nebo *Filozofie Arch Linuxu*, nejlépe jsou shrnuty zkratkou KISS (*Keep It Simple, Stupid* čili *Udělej to jednoduché, hlupáku*).

## Contents

*   [1 Jednoduchost](#Jednoduchost)
*   [2 Správnost kódu před pohodlím](#Správnost_kódu_před_pohodlím)
*   [3 Zaměření na uživatele](#Zaměření_na_uživatele)
*   [4 Otevřenost](#Otevřenost)
*   [5 Svoboda](#Svoboda)

## Jednoduchost

*Jednoduchost je nejvyšší formou dokonalosti.* — Leonardo da Vinci

Jednoduchost je naprosto základním cílem vývoje Archu. Mnoho distribucí GNU/Linuxu definuje sebe sama jako "jednoduché". Ovšem jednoduchost může být definována různě.

**Arch Linux definuje jednoduchost jako *bez zbytečných přídavků, změn nebo komplikací*, a poskytuje odlehčenou základní `UNIX`-like strukturu umožňující uživatelům utvářet systém podle svých vlastních potřeb. Krátce: elegantní, minimalistický přístup.**

Odlehčená základní struktura splňující vysoké programátorské standardy bude mít nižší požadavky na systémové zdroje. Základní systém je zbaven veškeré veškeré přeplácanosti, která by mohla zamlžit důležité součásti systému, nebo způsobit, že přístup k nim je složitý. Arch má zmodernizované, stručně komentované a čisté konfigurační soubory, které jsou přizpůsobeny pro rychlý přístup a editaci, bez neohrabaných grafických konfiguračních nástrojů skrývjících možnosti před uživateli. Systém Arch Linuxu je tedy snadno konfigurovatelný do nejmenšího detailu.

**Komplexnost bez komplikací.**

Arch Linux ponechává nezbytné složitosti systému GNU/Linux, udržuje je dobře organizované a transparentní. Vývojáři a uživatelé Arch Linuxu věří, že snaha skrýt složitosti systému vede ve skutečnosti k ještě složitějšímu systému, měli bychom se jí proto vyvarovat.

## Správnost kódu před pohodlím

*Správnost je jasně základní kvalitou. Pokud systém nedělá to co by měl, pak na všem ostatním záleží velmi málo.* — Bertrand Meyer

Arch Linux klade upřednostňuje eleganci návrhu a čistotu, správnost a jednoduchost kódu před zbytečným záplatováním, automatizací, líbivostí nebo přivětivostí pro nováčky. Softwarové záplaty jsou proto používány naprosto minimálně; v ideálním případě nikdy. Jednoduchý návrh a implementace vždy předčí jednoduché uživatelské rozhraní.

**Jednoduchost *implementace*, elegance kódu a minimalismus vždy budou hlavními prioritami vývoje Arch Linuxu.**

Koncepty, návrhy a funkce jsou generované a implementované užitím principů Arch Way, externí vlivy jsou drženy stranou. Vývojový tým Archu je pevný ve svém oddání filozofii Arch Way. Pokud sdílíte jejich vizi, jste vítání používat Arch.

## Zaměření na uživatele

Zatímco mnohé distribuce GNU/Linuxu se snaží být *uživatelsky přátelské* (z ang. *user-friendly*), Arch Linux vždy byl a bude *zaměřený na uživatele* (z ang. *user-centric*).

**Arch Linux se zaměřuje na schopné uživatele GNU/Linuxu, uživatele činí středem systému a dává jim plnou kontrolu a *odpovědnost* nad systémem.**

Uživatelé Arch Linuxu si systém spravují naprosto sami. Systém nabízí pouze velmi malou asistenci, kromě jednoduchých nástrojů pro správu, které jsou vytvořeny tak, že přesně předávají uživatelovy příkazy systému. Vývojáři Archu neplýtvají energií na vytváření zcela nových grafických nástrojů pro správu systému; Arch je založen na rozumném návrhu a excelentní dokumentaci.

Zaměření na uživatele také nezbytně znamená přístup "udělej si sám". Spíše než požadovat novou funkci od vývojářů, uživatelé Arch Linuxu mají tendenci řešit problémy sami a poté sdílejí své výsledky s komunitou a vývojářským týmem -- přístup "nejdřív si to zkus sám a pak se teprve ptej". To se týká zejména balíčků v Arch User Repository -- oficiálním repozitáři Arch Linuxu pro balíčky spravované komunitou.

## Otevřenost

Otevřenost jde ruku v ruce s jednoduchostí a je také jedním z vůdčích principů vývoje Arch Linuxu.

**Arch Linux používá jednoduché nástroje, které jsou vybrány nebo vytvořeny s ohledem na otevřenost zdrojového kódu i výstupů.**

Otevřenost odstraňuje všechny překážky a abstrakce mezi uživatelem a systémem, dává uživateli více kontroly nad systémem a zároveň zjednodušuje správu systému.

Otevřenost Arch Linuxu také znamená strmější křivku učení, ale zkušení uživatelé Arch Linuxu spíše považují ostatní, uzavřenější systémy za mnohem složitěji ovladatelné.

Princip otevřenosti se rozšiřuje na členy komunity, uživatelé Arch Linuxu jsou velmi ochotní pomoct, poradit nebo přispět komunitě.

## Svoboda

Dalším principem Arch Linuxu je svoboda. Uživatelé nejen činí všechna rozhodnutí o konfiguraci svého systému, ale také rozhodují o tom, jaký systém **bude**.

**Protože systém je jednoduchý, Arch Linux poskytuje svobodu provést s ním jakoukoli změnu.**

Čerstvě nainstalovaný Arch Linux poskytuje pouze základní komponenty bez automatické konfigurace. Uživatelé jsou schopni konfigurovat systém podle svých přání z příkazové řádky. Od začátku instalace je možno každou komponentu odstranit nebo nahradit jinou alternativou.

Velké množství balíčků a sestavovacích skriptů v různých repozitářích Arch Linuxu také podporuje svobodu volby, poskytují svobodný a otevřený software pro ty, kteří ho preferují, a proprietární software pro ty, kteří preferují *funkčnost před ideologií*. Uživatel je ten, kdo činí rozhodnutí.

Jak řekl Judd Vinet, zakladatel Arch Linuxu: "[Arch Linux] je takový, jakým si ho *vy* uděláte".
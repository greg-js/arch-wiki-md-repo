_Jelikož je kolem oficiálních repozitářů spousta zmatků, tento článek se pokouší vysvětlit jejich význam._

## Contents

*   [1 Úvod – co je to repozitář?](#.C3.9Avod_.E2.80.93_co_je_to_repozit.C3.A1.C5.99.3F)
*   [2 Historické pozadí](#Historick.C3.A9_pozad.C3.AD)
*   [3 [core]](#.5Bcore.5D)
*   [4 [extra]](#.5Bextra.5D)
*   [5 [community]](#.5Bcommunity.5D)
*   [6 [testing]](#.5Btesting.5D)
*   [7 [community-testing]](#.5Bcommunity-testing.5D)
*   [8 AUR nebo-li [unsupported]](#AUR_nebo-li_.5Bunsupported.5D)

## Úvod – co je to repozitář?

Slovo repozitář z anglického slova "repository" znamená schránka, úschovna, skladiště nebo zdroj. V souvislosti s balíčkovacími systémy linuxových distribucí repozitář představuje nejčatěji server (ale může to být i lokální adresář nebo vyměnitelný disk), na kterém jsou fyzicky umístěny softwarové balíčky připravené pro instalaci do systému. Těchto repozitářu (jak uvidíte v textu níže) existuje většinou více podle účelu, pro který jsou určeny (stabilní software, software k testovaní, ...). Software z připravených repozitářů můžete pohodlně instalovat pomocí správce balíčků – v případě Arch Linuxu se jedná o [pacmana](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"). Jediné, co musíte udělat, je nastavit v konfiguračním souboru správce balíčků adresy (cesty) k repozitářům a aktualizovat databází dostupných baličků, které se ve zvolených repozitářích nacházejí.

## Historické pozadí

Většina rozdělení repozitářů má historické důvody. Původně, když byl Arch Linux používán jen velmi malým počtem uživatelů, byl pouze jeden repozitář jménem _[official]_ (nyní **[core]**). Toho času obsahoval [official] v podstatě aplikace upřednostňované Juddem Vinetem. Byl navržen tak, aby obsahoval jediný od každého "typu" programu -- jedno desktopové prostředí, jeden hlavní prohlížeč atd.

Přirozeně se tehdy vyskytli uživatelé, kterým se výběr Judda nelíbil. Díky jednoduchosti používání [ABS](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)") si vytvářeli balíčky vlastní. Tyto balíčky šly do repozitáře nazvaného _[unofficial]_ a byly spravovány jinými vývojáři než Juddem. Časem se tyto dva repozitáře staly ze strany vývojářů podporované na stejné úrovni, takže již jména [official] a [unofficial] dále neodrážely jejich pravý účel. Posléze byly někdy poblíž verze vydání 0.5 přejmenovány na _[current]_ a _[extra]_.

Krátce po vydání 2007.8.1 byl [current] přejmenován na [core], aby se předešlo zmatkům ohledně jeho přesného obsahu. Repozitáře jsou nyní v očích vývojářů a komunity víceméně rovnocenné, ale u [core] jsou jisté rozdíly. Hlavní odlišnost je v tom, že pro instalační CD a ukázková vydání jsou použité _pouze_ balíčky z [core]. Tento repozitář poskytuje kompletní linuxový systém, i když to ještě nemusí být linuxový systém, který byste chtěli.

Kolem 0.5 nebo 0.6 zjistilo, že je spousta balíčků, které vývojáři nechtěli udržovat. Jeden z vývojářů (Xentac) založil "repozitáře pro důvěryhodné uživatele" (Trusted User Repositories), což byly neoficiální repozitáře, do kterých mohli důvěryhodní uživatelé umisťovat balíčky, které vytvořili. Existoval repozitář _[staging]_, odkud mohly být balíčky někým z vývojářů Arch Linuxu povýšeny do oficiálních repozitářů, ale jinak byli vývojáři a důvěryhodní uživatelé víceméně oddělení.

Takto to po nějakou dobu fungovalo, ale problém nastal, když byli důvěryhodní uživatelé svými repozitáři znudění a nebo když chtěli nedůvěryhodní uživatelé sdílet své vlastní balíčky. To vedlo k vývoji [AUR](https://aur.archlinux.org/). Důvěryhodní uživatelé (anglicky Trusted Users nebo zkráceně TU) byli spojeni do více provázané skupiny a nyní kolektivně udržují repozitář **[community]**. Jsou odděleni od vývojářů Arch Linuxu a moc s nimi nekomunikují, nicméně oblíbené balíčky jsou stále příležitostně povyšovány z [community] do **[extra]**. [AUR](https://aur.archlinux.org) též umožňuje nedůvěryhodným uživatelům, pokud chtějí, dát své PKGBUILDy k dispozici jiným uživatelům. Tyto balíčky nejsou podporovány a občas se jim říká repozitář **[unsupported]**, i když jelikož nejsou distribuovány žádné binární balíčky, ve skutečnosti to ani repozitář není. Důvěryhodní uživatelé mohou na základě vlastního úsudku adoptovat balíčky z [unsupported] do [community], ať už to je kvůli popularitě balíčku nebo jejich zájmu o jeho udržování.

## [core]

Repozitář [core] můžete najít v _core/os/i686_ nebo _core/os/x86_64_ na svém oblíbeném zrcadle. Obsahuje základní balíčky Arch Linuxu a některý rozšiřující software a poskytne vám plně funkční základní systém.

_Instalační CD obsahuje jednoduše instalační skript a obsah repozitáře core z některého dne._

## [extra]

Repozitář [extra] můžete najít v _extra/os/i686_ nebo _extra/os/x86_64_ na svém oblíbeném zrcadle. Obsahuje všechny balíčky, které nezapadají do [core] – například X.org, okenní správci, webové servery, multimediální přehrávače, jazyky jako Python, Ruby a Perl a mnoho dalších.

## [community]

Repozitář [community] můžete najít v _community/os/i686_ nebo _community/os/x86_64_ na svém oblíbeném zrcadle. Je udržován _důvěryhodnými uživateli_ (Trusted Users) a je součástí _AUR_. Obsahuje ty balíčky z _AUR_, které obdržely dostatečný počet hlasů a byly adoptovány některým z _důvěryhodných uživatelů_.

## [testing]

Repozitář [testing] můžete najít v _testing/os/i686_ nebo _testing/os/x86_64_ na svém oblíbeném zrcadle. [testing] je zvláštní tím, že obsahuje balíčky, které jsou kandidáty na přesun do repozitářů [core] nebo [extra]. Nové balíčky do [testing] putují, pokud:

*   se očekává, že něco mohou při aktualizaci rozbít, a musí tak být nejprve otestovány
*   vyžadují znovusestavení jiných balíčků. V tomto případě jsou všechny balíčky, které musí být znovu sestaveny, umístěny nejprve do [testing] a když je jejich sestavování dokončeno, jsou přesunuty zpět do ostatních repozitářů.

[testing] je jediným repozitářem, jehož jména balíčků smí kolidovat s jakýmkoliv jiným oficiálním repozitářem. Pokud je povolen, musí být prvním repozitářem v souboru _pacman.conf_.

Při povolení [testing] buďte opatrní. Váš systém se může po aktualizaci s povoleným repozitářem [testing] rozbít. Měli by ho používat pouze zkušení uživatelé, kteří vědí, jak si případně poradit s rozbitým systémem.

Repozitář [testing] není určen pro "nejnovější z nejnovějších" verze balíčků. Jeho částečný účel je pozdržet aktualizace balíčků, které mají potenciál způsobit rozbití systému, ať už proto, že jsou součástí balíčků v [core], nebo kvůli nějakým jiným důvodům. Proto jsou uživatelé repozitáře [testing] silně vyzýváni zapsat se na (anglický) mailing list arch-dev-public a ohlašovat všechny bugy na bug tracker.

## [community-testing]

Repozitář [community-testing] je podobný repozitáři [testing], ale je určen pro balíčky, které jsou kandidáty pro vstup do repozitáře [community].

## AUR nebo-li [unsupported]

[AUR](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)") (z anglického Arch User Repository) ve skutečnosti není vůbec repozitářem. Odkazuje na databázi skriptů pro sestavování balíčků, též známých jako PKGBUILD soubory, kterými přispěli sami uživatelé, proto je tento repozitář skutečně neoficiální. Uživatelé nemohou stahovat nebo instalovat balíčky z [AUR](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)") pomocí [pacmana](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"). Musí nejprve stáhnout soubory nutné pro sestavení balíčku a spustit program [makepkg](/index.php?title=Makepkg_(%C4%8Cesky)&action=edit&redlink=1 "Makepkg (Česky) (page does not exist)"), který stáhne zdrojové soubory a postará se o samotné sestavení balíčku. Tyto lokálně sestavené balíčky lze posléze nainstalovat pomocí [pacmana](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"). K automatizaci tohoto procesu lze použít některý z populárních [AUR pomocníků](/index.php?title=AUR_Helpers_(%C4%8Cesky)&action=edit&redlink=1 "AUR Helpers (Česky) (page does not exist)").
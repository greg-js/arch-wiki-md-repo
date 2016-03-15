## Contents

*   [1 Na začátek](#Na_za.C4.8D.C3.A1tek)
*   [2 backup soubory balíčků](#backup_soubory_bal.C3.AD.C4.8Dk.C5.AF)
*   [3 Popis druhů](#Popis_druh.C5.AF)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
    *   [3.3 .pacorig](#.pacorig)
*   [4 Lokalizace *.pac* souborů](#Lokalizace_.2A.pac.2A_soubor.C5.AF)
*   [5 Nástroje pro soubory .pacnew](#N.C3.A1stroje_pro_soubory_.pacnew)
*   [6 Zdroje](#Zdroje)

## Na začátek

Při upgradech nebo odstraňování balíčků vás [Pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)") čas od času informuje o souborech (obvykle konfiguračních v `/etc`), jenž jsou instalovány s příponou `.pacnew` nebo zálohovány s příponou `.pacsave`.

Soubor `.pacnew` může být vytvořen při upgradu balíčku (`pacman -Syu`, `pacman -Su` nebo `pacman -U`), aby se zamezilo přepsání již existujícího souboru, který byl předtím změněn uživatelem. Když tato situace nastane, ve výstupu pacmanu se objeví zpráva podobná následující:

```
warning: /etc/pam.d/usermod installed as /etc/pam.d/usermod.pacnew

```

Soubor `.pacsave` může být vytvořen při odstraňování balíčku (`pacman -R`) nebo jeho upgradu (balíček musí být nejdříve odstraněn). Když má databáze pacmanu záznam o tom, že by měl být jistý soubor vlastněný balíčkem zálohován, vytvoří soubor `.pacsave`. Když tato situace nastane, pacman zobrazí zprávu podobnou následující:

```
warning: /etc/pam.d/usermod saved as /etc/pam.d/usermod.pacsave

```

Tyto soubory vyžadují ruční zásah uživatele a je dobrým zvykem po každém upgradu nebo odstranění balíčku tuto situaci nějak vyřešit. V opačném případě mohou nesprávné konfigurace vyústit ve špatnou funkci softwaru nebo jeho neschopnost se vůbec spustit.

## `backup` soubory balíčků

Soubor `PKGBUILD` balíčkům určuje, které soubory mají být při upgradu nebo odstranění dotyčného balíčku zachovány nebo zálohovány. Například `PKGBUILD` pro `pulseaudio` obsahuje následující řádek:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

## Popis druhů

Různé druhy *.pac* souborů.

### .pacnew

Pro každý `backup` soubor, který je v právě upgradovaném balíčku, pacman vzájemně porovnává tři kontrolní součty MD5 generované z obsahu daného souboru: jeden součet pro verzi nainstalovanou původním balíčkem, jeden pro verzi momentálně sídlící v souborovém systému a jeden pro verzi z nového balíčku. Pokud současná verze ze souborového systému byla v minulosti ručně upravena, pacman nedokáže sloučit tyto změny s novou verzí souboru. Proto při upgradu namísto přepisování změněného souboru pacman uloží novou verzi s příponou `.pacnew` a ponechá stávající změnenou verzi nedotčenou.

Pokud zajdeme více do detailů, toto trojcestné srovnání součtů MD5 může skončit s jedním z následujících výsledků:

	původní = *X*, současný = *X*, nový = *X* 

	Všechny tři verze souboru mají shodný obsah, přepsání tedy není problém. Přepsat současnou verzi novou verzí a neoznamovat nic uživateli. (I když je obsah souboru shodný, toto přepsání zaktualizuje v souborovém systému informace ohledně času instalace, změny a přístupu k souboru. Zajistí též jakoukoliv změnu přístupových práv souboru.)

	původní = *X*, současný = *X*, nový = *Y* 

	Obsah současné verze je shodný s původní, ale nová verze je rozdílná. Jelikož uživatel v minulosti neupravil současnou verzi a nová verze může obsahovat vylepšení nebo opravy, přepsat současnou verzi novou verzí a neoznamovat nic uživateli. Toto je jediné automatické slučování změn, které pacman dokáže vykonávat.

	původní = *X*, současný = *Y*, nový = *X* 

	Původní balíček a nový balíček oba obsahují shodnou verzi souboru, ale verze momentálně sídlící v souborovém systému byla změněna. Ponechat současnou verzi, jak je, a zahodit novou verzi bez oznámení uživateli.

	původní = *X*, současný = *Y*, nový = *Y* 

	Nová verze je shodná se současnou. Přepsat současnou verzi novou verzí a neoznamovat nic uživateli. (I když je obsah souboru shodný, toto přepsání zaktualizuje v souborovém systému informace ohledně času instalace, změny a přístupu k souboru. Zajistí též jakoukoliv změnu přístupových práv souboru.)

	původní = *X*, současný = *Y*, nový = *Z* 

	Všechny tři verze jsou rozdílné. Ponechat současnou verzi, nainstalovat novou verzi s příponou `.pacnew` a varovat uživatele ohledně nové verze. Od uživatele se očekává, že ručně sloučí jakékoliv nutné změny z nové verze do té současné.

### .pacsave

Pokud uživatel změnil některý ze souborů jmenovaných v `backup`, pak bude k tomuto souboru přidána přípona `.pacsave` a zůstane v souborovém systému i poté, co bude odstraněn zbytek balíčku.

**Note:** Použití volby `-n` spolu s `pacman -R` způsobí kompletní odstranění *všech* souborů v zadaném balíčku. Žádné `.pacsave` soubory tedy vytvořeny nebudou.

### .pacorig

Když je při instalaci balíčku spatřen soubor (obvykle nějaká konfigurace v `/etc`), který nepatří žádnému nainstalovanému balíčku, ale je vypsán v poli `backup` pro momentálně zpracovávaný balíček, bude uložen s příponou `.pacorig` a nahrazen verzí z balíčku. To se obvykle stává, když je konfigurační soubor přesunut z jednoho balíčku do jiného. Pokud takový soubor není součástí pole `backup`, pacman oznámí konflikt souborů a ukončí svoji činnost.

**Note:** Jelikož `.pacorig` soubory vznikávají za zvláštních okolností, není pro jejich zpracování žádný jednotný postup. Pokud se o tomto případu ví, obvykle naleznete řešení tohoto konfliktu na [Arch News](https://www.archlinux.org/news/).

## Lokalizace *.pac* souborů

Arch Linux pro `.pacnew` soubory neposkytuje žádné oficiální nástroje. Budete je muset řešit sami; několik pomocných nástrojů je předvedeno v následující sekci. Pro ruční řešení budete nejprve muset tyto soubory nalézt. Při upgradu nebo odstraňování velkého počtu balíčků mohou být *.pac* soubory snadno přehlédnuty. Abyste zjistili, zda byly jakékoliv *.pac* vytvořeny:

Pro jednoduché hledání v místě, kde je uložena většina globálních konfigurací:

```
find /etc -name "*.pac*"

```

nebo na celém disku:

```
find / -name "*.pac*"

```

Případně pro jejich vyhledání použijte logy z pacmana:

```
egrep "pac(new|orig|save)" /var/log/pacman.log

```

Poznámka: z logu přímo nezjistíte, které z těchto souborů jsou momentálně ještě v souborovém systému a které již byly smazány.

## Nástroje pro soubory .pacnew

Jakmile máte všechny existující `.pacnew` soubory lokalizovány, můžete je vyřešit ručně pomocí běžných nástrojů pro slučování, např. [vimdiff (anglicky)](/index.php/Vim#Merging_Files_.28Vimdiff.29 "Vim"), ediff (součást [emacs (anglicky)](/index.php/Emacs#Using_Emacs_as_git_mergetool "Emacs")), meld (grafický nástroj pro Gnome) nebo Kompare (grafický nástroj pro KDE). Poté `.pacnew` soubory smažte.

V [repozitáři community](/index.php/AUR_-_u%C5%BEivatelsk%C3%BD_pr%C5%AFvodce_(%C4%8Cesky)#.5Bcommunity.5D "AUR - uživatelský průvodce (Česky)") a [uživatelském repozitáři (AUR)](/index.php/AUR_-_u%C5%BEivatelsk%C3%BD_pr%C5%AFvodce_(%C4%8Cesky)#Jak_na_bal.C3.AD.C4.8Dek_z_UNSUPPORTED "AUR - uživatelský průvodce (Česky)") je dostupných několik utilit, které poskytují různou úroveň automatizace těchto úkolů:

*   [Dotpac](/index.php/Dotpac "Dotpac") - Základní interaktivní skript s textovým rozhraním založeným na ncurses a užitečnou nápovědou. Žádné pomůcky pro ruční ani automatické slučování.
*   `pacdiff` - Velmi minimální a nezdokumentovaný konzolový skript. Je součástí balíčku [pacman](https://www.archlinux.org/packages/?name=pacman) v repozitáři community.
*   [pacdiffviewer](https://aur.archlinux.org/packages.php?ID=5863) - Plnohodnotný interaktivní konzolový skript se schopností automatického slučování. Je součástí balíčku [yaourt](/index.php/Yaourt_(%C4%8Cesky) "Yaourt (Česky)").
*   [diffpac](https://aur.archlinux.org/packages/diffpac/) - Samostatná náhražka za pacdiffviewer.

## Zdroje

*   Fóra Arch Linuxu: [Dealing With .pacnew Files (anglicky)](https://bbs.archlinux.org/viewtopic.php?id=53532)
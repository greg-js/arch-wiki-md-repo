Arch Linux je nezávisle vyvinutá komunitní distribuce GNU/Linuxu pro architektury [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64"), dost všestraná pro prakticky libovolné využití. Vývoj klade důraz na jednoduchost, minimalismus a eleganci kódu. Arch je instalován jako minimální základní systém a konfigurovaný uživatelem podle jejich vlastních potřeb a představ o ideálním prostředí. Volitelné závislosti balíčků nejsou automaticky instalovány, uživatel instaluje pouze to, co sám potřebuje, grafické konfigurační nástroje nejsou oficiálně poskytovány a většina systémové konfigurace probíhá na příkazová řádce a v textovém editoru. Arch je založen na rolling-release modelu a snaží se poskytovat vždy nejnovější stabilní verze většiny aplikací.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Historie](#Historie)
*   [2 Jednoduchost](#Jednoduchost)
*   [3 Modernost](#Modernost)
*   [4 Balíčkovací systém](#Balíčkovací_systém)
*   [5 Integrita balíčků](#Integrita_balíčků)
*   [6 Komunita](#Komunita)
*   [7 Shrnutí](#Shrnutí)

## Historie

Arch Linux začal vyvíjet kanadský programátor Judd Vinet. První verze, Arch Linux 0.1, vyšla 11\. března 2002\. Ačkoli je Arch kompletně nezávislý, čerpá inspiraci z jednoduchosti ostatních distribucí, včetně [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) a [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"). V roce 2007 odstoupil Judd Vinet z vedení projektu, aby se mohl věnovat ostatním zájmům, nahradil ho americký programátor Aaron Griffin, který vede projekt do dneška.

## Jednoduchost

Arch se drží své filozofie [The Arch Way](/index.php/The_Arch_Way_(%C4%8Cesky) "The Arch Way (Česky)"), jedná se o odlehčenou, flexibilní a jednoduchou distribuci. Při instalaci je poskytováno minimální prostředí (bez grafického rozhraní) kompilované pro architektury i686/x86-64: namísto odstraňování nepotřebných a nežádoucích balíčků má uživatel možnost stavět svůj systém na minimálním základu bez jakýchkoli preventivně zvolených výchozích nastavení. Díky filozofii návrhu a implementace Archu je jednoduché rozšiřovat a vytvářet libovolný typ systému, od minimalistického konzolového stroje až po mohutná funkcemi nabitá desktopová prostředí -- je to právě *uživatel* kdo rozhoduje o tom, jak jeho Arch systém bude vypadat.

## Modernost

Arch Linux se snaží poskytovat nejnovější stabilní vydání aplikací. Aktualizace jsou založeny na [rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") modelu, což umožňuje jednorázovou instalaci s postupnými aktualizacemi bez nutnosti neustále přeinstalovávat celý systém. Spuštěním jediného příkazu lze udržet Arch v aktuálním stavu s nejnovějšími verzemi všech aplikací.

Arch zahrnuje mnoho nových funkcí dostupných uživatelům GNU/Linuxu, včetně [systemd](/index.php/Systemd "Systemd") init systému, moderních souborových systémů (Ext2/3/4, Reiser, XFS, JFS, BTRFS), LVM2/EVMS, softwarového RAID, udev a initcpio (s [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) a také nejnovější dostupné verze linuxového jádra.

## Balíčkovací systém

Arch používá [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)"), což je snadno použitelný binární [správce balíků](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager"), který umožňuje aktualizaci celého systému pomocí jediného příkazu. Pacman je napsán v jazyce C a je od návrhu odlehčený, jednoduchý a velmi rychlý. Arch také poskytuje [Arch Build System](/index.php/Arch_Build_System_(%C4%8Cesky) "Arch Build System (Česky)"), s jehož pomocí lze jednoduše sestavovat a instalovat balíčky ze zdrojových kódů. ABS lze také synchronizovat pomocí jediného příkazu. Můžete si dokonce překompilovat celý systém pomocí jediného příkazu.

Arch podporuje architektury i686 a x86-64 v [oficiálních repozitářích](/index.php/Official_repositories_(%C4%8Cesky) "Official repositories (Česky)"), které poskytují několik tisíc vysoce kvalitních balíčků. Arch navíc povzbuzuje růst komunity tím, že nabízí [Arch User Repository](/index.php/Arch_User_Repository_(%C4%8Cesky) "Arch User Repository (Česky)"), který obsahuje tisíce uživatelských [PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)") skriptů na kompilaci a instalaci balíčků ze zdrojových kódů. Uživatelé také mohou jednoduše vytvořit a spravovat své vlastní repozitáře.

## Integrita balíčků

Arch poskytuje vanilla software bez záplat; balíčky jsou sestavovány přímo z [upstream](https://en.wikipedia.org/wiki/upstream_(software_development) zdrojových kódů, jak autor původně zamýšlel, aby byly distribuovány. Záplatování probíhá pouze v extrémních případech, aby se zabránilo závažnému rozbití balíčků v důsledku neshodujících se verzí, což se za použití rolling-release modelu může stát.

## Komunita

Komunita Arch Linuxu je velmi spolehlivá, živá a vlídná: všichni "Archisti" jsou povzbuzováni k zapojení se a přispění do distribuce, ať už ve formě pomoci s vývojem klíčového software, správy balíčků, hlášení nebo opravování [chyb](https://bugs.archlinux.org/), vylepšování [ArchWiki dokumentace](/index.php/Main_page_(%C4%8Cesky) "Main page (Česky)"), pomáhání ostatním uživatelům při řešení problémů nebo jen výměně názorů na [fóru](https://bbs.archlinux.org/), [emailových konferencích](https://mailman.archlinux.org/mailman/listinfo/), [IRC kanálech](/index.php/IRC_channels "IRC channels") nebo ve formě sdílení znalostí nebo dokonce vlastních aplikací. Arch Linux používají lidé na celé Zemi, existuje několik [mezinárodních komunit](/index.php/International_communities "International communities") nabízejících pomoc a poskytujících dokumentaci v mnoha jazycích.

Viz [Getting involved](/index.php/Getting_involved "Getting involved"), pokud se chcete stát aktivním členem komunity.

## Shrnutí

Arch Linux je všestranná a jednoduchá distribuce cílená na schopné uživatele GNU/Linuxu. Je působivé a jednoduché ji spravovat, což z ní dělá ideální distribuci pro servery a pracovní stanice. Pokud sdílíte tuto vizi jak by měla distribuce GNU/Linuxu vypadat, pak jste vítáni ji svobodně používat a zapojit se do komunity. Vítejte v Archu!